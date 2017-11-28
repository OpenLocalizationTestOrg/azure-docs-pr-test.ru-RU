---
title: "Начало работы с Центрами уведомлений Azure для приложений универсальной платформы Windows | Документация Майкрософт"
description: "При работе с этим руководством вы узнаете, как отправлять push-уведомления в приложение универсальной платформы Windows с помощью Центров уведомлений Azure."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: erikre
ms.assetid: cf307cf3-8c58-4628-9c63-8751e6a0ef43
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 9b50f1cca81348b69f7ff2d702c6c72871afe0a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a><span data-ttu-id="190b3-103">Начало работы с Центрами уведомлений для приложений универсальной платформы Windows</span><span class="sxs-lookup"><span data-stu-id="190b3-103">Getting started with Notification Hubs for Windows Universal Platform Apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="190b3-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="190b3-104">Overview</span></span>
<span data-ttu-id="190b3-105">В этом руководстве показано, как использовать Центры уведомлений Azure для отправки push-уведомлений в приложение универсальной платформы Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="190b3-105">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Universal Windows Platform (UWP) app.</span></span>

<span data-ttu-id="190b3-106">В этом учебнике вам предстоит создать пустое приложение Магазина Windows, получающее push-уведомления с помощью службы push-уведомлений Windows (WNS).</span><span class="sxs-lookup"><span data-stu-id="190b3-106">In this tutorial, you create a blank Windows Store app that receives push notifications by using the Windows Push Notification Service (WNS).</span></span> <span data-ttu-id="190b3-107">По завершении вы сможете рассылать push-уведомления на все устройства, где запущено ваше приложение, с помощью центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="190b3-107">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="190b3-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="190b3-108">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="190b3-109">Полный код для этого учебника можно найти на портале [GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span><span class="sxs-lookup"><span data-stu-id="190b3-109">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="190b3-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="190b3-110">Prerequisites</span></span>
<span data-ttu-id="190b3-111">Для работы с данным учебником требуется следующее:</span><span class="sxs-lookup"><span data-stu-id="190b3-111">This tutorial requires the following:</span></span>

