---
title: "Использование REST API оповещений Log Analytics в OMS"
description: "REST API оповещений Log Analytics позволяет создавать оповещения и управлять ими в Log Analytics — компоненте Operations Management Suite (OMS).  В этой статье приводятся сведения об интерфейсе API и примеры выполнения различных операций."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5ce72ffef4394bf3bbe39fa420c4fcaa965ae35c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a><span data-ttu-id="1649f-104">Создание правил генерации оповещений и управление ими в Log Analytics с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="1649f-104">Create and manage alert rules in Log Analytics with REST API</span></span>
<span data-ttu-id="1649f-105">REST API оповещений в Log Analytics позволяет создавать оповещения и управлять ими в Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="1649f-105">The Log Analytics Alert REST API allows you to create and manage alerts in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="1649f-106">В этой статье приводятся сведения об интерфейсе API и примеры выполнения различных операций.</span><span class="sxs-lookup"><span data-stu-id="1649f-106">This article provides details of the API and several examples for performing different operations.</span></span>

<span data-ttu-id="1649f-107">Для поиска в службе Log Analytics используется REST API категории RESTful — к нему можно получить доступ с помощью REST API Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1649f-107">The Log Analytics Search REST API is RESTful and can be accessed via the Azure Resource Manager REST API.</span></span> <span data-ttu-id="1649f-108">В этом документе вы найдете примеры, когда доступ к API из командной строки PowerShell осуществляется через [ARMClient](https://github.com/projectkudu/ARMClient) — инструмент командной строки с открытым исходным кодом, который упрощает вызов API Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1649f-108">In this document you will find examples where the API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open source command line tool that simplifies invoking the Azure Resource Manager API.</span></span> <span data-ttu-id="1649f-109">Использование ARMClient и PowerShell — это один из множества вариантов получения доступа к API поиска по службе Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1649f-109">The use of ARMClient and PowerShell is one of many options to access the Log Analytics Search API.</span></span> <span data-ttu-id="1649f-110">С помощью этих средств можно использовать API диспетчера ресурсов Azure категории RESTful для осуществления вызовов рабочих областей OMS и выполнения команд поиска в них.</span><span class="sxs-lookup"><span data-stu-id="1649f-110">With these tools you can utilize the RESTful Azure Resource Manager API to make calls to OMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="1649f-111">API будет выдавать результаты поиска в формате JSON, позволяя программно использовать результаты поиска различными способами.</span><span class="sxs-lookup"><span data-stu-id="1649f-111">The API will output search results to you in JSON format, allowing you to use the search results in many different ways programmatically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1649f-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1649f-112">Prerequisites</span></span>
<span data-ttu-id="1649f-113">В настоящее время оповещения могут создаваться только с помощью сохраненного поиска в службе Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1649f-113">Currently, alerts can only be created with a saved search in Log Analytics.</span></span>  <span data-ttu-id="1649f-114">Дополнительные сведения см. в статье [REST API поиска в журналах](log-analytics-log-search-api.md).</span><span class="sxs-lookup"><span data-stu-id="1649f-114">You can refer to the [Log Search REST API](log-analytics-log-search-api.md) for more information.</span></span>

## <a name="schedules"></a><span data-ttu-id="1649f-115">Расписания</span><span class="sxs-lookup"><span data-stu-id="1649f-115">Schedules</span></span>
<span data-ttu-id="1649f-116">Сохраненный поиск может включать одно расписание или несколько.</span><span class="sxs-lookup"><span data-stu-id="1649f-116">A saved search can have one or more schedules.</span></span> <span data-ttu-id="1649f-117">Расписание определяет, как часто выполняется поиск, а также интервал времени для определения условий.</span><span class="sxs-lookup"><span data-stu-id="1649f-117">The schedule defines how often the search is run and the time interval over which the criteria is identified.</span></span>
<span data-ttu-id="1649f-118">У расписаний есть свойства, приведенные в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="1649f-118">Schedules have the properties in the following table.</span></span>

