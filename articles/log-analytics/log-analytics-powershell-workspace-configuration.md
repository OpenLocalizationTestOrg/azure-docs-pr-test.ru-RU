---
title: "aaaUse PowerShell tooCreate и настройка рабочей областью аналитики журналов | Документы Microsoft"
description: "Log Analytics использует данные с серверов в вашей локальной или облачной инфраструктуре. При генерировании системой диагностики Azure можно брать данные компьютера из хранилища Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 3b9b7ade-3374-4596-afb1-51b695f481c2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: powershell
ms.topic: article
ms.date: 11/21/2016
ms.author: richrund
ms.openlocfilehash: a6d66194204cc58de6aafb687a19fe9611e0c58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-log-analytics-using-powershell"></a><span data-ttu-id="4f145-104">Управление Log Analytics с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f145-104">Manage Log Analytics using PowerShell</span></span>
<span data-ttu-id="4f145-105">Можно использовать hello [командлеты PowerShell аналитика журналов](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform различные функции в службе анализа журналов из командной строки или как часть сценария.</span><span class="sxs-lookup"><span data-stu-id="4f145-105">You can use hello [Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform various functions in Log Analytics from a command line or as part of a script.</span></span>  <span data-ttu-id="4f145-106">Примеры hello задачи, которые можно выполнять с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4f145-106">Examples of hello tasks you can perform with PowerShell include:</span></span>

* <span data-ttu-id="4f145-107">Создание рабочей области</span><span class="sxs-lookup"><span data-stu-id="4f145-107">Create a workspace</span></span>
* <span data-ttu-id="4f145-108">Добавление или удаление решения</span><span class="sxs-lookup"><span data-stu-id="4f145-108">Add or remove a solution</span></span>
* <span data-ttu-id="4f145-109">Импорт и экспорт сохраненных поисков</span><span class="sxs-lookup"><span data-stu-id="4f145-109">Import and export saved searches</span></span>
* <span data-ttu-id="4f145-110">Создание группы компьютеров</span><span class="sxs-lookup"><span data-stu-id="4f145-110">Create a computer group</span></span>
* <span data-ttu-id="4f145-111">Включить сбор журналов IIS с компьютеров с установленным агентом Windows hello</span><span class="sxs-lookup"><span data-stu-id="4f145-111">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
* <span data-ttu-id="4f145-112">Сбор счетчиков производительности с компьютеров под управлением Linux и Windows</span><span class="sxs-lookup"><span data-stu-id="4f145-112">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="4f145-113">Сбор событий из системного журнала с компьютеров Linux</span><span class="sxs-lookup"><span data-stu-id="4f145-113">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="4f145-114">Сбор событий из журналов событий Windows</span><span class="sxs-lookup"><span data-stu-id="4f145-114">Collect events from Windows event logs</span></span>
* <span data-ttu-id="4f145-115">Сбор пользовательских журналов событий</span><span class="sxs-lookup"><span data-stu-id="4f145-115">Collect custom event logs</span></span>
* <span data-ttu-id="4f145-116">Добавить hello журнала аналитика агента tooan виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="4f145-116">Add hello log analytics agent tooan Azure virtual machine</span></span>
* <span data-ttu-id="4f145-117">Настройка журнала аналитика tooindex собранные средствами диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="4f145-117">Configure log analytics tooindex data collected using Azure diagnostics</span></span>

<span data-ttu-id="4f145-118">Эта статья содержит два образца кода, иллюстрирующие некоторых функций hello, которые можно выполнять из PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4f145-118">This article provides two code samples that illustrate some of hello functions that you can perform from PowerShell.</span></span>  <span data-ttu-id="4f145-119">Можно ссылаться toohello [Справочник по командлетам PowerShell аналитика журналов](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) для других функций.</span><span class="sxs-lookup"><span data-stu-id="4f145-119">You can refer toohello [Log Analytics PowerShell cmdlet reference](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for other functions.</span></span>

> [!NOTE]
> <span data-ttu-id="4f145-120">Служба аналитики журналов был вызван ранее оперативной аналитики, поэтому это hello имя, используемое в командлетах hello.</span><span class="sxs-lookup"><span data-stu-id="4f145-120">Log Analytics was previously called Operational Insights, which is why it is hello name used in hello cmdlets.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="4f145-121">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4f145-121">Prerequisites</span></span>
<span data-ttu-id="4f145-122">Эти примеры работают с версию 2.3.0 или более поздней версии модуля AzureRm.OperationalInsights hello.</span><span class="sxs-lookup"><span data-stu-id="4f145-122">These examples work with version 2.3.0 or later of hello AzureRm.OperationalInsights module.</span></span>


## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="4f145-123">Создание и настройка рабочей области Log Analytics</span><span class="sxs-lookup"><span data-stu-id="4f145-123">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="4f145-124">Hello следующий скрипт образец показывает, как:</span><span class="sxs-lookup"><span data-stu-id="4f145-124">hello following script sample illustrates how to:</span></span>

1. <span data-ttu-id="4f145-125">Создание рабочей области</span><span class="sxs-lookup"><span data-stu-id="4f145-125">Create a workspace</span></span>
2. <span data-ttu-id="4f145-126">Список hello доступные решения</span><span class="sxs-lookup"><span data-stu-id="4f145-126">List hello available solutions</span></span>
3. <span data-ttu-id="4f145-127">Добавление рабочей области toohello решений</span><span class="sxs-lookup"><span data-stu-id="4f145-127">Add solutions toohello workspace</span></span>
4. <span data-ttu-id="4f145-128">Импорт сохраненных поисков</span><span class="sxs-lookup"><span data-stu-id="4f145-128">Import saved searches</span></span>
5. <span data-ttu-id="4f145-129">Экспорт сохраненных поисков</span><span class="sxs-lookup"><span data-stu-id="4f145-129">Export saved searches</span></span>
6. <span data-ttu-id="4f145-130">Создание группы компьютеров</span><span class="sxs-lookup"><span data-stu-id="4f145-130">Create a computer group</span></span>
7. <span data-ttu-id="4f145-131">Включить сбор журналов IIS с компьютеров с установленным агентом Windows hello</span><span class="sxs-lookup"><span data-stu-id="4f145-131">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
8. <span data-ttu-id="4f145-132">Сбор счетчиков производительности логического диска с компьютеров под управлением Linux ("Процент использования индексных дескрипторов"; "Свободно мегабайт"; "Процент используемого места"; "Количество обращений к диску (в секунду)"; "Количество обращений чтения или записи (в секунду))"</span><span class="sxs-lookup"><span data-stu-id="4f145-132">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
9. <span data-ttu-id="4f145-133">Сбор событий из системного журнала с компьютеров Linux</span><span class="sxs-lookup"><span data-stu-id="4f145-133">Collect syslog events from Linux computers</span></span>
10. <span data-ttu-id="4f145-134">Собирать события ошибок и предупреждений из hello журнал событий приложений с компьютеров Windows</span><span class="sxs-lookup"><span data-stu-id="4f145-134">Collect Error and Warning events from hello Application Event Log from Windows computers</span></span>
11. <span data-ttu-id="4f145-135">Сбор данных счетчика производительности "Доступный объем памяти" (в МБ) с компьютеров Windows</span><span class="sxs-lookup"><span data-stu-id="4f145-135">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
12. <span data-ttu-id="4f145-136">Сбор пользовательского журнала</span><span class="sxs-lookup"><span data-stu-id="4f145-136">Collect a custom log</span></span> 

```

$ResourceGroup = "oms-example"
$WorkspaceName = "log-analytics-" + (Get-Random -Maximum 99999) # workspace names need toobe unique - Get-Random helps with this for hello example code
$Location = "westeurope"

# List of solutions tooenable
$Solutions = "Security", "Updates", "SQLAssessment"

# Saved Searches tooimport
$ExportedSearches = @"
[
    {
        "Category":  "My Saved Searches",
        "DisplayName":  "WAD Events (All)",
        "Query":  "Type=Event SourceSystem:AzureStorage ",
        "Version":  1
    },
    {        
        "Category":  "My Saved Searches",
        "DisplayName":  "Current Disk Queue Length",
        "Query":  "Type=Perf ObjectName=LogicalDisk InstanceName=\"C:\" CounterName=\"Current Disk Queue Length\"",
        "Version":  1
    }
]
"@ | ConvertFrom-Json

# Custom Log toocollect
$CustomLog = @"
{
    "customLogName": "sampleCustomLog1", 
    "description": "Example custom log datasource", 
    "inputs": [
        { 
            "location": { 
            "fileSystemLocations": { 
                "windowsFileTypeLogPaths": [ "e:\\iis5\\*.log" ], 
                "linuxFileTypeLogPaths": [ "/var/logs" ] 
                } 
            }, 
        "recordDelimiter": { 
            "regexDelimiter": { 
                "pattern": "\\n", 
                "matchIndex": 0, 
                "matchIndexSpecified": true, 
                "numberedGroup": null 
                } 
            } 
        }
    ], 
    "extractions": [
        { 
            "extractionName": "TimeGenerated", 
            "extractionType": "DateTime", 
            "extractionProperties": { 
                "dateTimeExtraction": { 
                    "regex": null, 
                    "joinStringRegex": null 
                    } 
                } 
            }
        ] 
    }
"@

# Create hello resource group if needed
try {
    Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop
} catch {
    New-AzureRmResourceGroup -Name $ResourceGroup -Location $Location
}

# Create hello workspace
New-AzureRmOperationalInsightsWorkspace -Location $Location -Name $WorkspaceName -Sku Standard -ResourceGroupName $ResourceGroup

# List all solutions and their installation status
Get-AzureRmOperationalInsightsIntelligencePacks -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Add solutions
foreach ($solution in $Solutions) {
    Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -IntelligencePackName $solution -Enabled $true
}

#List enabled solutions
(Get-AzureRmOperationalInsightsIntelligencePacks -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName).Where({($_.enabled -eq $true)})

# Import Saved Searches
foreach ($search in $ExportedSearches) {
    $id = $search.Category + "|" + $search.DisplayName
    New-AzureRmOperationalInsightsSavedSearch -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId $id -DisplayName $search.DisplayName -Category $search.Category -Query $search.Query -Version $search.Version
}

# Export Saved Searches
(Get-AzureRmOperationalInsightsSavedSearch -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName).Value.Properties | ConvertTo-Json 

# Create Computer Group based on a query
New-AzureRmOperationalInsightsComputerGroup -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId "My Web Servers" -DisplayName "Web Servers" -Category "My Saved Searches" -Query "Computer=""web*"" | distinct Computer" -Version 1

# Create a computer group based on names (up too5000)
$computerGroup = """servername1.contoso.com"",""servername2.contoso.com"",""servername3.contoso.com"",""servername4.contoso.com"""
New-AzureRmOperationalInsightsComputerGroup -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId "My Named Servers" -DisplayName "Named Servers" -Category "My Saved Searches" -Query $computerGroup -Version 1

# Enable IIS Log Collection using agent
Enable-AzureRmOperationalInsightsIISLogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Linux Perf
New-AzureRmOperationalInsightsLinuxPerformanceObjectDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -ObjectName "Logical Disk" -InstanceName "*"  -CounterNames @("% Used Inodes", "Free Megabytes", "% Used Space", "Disk Transfers/sec", "Disk Reads/sec", "Disk Reads/sec", "Disk Writes/sec") -IntervalSeconds 20  -Name "Example Linux Disk Performance Counters"
Enable-AzureRmOperationalInsightsLinuxCustomLogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Linux Syslog
New-AzureRmOperationalInsightsLinuxSyslogDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -Facility "kern" -CollectEmergency -CollectAlert -CollectCritical -CollectError -CollectWarning -Name "Example kernal syslog collection"
Enable-AzureRmOperationalInsightsLinuxSyslogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Windows Event
New-AzureRmOperationalInsightsWindowsEventDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -EventLogName "Application" -CollectErrors -CollectWarnings -Name "Example Application Event Log"

# Windows Perf
New-AzureRmOperationalInsightsWindowsPerformanceCounterDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -ObjectName "Memory" -InstanceName "*" -CounterName "Available MBytes" -IntervalSeconds 20 -Name "Example Windows Performance Counter"

# Custom Logs
New-AzureRmOperationalInsightsCustomLogDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -CustomLogRawJson "$CustomLog" -Name "Example Custom Log Collection"

```

## <a name="configuring-log-analytics-tooindex-azure-diagnostics"></a><span data-ttu-id="4f145-137">Настройка tooindex анализа журналов диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="4f145-137">Configuring Log Analytics tooindex Azure diagnostics</span></span>
<span data-ttu-id="4f145-138">Для безагентного отслеживания ресурсов Azure hello ресурсы требуют рабочей областью аналитики журналов tooa toohave диагностики Azure toowrite включен и настроен.</span><span class="sxs-lookup"><span data-stu-id="4f145-138">For agentless monitoring of Azure resources, hello resources need toohave Azure diagnostics enabled and configured toowrite tooa Log Analytics workspace.</span></span> <span data-ttu-id="4f145-139">Этот подход отправляет данные непосредственно tooLog Analytics и не требует toobe данных, записанных tooa учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="4f145-139">This approach sends data directly tooLog Analytics and does not require data toobe written tooa storage account.</span></span> <span data-ttu-id="4f145-140">Ниже перечислены поддерживаемые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="4f145-140">Supported resources include:</span></span>

| <span data-ttu-id="4f145-141">Тип ресурса</span><span class="sxs-lookup"><span data-stu-id="4f145-141">Resource Type</span></span> | <span data-ttu-id="4f145-142">Журналы</span><span class="sxs-lookup"><span data-stu-id="4f145-142">Logs</span></span> | <span data-ttu-id="4f145-143">Метрики</span><span class="sxs-lookup"><span data-stu-id="4f145-143">Metrics</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4f145-144">Шлюзы приложений</span><span class="sxs-lookup"><span data-stu-id="4f145-144">Application Gateways</span></span>    | <span data-ttu-id="4f145-145">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-145">Yes</span></span> | <span data-ttu-id="4f145-146">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-146">Yes</span></span> |
| <span data-ttu-id="4f145-147">Учетные записи службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="4f145-147">Automation accounts</span></span>     | <span data-ttu-id="4f145-148">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-148">Yes</span></span> | |
| <span data-ttu-id="4f145-149">Учетные записи пакетной службы</span><span class="sxs-lookup"><span data-stu-id="4f145-149">Batch accounts</span></span>          | <span data-ttu-id="4f145-150">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-150">Yes</span></span> | <span data-ttu-id="4f145-151">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-151">Yes</span></span> |
| <span data-ttu-id="4f145-152">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4f145-152">Data Lake analytics</span></span>     | <span data-ttu-id="4f145-153">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-153">Yes</span></span> | | 
| <span data-ttu-id="4f145-154">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4f145-154">Data Lake store</span></span>         | <span data-ttu-id="4f145-155">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-155">Yes</span></span> | |
| <span data-ttu-id="4f145-156">пул эластичных баз данных SQL;</span><span class="sxs-lookup"><span data-stu-id="4f145-156">Elastic SQL Pool</span></span>        |     | <span data-ttu-id="4f145-157">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-157">Yes</span></span> |
| <span data-ttu-id="4f145-158">пространство имен концентратора событий;</span><span class="sxs-lookup"><span data-stu-id="4f145-158">Event Hub namespace</span></span>     |     | <span data-ttu-id="4f145-159">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-159">Yes</span></span> |
| <span data-ttu-id="4f145-160">Центры Интернета вещей;</span><span class="sxs-lookup"><span data-stu-id="4f145-160">IoT Hubs</span></span>                |     | <span data-ttu-id="4f145-161">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-161">Yes</span></span> |
| <span data-ttu-id="4f145-162">Хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="4f145-162">Key Vault</span></span>               | <span data-ttu-id="4f145-163">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-163">Yes</span></span> | |
| <span data-ttu-id="4f145-164">Балансировщики нагрузки</span><span class="sxs-lookup"><span data-stu-id="4f145-164">Load Balancers</span></span>          | <span data-ttu-id="4f145-165">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-165">Yes</span></span> | |
| <span data-ttu-id="4f145-166">Приложения логики</span><span class="sxs-lookup"><span data-stu-id="4f145-166">Logic Apps</span></span>              | <span data-ttu-id="4f145-167">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-167">Yes</span></span> | <span data-ttu-id="4f145-168">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-168">Yes</span></span> |
| <span data-ttu-id="4f145-169">группы сетевой безопасности;</span><span class="sxs-lookup"><span data-stu-id="4f145-169">Network Security Groups</span></span> | <span data-ttu-id="4f145-170">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-170">Yes</span></span> | |
| <span data-ttu-id="4f145-171">Кэш Redis</span><span class="sxs-lookup"><span data-stu-id="4f145-171">Redis Cache</span></span>             |     | <span data-ttu-id="4f145-172">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-172">Yes</span></span> |
| <span data-ttu-id="4f145-173">Службы поиска</span><span class="sxs-lookup"><span data-stu-id="4f145-173">Search services</span></span>         | <span data-ttu-id="4f145-174">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-174">Yes</span></span> | <span data-ttu-id="4f145-175">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-175">Yes</span></span> |
| <span data-ttu-id="4f145-176">Пространство имен служебной шины</span><span class="sxs-lookup"><span data-stu-id="4f145-176">Service Bus namespace</span></span>   |     | <span data-ttu-id="4f145-177">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-177">Yes</span></span> |
| <span data-ttu-id="4f145-178">SQL (версия 12)</span><span class="sxs-lookup"><span data-stu-id="4f145-178">SQL (v12)</span></span>               |     | <span data-ttu-id="4f145-179">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-179">Yes</span></span> |
| <span data-ttu-id="4f145-180">Веб-сайты</span><span class="sxs-lookup"><span data-stu-id="4f145-180">Web Sites</span></span>               |     | <span data-ttu-id="4f145-181">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-181">Yes</span></span> |
| <span data-ttu-id="4f145-182">Фермы веб-серверов</span><span class="sxs-lookup"><span data-stu-id="4f145-182">Web Server farms</span></span>        |     | <span data-ttu-id="4f145-183">Да</span><span class="sxs-lookup"><span data-stu-id="4f145-183">Yes</span></span> |

<span data-ttu-id="4f145-184">Подробности hello доступных метрик hello ссылаться слишком[поддерживаемых метрик с помощью монитора Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="4f145-184">For hello details of hello available metrics, refer too[supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="4f145-185">Hello сведений о доступных журналов hello, см. в разделе слишком[поддерживается для журналов диагностики служб и схемы](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span><span class="sxs-lookup"><span data-stu-id="4f145-185">For hello details of hello available logs, refer too[supported services and schema for diagnostic logs](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span></span>

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

<span data-ttu-id="4f145-186">Также можно использовать hello предшествующий командлет toocollect журналы из ресурсов, которые находятся в разных подписках.</span><span class="sxs-lookup"><span data-stu-id="4f145-186">You can also use hello preceding cmdlet toocollect logs from resources that are in different subscriptions.</span></span> <span data-ttu-id="4f145-187">командлет Hello является может toowork между подписками, так как вы указываете идентификатор hello оба ресурса hello Создание журналов и отправляемые журналы hello hello рабочей области.</span><span class="sxs-lookup"><span data-stu-id="4f145-187">hello cmdlet is able toowork across subscriptions since you are providing hello id of both hello resource creating logs and hello workspace hello logs are sent to.</span></span>


## <a name="configuring-log-analytics-tooindex-azure-diagnostics-from-storage"></a><span data-ttu-id="4f145-188">Настройка tooindex анализа журналов диагностики Azure из хранилища</span><span class="sxs-lookup"><span data-stu-id="4f145-188">Configuring Log Analytics tooindex Azure diagnostics from storage</span></span>
<span data-ttu-id="4f145-189">toocollect данных журнала из в выполняющемся экземпляре классический облачной службы или кластера service fabric, необходимо toofirst записи hello данных tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="4f145-189">toocollect log data from within a running instance of a classic cloud service or a service fabric cluster, you need toofirst write hello data tooAzure storage.</span></span> <span data-ttu-id="4f145-190">Служба аналитики журналов будет настроен toocollect hello журналов из учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="4f145-190">Log Analytics is then configured toocollect hello logs from hello storage account.</span></span> <span data-ttu-id="4f145-191">Ниже перечислены поддерживаемые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="4f145-191">Supported resources include:</span></span>

* <span data-ttu-id="4f145-192">классические облачные службы (рабочие и веб-роли);</span><span class="sxs-lookup"><span data-stu-id="4f145-192">Classic cloud services (web and worker roles)</span></span>
* <span data-ttu-id="4f145-193">кластеры Service Fabric;</span><span class="sxs-lookup"><span data-stu-id="4f145-193">Service fabric clusters</span></span>

<span data-ttu-id="4f145-194">Следующий пример показывает как Hello для:</span><span class="sxs-lookup"><span data-stu-id="4f145-194">hello following example shows how to:</span></span>

1. <span data-ttu-id="4f145-195">Список существующих учетных записей хранения hello и расположения, которые служба аналитики журналов будет индексировать данные из</span><span class="sxs-lookup"><span data-stu-id="4f145-195">List hello existing storage accounts and locations that Log Analytics will index data from</span></span>
2. <span data-ttu-id="4f145-196">Создание tooread конфигурации из учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="4f145-196">Create a configuration tooread from a storage account</span></span>
3. <span data-ttu-id="4f145-197">Вновь созданные tooindex данные конфигурации из дополнительных расположениях hello обновления</span><span class="sxs-lookup"><span data-stu-id="4f145-197">Update hello newly created configuration tooindex data from additional locations</span></span>
4. <span data-ttu-id="4f145-198">Удалить конфигурацию только что созданный hello</span><span class="sxs-lookup"><span data-stu-id="4f145-198">Delete hello newly created configuration</span></span>

```
# validTables = "WADWindowsEventLogsTable", "LinuxsyslogVer2v0", "WADServiceFabric*EventTable", "WADETWEventTable" 
$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq "your workspace name"})

# Update these two lines with hello storage account resource ID and hello storage account key for hello storage account you want tooLog Analytics too 
$storageId = "/subscriptions/ec11ca60-1234-491e-5678-0ea07feae25c/resourceGroups/demo/providers/Microsoft.Storage/storageAccounts/wadv2storage"
$key = "abcd=="

# List existing insights
Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

# Create a new insight
New-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -StorageAccountResourceId $storageId -StorageAccountKey $key -Tables @("WADWindowsEventLogsTable") -Containers @("wad-iis-logfiles")

# Update existing insight
Set-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -Tables @("WADWindowsEventLogsTable", "WADETWEventTable") -Containers @("wad-iis-logfiles")

# Remove hello insight
Remove-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" 

```

<span data-ttu-id="4f145-199">Также можно использовать hello предшествует журналы toocollect сценариев из учетных записей хранения в разных подписках.</span><span class="sxs-lookup"><span data-stu-id="4f145-199">You can also use hello preceding script toocollect logs from storage accounts in different subscriptions.</span></span> <span data-ttu-id="4f145-200">сценарий Hello — может toowork между подписками, поскольку вы указываете идентификатор ресурса для учетной записи хранилища hello и соответствующий ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="4f145-200">hello script is able toowork across subscriptions since you are providing hello storage account resource id and a corresponding access key.</span></span> <span data-ttu-id="4f145-201">При изменении ключа доступа hello необходимо tooupdate hello анализ toohave hello новый ключ хранилища.</span><span class="sxs-lookup"><span data-stu-id="4f145-201">When you change hello access key, you need tooupdate hello storage insight toohave hello new key.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4f145-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4f145-202">Next steps</span></span>
* <span data-ttu-id="4f145-203">Дополнительные сведения об использовании PowerShell для настройки Log Analytics см. в [описании командлетов PowerShell Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx).</span><span class="sxs-lookup"><span data-stu-id="4f145-203">[Review Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for additional information on using PowerShell for configuration of Log Analytics.</span></span>

