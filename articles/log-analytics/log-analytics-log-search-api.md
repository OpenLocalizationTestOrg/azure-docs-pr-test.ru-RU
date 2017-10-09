---
title: "REST API поиска журналов аналитики aaaLog | Документы Microsoft"
description: "Данное руководство содержит базовые знания о об использовании hello анализа журналов поиска REST API в hello Operations Management Suite (OMS) и содержит примеры, показывающие, как команды toouse hello."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: b4e9ebe8-80f0-418e-a855-de7954668df7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: dafe5eeb8cc11a339f2cbf78cec657e344d87cac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-log-search-rest-api"></a><span data-ttu-id="8fdad-103">API REST поиска по журналам Log Analytics</span><span class="sxs-lookup"><span data-stu-id="8fdad-103">Log Analytics log search REST API</span></span>
<span data-ttu-id="8fdad-104">Это руководство дает базовые знания, включая примеры того, как можно использовать REST API поиска аналитики журналов hello.</span><span class="sxs-lookup"><span data-stu-id="8fdad-104">This guide provides a basic tutorial, including examples, of how you can use hello Log Analytics Search REST API.</span></span> <span data-ttu-id="8fdad-105">Служба аналитики журналов является частью hello Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="8fdad-105">Log Analytics is part of hello Operations Management Suite (OMS).</span></span>

> [!NOTE]
> <span data-ttu-id="8fdad-106">Если обновленный toohello рабочей области [языка запросов новый журнал аналитики](log-analytics-log-search-upgrade.md), то toouse hello устаревших запросов языка с API поиска журналов hello продолжать, как описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="8fdad-106">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should continue toouse hello legacy query language with hello log search API as described in this article.</span></span>  <span data-ttu-id="8fdad-107">Новый API будет выпущена для обновленных рабочих областей и hello документация будет обновляться в это время.</span><span class="sxs-lookup"><span data-stu-id="8fdad-107">A new API will be released for upgraded workspaces, and hello documentation will be updated at that time.</span></span> 

> [!NOTE]
> <span data-ttu-id="8fdad-108">Служба аналитики журналов был вызван ранее оперативной аналитики, поэтому это hello имя, используемое в поставщике ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="8fdad-108">Log Analytics was previously called Operational Insights, which is why it is hello name used in hello resource provider.</span></span>
>
>

## <a name="overview-of-hello-log-search-rest-api"></a><span data-ttu-id="8fdad-109">Общие сведения о REST API поиска журналов hello</span><span class="sxs-lookup"><span data-stu-id="8fdad-109">Overview of hello Log Search REST API</span></span>
<span data-ttu-id="8fdad-110">Hello REST API поиска аналитики журналов относится к категории RESTful и может запускаться через API диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8fdad-110">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager API.</span></span> <span data-ttu-id="8fdad-111">В этой статье приведены примеры доступа к API hello через [ARMClient](https://github.com/projectkudu/ARMClient), Здравствуйте, средство командной строки открытым исходным кодом, который упрощает вызов API диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="8fdad-111">This article provides examples of accessing hello API through [ARMClient](https://github.com/projectkudu/ARMClient), an open source command-line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="8fdad-112">Использование ARMClient Hello является одним из многих параметров tooaccess hello API поиска аналитики журналов.</span><span class="sxs-lookup"><span data-stu-id="8fdad-112">hello use of ARMClient is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="8fdad-113">Другой вариант — модуля Azure PowerShell hello toouse для OperationalInsights, в который входят командлеты для доступа к поиска.</span><span class="sxs-lookup"><span data-stu-id="8fdad-113">Another option is toouse hello Azure PowerShell module for OperationalInsights, which includes cmdlets for accessing search.</span></span> <span data-ttu-id="8fdad-114">С помощью этих средств можно использовать рабочие области tooOMS вызовы toomake API диспетчера ресурсов Azure hello и выполнения команд поиска в них.</span><span class="sxs-lookup"><span data-stu-id="8fdad-114">With these tools, you can utilize hello Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="8fdad-115">Hello API выводит результаты поиска в формате JSON, позволяя результаты поиска hello toouse различными способами программными средствами.</span><span class="sxs-lookup"><span data-stu-id="8fdad-115">hello API outputs search results in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

