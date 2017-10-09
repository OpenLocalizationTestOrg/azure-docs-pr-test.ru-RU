---
title: "принудительные уведомления aaaAdd tooyour-приложения универсальной платформы Windows (UWP) | Документы Microsoft"
description: "Узнайте, как toouse мобильные приложения службы приложений Azure и концентраторов уведомлений Azure toosend push-уведомления tooyour универсальной платформы Windows (UWP) приложения."
services: app-service\mobile,notification-hubs
documentationcenter: windows
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6de1b9d4-bd28-43e4-8db4-94cd3b187aa3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 378ce59cab974830c0a3801108b24b30a21ae5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-windows-app"></a><span data-ttu-id="0bb5f-103">Добавление приложения Windows tooyour уведомлений push</span><span class="sxs-lookup"><span data-stu-id="0bb5f-103">Add push notifications tooyour Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="0bb5f-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="0bb5f-104">Overview</span></span>
<span data-ttu-id="0bb5f-105">В этом учебнике добавить push уведомления toohello [краткое руководство по Windows](app-service-mobile-windows-store-dotnet-get-started.md) проекта, чтобы каждый раз при вставке записи push-уведомление отправляется toohello устройства.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-105">In this tutorial, you add push notifications toohello [Windows quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="0bb5f-106">Если вы не используете hello загружен проект быстрый запуск сервера, будет необходимо hello пакета расширения уведомлений push.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="0bb5f-107">В разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <span data-ttu-id="0bb5f-108"><a name="configure-hub"></a>Настройка концентратора уведомлений</span><span class="sxs-lookup"><span data-stu-id="0bb5f-108"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="0bb5f-109">Регистрация приложения для работы с push-уведомлениями</span><span class="sxs-lookup"><span data-stu-id="0bb5f-109">Register your app for push notifications</span></span>
<span data-ttu-id="0bb5f-110">Требуется toosubmit toohello вашего приложения магазина Windows, а затем настроить toointegrate проекта на сервере с принудительной отправкой toosend Windows Notification Service (WNS).</span><span class="sxs-lookup"><span data-stu-id="0bb5f-110">You need toosubmit your app toohello Windows Store, then configure your server project toointegrate with Windows Notification Services (WNS) toosend push.</span></span>

