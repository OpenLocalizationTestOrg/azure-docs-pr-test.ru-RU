---
title: "Решение служб анализа SQL Azure в Log Analytics | Документация Майкрософт"
description: "Решение служб анализа SQL Azure поможет вам управлять базами данных SQL Azure."
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
ms.openlocfilehash: cab45cc6dd621eb4a95ef5f1842ec38c25e980b6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a><span data-ttu-id="4c23e-103">Мониторинг базы данных SQL Azure с помощью служб анализа SQL Azure (предварительная версия) в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="4c23e-103">Monitor Azure SQL Database using Azure SQL Analytics (Preview) in Log Analytics</span></span>

![Символ службы "Аналитика SQL Azure"](./media/log-analytics-azure-sql/azure-sql-symbol.png)

<span data-ttu-id="4c23e-105">Решение "Аналитика SQL Azure" в Azure Log Analytics собирает и отображает важные метрики производительности SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4c23e-105">The Azure SQL Analytics solution in Azure Log Analytics collects and visualizes important SQL Azure performance metrics.</span></span> <span data-ttu-id="4c23e-106">На основе этих метрик можно создавать пользовательские правила мониторинга и оповещения.</span><span class="sxs-lookup"><span data-stu-id="4c23e-106">By using the metrics that you collect with the solution, you can create custom monitoring rules and alerts.</span></span> <span data-ttu-id="4c23e-107">Вы можете отслеживать метрики базы данных SQL Azure и эластичных пулов в нескольких подписках Azure и эластичных пулах, а также визуализировать их.</span><span class="sxs-lookup"><span data-stu-id="4c23e-107">And, you can monitor Azure SQL Database and elastic pool metrics across multiple Azure subscriptions and elastic pools and visualize them.</span></span> <span data-ttu-id="4c23e-108">Решение также поможет вам определить проблемы на каждом уровне стека приложений.</span><span class="sxs-lookup"><span data-stu-id="4c23e-108">The solution also helps you to identify issues at each layer of your application stack.</span></span>  <span data-ttu-id="4c23e-109">Оно использует [метрики диагностики Azure](log-analytics-azure-storage.md) с представлениями Log Analytics, чтобы представить данные обо всех базах данных SQL Azure и эластичных пулах в единой рабочей области Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4c23e-109">It uses [Azure Diagnostic metrics](log-analytics-azure-storage.md) together with Log Analytics views to present data about all your Azure SQL databases and elastic pools in a single Log Analytics workspace.</span></span>

<span data-ttu-id="4c23e-110">Сейчас эта предварительная версия решения поддерживает 150 000 баз данных SQL Azure и 5 000 эластичных пулов SQL на каждую рабочую область.</span><span class="sxs-lookup"><span data-stu-id="4c23e-110">Currently, this preview solution supports up to 150,000 Azure SQL Databases and 5,000 SQL Elastic Pools per workspace.</span></span>

<span data-ttu-id="4c23e-111">Решение "Аналитика SQL Azure", как и другие решения, доступные для Log Analytics, помогает отслеживать и получать уведомления о работоспособности ресурсов Azure — в данном случае о базах данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4c23e-111">The Azure SQL Analytics solution, like others available for Log Analytics, helps you monitor and receive notifications about the health of your Azure resources—in this case, Azure SQL Database.</span></span> <span data-ttu-id="4c23e-112">База данных SQL Microsoft Azure представляет собой масштабируемую службу реляционных баз данных, предоставляющую возможности, аналогичные возможностям SQL Server, в приложениях, запущенных в облаке Azure.</span><span class="sxs-lookup"><span data-stu-id="4c23e-112">Microsoft Azure SQL Database is a scalable relational database service that provides familiar SQL-Server-like capabilities to applications running in the Azure cloud.</span></span> <span data-ttu-id="4c23e-113">Log Analytics помогает собирать, коррелировать и визуализировать структурированные и неструктурированные данные.</span><span class="sxs-lookup"><span data-stu-id="4c23e-113">Log Analytics helps you to collect, correlate, and visualize structured and unstructured data.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="4c23e-114">Подключенные источники</span><span class="sxs-lookup"><span data-stu-id="4c23e-114">Connected sources</span></span>

<span data-ttu-id="4c23e-115">Решение "Аналитика SQL Azure" не использует агенты для подключения к службе Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4c23e-115">The Azure SQL Analytics solution doesn't use agents to connect to the Log Analytics service.</span></span>

