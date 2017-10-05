---
title: "Схема подписки для службы \"Сетка событий Azure\""
description: "В этой статье описаны свойства для подписки на событие в службе \"Сетка событий Azure\"."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: eff2352066a76010d6d882a7b7e1961870cd2d46
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="event-grid-subscription-schema"></a><span data-ttu-id="26d43-103">Схема подписки для службы "Сетка событий"</span><span class="sxs-lookup"><span data-stu-id="26d43-103">Event Grid subscription schema</span></span>

<span data-ttu-id="26d43-104">Чтобы создать подписку для службы "Сетка событий", отправьте запрос на выполнение операции по созданию подписки на события.</span><span class="sxs-lookup"><span data-stu-id="26d43-104">To create an Event Grid subscription, you send a request to the Create Event subscription operation.</span></span> <span data-ttu-id="26d43-105">Используйте следующий формат:</span><span class="sxs-lookup"><span data-stu-id="26d43-105">Use the following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="26d43-106">Например, чтобы создать подписку на события для учетной записи хранения с именем `examplestorage` в группе ресурсов `examplegroup`, используйте следующий формат:</span><span class="sxs-lookup"><span data-stu-id="26d43-106">For example, to create an event subscription for a storage account named `examplestorage` in a resource group named `examplegroup`, use the following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="26d43-107">В этой статье приведены свойства и схема для основного текста запроса.</span><span class="sxs-lookup"><span data-stu-id="26d43-107">The article describes the properties and schema for the body of the request.</span></span>
 
## <a name="event-subscription-properties"></a><span data-ttu-id="26d43-108">Свойства подписки на события</span><span class="sxs-lookup"><span data-stu-id="26d43-108">Event subscription properties</span></span>

| <span data-ttu-id="26d43-109">Свойство</span><span class="sxs-lookup"><span data-stu-id="26d43-109">Property</span></span> | <span data-ttu-id="26d43-110">Тип</span><span class="sxs-lookup"><span data-stu-id="26d43-110">Type</span></span> | <span data-ttu-id="26d43-111">Описание</span><span class="sxs-lookup"><span data-stu-id="26d43-111">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="26d43-112">ресурс destination</span><span class="sxs-lookup"><span data-stu-id="26d43-112">destination</span></span> | <span data-ttu-id="26d43-113">object</span><span class="sxs-lookup"><span data-stu-id="26d43-113">object</span></span> | <span data-ttu-id="26d43-114">Объект, который определяет конечную точку.</span><span class="sxs-lookup"><span data-stu-id="26d43-114">The object that defines the endpoint.</span></span> |
| <span data-ttu-id="26d43-115">фильтр</span><span class="sxs-lookup"><span data-stu-id="26d43-115">filter</span></span> | <span data-ttu-id="26d43-116">object</span><span class="sxs-lookup"><span data-stu-id="26d43-116">object</span></span> | <span data-ttu-id="26d43-117">Необязательное поле для фильтрации событий по типам.</span><span class="sxs-lookup"><span data-stu-id="26d43-117">An optional field for filtering the types of events.</span></span> |

### <a name="destination-object"></a><span data-ttu-id="26d43-118">Объект destination</span><span class="sxs-lookup"><span data-stu-id="26d43-118">destination object</span></span>

| <span data-ttu-id="26d43-119">Свойство</span><span class="sxs-lookup"><span data-stu-id="26d43-119">Property</span></span> | <span data-ttu-id="26d43-120">Тип</span><span class="sxs-lookup"><span data-stu-id="26d43-120">Type</span></span> | <span data-ttu-id="26d43-121">Описание</span><span class="sxs-lookup"><span data-stu-id="26d43-121">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="26d43-122">endpointType</span><span class="sxs-lookup"><span data-stu-id="26d43-122">endpointType</span></span> | <span data-ttu-id="26d43-123">string</span><span class="sxs-lookup"><span data-stu-id="26d43-123">string</span></span> | <span data-ttu-id="26d43-124">Тип конечной точки для подписки (веб-перехватчик или HTTP, концентратор событий либо очередь).</span><span class="sxs-lookup"><span data-stu-id="26d43-124">The type of endpoint for the subscription (webhook/HTTP, Event Hub, or queue).</span></span> | 
| <span data-ttu-id="26d43-125">endpointUrl</span><span class="sxs-lookup"><span data-stu-id="26d43-125">endpointUrl</span></span> | <span data-ttu-id="26d43-126">string</span><span class="sxs-lookup"><span data-stu-id="26d43-126">string</span></span> |  | 

