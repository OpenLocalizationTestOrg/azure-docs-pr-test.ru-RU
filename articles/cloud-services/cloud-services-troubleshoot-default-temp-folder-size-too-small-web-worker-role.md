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
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a>Недостаточный размер стандартной папки TEMP для рабочей роли или веб-роли облачной службы
временный каталог облачной службы рабочей или веб-роли не может превышать 100 МБ, что может привести к полной в определенный момент по умолчанию Hello. В этой статье описывается как tooavoid заканчивается место для hello временный каталог.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a>Почему мне не хватает свободного места?
Hello стандартных Windows переменных среды TEMP и TMP, доступных toocode, на котором выполняется в приложении. TEMP и TMP точки tooa один каталог, который не может превышать 100 МБ. Все данные, хранящиеся в нем не сохраняются между жизненного цикла hello hello облачной службы; Если hello экземпляров ролей в облачной службе перезапускаются, каталог hello очищается.

## <a name="suggestion-toofix-hello-problem"></a>Проблема hello toofix предложений
Реализуйте один из следующих альтернативных hello:

* Настройте локальный ресурс хранилища и обращайтесь напрямую к нему, не используя TEMP или TMP. ресурс локального хранилища из кода, который выполняется в рамках приложение hello вызовов tooaccess [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) метод.
* Настройка ресурсов локального хранилища и точки hello TEMP и TMP каталоги toopoint toohello путь hello локального ресурса хранилища. Это изменение должно выполняться в рамках hello [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) метод.

Hello следующем примере кода показано, как toomodify hello целевые каталоги TEMP и TMP из метода OnStart hello:

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

## <a name="next-steps"></a>Дальнейшие действия
Прочитайте блог, который описывает [как tooincrease hello размер hello временной папки Azure веб-роли ASP.NET](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).

Просмотрите дополнительные [статьи об устранении неполадок](/?tag=top-support-issue&product=cloud-services) в облачных службах.

toolearn как выдает tootroubleshoot роль облачной службы с помощью диагностические данные Azure PaaS компьютера, просмотреть [серии публикаций в блоге Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