| <span data-ttu-id="1649f-119">Свойство</span><span class="sxs-lookup"><span data-stu-id="1649f-119">Property</span></span> | <span data-ttu-id="1649f-120">Описание</span><span class="sxs-lookup"><span data-stu-id="1649f-120">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1649f-121">Интервал</span><span class="sxs-lookup"><span data-stu-id="1649f-121">Interval</span></span> |<span data-ttu-id="1649f-122">Насколько часто выполняется поиск.</span><span class="sxs-lookup"><span data-stu-id="1649f-122">How often the search is run.</span></span> <span data-ttu-id="1649f-123">Измеряется в минутах.</span><span class="sxs-lookup"><span data-stu-id="1649f-123">Measured in minutes.</span></span> |
| <span data-ttu-id="1649f-124">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="1649f-124">QueryTimeSpan</span></span> |<span data-ttu-id="1649f-125">Интервал времени для вычисления условий.</span><span class="sxs-lookup"><span data-stu-id="1649f-125">The time interval over which the criteria is evaluated.</span></span> <span data-ttu-id="1649f-126">Значение должно быть больше или равно значению свойства Interval.</span><span class="sxs-lookup"><span data-stu-id="1649f-126">Must be equal to or greater than Interval.</span></span> <span data-ttu-id="1649f-127">Измеряется в минутах.</span><span class="sxs-lookup"><span data-stu-id="1649f-127">Measured in minutes.</span></span> |
| <span data-ttu-id="1649f-128">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="1649f-128">Version</span></span> |<span data-ttu-id="1649f-129">Используемая версия API.</span><span class="sxs-lookup"><span data-stu-id="1649f-129">The API version being used.</span></span>  <span data-ttu-id="1649f-130">Сейчас это свойство всегда должно иметь значение 1.</span><span class="sxs-lookup"><span data-stu-id="1649f-130">Currently, this should always be set to 1.</span></span> |

<span data-ttu-id="1649f-131">Например, рассмотрим запрос событий с интервалом (свойство Interval) 15 минут и временным диапазоном (свойство TimeSpan) 30 минут.</span><span class="sxs-lookup"><span data-stu-id="1649f-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span></span> <span data-ttu-id="1649f-132">В этом случае запрос будет выполняться каждые 15 минут, а оповещение будет создаваться, если условие по-прежнему соблюдается по прошествии 30-минутного периода.</span><span class="sxs-lookup"><span data-stu-id="1649f-132">In this case, the query would be run every 15 minutes, and an alert would be triggered if the criteria continued to resolve to true over a 30 minute span.</span></span>

### <a name="retrieving-schedules"></a><span data-ttu-id="1649f-133">Получение расписаний</span><span class="sxs-lookup"><span data-stu-id="1649f-133">Retrieving schedules</span></span>
<span data-ttu-id="1649f-134">Используйте метод Get для получения всех расписаний для сохраненного поиска.</span><span class="sxs-lookup"><span data-stu-id="1649f-134">Use the Get method to retrieve all schedules for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

<span data-ttu-id="1649f-135">Чтобы получить конкретное расписание для сохраненного поискового запроса, используйте метод Get с идентификатором расписания.</span><span class="sxs-lookup"><span data-stu-id="1649f-135">Use the Get method with a schedule ID to retrieve a particular schedule for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

<span data-ttu-id="1649f-136">Ниже приведен пример ответа для расписания.</span><span class="sxs-lookup"><span data-stu-id="1649f-136">Following is a sample response for a schedule.</span></span>

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a><span data-ttu-id="1649f-137">Создание расписания</span><span class="sxs-lookup"><span data-stu-id="1649f-137">Creating a schedule</span></span>
<span data-ttu-id="1649f-138">Чтобы создать расписание, используйте метод Put с уникальным идентификатором расписания.</span><span class="sxs-lookup"><span data-stu-id="1649f-138">Use the Put method with a unique schedule ID to create a new schedule.</span></span>  <span data-ttu-id="1649f-139">Обратите внимание, что нельзя использовать один и тот же идентификатор для двух расписаний, даже если они связаны с разными сохраненными поисковыми запросами.</span><span class="sxs-lookup"><span data-stu-id="1649f-139">Note that two schedules cannot have the same ID even if they are associated with different saved searches.</span></span>  <span data-ttu-id="1649f-140">При создании расписания в консоли OMS для идентификатора расписания создается GUID.</span><span class="sxs-lookup"><span data-stu-id="1649f-140">When you create a schedule in the OMS console, a GUID is created for the schedule ID.</span></span>

