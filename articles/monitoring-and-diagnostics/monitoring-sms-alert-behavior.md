---
title: "поведение предупреждения aaaSMS в группы действий | Документы Microsoft"
description: "Формат SMS-сообщений и отвечает на запросы toounsubscribe tooSMS сообщения, исключение: или обращаться за помощью."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 3cd09b1903e3472f6402f62b74409d97e7e7ea97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a><span data-ttu-id="b7fcf-103">Поведение SMS-оповещений в группе действий</span><span class="sxs-lookup"><span data-stu-id="b7fcf-103">SMS Alert Behavior in Action Groups</span></span>
## <a name="overview"></a><span data-ttu-id="b7fcf-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="b7fcf-104">Overview</span></span> ##
<span data-ttu-id="b7fcf-105">Группы действий позволяют tooconfigure список получателей.</span><span class="sxs-lookup"><span data-stu-id="b7fcf-105">Action groups enable you tooconfigure a list of receivers.</span></span> <span data-ttu-id="b7fcf-106">Затем можно использовать эти группы, при определении предупреждения журнала действий; Проверка того, что группа определенное действие получает уведомление при активации оповещения журнала действие hello.</span><span class="sxs-lookup"><span data-stu-id="b7fcf-106">These groups can then be leveraged when defining activity log alerts; ensuring that a particular action group is notified when hello activity log alert is triggered.</span></span> <span data-ttu-id="b7fcf-107">Одно из предупреждений поддерживается механизмы hello — SMS; оповещения Hello поддерживают двунаправленный обмен данными.</span><span class="sxs-lookup"><span data-stu-id="b7fcf-107">One of hello alerting mechanisms supported is SMS; hello alerts support bi-directional communication.</span></span> <span data-ttu-id="b7fcf-108">Пользователь может реагировать предупреждение tooan:</span><span class="sxs-lookup"><span data-stu-id="b7fcf-108">A user can respond tooan alert to:</span></span>

- <span data-ttu-id="b7fcf-109">**Отменить подписку на оповещения**. Пользователь может отменить подписку на все SMS-оповещения для всех групп действий или для отдельной группы действий.</span><span class="sxs-lookup"><span data-stu-id="b7fcf-109">**Unsubscribe from alerts:** A user can unsubscribe from all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="b7fcf-110">**Исключение: tooalerts:** пользователь может исключение: tooall SMS предупреждения для всех групп действий или группы действий в единственном числе.</span><span class="sxs-lookup"><span data-stu-id="b7fcf-110">**Resubscribe tooalerts:** A user can resubscribe tooall SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="b7fcf-111">**Запрашивать помощь:** пользователь может запросить дополнительные сведения о hello SMS.</span><span class="sxs-lookup"><span data-stu-id="b7fcf-111">**Request help:** A user can ask for more information on hello SMS.</span></span> <span data-ttu-id="b7fcf-112">Они будут перенаправленный toothis статьи</span><span class="sxs-lookup"><span data-stu-id="b7fcf-112">They will be redirected toothis article</span></span>

<span data-ttu-id="b7fcf-113">Эта статья описывает поведение hello hello SMS оповещений и hello ответа действия hello пользователь может предпринять на основе языковых стандартов hello hello пользователя на:</span><span class="sxs-lookup"><span data-stu-id="b7fcf-113">This article covers hello behavior of hello SMS alerts and hello response actions hello user can take based on hello locale of hello user:</span></span>

