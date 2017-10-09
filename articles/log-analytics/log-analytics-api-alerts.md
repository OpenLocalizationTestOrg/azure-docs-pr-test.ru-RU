---
title: "aaaUsing OMS API аналитики журналов оповещений REST"
description: "Hello API REST предупреждения аналитики журналов позволяет toocreate оповещений и управление ими в службе анализа журналов, являющейся частью Operations Management Suite (OMS).  Эта статья содержит сведения hello API и несколько примеров для выполнения различных операций."
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
ms.openlocfilehash: 418dc7eb71d6151c6380b8925f1f147a0e13b178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a><span data-ttu-id="18780-104">Создание правил генерации оповещений и управление ими в Log Analytics с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="18780-104">Create and manage alert rules in Log Analytics with REST API</span></span>
<span data-ttu-id="18780-105">Hello API REST предупреждения аналитики журналов позволяет toocreate оповещений и управление ими в Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="18780-105">hello Log Analytics Alert REST API allows you toocreate and manage alerts in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="18780-106">Эта статья содержит сведения hello API и несколько примеров для выполнения различных операций.</span><span class="sxs-lookup"><span data-stu-id="18780-106">This article provides details of hello API and several examples for performing different operations.</span></span>

<span data-ttu-id="18780-107">Hello REST API поиска аналитики журналов относится к категории RESTful и может запускаться через REST API диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="18780-107">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager REST API.</span></span> <span data-ttu-id="18780-108">В этом документе вы найдете примеры, когда hello API осуществляется из командной строки PowerShell с помощью [ARMClient](https://github.com/projectkudu/ARMClient), Здравствуйте, средство командной строки с открытым исходным, который упрощает вызов API диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="18780-108">In this document you will find examples where hello API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open source command line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="18780-109">Hello использование ARMClient и PowerShell является одним из многих параметров tooaccess hello API поиска аналитики журналов.</span><span class="sxs-lookup"><span data-stu-id="18780-109">hello use of ARMClient and PowerShell is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="18780-110">С помощью этих средств можно использовать рабочие области tooOMS вызовы toomake API диспетчера ресурсов Azure категории RESTful hello и выполнения команд поиска в них.</span><span class="sxs-lookup"><span data-stu-id="18780-110">With these tools you can utilize hello RESTful Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="18780-111">Hello API будет выдавать tooyou результаты поиска в формате JSON, позволяя результаты поиска hello toouse различными способами программными средствами.</span><span class="sxs-lookup"><span data-stu-id="18780-111">hello API will output search results tooyou in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18780-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="18780-112">Prerequisites</span></span>
<span data-ttu-id="18780-113">В настоящее время оповещения могут создаваться только с помощью сохраненного поиска в службе Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="18780-113">Currently, alerts can only be created with a saved search in Log Analytics.</span></span>  <span data-ttu-id="18780-114">Можно ссылаться toohello [REST API поиска журналов](log-analytics-log-search-api.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="18780-114">You can refer toohello [Log Search REST API](log-analytics-log-search-api.md) for more information.</span></span>

## <a name="schedules"></a><span data-ttu-id="18780-115">Расписания</span><span class="sxs-lookup"><span data-stu-id="18780-115">Schedules</span></span>
<span data-ttu-id="18780-116">Сохраненный поиск может включать одно расписание или несколько.</span><span class="sxs-lookup"><span data-stu-id="18780-116">A saved search can have one or more schedules.</span></span> <span data-ttu-id="18780-117">Hello расписание определяет частоту hello поиска выполняется и идентифицируется hello интервал времени, через какие критерии hello.</span><span class="sxs-lookup"><span data-stu-id="18780-117">hello schedule defines how often hello search is run and hello time interval over which hello criteria is identified.</span></span>
<span data-ttu-id="18780-118">Расписания, имеют свойства hello в hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="18780-118">Schedules have hello properties in hello following table.</span></span>

| <span data-ttu-id="18780-119">Свойство</span><span class="sxs-lookup"><span data-stu-id="18780-119">Property</span></span> | <span data-ttu-id="18780-120">Описание</span><span class="sxs-lookup"><span data-stu-id="18780-120">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="18780-121">Интервал</span><span class="sxs-lookup"><span data-stu-id="18780-121">Interval</span></span> |<span data-ttu-id="18780-122">Как часто hello поиска выполняется.</span><span class="sxs-lookup"><span data-stu-id="18780-122">How often hello search is run.</span></span> <span data-ttu-id="18780-123">Измеряется в минутах.</span><span class="sxs-lookup"><span data-stu-id="18780-123">Measured in minutes.</span></span> |
| <span data-ttu-id="18780-124">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="18780-124">QueryTimeSpan</span></span> |<span data-ttu-id="18780-125">интервал времени Hello какие hello для вычисления условия.</span><span class="sxs-lookup"><span data-stu-id="18780-125">hello time interval over which hello criteria is evaluated.</span></span> <span data-ttu-id="18780-126">Должно быть больше интервала равно tooor.</span><span class="sxs-lookup"><span data-stu-id="18780-126">Must be equal tooor greater than Interval.</span></span> <span data-ttu-id="18780-127">Измеряется в минутах.</span><span class="sxs-lookup"><span data-stu-id="18780-127">Measured in minutes.</span></span> |
| <span data-ttu-id="18780-128">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="18780-128">Version</span></span> |<span data-ttu-id="18780-129">Здравствуйте, используемой версии API.</span><span class="sxs-lookup"><span data-stu-id="18780-129">hello API version being used.</span></span>  <span data-ttu-id="18780-130">В настоящее время это всегда должен иметь значение too1.</span><span class="sxs-lookup"><span data-stu-id="18780-130">Currently, this should always be set too1.</span></span> |

<span data-ttu-id="18780-131">Например, рассмотрим запрос событий с интервалом (свойство Interval) 15 минут и временным диапазоном (свойство TimeSpan) 30 минут.</span><span class="sxs-lookup"><span data-stu-id="18780-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span></span> <span data-ttu-id="18780-132">В этом случае hello запрос будет выполняться каждые 15 минут, и будет запускаться оповещение, если критерий hello продолжение tooresolve tootrue через интервал 30 минут.</span><span class="sxs-lookup"><span data-stu-id="18780-132">In this case, hello query would be run every 15 minutes, and an alert would be triggered if hello criteria continued tooresolve tootrue over a 30 minute span.</span></span>

### <a name="retrieving-schedules"></a><span data-ttu-id="18780-133">Получение расписаний</span><span class="sxs-lookup"><span data-stu-id="18780-133">Retrieving schedules</span></span>
<span data-ttu-id="18780-134">Используйте hello получить метод tooretrieve все расписания сохраненного поиска.</span><span class="sxs-lookup"><span data-stu-id="18780-134">Use hello Get method tooretrieve all schedules for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

<span data-ttu-id="18780-135">Используйте hello Get-метод с tooretrieve идентификатор расписания определенное расписание сохраненного поиска.</span><span class="sxs-lookup"><span data-stu-id="18780-135">Use hello Get method with a schedule ID tooretrieve a particular schedule for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

<span data-ttu-id="18780-136">Ниже приведен пример ответа для расписания.</span><span class="sxs-lookup"><span data-stu-id="18780-136">Following is a sample response for a schedule.</span></span>

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

### <a name="creating-a-schedule"></a><span data-ttu-id="18780-137">Создание расписания</span><span class="sxs-lookup"><span data-stu-id="18780-137">Creating a schedule</span></span>
<span data-ttu-id="18780-138">Метод Put hello с расписание уникальный идентификатор toocreate новое расписание.</span><span class="sxs-lookup"><span data-stu-id="18780-138">Use hello Put method with a unique schedule ID toocreate a new schedule.</span></span>  <span data-ttu-id="18780-139">Обратите внимание, что два расписания не может иметь hello таким же Идентификатором даже если они связаны с другой, сохраненные поисковые запросы.</span><span class="sxs-lookup"><span data-stu-id="18780-139">Note that two schedules cannot have hello same ID even if they are associated with different saved searches.</span></span>  <span data-ttu-id="18780-140">При создании расписания в консоли OMS hello GUID создается для идентификатора расписания hello</span><span class="sxs-lookup"><span data-stu-id="18780-140">When you create a schedule in hello OMS console, a GUID is created for hello schedule ID.</span></span>

> [!NOTE]
> <span data-ttu-id="18780-141">Имя Hello все сохраненные поисковые запросы, отчеты и действия, созданные с помощью hello API аналитики журналов должно быть в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="18780-141">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a><span data-ttu-id="18780-142">Изменение расписания</span><span class="sxs-lookup"><span data-stu-id="18780-142">Editing a schedule</span></span>
<span data-ttu-id="18780-143">Метод Put hello с существующим расписанием идентификатор hello же сохраненный поиск toomodify, который в расписании.</span><span class="sxs-lookup"><span data-stu-id="18780-143">Use hello Put method with an existing schedule ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="18780-144">текст Hello hello запроса должен содержать etag hello hello расписания.</span><span class="sxs-lookup"><span data-stu-id="18780-144">hello body of hello request must include hello etag of hello schedule.</span></span>

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a><span data-ttu-id="18780-145">Удаление расписаний</span><span class="sxs-lookup"><span data-stu-id="18780-145">Deleting schedules</span></span>
<span data-ttu-id="18780-146">Метод Delete hello с toodelete идентификатор расписания расписания.</span><span class="sxs-lookup"><span data-stu-id="18780-146">Use hello Delete method with a schedule ID toodelete a schedule.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a><span data-ttu-id="18780-147">Действия</span><span class="sxs-lookup"><span data-stu-id="18780-147">Actions</span></span>
<span data-ttu-id="18780-148">Расписание может включать несколько действий.</span><span class="sxs-lookup"><span data-stu-id="18780-148">A schedule can have multiple actions.</span></span> <span data-ttu-id="18780-149">Действие может определять одну или несколько tooperform процессов, например отправку почты или запуск runbook, или он может определять пороговое значение, которое определяет, когда hello результатов поиска соответствующих некоторым условиям.</span><span class="sxs-lookup"><span data-stu-id="18780-149">An action may define one or more processes tooperform such as sending a mail or starting a runbook, or it may define a threshold that determines when hello results of a search match some criteria.</span></span>  <span data-ttu-id="18780-150">Некоторые действия будут определять, чтобы hello процессы выполняются при достижении порога hello.</span><span class="sxs-lookup"><span data-stu-id="18780-150">Some actions will define both so that hello processes are performed when hello threshold is met.</span></span>

<span data-ttu-id="18780-151">Все действия имеют свойства hello в hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="18780-151">All actions have hello properties in hello following table.</span></span>  <span data-ttu-id="18780-152">Разные типы оповещений имеют различные дополнительные свойства, которые описаны ниже.</span><span class="sxs-lookup"><span data-stu-id="18780-152">Different types of alerts have different additional properties which are described below.</span></span>

| <span data-ttu-id="18780-153">Свойство</span><span class="sxs-lookup"><span data-stu-id="18780-153">Property</span></span> | <span data-ttu-id="18780-154">Описание</span><span class="sxs-lookup"><span data-stu-id="18780-154">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="18780-155">Тип</span><span class="sxs-lookup"><span data-stu-id="18780-155">Type</span></span> |<span data-ttu-id="18780-156">Тип действия hello.</span><span class="sxs-lookup"><span data-stu-id="18780-156">Type of hello action.</span></span>  <span data-ttu-id="18780-157">В настоящее время hello возможные значения: предупреждение и веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="18780-157">Currently hello possible values are Alert and Webhook.</span></span> |
| <span data-ttu-id="18780-158">Имя</span><span class="sxs-lookup"><span data-stu-id="18780-158">Name</span></span> |<span data-ttu-id="18780-159">Отображаемое имя для hello предупреждения.</span><span class="sxs-lookup"><span data-stu-id="18780-159">Display name for hello alert.</span></span> |
| <span data-ttu-id="18780-160">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="18780-160">Version</span></span> |<span data-ttu-id="18780-161">Здравствуйте, используемой версии API.</span><span class="sxs-lookup"><span data-stu-id="18780-161">hello API version being used.</span></span>  <span data-ttu-id="18780-162">В настоящее время это всегда должен иметь значение too1.</span><span class="sxs-lookup"><span data-stu-id="18780-162">Currently, this should always be set too1.</span></span> |

### <a name="retrieving-actions"></a><span data-ttu-id="18780-163">Получение действий</span><span class="sxs-lookup"><span data-stu-id="18780-163">Retrieving actions</span></span>
<span data-ttu-id="18780-164">Используйте hello получить метод tooretrieve все действия для расписания.</span><span class="sxs-lookup"><span data-stu-id="18780-164">Use hello Get method tooretrieve all actions for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

<span data-ttu-id="18780-165">Используйте hello Get-метод с hello действия Идентификатором tooretrieve определенное действие для расписания.</span><span class="sxs-lookup"><span data-stu-id="18780-165">Use hello Get method with hello action ID tooretrieve a particular action for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a><span data-ttu-id="18780-166">Создание или изменение действий</span><span class="sxs-lookup"><span data-stu-id="18780-166">Creating or editing actions</span></span>
<span data-ttu-id="18780-167">Метод Put hello действия идентификатором, который является уникальным toohello расписание toocreate новое действие.</span><span class="sxs-lookup"><span data-stu-id="18780-167">Use hello Put method with an action ID that is unique toohello schedule toocreate a new action.</span></span>  <span data-ttu-id="18780-168">При создании действия в консоли OMS hello GUID является идентификатором hello действия.</span><span class="sxs-lookup"><span data-stu-id="18780-168">When you create an action in hello OMS console, a GUID is for hello action ID.</span></span>

> [!NOTE]
> <span data-ttu-id="18780-169">Имя Hello все сохраненные поисковые запросы, отчеты и действия, созданные с помощью hello API аналитики журналов должно быть в нижнем регистре.</span><span class="sxs-lookup"><span data-stu-id="18780-169">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

<span data-ttu-id="18780-170">Метод Put hello с существующие действием, идентификатор hello же сохраненный поиск toomodify, который в расписании.</span><span class="sxs-lookup"><span data-stu-id="18780-170">Use hello Put method with an existing action ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="18780-171">текст Hello hello запроса должен содержать etag hello hello расписания.</span><span class="sxs-lookup"><span data-stu-id="18780-171">hello body of hello request must include hello etag of hello schedule.</span></span>

<span data-ttu-id="18780-172">Формат запроса Hello для создания нового действия зависит от типа действия, поэтому эти образцы приведены в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="18780-172">hello request format for creating a new action varies by action type so these examples are provided in hello sections below.</span></span>

### <a name="deleting-actions"></a><span data-ttu-id="18780-173">Удаление действий</span><span class="sxs-lookup"><span data-stu-id="18780-173">Deleting actions</span></span>
<span data-ttu-id="18780-174">Метод Delete hello с hello действия Идентификатором toodelete действие.</span><span class="sxs-lookup"><span data-stu-id="18780-174">Use hello Delete method with hello action ID toodelete an action.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a><span data-ttu-id="18780-175">Действия оповещений</span><span class="sxs-lookup"><span data-stu-id="18780-175">Alert Actions</span></span>
<span data-ttu-id="18780-176">Расписание должно включать одно-единственное действие оповещения.</span><span class="sxs-lookup"><span data-stu-id="18780-176">A Schedule should have one and only one Alert action.</span></span>  <span data-ttu-id="18780-177">Оповещения имеют один или несколько разделов hello в hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="18780-177">Alert actions have one or more of hello sections in hello following table.</span></span>  <span data-ttu-id="18780-178">Они более подробно описаны далее.</span><span class="sxs-lookup"><span data-stu-id="18780-178">Each is described in further detail below.</span></span>

| <span data-ttu-id="18780-179">Раздел</span><span class="sxs-lookup"><span data-stu-id="18780-179">Section</span></span> | <span data-ttu-id="18780-180">Описание</span><span class="sxs-lookup"><span data-stu-id="18780-180">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="18780-181">Пороговое значение</span><span class="sxs-lookup"><span data-stu-id="18780-181">Threshold</span></span> |<span data-ttu-id="18780-182">Критерии, когда выполняется действие hello.</span><span class="sxs-lookup"><span data-stu-id="18780-182">Criteria for when hello action is run.</span></span> |
| <span data-ttu-id="18780-183">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="18780-183">EmailNotification</span></span> |<span data-ttu-id="18780-184">Отправьте почту toomultiple получателей.</span><span class="sxs-lookup"><span data-stu-id="18780-184">Send mail toomultiple recipients.</span></span> |
| <span data-ttu-id="18780-185">Исправление</span><span class="sxs-lookup"><span data-stu-id="18780-185">Remediation</span></span> |<span data-ttu-id="18780-186">Запуск runbook в автоматизации Azure tooattempt toocorrect обнаружить проблему.</span><span class="sxs-lookup"><span data-stu-id="18780-186">Start a runbook in Azure Automation tooattempt toocorrect identified issue.</span></span> |

#### <a name="thresholds"></a><span data-ttu-id="18780-187">Пороговые значения</span><span class="sxs-lookup"><span data-stu-id="18780-187">Thresholds</span></span>
<span data-ttu-id="18780-188">Действие оповещения должно включать одно-единственное пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="18780-188">An Alert action should have one and only one threshold.</span></span>  <span data-ttu-id="18780-189">При hello сохраненного поиска совпадения порог hello в действие, связанное с поиска, запускаются другие процессы в это действие.</span><span class="sxs-lookup"><span data-stu-id="18780-189">When hello results of a saved search match hello threshold in an action associated with that search, then any other processes in that action are run.</span></span>  <span data-ttu-id="18780-190">Действие также может содержать только пороговое значение, чтобы его можно было использовать с действиями других типов, которые не содержат пороговых значений.</span><span class="sxs-lookup"><span data-stu-id="18780-190">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span></span>

<span data-ttu-id="18780-191">Пороговые значения имеют свойства hello в hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="18780-191">Thresholds have hello properties in hello following table.</span></span>

| <span data-ttu-id="18780-192">Свойство</span><span class="sxs-lookup"><span data-stu-id="18780-192">Property</span></span> | <span data-ttu-id="18780-193">Описание</span><span class="sxs-lookup"><span data-stu-id="18780-193">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="18780-194">operator</span><span class="sxs-lookup"><span data-stu-id="18780-194">Operator</span></span> |<span data-ttu-id="18780-195">Оператор сравнения hello пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="18780-195">Operator for hello threshold comparison.</span></span> <br> <span data-ttu-id="18780-196">gt — больше</span><span class="sxs-lookup"><span data-stu-id="18780-196">gt = Greater Than</span></span> <br> <span data-ttu-id="18780-197">lt = меньше чем</span><span class="sxs-lookup"><span data-stu-id="18780-197">lt = Less Than</span></span> |
| <span data-ttu-id="18780-198">Значение</span><span class="sxs-lookup"><span data-stu-id="18780-198">Value</span></span> |<span data-ttu-id="18780-199">Значение порога hello.</span><span class="sxs-lookup"><span data-stu-id="18780-199">Value for hello threshold.</span></span> |

<span data-ttu-id="18780-200">Например, рассмотрим запрос событий с интервалом (свойство Interval) 15 минут, временным диапазоном (свойство TimeSpan) 30 минут и пороговым значением больше 10.</span><span class="sxs-lookup"><span data-stu-id="18780-200">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span></span> <span data-ttu-id="18780-201">В этом случае hello запрос будет выполняться каждые 15 минут, и будет запускаться оповещение, если возвращается 10 событий, созданные в течение определенного интервала 30 минут.</span><span class="sxs-lookup"><span data-stu-id="18780-201">In this case, hello query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30 minute span.</span></span>

<span data-ttu-id="18780-202">Ниже приведен пример ответа для действия, содержащего только пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="18780-202">Following is a sample response for an action with only a threshold.</span></span>  

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

<span data-ttu-id="18780-203">Используйте метод Put hello с уникальные действия Идентификатором toocreate новое действие пороговое значение для расписания.</span><span class="sxs-lookup"><span data-stu-id="18780-203">Use hello Put method with a unique action ID toocreate a new threshold action for a schedule.</span></span>  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

<span data-ttu-id="18780-204">Используйте метод Put hello с существующие идентификатор действия toomodify действия пороговое значение для расписания.</span><span class="sxs-lookup"><span data-stu-id="18780-204">Use hello Put method with an existing action ID toomodify a threshold action for a schedule.</span></span>  <span data-ttu-id="18780-205">текст Hello hello запроса должен содержать hello etag действие hello.</span><span class="sxs-lookup"><span data-stu-id="18780-205">hello body of hello request must include hello etag of hello action.</span></span>

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a><span data-ttu-id="18780-206">Уведомление по электронной почте</span><span class="sxs-lookup"><span data-stu-id="18780-206">Email Notification</span></span>
<span data-ttu-id="18780-207">Уведомления по электронной почте Отправить почту tooone или нескольких получателей.</span><span class="sxs-lookup"><span data-stu-id="18780-207">Email Notifications send mail tooone or more recipients.</span></span>  <span data-ttu-id="18780-208">Они включают свойства hello в hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="18780-208">They include hello properties in hello following table.</span></span>

| <span data-ttu-id="18780-209">Свойство</span><span class="sxs-lookup"><span data-stu-id="18780-209">Property</span></span> | <span data-ttu-id="18780-210">Описание</span><span class="sxs-lookup"><span data-stu-id="18780-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="18780-211">Recipients</span><span class="sxs-lookup"><span data-stu-id="18780-211">Recipients</span></span> |<span data-ttu-id="18780-212">Список адресов электронной почты.</span><span class="sxs-lookup"><span data-stu-id="18780-212">List of mail addresses.</span></span> |
| <span data-ttu-id="18780-213">Субъект</span><span class="sxs-lookup"><span data-stu-id="18780-213">Subject</span></span> |<span data-ttu-id="18780-214">Тема Hello почты hello.</span><span class="sxs-lookup"><span data-stu-id="18780-214">hello subject of hello mail.</span></span> |
| <span data-ttu-id="18780-215">Вложение</span><span class="sxs-lookup"><span data-stu-id="18780-215">Attachment</span></span> |<span data-ttu-id="18780-216">Вложения пока не поддерживаются, поэтому это свойство всегда будет иметь значение None.</span><span class="sxs-lookup"><span data-stu-id="18780-216">Attachments are not currently supported, so this will always have a value of “None”.</span></span> |

<span data-ttu-id="18780-217">Ниже приведен пример ответа для действия уведомления по электронной почте с пороговым значением.</span><span class="sxs-lookup"><span data-stu-id="18780-217">Following is a sample response for an email notification action with a threshold.</span></span>  

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
            "Subject": "This is hello subject",
            "Attachment": "None"
        },
        "Version": 1
    }

