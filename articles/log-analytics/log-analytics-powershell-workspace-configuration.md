---
title: "Использование PowerShell для создания и настройки рабочей области Log Analytics | Документация Майкрософт"
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
ms.openlocfilehash: 6807ab67e3593da82c147669b29bfdae3b6c967c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="manage-log-analytics-using-powershell"></a><span data-ttu-id="9dd87-104">Управление Log Analytics с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="9dd87-104">Manage Log Analytics using PowerShell</span></span>
<span data-ttu-id="9dd87-105">[Командлеты PowerShell Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) можно использовать для выполнения различных функций в Log Analytics как из командной строки, так и в составе сценария.</span><span class="sxs-lookup"><span data-stu-id="9dd87-105">You can use the [Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) to perform various functions in Log Analytics from a command line or as part of a script.</span></span>  <span data-ttu-id="9dd87-106">Примеры задач, которые можно выполнять с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9dd87-106">Examples of the tasks you can perform with PowerShell include:</span></span>

* <span data-ttu-id="9dd87-107">Создание рабочей области</span><span class="sxs-lookup"><span data-stu-id="9dd87-107">Create a workspace</span></span>
* <span data-ttu-id="9dd87-108">Добавление или удаление решения</span><span class="sxs-lookup"><span data-stu-id="9dd87-108">Add or remove a solution</span></span>
* <span data-ttu-id="9dd87-109">Импорт и экспорт сохраненных поисков</span><span class="sxs-lookup"><span data-stu-id="9dd87-109">Import and export saved searches</span></span>
* <span data-ttu-id="9dd87-110">Создание группы компьютеров</span><span class="sxs-lookup"><span data-stu-id="9dd87-110">Create a computer group</span></span>
* <span data-ttu-id="9dd87-111">Включение сбора журналов IIS с компьютеров, на которых установлен агент Windows</span><span class="sxs-lookup"><span data-stu-id="9dd87-111">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
* <span data-ttu-id="9dd87-112">Сбор счетчиков производительности с компьютеров под управлением Linux и Windows</span><span class="sxs-lookup"><span data-stu-id="9dd87-112">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="9dd87-113">Сбор событий из системного журнала с компьютеров Linux</span><span class="sxs-lookup"><span data-stu-id="9dd87-113">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="9dd87-114">Сбор событий из журналов событий Windows</span><span class="sxs-lookup"><span data-stu-id="9dd87-114">Collect events from Windows event logs</span></span>
* <span data-ttu-id="9dd87-115">Сбор пользовательских журналов событий</span><span class="sxs-lookup"><span data-stu-id="9dd87-115">Collect custom event logs</span></span>
* <span data-ttu-id="9dd87-116">Добавление агента Log Analytics в виртуальную машину Azure</span><span class="sxs-lookup"><span data-stu-id="9dd87-116">Add the log analytics agent to an Azure virtual machine</span></span>
* <span data-ttu-id="9dd87-117">Настройка Log Analytics для индексирования данных, собранных системой диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="9dd87-117">Configure log analytics to index data collected using Azure diagnostics</span></span>

