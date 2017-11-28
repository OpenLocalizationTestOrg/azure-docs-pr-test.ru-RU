---
title: "Примеры для быстрого запуска Azure Monitor с помощью PowerShell. | Документация Майкрософт"
description: "Используйте PowerShell для доступа к функциям Azure Monitor, например автоматическому масштабированию, оповещениям, объектам webhook и поиску в журналах действий."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c0761814-7148-4ab5-8c27-a2c9fa4cfef5
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 48f064884c2a6d0a55cc58a44169ed03c62de46d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="2647a-104">Примеры для быстрого запуска Azure Monitor с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="2647a-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="2647a-105">В этой статье показаны примеры команд PowerShell, с помощью которых можно быстро получить доступ к функциям Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="2647a-105">This article shows you sample PowerShell commands to help you access Azure Monitor features.</span></span> <span data-ttu-id="2647a-106">Azure Monitor позволяет выполнять автомасштабирование облачных служб, виртуальных машин и веб-приложений, отправлять оповещения и осуществлять вызов URL-адресов на основе значений настроенных данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="2647a-106">Azure Monitor allows you to AutoScale Cloud Services, Virtual Machines, and Web Apps and to send alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="2647a-107">Azure Monitor — это новое название для Azure Insights, актуальное с 25 сентября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="2647a-107">Azure Monitor is the new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="2647a-108">При этом пространства имен и соответствующие команды будут по-прежнему содержать фрагмент старого названия (insights).</span><span class="sxs-lookup"><span data-stu-id="2647a-108">However, the namespaces and thus the following commands still contain the "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="2647a-109">Настройка PowerShell</span><span class="sxs-lookup"><span data-stu-id="2647a-109">Set up PowerShell</span></span>
<span data-ttu-id="2647a-110">Если вы этого еще не сделали, настройте PowerShell для выполнения на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="2647a-110">If you haven't already, set up PowerShell to run on your computer.</span></span> <span data-ttu-id="2647a-111">Дополнительные сведения см. в разделе [Общие сведения об Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2647a-111">For more information, see [How to Install and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="2647a-112">Примеры в этой статье</span><span class="sxs-lookup"><span data-stu-id="2647a-112">Examples in this article</span></span>
<span data-ttu-id="2647a-113">Примеры в статье демонстрируют, как можно использовать командлеты Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="2647a-113">The examples in the article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="2647a-114">Можно также просмотреть полный список командлетов PowerShell (для мониторинга) в документации [Azure Monitor Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span><span class="sxs-lookup"><span data-stu-id="2647a-114">You can also review the entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="2647a-115">Вход в систему и использование подписок</span><span class="sxs-lookup"><span data-stu-id="2647a-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="2647a-116">Сначала войдите в свою подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="2647a-116">First, log in to your Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="2647a-117">Для этого необходимо войти в систему.</span><span class="sxs-lookup"><span data-stu-id="2647a-117">This requires you to sign in.</span></span> <span data-ttu-id="2647a-118">После этого вы увидите свою учетную запись, идентификатор клиента и идентификатор подписки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2647a-118">Once you do, your Account, TenantID and default Subscription ID are displayed.</span></span> <span data-ttu-id="2647a-119">Все командлеты Azure будут работать в контексте подписки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2647a-119">All the Azure cmdlets work in the context of your default subscription.</span></span> <span data-ttu-id="2647a-120">Чтобы просмотреть список доступных вам подписок, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="2647a-120">To view the list of subscriptions you have access to, use the following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="2647a-121">Чтобы сменить рабочий контекст на другую подписку, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="2647a-121">To change your working context to a different subscription, use the following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="2647a-122">Получение журнала действий для подписки</span><span class="sxs-lookup"><span data-stu-id="2647a-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="2647a-123">Используйте командлет `Get-AzureRmLog` .</span><span class="sxs-lookup"><span data-stu-id="2647a-123">Use the `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="2647a-124">Ниже приведено несколько типичных примеров.</span><span class="sxs-lookup"><span data-stu-id="2647a-124">The following are some common examples.</span></span>

<span data-ttu-id="2647a-125">Получение записей журнала, начиная с указанной даты и времени и до настоящего момента.</span><span class="sxs-lookup"><span data-stu-id="2647a-125">Get log entries from this time/date to present:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="2647a-126">Получение записей журнала в пределах диапазона дат и времени.</span><span class="sxs-lookup"><span data-stu-id="2647a-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="2647a-127">Получение записей журнала для определенной группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2647a-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="2647a-128">Получение записей журнала от конкретного поставщика ресурсов в пределах диапазона даты и времени.</span><span class="sxs-lookup"><span data-stu-id="2647a-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="2647a-129">Получение всех записей журнала для конкретной вызывающей стороны.</span><span class="sxs-lookup"><span data-stu-id="2647a-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="2647a-130">Следующая команда извлекает последние 1000 событий из журнала:</span><span class="sxs-lookup"><span data-stu-id="2647a-130">The following command retrieves the last 1000 events from the activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="2647a-131">`Get-AzureRmLog` поддерживает много других параметров.</span><span class="sxs-lookup"><span data-stu-id="2647a-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="2647a-132">Дополнительные сведения см. в справке по `Get-AzureRmLog`.</span><span class="sxs-lookup"><span data-stu-id="2647a-132">See the `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="2647a-133">`Get-AzureRmLog` предоставляет данные журнала только за 15 дней.</span><span class="sxs-lookup"><span data-stu-id="2647a-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="2647a-134">С помощью параметра **-MaxEvents** можно запрашивать N последних событий за 15 дней.</span><span class="sxs-lookup"><span data-stu-id="2647a-134">Using the **-MaxEvents** parameter allows you to query the last N events, beyond 15 days.</span></span> <span data-ttu-id="2647a-135">Чтобы получить события старше 15 дней, используйте REST API или пакет SDK (пример на C# с использованием пакета SDK).</span><span class="sxs-lookup"><span data-stu-id="2647a-135">To access events older than 15 days, use the REST API or SDK (C# sample using the SDK).</span></span> <span data-ttu-id="2647a-136">Если не указать **StartTime**, то значением **EndTime** по умолчанию будет минус один час.</span><span class="sxs-lookup"><span data-stu-id="2647a-136">If you do not include **StartTime**, then the default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="2647a-137">Если не указать **EndTime**, то значением по умолчанию будет текущее время.</span><span class="sxs-lookup"><span data-stu-id="2647a-137">If you do not include **EndTime**, then the default value is current time.</span></span> <span data-ttu-id="2647a-138">Все значения времени указаны в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="2647a-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="2647a-139">Извлечение журнала оповещений</span><span class="sxs-lookup"><span data-stu-id="2647a-139">Retrieve alerts history</span></span>
<span data-ttu-id="2647a-140">Чтобы просмотреть все события оповещения, можно запросить журналы Azure Resource Manager, используя следующие примеры.</span><span class="sxs-lookup"><span data-stu-id="2647a-140">To view all alert events, you can query the Azure Resource Manager logs using the following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="2647a-141">Чтобы просмотреть журнал для конкретного правила генерации оповещений, можно использовать командлет `Get-AzureRmAlertHistory` , передав идентификатор ресурса этого правила.</span><span class="sxs-lookup"><span data-stu-id="2647a-141">To view the history for a specific alert rule, you can use the `Get-AzureRmAlertHistory` cmdlet, passing in the resource ID of the alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="2647a-142">Командлет `Get-AzureRmAlertHistory` поддерживает различные параметры.</span><span class="sxs-lookup"><span data-stu-id="2647a-142">The `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="2647a-143">Дополнительные сведения см. в документации командлета [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span><span class="sxs-lookup"><span data-stu-id="2647a-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="2647a-144">Извлечение информации о правилах генерации оповещений</span><span class="sxs-lookup"><span data-stu-id="2647a-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="2647a-145">Все следующие команды оперируют с группой ресурсов montest.</span><span class="sxs-lookup"><span data-stu-id="2647a-145">All of the following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="2647a-146">Просмотр всех свойств правила генерации оповещений.</span><span class="sxs-lookup"><span data-stu-id="2647a-146">View all the properties of the alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="2647a-147">Извлечение всех оповещений о группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2647a-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="2647a-148">Извлечение всех правил генерации оповещений для целевого ресурса.</span><span class="sxs-lookup"><span data-stu-id="2647a-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="2647a-149">Например, можно извлечь все правила генерации оповещений, установленные для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2647a-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="2647a-150">`Get-AzureRmAlertRule` поддерживает и другие параметры.</span><span class="sxs-lookup"><span data-stu-id="2647a-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="2647a-151">Дополнительную информацию см. в документации [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx).</span><span class="sxs-lookup"><span data-stu-id="2647a-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="2647a-152">Создание оповещений о метриках</span><span class="sxs-lookup"><span data-stu-id="2647a-152">Create metric alerts</span></span>
<span data-ttu-id="2647a-153">С помощью командлета `Add-AlertRule` можно создать, обновить или отключить правило генерации оповещений.</span><span class="sxs-lookup"><span data-stu-id="2647a-153">You can use the `Add-AlertRule` cmdlet to create, update or disable an alert rule.</span></span>

<span data-ttu-id="2647a-154">С помощью `New-AzureRmAlertRuleEmail` и `New-AzureRmAlertRuleWebhook` можно создать свойства электронного адреса и веб-перехватчика, соответственно.</span><span class="sxs-lookup"><span data-stu-id="2647a-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="2647a-155">В командлете правила генерации оповещений назначьте их в качестве действий свойства **Actions** правила генерации оповещений.</span><span class="sxs-lookup"><span data-stu-id="2647a-155">In the Alert rule cmdlet, assign these as actions to the **Actions** property of the Alert Rule.</span></span>

<span data-ttu-id="2647a-156">В следующей таблице описаны параметры и значения, используемые для создания оповещения с использованием метрики.</span><span class="sxs-lookup"><span data-stu-id="2647a-156">The following table describes the parameters and values used to create an alert using a metric.</span></span>

| <span data-ttu-id="2647a-157">Параметр</span><span class="sxs-lookup"><span data-stu-id="2647a-157">parameter</span></span> | <span data-ttu-id="2647a-158">value</span><span class="sxs-lookup"><span data-stu-id="2647a-158">value</span></span> |
| --- | --- |
| <span data-ttu-id="2647a-159">Имя</span><span class="sxs-lookup"><span data-stu-id="2647a-159">Name</span></span> |<span data-ttu-id="2647a-160">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="2647a-160">simpletestdiskwrite</span></span> |
| <span data-ttu-id="2647a-161">Расположение этого правила генерации оповещений</span><span class="sxs-lookup"><span data-stu-id="2647a-161">Location of this alert rule</span></span> |<span data-ttu-id="2647a-162">Восток США</span><span class="sxs-lookup"><span data-stu-id="2647a-162">East US</span></span> |
| <span data-ttu-id="2647a-163">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2647a-163">ResourceGroup</span></span> |<span data-ttu-id="2647a-164">montest</span><span class="sxs-lookup"><span data-stu-id="2647a-164">montest</span></span> |
| <span data-ttu-id="2647a-165">TargetResourceId</span><span class="sxs-lookup"><span data-stu-id="2647a-165">TargetResourceId</span></span> |<span data-ttu-id="2647a-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="2647a-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="2647a-167">MetricName созданного оповещения</span><span class="sxs-lookup"><span data-stu-id="2647a-167">MetricName of the alert that is created</span></span> |<span data-ttu-id="2647a-168">\PhysicalDisk (_Total) \Disk операции записи в секунду. В разделе `Get-MetricDefinitions` командлет о том, как получить точные имена метрик</span><span class="sxs-lookup"><span data-stu-id="2647a-168">\PhysicalDisk(_Total)\Disk Writes/sec. See the `Get-MetricDefinitions` cmdlet about how to retrieve the exact metric names</span></span> |
| <span data-ttu-id="2647a-169">operator</span><span class="sxs-lookup"><span data-stu-id="2647a-169">operator</span></span> |<span data-ttu-id="2647a-170">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="2647a-170">GreaterThan</span></span> |
| <span data-ttu-id="2647a-171">Пороговое значение (число/с для этой метрики)</span><span class="sxs-lookup"><span data-stu-id="2647a-171">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="2647a-172">1</span><span class="sxs-lookup"><span data-stu-id="2647a-172">1</span></span> |
| <span data-ttu-id="2647a-173">WindowSize (в формате чч:мм:сс)</span><span class="sxs-lookup"><span data-stu-id="2647a-173">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="2647a-174">00:05:00</span><span class="sxs-lookup"><span data-stu-id="2647a-174">00:05:00</span></span> |
| <span data-ttu-id="2647a-175">агрегатор (статистические данные о метрике — в этом случае при использовании среднего значения)</span><span class="sxs-lookup"><span data-stu-id="2647a-175">aggregator (statistic of the metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="2647a-176">Средняя</span><span class="sxs-lookup"><span data-stu-id="2647a-176">Average</span></span> |
| <span data-ttu-id="2647a-177">пользовательские сообщения электронной почты (строковый массив)</span><span class="sxs-lookup"><span data-stu-id="2647a-177">custom emails (string array)</span></span> |<span data-ttu-id="2647a-178">'foo@example.com','bar@example.com'</span><span class="sxs-lookup"><span data-stu-id="2647a-178">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="2647a-179">отправка сообщений электронной почты владельцам, участникам и читателям</span><span class="sxs-lookup"><span data-stu-id="2647a-179">send email to owners, contributors and readers</span></span> |<span data-ttu-id="2647a-180">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="2647a-180">-SendToServiceOwners</span></span> |

<span data-ttu-id="2647a-181">Создание действия электронного сообщения</span><span class="sxs-lookup"><span data-stu-id="2647a-181">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="2647a-182">Создание действия веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="2647a-182">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="2647a-183">Создание правила генерации оповещений на основе метрики загруженности ЦП (%) для классической виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="2647a-183">Create the alert rule on the CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="2647a-184">Извлечение правила генерации оповещений</span><span class="sxs-lookup"><span data-stu-id="2647a-184">Retrieve the alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="2647a-185">Командлет добавления оповещения также обновляет правило, если уже существует правило генерации оповещений с заданными свойствами.</span><span class="sxs-lookup"><span data-stu-id="2647a-185">The Add alert cmdlet also updates the rule if an alert rule already exists for the given properties.</span></span> <span data-ttu-id="2647a-186">Чтобы отключить правило оповещения, необходимо добавить параметр **-DisableRule**.</span><span class="sxs-lookup"><span data-stu-id="2647a-186">To disable an alert rule, include the parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="2647a-187">Получение списка доступных метрик для оповещений</span><span class="sxs-lookup"><span data-stu-id="2647a-187">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="2647a-188">С помощью командлета `Get-AzureRmMetricDefinition` можно просмотреть список всех метрик для конкретного ресурса.</span><span class="sxs-lookup"><span data-stu-id="2647a-188">You can use the `Get-AzureRmMetricDefinition` cmdlet to view the list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="2647a-189">В следующем примере создается таблица, содержащая имена метрик и их единицы измерения.</span><span class="sxs-lookup"><span data-stu-id="2647a-189">The following example generates a table with the metric Name and the Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="2647a-190">Полный список доступных параметров для `Get-AzureRmMetricDefinition` представлен в разделе [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span><span class="sxs-lookup"><span data-stu-id="2647a-190">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="2647a-191">Создание параметров автомасштабирования и управление ими</span><span class="sxs-lookup"><span data-stu-id="2647a-191">Create and manage AutoScale settings</span></span>
<span data-ttu-id="2647a-192">Для ресурса, например веб-приложения, виртуальной машины, облачной службы или масштабируемого набора виртуальных машин, можно настроить только один параметр автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="2647a-192">A resource, such as a Web app, VM, Cloud Service or Virtual Machine Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="2647a-193">Однако у каждого параметра автомасштабирования может быть несколько профилей.</span><span class="sxs-lookup"><span data-stu-id="2647a-193">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="2647a-194">Например, один профиль для масштабирования на основе производительности, а второй — на основе расписания.</span><span class="sxs-lookup"><span data-stu-id="2647a-194">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="2647a-195">Для каждого профиля можно настроить несколько правил.</span><span class="sxs-lookup"><span data-stu-id="2647a-195">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="2647a-196">Дополнительные сведения об автомасштабировании см. в статье [Автомасштабирование облачной службы](../cloud-services/cloud-services-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="2647a-196">For more information about Autoscale, see [How to Autoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="2647a-197">Вот какие действия мы выполним.</span><span class="sxs-lookup"><span data-stu-id="2647a-197">Here are the steps we will use:</span></span>

1. <span data-ttu-id="2647a-198">Создадим правила.</span><span class="sxs-lookup"><span data-stu-id="2647a-198">Create rule(s).</span></span>
2. <span data-ttu-id="2647a-199">Создадим профили для сопоставления с созданными ранее правилами.</span><span class="sxs-lookup"><span data-stu-id="2647a-199">Create profile(s) mapping the rules that you created previously to the profiles.</span></span>
3. <span data-ttu-id="2647a-200">(Необязательно.) Создадим уведомления для автомасштабирования, настроив свойства веб-перехватчика и электронного адреса.</span><span class="sxs-lookup"><span data-stu-id="2647a-200">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="2647a-201">Создадим параметры автомасштабирования с именем целевого ресурса, сопоставив профили и уведомления, созданные на предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="2647a-201">Create an autoscale setting with a name on the target resource by mapping the profiles and notifications that you created in the previous steps.</span></span>

<span data-ttu-id="2647a-202">В следующих примерах показано, как создать параметр автомасштабирования для масштабируемого набора виртуальных машин для операционной системы Windows, основанный на метрике использования ЦП.</span><span class="sxs-lookup"><span data-stu-id="2647a-202">The following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using the CPU utilization metric.</span></span>

<span data-ttu-id="2647a-203">Сначала создайте правило для развертывания, которое увеличивает количество экземпляров.</span><span class="sxs-lookup"><span data-stu-id="2647a-203">First, create a rule to scale-out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="2647a-204">Затем создайте правило для свертывания, которое уменьшает количество экземпляров.</span><span class="sxs-lookup"><span data-stu-id="2647a-204">Next, create a rule to scale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="2647a-205">После этого создайте профиль для этих правил.</span><span class="sxs-lookup"><span data-stu-id="2647a-205">Then, create a profile for the rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="2647a-206">Создайте действие веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="2647a-206">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="2647a-207">Создайте свойство уведомления для параметра автомасштабирования, добавив в него электронный адрес и веб-перехватчик, созданные ранее.</span><span class="sxs-lookup"><span data-stu-id="2647a-207">Create the notification property for the autoscale setting, including email and the webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="2647a-208">Наконец, создайте параметр автомасштабирования, чтобы добавить в него профиль, который вы создали.</span><span class="sxs-lookup"><span data-stu-id="2647a-208">Finally, create the autoscale setting to add the profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="2647a-209">Дополнительные сведения об управлении параметрами автомасштабирования см. в документации [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span><span class="sxs-lookup"><span data-stu-id="2647a-209">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="2647a-210">Журнал автомасштабирования</span><span class="sxs-lookup"><span data-stu-id="2647a-210">Autoscale history</span></span>
<span data-ttu-id="2647a-211">В следующем примере показано, как можно просмотреть последние события автомасштабирования и оповещения.</span><span class="sxs-lookup"><span data-stu-id="2647a-211">The following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="2647a-212">Используйте поиск по журналу событий, чтобы просматривать историю автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="2647a-212">Use the activity log search to view the autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="2647a-213">Для получения журнала автомасштабирования можно использовать командлет `Get-AzureRmAutoScaleHistory` .</span><span class="sxs-lookup"><span data-stu-id="2647a-213">You can use the `Get-AzureRmAutoScaleHistory` cmdlet to retrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="2647a-214">Дополнительные сведения см. в документации [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span><span class="sxs-lookup"><span data-stu-id="2647a-214">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="2647a-215">Просмотр сведений о параметре автомасштабирования</span><span class="sxs-lookup"><span data-stu-id="2647a-215">View details for an autoscale setting</span></span>
<span data-ttu-id="2647a-216">Чтобы получить дополнительные сведения о параметре автомасштабирования, можно использовать командлет `Get-Autoscalesetting` .</span><span class="sxs-lookup"><span data-stu-id="2647a-216">You can use the `Get-Autoscalesetting` cmdlet to retrieve more information about the autoscale setting.</span></span>

<span data-ttu-id="2647a-217">В следующем примере отображаются сведения о всех параметрах автомасштабирования в группе ресурсов myrg1.</span><span class="sxs-lookup"><span data-stu-id="2647a-217">The following example shows details about all autoscale settings in the resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="2647a-218">В следующем примере отображаются сведения о всех параметрах автомасштабирования в группе ресурсов myrg1, и отдельно — о параметре автомасштабирования MyScaleVMSSSetting.</span><span class="sxs-lookup"><span data-stu-id="2647a-218">The following example shows details about all autoscale settings in the resource group 'myrg1' and specifically the autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="2647a-219">Удаление параметра автомасштабирования</span><span class="sxs-lookup"><span data-stu-id="2647a-219">Remove an autoscale setting</span></span>
<span data-ttu-id="2647a-220">Для удаления параметра автомасштабирования можно использовать командлет `Remove-Autoscalesetting` .</span><span class="sxs-lookup"><span data-stu-id="2647a-220">You can use the `Remove-Autoscalesetting` cmdlet to delete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="2647a-221">Управление профилями журнала действий</span><span class="sxs-lookup"><span data-stu-id="2647a-221">Manage log profiles for activity log</span></span>
<span data-ttu-id="2647a-222">Вы можете создать *профиль журнала*, экспортировать данные из журнала действий в учетную запись хранения и настроить для них период хранения.</span><span class="sxs-lookup"><span data-stu-id="2647a-222">You can create a *log profile* and export data from your activity log to a storage account and you can configure data retention for it.</span></span> <span data-ttu-id="2647a-223">При необходимости можно также осуществить потоковую передачу этих данных в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="2647a-223">Optionally, you can also stream the data to your Event Hub.</span></span> <span data-ttu-id="2647a-224">Обратите внимание, что в настоящее время доступна предварительная версия этой функции и можно создать только один профиль журнала на подписку.</span><span class="sxs-lookup"><span data-stu-id="2647a-224">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="2647a-225">Чтобы создать профили журнала и управлять ими, используйте следующие командлеты в текущей подписке.</span><span class="sxs-lookup"><span data-stu-id="2647a-225">You can use the following cmdlets with your current subscription to create and manage log profiles.</span></span> <span data-ttu-id="2647a-226">Вы также можете выбрать другую подписку.</span><span class="sxs-lookup"><span data-stu-id="2647a-226">You can also choose a particular subscription.</span></span> <span data-ttu-id="2647a-227">Хотя по умолчанию PowerShell использует текущую подписку, ее всегда можно сменить с помощью командлета `Set-AzureRmContext`.</span><span class="sxs-lookup"><span data-stu-id="2647a-227">Although PowerShell defaults to the current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="2647a-228">Вы можете настроить журнал действий для маршрутизации данных в любую учетную запись хранения или концентратор событий в пределах этой подписки.</span><span class="sxs-lookup"><span data-stu-id="2647a-228">You can configure activity log to route data to any storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="2647a-229">Данные записываются как файлы больших двоичных объектов в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="2647a-229">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="2647a-230">Получение профиля журнала</span><span class="sxs-lookup"><span data-stu-id="2647a-230">Get a log profile</span></span>
<span data-ttu-id="2647a-231">Чтобы получить существующие профили журнала, используйте командлет `Get-AzureRmLogProfile` .</span><span class="sxs-lookup"><span data-stu-id="2647a-231">To fetch your existing log profiles, use the `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="2647a-232">Добавление профиля журнала без хранения данных</span><span class="sxs-lookup"><span data-stu-id="2647a-232">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="2647a-233">Удаление профиля журнала</span><span class="sxs-lookup"><span data-stu-id="2647a-233">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="2647a-234">Добавление профиля журнала с хранением данных</span><span class="sxs-lookup"><span data-stu-id="2647a-234">Add a log profile with data retention</span></span>
<span data-ttu-id="2647a-235">Можно указать свойство **-RetentionInDays** с положительным целым числом дней хранения данных.</span><span class="sxs-lookup"><span data-stu-id="2647a-235">You can specify the **-RetentionInDays** property with the number of days, as a positive integer, where the data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="2647a-236">Добавление профиля журнала с периодом удержания и концентратором событий</span><span class="sxs-lookup"><span data-stu-id="2647a-236">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="2647a-237">Помимо направления данных в учетную запись хранения, их также можно в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="2647a-237">In addition to routing your data to storage account, you can also stream it to an Event Hub.</span></span> <span data-ttu-id="2647a-238">Обратите внимание, что это предварительная версия, и конфигурация учетной записи хранения является обязательной, а конфигурация концентратора событий — нет.</span><span class="sxs-lookup"><span data-stu-id="2647a-238">Note that in this preview release and the storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="2647a-239">Настройка журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="2647a-239">Configure diagnostics logs</span></span>
<span data-ttu-id="2647a-240">Многие службы Azure предоставляют дополнительные журналы и данные телеметрии. Их можно настроить соответствующим образом, чтобы сохранять в учетной записи хранения Azure, отправлять в концентраторы событий и (или) отправлять в рабочую область OMS Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2647a-240">Many Azure services provide additional logs and telemetry that can be configured to save data in your Azure Storage account, send to Event Hubs, and/or sent to an OMS Log Analytics workspace.</span></span> <span data-ttu-id="2647a-241">Эта операция может выполняться только на уровне ресурса, и учетная запись хранения или концентратор событий должны находиться в том же регионе, что и целевой ресурс, для которого настроены параметры диагностики.</span><span class="sxs-lookup"><span data-stu-id="2647a-241">That operation can only be performed at a resource level and the storage account or event hub should be present in the same region as the target resource where the diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="2647a-242">Получение параметра диагностики</span><span class="sxs-lookup"><span data-stu-id="2647a-242">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="2647a-243">Отключение параметра диагностики</span><span class="sxs-lookup"><span data-stu-id="2647a-243">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="2647a-244">Включение параметра диагностики без периода удержания</span><span class="sxs-lookup"><span data-stu-id="2647a-244">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="2647a-245">Включение параметра диагностики с периодом удержания</span><span class="sxs-lookup"><span data-stu-id="2647a-245">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="2647a-246">Включение параметра диагностики с периодом удержания для определенной категории журналов</span><span class="sxs-lookup"><span data-stu-id="2647a-246">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="2647a-247">Включение параметра диагностики для концентратора событий</span><span class="sxs-lookup"><span data-stu-id="2647a-247">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="2647a-248">Включение параметра диагностики для OMS</span><span class="sxs-lookup"><span data-stu-id="2647a-248">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