<span data-ttu-id="18780-218">Используйте метод Put hello с уникальные действия Идентификатором toocreate новое действие электронной почты для расписания.</span><span class="sxs-lookup"><span data-stu-id="18780-218">Use hello Put method with a unique action ID toocreate a new e-mail action for a schedule.</span></span>  <span data-ttu-id="18780-219">Hello следующем примере создается уведомление по электронной почте с пороговым значением, если результаты hello hello сохраненного поиска превышает порог hello отправляется сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="18780-219">hello following example creates an email notification with a threshold so hello mail is sent when hello results of hello saved search exceed hello threshold.</span></span>

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

<span data-ttu-id="18780-220">Используйте метод Put hello с существующие идентификатор действия toomodify действия электронной почты для расписания.</span><span class="sxs-lookup"><span data-stu-id="18780-220">Use hello Put method with an existing action ID toomodify an e-mail action for a schedule.</span></span>  <span data-ttu-id="18780-221">текст Hello hello запроса должен содержать hello etag действие hello.</span><span class="sxs-lookup"><span data-stu-id="18780-221">hello body of hello request must include hello etag of hello action.</span></span>

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a><span data-ttu-id="18780-222">Действия исправления</span><span class="sxs-lookup"><span data-stu-id="18780-222">Remediation actions</span></span>
<span data-ttu-id="18780-223">Исправления запустить runbook в автоматизации Azure, которую пытается выполнить toocorrect hello проблему, связанную с hello предупреждение.</span><span class="sxs-lookup"><span data-stu-id="18780-223">Remediations start a runbook in Azure Automation that attempts toocorrect hello problem identified by hello alert.</span></span>  <span data-ttu-id="18780-224">Необходимо создать веб-перехватчика для hello runbook, используемых в действие исправления и затем укажите hello URI в hello WebhookUri свойство.</span><span class="sxs-lookup"><span data-stu-id="18780-224">You must create a webhook for hello runbook used in a remediation action and then specify hello URI in hello WebhookUri property.</span></span>  <span data-ttu-id="18780-225">При создании этого действия, с помощью консоли OMS hello, для модуля runbook hello автоматически создается новое веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="18780-225">When you create this action using hello OMS console, a new webhook is automatically created for hello runbook.</span></span>

