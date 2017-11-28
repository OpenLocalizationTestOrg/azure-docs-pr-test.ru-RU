---
title: "aaaScheduler сущностей, основные понятия и термины | Документы Microsoft"
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
ms.openlocfilehash: 73e7de7bfd2937e401aeab05e0e10fa292cf37b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a><span data-ttu-id="a4c4f-104">Основные понятия, терминология и иерархия сущностей планировщика</span><span class="sxs-lookup"><span data-stu-id="a4c4f-104">Scheduler concepts, terminology, + entity hierarchy</span></span>
## <a name="scheduler-entity-hierarchy"></a><span data-ttu-id="a4c4f-105">Иерархия сущностей планировщика</span><span class="sxs-lookup"><span data-stu-id="a4c4f-105">Scheduler entity hierarchy</span></span>
<span data-ttu-id="a4c4f-106">Hello следующей таблице описаны основные ресурсы hello предоставляемые или используемые API планировщика hello.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-106">hello following table describes hello main resources exposed or used by hello Scheduler API:</span></span>

| <span data-ttu-id="a4c4f-107">Ресурс</span><span class="sxs-lookup"><span data-stu-id="a4c4f-107">Resource</span></span> | <span data-ttu-id="a4c4f-108">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="a4c4f-108">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a4c4f-109">**Коллекция заданий**</span><span class="sxs-lookup"><span data-stu-id="a4c4f-109">**Job collection**</span></span> |<span data-ttu-id="a4c4f-110">Коллекция заданий содержит группу заданий и сохраняет параметры, квоты и регулирования, которые являются общими для задания в коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-110">A job collection contains a group of jobs and maintains settings, quotas, and throttles that are shared by jobs within hello collection.</span></span> <span data-ttu-id="a4c4f-111">Коллекция заданий создается владельцем подписки и объединяет задания по областям использования или границам приложений.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-111">A job collection is created by a subscription owner and groups jobs together based on usage or application boundaries.</span></span> <span data-ttu-id="a4c4f-112">Это ограниченное tooone области.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-112">It’s constrained tooone region.</span></span> <span data-ttu-id="a4c4f-113">Она также позволяет hello принудительного применения квот использования hello tooconstrain всех заданий в этой коллекции.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-113">It also allows hello enforcement of quotas tooconstrain hello usage of all jobs in that collection.</span></span> <span data-ttu-id="a4c4f-114">Hello квот входят MaxJobs и MaxRecurrence.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-114">hello quotas include MaxJobs and MaxRecurrence.</span></span> |
| <span data-ttu-id="a4c4f-115">**Задание.**</span><span class="sxs-lookup"><span data-stu-id="a4c4f-115">**Job**</span></span> |<span data-ttu-id="a4c4f-116">Задание определяет одно повторяющееся действие с простой или сложной стратегией выполнения.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-116">A job defines a single recurrent action, with simple or complex strategies for execution.</span></span> <span data-ttu-id="a4c4f-117">К действиям относятся HTTP-запросы, запросы к очереди хранилища, запросы к очереди служебной шины и запросы к разделу служебной шины.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-117">Actions may include HTTP, storage queue, service bus queue, or service bus topic requests.</span></span> |
| <span data-ttu-id="a4c4f-118">**Журнал заданий**</span><span class="sxs-lookup"><span data-stu-id="a4c4f-118">**Job history**</span></span> |<span data-ttu-id="a4c4f-119">Журнал заданий содержит подробные сведения о выполнении заданий.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-119">A job history represents details for an execution of a job.</span></span> <span data-ttu-id="a4c4f-120">В нем указывается, было ли задание выполнено, а также все данные ответов.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-120">It contains success vs. failure, as well as any response details.</span></span> |

## <a name="scheduler-entity-management"></a><span data-ttu-id="a4c4f-121">Управление сущностями планировщика</span><span class="sxs-lookup"><span data-stu-id="a4c4f-121">Scheduler entity management</span></span>
<span data-ttu-id="a4c4f-122">На высоком уровне планировщик hello и API управления службами hello предоставляют следующие операции с ресурсами hello hello:</span><span class="sxs-lookup"><span data-stu-id="a4c4f-122">At a high level, hello scheduler and hello service management API expose hello following operations on hello resources:</span></span>

