---
title: "Пошаговое руководство мониторинг API-интерфейса REST aaaAzure | Документы Microsoft"
description: "Как tooauthenticate запрашивает hello tooand использования API REST мониторинга Azure."
author: mcollier
manager: 
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 565e6a88-3131-4a48-8b82-3effc9a3d5c6
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: mcollier
ms.openlocfilehash: b8ae3a03fd21af872f1dc5fed40a101a24ca1652
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitoring-rest-api-walkthrough"></a>Пошаговое руководство по REST API Azure Monitor
В этой статье показано, как tooperform проверки подлинности, чтобы код можно было использовать hello [Справочник по API REST монитор Microsoft Azure](https://msdn.microsoft.com/library/azure/dn931943.aspx).         

Hello API монитор Azure упрощает tooprogrammatically возможно получение hello доступен по умолчанию определения показателей (hello тип показателя, например время ЦП, запросы, т. д.), гранулярности и значения метрики. После получения данных hello могут сохраняться в отдельное хранилище данных как базы данных SQL Azure, Azure Cosmos DB или Озера данных Azure. Там при необходимости можно выполнить дополнительный анализ.

Помимо работы с различных точек данных метрик, как в этой статье показано, hello монитор API позволяет возможных toolist правила оповещений, Просмотр журналов действий и многое другое. Полный список доступных операций см. в разделе hello [Справочник по API REST монитор Microsoft Azure](https://msdn.microsoft.com/library/azure/dn931943.aspx).

## <a name="authenticating-azure-monitor-requests"></a>Аутентификация запросов Azure Monitor
Первым шагом Hello — tooauthenticate hello запрос.

Все задачи hello, исполняемые для модели проверки подлинности для использования hello hello Azure монитор API диспетчера ресурсов Azure. Поэтому все запросы должны быть аутентифицированы в Azure Active Directory (Azure AD). Один подход tooauthenticate hello клиента приложение toocreate участника-службы Azure AD и получить маркер проверки подлинности (JWT) hello. Hello следующий образец скрипта показывает создание участника службы с помощью PowerShell Azure AD. Более подробное Пошаговое руководство см. документацию toohello на [ресурсов tooaccess участника службы с помощью Azure PowerShell toocreate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password). Можно также слишком[Создание субъекта-службы через портал Azure hello](../azure-resource-manager/resource-group-create-service-principal-portal.md).

```PowerShell
$subscriptionId = "{azure-subscription-id}"
$resourceGroupName = "{resource-group-name}"
$location = "centralus"

# Authenticate tooa specific Azure subscription.
Login-AzureRmAccount -SubscriptionId $subscriptionId

# Password for hello service principal
$pwd = "{service-principal-password}"

# Create a new Azure AD application
$azureAdApplication = New-AzureRmADApplication `
                        -DisplayName "My Azure Monitor" `
                        -HomePage "https://localhost/azure-monitor" `
                        -IdentifierUris "https://localhost/azure-monitor" `
                        -Password $pwd

# Create a new service principal associated with hello designated application
New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

# Assign Reader role toohello newly created service principal
New-AzureRmRoleAssignment -RoleDefinitionName Reader `
                          -ServicePrincipalName $azureAdApplication.ApplicationId.Guid

```

hello tooquery монитор API Azure, клиентское приложение hello следует использовать hello ранее созданные tooauthenticate участника службы. Следующий пример скрипта PowerShell Hello показан один из способов, с помощью hello [библиотеку аутентификации Active Directory](../active-directory/active-directory-authentication-libraries.md) toohelp (ADAL) получение маркера проверки подлинности JWT hello. токен JWT Hello передается как часть параметра авторизации HTTP в toohello запросов API REST Azure монитора.

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

После завершения hello шаг настройки проверки подлинности запросов можно затем выполняется для hello API REST Azure монитора. Можно использовать два полезных запроса:

1. Список определений метрик hello для ресурса
2. Получение значения метрики hello

## <a name="retrieve-metric-definitions"></a>Получение определений метрик
> [!NOTE]
> tooretrieve определения метрик с помощью hello Azure REST API-Интерфейс монитора, используйте «2016-03-01» как hello версия API.
>
>

```PowerShell
$apiVersion = "2016-03-01"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metricDefinitions?api-version=${apiVersion}"

Invoke-RestMethod -Uri $request `
                  -Headers $authHeader `
                  -Method Get `
                  -Verbose
```
Для приложения логики Azure определения показателей hello должно выглядеть примерно toohello следующий снимок экрана:

![Представление ответа JSON для определения метрики](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

Дополнительные сведения см. в разделе hello [список определений метрик hello для ресурса в API REST Azure монитор](https://msdn.microsoft.com/library/azure/mt743621.aspx) документации.

## <a name="retrieve-metric-values"></a>Получение значений метрик
После определения доступных показателей hello известны, это то возможные tooretrieve hello связанные значения метрики. Имя метрики hello «значение» (не hello «localizedValue») используйте для фильтрации запросов (например, получение hello «Запросы» и «Время ЦП» метрики точек данных). Если не указано ни одного фильтра, возвращается метрики по умолчанию hello.

> [!NOTE]
> значения метрики tooretrieve с помощью hello Azure REST API-Интерфейс монитора, используйте «2016-06-01» как hello версия API.
>
>

**Метод**: GET

**URI запроса**: https://management.azure.com/subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/*{пространство_имен_поставщиков_ресурсов}*/*{тип_ресурса}*/*{имя_ресурса*/providers/microsoft.insights/metrics?$filter=*{фильтр}*&api-version=*{версия_API}*

Например данные метрик tooretrieve hello RunsSucceeded точек для заданного интервала времени hello и гран времени 1 час, hello запрос будет выглядеть следующим образом:

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

Hello результат будет выглядеть аналогичный пример toohello следующий снимок экрана:

![Ответ JSON, отображающий значение метрики "Среднее время ответа"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

tooretrieve указывает несколько данных или статистической обработки, добавьте имен определений метрик hello и фильтр toohello типов статистической обработки, как показано в следующий пример hello:

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a>Использование ARMClient
Альтернативные toousing PowerShell (как показано выше), является toouse [ARMClient](https://github.com/projectkudu/ARMClient) на компьютере Windows. ARMClient автоматически выполняет проверку подлинности hello Azure AD (и полученный маркер JWT). Hello ниже описывается использование ARMClient для получения данных метрик:

1. Установите [Chocolatey](https://chocolatey.org/) и [ARMClient](https://github.com/projectkudu/ARMClient).
2. В окне терминала введите *armclient.exe login*. Это приглашение toolog в tooAzure.
3. Введите *armclient GET [ИД_ресурса]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*.
4. Введите *armclient GET [ИД_ресурса]/providers/microsoft.insights/metrics?api-version=2016-06-01*.

![ALT «С помощью ARMClient toowork с API REST Azure мониторинг hello»](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-hello-resource-id"></a>Получить идентификатор ресурса hello
С помощью API-интерфейса REST hello поможет toounderstand hello доступные метрики определения гранулярности и связанных значений. Эти сведения будут полезны при использовании hello [Библиотека управления Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).

Для hello предшествующий код toouse идентификатор ресурса hello является полный путь toohello hello требуемого ресурсов Azure. Например tooquery от веб-приложение Azure, идентификатор ресурса hello будет следующим:

*/subscriptions/{ИД_подписки}/resourceGroups/{имя_группы_ресурсов}/providers/Microsoft.Web/sites/{имя_сайта}/*

Hello ниже приведено несколько примеров форматы идентификатор ресурса для различных ресурсов Azure.

* **Центр Интернета вещей**: /subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/Microsoft.Devices/IotHubs/*{имя_центра}*.
* **Пул эластичных баз данных SQL**: /subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/Microsoft.Sql/servers/*{база_данных_в_пуле}*/elasticpools/*{имя_пула_SQL}*.
* **База данных SQL (версии 12)**: /subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/Microsoft.Sql/servers/*{имя_сервера}*/databases/*{имя_базы_данных}*.
* **Служебная шина**: /subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/Microsoft.ServiceBus/*{пространство_имен}*/*{имя_служебной_шины}*.
* **Наборы масштабирования ВМ**: /subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{имя_ВМ}*.
* **Виртуальные машины**: /subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/Microsoft.Compute/virtualMachines/*{имя_ВМ}*.
* **Концентраторы событий**: /subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/Microsoft.EventHub/namespaces/*{пространство_имен_концентраторов_событий}*.

Существуют альтернативные подходы tooretrieving hello идентификатор ресурса, включая использование обозревателя ресурсов Azure, просмотр hello требуемого ресурса в hello портал Azure и с помощью PowerShell или Azure CLI hello.

### <a name="azure-resource-explorer"></a>Обозреватель ресурсов Azure
Идентификатор ресурса hello toofind для нужного ресурса, одним из подходов полезные — toouse hello [обозревателя ресурсов Azure](https://resources.azure.com) средства. Перейдите toohello требуемого ресурса и посмотрите на код hello, показано, как следующий снимок экрана приветствия:

![Azure Resource Explorer](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a>Портал Azure
Идентификатор ресурса Hello можно также получить из hello портал Azure. Таким образом, toodo перейдите toohello требуемого ресурса и выберите пункт Свойства. Hello идентификатор ресурса отображаются в колонке свойства hello, как показано на следующий снимок экрана приветствия:

![ALT «идентификатор ресурса отображаемых в колонке свойства hello в hello портал Azure»](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a>Azure PowerShell
с помощью командлетов Azure PowerShell также можно получить идентификатор ресурса Hello. Например идентификатор ресурса hello tooobtain для веб-приложение Azure выполните командлет Get-AzureRmWebApp hello, как следующий снимок экрана приветствия:

![Идентификатор ресурса, полученный с помощью PowerShell](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a>Инфраструктура CLI Azure
tooretrieve hello идентификатор ресурса, с помощью hello Azure CLI, выполните команду «Показать azure веб-приложение» hello, указав hello "--json" параметра, как показано на следующий снимок экрана приветствия:

![Идентификатор ресурса, полученный с помощью PowerShell](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a>Получение данных журнала действий
В tooworking сложения с определения показателей и связанные значения это также возможных tooretrieve дополнительные интересные аналитики tooAzure связанные ресурсы. Например, это возможно tooquery [журнал действий](https://msdn.microsoft.com/library/azure/dn931934.aspx) данных. Hello следующем образце показано использование данные журнала действий tooquery API REST Azure монитор hello в определенном диапазоне дат для подписки Azure:

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a>Дальнейшие действия
* Просмотрите hello [Обзор мониторинга](monitoring-overview.md).
* Представление hello [поддерживаемых метрик с помощью монитора Azure](monitoring-supported-metrics.md).
* Просмотрите hello [Справочник по API REST монитор Microsoft Azure](https://msdn.microsoft.com/library/azure/dn931943.aspx).
* Просмотрите hello [Библиотека управления Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).