<span data-ttu-id="8fdad-116">Hello диспетчера ресурсов Azure можно использовать через [библиотека для .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) и hello [API-интерфейса REST](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span><span class="sxs-lookup"><span data-stu-id="8fdad-116">hello Azure Resource Manager can be used via a [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) and hello [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span></span> <span data-ttu-id="8fdad-117">toolearn более, просмотрите hello связаны веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="8fdad-117">toolearn more, review hello linked web pages.</span></span>

> [!NOTE]
> <span data-ttu-id="8fdad-118">При использовании статистической обработки команды `|measure count()` или `distinct`, каждый вызов toosearch может возвращать не более 500 000 записей.</span><span class="sxs-lookup"><span data-stu-id="8fdad-118">If you use an aggregation command such as `|measure count()` or `distinct`, each call toosearch can return upto 500,000 records.</span></span> <span data-ttu-id="8fdad-119">Операции поиска, в которых не используется команда агрегирования, возвращают не более 5000 записей.</span><span class="sxs-lookup"><span data-stu-id="8fdad-119">Searches that do not include an aggregation command return upto 5,000 records.</span></span>
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a><span data-ttu-id="8fdad-120">Учебник по основам API REST поиска по службе Log Analytics</span><span class="sxs-lookup"><span data-stu-id="8fdad-120">Basic Log Analytics Search REST API tutorial</span></span>
### <a name="toouse-armclient"></a><span data-ttu-id="8fdad-121">toouse ARMClient</span><span class="sxs-lookup"><span data-stu-id="8fdad-121">toouse ARMClient</span></span>
1. <span data-ttu-id="8fdad-122">Установите [Chocolatey](https://chocolatey.org/), который является диспетчером пакетов с открытым исходным кодом для Windows.</span><span class="sxs-lookup"><span data-stu-id="8fdad-122">Install [Chocolatey](https://chocolatey.org/), which is an Open Source Package Manager for Windows.</span></span> <span data-ttu-id="8fdad-123">Откройте окно командной строки от имени администратора и выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="8fdad-123">Open a command prompt window as administrator and then run hello following command:</span></span>

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. <span data-ttu-id="8fdad-124">Установите ARMClient, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="8fdad-124">Install ARMClient by running hello following command:</span></span>

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a><span data-ttu-id="8fdad-125">tooperform поиска с помощью ARMClient</span><span class="sxs-lookup"><span data-stu-id="8fdad-125">tooperform a search using ARMClient</span></span>
1. <span data-ttu-id="8fdad-126">Войдите в учетную запись Майкрософт или в рабочую или учебную учетную запись:</span><span class="sxs-lookup"><span data-stu-id="8fdad-126">Log in using your Microsoft account or your work or school account:</span></span>

    ```
    armclient login
    ```

    <span data-ttu-id="8fdad-127">Успешного входа появится список всех подписок, привязанных toohello, учитывая учетной записи:</span><span class="sxs-lookup"><span data-stu-id="8fdad-127">A successful login lists all subscriptions tied toohello given account:</span></span>

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. <span data-ttu-id="8fdad-128">Получение рабочих областей Operations Management Suite hello:</span><span class="sxs-lookup"><span data-stu-id="8fdad-128">Get hello Operations Management Suite workspaces:</span></span>

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    <span data-ttu-id="8fdad-129">При успешном вызове Get отобразятся, все рабочие области привязан toohello подписки:</span><span class="sxs-lookup"><span data-stu-id="8fdad-129">A successful Get call would output all workspaces tied toohello subscription:</span></span>

    ```
    {
    "value": [
    {
      "properties": {
    "source": "External",
    "customerId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "portalUrl": "https://eus.login.mms.microsoft.com/SignIn.aspx?returnUrl=https%3a%2f%2feus.mms.microsoft.com%2fMain.aspx%3fcid%xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
      },
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/{WORKSPACE NAME}",
      "name": "{WORKSPACE NAME}",
      "type": "Microsoft.OperationalInsights/workspaces",
      "location": "East US"
       ]
    }
    ```
3. <span data-ttu-id="8fdad-130">Создание своей переменной поиска:</span><span class="sxs-lookup"><span data-stu-id="8fdad-130">Create your search variable:</span></span>

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. <span data-ttu-id="8fdad-131">Поиск с помощью новой переменной поиска:</span><span class="sxs-lookup"><span data-stu-id="8fdad-131">Search using your new search variable:</span></span>

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a><span data-ttu-id="8fdad-132">Примеры API REST поиска по службе Log Analytics</span><span class="sxs-lookup"><span data-stu-id="8fdad-132">Log Analytics Search REST API reference examples</span></span>
<span data-ttu-id="8fdad-133">Hello в следующих примерах показано, как можно использовать API поиска hello.</span><span class="sxs-lookup"><span data-stu-id="8fdad-133">hello following examples show you how you can use hello Search API.</span></span>

### <a name="search---actionread"></a><span data-ttu-id="8fdad-134">Поиск — Действие/Чтение</span><span class="sxs-lookup"><span data-stu-id="8fdad-134">Search - Action/Read</span></span>
<span data-ttu-id="8fdad-135">**Пример URL:**</span><span class="sxs-lookup"><span data-stu-id="8fdad-135">**Sample Url:**</span></span>

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

<span data-ttu-id="8fdad-136">**Запрос:**</span><span class="sxs-lookup"><span data-stu-id="8fdad-136">**Request:**</span></span>

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```
<span data-ttu-id="8fdad-137">Hello в следующей таблице описаны доступные свойства hello.</span><span class="sxs-lookup"><span data-stu-id="8fdad-137">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="8fdad-138">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="8fdad-138">**Property**</span></span> | <span data-ttu-id="8fdad-139">**Описание**</span><span class="sxs-lookup"><span data-stu-id="8fdad-139">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="8fdad-140">top</span><span class="sxs-lookup"><span data-stu-id="8fdad-140">top</span></span> |<span data-ttu-id="8fdad-141">Максимальное количество результатов tooreturn Hello.</span><span class="sxs-lookup"><span data-stu-id="8fdad-141">hello maximum number of results tooreturn.</span></span> |
| <span data-ttu-id="8fdad-142">highlight</span><span class="sxs-lookup"><span data-stu-id="8fdad-142">highlight</span></span> |<span data-ttu-id="8fdad-143">Содержит параметры pre и post, которые обычно используются для выделения соответствующих запросу полей</span><span class="sxs-lookup"><span data-stu-id="8fdad-143">Contains pre and post parameters, used usually for highlighting matching fields</span></span> |
| <span data-ttu-id="8fdad-144">pre</span><span class="sxs-lookup"><span data-stu-id="8fdad-144">pre</span></span> |<span data-ttu-id="8fdad-145">Префиксы hello в строковые поля tooyour соответствует заданному.</span><span class="sxs-lookup"><span data-stu-id="8fdad-145">Prefixes hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="8fdad-146">post</span><span class="sxs-lookup"><span data-stu-id="8fdad-146">post</span></span> |<span data-ttu-id="8fdad-147">Добавляет заданного поля соответствует tooyour строку hello.</span><span class="sxs-lookup"><span data-stu-id="8fdad-147">Appends hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="8fdad-148">query</span><span class="sxs-lookup"><span data-stu-id="8fdad-148">query</span></span> |<span data-ttu-id="8fdad-149">запрос поиска Hello используется toocollect и возвращать результаты.</span><span class="sxs-lookup"><span data-stu-id="8fdad-149">hello search query used toocollect and return results.</span></span> |
| <span data-ttu-id="8fdad-150">start</span><span class="sxs-lookup"><span data-stu-id="8fdad-150">start</span></span> |<span data-ttu-id="8fdad-151">Начало Hello hello временное окно, необходимо найти toobe результаты.</span><span class="sxs-lookup"><span data-stu-id="8fdad-151">hello beginning of hello time window you want results toobe found from.</span></span> |
| <span data-ttu-id="8fdad-152">end</span><span class="sxs-lookup"><span data-stu-id="8fdad-152">end</span></span> |<span data-ttu-id="8fdad-153">конец Hello hello временное окно, необходимо найти toobe результаты.</span><span class="sxs-lookup"><span data-stu-id="8fdad-153">hello end of hello time window you want results toobe found from.</span></span> |

<span data-ttu-id="8fdad-154">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="8fdad-154">**Response:**</span></span>

```
    {
      "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "__metadata" : {
        "resultType" : "raw",
        "total" : 1455,
        "top" : 150,
        "StartTime" : "2015-02-11T21:09:07.0345815Z",
        "Status" : "Successful",
        "LastUpdated" : "2015-02-11T21:09:07.331463Z",
        "CoreResponses" : [],
        "sort" : [{
          "name" : "TimeGenerated",
          "order" : "desc"
        }],
        "requestTime" : 450
      },
      "value": [{
        "SourceSystem" : "OpsManager",
        "TimeGenerated" : "2015-02-07T14:07:33Z",
        "Source" : "SideBySide",
        "EventLog" : "Application",
        "Computer" : "BAMBAM",
        "EventCategory" : 0,
        "EventLevel" : 1,
        "EventLevelName" : "Error",
        "UserName" : "N/A",
        "EventID" : 78,
        "MG" : "00000000-0000-0000-0000-000000000001",
        "TimeCollected" : "2015-02-07T14:10:04.69Z",
        "ManagementGroupName" : "AOI-5bf9a37f-e841-462b-80d2-1d19cd97dc40",
        "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "Type" : "Event",
        "__metadata" : {
          "Type" : "Event",
          "TimeGenerated" : "2015-02-07T14:07:33Z",
          "highlighting" : {
          "EventLevelName" : ["{[hl]}Error{[/hl]}"]
        }
      }]
    ],
            "start" : "2015-02-04T21:03:29.231Z",
            "end" : "2015-02-11T21:03:29.231Z"
          }
        }
      }]
    }
