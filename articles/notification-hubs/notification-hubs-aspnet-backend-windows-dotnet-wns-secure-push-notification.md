---
title: "aaaAzure Secure принудительной отправки уведомлений концентраторы"
description: "Узнайте, как безопасные toosend push-уведомления в Azure. Примеры кода на языке C# с использованием hello .NET API."
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 5aef50f4-80b3-460e-a9a7-7435001273bd
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: b6fe16c96d28d75ff698278409fb012472ba6396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="41c56-104">Безопасные push-уведомления посредством центров уведомлений Azure</span><span class="sxs-lookup"><span data-stu-id="41c56-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="41c56-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="41c56-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="41c56-106">iOS</span><span class="sxs-lookup"><span data-stu-id="41c56-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="41c56-107">Android</span><span class="sxs-lookup"><span data-stu-id="41c56-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="41c56-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="41c56-108">Overview</span></span>
<span data-ttu-id="41c56-109">Поддержка уведомлений Push в Microsoft Azure позволяет tooaccess к использованию, несколькими платформами, масштабируемых push-инфраструктуру, которая значительно упрощает реализацию hello push-уведомлений для индивидуальных пользователей и корпоративных приложений для мобильных устройств платформы.</span><span class="sxs-lookup"><span data-stu-id="41c56-109">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="41c56-110">Иногда из-за ограничений tooregulatory или безопасности, приложение может возникнуть tooinclude что-нибудь в hello уведомление, которое не может передаваться через инфраструктуру hello Стандартная push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="41c56-110">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="41c56-111">В данном учебнике как tooachieve hello такие же возможности, отправляя конфиденциальных данных через проверку подлинности безопасное соединение между hello клиентского устройства и внутреннего сервера приложения hello.</span><span class="sxs-lookup"><span data-stu-id="41c56-111">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client device and hello app backend.</span></span>

<span data-ttu-id="41c56-112">На высоком уровне hello поток выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="41c56-112">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="41c56-113">Hello приложения внутреннего интерфейса:</span><span class="sxs-lookup"><span data-stu-id="41c56-113">hello app back-end:</span></span>
   * <span data-ttu-id="41c56-114">Сохраняет полезную нагрузку в базе данных серверной части.</span><span class="sxs-lookup"><span data-stu-id="41c56-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="41c56-115">Отправляет идентификатор hello toohello устройства создания уведомления (отправляются без защиты данных).</span><span class="sxs-lookup"><span data-stu-id="41c56-115">Sends hello ID of this notification toohello device (no secure information is sent).</span></span>
