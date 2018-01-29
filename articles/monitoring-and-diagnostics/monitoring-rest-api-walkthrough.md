---
title: "Пошаговое руководство по REST API Azure Monitor | Документация Майкрософт"
description: "Эта статья содержит сведения об аутентификации запросов и использовании REST API Azure Monitor для получения доступных определений и значений метрик."
author: mcollier
manager: 
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 565e6a88-3131-4a48-8b82-3effc9a3d5c6
ms.service: monitoring-and-diagnostics
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: 
ms.search.region: 
ms.search.scope: 
ms.search.validFrom: 
ms.dyn365.ops.version: 
ms.topic: article
ms.date: 09/18/2017
ms.author: mcollier
ms.openlocfilehash: 357a63c65a4f6864dca259aad8a76f83681cd501
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/08/2017
---
# <a name="azure-monitoring-rest-api-walkthrough"></a>Пошаговое руководство по REST API Azure Monitor
В этой статье показано, как выполнять аутентификацию таким образом, чтобы в коде можно было использовать [справочник по REST API Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).         

API Azure Monitor позволяет программно получить определения доступных метрик по умолчанию, детализацию и значения метрик. Данные можно сохранить в отдельном хранилище данных, в том числе в базе данных SQL Azure, Azure Cosmos DB или Azure Data Lake. Там при необходимости можно выполнить дополнительный анализ.

Помимо работы с различными точками данных метрик API Monitor позволяет также получить список правил генерации оповещений, просмотреть журналы действий и многое другое. Полный список доступных операций см. в [справочнике по REST API для Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).

## <a name="authenticating-azure-monitor-requests"></a>Аутентификация запросов Azure Monitor
В первую очередь нужно аутентифицировать запрос.

Все задачи, выполняемые с использованием API Azure Monitor, используют модель аутентификации Azure Resource Manager. Поэтому все запросы должны быть аутентифицированы в Azure Active Directory (Azure AD). Один из способов аутентификации клиентского приложения — создание субъекта-службы Azure AD и получение маркера аутентификации (JWT). Приведенный ниже пример сценария демонстрирует создание субъекта-службы Azure AD посредством PowerShell. Более подробные пошаговые инструкции приведены в документации по [использованию Azure PowerShell для создания субъекта-службы для доступа к ресурсам](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password). Кроме того, [субъект-службу можно создать на портале Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md).

```PowerShell
$subscriptionId = "{azure-subscription-id}"
$resourceGroupName = "{resource-group-name}"

# Authenticate to a specific Azure subscription.
Login-AzureRmAccount -SubscriptionId $subscriptionId

# Password for the service principal
$pwd = "{service-principal-password}"

# Create a new Azure AD application
$azureAdApplication = New-AzureRmADApplication `
                        -DisplayName "My Azure Monitor" `
                        -HomePage "https://localhost/azure-monitor" `
                        -IdentifierUris "https://localhost/azure-monitor" `
                        -Password $pwd

# Create a new service principal associated with the designated application
New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

# Assign Reader role to the newly created service principal
New-AzureRmRoleAssignment -RoleDefinitionName Reader `
                          -ServicePrincipalName $azureAdApplication.ApplicationId.Guid

```

Чтобы отправить запрос к API Azure Monitor, клиентское приложение должно использовать ранее созданный субъект-службу для прохождения аутентификации. В приведенном ниже примере сценария PowerShell показан один подход, в котором для получения токена аутентификации JWT используется [библиотека аутентификации Active Directory](../active-directory/active-directory-authentication-libraries.md) (ADAL). Этот маркер JWT передается как часть параметра проверки подлинности HTTP в запросах к API Azure Monitor.

```PowerShell
$azureAdApplication = Get-AzureRmADApplication -IdentifierUri "https://localhost/azure-monitor"

$subscription = Get-AzureRmSubscription -SubscriptionId $subscriptionId

$clientId = $azureAdApplication.ApplicationId.Guid
$tenantId = $subscription.TenantId
$authUrl = "https://login.microsoftonline.com/${tenantId}"