<span data-ttu-id="18780-226">Исправления включены свойства hello в hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="18780-226">Remediations include hello properties in hello following table.</span></span>

| <span data-ttu-id="18780-227">Свойство</span><span class="sxs-lookup"><span data-stu-id="18780-227">Property</span></span> | <span data-ttu-id="18780-228">Описание</span><span class="sxs-lookup"><span data-stu-id="18780-228">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="18780-229">RunbookName</span><span class="sxs-lookup"><span data-stu-id="18780-229">RunbookName</span></span> |<span data-ttu-id="18780-230">Имя hello runbook.</span><span class="sxs-lookup"><span data-stu-id="18780-230">Name of hello runbook.</span></span> <span data-ttu-id="18780-231">Оно должно совпадать опубликованного модуля runbook в автоматизации hello учетной записи, настроенной в hello решение автоматизации в рабочую область OMS.</span><span class="sxs-lookup"><span data-stu-id="18780-231">This must match a published runbook in hello automation account configured in hello Automation Solution in your OMS workspace.</span></span> |
| <span data-ttu-id="18780-232">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="18780-232">WebhookUri</span></span> |<span data-ttu-id="18780-233">URI веб-перехватчика hello.</span><span class="sxs-lookup"><span data-stu-id="18780-233">URI of hello webhook.</span></span> |
| <span data-ttu-id="18780-234">Expiry</span><span class="sxs-lookup"><span data-stu-id="18780-234">Expiry</span></span> |<span data-ttu-id="18780-235">Дата окончания срока действия Hello и время веб-перехватчика hello.</span><span class="sxs-lookup"><span data-stu-id="18780-235">hello expiration date and time of hello webhook.</span></span>  <span data-ttu-id="18780-236">Если веб-перехватчика hello не имеет срока действия, это может быть любой допустимый будущую дату.</span><span class="sxs-lookup"><span data-stu-id="18780-236">If hello webhook doesn’t have an expiration, then this can be any valid future date.</span></span> |

