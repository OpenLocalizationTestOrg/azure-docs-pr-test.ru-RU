---
title: "Основные понятия, терминология и иерархия сущностей планировщика | Документация Майкрософт"
description: "Основные понятия, терминология и иерархия сущностей планировщика, включая задания и коллекции заданий.  Подробный пример запланированного задания."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 3ef16fab-d18a-48ba-8e56-3f3e0a1bcb92
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 0f035b58ccd140a5481703df7e184206da2ed651
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a><span data-ttu-id="7e8c8-104">Основные понятия, терминология и иерархия сущностей планировщика</span><span class="sxs-lookup"><span data-stu-id="7e8c8-104">Scheduler concepts, terminology, + entity hierarchy</span></span>
## <a name="scheduler-entity-hierarchy"></a><span data-ttu-id="7e8c8-105">Иерархия сущностей планировщика</span><span class="sxs-lookup"><span data-stu-id="7e8c8-105">Scheduler entity hierarchy</span></span>
<span data-ttu-id="7e8c8-106">В приведенной ниже таблице описаны основные ресурсы, которые предоставляет или использует API планировщика.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-106">The following table describes the main resources exposed or used by the Scheduler API:</span></span>

| <span data-ttu-id="7e8c8-107">Ресурс</span><span class="sxs-lookup"><span data-stu-id="7e8c8-107">Resource</span></span> | <span data-ttu-id="7e8c8-108">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="7e8c8-108">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7e8c8-109">**Коллекция заданий**</span><span class="sxs-lookup"><span data-stu-id="7e8c8-109">**Job collection**</span></span> |<span data-ttu-id="7e8c8-110">Коллекция заданий содержит группу заданий, а также параметры, квоты и регулирования, которые являются общими для заданий в этой коллекции.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-110">A job collection contains a group of jobs and maintains settings, quotas, and throttles that are shared by jobs within the collection.</span></span> <span data-ttu-id="7e8c8-111">Коллекция заданий создается владельцем подписки и объединяет задания по областям использования или границам приложений.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-111">A job collection is created by a subscription owner and groups jobs together based on usage or application boundaries.</span></span> <span data-ttu-id="7e8c8-112">Коллекция ограничивается одним регионом.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-112">It’s constrained to one region.</span></span> <span data-ttu-id="7e8c8-113">Позволяет также применять квоты (MaxJobs и MaxRecurrence) для ограничения использования всех входящих</span><span class="sxs-lookup"><span data-stu-id="7e8c8-113">It also allows the enforcement of quotas to constrain the usage of all jobs in that collection.</span></span> <span data-ttu-id="7e8c8-114">в коллекцию заданий.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-114">The quotas include MaxJobs and MaxRecurrence.</span></span> |
| <span data-ttu-id="7e8c8-115">**Задание.**</span><span class="sxs-lookup"><span data-stu-id="7e8c8-115">**Job**</span></span> |<span data-ttu-id="7e8c8-116">Задание определяет одно повторяющееся действие с простой или сложной стратегией выполнения.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-116">A job defines a single recurrent action, with simple or complex strategies for execution.</span></span> <span data-ttu-id="7e8c8-117">К действиям относятся HTTP-запросы, запросы к очереди хранилища, запросы к очереди служебной шины и запросы к разделу служебной шины.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-117">Actions may include HTTP, storage queue, service bus queue, or service bus topic requests.</span></span> |
| <span data-ttu-id="7e8c8-118">**Журнал заданий**</span><span class="sxs-lookup"><span data-stu-id="7e8c8-118">**Job history**</span></span> |<span data-ttu-id="7e8c8-119">Журнал заданий содержит подробные сведения о выполнении заданий.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-119">A job history represents details for an execution of a job.</span></span> <span data-ttu-id="7e8c8-120">В нем указывается, было ли задание выполнено, а также все данные ответов.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-120">It contains success vs. failure, as well as any response details.</span></span> |

## <a name="scheduler-entity-management"></a><span data-ttu-id="7e8c8-121">Управление сущностями планировщика</span><span class="sxs-lookup"><span data-stu-id="7e8c8-121">Scheduler entity management</span></span>
<span data-ttu-id="7e8c8-122">На высоком уровне планировщик и API управления службами позволяют выполнять с ресурсами следующие операции.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-122">At a high level, the scheduler and the service management API expose the following operations on the resources:</span></span>