$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl
$cred = New-Object -TypeName Microsoft.IdentityModel.Clients.ActiveDirectory.ClientCredential -ArgumentList ($clientId, $pwd)

$result = $AuthContext.AcquireToken("https://management.core.windows.net/", $cred)

# Build an array of HTTP header values
$authHeader = @{
'Content-Type'='application/json'
'Accept'='application/json'
'Authorization'=$result.CreateAuthorizationHeader()
}
```

После аутентификации можно будет выполнять запросы к REST API Azure Monitor. Можно использовать два полезных запроса:

1. вывод списка определений метрик для ресурса;
2. получение значений метрик.

## <a name="retrieve-metric-definitions-multi-dimensional-api"></a>Получение определений метрик (многомерные API)

[REST API определений метрик Azure Monitor](https://docs.microsoft.com/rest/api/monitor/metricdefinitions). Используется для доступа к списку метрик, которые доступны для службы.

**Метод**: GET

**URI запроса**: https://management.azure.com/subscriptions/*{идентификатор_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/*{пространство_имен_поставщика_ресурсов}*/*{тип_ресурса}*/*{имя_ресурса}*/providers/microsoft.insights/metricDefinitions?api-version*{версия_API}*

Например, запрос на получение определений метрик для учетной записи хранения Azure будет выглядеть следующим образом:

```PowerShell
$request = "https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Storage/accounts/ContosoStorage/providers/microsoft.insights/metricDefinitions?api-version=2017-05-01-preview"

Invoke-RestMethod -Uri $request `
                  -Headers $authHeader `
                  -Method Get `
                  -OutFile ".\contosostorage-metricdef-results.json" `
                  -Verbose

```
> [!NOTE]
> Чтобы получить определения метрик с помощью многомерных метрик REST API Azure Monitor, используйте 2017-05-01-preview в качестве версии API.
>
>

Полученный текст ответа JSON будет аналогичен приведенному ниже примеру. (Обратите внимание, что вторая метрика имеет измерения.)

```JSON
{
    "value": [
        {
            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Storage/accounts/ContosoStorage/providers/microsoft.insights/metricdefinitions/UsedCapacity",
            "resourceId": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Storage/accounts/ContosoStorage",
            "category": "Capacity",
            "name": {
                "value": "UsedCapacity",
                "localizedValue": "Used capacity"
            },
            "isDimensionRequired": false,
            "unit": "Bytes",
            "primaryAggregationType": "Average",
            "metricAvailabilities": [
                {
                    "timeGrain": "PT1M",
                    "retention": "P30D"
                },
                {
                    "timeGrain": "PT1H",
                    "retention": "P30D"
                }
            ]
        },
        {
            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Storage/accounts/ContosoStorage/providers/microsoft.insights/metricdefinitions/Transactions",
            "resourceId": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Storage/accounts/ContosoStorage",
            "category": "Transaction",
            "name": {
                "value": "Transactions",
                "localizedValue": "Transactions"
            },
            "isDimensionRequired": false,
            "unit": "Count",
            "primaryAggregationType": "Total",
            "metricAvailabilities": [
                {
                    "timeGrain": "PT1M",
                    "retention": "P30D"
                },
                {
                    "timeGrain": "PT1H",
                    "retention": "P30D"
                }
            ],
            "dimensions": [
                {
                    "value": "ResponseType",
                    "localizedValue": "Response type"
                },
                {
                    "value": "GeoType",
                    "localizedValue": "Geo type"
                },
                {
                    "value": "ApiName",
                    "localizedValue": "API name"
                }
            ]
        },
        ...
    ]
}
```

## <a name="retrieve-dimension-values-multi-dimensional-api"></a>Получение значений измерений (многомерные API)
Когда определения доступных метрик известны, могут возникнуть некоторые метрики c измерениями. Перед выполнением запроса для метрик может потребоваться выяснить, какие диапазоны значений имеют измерения. На основе этих значений измерений вы можете выбрать, следует ли фильтровать или сегментировать метрики, на основе значений измерений при запросе метрик. Используйте значение value имени метрики (а не localizedValue) для фильтрации запросов (например, получите точки данных метрик CpuTime и Requests). Если не указано ни одного фильтра, возвращается метрика по умолчанию.

> [!NOTE]
> Чтобы получить значения измерений с помощью REST API Azure Monitor, используйте 2017-05-01-preview в качестве версии API.
>
>

**Метод**: GET

**URI запроса**: https://management.azure.com/subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/*{пространство_имен_поставщиков_ресурсов}*/*{тип_ресурса}*/*{имя_ресурса}*/providers/microsoft.insights/metrics?metric=*{метрика}*&timespan=*{время_начала/время_окончания}*&$filter=*{фильтр}*&resultType=metadata&api-version=*{версия_API}*

Например, запрос на получение списка возможных значений измерений имени API для метрики транзакций в определенный диапазон времени будет выглядеть следующим образом:

```PowerShell
$filter = "APIName eq '*'"
$request = "https://management.azure.com/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Storage/accounts/ContosoStorage/providers/microsoft.insights/metrics?metric=Transactions&timespan=2017-09-01T00:00:00Z/2017-09-10T00:00:00Z&resultType=metadata&$filter=${filter}&api-version=2017-05-01-preview"
Invoke-RestMethod -Uri $request `
    -Headers $authHeader `
    -Method Get `
    -OutFile ".\contosostorage-dimension-values.json" `
    -Verbose
