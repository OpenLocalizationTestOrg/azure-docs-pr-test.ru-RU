---
title: "Концентратор уведомлений функции привязки aaaAzure | Документы Microsoft"
description: "Понять, как привязки toouse концентратор уведомлений Azure в функциях Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, динамические вычисления, независимая архитектура"
ms.assetid: 0ff0c949-20bf-430b-8dd5-d72b7b6ee6f7
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/27/2016
ms.author: glenga
ms.openlocfilehash: d192424a8ec701d02f8bcb4aa4c1d189b20537a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-notification-hub-output-binding"></a><span data-ttu-id="f72d8-104">Выходная привязка центра уведомлений для функций Azure</span><span class="sxs-lookup"><span data-stu-id="f72d8-104">Azure Functions Notification Hub output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="f72d8-105">В этой статье объясняется, как привязки концентратор уведомлений Azure tooconfigure и код в функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="f72d8-105">This article explains how tooconfigure and code Azure Notification Hub bindings in Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="f72d8-106">Функции могут отправлять push-уведомления всего несколькими строками кода, используя настроенный центр уведомлений Azure.</span><span class="sxs-lookup"><span data-stu-id="f72d8-106">Your functions can send push notifications using a configured Azure Notification Hub with a few lines of code.</span></span> <span data-ttu-id="f72d8-107">Однако hello концентратор уведомлений Azure должны быть настроены для платформы уведомления службы (PNS) необходимо toouse hello.</span><span class="sxs-lookup"><span data-stu-id="f72d8-107">However, hello Azure Notification Hub must be configured for hello Platform Notifications Services (PNS) you want toouse.</span></span> <span data-ttu-id="f72d8-108">Дополнительные сведения о настройке концентратор уведомлений Azure и разработка клиентских приложений, которые регистрируют tooreceive уведомления см. в разделе [Приступая к работе с концентраторами уведомлений](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) и выберите целевую платформу на приветствия клиента Вверх.</span><span class="sxs-lookup"><span data-stu-id="f72d8-108">For more information on configuring an Azure Notification Hub and developing a client applications that register tooreceive notifications, see [Getting started with Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) and click your target client platform at hello top.</span></span>

<span data-ttu-id="f72d8-109">Hello уведомлений, отправляемых может быть собственный уведомления или шаблон уведомления.</span><span class="sxs-lookup"><span data-stu-id="f72d8-109">hello notifications you send can be native notifications or template notifications.</span></span> <span data-ttu-id="f72d8-110">Получения собственных уведомлений платформы уведомлений, настроенной в hello `platform` свойство hello привязка для вывода.</span><span class="sxs-lookup"><span data-stu-id="f72d8-110">Native notifications target a specific notification platform as configured in hello `platform` property of hello output binding.</span></span> <span data-ttu-id="f72d8-111">Шаблон уведомления могут быть tootarget используется несколько платформ.</span><span class="sxs-lookup"><span data-stu-id="f72d8-111">A template notification can be used tootarget multiple platforms.</span></span>   

## <a name="notification-hub-output-binding-properties"></a><span data-ttu-id="f72d8-112">Свойства привязки для вывода центра уведомлений</span><span class="sxs-lookup"><span data-stu-id="f72d8-112">Notification hub output binding properties</span></span>
<span data-ttu-id="f72d8-113">файл function.json Hello предоставляет hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="f72d8-113">hello function.json file provides hello following properties:</span></span>

