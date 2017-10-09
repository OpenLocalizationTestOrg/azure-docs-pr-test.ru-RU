---
title: "решения для анализа SQL в службе анализа журналов aaaAzure | Документы Microsoft"
description: "Hello решения для анализа SQL Azure позволяет управлять базами данных Azure SQL."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: b2712749-1ded-40c4-b211-abc51cc65171
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: fe228bb3cb3f9d578a84707c3917f02fbeb8a627
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a><span data-ttu-id="bb48d-103">Мониторинг базы данных SQL Azure с помощью служб анализа SQL Azure (предварительная версия) в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="bb48d-103">Monitor Azure SQL Database using Azure SQL Analytics (Preview) in Log Analytics</span></span>

![Символ службы "Аналитика SQL Azure"](./media/log-analytics-azure-sql/azure-sql-symbol.png)

<span data-ttu-id="bb48d-105">Hello решения для анализа SQL Azure в службе анализа журналов Azure собирает и отображает важные показатели производительности SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="bb48d-105">hello Azure SQL Analytics solution in Azure Log Analytics collects and visualizes important SQL Azure performance metrics.</span></span> <span data-ttu-id="bb48d-106">С помощью hello показателей, собираемых с решением hello, можно создать пользовательские правила наблюдения и оповещения.</span><span class="sxs-lookup"><span data-stu-id="bb48d-106">By using hello metrics that you collect with hello solution, you can create custom monitoring rules and alerts.</span></span> <span data-ttu-id="bb48d-107">Вы можете отслеживать метрики базы данных SQL Azure и эластичных пулов в нескольких подписках Azure и эластичных пулах, а также визуализировать их.</span><span class="sxs-lookup"><span data-stu-id="bb48d-107">And, you can monitor Azure SQL Database and elastic pool metrics across multiple Azure subscriptions and elastic pools and visualize them.</span></span> <span data-ttu-id="bb48d-108">Hello решение также помогает tooidentify проблемы на каждом уровне стека вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="bb48d-108">hello solution also helps you tooidentify issues at each layer of your application stack.</span></span>  <span data-ttu-id="bb48d-109">Она использует [метрики диагностики Azure](log-analytics-azure-storage.md) вместе с анализа журналов представления toopresent данные обо всех базах данных Azure SQL и пулах эластичных БД в одной рабочей области аналитики журналов.</span><span class="sxs-lookup"><span data-stu-id="bb48d-109">It uses [Azure Diagnostic metrics](log-analytics-azure-storage.md) together with Log Analytics views toopresent data about all your Azure SQL databases and elastic pools in a single Log Analytics workspace.</span></span>

<span data-ttu-id="bb48d-110">В настоящее время это решение Предварительная версия поддерживает до too150 000 баз данных SQL Azure и 5000 пулов эластичных SQL каждой рабочей области.</span><span class="sxs-lookup"><span data-stu-id="bb48d-110">Currently, this preview solution supports up too150,000 Azure SQL Databases and 5,000 SQL Elastic Pools per workspace.</span></span>

<span data-ttu-id="bb48d-111">Hello решения для анализа SQL Azure, как и другие доступные для анализа журналов позволяет отслеживать и получать уведомления о работоспособности hello ресурсам Azure — в данном случае база данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="bb48d-111">hello Azure SQL Analytics solution, like others available for Log Analytics, helps you monitor and receive notifications about hello health of your Azure resources—in this case, Azure SQL Database.</span></span> <span data-ttu-id="bb48d-112">База данных SQL Microsoft Azure является масштабируемой реляционной базы данных служба, предоставляющая знакомы tooapplications возможности SQL Server подобные, работающих в облаке Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bb48d-112">Microsoft Azure SQL Database is a scalable relational database service that provides familiar SQL-Server-like capabilities tooapplications running in hello Azure cloud.</span></span> <span data-ttu-id="bb48d-113">Аналитика журналов позволяет toocollect, корреляции и визуализировать структурированные и неструктурированные данные.</span><span class="sxs-lookup"><span data-stu-id="bb48d-113">Log Analytics helps you toocollect, correlate, and visualize structured and unstructured data.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="bb48d-114">Подключенные источники</span><span class="sxs-lookup"><span data-stu-id="bb48d-114">Connected sources</span></span>

