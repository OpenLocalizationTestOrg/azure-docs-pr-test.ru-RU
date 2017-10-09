---
title: "aaaCollect Azure службы журналов и метрики для службы анализа журналов | Документы Microsoft"
description: "Настройка диагностики на ресурсы Azure toowrite журналы и показатели tooLog Analytics."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 84105740-3697-4109-bc59-2452c1131bfe
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1cede9a94ec83c4e3a95853dc2ec355d8df06d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="collect-azure-service-logs-and-metrics-for-use-in-log-analytics"></a>Сбор журналов и метрик для служб Azure для использования в Log Analytics

Сбор журналов и метрик для служб Azure можно выполнить четырьмя разными способами:

1. TooLog аналитика прямой диагностики Azure (*диагностики* в следующей таблице hello)
2. TooLog tooAzure хранилища для диагностики Azure Analytics (*хранения* в следующей таблице hello)
3. Соединители для служб Azure (*соединители* в следующей таблице hello)
4. Сценарии toocollect, а затем данные post в службе анализа журналов (в следующей таблице hello и для служб, которые не указаны, то пустые)


| служба                 | Тип ресурса                           | Журналы        | Метрики     | Решение |
| --- | --- | --- | --- | --- |
| Шлюзы приложений    | Microsoft.Network/applicationGateways   | Диагностика | Диагностика | [Анализ шлюзов приложений Azure](log-analytics-azure-networking-analytics.md#azure-application-gateway-analytics-solution-in-log-analytics) |
| Application Insights    |                                         | Соединитель   | Соединитель   | [Соединитель Application Insights](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/) (предварительная версия) |
| Учетные записи службы автоматизации     | Microsoft.Automation/AutomationAccounts | Диагностика |             | [Дополнительные сведения](../automation/automation-manage-send-joblogs-log-analytics.md)|
| Учетные записи пакетной службы          | Microsoft.Batch/batchAccounts           | Диагностика | Диагностика | |
| Классические облачные службы  |                                         | Хранилище     |             | [Дополнительные сведения](log-analytics-azure-storage-iis-table.md) |
| Cognitive Services      | Microsoft.CognitiveServices/accounts    |             | Диагностика | |
| Data Lake Analytics     | Microsoft.DataLakeAnalytics/accounts    | Диагностика |             | |
| Data Lake Store         | Microsoft.DataLakeStore/accounts        | Диагностика |             | |
| пространство имен концентратора событий;     | Microsoft.EventHub/namespaces           | Диагностика | Диагностика | |
| Центры Интернета вещей;                | Microsoft.Devices/IotHubs               |             | Диагностика | |
| хранилище ключей;               | Microsoft.KeyVault/vaults               | Диагностика |             | [Анализ Key Vault](log-analytics-azure-key-vault.md) |
| Балансировщики нагрузки          | Microsoft.Network/loadBalancers         | Диагностика |             |  |
| Приложения логики              | Microsoft.Logic/workflows <br> Microsoft.Logic/integrationAccounts | Диагностика | Диагностика | |
| группы сетевой безопасности; | Microsoft.Network/networksecuritygroups | Диагностика |             | [Анализ групп безопасности сети Azure](log-analytics-azure-networking-analytics.md#azure-network-security-group-analytics-solution-in-log-analytics) |
| Хранилища восстановления         | Microsoft.RecoveryServices/vaults       |             |             | [Служба анализа служб восстановления Azure (предварительная версия)](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
| Службы поиска         | Microsoft.Search/searchServices         | Диагностика | Диагностика | |
| Пространство имен служебной шины   | Microsoft.ServiceBus/namespaces         | Диагностика | Диагностика | [Служба анализа служебной шины (предварительная версия)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
| Service Fabric          |                                         | Хранилище     |             | [Анализ Service Fabric (предварительная версия)](log-analytics-service-fabric.md) |
| SQL (версия 12)               | Microsoft.Sql/servers/databases <br> Microsoft.Sql/servers/elasticPools |             | Диагностика | [Службы анализа SQL Azure (предварительная версия)](log-analytics-azure-sql.md) |
| Хранилище                 |                                         |             | Скрипт      | [Служба анализа службы хранилища Azure (предварительная версия)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution) |
| Виртуальные машины        | Microsoft.Compute/virtualMachines       | Добавочный номер   | Добавочный номер <br> Диагностика  | |
| Масштабируемые наборы виртуальных машин | Microsoft.Compute/virtualMachines <br> Microsoft.Compute/virtualMachineScaleSets/virtualMachines |             | Диагностика | |
| Фермы веб-серверов        | Microsoft.Web/serverfarms               |             | Диагностика | |
| Веб-сайты               | Microsoft.Web/sites <br> Microsoft.Web/sites/slots |             | Диагностика | [Служба анализа веб-приложений Azure (предварительная версия)](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureWebAppsAnalyticsOMS?tab=Overview) |


> [!NOTE]
> Для мониторинга виртуальных машин Azure (Linux и Windows), рекомендуется устанавливать hello [расширение ВМ аналитика журналов](log-analytics-azure-vm-extension.md). агент Hello предоставляет аналитики, полученные в виртуальных машинах. Можно также использовать расширение hello для набора масштабирования виртуальной машины.
>
>

## <a name="azure-diagnostics-direct-toolog-analytics"></a>Прямой tooLog диагностики Azure Analytics
Многие ресурсы Azure, журналы диагностики может toowrite и метрики, напрямую tooLog аналитика и она hello предпочтительный способ сбора данных hello для обработки. При использовании службы диагностики Azure, данные записываются немедленно tooLog аналитика, и нет данных без необходимости записи toofirst hello toostorage.

Ресурсы Azure, которые поддерживают [монитора Azure](../monitoring-and-diagnostics/monitoring-overview.md) может отправлять свои журналы и показатели непосредственно tooLog Analytics.

* Подробности hello доступных метрик hello ссылаться слишком[поддерживаемых метрик с помощью монитора Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md).
* Hello сведений о доступных журналов hello, см. в разделе слишком[поддерживается для журналов диагностики служб и схемы](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).

### <a name="enable-diagnostics-with-powershell"></a>Включение диагностики с помощью PowerShell
Требуется hello ноябрь 2016 г. (v2.3.0) или более поздней версии версии [Azure PowerShell](/powershell/azure/overview).

Здравствуйте, как следующая PowerShell в примере toouse [AzureRmDiagnosticSetting набор](/powershell/module/azurerm.insights/set-azurermdiagnosticsetting) tooenable диагностики на группы безопасности сети. Hello же подход работает для всех поддерживаемых ресурсов — задать `$resourceId` toohello идентификатор hello ресурс, tooenable диагностики для ресурса.

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO"

Set-AzureRmDiagnosticSetting -ResourceId $ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="enable-diagnostics-with-resource-manager-templates"></a>Включение диагностики с помощью шаблонов Resource Manager

tooenable диагностики для ресурса, когда он создается и диагностики hello отправили анализа журналов tooyour рабочую область, которую можно использовать аналогичный toohello шаблона, один ниже. Этот пример предназначен для учетной записи службы автоматизации, но он также подходит для всех поддерживаемых типов ресурсов.

```json
        {
            "type": "Microsoft.Automation/automationAccounts/providers/diagnosticSettings",
            "name": "[concat(parameters('omsAutomationAccountName'), '/', 'Microsoft.Insights/service')]",
            "apiVersion": "2015-07-01",
            "dependsOn": [
                "[concat('Microsoft.Automation/automationAccounts/', parameters('omsAutomationAccountName'))]",
                "[concat('Microsoft.OperationalInsights/workspaces/', parameters('omsWorkspaceName'))]"
            ],
            "properties": {
                "workspaceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('omsWorkspaceName'))]",
                "logs": [
                    {
                        "category": "JobLogs",
                        "enabled": true
                    },
                    {
                        "category": "JobStreams",
                        "enabled": true
                    }
                ]
            }
        }
```

[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="azure-diagnostics-toostorage-then-toolog-analytics"></a>Toostorage диагностики Azure, а затем tooLog аналитика

Для сбора журналов из в некоторые ресурсы, он возможных toosend hello журналы tooAzure хранилища и затем настройте журналы hello tooread анализа журналов из хранилища.

Служба аналитики журналов можно будет использовать диагностику toocollect этот подход из хранилища Azure для hello следующие журналы и ресурсы:

| Ресурс | Журналы |
| --- | --- |
| Service Fabric |Событие трассировки событий Windows <br> Операционное событие <br> Событие субъектов Reliable Actors <br> Событие надежных служб |
| Виртуальные машины |Системный журнал Linux <br> Событие Windows <br> Журнал IIS <br> Событие трассировки событий Windows |
| веб-роли; <br> Рабочие роли |Системный журнал Linux <br> Событие Windows <br> Журнал IIS <br> Событие трассировки событий Windows |

> [!NOTE]
> Взимается Стандартная Azure плата для хранилища и транзакций при отправке tooa учетной записи хранения диагностики и анализа журналов считывает hello данные из вашей учетной записи хранилища.
>
>

В разделе [используйте хранилище больших двоичных объектов для служб IIS и таблица хранения событий](log-analytics-azure-storage-iis-table.md) toolearn Дополнительные сведения о как служба аналитики журналов может собирать эти журналы.

## <a name="connectors-for-azure-services"></a>Соединители для служб Azure

Отсутствует соединитель для Application Insights, позволяющего данными, собранными toobe Application Insights отправлены tooLog Analytics.

Дополнительные сведения о hello [соединитель Application Insights](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/).

## <a name="scripts-toocollect-and-post-data-toolog-analytics"></a>Сценарии toocollect и post данных tooLog аналитика

Для служб Azure, которые не предоставляют tooLog журналы и показатели toosend прямым способом аналитики можно использовать сценарий автоматизации Azure toocollect hello журнала и метрик. Здравствуйте, затем отправить hello данных tooLog аналитика с помощью Hello сценария можно [API-Интерфейс сборщика данных](log-analytics-data-collector-api.md)

Коллекция Hello Azure шаблонов имеет [примеры использования автоматизации Azure](https://azure.microsoft.com/en-us/resources/templates/?term=OMS) toocollect данные из службы и отправкой tooLog Analytics.

## <a name="next-steps"></a>Дальнейшие действия

* [Использовать хранилище больших двоичных объектов для служб IIS и таблица хранения событий](log-analytics-azure-storage-iis-table.md) tooread hello журналы для служб Azure, которые записывают диагностики tootable хранилища или IIS заносит в журнал запись tooblob хранилища.
* [Включить решения](log-analytics-add-solutions.md) tooprovide понимание данных hello.
* [Использовать запросы поиска](log-analytics-log-searches.md) tooanalyze hello данных.