```

### <a name="searchid---actionread"></a><span data-ttu-id="8fdad-155">Поиск/{ID} - Действие/Чтение</span><span class="sxs-lookup"><span data-stu-id="8fdad-155">Search/{ID} - Action/Read</span></span>
<span data-ttu-id="8fdad-156">**Запрос содержимого сохраненных результатов поиска hello:**</span><span class="sxs-lookup"><span data-stu-id="8fdad-156">**Request hello contents of a Saved Search:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> <span data-ttu-id="8fdad-157">Если hello поиска возвращает со статусом «Ожидание», hello обновить результаты опроса можно сделать с помощью этого API.</span><span class="sxs-lookup"><span data-stu-id="8fdad-157">If hello search returns with a ‘Pending’ status, then polling hello updated results can be done through this API.</span></span> <span data-ttu-id="8fdad-158">Через 6 минут результат поиска hello hello, будут удалены из кэша hello и HTTP больше не будут возвращены.</span><span class="sxs-lookup"><span data-stu-id="8fdad-158">After 6 min, hello result of hello search will be dropped from hello cache and HTTP Gone will be returned.</span></span> <span data-ttu-id="8fdad-159">Если hello первоначального поискового запроса немедленно возвращает состояние «Успешно», результаты hello не добавляются toohello кэша, причиной этого tooreturn API HTTP Gone при запросе.</span><span class="sxs-lookup"><span data-stu-id="8fdad-159">If hello initial search request returns a ‘Successful’ status immediately, hello results are not added toohello cache causing this API tooreturn HTTP Gone if queried.</span></span> <span data-ttu-id="8fdad-160">содержимое результатов HTTP 200 Hello находятся в том же формате, что hello первоначального поискового запроса, но с обновленными значениями hello.</span><span class="sxs-lookup"><span data-stu-id="8fdad-160">hello contents of an HTTP 200 result are in hello same format as hello initial search request just with updated values.</span></span>
>
>

### <a name="saved-searches"></a><span data-ttu-id="8fdad-161">Сохраненные поисковые запросы</span><span class="sxs-lookup"><span data-stu-id="8fdad-161">Saved searches</span></span>
<span data-ttu-id="8fdad-162">**Запрос списка сохраненных поисковых запросов:**</span><span class="sxs-lookup"><span data-stu-id="8fdad-162">**Request List of Saved Searches:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

<span data-ttu-id="8fdad-163">Поддерживаемые методы: GET, PUT и DELETE.</span><span class="sxs-lookup"><span data-stu-id="8fdad-163">Supported methods: GET PUT DELETE</span></span>

<span data-ttu-id="8fdad-164">Поддерживаемые методы сбора данных: GET</span><span class="sxs-lookup"><span data-stu-id="8fdad-164">Supported collection methods: GET</span></span>

<span data-ttu-id="8fdad-165">Hello в следующей таблице описаны доступные свойства hello.</span><span class="sxs-lookup"><span data-stu-id="8fdad-165">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="8fdad-166">Свойство</span><span class="sxs-lookup"><span data-stu-id="8fdad-166">Property</span></span> | <span data-ttu-id="8fdad-167">Описание</span><span class="sxs-lookup"><span data-stu-id="8fdad-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8fdad-168">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="8fdad-168">Id</span></span> |<span data-ttu-id="8fdad-169">Уникальный идентификатор Hello.</span><span class="sxs-lookup"><span data-stu-id="8fdad-169">hello unique identifier.</span></span> |
| <span data-ttu-id="8fdad-170">Etag</span><span class="sxs-lookup"><span data-stu-id="8fdad-170">Etag</span></span> |<span data-ttu-id="8fdad-171">**Необходимо для обновления**.</span><span class="sxs-lookup"><span data-stu-id="8fdad-171">**Required for Patch**.</span></span> <span data-ttu-id="8fdad-172">Обновляется сервером при каждой операции записи.</span><span class="sxs-lookup"><span data-stu-id="8fdad-172">Updated by server on each write.</span></span> <span data-ttu-id="8fdad-173">Значение должно быть равно toohello текущее сохраненное значение или "*" tooupdate.</span><span class="sxs-lookup"><span data-stu-id="8fdad-173">Value must be equal toohello current stored value or ‘*’ tooupdate.</span></span> <span data-ttu-id="8fdad-174">Для старых или недопустимых значений возвращается 409.</span><span class="sxs-lookup"><span data-stu-id="8fdad-174">409 returned for old/invalid values.</span></span> |
| <span data-ttu-id="8fdad-175">properties.query</span><span class="sxs-lookup"><span data-stu-id="8fdad-175">properties.query</span></span> |<span data-ttu-id="8fdad-176">**Обязательный**.</span><span class="sxs-lookup"><span data-stu-id="8fdad-176">**Required**.</span></span> <span data-ttu-id="8fdad-177">Hello поисковый запрос.</span><span class="sxs-lookup"><span data-stu-id="8fdad-177">hello search query.</span></span> |
| <span data-ttu-id="8fdad-178">properties.displayName</span><span class="sxs-lookup"><span data-stu-id="8fdad-178">properties.displayName</span></span> |<span data-ttu-id="8fdad-179">**Обязательный**.</span><span class="sxs-lookup"><span data-stu-id="8fdad-179">**Required**.</span></span> <span data-ttu-id="8fdad-180">Hello определяемых пользователем отображаемое имя запроса hello.</span><span class="sxs-lookup"><span data-stu-id="8fdad-180">hello user-defined display name of hello query.</span></span> |
| <span data-ttu-id="8fdad-181">properties.category</span><span class="sxs-lookup"><span data-stu-id="8fdad-181">properties.category</span></span> |<span data-ttu-id="8fdad-182">**Обязательный**.</span><span class="sxs-lookup"><span data-stu-id="8fdad-182">**Required**.</span></span> <span data-ttu-id="8fdad-183">Hello определяемая пользователем Категория запроса hello.</span><span class="sxs-lookup"><span data-stu-id="8fdad-183">hello user-defined category of hello query.</span></span> |

> [!NOTE]
> <span data-ttu-id="8fdad-184">Hello API поиска аналитики журналов в настоящее время возвращает созданные пользователем сохраненные поисковые запросы, когда запрашиваются сохраненные поисковые запросы в рабочей области.</span><span class="sxs-lookup"><span data-stu-id="8fdad-184">hello Log Analytics search API currently returns user-created saved searches when polled for saved searches in a workspace.</span></span> <span data-ttu-id="8fdad-185">Hello API не возвращает сохраненные поисковые запросы, предоставляемых решениями.</span><span class="sxs-lookup"><span data-stu-id="8fdad-185">hello API does not return saved searches provided by solutions.</span></span>
>
>

### <a name="create-saved-searches"></a><span data-ttu-id="8fdad-186">Создание сохраненных поисковых запросов</span><span class="sxs-lookup"><span data-stu-id="8fdad-186">Create saved searches</span></span>
<span data-ttu-id="8fdad-187">**Запрос:**</span><span class="sxs-lookup"><span data-stu-id="8fdad-187">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> <span data-ttu-id="8fdad-188">Имя Hello все сохраненные поисковые запросы, отчеты и действия, созданные с помощью hello API аналитики журналов должно быть в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="8fdad-188">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

### <a name="delete-saved-searches"></a><span data-ttu-id="8fdad-189">Удаление сохраненных поисковых запросов</span><span class="sxs-lookup"><span data-stu-id="8fdad-189">Delete saved searches</span></span>
<span data-ttu-id="8fdad-190">**Запрос:**</span><span class="sxs-lookup"><span data-stu-id="8fdad-190">**Request:**</span></span>

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a><span data-ttu-id="8fdad-191">Изменение сохраненных поисковых запросов</span><span class="sxs-lookup"><span data-stu-id="8fdad-191">Update saved searches</span></span>
 <span data-ttu-id="8fdad-192">**Запрос:**</span><span class="sxs-lookup"><span data-stu-id="8fdad-192">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a><span data-ttu-id="8fdad-193">Метаданные (только JSON)</span><span class="sxs-lookup"><span data-stu-id="8fdad-193">Metadata - JSON only</span></span>
<span data-ttu-id="8fdad-194">Вот способ toosee hello полей для всех типов журналов hello данных, собранных в рабочей области.</span><span class="sxs-lookup"><span data-stu-id="8fdad-194">Here’s a way toosee hello fields for all log types for hello data collected in your workspace.</span></span> <span data-ttu-id="8fdad-195">Например если вы хотите узнать, если hello тип события содержит поле с именем компьютера, этот запрос является одним из способов toocheck.</span><span class="sxs-lookup"><span data-stu-id="8fdad-195">For example, if you want you know if hello Event type has a field named Computer, then this query is one way toocheck.</span></span>

<span data-ttu-id="8fdad-196">**Запрос полей**</span><span class="sxs-lookup"><span data-stu-id="8fdad-196">**Request for Fields:**</span></span>

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

<span data-ttu-id="8fdad-197">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="8fdad-197">**Response:**</span></span>

```
    {
      "__metadata" : {
        "schema" : {
          "name" : "Example Name",
          "version" : 2
        },
        "resultType" : "schema",
        "requestTime" : 35
      },
      "value" : [{
          "name" : "MG",
          "displayName" : "MG",
          "type" : "Guid",
          "facetable" : true,
          "display" : false,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Capacity_SMBUtilizationByHost", "Capacity_ArrayUtilization", "Capacity_SMBShareUtilization", "SQLAssessmentRecommendation", "Event", "ConfigurationChange", "ConfigurationAlert", "ADAssessmentRecommendation", "ConfigurationObject", "ConfigurationObjectProperty"]
        }, {
          "name" : "ManagementGroupName",
          "displayName" : "ManagementGroupName",
          "type" : "String",
          "facetable" : true,
          "display" : true,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Event", "ConfigurationChange", "ConfigurationAlert", "W3CIISLog", "AlertHistory", "Recommendation", "Alert", "SecurityEvent", "UpdateAgent", "RequiredUpdate", "ConfigurationObject", "ConfigurationObjectProperty"]
        }
      ]
    }
