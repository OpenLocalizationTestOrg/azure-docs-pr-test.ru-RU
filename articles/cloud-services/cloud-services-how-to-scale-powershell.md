---
title: "aaaScale облачной службы Azure в Windows PowerShell | Документы Microsoft"
description: "(классические) Узнайте, как toouse PowerShell tooscale веб-роли или рабочей роли или уменьшить в Azure."
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: ee37dd8c-6714-4c61-adb8-03d6bbf76c9a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: mmccrory
ms.openlocfilehash: cfac6660e84f8ae24e4e9bdd5bf2016fb9cd7045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-a-cloud-service-in-powershell"></a>Как tooscale облачной службы в PowerShell

Можно использовать Windows PowerShell tooscale веб-роли или рабочей роли in или out, добавив или удалив экземпляры.  

## <a name="log-in-tooazure"></a>Войдите в tooAzure

Прежде чем выполнять какие-либо операции с подпиской с помощью PowerShell, вы должны войти в систему.

```powershell
Add-AzureAccount
```

Если у вас несколько подписок, связанных с учетной записью, может потребоваться toochange hello текущей подписки в зависимости от того, где находится облачной службы. toocheck hello текущей подписке запуска:

```powershell
Get-AzureSubscription -Current
```

Если вам требуется toochange hello текущую подписку, выполните:

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-hello-current-instance-count-for-your-role"></a>Проверьте hello текущее количество экземпляров для роли

Выполните toocheck hello вашей роли в текущем состоянии.

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

Следует вернуть сведения о роли hello, включая его текущей операционной системы версии и число экземпляров. В этом случае имеется один экземпляр роли hello.

![Сведения о роли hello](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-hello-role-by-adding-more-instances"></a>Расширение роли hello, добавив дополнительные экземпляры

tooscale какая-то роль hello проход требуемого числа экземпляров как hello **число** toohello параметр **AzureRole набор** командлета:

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

блоки командлет Hello моментально при новые экземпляры hello подготавливаются и запущен. В течение этого времени, при открытии нового окна PowerShell и вызовите **Get-AzureRole** как показано выше, вы увидите hello. количество новых целевой экземпляр. И если проверить состояние роли hello hello портала вы увидите новый экземпляр hello запуска:

![Запуск экземпляра виртуальной машины на портале](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

После запуска экземпляров новый hello hello командлет возвращает успешно:

![Успешное увеличение числа экземпляров роли](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-hello-role-by-removing-instances"></a>Масштабировать, удалив экземпляры роли hello

Можно масштабировать в роли путем удаления экземпляров hello таким же образом. Набор hello **число** параметр на **AzureRole набор** toohello число экземпляров требуется toohave после масштабирования hello в операции.

## <a name="next-steps"></a>Дальнейшие действия

Не является автоматически масштабировать возможных tooconfigure для облачных служб из PowerShell. toodo, в разделе [облачную службу, как масштабировать tooauto](cloud-services-how-to-scale-portal.md).