> [!NOTE]
> <span data-ttu-id="1649f-141">Имена всех сохраненных поисковых запросов, отчетов и действий, создаваемых с помощью API Log Analytics, должны быть в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="1649f-141">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a><span data-ttu-id="1649f-142">Изменение расписания</span><span class="sxs-lookup"><span data-stu-id="1649f-142">Editing a schedule</span></span>
<span data-ttu-id="1649f-143">Чтобы изменить расписание, используйте метод Put с идентификатором существующего расписания для того же сохраненного поискового запроса.</span><span class="sxs-lookup"><span data-stu-id="1649f-143">Use the Put method with an existing schedule ID for the same saved search to modify that schedule.</span></span>  <span data-ttu-id="1649f-144">Текст запроса должен содержать Etag расписания.</span><span class="sxs-lookup"><span data-stu-id="1649f-144">The body of the request must include the etag of the schedule.</span></span>

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a><span data-ttu-id="1649f-145">Удаление расписаний</span><span class="sxs-lookup"><span data-stu-id="1649f-145">Deleting schedules</span></span>
<span data-ttu-id="1649f-146">Чтобы удалить расписание, используйте метод Delete с идентификатором расписания.</span><span class="sxs-lookup"><span data-stu-id="1649f-146">Use the Delete method with a schedule ID to delete a schedule.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a><span data-ttu-id="1649f-147">Действия</span><span class="sxs-lookup"><span data-stu-id="1649f-147">Actions</span></span>
<span data-ttu-id="1649f-148">Расписание может включать несколько действий.</span><span class="sxs-lookup"><span data-stu-id="1649f-148">A schedule can have multiple actions.</span></span> <span data-ttu-id="1649f-149">Действие может определять один выполняемый процесс или несколько (например, отправку почты или запуск модуля Runbook) или задавать пороговое значение, определяющее, когда результаты поиска отвечают некоторым условиям.</span><span class="sxs-lookup"><span data-stu-id="1649f-149">An action may define one or more processes to perform such as sending a mail or starting a runbook, or it may define a threshold that determines when the results of a search match some criteria.</span></span>  <span data-ttu-id="1649f-150">Некоторые действия будут определять оба элемента так, чтобы процессы выполнялись при достижении порогового значения.</span><span class="sxs-lookup"><span data-stu-id="1649f-150">Some actions will define both so that the processes are performed when the threshold is met.</span></span>

<span data-ttu-id="1649f-151">У всех действий есть свойства, приведенные в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="1649f-151">All actions have the properties in the following table.</span></span>  <span data-ttu-id="1649f-152">Разные типы оповещений имеют различные дополнительные свойства, которые описаны ниже.</span><span class="sxs-lookup"><span data-stu-id="1649f-152">Different types of alerts have different additional properties which are described below.</span></span>

| <span data-ttu-id="1649f-153">Свойство</span><span class="sxs-lookup"><span data-stu-id="1649f-153">Property</span></span> | <span data-ttu-id="1649f-154">Описание</span><span class="sxs-lookup"><span data-stu-id="1649f-154">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1649f-155">Тип</span><span class="sxs-lookup"><span data-stu-id="1649f-155">Type</span></span> |<span data-ttu-id="1649f-156">Тип действия.</span><span class="sxs-lookup"><span data-stu-id="1649f-156">Type of the action.</span></span>  <span data-ttu-id="1649f-157">Сейчас возможными значениями являются Alert и Webhook.</span><span class="sxs-lookup"><span data-stu-id="1649f-157">Currently the possible values are Alert and Webhook.</span></span> |
| <span data-ttu-id="1649f-158">Имя</span><span class="sxs-lookup"><span data-stu-id="1649f-158">Name</span></span> |<span data-ttu-id="1649f-159">Отображаемое имя оповещения.</span><span class="sxs-lookup"><span data-stu-id="1649f-159">Display name for the alert.</span></span> |
| <span data-ttu-id="1649f-160">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="1649f-160">Version</span></span> |<span data-ttu-id="1649f-161">Используемая версия API.</span><span class="sxs-lookup"><span data-stu-id="1649f-161">The API version being used.</span></span>  <span data-ttu-id="1649f-162">Сейчас это свойство всегда должно иметь значение 1.</span><span class="sxs-lookup"><span data-stu-id="1649f-162">Currently, this should always be set to 1.</span></span> |