```
Полученный текст ответа JSON будет аналогичен приведенному ниже примеру.

```JSON
{
  "timespan": "2017-09-01T00:00:00Z/2017-09-10T00:00:00Z",
  "value": [
    {
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Storage/accounts/ContosoStorage/providers/Microsoft.Insights/metrics/Transactions",
      "type": "Microsoft.Insights/metrics",
      "name": {
        "value": "Transactions",
        "localizedValue": "Transactions"
      },
      "unit": "Count",
      "timeseries": [
        {
          "metadatavalues": [
            {
              "name": {
                "value": "apiname",
                "localizedValue": "apiname"
              },
              "value": "DeleteBlob"
            }
          ]
        },
        {
          "metadatavalues": [
            {
              "name": {
                "value": "apiname",
                "localizedValue": "apiname"
              },
              "value": "SetBlobProperties"
            }
          ]
        },
        {
          "metadatavalues": [
            {
              "name": {
                "value": "apiname",
                "localizedValue": "apiname"
              },
              "value": "PutPage"
            }
          ]
        },
        {
          "metadatavalues": [
            {
              "name": {
                "value": "apiname",
                "localizedValue": "apiname"
              },
              "value": "Unknown"
            }
          ]
        },
        ...
      ]    
    }
  ]
}
```

## <a name="retrieve-metric-values-multi-dimensional-api"></a>Получение значений метрик (многомерные API)
Когда определения доступных метрик и возможных измерений известны, можно получить соответствующие значения метрик. Используйте значение value имени метрики (а не localizedValue) для запросов фильтрации. Если фильтры измерений не указаны, возвращается агрегированная метрика со сведением.

> [!NOTE]
> Чтобы получить значения многомерных метрик с помощью REST API Azure Monitor, используйте 2017-05-01-preview в качестве версии API.
>
>

**Метод**: GET

**URI запроса**: https://management.azure.com/subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/*{пространство_имен_поставщиков_ресурсов}*/*{тип_ресурса}*/*{имя_ресурса}*/providers/microsoft.insights/metrics?metric=*{метрика}*&timespan=*{время_начала/время_окончания}*&$filter=*{фильтр}*&interval=*{интервал_времени}*&aggregation=*{агрегирование}*&api-version=*{версия_API}*

Например, запрос на получение значений метрики транзакций с хранилищем за 5 минут для всех транзакций с именем API GetBlobProperties будет выглядеть следующим образом:

```PowerShell
$filter = "APIName eq 'GetBlobProperties'"
$request = "https://management.azure.com/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Storage/accounts/ContosoStorage/providers/microsoft.insights/metrics?metric=Transactions&timespan=2017-09-19T02:00:00Z/2017-09-19T02:05:00Z&$filter=${filter}&interval=PT1M&aggregation=Count&api-version=2017-05-01-preview"
Invoke-RestMethod -Uri $request `
    -Headers $authHeader `
    -Method Get `
    -OutFile ".\contosostorage-metric-values.json" `
    -Verbose