```

<span data-ttu-id="8fdad-198">Hello в следующей таблице описаны доступные свойства hello.</span><span class="sxs-lookup"><span data-stu-id="8fdad-198">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="8fdad-199">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="8fdad-199">**Property**</span></span> | <span data-ttu-id="8fdad-200">**Описание**</span><span class="sxs-lookup"><span data-stu-id="8fdad-200">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="8fdad-201">name</span><span class="sxs-lookup"><span data-stu-id="8fdad-201">name</span></span> |<span data-ttu-id="8fdad-202">Имя поля.</span><span class="sxs-lookup"><span data-stu-id="8fdad-202">Field name.</span></span> |
| <span data-ttu-id="8fdad-203">displayName</span><span class="sxs-lookup"><span data-stu-id="8fdad-203">displayName</span></span> |<span data-ttu-id="8fdad-204">Hello отображаемое имя поля hello.</span><span class="sxs-lookup"><span data-stu-id="8fdad-204">hello display name of hello field.</span></span> |
| <span data-ttu-id="8fdad-205">type</span><span class="sxs-lookup"><span data-stu-id="8fdad-205">type</span></span> |<span data-ttu-id="8fdad-206">Здравствуйте, тип значения поля hello.</span><span class="sxs-lookup"><span data-stu-id="8fdad-206">hello Type of hello field value.</span></span> |
| <span data-ttu-id="8fdad-207">facetable</span><span class="sxs-lookup"><span data-stu-id="8fdad-207">facetable</span></span> |<span data-ttu-id="8fdad-208">Сочетание текущих свойств indexed, stored и facet.</span><span class="sxs-lookup"><span data-stu-id="8fdad-208">Combination of current ‘indexed’, ‘stored ‘and ‘facet’ properties.</span></span> |
| <span data-ttu-id="8fdad-209">display</span><span class="sxs-lookup"><span data-stu-id="8fdad-209">display</span></span> |<span data-ttu-id="8fdad-210">Текущее свойство display.</span><span class="sxs-lookup"><span data-stu-id="8fdad-210">Current ‘display’ property.</span></span> <span data-ttu-id="8fdad-211">Если поле отображается при поиске, используется значение true.</span><span class="sxs-lookup"><span data-stu-id="8fdad-211">True if field is visible in search.</span></span> |
| <span data-ttu-id="8fdad-212">ownerType</span><span class="sxs-lookup"><span data-stu-id="8fdad-212">ownerType</span></span> |<span data-ttu-id="8fdad-213">Снижение tooonly типы, принадлежащие tooonboarded IP.</span><span class="sxs-lookup"><span data-stu-id="8fdad-213">Reduced tooonly Types belonging tooonboarded IP’s.</span></span> |

## <a name="optional-parameters"></a><span data-ttu-id="8fdad-214">Необязательные параметры</span><span class="sxs-lookup"><span data-stu-id="8fdad-214">Optional parameters</span></span>
<span data-ttu-id="8fdad-215">Hello следующую информацию описывает доступные необязательные параметры.</span><span class="sxs-lookup"><span data-stu-id="8fdad-215">hello following information describes optional parameters available.</span></span>

### <a name="highlighting"></a><span data-ttu-id="8fdad-216">Выделение</span><span class="sxs-lookup"><span data-stu-id="8fdad-216">Highlighting</span></span>
<span data-ttu-id="8fdad-217">параметр «Highlight» Hello является необязательным параметром можно использовать подсистемы поиска toorequest hello в ответ, добавить набор маркеров.</span><span class="sxs-lookup"><span data-stu-id="8fdad-217">hello “Highlight” parameter is an optional parameter you may use toorequest hello search subsystem include a set of markers in its response.</span></span>

<span data-ttu-id="8fdad-218">Эти маркеры указывают hello начало и окончание выделяемого текста, который сопоставляет термины hello, указанный в запросе поиска.</span><span class="sxs-lookup"><span data-stu-id="8fdad-218">These markers indicate hello start and end highlighted text that matches hello terms provided in your search query.</span></span>
<span data-ttu-id="8fdad-219">Можно указать начало hello и конечный маркеры, используемые выделенной hello toowrap поисковому запросу.</span><span class="sxs-lookup"><span data-stu-id="8fdad-219">You may specify hello start and end markers that are used by search toowrap hello highlighted term.</span></span>

<span data-ttu-id="8fdad-220">**Пример поискового запроса**</span><span class="sxs-lookup"><span data-stu-id="8fdad-220">**Example search query**</span></span>

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```

