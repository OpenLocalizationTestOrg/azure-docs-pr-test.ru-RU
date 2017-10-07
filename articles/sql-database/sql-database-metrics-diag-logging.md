---
title: "aaaAzure SQL базы данных метрик и ведения журнала диагностики | Документы Microsoft"
description: "Сведения о настройке использования ресурсов toostore ресурсов базы данных SQL Azure, подключение и статистику выполнения запросов."
services: sql-database
documentationcenter: 
author: vvasic
manager: jhubbard
editor: 
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: vvasic
ms.openlocfilehash: e6f9e24992ca4f84f701e1ef858e98dc7b481e28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-metrics-and-diagnostics-logging"></a><span data-ttu-id="633db-103">Метрики и журналы диагностики базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="633db-103">Azure SQL Database metrics and diagnostics logging</span></span> 
<span data-ttu-id="633db-104">База данных SQL Azure может выдавать значения метрик и журналы диагностики для упрощения мониторинга.</span><span class="sxs-lookup"><span data-stu-id="633db-104">Azure SQL Database can emit metrics and diagnostic logs for easier monitoring.</span></span> <span data-ttu-id="633db-105">Можно настроить использование ресурсов toostore базы данных SQL Azure, сотрудников и сеансы и соединения до одного из этих ресурсов Azure:</span><span class="sxs-lookup"><span data-stu-id="633db-105">You can configure Azure SQL Database toostore resource usage, workers and sessions, and connectivity into one of these Azure resources:</span></span>
- <span data-ttu-id="633db-106">**Служба хранилища Azure**: для архивации больших объемов телеметрии по оптимальной стоимости.</span><span class="sxs-lookup"><span data-stu-id="633db-106">**Azure Storage**: For archiving vast amounts of telemetry for a small price</span></span>
- <span data-ttu-id="633db-107">**Концентратор событий Azure**: для интеграции телеметрии базы данных SQL Azure с настраиваемым решением для мониторинга или горячими конвейерами.</span><span class="sxs-lookup"><span data-stu-id="633db-107">**Azure Event Hub**: For integrating Azure SQL Database telemetry with your custom monitoring solution or hot pipelines</span></span>
- <span data-ttu-id="633db-108">**Azure Log Analytics**: для стандартной hello решением с отчетов, предупреждения и устранения возможности для мониторинга</span><span class="sxs-lookup"><span data-stu-id="633db-108">**Azure Log Analytics**: For out of hello box monitoring solution with reporting, alerting, and mitigating capabilities</span></span> 

    ![архитектура](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="enable-logging"></a><span data-ttu-id="633db-110">Включение ведения журналов</span><span class="sxs-lookup"><span data-stu-id="633db-110">Enable logging</span></span>

<span data-ttu-id="633db-111">Метрики и журналы диагностики не включены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="633db-111">Metrics and diagnostics logging is not enabled by default.</span></span> <span data-ttu-id="633db-112">Можно включить и управлять метрик и ведения журнала диагностики с помощью одного из следующих методов hello:</span><span class="sxs-lookup"><span data-stu-id="633db-112">You can enable and manage metrics and diagnostics logging using one of hello following methods:</span></span>
- <span data-ttu-id="633db-113">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="633db-113">Azure portal</span></span>
- <span data-ttu-id="633db-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="633db-114">PowerShell</span></span>
- <span data-ttu-id="633db-115">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="633db-115">Azure CLI</span></span>
- <span data-ttu-id="633db-116">Интерфейс REST API</span><span class="sxs-lookup"><span data-stu-id="633db-116">REST API</span></span> 
- <span data-ttu-id="633db-117">Шаблон Resource Manager</span><span class="sxs-lookup"><span data-stu-id="633db-117">Resource Manager template</span></span>

<span data-ttu-id="633db-118">При включении метрик и ведения журнала диагностики, необходимо toospecify hello ресурсов Azure, где собираются выбранных данных.</span><span class="sxs-lookup"><span data-stu-id="633db-118">When you enable metrics and diagnostics logging, you need toospecify hello Azure resource where selected data is collected.</span></span> <span data-ttu-id="633db-119">Доступны следующие варианты:</span><span class="sxs-lookup"><span data-stu-id="633db-119">Options available:</span></span>
- <span data-ttu-id="633db-120">Служба Log Analytics</span><span class="sxs-lookup"><span data-stu-id="633db-120">Log analytics</span></span>
- <span data-ttu-id="633db-121">Концентратор событий</span><span class="sxs-lookup"><span data-stu-id="633db-121">Event Hub</span></span>
- <span data-ttu-id="633db-122">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="633db-122">Azure Storage</span></span> 

<span data-ttu-id="633db-123">Вы можете подготовить новый ресурс Azure или выбрать имеющийся.</span><span class="sxs-lookup"><span data-stu-id="633db-123">You can provision a new Azure resource or select an existing resource.</span></span> <span data-ttu-id="633db-124">После выбора hello ресурса хранилища, необходимо toospecify какие toocollect данных.</span><span class="sxs-lookup"><span data-stu-id="633db-124">After selecting hello storage resource, you need toospecify which data toocollect.</span></span> <span data-ttu-id="633db-125">Доступны следующие варианты.</span><span class="sxs-lookup"><span data-stu-id="633db-125">Options available include:</span></span>

- <span data-ttu-id="633db-126">**[Метрики 1 минуты](sql-database-metrics-diag-logging.md#1-minute-metrics)** содержат сведения о проценте использования DTU, ограничении DTU, проценте использования ЦП, проценте чтения физических данных, проценте записей в журнал, проценте успешных, неудачных или заблокированных подключений брандмауэра, проценте сеансов, проценте рабочих ролей, хранилище, проценте хранилища, проценте хранилища XTP.</span><span class="sxs-lookup"><span data-stu-id="633db-126">**[1-minute metrics](sql-database-metrics-diag-logging.md#1-minute-metrics)** - contains DTU percentage, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage</span></span>

<span data-ttu-id="633db-127">Если указать учетную запись AzureStorage или концентратор событий, можно указать toospecify политики хранения данных, которые старше выбранного периода времени удаляется.</span><span class="sxs-lookup"><span data-stu-id="633db-127">If you specify Event Hub or an AzureStorage account, you can specify a retention policy toospecify that data that is older than a selected time period is deleted.</span></span> <span data-ttu-id="633db-128">При указании анализа журналов hello политики хранения зависит от hello выбранная Ценовая категория.</span><span class="sxs-lookup"><span data-stu-id="633db-128">If you specify Log Analytics, hello retention policy depends on hello selected pricing tier.</span></span> <span data-ttu-id="633db-129">Узнайте больше о [ценах на Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics/).</span><span class="sxs-lookup"><span data-stu-id="633db-129">Read more about [Log Analytics pricing](https://azure.microsoft.com/pricing/details/log-analytics/).</span></span> 

<span data-ttu-id="633db-130">Рекомендуется прочитать обоих hello [Обзор метрик в Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) и [Обзор служб Azure журналам диагностики](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) статьи, посвященные toogain понимание не только как tooenable ведения журналов, но hello метрики и журнала категории поддерживается hello различных служб Azure.</span><span class="sxs-lookup"><span data-stu-id="633db-130">We recommend that you read both hello [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles toogain an understanding of not only how tooenable logging, but hello metrics and log categories supported by hello various Azure services.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="633db-131">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="633db-131">Azure portal</span></span>

<span data-ttu-id="633db-132">метрики tooenable и журналы диагностики в hello портал Azure перейдите базы данных Azure SQL tooyour или эластичный пул страниц и нажмите кнопку **параметров диагностики**.</span><span class="sxs-lookup"><span data-stu-id="633db-132">tooenable metrics and diagnostic logs collection in hello Azure portal, navigate tooyour Azure SQL database or elastic pool page, and then click **Diagnostic settings**.</span></span>

   ![включить в hello портал Azure](./media/sql-database-metrics-diag-logging/enable-portal.png)

### <a name="powershell"></a><span data-ttu-id="633db-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="633db-134">PowerShell</span></span>

<span data-ttu-id="633db-135">tooenable метрик и ведения журнала диагностики с помощью PowerShell, используйте hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="633db-135">tooenable metrics and diagnostics logging using PowerShell, use hello following commands:</span></span>

- <span data-ttu-id="633db-136">хранение tooenable в журналах диагностики в учетную запись хранилища, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="633db-136">tooenable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   <span data-ttu-id="633db-137">Hello идентификатор учетной записи хранилища — идентификатор ресурса hello, для журналов toowhich учетной записи хранилища hello, требуется toosend hello.</span><span class="sxs-lookup"><span data-stu-id="633db-137">hello Storage Account ID is hello resource id for hello storage account toowhich you want toosend hello logs.</span></span>

- <span data-ttu-id="633db-138">tooenable потоковую передачу журналов диагностики tooan концентратора событий, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="633db-138">tooenable streaming of Diagnostic Logs tooan Event Hub, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   <span data-ttu-id="633db-139">Hello ИД правила Service Bus представляет собой строку следующего формата:</span><span class="sxs-lookup"><span data-stu-id="633db-139">hello Service Bus Rule ID is a string with this format:</span></span>

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- <span data-ttu-id="633db-140">tooenable отправки журналов диагностики рабочей области аналитики журналов tooa, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="633db-140">tooenable sending of Diagnostic Logs tooa Log Analytics workspace, use this command:</span></span>

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
   ```

- <span data-ttu-id="633db-141">Вы можете получить идентификатор ресурса hello рабочей области аналитики журналов с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="633db-141">You can obtain hello resource id of your Log Analytics workspace using hello following command:</span></span>

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

<span data-ttu-id="633db-142">Эти параметры tooenable можно объединить несколько параметров вывода.</span><span class="sxs-lookup"><span data-stu-id="633db-142">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="cli"></a><span data-ttu-id="633db-143">Интерфейс командной строки</span><span class="sxs-lookup"><span data-stu-id="633db-143">CLI</span></span>

<span data-ttu-id="633db-144">метрики tooenable и с помощью ведения журнала диагностики hello Azure CLI, hello используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="633db-144">tooenable metrics and diagnostics logging using hello Azure CLI, use hello following commands:</span></span>

- <span data-ttu-id="633db-145">хранение tooenable в журналах диагностики в учетную запись хранилища, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="633db-145">tooenable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   <span data-ttu-id="633db-146">Hello идентификатор учетной записи хранилища — идентификатор ресурса hello, для журналов toowhich учетной записи хранилища hello, требуется toosend hello.</span><span class="sxs-lookup"><span data-stu-id="633db-146">hello Storage Account ID is hello resource id for hello storage account toowhich you want toosend hello logs.</span></span>

- <span data-ttu-id="633db-147">tooenable потоковую передачу журналов диагностики tooan концентратора событий, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="633db-147">tooenable streaming of Diagnostic Logs tooan Event Hub, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   <span data-ttu-id="633db-148">Hello ИД правила Service Bus представляет собой строку следующего формата:</span><span class="sxs-lookup"><span data-stu-id="633db-148">hello Service Bus Rule ID is a string with this format:</span></span>

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- <span data-ttu-id="633db-149">tooenable отправки журналов диагностики рабочей области аналитики журналов tooa, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="633db-149">tooenable sending of Diagnostic Logs tooa Log Analytics workspace, use this command:</span></span>

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
   ```

<span data-ttu-id="633db-150">Эти параметры tooenable можно объединить несколько параметров вывода.</span><span class="sxs-lookup"><span data-stu-id="633db-150">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="rest-api"></a><span data-ttu-id="633db-151">Интерфейс REST API</span><span class="sxs-lookup"><span data-stu-id="633db-151">REST API</span></span>

<span data-ttu-id="633db-152">Дополнительные сведения см. слишком[изменения параметров диагностики с помощью API REST Azure монитор hello](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="633db-152">Read about how too[change Diagnostic settings using hello Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> 

### <a name="resource-manager-template"></a><span data-ttu-id="633db-153">Шаблон Resource Manager</span><span class="sxs-lookup"><span data-stu-id="633db-153">Resource Manager template</span></span>

<span data-ttu-id="633db-154">Дополнительные сведения см. слишком[Включение параметров диагностики при создании ресурса, с помощью шаблона диспетчера ресурсов](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span><span class="sxs-lookup"><span data-stu-id="633db-154">Read about how too[enable Diagnostic settings at resource creation using Resource Manager template](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md).</span></span> 

## <a name="stream-into-log-analytics"></a><span data-ttu-id="633db-155">Поток в службе Log Analytics</span><span class="sxs-lookup"><span data-stu-id="633db-155">Stream into Log Analytics</span></span> 
<span data-ttu-id="633db-156">Azure метрики базы данных SQL и журналы диагностики может передаваться в службе анализа журналов с помощью параметра встроенных «отправить tooLog аналитика» hello, портале hello, или путем включения аналитики журналов в параметрах диагностики через командлеты Azure PowerShell, Azure CLI или монитор REST Azure API-ИНТЕРФЕЙС.</span><span class="sxs-lookup"><span data-stu-id="633db-156">Azure SQL Database metrics and diagnostic logs can be streamed into Log Analytics using hello built-in “Send tooLog Analytics” option in hello portal, or by enabling Log Analytics in a diagnostic setting via Azure PowerShell cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="installation-overview"></a><span data-ttu-id="633db-157">Обзор установки</span><span class="sxs-lookup"><span data-stu-id="633db-157">Installation overview</span></span>

<span data-ttu-id="633db-158">Мониторинг транспортной карты базы данных SQL Azure упрощен благодаря службе Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="633db-158">Monitoring Azure SQL Database fleet is simple with Log Analytics.</span></span> <span data-ttu-id="633db-159">Необходимо выполнить три шага:</span><span class="sxs-lookup"><span data-stu-id="633db-159">Three steps are required:</span></span>

1.  <span data-ttu-id="633db-160">Создание ресурса Log Analytics</span><span class="sxs-lookup"><span data-stu-id="633db-160">Create Log Analytics resource</span></span>
2.  <span data-ttu-id="633db-161">Настройка метрики toorecord баз данных и журналов диагностики в hello создана служба аналитики журналов</span><span class="sxs-lookup"><span data-stu-id="633db-161">Configure databases toorecord metrics and diagnostic logs into hello created Log Analytics</span></span>
3.  <span data-ttu-id="633db-162">Установить решение **Аналитика SQL Azure** из коллекции в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="633db-162">Install **Azure SQL Analytics** solution from gallery in Log Analytics</span></span>

### <a name="create-log-analytics-resource"></a><span data-ttu-id="633db-163">Создание ресурса Log Analytics</span><span class="sxs-lookup"><span data-stu-id="633db-163">Create Log Analytics resource</span></span>

1. <span data-ttu-id="633db-164">Нажмите кнопку **New** в левом меню hello.</span><span class="sxs-lookup"><span data-stu-id="633db-164">Click **New** in hello left-hand menu.</span></span>
2. <span data-ttu-id="633db-165">Щелкните **Monitoring + Management** (Мониторинг и управление).</span><span class="sxs-lookup"><span data-stu-id="633db-165">Click **Monitoring + Management**</span></span>
3. <span data-ttu-id="633db-166">Щелкните **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="633db-166">Click **Log Analytics**</span></span>
4. <span data-ttu-id="633db-167">Заполнить hello Дополнительные сведения, необходимые в форме аналитики журналов hello: имя рабочей области, подписки, группы ресурсов, расположение и ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="633db-167">Fill in hello Log Analytics form with hello additional information required: workspace name, subscription, resource group, location, and pricing tier.</span></span>

   ![Служба Log Analytics](./media/sql-database-metrics-diag-logging/log-analytics.png)

### <a name="configure-databases-toorecord-metrics-and-diagnostic-logs"></a><span data-ttu-id="633db-169">Настройка метрик toorecord баз данных и журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="633db-169">Configure databases toorecord metrics and diagnostic logs</span></span>

<span data-ttu-id="633db-170">простым способом tooconfigure Hello где баз данных записать их показатели выполняется с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="633db-170">hello easiest way tooconfigure where databases record their metrics is through hello Azure portal.</span></span> <span data-ttu-id="633db-171">В hello портал Azure, перейдите tooyour ресурсов базы данных SQL Azure и нажмите кнопку **параметры диагностики**.</span><span class="sxs-lookup"><span data-stu-id="633db-171">In hello Azure portal, navigate tooyour Azure SQL Database resource and click **Diagnostics settings**.</span></span> 

### <a name="install-hello-azure-sql-analytics-solution-from-gallery"></a><span data-ttu-id="633db-172">Установка решения hello аналитики SQL Azure из коллекции</span><span class="sxs-lookup"><span data-stu-id="633db-172">Install hello Azure SQL Analytics solution from gallery</span></span>  

1. <span data-ttu-id="633db-173">После hello ресурсов анализа журналов и данных передается ее установки решения для анализа SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="633db-173">Once hello Log Analytics resource is created and your data is flowing into it, install Azure SQL Analytics solution.</span></span> <span data-ttu-id="633db-174">Это можно сделать с помощью hello **коллекции решений** , можно найти на домашней странице OMS hello и в боковом меню hello.</span><span class="sxs-lookup"><span data-stu-id="633db-174">This can be done through hello **Solutions Gallery** that you can find on hello OMS homepage and in hello side menu.</span></span> <span data-ttu-id="633db-175">В галерее hello, найдите и щелкните **SQL Azure Analytics** решения и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="633db-175">In hello gallery, find and click **Azure SQL Analytics** solution and click **Add**.</span></span>

   ![решение мониторинга](./media/sql-database-metrics-diag-logging/monitoring-solution.png)

2. <span data-ttu-id="633db-177">На домашней странице OMS появится новая плитка под названием **Аналитика SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="633db-177">On your OMS homepage, a new tile called **Azure SQL Analytics** appears.</span></span> <span data-ttu-id="633db-178">При выборе этой плитки откроется панель SQL Azure Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="633db-178">Selecting this tile opens hello Azure SQL Analytics dashboard.</span></span>

### <a name="using-azure-sql-analytics-solution"></a><span data-ttu-id="633db-179">Использование решения "Аналитика SQL Azure"</span><span class="sxs-lookup"><span data-stu-id="633db-179">Using Azure SQL Analytics Solution</span></span>

<span data-ttu-id="633db-180">Аналитика SQL Azure имеет иерархическую панель мониторинга, которая позволяет вам toonavigate через иерархию hello ресурсов базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="633db-180">Azure SQL Analytics is a hierarchical dashboard that allows you toonavigate through hello hierarchy of Azure SQL Database resources.</span></span> <span data-ttu-id="633db-181">Эта возможность позволяет вам toodo высокого уровня мониторинга но он также позволяет tooscope вашей мониторинга toojust hello правый набор ресурсов.</span><span class="sxs-lookup"><span data-stu-id="633db-181">This capability enables you toodo high-level monitoring but it also enables you tooscope your monitoring toojust hello right set of resources.</span></span>
<span data-ttu-id="633db-182">Панель мониторинга содержит списки hello разных ресурсов в рамках hello выбранного ресурса.</span><span class="sxs-lookup"><span data-stu-id="633db-182">Dashboard contains hello lists of different resources under hello selected resource.</span></span> <span data-ttu-id="633db-183">Например, для выбранной подписки можно увидеть hello все серверы, эластичные пулы и базы данных, принадлежащие toohello выбранной подписки.</span><span class="sxs-lookup"><span data-stu-id="633db-183">For example, for a selected subscription you can see hello all servers, elastic pools and databases that belong toohello selected subscription.</span></span> <span data-ttu-id="633db-184">Кроме того для пулов эластичных и баз данных, можно просмотреть метрики использования ресурсов hello этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="633db-184">Additionally, for Elastic Pools and databases, you can see hello resource usage metrics of that resource.</span></span> <span data-ttu-id="633db-185">Сюда входят диаграммы для DTU, ЦП, операций ввода-вывода, операций записи в журнал, сеансов, рабочих ролей, подключений и объема хранилища в ГБ.</span><span class="sxs-lookup"><span data-stu-id="633db-185">This includes charts for DTU, CPU, IO, LOG, sessions, workers, connections, and storage in GB.</span></span>

## <a name="stream-into-azure-event-hub"></a><span data-ttu-id="633db-186">Потоковая передача в концентратор событий Azure</span><span class="sxs-lookup"><span data-stu-id="633db-186">Stream into Azure Event Hub</span></span>

<span data-ttu-id="633db-187">Azure метрики базы данных SQL и журналы диагностики может передаваться в концентратор событий с помощью параметра встроенных «поток tooan концентратор событий» hello, hello портала или включив ИД правила Service Bus в параметрах диагностики через командлеты PowerShell Azure, Azure CLI или монитор REST Azure API-ИНТЕРФЕЙС.</span><span class="sxs-lookup"><span data-stu-id="633db-187">Azure SQL Database metrics and diagnostic logs can be streamed into Event Hub using hello built-in “Stream tooan event hub” option in hello portal, or by enabling Service Bus Rule Id in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span> 

### <a name="what-toodo-with-metrics-and-diagnostic-logs-in-event-hub"></a><span data-ttu-id="633db-188">Какие toodo с показателями и в журналах диагностики в концентратор событий?</span><span class="sxs-lookup"><span data-stu-id="633db-188">What toodo with metrics and diagnostic logs in Event Hub?</span></span>
<span data-ttu-id="633db-189">После hello выбранных данных поступает в концентратор событий, существует один подробный tooenabling шаг сложных сценариях мониторинга.</span><span class="sxs-lookup"><span data-stu-id="633db-189">Once hello selected data is streamed into Event Hub, you are one step closer tooenabling advanced monitoring scenarios.</span></span> <span data-ttu-id="633db-190">Концентраторов событий действует как hello «дверью» для конвейера событий и сбора данных в концентратор событий, он может преобразовываться и сохраненных с помощью любого поставщика аналитика в реальном времени или адаптеры пакетной обработки хранилища.</span><span class="sxs-lookup"><span data-stu-id="633db-190">Event Hubs acts as hello "front door" for an event pipeline, and once data is collected into an Event Hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="633db-191">Концентраторы событий отделяет hello рабочего потока событий из hello использования этих событий, чтобы потребители событий можно получать доступ к событиям hello по собственному расписанию.</span><span class="sxs-lookup"><span data-stu-id="633db-191">Event Hubs decouples hello production of a stream of events from hello consumption of those events, so that event consumers can access hello events on their own schedule.</span></span> <span data-ttu-id="633db-192">Дополнительные сведения о концентраторе событий см. в статьях:</span><span class="sxs-lookup"><span data-stu-id="633db-192">For more information on Event Hub, see:</span></span>

- <span data-ttu-id="633db-193">[Что такое концентраторы событий Azure?](../event-hubs/event-hubs-what-is-event-hubs.md)</span><span class="sxs-lookup"><span data-stu-id="633db-193">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
- [<span data-ttu-id="633db-194">Приступая к работе с концентраторами событий</span><span class="sxs-lookup"><span data-stu-id="633db-194">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)


<span data-ttu-id="633db-195">Вот лишь несколько способов, которые можно использовать возможность потоковой передачи hello.</span><span class="sxs-lookup"><span data-stu-id="633db-195">Here are just a few ways you might use hello streaming capability:</span></span>

-   <span data-ttu-id="633db-196">Служба работоспособности при потоковой передаче данных «Горячий путь» tooPowerBI - с помощью концентраторов событий, Stream Analytics и PowerBI, можно легко преобразовать метрики и диагностики данных почти в реальном времени аналитики для служб Azure.</span><span class="sxs-lookup"><span data-stu-id="633db-196">View service health by streaming “hot path” data tooPowerBI - Using Event Hubs, Stream Analytics, and PowerBI, you can easily transform your metrics and diagnostics data into near real-time insights on your Azure services.</span></span> <span data-ttu-id="633db-197">Обзор как tooset копирование концентраторов событий обработки данных с Stream Analytics и использовать PowerBI в качестве выходных данных. в разделе [Stream Analytics и Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="633db-197">For an overview of how tooset up an Event Hubs, process data with Stream Analytics, and use PowerBI as an output, see [Stream Analytics and Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md).</span></span>
-   <span data-ttu-id="633db-198">Поток журналы сторонних toothird ведение журнала и телеметрии потоки — концентраторов событий с помощью потоковой передачи, вы можно получить метрики и журналы диагностики в toodifferent аналитические решения сторонних мониторинга и журнала.</span><span class="sxs-lookup"><span data-stu-id="633db-198">Stream logs toothird-party logging and telemetry streams – Using Event Hubs streaming you can get your metrics and diagnostic logs in toodifferent third-party monitoring and log analytics solutions.</span></span> 
-   <span data-ttu-id="633db-199">Построение пользовательского телеметрии и платформ ведения журнала — платформа пользовательские телеметрии или уже являются мысли о построении один hello высокомасштабируемых публикации подписки характер концентраторов событий позволяет tooflexibly приема журналы диагностики.</span><span class="sxs-lookup"><span data-stu-id="633db-199">Build a custom telemetry and logging platform – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest diagnostic logs.</span></span> <span data-ttu-id="633db-200">В разделе [toousing руководство Dan Rosanova концентраторов событий на платформе телеметрии масштабе](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span><span class="sxs-lookup"><span data-stu-id="633db-200">See [Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/).</span></span>

## <a name="stream-into-azure-storage"></a><span data-ttu-id="633db-201">Потоковая передача в службу хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="633db-201">Stream into Azure Storage</span></span>

<span data-ttu-id="633db-202">Azure метрики базы данных SQL и журналы диагностики могут храниться в хранилище Azure с помощью hello встроенный параметр «Архивировать tooa учетной записи хранения» в hello портал Azure или путем включения хранилища Azure в параметрах диагностики через командлеты PowerShell Azure, Azure или Azure CLI Монитор API REST.</span><span class="sxs-lookup"><span data-stu-id="633db-202">Azure SQL Database metrics and diagnostic logs can be stored into Azure Storage using hello built-in "Archive tooa storage account” option in hello Azure portal, or by enabling Azure Storage in a diagnostic setting via Azure PowerShell Cmdlets, Azure CLI, or Azure Monitor REST API.</span></span>

### <a name="schema-of-metrics-and-diagnostic-logs-in-hello-storage-account"></a><span data-ttu-id="633db-203">Схема метрик и в журналах диагностики в учетной записи хранилища hello</span><span class="sxs-lookup"><span data-stu-id="633db-203">Schema of metrics and diagnostic logs in hello storage account</span></span>

<span data-ttu-id="633db-204">После настройки метрики и журналы диагностики, контейнер хранилища создается в учетной записи хранения hello, заданные при hello первой строки данных недоступны.</span><span class="sxs-lookup"><span data-stu-id="633db-204">Once you have set up metrics and diagnostic logs collection, a storage container is created in hello storage account you selected when hello first rows of data are available.</span></span> <span data-ttu-id="633db-205">Эти большие двоичные объекты Hello структура выглядит:</span><span class="sxs-lookup"><span data-stu-id="633db-205">hello structure of these blobs is:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ databases/{database_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```
    
<span data-ttu-id="633db-206">Или даже еще проще:</span><span class="sxs-lookup"><span data-stu-id="633db-206">Or, more simply:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

<span data-ttu-id="633db-207">Например, большой двоичный объект метрики 1 минуты может иметь такое имя:</span><span class="sxs-lookup"><span data-stu-id="633db-207">For example, a blob name for 1-minute metrics might be:</span></span>

```powershell
insights-metrics-minute/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.SQL/ servers/Server1/databases/database1/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

<span data-ttu-id="633db-208">В случае, если вам нужны данные hello toorecord из hello эластичного пула, имя BLOB-объекта немного отличается.</span><span class="sxs-lookup"><span data-stu-id="633db-208">In case you want toorecord hello data from hello Elastic Pool, blob name is a bit different:</span></span>

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ elasticPools/{elastic_pool_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

### <a name="download-metrics-and-logs-from-azure-storage"></a><span data-ttu-id="633db-209">Загрузка метрик и журналов из службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="633db-209">Download metrics and logs from Azure storage</span></span>

<span data-ttu-id="633db-210">Ознакомьтесь с разделом [Скачивание больших двоичных объектов](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs).</span><span class="sxs-lookup"><span data-stu-id="633db-210">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>

## <a name="1-minute-metrics"></a><span data-ttu-id="633db-211">Метрики 1 минуты</span><span class="sxs-lookup"><span data-stu-id="633db-211">1-minute metrics</span></span>

| |  |
|---|---|
|<span data-ttu-id="633db-212">**Ресурс**</span><span class="sxs-lookup"><span data-stu-id="633db-212">**Resource**</span></span>|<span data-ttu-id="633db-213">**Метрики**</span><span class="sxs-lookup"><span data-stu-id="633db-213">**Metrics**</span></span>|
|<span data-ttu-id="633db-214">База данных</span><span class="sxs-lookup"><span data-stu-id="633db-214">Database</span></span>|<span data-ttu-id="633db-215">Сведения о проценте использования DTU, используемых единицах DTU, ограничении DTU, проценте использования ЦП, проценте чтения физических данных, проценте записей в журнал, проценте успешных, неудачных или заблокированных подключений брандмауэра, проценте сеансов, проценте рабочих ролей, хранилище, проценте хранилища, проценте хранилища XTP, взаимоблокировках</span><span class="sxs-lookup"><span data-stu-id="633db-215">DTU percentage, DTU used, DTU limit, CPU percentage, Physical data read percentage, Log write percentage, Successful/Failed/Blocked by firewall connections, sessions percentage, workers percentage, storage, storage percentage, XTP storage percentage, deadlocks</span></span> |
|<span data-ttu-id="633db-216">Эластичный пул</span><span class="sxs-lookup"><span data-stu-id="633db-216">Elastic pool</span></span>|<span data-ttu-id="633db-217">Сведения о проценте использования DTU, используемых единицах DTU, ограничении DTU, проценте использования ЦП, проценте чтения физических данных, проценте записей в журнал, проценте сеансов, проценте рабочих ролей, хранилище, проценте хранилища, ограничении хранилища, проценте хранилища XTP</span><span class="sxs-lookup"><span data-stu-id="633db-217">eDTU percentage, eDTU used, eDTU limit, CPU percentage, Physical data read percentage, Log write percentage, sessions percentage, workers percentage, storage, storage percentage, storage limit, XTP storage percentage</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="633db-218">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="633db-218">Next steps</span></span>

- <span data-ttu-id="633db-219">Чтение обоих hello [Обзор метрик в Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) и [Обзор служб Azure журналам диагностики](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) статьи, посвященные toogain понимание не только как tooenable ведения журнала, но hello метрик и журнала категорий поддерживается hello различных служб Azure.</span><span class="sxs-lookup"><span data-stu-id="633db-219">Read both hello [Overview of metrics in Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) and [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) articles toogain an understanding of not only how tooenable logging, but hello metrics and log categories supported by hello various Azure services.</span></span>
- <span data-ttu-id="633db-220">Прочтите эти toolearn статьи о концентраторах событий:</span><span class="sxs-lookup"><span data-stu-id="633db-220">Read these articles toolearn about event hubs:</span></span>
   - <span data-ttu-id="633db-221">[Что такое концентраторы событий Azure?](../event-hubs/event-hubs-what-is-event-hubs.md)</span><span class="sxs-lookup"><span data-stu-id="633db-221">[What are Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)?</span></span>
   - [<span data-ttu-id="633db-222">Начало работы с концентраторами событий</span><span class="sxs-lookup"><span data-stu-id="633db-222">Get started with Event Hubs</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- <span data-ttu-id="633db-223">Ознакомьтесь с разделом [Скачивание больших двоичных объектов](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs).</span><span class="sxs-lookup"><span data-stu-id="633db-223">See [Download metrics and diagnostic logs from Azure Storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)</span></span>