| <span data-ttu-id="a4c4f-123">Функция</span><span class="sxs-lookup"><span data-stu-id="a4c4f-123">Capability</span></span> | <span data-ttu-id="a4c4f-124">Описание и URI-адрес</span><span class="sxs-lookup"><span data-stu-id="a4c4f-124">Description and URI address</span></span> |
| --- | --- |
| <span data-ttu-id="a4c4f-125">**Управление коллекциями заданий**</span><span class="sxs-lookup"><span data-stu-id="a4c4f-125">**Job collection management**</span></span> |<span data-ttu-id="a4c4f-126">GET, PUT и DELETE поддержку для создания и изменения коллекций заданий и заданий hello, содержащийся в ней.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-126">GET, PUT, and DELETE support for creating and modifying job collections and hello jobs contained therein.</span></span> <span data-ttu-id="a4c4f-127">Коллекция заданий — это контейнер для заданий и сопоставляет tooquotas и общих настроек.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-127">A job collection is a container for jobs and maps tooquotas and shared settings.</span></span> <span data-ttu-id="a4c4f-128">В качестве примеров квот (которые подробно описаны ниже) можно привести максимальное число заданий и наименьший интервал повторения.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-128">Examples of quotas, described later, are maximum number of jobs and smallest recurrence interval.</span></span> <p><span data-ttu-id="a4c4f-129">PUT и DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="a4c4f-129">PUT and DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p><p><span data-ttu-id="a4c4f-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span><span class="sxs-lookup"><span data-stu-id="a4c4f-130">GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</span></span></p> |
| <span data-ttu-id="a4c4f-131">**Управление заданиями**</span><span class="sxs-lookup"><span data-stu-id="a4c4f-131">**Job management**</span></span> |<span data-ttu-id="a4c4f-132">Поддержка запросов GET, PUT, POST, PATCH и DELETE для создания и изменения облачных заданий.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-132">GET, PUT, POST, PATCH, and DELETE support for creating and modifying jobs.</span></span> <span data-ttu-id="a4c4f-133">Все задания должны принадлежать tooa коллекции заданий, которая уже существует, то есть нет неявного создания.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-133">All jobs must belong tooa job collection that already exists, so there is no implicit creation.</span></span> <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| <span data-ttu-id="a4c4f-134">**Управление журналами заданий**</span><span class="sxs-lookup"><span data-stu-id="a4c4f-134">**Job history management**</span></span> |<span data-ttu-id="a4c4f-135">Поддержка запроса GET для извлечения журнала заданий за последние 60 дней с указанием времени и результатов выполнения.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-135">GET support for fetching 60 days of job execution history, such as job elapsed time and job execution results.</span></span> <span data-ttu-id="a4c4f-136">Добавляет поддержку строкового параметра запроса для фильтрации результатов по состоянию и статусу.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-136">Adds query string parameter support for filtering based on state and status.</span></span> <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a><span data-ttu-id="a4c4f-137">Типы заданий</span><span class="sxs-lookup"><span data-stu-id="a4c4f-137">Job types</span></span>
<span data-ttu-id="a4c4f-138">Существует несколько типов заданий: задания HTTP (включая задания HTTPS, поддерживающие протокол SSL), задания очереди хранилища, задания очереди служебной шины и задания раздела служебной шины.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-138">There are multiple types of jobs: HTTP jobs (including HTTPS jobs that support SSL), storage queue jobs, service bus queue jobs, and service bus topic jobs.</span></span> <span data-ttu-id="a4c4f-139">Задания HTTP применяются, если у вас есть конечная точка существующей рабочей нагрузки или службы.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-139">HTTP jobs are ideal if you have an endpoint of an existing workload or service.</span></span> <span data-ttu-id="a4c4f-140">Можно использовать очереди заданий toopost сообщения toostorage очереди хранилища, поэтому эти задания лучше подходят для рабочих нагрузок, использующих очереди хранилища.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-140">You can use storage queue jobs toopost messages toostorage queues, so those jobs are ideal for workloads that use storage queues.</span></span> <span data-ttu-id="a4c4f-141">Аналогичным образом задания служебной шины идеально подходят для рабочих нагрузок, использующих очереди и разделы служебной шины.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-141">Similarly, service bus jobs are ideal for workloads that use service bus queues and topics.</span></span>

