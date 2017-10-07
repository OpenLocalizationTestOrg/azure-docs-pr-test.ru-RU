---
title: "Схема подписки aaaAzure сетки событий"
description: "Описание свойств hello для подписки tooan события с сеткой событий Azure."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: 6a96d67975a5a733c5ea3c56ea54501f94ea4cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-subscription-schema"></a>Схема подписки для службы "Сетка событий"

toocreate подписку на событие сетки, следует отправить запрос toohello операция Create Event подписки. Hello используйте следующий формат:

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

Например, toocreate подписку на событие с именем учетной записи хранения `examplestorage` в группу ресурсов с именем `examplegroup`, используйте hello следующий формат:

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

Hello статье описаны свойства hello и схемы для hello тексте hello запроса.
 
## <a name="event-subscription-properties"></a>Свойства подписки на события

| Свойство | Тип | Описание |
| -------- | ---- | ----------- |
| ресурс destination | object | Hello объекта, который определяет конечную точку hello. |
| фильтр | object | Необязательное поле для фильтрации hello типов событий. |

### <a name="destination-object"></a>Объект destination

| Свойство | Тип | Описание |
| -------- | ---- | ----------- |
| endpointType | string | Hello тип конечной точки для hello подписки (веб-перехватчика/HTTP, концентратора событий или очереди). | 
| endpointUrl | string |  | 

### <a name="filter-object"></a>Объект filter

| Свойство | Тип | Описание |
| -------- | ---- | ----------- |
| includedEventTypes | array | Совпадать, если тип события hello в сообщение о событии hello: точное совпадение tooone этих имен типов событий. Вызывает ошибку, если не совпадает с именем события hello зарегистрированные имена типов событий для источника событий hello. По умолчанию соответствует всем типам событий. |
| subjectBeginsWith | string | Соответствие префикса фильтра toohello поле subject hello сообщения о событии. по умолчанию Hello или пустая строка соответствует всем. | 
| subjectEndsWith | string | Суффикс match фильтра toohello поле subject hello сообщения о событии. по умолчанию Hello или пустая строка соответствует всем. |
| subjectIsCaseSensitive | string | Управляет сопоставлением с учетом регистра в фильтрах. |


## <a name="example-subscription-schema"></a>Пример схемы подписки

```json
{
  "properties": {
    "destination": {
      "endpointType": "webhook",
      "properties": {
          "endpointUrl": "https://example.azurewebsites.net/api/HttpTriggerCSharp1?code=VXbGWce53l48Mt8wuotr0GPmyJ/nDT4hgdFj9DpBiRt38qqnnm5OFg=="
      }
    },
    "filter": {
      "includedEventTypes": [ "blobCreated", "blobDeleted" ],
      "subjectBeginsWith": "blobServices/default/containers/mycontainer/log",
      "subjectEndsWith": ".jpg",
      "subjectIsCaseSensitive": "true"
    }
  }
}
```

## <a name="next-steps"></a>Дальнейшие действия

* Введение tooEvent сетки. в разделе [возможности сетки событий?](overview.md)
