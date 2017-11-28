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
# <a name="event-grid-subscription-schema"></a><span data-ttu-id="e0d43-103">Схема подписки для службы "Сетка событий"</span><span class="sxs-lookup"><span data-stu-id="e0d43-103">Event Grid subscription schema</span></span>

<span data-ttu-id="e0d43-104">toocreate подписку на событие сетки, следует отправить запрос toohello операция Create Event подписки.</span><span class="sxs-lookup"><span data-stu-id="e0d43-104">toocreate an Event Grid subscription, you send a request toohello Create Event subscription operation.</span></span> <span data-ttu-id="e0d43-105">Hello используйте следующий формат:</span><span class="sxs-lookup"><span data-stu-id="e0d43-105">Use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="e0d43-106">Например, toocreate подписку на событие с именем учетной записи хранения `examplestorage` в группу ресурсов с именем `examplegroup`, используйте hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="e0d43-106">For example, toocreate an event subscription for a storage account named `examplestorage` in a resource group named `examplegroup`, use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="e0d43-107">Hello статье описаны свойства hello и схемы для hello тексте hello запроса.</span><span class="sxs-lookup"><span data-stu-id="e0d43-107">hello article describes hello properties and schema for hello body of hello request.</span></span>
 
## <a name="event-subscription-properties"></a><span data-ttu-id="e0d43-108">Свойства подписки на события</span><span class="sxs-lookup"><span data-stu-id="e0d43-108">Event subscription properties</span></span>

| <span data-ttu-id="e0d43-109">Свойство</span><span class="sxs-lookup"><span data-stu-id="e0d43-109">Property</span></span> | <span data-ttu-id="e0d43-110">Тип</span><span class="sxs-lookup"><span data-stu-id="e0d43-110">Type</span></span> | <span data-ttu-id="e0d43-111">Описание</span><span class="sxs-lookup"><span data-stu-id="e0d43-111">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="e0d43-112">ресурс destination</span><span class="sxs-lookup"><span data-stu-id="e0d43-112">destination</span></span> | <span data-ttu-id="e0d43-113">object</span><span class="sxs-lookup"><span data-stu-id="e0d43-113">object</span></span> | <span data-ttu-id="e0d43-114">Hello объекта, который определяет конечную точку hello.</span><span class="sxs-lookup"><span data-stu-id="e0d43-114">hello object that defines hello endpoint.</span></span> |
| <span data-ttu-id="e0d43-115">фильтр</span><span class="sxs-lookup"><span data-stu-id="e0d43-115">filter</span></span> | <span data-ttu-id="e0d43-116">object</span><span class="sxs-lookup"><span data-stu-id="e0d43-116">object</span></span> | <span data-ttu-id="e0d43-117">Необязательное поле для фильтрации hello типов событий.</span><span class="sxs-lookup"><span data-stu-id="e0d43-117">An optional field for filtering hello types of events.</span></span> |

### <a name="destination-object"></a><span data-ttu-id="e0d43-118">Объект destination</span><span class="sxs-lookup"><span data-stu-id="e0d43-118">destination object</span></span>

| <span data-ttu-id="e0d43-119">Свойство</span><span class="sxs-lookup"><span data-stu-id="e0d43-119">Property</span></span> | <span data-ttu-id="e0d43-120">Тип</span><span class="sxs-lookup"><span data-stu-id="e0d43-120">Type</span></span> | <span data-ttu-id="e0d43-121">Описание</span><span class="sxs-lookup"><span data-stu-id="e0d43-121">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="e0d43-122">endpointType</span><span class="sxs-lookup"><span data-stu-id="e0d43-122">endpointType</span></span> | <span data-ttu-id="e0d43-123">string</span><span class="sxs-lookup"><span data-stu-id="e0d43-123">string</span></span> | <span data-ttu-id="e0d43-124">Hello тип конечной точки для hello подписки (веб-перехватчика/HTTP, концентратора событий или очереди).</span><span class="sxs-lookup"><span data-stu-id="e0d43-124">hello type of endpoint for hello subscription (webhook/HTTP, Event Hub, or queue).</span></span> | 
| <span data-ttu-id="e0d43-125">endpointUrl</span><span class="sxs-lookup"><span data-stu-id="e0d43-125">endpointUrl</span></span> | <span data-ttu-id="e0d43-126">string</span><span class="sxs-lookup"><span data-stu-id="e0d43-126">string</span></span> |  | 