## <a name="usacanada-sms-behavior"></a><span data-ttu-id="b7fcf-114">SMS-оповещения в США и Канаде</span><span class="sxs-lookup"><span data-stu-id="b7fcf-114">USA/Canada SMS behavior</span></span>
### <a name="receiving-an-sms-alert"></a><span data-ttu-id="b7fcf-115">Получение SMS-оповещения</span><span class="sxs-lookup"><span data-stu-id="b7fcf-115">Receiving an SMS Alert</span></span>
<span data-ttu-id="b7fcf-116">Получатель SMS, настроенный в группе действий, получит SMS при активации оповещения.</span><span class="sxs-lookup"><span data-stu-id="b7fcf-116">An SMS receiver, who is configured as part of an action group, will receive an SMS when an alert fires.</span></span> <span data-ttu-id="b7fcf-117">Hello SMS будет нести hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="b7fcf-117">hello SMS will carry hello following information:</span></span>
* <span data-ttu-id="b7fcf-118">Короткого имени группы действий hello было отправлено это предупреждение</span><span class="sxs-lookup"><span data-stu-id="b7fcf-118">Shortname of hello action group this alert was sent to</span></span>
- <span data-ttu-id="b7fcf-119">Заголовок оповещения hello</span><span class="sxs-lookup"><span data-stu-id="b7fcf-119">Title of hello alert</span></span>

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a><span data-ttu-id="b7fcf-120">Отмена подписки на SMS-оповещения для отдельной группы действий</span><span class="sxs-lookup"><span data-stu-id="b7fcf-120">Unsubscribing from SMS alerts for one action group</span></span>
<span data-ttu-id="b7fcf-121">Пользователь отказаться от получения SMS для предупреждения для одного действия группы с отвечает shortcode toohello 20873 с ключевыми словами hello: «отключить &lt;короткого имени группы действий&gt;».</span><span class="sxs-lookup"><span data-stu-id="b7fcf-121">A user can unsubscribe from SMS for alerts for one action group by responding toohello shortcode 20873 with hello keywords: “DISABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="b7fcf-122">Например,</span><span class="sxs-lookup"><span data-stu-id="b7fcf-122">Ex.</span></span> <span data-ttu-id="b7fcf-123">Пользователь, который toounsubscribe на основе предупреждений для группы действий с hello shortname «Azure» отправляла shortcode toohello SMS 20873 с надписью «Отключить Azure»</span><span class="sxs-lookup"><span data-stu-id="b7fcf-123">A user wishing toounsubscribe from alerts for an action group with hello shortname “Azure”, would send an SMS toohello shortcode 20873 that says “DISABLE Azure”</span></span>

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a><span data-ttu-id="b7fcf-124">Отмена подписки на SMS-оповещения для всех групп действий</span><span class="sxs-lookup"><span data-stu-id="b7fcf-124">Unsubscribing from SMS alerts for all action groups</span></span>
<span data-ttu-id="b7fcf-125">Пользователь отказаться от получения все SMS предупреждения для всех групп действий по отвечает shortcode toohello 20873 с любым из следующих ключевых слов hello:</span><span class="sxs-lookup"><span data-stu-id="b7fcf-125">A user can unsubscribe from all SMS alerts for all action groups by responding toohello shortcode 20873 with any of hello following keywords:</span></span>
* <span data-ttu-id="b7fcf-126">STOP</span><span class="sxs-lookup"><span data-stu-id="b7fcf-126">STOP</span></span>

<span data-ttu-id="b7fcf-127">Например,</span><span class="sxs-lookup"><span data-stu-id="b7fcf-127">Ex.</span></span> <span data-ttu-id="b7fcf-128">Пользователь, который toounsubscribe из всех SMS оповещений для всех групп действий отправляла shortcode toohello SMS 20873 с надписью «ОСТАНОВИТЬ»</span><span class="sxs-lookup"><span data-stu-id="b7fcf-128">A user wishing toounsubscribe from all SMS alerts for all action groups, would send an SMS toohello shortcode 20873 that says “STOP”</span></span>

>[!NOTE]
><span data-ttu-id="b7fcf-129">Если пользователь отменил подписку на оповещения SMS, но затем добавляется новая группа действий tooa; они будут получать предупреждения SMS для этого новая группа действий, но остаются отменена все предыдущие действия группы.</span><span class="sxs-lookup"><span data-stu-id="b7fcf-129">If a user has unsubscribed from SMS alerts, but is then added tooa new action group; they WILL receive SMS alerts for that new action group, but remain unsubscribed from all previous action groups.</span></span>
>
>