<span data-ttu-id="8fdad-221">**Пример результата:**</span><span class="sxs-lookup"><span data-stu-id="8fdad-221">**Sample result:**</span></span>

```
    {
        "TimeGenerated":
        "2015-05-18T23:55:59Z", "Source":
        "EventLog": "Application",
        "Computer": "smokedturkey.net",
        "EventCategory": 0,
        "EventLevel":1,
        "EventLevelName":
        "Error"
        "Manager ", "__metadata":
        {
            "Type": "Event",
            "TimeGenerated": "2015-05-18T23:55:59Z",
            "highlighting": {
                "EventLevelName":
                ["{[hl]}Error{[/hl]}"]
            }
        }
    }
```

<span data-ttu-id="8fdad-222">Обратите внимание, что hello предыдущий результат содержит сообщение об ошибке, префиксом и постфиксом.</span><span class="sxs-lookup"><span data-stu-id="8fdad-222">Notice that hello preceding result contains an error message that has been prefixed and appended.</span></span>

## <a name="computer-groups"></a><span data-ttu-id="8fdad-223">Группы компьютеров</span><span class="sxs-lookup"><span data-stu-id="8fdad-223">Computer groups</span></span>
<span data-ttu-id="8fdad-224">Группы компьютеров — специальные сохраненные поисковые запросы, возвращающие набор компьютеров.</span><span class="sxs-lookup"><span data-stu-id="8fdad-224">Computer groups are special saved searches that return a set of computers.</span></span>  <span data-ttu-id="8fdad-225">Группы компьютеров можно использовать на других компьютерах запросы toolimit hello результаты toohello в группе hello.</span><span class="sxs-lookup"><span data-stu-id="8fdad-225">You can use a computer group in other queries toolimit hello results toohello computers in hello group.</span></span>  <span data-ttu-id="8fdad-226">Группа компьютеров реализуется как сохраненный поисковый запрос с тегом Group (Группа) и значением Computer (Компьютер).</span><span class="sxs-lookup"><span data-stu-id="8fdad-226">A computer group is implemented as a saved search with a Group tag with a value of Computer.</span></span>