1. <span data-ttu-id="0bb5f-111">В обозревателе решений Visual Studio, щелкните правой кнопкой мыши проект приложения hello UWP, щелкните **хранилища** > **связать приложение с hello хранилища...** .</span><span class="sxs-lookup"><span data-stu-id="0bb5f-111">In Visual Studio Solution Explorer, right-click hello UWP app project, click **Store** > **Associate App with hello Store...**.</span></span>

    ![Связь приложения с Магазином Windows](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. <span data-ttu-id="0bb5f-113">В мастере приветствия щелкните **Далее**, войти в учетную запись Майкрософт, введите имя приложения в **зарезервировать новое имя приложения**, нажмите кнопку **резерва**.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-113">In hello wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="0bb5f-114">После регистрации приложения hello hello успешно создан, выберите новое имя приложения, нажмите кнопку **Далее**, а затем нажмите кнопку **связать**.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-114">After hello app registration is successfully created, select hello new app name, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="0bb5f-115">Это добавляет манифест приложения toohello сведения о регистрации требуется hello магазина Windows.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-115">This adds hello required Windows Store registration information toohello application manifest.</span></span>  
4. <span data-ttu-id="0bb5f-116">Перейдите toohello [центра разработчиков Windows](https://dev.windows.com/en-us/overview)вход с учетной записью Майкрософт, нажмите кнопку Регистрация нового приложения hello в **Мои приложения**, затем разверните **службы**  >  **Push-уведомления**.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-116">Navigate toohello [Windows Dev Center](https://dev.windows.com/en-us/overview), sign-in with your Microsoft account, click hello new app registration in **My apps**, then expand **Services** > **Push notifications**.</span></span>
5. <span data-ttu-id="0bb5f-117">В hello **Push-уведомления** щелкните **узла службы Live** под **мобильных служб Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-117">In hello **Push notifications** page, click **Live Services site** under **Microsoft Azure Mobile Services**.</span></span>
6. <span data-ttu-id="0bb5f-118">На странице регистрации hello, запишите значение hello в **секреты приложения** и hello **ИД безопасности пакета**, который затем используется tooconfigure серверной части мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-118">In hello registration page, make a note of hello value under **Application secrets** and hello **Package SID**, which you will next use tooconfigure your mobile app backend.</span></span>

    ![Связь приложения с Магазином Windows](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > <span data-ttu-id="0bb5f-120">Hello секрета клиента и ИД безопасности пакета являются важными элементами обеспечения безопасности.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-120">hello client secret and package SID are important security credentials.</span></span> <span data-ttu-id="0bb5f-121">Не сообщайте никому эти значения и не распространяйте их вместе со своим приложением.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-121">Do not share these values with anyone or distribute them with your app.</span></span> <span data-ttu-id="0bb5f-122">Hello **идентификатор приложения** с проверки подлинности учетной записи Майкрософт секретный tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-122">hello **Application Id** is used with hello secret tooconfigure Microsoft Account authentication.</span></span>
   >
   >

## <a name="configure-hello-backend-toosend-push-notifications"></a><span data-ttu-id="0bb5f-123">Настройка внутреннего toosend hello push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="0bb5f-123">Configure hello backend toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <span data-ttu-id="0bb5f-124"><a id="update-service"></a>Обновление сервера toosend hello push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="0bb5f-124"><a id="update-service"></a>Update hello server toosend push notifications</span></span>
<span data-ttu-id="0bb5f-125">Процедура hello ниже, соответствующую типу вашего внутреннего проекта&mdash;либо [серверное приложение .NET](#dotnet) или [Node.js серверной](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="0bb5f-125">Use hello procedure below that matches your backend project type&mdash;either [.NET backend](#dotnet) or [Node.js backend](#nodejs).</span></span>

### <span data-ttu-id="0bb5f-126"><a name="dotnet"></a>Серверный проект .NET</span><span class="sxs-lookup"><span data-stu-id="0bb5f-126"><a name="dotnet"></a>.NET backend project</span></span>
1. <span data-ttu-id="0bb5f-127">В Visual Studio, щелкните правой кнопкой мыши проект сервера hello и нажмите кнопку **управление пакетами NuGet**, поиск Microsoft.Azure.NotificationHubs, а затем нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-127">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for Microsoft.Azure.NotificationHubs, then click **Install**.</span></span> <span data-ttu-id="0bb5f-128">При этом устанавливаются hello концентраторы уведомлений клиентской библиотеки.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-128">This installs hello Notification Hubs client library.</span></span>
2. <span data-ttu-id="0bb5f-129">Разверните **контроллеров**откройте TodoItemController.cs и добавьте следующее hello операторы using:</span><span class="sxs-lookup"><span data-stu-id="0bb5f-129">Expand **Controllers**, open TodoItemController.cs, and add hello following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="0bb5f-130">В hello **PostTodoItem** метод, добавьте следующий код после вызова hello слишком hello**InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="0bb5f-130">In hello **PostTodoItem** method, add hello following code after hello call too**InsertAsync**:</span></span>

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create hello notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send hello push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="0bb5f-131">Этот код показывает toosend концентратора уведомлений hello push-уведомление после вставки нового элемента.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-131">This code tells hello notification hub toosend a push notification after a new item is insertion.</span></span>
4. <span data-ttu-id="0bb5f-132">Повторная публикация проекта сервера hello.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-132">Republish hello server project.</span></span>

### <span data-ttu-id="0bb5f-133"><a name="nodejs"></a>Серверный проект Node.js</span><span class="sxs-lookup"><span data-stu-id="0bb5f-133"><a name="nodejs"></a>Node.js backend project</span></span>
1. <span data-ttu-id="0bb5f-134">Если вы еще не сделали этого, [загрузите проект краткое руководство hello](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) или в противном случае используйте hello [интерактивном редакторе в hello портал Azure](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="0bb5f-134">If you haven't already done so, [download hello quickstart project](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use hello [online editor in hello Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="0bb5f-135">Замените существующий код hello в файле todoitem.js hello hello следующее:</span><span class="sxs-lookup"><span data-stu-id="0bb5f-135">Replace hello existing code in hello todoitem.js file with hello following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello WNS payload that contains hello new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a WNS native toast notification.
                    context.push.wns.sendToast(null, payload, function (error) {
                        if (error) {
                            logger.error('Error while sending push notification: ', error);
                        } else {
                            logger.info('Push notification sent successfully!');
                        }
                    });
                }
                // Don't forget tooreturn hello results from hello context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;

    <span data-ttu-id="0bb5f-136">Это отправляет всплывающее уведомление WNS, содержащий hello item.text при вставке нового элемента todo.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-136">This sends a WNS toast notification that contains hello item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="0bb5f-137">При редактировании файла hello на локальном компьютере повторно опубликуйте проект сервера hello.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-137">When editing hello file on your local computer, republish hello server project.</span></span>

## <span data-ttu-id="0bb5f-138"><a id="update-app"></a>Добавить приложение tooyour уведомлений push</span><span class="sxs-lookup"><span data-stu-id="0bb5f-138"><a id="update-app"></a>Add push notifications tooyour app</span></span>
<span data-ttu-id="0bb5f-139">Затем приложение необходимо зарегистрировать для получения push-уведомлений при запуске.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-139">Next, your app must register for push notifications on start-up.</span></span> <span data-ttu-id="0bb5f-140">Уже включена аутентификация, убедитесь в том, что hello пользователь выполняет вход перед попыткой tooregister push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-140">When you have already enabled authentication, make sure that hello user signs-in before trying tooregister for push notifications.</span></span>

1. <span data-ttu-id="0bb5f-141">Откройте hello **App.xaml.cs** файл проекта и добавьте следующее hello `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="0bb5f-141">Open hello **App.xaml.cs** project file and add hello following `using` statements:</span></span>

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. <span data-ttu-id="0bb5f-142">В hello того же файла, добавьте следующее hello **InitNotificationsAsync** toohello определение метода **приложения** класса:</span><span class="sxs-lookup"><span data-stu-id="0bb5f-142">In hello same file, add hello following **InitNotificationsAsync** method definition toohello **App** class:</span></span>

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register hello channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    <span data-ttu-id="0bb5f-143">Этот код извлекает из WNS hello ChannelURI для приложения hello и затем выполняется регистрация, ChannelURI приложение мобильного приложения службы.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-143">This code retrieves hello ChannelURI for hello app from WNS, and then registers that ChannelURI with your App Service Mobile App.</span></span>
3. <span data-ttu-id="0bb5f-144">Вверху hello hello **OnLaunched** обработчик событий в **App.xaml.cs**, добавить hello **async** определение метода toohello модификатор и добавьте hello следующий вызов toohello новый  **InitNotificationsAsync** методом, как следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="0bb5f-144">At hello top of hello **OnLaunched** event handler in **App.xaml.cs**, add hello **async** modifier toohello method definition and add hello following call toohello new **InitNotificationsAsync** method, as in hello following example:</span></span>

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    <span data-ttu-id="0bb5f-145">Это гарантирует, что приветствия кратковременных ChannelURI регистрируется при каждом запуске приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-145">This guarantees that hello short-lived ChannelURI is registered each time hello application is launched.</span></span>
4. <span data-ttu-id="0bb5f-146">Перестройте проект приложения UWP.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-146">Rebuild your UWP app project.</span></span> <span data-ttu-id="0bb5f-147">Приложение больше не готов tooreceive всплывающие уведомления.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-147">Your app is now ready tooreceive toast notifications.</span></span>

## <span data-ttu-id="0bb5f-148"><a id="test"></a>Тестирование push-уведомлений в приложении</span><span class="sxs-lookup"><span data-stu-id="0bb5f-148"><a id="test"></a>Test push notifications in your app</span></span>
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <span data-ttu-id="0bb5f-149"><a id="more"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0bb5f-149"><a id="more"></a>Next steps</span></span>
<span data-ttu-id="0bb5f-150">Дополнительные сведения о push-уведомлениях:</span><span class="sxs-lookup"><span data-stu-id="0bb5f-150">Learn more about push notifications:</span></span>

* [<span data-ttu-id="0bb5f-151">Управление toouse hello клиента для мобильных приложений Azure</span><span class="sxs-lookup"><span data-stu-id="0bb5f-151">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  <span data-ttu-id="0bb5f-152">Шаблоны обеспечивают гибкость toosend кросс платформенных Push-уведомлений, а также локализованные Push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-152">Templates give you flexibility toosend cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="0bb5f-153">Узнайте, как шаблоны tooregister.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-153">Learn how tooregister templates.</span></span>
* [<span data-ttu-id="0bb5f-154">Диагностика неполадок, связанных с push-уведомлениями</span><span class="sxs-lookup"><span data-stu-id="0bb5f-154">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="0bb5f-155">Существуют различные причины, по которым уведомления могут теряться или не доходить до устройств.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-155">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="0bb5f-156">В этом разделе показано, как tooanalyze и выясните, hello корневой причиной сбоев уведомлений push.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-156">This topic shows you how tooanalyze and figure out hello root cause of push notification failures.</span></span>

<span data-ttu-id="0bb5f-157">Рассмотрим, продолжая tooone из hello следующие учебники:</span><span class="sxs-lookup"><span data-stu-id="0bb5f-157">Consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="0bb5f-158">Добавить приложение tooyour проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="0bb5f-158">Add authentication tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="0bb5f-159">Узнайте, как пользователи tooauthenticate приложения с поставщиком удостоверений.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-159">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="0bb5f-160">Включение автономной синхронизации для приложения</span><span class="sxs-lookup"><span data-stu-id="0bb5f-160">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="0bb5f-161">Узнайте, как автономные tooadd поддерживают приложения с помощью внутреннего сервера мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-161">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="0bb5f-162">Автономная синхронизация позволяет конечным пользователям toointeract с мобильным приложением&mdash;Просмотр, добавление или изменение данных&mdash;даже в том случае, если нет сетевого соединения.</span><span class="sxs-lookup"><span data-stu-id="0bb5f-162">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