```
Полученный текст ответа JSON будет аналогичен приведенному ниже примеру.

```JSON
{
  "cost": 0,
  "timespan": "2017-09-19T02:00:00Z/2017-09-19T02:05:00Z",
  "interval": "PT1M",
  "value": [
    {
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Storage/accounts/ContosoStorage/providers/Microsoft.Insights/metrics/Transactions",
      "type": "Microsoft.Insights/metrics",
      "name": {
        "value": "Transactions",
        "localizedValue": "Transactions"
      },
      "unit": "Count",
      "timeseries": [
        {
          "metadatavalues": [
            {
              "name": {
                "value": "apiname",
                "localizedValue": "apiname"
              },
              "value": "GetBlobProperties"
            }
          ],
          "data": [
            {
              "timeStamp": "2017-09-19T02:00:00Z",
              "count": 2.0
            },
            {
              "timeStamp": "2017-09-19T02:01:00Z",
              "count": 1.0
            },
            {
              "timeStamp": "2017-09-19T02:02:00Z",
              "count": 3.0
            },
            {
              "timeStamp": "2017-09-19T02:03:00Z",
              "count": 7.0
            },
            {
              "timeStamp": "2017-09-19T02:04:00Z",
              "count": 2.0
            }
          ]
        }
      ]
    }
  ]
}
```

## <a name="retrieve-metric-definitions"></a>Получение определений метрик
[REST API определений метрик Azure Monitor](https://msdn.microsoft.com/library/mt743621.aspx). Используется для доступа к списку метрик, которые доступны для службы.

**Метод**: GET

**URI запроса**: https://management.azure.com/subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/*{пространство_имен_поставщиков_ресурсов}*/*{тип_ресурса}*/*{имя_ресурса}*/providers/microsoft.insights/metricDefinitions?api-version*{версия_API}*

Например, чтобы получить определения метрик для приложения логики Azure, запрос будет выглядеть следующим образом:

```PowerShell
$request = "https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets/providers/microsoft.insights/metricDefinitions?api-version=2016-03-01"

Invoke-RestMethod -Uri $request `
                  -Headers $authHeader `
                  -Method Get `
                  -OutFile ".\contostweets-metricdef-results.json" `
                  -Verbose
