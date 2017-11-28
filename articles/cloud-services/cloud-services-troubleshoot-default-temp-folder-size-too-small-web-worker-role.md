---
title: "размер папки TEMP aaaDefault слишком мал для роли | Документы Microsoft"
description: "Роль облачной службы имеет ограниченный объем пространства для папки TEMP hello. Также приводятся советы о том, как tooavoid мало свободного места."
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
ms.openlocfilehash: 307dc20f3264e29d122a6616be0028d2ec1282c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a><span data-ttu-id="0e67d-104">Недостаточный размер стандартной папки TEMP для рабочей роли или веб-роли облачной службы</span><span class="sxs-lookup"><span data-stu-id="0e67d-104">Default TEMP folder size is too small on a cloud service web/worker role</span></span>
<span data-ttu-id="0e67d-105">временный каталог облачной службы рабочей или веб-роли не может превышать 100 МБ, что может привести к полной в определенный момент по умолчанию Hello.</span><span class="sxs-lookup"><span data-stu-id="0e67d-105">hello default temporary directory of a cloud service worker or web role has a maximum size of 100 MB, which may become full at some point.</span></span> <span data-ttu-id="0e67d-106">В этой статье описывается как tooavoid заканчивается место для hello временный каталог.</span><span class="sxs-lookup"><span data-stu-id="0e67d-106">This article describes how tooavoid running out of space for hello temporary directory.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a><span data-ttu-id="0e67d-107">Почему мне не хватает свободного места?</span><span class="sxs-lookup"><span data-stu-id="0e67d-107">Why do I run out of space?</span></span>
<span data-ttu-id="0e67d-108">Hello стандартных Windows переменных среды TEMP и TMP, доступных toocode, на котором выполняется в приложении.</span><span class="sxs-lookup"><span data-stu-id="0e67d-108">hello standard Windows environment variables TEMP and TMP are available toocode that is running in your application.</span></span> <span data-ttu-id="0e67d-109">TEMP и TMP точки tooa один каталог, который не может превышать 100 МБ.</span><span class="sxs-lookup"><span data-stu-id="0e67d-109">Both TEMP and TMP point tooa single directory that has a maximum size of 100 MB.</span></span> <span data-ttu-id="0e67d-110">Все данные, хранящиеся в нем не сохраняются между жизненного цикла hello hello облачной службы; Если hello экземпляров ролей в облачной службе перезапускаются, каталог hello очищается.</span><span class="sxs-lookup"><span data-stu-id="0e67d-110">Any data that is stored in this directory is not persisted across hello lifecycle of hello cloud service; if hello role instances in a cloud service are recycled, hello directory is cleaned.</span></span>

## <a name="suggestion-toofix-hello-problem"></a><span data-ttu-id="0e67d-111">Проблема hello toofix предложений</span><span class="sxs-lookup"><span data-stu-id="0e67d-111">Suggestion toofix hello problem</span></span>
<span data-ttu-id="0e67d-112">Реализуйте один из следующих альтернативных hello:</span><span class="sxs-lookup"><span data-stu-id="0e67d-112">Implement one of hello following alternatives:</span></span>

* <span data-ttu-id="0e67d-113">Настройте локальный ресурс хранилища и обращайтесь напрямую к нему, не используя TEMP или TMP.</span><span class="sxs-lookup"><span data-stu-id="0e67d-113">Configure a local storage resource, and access it directly instead of using TEMP or TMP.</span></span> <span data-ttu-id="0e67d-114">ресурс локального хранилища из кода, который выполняется в рамках приложение hello вызовов tooaccess [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) метод.</span><span class="sxs-lookup"><span data-stu-id="0e67d-114">tooaccess a local storage resource from code that is running within your application, call hello [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>
* <span data-ttu-id="0e67d-115">Настройка ресурсов локального хранилища и точки hello TEMP и TMP каталоги toopoint toohello путь hello локального ресурса хранилища.</span><span class="sxs-lookup"><span data-stu-id="0e67d-115">Configure a local storage resource, and point hello TEMP and TMP directories toopoint toohello path of hello local storage resource.</span></span> <span data-ttu-id="0e67d-116">Это изменение должно выполняться в рамках hello [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) метод.</span><span class="sxs-lookup"><span data-stu-id="0e67d-116">This modification should be performed within hello [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method.</span></span>

<span data-ttu-id="0e67d-117">Hello следующем примере кода показано, как toomodify hello целевые каталоги TEMP и TMP из метода OnStart hello:</span><span class="sxs-lookup"><span data-stu-id="0e67d-117">hello following code example shows how toomodify hello target directories for TEMP and TMP from within hello OnStart method:</span></span>

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // hello local resource declaration must have been added toothe
            // service definition file for hello role named WorkerRole1:
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

            // hello rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="0e67d-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0e67d-118">Next steps</span></span>
<span data-ttu-id="0e67d-119">Прочитайте блог, который описывает [как tooincrease hello размер hello временной папки Azure веб-роли ASP.NET](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span><span class="sxs-lookup"><span data-stu-id="0e67d-119">Read a blog that describes [How tooincrease hello size of hello Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span></span>

<span data-ttu-id="0e67d-120">Просмотрите дополнительные [статьи об устранении неполадок](/?tag=top-support-issue&product=cloud-services) в облачных службах.</span><span class="sxs-lookup"><span data-stu-id="0e67d-120">View more [troubleshooting articles](/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="0e67d-121">toolearn как выдает tootroubleshoot роль облачной службы с помощью диагностические данные Azure PaaS компьютера, просмотреть [серии публикаций в блоге Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="0e67d-121">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, view [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