| <span data-ttu-id="7e8c8-123">Функция</span><span class="sxs-lookup"><span data-stu-id="7e8c8-123">Capability</span></span> | <span data-ttu-id="7e8c8-124">Описание и URI-адрес</span><span class="sxs-lookup"><span data-stu-id="7e8c8-124">Description and URI address</span></span> |
| --- | --- |
| <span data-ttu-id="7e8c8-125">**Управление коллекциями заданий**</span><span class="sxs-lookup"><span data-stu-id="7e8c8-125">**Job collection management**</span></span> |<span data-ttu-id="7e8c8-126">Поддержка запросов GET, PUT и DELETE для создания и изменения коллекций и содержащихся в них заданий.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-126">GET, PUT, and DELETE support for creating and modifying job collections and the jobs contained therein.</span></span> <span data-ttu-id="7e8c8-127">Коллекция заданий — это контейнер для заданий, который сопоставляется с квотами и общими настройками.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-127">A job collection is a container for jobs and maps to quotas and shared settings.</span></span> <span data-ttu-id="7e8c8-128">В качестве примеров квот (которые подробно описаны ниже) можно привести максимальное число заданий и наименьший интервал повторения.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-128">Examples of quotas, described later, are maximum number of jobs and smallest recurrence interval.</span></span> <p><span data-ttu-id="7e8c8-129">PUT и DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="7e8c8-129">PUT and DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p><p><span data-ttu-id="7e8c8-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="7e8c8-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p> |
| <span data-ttu-id="7e8c8-131">**Управление заданиями**</span><span class="sxs-lookup"><span data-stu-id="7e8c8-131">**Job management**</span></span> |<span data-ttu-id="7e8c8-132">Поддержка запросов GET, PUT, POST, PATCH и DELETE для создания и изменения облачных заданий.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-132">GET, PUT, POST, PATCH, and DELETE support for creating and modifying jobs.</span></span> <span data-ttu-id="7e8c8-133">Все задания должны входить в уже существующую коллекцию, поэтому имплицитное создание коллекций не предусмотрено.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-133">All jobs must belong to a job collection that already exists, so there is no implicit creation.</span></span> <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| <span data-ttu-id="7e8c8-134">**Управление журналами заданий**</span><span class="sxs-lookup"><span data-stu-id="7e8c8-134">**Job history management**</span></span> |<span data-ttu-id="7e8c8-135">Поддержка запроса GET для извлечения журнала заданий за последние 60 дней с указанием времени и результатов выполнения.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-135">GET support for fetching 60 days of job execution history, such as job elapsed time and job execution results.</span></span> <span data-ttu-id="7e8c8-136">Добавляет поддержку строкового параметра запроса для фильтрации результатов по состоянию и статусу.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-136">Adds query string parameter support for filtering based on state and status.</span></span> <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a><span data-ttu-id="7e8c8-137">Типы заданий</span><span class="sxs-lookup"><span data-stu-id="7e8c8-137">Job types</span></span>
<span data-ttu-id="7e8c8-138">Существует несколько типов заданий: задания HTTP (включая задания HTTPS, поддерживающие протокол SSL), задания очереди хранилища, задания очереди служебной шины и задания раздела служебной шины.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-138">There are multiple types of jobs: HTTP jobs (including HTTPS jobs that support SSL), storage queue jobs, service bus queue jobs, and service bus topic jobs.</span></span> <span data-ttu-id="7e8c8-139">Задания HTTP применяются, если у вас есть конечная точка существующей рабочей нагрузки или службы.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-139">HTTP jobs are ideal if you have an endpoint of an existing workload or service.</span></span> <span data-ttu-id="7e8c8-140">С помощью заданий очереди хранилища сообщения можно помещать в очереди хранилища, а значит, подходят для рабочих нагрузок, использующих очереди хранилища.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-140">You can use storage queue jobs to post messages to storage queues, so those jobs are ideal for workloads that use storage queues.</span></span> <span data-ttu-id="7e8c8-141">Аналогичным образом задания служебной шины идеально подходят для рабочих нагрузок, использующих очереди и разделы служебной шины.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-141">Similarly, service bus jobs are ideal for workloads that use service bus queues and topics.</span></span>

