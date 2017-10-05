---
title: "Выходная привязка центра уведомлений для Функций Azure | Документация Майкрософт"
description: "Узнайте, как использовать привязки центра уведомлений Azure в функциях Azure."
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
ms.openlocfilehash: fa3d37b963c1bb6b58127b9180cd657d7b1dabcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-notification-hub-output-binding"></a><span data-ttu-id="0fe06-104">Выходная привязка центра уведомлений для функций Azure</span><span class="sxs-lookup"><span data-stu-id="0fe06-104">Azure Functions Notification Hub output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="0fe06-105">Эта статья объясняет, как настроить и запрограммировать привязки центра уведомлений Azure в функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="0fe06-105">This article explains how to configure and code Azure Notification Hub bindings in Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="0fe06-106">Функции могут отправлять push-уведомления всего несколькими строками кода, используя настроенный центр уведомлений Azure.</span><span class="sxs-lookup"><span data-stu-id="0fe06-106">Your functions can send push notifications using a configured Azure Notification Hub with a few lines of code.</span></span> <span data-ttu-id="0fe06-107">Однако центр уведомлений Azure нужно настроить для служб уведомлений платформы (PNS), которые необходимо использовать.</span><span class="sxs-lookup"><span data-stu-id="0fe06-107">However, the Azure Notification Hub must be configured for the Platform Notifications Services (PNS) you want to use.</span></span> <span data-ttu-id="0fe06-108">Чтобы получить дополнительные сведения о настройке центра уведомлений Azure и разработке клиентских приложений, которые регистрируют для получения уведомлений, перейдите к статье [Приступая к работе с центрами уведомлений](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) и щелкните необходимую клиентскую платформу вверху.</span><span class="sxs-lookup"><span data-stu-id="0fe06-108">For more information on configuring an Azure Notification Hub and developing a client applications that register to receive notifications, see [Getting started with Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) and click your target client platform at the top.</span></span>

<span data-ttu-id="0fe06-109">Можно отправлять собственные или шаблонные уведомления.</span><span class="sxs-lookup"><span data-stu-id="0fe06-109">The notifications you send can be native notifications or template notifications.</span></span> <span data-ttu-id="0fe06-110">Собственные уведомления нацелены на определенную платформу уведомлений, указанную в свойстве `platform` привязки для вывода.</span><span class="sxs-lookup"><span data-stu-id="0fe06-110">Native notifications target a specific notification platform as configured in the `platform` property of the output binding.</span></span> <span data-ttu-id="0fe06-111">Шаблонное уведомление можно использовать для нескольких платформ.</span><span class="sxs-lookup"><span data-stu-id="0fe06-111">A template notification can be used to target multiple platforms.</span></span>   

## <a name="notification-hub-output-binding-properties"></a><span data-ttu-id="0fe06-112">Свойства привязки для вывода центра уведомлений</span><span class="sxs-lookup"><span data-stu-id="0fe06-112">Notification hub output binding properties</span></span>
<span data-ttu-id="0fe06-113">Файл function.json содержит следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="0fe06-113">The function.json file provides the following properties:</span></span>

