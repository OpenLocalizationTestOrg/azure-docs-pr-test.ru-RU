---
title: "aaaAzure сетки событий доставки и повторите попытку"
description: "В статье описывается, как сетка событий Azure передает события и обрабатывает недоставленные сообщения."
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: 874b3bf8892fbf803ef40f29d0ec10eb50150916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-message-delivery-and-retry"></a><span data-ttu-id="37b74-103">Доставка и повторные попытки доставки сообщений сетки событий</span><span class="sxs-lookup"><span data-stu-id="37b74-103">Event Grid message delivery and retry</span></span> 

<span data-ttu-id="37b74-104">В этой статье описывается, как сетка событий Azure обрабатывает события, когда доставка не подтверждена.</span><span class="sxs-lookup"><span data-stu-id="37b74-104">This article describes how Azure Event Grid handles events when delivery is not acknowledged.</span></span>

<span data-ttu-id="37b74-105">Сетка событий обеспечивает надежную доставку.</span><span class="sxs-lookup"><span data-stu-id="37b74-105">Event Grid provides durable delivery.</span></span> <span data-ttu-id="37b74-106">Она обеспечивает доставку каждого сообщения по крайней мере один раз для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="37b74-106">It delivers each message at least once for each subscription.</span></span> <span data-ttu-id="37b74-107">События веб-перехватчика toohello зарегистрированные каждой подписки отправляются немедленно.</span><span class="sxs-lookup"><span data-stu-id="37b74-107">Events are sent toohello registered webhook of each subscription immediately.</span></span> <span data-ttu-id="37b74-108">Если веб-перехватчика не подтверждения получения события в течение 60 секунд доставки первой hello попыток, сетки событий повторных попыток доставки hello события.</span><span class="sxs-lookup"><span data-stu-id="37b74-108">If a webhook does not acknowledge receipt of an event within 60 seconds of hello first delivery attempt, Event Grid retries delivery of hello event.</span></span>

## <a name="message-delivery-status"></a><span data-ttu-id="37b74-109">Состояние доставки сообщения</span><span class="sxs-lookup"><span data-stu-id="37b74-109">Message delivery status</span></span>

<span data-ttu-id="37b74-110">Сетка событий использует HTTP ответа коды tooacknowledge поступления событий.</span><span class="sxs-lookup"><span data-stu-id="37b74-110">Event Grid uses HTTP response codes tooacknowledge receipt of events.</span></span> 

### <a name="success-codes"></a><span data-ttu-id="37b74-111">Коды успешной доставки</span><span class="sxs-lookup"><span data-stu-id="37b74-111">Success codes</span></span>

<span data-ttu-id="37b74-112">Hello следующие коды ответа HTTP указать, что событие было предоставлено успешно tooyour веб-перехватчика.</span><span class="sxs-lookup"><span data-stu-id="37b74-112">hello following HTTP response codes indicate that an event has been delivered successfully tooyour webhook.</span></span> <span data-ttu-id="37b74-113">В этом случае сетка события считает доставку выполненной.</span><span class="sxs-lookup"><span data-stu-id="37b74-113">Event Grid considers delivery complete.</span></span>

- <span data-ttu-id="37b74-114">200 ОК</span><span class="sxs-lookup"><span data-stu-id="37b74-114">200 OK</span></span>
- <span data-ttu-id="37b74-115">202 — принято</span><span class="sxs-lookup"><span data-stu-id="37b74-115">202 Accepted</span></span>

### <a name="failure-codes"></a><span data-ttu-id="37b74-116">Коды сбоя доставки</span><span class="sxs-lookup"><span data-stu-id="37b74-116">Failure codes</span></span>

<span data-ttu-id="37b74-117">следующие коды ответа HTTP Hello сообщение, что попытка доставки событий.</span><span class="sxs-lookup"><span data-stu-id="37b74-117">hello following HTTP response codes indicate that an event delivery attempt failed.</span></span> <span data-ttu-id="37b74-118">Сетка события повторяет попытку toosend hello событий.</span><span class="sxs-lookup"><span data-stu-id="37b74-118">Event Grid tries again toosend hello event.</span></span> 