### <a name="filter-object"></a><span data-ttu-id="26d43-127">Объект filter</span><span class="sxs-lookup"><span data-stu-id="26d43-127">filter object</span></span>

| <span data-ttu-id="26d43-128">Свойство</span><span class="sxs-lookup"><span data-stu-id="26d43-128">Property</span></span> | <span data-ttu-id="26d43-129">Тип</span><span class="sxs-lookup"><span data-stu-id="26d43-129">Type</span></span> | <span data-ttu-id="26d43-130">Описание</span><span class="sxs-lookup"><span data-stu-id="26d43-130">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="26d43-131">includedEventTypes</span><span class="sxs-lookup"><span data-stu-id="26d43-131">includedEventTypes</span></span> | <span data-ttu-id="26d43-132">array</span><span class="sxs-lookup"><span data-stu-id="26d43-132">array</span></span> | <span data-ttu-id="26d43-133">Выполняет сопоставление, если тип события, указанный в сообщении о событии, полностью соответствует одному из этих типов.</span><span class="sxs-lookup"><span data-stu-id="26d43-133">Match when the event type in the event message is an exact match to one of these event type names.</span></span> <span data-ttu-id="26d43-134">Вызывает ошибку, если имя события не соответствует зарегистрированному имени типа для источника события.</span><span class="sxs-lookup"><span data-stu-id="26d43-134">Raises an error when event name does not match the registered event type names for the event source.</span></span> <span data-ttu-id="26d43-135">По умолчанию соответствует всем типам событий.</span><span class="sxs-lookup"><span data-stu-id="26d43-135">Default matches all event types.</span></span> |
| <span data-ttu-id="26d43-136">subjectBeginsWith</span><span class="sxs-lookup"><span data-stu-id="26d43-136">subjectBeginsWith</span></span> | <span data-ttu-id="26d43-137">string</span><span class="sxs-lookup"><span data-stu-id="26d43-137">string</span></span> | <span data-ttu-id="26d43-138">Фильтр соответствия префиксу для поля темы в сообщении о событии.</span><span class="sxs-lookup"><span data-stu-id="26d43-138">A prefix-match filter to the subject field in the event message.</span></span> <span data-ttu-id="26d43-139">Строка по умолчанию или пустая строка соответствует всем типам.</span><span class="sxs-lookup"><span data-stu-id="26d43-139">The default or empty string matches all.</span></span> | 
| <span data-ttu-id="26d43-140">subjectEndsWith</span><span class="sxs-lookup"><span data-stu-id="26d43-140">subjectEndsWith</span></span> | <span data-ttu-id="26d43-141">string</span><span class="sxs-lookup"><span data-stu-id="26d43-141">string</span></span> | <span data-ttu-id="26d43-142">Фильтр соответствия суффиксу для поля темы в сообщении о событии.</span><span class="sxs-lookup"><span data-stu-id="26d43-142">A suffix-match filter to the subject field in the event message.</span></span> <span data-ttu-id="26d43-143">Строка по умолчанию или пустая строка соответствует всем типам.</span><span class="sxs-lookup"><span data-stu-id="26d43-143">The default or empty string matches all.</span></span> |
| <span data-ttu-id="26d43-144">subjectIsCaseSensitive</span><span class="sxs-lookup"><span data-stu-id="26d43-144">subjectIsCaseSensitive</span></span> | <span data-ttu-id="26d43-145">string</span><span class="sxs-lookup"><span data-stu-id="26d43-145">string</span></span> | <span data-ttu-id="26d43-146">Управляет сопоставлением с учетом регистра в фильтрах.</span><span class="sxs-lookup"><span data-stu-id="26d43-146">Controls case-sensitive matching for filters.</span></span> |


## <a name="example-subscription-schema"></a><span data-ttu-id="26d43-147">Пример схемы подписки</span><span class="sxs-lookup"><span data-stu-id="26d43-147">Example subscription schema</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="26d43-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="26d43-148">Next steps</span></span>

* <span data-ttu-id="26d43-149">См. дополнительные сведения о [службе "Сетка событий Azure"](overview.md).</span><span class="sxs-lookup"><span data-stu-id="26d43-149">For an introduction to Event Grid, see [What is Event Grid?](overview.md)</span></span>