### <a name="retrieving-actions"></a><span data-ttu-id="1649f-163">Получение действий</span><span class="sxs-lookup"><span data-stu-id="1649f-163">Retrieving actions</span></span>
<span data-ttu-id="1649f-164">Используйте метод Get для получения всех действий для расписания.</span><span class="sxs-lookup"><span data-stu-id="1649f-164">Use the Get method to retrieve all actions for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

<span data-ttu-id="1649f-165">Используйте метод Get с идентификатором действия для получения конкретного действия для расписания.</span><span class="sxs-lookup"><span data-stu-id="1649f-165">Use the Get method with the action ID to retrieve a particular action for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a><span data-ttu-id="1649f-166">Создание или изменение действий</span><span class="sxs-lookup"><span data-stu-id="1649f-166">Creating or editing actions</span></span>
<span data-ttu-id="1649f-167">Чтобы создать действие, используйте метод Put с идентификатором действия, уникальным для расписания.</span><span class="sxs-lookup"><span data-stu-id="1649f-167">Use the Put method with an action ID that is unique to the schedule to create a new action.</span></span>  <span data-ttu-id="1649f-168">При создании действия в консоли OMS для идентификатора действия отображается GUID.</span><span class="sxs-lookup"><span data-stu-id="1649f-168">When you create an action in the OMS console, a GUID is for the action ID.</span></span>

> [!NOTE]
> <span data-ttu-id="1649f-169">Имена всех сохраненных поисковых запросов, отчетов и действий, создаваемых с помощью API Log Analytics, должны быть в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="1649f-169">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

<span data-ttu-id="1649f-170">Чтобы изменить расписание, используйте метод Put с идентификатором существующего действия для того же сохраненного поискового запроса.</span><span class="sxs-lookup"><span data-stu-id="1649f-170">Use the Put method with an existing action ID for the same saved search to modify that schedule.</span></span>  <span data-ttu-id="1649f-171">Текст запроса должен содержать Etag расписания.</span><span class="sxs-lookup"><span data-stu-id="1649f-171">The body of the request must include the etag of the schedule.</span></span>

<span data-ttu-id="1649f-172">Формат запроса для создания действия зависит от типа действия, поэтому эти примеры приведены в разделах ниже.</span><span class="sxs-lookup"><span data-stu-id="1649f-172">The request format for creating a new action varies by action type so these examples are provided in the sections below.</span></span>

### <a name="deleting-actions"></a><span data-ttu-id="1649f-173">Удаление действий</span><span class="sxs-lookup"><span data-stu-id="1649f-173">Deleting actions</span></span>
<span data-ttu-id="1649f-174">Для удаления действия используйте метод Delete с идентификатором действия.</span><span class="sxs-lookup"><span data-stu-id="1649f-174">Use the Delete method with the action ID to delete an action.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a><span data-ttu-id="1649f-175">Действия оповещений</span><span class="sxs-lookup"><span data-stu-id="1649f-175">Alert Actions</span></span>
<span data-ttu-id="1649f-176">Расписание должно включать одно-единственное действие оповещения.</span><span class="sxs-lookup"><span data-stu-id="1649f-176">A Schedule should have one and only one Alert action.</span></span>  <span data-ttu-id="1649f-177">Действия оповещений включают один или несколько разделов в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="1649f-177">Alert actions have one or more of the sections in the following table.</span></span>  <span data-ttu-id="1649f-178">Они более подробно описаны далее.</span><span class="sxs-lookup"><span data-stu-id="1649f-178">Each is described in further detail below.</span></span>

| <span data-ttu-id="1649f-179">Раздел</span><span class="sxs-lookup"><span data-stu-id="1649f-179">Section</span></span> | <span data-ttu-id="1649f-180">Описание</span><span class="sxs-lookup"><span data-stu-id="1649f-180">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1649f-181">Пороговое значение</span><span class="sxs-lookup"><span data-stu-id="1649f-181">Threshold</span></span> |<span data-ttu-id="1649f-182">Условие для запуска действия.</span><span class="sxs-lookup"><span data-stu-id="1649f-182">Criteria for when the action is run.</span></span> |
| <span data-ttu-id="1649f-183">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="1649f-183">EmailNotification</span></span> |<span data-ttu-id="1649f-184">Отправка сообщения нескольким получателям.</span><span class="sxs-lookup"><span data-stu-id="1649f-184">Send mail to multiple recipients.</span></span> |
| <span data-ttu-id="1649f-185">Исправление</span><span class="sxs-lookup"><span data-stu-id="1649f-185">Remediation</span></span> |<span data-ttu-id="1649f-186">Запуск модуля Runbook в службе автоматизации Azure для попытки исправления выявленной проблемы.</span><span class="sxs-lookup"><span data-stu-id="1649f-186">Start a runbook in Azure Automation to attempt to correct identified issue.</span></span> |