<span data-ttu-id="4c23e-116">В следующей таблице описаны подключенные источники, которые поддерживаются этим решением.</span><span class="sxs-lookup"><span data-stu-id="4c23e-116">The following table describes the connected sources that are supported by this solution.</span></span>

| <span data-ttu-id="4c23e-117">Подключенный источник</span><span class="sxs-lookup"><span data-stu-id="4c23e-117">Connected Source</span></span> | <span data-ttu-id="4c23e-118">Поддержка</span><span class="sxs-lookup"><span data-stu-id="4c23e-118">Support</span></span> | <span data-ttu-id="4c23e-119">Описание</span><span class="sxs-lookup"><span data-stu-id="4c23e-119">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="4c23e-120">Агенты Windows</span><span class="sxs-lookup"><span data-stu-id="4c23e-120">Windows agents</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="4c23e-121">Нет</span><span class="sxs-lookup"><span data-stu-id="4c23e-121">No</span></span> | <span data-ttu-id="4c23e-122">Решение не использует прямые агенты Windows.</span><span class="sxs-lookup"><span data-stu-id="4c23e-122">Direct Windows agents are not used by the solution.</span></span> |
| [<span data-ttu-id="4c23e-123">Агенты Linux</span><span class="sxs-lookup"><span data-stu-id="4c23e-123">Linux agents</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="4c23e-124">Нет</span><span class="sxs-lookup"><span data-stu-id="4c23e-124">No</span></span> | <span data-ttu-id="4c23e-125">Решение не использует прямые агенты Linux.</span><span class="sxs-lookup"><span data-stu-id="4c23e-125">Direct Linux agents are not used by the solution.</span></span> |
| [<span data-ttu-id="4c23e-126">Группы управления SCOM</span><span class="sxs-lookup"><span data-stu-id="4c23e-126">SCOM management group</span></span>](log-analytics-om-agents.md) | <span data-ttu-id="4c23e-127">Нет</span><span class="sxs-lookup"><span data-stu-id="4c23e-127">No</span></span> | <span data-ttu-id="4c23e-128">Решение не использует прямое подключение агента SCOM к Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4c23e-128">A direct connection from the SCOM agent to Log Analytics is not used by the solution.</span></span> |
| [<span data-ttu-id="4c23e-129">Учетная запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="4c23e-129">Azure storage account</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="4c23e-130">Нет</span><span class="sxs-lookup"><span data-stu-id="4c23e-130">No</span></span> | <span data-ttu-id="4c23e-131">Log Analytics не считывает данные из учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="4c23e-131">Log Analytics does not read the data from a storage account.</span></span> |
| [<span data-ttu-id="4c23e-132">Настройка системы диагностики Azure для входа в Application Insights</span><span class="sxs-lookup"><span data-stu-id="4c23e-132">Azure diagnostics</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="4c23e-133">Да</span><span class="sxs-lookup"><span data-stu-id="4c23e-133">Yes</span></span> | <span data-ttu-id="4c23e-134">Данные метрик Azure отправляются в Log Analytics из Azure непосредственно.</span><span class="sxs-lookup"><span data-stu-id="4c23e-134">Azure metric data is sent to Log Analytics directly by Azure.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="4c23e-135">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4c23e-135">Prerequisites</span></span>

- <span data-ttu-id="4c23e-136">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="4c23e-136">An Azure Subscription.</span></span> <span data-ttu-id="4c23e-137">Если у вас ее нет, вы можете создать ее [бесплатно](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="4c23e-137">If you don't have one, you can create one for [free](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="4c23e-138">Рабочая область Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4c23e-138">A Log Analytics workspace.</span></span> <span data-ttu-id="4c23e-139">Вы можете использовать имеющуюся рабочую область или же [создать ее](log-analytics-get-started.md), прежде чем начать использовать это решение.</span><span class="sxs-lookup"><span data-stu-id="4c23e-139">You can use an existing one, or you can [create a new one](log-analytics-get-started.md) before you start using this solution.</span></span>
- <span data-ttu-id="4c23e-140">Включите систему диагностики Azure для баз данных SQL Azure и эластичных пулов и [настройте для них отправку данных в Log Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span><span class="sxs-lookup"><span data-stu-id="4c23e-140">Enable Azure Diagnostics for your Azure SQL databases and elastic pools and [configure them to send their data to Log Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span>

## <a name="configuration"></a><span data-ttu-id="4c23e-141">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="4c23e-141">Configuration</span></span>

<span data-ttu-id="4c23e-142">Чтобы добавить решение "Аналитика SQL Azure" в рабочую область, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="4c23e-142">Perform the following steps to add the Azure SQL Analytics solution to your workspace.</span></span>

1. <span data-ttu-id="4c23e-143">Решение для анализа Azure SQL необходимо добавить в рабочую область из [Azure Мarketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) или в соответствии с инструкциями по [добавлению решений Log Analytics из коллекции решений](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="4c23e-143">Add the Azure SQL Analytics solution to your workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="4c23e-144">На портале Azure щелкните **Создать** (знак +), а затем в списке ресурсов выберите **Мониторинг и управление**.</span><span class="sxs-lookup"><span data-stu-id="4c23e-144">In the Azure portal, click **New** (the + symbol), then in the list of resources, select **Monitoring + Management**.</span></span>  
    <span data-ttu-id="4c23e-145">![Мониторинг и управление](./media/log-analytics-azure-sql/monitoring-management.png)</span><span class="sxs-lookup"><span data-stu-id="4c23e-145">![Monitoring + Management](./media/log-analytics-azure-sql/monitoring-management.png)</span></span>
3. <span data-ttu-id="4c23e-146">В списке **Мониторинг и управление** щелкните **Показать все**.</span><span class="sxs-lookup"><span data-stu-id="4c23e-146">In the **Monitoring + Management** list click **See all**.</span></span>
4. <span data-ttu-id="4c23e-147">В списке **Рекомендуется** выберите **More** (Дополнительно), а затем в новом списке найдите и выберите **Службы анализа SQL Azure (предварительная версия)**.</span><span class="sxs-lookup"><span data-stu-id="4c23e-147">In the **Recommended** list, click **More** , and then in the new list, find **Azure SQL Analytics (Preview)** and then select it.</span></span>  
    <span data-ttu-id="4c23e-148">![Решение служб анализа SQL Azure](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span><span class="sxs-lookup"><span data-stu-id="4c23e-148">![Azure SQL Analytics solution](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span></span>
5. <span data-ttu-id="4c23e-149">В колонке **Службы анализа SQL Azure (предварительная версия)** щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4c23e-149">In the **Azure SQL Analytics (Preview)** blade, click **Create**.</span></span>  
    <span data-ttu-id="4c23e-150">![Создание](./media/log-analytics-azure-sql/portal-create.png)</span><span class="sxs-lookup"><span data-stu-id="4c23e-150">![Create](./media/log-analytics-azure-sql/portal-create.png)</span></span>
6. <span data-ttu-id="4c23e-151">В колонке **Создание решения** выберите рабочую область, в которую необходимо добавить решение, а затем нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4c23e-151">In the **Create new solution** blade, select the workspace that you want to add the solution to and then click **Create**.</span></span>  
    <span data-ttu-id="4c23e-152">![Добавление в рабочую область](./media/log-analytics-azure-sql/add-to-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="4c23e-152">![add to workspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span></span>


### <a name="to-configure-multiple-azure-subscriptions"></a><span data-ttu-id="4c23e-153">Настройка нескольких подписок Azure</span><span class="sxs-lookup"><span data-stu-id="4c23e-153">To configure multiple Azure subscriptions</span></span>

<span data-ttu-id="4c23e-154">Чтобы обеспечить поддержку нескольких подписок, используйте сценарий PowerShell. Дополнительные сведения см. в статье [Enable Azure resource metrics logging using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/) (Включение ведения журнала метрик ресурсов Azure с помощью PowerShell).</span><span class="sxs-lookup"><span data-stu-id="4c23e-154">To support multiple subscriptions, use the PowerShell script from [Enable Azure resource metrics logging using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span> <span data-ttu-id="4c23e-155">Укажите идентификатор ресурса рабочей области в качестве параметра при выполнении скрипта для отправки диагностических данных из ресурсов в одной подписке Azure в рабочую область в другой подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="4c23e-155">Provide the workspace resource ID as a parameter when executing the script to send diagnostic data from resources in one Azure subscription to a workspace in another Azure subscription.</span></span>

<span data-ttu-id="4c23e-156">**Пример**</span><span class="sxs-lookup"><span data-stu-id="4c23e-156">**Example**</span></span>

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-the-solution"></a><span data-ttu-id="4c23e-157">Использование решения</span><span class="sxs-lookup"><span data-stu-id="4c23e-157">Using the solution</span></span>

<span data-ttu-id="4c23e-158">Вместе с решением в рабочую область добавляется элемент служб анализа SQL Azure. Кроме того, он появляется в общих сведениях.</span><span class="sxs-lookup"><span data-stu-id="4c23e-158">When you add the solution to your workspace, the Azure SQL Analytics tile is added to your workspace, and it appears in Overview.</span></span> <span data-ttu-id="4c23e-159">В элементе отображаются сведения о количестве баз данных и эластичных пулов SQL Azure, к которым подключено решение.</span><span class="sxs-lookup"><span data-stu-id="4c23e-159">The tile shows the number of Azure SQL databases and Azure SQL elastic pools that the solution is connected to.</span></span>

![Элемент служб анализа SQL Azure](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a><span data-ttu-id="4c23e-161">Просмотр данных службы "Аналитика SQL Azure"</span><span class="sxs-lookup"><span data-stu-id="4c23e-161">Viewing Azure SQL Analytics data</span></span>

<span data-ttu-id="4c23e-162">Щелкните плитку **Azure SQL Analytics** (Аналитика SQL Azure), чтобы открыть панель мониторинга службы "Аналитика SQL Azure".</span><span class="sxs-lookup"><span data-stu-id="4c23e-162">Click on the **Azure SQL Analytics** tile to open the Azure SQL Analytics dashboard.</span></span> <span data-ttu-id="4c23e-163">Панель мониторинга содержит колонки, определенные ниже.</span><span class="sxs-lookup"><span data-stu-id="4c23e-163">The dashboard includes the blades defined below.</span></span> <span data-ttu-id="4c23e-164">В каждой колонке приведено до 15 ресурсов (подписка, сервер, эластичный пул и база данных).</span><span class="sxs-lookup"><span data-stu-id="4c23e-164">Each blade lists up to 15 resources (subscription, server, elastic pool, and database).</span></span> <span data-ttu-id="4c23e-165">Щелкните любой из ресурсов, чтобы открыть для него панель мониторинга.</span><span class="sxs-lookup"><span data-stu-id="4c23e-165">Click any of the resources to open the dashboard for that specific resource.</span></span> <span data-ttu-id="4c23e-166">Эластичный пул или база данных содержит диаграммы с метриками для выбранного ресурса.</span><span class="sxs-lookup"><span data-stu-id="4c23e-166">Elastic Pool or Database contains the charts with metrics for a selected resource.</span></span> <span data-ttu-id="4c23e-167">Щелкните диаграмму, чтобы открыть диалоговое окно поиска по журналам.</span><span class="sxs-lookup"><span data-stu-id="4c23e-167">Click a chart to open the Log Search dialog.</span></span>

| <span data-ttu-id="4c23e-168">Колонка</span><span class="sxs-lookup"><span data-stu-id="4c23e-168">Blade</span></span> | <span data-ttu-id="4c23e-169">Описание</span><span class="sxs-lookup"><span data-stu-id="4c23e-169">Description</span></span> |
|---|---|
| <span data-ttu-id="4c23e-170">Подписки</span><span class="sxs-lookup"><span data-stu-id="4c23e-170">Subscriptions</span></span> | <span data-ttu-id="4c23e-171">Список подписок с количеством подключенных серверов, пулов и баз данных.</span><span class="sxs-lookup"><span data-stu-id="4c23e-171">List of subscriptions with number of connected servers, pools, and databases.</span></span> |
| <span data-ttu-id="4c23e-172">Серверы</span><span class="sxs-lookup"><span data-stu-id="4c23e-172">Servers</span></span> | <span data-ttu-id="4c23e-173">Список серверов с количеством подключенных пулов и баз данных.</span><span class="sxs-lookup"><span data-stu-id="4c23e-173">List of servers with number of connected pools and databases.</span></span> |
| <span data-ttu-id="4c23e-174">Эластичные пулы</span><span class="sxs-lookup"><span data-stu-id="4c23e-174">Elastic Pools</span></span> | <span data-ttu-id="4c23e-175">Список подключенных эластичных пулов с максимальным объемом хранилища в ГБ и eDTU в течение наблюдаемого периода времени.</span><span class="sxs-lookup"><span data-stu-id="4c23e-175">List of connected elastic pools with maximum GB and eDTU in the observed period.</span></span> |
|<span data-ttu-id="4c23e-176">Базы данных</span><span class="sxs-lookup"><span data-stu-id="4c23e-176">Databases</span></span> | <span data-ttu-id="4c23e-177">Список подключенных баз данных с максимальным объемом хранилища в ГБ и eDTU в течение наблюдаемого периода времени.</span><span class="sxs-lookup"><span data-stu-id="4c23e-177">List of connected databases with maximum GB and DTU in the observed period.</span></span>|


### <a name="analyze-data-and-create-alerts"></a><span data-ttu-id="4c23e-178">Анализ данных и создание оповещений</span><span class="sxs-lookup"><span data-stu-id="4c23e-178">Analyze data and create alerts</span></span>

<span data-ttu-id="4c23e-179">Оповещения можно легко создать с помощью данных, поступающих из ресурсов базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4c23e-179">You can easily create alerts with the data coming from Azure SQL Database resources.</span></span> <span data-ttu-id="4c23e-180">Вот несколько полезных запросов для [поиска по журналам](log-analytics-log-searches.md), которые можно использовать для предупреждений.</span><span class="sxs-lookup"><span data-stu-id="4c23e-180">Here are a couple of useful [log search](log-analytics-log-searches.md) queries that you can use for alerting:</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


<span data-ttu-id="4c23e-181">*Высокий уровень DTU в базе данных SQL Azure*</span><span class="sxs-lookup"><span data-stu-id="4c23e-181">*High DTU on Azure SQL Database*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="4c23e-182">*Высокий уровень DTU в эластичном пуле базы данных SQL Azure*</span><span class="sxs-lookup"><span data-stu-id="4c23e-182">*High DTU on Azure SQL Database Elastic Pool*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="4c23e-183">Используя запросы на основе оповещений, можно создавать предупреждения об определенных пороговых значениях для баз данных и эластичных пулов SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4c23e-183">You can use these alert-based queries to alert on specific thresholds for both Azure SQL Database and elastic pools.</span></span> <span data-ttu-id="4c23e-184">Чтобы настроить оповещение для рабочей области OMS, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="4c23e-184">To configure an alert for your OMS workspace:</span></span>

#### <a name="to-configure-an-alert-for-your-workspace"></a><span data-ttu-id="4c23e-185">Чтобы настроить оповещение для рабочей области, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="4c23e-185">To configure an alert for your workspace</span></span>

1. <span data-ttu-id="4c23e-186">Перейдите на [портал OMS](http://mms.microsoft.com/) и войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="4c23e-186">Go to the [OMS portal](http://mms.microsoft.com/) and sign in.</span></span>
2. <span data-ttu-id="4c23e-187">Откройте рабочую область, настроенную для решения.</span><span class="sxs-lookup"><span data-stu-id="4c23e-187">Open the workspace that you have configured for the solution.</span></span>
3. <span data-ttu-id="4c23e-188">На странице обзора щелкните элемент **Службы анализа SQL Azure (предварительная версия)**.</span><span class="sxs-lookup"><span data-stu-id="4c23e-188">On the Overview page, click the **Azure SQL Analytics (Preview)** tile.</span></span>
4. <span data-ttu-id="4c23e-189">Выполните один из примеров запросов.</span><span class="sxs-lookup"><span data-stu-id="4c23e-189">Run one of the example queries.</span></span>
5. <span data-ttu-id="4c23e-190">В поиске по журналам щелкните **Оповещение**.</span><span class="sxs-lookup"><span data-stu-id="4c23e-190">In Log Search, click **Alert**.</span></span>  
<span data-ttu-id="4c23e-191">![Создание оповещения в поиске](./media/log-analytics-azure-sql/create-alert01.png)</span><span class="sxs-lookup"><span data-stu-id="4c23e-191">![create alert in search](./media/log-analytics-azure-sql/create-alert01.png)</span></span>
6. <span data-ttu-id="4c23e-192">На странице **Добавить правило оповещения** настройте соответствующие свойства и определенные пороговые значения, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4c23e-192">On the **Add Alert Rule** page, configure the appropriate properties and the specific thresholds that you want and then click **Save**.</span></span>  
<span data-ttu-id="4c23e-193">![Добавление правила оповещения](./media/log-analytics-azure-sql/create-alert02.png)</span><span class="sxs-lookup"><span data-stu-id="4c23e-193">![add alert rule](./media/log-analytics-azure-sql/create-alert02.png)</span></span>

### <a name="act-on-azure-sql-analytics-data"></a><span data-ttu-id="4c23e-194">Выполнение действий над данными службы "Аналитика SQL Azure"</span><span class="sxs-lookup"><span data-stu-id="4c23e-194">Act on Azure SQL Analytics data</span></span>

<span data-ttu-id="4c23e-195">К примеру, один из наиболее полезных запросов, которые можно выполнить, заключается в сравнении использования DTU для всех эластичных пулов SQL Azure во всех подписках Azure.</span><span class="sxs-lookup"><span data-stu-id="4c23e-195">As an example, one of the most useful queries that you can perform is to compare the DTU utilization for all Azure SQL Elastic Pools across all your Azure subscriptions.</span></span> <span data-ttu-id="4c23e-196">Единица пропускной способности базы данных (DTU) выражает относительную емкость уровня производительности пулов и баз данных уровня "Базовый", "Стандартный" и "Премиум".</span><span class="sxs-lookup"><span data-stu-id="4c23e-196">Database Throughput Unit (DTU) provides a way to describe the relative capacity of a performance level of Basic, Standard, and Premium databases and pools.</span></span> <span data-ttu-id="4c23e-197">Единицы DTU получают на основе показателей ЦП, памяти, операций чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="4c23e-197">DTUs are based on a blended measure of CPU, memory, reads, and writes.</span></span> <span data-ttu-id="4c23e-198">С увеличением числа единиц DTU увеличивается также и мощность, предлагаемая на уровне производительности.</span><span class="sxs-lookup"><span data-stu-id="4c23e-198">As DTUs increase, the power offered by the performance level increases.</span></span> <span data-ttu-id="4c23e-199">Например, уровень производительности с 5 единицами DTU в пять раз выше уровня производительности с 1 единицей DTU.</span><span class="sxs-lookup"><span data-stu-id="4c23e-199">For example, a performance level with 5 DTUs has five times more power than a performance level with 1 DTU.</span></span> <span data-ttu-id="4c23e-200">К каждому серверу и эластичному пулу применяется максимальная квота DTU.</span><span class="sxs-lookup"><span data-stu-id="4c23e-200">A maximum DTU quota applies to each server and elastic pool.</span></span>

<span data-ttu-id="4c23e-201">Выполнив следующий запрос поиска по журналам, вы можете легко определить степень использования эластичных пулов SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4c23e-201">By running the following Log Search query, you can easily tell if you are underutilizing or over utilizing your SQL Azure elastic pools.</span></span>

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> <span data-ttu-id="4c23e-202">Если ваша рабочая область переведена на [язык запросов Log Analytics](log-analytics-log-search-upgrade.md), приведенный выше запрос будет изменен следующим образом.</span><span class="sxs-lookup"><span data-stu-id="4c23e-202">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above query would change to the following.</span></span>
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

<span data-ttu-id="4c23e-203">Как видно из примера ниже, в одном эластичном пуле используется практически 100 % единиц DTU, тогда как показатели других чрезвычайно низкие.</span><span class="sxs-lookup"><span data-stu-id="4c23e-203">In the following example, you can see that one elastic pool has a high usage near 100% DTU while others have very little usage.</span></span> <span data-ttu-id="4c23e-204">С помощью журналов действий Azure вы можете устранить потенциальные последние изменения в окружении.</span><span class="sxs-lookup"><span data-stu-id="4c23e-204">You can investigate further to troubleshoot potential recent changes in your environment using Azure Activity logs.</span></span>

![Результаты поиска по журналам. Высокая загрузка](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a><span data-ttu-id="4c23e-206">См. также</span><span class="sxs-lookup"><span data-stu-id="4c23e-206">See also</span></span>

- <span data-ttu-id="4c23e-207">Используйте [поиск по журналам](log-analytics-log-searches.md) в Log Analytics для просмотра подробных данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4c23e-207">Use [Log Searches](log-analytics-log-searches.md) in Log Analytics to view detailed Azure SQL data.</span></span>
- <span data-ttu-id="4c23e-208">[Создавайте пользовательские панели мониторинга](log-analytics-dashboards.md), отображающие данные SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4c23e-208">[Create your own dashboards](log-analytics-dashboards.md) showing Azure SQL data.</span></span>
- <span data-ttu-id="4c23e-209">[Создавайте оповещения](log-analytics-alerts.md), предупреждающие о возникновении определенных событий SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4c23e-209">[Create alerts](log-analytics-alerts.md) when specific Azure SQL events occur.</span></span>
