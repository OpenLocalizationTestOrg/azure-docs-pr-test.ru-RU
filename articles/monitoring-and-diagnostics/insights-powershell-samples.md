---
title: "Примеры быстрого запуска монитора PowerShell aaaAzure. | Документация Майкрософт"
description: "С помощью PowerShell tooaccess монитора Azure функции, такие как Автомасштабирование, предупреждения, веб-перехватчиков и поиска журналы действий."
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
ms.openlocfilehash: 6eece0b0227e0bbf08225bd330d0601169911f55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-powershell-quick-start-samples"></a><span data-ttu-id="ea1dc-104">Примеры для быстрого запуска Azure Monitor с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea1dc-104">Azure Monitor PowerShell quick start samples</span></span>
<span data-ttu-id="ea1dc-105">Это статье показывает пример toohelp команд PowerShell, можно получить доступ к возможности Azure монитора.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-105">This article shows you sample PowerShell commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="ea1dc-106">Монитор Azure позволяет tooAutoScale облачных служб, виртуальных машин и веб-приложений и toosend уведомлений или вызов веб-адреса на основе значений данных телеметрии, настроенных.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-106">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="ea1dc-107">Монитор Azure — новое имя hello что был вызван «Azure Insights» до 25 сентября 2016 года.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-107">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="ea1dc-108">Однако hello пространств имен и, следовательно, hello, следующие команды по-прежнему содержать аналитики «hello».</span><span class="sxs-lookup"><span data-stu-id="ea1dc-108">However, hello namespaces and thus hello following commands still contain hello "insights".</span></span>
> 
> 

## <a name="set-up-powershell"></a><span data-ttu-id="ea1dc-109">Настройка PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea1dc-109">Set up PowerShell</span></span>
<span data-ttu-id="ea1dc-110">Если это еще не сделано, установите toorun PowerShell на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-110">If you haven't already, set up PowerShell toorun on your computer.</span></span> <span data-ttu-id="ea1dc-111">Дополнительные сведения см. в разделе [как tooInstall и настроить PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ea1dc-111">For more information, see [How tooInstall and Configure PowerShell](/powershell/azure/overview).</span></span>