<span data-ttu-id="9dd87-118">Эта статья содержит два примера кода, иллюстрирующих некоторые доступные в PowerShell функции.</span><span class="sxs-lookup"><span data-stu-id="9dd87-118">This article provides two code samples that illustrate some of the functions that you can perform from PowerShell.</span></span>  <span data-ttu-id="9dd87-119">Сведения о других функциях см. в [справочнике по командлетам PowerShell Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx).</span><span class="sxs-lookup"><span data-stu-id="9dd87-119">You can refer to the [Log Analytics PowerShell cmdlet reference](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for other functions.</span></span>

> [!NOTE]
> <span data-ttu-id="9dd87-120">Компонент Log Analytics раньше назывался Operational Insights, поэтому именно такое имя используется в командлетах.</span><span class="sxs-lookup"><span data-stu-id="9dd87-120">Log Analytics was previously called Operational Insights, which is why it is the name used in the cmdlets.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="9dd87-121">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9dd87-121">Prerequisites</span></span>
<span data-ttu-id="9dd87-122">Эти примеры работают с версией 2.3.0 или более поздней версией модуля AzureRm.OperationalInsights.</span><span class="sxs-lookup"><span data-stu-id="9dd87-122">These examples work with version 2.3.0 or later of the AzureRm.OperationalInsights module.</span></span>


## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="9dd87-123">Создание и настройка рабочей области Log Analytics</span><span class="sxs-lookup"><span data-stu-id="9dd87-123">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="9dd87-124">Этот пример сценария иллюстрирует следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="9dd87-124">The following script sample illustrates how to:</span></span>

1. <span data-ttu-id="9dd87-125">Создание рабочей области</span><span class="sxs-lookup"><span data-stu-id="9dd87-125">Create a workspace</span></span>
2. <span data-ttu-id="9dd87-126">Вывод списка доступных решений</span><span class="sxs-lookup"><span data-stu-id="9dd87-126">List the available solutions</span></span>
3. <span data-ttu-id="9dd87-127">Добавление решений в рабочую область</span><span class="sxs-lookup"><span data-stu-id="9dd87-127">Add solutions to the workspace</span></span>
4. <span data-ttu-id="9dd87-128">Импорт сохраненных поисков</span><span class="sxs-lookup"><span data-stu-id="9dd87-128">Import saved searches</span></span>
5. <span data-ttu-id="9dd87-129">Экспорт сохраненных поисков</span><span class="sxs-lookup"><span data-stu-id="9dd87-129">Export saved searches</span></span>
6. <span data-ttu-id="9dd87-130">Создание группы компьютеров</span><span class="sxs-lookup"><span data-stu-id="9dd87-130">Create a computer group</span></span>
7. <span data-ttu-id="9dd87-131">Включение сбора журналов IIS с компьютеров, на которых установлен агент Windows</span><span class="sxs-lookup"><span data-stu-id="9dd87-131">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
8. <span data-ttu-id="9dd87-132">Сбор счетчиков производительности логического диска с компьютеров под управлением Linux ("Процент использования индексных дескрипторов"; "Свободно мегабайт"; "Процент используемого места"; "Количество обращений к диску (в секунду)"; "Количество обращений чтения или записи (в секунду))"</span><span class="sxs-lookup"><span data-stu-id="9dd87-132">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
9. <span data-ttu-id="9dd87-133">Сбор событий из системного журнала с компьютеров Linux</span><span class="sxs-lookup"><span data-stu-id="9dd87-133">Collect syslog events from Linux computers</span></span>
10. <span data-ttu-id="9dd87-134">Сбор событий (ошибок и предупреждений) из журнала событий приложений с компьютеров Windows</span><span class="sxs-lookup"><span data-stu-id="9dd87-134">Collect Error and Warning events from the Application Event Log from Windows computers</span></span>
11. <span data-ttu-id="9dd87-135">Сбор данных счетчика производительности "Доступный объем памяти" (в МБ) с компьютеров Windows</span><span class="sxs-lookup"><span data-stu-id="9dd87-135">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
12. <span data-ttu-id="9dd87-136">Сбор пользовательского журнала</span><span class="sxs-lookup"><span data-stu-id="9dd87-136">Collect a custom log</span></span> 

```

$ResourceGroup = "oms-example"
$WorkspaceName = "log-analytics-" + (Get-Random -Maximum 99999) # workspace names need to be unique - Get-Random helps with this for the example code
$Location = "westeurope"

# List of solutions to enable
$Solutions = "Security", "Updates", "SQLAssessment"

# Saved Searches to import
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

# Custom Log to collect
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

# Create the resource group if needed
try {
    Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop
} catch {
    New-AzureRmResourceGroup -Name $ResourceGroup -Location $Location
}

# Create the workspace
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

# Create a computer group based on names (up to 5000)
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

## <a name="configuring-log-analytics-to-index-azure-diagnostics"></a><span data-ttu-id="9dd87-137">Настройка Log Analytics для индексации системы диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="9dd87-137">Configuring Log Analytics to index Azure diagnostics</span></span>
<span data-ttu-id="9dd87-138">Для отслеживания ресурсов Azure без использования агента необходимо включить для этих ресурсов систему диагностики Azure и настроить ее для записи данных в рабочую область Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="9dd87-138">For agentless monitoring of Azure resources, the resources need to have Azure diagnostics enabled and configured to write to a Log Analytics workspace.</span></span> <span data-ttu-id="9dd87-139">Это позволяет отправлять данные непосредственно в Log Analytics, не записывая их в учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="9dd87-139">This approach sends data directly to Log Analytics and does not require data to be written to a storage account.</span></span> <span data-ttu-id="9dd87-140">Ниже перечислены поддерживаемые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="9dd87-140">Supported resources include:</span></span>

| <span data-ttu-id="9dd87-141">Тип ресурса</span><span class="sxs-lookup"><span data-stu-id="9dd87-141">Resource Type</span></span> | <span data-ttu-id="9dd87-142">Журналы</span><span class="sxs-lookup"><span data-stu-id="9dd87-142">Logs</span></span> | <span data-ttu-id="9dd87-143">Метрики</span><span class="sxs-lookup"><span data-stu-id="9dd87-143">Metrics</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9dd87-144">Шлюзы приложений</span><span class="sxs-lookup"><span data-stu-id="9dd87-144">Application Gateways</span></span>    | <span data-ttu-id="9dd87-145">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-145">Yes</span></span> | <span data-ttu-id="9dd87-146">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-146">Yes</span></span> |
| <span data-ttu-id="9dd87-147">Учетные записи службы автоматизации</span><span class="sxs-lookup"><span data-stu-id="9dd87-147">Automation accounts</span></span>     | <span data-ttu-id="9dd87-148">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-148">Yes</span></span> | |
| <span data-ttu-id="9dd87-149">Учетные записи пакетной службы</span><span class="sxs-lookup"><span data-stu-id="9dd87-149">Batch accounts</span></span>          | <span data-ttu-id="9dd87-150">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-150">Yes</span></span> | <span data-ttu-id="9dd87-151">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-151">Yes</span></span> |
| <span data-ttu-id="9dd87-152">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="9dd87-152">Data Lake analytics</span></span>     | <span data-ttu-id="9dd87-153">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-153">Yes</span></span> | | 
| <span data-ttu-id="9dd87-154">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="9dd87-154">Data Lake store</span></span>         | <span data-ttu-id="9dd87-155">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-155">Yes</span></span> | |
| <span data-ttu-id="9dd87-156">пул эластичных баз данных SQL;</span><span class="sxs-lookup"><span data-stu-id="9dd87-156">Elastic SQL Pool</span></span>        |     | <span data-ttu-id="9dd87-157">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-157">Yes</span></span> |
| <span data-ttu-id="9dd87-158">пространство имен концентратора событий;</span><span class="sxs-lookup"><span data-stu-id="9dd87-158">Event Hub namespace</span></span>     |     | <span data-ttu-id="9dd87-159">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-159">Yes</span></span> |
| <span data-ttu-id="9dd87-160">Центры Интернета вещей;</span><span class="sxs-lookup"><span data-stu-id="9dd87-160">IoT Hubs</span></span>                |     | <span data-ttu-id="9dd87-161">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-161">Yes</span></span> |
| <span data-ttu-id="9dd87-162">Хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="9dd87-162">Key Vault</span></span>               | <span data-ttu-id="9dd87-163">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-163">Yes</span></span> | |
| <span data-ttu-id="9dd87-164">Балансировщики нагрузки</span><span class="sxs-lookup"><span data-stu-id="9dd87-164">Load Balancers</span></span>          | <span data-ttu-id="9dd87-165">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-165">Yes</span></span> | |
| <span data-ttu-id="9dd87-166">Приложения логики</span><span class="sxs-lookup"><span data-stu-id="9dd87-166">Logic Apps</span></span>              | <span data-ttu-id="9dd87-167">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-167">Yes</span></span> | <span data-ttu-id="9dd87-168">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-168">Yes</span></span> |
| <span data-ttu-id="9dd87-169">группы сетевой безопасности;</span><span class="sxs-lookup"><span data-stu-id="9dd87-169">Network Security Groups</span></span> | <span data-ttu-id="9dd87-170">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-170">Yes</span></span> | |
| <span data-ttu-id="9dd87-171">Кэш Redis</span><span class="sxs-lookup"><span data-stu-id="9dd87-171">Redis Cache</span></span>             |     | <span data-ttu-id="9dd87-172">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-172">Yes</span></span> |
| <span data-ttu-id="9dd87-173">Службы поиска</span><span class="sxs-lookup"><span data-stu-id="9dd87-173">Search services</span></span>         | <span data-ttu-id="9dd87-174">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-174">Yes</span></span> | <span data-ttu-id="9dd87-175">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-175">Yes</span></span> |
| <span data-ttu-id="9dd87-176">Пространство имен служебной шины</span><span class="sxs-lookup"><span data-stu-id="9dd87-176">Service Bus namespace</span></span>   |     | <span data-ttu-id="9dd87-177">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-177">Yes</span></span> |
| <span data-ttu-id="9dd87-178">SQL (версия 12)</span><span class="sxs-lookup"><span data-stu-id="9dd87-178">SQL (v12)</span></span>               |     | <span data-ttu-id="9dd87-179">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-179">Yes</span></span> |
| <span data-ttu-id="9dd87-180">Веб-сайты</span><span class="sxs-lookup"><span data-stu-id="9dd87-180">Web Sites</span></span>               |     | <span data-ttu-id="9dd87-181">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-181">Yes</span></span> |
| <span data-ttu-id="9dd87-182">Фермы веб-серверов</span><span class="sxs-lookup"><span data-stu-id="9dd87-182">Web Server farms</span></span>        |     | <span data-ttu-id="9dd87-183">Да</span><span class="sxs-lookup"><span data-stu-id="9dd87-183">Yes</span></span> |

<span data-ttu-id="9dd87-184">Дополнительные сведения о доступных метриках см. в разделе [Метрики, поддерживаемые Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="9dd87-184">For the details of the available metrics, refer to [supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="9dd87-185">Дополнительные сведения о доступных журналах см. в разделе [Поддерживаемые службы и схемы для журналов диагностики](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span><span class="sxs-lookup"><span data-stu-id="9dd87-185">For the details of the available logs, refer to [supported services and schema for diagnostic logs](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span></span>

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

<span data-ttu-id="9dd87-186">Кроме того, вы можете использовать предыдущий командлет для сбора журналов из ресурсов, которые находятся в разных подписках.</span><span class="sxs-lookup"><span data-stu-id="9dd87-186">You can also use the preceding cmdlet to collect logs from resources that are in different subscriptions.</span></span> <span data-ttu-id="9dd87-187">Этот командлет может работать в нескольких подписках, так как вы предоставляете идентификаторы ресурса, для которого создаются журналы, и рабочей области, в которую они отправляются.</span><span class="sxs-lookup"><span data-stu-id="9dd87-187">The cmdlet is able to work across subscriptions since you are providing the id of both the resource creating logs and the workspace the logs are sent to.</span></span>


## <a name="configuring-log-analytics-to-index-azure-diagnostics-from-storage"></a><span data-ttu-id="9dd87-188">Настройка Log Analytics для индексации системы диагностики Azure из хранилища</span><span class="sxs-lookup"><span data-stu-id="9dd87-188">Configuring Log Analytics to index Azure diagnostics from storage</span></span>
<span data-ttu-id="9dd87-189">Для сбора данных журнала из работающего экземпляра классической облачной службы или кластера Service Fabric необходимо сначала записать данные в службу хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9dd87-189">To collect log data from within a running instance of a classic cloud service or a service fabric cluster, you need to first write the data to Azure storage.</span></span> <span data-ttu-id="9dd87-190">После этого следует настроить Log Analytics для сбора журналов из учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="9dd87-190">Log Analytics is then configured to collect the logs from the storage account.</span></span> <span data-ttu-id="9dd87-191">Ниже перечислены поддерживаемые ресурсы:</span><span class="sxs-lookup"><span data-stu-id="9dd87-191">Supported resources include:</span></span>

* <span data-ttu-id="9dd87-192">классические облачные службы (рабочие и веб-роли);</span><span class="sxs-lookup"><span data-stu-id="9dd87-192">Classic cloud services (web and worker roles)</span></span>
* <span data-ttu-id="9dd87-193">кластеры Service Fabric;</span><span class="sxs-lookup"><span data-stu-id="9dd87-193">Service fabric clusters</span></span>

<span data-ttu-id="9dd87-194">В приведенном ниже примере показано, как выполнить следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="9dd87-194">The following example shows how to:</span></span>

1. <span data-ttu-id="9dd87-195">Вывод списка существующих учетных записей хранения и расположений, откуда Log Analytics будет индексировать данные.</span><span class="sxs-lookup"><span data-stu-id="9dd87-195">List the existing storage accounts and locations that Log Analytics will index data from</span></span>
2. <span data-ttu-id="9dd87-196">Создание конфигурации для чтения из учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="9dd87-196">Create a configuration to read from a storage account</span></span>
3. <span data-ttu-id="9dd87-197">Обновление созданной конфигурации для индексирования данных из дополнительных расположений</span><span class="sxs-lookup"><span data-stu-id="9dd87-197">Update the newly created configuration to index data from additional locations</span></span>
4. <span data-ttu-id="9dd87-198">Удаление созданной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9dd87-198">Delete the newly created configuration</span></span>

```
# validTables = "WADWindowsEventLogsTable", "LinuxsyslogVer2v0", "WADServiceFabric*EventTable", "WADETWEventTable" 
$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq "your workspace name"})