## <a name="the-job-entity-in-detail"></a><span data-ttu-id="7e8c8-142">Сущность задания в деталях</span><span class="sxs-lookup"><span data-stu-id="7e8c8-142">The "job" entity in detail</span></span>
<span data-ttu-id="7e8c8-143">На базовом уровне запланированное задание состоит из нескольких частей.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-143">At a basic level, a scheduled job has several parts:</span></span>

* <span data-ttu-id="7e8c8-144">Действие, выполняемое при срабатывании таймера задания.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-144">The action to perform when the job timer fires</span></span>  
* <span data-ttu-id="7e8c8-145">(Необязательно.) Время выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-145">(Optional) The time to run the job</span></span>  
* <span data-ttu-id="7e8c8-146">(Необязательно.) Время и периодичность повторного выполнения.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-146">(Optional) When and how often to repeat the job</span></span>  
* <span data-ttu-id="7e8c8-147">(Необязательно.) Действие, выполняемое в случае невыполнения первичного действия.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-147">(Optional) An action to fire if the primary action fails</span></span>  

<span data-ttu-id="7e8c8-148">На внутреннем уровне запланированное задание содержит также системные данные, такие как следующее запланированное время выполнения.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-148">Internally, a scheduled job also contains system-provided data such as the next scheduled execution time.</span></span>

<span data-ttu-id="7e8c8-149">В следующем коде приведен подробный пример запланированного задания.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-149">The following code provides a comprehensive example of a scheduled job.</span></span> <span data-ttu-id="7e8c8-150">Подробности см. в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-150">Details are provided in subsequent sections.</span></span>

    {
        "startTime": "2012-08-04T00:00Z",               // optional
        "action":
        {
            "type": "http",
            "retryPolicy": { "retryType":"none" },
            "request":
            {
                "uri": "http://contoso.com/foo",        // required
                "method": "PUT",                        // required
                "body": "Posting from a timer",         // optional
                "headers":                              // optional

                {
                    "Content-Type": "application/json"
                },
            },
           "errorAction":
           {
               "type": "http",
               "request":
               {
                   "uri": "http://contoso.com/notifyError",
                   "method": "POST",
               },
           },
        },
        "recurrence":                                   // optional
        {
            "frequency": "week",                        // can be "year" "month" "day" "week" "minute"
            "interval": 1,                              // optional, how often to fire (default to 1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default to recur infinitely)
            "endTime": "2012-11-04",                     // optional (default to recur infinitely)
        },
        "state": "disabled",                           // enabled or disabled
        "status":                                       // controlled by Scheduler service
        {
            "lastExecutionTime": "2007-03-01T13:00:00Z",
            "nextExecutionTime": "2007-03-01T14:00:00Z ",
            "executionCount": 3,
                                                "failureCount": 0,
                                                "faultedCount": 0
        },
    }

<span data-ttu-id="7e8c8-151">Как видно из приведенного выше примера запланированного задания, определение задания состоит из нескольких частей.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-151">As seen in the sample scheduled job above, a job definition has several parts:</span></span>

* <span data-ttu-id="7e8c8-152">Время начала (startTime).</span><span class="sxs-lookup"><span data-stu-id="7e8c8-152">Start time (“startTime”)</span></span>  
* <span data-ttu-id="7e8c8-153">Действие (action), которое включает действие ошибки (errorAction).</span><span class="sxs-lookup"><span data-stu-id="7e8c8-153">Action (“action”), which includes error action (“errorAction”)</span></span>
* <span data-ttu-id="7e8c8-154">Повторение (recurrence).</span><span class="sxs-lookup"><span data-stu-id="7e8c8-154">Recurrence (“recurrence”)</span></span>  
* <span data-ttu-id="7e8c8-155">Состояние (state).</span><span class="sxs-lookup"><span data-stu-id="7e8c8-155">State (“state”)</span></span>  
* <span data-ttu-id="7e8c8-156">Статус (status).</span><span class="sxs-lookup"><span data-stu-id="7e8c8-156">Status (“status”)</span></span>  
* <span data-ttu-id="7e8c8-157">Политика повтора (retryPolicy).</span><span class="sxs-lookup"><span data-stu-id="7e8c8-157">Retry policy (“retryPolicy”)</span></span>  

<span data-ttu-id="7e8c8-158">Рассмотрим каждую часть подробно.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-158">Let’s examine each of these in detail:</span></span>

