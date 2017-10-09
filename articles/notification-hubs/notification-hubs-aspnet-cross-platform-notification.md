---
title: "toousers aaaSend кросс платформенных уведомлений с концентраторами уведомлений (ASP.NET)"
description: "Узнайте, как toosend шаблоны концентраторы уведомлений toouse в одном запросе уведомления зависящий от платформы, предназначенный для всех платформ."
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
ms.openlocfilehash: f105b871b809e739dd5c05ea819ad135e842ebb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="send-cross-platform-notifications-toousers-with-notification-hubs"></a><span data-ttu-id="9cce2-103">Отправлять уведомления кросс платформенных toousers с концентраторами уведомлений</span><span class="sxs-lookup"><span data-stu-id="9cce2-103">Send cross-platform notifications toousers with Notification Hubs</span></span>
<span data-ttu-id="9cce2-104">В предыдущем учебнике hello [уведомить пользователей с концентраторами уведомлений], вы узнали, как toopush уведомления tooall устройства, зарегистрированные с конкретного прошедшего проверку пользователя.</span><span class="sxs-lookup"><span data-stu-id="9cce2-104">In hello previous tutorial [Notify users with Notification Hubs], you learned how toopush notifications tooall devices registered by a specific authenticated user.</span></span> <span data-ttu-id="9cce2-105">В этом учебнике нескольких запросов были необходимые toosend уведомления tooeach поддерживается клиентской платформе.</span><span class="sxs-lookup"><span data-stu-id="9cce2-105">In that tutorial, multiple requests were required toosend a notification tooeach supported client platform.</span></span> <span data-ttu-id="9cce2-106">Уведомления концентраторов поддерживает шаблоны, которые позволяют указать, как конкретного устройства хочет tooreceive уведомления.</span><span class="sxs-lookup"><span data-stu-id="9cce2-106">Notification Hubs supports templates, which let you specify how a specific device wants tooreceive notifications.</span></span> <span data-ttu-id="9cce2-107">Это упрощает отправку кроссплатформенных уведомлений.</span><span class="sxs-lookup"><span data-stu-id="9cce2-107">This simplifies sending cross-platform notifications.</span></span> <span data-ttu-id="9cce2-108">В этом разделе показано, как tootake преимуществами toosend шаблоны, в один запрос, зависящий от платформы уведомление, предназначенный для всех платформ.</span><span class="sxs-lookup"><span data-stu-id="9cce2-108">This topic demonstrates how tootake advantage of templates toosend, in a single request, a platform-agnostic notification that targets all platforms.</span></span> <span data-ttu-id="9cce2-109">Дополнительные сведения о шаблонах см. в статье [Общие сведения о концентраторах уведомлений][Templates].</span><span class="sxs-lookup"><span data-stu-id="9cce2-109">For more detailed information about templates, see [Azure Notification Hubs Overview][Templates].</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9cce2-110">Проекты Windows Phone 8.1 и более ранней версии не поддерживаются в Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="9cce2-110">Windows Phone projects 8.1 and earlier are not supported using Visual Studio 2017.</span></span> <span data-ttu-id="9cce2-111">Дополнительные сведения см. в статье [Целевая платформа и совместимость для Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="9cce2-111">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="9cce2-112">Концентраторы уведомлений позволяет tooregister устройства несколько шаблонов с hello таким же тегом.</span><span class="sxs-lookup"><span data-stu-id="9cce2-112">Notification Hubs allows a device tooregister multiple templates with hello same tag.</span></span> <span data-ttu-id="9cce2-113">В этом случае входящего сообщения, предназначенные для тега приведет несколько уведомлений доставляться toohello устройства, один для каждого шаблона.</span><span class="sxs-lookup"><span data-stu-id="9cce2-113">In this case, an incoming message targeting that tag results in multiple notifications delivered toohello device, one for each template.</span></span> <span data-ttu-id="9cce2-114">Это позволяет вам toodisplay hello одного сообщения в несколько уведомлений visual, такие как оба значка, а всплывающее уведомление в приложении для магазина Windows.</span><span class="sxs-lookup"><span data-stu-id="9cce2-114">This enables you toodisplay hello same message in multiple visual notifications, such as both as a badge and as a toast notification in a Windows Store app.</span></span>
> 
> 

<span data-ttu-id="9cce2-115">Выполните следующие шаги toosend кросс платформенных уведомления с помощью шаблонов hello.</span><span class="sxs-lookup"><span data-stu-id="9cce2-115">Complete hello following steps toosend cross-platform notifications using templates:</span></span>