<span data-ttu-id="8fdad-227">Ниже представлен пример ответа для группы компьютеров.</span><span class="sxs-lookup"><span data-stu-id="8fdad-227">Following is a sample response for a computer group.</span></span>

```
    "etag": "W/\"datetime'2016-04-01T13%3A38%3A04.7763203Z'\"",
    "properties": {
        "Category": "My Computer Groups",
        "DisplayName": "My Computer Group",
        "Query": "srv* | Distinct Computer",
        "Tags": [{
            "Name": "Group",
            "Value": "Computer"
          }],
    "Version": 1
    }
```

### <a name="retrieving-computer-groups"></a><span data-ttu-id="8fdad-228">Извлечение группы компьютеров</span><span class="sxs-lookup"><span data-stu-id="8fdad-228">Retrieving computer groups</span></span>
<span data-ttu-id="8fdad-229">группы компьютеров, используйте hello метод Get с группой hello tooretrieve по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="8fdad-229">tooretrieve a computer group, use hello Get method with hello group ID.</span></span>

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a><span data-ttu-id="8fdad-230">Создание или обновление группы компьютеров</span><span class="sxs-lookup"><span data-stu-id="8fdad-230">Creating or updating a computer group</span></span>
<span data-ttu-id="8fdad-231">toocreate группы компьютеров, используйте hello метода Put с идентификатором уникальный сохраненные условия поиска.</span><span class="sxs-lookup"><span data-stu-id="8fdad-231">toocreate a computer group, use hello Put method with a unique saved search ID.</span></span> <span data-ttu-id="8fdad-232">Если используется существующий идентификатор группы компьютеров, он будет изменен.</span><span class="sxs-lookup"><span data-stu-id="8fdad-232">If you use an existing computer group ID, then that one is modified.</span></span> <span data-ttu-id="8fdad-233">При создании группы компьютеров на портале службы анализа журналов hello идентификатор hello создается из группы hello и имени.</span><span class="sxs-lookup"><span data-stu-id="8fdad-233">When you create a computer group in hello Log Analytics portal, then hello ID is created from hello group and name.</span></span>