#### <a name="thresholds"></a><span data-ttu-id="1649f-187">Пороговые значения</span><span class="sxs-lookup"><span data-stu-id="1649f-187">Thresholds</span></span>
<span data-ttu-id="1649f-188">Действие оповещения должно включать одно-единственное пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="1649f-188">An Alert action should have one and only one threshold.</span></span>  <span data-ttu-id="1649f-189">Когда результат сохраненного поиска соответствует пороговому значению в действии, связанном с этим поиском, запускаются другие процессы в этом действии.</span><span class="sxs-lookup"><span data-stu-id="1649f-189">When the results of a saved search match the threshold in an action associated with that search, then any other processes in that action are run.</span></span>  <span data-ttu-id="1649f-190">Действие также может содержать только пороговое значение, чтобы его можно было использовать с действиями других типов, которые не содержат пороговых значений.</span><span class="sxs-lookup"><span data-stu-id="1649f-190">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span></span>

<span data-ttu-id="1649f-191">У пороговых значений есть свойства, приведенные в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="1649f-191">Thresholds have the properties in the following table.</span></span>

| <span data-ttu-id="1649f-192">Свойство</span><span class="sxs-lookup"><span data-stu-id="1649f-192">Property</span></span> | <span data-ttu-id="1649f-193">Описание</span><span class="sxs-lookup"><span data-stu-id="1649f-193">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1649f-194">Оператор</span><span class="sxs-lookup"><span data-stu-id="1649f-194">Operator</span></span> |<span data-ttu-id="1649f-195">Оператор для сравнения порогового значения.</span><span class="sxs-lookup"><span data-stu-id="1649f-195">Operator for the threshold comparison.</span></span> <br> <span data-ttu-id="1649f-196">gt — больше</span><span class="sxs-lookup"><span data-stu-id="1649f-196">gt = Greater Than</span></span> <br> <span data-ttu-id="1649f-197">lt = меньше чем</span><span class="sxs-lookup"><span data-stu-id="1649f-197">lt = Less Than</span></span> |
| <span data-ttu-id="1649f-198">Значение</span><span class="sxs-lookup"><span data-stu-id="1649f-198">Value</span></span> |<span data-ttu-id="1649f-199">Пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="1649f-199">Value for the threshold.</span></span> |

<span data-ttu-id="1649f-200">Например, рассмотрим запрос событий с интервалом (свойство Interval) 15 минут, временным диапазоном (свойство TimeSpan) 30 минут и пороговым значением больше 10.</span><span class="sxs-lookup"><span data-stu-id="1649f-200">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span></span> <span data-ttu-id="1649f-201">В этом случае запрос будет выполняться каждые 15 минут, а оповещение будет создаваться при возврате 10 событий, созданных за 30-минутный период.</span><span class="sxs-lookup"><span data-stu-id="1649f-201">In this case, the query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30 minute span.</span></span>

<span data-ttu-id="1649f-202">Ниже приведен пример ответа для действия, содержащего только пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="1649f-202">Following is a sample response for an action with only a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

<span data-ttu-id="1649f-203">Чтобы создать действие с пороговым значением для расписания, используйте метод Put с уникальным идентификатором действия.</span><span class="sxs-lookup"><span data-stu-id="1649f-203">Use the Put method with a unique action ID to create a new threshold action for a schedule.</span></span>  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