<span data-ttu-id="18780-237">Ниже приведен пример ответа для действия исправления с пороговым значением.</span><span class="sxs-lookup"><span data-stu-id="18780-237">Following is a sample response for a remediation action with a threshold.</span></span>

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

<span data-ttu-id="18780-238">Используйте метод Put hello с уникальным действия Идентификатором toocreate новое действие исправления для расписания.</span><span class="sxs-lookup"><span data-stu-id="18780-238">Use hello Put method with a unique action ID toocreate a new remediation action for a schedule.</span></span>  <span data-ttu-id="18780-239">Hello пример создает исправление с пороговым значением, hello runbook запускается в том случае, если результаты hello hello сохраненного поиска превышает порог hello.</span><span class="sxs-lookup"><span data-stu-id="18780-239">hello following example creates a remediation with a threshold so hello runbook is started when hello results of hello saved search exceed hello threshold.</span></span>

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

<span data-ttu-id="18780-240">Используйте метод Put hello с существующие toomodify идентификатор действия действие исправления для расписания.</span><span class="sxs-lookup"><span data-stu-id="18780-240">Use hello Put method with an existing action ID toomodify a remediation action for a schedule.</span></span>  <span data-ttu-id="18780-241">текст Hello hello запроса должен содержать hello etag действие hello.</span><span class="sxs-lookup"><span data-stu-id="18780-241">hello body of hello request must include hello etag of hello action.</span></span>

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a><span data-ttu-id="18780-242">Пример</span><span class="sxs-lookup"><span data-stu-id="18780-242">Example</span></span>
<span data-ttu-id="18780-243">Ниже приведен полный пример toocreate новое оповещение по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="18780-243">Following is a complete example toocreate a new email alert.</span></span>  <span data-ttu-id="18780-244">Создается новое расписание, а также действие, содержащее пороговое значение и сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="18780-244">This creates a new schedule along with an action containing a threshold and email.</span></span>

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a><span data-ttu-id="18780-245">Действия webhook</span><span class="sxs-lookup"><span data-stu-id="18780-245">Webhook actions</span></span>
<span data-ttu-id="18780-246">Действия веб-перехватчика запустить процесс путем вызова URL-адрес и Дополнительно может предоставлять полезные данные toobe отправлено.</span><span class="sxs-lookup"><span data-stu-id="18780-246">Webhook actions start a process by calling a URL and optionally providing a payload toobe sent.</span></span>  <span data-ttu-id="18780-247">Они являются подобные действия tooRemediation, за исключением того, они предназначены для веб-перехватчиков, который может вызывать процессами, отличными от Runbook автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="18780-247">They are similar tooRemediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span>  <span data-ttu-id="18780-248">Они также предоставляют hello дополнительную возможность предоставления удаленных процессов toohello toobe доставляется полезных данных.</span><span class="sxs-lookup"><span data-stu-id="18780-248">They also provide hello additional option of providing a payload toobe delivered toohello remote process.</span></span>

