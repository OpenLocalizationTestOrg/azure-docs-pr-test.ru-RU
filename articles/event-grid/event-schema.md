---
title: "Схема событий aaaAzure сетки событий"
description: "Описывает свойства hello, которые предоставляются для событий с сеткой событий Azure."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/15/2017
ms.author: babanisa
ms.openlocfilehash: 37178a5650b93fd9072d9cff3333aae14b2a2ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-event-schema"></a><span data-ttu-id="26823-103">Схема событий службы "Сетка событий Azure"</span><span class="sxs-lookup"><span data-stu-id="26823-103">Event Grid event schema</span></span>

<span data-ttu-id="26823-104">В этой статье предоставляет свойства hello и схемы для событий.</span><span class="sxs-lookup"><span data-stu-id="26823-104">This article provides hello properties and schema for events.</span></span> <span data-ttu-id="26823-105">События включают пять обязательных свойств строки и обязательный объект **данных**.</span><span class="sxs-lookup"><span data-stu-id="26823-105">Events consist of a set of five required string properties and a required **data** object.</span></span> <span data-ttu-id="26823-106">свойства Hello — распространенные события tooall из любого издателя.</span><span class="sxs-lookup"><span data-stu-id="26823-106">hello properties are common tooall events from any publisher.</span></span> <span data-ttu-id="26823-107">Hello **данные** объект содержит свойства, которые являются определенной tooeach издателя.</span><span class="sxs-lookup"><span data-stu-id="26823-107">hello **data** object contains properties that are specific tooeach publisher.</span></span> <span data-ttu-id="26823-108">Разделы, системы эти свойства являются toohello конкретного поставщика ресурсов, хранения или концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="26823-108">For system topics, these properties are specific toohello resource provider, such as Storage or Event Hubs.</span></span>

<span data-ttu-id="26823-109">События отправляются tooAzure сетки событий в массив, который может содержать несколько объектов события.</span><span class="sxs-lookup"><span data-stu-id="26823-109">Events are sent tooAzure Event Grid in an array, which can contain multiple event objects.</span></span> <span data-ttu-id="26823-110">Если имеется только одно событие, hello массива имеет длину 1.</span><span class="sxs-lookup"><span data-stu-id="26823-110">If there is only a single event, hello array has a length of 1.</span></span> 
 
## <a name="event-properties"></a><span data-ttu-id="26823-111">Свойства события</span><span class="sxs-lookup"><span data-stu-id="26823-111">Event properties</span></span>

<span data-ttu-id="26823-112">Все события будут содержать hello же следующие данных верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="26823-112">All events will contain hello same following top level data.</span></span>

| <span data-ttu-id="26823-113">Свойство</span><span class="sxs-lookup"><span data-stu-id="26823-113">Property</span></span> | <span data-ttu-id="26823-114">Тип</span><span class="sxs-lookup"><span data-stu-id="26823-114">Type</span></span> | <span data-ttu-id="26823-115">Описание</span><span class="sxs-lookup"><span data-stu-id="26823-115">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="26823-116">Раздел</span><span class="sxs-lookup"><span data-stu-id="26823-116">topic</span></span> | <span data-ttu-id="26823-117">string</span><span class="sxs-lookup"><span data-stu-id="26823-117">string</span></span> | <span data-ttu-id="26823-118">Источник события toohello ресурсов полный путь.</span><span class="sxs-lookup"><span data-stu-id="26823-118">Full resource path toohello event source.</span></span> <span data-ttu-id="26823-119">Это поле защищено от записи.</span><span class="sxs-lookup"><span data-stu-id="26823-119">This field is not writeable.</span></span> |
| <span data-ttu-id="26823-120">subject</span><span class="sxs-lookup"><span data-stu-id="26823-120">subject</span></span> | <span data-ttu-id="26823-121">string</span><span class="sxs-lookup"><span data-stu-id="26823-121">string</span></span> | <span data-ttu-id="26823-122">Тема события toohello определенный путь издателя.</span><span class="sxs-lookup"><span data-stu-id="26823-122">Publisher defined path toohello event subject.</span></span> |
| <span data-ttu-id="26823-123">eventType</span><span class="sxs-lookup"><span data-stu-id="26823-123">eventType</span></span> | <span data-ttu-id="26823-124">string</span><span class="sxs-lookup"><span data-stu-id="26823-124">string</span></span> | <span data-ttu-id="26823-125">Одно из hello зарегистрированные типы событий для этого источника событий.</span><span class="sxs-lookup"><span data-stu-id="26823-125">One of hello registered event types for this event source.</span></span> |
| <span data-ttu-id="26823-126">eventTime</span><span class="sxs-lookup"><span data-stu-id="26823-126">eventTime</span></span> | <span data-ttu-id="26823-127">string</span><span class="sxs-lookup"><span data-stu-id="26823-127">string</span></span> | <span data-ttu-id="26823-128">событие hello Hello времени формируется на основе времени UTC hello поставщика.</span><span class="sxs-lookup"><span data-stu-id="26823-128">hello time hello event is generated based on hello provider's UTC time.</span></span> |
| <span data-ttu-id="26823-129">id</span><span class="sxs-lookup"><span data-stu-id="26823-129">id</span></span> | <span data-ttu-id="26823-130">string</span><span class="sxs-lookup"><span data-stu-id="26823-130">string</span></span> | <span data-ttu-id="26823-131">Уникальный идентификатор для события hello.</span><span class="sxs-lookup"><span data-stu-id="26823-131">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="26823-132">data</span><span class="sxs-lookup"><span data-stu-id="26823-132">data</span></span> | <span data-ttu-id="26823-133">object</span><span class="sxs-lookup"><span data-stu-id="26823-133">object</span></span> | <span data-ttu-id="26823-134">Поставщик данных о событиях определенные toohello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="26823-134">Event data specific toohello resource provider.</span></span> |