<span data-ttu-id="1649f-204">Чтобы изменить действие с пороговым значением для расписания, используйте метод Put с идентификатором существующего действия.</span><span class="sxs-lookup"><span data-stu-id="1649f-204">Use the Put method with an existing action ID to modify a threshold action for a schedule.</span></span>  <span data-ttu-id="1649f-205">Текст запроса должен содержать Etag действия.</span><span class="sxs-lookup"><span data-stu-id="1649f-205">The body of the request must include the etag of the action.</span></span>

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a><span data-ttu-id="1649f-206">Уведомление по электронной почте</span><span class="sxs-lookup"><span data-stu-id="1649f-206">Email Notification</span></span>
<span data-ttu-id="1649f-207">Уведомления отправляются для одного или нескольких получателей по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="1649f-207">Email Notifications send mail to one or more recipients.</span></span>  <span data-ttu-id="1649f-208">Уведомления могут включать свойства, приведенные в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="1649f-208">They include the properties in the following table.</span></span>

| <span data-ttu-id="1649f-209">Свойство</span><span class="sxs-lookup"><span data-stu-id="1649f-209">Property</span></span> | <span data-ttu-id="1649f-210">Описание</span><span class="sxs-lookup"><span data-stu-id="1649f-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1649f-211">Recipients</span><span class="sxs-lookup"><span data-stu-id="1649f-211">Recipients</span></span> |<span data-ttu-id="1649f-212">Список адресов электронной почты.</span><span class="sxs-lookup"><span data-stu-id="1649f-212">List of mail addresses.</span></span> |
| <span data-ttu-id="1649f-213">Субъект</span><span class="sxs-lookup"><span data-stu-id="1649f-213">Subject</span></span> |<span data-ttu-id="1649f-214">Тема сообщения электронной почты.</span><span class="sxs-lookup"><span data-stu-id="1649f-214">The subject of the mail.</span></span> |
| <span data-ttu-id="1649f-215">Вложение</span><span class="sxs-lookup"><span data-stu-id="1649f-215">Attachment</span></span> |<span data-ttu-id="1649f-216">Вложения пока не поддерживаются, поэтому это свойство всегда будет иметь значение None.</span><span class="sxs-lookup"><span data-stu-id="1649f-216">Attachments are not currently supported, so this will always have a value of “None”.</span></span> |

<span data-ttu-id="1649f-217">Ниже приведен пример ответа для действия уведомления по электронной почте с пороговым значением.</span><span class="sxs-lookup"><span data-stu-id="1649f-217">Following is a sample response for an email notification action with a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is the subject",
            "Attachment": "None"
        },
        "Version": 1
    }

<span data-ttu-id="1649f-218">Чтобы создать действие почты для расписания, используйте метод Put с уникальным идентификатором действия.</span><span class="sxs-lookup"><span data-stu-id="1649f-218">Use the Put method with a unique action ID to create a new e-mail action for a schedule.</span></span>  <span data-ttu-id="1649f-219">В следующем примере создается уведомление по электронной почте с пороговым значением, которое отправляется в случае, если результаты сохраненного поиска превышают пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="1649f-219">The following example creates an email notification with a threshold so the mail is sent when the results of the saved search exceed the threshold.</span></span>

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

<span data-ttu-id="1649f-220">Чтобы изменить действие почты для расписания, используйте метод Put с идентификатором существующего действия.</span><span class="sxs-lookup"><span data-stu-id="1649f-220">Use the Put method with an existing action ID to modify an e-mail action for a schedule.</span></span>  <span data-ttu-id="1649f-221">Текст запроса должен содержать Etag действия.</span><span class="sxs-lookup"><span data-stu-id="1649f-221">The body of the request must include the etag of the action.</span></span>

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a><span data-ttu-id="1649f-222">Действия исправления</span><span class="sxs-lookup"><span data-stu-id="1649f-222">Remediation actions</span></span>
<span data-ttu-id="1649f-223">Служба исправлений запускает модуль Runbook в службе автоматизации Azure, который пытается устранить проблему, указанную в оповещении.</span><span class="sxs-lookup"><span data-stu-id="1649f-223">Remediations start a runbook in Azure Automation that attempts to correct the problem identified by the alert.</span></span>  <span data-ttu-id="1649f-224">Вам потребуется создать объект webhook для модуля Runbook, используемого в действии исправления, а затем указать его универсальный код ресурса (URI) в свойстве WebhookUri.</span><span class="sxs-lookup"><span data-stu-id="1649f-224">You must create a webhook for the runbook used in a remediation action and then specify the URI in the WebhookUri property.</span></span>  <span data-ttu-id="1649f-225">При создании этого действия с помощью консоли OMS новый объект webhook для модуля Runbook создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="1649f-225">When you create this action using the OMS console, a new webhook is automatically created for the runbook.</span></span>

