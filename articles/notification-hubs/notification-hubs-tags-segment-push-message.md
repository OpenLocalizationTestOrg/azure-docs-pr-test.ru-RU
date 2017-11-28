---
title: "Маршрутизация и выражения тегов"
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
ms.openlocfilehash: 18faa88641623e1248d6a33bc2d87099e1c9f624
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="routing-and-tag-expressions"></a><span data-ttu-id="cc1e8-103">Маршрутизация и выражения тегов</span><span class="sxs-lookup"><span data-stu-id="cc1e8-103">Routing and tag expressions</span></span>
## <a name="overview"></a><span data-ttu-id="cc1e8-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="cc1e8-104">Overview</span></span>
<span data-ttu-id="cc1e8-105">Выражения тегов позволяют выбирать определенные целевые наборы устройств, а точнее регистраций, при отправке push-уведомлений через центры уведомлений.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-105">Tag expressions enable you to target specific sets of devices, or more specifically registrations, when sending a push notification through Notification Hubs.</span></span>

## <a name="targeting-specific-registrations"></a><span data-ttu-id="cc1e8-106">Выбор регистраций</span><span class="sxs-lookup"><span data-stu-id="cc1e8-106">Targeting specific registrations</span></span>
<span data-ttu-id="cc1e8-107">Единственный способ выбрать определенные регистрации для получения уведомлений — это связать с ними теги, а затем указывать эти теги в качестве назначения.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-107">The only way to target specific notification registrations is to associate tags with them, then target those tags.</span></span> <span data-ttu-id="cc1e8-108">Как описано в статье [Управление регистрациями](notification-hubs-push-notification-registration-management.md), для получения push-уведомлений приложение должно зарегистрировать маркер устройства в центре уведомлений.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-108">As discussed in [Registration Management](notification-hubs-push-notification-registration-management.md), in order to receive push notifications an app has to register a device handle on a notification hub.</span></span> <span data-ttu-id="cc1e8-109">После создания регистрации в центре уведомлений серверная часть приложения может отправлять ей push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-109">Once a registration is created on a notification hub, the application backend can send push notifications to it.</span></span>
<span data-ttu-id="cc1e8-110">Серверная часть приложения выбирает целевые регистрации для отправки определенных уведомлений следующим образом.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-110">The application backend can choose the registrations to target with a specific notification in the following ways:</span></span>

1. <span data-ttu-id="cc1e8-111">**Широковещательная рассылка**: уведомление получают все регистрации в центре уведомлений.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-111">**Broadcast**: all registrations in the notification hub receive the notification.</span></span>
2. <span data-ttu-id="cc1e8-112">**По тегу**: уведомление получают все регистрации, которые содержат указанный тег.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-112">**Tag**: all registrations that contain the specified tag receive the notification.</span></span>
3. <span data-ttu-id="cc1e8-113">**По выражению тега**: уведомление получают все регистрации, набор тегов которых соответствует указанному выражению.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-113">**Tag expression**: all registrations whose set of tags match the specified expression receive the notification.</span></span>

## <a name="tags"></a><span data-ttu-id="cc1e8-114">Теги</span><span class="sxs-lookup"><span data-stu-id="cc1e8-114">Tags</span></span>
<span data-ttu-id="cc1e8-115">Тег может быть любой строкой, до 120 символов, содержащая буквы, цифры и следующие символы, отличные от буквенно-цифровых: «_», "@", «#», ". «,»:", "-".</span><span class="sxs-lookup"><span data-stu-id="cc1e8-115">A tag can be any string, up to 120 characters, containing alphanumeric and the following non-alphanumeric characters: ‘_’, ‘@’, ‘#’, ‘.’, ‘:’, ‘-’.</span></span> <span data-ttu-id="cc1e8-116">В следующем примере показано приложение, из которого можно получать всплывающие уведомления об определенных музыкальных группах.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-116">The following example shows an application from which you can receive toast notifications about specific music groups.</span></span> <span data-ttu-id="cc1e8-117">В этом случае для маршрутизации уведомлений удобно пометить регистрации тегами различных групп, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-117">In this scenario, a simple way to route notifications is to label registrations with tags that represent the different bands, as in the following picture.</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

<span data-ttu-id="cc1e8-118">На этом рисунке сообщение с тегом **Beatles** поступает только на планшет, зарегистрированный с тегом **Beatles**.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-118">In this picture, the message tagged **Beatles** reaches only the tablet that registered with the tag **Beatles**.</span></span>

