---
title: "aaaRouting и выражения с тегами"
description: "В этом разделе рассказывается о маршрутизации и выражениях тегов для центров уведомлений Azure."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: 0fffb3bb-8ed8-4e0f-89e8-0de24a47f644
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c2c60500f7469f1cb1a73a5cf63c221a9ad6cbb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="routing-and-tag-expressions"></a><span data-ttu-id="28efa-103">Маршрутизация и выражения тегов</span><span class="sxs-lookup"><span data-stu-id="28efa-103">Routing and tag expressions</span></span>
## <a name="overview"></a><span data-ttu-id="28efa-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="28efa-104">Overview</span></span>
<span data-ttu-id="28efa-105">Выражения с тегами позволяют tootarget определенные наборы устройств или точнее, регистрации при отправке push-уведомлений через концентраторы уведомлений.</span><span class="sxs-lookup"><span data-stu-id="28efa-105">Tag expressions enable you tootarget specific sets of devices, or more specifically registrations, when sending a push notification through Notification Hubs.</span></span>

## <a name="targeting-specific-registrations"></a><span data-ttu-id="28efa-106">Выбор регистраций</span><span class="sxs-lookup"><span data-stu-id="28efa-106">Targeting specific registrations</span></span>
<span data-ttu-id="28efa-107">Hello только способом tootarget конкретных уведомление о регистрации является теги tooassociate с ними, назначить эти теги.</span><span class="sxs-lookup"><span data-stu-id="28efa-107">hello only way tootarget specific notification registrations is tooassociate tags with them, then target those tags.</span></span> <span data-ttu-id="28efa-108">Как было сказано в [управления регистрацией](notification-hubs-push-notification-registration-management.md), в порядке tooreceive отправке уведомлений приложение должно tooregister устройства обработки в концентраторе уведомлений.</span><span class="sxs-lookup"><span data-stu-id="28efa-108">As discussed in [Registration Management](notification-hubs-push-notification-registration-management.md), in order tooreceive push notifications an app has tooregister a device handle on a notification hub.</span></span> <span data-ttu-id="28efa-109">После создания регистрации в концентраторе уведомлений внутренняя служба приложения hello может отправлять уведомления tooit push.</span><span class="sxs-lookup"><span data-stu-id="28efa-109">Once a registration is created on a notification hub, hello application backend can send push notifications tooit.</span></span>
<span data-ttu-id="28efa-110">Внутренняя служба приложения Hello можно выбрать tootarget регистраций hello определенных уведомлений в hello следующих способов:</span><span class="sxs-lookup"><span data-stu-id="28efa-110">hello application backend can choose hello registrations tootarget with a specific notification in hello following ways:</span></span>

1. <span data-ttu-id="28efa-111">**Рассылка**: hello уведомление получают все регистрации в концентраторе уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="28efa-111">**Broadcast**: all registrations in hello notification hub receive hello notification.</span></span>
2. <span data-ttu-id="28efa-112">**Тег**: все регистрации, которые содержат указанный hello тег hello уведомления.</span><span class="sxs-lookup"><span data-stu-id="28efa-112">**Tag**: all registrations that contain hello specified tag receive hello notification.</span></span>
3. <span data-ttu-id="28efa-113">**Выражение с тегами**: hello уведомление получают все регистрации, которого набор тегов соответствия hello указанного выражения.</span><span class="sxs-lookup"><span data-stu-id="28efa-113">**Tag expression**: all registrations whose set of tags match hello specified expression receive hello notification.</span></span>

## <a name="tags"></a><span data-ttu-id="28efa-114">Теги</span><span class="sxs-lookup"><span data-stu-id="28efa-114">Tags</span></span>
<span data-ttu-id="28efa-115">Тег может быть любой строкой, копирование too120 символов, содержащей буквенно-цифровые и hello следующие символы, отличные от буквенно-цифровых: «_», "@", «#», ". «,»:", "-".</span><span class="sxs-lookup"><span data-stu-id="28efa-115">A tag can be any string, up too120 characters, containing alphanumeric and hello following non-alphanumeric characters: ‘_’, ‘@’, ‘#’, ‘.’, ‘:’, ‘-’.</span></span> <span data-ttu-id="28efa-116">Hello пример приложения, из которого можно получать всплывающие уведомления об определенных музыкальных группах.</span><span class="sxs-lookup"><span data-stu-id="28efa-116">hello following example shows an application from which you can receive toast notifications about specific music groups.</span></span> <span data-ttu-id="28efa-117">В этом случае уведомления tooroute простой способ — toolabel регистраций тегами различных исполнителей hello, как hello следующий рисунок.</span><span class="sxs-lookup"><span data-stu-id="28efa-117">In this scenario, a simple way tooroute notifications is toolabel registrations with tags that represent hello different bands, as in hello following picture.</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