* <span data-ttu-id="f72d8-114">`name`: Переменной имя, используемое в коде функция для концентратора уведомлений приветственное сообщение.</span><span class="sxs-lookup"><span data-stu-id="f72d8-114">`name` : Variable name used in function code for hello notification hub message.</span></span>
* <span data-ttu-id="f72d8-115">`type`: необходимо задать слишком*«концентратора уведомлений»*.</span><span class="sxs-lookup"><span data-stu-id="f72d8-115">`type` : must be set too*"notificationHub"*.</span></span>
* <span data-ttu-id="f72d8-116">`tagExpression`: Выражения с тегами разрешить toospecify доставить уведомления tooa набора устройств, имеющих зарегистрированные tooreceive уведомлений, которые соответствуют hello выражение тегов.</span><span class="sxs-lookup"><span data-stu-id="f72d8-116">`tagExpression` : Tag expressions allow you toospecify that notifications be delivered tooa set of devices who have registered tooreceive notifications that match hello tag expression.</span></span>  <span data-ttu-id="f72d8-117">Дополнительные сведения см. в статье [Маршрутизация и выражения тегов](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="f72d8-117">For more information, see [Routing and tag expressions](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span></span>
* <span data-ttu-id="f72d8-118">`hubName`: Имя ресурса концентратора уведомлений hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f72d8-118">`hubName` : Name of hello notification hub resource in hello Azure portal.</span></span>
* <span data-ttu-id="f72d8-119">`connection`: Строка подключения должна быть **параметр приложения** toohello задать строку подключения *DefaultFullSharedAccessSignature* значения для центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="f72d8-119">`connection` : This connection string must be an **Application Setting** connection string set toohello *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
* <span data-ttu-id="f72d8-120">`direction`: необходимо задать слишком*«out»*.</span><span class="sxs-lookup"><span data-stu-id="f72d8-120">`direction` : must be set too*"out"*.</span></span> 
* <span data-ttu-id="f72d8-121">`platform`: свойство платформы hello указывает платформу уведомления hello целей уведомления.</span><span class="sxs-lookup"><span data-stu-id="f72d8-121">`platform` : hello platform property indicates hello notification platform your notification targets.</span></span> <span data-ttu-id="f72d8-122">Должен быть hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="f72d8-122">Must be one of hello following values:</span></span>
  * <span data-ttu-id="f72d8-123">По умолчанию если выходных данных hello привязки указано свойство платформы hello шаблон уведомления может быть используется tootarget на любой платформе, настроенного на hello концентратор уведомлений Azure.</span><span class="sxs-lookup"><span data-stu-id="f72d8-123">By default, if hello platform property is omitted from hello output binding, template notifications can be used tootarget any platform configured on hello Azure Notification Hub.</span></span> <span data-ttu-id="f72d8-124">Дополнительные сведения об использовании шаблонов в целом toosend кросс-уведомлений платформы с концентратор уведомлений Azure. в разделе [шаблоны](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="f72d8-124">For more information on using templates in general toosend cross platform notifications with an Azure Notification Hub, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>
  * <span data-ttu-id="f72d8-125">`apns` — служба push-уведомлений Apple.</span><span class="sxs-lookup"><span data-stu-id="f72d8-125">`apns` : Apple Push Notification Service.</span></span> <span data-ttu-id="f72d8-126">Дополнительные сведения о настройке hello концентратора уведомлений для APNS и получение уведомления hello в клиентском приложении см. в разделе [tooiOS уведомления Принудительная отправка с концентраторами уведомлений Azure](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="f72d8-126">For more information on configuring hello notification hub for APNS and receiving hello notification in a client app, see [Sending push notifications tooiOS with Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span></span> 
  * <span data-ttu-id="f72d8-127">`adm` — [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span><span class="sxs-lookup"><span data-stu-id="f72d8-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span></span> <span data-ttu-id="f72d8-128">Дополнительные сведения о настройке hello концентратора уведомлений для ADM и получение hello уведомления в приложении Kindle см. в разделе [Приступая к работе с концентраторами уведомлений для Kindle приложений](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="f72d8-128">For more information on configuring hello notification hub for ADM and receiving hello notification in a Kindle app, see [Getting Started with Notification Hubs for Kindle apps](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span></span> 
  * <span data-ttu-id="f72d8-129">`gcm` — [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="f72d8-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span></span> <span data-ttu-id="f72d8-130">Firebase Cloud Messaging, являющийся hello новую версию GCM, также поддерживается.</span><span class="sxs-lookup"><span data-stu-id="f72d8-130">Firebase Cloud Messaging, which is hello new version of GCM, is also supported.</span></span> <span data-ttu-id="f72d8-131">Дополнительные сведения о настройке hello концентратора уведомлений для GCM/FCM и получение hello уведомления в клиентское приложение для Android см. в разделе [tooAndroid уведомления Принудительная отправка с концентраторами уведомлений Azure](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="f72d8-131">For more information on configuring hello notification hub for GCM/FCM and receiving hello notification in an Android client app, see [Sending push notifications tooAndroid with Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span></span>
  * <span data-ttu-id="f72d8-132">`wns` — [службы push-уведомлений Windows](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) для различных платформ Windows.</span><span class="sxs-lookup"><span data-stu-id="f72d8-132">`wns` : [Windows Push Notification Services](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) targeting Windows platforms.</span></span> <span data-ttu-id="f72d8-133">Службы WNS поддерживают также Windows Phone 8.1 и более поздние версии.</span><span class="sxs-lookup"><span data-stu-id="f72d8-133">Windows Phone 8.1 and later is also supported by WNS.</span></span> <span data-ttu-id="f72d8-134">Дополнительные сведения о настройке hello концентратора уведомлений для службы WNS и получение hello уведомления в приложении универсальной платформы Windows (UWP) см. в разделе [Приступая к работе с уведомления концентраторов для универсальной платформы приложений для Windows](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="f72d8-134">For more information on configuring hello notification hub for WNS and receiving hello notification in a Universal Windows Platform (UWP) app, see [Getting started with Notification Hubs for Windows Universal Platform Apps](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span></span>
  * <span data-ttu-id="f72d8-135">`mpns` — [служба push-уведомлений Майкрософт](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span><span class="sxs-lookup"><span data-stu-id="f72d8-135">`mpns` : [Microsoft Push Notification Service](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span></span> <span data-ttu-id="f72d8-136">Данная платформа поддерживает Windows Phone 8 и более ранние версии платформ Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="f72d8-136">This platform supports Windows Phone 8 and earlier Windows Phone platforms.</span></span> <span data-ttu-id="f72d8-137">Дополнительные сведения о настройке hello концентратора уведомлений для MPNS и получение hello уведомления в приложения Windows Phone см. в разделе [Отправка push-уведомлений с концентраторами уведомлений Azure на Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span><span class="sxs-lookup"><span data-stu-id="f72d8-137">For more information on configuring hello notification hub for MPNS and receiving hello notification in a Windows Phone app, see [Sending push notifications with Azure Notification Hubs on Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span></span>

<span data-ttu-id="f72d8-138">Пример файла function.json:</span><span class="sxs-lookup"><span data-stu-id="f72d8-138">Example function.json:</span></span>

```json
{
  "bindings": [
    {
      "name": "notification",
      "type": "notificationHub",
      "tagExpression": "",
      "hubName": "my-notification-hub",
      "connection": "MyHubConnectionString",
      "platform": "gcm",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

## <a name="notification-hub-connection-string-setup"></a><span data-ttu-id="f72d8-139">Настройка строки подключения центра уведомлений</span><span class="sxs-lookup"><span data-stu-id="f72d8-139">Notification hub connection string setup</span></span>
<span data-ttu-id="f72d8-140">Привязка для вывода toouse концентратор уведомлений, необходимо настроить hello строку подключения для hello концентратора.</span><span class="sxs-lookup"><span data-stu-id="f72d8-140">toouse a Notification hub output binding, you must configure hello connection string for hello hub.</span></span> <span data-ttu-id="f72d8-141">Это можно сделать на hello *Интеграция* вкладку, выбрав концентратор уведомлений или создать новую.</span><span class="sxs-lookup"><span data-stu-id="f72d8-141">This can be done on hello *Integrate* tab by selecting your notification hub or creating a new one.</span></span> 

<span data-ttu-id="f72d8-142">Можно также вручную добавить строку подключения для существующий концентратор, добавив строку подключения для hello *DefaultFullSharedAccessSignature* tooyour концентратора уведомлений.</span><span class="sxs-lookup"><span data-stu-id="f72d8-142">You can also manually add a connection string for an existing hub by adding a connection string for hello *DefaultFullSharedAccessSignature* tooyour notification hub.</span></span> <span data-ttu-id="f72d8-143">Эта строка подключения предоставляет доступ к функции разрешение toosend уведомляющих сообщений.</span><span class="sxs-lookup"><span data-stu-id="f72d8-143">This connection string provides your function access permission toosend notification messages.</span></span> <span data-ttu-id="f72d8-144">Hello *DefaultFullSharedAccessSignature* значение строки подключения может осуществляться из hello **ключей** кнопку в главной колонке hello ресурса концентратора уведомлений в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f72d8-144">hello *DefaultFullSharedAccessSignature* connection string value can be accessed from hello **keys** button in hello main blade of your notification hub resource in hello Azure portal.</span></span> <span data-ttu-id="f72d8-145">toomanually добавить строку подключения для вашего концентратора hello используйте следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="f72d8-145">toomanually add a connection string for your hub, use hello following steps:</span></span> 

1. <span data-ttu-id="f72d8-146">На hello **функции приложения** колонке hello портала Azure щелкните **параметрами приложения функции > Перейти параметры службы tooApp**.</span><span class="sxs-lookup"><span data-stu-id="f72d8-146">On hello **Function app** blade of hello Azure portal, click **Function App Settings > Go tooApp Service settings**.</span></span>
2. <span data-ttu-id="f72d8-147">В hello **параметры** колонка, щелкните **параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="f72d8-147">In hello **Settings** blade, click **Application Settings**.</span></span>
3. <span data-ttu-id="f72d8-148">Прокрутите вниз toohello **параметры приложения** раздела и Добавление именованного записи для *DefaultFullSharedAccessSignature* значения для центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="f72d8-148">Scroll down toohello **App settings** section, and add a named entry for *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
4. <span data-ttu-id="f72d8-149">Ссылаться на строку имени параметра в hello привязок выходного приложения.</span><span class="sxs-lookup"><span data-stu-id="f72d8-149">Reference your App setting string name in hello output bindings.</span></span> <span data-ttu-id="f72d8-150">Аналогичные слишком**MyHubConnectionString** используется в приведенном выше примере hello.</span><span class="sxs-lookup"><span data-stu-id="f72d8-150">Similar too**MyHubConnectionString** used in hello example above.</span></span>

## <a name="apns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="f72d8-151">Использование собственных уведомлений APNs с триггерами очереди на языке C#</span><span class="sxs-lookup"><span data-stu-id="f72d8-151">APNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="f72d8-152">В этом примере показано, как toouse типы, определенные в hello [библиотека концентраторы уведомлений Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend собственные уведомления APNS.</span><span class="sxs-lookup"><span data-stu-id="f72d8-152">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native APNS notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="f72d8-153">Использование собственных уведомлений GCM с триггерами очереди на языке C#</span><span class="sxs-lookup"><span data-stu-id="f72d8-153">GCM native notifications with C# queue triggers</span></span>
<span data-ttu-id="f72d8-154">В этом примере показано, как toouse типы, определенные в hello [библиотека концентраторы уведомлений Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend собственные уведомления GCM.</span><span class="sxs-lookup"><span data-stu-id="f72d8-154">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native GCM notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="f72d8-155">Использование собственных уведомлений WNS с триггерами очереди на языке C#</span><span class="sxs-lookup"><span data-stu-id="f72d8-155">WNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="f72d8-156">В этом примере показано, как toouse типы, определенные в hello [библиотека концентраторы уведомлений Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend собственного WNS всплывающих уведомлений.</span><span class="sxs-lookup"><span data-stu-id="f72d8-156">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native WNS toast notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello XML format for a native WNS toast notification is ...
    // <?xml version="1.0" encoding="utf-8"?>
    // <toast>
    //      <visual>
    //     <binding template="ToastText01">
    //       <text id="1">notification message</text>
    //     </binding>
    //   </visual>
    // </toast>

    log.Info($"Sending WNS toast notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string wnsNotificationPayload = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                                    "<toast><visual><binding template=\"ToastText01\">" +
                                        "<text id=\"1\">" + 
                                            "A new user wants toobe added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="template-example-for-nodejs-timer-triggers"></a><span data-ttu-id="f72d8-157">Пример шаблона для триггеров таймера на основе Node.js</span><span class="sxs-lookup"><span data-stu-id="f72d8-157">Template example for Node.js timer triggers</span></span>
<span data-ttu-id="f72d8-158">В этом примере отправляется уведомление для [регистрации шаблона](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md), содержащего свойства `location` и `message`.</span><span class="sxs-lookup"><span data-stu-id="f72d8-158">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);  
    context.bindings.notification = {
        location: "Redmond",
        message: "Hello from Node!"
    };
    context.done();
};
```

## <a name="template-example-for-f-timer-triggers"></a><span data-ttu-id="f72d8-159">Пример шаблона для триггеров таймера на языке F#</span><span class="sxs-lookup"><span data-stu-id="f72d8-159">Template example for F# timer triggers</span></span>
<span data-ttu-id="f72d8-160">В этом примере отправляется уведомление для [регистрации шаблона](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md), содержащего свойства `location` и `message`.</span><span class="sxs-lookup"><span data-stu-id="f72d8-160">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a><span data-ttu-id="f72d8-161">Пример шаблона с параметром вывода</span><span class="sxs-lookup"><span data-stu-id="f72d8-161">Template example using an out parameter</span></span>
<span data-ttu-id="f72d8-162">Этот пример отправляет уведомление [регистрацию шаблона](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) , содержащий `message` заполнителя в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="f72d8-162">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in hello template.</span></span>

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static void Run(string myQueueItem,  out IDictionary<string, string> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = GetTemplateProperties(myQueueItem);
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return templateProperties;
}
```

## <a name="template-example-with-asynchronous-function"></a><span data-ttu-id="f72d8-163">Пример шаблона с асинхронной функцией</span><span class="sxs-lookup"><span data-stu-id="f72d8-163">Template example with asynchronous function</span></span>
<span data-ttu-id="f72d8-164">При использовании асинхронного кода параметры вывода не допускаются.</span><span class="sxs-lookup"><span data-stu-id="f72d8-164">If you are using asynchronous code, out parameters are not allowed.</span></span> <span data-ttu-id="f72d8-165">В этом случае использовать `IAsyncCollector` tooreturn создания шаблона уведомления.</span><span class="sxs-lookup"><span data-stu-id="f72d8-165">In this case use `IAsyncCollector` tooreturn your template notification.</span></span> <span data-ttu-id="f72d8-166">Hello ниже приведен пример асинхронной приведенного выше кода hello.</span><span class="sxs-lookup"><span data-stu-id="f72d8-166">hello following code is an asynchronous example of hello code above.</span></span> 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification tooNotification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants toobe added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a><span data-ttu-id="f72d8-167">Пример шаблона с использованием JSON</span><span class="sxs-lookup"><span data-stu-id="f72d8-167">Template example using JSON</span></span>
<span data-ttu-id="f72d8-168">Этот пример отправляет уведомление [регистрацию шаблона](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) , содержащий `message` заполнитель в шаблон hello, используя допустимую строку JSON.</span><span class="sxs-lookup"><span data-stu-id="f72d8-168">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in hello template using a valid JSON string.</span></span>

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a><span data-ttu-id="f72d8-169">Пример шаблона, в котором используются типы из библиотеки центров уведомлений</span><span class="sxs-lookup"><span data-stu-id="f72d8-169">Template example using Notification Hubs library types</span></span>
<span data-ttu-id="f72d8-170">В этом примере показано, как toouse типы, определенные в hello [библиотека концентраторы уведомлений Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="f72d8-170">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"

using System;
using System.Threading.Tasks;
using Microsoft.Azure.NotificationHubs;

public static void Run(string myQueueItem,  out Notification notification, TraceWriter log)
{
   log.Info($"C# Queue trigger function processed: {myQueueItem}");
   notification = GetTemplateNotification(myQueueItem);
}

private static TemplateNotification GetTemplateNotification(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return new TemplateNotification(templateProperties);
}
```

## <a name="next-steps"></a><span data-ttu-id="f72d8-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f72d8-171">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