<span data-ttu-id="1649f-226">Исправления могут включать свойства, приведенные в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="1649f-226">Remediations include the properties in the following table.</span></span>

| <span data-ttu-id="1649f-227">Свойство</span><span class="sxs-lookup"><span data-stu-id="1649f-227">Property</span></span> | <span data-ttu-id="1649f-228">Описание</span><span class="sxs-lookup"><span data-stu-id="1649f-228">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1649f-229">RunbookName</span><span class="sxs-lookup"><span data-stu-id="1649f-229">RunbookName</span></span> |<span data-ttu-id="1649f-230">Имя модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="1649f-230">Name of the runbook.</span></span> <span data-ttu-id="1649f-231">Оно должно соответствовать имени опубликованного модуля Runbook в учетной записи автоматизации, настроенной в решении автоматизации в рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="1649f-231">This must match a published runbook in the automation account configured in the Automation Solution in your OMS workspace.</span></span> |
| <span data-ttu-id="1649f-232">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="1649f-232">WebhookUri</span></span> |<span data-ttu-id="1649f-233">Универсальный код ресурса (URI) объекта webhook.</span><span class="sxs-lookup"><span data-stu-id="1649f-233">URI of the webhook.</span></span> |
| <span data-ttu-id="1649f-234">Expiry</span><span class="sxs-lookup"><span data-stu-id="1649f-234">Expiry</span></span> |<span data-ttu-id="1649f-235">Дата и время окончания срока действия объекта webhook.</span><span class="sxs-lookup"><span data-stu-id="1649f-235">The expiration date and time of the webhook.</span></span>  <span data-ttu-id="1649f-236">Если объект webhook не имеет срока действия, это может быть любая допустимая дата в будущем.</span><span class="sxs-lookup"><span data-stu-id="1649f-236">If the webhook doesn’t have an expiration, then this can be any valid future date.</span></span> |

<span data-ttu-id="1649f-237">Ниже приведен пример ответа для действия исправления с пороговым значением.</span><span class="sxs-lookup"><span data-stu-id="1649f-237">Following is a sample response for a remediation action with a threshold.</span></span>

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

<span data-ttu-id="1649f-238">Чтобы создать действие исправления для расписания, используйте метод Put с уникальным идентификатором действия.</span><span class="sxs-lookup"><span data-stu-id="1649f-238">Use the Put method with a unique action ID to create a new remediation action for a schedule.</span></span>  <span data-ttu-id="1649f-239">В следующем примере создается исправление с пороговым значением для запуска модуля Runbook в случае, если результаты сохраненного поиска превышают пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="1649f-239">The following example creates a remediation with a threshold so the runbook is started when the results of the saved search exceed the threshold.</span></span>

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

<span data-ttu-id="1649f-240">Чтобы изменить действие исправления для расписания, используйте метод Put с идентификатором существующего действия.</span><span class="sxs-lookup"><span data-stu-id="1649f-240">Use the Put method with an existing action ID to modify a remediation action for a schedule.</span></span>  <span data-ttu-id="1649f-241">Текст запроса должен содержать Etag действия.</span><span class="sxs-lookup"><span data-stu-id="1649f-241">The body of the request must include the etag of the action.</span></span>

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a><span data-ttu-id="1649f-242">Пример</span><span class="sxs-lookup"><span data-stu-id="1649f-242">Example</span></span>
<span data-ttu-id="1649f-243">Ниже приведен полный пример создания оповещения по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="1649f-243">Following is a complete example to create a new email alert.</span></span>  <span data-ttu-id="1649f-244">Создается новое расписание, а также действие, содержащее пороговое значение и сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="1649f-244">This creates a new schedule along with an action containing a threshold and email.</span></span>

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a><span data-ttu-id="1649f-245">Действия webhook</span><span class="sxs-lookup"><span data-stu-id="1649f-245">Webhook actions</span></span>
<span data-ttu-id="1649f-246">Действия webhook запускают процесс путем вызова URL-адреса и, при необходимости, предоставления полезных данных для отправки.</span><span class="sxs-lookup"><span data-stu-id="1649f-246">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span></span>  <span data-ttu-id="1649f-247">Они похожи на действия исправления, но предназначены для объектов webhook, которые могут вызывать процессы, отличные от модулей Runbook службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="1649f-247">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span>  <span data-ttu-id="1649f-248">Они также включают дополнительную возможность предоставления полезных данных, доставляемых в удаленный процесс.</span><span class="sxs-lookup"><span data-stu-id="1649f-248">They also provide the additional option of providing a payload to be delivered to the remote process.</span></span>

