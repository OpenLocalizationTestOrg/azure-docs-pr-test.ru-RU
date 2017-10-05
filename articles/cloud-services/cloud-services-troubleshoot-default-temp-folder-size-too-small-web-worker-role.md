---
title: "Недостаточный размер папки TEMP по умолчанию для роли | Документация Майкрософт"
description: "Роль облачной службы располагает ограниченным объемом места в папке TEMP. Эта статья содержит советы о том, как предотвратить нехватку места."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 9f2af8dd-2012-4b36-9dd5-19bf6a67e47d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 577d090a009eb2331b401273257c7cc7c1eea772
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a><span data-ttu-id="17f6a-104">Недостаточный размер стандартной папки TEMP для рабочей роли или веб-роли облачной службы</span><span class="sxs-lookup"><span data-stu-id="17f6a-104">Default TEMP folder size is too small on a cloud service web/worker role</span></span>
<span data-ttu-id="17f6a-105">Максимальный размер временного каталога по умолчанию рабочей роли или веб-роли облачной службы составляет 100 МБ, чего может оказаться недостаточно в определенный момент.</span><span class="sxs-lookup"><span data-stu-id="17f6a-105">The default temporary directory of a cloud service worker or web role has a maximum size of 100 MB, which may become full at some point.</span></span> <span data-ttu-id="17f6a-106">В этой статье описано, как можно предотвратить нехватку места для временного каталога.</span><span class="sxs-lookup"><span data-stu-id="17f6a-106">This article describes how to avoid running out of space for the temporary directory.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a><span data-ttu-id="17f6a-107">Почему мне не хватает свободного места?</span><span class="sxs-lookup"><span data-stu-id="17f6a-107">Why do I run out of space?</span></span>
<span data-ttu-id="17f6a-108">В выполняемом в вашей программе коде используются стандартные переменные среды Windows: TEMP и TMP.</span><span class="sxs-lookup"><span data-stu-id="17f6a-108">The standard Windows environment variables TEMP and TMP are available to code that is running in your application.</span></span> <span data-ttu-id="17f6a-109">Переменные TEMP и TMP указывают на один каталог с максимальным размером в 100 МБ.</span><span class="sxs-lookup"><span data-stu-id="17f6a-109">Both TEMP and TMP point to a single directory that has a maximum size of 100 MB.</span></span> <span data-ttu-id="17f6a-110">Данные, хранящиеся в этом каталоге, не хранятся на протяжении жизненного цикла облачной службы; если экземпляры роли в облачной службе перезапускаются, этот каталог очищается.</span><span class="sxs-lookup"><span data-stu-id="17f6a-110">Any data that is stored in this directory is not persisted across the lifecycle of the cloud service; if the role instances in a cloud service are recycled, the directory is cleaned.</span></span>

## <a name="suggestion-to-fix-the-problem"></a><span data-ttu-id="17f6a-111">Предложение по устранению проблемы</span><span class="sxs-lookup"><span data-stu-id="17f6a-111">Suggestion to fix the problem</span></span>
<span data-ttu-id="17f6a-112">Примените один из следующих альтернативных способов.</span><span class="sxs-lookup"><span data-stu-id="17f6a-112">Implement one of the following alternatives:</span></span>

* <span data-ttu-id="17f6a-113">Настройте локальный ресурс хранилища и обращайтесь напрямую к нему, не используя TEMP или TMP.</span><span class="sxs-lookup"><span data-stu-id="17f6a-113">Configure a local storage resource, and access it directly instead of using TEMP or TMP.</span></span> <span data-ttu-id="17f6a-114">Чтобы получить доступ к локальному ресурсу хранилища из кода, запущенного в программе, вызовите метод [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) .</span><span class="sxs-lookup"><span data-stu-id="17f6a-114">To access a local storage resource from code that is running within your application, call the [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>
* <span data-ttu-id="17f6a-115">Настройте локальный ресурс хранилища и задайте каталоги TEMP и TMP, чтобы указать путь к этому локальному ресурсу хранилища.</span><span class="sxs-lookup"><span data-stu-id="17f6a-115">Configure a local storage resource, and point the TEMP and TMP directories to point to the path of the local storage resource.</span></span> <span data-ttu-id="17f6a-116">Это изменение следует выполнить внутри метода [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) .</span><span class="sxs-lookup"><span data-stu-id="17f6a-116">This modification should be performed within the [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method.</span></span>

<span data-ttu-id="17f6a-117">В следующем примере кода показано, как изменить целевые каталоги TEMP и TMP из метода OnStart:</span><span class="sxs-lookup"><span data-stu-id="17f6a-117">The following code example shows how to modify the target directories for TEMP and TMP from within the OnStart method:</span></span>

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // The local resource declaration must have been added to the
            // service definition file for the role named WorkerRole1:
            //
            // <LocalResources>
            //    <LocalStorage name="CustomTempLocalStore"
            //                  cleanOnRoleRecycle="false"
            //                  sizeInMB="1024" />
            // </LocalResources>

            string customTempLocalResourcePath =
            RoleEnvironment.GetLocalResource("CustomTempLocalStore").RootPath;
            Environment.SetEnvironmentVariable("TMP", customTempLocalResourcePath);
            Environment.SetEnvironmentVariable("TEMP", customTempLocalResourcePath);

            // The rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="17f6a-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="17f6a-118">Next steps</span></span>
<span data-ttu-id="17f6a-119">См. блог, в котором описывается, [как увеличить размер временной папки ASP.NET веб-ролей Azure](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span><span class="sxs-lookup"><span data-stu-id="17f6a-119">Read a blog that describes [How to increase the size of the Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span></span>

<span data-ttu-id="17f6a-120">Просмотрите дополнительные [статьи об устранении неполадок](/?tag=top-support-issue&product=cloud-services) в облачных службах.</span><span class="sxs-lookup"><span data-stu-id="17f6a-120">View more [troubleshooting articles](/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="17f6a-121">Чтобы узнать, как устранять неполадки ролей облачной службы с помощью диагностических данных компьютеров Azure PaaS, изучите [серию статей в блоге Кевина Уильямсона](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="17f6a-121">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, view [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
