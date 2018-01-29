---
title: "Схема событий службы \"Сетка событий Azure\" для хранилища больших двоичных объектов"
description: "Описание свойств событий хранилища больших двоичных объектов в службе \"Сетка событий Azure\""
services: event-grid
author: tfitzmac
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 11/08/2017
ms.author: tomfitz
ms.openlocfilehash: bdc64733b75fd809cf0245986aa96370343c1a34
ms.sourcegitcommit: 6a22af82b88674cd029387f6cedf0fb9f8830afd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/11/2017
---
# <a name="azure-event-grid-event-schema-for-blob-storage"></a>Схема событий службы "Сетка событий Azure" для хранилища BLOB-объектов

В этой статье описаны свойства и схема событий хранилища BLOB-объектов. Общие сведения о схемах событий см. в статье [Схема событий службы "Сетка событий Azure"](event-schema.md).

## <a name="available-event-types"></a>Доступные типы событий

Хранилище BLOB-объектов выдает следующие типы событий:

| Тип события | Описание |
| ---------- | ----------- |
| Microsoft.Storage.BlobCreated | Возникает при создании BLOB-объекта. |
| Microsoft.Storage.BlobDeleted | Возникает при удалении BLOB-объекта. |

## <a name="example-event"></a>Пример события

В примере ниже показана схема события создания BLOB-объекта. 

```json
[{
  "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.Storage/storageAccounts/xstoretestaccount",
  "subject": "/blobServices/default/containers/testcontainer/blobs/testfile.txt",
  "eventType": "Microsoft.Storage.BlobCreated",
  "eventTime": "2017-06-26T18:41:00.9584103Z",
  "id": "831e1650-001e-001b-66ab-eeb76e069631",
  "data": {
    "api": "PutBlockList",
    "clientRequestId": "6d79dbfb-0e37-4fc4-981f-442c9ca65760",
    "requestId": "831e1650-001e-001b-66ab-eeb76e000000",
    "eTag": "0x8D4BCC2E4835CD0",
    "contentType": "text/plain",
    "contentLength": 524288,
    "blobType": "BlockBlob",
    "url": "https://example.blob.core.windows.net/testcontainer/testfile.txt",
    "sequencer": "00000000000004420000000000028963",
    "storageDiagnostics": {
      "batchId": "b68529f3-68cd-4744-baa4-3c0498ec19f0"
    }
  }
}]
```

Схема события удаления BLOB-объекта аналогична. 

```json
[{
  "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.Storage/storageAccounts/xstoretestaccount",
  "subject": "/blobServices/default/containers/testcontainer/blobs/testfile.txt",
  "eventType": "Microsoft.Storage.BlobDeleted",
  "eventTime": "2017-11-07T20:09:22.5674003Z",
  "id": "4c2359fe-001e-00ba-0e04-58586806d298",
  "data": {
    "api": "DeleteBlob",
    "requestId": "4c2359fe-001e-00ba-0e04-585868000000",
    "contentType": "text/plain",
    "blobType": "BlockBlob",
    "url": "https://example.blob.core.windows.net/testcontainer/testfile.txt",
    "sequencer": "0000000000000281000000000002F5CA",
    "storageDiagnostics": {
      "batchId": "b68529f3-68cd-4744-baa4-3c0498ec19f0"
    }
  }
}]
```
 
## <a name="event-properties"></a>Свойства события

Событие содержит следующие высокоуровневые данные:

| Свойство | Тип | Описание |
| -------- | ---- | ----------- |
| Раздел | string | Полный путь к ресурсу для источника событий. Это поле защищено от записи. |
| subject | string | Определенный издателем путь к субъекту событий. |
| eventType | string | Один из зарегистрированных типов событий для этого источника событий. |
| eventTime | string | Время создания события с учетом времени поставщика в формате UTC. |
| id | string | Уникальный идентификатор события. |
| data | object | Данные события хранилища BLOB-объектов. |

Объект данных имеет следующие свойства:

| Свойство | Тип | Описание |
| -------- | ---- | ----------- |
| api | string | Операция, вызвавшая событие. |
| clientRequestId | string | Сформированное клиентом непрозрачное значение с ограничением в 1 КБ символов. Если включено ведение журнала аналитики хранилища, значение записывается в журналы аналитики. |
| requestId | string | Уникальный идентификатор запроса. Используется для устранения неполадок в запросе. |
| eTag | string | Значение, которое позволяет выполнять операции условно. |
| сontentType | string | Тип содержимого, указанный для BLOB-объекта. |
| contentLength | integer | Размер большого двоичного объекта в байтах. |
| blobType | string | Тип большого двоичного объекта. |
| url | string | Путь к BLOB-объекту. |
| sequencer | string | Контролируемое пользователем значение, которое можно использовать для отслеживания запросов. |
| storageDiagnostics | object | Информация о диагностике хранилища. |
 
## <a name="next-steps"></a>Дальнейшие действия

* См. общие сведения о [службе "Сетка событий Azure"](overview.md).
* Дополнительные сведения о создании подписки на Сетку событий Azure см. в статье [Схема подписки для службы "Сетка событий"](subscription-creation-schema.md).
* Основные сведения о работе с событиями хранилища BLOB-объектов см. в статье [Перенаправление событий хранилища BLOB-объектов в пользовательскую конечную веб-точку (предварительная версия)](../storage/blobs/storage-blob-event-quickstart.md?toc=%2fazure%2fevent-grid%2ftoc.json). 