```
> [!NOTE]
> Чтобы получить определения метрик с помощью REST API Azure Monitor, используйте API версии 2016-03-01.
>
>

Полученный текст ответа JSON будет аналогичен приведенному ниже примеру.
```JSON
{
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets/providers/microsoft.insights/metricdefinitions",
  "value": [
    {
      "name": {
        "value": "RunsStarted",
        "localizedValue": "Runs Started"
      },
      "category": "AllMetrics",
      "startTime": "0001-01-01T00:00:00Z",
      "endTime": "0001-01-01T00:00:00Z",
      "unit": "Count",
      "primaryAggregationType": "Total",
      "resourceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets",
      "resourceId": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets",
      "metricAvailabilities": [
        {
          "timeGrain": "PT1M",
          "retention": "P30D",
          "location": null,
          "blobLocation": null
        },
        {
          "timeGrain": "PT1H",
          "retention": "P30D",
          "location": null,
          "blobLocation": null
        }
      ],
      "properties": null,
      "dimensions": null,
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets/providers/microsoft.insights/metricdefinitions/RunsStarted",
      "supportedAggregationTypes": [ "None", "Average", "Minimum", "Maximum", "Total", "Count" ]
    }
  ]
}
```

Дополнительные сведения см. в статье [List metric definitions for a resource in Azure Monitor REST API](https://msdn.microsoft.com/library/azure/mt743621.aspx) (Вывод списка определений метрик для ресурса в REST API Azure Monitor).

## <a name="retrieve-metric-values"></a>Получение значений метрик
Когда определения доступных метрик известны, можно получить соответствующие значения метрик. Используйте значение value имени метрики (а не localizedValue) для фильтрации запросов (например, получите точки данных метрик CpuTime и Requests). Если не указано ни одного фильтра, возвращается метрика по умолчанию.

> [!NOTE]
> Чтобы получить значения метрики с помощью REST API Azure Monitor, используйте API версии 2016-09-01.
>
>

**Метод**: GET

**URI запроса**: https://management.azure.com/subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/*{пространство_имен_поставщиков_ресурсов}*/*{тип_ресурса}*/*{имя_ресурса*/providers/microsoft.insights/metrics?$filter=*{фильтр}*&api-version=*{версия_API}*

Например, запрос для получения точек данных метрики RunsSucceeded в заданном диапазоне времени с интервалом в 1 час будет выглядеть следующим образом.

```PowerShell
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2017-08-18T19:00:00 and endTime eq 2017-08-18T23:00:00 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets/providers/microsoft.insights/metrics?$filter=${filter}&api-version=2016-09-01"
Invoke-RestMethod -Uri $request `
    -Headers $authHeader `
    -Method Get `
    -OutFile ".\contostweets-metrics-results.json" `
    -Verbose
```

Полученный текст ответа JSON будет аналогичен приведенному ниже примеру.

```JSON
{
  "value": [
    {
      "data": [
        {
          "timeStamp": "2017-08-18T19:00:00Z",
          "total": 0.0
        },
        {
          "timeStamp": "2017-08-18T20:00:00Z",
          "total": 159.0
        },
        {
          "timeStamp": "2017-08-18T21:00:00Z",
          "total": 174.0
        },
        {
          "timeStamp": "2017-08-18T22:00:00Z",
          "total": 97.0
        }
      ],
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets/providers/Microsoft.Insights/metrics/RunsSucceeded",
      "name": {
        "value": "RunsSucceeded",
        "localizedValue": "Runs Succeeded"
      },
      "type": "Microsoft.Insights/metrics",
      "unit": "Count"
    }
  ]
}
```

Чтобы получить несколько точек данных или точек статистической обработки, добавьте имена определений метрик и типы статистической обработки в фильтр, как показано в примере ниже.

```PowerShell
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2017-08-18T21:00:00 and endTime eq 2017-08-18T21:30:00 and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets/providers/microsoft.insights/metrics?$filter=${filter}&api-version=2016-09-01"
Invoke-RestMethod -Uri $request `
    -Headers $authHeader `
    -Method Get `
    -OutFile ".\contostweets-metrics-multiple-results.json" `
    -Verbose
