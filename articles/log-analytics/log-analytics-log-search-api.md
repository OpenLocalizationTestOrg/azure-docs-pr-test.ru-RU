---
title: "REST API поиска по журналам в Log Analytics | Документация Майкрософт"
description: "Данное руководство дает базовые знания о том, как использовать API REST поиска по службе Log Analytics в Operational Insights Suite (OMS), и содержит примеры использования команд."
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
ms.openlocfilehash: 78afb2f065dde4a3e7a3ab787c939b3c52b72cc6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="log-analytics-log-search-rest-api"></a><span data-ttu-id="c5696-103">API REST поиска по журналам Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c5696-103">Log Analytics log search REST API</span></span>
<span data-ttu-id="c5696-104">В этом базовом руководстве представлены примеры использования API REST поиска по службе Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c5696-104">This guide provides a basic tutorial, including examples, of how you can use the Log Analytics Search REST API.</span></span> <span data-ttu-id="c5696-105">Log Analytics входит в пакет Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="c5696-105">Log Analytics is part of the Operations Management Suite (OMS).</span></span>

> [!NOTE]
> <span data-ttu-id="c5696-106">Если рабочая область использует [новый язык запросов Log Analytics](log-analytics-log-search-upgrade.md), с API поиска по журналам по-прежнему используйте прежний язык запросов, как описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="c5696-106">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should continue to use the legacy query language with the log search API as described in this article.</span></span>  <span data-ttu-id="c5696-107">Мы планируем выпустить новый API для обновленных рабочих областей и после этого изменить соответствующим образом эту статью.</span><span class="sxs-lookup"><span data-stu-id="c5696-107">A new API will be released for upgraded workspaces, and the documentation will be updated at that time.</span></span> 

> [!NOTE]
> <span data-ttu-id="c5696-108">Компонент Log Analytics раньше назывался Operational Insights, поэтому именно такое имя используется в поставщиках ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c5696-108">Log Analytics was previously called Operational Insights, which is why it is the name used in the resource provider.</span></span>
>
>