# Update these two lines with the storage account resource ID and the storage account key for the storage account you want to Log Analytics to  
$storageId = "/subscriptions/ec11ca60-1234-491e-5678-0ea07feae25c/resourceGroups/demo/providers/Microsoft.Storage/storageAccounts/wadv2storage"
$key = "abcd=="

# List existing insights
Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

# Create a new insight
New-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -StorageAccountResourceId $storageId -StorageAccountKey $key -Tables @("WADWindowsEventLogsTable") -Containers @("wad-iis-logfiles")

# Update existing insight
Set-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -Tables @("WADWindowsEventLogsTable", "WADETWEventTable") -Containers @("wad-iis-logfiles")

# Remove the insight
Remove-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" 

```

<span data-ttu-id="9dd87-199">Кроме того, вы можете использовать предыдущий сценарий для сбора журналов из учетных записей хранения, которые находятся в разных подписках.</span><span class="sxs-lookup"><span data-stu-id="9dd87-199">You can also use the preceding script to collect logs from storage accounts in different subscriptions.</span></span> <span data-ttu-id="9dd87-200">Этот сценарий может работать в нескольких подписках, так как вы предоставляете идентификатор ресурса учетной записи хранения и соответствующий ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="9dd87-200">The script is able to work across subscriptions since you are providing the storage account resource id and a corresponding access key.</span></span> <span data-ttu-id="9dd87-201">При изменении ключа доступа необходимо обновить данные хранилища с учетом нового ключа.</span><span class="sxs-lookup"><span data-stu-id="9dd87-201">When you change the access key, you need to update the storage insight to have the new key.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9dd87-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9dd87-202">Next steps</span></span>
* <span data-ttu-id="9dd87-203">Дополнительные сведения об использовании PowerShell для настройки Log Analytics см. в [описании командлетов PowerShell Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx).</span><span class="sxs-lookup"><span data-stu-id="9dd87-203">[Review Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for additional information on using PowerShell for configuration of Log Analytics.</span></span>

