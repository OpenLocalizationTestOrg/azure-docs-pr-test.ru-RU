---
title: "Журналы диагностики концентраторов событий Azure | Документация Майкрософт"
description: "Узнайте, как настроить журналы диагностики для концентраторов событий в Azure."
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
ms.openlocfilehash: 09bc62f4918635419d74ef3ae400a41d4ce58b5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="event-hubs-diagnostic-logs"></a><span data-ttu-id="dbc93-103">Журналы диагностики концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="dbc93-103">Event Hubs diagnostic logs</span></span>

<span data-ttu-id="dbc93-104">Для концентраторов событий Azure можно просмотреть журналы двух типов.</span><span class="sxs-lookup"><span data-stu-id="dbc93-104">You can view two types of logs for Azure Event Hubs:</span></span>
* <span data-ttu-id="dbc93-105">**[Журналы действий](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="dbc93-105">**[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**.</span></span> <span data-ttu-id="dbc93-106">Эти журналы содержат сведения об операциях, выполняемых с заданием.</span><span class="sxs-lookup"><span data-stu-id="dbc93-106">These logs have information about operations performed on a job.</span></span> <span data-ttu-id="dbc93-107">Данные журналы всегда включены.</span><span class="sxs-lookup"><span data-stu-id="dbc93-107">The logs are always enabled.</span></span>
* <span data-ttu-id="dbc93-108">**[Журналы диагностики](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span><span class="sxs-lookup"><span data-stu-id="dbc93-108">**[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**.</span></span> <span data-ttu-id="dbc93-109">Вы можете настроить журналы диагностики, чтобы получать более подробные сведения обо всем, что происходит с заданием.</span><span class="sxs-lookup"><span data-stu-id="dbc93-109">You can configure diagnostic logs for a richer view of everything that happens with a job.</span></span> <span data-ttu-id="dbc93-110">Журналы диагностики охватывают действия с момента создания задания до его удаления, включая обновления и действия, которые происходят во время выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="dbc93-110">Diagnostic logs cover activities from the time the job is created until the job is deleted, including updates and activities that occur while the job is running.</span></span>

## <a name="turn-on-diagnostic-logs"></a><span data-ttu-id="dbc93-111">Включение журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="dbc93-111">Turn on diagnostic logs</span></span>
<span data-ttu-id="dbc93-112">По умолчанию журналы диагностики отключены.</span><span class="sxs-lookup"><span data-stu-id="dbc93-112">Diagnostics logs are disabled by default.</span></span> <span data-ttu-id="dbc93-113">Включение журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="dbc93-113">To enable diagnostic logs:</span></span>

1.  <span data-ttu-id="dbc93-114">На [портале Azure](https://portal.azure.com) в разделе **Мониторинг и управление** щелкните **Журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="dbc93-114">In the [Azure portal](https://portal.azure.com), under **Monitoring + Management**, click **Diagnostics logs**.</span></span>

    ![Перемещение к колонке журналов диагностики](./media/event-hubs-diagnostic-logs/image1.png)

2.  <span data-ttu-id="dbc93-116">Выберите ресурс, который необходимо отслеживать.</span><span class="sxs-lookup"><span data-stu-id="dbc93-116">Click the resource you want to monitor.</span></span>

3.  <span data-ttu-id="dbc93-117">Щелкните **Включить диагностику**.</span><span class="sxs-lookup"><span data-stu-id="dbc93-117">Click **Turn on diagnostics**.</span></span>

    ![Включение журналов диагностики](./media/event-hubs-diagnostic-logs/image2.png)

4.  <span data-ttu-id="dbc93-119">Для параметра **Состояние** щелкните **Вкл**.</span><span class="sxs-lookup"><span data-stu-id="dbc93-119">For **Status**, click **On**.</span></span>

    ![Изменение состояния журналов диагностики](./media/event-hubs-diagnostic-logs/image3.png)

5.  <span data-ttu-id="dbc93-121">Настройте нужную цель для архивирования, например учетную запись хранения, концентратор событий или Azure Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="dbc93-121">Set the archive target that you want; for example, a storage account, an event hub, or Azure Log Analytics.</span></span>

6.  <span data-ttu-id="dbc93-122">Сохраните новые параметры диагностики.</span><span class="sxs-lookup"><span data-stu-id="dbc93-122">Save the new diagnostics settings.</span></span>

<span data-ttu-id="dbc93-123">Новые параметры вступят в силу в течение 10 минут.</span><span class="sxs-lookup"><span data-stu-id="dbc93-123">New settings take effect in about 10 minutes.</span></span> <span data-ttu-id="dbc93-124">После этого журналы появятся в настроенной цели для архивирования на вкладке **Журналы диагностики**.</span><span class="sxs-lookup"><span data-stu-id="dbc93-124">After that, logs appear in the configured archival target, on the **Diagnostics logs** blade.</span></span>

<span data-ttu-id="dbc93-125">Дополнительные сведения о настройке системы диагностики доступны в [обзоре журналов диагностики Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="dbc93-125">For more information about configuring diagnostics, see the [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).</span></span>

## <a name="diagnostic-logs-categories"></a><span data-ttu-id="dbc93-126">Категории журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="dbc93-126">Diagnostic logs categories</span></span>
<span data-ttu-id="dbc93-127">Концентраторы событий записывают журналы диагностики двух категорий.</span><span class="sxs-lookup"><span data-stu-id="dbc93-127">Event Hubs captures diagnostic logs for two categories:</span></span>

* <span data-ttu-id="dbc93-128">**ArchiveLogs**: журналы, связанные с архивами концентраторов событий, в частности, с ошибками архива.</span><span class="sxs-lookup"><span data-stu-id="dbc93-128">**ArchiveLogs**: logs related to Event Hubs archives, specifically, logs related to archive errors.</span></span>
* <span data-ttu-id="dbc93-129">**OperationalLogs**: сведения о том, что происходит во время операций концентраторов событий, в частности, тип операции, включая создание концентратора событий, используемые ресурсы, а также состояние операции.</span><span class="sxs-lookup"><span data-stu-id="dbc93-129">**OperationalLogs**: information about what is happening during Event Hubs operations, specifically, the operation type, including event hub creation, resources used, and the status of the operation.</span></span>

## <a name="diagnostic-logs-schema"></a><span data-ttu-id="dbc93-130">Схема журналов диагностики</span><span class="sxs-lookup"><span data-stu-id="dbc93-130">Diagnostic logs schema</span></span>
<span data-ttu-id="dbc93-131">Все журналы хранятся в формате JSON (нотация объектов JavaScript).</span><span class="sxs-lookup"><span data-stu-id="dbc93-131">All logs are stored in JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="dbc93-132">Каждая запись содержит строковые поля, использующие формат, описанный в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="dbc93-132">Each entry has string fields that use the format described in the following sections.</span></span>

### <a name="archive-logs-schema"></a><span data-ttu-id="dbc93-133">Схема архивных журналов</span><span class="sxs-lookup"><span data-stu-id="dbc93-133">Archive logs schema</span></span>

<span data-ttu-id="dbc93-134">Строки JSON архивных журналов содержат элементы, перечисленные в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="dbc93-134">Archive log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="dbc93-135">Имя</span><span class="sxs-lookup"><span data-stu-id="dbc93-135">Name</span></span> | <span data-ttu-id="dbc93-136">Описание</span><span class="sxs-lookup"><span data-stu-id="dbc93-136">Description</span></span>
------- | -------
<span data-ttu-id="dbc93-137">TaskName</span><span class="sxs-lookup"><span data-stu-id="dbc93-137">TaskName</span></span> | <span data-ttu-id="dbc93-138">Описание задачи, завершившейся сбоем.</span><span class="sxs-lookup"><span data-stu-id="dbc93-138">Description of the task that failed.</span></span>
<span data-ttu-id="dbc93-139">ActivityId</span><span class="sxs-lookup"><span data-stu-id="dbc93-139">ActivityId</span></span> | <span data-ttu-id="dbc93-140">Внутренний идентификатор, используемый для отслеживания.</span><span class="sxs-lookup"><span data-stu-id="dbc93-140">Internal ID, used for tracking.</span></span>
<span data-ttu-id="dbc93-141">trackingId</span><span class="sxs-lookup"><span data-stu-id="dbc93-141">trackingId</span></span> | <span data-ttu-id="dbc93-142">Внутренний идентификатор, используемый для отслеживания.</span><span class="sxs-lookup"><span data-stu-id="dbc93-142">Internal ID, used for tracking.</span></span>
<span data-ttu-id="dbc93-143">resourceId</span><span class="sxs-lookup"><span data-stu-id="dbc93-143">resourceId</span></span> | <span data-ttu-id="dbc93-144">Идентификатор ресурса Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dbc93-144">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="dbc93-145">eventHub</span><span class="sxs-lookup"><span data-stu-id="dbc93-145">eventHub</span></span> | <span data-ttu-id="dbc93-146">Полное имя концентратора событий (включает в себя имя пространства имен).</span><span class="sxs-lookup"><span data-stu-id="dbc93-146">Event hub full name (includes namespace name).</span></span>
<span data-ttu-id="dbc93-147">partitionId</span><span class="sxs-lookup"><span data-stu-id="dbc93-147">partitionId</span></span> | <span data-ttu-id="dbc93-148">Секция концентратора событий, в которую записываются данные.</span><span class="sxs-lookup"><span data-stu-id="dbc93-148">Event Hub partition being written to.</span></span>
<span data-ttu-id="dbc93-149">archiveStep</span><span class="sxs-lookup"><span data-stu-id="dbc93-149">archiveStep</span></span> | <span data-ttu-id="dbc93-150">ArchiveFlushWriter</span><span class="sxs-lookup"><span data-stu-id="dbc93-150">ArchiveFlushWriter</span></span>
<span data-ttu-id="dbc93-151">startTime</span><span class="sxs-lookup"><span data-stu-id="dbc93-151">startTime</span></span> | <span data-ttu-id="dbc93-152">Время начала сбоя.</span><span class="sxs-lookup"><span data-stu-id="dbc93-152">Failure start time.</span></span>
<span data-ttu-id="dbc93-153">failures</span><span class="sxs-lookup"><span data-stu-id="dbc93-153">failures</span></span> | <span data-ttu-id="dbc93-154">Количество произошедших сбоев.</span><span class="sxs-lookup"><span data-stu-id="dbc93-154">Number of times failure occurred.</span></span>
<span data-ttu-id="dbc93-155">durationInSeconds</span><span class="sxs-lookup"><span data-stu-id="dbc93-155">durationInSeconds</span></span> | <span data-ttu-id="dbc93-156">Продолжительность сбоя.</span><span class="sxs-lookup"><span data-stu-id="dbc93-156">Duration of failure.</span></span>
<span data-ttu-id="dbc93-157">Message</span><span class="sxs-lookup"><span data-stu-id="dbc93-157">message</span></span> | <span data-ttu-id="dbc93-158">Сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="dbc93-158">Error message.</span></span>
<span data-ttu-id="dbc93-159">category</span><span class="sxs-lookup"><span data-stu-id="dbc93-159">category</span></span> | <span data-ttu-id="dbc93-160">ArchiveLogs</span><span class="sxs-lookup"><span data-stu-id="dbc93-160">ArchiveLogs</span></span>

<span data-ttu-id="dbc93-161">Ниже приведен пример строки JSON журнала архивирования.</span><span class="sxs-lookup"><span data-stu-id="dbc93-161">The following code is an example of an archive log JSON string:</span></span>

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
     "message": "Microsoft.WindowsAzure.Storage.StorageException: The remote server returned an error: (404) Not Found. ---> System.Net.WebException: The remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a><span data-ttu-id="dbc93-162">Схема операционных журналов</span><span class="sxs-lookup"><span data-stu-id="dbc93-162">Operational logs schema</span></span>

<span data-ttu-id="dbc93-163">Строки JSON операционного журнала содержат элементы, перечисленные в приведенной ниже таблице.</span><span class="sxs-lookup"><span data-stu-id="dbc93-163">Operational log JSON strings include elements listed in the following table:</span></span>

<span data-ttu-id="dbc93-164">Имя</span><span class="sxs-lookup"><span data-stu-id="dbc93-164">Name</span></span> | <span data-ttu-id="dbc93-165">Описание</span><span class="sxs-lookup"><span data-stu-id="dbc93-165">Description</span></span>
------- | -------
<span data-ttu-id="dbc93-166">ActivityId</span><span class="sxs-lookup"><span data-stu-id="dbc93-166">ActivityId</span></span> | <span data-ttu-id="dbc93-167">Внутренний идентификатор, используемый для отслеживания.</span><span class="sxs-lookup"><span data-stu-id="dbc93-167">Internal ID, used to track purpose.</span></span>
<span data-ttu-id="dbc93-168">EventName</span><span class="sxs-lookup"><span data-stu-id="dbc93-168">EventName</span></span> | <span data-ttu-id="dbc93-169">Имя операции.</span><span class="sxs-lookup"><span data-stu-id="dbc93-169">Operation name.</span></span>  
<span data-ttu-id="dbc93-170">resourceId</span><span class="sxs-lookup"><span data-stu-id="dbc93-170">resourceId</span></span> | <span data-ttu-id="dbc93-171">Идентификатор ресурса Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dbc93-171">Azure Resource Manager resource ID.</span></span>
<span data-ttu-id="dbc93-172">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="dbc93-172">SubscriptionId</span></span> | <span data-ttu-id="dbc93-173">Идентификатор подписки.</span><span class="sxs-lookup"><span data-stu-id="dbc93-173">Subscription ID.</span></span>
<span data-ttu-id="dbc93-174">EventTimeString</span><span class="sxs-lookup"><span data-stu-id="dbc93-174">EventTimeString</span></span> | <span data-ttu-id="dbc93-175">Время операции.</span><span class="sxs-lookup"><span data-stu-id="dbc93-175">Operation time.</span></span>
<span data-ttu-id="dbc93-176">EventProperties</span><span class="sxs-lookup"><span data-stu-id="dbc93-176">EventProperties</span></span> | <span data-ttu-id="dbc93-177">Свойства операции.</span><span class="sxs-lookup"><span data-stu-id="dbc93-177">Operation properties.</span></span>
<span data-ttu-id="dbc93-178">Status</span><span class="sxs-lookup"><span data-stu-id="dbc93-178">Status</span></span> | <span data-ttu-id="dbc93-179">Состояние операции.</span><span class="sxs-lookup"><span data-stu-id="dbc93-179">Operation status.</span></span>
<span data-ttu-id="dbc93-180">Caller</span><span class="sxs-lookup"><span data-stu-id="dbc93-180">Caller</span></span> | <span data-ttu-id="dbc93-181">Объект, вызвавший операцию (портал Azure или клиент управления).</span><span class="sxs-lookup"><span data-stu-id="dbc93-181">Caller of operation (Azure portal or management client).</span></span>
<span data-ttu-id="dbc93-182">category</span><span class="sxs-lookup"><span data-stu-id="dbc93-182">category</span></span> | <span data-ttu-id="dbc93-183">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="dbc93-183">OperationalLogs</span></span>

<span data-ttu-id="dbc93-184">Ниже приведен пример строки JSON операционного журнала.</span><span class="sxs-lookup"><span data-stu-id="dbc93-184">The following code is an example of an operational log JSON string:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="dbc93-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dbc93-185">Next steps</span></span>
* [<span data-ttu-id="dbc93-186">Что такое концентраторы событий Azure?</span><span class="sxs-lookup"><span data-stu-id="dbc93-186">Introduction to Event Hubs</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="dbc93-187">Общие сведения об API концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="dbc93-187">Event Hubs API overview</span></span>](event-hubs-api-overview.md)
* [<span data-ttu-id="dbc93-188">Начало работы с концентраторами событий</span><span class="sxs-lookup"><span data-stu-id="dbc93-188">Get started with Event Hubs</span></span>](event-hubs-csharp-ephcs-getstarted.md)