- <span data-ttu-id="37b74-119">400 — недопустимый запрос</span><span class="sxs-lookup"><span data-stu-id="37b74-119">400 Bad Request</span></span>
- <span data-ttu-id="37b74-120">401 — недостаточно прав</span><span class="sxs-lookup"><span data-stu-id="37b74-120">401 Unauthorized</span></span>
- <span data-ttu-id="37b74-121">404 — не найдено</span><span class="sxs-lookup"><span data-stu-id="37b74-121">404 Not Found</span></span>
- <span data-ttu-id="37b74-122">408 — истекло время ожидания запроса</span><span class="sxs-lookup"><span data-stu-id="37b74-122">408 Request timeout</span></span>
- <span data-ttu-id="37b74-123">414 — слишком длинный универсальный код ресурса (URI)</span><span class="sxs-lookup"><span data-stu-id="37b74-123">414 URI Too Long</span></span>
- <span data-ttu-id="37b74-124">500 — Внутренняя ошибка сервера</span><span class="sxs-lookup"><span data-stu-id="37b74-124">500 Internal Server Error</span></span>
- <span data-ttu-id="37b74-125">503 — Служба недоступна</span><span class="sxs-lookup"><span data-stu-id="37b74-125">503 Service Unavailable</span></span>
- <span data-ttu-id="37b74-126">504 — Истекло время ожидания шлюза</span><span class="sxs-lookup"><span data-stu-id="37b74-126">504 Gateway Timeout</span></span>

<span data-ttu-id="37b74-127">Любой другой код ответа или его отсутствие указывают на сбой.</span><span class="sxs-lookup"><span data-stu-id="37b74-127">Any other response code or a lack of a response indicates a failure.</span></span> <span data-ttu-id="37b74-128">Сетка событий повторно предпринимает попытку доставки.</span><span class="sxs-lookup"><span data-stu-id="37b74-128">Event Grid retries delivery.</span></span> 

## <a name="retry-intervals"></a><span data-ttu-id="37b74-129">Интервалы повтора</span><span class="sxs-lookup"><span data-stu-id="37b74-129">Retry intervals</span></span>

<span data-ttu-id="37b74-130">Для доставки событий сетка событий использует политику экспоненциального увеличения задержки повтора.</span><span class="sxs-lookup"><span data-stu-id="37b74-130">Event Grid uses an exponential backoff retry policy for event delivery.</span></span> <span data-ttu-id="37b74-131">Если ваш веб-перехватчика не отвечает или возвращает код ошибки, события сетки повторных попыток доставки на hello следующие расписания:</span><span class="sxs-lookup"><span data-stu-id="37b74-131">If your webhook does not respond or returns a failure code, Event Grid retries delivery on hello following schedule:</span></span>

1. <span data-ttu-id="37b74-132">10 с</span><span class="sxs-lookup"><span data-stu-id="37b74-132">10 seconds</span></span>
2. <span data-ttu-id="37b74-133">30 секунд</span><span class="sxs-lookup"><span data-stu-id="37b74-133">30 seconds</span></span>
3. <span data-ttu-id="37b74-134">1 минута</span><span class="sxs-lookup"><span data-stu-id="37b74-134">1 minute</span></span>
4. <span data-ttu-id="37b74-135">5 мин</span><span class="sxs-lookup"><span data-stu-id="37b74-135">5 minutes</span></span>
5. <span data-ttu-id="37b74-136">10 минут</span><span class="sxs-lookup"><span data-stu-id="37b74-136">10 minutes</span></span>
6. <span data-ttu-id="37b74-137">30 минут</span><span class="sxs-lookup"><span data-stu-id="37b74-137">30 minutes</span></span>
7. <span data-ttu-id="37b74-138">1 час</span><span class="sxs-lookup"><span data-stu-id="37b74-138">1 hour</span></span>

<span data-ttu-id="37b74-139">Сетка события добавляет интервалы повтора tooall небольшой случайный выбор срока.</span><span class="sxs-lookup"><span data-stu-id="37b74-139">Event Grid adds a small randomization tooall retry intervals.</span></span>

## <a name="retry-duration"></a><span data-ttu-id="37b74-140">Длительность повтора</span><span class="sxs-lookup"><span data-stu-id="37b74-140">Retry duration</span></span>

<span data-ttu-id="37b74-141">Во время просмотра hello Azure сетки событий истечения срока действия все события, которые не были доставлены в течение двух часов.</span><span class="sxs-lookup"><span data-stu-id="37b74-141">During hello preview, Azure Event Grid expires all events that are not delivered within two hours.</span></span> <span data-ttu-id="37b74-142">Перед общей доступности этого времени будет Повышенная too24 часа.</span><span class="sxs-lookup"><span data-stu-id="37b74-142">Before General Availability, this time will be increased too24 hours.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="37b74-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="37b74-143">Next steps</span></span>

* <span data-ttu-id="37b74-144">Введение tooEvent сетки. в разделе [о сетки событий](overview.md).</span><span class="sxs-lookup"><span data-stu-id="37b74-144">For an introduction tooEvent Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="37b74-145">tooquickly приступить к работе с помощью сетки событий см. в разделе [Создание и маршрута пользовательские события с сеткой событий Azure](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="37b74-145">tooquickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>