<span data-ttu-id="bb48d-115">Hello решения для анализа SQL Azure не использует агенты tooconnect toohello службы анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="bb48d-115">hello Azure SQL Analytics solution doesn't use agents tooconnect toohello Log Analytics service.</span></span>

<span data-ttu-id="bb48d-116">Привет, в следующей таблице описываются hello подключенных источников, которые поддерживаются в этом решении.</span><span class="sxs-lookup"><span data-stu-id="bb48d-116">hello following table describes hello connected sources that are supported by this solution.</span></span>

| <span data-ttu-id="bb48d-117">Подключенный источник</span><span class="sxs-lookup"><span data-stu-id="bb48d-117">Connected Source</span></span> | <span data-ttu-id="bb48d-118">Поддержка</span><span class="sxs-lookup"><span data-stu-id="bb48d-118">Support</span></span> | <span data-ttu-id="bb48d-119">Описание</span><span class="sxs-lookup"><span data-stu-id="bb48d-119">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="bb48d-120">Агенты Windows</span><span class="sxs-lookup"><span data-stu-id="bb48d-120">Windows agents</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="bb48d-121">Нет</span><span class="sxs-lookup"><span data-stu-id="bb48d-121">No</span></span> | <span data-ttu-id="bb48d-122">Прямой агентов Windows hello решения не используются.</span><span class="sxs-lookup"><span data-stu-id="bb48d-122">Direct Windows agents are not used by hello solution.</span></span> |
| [<span data-ttu-id="bb48d-123">Агенты Linux</span><span class="sxs-lookup"><span data-stu-id="bb48d-123">Linux agents</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="bb48d-124">Нет</span><span class="sxs-lookup"><span data-stu-id="bb48d-124">No</span></span> | <span data-ttu-id="bb48d-125">Прямой агенты Linux не используются решением hello.</span><span class="sxs-lookup"><span data-stu-id="bb48d-125">Direct Linux agents are not used by hello solution.</span></span> |
| [<span data-ttu-id="bb48d-126">Группы управления SCOM</span><span class="sxs-lookup"><span data-stu-id="bb48d-126">SCOM management group</span></span>](log-analytics-om-agents.md) | <span data-ttu-id="bb48d-127">Нет</span><span class="sxs-lookup"><span data-stu-id="bb48d-127">No</span></span> | <span data-ttu-id="bb48d-128">Прямое подключение от tooLog агент SCOM hello Analytics решением hello не используется.</span><span class="sxs-lookup"><span data-stu-id="bb48d-128">A direct connection from hello SCOM agent tooLog Analytics is not used by hello solution.</span></span> |
| [<span data-ttu-id="bb48d-129">Учетная запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="bb48d-129">Azure storage account</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="bb48d-130">Нет</span><span class="sxs-lookup"><span data-stu-id="bb48d-130">No</span></span> | <span data-ttu-id="bb48d-131">Служба аналитики журналов не прочитать hello данные из учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="bb48d-131">Log Analytics does not read hello data from a storage account.</span></span> |
| [<span data-ttu-id="bb48d-132">Настройка системы диагностики Azure для входа в Application Insights</span><span class="sxs-lookup"><span data-stu-id="bb48d-132">Azure diagnostics</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="bb48d-133">Да</span><span class="sxs-lookup"><span data-stu-id="bb48d-133">Yes</span></span> | <span data-ttu-id="bb48d-134">Azure метрики данные отправляются tooLog Analytics непосредственно в Azure.</span><span class="sxs-lookup"><span data-stu-id="bb48d-134">Azure metric data is sent tooLog Analytics directly by Azure.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="bb48d-135">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bb48d-135">Prerequisites</span></span>

- <span data-ttu-id="bb48d-136">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="bb48d-136">An Azure Subscription.</span></span> <span data-ttu-id="bb48d-137">Если у вас ее нет, вы можете создать ее [бесплатно](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="bb48d-137">If you don't have one, you can create one for [free](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="bb48d-138">Рабочая область Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="bb48d-138">A Log Analytics workspace.</span></span> <span data-ttu-id="bb48d-139">Вы можете использовать имеющуюся рабочую область или же [создать ее](log-analytics-get-started.md), прежде чем начать использовать это решение.</span><span class="sxs-lookup"><span data-stu-id="bb48d-139">You can use an existing one, or you can [create a new one](log-analytics-get-started.md) before you start using this solution.</span></span>
- <span data-ttu-id="bb48d-140">Включение диагностики Azure для баз данных Azure SQL и эластичные пулы и [настроить их toosend их tooLog данных аналитики](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span><span class="sxs-lookup"><span data-stu-id="bb48d-140">Enable Azure Diagnostics for your Azure SQL databases and elastic pools and [configure them toosend their data tooLog Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span>

## <a name="configuration"></a><span data-ttu-id="bb48d-141">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="bb48d-141">Configuration</span></span>

<span data-ttu-id="bb48d-142">Выполните следующие шаги tooadd hello Azure SQL решения tooyour рабочей областью аналитики hello.</span><span class="sxs-lookup"><span data-stu-id="bb48d-142">Perform hello following steps tooadd hello Azure SQL Analytics solution tooyour workspace.</span></span>

1. <span data-ttu-id="bb48d-143">Добавление hello SQL Azure Analytics решения tooyour рабочей области из [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) или с помощью hello процесс, описанный в [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="bb48d-143">Add hello Azure SQL Analytics solution tooyour workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="bb48d-144">В hello портал Azure, щелкните **New** (hello символу "+"), hello выберите в списке ресурсов, **мониторинг + управления**.</span><span class="sxs-lookup"><span data-stu-id="bb48d-144">In hello Azure portal, click **New** (hello + symbol), then in hello list of resources, select **Monitoring + Management**.</span></span>  
    <span data-ttu-id="bb48d-145">![Мониторинг и управление](./media/log-analytics-azure-sql/monitoring-management.png)</span><span class="sxs-lookup"><span data-stu-id="bb48d-145">![Monitoring + Management](./media/log-analytics-azure-sql/monitoring-management.png)</span></span>
3. <span data-ttu-id="bb48d-146">В hello **мониторинг + управления** выберите **все**.</span><span class="sxs-lookup"><span data-stu-id="bb48d-146">In hello **Monitoring + Management** list click **See all**.</span></span>
4. <span data-ttu-id="bb48d-147">В hello **рекомендуется** выберите **дополнительные** и в новый список hello, найдите **аналитики SQL Azure (Предварительная версия)** и выберите его.</span><span class="sxs-lookup"><span data-stu-id="bb48d-147">In hello **Recommended** list, click **More** , and then in hello new list, find **Azure SQL Analytics (Preview)** and then select it.</span></span>  
    <span data-ttu-id="bb48d-148">![Решение служб анализа SQL Azure](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span><span class="sxs-lookup"><span data-stu-id="bb48d-148">![Azure SQL Analytics solution](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span></span>
5. <span data-ttu-id="bb48d-149">В hello **аналитики SQL Azure (Предварительная версия)** колонка, щелкните **создать**.</span><span class="sxs-lookup"><span data-stu-id="bb48d-149">In hello **Azure SQL Analytics (Preview)** blade, click **Create**.</span></span>  
    <span data-ttu-id="bb48d-150">![Создание](./media/log-analytics-azure-sql/portal-create.png)</span><span class="sxs-lookup"><span data-stu-id="bb48d-150">![Create](./media/log-analytics-azure-sql/portal-create.png)</span></span>
6. <span data-ttu-id="bb48d-151">В hello **Создание нового решения** колонки, рабочей области выберите hello, необходимо решение tooand tooadd hello, нажмите кнопку '' **создать**.</span><span class="sxs-lookup"><span data-stu-id="bb48d-151">In hello **Create new solution** blade, select hello workspace that you want tooadd hello solution tooand then click **Create**.</span></span>  
    <span data-ttu-id="bb48d-152">![добавить tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="bb48d-152">![add tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span></span>


### <a name="tooconfigure-multiple-azure-subscriptions"></a><span data-ttu-id="bb48d-153">tooconfigure несколько подписок Azure</span><span class="sxs-lookup"><span data-stu-id="bb48d-153">tooconfigure multiple Azure subscriptions</span></span>

<span data-ttu-id="bb48d-154">toosupport несколько подписок, использовать сценарий PowerShell hello из [Azure включить ведение журнала метрики ресурсов с помощью PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span><span class="sxs-lookup"><span data-stu-id="bb48d-154">toosupport multiple subscriptions, use hello PowerShell script from [Enable Azure resource metrics logging using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span> <span data-ttu-id="bb48d-155">Предоставить идентификатор ресурса hello рабочей области в качестве параметра при выполнении hello сценария toosend диагностических данных из ресурсов в рабочей области tooa одной подписки Azure в другой подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="bb48d-155">Provide hello workspace resource ID as a parameter when executing hello script toosend diagnostic data from resources in one Azure subscription tooa workspace in another Azure subscription.</span></span>

<span data-ttu-id="bb48d-156">**Пример**</span><span class="sxs-lookup"><span data-stu-id="bb48d-156">**Example**</span></span>

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-hello-solution"></a><span data-ttu-id="bb48d-157">С помощью решения hello</span><span class="sxs-lookup"><span data-stu-id="bb48d-157">Using hello solution</span></span>

<span data-ttu-id="bb48d-158">При добавлении рабочей области tooyour решения hello SQL Azure Analytics плитки приветствия добавляется tooyour рабочей области, и он отображается в обзоре.</span><span class="sxs-lookup"><span data-stu-id="bb48d-158">When you add hello solution tooyour workspace, hello Azure SQL Analytics tile is added tooyour workspace, and it appears in Overview.</span></span> <span data-ttu-id="bb48d-159">Hello отражает количество hello баз данных Azure SQL и пулах эластичных БД Azure SQL, к которой подключен hello решения.</span><span class="sxs-lookup"><span data-stu-id="bb48d-159">hello tile shows hello number of Azure SQL databases and Azure SQL elastic pools that hello solution is connected to.</span></span>

![Элемент служб анализа SQL Azure](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a><span data-ttu-id="bb48d-161">Просмотр данных службы "Аналитика SQL Azure"</span><span class="sxs-lookup"><span data-stu-id="bb48d-161">Viewing Azure SQL Analytics data</span></span>

<span data-ttu-id="bb48d-162">Щелкните hello **SQL Azure Analytics** панель мониторинга для SQL Azure Analytics hello tooopen плитки.</span><span class="sxs-lookup"><span data-stu-id="bb48d-162">Click on hello **Azure SQL Analytics** tile tooopen hello Azure SQL Analytics dashboard.</span></span> <span data-ttu-id="bb48d-163">панель мониторинга Hello включает колонках hello, описанные ниже.</span><span class="sxs-lookup"><span data-stu-id="bb48d-163">hello dashboard includes hello blades defined below.</span></span> <span data-ttu-id="bb48d-164">Каждой колонки список ресурсов too15 (подписки, сервер, эластичного пула и базы данных).</span><span class="sxs-lookup"><span data-stu-id="bb48d-164">Each blade lists up too15 resources (subscription, server, elastic pool, and database).</span></span> <span data-ttu-id="bb48d-165">Щелкните любой мониторинга hello tooopen hello ресурсы для конкретного ресурса.</span><span class="sxs-lookup"><span data-stu-id="bb48d-165">Click any of hello resources tooopen hello dashboard for that specific resource.</span></span> <span data-ttu-id="bb48d-166">Эластичный пул или база данных содержит hello диаграммы с метрик для выбранного ресурса.</span><span class="sxs-lookup"><span data-stu-id="bb48d-166">Elastic Pool or Database contains hello charts with metrics for a selected resource.</span></span> <span data-ttu-id="bb48d-167">Щелкните диалоговое окно поиска журналов hello tooopen диаграммы.</span><span class="sxs-lookup"><span data-stu-id="bb48d-167">Click a chart tooopen hello Log Search dialog.</span></span>

| <span data-ttu-id="bb48d-168">Колонка</span><span class="sxs-lookup"><span data-stu-id="bb48d-168">Blade</span></span> | <span data-ttu-id="bb48d-169">Описание</span><span class="sxs-lookup"><span data-stu-id="bb48d-169">Description</span></span> |
|---|---|
| <span data-ttu-id="bb48d-170">Подписки</span><span class="sxs-lookup"><span data-stu-id="bb48d-170">Subscriptions</span></span> | <span data-ttu-id="bb48d-171">Список подписок с количеством подключенных серверов, пулов и баз данных.</span><span class="sxs-lookup"><span data-stu-id="bb48d-171">List of subscriptions with number of connected servers, pools, and databases.</span></span> |
| <span data-ttu-id="bb48d-172">Серверы</span><span class="sxs-lookup"><span data-stu-id="bb48d-172">Servers</span></span> | <span data-ttu-id="bb48d-173">Список серверов с количеством подключенных пулов и баз данных.</span><span class="sxs-lookup"><span data-stu-id="bb48d-173">List of servers with number of connected pools and databases.</span></span> |
| <span data-ttu-id="bb48d-174">Эластичные пулы</span><span class="sxs-lookup"><span data-stu-id="bb48d-174">Elastic Pools</span></span> | <span data-ttu-id="bb48d-175">Список подключенных эластичные пулы с максимальной ГБ и eDTU в hello наблюдается периода.</span><span class="sxs-lookup"><span data-stu-id="bb48d-175">List of connected elastic pools with maximum GB and eDTU in hello observed period.</span></span> |
|<span data-ttu-id="bb48d-176">Базы данных</span><span class="sxs-lookup"><span data-stu-id="bb48d-176">Databases</span></span> | <span data-ttu-id="bb48d-177">Список подключенных баз данных с максимальной ГБ и DTU в hello окончание периода.</span><span class="sxs-lookup"><span data-stu-id="bb48d-177">List of connected databases with maximum GB and DTU in hello observed period.</span></span>|


### <a name="analyze-data-and-create-alerts"></a><span data-ttu-id="bb48d-178">Анализ данных и создание оповещений</span><span class="sxs-lookup"><span data-stu-id="bb48d-178">Analyze data and create alerts</span></span>

<span data-ttu-id="bb48d-179">Можно легко создать предупреждения с hello данные поступают из ресурсов базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="bb48d-179">You can easily create alerts with hello data coming from Azure SQL Database resources.</span></span> <span data-ttu-id="bb48d-180">Вот несколько полезных запросов для [поиска по журналам](log-analytics-log-searches.md), которые можно использовать для предупреждений.</span><span class="sxs-lookup"><span data-stu-id="bb48d-180">Here are a couple of useful [log search](log-analytics-log-searches.md) queries that you can use for alerting:</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


<span data-ttu-id="bb48d-181">*Высокий уровень DTU в базе данных SQL Azure*</span><span class="sxs-lookup"><span data-stu-id="bb48d-181">*High DTU on Azure SQL Database*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="bb48d-182">*Высокий уровень DTU в эластичном пуле базы данных SQL Azure*</span><span class="sxs-lookup"><span data-stu-id="bb48d-182">*High DTU on Azure SQL Database Elastic Pool*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="bb48d-183">Можно использовать эти запросы на основе оповещения tooalert на определенные пороговые значения для базы данных SQL Azure и эластичные пулы.</span><span class="sxs-lookup"><span data-stu-id="bb48d-183">You can use these alert-based queries tooalert on specific thresholds for both Azure SQL Database and elastic pools.</span></span> <span data-ttu-id="bb48d-184">tooconfigure оповещение для рабочей области OMS:</span><span class="sxs-lookup"><span data-stu-id="bb48d-184">tooconfigure an alert for your OMS workspace:</span></span>

#### <a name="tooconfigure-an-alert-for-your-workspace"></a><span data-ttu-id="bb48d-185">tooconfigure оповещение для рабочей области</span><span class="sxs-lookup"><span data-stu-id="bb48d-185">tooconfigure an alert for your workspace</span></span>

1. <span data-ttu-id="bb48d-186">Go toohello [портал OMS](http://mms.microsoft.com/) и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="bb48d-186">Go toohello [OMS portal](http://mms.microsoft.com/) and sign in.</span></span>
2. <span data-ttu-id="bb48d-187">Откройте рабочую область hello, настроенное для решения hello.</span><span class="sxs-lookup"><span data-stu-id="bb48d-187">Open hello workspace that you have configured for hello solution.</span></span>
3. <span data-ttu-id="bb48d-188">На странице приветствия Обзор щелкните hello **аналитики SQL Azure (Предварительная версия)** плитки.</span><span class="sxs-lookup"><span data-stu-id="bb48d-188">On hello Overview page, click hello **Azure SQL Analytics (Preview)** tile.</span></span>
4. <span data-ttu-id="bb48d-189">Выполните одну из hello примеров запросов.</span><span class="sxs-lookup"><span data-stu-id="bb48d-189">Run one of hello example queries.</span></span>
5. <span data-ttu-id="bb48d-190">В поиске по журналам щелкните **Оповещение**.</span><span class="sxs-lookup"><span data-stu-id="bb48d-190">In Log Search, click **Alert**.</span></span>  
<span data-ttu-id="bb48d-191">![Создание оповещения в поиске](./media/log-analytics-azure-sql/create-alert01.png)</span><span class="sxs-lookup"><span data-stu-id="bb48d-191">![create alert in search](./media/log-analytics-azure-sql/create-alert01.png)</span></span>
6. <span data-ttu-id="bb48d-192">На hello **добавить правило оповещения** задайте соответствующие свойства hello и hello определенных пороговых значений и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bb48d-192">On hello **Add Alert Rule** page, configure hello appropriate properties and hello specific thresholds that you want and then click **Save**.</span></span>  
<span data-ttu-id="bb48d-193">![Добавление правила оповещения](./media/log-analytics-azure-sql/create-alert02.png)</span><span class="sxs-lookup"><span data-stu-id="bb48d-193">![add alert rule](./media/log-analytics-azure-sql/create-alert02.png)</span></span>

### <a name="act-on-azure-sql-analytics-data"></a><span data-ttu-id="bb48d-194">Выполнение действий над данными службы "Аналитика SQL Azure"</span><span class="sxs-lookup"><span data-stu-id="bb48d-194">Act on Azure SQL Analytics data</span></span>

<span data-ttu-id="bb48d-195">Например одна из hello самые полезные запросы, которые можно выполнять — toocompare hello DTU использования для всех пулов эластичных SQL Azure во всех подписках Azure.</span><span class="sxs-lookup"><span data-stu-id="bb48d-195">As an example, one of hello most useful queries that you can perform is toocompare hello DTU utilization for all Azure SQL Elastic Pools across all your Azure subscriptions.</span></span> <span data-ttu-id="bb48d-196">Единица пропускной способности базы данных (DTU) предоставляет toodescribe способом hello относительную емкость уровня производительности баз данных Basic, Standard и Premium и пулы.</span><span class="sxs-lookup"><span data-stu-id="bb48d-196">Database Throughput Unit (DTU) provides a way toodescribe hello relative capacity of a performance level of Basic, Standard, and Premium databases and pools.</span></span> <span data-ttu-id="bb48d-197">Единицы DTU получают на основе показателей ЦП, памяти, операций чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="bb48d-197">DTUs are based on a blended measure of CPU, memory, reads, and writes.</span></span> <span data-ttu-id="bb48d-198">При увеличении количества Dtu, hello возможности, предлагаемые уровня увеличения производительности hello.</span><span class="sxs-lookup"><span data-stu-id="bb48d-198">As DTUs increase, hello power offered by hello performance level increases.</span></span> <span data-ttu-id="bb48d-199">Например, уровень производительности с 5 единицами DTU в пять раз выше уровня производительности с 1 единицей DTU.</span><span class="sxs-lookup"><span data-stu-id="bb48d-199">For example, a performance level with 5 DTUs has five times more power than a performance level with 1 DTU.</span></span> <span data-ttu-id="bb48d-200">Максимальная квота DTU применяется tooeach сервера и переменной ширины пула.</span><span class="sxs-lookup"><span data-stu-id="bb48d-200">A maximum DTU quota applies tooeach server and elastic pool.</span></span>

<span data-ttu-id="bb48d-201">Выполняя следующий запрос поиска журнала hello, можно легко отличить недостаточно или более использование пулов эластичных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="bb48d-201">By running hello following Log Search query, you can easily tell if you are underutilizing or over utilizing your SQL Azure elastic pools.</span></span>

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> <span data-ttu-id="bb48d-202">Если обновленный toohello рабочей области [языка запросов новый журнал аналитики](log-analytics-log-search-upgrade.md), то hello выше запрос изменится toohello следующее.</span><span class="sxs-lookup"><span data-stu-id="bb48d-202">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

<span data-ttu-id="bb48d-203">В следующем примере hello, можно видно, один эластичный пул имеет высокую загруженность близка к 100% DTU, тогда как другие содержат очень мало использования.</span><span class="sxs-lookup"><span data-stu-id="bb48d-203">In hello following example, you can see that one elastic pool has a high usage near 100% DTU while others have very little usage.</span></span> <span data-ttu-id="bb48d-204">В среде с помощью журналов действий Azure можно изучить tootroubleshoot потенциальных последние изменения.</span><span class="sxs-lookup"><span data-stu-id="bb48d-204">You can investigate further tootroubleshoot potential recent changes in your environment using Azure Activity logs.</span></span>

![Результаты поиска по журналам. Высокая загрузка](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a><span data-ttu-id="bb48d-206">См. также</span><span class="sxs-lookup"><span data-stu-id="bb48d-206">See also</span></span>

- <span data-ttu-id="bb48d-207">Используйте [запросов поиска журналов](log-analytics-log-searches.md) в службе анализа журналов tooview подробных данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="bb48d-207">Use [Log Searches](log-analytics-log-searches.md) in Log Analytics tooview detailed Azure SQL data.</span></span>
- <span data-ttu-id="bb48d-208">[Создавайте пользовательские панели мониторинга](log-analytics-dashboards.md), отображающие данные SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="bb48d-208">[Create your own dashboards](log-analytics-dashboards.md) showing Azure SQL data.</span></span>
- <span data-ttu-id="bb48d-209">[Создавайте оповещения](log-analytics-alerts.md), предупреждающие о возникновении определенных событий SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="bb48d-209">[Create alerts](log-analytics-alerts.md) when specific Azure SQL events occur.</span></span>