## <a name="examples-in-this-article"></a><span data-ttu-id="ea1dc-112">Примеры в этой статье</span><span class="sxs-lookup"><span data-stu-id="ea1dc-112">Examples in this article</span></span>
<span data-ttu-id="ea1dc-113">Hello в статье hello примерах об использовании командлетов Azure монитора.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-113">hello examples in hello article illustrate how you can use Azure Monitor cmdlets.</span></span> <span data-ttu-id="ea1dc-114">Можно также просмотреть hello весь список командлетов Azure PowerShell монитора на [командлеты Azure монитора (аналитика)](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea1dc-114">You can also review hello entire list of Azure Monitor PowerShell cmdlets at [Azure Monitor (Insights) Cmdlets](https://msdn.microsoft.com/library/azure/mt282452#40v=azure.200#41.aspx).</span></span>

## <a name="sign-in-and-use-subscriptions"></a><span data-ttu-id="ea1dc-115">Вход в систему и использование подписок</span><span class="sxs-lookup"><span data-stu-id="ea1dc-115">Sign in and use subscriptions</span></span>
<span data-ttu-id="ea1dc-116">Во-первых войдите в tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-116">First, log in tooyour Azure subscription.</span></span>

```PowerShell
Login-AzureRmAccount
```

<span data-ttu-id="ea1dc-117">Для этого в toosign.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-117">This requires you toosign in.</span></span> <span data-ttu-id="ea1dc-118">После этого вы увидите свою учетную запись, идентификатор клиента и идентификатор подписки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-118">Once you do, your Account, TenantID and default Subscription ID are displayed.</span></span> <span data-ttu-id="ea1dc-119">Все hello Azure командлеты работают в контексте hello подписки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-119">All hello Azure cmdlets work in hello context of your default subscription.</span></span> <span data-ttu-id="ea1dc-120">tooview hello список подписок, доступ к, используйте следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-120">tooview hello list of subscriptions you have access to, use hello following command.</span></span>

```PowerShell
Get-AzureRmSubscription
```

<span data-ttu-id="ea1dc-121">toochange рабочий контекст tooa другой подпиской, hello используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-121">toochange your working context tooa different subscription, use hello following command.</span></span>

```PowerShell
Set-AzureRmContext -SubscriptionId <subscriptionid>
```


## <a name="retrieve-activity-log-for-a-subscription"></a><span data-ttu-id="ea1dc-122">Получение журнала действий для подписки</span><span class="sxs-lookup"><span data-stu-id="ea1dc-122">Retrieve Activity log for a subscription</span></span>
<span data-ttu-id="ea1dc-123">Используйте hello `Get-AzureRmLog` командлета.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-123">Use hello `Get-AzureRmLog` cmdlet.</span></span>  <span data-ttu-id="ea1dc-124">Hello ниже приведены некоторые примеры.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-124">hello following are some common examples.</span></span>

<span data-ttu-id="ea1dc-125">Получение записей журнала из этого toopresent даты и времени:</span><span class="sxs-lookup"><span data-stu-id="ea1dc-125">Get log entries from this time/date toopresent:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2016-03-01T10:30
```

<span data-ttu-id="ea1dc-126">Получение записей журнала в пределах диапазона дат и времени.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-126">Get log entries between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="ea1dc-127">Получение записей журнала для определенной группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-127">Get log entries from a specific resource group:</span></span>

```PowerShell
Get-AzureRmLog -ResourceGroup 'myrg1'
```

<span data-ttu-id="ea1dc-128">Получение записей журнала от конкретного поставщика ресурсов в пределах диапазона даты и времени.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-128">Get log entries from a specific resource provider between a time/date range:</span></span>

```PowerShell
Get-AzureRmLog -ResourceProvider 'Microsoft.Web' -StartTime 2015-01-01T10:30 -EndTime 2015-01-01T11:30
```

<span data-ttu-id="ea1dc-129">Получение всех записей журнала для конкретной вызывающей стороны.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-129">Get all log entries with a specific caller:</span></span>

```PowerShell
Get-AzureRmLog -Caller 'myname@company.com'
```

<span data-ttu-id="ea1dc-130">Следующая команда извлекает Hello hello последних 1000 событий из журнала активности hello:</span><span class="sxs-lookup"><span data-stu-id="ea1dc-130">hello following command retrieves hello last 1000 events from hello activity log:</span></span>

```PowerShell
Get-AzureRmLog -MaxEvents 1000
```

<span data-ttu-id="ea1dc-131">`Get-AzureRmLog` поддерживает много других параметров.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-131">`Get-AzureRmLog` supports many other parameters.</span></span> <span data-ttu-id="ea1dc-132">В разделе hello `Get-AzureRmLog` ссылку для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-132">See hello `Get-AzureRmLog` reference for more information.</span></span>

> [!NOTE]
> <span data-ttu-id="ea1dc-133">`Get-AzureRmLog` предоставляет данные журнала только за 15 дней.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-133">`Get-AzureRmLog` only provides 15 days of history.</span></span> <span data-ttu-id="ea1dc-134">С помощью hello **- MaxEvents** параметр позволяет tooquery hello последние N событий, за 15 дней.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-134">Using hello **-MaxEvents** parameter allows you tooquery hello last N events, beyond 15 days.</span></span> <span data-ttu-id="ea1dc-135">события tooaccess старее 15 дней используйте hello API-интерфейса REST или пакета SDK (пример на C# с помощью пакета SDK для hello).</span><span class="sxs-lookup"><span data-stu-id="ea1dc-135">tooaccess events older than 15 days, use hello REST API or SDK (C# sample using hello SDK).</span></span> <span data-ttu-id="ea1dc-136">Если не включать **StartTime**, то значение по умолчанию hello **EndTime** минус один час.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-136">If you do not include **StartTime**, then hello default value is **EndTime** minus one hour.</span></span> <span data-ttu-id="ea1dc-137">Если не включать **EndTime**, то значение по умолчанию hello текущее время.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-137">If you do not include **EndTime**, then hello default value is current time.</span></span> <span data-ttu-id="ea1dc-138">Все значения времени указаны в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-138">All times are in UTC.</span></span>
> 
> 

## <a name="retrieve-alerts-history"></a><span data-ttu-id="ea1dc-139">Извлечение журнала оповещений</span><span class="sxs-lookup"><span data-stu-id="ea1dc-139">Retrieve alerts history</span></span>
<span data-ttu-id="ea1dc-140">все предупреждения событий, вы можете запросить tooview hello журналы диспетчера ресурсов Azure, используя следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-140">tooview all alert events, you can query hello Azure Resource Manager logs using hello following examples.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/alertRules" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="ea1dc-141">правило tooview hello журнала для указанного предупреждения, можно использовать hello `Get-AzureRmAlertHistory` командлета, передавая идентификатор ресурса hello hello правило оповещения.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-141">tooview hello history for a specific alert rule, you can use hello `Get-AzureRmAlertHistory` cmdlet, passing in hello resource ID of hello alert rule.</span></span>

```PowerShell
Get-AzureRmAlertHistory -ResourceId /subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/myalert -StartTime 2016-03-1 -Status Activated
```

<span data-ttu-id="ea1dc-142">Hello `Get-AzureRmAlertHistory` командлет поддерживает различные параметры.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-142">hello `Get-AzureRmAlertHistory` cmdlet supports various parameters.</span></span> <span data-ttu-id="ea1dc-143">Дополнительные сведения см. в документации командлета [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea1dc-143">More information, see [Get-AlertHistory](https://msdn.microsoft.com/library/mt282453.aspx).</span></span>

## <a name="retrieve-information-on-alert-rules"></a><span data-ttu-id="ea1dc-144">Извлечение информации о правилах генерации оповещений</span><span class="sxs-lookup"><span data-stu-id="ea1dc-144">Retrieve information on alert rules</span></span>
<span data-ttu-id="ea1dc-145">Все следующие команды hello, влияют на группу ресурсов с именем «montest».</span><span class="sxs-lookup"><span data-stu-id="ea1dc-145">All of hello following commands act on a Resource Group named "montest".</span></span>

<span data-ttu-id="ea1dc-146">Просмотрите все свойства hello hello правило генерации оповещений:</span><span class="sxs-lookup"><span data-stu-id="ea1dc-146">View all hello properties of hello alert rule:</span></span>

```PowerShell
Get-AzureRmAlertRule -Name simpletestCPU -ResourceGroup montest -DetailedOutput
```

<span data-ttu-id="ea1dc-147">Извлечение всех оповещений о группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-147">Retrieve all alerts on a resource group:</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest
```

<span data-ttu-id="ea1dc-148">Извлечение всех правил генерации оповещений для целевого ресурса.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-148">Retrieve all alert rules set for a target resource.</span></span> <span data-ttu-id="ea1dc-149">Например, можно извлечь все правила генерации оповещений, установленные для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-149">For example, all alert rules set on a VM.</span></span>

```PowerShell
Get-AzureRmAlertRule -ResourceGroup montest -TargetResourceId /subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig
```

<span data-ttu-id="ea1dc-150">`Get-AzureRmAlertRule` поддерживает и другие параметры.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-150">`Get-AzureRmAlertRule` supports other parameters.</span></span> <span data-ttu-id="ea1dc-151">Дополнительную информацию см. в документации [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea1dc-151">See [Get-AlertRule](https://msdn.microsoft.com/library/mt282459.aspx) for more information.</span></span>

## <a name="create-metric-alerts"></a><span data-ttu-id="ea1dc-152">Создание оповещений о метриках</span><span class="sxs-lookup"><span data-stu-id="ea1dc-152">Create metric alerts</span></span>
<span data-ttu-id="ea1dc-153">Можно использовать hello `Add-AlertRule` toocreate командлета, обновление или отключение правила оповещения.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-153">You can use hello `Add-AlertRule` cmdlet toocreate, update or disable an alert rule.</span></span>

<span data-ttu-id="ea1dc-154">С помощью `New-AzureRmAlertRuleEmail` и `New-AzureRmAlertRuleWebhook` можно создать свойства электронного адреса и веб-перехватчика, соответственно.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-154">You can create email and webhook properties using  `New-AzureRmAlertRuleEmail` and `New-AzureRmAlertRuleWebhook`, respectively.</span></span> <span data-ttu-id="ea1dc-155">В командлете правило генерации оповещений hello, назначьте их в качестве действия toohello **действия** свойство hello правило оповещения.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-155">In hello Alert rule cmdlet, assign these as actions toohello **Actions** property of hello Alert Rule.</span></span>

<span data-ttu-id="ea1dc-156">Hello в следующей таблице описаны параметры hello и значения используется toocreate оповещение с использованием показателя.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-156">hello following table describes hello parameters and values used toocreate an alert using a metric.</span></span>

| <span data-ttu-id="ea1dc-157">Параметр</span><span class="sxs-lookup"><span data-stu-id="ea1dc-157">parameter</span></span> | <span data-ttu-id="ea1dc-158">value</span><span class="sxs-lookup"><span data-stu-id="ea1dc-158">value</span></span> |
| --- | --- |
| <span data-ttu-id="ea1dc-159">Имя</span><span class="sxs-lookup"><span data-stu-id="ea1dc-159">Name</span></span> |<span data-ttu-id="ea1dc-160">simpletestdiskwrite</span><span class="sxs-lookup"><span data-stu-id="ea1dc-160">simpletestdiskwrite</span></span> |
| <span data-ttu-id="ea1dc-161">Расположение этого правила генерации оповещений</span><span class="sxs-lookup"><span data-stu-id="ea1dc-161">Location of this alert rule</span></span> |<span data-ttu-id="ea1dc-162">Восток США</span><span class="sxs-lookup"><span data-stu-id="ea1dc-162">East US</span></span> |
| <span data-ttu-id="ea1dc-163">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ea1dc-163">ResourceGroup</span></span> |<span data-ttu-id="ea1dc-164">montest</span><span class="sxs-lookup"><span data-stu-id="ea1dc-164">montest</span></span> |
| <span data-ttu-id="ea1dc-165">TargetResourceId</span><span class="sxs-lookup"><span data-stu-id="ea1dc-165">TargetResourceId</span></span> |<span data-ttu-id="ea1dc-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span><span class="sxs-lookup"><span data-stu-id="ea1dc-166">/subscriptions/s1/resourceGroups/montest/providers/Microsoft.Compute/virtualMachines/testconfig</span></span> |
| <span data-ttu-id="ea1dc-167">MetricName hello предупреждения, которая создается</span><span class="sxs-lookup"><span data-stu-id="ea1dc-167">MetricName of hello alert that is created</span></span> |<span data-ttu-id="ea1dc-168">\PhysicalDisk (_Total) \Disk операции записи в секунду. В разделе hello `Get-MetricDefinitions` по командлетам как tooretrieve hello точные имена метрик</span><span class="sxs-lookup"><span data-stu-id="ea1dc-168">\PhysicalDisk(_Total)\Disk Writes/sec. See hello `Get-MetricDefinitions` cmdlet about how tooretrieve hello exact metric names</span></span> |
| <span data-ttu-id="ea1dc-169">operator</span><span class="sxs-lookup"><span data-stu-id="ea1dc-169">operator</span></span> |<span data-ttu-id="ea1dc-170">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="ea1dc-170">GreaterThan</span></span> |
| <span data-ttu-id="ea1dc-171">Пороговое значение (число/с для этой метрики)</span><span class="sxs-lookup"><span data-stu-id="ea1dc-171">Threshold value (count/sec in for this metric)</span></span> |<span data-ttu-id="ea1dc-172">1</span><span class="sxs-lookup"><span data-stu-id="ea1dc-172">1</span></span> |
| <span data-ttu-id="ea1dc-173">WindowSize (в формате чч:мм:сс)</span><span class="sxs-lookup"><span data-stu-id="ea1dc-173">WindowSize (hh:mm:ss format)</span></span> |<span data-ttu-id="ea1dc-174">00:05:00</span><span class="sxs-lookup"><span data-stu-id="ea1dc-174">00:05:00</span></span> |
| <span data-ttu-id="ea1dc-175">средство инвентаризации (статистики hello метрики, которые используются в этом случае среднее количество)</span><span class="sxs-lookup"><span data-stu-id="ea1dc-175">aggregator (statistic of hello metric, which uses Average count, in this case)</span></span> |<span data-ttu-id="ea1dc-176">Средняя</span><span class="sxs-lookup"><span data-stu-id="ea1dc-176">Average</span></span> |
| <span data-ttu-id="ea1dc-177">пользовательские сообщения электронной почты (строковый массив)</span><span class="sxs-lookup"><span data-stu-id="ea1dc-177">custom emails (string array)</span></span> |<span data-ttu-id="ea1dc-178">'foo@example.com','bar@example.com'</span><span class="sxs-lookup"><span data-stu-id="ea1dc-178">'foo@example.com','bar@example.com'</span></span> |
| <span data-ttu-id="ea1dc-179">Отправить по электронной почте tooowners, участники и Читатели</span><span class="sxs-lookup"><span data-stu-id="ea1dc-179">send email tooowners, contributors and readers</span></span> |<span data-ttu-id="ea1dc-180">-SendToServiceOwners</span><span class="sxs-lookup"><span data-stu-id="ea1dc-180">-SendToServiceOwners</span></span> |

<span data-ttu-id="ea1dc-181">Создание действия электронного сообщения</span><span class="sxs-lookup"><span data-stu-id="ea1dc-181">Create an Email action</span></span>

```PowerShell
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
```

<span data-ttu-id="ea1dc-182">Создание действия веб-перехватчика</span><span class="sxs-lookup"><span data-stu-id="ea1dc-182">Create a Webhook action</span></span>

```PowerShell
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://example.com?token=mytoken
```

<span data-ttu-id="ea1dc-183">Создание правила оповещения hello на метрику % ЦП hello в классической виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="ea1dc-183">Create hello alert rule on hello CPU% metric on a classic VM</span></span>

```PowerShell
Add-AzureRmMetricAlertRule -Name vmcpu_gt_1 -Location "East US" -ResourceGroup myrg1 -TargetResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.ClassicCompute/virtualMachines/my_vm1 -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 1 -WindowSize 00:05:00 -TimeAggregationOperator Average -Actions $actionEmail, $actionWebhook -Description "alert on CPU > 1%"
```

<span data-ttu-id="ea1dc-184">Получить правило генерации оповещений hello</span><span class="sxs-lookup"><span data-stu-id="ea1dc-184">Retrieve hello alert rule</span></span>

```PowerShell
Get-AzureRmAlertRule -Name vmcpu_gt_1 -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="ea1dc-185">Hello добавить оповещения также обновляет правило hello Если правило генерации оповещений для заданного свойства hello уже существует.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-185">hello Add alert cmdlet also updates hello rule if an alert rule already exists for hello given properties.</span></span> <span data-ttu-id="ea1dc-186">toodisable правило генерации оповещений, включите параметр hello **- DisableRule**.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-186">toodisable an alert rule, include hello parameter **-DisableRule**.</span></span>

## <a name="get-a-list-of-available-metrics-for-alerts"></a><span data-ttu-id="ea1dc-187">Получение списка доступных метрик для оповещений</span><span class="sxs-lookup"><span data-stu-id="ea1dc-187">Get a list of available metrics for alerts</span></span>
<span data-ttu-id="ea1dc-188">Можно использовать hello `Get-AzureRmMetricDefinition` командлет tooview hello список все метрики для конкретного ресурса.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-188">You can use hello `Get-AzureRmMetricDefinition` cmdlet tooview hello list of all metrics for a specific resource.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id>
```

<span data-ttu-id="ea1dc-189">Hello следующий пример создает таблицу с метрикой hello имя и hello единицы для него.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-189">hello following example generates a table with hello metric Name and hello Unit for it.</span></span>

```PowerShell
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

<span data-ttu-id="ea1dc-190">Полный список доступных параметров для `Get-AzureRmMetricDefinition` представлен в разделе [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea1dc-190">A full list of available options for `Get-AzureRmMetricDefinition` is available at [Get-MetricDefinitions](https://msdn.microsoft.com/library/mt282458.aspx).</span></span>

## <a name="create-and-manage-autoscale-settings"></a><span data-ttu-id="ea1dc-191">Создание параметров автомасштабирования и управление ими</span><span class="sxs-lookup"><span data-stu-id="ea1dc-191">Create and manage AutoScale settings</span></span>
<span data-ttu-id="ea1dc-192">Для ресурса, например веб-приложения, виртуальной машины, облачной службы или масштабируемого набора виртуальных машин, можно настроить только один параметр автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-192">A resource, such as a Web app, VM, Cloud Service or Virtual Machine Scale Set can have only one autoscale setting configured for it.</span></span>
<span data-ttu-id="ea1dc-193">Однако у каждого параметра автомасштабирования может быть несколько профилей.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-193">However, each autoscale setting can have multiple profiles.</span></span> <span data-ttu-id="ea1dc-194">Например, один профиль для масштабирования на основе производительности, а второй — на основе расписания.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-194">For example, one for a performance-based scale profile and a second one for a schedule-based profile.</span></span> <span data-ttu-id="ea1dc-195">Для каждого профиля можно настроить несколько правил.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-195">Each profile can have multiple rules configured on it.</span></span> <span data-ttu-id="ea1dc-196">Дополнительные сведения о автомасштабирования см. в разделе [как tooAutoscale приложения](../cloud-services/cloud-services-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="ea1dc-196">For more information about Autoscale, see [How tooAutoscale an Application](../cloud-services/cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="ea1dc-197">Ниже приведены шаги hello, которые будут использоваться.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-197">Here are hello steps we will use:</span></span>

1. <span data-ttu-id="ea1dc-198">Создадим правила.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-198">Create rule(s).</span></span>
2. <span data-ttu-id="ea1dc-199">Создайте профили правила сопоставления hello, созданный ранее toohello профилей.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-199">Create profile(s) mapping hello rules that you created previously toohello profiles.</span></span>
3. <span data-ttu-id="ea1dc-200">(Необязательно.) Создадим уведомления для автомасштабирования, настроив свойства веб-перехватчика и электронного адреса.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-200">Optional: Create notifications for autoscale by configuring webhook and email properties.</span></span>
4. <span data-ttu-id="ea1dc-201">Создание параметров автоматического масштабирования с именем hello целевого ресурса путем сопоставления профилей hello и уведомления, созданные в предыдущих шагах hello.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-201">Create an autoscale setting with a name on hello target resource by mapping hello profiles and notifications that you created in hello previous steps.</span></span>

<span data-ttu-id="ea1dc-202">Hello следующих примерах показано, как создать параметров автоматического масштабирования для набора масштабирования виртуальных машин для операционной системы Windows, с помощью приложения hello ЦП метрики использования.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-202">hello following examples show you how you can create an Autoscale setting for a Virtual Machine Scale Set for a Windows operating system based by using hello CPU utilization metric.</span></span>

<span data-ttu-id="ea1dc-203">Сначала создайте правило tooscale выход, с увеличением числа экземпляра.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-203">First, create a rule tooscale-out, with an instance count increase.</span></span>

```PowerShell
$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Increase -ScaleActionValue 1
```        

<span data-ttu-id="ea1dc-204">Создайте правило tooscale в с уменьшение числа экземпляра.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-204">Next, create a rule tooscale-in, with an instance count decrease.</span></span>

```PowerShell
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -Operator GreaterThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:10:00 -ScaleActionCooldown 00:10:00 -ScaleActionDirection Decrease -ScaleActionValue 1
```

<span data-ttu-id="ea1dc-205">Затем создайте профиль для правил hello.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-205">Then, create a profile for hello rules.</span></span>

```PowerShell
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "My_Profile"
```

<span data-ttu-id="ea1dc-206">Создайте действие веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-206">Create a webhook property.</span></span>

```PowerShell
$webhook_scale = New-AzureRmAutoscaleWebhook -ServiceUri "https://example.com?mytoken=mytokenvalue"
```

<span data-ttu-id="ea1dc-207">Создайте свойство hello уведомления для параметра автоматического масштабирования hello, включая сообщения электронной почты и hello веб-перехватчика, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-207">Create hello notification property for hello autoscale setting, including email and hello webhook that you created previously.</span></span>

```PowerShell
$notification1= New-AzureRmAutoscaleNotification -CustomEmails ashwink@microsoft.com -SendEmailToSubscriptionAdministrators SendEmailToSubscriptionCoAdministrators -Webhooks $webhook_scale
```

<span data-ttu-id="ea1dc-208">Наконец создайте hello автомасштабирования параметр tooadd hello профиль, созданный выше.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-208">Finally, create hello autoscale setting tooadd hello profile that you created above.</span></span>

```PowerShell
Add-AzureRmAutoscaleSetting -Location "East US" -Name "MyScaleVMSSSetting" -ResourceGroup big2 -TargetResourceId /subscriptions/s1/resourceGroups/big2/providers/Microsoft.Compute/virtualMachineScaleSets/big2 -AutoscaleProfiles $profile1 -Notifications $notification1
```

<span data-ttu-id="ea1dc-209">Дополнительные сведения об управлении параметрами автомасштабирования см. в документации [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea1dc-209">For more information about managing Autoscale settings, see [Get-AutoscaleSetting](https://msdn.microsoft.com/library/mt282461.aspx).</span></span>

## <a name="autoscale-history"></a><span data-ttu-id="ea1dc-210">Журнал автомасштабирования</span><span class="sxs-lookup"><span data-stu-id="ea1dc-210">Autoscale history</span></span>
<span data-ttu-id="ea1dc-211">Hello следующем примере показано, как можно просмотреть последние события автоматического масштабирования и предупреждение.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-211">hello following example shows you how you can view recent autoscale and alert events.</span></span> <span data-ttu-id="ea1dc-212">Используйте hello поиска журнала действий tooview историю автомасштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-212">Use hello activity log search tooview hello autoscale history.</span></span>

```PowerShell
Get-AzureRmLog -Caller "Microsoft.Insights/autoscaleSettings" -DetailedOutput -StartTime 2015-03-01
```

<span data-ttu-id="ea1dc-213">Можно использовать hello `Get-AzureRmAutoScaleHistory` tooretrieve командлет историю автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-213">You can use hello `Get-AzureRmAutoScaleHistory` cmdlet tooretrieve AutoScale history.</span></span>

```PowerShell
Get-AzureRmAutoScaleHistory -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/microsoft.insights/autoscalesettings/myScaleSetting -StartTime 2016-03-15 -DetailedOutput
```

<span data-ttu-id="ea1dc-214">Дополнительные сведения см. в документации [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea1dc-214">For more information, see [Get-AutoscaleHistory](https://msdn.microsoft.com/library/mt282464.aspx).</span></span>

### <a name="view-details-for-an-autoscale-setting"></a><span data-ttu-id="ea1dc-215">Просмотр сведений о параметре автомасштабирования</span><span class="sxs-lookup"><span data-stu-id="ea1dc-215">View details for an autoscale setting</span></span>
<span data-ttu-id="ea1dc-216">Можно использовать hello `Get-Autoscalesetting` tooretrieve командлет Дополнительные сведения о настройке автомасштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-216">You can use hello `Get-Autoscalesetting` cmdlet tooretrieve more information about hello autoscale setting.</span></span>

<span data-ttu-id="ea1dc-217">Hello пример сведения обо всех параметрах автоматического масштабирования в группе ресурсов hello «myrg1».</span><span class="sxs-lookup"><span data-stu-id="ea1dc-217">hello following example shows details about all autoscale settings in hello resource group 'myrg1'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -DetailedOutput
```

<span data-ttu-id="ea1dc-218">Hello следующий пример показывает сведения обо всех параметрах автоматического масштабирования в группе ресурсов hello «myrg1» и в частности hello с именем «MyScaleVMSSSetting» параметр автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-218">hello following example shows details about all autoscale settings in hello resource group 'myrg1' and specifically hello autoscale setting named 'MyScaleVMSSSetting'.</span></span>

```PowerShell
Get-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting -DetailedOutput
```

### <a name="remove-an-autoscale-setting"></a><span data-ttu-id="ea1dc-219">Удаление параметра автомасштабирования</span><span class="sxs-lookup"><span data-stu-id="ea1dc-219">Remove an autoscale setting</span></span>
<span data-ttu-id="ea1dc-220">Можно использовать hello `Remove-Autoscalesetting` toodelete командлет параметров автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-220">You can use hello `Remove-Autoscalesetting` cmdlet toodelete an autoscale setting.</span></span>

```PowerShell
Remove-AzureRmAutoscalesetting -ResourceGroup myrg1 -Name MyScaleVMSSSetting
```

## <a name="manage-log-profiles-for-activity-log"></a><span data-ttu-id="ea1dc-221">Управление профилями журнала действий</span><span class="sxs-lookup"><span data-stu-id="ea1dc-221">Manage log profiles for activity log</span></span>
<span data-ttu-id="ea1dc-222">Можно создать *входа профиль* и экспорт данных из вашей учетной записи действия журнала tooa хранения и можно настроить хранение данных для него.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-222">You can create a *log profile* and export data from your activity log tooa storage account and you can configure data retention for it.</span></span> <span data-ttu-id="ea1dc-223">При необходимости можно осуществлять потоковую tooyour hello данных концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-223">Optionally, you can also stream hello data tooyour Event Hub.</span></span> <span data-ttu-id="ea1dc-224">Обратите внимание, что в настоящее время доступна предварительная версия этой функции и можно создать только один профиль журнала на подписку.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-224">Note that this feature is currently in Preview and you can only create one log profile per subscription.</span></span> <span data-ttu-id="ea1dc-225">Можно использовать следующие командлеты с вашей текущей подписки toocreate hello и управления профилями журнала.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-225">You can use hello following cmdlets with your current subscription toocreate and manage log profiles.</span></span> <span data-ttu-id="ea1dc-226">Вы также можете выбрать другую подписку.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-226">You can also choose a particular subscription.</span></span> <span data-ttu-id="ea1dc-227">Несмотря на то, что PowerShell значения по умолчанию для текущей подписки toohello всегда можно изменить, используя `Set-AzureRmContext`.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-227">Although PowerShell defaults toohello current subscription, you can always change that using `Set-AzureRmContext`.</span></span> <span data-ttu-id="ea1dc-228">Можно настроить учетную запись хранения tooany данных в tooroute журнала действий или концентратор событий в пределах этой подписки.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-228">You can configure activity log tooroute data tooany storage account or Event Hub within that subscription.</span></span> <span data-ttu-id="ea1dc-229">Данные записываются как файлы больших двоичных объектов в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-229">Data is written as blob files in JSON format.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="ea1dc-230">Получение профиля журнала</span><span class="sxs-lookup"><span data-stu-id="ea1dc-230">Get a log profile</span></span>
<span data-ttu-id="ea1dc-231">toofetch существующие профили журнала, используйте hello `Get-AzureRmLogProfile` командлета.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-231">toofetch your existing log profiles, use hello `Get-AzureRmLogProfile` cmdlet.</span></span>

### <a name="add-a-log-profile-without-data-retention"></a><span data-ttu-id="ea1dc-232">Добавление профиля журнала без хранения данных</span><span class="sxs-lookup"><span data-stu-id="ea1dc-232">Add a log profile without data retention</span></span>
```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="ea1dc-233">Удаление профиля журнала</span><span class="sxs-lookup"><span data-stu-id="ea1dc-233">Remove a log profile</span></span>
```PowerShell
Remove-AzureRmLogProfile -name my_log_profile_s1
```

### <a name="add-a-log-profile-with-data-retention"></a><span data-ttu-id="ea1dc-234">Добавление профиля журнала с хранением данных</span><span class="sxs-lookup"><span data-stu-id="ea1dc-234">Add a log profile with data retention</span></span>
<span data-ttu-id="ea1dc-235">Можно указать hello **- RetentionInDays** свойство с hello количество дней, в виде положительного целого числа, где хранятся данные hello.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-235">You can specify hello **-RetentionInDays** property with hello number of days, as a positive integer, where hello data is retained.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

### <a name="add-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="ea1dc-236">Добавление профиля журнала с периодом удержания и концентратором событий</span><span class="sxs-lookup"><span data-stu-id="ea1dc-236">Add log profile with retention and EventHub</span></span>
<span data-ttu-id="ea1dc-237">В дополнение toorouting toostorage учетной записи данных, вы также осуществляет потоковую передачу его tooan концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-237">In addition toorouting your data toostorage account, you can also stream it tooan Event Hub.</span></span> <span data-ttu-id="ea1dc-238">Обратите внимание, что в этой предварительной версии выпуска и hello конфигурацию учетной записи хранения является обязательным, но конфигурация концентратора событий не является обязательной.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-238">Note that in this preview release and hello storage account configuration is mandatory but Event Hub configuration is optional.</span></span>

```PowerShell
Add-AzureRmLogProfile -Name my_log_profile_s1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia -RetentionInDays 90
```

## <a name="configure-diagnostics-logs"></a><span data-ttu-id="ea1dc-239">Настройка журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="ea1dc-239">Configure diagnostics logs</span></span>
<span data-ttu-id="ea1dc-240">Многие службы Azure предоставляют дополнительные журналы и данные телеметрии, может быть toosave настроенных данных в вашей учетной записи хранилища Azure, отправить tooEvent концентраторов и/или отправлено рабочей области аналитики журналов OMS tooan.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-240">Many Azure services provide additional logs and telemetry that can be configured toosave data in your Azure Storage account, send tooEvent Hubs, and/or sent tooan OMS Log Analytics workspace.</span></span> <span data-ttu-id="ea1dc-241">Эта операция может выполняться только на уровне ресурсов и хранилища hello учетной записи или события концентратора должны присутствовать в hello же регионе, где целевой ресурс hello где hello диагностики настраивается.</span><span class="sxs-lookup"><span data-stu-id="ea1dc-241">That operation can only be performed at a resource level and hello storage account or event hub should be present in hello same region as hello target resource where hello diagnostics setting is configured.</span></span>

### <a name="get-diagnostic-setting"></a><span data-ttu-id="ea1dc-242">Получение параметра диагностики</span><span class="sxs-lookup"><span data-stu-id="ea1dc-242">Get diagnostic setting</span></span>
```PowerShell
Get-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp
```

<span data-ttu-id="ea1dc-243">Отключение параметра диагностики</span><span class="sxs-lookup"><span data-stu-id="ea1dc-243">Disable diagnostic setting</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $false
```

<span data-ttu-id="ea1dc-244">Включение параметра диагностики без периода удержания</span><span class="sxs-lookup"><span data-stu-id="ea1dc-244">Enable diagnostic setting without retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true
```

<span data-ttu-id="ea1dc-245">Включение параметра диагностики с периодом удержания</span><span class="sxs-lookup"><span data-stu-id="ea1dc-245">Enable diagnostic setting with retention</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Logic/workflows/andy0315logicapp -StorageAccountId /subscriptions/s1/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/mystorageaccount -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="ea1dc-246">Включение параметра диагностики с периодом удержания для определенной категории журналов</span><span class="sxs-lookup"><span data-stu-id="ea1dc-246">Enable diagnostic setting with retention for a specific log category</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/sakteststorage -Categories NetworkSecurityGroupEvent -Enable $true -RetentionEnabled $true -RetentionInDays 90
```

<span data-ttu-id="ea1dc-247">Включение параметра диагностики для концентратора событий</span><span class="sxs-lookup"><span data-stu-id="ea1dc-247">Enable diagnostic setting for Event Hubs</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Enable $true
```

<span data-ttu-id="ea1dc-248">Включение параметра диагностики для OMS</span><span class="sxs-lookup"><span data-stu-id="ea1dc-248">Enable diagnostic setting for OMS</span></span>

```PowerShell
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Network/networkSecurityGroups/viruela1 -WorkspaceId 76d785fd-d1ce-4f50-8ca3-858fc819ca0f -Enabled $true

```