<span data-ttu-id="cc1e8-119">Дополнительные сведения о создании регистраций по тегам см. в статье [Управление регистрацией](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="cc1e8-119">For more information about creating registrations for tags, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

<span data-ttu-id="cc1e8-120">Можно отправлять уведомления для тегов, используя методы отправки уведомлений класса `Microsoft.Azure.NotificationHubs.NotificationHubClient` из пакета SDK [центров уведомлений Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) .</span><span class="sxs-lookup"><span data-stu-id="cc1e8-120">You can send notifications to tags using the send notifications methods of the `Microsoft.Azure.NotificationHubs.NotificationHubClient` class in the [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span></span> <span data-ttu-id="cc1e8-121">Также можно использовать Node.js или интерфейсы API REST push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-121">You can also use Node.js, or the Push Notifications REST APIs.</span></span>  <span data-ttu-id="cc1e8-122">Ниже приведен пример с использованием пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-122">Here's an example using the SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




<span data-ttu-id="cc1e8-123">Теги необязательно определяются заранее и могут быть связаны с несколькими аспектами приложения.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-123">Tags do not have to be pre-provisioned and can refer to multiple app-specific concepts.</span></span> <span data-ttu-id="cc1e8-124">Например, пользователи приложения из этого примера могут оставлять свои комментарии по группам и хотят получать всплывающие уведомления не только о комментариях по своим любимым группам, но и обо всех комментариях от своих друзей, независимо от того, какую группу они комментируют.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-124">For example, users of this example application can comment on bands and want to receive toasts, not only for the comments on their favorite bands, but also for all comments from their friends, regardless of the band on which they are commenting.</span></span> <span data-ttu-id="cc1e8-125">На рисунке ниже показан пример такого сценария.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-125">The following picture shows an example of this scenario:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

<span data-ttu-id="cc1e8-126">На этом рисунке Алиса интересуется новостями о Beatles, а Боб — о Wailers.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-126">In this picture, Alice is interested in updates for the Beatles, and Bob is interested in updates for the Wailers.</span></span> <span data-ttu-id="cc1e8-127">Боба также интересуют комментарии Чарли, а Чарли интересуется Wailers.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-127">Bob is also interested in Charlie’s comments, and Charlie is in interested in the Wailers.</span></span> <span data-ttu-id="cc1e8-128">Когда отправляется уведомление о комментарии Чарли по Beatles, его получают и Алиса, и Боб.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-128">When a notification is sent for Charlie’s comment on the Beatles, both Alice and Bob receive it.</span></span>

<span data-ttu-id="cc1e8-129">Несмотря на то, что теги могут соответствовать нескольким характеристикам сразу (например, "band_Beatles" или "follows_Charlie"), они являются простыми строками, это не свойства со значениями.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-129">While you can encode multiple concerns in tags (for example, “band_Beatles” or “follows_Charlie”), tags are simple strings and not properties with values.</span></span> <span data-ttu-id="cc1e8-130">Успешное сопоставление с регистрацией происходит только при наличии или отсутствии конкретного тега.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-130">A registration is matched only on the presence or absence of a specific tag.</span></span>

<span data-ttu-id="cc1e8-131">Полное пошаговое руководство по использованию тегов для отправки сообщений по группам интересов см. в статье [Использование Центров уведомлений для передачи экстренных новостей](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span><span class="sxs-lookup"><span data-stu-id="cc1e8-131">For a full step-by-step tutorial on how to use tags for sending to interest groups, see [Breaking News](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span></span>

## <a name="using-tags-to-target-users"></a><span data-ttu-id="cc1e8-132">Использование тегов для выбора конечных пользователей</span><span class="sxs-lookup"><span data-stu-id="cc1e8-132">Using tags to target users</span></span>
<span data-ttu-id="cc1e8-133">Теги также могут использоваться для идентификации всех устройств определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-133">Another way to use tags is to identify all the devices of a particular user.</span></span> <span data-ttu-id="cc1e8-134">Регистрации можно пометить тегом, который содержит идентификатор пользователя, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-134">Registrations can be tagged with a tag that contains a user id, as in the following picture:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

<span data-ttu-id="cc1e8-135">На этом рисунке сообщение с тегом Alice поступает во все регистрации с тегом Alice, то есть на все устройства Алисы.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-135">In this picture, the message tagged uid:Alice reaches all registrations tagged uid:Alice; hence, all of Alice’s devices.</span></span>

## <a name="tag-expressions"></a><span data-ttu-id="cc1e8-136">Выражения тегов</span><span class="sxs-lookup"><span data-stu-id="cc1e8-136">Tag expressions</span></span>
<span data-ttu-id="cc1e8-137">Бывают случаи, когда уведомление должно направляться в ряд регистраций, которые определяются не одним тегом, а логическим выражением с тегами.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-137">There are cases in which a notification has to target a set of registrations that is identified not by a single tag, but by a Boolean expression on tags.</span></span>

<span data-ttu-id="cc1e8-138">Рассмотрим спортивное приложение, которое отправляет напоминание всем пользователям в Бостоне об игре между командами Red Sox и Cardinals.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-138">Consider a sports application that sends a reminder to everyone in Boston about a game between the Red Sox and Cardinals.</span></span> <span data-ttu-id="cc1e8-139">Если в клиентском приложении регистрируются теги об интересе к командам и месту, то уведомление должно отправляться всем пользователям в Бостоне, интересующимся Red Sox или Cardinals.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-139">If the client app registers tags about interest in teams and location, then the notification should be targeted to everyone in Boston who is interested in either the Red Sox or the Cardinals.</span></span> <span data-ttu-id="cc1e8-140">Это условие можно задать с помощью следующего логического выражения:</span><span class="sxs-lookup"><span data-stu-id="cc1e8-140">This condition can be expressed with the following Boolean expression:</span></span>

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

<span data-ttu-id="cc1e8-141">Выражения тегов могут содержать любые логические операторы, такие как AND (&&), OR (||) и NOT (!).</span><span class="sxs-lookup"><span data-stu-id="cc1e8-141">Tag expressions can contain all Boolean operators, such as AND (&&), OR (||), and NOT (!).</span></span> <span data-ttu-id="cc1e8-142">В них также можно использовать скобки.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-142">They can also contain parentheses.</span></span> <span data-ttu-id="cc1e8-143">В выражении можно использовать не больше 20 тегов, если в нем содержатся только операторы OR; в противном случае максимальное число тегов равно 6.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-143">Tag expressions are limited to 20 tags if they contain only ORs; otherwise they are limited to 6 tags.</span></span>

<span data-ttu-id="cc1e8-144">Ниже приведен пример отправки уведомлений с помощью выражения тегов и пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="cc1e8-144">Here's an example for sending notifications with tag expressions using the SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    String userTag = "(location_Boston && !follows_Cardinals)";    

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You want info on the Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You want info on the Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