### <a name="resubscribing-toosms-alerts-for-one-action-group"></a><span data-ttu-id="b7fcf-130">Resubscribing tooSMS предупреждения для одной группы действий</span><span class="sxs-lookup"><span data-stu-id="b7fcf-130">Resubscribing tooSMS alerts for one action group</span></span>
<span data-ttu-id="b7fcf-131">Пользователь может исключение: tooSMS для оповещения для одного действия группы с отвечает shortcode toohello 20873 с ключевыми словами hello: «ВКЛЮЧИТЬ &lt;короткого имени группы действий&gt;».</span><span class="sxs-lookup"><span data-stu-id="b7fcf-131">A user can resubscribe tooSMS for alerts for one action group by responding toohello shortcode 20873 with hello keywords: “ENABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="b7fcf-132">Например,</span><span class="sxs-lookup"><span data-stu-id="b7fcf-132">Ex.</span></span> <span data-ttu-id="b7fcf-133">Пользователь, который tooalerts tooresubscribe для группы действий с hello shortname «Azure» отправляла shortcode toohello SMS 20873 с надписью «ВКЛЮЧИТЬ Azure»</span><span class="sxs-lookup"><span data-stu-id="b7fcf-133">A user wishing tooresubscribe tooalerts for an action group with hello shortname “Azure”, would send an SMS toohello shortcode 20873 that says “ENABLE Azure”</span></span>

### <a name="resubscribing-toosms-alerts-for-all-action-groups"></a><span data-ttu-id="b7fcf-134">Resubscribing tooSMS предупреждения для всех групп действий</span><span class="sxs-lookup"><span data-stu-id="b7fcf-134">Resubscribing tooSMS alerts for all action groups</span></span>
<span data-ttu-id="b7fcf-135">Пользователь может исключение: tooall SMS для оповещений для всех групп действий по отвечает shortcode toohello 20873 с любым из следующих ключевых слов hello:</span><span class="sxs-lookup"><span data-stu-id="b7fcf-135">A user can resubscribe tooall SMS for alerts for all action groups by responding toohello shortcode 20873 with any of hello following keywords:</span></span>

* <span data-ttu-id="b7fcf-136">START</span><span class="sxs-lookup"><span data-stu-id="b7fcf-136">START</span></span>

<span data-ttu-id="b7fcf-137">Например,</span><span class="sxs-lookup"><span data-stu-id="b7fcf-137">Ex.</span></span> <span data-ttu-id="b7fcf-138">Пользователь, который toounsubscribe из всех SMS оповещений для всех групп действий отправляла shortcode toohello SMS 20873 с надписью «Пуск»</span><span class="sxs-lookup"><span data-stu-id="b7fcf-138">A user wishing toounsubscribe from all SMS alerts for all action groups, would send an SMS toohello shortcode 20873 that says “START”</span></span>

### <a name="requesting-help-via-sms"></a><span data-ttu-id="b7fcf-139">Запрос справки с помощью SMS</span><span class="sxs-lookup"><span data-stu-id="b7fcf-139">Requesting help via SMS</span></span>
<span data-ttu-id="b7fcf-140">Пользователь может запросить дополнительные сведения о hello SMS, что получили по отвечает toohello shortcode 20873 с любым из следующих ключевых слов hello:</span><span class="sxs-lookup"><span data-stu-id="b7fcf-140">A user can ask for more information about hello SMS they have received by responding toohello shortcode 20873 with any of hello following keywords:</span></span>
* <span data-ttu-id="b7fcf-141">HELP</span><span class="sxs-lookup"><span data-stu-id="b7fcf-141">HELP</span></span>

<span data-ttu-id="b7fcf-142">Ответ будет отправлено toohello пользователя со статьей toothis в связи.</span><span class="sxs-lookup"><span data-stu-id="b7fcf-142">A response will be sent toohello user with a link toothis article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7fcf-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b7fcf-143">Next Steps</span></span>
<span data-ttu-id="b7fcf-144">Получить [Обзор оповещения журнала действий](monitoring-overview-alerts.md) и узнайте, как tooget оповещения</span><span class="sxs-lookup"><span data-stu-id="b7fcf-144">Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how tooget alerted</span></span>  
<span data-ttu-id="b7fcf-145">Узнайте больше об [ограничении частоты отправки SMS](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="b7fcf-145">Learn more about [SMS rate limiting](monitoring-alerts-rate-limiting.md)</span></span>  
<span data-ttu-id="b7fcf-146">Узнайте больше о [группах действий](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="b7fcf-146">Learn more about [action groups](monitoring-action-groups.md)</span></span>
