---
title: "оповещения aaaCreate для служб Azure - PowerShell | Документы Microsoft"
description: "Триггер сообщения электронной почты, уведомления, вызовите URL-адреса веб-сайтов (веб-перехватчиков) или автоматизации при соблюдении заданных условий hello."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d26ab15b-7b7e-42a9-81c8-3ce9ead5d252
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: robb
ms.openlocfilehash: 80d3a3f194fc6a5a09a81d04206ea7a1640bddb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a><span data-ttu-id="ebd25-103">Создание оповещений метрик в Azure Monitor для служб Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ebd25-103">Create metric alerts in Azure Monitor for Azure services - PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ebd25-104">Портал</span><span class="sxs-lookup"><span data-stu-id="ebd25-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="ebd25-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ebd25-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="ebd25-106">ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ</span><span class="sxs-lookup"><span data-stu-id="ebd25-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="ebd25-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="ebd25-107">Overview</span></span>
<span data-ttu-id="ebd25-108">В этой статье показано, как tooset копирование Azure метрики оповещений с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ebd25-108">This article shows you how tooset up Azure metric alerts using PowerShell.</span></span>  

<span data-ttu-id="ebd25-109">Вы можете получать оповещения на основе отслеживания метрик или событий в службах Azure.</span><span class="sxs-lookup"><span data-stu-id="ebd25-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="ebd25-110">**Значения метрик** - hello предупредить триггеры hello значение указанной метрики пересекает пороговое значение, присваиваемое в любом направлении.</span><span class="sxs-lookup"><span data-stu-id="ebd25-110">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="ebd25-111">То есть, и триггеров при hello сначала условия, и затем позже при, условия больше не выполнены.</span><span class="sxs-lookup"><span data-stu-id="ebd25-111">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="ebd25-112">**События журнала действий**. Оповещение может активироваться при *каждом* событии или только тогда, когда выполняются определенные события.</span><span class="sxs-lookup"><span data-stu-id="ebd25-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="ebd25-113">Дополнительные сведения об активности журнала предупреждений toolearn [щелкните здесь](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="ebd25-113">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="ebd25-114">Вы можете настроить метрики оповещений toodo hello следующие при инициировании:</span><span class="sxs-lookup"><span data-stu-id="ebd25-114">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="ebd25-115">Отправить администратору службы toohello уведомлений электронной почты и соадминистраторы</span><span class="sxs-lookup"><span data-stu-id="ebd25-115">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="ebd25-116">Отправьте по электронной почте tooadditional сообщений электронной почты, указанных вами.</span><span class="sxs-lookup"><span data-stu-id="ebd25-116">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="ebd25-117">вызов webhook;</span><span class="sxs-lookup"><span data-stu-id="ebd25-117">call a webhook</span></span>
* <span data-ttu-id="ebd25-118">Запустите выполнение runbook для Azure (только из hello портал Azure)</span><span class="sxs-lookup"><span data-stu-id="ebd25-118">start execution of an Azure runbook (only from hello Azure portal)</span></span>

<span data-ttu-id="ebd25-119">Для настройки правил генерации оповещений и получении сведений о них можно использовать:</span><span class="sxs-lookup"><span data-stu-id="ebd25-119">You can configure and get information about alert rules using</span></span>

* [<span data-ttu-id="ebd25-120">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="ebd25-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="ebd25-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ebd25-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="ebd25-122">интерфейс командной строки (CLI)</span><span class="sxs-lookup"><span data-stu-id="ebd25-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="ebd25-123">Azure Monitor REST API</span><span class="sxs-lookup"><span data-stu-id="ebd25-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="ebd25-124">Дополнительные сведения, всегда можно ввести ```Get-Help``` и затем hello команду PowerShell, требуется получить справку.</span><span class="sxs-lookup"><span data-stu-id="ebd25-124">For additional information, you can always type ```Get-Help``` and then hello PowerShell command you want help on.</span></span>

## <a name="create-alert-rules-in-powershell"></a><span data-ttu-id="ebd25-125">Создание правил генерации оповещений в PowerShell</span><span class="sxs-lookup"><span data-stu-id="ebd25-125">Create alert rules in PowerShell</span></span>
1. <span data-ttu-id="ebd25-126">Войдите в tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ebd25-126">Log in tooAzure.</span></span>   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. <span data-ttu-id="ebd25-127">Получить список подписок hello достаточно.</span><span class="sxs-lookup"><span data-stu-id="ebd25-127">Get a list of hello subscriptions you have available.</span></span> <span data-ttu-id="ebd25-128">Убедитесь, что вы работаете с hello правильные подписка.</span><span class="sxs-lookup"><span data-stu-id="ebd25-128">Verify that you are working with hello right subscription.</span></span> <span data-ttu-id="ebd25-129">Если нет, присвойте ему значение toohello вправо на один с выходными данными hello `Get-AzureRmSubscription`.</span><span class="sxs-lookup"><span data-stu-id="ebd25-129">If not, set it toohello right one using hello output from `Get-AzureRmSubscription`.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. <span data-ttu-id="ebd25-130">toolist существующие правила в группе ресурсов, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ebd25-130">toolist existing rules on a resource group, use hello following command:</span></span>

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. <span data-ttu-id="ebd25-131">toocreate правило, требуется toohave несколько важных аспекта сведений сначала.</span><span class="sxs-lookup"><span data-stu-id="ebd25-131">toocreate a rule, you need toohave several important pieces of information first.</span></span>

  * <span data-ttu-id="ebd25-132">Hello **идентификатор ресурса** для hello ресурса требуется tooset оповещение для</span><span class="sxs-lookup"><span data-stu-id="ebd25-132">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="ebd25-133">Hello **определения показателей** доступны для этого ресурса</span><span class="sxs-lookup"><span data-stu-id="ebd25-133">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="ebd25-134">Одним из способов tooget hello идентификатор ресурса — toouse hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ebd25-134">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="ebd25-135">Предположим, что ресурс hello уже создан, выберите его в портал hello.</span><span class="sxs-lookup"><span data-stu-id="ebd25-135">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="ebd25-136">Выберите в колонке Далее hello *свойства* под hello *параметры* раздела.</span><span class="sxs-lookup"><span data-stu-id="ebd25-136">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="ebd25-137">**Идентификатор РЕСУРСА** — это поле в колонке Далее hello.</span><span class="sxs-lookup"><span data-stu-id="ebd25-137">**RESOURCE ID** is a field in hello next blade.</span></span> <span data-ttu-id="ebd25-138">Другим способом является toouse hello [обозревателя ресурсов Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ebd25-138">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="ebd25-139">Ниже приведен пример идентификатора ресурса для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ebd25-139">An example Resource ID for a web app is</span></span>

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="ebd25-140">Можно использовать `Get-AzureRmMetricDefinition` список hello tooview все определения показателей для конкретного ресурса.</span><span class="sxs-lookup"><span data-stu-id="ebd25-140">You can use `Get-AzureRmMetricDefinition` tooview hello list of all metric definitions for a specific resource.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     <span data-ttu-id="ebd25-141">Hello следующий пример создает таблицу с метрикой hello имя и hello единицы для этой метрики.</span><span class="sxs-lookup"><span data-stu-id="ebd25-141">hello following example generates a table with hello metric Name and hello Unit for that metric.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     <span data-ttu-id="ebd25-142">Полный список доступных параметров Get-AzureRmMetricDefinition можно получить, выполнив Get-MetricDefinitions.</span><span class="sxs-lookup"><span data-stu-id="ebd25-142">A full list of available options for Get-AzureRmMetricDefinition is available by running Get-MetricDefinitions.</span></span>
5. <span data-ttu-id="ebd25-143">Здравствуйте, следующий пример настраивает оповещение на ресурс веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="ebd25-143">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="ebd25-144">Hello предупреждения триггеры всякий раз, когда постоянно получает любой трафик, 5 минут, и снова при получении трафика на 5 минут.</span><span class="sxs-lookup"><span data-stu-id="ebd25-144">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. <span data-ttu-id="ebd25-145">toocreate веб-перехватчик или отправить электронную почту, если оповещение триггерами, сначала создайте hello электронной почты и/или веб-привязок.</span><span class="sxs-lookup"><span data-stu-id="ebd25-145">toocreate webhook or send email when an alert triggers, first create hello email and/or webhooks.</span></span> <span data-ttu-id="ebd25-146">Немедленно создайте правило hello позже с hello - тег действия и, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="ebd25-146">Then immediately create hello rule afterwards with hello -Actions tag and as shown in hello following example.</span></span> <span data-ttu-id="ebd25-147">С помощью PowerShell невозможно связать webhook или электронные адреса с уже созданными правилами.</span><span class="sxs-lookup"><span data-stu-id="ebd25-147">You cannot associate webhook or emails with already created rules via PowerShell.</span></span>

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. <span data-ttu-id="ebd25-148">tooverify, что оповещения были созданы правильно, просмотрев hello отдельных правил.</span><span class="sxs-lookup"><span data-stu-id="ebd25-148">tooverify that your alerts have been created properly by looking at hello individual rules.</span></span>

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. <span data-ttu-id="ebd25-149">Удалите свои оповещения.</span><span class="sxs-lookup"><span data-stu-id="ebd25-149">Delete your alerts.</span></span> <span data-ttu-id="ebd25-150">Эти команды удаляют hello правил, созданных ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="ebd25-150">These commands delete hello rules created previously in this article.</span></span>

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a><span data-ttu-id="ebd25-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ebd25-151">Next steps</span></span>
* <span data-ttu-id="ebd25-152">[Обзор мониторинг Azure](monitoring-overview.md) включая hello типы данных, можно собирать и контролировать.</span><span class="sxs-lookup"><span data-stu-id="ebd25-152">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="ebd25-153">Узнайте больше о [настройке веб-перехватчиков webhook в оповещениях](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="ebd25-153">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="ebd25-154">Узнайте больше о [настройке оповещений о событиях журнала действий](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="ebd25-154">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="ebd25-155">Узнайте больше о [модулях Runbook службы автоматизации Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="ebd25-155">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="ebd25-156">Получить [Обзор сбора журналов диагностики](monitoring-overview-of-diagnostic-logs.md) toocollect подробные показатели высокой частотой в службе.</span><span class="sxs-lookup"><span data-stu-id="ebd25-156">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="ebd25-157">Получить [Обзор сбора метрик](insights-how-to-customize-monitoring.md) toomake убедиться, что служба становится доступной и отвечать на запросы.</span><span class="sxs-lookup"><span data-stu-id="ebd25-157">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