1. <span data-ttu-id="9cce2-116">В hello обозревателя решений в Visual Studio разверните hello **контроллеров** папки, а затем откройте hello RegisterController.cs файла.</span><span class="sxs-lookup"><span data-stu-id="9cce2-116">In hello Solution Explorer in Visual Studio, expand hello **Controllers** folder, then open hello RegisterController.cs file.</span></span>
2. <span data-ttu-id="9cce2-117">Найдите hello блок кода в hello **поместить** метод, который создает новую регистрацию замените hello `switch` содержимого с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="9cce2-117">Locate hello block of code in hello **Put** method that creates a new registration replace hello `switch` content with hello following code:</span></span>
   
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
   
    <span data-ttu-id="9cce2-118">Этот код вызывает метод платформой toocreate hello регистрацию шаблона вместо собственную регистрацию.</span><span class="sxs-lookup"><span data-stu-id="9cce2-118">This code calls hello platform-specific method toocreate a template registration instead of a native registration.</span></span> <span data-ttu-id="9cce2-119">Уже имеющиеся регистрации изменять не нужно, поскольку регистрация шаблонов является производной от собственной регистрации.</span><span class="sxs-lookup"><span data-stu-id="9cce2-119">Existing registrations need not be modified because template registrations derive from native registrations.</span></span>
3. <span data-ttu-id="9cce2-120">В hello **уведомления** контроллер, замените hello **sendNotification** метод с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="9cce2-120">In hello **Notifications** controller, replace hello **sendNotification** method with hello following code:</span></span>
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    <span data-ttu-id="9cce2-121">Этот код отправляет уведомление tooall платформы на hello же время и без необходимости toospecify собственного полезных данных.</span><span class="sxs-lookup"><span data-stu-id="9cce2-121">This code sends a notification tooall platforms at hello same time and without having toospecify a native payload.</span></span> <span data-ttu-id="9cce2-122">Строит концентраторов уведомлений и доставляет hello устройства tooevery правильный полезных данных с помощью предоставленных hello *тега* значение, как указано в шаблонах hello зарегистрирован.</span><span class="sxs-lookup"><span data-stu-id="9cce2-122">Notification Hubs builds and delivers hello correct payload tooevery device with hello provided *tag* value, as specified in hello registered templates.</span></span>
4. <span data-ttu-id="9cce2-123">Повторно опубликуйте серверный проект WebApi.</span><span class="sxs-lookup"><span data-stu-id="9cce2-123">Re-publish your WebApi back-end project.</span></span>
5. <span data-ttu-id="9cce2-124">Снова запустите клиентское приложение hello и убедитесь, что регистрация выполняется успешно.</span><span class="sxs-lookup"><span data-stu-id="9cce2-124">Run hello client app again and verify that registration succeeds.</span></span>
6. <span data-ttu-id="9cce2-125">(Необязательно) Развернуть hello клиентского приложения tooa второго устройства, а затем выполните приложение hello.</span><span class="sxs-lookup"><span data-stu-id="9cce2-125">(Optional) Deploy hello client app tooa second device, then run hello app.</span></span>
   
    <span data-ttu-id="9cce2-126">Обратите внимание, что на каждом из устройств отображается уведомление.</span><span class="sxs-lookup"><span data-stu-id="9cce2-126">Note that a notification is displayed on each device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cce2-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9cce2-127">Next Steps</span></span>
<span data-ttu-id="9cce2-128">Теперь, когда вы завершили работу с данным учебником, вы можете узнать больше о центрах уведомлений и шаблонах в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="9cce2-128">Now that you have completed this tutorial, find out more about Notification Hubs and templates in these topics:</span></span>

* <span data-ttu-id="9cce2-129">**[Использование концентраторов уведомлений toosend новости]**</span><span class="sxs-lookup"><span data-stu-id="9cce2-129">**[Use Notification Hubs toosend breaking news]**</span></span> <br/><span data-ttu-id="9cce2-130">Демонстрация другого сценария для использования шаблонов.</span><span class="sxs-lookup"><span data-stu-id="9cce2-130">Demonstrates another scenario for using templates</span></span>
* <span data-ttu-id="9cce2-131">**[Общие сведения о концентраторах уведомлений][Templates]**</span><span class="sxs-lookup"><span data-stu-id="9cce2-131">**[Azure Notification Hubs Overview][Templates]**</span></span><br/><span data-ttu-id="9cce2-132">содержится более подробная информация о шаблонах.</span><span class="sxs-lookup"><span data-stu-id="9cce2-132">Overview topic has more detailed information on templates.</span></span>

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push toousers ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push toousers Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

[Использование концентраторов уведомлений toosend новости]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
[уведомить пользователей с концентраторами уведомлений]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How toofor Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
