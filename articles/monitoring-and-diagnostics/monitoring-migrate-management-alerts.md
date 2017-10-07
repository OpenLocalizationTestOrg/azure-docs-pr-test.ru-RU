---
title: "aaaMigrate Azure предупреждениями на события управления tooActivity предупреждения журнала | Документы Microsoft"
description: "Оповещения о событиях управления будут удалены 1 октября. Подготовьтесь к этому, перенеся существующие оповещения."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: johnkem
ms.openlocfilehash: e00bc4f0bad4e8f97443310770c333d250e343ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-alerts-on-management-events-tooactivity-log-alerts"></a>Оповещения Azure управления предупреждения о событиях tooActivity журнала миграции


> [!WARNING]
> Оповещения о событиях управления будут отключены в течение или после 1 октября. Используйте направлениях hello ниже toounderstand, если у вас есть эти предупреждения и перенести их в этом случае.
>
> 

## <a name="what-is-changing"></a>Изменения

Монитор Azure (прежнее название — аналитики Azure) предлагается toocreate возможность оповещение, которое запускается из событий управления и созданных уведомлений tooa веб-перехватчика URL-адрес или по электронной почте адресов. Эти оповещения можно было создать одним из следующих способов:
* Hello портал Azure для определенных типов ресурсов, в разделе мониторинг -> оповещения -> Добавить оповещения, где «Предупреждение на» установлено слишком «События»
* Выполнение командлета PowerShell Add-AzureRmLogAlertRule hello
* С помощью непосредственно [hello предупреждения API REST](http://docs.microsoft.com/rest/api/monitor/alertrules) с odata.type = «ManagementEventRuleCondition» и dataSource.odata.type = «RuleManagementEventDataSource»
 
Hello следующий сценарий PowerShell возвращает список всех оповещений о событиях управления, имеющихся в подписке, а также задать для каждого предупреждения условий hello.

```powershell
Login-AzureRmAccount
$alerts = $null
foreach ($rg in Get-AzureRmResourceGroup ) {
  $alerts += Get-AzureRmAlertRule -ResourceGroup $rg.ResourceGroupName
}
foreach ($alert in $alerts) {
  if($alert.Properties.Condition.DataSource.GetType().Name.Equals("RuleManagementEventDataSource")) {
    "Alert Name: " + $alert.Name
    "Alert Resource ID: " + $alert.Id
    "Alert conditions:"
    $alert.Properties.Condition.DataSource
    "---------------------------------"
  }
} 
```

При наличии без предупреждений о событиях управления выше командлет PowerShell hello выдаст ряд предупреждающих сообщений, похожее на следующее:

`WARNING: hello output of this cmdlet will be flattened, i.e. elimination of hello properties field, in a future release tooimprove hello user experience.`

Эти предупреждения можно игнорировать. При наличии предупреждений о событиях управления, hello выходные данные командлета PowerShell будет выглядеть следующим образом:

```
Alert Name: webhookEvent1
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/webhookEvent1
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : microsoft.web/sites/start/action
ResourceGroupName    : 
ResourceProviderName : 
Status               : succeeded
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Web/sites/samplealertapp

---------------------------------
Alert Name: someclilogalert
Alert Resource ID: /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/microsoft.insights/alertrules/someclilogalert
Alert conditions:

EventName            : 
EventSource          : 
Level                : 
OperationName        : Start
ResourceGroupName    : 
ResourceProviderName : 
Status               : 
SubStatus            : 
Claims               : Microsoft.Azure.Management.Monitor.Management.Models.RuleManagementEventClaimsDataSource
ResourceUri          : /subscriptions/<subscription-id>/resourceGroups/<resourcegroup-name>/providers/Microsoft.Compute/virtualMachines/Seaofclouds

---------------------------------
```

Пунктирная линия отделяется каждого предупреждения и сведения включают идентификатор ресурса hello предупреждение hello и конкретного правила hello отслеживается.

Эта функция заменена слишком[предупреждения журнала действий Azure монитор](monitoring-activity-log-alerts.md). Эти новые оповещения позволяют tooset условие в журнал событий и получать уведомление, когда новое событие соответствует условию hello. Они также предоставляют ряд усовершенствований по сравнению с оповещениями о событиях управления.
* Вы можете повторно использовать группе получателей уведомлений («действия») для большого числа предупреждений с помощью [группы действий](monitoring-action-groups.md), Уменьшение сложности hello изменения, кто должен получить оповещение.
* Вы можете получать уведомления непосредственно на телефон в виде SMS с помощью группы действий.
* Вы можете [создавать оповещения журнала действий с помощью шаблонов Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).
* Можно создать условия с большую гибкость и сложность toomeet конкретных потребностей.
* Уведомления доставляются быстрее.
 
## <a name="how-toomigrate"></a>Как toomigrate
 
toocreate создать действие журнала предупреждения, вы можете сделать следующее.
* Выполните [нашем руководстве на как toocreate оповещения в hello портал Azure](monitoring-activity-log-alerts.md)
* Узнайте, каким образом слишком[создать предупреждение, с помощью шаблона диспетчера ресурсов](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
 
Предупреждения о событиях управления, которые ранее были созданы не будут автоматически перенесенных tooActivity предупреждения журнала. Необходимо toouse hello, предшествующие предупреждения hello toolist сценарий PowerShell на события управления сейчас настроили и вручную повторно создаются как предупреждения журнала действий. Это необходимо сделать до 1 октября, после чего оповещения о событиях управления больше не будут отображаться в вашей подписке Azure. Другие типы оповещений Azure, включая оповещения о метриках Azure Monitor, оповещения Application Insights и оповещения Log Analytics, это изменение не затрагивает. Если у вас возникли вопросы, учет в hello комментарии ниже.


## <a name="next-steps"></a>Дальнейшие действия

* Узнайте больше о [журнале действий](monitoring-overview-activity-logs.md).
* Настройте [оповещения журнала действий на портале Azure](monitoring-activity-log-alerts.md).
* Настройте [оповещения журнала действий с помощью Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).
* Просмотрите hello [схема предупреждения веб-перехватчика журнала активности](monitoring-activity-log-alerts-webhook.md)
* Узнайте больше об [уведомлениях службы](monitoring-service-notifications.md).
* Узнайте больше о [группах действий](monitoring-action-groups.md).