## <a name="available-event-sources"></a><span data-ttu-id="26823-135">Доступные источники событий</span><span class="sxs-lookup"><span data-stu-id="26823-135">Available event sources</span></span>

<span data-ttu-id="26823-136">следующие источники событий Hello публикации событий для использования через сетки событий:</span><span class="sxs-lookup"><span data-stu-id="26823-136">hello following event sources publish events for consumption via Event Grid:</span></span>

* <span data-ttu-id="26823-137">Группы ресурсов (операции управления)</span><span class="sxs-lookup"><span data-stu-id="26823-137">Resource Groups (management operations)</span></span>
* <span data-ttu-id="26823-138">Подписки Azure (операции управления)</span><span class="sxs-lookup"><span data-stu-id="26823-138">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="26823-139">Концентраторы событий</span><span class="sxs-lookup"><span data-stu-id="26823-139">Event Hubs</span></span>
* <span data-ttu-id="26823-140">Пользовательские разделы</span><span class="sxs-lookup"><span data-stu-id="26823-140">Custom Topics</span></span>

## <a name="azure-subscriptions"></a><span data-ttu-id="26823-141">Подписки Azure</span><span class="sxs-lookup"><span data-stu-id="26823-141">Azure Subscriptions</span></span>

<span data-ttu-id="26823-142">Подписки Azure теперь могут создавать события управления из Azure Resource Manager, например при создании виртуальной машины или удалении учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="26823-142">Azure subscriptions can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="26823-143">Доступные типы событий</span><span class="sxs-lookup"><span data-stu-id="26823-143">Available event types</span></span>

- <span data-ttu-id="26823-144">**Microsoft.Resources.ResourceWriteSuccess**: возникает при успешном создании или обновлении ресурса.</span><span class="sxs-lookup"><span data-stu-id="26823-144">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="26823-145">**Microsoft.Resources.ResourceWriteFailure**: возникает при ошибке создания или обновления ресурса.</span><span class="sxs-lookup"><span data-stu-id="26823-145">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="26823-146">**Microsoft.Resources.ResourceWriteCancel**: возникает при отмене создания или обновления ресурса.</span><span class="sxs-lookup"><span data-stu-id="26823-146">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="26823-147">**Microsoft.Resources.ResourceDeleteSuccess**: возникает при успешном удалении ресурса.</span><span class="sxs-lookup"><span data-stu-id="26823-147">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="26823-148">**Microsoft.Resources.ResourceDeleteFailure**: возникает при ошибке удаления ресурса.</span><span class="sxs-lookup"><span data-stu-id="26823-148">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="26823-149">**Microsoft.Resources.ResourceDeleteCancel**: возникает при отмене удаления ресурса.</span><span class="sxs-lookup"><span data-stu-id="26823-149">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="26823-150">Это происходит при отмене развертывания шаблона.</span><span class="sxs-lookup"><span data-stu-id="26823-150">This happens when template deployment is cancelled.</span></span>

### <a name="example-event-schema"></a><span data-ttu-id="26823-151">Пример схемы событий</span><span class="sxs-lookup"><span data-stu-id="26823-151">Example event schema</span></span>

