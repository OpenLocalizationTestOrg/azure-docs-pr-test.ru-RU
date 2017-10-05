---
title: "Безопасные push-уведомления для концентраторов уведомлений Azure"
description: "Узнайте, как отправлять безопасные push-уведомления в Azure. Примеры кода написаны на C# с использованием API .NET."
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
ms.openlocfilehash: 9c626ec1534c4899588150a58c0da57b9d963f6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="88bfd-104">Безопасные push-уведомления для концентраторов уведомлений Azure</span><span class="sxs-lookup"><span data-stu-id="88bfd-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="88bfd-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="88bfd-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="88bfd-106">iOS</span><span class="sxs-lookup"><span data-stu-id="88bfd-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="88bfd-107">Android</span><span class="sxs-lookup"><span data-stu-id="88bfd-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="88bfd-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="88bfd-108">Overview</span></span>
<span data-ttu-id="88bfd-109">Поддержка push-уведомлений в Microsoft Azure позволяет получить доступ к простой в использовании, многоплатформенной и масштабируемой инфраструктуре для отправки push-уведомлений, которая значительно упрощает реализацию push-уведомлений как для индивидуальных пользователей, так и для корпоративных приложений для мобильных платформ.</span><span class="sxs-lookup"><span data-stu-id="88bfd-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="88bfd-110">Из-за ограничений, связанных с правовыми нормами или обеспечением безопасности, иногда в уведомлении могут присутствовать данные, которые нельзя передать через стандартную инфраструктуру push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="88bfd-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="88bfd-111">В этом учебнике рассказывается о том, как реализовать этот принцип при отправке важной информации через защищенное соединение с проверкой подлинности, установленное между устройством клиента и серверной частью приложения.</span><span class="sxs-lookup"><span data-stu-id="88bfd-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span></span>

<span data-ttu-id="88bfd-112">На высоком уровне поток можно представить следующим образом.</span><span class="sxs-lookup"><span data-stu-id="88bfd-112">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="88bfd-113">Серверная часть приложения:</span><span class="sxs-lookup"><span data-stu-id="88bfd-113">The app back-end:</span></span>
   * <span data-ttu-id="88bfd-114">Сохраняет полезную нагрузку в базе данных серверной части.</span><span class="sxs-lookup"><span data-stu-id="88bfd-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="88bfd-115">Отправляет идентификатор этого уведомления устройству (защищаемые сведения не передаются).</span><span class="sxs-lookup"><span data-stu-id="88bfd-115">Sends the ID of this notification to the device (no secure information is sent).</span></span>
