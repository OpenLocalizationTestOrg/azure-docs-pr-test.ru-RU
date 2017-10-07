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
# <a name="azure-monitoring-rest-api-walkthrough"></a><span data-ttu-id="14791-103">Пошаговое руководство по REST API Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="14791-103">Azure Monitoring REST API Walkthrough</span></span>
<span data-ttu-id="14791-104">В этой статье показано, как tooperform проверки подлинности, чтобы код можно было использовать hello [Справочник по API REST монитор Microsoft Azure](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="14791-104">This article shows you how tooperform authentication so your code can use hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>         

<span data-ttu-id="14791-105">Hello API монитор Azure упрощает tooprogrammatically возможно получение hello доступен по умолчанию определения показателей (hello тип показателя, например время ЦП, запросы, т. д.), гранулярности и значения метрики.</span><span class="sxs-lookup"><span data-stu-id="14791-105">hello Azure Monitor API makes it possible tooprogrammatically retrieve hello available default metric definitions (hello type of metric such as CPU Time, Requests, etc.), granularity, and metric values.</span></span> <span data-ttu-id="14791-106">После получения данных hello могут сохраняться в отдельное хранилище данных как базы данных SQL Azure, Azure Cosmos DB или Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="14791-106">Once retrieved, hello data can be saved in a separate data store such as Azure SQL Database, Azure Cosmos DB, or Azure Data Lake.</span></span> <span data-ttu-id="14791-107">Там при необходимости можно выполнить дополнительный анализ.</span><span class="sxs-lookup"><span data-stu-id="14791-107">From there additional analysis can be performed as needed.</span></span>

<span data-ttu-id="14791-108">Помимо работы с различных точек данных метрик, как в этой статье показано, hello монитор API позволяет возможных toolist правила оповещений, Просмотр журналов действий и многое другое.</span><span class="sxs-lookup"><span data-stu-id="14791-108">Besides working with various metric data points, as this article demonstrates, hello Monitor API makes it possible toolist alert rules, view activity logs, and much more.</span></span> <span data-ttu-id="14791-109">Полный список доступных операций см. в разделе hello [Справочник по API REST монитор Microsoft Azure](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="14791-109">For a full list of available operations, see hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

## <a name="authenticating-azure-monitor-requests"></a><span data-ttu-id="14791-110">Аутентификация запросов Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="14791-110">Authenticating Azure Monitor Requests</span></span>
<span data-ttu-id="14791-111">Первым шагом Hello — tooauthenticate hello запрос.</span><span class="sxs-lookup"><span data-stu-id="14791-111">hello first step is tooauthenticate hello request.</span></span>

<span data-ttu-id="14791-112">Все задачи hello, исполняемые для модели проверки подлинности для использования hello hello Azure монитор API диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="14791-112">All hello tasks executed against hello Azure Monitor API use hello Azure Resource Manager authentication model.</span></span> <span data-ttu-id="14791-113">Поэтому все запросы должны быть аутентифицированы в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="14791-113">Therefore, all requests must be authenticated with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="14791-114">Один подход tooauthenticate hello клиента приложение toocreate участника-службы Azure AD и получить маркер проверки подлинности (JWT) hello.</span><span class="sxs-lookup"><span data-stu-id="14791-114">One approach tooauthenticate hello client application is toocreate an Azure AD service principal and retrieve hello authentication (JWT) token.</span></span> <span data-ttu-id="14791-115">Hello следующий образец скрипта показывает создание участника службы с помощью PowerShell Azure AD.</span><span class="sxs-lookup"><span data-stu-id="14791-115">hello following sample script demonstrates creating an Azure AD service principal via PowerShell.</span></span> <span data-ttu-id="14791-116">Более подробное Пошаговое руководство см. документацию toohello на [ресурсов tooaccess участника службы с помощью Azure PowerShell toocreate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span><span class="sxs-lookup"><span data-stu-id="14791-116">For a more detailed walk-through, refer toohello documentation on [using Azure PowerShell toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password).</span></span> <span data-ttu-id="14791-117">Можно также слишком[Создание субъекта-службы через портал Azure hello](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="14791-117">It is also possible too[create a service principal via hello Azure portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

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

<span data-ttu-id="14791-118">hello tooquery монитор API Azure, клиентское приложение hello следует использовать hello ранее созданные tooauthenticate участника службы.</span><span class="sxs-lookup"><span data-stu-id="14791-118">tooquery hello Azure Monitor API, hello client application should use hello previously created service principal tooauthenticate.</span></span> <span data-ttu-id="14791-119">Следующий пример скрипта PowerShell Hello показан один из способов, с помощью hello [библиотеку аутентификации Active Directory](../active-directory/active-directory-authentication-libraries.md) toohelp (ADAL) получение маркера проверки подлинности JWT hello.</span><span class="sxs-lookup"><span data-stu-id="14791-119">hello following example PowerShell script shows one approach, using hello [Active Directory Authentication Library](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp get hello JWT authentication token.</span></span> <span data-ttu-id="14791-120">токен JWT Hello передается как часть параметра авторизации HTTP в toohello запросов API REST Azure монитора.</span><span class="sxs-lookup"><span data-stu-id="14791-120">hello JWT token is passed as part of an HTTP Authorization parameter in requests toohello Azure Monitor REST API.</span></span>

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

<span data-ttu-id="14791-121">После завершения hello шаг настройки проверки подлинности запросов можно затем выполняется для hello API REST Azure монитора.</span><span class="sxs-lookup"><span data-stu-id="14791-121">Once hello authentication setup step is complete, queries can then be executed against hello Azure Monitor REST API.</span></span> <span data-ttu-id="14791-122">Можно использовать два полезных запроса:</span><span class="sxs-lookup"><span data-stu-id="14791-122">There are two helpful queries:</span></span>

1. <span data-ttu-id="14791-123">Список определений метрик hello для ресурса</span><span class="sxs-lookup"><span data-stu-id="14791-123">List hello metric definitions for a resource</span></span>
2. <span data-ttu-id="14791-124">Получение значения метрики hello</span><span class="sxs-lookup"><span data-stu-id="14791-124">Retrieve hello metric values</span></span>

## <a name="retrieve-metric-definitions"></a><span data-ttu-id="14791-125">Получение определений метрик</span><span class="sxs-lookup"><span data-stu-id="14791-125">Retrieve Metric Definitions</span></span>
> [!NOTE]
> <span data-ttu-id="14791-126">tooretrieve определения метрик с помощью hello Azure REST API-Интерфейс монитора, используйте «2016-03-01» как hello версия API.</span><span class="sxs-lookup"><span data-stu-id="14791-126">tooretrieve metric definitions using hello Azure Monitor REST API, use "2016-03-01" as hello API version.</span></span>
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
<span data-ttu-id="14791-127">Для приложения логики Azure определения показателей hello должно выглядеть примерно toohello следующий снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="14791-127">For an Azure Logic App, hello metric definitions would appear similar toohello following screenshot:</span></span>

![Представление ответа JSON для определения метрики](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

<span data-ttu-id="14791-129">Дополнительные сведения см. в разделе hello [список определений метрик hello для ресурса в API REST Azure монитор](https://msdn.microsoft.com/library/azure/mt743621.aspx) документации.</span><span class="sxs-lookup"><span data-stu-id="14791-129">For more information, see hello [List hello metric definitions for a resource in Azure Monitor REST API](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentation.</span></span>

## <a name="retrieve-metric-values"></a><span data-ttu-id="14791-130">Получение значений метрик</span><span class="sxs-lookup"><span data-stu-id="14791-130">Retrieve Metric Values</span></span>
<span data-ttu-id="14791-131">После определения доступных показателей hello известны, это то возможные tooretrieve hello связанные значения метрики.</span><span class="sxs-lookup"><span data-stu-id="14791-131">Once hello available metric definitions are known, it is then possible tooretrieve hello related metric values.</span></span> <span data-ttu-id="14791-132">Имя метрики hello «значение» (не hello «localizedValue») используйте для фильтрации запросов (например, получение hello «Запросы» и «Время ЦП» метрики точек данных).</span><span class="sxs-lookup"><span data-stu-id="14791-132">Use hello metric’s name ‘value’ (not hello ‘localizedValue’) for any filtering requests (for example, retrieve hello ‘CpuTime’ and ‘Requests’ metric data points).</span></span> <span data-ttu-id="14791-133">Если не указано ни одного фильтра, возвращается метрики по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="14791-133">If no filters are specified, hello default metric is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="14791-134">значения метрики tooretrieve с помощью hello Azure REST API-Интерфейс монитора, используйте «2016-06-01» как hello версия API.</span><span class="sxs-lookup"><span data-stu-id="14791-134">tooretrieve metric values using hello Azure Monitor REST API, use "2016-06-01" as hello API version.</span></span>
>
>

<span data-ttu-id="14791-135">**Метод**: GET</span><span class="sxs-lookup"><span data-stu-id="14791-135">**Method**: GET</span></span>

<span data-ttu-id="14791-136">**URI запроса**: https://management.azure.com/subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/*{пространство_имен_поставщиков_ресурсов}*/*{тип_ресурса}*/*{имя_ресурса*/providers/microsoft.insights/metrics?$filter=*{фильтр}*&api-version=*{версия_API}*</span><span class="sxs-lookup"><span data-stu-id="14791-136">**Request URI**: https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?$filter=*{filter}*&api-version=*{apiVersion}*</span></span>

<span data-ttu-id="14791-137">Например данные метрик tooretrieve hello RunsSucceeded точек для заданного интервала времени hello и гран времени 1 час, hello запрос будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="14791-137">For example, tooretrieve hello RunsSucceeded metric data points for hello given time range and for a time grain of 1 hour, hello request would be as follows:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

<span data-ttu-id="14791-138">Hello результат будет выглядеть аналогичный пример toohello следующий снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="14791-138">hello result would appear similar toohello example following screenshot:</span></span>

![Ответ JSON, отображающий значение метрики "Среднее время ответа"](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

<span data-ttu-id="14791-140">tooretrieve указывает несколько данных или статистической обработки, добавьте имен определений метрик hello и фильтр toohello типов статистической обработки, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="14791-140">tooretrieve multiple data or aggregation points, add hello metric definition names and aggregation types toohello filter, as seen in hello following example:</span></span>

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a><span data-ttu-id="14791-141">Использование ARMClient</span><span class="sxs-lookup"><span data-stu-id="14791-141">Use ARMClient</span></span>
<span data-ttu-id="14791-142">Альтернативные toousing PowerShell (как показано выше), является toouse [ARMClient](https://github.com/projectkudu/ARMClient) на компьютере Windows.</span><span class="sxs-lookup"><span data-stu-id="14791-142">An alternative toousing PowerShell (as shown above), is toouse [ARMClient](https://github.com/projectkudu/ARMClient) on your Windows machine.</span></span> <span data-ttu-id="14791-143">ARMClient автоматически выполняет проверку подлинности hello Azure AD (и полученный маркер JWT).</span><span class="sxs-lookup"><span data-stu-id="14791-143">ARMClient handles hello Azure AD authentication (and resulting JWT token) automatically.</span></span> <span data-ttu-id="14791-144">Hello ниже описывается использование ARMClient для получения данных метрик:</span><span class="sxs-lookup"><span data-stu-id="14791-144">hello following steps outline use of ARMClient for retrieving metric data:</span></span>

1. <span data-ttu-id="14791-145">Установите [Chocolatey](https://chocolatey.org/) и [ARMClient](https://github.com/projectkudu/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="14791-145">Install [Chocolatey](https://chocolatey.org/) and [ARMClient](https://github.com/projectkudu/ARMClient).</span></span>
2. <span data-ttu-id="14791-146">В окне терминала введите *armclient.exe login*.</span><span class="sxs-lookup"><span data-stu-id="14791-146">In a terminal window, type *armclient.exe login*.</span></span> <span data-ttu-id="14791-147">Это приглашение toolog в tooAzure.</span><span class="sxs-lookup"><span data-stu-id="14791-147">This prompts you toolog in tooAzure.</span></span>
3. <span data-ttu-id="14791-148">Введите *armclient GET [ИД_ресурса]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*.</span><span class="sxs-lookup"><span data-stu-id="14791-148">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*</span></span>
4. <span data-ttu-id="14791-149">Введите *armclient GET [ИД_ресурса]/providers/microsoft.insights/metrics?api-version=2016-06-01*.</span><span class="sxs-lookup"><span data-stu-id="14791-149">Type *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-06-01*</span></span>

![ALT «С помощью ARMClient toowork с API REST Azure мониторинг hello»](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-hello-resource-id"></a><span data-ttu-id="14791-151">Получить идентификатор ресурса hello</span><span class="sxs-lookup"><span data-stu-id="14791-151">Retrieve hello Resource ID</span></span>
<span data-ttu-id="14791-152">С помощью API-интерфейса REST hello поможет toounderstand hello доступные метрики определения гранулярности и связанных значений.</span><span class="sxs-lookup"><span data-stu-id="14791-152">Using hello REST API can really help toounderstand hello available metric definitions, granularity, and related values.</span></span> <span data-ttu-id="14791-153">Эти сведения будут полезны при использовании hello [Библиотека управления Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="14791-153">That information is helpful when using hello [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>

<span data-ttu-id="14791-154">Для hello предшествующий код toouse идентификатор ресурса hello является полный путь toohello hello требуемого ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="14791-154">For hello preceding code, hello resource ID toouse is hello full path toohello desired Azure resource.</span></span> <span data-ttu-id="14791-155">Например tooquery от веб-приложение Azure, идентификатор ресурса hello будет следующим:</span><span class="sxs-lookup"><span data-stu-id="14791-155">For example, tooquery against an Azure Web App, hello resource ID would be:</span></span>

<span data-ttu-id="14791-156">*/subscriptions/{ИД_подписки}/resourceGroups/{имя_группы_ресурсов}/providers/Microsoft.Web/sites/{имя_сайта}/*</span><span class="sxs-lookup"><span data-stu-id="14791-156">*/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{site-name}/*</span></span>

<span data-ttu-id="14791-157">Hello ниже приведено несколько примеров форматы идентификатор ресурса для различных ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="14791-157">hello following list contains a few examples of resource ID formats for various Azure resources:</span></span>

* <span data-ttu-id="14791-158">**Центр Интернета вещей**: /subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/Microsoft.Devices/IotHubs/*{имя_центра}*.</span><span class="sxs-lookup"><span data-stu-id="14791-158">**IoT Hub** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Devices/IotHubs/*{iot-hub-name}*</span></span>
* <span data-ttu-id="14791-159">**Пул эластичных баз данных SQL**: /subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/Microsoft.Sql/servers/*{база_данных_в_пуле}*/elasticpools/*{имя_пула_SQL}*.</span><span class="sxs-lookup"><span data-stu-id="14791-159">**Elastic SQL Pool** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{pool-db}*/elasticpools/*{sql-pool-name}*</span></span>
* <span data-ttu-id="14791-160">**База данных SQL (версии 12)**: /subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/Microsoft.Sql/servers/*{имя_сервера}*/databases/*{имя_базы_данных}*.</span><span class="sxs-lookup"><span data-stu-id="14791-160">**SQL Database (v12)** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Sql/servers/*{server-name}*/databases/*{database-name}*</span></span>
* <span data-ttu-id="14791-161">**Служебная шина**: /subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/Microsoft.ServiceBus/*{пространство_имен}*/*{имя_служебной_шины}*.</span><span class="sxs-lookup"><span data-stu-id="14791-161">**Service Bus** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.ServiceBus/*{namespace}*/*{servicebus-name}*</span></span>
* <span data-ttu-id="14791-162">**Наборы масштабирования ВМ**: /subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{имя_ВМ}*.</span><span class="sxs-lookup"><span data-stu-id="14791-162">**VM Scale Sets** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*</span></span>
* <span data-ttu-id="14791-163">**Виртуальные машины**: /subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/Microsoft.Compute/virtualMachines/*{имя_ВМ}*.</span><span class="sxs-lookup"><span data-stu-id="14791-163">**VMs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachines/*{vm-name}*</span></span>
* <span data-ttu-id="14791-164">**Концентраторы событий**: /subscriptions/*{ИД_подписки}*/resourceGroups/*{имя_группы_ресурсов}*/providers/Microsoft.EventHub/namespaces/*{пространство_имен_концентраторов_событий}*.</span><span class="sxs-lookup"><span data-stu-id="14791-164">**Event Hubs** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.EventHub/namespaces/*{eventhub-namespace}*</span></span>

<span data-ttu-id="14791-165">Существуют альтернативные подходы tooretrieving hello идентификатор ресурса, включая использование обозревателя ресурсов Azure, просмотр hello требуемого ресурса в hello портал Azure и с помощью PowerShell или Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="14791-165">There are alternative approaches tooretrieving hello resource ID, including using Azure Resource Explorer, viewing hello desired resource in hello Azure portal, and via PowerShell or hello Azure CLI.</span></span>

### <a name="azure-resource-explorer"></a><span data-ttu-id="14791-166">Обозреватель ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="14791-166">Azure Resource Explorer</span></span>
<span data-ttu-id="14791-167">Идентификатор ресурса hello toofind для нужного ресурса, одним из подходов полезные — toouse hello [обозревателя ресурсов Azure](https://resources.azure.com) средства.</span><span class="sxs-lookup"><span data-stu-id="14791-167">toofind hello resource ID for a desired resource, one helpful approach is toouse hello [Azure Resource Explorer](https://resources.azure.com) tool.</span></span> <span data-ttu-id="14791-168">Перейдите toohello требуемого ресурса и посмотрите на код hello, показано, как следующий снимок экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="14791-168">Navigate toohello desired resource and then look at hello ID shown, as in hello following screenshot:</span></span>

![Azure Resource Explorer](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a><span data-ttu-id="14791-170">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="14791-170">Azure portal</span></span>
<span data-ttu-id="14791-171">Идентификатор ресурса Hello можно также получить из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="14791-171">hello resource ID can also be obtained from hello Azure portal.</span></span> <span data-ttu-id="14791-172">Таким образом, toodo перейдите toohello требуемого ресурса и выберите пункт Свойства.</span><span class="sxs-lookup"><span data-stu-id="14791-172">toodo so, navigate toohello desired resource and then select Properties.</span></span> <span data-ttu-id="14791-173">Hello идентификатор ресурса отображаются в колонке свойства hello, как показано на следующий снимок экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="14791-173">hello Resource ID is displayed in hello Properties blade, as seen in hello following screenshot:</span></span>

![ALT «идентификатор ресурса отображаемых в колонке свойства hello в hello портал Azure»](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a><span data-ttu-id="14791-175">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="14791-175">Azure PowerShell</span></span>
<span data-ttu-id="14791-176">с помощью командлетов Azure PowerShell также можно получить идентификатор ресурса Hello.</span><span class="sxs-lookup"><span data-stu-id="14791-176">hello resource ID can be retrieved using Azure PowerShell cmdlets as well.</span></span> <span data-ttu-id="14791-177">Например идентификатор ресурса hello tooobtain для веб-приложение Azure выполните командлет Get-AzureRmWebApp hello, как следующий снимок экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="14791-177">For example, tooobtain hello resource ID for an Azure Web App, execute hello Get-AzureRmWebApp cmdlet, as in hello following screenshot:</span></span>

![Идентификатор ресурса, полученный с помощью PowerShell](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a><span data-ttu-id="14791-179">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="14791-179">Azure CLI</span></span>
<span data-ttu-id="14791-180">tooretrieve hello идентификатор ресурса, с помощью hello Azure CLI, выполните команду «Показать azure веб-приложение» hello, указав hello "--json" параметра, как показано на следующий снимок экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="14791-180">tooretrieve hello resource ID using hello Azure CLI, execute hello 'azure webapp show' command, specifying hello '--json' option, as shown in hello following screenshot:</span></span>

![Идентификатор ресурса, полученный с помощью PowerShell](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a><span data-ttu-id="14791-182">Получение данных журнала действий</span><span class="sxs-lookup"><span data-stu-id="14791-182">Retrieve Activity Log Data</span></span>
<span data-ttu-id="14791-183">В tooworking сложения с определения показателей и связанные значения это также возможных tooretrieve дополнительные интересные аналитики tooAzure связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="14791-183">In addition tooworking with metric definitions and related values, it is also possible tooretrieve additional interesting insights related tooAzure resources.</span></span> <span data-ttu-id="14791-184">Например, это возможно tooquery [журнал действий](https://msdn.microsoft.com/library/azure/dn931934.aspx) данных.</span><span class="sxs-lookup"><span data-stu-id="14791-184">As an example, it is possible tooquery [activity log](https://msdn.microsoft.com/library/azure/dn931934.aspx) data.</span></span> <span data-ttu-id="14791-185">Hello следующем образце показано использование данные журнала действий tooquery API REST Azure монитор hello в определенном диапазоне дат для подписки Azure:</span><span class="sxs-lookup"><span data-stu-id="14791-185">hello following sample demonstrates using hello Azure Monitor REST API tooquery activity log data within a specific date range for an Azure subscription:</span></span>

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a><span data-ttu-id="14791-186">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="14791-186">Next steps</span></span>
* <span data-ttu-id="14791-187">Просмотрите hello [Обзор мониторинга](monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="14791-187">Review hello [Overview of Monitoring](monitoring-overview.md).</span></span>
* <span data-ttu-id="14791-188">Представление hello [поддерживаемых метрик с помощью монитора Azure](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="14791-188">View hello [Supported metrics with Azure Monitor](monitoring-supported-metrics.md).</span></span>
* <span data-ttu-id="14791-189">Просмотрите hello [Справочник по API REST монитор Microsoft Azure](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="14791-189">Review hello [Microsoft Azure Monitor REST API Reference](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>
* <span data-ttu-id="14791-190">Просмотрите hello [Библиотека управления Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span><span class="sxs-lookup"><span data-stu-id="14791-190">Review hello [Azure Management Library](https://msdn.microsoft.com/library/azure/mt417623.aspx).</span></span>