```json
[
    {
    "topic":"/subscriptions/{subscription-id}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="resource-groups"></a><span data-ttu-id="26823-152">Группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="26823-152">Resource Groups</span></span>

<span data-ttu-id="26823-153">Группы ресурсов теперь могут создавать события управления из Azure Resource Manager, например при создании виртуальной машины или удалении учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="26823-153">Resource Groups can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="26823-154">Доступные типы событий</span><span class="sxs-lookup"><span data-stu-id="26823-154">Available event types</span></span>

- <span data-ttu-id="26823-155">**Microsoft.Resources.ResourceWriteSuccess**: возникает при успешном создании или обновлении ресурса.</span><span class="sxs-lookup"><span data-stu-id="26823-155">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="26823-156">**Microsoft.Resources.ResourceWriteFailure**: возникает при ошибке создания или обновления ресурса.</span><span class="sxs-lookup"><span data-stu-id="26823-156">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="26823-157">**Microsoft.Resources.ResourceWriteCancel**: возникает при отмене создания или обновления ресурса.</span><span class="sxs-lookup"><span data-stu-id="26823-157">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="26823-158">**Microsoft.Resources.ResourceDeleteSuccess**: возникает при успешном удалении ресурса.</span><span class="sxs-lookup"><span data-stu-id="26823-158">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="26823-159">**Microsoft.Resources.ResourceDeleteFailure**: возникает при ошибке удаления ресурса.</span><span class="sxs-lookup"><span data-stu-id="26823-159">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="26823-160">**Microsoft.Resources.ResourceDeleteCancel**: возникает при отмене удаления ресурса.</span><span class="sxs-lookup"><span data-stu-id="26823-160">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="26823-161">Это происходит при отмене развертывания шаблона.</span><span class="sxs-lookup"><span data-stu-id="26823-161">This happens when template deployment is cancelled.</span></span>

### <a name="example-event"></a><span data-ttu-id="26823-162">Пример события</span><span class="sxs-lookup"><span data-stu-id="26823-162">Example event</span></span>

```json
[
    {
    "topic":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="event-hubs"></a><span data-ttu-id="26823-163">Концентраторы событий</span><span class="sxs-lookup"><span data-stu-id="26823-163">Event Hubs</span></span>

<span data-ttu-id="26823-164">События концентраторов событий, в настоящее время создается только файл автоматически отправляется toostorage, с помощью функции отслеживания hello.</span><span class="sxs-lookup"><span data-stu-id="26823-164">Event Hubs events are currently only emitted when a file is automatically sent toostorage using hello Capture feature.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="26823-165">Доступные типы событий</span><span class="sxs-lookup"><span data-stu-id="26823-165">Available event types</span></span>

- <span data-ttu-id="26823-166">**Microsoft.EventHub.CaptureFileCreated**: возникает при создании файла записи.</span><span class="sxs-lookup"><span data-stu-id="26823-166">**Microsoft.EventHub.CaptureFileCreated**: Raised when a capture file is created.</span></span>

### <a name="example-event"></a><span data-ttu-id="26823-167">Пример события</span><span class="sxs-lookup"><span data-stu-id="26823-167">Example event</span></span>

<span data-ttu-id="26823-168">Образец показывает схему hello концентраторов событий событие, возникающее при записи в котором хранится файл.</span><span class="sxs-lookup"><span data-stu-id="26823-168">This sample event shows hello schema of an Event Hubs event raised when Capture stores a file.</span></span> 

```json
[
    {
        "topic": "/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.EventHub/namespaces/{event-hubs-ns}",
        "subject": "eventhubs/eh1",
        "eventType": "Microsoft.EventHub.CaptureFileCreated",
        "eventTime": "2017-07-11T00:55:55.0120485Z",
        "id": "bd440490-a65e-4c97-8298-ef1eb325673c",
        "data": {
            "fileUrl": "https://gridtest1.blob.core.windows.net/acontainer/eventgridtest1/eh1/1/2017/07/11/00/54/54.avro",
            "fileType": "AzureBlockBlob",
            "partitionId": "1",
            "sizeInBytes": 0,
            "eventCount": 0,
            "firstSequenceNumber": -1,
            "lastSequenceNumber": -1,
            "firstEnqueueTime": "0001-01-01T00:00:00",
            "lastEnqueueTime": "0001-01-01T00:00:00"
        },
    }
]

```



## <a name="azure-blob-storage"></a><span data-ttu-id="26823-169">Хранилище больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="26823-169">Azure Blob Storage</span></span>

<span data-ttu-id="26823-170">Служба хранилища BLOB-объектов Azure в закрытой предварительной версии с регистрацией для интеграции со службой "Сетка событий Azure".</span><span class="sxs-lookup"><span data-stu-id="26823-170">Azure Blob Storage in private preview with sign-up for integration with Event Grid.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="26823-171">Доступные типы событий</span><span class="sxs-lookup"><span data-stu-id="26823-171">Available event types</span></span>

- <span data-ttu-id="26823-172">**Microsoft.Storage.BlobCreated**: возникает при создании большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="26823-172">**Microsoft.Storage.BlobCreated**: Raised when a blob is created.</span></span>
- <span data-ttu-id="26823-173">**Microsoft.Storage.BlobDeleted**: возникает при удалении большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="26823-173">**Microsoft.Storage.BlobDeleted**: Raised when a blob is deleted.</span></span>

### <a name="example-event"></a><span data-ttu-id="26823-174">Пример события</span><span class="sxs-lookup"><span data-stu-id="26823-174">Example event</span></span>

<span data-ttu-id="26823-175">Образец показывает hello схему хранилища событие, возникающее при создании большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="26823-175">This sample event shows hello schema of a storage event raised when a blob is created.</span></span> 

```json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.Storage/storageAccounts/xstoretestaccount",
    "subject": "/blobServices/default/containers/oc2d2817345i200097container/blobs/oc2d2817345i20002296blob",
    "eventType": "Microsoft.Storage.BlobCreated",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "id": "831e1650-001e-001b-66ab-eeb76e069631",
    "data": {
      "api": "PutBlockList",
      "clientRequestId": "6d79dbfb-0e37-4fc4-981f-442c9ca65760",
      "requestId": "831e1650-001e-001b-66ab-eeb76e000000",
      "eTag": "0x8D4BCC2E4835CD0",
      "contentType": "application/octet-stream",
      "contentLength": 524288,
      "blobType": "BlockBlob",
      "url": "https://oc2d2817345i60006.blob.core.windows.net/oc2d2817345i200097container/oc2d2817345i20002296blob",
      "sequencer": "00000000000004420000000000028963",
      "storageDiagnostics": {
        "batchId": "b68529f3-68cd-4744-baa4-3c0498ec19f0"
      }
    }
  }
]
```




## <a name="custom-topics"></a><span data-ttu-id="26823-176">Пользовательские разделы</span><span class="sxs-lookup"><span data-stu-id="26823-176">Custom Topics</span></span>

<span data-ttu-id="26823-177">полезные данные Hello пользовательских событий определенные пользователем и может быть любой адрес правильно отформатирован JSON.</span><span class="sxs-lookup"><span data-stu-id="26823-177">hello data payload of your custom events is defined by you and can be any well formated JSON.</span></span> <span data-ttu-id="26823-178">Hello данных верхнего уровня должен содержать hello же поля как стандартный ресурса определенного события.</span><span class="sxs-lookup"><span data-stu-id="26823-178">hello top level data should contain hello same fields as standard resource defined events.</span></span> <span data-ttu-id="26823-179">При публикации события toocustom разделы следует моделирования hello субъект вашей tooaid события в маршрутизации и фильтрации.</span><span class="sxs-lookup"><span data-stu-id="26823-179">When publishing events toocustom topics you should consider modeling hello subject of your events tooaid in routing and filtering.</span></span>

### <a name="example-event"></a><span data-ttu-id="26823-180">Пример события</span><span class="sxs-lookup"><span data-stu-id="26823-180">Example event</span></span>

<span data-ttu-id="26823-181">Следующий пример Hello показывает событие для пользовательский раздел:</span><span class="sxs-lookup"><span data-stu-id="26823-181">hello following example shows an event for a custom topic:</span></span>
````json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.EventGrid/topics/myeventgridtopic",
    "subject": "/myapp/vehicles/motorcycles",    
    "id": "b68529f3-68cd-4744-baa4-3c0498ec19e2",
    "eventType": "recordInserted",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "data":{
      "make": "Ducati",
      "model": "Monster"
    }
  }
]

````

## <a name="next-steps"></a><span data-ttu-id="26823-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="26823-182">Next steps</span></span>

* <span data-ttu-id="26823-183">Введение tooEvent сетки. в разделе [возможности сетки событий?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="26823-183">For an introduction tooEvent Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="26823-184">toolearn о создании подписки на события сетки. в разделе [схему подписки сетки событий](subscription-creation-schema.md).</span><span class="sxs-lookup"><span data-stu-id="26823-184">toolearn about creating an Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