<span data-ttu-id="1649f-249">Действиям webhook не назначается пороговое значение, однако их необходимо добавлять в расписание, которое включает действие оповещения с пороговым значением.</span><span class="sxs-lookup"><span data-stu-id="1649f-249">Webhook actions do not have a threshold but instead should be added to a schedule that has an Alert action with a threshold.</span></span>  <span data-ttu-id="1649f-250">Можно добавить несколько действий webhook, которые будут выполняться все одновременно при достижении порогового значения.</span><span class="sxs-lookup"><span data-stu-id="1649f-250">You can add multiple Webhook actions that will all be run when the threshold is met.</span></span>

<span data-ttu-id="1649f-251">Действия webhook могут включать свойства, приведенные в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="1649f-251">Webhook actions include the properties in the following table.</span></span>

| <span data-ttu-id="1649f-252">Свойство</span><span class="sxs-lookup"><span data-stu-id="1649f-252">Property</span></span> | <span data-ttu-id="1649f-253">Описание</span><span class="sxs-lookup"><span data-stu-id="1649f-253">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1649f-254">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="1649f-254">WebhookUri</span></span> |<span data-ttu-id="1649f-255">Тема сообщения электронной почты.</span><span class="sxs-lookup"><span data-stu-id="1649f-255">The subject of the mail.</span></span> |
| <span data-ttu-id="1649f-256">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="1649f-256">CustomPayload</span></span> |<span data-ttu-id="1649f-257">Пользовательские полезные данные, отправляемые в объект webhook.</span><span class="sxs-lookup"><span data-stu-id="1649f-257">Custom payload to be sent to the webhook.</span></span>  <span data-ttu-id="1649f-258">Формат зависит от данных, ожидаемых объектом webhook.</span><span class="sxs-lookup"><span data-stu-id="1649f-258">The format will depend on what the webhook is expecting.</span></span> |

<span data-ttu-id="1649f-259">Ниже приведен пример ответа для действия webhook и соответствующее действие оповещения с пороговым значением.</span><span class="sxs-lookup"><span data-stu-id="1649f-259">Following is a sample response for webhook action and an associated alert action with a threshold.</span></span>

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

#### <a name="create-or-edit-a-webhook-action"></a><span data-ttu-id="1649f-260">Создание или изменение действий webhook</span><span class="sxs-lookup"><span data-stu-id="1649f-260">Create or edit a webhook action</span></span>
<span data-ttu-id="1649f-261">Чтобы создать действие webhook для расписания, используйте метод Put с уникальным идентификатором действия.</span><span class="sxs-lookup"><span data-stu-id="1649f-261">Use the Put method with a unique action ID to create a new webhook action for a schedule.</span></span>  <span data-ttu-id="1649f-262">В следующем примере создается действие webhook и запускается действие оповещения с пороговым значением, если результаты сохраненного поиска превышают пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="1649f-262">The following example creates a Webhook action and an Alert action with a threshold so that the webhook will be triggered when the results of the saved search exceed the threshold.</span></span>

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

<span data-ttu-id="1649f-263">Чтобы изменить действие webhook для расписания, используйте метод Put с идентификатором существующего действия.</span><span class="sxs-lookup"><span data-stu-id="1649f-263">Use the Put method with an existing action ID to modify a webhook action for a schedule.</span></span>  <span data-ttu-id="1649f-264">Текст запроса должен содержать Etag действия.</span><span class="sxs-lookup"><span data-stu-id="1649f-264">The body of the request must include the etag of the action.</span></span>

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a><span data-ttu-id="1649f-265">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1649f-265">Next steps</span></span>
* <span data-ttu-id="1649f-266">Используйте [REST API для выполнения поиска в журналах](log-analytics-log-search-api.md) в службе Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1649f-266">Use the [REST API to perform log searches](log-analytics-log-search-api.md) in Log Analytics.</span></span>

