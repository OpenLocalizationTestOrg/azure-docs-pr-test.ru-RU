---
title: "журналы диагностики концентраторов событий aaaAzure | Документы Microsoft"
description: "Узнайте, как tooset копирование журналов диагностики для концентраторов событий в Azure."
keywords: 
documentationcenter: 
services: event-hubs
author: banisadr
manager: 
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: sethm;babanisa
ms.openlocfilehash: d2054e2e444e715e5077fe2608fe1e009e6c1d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-diagnostic-logs"></a><span data-ttu-id="b0953-103">Журналы диагностики концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="b0953-103">Event Hubs diagnostic logs</span></span>

<span data-ttu-id="b0953-104">Для концентраторов событий Azure можно просмотреть журналы двух типов.</span><span class="sxs-lookup"><span data-stu-id="b0953-104">You can view two types of logs for Azure Event Hubs:</span></span>
* <span data-ttu-id="b0953-105">**[Журналы действий](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="b0953-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="b0953-106">Эти журналы содержат сведения об операциях, выполняемых с заданием.</span><span class="sxs-lookup"><span data-stu-id="b0953-106">These logs have information about operations performed on a job.</span></span> <span data-ttu-id="b0953-107">журналы Hello всегда включен.</span><span class="sxs-lookup"><span data-stu-id="b0953-107">hello logs are always enabled.</span></span>
* <span data-ttu-id="b0953-108">**[Журналы диагностики](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="b0953-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="b0953-109">Вы можете настроить журналы диагностики, чтобы получать более подробные сведения обо всем, что происходит с заданием.</span><span class="sxs-lookup"><span data-stu-id="b0953-109">You can configure diagnostic logs for a richer view of everything that happens with a job.</span></span> <span data-ttu-id="b0953-110">Действия титульных журналы диагностики с момента создания задания hello до удаления задания hello, включая обновления и действия, которые могут возникнуть при выполнении задания hello hello.</span><span class="sxs-lookup"><span data-stu-id="b0953-110">Diagnostic logs cover activities from hello time hello job is created until hello job is deleted, including updates and activities that occur while hello job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="b0953-111">Включение журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="b0953-111">Turn on diagnostic logs</span></span>
<span data-ttu-id="b0953-112">По умолчанию журналы диагностики отключены.</span><span class="sxs-lookup"><span data-stu-id="b0953-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="b0953-113">журналы диагностики tooenable:</span><span class="sxs-lookup"><span data-stu-id="b0953-113">tooenable diagnostic logs:</span></span>

1.  <span data-ttu-id="b0953-114">В hello [портал Azure](https://portal.azure.com)в разделе **мониторинг + управления**, нажмите кнопку **журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="b0953-114">In hello [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![журналы toodiagnostic колонке навигации](./media/event-hubs-diagnostic-logs/image1.png)

2.  <span data-ttu-id="b0953-116">Щелкните ресурс hello требуется toomonitor.</span><span class="sxs-lookup"><span data-stu-id="b0953-116">Click hello resource you want toomonitor.</span></span>

3.  <span data-ttu-id="b0953-117">Щелкните **Включить диагностику**.</span><span class="sxs-lookup"><span data-stu-id="b0953-117">Click **Turn on diagnostics**.</span></span>

    ![Включение журналов диагностики](./media/event-hubs-diagnostic-logs/image2.png)

4.  <span data-ttu-id="b0953-119">Для параметра **Состояние** щелкните **Вкл**.</span><span class="sxs-lookup"><span data-stu-id="b0953-119">For **Status**, click **On**.</span></span>

    ![Изменение состояния hello журналов диагностики](./media/event-hubs-diagnostic-logs/image3.png)

5.  <span data-ttu-id="b0953-121">Набор hello архив целевой объекты; например учетная запись хранения, концентратора событий или анализа журналов Azure.</span><span class="sxs-lookup"><span data-stu-id="b0953-121">Set hello archive target that you want; for example, a storage account, an event hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="b0953-122">Сохраните новые параметры диагностики hello.</span><span class="sxs-lookup"><span data-stu-id="b0953-122">Save hello new diagnostics settings.</span></span>

<span data-ttu-id="b0953-123">Новые параметры вступят в силу в течение 10 минут.</span><span class="sxs-lookup"><span data-stu-id="b0953-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="b0953-124">После этого журналы отображаются на конечном архивных hello настроен на hello **журналы диагностики** колонку.</span><span class="sxs-lookup"><span data-stu-id="b0953-124">After that, logs appear in hello configured archival target, on hello **Diagnostics logs** blade.</span></span>

<span data-ttu-id="b0953-125">Дополнительные сведения о настройке диагностики см. в разделе hello [Обзор Azure журналам диагностики](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="b0953-125">For more information about configuring diagnostics, see hello [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-categories"></a><span data-ttu-id="b0953-126">Категории журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="b0953-126">Diagnostic logs categories</span></span>
<span data-ttu-id="b0953-127">Концентраторы событий записывают журналы диагностики двух категорий.</span><span class="sxs-lookup"><span data-stu-id="b0953-127">Event Hubs captures diagnostic logs for two categories:</span></span>

* <span data-ttu-id="b0953-128">**ArchiveLogs**: журналы, связанные с архивами tooEvent концентраторы, в частности, регистрирует ошибки, связанные tooarchive.</span><span class="sxs-lookup"><span data-stu-id="b0953-128">**ArchiveLogs**: logs related tooEvent Hubs archives, specifically, logs related tooarchive errors.</span></span>
* <span data-ttu-id="b0953-129">**OperationalLogs**: сведения о выполняемых во время операций концентраторов событий, в частности, hello тип операции, включая создание концентратора событий, использование ресурсов и состояние операции hello hello.</span><span class="sxs-lookup"><span data-stu-id="b0953-129">**OperationalLogs**: information about what is happening during Event Hubs operations, specifically, hello operation type, including event hub creation, resources used, and hello status of hello operation.</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="b0953-130">Схема журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="b0953-130">Diagnostic logs schema</span></span>
<span data-ttu-id="b0953-131">Все журналы хранятся в формате JSON (нотация объектов JavaScript).</span><span class="sxs-lookup"><span data-stu-id="b0953-131">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="b0953-132">Каждая запись содержит поля строки, используйте формат hello, описанные в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="b0953-132">Each entry has string fields that use hello format described in hello following sections.</span></span>

### <a name="archive-logs-schema"></a><span data-ttu-id="b0953-133">Схема архивных журналов</span><span class="sxs-lookup"><span data-stu-id="b0953-133">Archive logs schema</span></span>

<span data-ttu-id="b0953-134">Строки JSON архив журнала включать элементы, перечисленные в следующей таблице hello:</span><span class="sxs-lookup"><span data-stu-id="b0953-134">Archive log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="b0953-135">Имя</span><span class="sxs-lookup"><span data-stu-id="b0953-135">Name</span></span> | <span data-ttu-id="b0953-136">Описание</span><span class="sxs-lookup"><span data-stu-id="b0953-136">Description</span></span>
------- | -------
<span data-ttu-id="b0953-137">TaskName</span><span class="sxs-lookup"><span data-stu-id="b0953-137">TaskName</span></span> | <span data-ttu-id="b0953-138">Описание задачи hello, завершившегося ошибкой.</span><span class="sxs-lookup"><span data-stu-id="b0953-138">Description of hello task that failed.</span></span>
<span data-ttu-id="b0953-139">ActivityId</span><span class="sxs-lookup"><span data-stu-id="b0953-139">ActivityId</span></span> | <span data-ttu-id="b0953-140">Внутренний идентификатор, используемый для отслеживания.</span><span class="sxs-lookup"><span data-stu-id="b0953-140">Internal ID, used for tracking.</span></span>
<span data-ttu-id="b0953-141">trackingId</span><span class="sxs-lookup"><span data-stu-id="b0953-141">trackingId</span></span> | <span data-ttu-id="b0953-142">Внутренний идентификатор, используемый для отслеживания.</span><span class="sxs-lookup"><span data-stu-id="b0953-142">Internal ID, used for tracking.</span></span>
<span data-ttu-id="b0953-143">resourceId</span><span class="sxs-lookup"><span data-stu-id="b0953-143">resourceId</span></span> | <span data-ttu-id="b0953-144">Идентификатор ресурса Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b0953-144">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="b0953-145">eventHub</span><span class="sxs-lookup"><span data-stu-id="b0953-145">eventHub</span></span> | <span data-ttu-id="b0953-146">Полное имя концентратора событий (включает в себя имя пространства имен).</span><span class="sxs-lookup"><span data-stu-id="b0953-146">Event hub full name (includes namespace name).</span></span>
<span data-ttu-id="b0953-147">partitionId</span><span class="sxs-lookup"><span data-stu-id="b0953-147">partitionId</span></span> | <span data-ttu-id="b0953-148">Секция концентратора событий, в которую записываются данные.</span><span class="sxs-lookup"><span data-stu-id="b0953-148">Event Hub partition being written to.</span></span>
<span data-ttu-id="b0953-149">archiveStep</span><span class="sxs-lookup"><span data-stu-id="b0953-149">archiveStep</span></span> | <span data-ttu-id="b0953-150">ArchiveFlushWriter</span><span class="sxs-lookup"><span data-stu-id="b0953-150">ArchiveFlushWriter</span></span>
<span data-ttu-id="b0953-151">startTime</span><span class="sxs-lookup"><span data-stu-id="b0953-151">startTime</span></span> | <span data-ttu-id="b0953-152">Время начала сбоя.</span><span class="sxs-lookup"><span data-stu-id="b0953-152">Failure start time.</span></span>
<span data-ttu-id="b0953-153">failures</span><span class="sxs-lookup"><span data-stu-id="b0953-153">failures</span></span> | <span data-ttu-id="b0953-154">Количество произошедших сбоев.</span><span class="sxs-lookup"><span data-stu-id="b0953-154">Number of times failure occurred.</span></span>
<span data-ttu-id="b0953-155">durationInSeconds</span><span class="sxs-lookup"><span data-stu-id="b0953-155">durationInSeconds</span></span> | <span data-ttu-id="b0953-156">Продолжительность сбоя.</span><span class="sxs-lookup"><span data-stu-id="b0953-156">Duration of failure.</span></span>
<span data-ttu-id="b0953-157">Message</span><span class="sxs-lookup"><span data-stu-id="b0953-157">message</span></span> | <span data-ttu-id="b0953-158">Сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="b0953-158">Error message.</span></span>
<span data-ttu-id="b0953-159">category</span><span class="sxs-lookup"><span data-stu-id="b0953-159">category</span></span> | <span data-ttu-id="b0953-160">ArchiveLogs</span><span class="sxs-lookup"><span data-stu-id="b0953-160">ArchiveLogs</span></span>

<span data-ttu-id="b0953-161">Hello следующий код является примером журнал архива строки JSON:</span><span class="sxs-lookup"><span data-stu-id="b0953-161">hello following code is an example of an archive log JSON string:</span></span>

```json
{
     "TaskName": "EventHubArchiveUserError",
     "ActivityId": "21b89a0b-8095-471a-9db8-d151d74ecf26",
     "trackingId": "21b89a0b-8095-471a-9db8-d151d74ecf26_B7",
     "resourceId": "/SUBSCRIPTIONS/854D368F-1828-428F-8F3C-F2AFFA9B2F7D/RESOURCEGROUPS/DEFAULT-EVENTHUB-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/FBETTATI-OPERA-EVENTHUB",
     "eventHub": "fbettati-opera-eventhub:eventhub:eh123~32766",
     "partitionId": "1",
     "archiveStep": "ArchiveFlushWriter",
     "startTime": "9/22/2016 5:11:21 AM",
     "failures": 3,
     "durationInSeconds": 360,
     "message": "Microsoft.WindowsAzure.Storage.StorageException: hello remote server returned an error: (404) Not Found. ---> System.Net.WebException: hello remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a><span data-ttu-id="b0953-162">Схема операционных журналов</span><span class="sxs-lookup"><span data-stu-id="b0953-162">Operational logs schema</span></span>

<span data-ttu-id="b0953-163">Операционный журнал JSON строки включать элементы, перечисленные в следующей таблице hello:</span><span class="sxs-lookup"><span data-stu-id="b0953-163">Operational log JSON strings include elements listed in hello following table:</span></span>

<span data-ttu-id="b0953-164">Имя</span><span class="sxs-lookup"><span data-stu-id="b0953-164">Name</span></span> | <span data-ttu-id="b0953-165">Описание</span><span class="sxs-lookup"><span data-stu-id="b0953-165">Description</span></span>
------- | -------
<span data-ttu-id="b0953-166">ActivityId</span><span class="sxs-lookup"><span data-stu-id="b0953-166">ActivityId</span></span> | <span data-ttu-id="b0953-167">Внутренний идентификатор, используемый tootrack цели.</span><span class="sxs-lookup"><span data-stu-id="b0953-167">Internal ID, used tootrack purpose.</span></span>
<span data-ttu-id="b0953-168">EventName</span><span class="sxs-lookup"><span data-stu-id="b0953-168">EventName</span></span> | <span data-ttu-id="b0953-169">Имя операции.</span><span class="sxs-lookup"><span data-stu-id="b0953-169">Operation name.</span></span>  
<span data-ttu-id="b0953-170">resourceId</span><span class="sxs-lookup"><span data-stu-id="b0953-170">resourceId</span></span> | <span data-ttu-id="b0953-171">Идентификатор ресурса Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b0953-171">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="b0953-172">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="b0953-172">SubscriptionId</span></span> | <span data-ttu-id="b0953-173">Идентификатор подписки.</span><span class="sxs-lookup"><span data-stu-id="b0953-173">Subscription ID.</span></span>
<span data-ttu-id="b0953-174">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="b0953-174">EventTimeString</span></span> | <span data-ttu-id="b0953-175">Время операции.</span><span class="sxs-lookup"><span data-stu-id="b0953-175">Operation time.</span></span>
<span data-ttu-id="b0953-176">EventProperties</span><span class="sxs-lookup"><span data-stu-id="b0953-176">EventProperties</span></span> | <span data-ttu-id="b0953-177">Свойства операции.</span><span class="sxs-lookup"><span data-stu-id="b0953-177">Operation properties.</span></span>
<span data-ttu-id="b0953-178">Status</span><span class="sxs-lookup"><span data-stu-id="b0953-178">Status</span></span> | <span data-ttu-id="b0953-179">Состояние операции.</span><span class="sxs-lookup"><span data-stu-id="b0953-179">Operation status.</span></span>
<span data-ttu-id="b0953-180">Caller</span><span class="sxs-lookup"><span data-stu-id="b0953-180">Caller</span></span> | <span data-ttu-id="b0953-181">Объект, вызвавший операцию (портал Azure или клиент управления).</span><span class="sxs-lookup"><span data-stu-id="b0953-181">Caller of operation (Azure portal or management client).</span></span>
<span data-ttu-id="b0953-182">category</span><span class="sxs-lookup"><span data-stu-id="b0953-182">category</span></span> | <span data-ttu-id="b0953-183">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="b0953-183">OperationalLogs</span></span>

<span data-ttu-id="b0953-184">Hello ниже приведен пример строки JSON Операционный журнал:</span><span class="sxs-lookup"><span data-stu-id="b0953-184">hello following code is an example of an operational log JSON string:</span></span>

```json
Example:
{
     "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
     "EventName": "Create EventHub",
     "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/SHOEBOXEHNS-CY4001",
     "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
     "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
     "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
     "Status": "Succeeded",
     "Caller": "ServiceBus Client",
     "category": "OperationalLogs"
}
```

## <a name="next-steps"></a><span data-ttu-id="b0953-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b0953-185">Next steps</span></span>
* [<span data-ttu-id="b0953-186">Введение tooEvent концентраторы</span><span class="sxs-lookup"><span data-stu-id="b0953-186">Introduction tooEvent Hubs</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="b0953-187">Общие сведения об API концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="b0953-187">Event Hubs API overview</span></span>](event-hubs-api-overview.md)
* [<span data-ttu-id="b0953-188">Начало работы с концентраторами событий</span><span class="sxs-lookup"><span data-stu-id="b0953-188">Get started with Event Hubs</span></span>](event-hubs-csharp-ephcs-getstarted.md)
