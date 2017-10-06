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
# <a name="manage-log-analytics-using-powershell"></a>Управление Log Analytics с помощью PowerShell
Можно использовать hello [командлеты PowerShell аналитика журналов](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform различные функции в службе анализа журналов из командной строки или как часть сценария.  Примеры hello задачи, которые можно выполнять с помощью PowerShell.

* Создание рабочей области
* Добавление или удаление решения
* Импорт и экспорт сохраненных поисков
* Создание группы компьютеров
* Включить сбор журналов IIS с компьютеров с установленным агентом Windows hello
* Сбор счетчиков производительности с компьютеров под управлением Linux и Windows
* Сбор событий из системного журнала с компьютеров Linux 
* Сбор событий из журналов событий Windows
* Сбор пользовательских журналов событий
* Добавить hello журнала аналитика агента tooan виртуальной машины Azure
* Настройка журнала аналитика tooindex собранные средствами диагностики Azure

Эта статья содержит два образца кода, иллюстрирующие некоторых функций hello, которые можно выполнять из PowerShell.  Можно ссылаться toohello [Справочник по командлетам PowerShell аналитика журналов](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) для других функций.

> [!NOTE]
> Служба аналитики журналов был вызван ранее оперативной аналитики, поэтому это hello имя, используемое в командлетах hello.
> 
> 

## <a name="prerequisites"></a>Предварительные требования
Эти примеры работают с версию 2.3.0 или более поздней версии модуля AzureRm.OperationalInsights hello.


## <a name="create-and-configure-a-log-analytics-workspace"></a>Создание и настройка рабочей области Log Analytics
Hello следующий скрипт образец показывает, как:

1. Создание рабочей области
2. Список hello доступные решения
3. Добавление рабочей области toohello решений
4. Импорт сохраненных поисков
5. Экспорт сохраненных поисков
6. Создание группы компьютеров
7. Включить сбор журналов IIS с компьютеров с установленным агентом Windows hello
8. Сбор счетчиков производительности логического диска с компьютеров под управлением Linux ("Процент использования индексных дескрипторов"; "Свободно мегабайт"; "Процент используемого места"; "Количество обращений к диску (в секунду)"; "Количество обращений чтения или записи (в секунду))"
9. Сбор событий из системного журнала с компьютеров Linux
10. Собирать события ошибок и предупреждений из hello журнал событий приложений с компьютеров Windows
11. Сбор данных счетчика производительности "Доступный объем памяти" (в МБ) с компьютеров Windows
12. Сбор пользовательского журнала 

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

## <a name="configuring-log-analytics-tooindex-azure-diagnostics"></a>Настройка tooindex анализа журналов диагностики Azure
Для безагентного отслеживания ресурсов Azure hello ресурсы требуют рабочей областью аналитики журналов tooa toohave диагностики Azure toowrite включен и настроен. Этот подход отправляет данные непосредственно tooLog Analytics и не требует toobe данных, записанных tooa учетной записи хранилища. Ниже перечислены поддерживаемые ресурсы.

| Тип ресурса | Журналы | Метрики |
| --- | --- | --- |
| Шлюзы приложений    | Да | Да |
| Учетные записи службы автоматизации     | Да | |
| Учетные записи пакетной службы          | Да | Да |
| Data Lake Analytics     | Да | | 
| Data Lake Store         | Да | |
| пул эластичных баз данных SQL;        |     | Да |
| пространство имен концентратора событий;     |     | Да |
| Центры Интернета вещей;                |     | Да |
| Хранилище ключей               | Да | |
| Балансировщики нагрузки          | Да | |
| Приложения логики              | Да | Да |
| группы сетевой безопасности; | Да | |
| Кэш Redis             |     | Да |
| Службы поиска         | Да | Да |
| Пространство имен служебной шины   |     | Да |
| SQL (версия 12)               |     | Да |
| Веб-сайты               |     | Да |
| Фермы веб-серверов        |     | Да |

Подробности hello доступных метрик hello ссылаться слишком[поддерживаемых метрик с помощью монитора Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md).

Hello сведений о доступных журналов hello, см. в разделе слишком[поддерживается для журналов диагностики служб и схемы](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

Также можно использовать hello предшествующий командлет toocollect журналы из ресурсов, которые находятся в разных подписках. командлет Hello является может toowork между подписками, так как вы указываете идентификатор hello оба ресурса hello Создание журналов и отправляемые журналы hello hello рабочей области.


## <a name="configuring-log-analytics-tooindex-azure-diagnostics-from-storage"></a>Настройка tooindex анализа журналов диагностики Azure из хранилища
toocollect данных журнала из в выполняющемся экземпляре классический облачной службы или кластера service fabric, необходимо toofirst записи hello данных tooAzure хранилища. Служба аналитики журналов будет настроен toocollect hello журналов из учетной записи хранения hello. Ниже перечислены поддерживаемые ресурсы.

* классические облачные службы (рабочие и веб-роли);
* кластеры Service Fabric;

Следующий пример показывает как Hello для:

1. Список существующих учетных записей хранения hello и расположения, которые служба аналитики журналов будет индексировать данные из
2. Создание tooread конфигурации из учетной записи хранения
3. Вновь созданные tooindex данные конфигурации из дополнительных расположениях hello обновления
4. Удалить конфигурацию только что созданный hello

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

Также можно использовать hello предшествует журналы toocollect сценариев из учетных записей хранения в разных подписках. сценарий Hello — может toowork между подписками, поскольку вы указываете идентификатор ресурса для учетной записи хранилища hello и соответствующий ключ доступа. При изменении ключа доступа hello необходимо tooupdate hello анализ toohave hello новый ключ хранилища.


## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения об использовании PowerShell для настройки Log Analytics см. в [описании командлетов PowerShell Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx).

