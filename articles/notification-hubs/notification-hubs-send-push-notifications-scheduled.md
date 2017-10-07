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
# <a name="how-to-send-scheduled-notifications"></a>Практическое руководство. Отправка запланированных уведомлений
## <a name="overview"></a>Обзор
Если у вас есть сценарии, в котором требуется будущих toosend уведомление в определенный момент hello, но нет toowake простой способ копирования уведомления hello toosend серверного кода. Уровень Standard концентраторов уведомлений поддерживает функцию, которая позволяет вам уведомления tooschedule копирование too7 дней в будущем hello.

При отправке уведомления просто используйте hello [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) класса в hello SDK концентраторов уведомлений, как показано в следующий пример hello:

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

Кроме того, вы можете отменить ранее запланированное уведомление, используя его notificationId.

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

Нет никаких ограничений на количество запланированных уведомлений, которые можно отправить в hello.