<span data-ttu-id="18780-249">Действия веб-перехватчика нет порогового значения, но вместо этого следует добавить tooa расписание, которое имеет действие по оповещению с пороговым значением.</span><span class="sxs-lookup"><span data-stu-id="18780-249">Webhook actions do not have a threshold but instead should be added tooa schedule that has an Alert action with a threshold.</span></span>  <span data-ttu-id="18780-250">Можно добавить несколько действий веб-перехватчика, все выполняемые при достижении порога hello.</span><span class="sxs-lookup"><span data-stu-id="18780-250">You can add multiple Webhook actions that will all be run when hello threshold is met.</span></span>

<span data-ttu-id="18780-251">Веб-перехватчика действия включают свойства hello в hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="18780-251">Webhook actions include hello properties in hello following table.</span></span>

| <span data-ttu-id="18780-252">Свойство</span><span class="sxs-lookup"><span data-stu-id="18780-252">Property</span></span> | <span data-ttu-id="18780-253">Описание</span><span class="sxs-lookup"><span data-stu-id="18780-253">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="18780-254">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="18780-254">WebhookUri</span></span> |<span data-ttu-id="18780-255">Тема Hello почты hello.</span><span class="sxs-lookup"><span data-stu-id="18780-255">hello subject of hello mail.</span></span> |
| <span data-ttu-id="18780-256">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="18780-256">CustomPayload</span></span> |<span data-ttu-id="18780-257">Настраиваемые полезные данные отправлены toobe toohello веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="18780-257">Custom payload toobe sent toohello webhook.</span></span>  <span data-ttu-id="18780-258">Формат Hello будет зависеть от ожидается какой веб-перехватчика hello.</span><span class="sxs-lookup"><span data-stu-id="18780-258">hello format will depend on what hello webhook is expecting.</span></span> |

