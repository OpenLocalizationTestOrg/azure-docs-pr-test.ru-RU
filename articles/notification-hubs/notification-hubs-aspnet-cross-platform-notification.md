---
title: "Отправка кроссплатформенных уведомлений пользователям с помощью центров уведомлений (ASP.NET)"
description: "Узнайте, как использовать шаблоны центров уведомлений для отправки в одном запросе независимых от платформы уведомлений, предназначенных для всех платформ."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 11d2131b-f683-47fd-a691-4cdfc696f62b
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: ef971fcfe68978ea9ce0810c69efbe134bb15f8a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="send-cross-platform-notifications-to-users-with-notification-hubs"></a><span data-ttu-id="73dec-103">Отправка кроссплатформенных уведомлений пользователям с помощью центров уведомлений</span><span class="sxs-lookup"><span data-stu-id="73dec-103">Send cross-platform notifications to users with Notification Hubs</span></span>
<span data-ttu-id="73dec-104">В предыдущем руководстве под названием [Уведомление пользователей с помощью Центров уведомлений] вы научились отправлять push-уведомления на все устройства, зарегистрированные конкретным пользователем, прошедшим проверку.</span><span class="sxs-lookup"><span data-stu-id="73dec-104">In the previous tutorial [Notify users with Notification Hubs], you learned how to push notifications to all devices registered by a specific authenticated user.</span></span> <span data-ttu-id="73dec-105">В этом учебнике для отправки уведомления на каждую поддерживаемую платформу клиента требовалось несколько запросов.</span><span class="sxs-lookup"><span data-stu-id="73dec-105">In that tutorial, multiple requests were required to send a notification to each supported client platform.</span></span> <span data-ttu-id="73dec-106">Концентраторы уведомлений поддерживают шаблоны, которые позволяют указать, каким образом конкретное устройство должно получать уведомления.</span><span class="sxs-lookup"><span data-stu-id="73dec-106">Notification Hubs supports templates, which let you specify how a specific device wants to receive notifications.</span></span> <span data-ttu-id="73dec-107">Это упрощает отправку кроссплатформенных уведомлений.</span><span class="sxs-lookup"><span data-stu-id="73dec-107">This simplifies sending cross-platform notifications.</span></span> <span data-ttu-id="73dec-108">В этой статье рассказывается, как воспользоваться преимуществами шаблонов для отправки в одном запросе независимых от платформы уведомлений, предназначенных для всех платформ.</span><span class="sxs-lookup"><span data-stu-id="73dec-108">This topic demonstrates how to take advantage of templates to send, in a single request, a platform-agnostic notification that targets all platforms.</span></span> <span data-ttu-id="73dec-109">Дополнительные сведения о шаблонах см. в статье [Общие сведения о концентраторах уведомлений][Templates].</span><span class="sxs-lookup"><span data-stu-id="73dec-109">For more detailed information about templates, see [Azure Notification Hubs Overview][Templates].</span></span>
> [!IMPORTANT]
> <span data-ttu-id="73dec-110">Проекты Windows Phone 8.1 и более ранней версии не поддерживаются в Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="73dec-110">Windows Phone projects 8.1 and earlier are not supported using Visual Studio 2017.</span></span> <span data-ttu-id="73dec-111">Дополнительные сведения см. в статье [Целевая платформа и совместимость для Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="73dec-111">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="73dec-112">Центры уведомлений позволяют устройству зарегистрировать несколько шаблонов с одним и тем же тегом.</span><span class="sxs-lookup"><span data-stu-id="73dec-112">Notification Hubs allows a device to register multiple templates with the same tag.</span></span> <span data-ttu-id="73dec-113">В этом случае входящее сообщение, предназначенное для этого тега, приводит к отправке на устройство нескольких уведомлений, по одному для каждого шаблона.</span><span class="sxs-lookup"><span data-stu-id="73dec-113">In this case, an incoming message targeting that tag results in multiple notifications delivered to the device, one for each template.</span></span> <span data-ttu-id="73dec-114">Это дает возможность отображения одного сообщения в нескольких визуальных уведомлениях, например в виде значка и в виде всплывающего уведомления в Магазине Windows.</span><span class="sxs-lookup"><span data-stu-id="73dec-114">This enables you to display the same message in multiple visual notifications, such as both as a badge and as a toast notification in a Windows Store app.</span></span>
> 
> 

<span data-ttu-id="73dec-115">Выполните следующие действия для отправки кроссплатформенных уведомлений с использованием шаблонов:</span><span class="sxs-lookup"><span data-stu-id="73dec-115">Complete the following steps to send cross-platform notifications using templates:</span></span>

1. <span data-ttu-id="73dec-116">В обозревателе решений в Visual Studio разверните папку **Контроллеры** , затем откройте файл RegisterController.cs.</span><span class="sxs-lookup"><span data-stu-id="73dec-116">In the Solution Explorer in Visual Studio, expand the **Controllers** folder, then open the RegisterController.cs file.</span></span>
2. <span data-ttu-id="73dec-117">Найдите в методе **Put** блок кода, создающий регистрацию, и замените содержимое `switch` следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="73dec-117">Locate the block of code in the **Put** method that creates a new registration replace the `switch` content with the following code:</span></span>
   
        switch (deviceUpdate.Platform)
        {
            case "mpns":
                var toastTemplate = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>$(message)</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
                registration = new MpnsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "wns":
                toastTemplate = @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(message)</text></binding></visual></toast>";
                registration = new WindowsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "apns":
                var alertTemplate = "{\"aps\":{\"alert\":\"$(message)\"}}";
                registration = new AppleTemplateRegistrationDescription(deviceUpdate.Handle, alertTemplate);
                break;
            case "gcm":
                var messageTemplate = "{\"data\":{\"message\":\"$(message)\"}}";
                registration = new GcmTemplateRegistrationDescription(deviceUpdate.Handle, messageTemplate);
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }
   
    <span data-ttu-id="73dec-118">Этот код вызывает метод, используемый на конкретной платформе для регистрации шаблонов вместо собственной регистрации.</span><span class="sxs-lookup"><span data-stu-id="73dec-118">This code calls the platform-specific method to create a template registration instead of a native registration.</span></span> <span data-ttu-id="73dec-119">Уже имеющиеся регистрации изменять не нужно, поскольку регистрация шаблонов является производной от собственной регистрации.</span><span class="sxs-lookup"><span data-stu-id="73dec-119">Existing registrations need not be modified because template registrations derive from native registrations.</span></span>
3. <span data-ttu-id="73dec-120">В контроллере **Уведомления** замените метод **sendNotification** следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="73dec-120">In the **Notifications** controller, replace the **sendNotification** method with the following code:</span></span>
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    <span data-ttu-id="73dec-121">Этот код отправляет уведомление одновременно для всех платформ без необходимости указания собственных полезных данных.</span><span class="sxs-lookup"><span data-stu-id="73dec-121">This code sends a notification to all platforms at the same time and without having to specify a native payload.</span></span> <span data-ttu-id="73dec-122">Центры уведомлений создают и доставляют правильные полезные данные для каждого устройства с указанным значением *тега* в соответствии с зарегистрированными шаблонами.</span><span class="sxs-lookup"><span data-stu-id="73dec-122">Notification Hubs builds and delivers the correct payload to every device with the provided *tag* value, as specified in the registered templates.</span></span>
4. <span data-ttu-id="73dec-123">Повторно опубликуйте серверный проект WebApi.</span><span class="sxs-lookup"><span data-stu-id="73dec-123">Re-publish your WebApi back-end project.</span></span>
5. <span data-ttu-id="73dec-124">Снова запустите клиентское приложение и убедитесь, что регистрация прошла успешно.</span><span class="sxs-lookup"><span data-stu-id="73dec-124">Run the client app again and verify that registration succeeds.</span></span>
6. <span data-ttu-id="73dec-125">(Необязательно) Разверните клиентское приложение на втором устройстве, а затем запустите это приложение.</span><span class="sxs-lookup"><span data-stu-id="73dec-125">(Optional) Deploy the client app to a second device, then run the app.</span></span>
   
    <span data-ttu-id="73dec-126">Обратите внимание, что на каждом из устройств отображается уведомление.</span><span class="sxs-lookup"><span data-stu-id="73dec-126">Note that a notification is displayed on each device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73dec-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="73dec-127">Next Steps</span></span>
<span data-ttu-id="73dec-128">Теперь, когда вы завершили работу с данным учебником, вы можете узнать больше о центрах уведомлений и шаблонах в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="73dec-128">Now that you have completed this tutorial, find out more about Notification Hubs and templates in these topics:</span></span>

* <span data-ttu-id="73dec-129">**[Использование Центров уведомлений для передачи экстренных новостей]**</span><span class="sxs-lookup"><span data-stu-id="73dec-129">**[Use Notification Hubs to send breaking news]**</span></span> <br/><span data-ttu-id="73dec-130">Демонстрация другого сценария для использования шаблонов.</span><span class="sxs-lookup"><span data-stu-id="73dec-130">Demonstrates another scenario for using templates</span></span>
* <span data-ttu-id="73dec-131">**[Общие сведения о концентраторах уведомлений][Templates]**</span><span class="sxs-lookup"><span data-stu-id="73dec-131">**[Azure Notification Hubs Overview][Templates]**</span></span><br/><span data-ttu-id="73dec-132">содержится более подробная информация о шаблонах.</span><span class="sxs-lookup"><span data-stu-id="73dec-132">Overview topic has more detailed information on templates.</span></span>

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push to users ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push to users Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

<span data-ttu-id="73dec-133">[Использование Центров уведомлений для передачи экстренных новостей]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="73dec-133">[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
<span data-ttu-id="73dec-134">[Уведомление пользователей с помощью Центров уведомлений]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="73dec-134">[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How to for Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