### <a name="filter-object"></a><span data-ttu-id="e0d43-127">Объект filter</span><span class="sxs-lookup"><span data-stu-id="e0d43-127">filter object</span></span>

| <span data-ttu-id="e0d43-128">Свойство</span><span class="sxs-lookup"><span data-stu-id="e0d43-128">Property</span></span> | <span data-ttu-id="e0d43-129">Тип</span><span class="sxs-lookup"><span data-stu-id="e0d43-129">Type</span></span> | <span data-ttu-id="e0d43-130">Описание</span><span class="sxs-lookup"><span data-stu-id="e0d43-130">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="e0d43-131">includedEventTypes</span><span class="sxs-lookup"><span data-stu-id="e0d43-131">includedEventTypes</span></span> | <span data-ttu-id="e0d43-132">array</span><span class="sxs-lookup"><span data-stu-id="e0d43-132">array</span></span> | <span data-ttu-id="e0d43-133">Совпадать, если тип события hello в сообщение о событии hello: точное совпадение tooone этих имен типов событий.</span><span class="sxs-lookup"><span data-stu-id="e0d43-133">Match when hello event type in hello event message is an exact match tooone of these event type names.</span></span> <span data-ttu-id="e0d43-134">Вызывает ошибку, если не совпадает с именем события hello зарегистрированные имена типов событий для источника событий hello.</span><span class="sxs-lookup"><span data-stu-id="e0d43-134">Raises an error when event name does not match hello registered event type names for hello event source.</span></span> <span data-ttu-id="e0d43-135">По умолчанию соответствует всем типам событий.</span><span class="sxs-lookup"><span data-stu-id="e0d43-135">Default matches all event types.</span></span> |
| <span data-ttu-id="e0d43-136">subjectBeginsWith</span><span class="sxs-lookup"><span data-stu-id="e0d43-136">subjectBeginsWith</span></span> | <span data-ttu-id="e0d43-137">string</span><span class="sxs-lookup"><span data-stu-id="e0d43-137">string</span></span> | <span data-ttu-id="e0d43-138">Соответствие префикса фильтра toohello поле subject hello сообщения о событии.</span><span class="sxs-lookup"><span data-stu-id="e0d43-138">A prefix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="e0d43-139">по умолчанию Hello или пустая строка соответствует всем.</span><span class="sxs-lookup"><span data-stu-id="e0d43-139">hello default or empty string matches all.</span></span> | 
| <span data-ttu-id="e0d43-140">subjectEndsWith</span><span class="sxs-lookup"><span data-stu-id="e0d43-140">subjectEndsWith</span></span> | <span data-ttu-id="e0d43-141">string</span><span class="sxs-lookup"><span data-stu-id="e0d43-141">string</span></span> | <span data-ttu-id="e0d43-142">Суффикс match фильтра toohello поле subject hello сообщения о событии.</span><span class="sxs-lookup"><span data-stu-id="e0d43-142">A suffix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="e0d43-143">по умолчанию Hello или пустая строка соответствует всем.</span><span class="sxs-lookup"><span data-stu-id="e0d43-143">hello default or empty string matches all.</span></span> |
| <span data-ttu-id="e0d43-144">subjectIsCaseSensitive</span><span class="sxs-lookup"><span data-stu-id="e0d43-144">subjectIsCaseSensitive</span></span> | <span data-ttu-id="e0d43-145">string</span><span class="sxs-lookup"><span data-stu-id="e0d43-145">string</span></span> | <span data-ttu-id="e0d43-146">Управляет сопоставлением с учетом регистра в фильтрах.</span><span class="sxs-lookup"><span data-stu-id="e0d43-146">Controls case-sensitive matching for filters.</span></span> |


## <a name="example-subscription-schema"></a><span data-ttu-id="e0d43-147">Пример схемы подписки</span><span class="sxs-lookup"><span data-stu-id="e0d43-147">Example subscription schema</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e0d43-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e0d43-148">Next steps</span></span>

* <span data-ttu-id="e0d43-149">Введение tooEvent сетки. в разделе [возможности сетки событий?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="e0d43-149">For an introduction tooEvent Grid, see [What is Event Grid?](overview.md)</span></span>