* <span data-ttu-id="190b3-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) или более поздняя версия.</span><span class="sxs-lookup"><span data-stu-id="190b3-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) or later</span></span>
* [<span data-ttu-id="190b3-113">Установленные средства разработки универсальных приложений Windows</span><span class="sxs-lookup"><span data-stu-id="190b3-113">Universal Windows App Development Tools installed</span></span>](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* <span data-ttu-id="190b3-114">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="190b3-114">An active Azure account</span></span> <br/><span data-ttu-id="190b3-115">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="190b3-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="190b3-116">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="190b3-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span></span>
* <span data-ttu-id="190b3-117">Активная учетная запись Магазина Windows.</span><span class="sxs-lookup"><span data-stu-id="190b3-117">An active Windows Store account</span></span>

<span data-ttu-id="190b3-118">Завершение изучения этого руководства является необходимым условием для работы со всеми другими руководствами, посвященными Центрам уведомлений для приложений универсальной платформы Windows.</span><span class="sxs-lookup"><span data-stu-id="190b3-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Universal Platform apps.</span></span>

## <a name="register-your-app-for-the-windows-store"></a><span data-ttu-id="190b3-119">Регистрация приложения для Магазина Windows</span><span class="sxs-lookup"><span data-stu-id="190b3-119">Register your app for the Windows Store</span></span>
<span data-ttu-id="190b3-120">Чтобы отправлять push-уведомления в приложения UWP, необходимо связать приложение с Магазином Windows.</span><span class="sxs-lookup"><span data-stu-id="190b3-120">To send push notifications to UWP apps, you must associate your app to the Windows Store.</span></span> <span data-ttu-id="190b3-121">После этого необходимо настроить концентратор уведомлений на интеграцию с WNS.</span><span class="sxs-lookup"><span data-stu-id="190b3-121">You must then configure your notification hub to integrate with WNS.</span></span>

1. <span data-ttu-id="190b3-122">Если вы еще не зарегистрировали свое приложение, перейдите в [Центр разработки для Windows](https://dev.windows.com/overview), войдите с помощью учетной записи Майкрософт, а затем щелкните **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="190b3-122">If you have not already registered your app, navigate to the [Windows Dev Center](https://dev.windows.com/overview), sign in with your Microsoft account, and then click **Create a new app**.</span></span>

2. <span data-ttu-id="190b3-123">Введите имя приложения и нажмите кнопку **Зарезервировать имя приложения**.</span><span class="sxs-lookup"><span data-stu-id="190b3-123">Type a name for your app and click **Reserve app name**.</span></span> <span data-ttu-id="190b3-124">При этом создается новая регистрация в Магазине Windows для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="190b3-124">This creates a new Windows Store registration for your app.</span></span>

3. <span data-ttu-id="190b3-125">В Visual Studio создайте проект приложения Visual C# для Магазина с помощью шаблона **Пустое приложение** универсального приложения Windows и щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="190b3-125">In Visual Studio, create a new Visual C# Store Apps project by using the Windows Universal **Blank App** template and click **OK**.</span></span>

4. <span data-ttu-id="190b3-126">Примите значения по умолчанию для целевой и минимальной версий платформы.</span><span class="sxs-lookup"><span data-stu-id="190b3-126">Accept the defaults for the target and minimum platform versions.</span></span>

5. <span data-ttu-id="190b3-127">В обозревателе решений щелкните правой кнопкой мыши проект приложения для Магазина Windows, щелкните **Магазин**, а затем — **Связать приложение с Магазином...**.</span><span class="sxs-lookup"><span data-stu-id="190b3-127">In Solution Explorer, right-click the Windows Store app project, click **Store**, and then click **Associate App with the Store...**.</span></span> <span data-ttu-id="190b3-128">Откроется мастер **Свяжите свое приложение с Магазином Windows** .</span><span class="sxs-lookup"><span data-stu-id="190b3-128">The **Associate Your App with the Windows Store** wizard appears.</span></span>

6. <span data-ttu-id="190b3-129">В мастере войдите с помощью учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="190b3-129">In the wizard, sign in with your Microsoft account.</span></span>

7. <span data-ttu-id="190b3-130">Выберите приложение, зарегистрированное на шаге 2, щелкните **Далее**, а затем — **Связать**.</span><span class="sxs-lookup"><span data-stu-id="190b3-130">Click the app that you registered in step 2, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="190b3-131">Это добавляет необходимые регистрационные данные Магазина Windows в манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="190b3-131">This adds the required Windows Store registration information to the application manifest.</span></span>

8. <span data-ttu-id="190b3-132">На странице [Центр разработки для Windows](http://dev.windows.com/overview) вашего нового приложения щелкните **Службы**, а затем **Push-уведомления** и **WNS/MPNS**.</span><span class="sxs-lookup"><span data-stu-id="190b3-132">Back on the [Windows Dev Center](http://dev.windows.com/overview) page for your new app, click **Services**, click **Push notifications**, and then click **WNS/MPNS**.</span></span>

9. <span data-ttu-id="190b3-133">Щелкните **Новое уведомление**.</span><span class="sxs-lookup"><span data-stu-id="190b3-133">Click **New Notification**.</span></span>

10. <span data-ttu-id="190b3-134">Щелкните шаблон **Blank (Toast)** (Пустое (всплывающее)) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="190b3-134">Click **Blank (Toast)** template and then click **OK**.</span></span>

11. <span data-ttu-id="190b3-135">Введите **имя** уведомления и **контекстное** сообщение Visual.</span><span class="sxs-lookup"><span data-stu-id="190b3-135">Enter a notification **Name** and Visual **Context** message.</span></span> <span data-ttu-id="190b3-136">Затем щелкните **Save as draft** (Сохранить как черновик).</span><span class="sxs-lookup"><span data-stu-id="190b3-136">Then click **Save as draft**.</span></span>

12. <span data-ttu-id="190b3-137">Перейдите на [портал регистрации приложений](http://apps.dev.microsoft.com) и войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="190b3-137">Navigate to the [Application Registration Portal](http://apps.dev.microsoft.com) and log in.</span></span>

13. <span data-ttu-id="190b3-138">Щелкните имя приложения.</span><span class="sxs-lookup"><span data-stu-id="190b3-138">Click on your application name.</span></span> <span data-ttu-id="190b3-139">Запишите значение пароля в разделе **секретов приложения** и значение **идентификатора безопасности пакета (SID)**, указанное в параметрах платформы **Магазина Windows**.</span><span class="sxs-lookup"><span data-stu-id="190b3-139">Make a note of the **Application Secret** password and the **Package security identifier (SID)** located in the **Windows Store** platform settings.</span></span>

     > [AZURE.WARNING]
    <span data-ttu-id="190b3-140">Секрет приложения и ИД безопасности пакета — это важные учетные данные для безопасного доступа.</span><span class="sxs-lookup"><span data-stu-id="190b3-140">The application secret and package SID are important security credentials.</span></span> <span data-ttu-id="190b3-141">Не сообщайте никому эти значения и не распространяйте их вместе со своим приложением.</span><span class="sxs-lookup"><span data-stu-id="190b3-141">Do not share these values with anyone or distribute them with your app.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="190b3-142">Настройка концентратора уведомлений</span><span class="sxs-lookup"><span data-stu-id="190b3-142">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="190b3-143">Выберите пункт <b>Службы уведомлений</b>, а затем — <b>Windows (WNS)</b>.</span><span class="sxs-lookup"><span data-stu-id="190b3-143">Select the <b>Notification Services</b> option and the <b>Windows (WNS)</b> option.</span></span> <span data-ttu-id="190b3-144">После этого в поле <b>Секрет приложения</b> введите значение <b>секрета приложения</b>.</span><span class="sxs-lookup"><span data-stu-id="190b3-144">Then enter the <b>Application secret</b> password in the <b>Security Key</b> field.</span></span> <span data-ttu-id="190b3-145">Введите значение <b>идентификатора безопасности пакета</b>, полученное из WNS при работе с предыдущим разделом, и нажмите кнопку <b>Сохранить</b>.</span><span class="sxs-lookup"><span data-stu-id="190b3-145">Enter your <b>Package SID</b> value that you obtained from WNS in the previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

<span data-ttu-id="190b3-146">Концентратор уведомлений теперь настроен для работы с WNS, и у вас есть строки подключения, чтобы зарегистрировать приложение и отправлять уведомления.</span><span class="sxs-lookup"><span data-stu-id="190b3-146">Your notification hub is now configured to work with WNS, and you have the connection strings to register your app and send notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="190b3-147">Подключение приложения к центру уведомлений</span><span class="sxs-lookup"><span data-stu-id="190b3-147">Connect your app to the notification hub</span></span>
1. <span data-ttu-id="190b3-148">В Visual Studio щелкните решение правой кнопкой мыши, а затем выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="190b3-148">In Visual Studio, right-click the solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="190b3-149">Откроется диалоговое окно **Управление пакетами NuGet** .</span><span class="sxs-lookup"><span data-stu-id="190b3-149">This displays the **Manage NuGet Packages** dialog box.</span></span>
2. <span data-ttu-id="190b3-150">Выполните поиск по запросу `WindowsAzure.Messaging.Managed` и нажмите кнопку **Установить**, после чего примите условия использования.</span><span class="sxs-lookup"><span data-stu-id="190b3-150">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and accept the terms of use.</span></span>
   
    ![][20]
   
    <span data-ttu-id="190b3-151">После этого будут выполнены скачивание, установка и добавление ссылки на библиотеку Azure Messaging для Windows с помощью <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">пакета NuGet WindowsAzure.Messaging.Managed</a>.</span><span class="sxs-lookup"><span data-stu-id="190b3-151">This downloads, installs, and adds a reference to the Azure Messaging library for Windows by using the <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
3. <span data-ttu-id="190b3-152">Откройте файл проекта App.xaml.cs и добавьте следующие операторы `using` .</span><span class="sxs-lookup"><span data-stu-id="190b3-152">Open the App.xaml.cs project file and add the following `using` statements.</span></span> 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. <span data-ttu-id="190b3-153">Кроме того, в файле App.xaml.cs добавьте определение метода **InitNotificationsAsync** в класс **App**:</span><span class="sxs-lookup"><span data-stu-id="190b3-153">Also in App.xaml.cs, add the following **InitNotificationsAsync** method definition to the **App** class:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    <span data-ttu-id="190b3-154">Этот код получает универсальный идентификатор ресурса (URI) канала для приложения из WNS, а затем регистрирует этот идентификатор в вашем центре уведомлений.</span><span class="sxs-lookup"><span data-stu-id="190b3-154">This code retrieves the channel URI for the app from WNS, and then registers that channel URI with your notification hub.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="190b3-155">Обязательно замените заполнитель your hub name именем центра уведомлений, которое отображается на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="190b3-155">Make sure to replace the "your hub name" placeholder with the name of the notification hub that appears in the Azure Portal.</span></span> <span data-ttu-id="190b3-156">Кроме того, замените заполнитель строки подключения на строку подключения **DefaultListenSharedAccessSignature**, полученную на странице **Access Polices** (Политики доступа) Центра уведомлений при работе с предыдущим разделом.</span><span class="sxs-lookup"><span data-stu-id="190b3-156">Also replace the connection string placeholder with the **DefaultListenSharedAccessSignature** connection string that you obtained from the **Access Polices** page of your Notification Hub in a previous section.</span></span>
   > 
   > 
5. <span data-ttu-id="190b3-157">В верхней части обработчика событий **OnLaunched** в файле App.xaml.cs добавьте в новый метод **InitNotificationsAsync** следующий вызов:</span><span class="sxs-lookup"><span data-stu-id="190b3-157">At the top of the **OnLaunched** event handler in App.xaml.cs, add the following call to the new **InitNotificationsAsync** method:</span></span>
   
        InitNotificationsAsync();
   
    <span data-ttu-id="190b3-158">Это обеспечит регистрацию URI канала в центре уведомлений при каждом запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="190b3-158">This guarantees that the channel URI is registered in your notification hub each time the application is launched.</span></span>
6. <span data-ttu-id="190b3-159">Нажмите клавишу **F5**, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="190b3-159">Press the **F5** key to run the app.</span></span> <span data-ttu-id="190b3-160">Отображается всплывающее диалоговое окно с ключом регистрации.</span><span class="sxs-lookup"><span data-stu-id="190b3-160">A pop-up dialog that contains the registration key is displayed.</span></span>

<span data-ttu-id="190b3-161">Теперь приложение готово к получению всплывающих уведомлений.</span><span class="sxs-lookup"><span data-stu-id="190b3-161">Your app is now ready to receive toast notifications.</span></span>

## <a name="send-notifications"></a><span data-ttu-id="190b3-162">Отправка уведомлений</span><span class="sxs-lookup"><span data-stu-id="190b3-162">Send notifications</span></span>
<span data-ttu-id="190b3-163">Вы можете быстро проверить получение уведомлений в приложении. Для этого отправьте уведомление на [портале Azure](https://portal.azure.com/), нажав кнопку **Тестовая отправка** в центре уведомлений, как показано на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="190b3-163">You can quickly test receiving notifications in your app by sending notifications in the [Azure Portal](https://portal.azure.com/) using the **Test Send** button on the notification hub, as shown in the screen below.</span></span>

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

<span data-ttu-id="190b3-164">Push-уведомления обычно отправляются в серверной службе, например мобильными службами или ASP.NET, с помощью совместимой библиотеки.</span><span class="sxs-lookup"><span data-stu-id="190b3-164">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="190b3-165">Также можно напрямую использовать REST API для отправки уведомлений, если для серверной части библиотека недоступна.</span><span class="sxs-lookup"><span data-stu-id="190b3-165">You can also use the REST API directly to send notification messages if a library is not available for your back-end.</span></span> 

<span data-ttu-id="190b3-166">В этом учебнике мы пойдем по простому пути и продемонстрируем тестирование клиентского приложения, отправляя уведомления с помощью пакета SDK для .NET для центров уведомлений не в серверную службу, а в консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="190b3-166">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using the .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="190b3-167">В качестве следующего шага по отправке уведомлений с сервера ASP.NET рекомендуем ознакомиться с руководством [Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET] .</span><span class="sxs-lookup"><span data-stu-id="190b3-167">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="190b3-168">Можно использовать следующие способы отправки уведомлений.</span><span class="sxs-lookup"><span data-stu-id="190b3-168">However, the following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="190b3-169">**Интерфейс REST**. [Интерфейс REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx) поддерживает уведомления на любой серверной платформе.</span><span class="sxs-lookup"><span data-stu-id="190b3-169">**REST Interface**:  You can support notification on any backend platform using  the [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="190b3-170">**Пакет SDK .NET для Центров уведомлений Microsoft Azure**. В диспетчере пакетов NuGet для Visual Studio выполните команду [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="190b3-170">**Microsoft Azure Notification Hubs .NET SDK**: In the Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="190b3-171">**Node.js**. [Использование центров уведомлений из Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="190b3-171">**Node.js** : [How to use Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="190b3-172">**Мобильные приложения Azure**. Пример отправки уведомлений из мобильного приложения Azure, интегрированного с Центрами уведомлений, см. в статье [Добавление push-уведомлений в приложение Windows](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="190b3-172">**Azure Mobile Apps**: For an example of how to send notifications from an Azure Mobile App that's integrated with Notification Hubs, see [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="190b3-173">**Java или PHP**. Примеры отправки уведомлений с использованием REST API см. в статьях "Использование концентраторов уведомлений из Java и "Использование концентраторов уведомлений из PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="190b3-173">**Java / PHP**: For an example of how to send notifications by using the REST APIs, see "How to use Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-console-app"></a><span data-ttu-id="190b3-174">(Необязательно) Отправке уведомлений из консольного приложения в C#</span><span class="sxs-lookup"><span data-stu-id="190b3-174">(Optional) Send notifications from a console app</span></span>
<span data-ttu-id="190b3-175">Для отправки уведомлений с помощью консольного приложения .NET выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="190b3-175">To send notifications by using a .NET console application follow these steps.</span></span> 

1. <span data-ttu-id="190b3-176">Щелкните решение правой кнопкой мыши, выберите пункты **Добавить** и **Создать проект...**. После этого в разделе **Visual C#** выберите **Windows** и **Консольное приложение**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="190b3-176">Right-click the solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
    <span data-ttu-id="190b3-177">При этом в решение добавляется новое консольное приложение Visual C#.</span><span class="sxs-lookup"><span data-stu-id="190b3-177">This adds a new Visual C# console application to the solution.</span></span> <span data-ttu-id="190b3-178">Это можно сделать также и в отдельном решении.</span><span class="sxs-lookup"><span data-stu-id="190b3-178">You can also do this in a separate solution.</span></span>

2. <span data-ttu-id="190b3-179">В Visual Studio последовательно выберите элементы **Сервис**, **Диспетчер пакетов NuGet** и **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="190b3-179">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="190b3-180">В результате в Visual Studio откроется консоль диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="190b3-180">This displays the Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="190b3-181">В окне консоли диспетчера пакетов задайте свойство **Проект по умолчанию** для нового проекта консольного приложения, а затем в окне консоли выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="190b3-181">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="190b3-182">После этого будет добавлена ссылка на пакет SDK для Центров уведомлений Azure с помощью <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">пакета NuGet Microsoft.Azure.Notification Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="190b3-182">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="190b3-183">Откройте файл Program.cs и добавьте следующий оператор `using` :</span><span class="sxs-lookup"><span data-stu-id="190b3-183">Open the Program.cs file and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="190b3-184">Добавьте в класс **Program** следующий метод:</span><span class="sxs-lookup"><span data-stu-id="190b3-184">In the **Program** class, add the following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure to replace the "hub name" placeholder with the name of the notification hub that as it appears in the Azure Portal. Also, replace the connection string placeholder with the **DefaultFullSharedAccessSignature** connection string that you obtained from the **Access Policies** page of your Notification Hub in the section called "Configure your notification hub."
   
   > [!NOTE]
   > <span data-ttu-id="190b3-185">Обязательно используйте строку подключения с **полным** доступом, а не c доступом к **прослушиванию**.</span><span class="sxs-lookup"><span data-stu-id="190b3-185">Make sure that you use the connection string that has **Full** access, not **Listen** access.</span></span> <span data-ttu-id="190b3-186">У строки с доступом к прослушиванию отсутствуют разрешения для отправки уведомлений.</span><span class="sxs-lookup"><span data-stu-id="190b3-186">The listen-access string does not have permissions to send notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="190b3-187">Добавьте следующие строки в метод **Main** :</span><span class="sxs-lookup"><span data-stu-id="190b3-187">Add the following lines in the **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="190b3-188">В Visual Studio щелкните проект консольного приложения правой кнопкой мыши и выберите пункт **Назначить запускаемым проектом** .</span><span class="sxs-lookup"><span data-stu-id="190b3-188">Right-click the console application project in Visual Studio, and click **Set as StartUp Project** to set it as the startup project.</span></span> <span data-ttu-id="190b3-189">Нажмите клавишу **F5**, чтобы запустить консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="190b3-189">Then press the **F5** key to run the application.</span></span>
   
    <span data-ttu-id="190b3-190">На всех зарегистрированных устройствах будет получено всплывающее уведомление.</span><span class="sxs-lookup"><span data-stu-id="190b3-190">You will receive a toast notification on all registered devices.</span></span> <span data-ttu-id="190b3-191">Если щелкнуть заголовок уведомления или коснуться его, приложение будет загружено.</span><span class="sxs-lookup"><span data-stu-id="190b3-191">Clicking or tapping the toast banner loads the app.</span></span>

<span data-ttu-id="190b3-192">В таких разделах MSDN, как [каталог всплывающих уведомлений], [каталог плиток] и [обзор индикаторов событий], можно найти всю полезную информацию по данной теме.</span><span class="sxs-lookup"><span data-stu-id="190b3-192">You can find all the supported payloads in the [toast catalog], [tile catalog], and [badge overview] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="190b3-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="190b3-193">Next steps</span></span>
<span data-ttu-id="190b3-194">В этом простом примере осуществляется рассылка уведомлений на все устройства Windows через портал или консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="190b3-194">In this simple example, you sent broadcast notifications to all your Windows devices using the portal or a console app.</span></span> <span data-ttu-id="190b3-195">На следующем этапе мы рекомендуем ознакомиться с руководством [Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET] .</span><span class="sxs-lookup"><span data-stu-id="190b3-195">We recommend the [Use Notification Hubs to push notifications to users] tutorial as the next step.</span></span> <span data-ttu-id="190b3-196">В нем описана процедура отправки уведомлений с сервера ASP.NET определенным пользователям с использованием тегов.</span><span class="sxs-lookup"><span data-stu-id="190b3-196">It will show you how to send notifications from an ASP.NET backend using tags to target specific users.</span></span>

<span data-ttu-id="190b3-197">Если необходимо разделить пользователей по группам интересов, см. раздел [Использование концентраторов уведомлений для передачи экстренных новостей].</span><span class="sxs-lookup"><span data-stu-id="190b3-197">If you want to segment your users by interest groups, see [Use Notification Hubs to send breaking news].</span></span> 

<span data-ttu-id="190b3-198">Дополнительные сведения о Центрах уведомлений см. в статье [Notification Hubs Guidance](notification-hubs-push-notification-overview.md) (Общие сведения о Центрах уведомлений).</span><span class="sxs-lookup"><span data-stu-id="190b3-198">To learn more general information about Notification Hubs, see [Notification Hubs Guidance](notification-hubs-push-notification-overview.md).</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

<span data-ttu-id="190b3-199">[Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="190b3-199">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
<span data-ttu-id="190b3-200">[Использование концентраторов уведомлений для передачи экстренных новостей]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="190b3-200">[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>

<span data-ttu-id="190b3-201">[каталог всплывающих уведомлений]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx</span><span class="sxs-lookup"><span data-stu-id="190b3-201">[toast catalog]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx</span></span>
<span data-ttu-id="190b3-202">[каталог плиток]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx</span><span class="sxs-lookup"><span data-stu-id="190b3-202">[tile catalog]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx</span></span>
<span data-ttu-id="190b3-203">[обзор индикаторов событий]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx</span><span class="sxs-lookup"><span data-stu-id="190b3-203">[badge overview]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx</span></span>
