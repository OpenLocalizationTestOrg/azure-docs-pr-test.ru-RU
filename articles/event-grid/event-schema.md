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
# <a name="event-grid-event-schema"></a>Схема событий службы "Сетка событий Azure"

В этой статье предоставляет свойства hello и схемы для событий. События включают пять обязательных свойств строки и обязательный объект **данных**. свойства Hello — распространенные события tooall из любого издателя. Hello **данные** объект содержит свойства, которые являются определенной tooeach издателя. Разделы, системы эти свойства являются toohello конкретного поставщика ресурсов, хранения или концентраторов событий.

События отправляются tooAzure сетки событий в массив, который может содержать несколько объектов события. Если имеется только одно событие, hello массива имеет длину 1. 
 
## <a name="event-properties"></a>Свойства события

Все события будут содержать hello же следующие данных верхнего уровня.

| Свойство | Тип | Описание |
| -------- | ---- | ----------- |
| Раздел | string | Источник события toohello ресурсов полный путь. Это поле защищено от записи. |
| subject | string | Тема события toohello определенный путь издателя. |
| eventType | string | Одно из hello зарегистрированные типы событий для этого источника событий. |
| eventTime | string | событие hello Hello времени формируется на основе времени UTC hello поставщика. |
| id | string | Уникальный идентификатор для события hello. |
| data | object | Поставщик данных о событиях определенные toohello ресурсов. |

## <a name="available-event-sources"></a>Доступные источники событий

следующие источники событий Hello публикации событий для использования через сетки событий:

* Группы ресурсов (операции управления)
* Подписки Azure (операции управления)
* Концентраторы событий
* Пользовательские разделы

## <a name="azure-subscriptions"></a>Подписки Azure

Подписки Azure теперь могут создавать события управления из Azure Resource Manager, например при создании виртуальной машины или удалении учетной записи хранения.

### <a name="available-event-types"></a>Доступные типы событий

- **Microsoft.Resources.ResourceWriteSuccess**: возникает при успешном создании или обновлении ресурса.  
- **Microsoft.Resources.ResourceWriteFailure**: возникает при ошибке создания или обновления ресурса.  
- **Microsoft.Resources.ResourceWriteCancel**: возникает при отмене создания или обновления ресурса.  
- **Microsoft.Resources.ResourceDeleteSuccess**: возникает при успешном удалении ресурса.  
- **Microsoft.Resources.ResourceDeleteFailure**: возникает при ошибке удаления ресурса.  
- **Microsoft.Resources.ResourceDeleteCancel**: возникает при отмене удаления ресурса. Это происходит при отмене развертывания шаблона.

### <a name="example-event-schema"></a>Пример схемы событий

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



## <a name="resource-groups"></a>Группы ресурсов

Группы ресурсов теперь могут создавать события управления из Azure Resource Manager, например при создании виртуальной машины или удалении учетной записи хранения.

### <a name="available-event-types"></a>Доступные типы событий

- **Microsoft.Resources.ResourceWriteSuccess**: возникает при успешном создании или обновлении ресурса.  
- **Microsoft.Resources.ResourceWriteFailure**: возникает при ошибке создания или обновления ресурса.  
- **Microsoft.Resources.ResourceWriteCancel**: возникает при отмене создания или обновления ресурса.  
- **Microsoft.Resources.ResourceDeleteSuccess**: возникает при успешном удалении ресурса.  
- **Microsoft.Resources.ResourceDeleteFailure**: возникает при ошибке удаления ресурса.  
- **Microsoft.Resources.ResourceDeleteCancel**: возникает при отмене удаления ресурса. Это происходит при отмене развертывания шаблона.

### <a name="example-event"></a>Пример события

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



## <a name="event-hubs"></a>Концентраторы событий

События концентраторов событий, в настоящее время создается только файл автоматически отправляется toostorage, с помощью функции отслеживания hello.

### <a name="available-event-types"></a>Доступные типы событий

- **Microsoft.EventHub.CaptureFileCreated**: возникает при создании файла записи.

### <a name="example-event"></a>Пример события

Образец показывает схему hello концентраторов событий событие, возникающее при записи в котором хранится файл. 

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



## <a name="azure-blob-storage"></a>Хранилище больших двоичных объектов Azure

Служба хранилища BLOB-объектов Azure в закрытой предварительной версии с регистрацией для интеграции со службой "Сетка событий Azure".

### <a name="available-event-types"></a>Доступные типы событий

- **Microsoft.Storage.BlobCreated**: возникает при создании большого двоичного объекта.
- **Microsoft.Storage.BlobDeleted**: возникает при удалении большого двоичного объекта.

### <a name="example-event"></a>Пример события

Образец показывает hello схему хранилища событие, возникающее при создании большого двоичного объекта. 

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




## <a name="custom-topics"></a>Пользовательские разделы

полезные данные Hello пользовательских событий определенные пользователем и может быть любой адрес правильно отформатирован JSON. Hello данных верхнего уровня должен содержать hello же поля как стандартный ресурса определенного события. При публикации события toocustom разделы следует моделирования hello субъект вашей tooaid события в маршрутизации и фильтрации.

### <a name="example-event"></a>Пример события

Следующий пример Hello показывает событие для пользовательский раздел:
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

## <a name="next-steps"></a>Дальнейшие действия

* Введение tooEvent сетки. в разделе [возможности сетки событий?](overview.md)
* toolearn о создании подписки на события сетки. в разделе [схему подписки сетки событий](subscription-creation-schema.md).