2. <span data-ttu-id="41c56-116">приложение Hello на устройстве hello, при получении уведомления hello:</span><span class="sxs-lookup"><span data-stu-id="41c56-116">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="41c56-117">устройство Hello обращается hello серверной части запроса hello безопасного полезных данных.</span><span class="sxs-lookup"><span data-stu-id="41c56-117">hello device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="41c56-118">приложение Hello можно показать hello полезных данных в виде уведомлений на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="41c56-118">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="41c56-119">Очень важно, toonote, что предшествующий потока hello (и в этом учебнике) предполагается устройства hello склада маркер проверки подлинности в локальном хранилище после hello пользователь вошел в систему.</span><span class="sxs-lookup"><span data-stu-id="41c56-119">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="41c56-120">Это гарантирует полностью эффективной работы, как hello устройства можно получить полезные данные безопасного hello уведомления, с помощью этого токена.</span><span class="sxs-lookup"><span data-stu-id="41c56-120">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="41c56-121">Если приложение не хранить токены проверки подлинности на устройстве hello или может быть просрочен эти токены, hello приложения для устройств, при получении уведомления hello отображать универсального уведомление запроса приложение hello toolaunch hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="41c56-121">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="41c56-122">Затем приложение Hello проверяет подлинность пользователя hello и приводятся полезные данные уведомления hello.</span><span class="sxs-lookup"><span data-stu-id="41c56-122">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="41c56-123">В этом учебнике принудительной защиты как toosend push-уведомление безопасно.</span><span class="sxs-lookup"><span data-stu-id="41c56-123">This Secure Push tutorial shows how toosend a push notification securely.</span></span> <span data-ttu-id="41c56-124">Hello учебник построен на hello [уведомить пользователей](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) учебник, поэтому hello шаги в этом учебнике должна выполнять первой.</span><span class="sxs-lookup"><span data-stu-id="41c56-124">hello tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, so you should complete hello steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="41c56-125">В этом учебнике подразумевается, что вы создали и настроили центр уведомлений в соответствии с описанием в руководстве [Приступая к работе с центрами уведомлений (Магазин Windows)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="41c56-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span></span>
> <span data-ttu-id="41c56-126">Кроме того, обратите внимание, что для Windows Phone 8.1 требуются учетные данные Windows (не Windows Phone) и что фоновые задачи не работают на Windows Phone 8.0 и в Silverlight 8.1.</span><span class="sxs-lookup"><span data-stu-id="41c56-126">Also, note that Windows Phone 8.1 requires Windows (not Windows Phone) credentials, and that background tasks do not work on Windows Phone 8.0 or Silverlight 8.1.</span></span> <span data-ttu-id="41c56-127">Для приложений для магазина Windows, можно получать уведомления в фоновом режиме, только в том случае, если включить экран блокировки является приложение hello (щелкните флажок hello в hello Appmanifest).</span><span class="sxs-lookup"><span data-stu-id="41c56-127">For Windows Store applications, you can receive notifications via a background task only if hello app is lock-screen enabled (click hello checkbox in hello Appmanifest).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-windows-phone-project"></a><span data-ttu-id="41c56-128">Изменение hello проекта Windows Phone</span><span class="sxs-lookup"><span data-stu-id="41c56-128">Modify hello Windows Phone Project</span></span>
1. <span data-ttu-id="41c56-129">В hello **NotifyUserWindowsPhone** , добавьте следующий код tooApp.xaml.cs tooregister hello принудительной фоновой задачей hello.</span><span class="sxs-lookup"><span data-stu-id="41c56-129">In hello **NotifyUserWindowsPhone** project, add hello following code tooApp.xaml.cs tooregister hello push background task.</span></span> <span data-ttu-id="41c56-130">Добавьте следующие строки кода в конце hello hello hello `OnLaunched()` метод:</span><span class="sxs-lookup"><span data-stu-id="41c56-130">Add hello following line of code at hello end of hello `OnLaunched()` method:</span></span>
   
        RegisterBackgroundTask();
2. <span data-ttu-id="41c56-131">По-прежнему в App.xaml.cs, добавьте следующий код сразу после hello hello `OnLaunched()` метод:</span><span class="sxs-lookup"><span data-stu-id="41c56-131">Still in App.xaml.cs, add hello following code immediately after hello `OnLaunched()` method:</span></span>
   
        private async void RegisterBackgroundTask()
        {
            if (!Windows.ApplicationModel.Background.BackgroundTaskRegistration.AllTasks.Any(i => i.Value.Name == "PushBackgroundTask"))
            {
                var result = await BackgroundExecutionManager.RequestAccessAsync();
                var builder = new BackgroundTaskBuilder();
   
                builder.Name = "PushBackgroundTask";
                builder.TaskEntryPoint = typeof(PushBackgroundComponent.PushBackgroundTask).FullName;
                builder.SetTrigger(new Windows.ApplicationModel.Background.PushNotificationTrigger());
                BackgroundTaskRegistration task = builder.Register();
            }
        }
3. <span data-ttu-id="41c56-132">Добавьте следующее hello `using` операторы в начале hello hello App.xaml.cs файла:</span><span class="sxs-lookup"><span data-stu-id="41c56-132">Add hello following `using` statements at hello top of hello App.xaml.cs file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. <span data-ttu-id="41c56-133">Из hello **файл** меню в Visual Studio щелкните **сохранить все**.</span><span class="sxs-lookup"><span data-stu-id="41c56-133">From hello **File** menu in Visual Studio, click **Save All**.</span></span>

## <a name="create-hello-push-background-component"></a><span data-ttu-id="41c56-134">Создать hello Push фона компонента</span><span class="sxs-lookup"><span data-stu-id="41c56-134">Create hello Push Background Component</span></span>
<span data-ttu-id="41c56-135">Hello следующим шагом является toocreate hello принудительной фона компонента.</span><span class="sxs-lookup"><span data-stu-id="41c56-135">hello next step is toocreate hello push background component.</span></span>

1. <span data-ttu-id="41c56-136">В обозревателе решений щелкните правой кнопкой мыши узел верхнего уровня hello hello решения (**SecurePush решения** в данном случае), нажмите кнопку **добавить**, нажмите кнопку **новый проект**.</span><span class="sxs-lookup"><span data-stu-id="41c56-136">In Solution Explorer, right-click hello top-level node of hello solution (**Solution SecurePush** in this case), then click **Add**, then click **New Project**.</span></span>
2. <span data-ttu-id="41c56-137">Разверните пункт **Приложения Магазина**, затем щелкните **Приложения Windows Phone** и выберите **Компонент среды выполнения Windows (Windows Phone)**.</span><span class="sxs-lookup"><span data-stu-id="41c56-137">Expand **Store Apps**, then click **Windows Phone Apps**, then click **Windows Runtime Component (Windows Phone)**.</span></span> <span data-ttu-id="41c56-138">Имя проекта hello **PushBackgroundComponent**и нажмите кнопку **ОК** toocreate hello проекта.</span><span class="sxs-lookup"><span data-stu-id="41c56-138">Name hello project **PushBackgroundComponent**, and then click **OK** toocreate hello project.</span></span>
   
    ![][12]
3. <span data-ttu-id="41c56-139">В обозревателе решений щелкните правой кнопкой мыши hello **PushBackgroundComponent (Windows Phone 8.1)** проекта, а затем нажмите кнопку **добавить**, нажмите кнопку **класса**.</span><span class="sxs-lookup"><span data-stu-id="41c56-139">In Solution Explorer, right-click hello **PushBackgroundComponent (Windows Phone 8.1)** project, then click **Add**, then click **Class**.</span></span> <span data-ttu-id="41c56-140">Имя нового класса hello **PushBackgroundTask.cs**.</span><span class="sxs-lookup"><span data-stu-id="41c56-140">Name hello new class **PushBackgroundTask.cs**.</span></span> <span data-ttu-id="41c56-141">Нажмите кнопку **добавить** toogenerate hello класса.</span><span class="sxs-lookup"><span data-stu-id="41c56-141">Click **Add** toogenerate hello class.</span></span>
4. <span data-ttu-id="41c56-142">Замените все содержимое hello hello **PushBackgroundComponent** определения пространства имен с hello после кода, заменив заполнитель hello `{back-end endpoint}` с конечной точкой hello серверной части, полученный при развертывании вашей Тыловой:</span><span class="sxs-lookup"><span data-stu-id="41c56-142">Replace hello entire contents of hello **PushBackgroundComponent** namespace definition with hello following code, substituting hello placeholder `{back-end endpoint}` with hello back-end endpoint obtained while deploying your back-end:</span></span>
   
        public sealed class Notification
            {
                public int Id { get; set; }
                public string Payload { get; set; }
                public bool Read { get; set; }
            }
   
            public sealed class PushBackgroundTask : IBackgroundTask
            {
                private string GET_URL = "{back-end endpoint}/api/notifications/";
   
                async void IBackgroundTask.Run(IBackgroundTaskInstance taskInstance)
                {
                    // Store hello content received from hello notification so it can be retrieved from hello UI.
                    RawNotification raw = (RawNotification)taskInstance.TriggerDetails;
                    var notificationId = raw.Content;
   
                    // retrieve content
                    BackgroundTaskDeferral deferral = taskInstance.GetDeferral();
                    var httpClient = new HttpClient();
                    var settings = ApplicationData.Current.LocalSettings.Values;
                    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                    var notificationString = await httpClient.GetStringAsync(GET_URL + notificationId);
   
                    var notification = JsonConvert.DeserializeObject<Notification>(notificationString);
   
                    ShowToast(notification);
   
                    deferral.Complete();
                }
   
                private void ShowToast(Notification notification)
                {
                    ToastTemplateType toastTemplate = ToastTemplateType.ToastText01;
                    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(toastTemplate);
                    XmlNodeList toastTextElements = toastXml.GetElementsByTagName("text");
                    toastTextElements[0].AppendChild(toastXml.CreateTextNode(notification.Payload));
                    ToastNotification toast = new ToastNotification(toastXml);
                    ToastNotificationManager.CreateToastNotifier().Show(toast);
                }
            }
5. <span data-ttu-id="41c56-143">В обозревателе решений щелкните правой кнопкой мыши hello **PushBackgroundComponent (Windows Phone 8.1)** проект и выберите пункт **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="41c56-143">In Solution Explorer, right-click hello **PushBackgroundComponent (Windows Phone 8.1)** project and then click **Manage NuGet Packages**.</span></span>
6. <span data-ttu-id="41c56-144">В левой части окна hello, выберите **Online**.</span><span class="sxs-lookup"><span data-stu-id="41c56-144">On hello left-hand side, click **Online**.</span></span>
7. <span data-ttu-id="41c56-145">В hello **поиска** введите **HTTP-клиент**.</span><span class="sxs-lookup"><span data-stu-id="41c56-145">In hello **Search** box, type **Http Client**.</span></span>
8. <span data-ttu-id="41c56-146">В списке результатов hello, нажмите кнопку **клиентских библиотек HTTP Майкрософт**, а затем нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="41c56-146">In hello results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="41c56-147">Завершить установку hello.</span><span class="sxs-lookup"><span data-stu-id="41c56-147">Complete hello installation.</span></span>
9. <span data-ttu-id="41c56-148">Вернитесь в hello NuGet **поиска** введите **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="41c56-148">Back in hello NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="41c56-149">Установка hello **Json.NET** пакета, а затем hello закрыть окно диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="41c56-149">Install hello **Json.NET** package, then close hello NuGet Package Manager window.</span></span>
10. <span data-ttu-id="41c56-150">Добавьте следующее hello `using` инструкции вверху hello hello **PushBackgroundTask.cs** файла:</span><span class="sxs-lookup"><span data-stu-id="41c56-150">Add hello following `using` statements at hello top of hello **PushBackgroundTask.cs** file:</span></span>
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. <span data-ttu-id="41c56-151">В обозревателе решений в hello **NotifyUserWindowsPhone (Windows Phone 8.1)** щелкните правой кнопкой мыши проект **ссылки**, нажмите кнопку **добавить ссылку...** . В диалоговом окне диспетчера ссылок hello, установите флажок "hello" рядом слишком**PushBackgroundComponent**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="41c56-151">In Solution Explorer, in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** project, right-click **References**, then click **Add Reference...**. In hello Reference Manager dialog, check hello box next too**PushBackgroundComponent**, and then click **OK**.</span></span>
12. <span data-ttu-id="41c56-152">В обозревателе решений дважды щелкните **Package.appxmanifest** в hello **NotifyUserWindowsPhone (Windows Phone 8.1)** проекта.</span><span class="sxs-lookup"><span data-stu-id="41c56-152">In Solution Explorer, double-click **Package.appxmanifest** in hello **NotifyUserWindowsPhone (Windows Phone 8.1)** project.</span></span> <span data-ttu-id="41c56-153">В разделе **уведомления**, задайте **поддержкой всплывающих** слишком**Да**.</span><span class="sxs-lookup"><span data-stu-id="41c56-153">Under **Notifications**, set **Toast Capable** too**Yes**.</span></span>
    
    ![][3]
13. <span data-ttu-id="41c56-154">В по-прежнему **Package.appxmanifest**, нажмите кнопку hello **объявления** меню верхней hello.</span><span class="sxs-lookup"><span data-stu-id="41c56-154">Still in **Package.appxmanifest**, click hello **Declarations** menu near hello top.</span></span> <span data-ttu-id="41c56-155">В hello **доступные объявления** раскрывающийся список, нажмите кнопку **фоновые задачи**, а затем нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="41c56-155">In hello **Available Declarations** dropdown, click **Background Tasks**, and then click **Add**.</span></span>
14. <span data-ttu-id="41c56-156">В **Package.appxmanifest** в разделе **Свойства** включите параметр **Push-уведомление**.</span><span class="sxs-lookup"><span data-stu-id="41c56-156">In **Package.appxmanifest**, under **Properties**, check **Push notification**.</span></span>
15. <span data-ttu-id="41c56-157">В **Package.appxmanifest**в разделе **параметры приложения**, тип **PushBackgroundComponent.PushBackgroundTask** в hello **точки входа** поле.</span><span class="sxs-lookup"><span data-stu-id="41c56-157">In **Package.appxmanifest**, under **App Settings**, type **PushBackgroundComponent.PushBackgroundTask** in hello **Entry Point** field.</span></span>
    
    ![][13]
16. <span data-ttu-id="41c56-158">Из hello **файл** меню, нажмите кнопку **сохранить все**.</span><span class="sxs-lookup"><span data-stu-id="41c56-158">From hello **File** menu, click **Save All**.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="41c56-159">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="41c56-159">Run hello Application</span></span>
<span data-ttu-id="41c56-160">toorun Здравствуйте, приложения, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="41c56-160">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="41c56-161">В Visual Studio, запустите hello **AppBackend** приложения веб-API.</span><span class="sxs-lookup"><span data-stu-id="41c56-161">In Visual Studio, run hello **AppBackend** Web API application.</span></span> <span data-ttu-id="41c56-162">Отобразится веб-страница ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="41c56-162">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="41c56-163">В Visual Studio, запустите hello **NotifyUserWindowsPhone (Windows Phone 8.1)** приложения Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="41c56-163">In Visual Studio, run hello **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone app.</span></span> <span data-ttu-id="41c56-164">Эмулятор Windows Phone Hello запускается и автоматически загружает приложение hello.</span><span class="sxs-lookup"><span data-stu-id="41c56-164">hello Windows Phone emulator runs and loads hello app automatically.</span></span>
3. <span data-ttu-id="41c56-165">В hello **NotifyUserWindowsPhone** приложения пользовательского интерфейса, введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="41c56-165">In hello **NotifyUserWindowsPhone** app UI, enter a username and password.</span></span> <span data-ttu-id="41c56-166">Это может быть любой строкой, но они должны быть hello одинаковое значение.</span><span class="sxs-lookup"><span data-stu-id="41c56-166">These can be any string, but they must be hello same value.</span></span>
4. <span data-ttu-id="41c56-167">В hello **NotifyUserWindowsPhone** приложения пользовательского интерфейса, нажмите кнопку **входа и регистрации**.</span><span class="sxs-lookup"><span data-stu-id="41c56-167">In hello **NotifyUserWindowsPhone** app UI, click **Log in and register**.</span></span> <span data-ttu-id="41c56-168">Затем нажмите **Отправить push-уведомление**.</span><span class="sxs-lookup"><span data-stu-id="41c56-168">Then click **Send push**.</span></span>

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