## <a name="starttime"></a><span data-ttu-id="7e8c8-159">startTime</span><span class="sxs-lookup"><span data-stu-id="7e8c8-159">startTime</span></span>
<span data-ttu-id="7e8c8-160">startTime — это время начала, которое позволяет вызывающему объекту указать смещение часового пояса в сети в [формате ISO-8601](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="7e8c8-160">The "startTime” is the start time and allows the caller to specify a time zone offset on the wire in [ISO-8601 format](http://en.wikipedia.org/wiki/ISO_8601).</span></span>

## <a name="action-and-erroraction"></a><span data-ttu-id="7e8c8-161">action и errorAction</span><span class="sxs-lookup"><span data-stu-id="7e8c8-161">action and errorAction</span></span>
<span data-ttu-id="7e8c8-162">action — это действие, вызываемое при каждом выполнении задания и описывающее тип вызова службы.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-162">The “action” is the action invoked on each occurrence and describes a type of service invocation.</span></span> <span data-ttu-id="7e8c8-163">action — это действие, которое будет выполняться по указанному расписанию.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-163">The action is what will be executed on the provided schedule.</span></span> <span data-ttu-id="7e8c8-164">Планировщик поддерживает действия, связанные с HTTP, очередью хранилища, разделом служебной шины и очередью служебной шины.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-164">Scheduler supports HTTP, storage queue, service bus topic, and service bus queue actions.</span></span>

<span data-ttu-id="7e8c8-165">В приведенном выше примере используется действие HTTP.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-165">The action in the example above is an HTTP action.</span></span> <span data-ttu-id="7e8c8-166">Ниже приведен пример с действием очереди хранилища.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-166">Below is an example of a storage queue action:</span></span>

    {
            "type": "storageQueue",
            "queueMessage":
            {
                "storageAccount": "myStorageAccount",  // required
                "queueName": "myqueue",                // required
                "sasToken": "TOKEN",                   // required
                "message":                             // required
                    "My message body",
            },
    }

<span data-ttu-id="7e8c8-167">Ниже приведен пример действия раздела служебной шины.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-167">Below is an example of a service bus topic action.</span></span>

  <span data-ttu-id="7e8c8-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span><span class="sxs-lookup"><span data-stu-id="7e8c8-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span></span>  
      <span data-ttu-id="7e8c8-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Может быть netMessaging или AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Сообщение", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span><span class="sxs-lookup"><span data-stu-id="7e8c8-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span></span>

<span data-ttu-id="7e8c8-170">Ниже приведен пример действия очереди служебной шины.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-170">Below is an example of a service bus queue action:</span></span>

  <span data-ttu-id="7e8c8-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span><span class="sxs-lookup"><span data-stu-id="7e8c8-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span></span>  
      <span data-ttu-id="7e8c8-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Может быть netMessaging или AMQP "authentication": {</span><span class="sxs-lookup"><span data-stu-id="7e8c8-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span></span>  
        <span data-ttu-id="7e8c8-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Сообщение",</span><span class="sxs-lookup"><span data-stu-id="7e8c8-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span></span>  
      <span data-ttu-id="7e8c8-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span><span class="sxs-lookup"><span data-stu-id="7e8c8-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span></span>

<span data-ttu-id="7e8c8-175">errorAction ― это обработчик ошибок, действие, которое вызывается при невыполнении основного действия.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-175">The “errorAction” is the error handler, the action invoked when the primary action fails.</span></span> <span data-ttu-id="7e8c8-176">Данная переменная позволяет вызвать конечную точку обработки ошибок или отправить пользователю уведомление.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-176">You can use this variable to call an error-handling endpoint or send a user notification.</span></span> <span data-ttu-id="7e8c8-177">Это можно использовать для того, чтобы достигнуть дополнительной конечной точки, если основная недоступна (например, при аварии на сайте конечной точки), или оповестить конечную точку обработки ошибок.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-177">This can be used for reaching a secondary endpoint in the case that the primary is not available (e.g., in the case of a disaster at the endpoint’s site) or can be used for notifying an error handling endpoint.</span></span> <span data-ttu-id="7e8c8-178">Аналогично основному действию, переменная errorAction может содержать как простой, так и сложный алгоритм в зависимости от других действий.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-178">Just like the primary action, the error action can be simple or composite logic based on other actions.</span></span> <span data-ttu-id="7e8c8-179">Инструкции по созданию маркера SAS см. в статье о [создании и использовании подписанного URL-адреса](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="7e8c8-179">To learn how to create a SAS token, refer to [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="recurrence"></a><span data-ttu-id="7e8c8-180">recurrence</span><span class="sxs-lookup"><span data-stu-id="7e8c8-180">recurrence</span></span>
<span data-ttu-id="7e8c8-181">Параметр recurrence состоит из нескольких частей.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-181">Recurrence has several parts:</span></span>

* <span data-ttu-id="7e8c8-182">Частота (frequency): минута, час, день, неделя, месяц или год.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-182">Frequency: One of minute, hour, day, week, month, year</span></span>  
* <span data-ttu-id="7e8c8-183">Интервал (interval): количество повторений с указанной частотой.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-183">Interval: Interval at the given frequency for the recurrence</span></span>  
* <span data-ttu-id="7e8c8-184">Предписанное расписание (schedule): минуты, часы, дни недели, месяцы и числа месяца, в которые будет выполняться повторение.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-184">Prescribed schedule: Specify minutes, hours, weekdays, months, and monthdays of the recurrence</span></span>  
* <span data-ttu-id="7e8c8-185">Количество (count): число повторений.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-185">Count: Count of occurrences</span></span>  
* <span data-ttu-id="7e8c8-186">Время окончания (endTime): время, после которого задания выполняться не будут.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-186">End time: No jobs will execute after the specified end time</span></span>  

<span data-ttu-id="7e8c8-187">Задание повторяется, если его определение JSON включает объект повторения.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-187">A job is recurring if it has a recurring object specified in its JSON definition.</span></span> <span data-ttu-id="7e8c8-188">Если указаны параметры count и endTime, приоритет отдается условию завершения, которое выполняется первым.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-188">If both count and endTime are specified, the completion rule that occurs first is honored.</span></span>

## <a name="state"></a><span data-ttu-id="7e8c8-189">state</span><span class="sxs-lookup"><span data-stu-id="7e8c8-189">state</span></span>
<span data-ttu-id="7e8c8-190">Состояние задания может иметь одно из четырех значений: "включено", "отключено", "завершено" или "неисправно".</span><span class="sxs-lookup"><span data-stu-id="7e8c8-190">The state of the job is one of four values: enabled, disabled, completed, or faulted.</span></span> <span data-ttu-id="7e8c8-191">Для перевода заданий в состояние "включено" или "отключено" можно использовать задания PUT и PATCH.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-191">You can PUT or PATCH jobs so as to update them to the enabled or disabled state.</span></span> <span data-ttu-id="7e8c8-192">Если задание завершено или неисправно, обновить его итоговое состояние нельзя (однако, задание может быть УДАЛЕНО).</span><span class="sxs-lookup"><span data-stu-id="7e8c8-192">If a job has been completed or faulted, that is a final state that cannot be updated (though the job can still be DELETED).</span></span> <span data-ttu-id="7e8c8-193">Пример свойства state выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7e8c8-193">An example of the state property is as follows:</span></span>

        "state": "disabled", // enabled, disabled, completed, or faulted
<span data-ttu-id="7e8c8-194">Завершенные и неисправные задания удаляются через 60 дней.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-194">Completed and faulted jobs are deleted after 60 days.</span></span>

## <a name="status"></a><span data-ttu-id="7e8c8-195">status</span><span class="sxs-lookup"><span data-stu-id="7e8c8-195">status</span></span>
<span data-ttu-id="7e8c8-196">После запуска задания планировщик возвращает информацию о текущем статусе его выполнения.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-196">Once a Scheduler job has started, information will be returned about the current status of the job.</span></span> <span data-ttu-id="7e8c8-197">Пользователь не может настраивать этот объект — его задает система.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-197">This object is not settable by the user—it’s set by the system.</span></span> <span data-ttu-id="7e8c8-198">При этом он включается в объект задания (а не является отдельным связанным ресурсом), что позволяет легко узнавать статус задания.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-198">However, it is included in the job object (rather than a separate linked resource) so that one can obtain the status of a job easily.</span></span>

<span data-ttu-id="7e8c8-199">Статус задания содержит время предыдущего выполнения (если задание уже выполнялось), время следующего запланированного выполнения (для незавершенных заданий) и количество выполнений.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-199">Job status includes the time of the previous execution (if any), the time of the next scheduled execution (for in-progress jobs), and the execution count of the job.</span></span>

## <a name="retrypolicy"></a><span data-ttu-id="7e8c8-200">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="7e8c8-200">retryPolicy</span></span>
<span data-ttu-id="7e8c8-201">Если задание планировщика выполнить не удается, можно настроить политику повтора, указав условия и порядок повторного выполнения действия.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-201">If a Scheduler job fails, it is possible to specify a retry policy to determine whether and how the action is retried.</span></span> <span data-ttu-id="7e8c8-202">Политика повтора определяется объектом **retryType** — если она не установлена, данный объект имеет значение **none**, как показано выше.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-202">This is determined by the **retryType** object—it is set to **none** if there is no retry policy, as shown above.</span></span> <span data-ttu-id="7e8c8-203">Если политика повтора имеется, установите значение **fixed** .</span><span class="sxs-lookup"><span data-stu-id="7e8c8-203">Set it to **fixed** if there is a retry policy.</span></span>

<span data-ttu-id="7e8c8-204">Для настройки политики повторных попыток можно указать два дополнительных параметра: интервал повтора (**retryInterval**) и число повторов (**retryCount**).</span><span class="sxs-lookup"><span data-stu-id="7e8c8-204">To set a retry policy, two additional settings may be specified: a retry interval (**retryInterval**) and the number of retries (**retryCount**).</span></span>

<span data-ttu-id="7e8c8-205">Интервал повтора, определяемый объектом **retryInterval** , представляет собой промежуток времени между повторными попытками.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-205">The retry interval, specified with the **retryInterval** object, is the interval between retries.</span></span> <span data-ttu-id="7e8c8-206">Значение по умолчанию составляет 30 секунд, минимальное настраиваемое значение — 15 секунд, а максимальное — 18 месяцев.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-206">Its default value is 30 seconds, its minimum configurable value is 15 seconds, and its maximum value is 18 months.</span></span> <span data-ttu-id="7e8c8-207">Для заданий в бесплатных коллекциях минимальное настраиваемое значение составляет 1 час.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-207">Jobs in Free job collections have a minimum configurable value of 1 hour.</span></span>  <span data-ttu-id="7e8c8-208">Значение устанавливается в формате ISO-8601.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-208">It is defined in the ISO 8601 format.</span></span> <span data-ttu-id="7e8c8-209">Число повторов определяется объектом **retryCount** и представляет собой количество предпринимаемых повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-209">Similarly, the value of the number of retries is specified with the **retryCount** object; it is the number of times a retry is attempted.</span></span> <span data-ttu-id="7e8c8-210">Значение по умолчанию равно 4, а максимальное значение — 20\.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-210">Its default value is 4, and its maximum value is 20\.</span></span> <span data-ttu-id="7e8c8-211">Оба **retryInterval** и **retryCount** являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-211">Both **retryInterval** and **retryCount** are optional.</span></span> <span data-ttu-id="7e8c8-212">Они получают свои значения по умолчанию, если объекту **retryType** присваивается значение **fixed** и никакие другие значения явно не задаются.</span><span class="sxs-lookup"><span data-stu-id="7e8c8-212">They are given their default values if **retryType** is set to **fixed** and no values are specified explicitly.</span></span>

## <a name="see-also"></a><span data-ttu-id="7e8c8-213">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="7e8c8-213">See also</span></span>
 [<span data-ttu-id="7e8c8-214">Что такое планировщик?</span><span class="sxs-lookup"><span data-stu-id="7e8c8-214">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="7e8c8-215">Приступая к работе с планировщиком Azure на портале Azure</span><span class="sxs-lookup"><span data-stu-id="7e8c8-215">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="7e8c8-216">Планы и выставление счетов в планировщике Azure</span><span class="sxs-lookup"><span data-stu-id="7e8c8-216">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="7e8c8-217">Как создавать сложные расписания и расширенное повторение с помощью планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="7e8c8-217">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="7e8c8-218">Справочник по API REST планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="7e8c8-218">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="7e8c8-219">Справочник по командлетам PowerShell планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="7e8c8-219">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="7e8c8-220">Высокая доступность и надежность планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="7e8c8-220">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="7e8c8-221">Ограничения, значения по умолчанию и коды ошибок планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="7e8c8-221">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="7e8c8-222">Исходящая аутентификация планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="7e8c8-222">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

