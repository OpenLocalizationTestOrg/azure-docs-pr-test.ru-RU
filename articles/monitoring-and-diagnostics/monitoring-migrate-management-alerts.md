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
# <a name="migrate-azure-alerts-on-management-events-tooactivity-log-alerts"></a><span data-ttu-id="bf84a-104">Оповещения Azure управления предупреждения о событиях tooActivity журнала миграции</span><span class="sxs-lookup"><span data-stu-id="bf84a-104">Migrate Azure alerts on management events tooActivity Log alerts</span></span>


> [!WARNING]
> <span data-ttu-id="bf84a-105">Оповещения о событиях управления будут отключены в течение или после 1 октября.</span><span class="sxs-lookup"><span data-stu-id="bf84a-105">Alerts on management events will be turned off on or after October 1.</span></span> <span data-ttu-id="bf84a-106">Используйте направлениях hello ниже toounderstand, если у вас есть эти предупреждения и перенести их в этом случае.</span><span class="sxs-lookup"><span data-stu-id="bf84a-106">Use hello directions below toounderstand if you have these alerts and migrate them if so.</span></span>
>
> 

## <a name="what-is-changing"></a><span data-ttu-id="bf84a-107">Изменения</span><span class="sxs-lookup"><span data-stu-id="bf84a-107">What is changing</span></span>