## <a name="hello-job-entity-in-detail"></a><span data-ttu-id="a4c4f-142">сущность «задание» Hello подробно</span><span class="sxs-lookup"><span data-stu-id="a4c4f-142">hello "job" entity in detail</span></span>
<span data-ttu-id="a4c4f-143">На базовом уровне запланированное задание состоит из нескольких частей.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-143">At a basic level, a scheduled job has several parts:</span></span>

* <span data-ttu-id="a4c4f-144">Hello tooperform действие при запуске задания таймера hello</span><span class="sxs-lookup"><span data-stu-id="a4c4f-144">hello action tooperform when hello job timer fires</span></span>  
* <span data-ttu-id="a4c4f-145">Задание hello toorun hello (необязательно)</span><span class="sxs-lookup"><span data-stu-id="a4c4f-145">(Optional) hello time toorun hello job</span></span>  
* <span data-ttu-id="a4c4f-146">(Необязательно) Когда и как часто toorepeat hello задания</span><span class="sxs-lookup"><span data-stu-id="a4c4f-146">(Optional) When and how often toorepeat hello job</span></span>  
* <span data-ttu-id="a4c4f-147">(Необязательно) Toofire действия при сбое основного действия hello</span><span class="sxs-lookup"><span data-stu-id="a4c4f-147">(Optional) An action toofire if hello primary action fails</span></span>  

<span data-ttu-id="a4c4f-148">Внутренне запланированное задание также содержит системные данные, такие как hello следующее запланированное время выполнения.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-148">Internally, a scheduled job also contains system-provided data such as hello next scheduled execution time.</span></span>

<span data-ttu-id="a4c4f-149">После кода Hello предоставляет подробный пример запланированного задания.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-149">hello following code provides a comprehensive example of a scheduled job.</span></span> <span data-ttu-id="a4c4f-150">Подробности см. в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-150">Details are provided in subsequent sections.</span></span>

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
            "interval": 1,                              // optional, how often toofire (default too1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default toorecur infinitely)
            "endTime": "2012-11-04",                     // optional (default toorecur infinitely)
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

<span data-ttu-id="a4c4f-151">По результатам hello образец запланированное задание выше, определение задания состоит из нескольких частей:</span><span class="sxs-lookup"><span data-stu-id="a4c4f-151">As seen in hello sample scheduled job above, a job definition has several parts:</span></span>

* <span data-ttu-id="a4c4f-152">Время начала (startTime).</span><span class="sxs-lookup"><span data-stu-id="a4c4f-152">Start time (“startTime”)</span></span>  
* <span data-ttu-id="a4c4f-153">Действие (action), которое включает действие ошибки (errorAction).</span><span class="sxs-lookup"><span data-stu-id="a4c4f-153">Action (“action”), which includes error action (“errorAction”)</span></span>
* <span data-ttu-id="a4c4f-154">Повторение (recurrence).</span><span class="sxs-lookup"><span data-stu-id="a4c4f-154">Recurrence (“recurrence”)</span></span>  
* <span data-ttu-id="a4c4f-155">Состояние (state).</span><span class="sxs-lookup"><span data-stu-id="a4c4f-155">State (“state”)</span></span>  
* <span data-ttu-id="a4c4f-156">Статус (status).</span><span class="sxs-lookup"><span data-stu-id="a4c4f-156">Status (“status”)</span></span>  
* <span data-ttu-id="a4c4f-157">Политика повтора (retryPolicy).</span><span class="sxs-lookup"><span data-stu-id="a4c4f-157">Retry policy (“retryPolicy”)</span></span>  

<span data-ttu-id="a4c4f-158">Рассмотрим каждую часть подробно.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-158">Let’s examine each of these in detail:</span></span>