<span data-ttu-id="28efa-118">На этом рисунке сообщение hello с тегом **Beatles** достигает только hello планшет, зарегистрированный с тегом hello **Beatles**.</span><span class="sxs-lookup"><span data-stu-id="28efa-118">In this picture, hello message tagged **Beatles** reaches only hello tablet that registered with hello tag **Beatles**.</span></span>

<span data-ttu-id="28efa-119">Дополнительные сведения о создании регистраций по тегам см. в статье [Управление регистрацией](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="28efa-119">For more information about creating registrations for tags, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

<span data-ttu-id="28efa-120">Вы можете отправить tootags уведомления с помощью hello отправлять уведомления методы hello `Microsoft.Azure.NotificationHubs.NotificationHubClient` класса в hello [концентраторы уведомлений Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span><span class="sxs-lookup"><span data-stu-id="28efa-120">You can send notifications tootags using hello send notifications methods of hello `Microsoft.Azure.NotificationHubs.NotificationHubClient` class in hello [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span></span> <span data-ttu-id="28efa-121">Также можно использовать Node.js или hello интерфейсы API REST Push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="28efa-121">You can also use Node.js, or hello Push Notifications REST APIs.</span></span>  <span data-ttu-id="28efa-122">Ниже приведен пример использования hello SDK.</span><span class="sxs-lookup"><span data-stu-id="28efa-122">Here's an example using hello SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




<span data-ttu-id="28efa-123">Теги имеют toobe предварительно подготовлены и могут ссылаться понятия toomultiple конкретного приложения.</span><span class="sxs-lookup"><span data-stu-id="28efa-123">Tags do not have toobe pre-provisioned and can refer toomultiple app-specific concepts.</span></span> <span data-ttu-id="28efa-124">Например пользователи в этом примере приложения могут комментировать исполнителей и требуется tooreceive всплывающие уведомления не только для hello комментариев по своим любимым исполнителям, но также и всех комментариев из своих друзей, независимо от того, hello аппаратного контроллера управления, на котором они комментируют.</span><span class="sxs-lookup"><span data-stu-id="28efa-124">For example, users of this example application can comment on bands and want tooreceive toasts, not only for hello comments on their favorite bands, but also for all comments from their friends, regardless of hello band on which they are commenting.</span></span> <span data-ttu-id="28efa-125">Следующий рисунок Hello показан пример такого сценария.</span><span class="sxs-lookup"><span data-stu-id="28efa-125">hello following picture shows an example of this scenario:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

<span data-ttu-id="28efa-126">На этом рисунке Алиса интересуется обновлениями для hello Beatles, а Бобу интересны обновления для hello Wailers.</span><span class="sxs-lookup"><span data-stu-id="28efa-126">In this picture, Alice is interested in updates for hello Beatles, and Bob is interested in updates for hello Wailers.</span></span> <span data-ttu-id="28efa-127">Боба также интересуют комментарии Чарли, а Чарли интересны hello Wailers.</span><span class="sxs-lookup"><span data-stu-id="28efa-127">Bob is also interested in Charlie’s comments, and Charlie is in interested in hello Wailers.</span></span> <span data-ttu-id="28efa-128">При отправке уведомления о комментарии Чарли по hello Beatles, Анна и Виктор его получения.</span><span class="sxs-lookup"><span data-stu-id="28efa-128">When a notification is sent for Charlie’s comment on hello Beatles, both Alice and Bob receive it.</span></span>

<span data-ttu-id="28efa-129">Несмотря на то, что теги могут соответствовать нескольким характеристикам сразу (например, "band_Beatles" или "follows_Charlie"), они являются простыми строками, это не свойства со значениями.</span><span class="sxs-lookup"><span data-stu-id="28efa-129">While you can encode multiple concerns in tags (for example, “band_Beatles” or “follows_Charlie”), tags are simple strings and not properties with values.</span></span> <span data-ttu-id="28efa-130">Регистрация выбирается только на hello наличие или отсутствие конкретного тега.</span><span class="sxs-lookup"><span data-stu-id="28efa-130">A registration is matched only on hello presence or absence of a specific tag.</span></span>

<span data-ttu-id="28efa-131">Полное Пошаговое руководство по как toouse тегов для отправки toointerest групп см. в разделе [последние новости](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span><span class="sxs-lookup"><span data-stu-id="28efa-131">For a full step-by-step tutorial on how toouse tags for sending toointerest groups, see [Breaking News](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span></span>

## <a name="using-tags-tootarget-users"></a><span data-ttu-id="28efa-132">С помощью тегов tootarget пользователей</span><span class="sxs-lookup"><span data-stu-id="28efa-132">Using tags tootarget users</span></span>
<span data-ttu-id="28efa-133">Теги toouse другим способом является tooidentify все устройства hello определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="28efa-133">Another way toouse tags is tooidentify all hello devices of a particular user.</span></span> <span data-ttu-id="28efa-134">Регистрации можно пометить тегом, который содержит идентификатор пользователя, как и следующий рисунок hello:</span><span class="sxs-lookup"><span data-stu-id="28efa-134">Registrations can be tagged with a tag that contains a user id, as in hello following picture:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

<span data-ttu-id="28efa-135">На этом рисунке UID: Alice тегом сообщение hello достигает с тегами UID: Alice все регистрации; Таким образом все устройства Элис.</span><span class="sxs-lookup"><span data-stu-id="28efa-135">In this picture, hello message tagged uid:Alice reaches all registrations tagged uid:Alice; hence, all of Alice’s devices.</span></span>

## <a name="tag-expressions"></a><span data-ttu-id="28efa-136">Выражения тегов</span><span class="sxs-lookup"><span data-stu-id="28efa-136">Tag expressions</span></span>
<span data-ttu-id="28efa-137">Существуют случаи, когда уведомление должно tootarget набор регистраций, идентифицируется не по одному тегу, а по логическому выражению с тегами.</span><span class="sxs-lookup"><span data-stu-id="28efa-137">There are cases in which a notification has tootarget a set of registrations that is identified not by a single tag, but by a Boolean expression on tags.</span></span>

<span data-ttu-id="28efa-138">Рассмотрим Спортивное приложение, которое отправляет Boston tooeveryone напоминание об игре между командами hello Red Sox и Cardinals.</span><span class="sxs-lookup"><span data-stu-id="28efa-138">Consider a sports application that sends a reminder tooeveryone in Boston about a game between hello Red Sox and Cardinals.</span></span> <span data-ttu-id="28efa-139">Если hello клиентское приложение регистрирует теги об интересе к командам и месту, уведомление hello должно быть целевых tooeveryone в Бостоне, интересующимся hello Red Sox или hello Cardinals.</span><span class="sxs-lookup"><span data-stu-id="28efa-139">If hello client app registers tags about interest in teams and location, then hello notification should be targeted tooeveryone in Boston who is interested in either hello Red Sox or hello Cardinals.</span></span> <span data-ttu-id="28efa-140">Это условие может быть выражено с hello следующее логическое выражение:</span><span class="sxs-lookup"><span data-stu-id="28efa-140">This condition can be expressed with hello following Boolean expression:</span></span>

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

<span data-ttu-id="28efa-141">Выражения тегов могут содержать любые логические операторы, такие как AND (&&), OR (||) и NOT (!).</span><span class="sxs-lookup"><span data-stu-id="28efa-141">Tag expressions can contain all Boolean operators, such as AND (&&), OR (||), and NOT (!).</span></span> <span data-ttu-id="28efa-142">В них также можно использовать скобки.</span><span class="sxs-lookup"><span data-stu-id="28efa-142">They can also contain parentheses.</span></span> <span data-ttu-id="28efa-143">Выражения с тегами являются ограниченные too20 тегами, если они содержат только операторы OR, то; в противном случае они не ограниченной too6 тегов.</span><span class="sxs-lookup"><span data-stu-id="28efa-143">Tag expressions are limited too20 tags if they contain only ORs; otherwise they are limited too6 tags.</span></span>

<span data-ttu-id="28efa-144">Ниже приведен пример отправки уведомлений с помощью выражения с тегами с помощью пакета SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="28efa-144">Here's an example for sending notifications with tag expressions using hello SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    String userTag = "(location_Boston && !follows_Cardinals)";    

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You want info on hello Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You want info on hello Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
