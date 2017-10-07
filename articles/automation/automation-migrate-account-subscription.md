---
title: "aaaMigrate учетной записи автоматизации и ресурсам | Документы Microsoft"
description: "В этой статье описывается, как toomove автоматизации учетной записи в службе автоматизации Azure и связанных ресурсов из tooanother одна подписка."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9c2db4a2-f324-48dc-8ce7-3343bf7230d5
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte
ms.openlocfilehash: 201c9091cd2d78d7ea407c1e5fb27f366bb4fa8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-automation-account-and-resources"></a>Перенос учетной записи и ресурсов службы автоматизации
Для учетных записей автоматизации и его связанные ресурсы (т. е. ресурсы, модули Runbook, модули, т. д.), которые вы создали в hello портал Azure и хотите toomigrate из одного ресурса группы tooanother или из tooanother одна подписка для этого можно легко с Hello [перемещение ресурсов](../azure-resource-manager/resource-group-move-resources.md) компонент, доступный в hello портал Azure. Тем не менее, прежде чем выполнять это действие, необходимо просмотреть следующие hello [контрольный список до перемещения ресурсов](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) и Кроме того, список hello ниже определенного tooAutomation.   

1. Hello назначения подписку или группу ресурсов должен быть в одном регионе, что источник hello.  Это означает, что учетные записи службы автоматизации нельзя перемещать между регионами.
2. При перемещении ресурсов (например, модули Runbook, заданий, т. д.), исходная группа hello и целевая группа hello блокируются hello время выполнения операции hello. Записи и удаления операций блокируются на группах hello до завершения перемещения hello.  
3. Модулей Runbook или переменные, которые ссылаются идентификатор ресурса или подписки из существующей подписки hello потребуется toobe обновлена после завершения миграции.   

> [!NOTE]
> Данная функция не поддерживает перемещение классических ресурсов службы автоматизации.
>
>

## <a name="toomove-hello-automation-account-using-hello-portal"></a>Учетная запись службы автоматизации с помощью портала hello hello toomove
1. Ваша учетная запись автоматизации щелкните **переместить** hello верхней части колонки hello.<br> ![Параметр "Переместить"](media/automation-migrate-account-subscription/automation-menu-move.png)<br>
2. На hello **перемещение ресурсов** колонки, обратите внимание, что она представляет tooboth связанные ресурсы, ваша учетная запись автоматизации и вашей группы ресурсов.  Выберите hello **подписки** и **группы ресурсов** из раскрывающихся списков hello или hello выберите параметр **создать новую группу ресурсов** и введите новое имя группы ресурсов в поле Hello.  
3. Просмотрите и выберите hello флажок tooacknowledge вы *понять средства и сценарии, будет необходимости обновить toobe toouse новые идентификаторы ресурсов после перемещения ресурсов* и нажмите кнопку **ОК**.<br> ![Колонка "Перемещение ресурсов"](media/automation-migrate-account-subscription/automation-move-resources-blade.png)<br>   

Это действие займет несколько минут toocomplete.  В разделе **Уведомления** будет показано состояние каждого выполняемого действия — проверки, переноса и т. д., после чего отобразится сообщение о завершении операции.     

## <a name="toomove-hello-automation-account-using-powershell"></a>toomove hello учетной записи автоматизации с помощью PowerShell
toomove существующую группу ресурсов tooanother ресурсов автоматизации или подписку, используйте hello **Get-AzureRmResource** командлет tooget hello конкретных учетная запись службы автоматизации и затем **Move-AzureRmResource** Переместите hello tooperform командлета.

Hello первом примере показано, как toomove автоматизации учетной записи tooa новую группу ресурсов.

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

После выполнения hello выше примере можно запрашиваемые tooverify требуется tooperform это действие.  После нажатия кнопки **Да** и разрешить Здравствуйте tooproceed скрипт, пользователь не будет получать уведомления при выполнении миграции hello.  

toomove tooa новую подписку, добавьте значение hello *DestinationSubscriptionId* параметра.

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

Как и в предыдущем примере hello будет запрашиваемые tooconfirm hello перемещения.  

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о перемещения группы ресурсов toonew ресурсов или подписки см. в разделе [переместить группу ресурсов toonew ресурсов или подписку](../azure-resource-manager/resource-group-move-resources.md)
* Дополнительные сведения об элементе управления доступом на основе ролей в службе автоматизации Azure дополнительную информацию слишком[управления доступом на основе ролей в службе автоматизации Azure](automation-role-based-access-control.md).
* в разделе toolearn о командлетах PowerShell для управления подпиской, [с помощью Azure PowerShell с помощью диспетчера ресурсов](../azure-resource-manager/powershell-azure-resource-manager.md)
* toolearn портала возможности для управления подпиской, в разделе [использование ресурсов toomanage портала Azure hello](../azure-resource-manager/resource-group-portal.md).
