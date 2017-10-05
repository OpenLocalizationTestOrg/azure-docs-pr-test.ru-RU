---
title: "Как отправлять запланированные уведомления | Документация Майкрософт"
description: "В этом разделе описывается использование запланированных уведомлений с помощью центров уведомлений Azure."
services: notification-hubs
documentationcenter: .net
keywords: "push-уведомления, push-уведомление, планирование push-уведомлений"
author: ysxu
manager: erikre
editor: 
ms.assetid: 6b718c75-75dd-4c99-aee3-db1288235c1a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: efac6e1ecc00359f1622d380333140bc055c83e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-scheduled-notifications"></a><span data-ttu-id="6e901-104">Практическое руководство. Отправка запланированных уведомлений</span><span class="sxs-lookup"><span data-stu-id="6e901-104">How To: Send scheduled notifications</span></span>
## <a name="overview"></a><span data-ttu-id="6e901-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="6e901-105">Overview</span></span>
<span data-ttu-id="6e901-106">Предположим, возникла необходимость отправить уведомление в какой-либо момент в будущем, но у вас нет простого способа пробудить внутренней код для отправки уведомления.</span><span class="sxs-lookup"><span data-stu-id="6e901-106">If you have a scenario in which you want to send a notification at some point in the future, but do not have an easy way to wake up your back-end code to send the notification.</span></span> <span data-ttu-id="6e901-107">Центры уведомлений уровня "Стандартный" поддерживает функцию, которая позволяет запланировать уведомления на будущее до 7 дней.</span><span class="sxs-lookup"><span data-stu-id="6e901-107">Standard tier Notification Hubs supports a feature that enables you to schedule notifications up to 7 days in the future.</span></span>

<span data-ttu-id="6e901-108">При отправке уведомления просто используйте класс [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) из пакета SDK центров уведомлений, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="6e901-108">When sending a notification, simply use the [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) class in the Notification Hubs SDK as shown in the following example:</span></span>

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

<span data-ttu-id="6e901-109">Кроме того, вы можете отменить ранее запланированное уведомление, используя его notificationId.</span><span class="sxs-lookup"><span data-stu-id="6e901-109">Also, you can cancel a previously scheduled notification using its notificationId:</span></span>

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

<span data-ttu-id="6e901-110">Количество запланированных уведомлений, которые можно отправлять, не ограничено.</span><span class="sxs-lookup"><span data-stu-id="6e901-110">There are no limits on the number of scheduled notifications you can send.</span></span>