<span data-ttu-id="8fdad-234">Hello запрос, используемый для определения группы hello должен возвращать набор компьютеров для группы toofunction hello должным образом.</span><span class="sxs-lookup"><span data-stu-id="8fdad-234">hello query used for hello group definition must return a set of computers for hello group toofunction properly.</span></span>  <span data-ttu-id="8fdad-235">Рекомендуется завершении запроса с `| Distinct Computer` tooensure hello правильные данные возвращаются.</span><span class="sxs-lookup"><span data-stu-id="8fdad-235">It's recommended that you end your query with `| Distinct Computer` tooensure hello correct data is returned.</span></span>

<span data-ttu-id="8fdad-236">Определение Hello hello сохраненного поиска необходимо включить тег с именем группы со значением компьютера для поиска toobe hello, классифицируются как группы компьютеров.</span><span class="sxs-lookup"><span data-stu-id="8fdad-236">hello definition of hello saved search must include a tag named Group with a value of Computer for hello search toobe classified as a computer group.</span></span>

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a><span data-ttu-id="8fdad-237">Удаление группы компьютеров</span><span class="sxs-lookup"><span data-stu-id="8fdad-237">Deleting computer groups</span></span>
<span data-ttu-id="8fdad-238">группы компьютеров, используйте hello метода Delete с группой hello toodelete по идентификатору.</span><span class="sxs-lookup"><span data-stu-id="8fdad-238">toodelete a computer group, use hello Delete method with hello group ID.</span></span>

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a><span data-ttu-id="8fdad-239">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8fdad-239">Next steps</span></span>
* <span data-ttu-id="8fdad-240">Дополнительные сведения о [входа выполняет](log-analytics-log-searches.md) toobuild запросы, использующие настраиваемые поля для критериев.</span><span class="sxs-lookup"><span data-stu-id="8fdad-240">Learn about [log searches](log-analytics-log-searches.md) toobuild queries using custom fields for criteria.</span></span>