## <a name="starttime"></a><span data-ttu-id="a4c4f-159">startTime</span><span class="sxs-lookup"><span data-stu-id="a4c4f-159">startTime</span></span>
<span data-ttu-id="a4c4f-160">Hello «startTime» время начала hello и позволяет hello вызывающего объекта toospecify сети hello в смещение часового пояса [формата ISO 8601](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="a4c4f-160">hello "startTime” is hello start time and allows hello caller toospecify a time zone offset on hello wire in [ISO-8601 format](http://en.wikipedia.org/wiki/ISO_8601).</span></span>

## <a name="action-and-erroraction"></a><span data-ttu-id="a4c4f-161">action и errorAction</span><span class="sxs-lookup"><span data-stu-id="a4c4f-161">action and errorAction</span></span>
<span data-ttu-id="a4c4f-162">Действие «Hello» — hello действие, вызываемое при каждом выполнении и описывает тип вызова службы.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-162">hello “action” is hello action invoked on each occurrence and describes a type of service invocation.</span></span> <span data-ttu-id="a4c4f-163">Действие Hello является то, что будет выполняться по hello указано расписание.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-163">hello action is what will be executed on hello provided schedule.</span></span> <span data-ttu-id="a4c4f-164">Планировщик поддерживает действия, связанные с HTTP, очередью хранилища, разделом служебной шины и очередью служебной шины.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-164">Scheduler supports HTTP, storage queue, service bus topic, and service bus queue actions.</span></span>

<span data-ttu-id="a4c4f-165">Действие Hello в приведенном выше примере hello является действие HTTP.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-165">hello action in hello example above is an HTTP action.</span></span> <span data-ttu-id="a4c4f-166">Ниже приведен пример с действием очереди хранилища.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-166">Below is an example of a storage queue action:</span></span>

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

<span data-ttu-id="a4c4f-167">Ниже приведен пример действия раздела служебной шины.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-167">Below is an example of a service bus topic action.</span></span>

  <span data-ttu-id="a4c4f-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span><span class="sxs-lookup"><span data-stu-id="a4c4f-168">"action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",</span></span>  
      <span data-ttu-id="a4c4f-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Может быть netMessaging или AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Сообщение", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span><span class="sxs-lookup"><span data-stu-id="a4c4f-169">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }</span></span>

<span data-ttu-id="a4c4f-170">Ниже приведен пример действия очереди служебной шины.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-170">Below is an example of a service bus queue action:</span></span>

  <span data-ttu-id="a4c4f-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span><span class="sxs-lookup"><span data-stu-id="a4c4f-171">"action": { "serviceBusQueueMessage": { "queueName": "q1",</span></span>  
      <span data-ttu-id="a4c4f-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Может быть netMessaging или AMQP "authentication": {</span><span class="sxs-lookup"><span data-stu-id="a4c4f-172">"namespace": "mySBNamespace", "transportType": "netMessaging", // Can be either netMessaging or AMQP "authentication": {</span></span>  
        <span data-ttu-id="a4c4f-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Сообщение",</span><span class="sxs-lookup"><span data-stu-id="a4c4f-173">"sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Some message",</span></span>  
      <span data-ttu-id="a4c4f-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span><span class="sxs-lookup"><span data-stu-id="a4c4f-174">"brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }</span></span>