<span data-ttu-id="18780-259">Ниже приведен пример ответа для действия webhook и соответствующее действие оповещения с пороговым значением.</span><span class="sxs-lookup"><span data-stu-id="18780-259">Following is a sample response for webhook action and an associated alert action with a threshold.</span></span>

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

#### <a name="create-or-edit-a-webhook-action"></a><span data-ttu-id="18780-260">Создание или изменение действий webhook</span><span class="sxs-lookup"><span data-stu-id="18780-260">Create or edit a webhook action</span></span>
<span data-ttu-id="18780-261">Используйте метод Put hello с уникальные действия Идентификатором toocreate новое действие веб-перехватчика для расписания.</span><span class="sxs-lookup"><span data-stu-id="18780-261">Use hello Put method with a unique action ID toocreate a new webhook action for a schedule.</span></span>  <span data-ttu-id="18780-262">Hello следующем примере создается действие веб-перехватчика или предупреждений с пороговым значением, чтобы веб-перехватчика hello будут создаваться при hello результаты hello сохраненного поиска превышает порог hello.</span><span class="sxs-lookup"><span data-stu-id="18780-262">hello following example creates a Webhook action and an Alert action with a threshold so that hello webhook will be triggered when hello results of hello saved search exceed hello threshold.</span></span>

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

<span data-ttu-id="18780-263">Используйте метод Put hello с существующие идентификатор действия toomodify действия веб-перехватчика для расписания.</span><span class="sxs-lookup"><span data-stu-id="18780-263">Use hello Put method with an existing action ID toomodify a webhook action for a schedule.</span></span>  <span data-ttu-id="18780-264">текст Hello hello запроса должен содержать hello etag действие hello.</span><span class="sxs-lookup"><span data-stu-id="18780-264">hello body of hello request must include hello etag of hello action.</span></span>

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a><span data-ttu-id="18780-265">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="18780-265">Next steps</span></span>
* <span data-ttu-id="18780-266">Используйте hello [REST API поиска журналов tooperform](log-analytics-log-search-api.md) в службе анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="18780-266">Use hello [REST API tooperform log searches](log-analytics-log-search-api.md) in Log Analytics.</span></span>