```
Полученный текст ответа JSON будет аналогичен приведенному ниже примеру.

```JSON
{
  "value": [
    {
      "data": [
        {
          "timeStamp": "2017-08-18T21:03:00Z",
          "total": 5.0,
          "average": 1.0
        },
        {
          "timeStamp": "2017-08-18T21:04:00Z",
          "total": 7.0,
          "average": 1.0
        }
      ],
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets/providers/Microsoft.Insights/metrics/ActionsCompleted",
      "name": {
        "value": "ActionsCompleted",
        "localizedValue": "Actions Completed "
      },
      "type": "Microsoft.Insights/metrics",
      "unit": "Count"
    },
    {
      "data": [
        {
          "timeStamp": "2017-08-18T21:03:00Z",
          "total": 5.0,
          "average": 1.0
        },
        {
          "timeStamp": "2017-08-18T21:04:00Z",
          "total": 7.0,
          "average": 1.0
        }
      ],
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets/providers/Microsoft.Insights/metrics/RunsSucceeded",
      "name": {
        "value": "RunsSucceeded",
        "localizedValue": "Runs Succeeded"
      },
      "type": "Microsoft.Insights/metrics",
      "unit": "Count"
    }
  ]
}
```

### <a name="use-armclient"></a>Использование ARMClient
Дополнительно на компьютере Windows можно использовать [ARMClient](https://github.com/projectkudu/armclient). ARMClient автоматически обрабатывает аутентификацию в Azure AD (и полученный маркер JWT). Ниже описано использование ARMClient для получения данных метрик.

1. Установите [Chocolatey](https://chocolatey.org/) и [ARMClient](https://github.com/projectkudu/armclient).
2. В окне терминала введите *armclient.exe login*. После этого отобразится запрос на вход в Azure.
3. Введите *armclient GET [ИД_ресурса]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*.
4. Введите *armclient GET [ИД_ресурса]/providers/microsoft.insights/metrics?api-version=2016-09-01*.

Например, чтобы получить определения метрик для конкретного приложения логики, выполните следующую команду:
```
armclient GET /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets/providers/microsoft.insights/metricDefinitions?api-version=2016-03-01
```


## <a name="retrieve-the-resource-id"></a>Получение идентификатора ресурса
Применение REST API действительно помогает понять доступные определения метрик, детализацию и связанные значения. Эта информация полезна при использовании [библиотеки управления Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).

Для приведенного выше кода используемый идентификатор ресурса — это полный путь к нужному ресурсу Azure. Например, для запроса к веб-приложению Azure идентификатор ресурса будет следующим.

*/subscriptions/{ИД_подписки}/resourceGroups/{имя_группы_ресурсов}/providers/Microsoft.Web/sites/{имя_сайта}/*

Приведенный ниже список содержит несколько примеров форматов идентификаторов различных ресурсов Azure.

* 
            **Центр Интернета вещей**: /subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/Microsoft.Devices/IotHubs/*{имя_центра_IoT}*.
* **Пул эластичных баз данных SQL**: /subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/Microsoft.Sql/servers/*{база_данных_в_пуле}*/elasticpools/*{имя_пула_SQL}*.
* **База данных SQL (версии 12)**: /subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/Microsoft.Sql/servers/*{имя_сервера}*/databases/*{имя_базы_данных}*.
* **Служебная шина**: /subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/Microsoft.ServiceBus/*{пространство_имен}*/*{имя_служебной_шины}*.
* **Масштабируемые наборы виртуальных машин**: /subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{имя_ВМ}*.
* **Виртуальные машины**: /subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/Microsoft.Compute/virtualMachines/*{имя_ВМ}*.
* **Концентраторы событий**: /subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/Microsoft.EventHub/namespaces/*{пространство_имен_концентраторов_событий}*.

Существуют альтернативные подходы к извлечению идентификатора ресурса, включая использование Azure Resource Explorer, PowerShell, интерфейса командной строки Azure и просмотр требуемого ресурса на портале Azure.

### <a name="azure-resource-explorer"></a>Обозреватель ресурсов Azure
Чтобы найти идентификатор требуемого ресурса, удобно использовать инструмент [Azure Resource Explorer](https://resources.azure.com) . Перейдите к нужному ресурсу и просмотрите отображенный идентификатор, как показано на следующем снимке экрана.

![Azure Resource Explorer](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a>Портал Azure
Идентификатор ресурса можно также получить на портале Azure. Для этого перейдите к нужному ресурсу и выберите "Свойства". Идентификатор ресурса отображается в разделе "Свойства", как показано на следующем снимке экрана:

![Идентификатор ресурса в колонке "Свойства" на портале Azure](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a>Azure PowerShell
Идентификатор ресурса можно получить и с помощью командлетов Azure PowerShell. Например, чтобы получить идентификатор ресурса для приложения логики Azure, выполните командлет Get-AzureLogicApp, как показано в следующем примере.

```PowerShell
Get-AzureRmLogicApp -ResourceGroupName azmon-rest-api-walkthrough -Name contosotweets
```

Результаты должны иметь следующий вид:
```
Id             : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets
Name           : ContosoTweets
Type           : Microsoft.Logic/workflows
Location       : centralus
ChangedTime    : 8/21/2017 6:58:57 PM
CreatedTime    : 8/18/2017 7:54:21 PM
AccessEndpoint : https://prod-08.centralus.logic.azure.com:443/workflows/f3a91b352fcc47e6bff989b85446c5db
State          : Enabled
Definition     : {$schema, contentVersion, parameters, triggers...}
Parameters     : {[$connections, Microsoft.Azure.Management.Logic.Models.WorkflowParameter]}
SkuName        :
AppServicePlan :
PlanType       :
PlanId         :
Version        : 08586982649483762729
```


### <a name="azure-cli"></a>Инфраструктура CLI Azure
Чтобы получить идентификатор ресурса для учетной записи хранения Azure с помощью Azure CLI, выполните команду az storage account show, как показано в следующем примере:

```
az storage account show -g azmon-rest-api-walkthrough -n contosotweets2017
```

Результаты должны иметь следующий вид:
```JSON
{
  "accessTier": null,
  "creationTime": "2017-08-18T19:58:41.840552+00:00",
  "customDomain": null,
  "enableHttpsTrafficOnly": false,
  "encryption": null,
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Storage/storageAccounts/contosotweets2017",
  "identity": null,
  "kind": "Storage",
  "lastGeoFailoverTime": null,
  "location": "centralus",
  "name": "contosotweets2017",
  "networkAcls": null,
  "primaryEndpoints": {
    "blob": "https://contosotweets2017.blob.core.windows.net/",
    "file": "https://contosotweets2017.file.core.windows.net/",
    "queue": "https://contosotweets2017.queue.core.windows.net/",
    "table": "https://contosotweets2017.table.core.windows.net/"
  },
  "primaryLocation": "centralus",
  "provisioningState": "Succeeded",
  "resourceGroup": "azmon-rest-api-walkthrough",
  "secondaryEndpoints": null,
  "secondaryLocation": "eastus2",
  "sku": {
    "name": "Standard_GRS",
    "tier": "Standard"
  },
  "statusOfPrimary": "available",
  "statusOfSecondary": "available",
  "tags": {},
  "type": "Microsoft.Storage/storageAccounts"
}
```

> [!NOTE]
> Приложения логики Azure еще недоступны в Azure CLI, поэтому в предыдущем примере использовалась учетная запись хранения Azure.
>
>

## <a name="retrieve-activity-log-data"></a>Получение данных журнала действий
Помимо определений метрик и связанных значений можно также использовать REST API Azure Monitor, чтобы получить дополнительные интересные сведения, связанные с ресурсами Azure. Например, можно запросить данные [журнала действий](https://msdn.microsoft.com/library/azure/dn931934.aspx) . В приведенном ниже примере показано использование REST API Azure Monitor для запроса данных журнала действий для подписки Azure в определенном диапазоне дат.

```PowerShell
$apiVersion = "2015-04-01"
$filter = "eventTimestamp ge '2017-08-18' and eventTimestamp le '2017-08-19'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&$filter=${filter}"
Invoke-RestMethod -Uri $request `
    -Headers $authHeader `
    -Method Get `
    -Verbose
```

## <a name="next-steps"></a>Дальнейшие действия
* Прочитайте [общие сведения о мониторинге](monitoring-overview.md).
* Ознакомьтесь с разделом [Метрики, поддерживаемые Azure Monitor](monitoring-supported-metrics.md).
* Ознакомьтесь со [справочником по REST API Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).
* Ознакомьтесь с [библиотекой управления Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).