<span data-ttu-id="bf84a-108">Монитор Azure (прежнее название — аналитики Azure) предлагается toocreate возможность оповещение, которое запускается из событий управления и созданных уведомлений tooa веб-перехватчика URL-адрес или по электронной почте адресов.</span><span class="sxs-lookup"><span data-stu-id="bf84a-108">Azure Monitor (formerly Azure Insights) offered a capability toocreate an alert that triggered off of management events and generated notifications tooa webhook URL or email addresses.</span></span> <span data-ttu-id="bf84a-109">Эти оповещения можно было создать одним из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="bf84a-109">You may have created one of these alerts any of these ways:</span></span>
* <span data-ttu-id="bf84a-110">Hello портал Azure для определенных типов ресурсов, в разделе мониторинг -> оповещения -> Добавить оповещения, где «Предупреждение на» установлено слишком «События»</span><span class="sxs-lookup"><span data-stu-id="bf84a-110">In hello Azure portal for certain resource types, under Monitoring -> Alerts -> Add Alert, where “Alert on” is set too“Events”</span></span>
* <span data-ttu-id="bf84a-111">Выполнение командлета PowerShell Add-AzureRmLogAlertRule hello</span><span class="sxs-lookup"><span data-stu-id="bf84a-111">By running hello Add-AzureRmLogAlertRule PowerShell cmdlet</span></span>
* <span data-ttu-id="bf84a-112">С помощью непосредственно [hello предупреждения API REST](http://docs.microsoft.com/rest/api/monitor/alertrules) с odata.type = «ManagementEventRuleCondition» и dataSource.odata.type = «RuleManagementEventDataSource»</span><span class="sxs-lookup"><span data-stu-id="bf84a-112">By directly using [hello alert REST API](http://docs.microsoft.com/rest/api/monitor/alertrules) with odata.type = “ManagementEventRuleCondition” and dataSource.odata.type = “RuleManagementEventDataSource”</span></span>
 
<span data-ttu-id="bf84a-113">Hello следующий сценарий PowerShell возвращает список всех оповещений о событиях управления, имеющихся в подписке, а также задать для каждого предупреждения условий hello.</span><span class="sxs-lookup"><span data-stu-id="bf84a-113">hello following PowerShell script returns a list of all alerts on management events that you have in your subscription, as well as hello conditions set on each alert.</span></span>

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

<span data-ttu-id="bf84a-114">При наличии без предупреждений о событиях управления выше командлет PowerShell hello выдаст ряд предупреждающих сообщений, похожее на следующее:</span><span class="sxs-lookup"><span data-stu-id="bf84a-114">If you have no alerts on management events, hello PowerShell cmdlet above will output a series of warning messages like this one:</span></span>

`WARNING: hello output of this cmdlet will be flattened, i.e. elimination of hello properties field, in a future release tooimprove hello user experience.`

<span data-ttu-id="bf84a-115">Эти предупреждения можно игнорировать.</span><span class="sxs-lookup"><span data-stu-id="bf84a-115">These warning messages can be ignored.</span></span> <span data-ttu-id="bf84a-116">При наличии предупреждений о событиях управления, hello выходные данные командлета PowerShell будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="bf84a-116">If you do have alerts on management events, hello output of this PowerShell cmdlet will look like this:</span></span>

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

<span data-ttu-id="bf84a-117">Пунктирная линия отделяется каждого предупреждения и сведения включают идентификатор ресурса hello предупреждение hello и конкретного правила hello отслеживается.</span><span class="sxs-lookup"><span data-stu-id="bf84a-117">Each alert is separated by a dashed line and details include hello resource ID of hello alert and hello specific rule being monitored.</span></span>

<span data-ttu-id="bf84a-118">Эта функция заменена слишком[предупреждения журнала действий Azure монитор](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="bf84a-118">This functionality has been transitioned too[Azure Monitor Activity Log Alerts](monitoring-activity-log-alerts.md).</span></span> <span data-ttu-id="bf84a-119">Эти новые оповещения позволяют tooset условие в журнал событий и получать уведомление, когда новое событие соответствует условию hello.</span><span class="sxs-lookup"><span data-stu-id="bf84a-119">These new alerts enable you tooset a condition on Activity Log events and receive a notification when a new event matches hello condition.</span></span> <span data-ttu-id="bf84a-120">Они также предоставляют ряд усовершенствований по сравнению с оповещениями о событиях управления.</span><span class="sxs-lookup"><span data-stu-id="bf84a-120">They also offer several improvements from alerts on management events:</span></span>
* <span data-ttu-id="bf84a-121">Вы можете повторно использовать группе получателей уведомлений («действия») для большого числа предупреждений с помощью [группы действий](monitoring-action-groups.md), Уменьшение сложности hello изменения, кто должен получить оповещение.</span><span class="sxs-lookup"><span data-stu-id="bf84a-121">You can reuse your group of notification recipients (“actions”) across many alerts using [Action Groups](monitoring-action-groups.md), reducing hello complexity of changing who should receive an alert.</span></span>
* <span data-ttu-id="bf84a-122">Вы можете получать уведомления непосредственно на телефон в виде SMS с помощью группы действий.</span><span class="sxs-lookup"><span data-stu-id="bf84a-122">You can receive a notification directly on your phone using SMS with Action Groups.</span></span>
* <span data-ttu-id="bf84a-123">Вы можете [создавать оповещения журнала действий с помощью шаблонов Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="bf84a-123">You can [create Activity Log Alerts with Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
* <span data-ttu-id="bf84a-124">Можно создать условия с большую гибкость и сложность toomeet конкретных потребностей.</span><span class="sxs-lookup"><span data-stu-id="bf84a-124">You can create conditions with greater flexibility and complexity toomeet your specific needs.</span></span>
* <span data-ttu-id="bf84a-125">Уведомления доставляются быстрее.</span><span class="sxs-lookup"><span data-stu-id="bf84a-125">Notifications are delivered more quickly.</span></span>
 
## <a name="how-toomigrate"></a><span data-ttu-id="bf84a-126">Как toomigrate</span><span class="sxs-lookup"><span data-stu-id="bf84a-126">How toomigrate</span></span>
 
<span data-ttu-id="bf84a-127">toocreate создать действие журнала предупреждения, вы можете сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="bf84a-127">toocreate a new Activity Log Alert, you can either:</span></span>
* <span data-ttu-id="bf84a-128">Выполните [нашем руководстве на как toocreate оповещения в hello портал Azure](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="bf84a-128">Follow [our guide on how toocreate an alert in hello Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="bf84a-129">Узнайте, каким образом слишком[создать предупреждение, с помощью шаблона диспетчера ресурсов](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="bf84a-129">Learn how too[create an alert using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
 
<span data-ttu-id="bf84a-130">Предупреждения о событиях управления, которые ранее были созданы не будут автоматически перенесенных tooActivity предупреждения журнала.</span><span class="sxs-lookup"><span data-stu-id="bf84a-130">Alerts on management events that you have previously created will not be automatically migrated tooActivity Log Alerts.</span></span> <span data-ttu-id="bf84a-131">Необходимо toouse hello, предшествующие предупреждения hello toolist сценарий PowerShell на события управления сейчас настроили и вручную повторно создаются как предупреждения журнала действий.</span><span class="sxs-lookup"><span data-stu-id="bf84a-131">You need toouse hello preceding PowerShell script toolist hello alerts on management events that you currently have configured and manually recreate them as Activity Log Alerts.</span></span> <span data-ttu-id="bf84a-132">Это необходимо сделать до 1 октября, после чего оповещения о событиях управления больше не будут отображаться в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="bf84a-132">This must be done before October 1, after which alerts on management events will no longer be visible in your Azure subscription.</span></span> <span data-ttu-id="bf84a-133">Другие типы оповещений Azure, включая оповещения о метриках Azure Monitor, оповещения Application Insights и оповещения Log Analytics, это изменение не затрагивает.</span><span class="sxs-lookup"><span data-stu-id="bf84a-133">Other types of Azure alerts, including Azure Monitor metric alerts, Application Insights alerts, and Log Analytics alerts are unaffected by this change.</span></span> <span data-ttu-id="bf84a-134">Если у вас возникли вопросы, учет в hello комментарии ниже.</span><span class="sxs-lookup"><span data-stu-id="bf84a-134">If you have any questions, post in hello comments below.</span></span>


## <a name="next-steps"></a><span data-ttu-id="bf84a-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bf84a-135">Next steps</span></span>

* <span data-ttu-id="bf84a-136">Узнайте больше о [журнале действий](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="bf84a-136">Learn more about [Activity Log](monitoring-overview-activity-logs.md)</span></span>
* <span data-ttu-id="bf84a-137">Настройте [оповещения журнала действий на портале Azure](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="bf84a-137">Configure [Activity Log Alerts via Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="bf84a-138">Настройте [оповещения журнала действий с помощью Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="bf84a-138">Configure [Activity Log Alerts via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
* <span data-ttu-id="bf84a-139">Просмотрите hello [схема предупреждения веб-перехватчика журнала активности](monitoring-activity-log-alerts-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="bf84a-139">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)</span></span>
* <span data-ttu-id="bf84a-140">Узнайте больше об [уведомлениях службы](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="bf84a-140">Learn more about [Service Notifications](monitoring-service-notifications.md)</span></span>
* <span data-ttu-id="bf84a-141">Узнайте больше о [группах действий](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="bf84a-141">Learn more about [Action Groups](monitoring-action-groups.md)</span></span>
