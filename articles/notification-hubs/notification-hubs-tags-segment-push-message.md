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
# <a name="routing-and-tag-expressions"></a>Маршрутизация и выражения тегов
## <a name="overview"></a>Обзор
Выражения с тегами позволяют tootarget определенные наборы устройств или точнее, регистрации при отправке push-уведомлений через концентраторы уведомлений.

## <a name="targeting-specific-registrations"></a>Выбор регистраций
Hello только способом tootarget конкретных уведомление о регистрации является теги tooassociate с ними, назначить эти теги. Как было сказано в [управления регистрацией](notification-hubs-push-notification-registration-management.md), в порядке tooreceive отправке уведомлений приложение должно tooregister устройства обработки в концентраторе уведомлений. После создания регистрации в концентраторе уведомлений внутренняя служба приложения hello может отправлять уведомления tooit push.
Внутренняя служба приложения Hello можно выбрать tootarget регистраций hello определенных уведомлений в hello следующих способов:

1. **Рассылка**: hello уведомление получают все регистрации в концентраторе уведомлений hello.
2. **Тег**: все регистрации, которые содержат указанный hello тег hello уведомления.
3. **Выражение с тегами**: hello уведомление получают все регистрации, которого набор тегов соответствия hello указанного выражения.

## <a name="tags"></a>Теги
Тег может быть любой строкой, копирование too120 символов, содержащей буквенно-цифровые и hello следующие символы, отличные от буквенно-цифровых: «_», "@", «#», ". «,»:", "-". Hello пример приложения, из которого можно получать всплывающие уведомления об определенных музыкальных группах. В этом случае уведомления tooroute простой способ — toolabel регистраций тегами различных исполнителей hello, как hello следующий рисунок.

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

На этом рисунке сообщение hello с тегом **Beatles** достигает только hello планшет, зарегистрированный с тегом hello **Beatles**.

Дополнительные сведения о создании регистраций по тегам см. в статье [Управление регистрацией](notification-hubs-push-notification-registration-management.md).

Вы можете отправить tootags уведомления с помощью hello отправлять уведомления методы hello `Microsoft.Azure.NotificationHubs.NotificationHubClient` класса в hello [концентраторы уведомлений Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK. Также можно использовать Node.js или hello интерфейсы API REST Push-уведомлений.  Ниже приведен пример использования hello SDK.

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




Теги имеют toobe предварительно подготовлены и могут ссылаться понятия toomultiple конкретного приложения. Например пользователи в этом примере приложения могут комментировать исполнителей и требуется tooreceive всплывающие уведомления не только для hello комментариев по своим любимым исполнителям, но также и всех комментариев из своих друзей, независимо от того, hello аппаратного контроллера управления, на котором они комментируют. Следующий рисунок Hello показан пример такого сценария.

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

На этом рисунке Алиса интересуется обновлениями для hello Beatles, а Бобу интересны обновления для hello Wailers. Боба также интересуют комментарии Чарли, а Чарли интересны hello Wailers. При отправке уведомления о комментарии Чарли по hello Beatles, Анна и Виктор его получения.

Несмотря на то, что теги могут соответствовать нескольким характеристикам сразу (например, "band_Beatles" или "follows_Charlie"), они являются простыми строками, это не свойства со значениями. Регистрация выбирается только на hello наличие или отсутствие конкретного тега.

Полное Пошаговое руководство по как toouse тегов для отправки toointerest групп см. в разделе [последние новости](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).

## <a name="using-tags-tootarget-users"></a>С помощью тегов tootarget пользователей
Теги toouse другим способом является tooidentify все устройства hello определенного пользователя. Регистрации можно пометить тегом, который содержит идентификатор пользователя, как и следующий рисунок hello:

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

На этом рисунке UID: Alice тегом сообщение hello достигает с тегами UID: Alice все регистрации; Таким образом все устройства Элис.

## <a name="tag-expressions"></a>Выражения тегов
Существуют случаи, когда уведомление должно tootarget набор регистраций, идентифицируется не по одному тегу, а по логическому выражению с тегами.

Рассмотрим Спортивное приложение, которое отправляет Boston tooeveryone напоминание об игре между командами hello Red Sox и Cardinals. Если hello клиентское приложение регистрирует теги об интересе к командам и месту, уведомление hello должно быть целевых tooeveryone в Бостоне, интересующимся hello Red Sox или hello Cardinals. Это условие может быть выражено с hello следующее логическое выражение:

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

Выражения тегов могут содержать любые логические операторы, такие как AND (&&), OR (||) и NOT (!). В них также можно использовать скобки. Выражения с тегами являются ограниченные too20 тегами, если они содержат только операторы OR, то; в противном случае они не ограниченной too6 тегов.

Ниже приведен пример отправки уведомлений с помощью выражения с тегами с помощью пакета SDK для hello.

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