2. <span data-ttu-id="88bfd-116">Приложение на устройстве при получении уведомления:</span><span class="sxs-lookup"><span data-stu-id="88bfd-116">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="88bfd-117">Устройство связывается с серверной частью и запрашивает полезную нагрузку.</span><span class="sxs-lookup"><span data-stu-id="88bfd-117">The device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="88bfd-118">Приложение может показывать полезную нагрузку в виде уведомления на устройстве.</span><span class="sxs-lookup"><span data-stu-id="88bfd-118">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="88bfd-119">Стоит отметить: в предыдущем потоке (и в этом учебнике) мы предположили, что устройство сохраняет маркер проверки подлинности в локальном хранилище после входа пользователя.</span><span class="sxs-lookup"><span data-stu-id="88bfd-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="88bfd-120">Таким образом обеспечивается удобство работы, так как с помощью этого маркера устройство способно получать безопасные полезные данные уведомлений.</span><span class="sxs-lookup"><span data-stu-id="88bfd-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="88bfd-121">Если приложение не сохраняет маркеры проверки подлинности на устройстве, или если истек срок действия маркеров, приложение устройства, после получения уведомления, должно отобразить общее уведомление, предлагая пользователю запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="88bfd-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="88bfd-122">Затем приложение выполняет проверку подлинности пользователя и отображает полезную нагрузку уведомления.</span><span class="sxs-lookup"><span data-stu-id="88bfd-122">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="88bfd-123">В этом учебнике по безопасности push-уведомлений показано, как безопасно отправлять push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="88bfd-123">This Secure Push tutorial shows how to send a push notification securely.</span></span> <span data-ttu-id="88bfd-124">Данное руководство является продолжением другого учебника под названием [Уведомление пользователей](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) , поэтому необходимо сначала выполнить шаги в указанном учебнике.</span><span class="sxs-lookup"><span data-stu-id="88bfd-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="88bfd-125">В этом учебнике подразумевается, что вы создали и настроили центр уведомлений в соответствии с описанием в руководстве [Приступая к работе с центрами уведомлений (Магазин Windows)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="88bfd-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span></span>
> <span data-ttu-id="88bfd-126">Кроме того, обратите внимание, что для Windows Phone 8.1 требуются учетные данные Windows (не Windows Phone) и что фоновые задачи не работают на Windows Phone 8.0 и в Silverlight 8.1.</span><span class="sxs-lookup"><span data-stu-id="88bfd-126">Also, note that Windows Phone 8.1 requires Windows (not Windows Phone) credentials, and that background tasks do not work on Windows Phone 8.0 or Silverlight 8.1.</span></span> <span data-ttu-id="88bfd-127">При работе в приложениями из Магазина Windows уведомления можно получать через фоновую задачу только в том случае, если включен экран блокировки приложения (установите флажок в Appmanifest).</span><span class="sxs-lookup"><span data-stu-id="88bfd-127">For Windows Store applications, you can receive notifications via a background task only if the app is lock-screen enabled (click the checkbox in the Appmanifest).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-windows-phone-project"></a><span data-ttu-id="88bfd-128">Изменение проекта для Windows Phone</span><span class="sxs-lookup"><span data-stu-id="88bfd-128">Modify the Windows Phone Project</span></span>
1. <span data-ttu-id="88bfd-129">В проекте **NotifyUserWindowsPhone** добавьте следующий код в App.xaml.cs, чтобы зарегистрировать фоновую задачу push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="88bfd-129">In the **NotifyUserWindowsPhone** project, add the following code to App.xaml.cs to register the push background task.</span></span> <span data-ttu-id="88bfd-130">В конце метода `OnLaunched()` добавьте следующую строку кода:</span><span class="sxs-lookup"><span data-stu-id="88bfd-130">Add the following line of code at the end of the `OnLaunched()` method:</span></span>
   
        RegisterBackgroundTask();
2. <span data-ttu-id="88bfd-131">Находясь в App.xaml.cs, добавьте следующий код сразу после метода `OnLaunched()` :</span><span class="sxs-lookup"><span data-stu-id="88bfd-131">Still in App.xaml.cs, add the following code immediately after the `OnLaunched()` method:</span></span>
   
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
3. <span data-ttu-id="88bfd-132">Добавьте в начало файла App.xaml.cs следующие операторы `using` :</span><span class="sxs-lookup"><span data-stu-id="88bfd-132">Add the following `using` statements at the top of the App.xaml.cs file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. <span data-ttu-id="88bfd-133">В меню **Файл** Visual Studio выберите **Сохранить все**.</span><span class="sxs-lookup"><span data-stu-id="88bfd-133">From the **File** menu in Visual Studio, click **Save All**.</span></span>

## <a name="create-the-push-background-component"></a><span data-ttu-id="88bfd-134">Создайте фоновый компонент push-уведомления</span><span class="sxs-lookup"><span data-stu-id="88bfd-134">Create the Push Background Component</span></span>
<span data-ttu-id="88bfd-135">Следующий шаг заключается в создании фонового компонента push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="88bfd-135">The next step is to create the push background component.</span></span>

1. <span data-ttu-id="88bfd-136">В обозревателе решений щелкните правой кнопкой мыши узел верхнего уровня решения (в данном случае — **Solution SecurePush**), а затем нажмите кнопку **Добавить**, после чего щелкните **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="88bfd-136">In Solution Explorer, right-click the top-level node of the solution (**Solution SecurePush** in this case), then click **Add**, then click **New Project**.</span></span>
2. <span data-ttu-id="88bfd-137">Разверните пункт **Приложения Магазина**, затем щелкните **Приложения Windows Phone** и выберите **Компонент среды выполнения Windows (Windows Phone)**.</span><span class="sxs-lookup"><span data-stu-id="88bfd-137">Expand **Store Apps**, then click **Windows Phone Apps**, then click **Windows Runtime Component (Windows Phone)**.</span></span> <span data-ttu-id="88bfd-138">Присвойте проекту имя **PushBackgroundComponent**, а затем нажмите кнопку **ОК**, чтобы создать проект.</span><span class="sxs-lookup"><span data-stu-id="88bfd-138">Name the project **PushBackgroundComponent**, and then click **OK** to create the project.</span></span>
   
    ![][12]
3. <span data-ttu-id="88bfd-139">В обозревателе решений щелкните правой кнопкой мыши проект **PushBackgroundComponent (Windows Phone 8.1)**, а затем щелкните **Добавить** и выберите **Класс**.</span><span class="sxs-lookup"><span data-stu-id="88bfd-139">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project, then click **Add**, then click **Class**.</span></span> <span data-ttu-id="88bfd-140">Присвойте новому классу имя **PushBackgroundTask.cs**.</span><span class="sxs-lookup"><span data-stu-id="88bfd-140">Name the new class **PushBackgroundTask.cs**.</span></span> <span data-ttu-id="88bfd-141">Щелкните кнопку **Добавить** , чтобы создать класс.</span><span class="sxs-lookup"><span data-stu-id="88bfd-141">Click **Add** to generate the class.</span></span>
4. <span data-ttu-id="88bfd-142">Замените все содержимое определения пространства имен **PushBackgroundComponent** следующим кодом, заменив заполнитель `{back-end endpoint}` конечной точкой серверной части, полученной при развертывании серверной части:</span><span class="sxs-lookup"><span data-stu-id="88bfd-142">Replace the entire contents of the **PushBackgroundComponent** namespace definition with the following code, substituting the placeholder `{back-end endpoint}` with the back-end endpoint obtained while deploying your back-end:</span></span>
   
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
                    // Store the content received from the notification so it can be retrieved from the UI.
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
5. <span data-ttu-id="88bfd-143">В обозревателе решений щелкните правой кнопкой мыши проект **PushBackgroundComponent (Windows Phone 8.1)**, а затем щелкните **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="88bfd-143">In Solution Explorer, right-click the **PushBackgroundComponent (Windows Phone 8.1)** project and then click **Manage NuGet Packages**.</span></span>
6. <span data-ttu-id="88bfd-144">В левой части окна выберите **В сети**.</span><span class="sxs-lookup"><span data-stu-id="88bfd-144">On the left-hand side, click **Online**.</span></span>
7. <span data-ttu-id="88bfd-145">В текстовом поле **Поиск** введите **Клиент HTTP**.</span><span class="sxs-lookup"><span data-stu-id="88bfd-145">In the **Search** box, type **Http Client**.</span></span>
8. <span data-ttu-id="88bfd-146">В списке результатов выберите **Клиентские библиотеки Microsoft HTTP** и нажмите **Установить**.</span><span class="sxs-lookup"><span data-stu-id="88bfd-146">In the results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="88bfd-147">Выполните установку.</span><span class="sxs-lookup"><span data-stu-id="88bfd-147">Complete the installation.</span></span>
9. <span data-ttu-id="88bfd-148">Вернитесь к полю NuGet **Поиск** и введите **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="88bfd-148">Back in the NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="88bfd-149">Установите пакет **Json.NET** , затем закройте окно диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="88bfd-149">Install the **Json.NET** package, then close the NuGet Package Manager window.</span></span>
10. <span data-ttu-id="88bfd-150">Добавьте следующие операторы `using` в начало файла **PushBackgroundTask.cs** :</span><span class="sxs-lookup"><span data-stu-id="88bfd-150">Add the following `using` statements at the top of the **PushBackgroundTask.cs** file:</span></span>
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. <span data-ttu-id="88bfd-151">В обозревателе решений в проекте **NotifyUserWindowsPhone (Windows Phone 8.1)** щелкните правой кнопкой мыши **Ссылки**, а затем щелкните **Добавить ссылку...**.</span><span class="sxs-lookup"><span data-stu-id="88bfd-151">In Solution Explorer, in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project, right-click **References**, then click **Add Reference...**.</span></span> <span data-ttu-id="88bfd-152">В диалоговом окне "Диспетчер ссылок" установите флажок **PushBackgroundComponent**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="88bfd-152">In the Reference Manager dialog, check the box next to **PushBackgroundComponent**, and then click **OK**.</span></span>
12. <span data-ttu-id="88bfd-153">В обозревателе решений дважды щелкните **Package.appxmanifest** в проекте **NotifyUserWindowsPhone (Windows Phone 8.1)**.</span><span class="sxs-lookup"><span data-stu-id="88bfd-153">In Solution Explorer, double-click **Package.appxmanifest** in the **NotifyUserWindowsPhone (Windows Phone 8.1)** project.</span></span> <span data-ttu-id="88bfd-154">В поле **Уведомления** установите для параметра **Всплывающие уведомления** значение **Да**.</span><span class="sxs-lookup"><span data-stu-id="88bfd-154">Under **Notifications**, set **Toast Capable** to **Yes**.</span></span>
    
    ![][3]
13. <span data-ttu-id="88bfd-155">Находясь в **Package.appxmanifest**, откройте меню **Объявления** вверху.</span><span class="sxs-lookup"><span data-stu-id="88bfd-155">Still in **Package.appxmanifest**, click the **Declarations** menu near the top.</span></span> <span data-ttu-id="88bfd-156">В раскрывающемся списке **Доступные объявления** щелкните **Фоновые задачи** и затем нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="88bfd-156">In the **Available Declarations** dropdown, click **Background Tasks**, and then click **Add**.</span></span>
14. <span data-ttu-id="88bfd-157">В **Package.appxmanifest** в разделе **Свойства** включите параметр **Push-уведомление**.</span><span class="sxs-lookup"><span data-stu-id="88bfd-157">In **Package.appxmanifest**, under **Properties**, check **Push notification**.</span></span>
15. <span data-ttu-id="88bfd-158">В **Package.appxmanifest** в области **Параметры приложения** введите **PushBackgroundComponent.PushBackgroundTask** в поле **Точка входа**.</span><span class="sxs-lookup"><span data-stu-id="88bfd-158">In **Package.appxmanifest**, under **App Settings**, type **PushBackgroundComponent.PushBackgroundTask** in the **Entry Point** field.</span></span>
    
    ![][13]
16. <span data-ttu-id="88bfd-159">В меню **Файл** выберите **Сохранить все**.</span><span class="sxs-lookup"><span data-stu-id="88bfd-159">From the **File** menu, click **Save All**.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="88bfd-160">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="88bfd-160">Run the Application</span></span>
<span data-ttu-id="88bfd-161">Для запуска приложения выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="88bfd-161">To run the application, do the following:</span></span>

1. <span data-ttu-id="88bfd-162">В Visual Studio запустите приложение веб-API **AppBackend** .</span><span class="sxs-lookup"><span data-stu-id="88bfd-162">In Visual Studio, run the **AppBackend** Web API application.</span></span> <span data-ttu-id="88bfd-163">Отобразится веб-страница ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="88bfd-163">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="88bfd-164">В Visual Studio запустите приложение **NotifyUserWindowsPhone (Windows Phone 8.1)** для Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="88bfd-164">In Visual Studio, run the **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone app.</span></span> <span data-ttu-id="88bfd-165">Эмулятор Windows Phone запустится и автоматически загрузит приложение.</span><span class="sxs-lookup"><span data-stu-id="88bfd-165">The Windows Phone emulator runs and loads the app automatically.</span></span>
3. <span data-ttu-id="88bfd-166">В пользовательском интерфейсе приложения **NotifyUserWindowsPhone** введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="88bfd-166">In the **NotifyUserWindowsPhone** app UI, enter a username and password.</span></span> <span data-ttu-id="88bfd-167">Это могут быть любые совпадающие строки.</span><span class="sxs-lookup"><span data-stu-id="88bfd-167">These can be any string, but they must be the same value.</span></span>
4. <span data-ttu-id="88bfd-168">В пользовательском интерфейсе приложения **NotifyUserWindowsPhone** щелкните **Log in and register** (Вход и регистрация).</span><span class="sxs-lookup"><span data-stu-id="88bfd-168">In the **NotifyUserWindowsPhone** app UI, click **Log in and register**.</span></span> <span data-ttu-id="88bfd-169">Затем нажмите **Отправить push-уведомление**.</span><span class="sxs-lookup"><span data-stu-id="88bfd-169">Then click **Send push**.</span></span>

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