## <a name="overview-of-the-log-search-rest-api"></a><span data-ttu-id="c5696-109">Обзор API REST поиска по журналу</span><span class="sxs-lookup"><span data-stu-id="c5696-109">Overview of the Log Search REST API</span></span>
<span data-ttu-id="c5696-110">Для поиска по службе Log Analytics используется API REST категории RESTful — к нему можно получить доступ с помощью API Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c5696-110">The Log Analytics Search REST API is RESTful and can be accessed via the Azure Resource Manager API.</span></span> <span data-ttu-id="c5696-111">В этой статье вы найдете примеры, когда доступ к API осуществляется через [ARMClient](https://github.com/projectkudu/ARMClient) — инструмент командной строки с открытым кодом, который упрощает вызов API Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c5696-111">This article provides examples of accessing the API through [ARMClient](https://github.com/projectkudu/ARMClient), an open source command-line tool that simplifies invoking the Azure Resource Manager API.</span></span> <span data-ttu-id="c5696-112">Использование ARMClient — это один из множества вариантов получения доступа к API поиска по службе Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c5696-112">The use of ARMClient is one of many options to access the Log Analytics Search API.</span></span> <span data-ttu-id="c5696-113">Другой вариант — использовать модуль Azure PowerShell для Operational Insights, включающий командлеты для доступа к службе поиска.</span><span class="sxs-lookup"><span data-stu-id="c5696-113">Another option is to use the Azure PowerShell module for OperationalInsights, which includes cmdlets for accessing search.</span></span> <span data-ttu-id="c5696-114">С помощью этих инструментов можно использовать API Azure Resource Manager для осуществления вызовов рабочих областей OMS и выполнения команд поиска в них.</span><span class="sxs-lookup"><span data-stu-id="c5696-114">With these tools, you can utilize the Azure Resource Manager API to make calls to OMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="c5696-115">API выдает результаты поиска в формате JSON, позволяя программно использовать результаты поиска различными способами.</span><span class="sxs-lookup"><span data-stu-id="c5696-115">The API outputs search results in JSON format, allowing you to use the search results in many different ways programmatically.</span></span>

<span data-ttu-id="c5696-116">Azure Resource Manager можно использовать через [библиотеку для .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx), а также через [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span><span class="sxs-lookup"><span data-stu-id="c5696-116">The Azure Resource Manager can be used via a [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) and the [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span></span> <span data-ttu-id="c5696-117">Дополнительные сведения см. на связанных веб-страницах.</span><span class="sxs-lookup"><span data-stu-id="c5696-117">To learn more, review the linked web pages.</span></span>

> [!NOTE]
> <span data-ttu-id="c5696-118">При использовании команды агрегирования, например `|measure count()` или `distinct`, каждый вызов службы поиска может возвращать не более 500 000 записей.</span><span class="sxs-lookup"><span data-stu-id="c5696-118">If you use an aggregation command such as `|measure count()` or `distinct`, each call to search can return upto 500,000 records.</span></span> <span data-ttu-id="c5696-119">Операции поиска, в которых не используется команда агрегирования, возвращают не более 5000 записей.</span><span class="sxs-lookup"><span data-stu-id="c5696-119">Searches that do not include an aggregation command return upto 5,000 records.</span></span>
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a><span data-ttu-id="c5696-120">Учебник по основам API REST поиска по службе Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c5696-120">Basic Log Analytics Search REST API tutorial</span></span>
### <a name="to-use-armclient"></a><span data-ttu-id="c5696-121">Использование ARMClient</span><span class="sxs-lookup"><span data-stu-id="c5696-121">To use ARMClient</span></span>
1. <span data-ttu-id="c5696-122">Установите [Chocolatey](https://chocolatey.org/), который является диспетчером пакетов с открытым исходным кодом для Windows.</span><span class="sxs-lookup"><span data-stu-id="c5696-122">Install [Chocolatey](https://chocolatey.org/), which is an Open Source Package Manager for Windows.</span></span> <span data-ttu-id="c5696-123">Откройте окно командной строки от имени администратора, а затем выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c5696-123">Open a command prompt window as administrator and then run the following command:</span></span>

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. <span data-ttu-id="c5696-124">Установите ARMClient, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c5696-124">Install ARMClient by running the following command:</span></span>

    ```
    choco install armclient
    ```

### <a name="to-perform-a-search-using-armclient"></a><span data-ttu-id="c5696-125">Выполнение поиска с помощью ARMClient</span><span class="sxs-lookup"><span data-stu-id="c5696-125">To perform a search using ARMClient</span></span>
1. <span data-ttu-id="c5696-126">Войдите в учетную запись Майкрософт или в рабочую или учебную учетную запись:</span><span class="sxs-lookup"><span data-stu-id="c5696-126">Log in using your Microsoft account or your work or school account:</span></span>

    ```
    armclient login
    ```

    <span data-ttu-id="c5696-127">При успешном выполнении входа появится список всех подписок, привязанных к данной учетной записи:</span><span class="sxs-lookup"><span data-stu-id="c5696-127">A successful login lists all subscriptions tied to the given account:</span></span>

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. <span data-ttu-id="c5696-128">Получение рабочих областей Operations Management Suite Workspaces:</span><span class="sxs-lookup"><span data-stu-id="c5696-128">Get the Operations Management Suite workspaces:</span></span>

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    <span data-ttu-id="c5696-129">При успешном вызове Get отобразятся все рабочие области, привязанные к подписке:</span><span class="sxs-lookup"><span data-stu-id="c5696-129">A successful Get call would output all workspaces tied to the subscription:</span></span>

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
3. <span data-ttu-id="c5696-130">Создание своей переменной поиска:</span><span class="sxs-lookup"><span data-stu-id="c5696-130">Create your search variable:</span></span>

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. <span data-ttu-id="c5696-131">Поиск с помощью новой переменной поиска:</span><span class="sxs-lookup"><span data-stu-id="c5696-131">Search using your new search variable:</span></span>

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a><span data-ttu-id="c5696-132">Примеры API REST поиска по службе Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c5696-132">Log Analytics Search REST API reference examples</span></span>
<span data-ttu-id="c5696-133">На следующих примерах показано, как можно использовать API поиска.</span><span class="sxs-lookup"><span data-stu-id="c5696-133">The following examples show you how you can use the Search API.</span></span>

### <a name="search---actionread"></a><span data-ttu-id="c5696-134">Поиск — Действие/Чтение</span><span class="sxs-lookup"><span data-stu-id="c5696-134">Search - Action/Read</span></span>
<span data-ttu-id="c5696-135">**Пример URL:**</span><span class="sxs-lookup"><span data-stu-id="c5696-135">**Sample Url:**</span></span>

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

<span data-ttu-id="c5696-136">**Запрос:**</span><span class="sxs-lookup"><span data-stu-id="c5696-136">**Request:**</span></span>

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
<span data-ttu-id="c5696-137">В следующей таблице описаны имеющиеся свойства.</span><span class="sxs-lookup"><span data-stu-id="c5696-137">The following table describes the properties that are available.</span></span>

| <span data-ttu-id="c5696-138">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="c5696-138">**Property**</span></span> | <span data-ttu-id="c5696-139">**Описание**</span><span class="sxs-lookup"><span data-stu-id="c5696-139">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="c5696-140">top</span><span class="sxs-lookup"><span data-stu-id="c5696-140">top</span></span> |<span data-ttu-id="c5696-141">Максимальное количество отображаемых результатов.</span><span class="sxs-lookup"><span data-stu-id="c5696-141">The maximum number of results to return.</span></span> |
| <span data-ttu-id="c5696-142">highlight</span><span class="sxs-lookup"><span data-stu-id="c5696-142">highlight</span></span> |<span data-ttu-id="c5696-143">Содержит параметры pre и post, которые обычно используются для выделения соответствующих запросу полей</span><span class="sxs-lookup"><span data-stu-id="c5696-143">Contains pre and post parameters, used usually for highlighting matching fields</span></span> |
| <span data-ttu-id="c5696-144">pre</span><span class="sxs-lookup"><span data-stu-id="c5696-144">pre</span></span> |<span data-ttu-id="c5696-145">Добавляет заданную строку перед соответствующими запросу полями.</span><span class="sxs-lookup"><span data-stu-id="c5696-145">Prefixes the given string to your matched fields.</span></span> |
| <span data-ttu-id="c5696-146">post</span><span class="sxs-lookup"><span data-stu-id="c5696-146">post</span></span> |<span data-ttu-id="c5696-147">Добавляет заданную строку после соответствующих запросу полей.</span><span class="sxs-lookup"><span data-stu-id="c5696-147">Appends the given string to your matched fields.</span></span> |
| <span data-ttu-id="c5696-148">запрос</span><span class="sxs-lookup"><span data-stu-id="c5696-148">query</span></span> |<span data-ttu-id="c5696-149">Поисковый запрос, используемый для сбора и отображения результатов.</span><span class="sxs-lookup"><span data-stu-id="c5696-149">The search query used to collect and return results.</span></span> |
| <span data-ttu-id="c5696-150">start</span><span class="sxs-lookup"><span data-stu-id="c5696-150">start</span></span> |<span data-ttu-id="c5696-151">Начало периода, за который необходимо собрать результаты.</span><span class="sxs-lookup"><span data-stu-id="c5696-151">The beginning of the time window you want results to be found from.</span></span> |
| <span data-ttu-id="c5696-152">end</span><span class="sxs-lookup"><span data-stu-id="c5696-152">end</span></span> |<span data-ttu-id="c5696-153">Окончание периода, за который необходимо собрать результаты.</span><span class="sxs-lookup"><span data-stu-id="c5696-153">The end of the time window you want results to be found from.</span></span> |

<span data-ttu-id="c5696-154">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="c5696-154">**Response:**</span></span>

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

### <a name="searchid---actionread"></a><span data-ttu-id="c5696-155">Поиск/{ID} - Действие/Чтение</span><span class="sxs-lookup"><span data-stu-id="c5696-155">Search/{ID} - Action/Read</span></span>
<span data-ttu-id="c5696-156">**Запрос содержимого сохраненных результатов поиска:**</span><span class="sxs-lookup"><span data-stu-id="c5696-156">**Request the contents of a Saved Search:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> <span data-ttu-id="c5696-157">Если результаты поиска выдаются со статусом "Ожидание", данный API можно использовать для запроса обновленных результатов.</span><span class="sxs-lookup"><span data-stu-id="c5696-157">If the search returns with a ‘Pending’ status, then polling the updated results can be done through this API.</span></span> <span data-ttu-id="c5696-158">Через 6 минут результат поиска удаляется из кэша и выдается статус HTTP Gone.</span><span class="sxs-lookup"><span data-stu-id="c5696-158">After 6 min, the result of the search will be dropped from the cache and HTTP Gone will be returned.</span></span> <span data-ttu-id="c5696-159">Если по первому поисковому запросу сразу выдаются результаты с состоянием "Успешно", они не добавляются в кэш, в результате чего при запросе этот API выдает статус HTTP Gone.</span><span class="sxs-lookup"><span data-stu-id="c5696-159">If the initial search request returns a ‘Successful’ status immediately, the results are not added to the cache causing this API to return HTTP Gone if queried.</span></span> <span data-ttu-id="c5696-160">Содержимое результатов HTTP 200 представляется в том же формате, что и у первоначального поискового запроса, но с обновленными значениями.</span><span class="sxs-lookup"><span data-stu-id="c5696-160">The contents of an HTTP 200 result are in the same format as the initial search request just with updated values.</span></span>
>
>

### <a name="saved-searches"></a><span data-ttu-id="c5696-161">Сохраненные поисковые запросы</span><span class="sxs-lookup"><span data-stu-id="c5696-161">Saved searches</span></span>
<span data-ttu-id="c5696-162">**Запрос списка сохраненных поисковых запросов:**</span><span class="sxs-lookup"><span data-stu-id="c5696-162">**Request List of Saved Searches:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

<span data-ttu-id="c5696-163">Поддерживаемые методы: GET, PUT и DELETE.</span><span class="sxs-lookup"><span data-stu-id="c5696-163">Supported methods: GET PUT DELETE</span></span>

<span data-ttu-id="c5696-164">Поддерживаемые методы сбора данных: GET</span><span class="sxs-lookup"><span data-stu-id="c5696-164">Supported collection methods: GET</span></span>

<span data-ttu-id="c5696-165">В следующей таблице описаны имеющиеся свойства.</span><span class="sxs-lookup"><span data-stu-id="c5696-165">The following table describes the properties that are available.</span></span>

| <span data-ttu-id="c5696-166">Свойство</span><span class="sxs-lookup"><span data-stu-id="c5696-166">Property</span></span> | <span data-ttu-id="c5696-167">Описание</span><span class="sxs-lookup"><span data-stu-id="c5696-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c5696-168">Идентификатор</span><span class="sxs-lookup"><span data-stu-id="c5696-168">Id</span></span> |<span data-ttu-id="c5696-169">Уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="c5696-169">The unique identifier.</span></span> |
| <span data-ttu-id="c5696-170">Etag</span><span class="sxs-lookup"><span data-stu-id="c5696-170">Etag</span></span> |<span data-ttu-id="c5696-171">**Необходимо для обновления**.</span><span class="sxs-lookup"><span data-stu-id="c5696-171">**Required for Patch**.</span></span> <span data-ttu-id="c5696-172">Обновляется сервером при каждой операции записи.</span><span class="sxs-lookup"><span data-stu-id="c5696-172">Updated by server on each write.</span></span> <span data-ttu-id="c5696-173">Для обновления требуется, чтобы в качестве значения использовалось текущее сохраненное значение или символ *.</span><span class="sxs-lookup"><span data-stu-id="c5696-173">Value must be equal to the current stored value or ‘*’ to update.</span></span> <span data-ttu-id="c5696-174">Для старых или недопустимых значений возвращается 409.</span><span class="sxs-lookup"><span data-stu-id="c5696-174">409 returned for old/invalid values.</span></span> |
| <span data-ttu-id="c5696-175">properties.query</span><span class="sxs-lookup"><span data-stu-id="c5696-175">properties.query</span></span> |<span data-ttu-id="c5696-176">**Обязательный**.</span><span class="sxs-lookup"><span data-stu-id="c5696-176">**Required**.</span></span> <span data-ttu-id="c5696-177">Поисковый запрос.</span><span class="sxs-lookup"><span data-stu-id="c5696-177">The search query.</span></span> |
| <span data-ttu-id="c5696-178">properties.displayName</span><span class="sxs-lookup"><span data-stu-id="c5696-178">properties.displayName</span></span> |<span data-ttu-id="c5696-179">**Обязательный**.</span><span class="sxs-lookup"><span data-stu-id="c5696-179">**Required**.</span></span> <span data-ttu-id="c5696-180">Определяемое пользователем отображаемое имя запроса.</span><span class="sxs-lookup"><span data-stu-id="c5696-180">The user-defined display name of the query.</span></span> |
| <span data-ttu-id="c5696-181">properties.category</span><span class="sxs-lookup"><span data-stu-id="c5696-181">properties.category</span></span> |<span data-ttu-id="c5696-182">**Обязательный**.</span><span class="sxs-lookup"><span data-stu-id="c5696-182">**Required**.</span></span> <span data-ttu-id="c5696-183">Определяемая пользователем категория запроса.</span><span class="sxs-lookup"><span data-stu-id="c5696-183">The user-defined category of the query.</span></span> |

> [!NOTE]
> <span data-ttu-id="c5696-184">Сейчас, когда поступают запросы на сохраненные поисковые запросы в рабочей области, API поиска по службе Log Analytics возвращает сохраненные поисковые запросы, созданные пользователем.</span><span class="sxs-lookup"><span data-stu-id="c5696-184">The Log Analytics search API currently returns user-created saved searches when polled for saved searches in a workspace.</span></span> <span data-ttu-id="c5696-185">Сохраненные поисковые запросы, созданные решениями, не возвращаются.</span><span class="sxs-lookup"><span data-stu-id="c5696-185">The API does not return saved searches provided by solutions.</span></span>
>
>

### <a name="create-saved-searches"></a><span data-ttu-id="c5696-186">Создание сохраненных поисковых запросов</span><span class="sxs-lookup"><span data-stu-id="c5696-186">Create saved searches</span></span>
<span data-ttu-id="c5696-187">**Запрос:**</span><span class="sxs-lookup"><span data-stu-id="c5696-187">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> <span data-ttu-id="c5696-188">Имена всех сохраненных поисковых запросов, отчетов и действий, создаваемых с помощью API Log Analytics, должны быть в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="c5696-188">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

### <a name="delete-saved-searches"></a><span data-ttu-id="c5696-189">Удаление сохраненных поисковых запросов</span><span class="sxs-lookup"><span data-stu-id="c5696-189">Delete saved searches</span></span>
<span data-ttu-id="c5696-190">**Запрос:**</span><span class="sxs-lookup"><span data-stu-id="c5696-190">**Request:**</span></span>

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a><span data-ttu-id="c5696-191">Изменение сохраненных поисковых запросов</span><span class="sxs-lookup"><span data-stu-id="c5696-191">Update saved searches</span></span>
 <span data-ttu-id="c5696-192">**Запрос:**</span><span class="sxs-lookup"><span data-stu-id="c5696-192">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a><span data-ttu-id="c5696-193">Метаданные (только JSON)</span><span class="sxs-lookup"><span data-stu-id="c5696-193">Metadata - JSON only</span></span>
<span data-ttu-id="c5696-194">Вот способ узнать, какие поля есть в журналах данных, собранных в рабочей области. Этот способ подходит для всех типов журналов.</span><span class="sxs-lookup"><span data-stu-id="c5696-194">Here’s a way to see the fields for all log types for the data collected in your workspace.</span></span> <span data-ttu-id="c5696-195">Например, если вы хотите узнать, есть ли в типе события поле с именем компьютера, это можно сделать с помощью запроса.</span><span class="sxs-lookup"><span data-stu-id="c5696-195">For example, if you want you know if the Event type has a field named Computer, then this query is one way to check.</span></span>

<span data-ttu-id="c5696-196">**Запрос полей**</span><span class="sxs-lookup"><span data-stu-id="c5696-196">**Request for Fields:**</span></span>

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

<span data-ttu-id="c5696-197">**Ответ.**</span><span class="sxs-lookup"><span data-stu-id="c5696-197">**Response:**</span></span>

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

<span data-ttu-id="c5696-198">В следующей таблице описаны имеющиеся свойства.</span><span class="sxs-lookup"><span data-stu-id="c5696-198">The following table describes the properties that are available.</span></span>

| <span data-ttu-id="c5696-199">**Свойство**</span><span class="sxs-lookup"><span data-stu-id="c5696-199">**Property**</span></span> | <span data-ttu-id="c5696-200">**Описание**</span><span class="sxs-lookup"><span data-stu-id="c5696-200">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="c5696-201">name</span><span class="sxs-lookup"><span data-stu-id="c5696-201">name</span></span> |<span data-ttu-id="c5696-202">Имя поля.</span><span class="sxs-lookup"><span data-stu-id="c5696-202">Field name.</span></span> |
| <span data-ttu-id="c5696-203">displayName</span><span class="sxs-lookup"><span data-stu-id="c5696-203">displayName</span></span> |<span data-ttu-id="c5696-204">Отображаемое имя поля.</span><span class="sxs-lookup"><span data-stu-id="c5696-204">The display name of the field.</span></span> |
| <span data-ttu-id="c5696-205">type</span><span class="sxs-lookup"><span data-stu-id="c5696-205">type</span></span> |<span data-ttu-id="c5696-206">Тип значения в поле.</span><span class="sxs-lookup"><span data-stu-id="c5696-206">The Type of the field value.</span></span> |
| <span data-ttu-id="c5696-207">facetable</span><span class="sxs-lookup"><span data-stu-id="c5696-207">facetable</span></span> |<span data-ttu-id="c5696-208">Сочетание текущих свойств indexed, stored и facet.</span><span class="sxs-lookup"><span data-stu-id="c5696-208">Combination of current ‘indexed’, ‘stored ‘and ‘facet’ properties.</span></span> |
| <span data-ttu-id="c5696-209">display</span><span class="sxs-lookup"><span data-stu-id="c5696-209">display</span></span> |<span data-ttu-id="c5696-210">Текущее свойство display.</span><span class="sxs-lookup"><span data-stu-id="c5696-210">Current ‘display’ property.</span></span> <span data-ttu-id="c5696-211">Если поле отображается при поиске, используется значение true.</span><span class="sxs-lookup"><span data-stu-id="c5696-211">True if field is visible in search.</span></span> |
| <span data-ttu-id="c5696-212">ownerType</span><span class="sxs-lookup"><span data-stu-id="c5696-212">ownerType</span></span> |<span data-ttu-id="c5696-213">Используются только типы, принадлежащие подключенным IP-адресам.</span><span class="sxs-lookup"><span data-stu-id="c5696-213">Reduced to only Types belonging to onboarded IP’s.</span></span> |

## <a name="optional-parameters"></a><span data-ttu-id="c5696-214">Необязательные параметры</span><span class="sxs-lookup"><span data-stu-id="c5696-214">Optional parameters</span></span>
<span data-ttu-id="c5696-215">Ниже описаны дополнительные параметры, использовать которые необязательно.</span><span class="sxs-lookup"><span data-stu-id="c5696-215">The following information describes optional parameters available.</span></span>

### <a name="highlighting"></a><span data-ttu-id="c5696-216">Выделение</span><span class="sxs-lookup"><span data-stu-id="c5696-216">Highlighting</span></span>
<span data-ttu-id="c5696-217">Highlight — необязательный параметр, который сообщает поисковой подсистеме, что в ответ нужно добавить набор маркеров.</span><span class="sxs-lookup"><span data-stu-id="c5696-217">The “Highlight” parameter is an optional parameter you may use to request the search subsystem include a set of markers in its response.</span></span>

<span data-ttu-id="c5696-218">Эти маркеры указывают на начало и окончание выделяемого текста, который соответствует поисковому запросу.</span><span class="sxs-lookup"><span data-stu-id="c5696-218">These markers indicate the start and end highlighted text that matches the terms provided in your search query.</span></span>
<span data-ttu-id="c5696-219">Начальный и конечный маркеры, которые поисковая система будет использовать для выделения текста, можно задавать.</span><span class="sxs-lookup"><span data-stu-id="c5696-219">You may specify the start and end markers that are used by search to wrap the highlighted term.</span></span>

<span data-ttu-id="c5696-220">**Пример поискового запроса**</span><span class="sxs-lookup"><span data-stu-id="c5696-220">**Example search query**</span></span>

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

<span data-ttu-id="c5696-221">**Пример результата:**</span><span class="sxs-lookup"><span data-stu-id="c5696-221">**Sample result:**</span></span>

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

<span data-ttu-id="c5696-222">Обратите внимание, что предыдущий результат содержит сообщение об ошибке с префиксом и постфиксом.</span><span class="sxs-lookup"><span data-stu-id="c5696-222">Notice that the preceding result contains an error message that has been prefixed and appended.</span></span>

## <a name="computer-groups"></a><span data-ttu-id="c5696-223">Группы компьютеров</span><span class="sxs-lookup"><span data-stu-id="c5696-223">Computer groups</span></span>
<span data-ttu-id="c5696-224">Группы компьютеров — специальные сохраненные поисковые запросы, возвращающие набор компьютеров.</span><span class="sxs-lookup"><span data-stu-id="c5696-224">Computer groups are special saved searches that return a set of computers.</span></span>  <span data-ttu-id="c5696-225">Группу компьютеров можно использовать в других запросах, чтобы ограничить результаты компьютерами, которые входят в группу.</span><span class="sxs-lookup"><span data-stu-id="c5696-225">You can use a computer group in other queries to limit the results to the computers in the group.</span></span>  <span data-ttu-id="c5696-226">Группа компьютеров реализуется как сохраненный поисковый запрос с тегом Group (Группа) и значением Computer (Компьютер).</span><span class="sxs-lookup"><span data-stu-id="c5696-226">A computer group is implemented as a saved search with a Group tag with a value of Computer.</span></span>

<span data-ttu-id="c5696-227">Ниже представлен пример ответа для группы компьютеров.</span><span class="sxs-lookup"><span data-stu-id="c5696-227">Following is a sample response for a computer group.</span></span>

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

### <a name="retrieving-computer-groups"></a><span data-ttu-id="c5696-228">Извлечение группы компьютеров</span><span class="sxs-lookup"><span data-stu-id="c5696-228">Retrieving computer groups</span></span>
<span data-ttu-id="c5696-229">Для извлечения группы компьютеров используйте метод Get с идентификатором группы.</span><span class="sxs-lookup"><span data-stu-id="c5696-229">To retrieve a computer group, use the Get method with the group ID.</span></span>

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a><span data-ttu-id="c5696-230">Создание или обновление группы компьютеров</span><span class="sxs-lookup"><span data-stu-id="c5696-230">Creating or updating a computer group</span></span>
<span data-ttu-id="c5696-231">Для создания группы компьютеров используйте метод Put с уникальным идентификатором сохраненного поискового запроса.</span><span class="sxs-lookup"><span data-stu-id="c5696-231">To create a computer group, use the Put method with a unique saved search ID.</span></span> <span data-ttu-id="c5696-232">Если используется существующий идентификатор группы компьютеров, он будет изменен.</span><span class="sxs-lookup"><span data-stu-id="c5696-232">If you use an existing computer group ID, then that one is modified.</span></span> <span data-ttu-id="c5696-233">Если группа компьютеров создается на портале Log Analytics, идентификатор создается из группы и имени.</span><span class="sxs-lookup"><span data-stu-id="c5696-233">When you create a computer group in the Log Analytics portal, then the ID is created from the group and name.</span></span>

<span data-ttu-id="c5696-234">Для правильной работы запрос, используемый для определения группы, должен возвращать набор компьютеров для группы.</span><span class="sxs-lookup"><span data-stu-id="c5696-234">The query used for the group definition must return a set of computers for the group to function properly.</span></span>  <span data-ttu-id="c5696-235">Для получения правильных данных рекомендуется заканчивать запрос строкой `| Distinct Computer`.</span><span class="sxs-lookup"><span data-stu-id="c5696-235">It's recommended that you end your query with `| Distinct Computer` to ensure the correct data is returned.</span></span>

<span data-ttu-id="c5696-236">Для того чтобы поиск классифицировался как группа компьютеров, определение сохраненного поискового запроса должно включать тег Group (Группа) со значением Computer (Компьютер).</span><span class="sxs-lookup"><span data-stu-id="c5696-236">The definition of the saved search must include a tag named Group with a value of Computer for the search to be classified as a computer group.</span></span>

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a><span data-ttu-id="c5696-237">Удаление группы компьютеров</span><span class="sxs-lookup"><span data-stu-id="c5696-237">Deleting computer groups</span></span>
<span data-ttu-id="c5696-238">Для удаления группы компьютеров используйте метод Delete с идентификатором группы.</span><span class="sxs-lookup"><span data-stu-id="c5696-238">To delete a computer group, use the Delete method with the group ID.</span></span>

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a><span data-ttu-id="c5696-239">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c5696-239">Next steps</span></span>
* <span data-ttu-id="c5696-240">Узнайте больше о [запросах поиска по журналу](log-analytics-log-searches.md) для создания запросов с использованием настраиваемых полей в качестве условия.</span><span class="sxs-lookup"><span data-stu-id="c5696-240">Learn about [log searches](log-analytics-log-searches.md) to build queries using custom fields for criteria.</span></span>
