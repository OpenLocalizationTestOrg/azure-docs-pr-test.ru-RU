---
title: "уведомлений о запланированных aaaHow toosend | Документы Microsoft"
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
ms.openlocfilehash: 9b3ba715dad6f5d824a615e83f2863b0db47b533
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-send-scheduled-notifications"></a><span data-ttu-id="b4172-104">Практическое руководство. Отправка запланированных уведомлений</span><span class="sxs-lookup"><span data-stu-id="b4172-104">How To: Send scheduled notifications</span></span>
## <a name="overview"></a><span data-ttu-id="b4172-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="b4172-105">Overview</span></span>
<span data-ttu-id="b4172-106">Если у вас есть сценарии, в котором требуется будущих toosend уведомление в определенный момент hello, но нет toowake простой способ копирования уведомления hello toosend серверного кода.</span><span class="sxs-lookup"><span data-stu-id="b4172-106">If you have a scenario in which you want toosend a notification at some point in hello future, but do not have an easy way toowake up your back-end code toosend hello notification.</span></span> <span data-ttu-id="b4172-107">Уровень Standard концентраторов уведомлений поддерживает функцию, которая позволяет вам уведомления tooschedule копирование too7 дней в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="b4172-107">Standard tier Notification Hubs supports a feature that enables you tooschedule notifications up too7 days in hello future.</span></span>

<span data-ttu-id="b4172-108">При отправке уведомления просто используйте hello [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) класса в hello SDK концентраторов уведомлений, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="b4172-108">When sending a notification, simply use hello [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) class in hello Notification Hubs SDK as shown in hello following example:</span></span>

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

<span data-ttu-id="b4172-109">Кроме того, вы можете отменить ранее запланированное уведомление, используя его notificationId.</span><span class="sxs-lookup"><span data-stu-id="b4172-109">Also, you can cancel a previously scheduled notification using its notificationId:</span></span>

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

<span data-ttu-id="b4172-110">Нет никаких ограничений на количество запланированных уведомлений, которые можно отправить в hello.</span><span class="sxs-lookup"><span data-stu-id="b4172-110">There are no limits on hello number of scheduled notifications you can send.</span></span>