* <span data-ttu-id="0fe06-114">`name` — имя переменной, используемой в коде функции для сообщения центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="0fe06-114">`name` : Variable name used in function code for the notification hub message.</span></span>
* <span data-ttu-id="0fe06-115">`type` — для этого свойства следует задать значение *notificationHub*.</span><span class="sxs-lookup"><span data-stu-id="0fe06-115">`type` : must be set to *"notificationHub"*.</span></span>
* <span data-ttu-id="0fe06-116">`tagExpression` — с помощью выражений тегов можно указать, что уведомления должны отправляться на устройства, зарегистрированные для получения уведомлений, соответствующих выражению тега.</span><span class="sxs-lookup"><span data-stu-id="0fe06-116">`tagExpression` : Tag expressions allow you to specify that notifications be delivered to a set of devices who have registered to receive notifications that match the tag expression.</span></span>  <span data-ttu-id="0fe06-117">Дополнительные сведения см. в статье [Маршрутизация и выражения тегов](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="0fe06-117">For more information, see [Routing and tag expressions](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span></span>
* <span data-ttu-id="0fe06-118">`hubName` — имя ресурса центра уведомлений на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="0fe06-118">`hubName` : Name of the notification hub resource in the Azure portal.</span></span>
* <span data-ttu-id="0fe06-119">`connection` — строка подключения **параметра приложения** , для которой задано значение *DefaultFullSharedAccessSignature* для центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="0fe06-119">`connection` : This connection string must be an **Application Setting** connection string set to the *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
* <span data-ttu-id="0fe06-120">`direction` — для этого свойства необходимо задать значение *out*.</span><span class="sxs-lookup"><span data-stu-id="0fe06-120">`direction` : must be set to *"out"*.</span></span> 
* <span data-ttu-id="0fe06-121">`platform` — свойство платформы, которое указывает целевую платформу уведомлений для ваших уведомлений.</span><span class="sxs-lookup"><span data-stu-id="0fe06-121">`platform` : The platform property indicates the notification platform your notification targets.</span></span> <span data-ttu-id="0fe06-122">Необходимо установить одно из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="0fe06-122">Must be one of the following values:</span></span>
  * <span data-ttu-id="0fe06-123">По умолчанию, если свойство платформы отсутствует в выходной привязке, шаблонные уведомления могут использоваться для любой платформы, настроенной в концентраторе уведомлений Azure.</span><span class="sxs-lookup"><span data-stu-id="0fe06-123">By default, if the platform property is omitted from the output binding, template notifications can be used to target any platform configured on the Azure Notification Hub.</span></span> <span data-ttu-id="0fe06-124">Дополнительные общие сведения об использовании шаблонов для отправки кроссплатформенных уведомлений с помощью центра уведомлений Azure см. в разделе [Шаблоны](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="0fe06-124">For more information on using templates in general to send cross platform notifications with an Azure Notification Hub, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>
  * <span data-ttu-id="0fe06-125">`apns` — служба push-уведомлений Apple.</span><span class="sxs-lookup"><span data-stu-id="0fe06-125">`apns` : Apple Push Notification Service.</span></span> <span data-ttu-id="0fe06-126">Дополнительные сведения о настройке центра уведомлений для APNs и получении уведомлений в клиентском приложении см. в разделе [Отправка push-уведомлений с помощью центров уведомлений Azure в iOS](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0fe06-126">For more information on configuring the notification hub for APNS and receiving the notification in a client app, see [Sending push notifications to iOS with Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span></span> 
  * <span data-ttu-id="0fe06-127">`adm` — [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span><span class="sxs-lookup"><span data-stu-id="0fe06-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span></span> <span data-ttu-id="0fe06-128">Дополнительные сведения о настройке центра уведомлений для ADM и получении уведомлений в приложении Kindle см. в разделе [Приступая к работе с Центрами уведомлений для приложений Kindle](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="0fe06-128">For more information on configuring the notification hub for ADM and receiving the notification in a Kindle app, see [Getting Started with Notification Hubs for Kindle apps](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span></span> 
  * <span data-ttu-id="0fe06-129">`gcm` — [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="0fe06-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span></span> <span data-ttu-id="0fe06-130">Также поддерживается новая версия GCM, Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="0fe06-130">Firebase Cloud Messaging, which is the new version of GCM, is also supported.</span></span> <span data-ttu-id="0fe06-131">Дополнительные сведения о настройке центра уведомлений для GCM или FCM и получении уведомлений в клиентском приложении Android см. в разделе [Отправка push-уведомлений в приложения Android с помощью центров уведомлений Azure](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0fe06-131">For more information on configuring the notification hub for GCM/FCM and receiving the notification in an Android client app, see [Sending push notifications to Android with Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span></span>
  * <span data-ttu-id="0fe06-132">`wns` — [службы push-уведомлений Windows](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) для различных платформ Windows.</span><span class="sxs-lookup"><span data-stu-id="0fe06-132">`wns` : [Windows Push Notification Services](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) targeting Windows platforms.</span></span> <span data-ttu-id="0fe06-133">Службы WNS поддерживают также Windows Phone 8.1 и более поздние версии.</span><span class="sxs-lookup"><span data-stu-id="0fe06-133">Windows Phone 8.1 and later is also supported by WNS.</span></span> <span data-ttu-id="0fe06-134">Дополнительные сведения о настройке центра уведомлений для WNS и получении уведомлений в приложении универсальной платформы Windows (UWP) см. в разделе [Начало работы с Центрами уведомлений для приложений универсальной платформы Windows](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="0fe06-134">For more information on configuring the notification hub for WNS and receiving the notification in a Universal Windows Platform (UWP) app, see [Getting started with Notification Hubs for Windows Universal Platform Apps](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span></span>
  * <span data-ttu-id="0fe06-135">`mpns` — [служба push-уведомлений Майкрософт](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span><span class="sxs-lookup"><span data-stu-id="0fe06-135">`mpns` : [Microsoft Push Notification Service](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span></span> <span data-ttu-id="0fe06-136">Данная платформа поддерживает Windows Phone 8 и более ранние версии платформ Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="0fe06-136">This platform supports Windows Phone 8 and earlier Windows Phone platforms.</span></span> <span data-ttu-id="0fe06-137">Дополнительные сведения о настройке центра уведомлений для MPNS и получении уведомлений в приложении Windows Phone см. в разделе [Отправка push-уведомлений в приложения Windows Phone с помощью центров уведомлений Azure](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md).</span><span class="sxs-lookup"><span data-stu-id="0fe06-137">For more information on configuring the notification hub for MPNS and receiving the notification in a Windows Phone app, see [Sending push notifications with Azure Notification Hubs on Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span></span>

<span data-ttu-id="0fe06-138">Пример файла function.json:</span><span class="sxs-lookup"><span data-stu-id="0fe06-138">Example function.json:</span></span>

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

## <a name="notification-hub-connection-string-setup"></a><span data-ttu-id="0fe06-139">Настройка строки подключения центра уведомлений</span><span class="sxs-lookup"><span data-stu-id="0fe06-139">Notification hub connection string setup</span></span>
<span data-ttu-id="0fe06-140">Для использования привязки для вывода центра уведомлений необходимо настроить отдельную строку подключения.</span><span class="sxs-lookup"><span data-stu-id="0fe06-140">To use a Notification hub output binding, you must configure the connection string for the hub.</span></span> <span data-ttu-id="0fe06-141">Это можно сделать на вкладке *Интеграция*, выбрав центр уведомлений или создав его.</span><span class="sxs-lookup"><span data-stu-id="0fe06-141">This can be done on the *Integrate* tab by selecting your notification hub or creating a new one.</span></span> 

<span data-ttu-id="0fe06-142">Можно также вручную добавить строку подключения для имеющегося центра, указав ее в качестве значения *DefaultFullSharedAccessSignature* для центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="0fe06-142">You can also manually add a connection string for an existing hub by adding a connection string for the *DefaultFullSharedAccessSignature* to your notification hub.</span></span> <span data-ttu-id="0fe06-143">Эта строка подключения предоставляет разрешение на доступ к функции для отправки сообщений с уведомлениями.</span><span class="sxs-lookup"><span data-stu-id="0fe06-143">This connection string provides your function access permission to send notification messages.</span></span> <span data-ttu-id="0fe06-144">Для доступа к строке подключения *DefaultFullSharedAccessSignature* нажмите кнопку **Ключи** в главной колонке для ресурса центра уведомлений на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="0fe06-144">The *DefaultFullSharedAccessSignature* connection string value can be accessed from the **keys** button in the main blade of your notification hub resource in the Azure portal.</span></span> <span data-ttu-id="0fe06-145">Чтобы добавить строку подключения для центра вручную, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="0fe06-145">To manually add a connection string for your hub, use the following steps:</span></span> 

1. <span data-ttu-id="0fe06-146">В колонке **Приложение-функция** на портале Azure щелкните **Параметры приложения-функции > Перейти к параметрам службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="0fe06-146">On the **Function app** blade of the Azure portal, click **Function App Settings > Go to App Service settings**.</span></span>
2. <span data-ttu-id="0fe06-147">В колонке **Параметры** щелкните раздел **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="0fe06-147">In the **Settings** blade, click **Application Settings**.</span></span>
3. <span data-ttu-id="0fe06-148">Прокрутите страницу вниз до раздела **Параметры приложения** и добавьте именованную запись в качестве значения *DefaultFullSharedAccessSignature* для центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="0fe06-148">Scroll down to the **App settings** section, and add a named entry for *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
4. <span data-ttu-id="0fe06-149">Укажите имя строки параметров приложения в выходных привязках.</span><span class="sxs-lookup"><span data-stu-id="0fe06-149">Reference your App setting string name in the output bindings.</span></span> <span data-ttu-id="0fe06-150">Это имя должно быть аналогично строке **MyHubConnectionString**, использованной в приведенном выше примере.</span><span class="sxs-lookup"><span data-stu-id="0fe06-150">Similar to **MyHubConnectionString** used in the example above.</span></span>

## <a name="apns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="0fe06-151">Использование собственных уведомлений APNs с триггерами очереди на языке C#</span><span class="sxs-lookup"><span data-stu-id="0fe06-151">APNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="0fe06-152">В этом примере показано, как использовать типы, определенные в [библиотеке центров уведомлений Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/), для отправки собственного уведомления APNs.</span><span class="sxs-lookup"><span data-stu-id="0fe06-152">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native APNS notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="0fe06-153">Использование собственных уведомлений GCM с триггерами очереди на языке C#</span><span class="sxs-lookup"><span data-stu-id="0fe06-153">GCM native notifications with C# queue triggers</span></span>
<span data-ttu-id="0fe06-154">В этом примере показано, как использовать типы, определенные в [библиотеке центров уведомлений Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/), для отправки собственного уведомления GCM.</span><span class="sxs-lookup"><span data-stu-id="0fe06-154">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native GCM notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="0fe06-155">Использование собственных уведомлений WNS с триггерами очереди на языке C#</span><span class="sxs-lookup"><span data-stu-id="0fe06-155">WNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="0fe06-156">В этом примере показано, как использовать типы, определенные в [библиотеке центров уведомлений Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/), для отправки всплывающего уведомления WNS.</span><span class="sxs-lookup"><span data-stu-id="0fe06-156">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native WNS toast notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The XML format for a native WNS toast notification is ...
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
                                            "A new user wants to be added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="template-example-for-nodejs-timer-triggers"></a><span data-ttu-id="0fe06-157">Пример шаблона для триггеров таймера на основе Node.js</span><span class="sxs-lookup"><span data-stu-id="0fe06-157">Template example for Node.js timer triggers</span></span>
<span data-ttu-id="0fe06-158">В этом примере отправляется уведомление для [регистрации шаблона](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md), содержащего свойства `location` и `message`.</span><span class="sxs-lookup"><span data-stu-id="0fe06-158">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

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

## <a name="template-example-for-f-timer-triggers"></a><span data-ttu-id="0fe06-159">Пример шаблона для триггеров таймера на языке F#</span><span class="sxs-lookup"><span data-stu-id="0fe06-159">Template example for F# timer triggers</span></span>
<span data-ttu-id="0fe06-160">В этом примере отправляется уведомление для [регистрации шаблона](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md), содержащего свойства `location` и `message`.</span><span class="sxs-lookup"><span data-stu-id="0fe06-160">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a><span data-ttu-id="0fe06-161">Пример шаблона с параметром вывода</span><span class="sxs-lookup"><span data-stu-id="0fe06-161">Template example using an out parameter</span></span>
<span data-ttu-id="0fe06-162">В этом примере отправляется уведомление для [регистрации шаблона](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md), содержащего заполнитель `message`.</span><span class="sxs-lookup"><span data-stu-id="0fe06-162">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template.</span></span>

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

## <a name="template-example-with-asynchronous-function"></a><span data-ttu-id="0fe06-163">Пример шаблона с асинхронной функцией</span><span class="sxs-lookup"><span data-stu-id="0fe06-163">Template example with asynchronous function</span></span>
<span data-ttu-id="0fe06-164">При использовании асинхронного кода параметры вывода не допускаются.</span><span class="sxs-lookup"><span data-stu-id="0fe06-164">If you are using asynchronous code, out parameters are not allowed.</span></span> <span data-ttu-id="0fe06-165">В этом случае для возвращения шаблонного уведомления следует использовать `IAsyncCollector`.</span><span class="sxs-lookup"><span data-stu-id="0fe06-165">In this case use `IAsyncCollector` to return your template notification.</span></span> <span data-ttu-id="0fe06-166">Ниже приведен пример асинхронного кода, описанного выше.</span><span class="sxs-lookup"><span data-stu-id="0fe06-166">The following code is an asynchronous example of the code above.</span></span> 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification to Notification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants to be added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a><span data-ttu-id="0fe06-167">Пример шаблона с использованием JSON</span><span class="sxs-lookup"><span data-stu-id="0fe06-167">Template example using JSON</span></span>
<span data-ttu-id="0fe06-168">В этом примере отправляется уведомление для [регистрации шаблона](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md), содержащего заполнитель `message` и использующего допустимую строку JSON.</span><span class="sxs-lookup"><span data-stu-id="0fe06-168">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template using a valid JSON string.</span></span>

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a><span data-ttu-id="0fe06-169">Пример шаблона, в котором используются типы из библиотеки центров уведомлений</span><span class="sxs-lookup"><span data-stu-id="0fe06-169">Template example using Notification Hubs library types</span></span>
<span data-ttu-id="0fe06-170">В этом примере показано, как использовать типы, определенные в [библиотеке центров уведомлений Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="0fe06-170">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="0fe06-171">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0fe06-171">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