<span data-ttu-id="a4c4f-175">Hello «errorAction» — обработчик ошибок hello, вызывается при сбое основного действия hello действие hello.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-175">hello “errorAction” is hello error handler, hello action invoked when hello primary action fails.</span></span> <span data-ttu-id="a4c4f-176">Можно использовать этот переменной toocall конечную точку обработки ошибок или отправить уведомления пользователям.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-176">You can use this variable toocall an error-handling endpoint or send a user notification.</span></span> <span data-ttu-id="a4c4f-177">Это можно использовать для достижения этого hello вторичной конечной точки в случае hello основной недоступен (например, в случае аварии на узле конечной точки hello hello) или может использоваться для уведомления конечную точку обработки ошибок.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-177">This can be used for reaching a secondary endpoint in hello case that hello primary is not available (e.g., in hello case of a disaster at hello endpoint’s site) or can be used for notifying an error handling endpoint.</span></span> <span data-ttu-id="a4c4f-178">Так же, как hello главное действие действие при возникновении ошибки hello может быть простая или составная логика, основанная на других действиях.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-178">Just like hello primary action, hello error action can be simple or composite logic based on other actions.</span></span> <span data-ttu-id="a4c4f-179">как toocreate маркер SAS см. слишком toolearn[Создание и использование подписи общего доступа](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4c4f-179">toolearn how toocreate a SAS token, refer too[Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="recurrence"></a><span data-ttu-id="a4c4f-180">recurrence</span><span class="sxs-lookup"><span data-stu-id="a4c4f-180">recurrence</span></span>
<span data-ttu-id="a4c4f-181">Параметр recurrence состоит из нескольких частей.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-181">Recurrence has several parts:</span></span>

* <span data-ttu-id="a4c4f-182">Частота (frequency): минута, час, день, неделя, месяц или год.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-182">Frequency: One of minute, hour, day, week, month, year</span></span>  
* <span data-ttu-id="a4c4f-183">Интервал: Интервал hello, заданных частоту повторения hello</span><span class="sxs-lookup"><span data-stu-id="a4c4f-183">Interval: Interval at hello given frequency for hello recurrence</span></span>  
* <span data-ttu-id="a4c4f-184">Предписанное расписание: укажите минуты, часы, дни недели, месяцы и дни месяца для повторения hello</span><span class="sxs-lookup"><span data-stu-id="a4c4f-184">Prescribed schedule: Specify minutes, hours, weekdays, months, and monthdays of hello recurrence</span></span>  
* <span data-ttu-id="a4c4f-185">Количество (count): число повторений.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-185">Count: Count of occurrences</span></span>  
* <span data-ttu-id="a4c4f-186">Время окончания: никакие задания не будет выполняться после hello указано время окончания</span><span class="sxs-lookup"><span data-stu-id="a4c4f-186">End time: No jobs will execute after hello specified end time</span></span>  

<span data-ttu-id="a4c4f-187">Задание повторяется, если его определение JSON включает объект повторения.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-187">A job is recurring if it has a recurring object specified in its JSON definition.</span></span> <span data-ttu-id="a4c4f-188">Если указаны count и endTime учитывается hello правилу выполнения, которая должна выполняться первой.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-188">If both count and endTime are specified, hello completion rule that occurs first is honored.</span></span>

## <a name="state"></a><span data-ttu-id="a4c4f-189">state</span><span class="sxs-lookup"><span data-stu-id="a4c4f-189">state</span></span>
<span data-ttu-id="a4c4f-190">состояние Hello hello задания является одним из четырех значений: включено, отключено, завершена или произошел сбой.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-190">hello state of hello job is one of four values: enabled, disabled, completed, or faulted.</span></span> <span data-ttu-id="a4c4f-191">Можно ПОМЕСТИТЬ или исправление для задания, так как tooupdate их toohello включен или отключенном состоянии.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-191">You can PUT or PATCH jobs so as tooupdate them toohello enabled or disabled state.</span></span> <span data-ttu-id="a4c4f-192">Если задание завершено или произошел сбой, то есть конечное состояние, которое не может быть обновлен (но hello задания по-прежнему может быть удалено).</span><span class="sxs-lookup"><span data-stu-id="a4c4f-192">If a job has been completed or faulted, that is a final state that cannot be updated (though hello job can still be DELETED).</span></span> <span data-ttu-id="a4c4f-193">Пример свойства состояния hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a4c4f-193">An example of hello state property is as follows:</span></span>

        "state": "disabled", // enabled, disabled, completed, or faulted
<span data-ttu-id="a4c4f-194">Завершенные и неисправные задания удаляются через 60 дней.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-194">Completed and faulted jobs are deleted after 60 days.</span></span>

## <a name="status"></a><span data-ttu-id="a4c4f-195">status</span><span class="sxs-lookup"><span data-stu-id="a4c4f-195">status</span></span>
<span data-ttu-id="a4c4f-196">После запуска задания планировщика будут возвращены сведения о текущем состоянии hello hello задания.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-196">Once a Scheduler job has started, information will be returned about hello current status of hello job.</span></span> <span data-ttu-id="a4c4f-197">Этот объект не может задаваться пользователем hello — он задается системой hello.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-197">This object is not settable by hello user—it’s set by hello system.</span></span> <span data-ttu-id="a4c4f-198">Тем не менее он включен в hello объекта задания (а не отдельным связанным ресурсом), чтобы один легко получить hello состояния задания.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-198">However, it is included in hello job object (rather than a separate linked resource) so that one can obtain hello status of a job easily.</span></span>

<span data-ttu-id="a4c4f-199">Состояние задания содержит время hello hello предыдущего выполнения (если таковые имеются), hello время следующего запланированного выполнения hello (для выполняющихся заданий) и число выполнений hello hello задания.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-199">Job status includes hello time of hello previous execution (if any), hello time of hello next scheduled execution (for in-progress jobs), and hello execution count of hello job.</span></span>

## <a name="retrypolicy"></a><span data-ttu-id="a4c4f-200">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="a4c4f-200">retryPolicy</span></span>
<span data-ttu-id="a4c4f-201">При сбое задания планировщика это возможных toospecify toodetermine политики повтора, повторяется ли и каким образом действие hello.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-201">If a Scheduler job fails, it is possible toospecify a retry policy toodetermine whether and how hello action is retried.</span></span> <span data-ttu-id="a4c4f-202">Это определяется hello **тип повторов** объект — установлено слишком**нет** Если нет политики повтора, как показано выше.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-202">This is determined by hello **retryType** object—it is set too**none** if there is no retry policy, as shown above.</span></span> <span data-ttu-id="a4c4f-203">Задайте для него слишком**фиксированной** при наличии политики повтора.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-203">Set it too**fixed** if there is a retry policy.</span></span>

<span data-ttu-id="a4c4f-204">tooset политику повтора можно указать два дополнительных параметра: интервал повтора (**retryInterval**) и hello число повторных попыток (**retryCount**).</span><span class="sxs-lookup"><span data-stu-id="a4c4f-204">tooset a retry policy, two additional settings may be specified: a retry interval (**retryInterval**) and hello number of retries (**retryCount**).</span></span>

<span data-ttu-id="a4c4f-205">Интервал повтора Hello, указанный с hello **retryInterval** , является hello интервал между повторными попытками.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-205">hello retry interval, specified with hello **retryInterval** object, is hello interval between retries.</span></span> <span data-ttu-id="a4c4f-206">Значение по умолчанию составляет 30 секунд, минимальное настраиваемое значение — 15 секунд, а максимальное — 18 месяцев.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-206">Its default value is 30 seconds, its minimum configurable value is 15 seconds, and its maximum value is 18 months.</span></span> <span data-ttu-id="a4c4f-207">Для заданий в бесплатных коллекциях минимальное настраиваемое значение составляет 1 час.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-207">Jobs in Free job collections have a minimum configurable value of 1 hour.</span></span>  <span data-ttu-id="a4c4f-208">Он определен в формате ISO 8601 hello.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-208">It is defined in hello ISO 8601 format.</span></span> <span data-ttu-id="a4c4f-209">Аналогичным образом, заданное значение hello hello число повторных попыток с hello **retryCount** объекта; это hello количество попыток.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-209">Similarly, hello value of hello number of retries is specified with hello **retryCount** object; it is hello number of times a retry is attempted.</span></span> <span data-ttu-id="a4c4f-210">Значение по умолчанию равно 4, а максимальное значение — 20\.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-210">Its default value is 4, and its maximum value is 20\.</span></span> <span data-ttu-id="a4c4f-211">Оба **retryInterval** и **retryCount** являются необязательными.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-211">Both **retryInterval** and **retryCount** are optional.</span></span> <span data-ttu-id="a4c4f-212">Они получают их значения по умолчанию, если **тип повторов** задано слишком**фиксированной** и значения не указаны явным образом.</span><span class="sxs-lookup"><span data-stu-id="a4c4f-212">They are given their default values if **retryType** is set too**fixed** and no values are specified explicitly.</span></span>

## <a name="see-also"></a><span data-ttu-id="a4c4f-213">См. также</span><span class="sxs-lookup"><span data-stu-id="a4c4f-213">See also</span></span>
 [<span data-ttu-id="a4c4f-214">Что такое планировщик?</span><span class="sxs-lookup"><span data-stu-id="a4c4f-214">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="a4c4f-215">Начало работы с планировщиком в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="a4c4f-215">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="a4c4f-216">Планы и выставление счетов в планировщике Azure</span><span class="sxs-lookup"><span data-stu-id="a4c4f-216">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="a4c4f-217">Как планирует комплексного toobuild и дополнительно повторения с планировщиком Azure</span><span class="sxs-lookup"><span data-stu-id="a4c4f-217">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="a4c4f-218">Справочник по API REST планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="a4c4f-218">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="a4c4f-219">Справочник по командлетам PowerShell планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="a4c4f-219">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="a4c4f-220">Высокая доступность и надежность планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="a4c4f-220">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="a4c4f-221">Ограничения, значения по умолчанию и коды ошибок планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="a4c4f-221">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="a4c4f-222">Исходящая аутентификация планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="a4c4f-222">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

