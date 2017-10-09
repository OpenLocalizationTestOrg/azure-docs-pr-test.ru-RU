---
title: "aaaGet работы с Azure уведомления концентраторов для универсальной платформы приложений для Windows | Документы Microsoft"
description: "В этом учебнике вы узнаете, как toouse концентраторов уведомлений Azure toopush уведомления tooa приложения универсальной платформы Windows."
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
ms.openlocfilehash: 11056842d205522ed493dc61c76ecf78ebb5a363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a><span data-ttu-id="2cdf5-103">Начало работы с Центрами уведомлений для приложений универсальной платформы Windows</span><span class="sxs-lookup"><span data-stu-id="2cdf5-103">Getting started with Notification Hubs for Windows Universal Platform Apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="2cdf5-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="2cdf5-104">Overview</span></span>
<span data-ttu-id="2cdf5-105">Этот учебник показывает, как toosend toouse концентраторов уведомлений Azure push-уведомления tooa универсальной платформы Windows (UWP) приложения.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Universal Windows Platform (UWP) app.</span></span>

<span data-ttu-id="2cdf5-106">В этом учебнике создается пустое приложение магазина Windows, получающий push-уведомления с помощью hello Windows Push Notification Service (WNS).</span><span class="sxs-lookup"><span data-stu-id="2cdf5-106">In this tutorial, you create a blank Windows Store app that receives push notifications by using hello Windows Push Notification Service (WNS).</span></span> <span data-ttu-id="2cdf5-107">После завершения вы будете иметь доступ toouse вашей toobroadcast концентратора уведомлений push-уведомления tooall hello устройств под управлением приложения.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-107">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2cdf5-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="2cdf5-108">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="2cdf5-109">код завершения Hello в этом учебнике можно найти на GitHub [здесь](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span><span class="sxs-lookup"><span data-stu-id="2cdf5-109">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2cdf5-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2cdf5-110">Prerequisites</span></span>
<span data-ttu-id="2cdf5-111">Этот учебник требует hello следующее:</span><span class="sxs-lookup"><span data-stu-id="2cdf5-111">This tutorial requires hello following:</span></span>

* <span data-ttu-id="2cdf5-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) или более поздняя версия.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) or later</span></span>
* [<span data-ttu-id="2cdf5-113">Установленные средства разработки универсальных приложений Windows</span><span class="sxs-lookup"><span data-stu-id="2cdf5-113">Universal Windows App Development Tools installed</span></span>](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* <span data-ttu-id="2cdf5-114">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-114">An active Azure account</span></span> <br/><span data-ttu-id="2cdf5-115">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2cdf5-116">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="2cdf5-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span></span>
* <span data-ttu-id="2cdf5-117">Активная учетная запись Магазина Windows.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-117">An active Windows Store account</span></span>

<span data-ttu-id="2cdf5-118">Завершение изучения этого руководства является необходимым условием для работы со всеми другими руководствами, посвященными Центрам уведомлений для приложений универсальной платформы Windows.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Universal Platform apps.</span></span>

## <a name="register-your-app-for-hello-windows-store"></a><span data-ttu-id="2cdf5-119">Регистрация приложения для магазина Windows hello</span><span class="sxs-lookup"><span data-stu-id="2cdf5-119">Register your app for hello Windows Store</span></span>
<span data-ttu-id="2cdf5-120">toosend принудительной уведомления tooUWP приложений, необходимо связать toohello вашего приложения магазина Windows.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-120">toosend push notifications tooUWP apps, you must associate your app toohello Windows Store.</span></span> <span data-ttu-id="2cdf5-121">Затем необходимо настроить на toointegrate концентратора уведомлений с WNS.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-121">You must then configure your notification hub toointegrate with WNS.</span></span>

1. <span data-ttu-id="2cdf5-122">Если приложение еще не зарегистрирован, перейдите в папку toohello [центра разработчиков Windows](https://dev.windows.com/overview), войти в учетную запись Майкрософт и нажмите кнопку **создайте новое приложение**.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-122">If you have not already registered your app, navigate toohello [Windows Dev Center](https://dev.windows.com/overview), sign in with your Microsoft account, and then click **Create a new app**.</span></span>

2. <span data-ttu-id="2cdf5-123">Введите имя приложения и нажмите кнопку **Зарезервировать имя приложения**.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-123">Type a name for your app and click **Reserve app name**.</span></span> <span data-ttu-id="2cdf5-124">При этом создается новая регистрация в Магазине Windows для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-124">This creates a new Windows Store registration for your app.</span></span>

3. <span data-ttu-id="2cdf5-125">В Visual Studio, создайте новый проект Visual C# магазина с помощью универсальных Windows hello **пустое приложение** шаблона и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-125">In Visual Studio, create a new Visual C# Store Apps project by using hello Windows Universal **Blank App** template and click **OK**.</span></span>

4. <span data-ttu-id="2cdf5-126">Примите значения по умолчанию hello для hello целевую и минимальную версии платформы.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-126">Accept hello defaults for hello target and minimum platform versions.</span></span>

5. <span data-ttu-id="2cdf5-127">В обозревателе решений щелкните правой кнопкой мыши проект приложения для магазина Windows hello, нажмите кнопку **хранилища**, а затем нажмите кнопку **связать приложение с hello хранилища...** . hello **связывать приложения с магазина Windows hello** откроется окно мастера.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-127">In Solution Explorer, right-click hello Windows Store app project, click **Store**, and then click **Associate App with hello Store...**. hello **Associate Your App with hello Windows Store** wizard appears.</span></span>

6. <span data-ttu-id="2cdf5-128">В мастере hello войти в учетную запись Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-128">In hello wizard, sign in with your Microsoft account.</span></span>

7. <span data-ttu-id="2cdf5-129">Выберите приложение hello, зарегистрированный на шаге 2, щелкните **Далее**, а затем нажмите кнопку **связать**.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-129">Click hello app that you registered in step 2, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="2cdf5-130">Это добавляет манифест приложения toohello сведения о регистрации требуется hello магазина Windows.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-130">This adds hello required Windows Store registration information toohello application manifest.</span></span>

8. <span data-ttu-id="2cdf5-131">Включите hello [центра разработчиков Windows](http://dev.windows.com/overview) для нового приложения и щелкните **службы**, нажмите кнопку **Push-уведомления**и нажмите кнопку **WNS или MPNS**.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-131">Back on hello [Windows Dev Center](http://dev.windows.com/overview) page for your new app, click **Services**, click **Push notifications**, and then click **WNS/MPNS**.</span></span>

9. <span data-ttu-id="2cdf5-132">Щелкните **Новое уведомление**.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-132">Click **New Notification**.</span></span>

10. <span data-ttu-id="2cdf5-133">Щелкните шаблон **Blank (Toast)** (Пустое (всплывающее)) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-133">Click **Blank (Toast)** template and then click **OK**.</span></span>

11. <span data-ttu-id="2cdf5-134">Введите **имя** уведомления и **контекстное** сообщение Visual.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-134">Enter a notification **Name** and Visual **Context** message.</span></span> <span data-ttu-id="2cdf5-135">Затем щелкните **Save as draft** (Сохранить как черновик).</span><span class="sxs-lookup"><span data-stu-id="2cdf5-135">Then click **Save as draft**.</span></span>

12. <span data-ttu-id="2cdf5-136">Перейдите toohello [портала регистрации приложения](http://apps.dev.microsoft.com) и войдите в систему.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-136">Navigate toohello [Application Registration Portal](http://apps.dev.microsoft.com) and log in.</span></span>

13. <span data-ttu-id="2cdf5-137">Щелкните имя приложения.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-137">Click on your application name.</span></span> <span data-ttu-id="2cdf5-138">Запишите hello **секрет приложения** пароль и hello **пакета идентификатор безопасности (SID)** в hello **магазина Windows** параметры платформы.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-138">Make a note of hello **Application Secret** password and hello **Package security identifier (SID)** located in hello **Windows Store** platform settings.</span></span>

     > [AZURE.WARNING]
    <span data-ttu-id="2cdf5-139">секрет приложения Hello и ИД безопасности пакета являются важными элементами обеспечения безопасности.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-139">hello application secret and package SID are important security credentials.</span></span> <span data-ttu-id="2cdf5-140">Не сообщайте никому эти значения и не распространяйте их вместе со своим приложением.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-140">Do not share these values with anyone or distribute them with your app.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="2cdf5-141">Настройка концентратора уведомлений</span><span class="sxs-lookup"><span data-stu-id="2cdf5-141">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="2cdf5-142">Выберите hello <b>служб Notification Services</b> параметр и hello <b>Windows (WNS)</b> параметр.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-142">Select hello <b>Notification Services</b> option and hello <b>Windows (WNS)</b> option.</span></span> <span data-ttu-id="2cdf5-143">Затем введите hello <b>секрет приложения</b> пароль в hello <b>ключ безопасности</b> поля.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-143">Then enter hello <b>Application secret</b> password in hello <b>Security Key</b> field.</span></span> <span data-ttu-id="2cdf5-144">Введите ваш <b>ИД безопасности пакета</b> значения, полученные из WNS в предыдущем разделе hello и нажмите кнопку <b>Сохранить</b>.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-144">Enter your <b>Package SID</b> value that you obtained from WNS in hello previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

<span data-ttu-id="2cdf5-145">Концентратор уведомлений будет настроенных toowork с WNS, и иметь tooregister строки подключения hello приложения и отправку уведомлений.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-145">Your notification hub is now configured toowork with WNS, and you have hello connection strings tooregister your app and send notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="2cdf5-146">Подключение приложения toohello концентратор уведомлений</span><span class="sxs-lookup"><span data-stu-id="2cdf5-146">Connect your app toohello notification hub</span></span>
1. <span data-ttu-id="2cdf5-147">В Visual Studio, щелкните правой кнопкой мыши решение hello и нажмите кнопку **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-147">In Visual Studio, right-click hello solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="2cdf5-148">При этом отображаются hello **управление пакетами NuGet** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-148">This displays hello **Manage NuGet Packages** dialog box.</span></span>
2. <span data-ttu-id="2cdf5-149">Поиск `WindowsAzure.Messaging.Managed` и нажмите кнопку **установить**и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-149">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and accept hello terms of use.</span></span>
   
    ![][20]
   
    <span data-ttu-id="2cdf5-150">Это загружает устанавливает и добавляет библиотеку обмена сообщениями Azure toohello ссылки для Windows с помощью hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">пакет WindowsAzure.Messaging.Managed NuGet</a>.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-150">This downloads, installs, and adds a reference toohello Azure Messaging library for Windows by using hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
3. <span data-ttu-id="2cdf5-151">Откройте файл проекта App.xaml.cs hello и добавьте следующее hello `using` инструкции.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-151">Open hello App.xaml.cs project file and add hello following `using` statements.</span></span> 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. <span data-ttu-id="2cdf5-152">Также в App.xaml.cs, добавьте следующее hello **InitNotificationsAsync** toohello определение метода **приложения** класса:</span><span class="sxs-lookup"><span data-stu-id="2cdf5-152">Also in App.xaml.cs, add hello following **InitNotificationsAsync** method definition toohello **App** class:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    <span data-ttu-id="2cdf5-153">Этот код извлекает из WNS hello URI канала для приложения hello и затем регистрирует URI канала в концентраторе уведомлений.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-153">This code retrieves hello channel URI for hello app from WNS, and then registers that channel URI with your notification hub.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2cdf5-154">Убедитесь, что tooreplace hello заполнитель «имя концентратора» hello имя концентратора уведомлений hello в hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-154">Make sure tooreplace hello "your hub name" placeholder with hello name of hello notification hub that appears in hello Azure Portal.</span></span> <span data-ttu-id="2cdf5-155">Также замените заполнитель строки подключения hello hello **DefaultListenSharedAccessSignature** строку подключения, который получен из hello **политики доступа** страницы центра уведомлений в предыдущего раздела.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-155">Also replace hello connection string placeholder with hello **DefaultListenSharedAccessSignature** connection string that you obtained from hello **Access Polices** page of your Notification Hub in a previous section.</span></span>
   > 
   > 
5. <span data-ttu-id="2cdf5-156">Вверху hello hello **OnLaunched** обработчик событий в App.xaml.cs, добавьте после вызова toohello новый hello **InitNotificationsAsync** метод:</span><span class="sxs-lookup"><span data-stu-id="2cdf5-156">At hello top of hello **OnLaunched** event handler in App.xaml.cs, add hello following call toohello new **InitNotificationsAsync** method:</span></span>
   
        InitNotificationsAsync();
   
    <span data-ttu-id="2cdf5-157">Это гарантирует зарегистрировано на концентраторе уведомлений, запускаемого каждое приложение hello времени URI канала hello.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-157">This guarantees that hello channel URI is registered in your notification hub each time hello application is launched.</span></span>
6. <span data-ttu-id="2cdf5-158">Нажмите клавишу hello **F5** приложение hello toorun ключа.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-158">Press hello **F5** key toorun hello app.</span></span> <span data-ttu-id="2cdf5-159">Отображается всплывающее диалоговое окно, содержащее ключ регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-159">A pop-up dialog that contains hello registration key is displayed.</span></span>

<span data-ttu-id="2cdf5-160">Приложение больше не готов tooreceive всплывающие уведомления.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-160">Your app is now ready tooreceive toast notifications.</span></span>

## <a name="send-notifications"></a><span data-ttu-id="2cdf5-161">Отправка уведомлений</span><span class="sxs-lookup"><span data-stu-id="2cdf5-161">Send notifications</span></span>
<span data-ttu-id="2cdf5-162">Можно быстро проверить получение уведомлений в приложение путем отправки уведомления в hello [портала Azure](https://portal.azure.com/) с помощью hello **Тестовая отправка** кнопку на концентраторе уведомлений hello, как показано ниже экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-162">You can quickly test receiving notifications in your app by sending notifications in hello [Azure Portal](https://portal.azure.com/) using hello **Test Send** button on hello notification hub, as shown in hello screen below.</span></span>

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

<span data-ttu-id="2cdf5-163">Push-уведомления обычно отправляются в серверной службе, например мобильными службами или ASP.NET, с помощью совместимой библиотеки.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-163">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="2cdf5-164">Также можно использовать hello REST API напрямую toosend уведомления сообщений, если библиотека недоступна для серверной части.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-164">You can also use hello REST API directly toosend notification messages if a library is not available for your back-end.</span></span> 

<span data-ttu-id="2cdf5-165">В этом учебнике мы должен быть простым и просто демонстрации тестирование приложения клиента путем отправки уведомлений с использованием hello .NET SDK для концентраторов уведомлений в консольном приложении, а не серверной службы.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-165">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="2cdf5-166">Мы рекомендуем hello [toousers уведомления toopush использования концентраторов уведомлений] учебника hello на следующем шаге для отправки уведомлений из серверной части ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-166">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="2cdf5-167">Тем не менее можно использовать следующие подходы hello для отправки уведомлений:</span><span class="sxs-lookup"><span data-stu-id="2cdf5-167">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="2cdf5-168">**Интерфейс REST**: может поддерживать уведомления на любой платформе серверной части, с помощью hello [интерфейс REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="2cdf5-168">**REST Interface**:  You can support notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="2cdf5-169">**Пакета SDK .NET концентраторы уведомлений Microsoft Azure**: В hello диспетчера пакетов Nuget для Visual Studio, запустите [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="2cdf5-169">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="2cdf5-170">**Node.js** : [как концентраторы уведомлений из Node.js toouse](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="2cdf5-170">**Node.js** : [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="2cdf5-171">**Мобильные приложения Azure**: пример того, как toosend уведомления от мобильного приложения Azure, интегрируется с концентраторами уведомлений в разделе [Добавление push-уведомлений для мобильных приложений](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="2cdf5-171">**Azure Mobile Apps**: For an example of how toosend notifications from an Azure Mobile App that's integrated with Notification Hubs, see [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="2cdf5-172">**Java / PHP**: пример как toosend уведомления с помощью hello API-интерфейс REST, в разделе «как toouse концентраторы уведомлений из Java и PHP» ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="2cdf5-172">**Java / PHP**: For an example of how toosend notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-console-app"></a><span data-ttu-id="2cdf5-173">(Необязательно) Отправке уведомлений из консольного приложения в C#</span><span class="sxs-lookup"><span data-stu-id="2cdf5-173">(Optional) Send notifications from a console app</span></span>
<span data-ttu-id="2cdf5-174">toosend уведомления с помощью консольного приложения .NET выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-174">toosend notifications by using a .NET console application follow these steps.</span></span> 

1. <span data-ttu-id="2cdf5-175">Щелкните правой кнопкой мыши решение hello, выберите **добавить** и **новый проект...** , а затем в разделе **Visual C#**, нажмите кнопку **Windows** и **консольное приложение**и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-175">Right-click hello solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
    <span data-ttu-id="2cdf5-176">Используется для добавления нового Visual C# консольного приложения toohello решения.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-176">This adds a new Visual C# console application toohello solution.</span></span> <span data-ttu-id="2cdf5-177">Это можно сделать также и в отдельном решении.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-177">You can also do this in a separate solution.</span></span>

2. <span data-ttu-id="2cdf5-178">В Visual Studio последовательно выберите элементы **Сервис**, **Диспетчер пакетов NuGet** и **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-178">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="2cdf5-179">Откроется консоль диспетчера пакетов hello в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-179">This displays hello Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="2cdf5-180">В hello в окне консоли диспетчера пакетов, задайте hello **проекта по умолчанию** tooyour нового консольного приложения проекта, а затем в окне консоли hello, выполните hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2cdf5-180">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="2cdf5-181">При этом добавляется ссылка toohello концентраторов уведомлений Azure SDK с помощью hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">пакет NuGet концентраторов Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-181">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="2cdf5-182">Откройте файл Program.cs hello и добавьте следующее hello `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="2cdf5-182">Open hello Program.cs file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="2cdf5-183">В hello **программы** добавьте следующий метод hello:</span><span class="sxs-lookup"><span data-stu-id="2cdf5-183">In hello **Program** class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure tooreplace hello "hub name" placeholder with hello name of hello notification hub that as it appears in hello Azure Portal. Also, replace hello connection string placeholder with hello **DefaultFullSharedAccessSignature** connection string that you obtained from hello **Access Policies** page of your Notification Hub in hello section called "Configure your notification hub."
   
   > [!NOTE]
   > <span data-ttu-id="2cdf5-184">Убедитесь, что используются hello строки подключения, которая содержит **полного** доступ, не **прослушивания** доступа.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-184">Make sure that you use hello connection string that has **Full** access, not **Listen** access.</span></span> <span data-ttu-id="2cdf5-185">Строка Hello прослушивания доступа не имеет разрешения toosend уведомления.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-185">hello listen-access string does not have permissions toosend notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="2cdf5-186">Добавьте следующие строки в hello hello **Main** метод:</span><span class="sxs-lookup"><span data-stu-id="2cdf5-186">Add hello following lines in hello **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="2cdf5-187">Щелкните правой кнопкой мыши проект консольного приложения hello в Visual Studio, а затем нажмите кнопку **Назначить запускаемым проектом** tooset его hello запускаемым проектом.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-187">Right-click hello console application project in Visual Studio, and click **Set as StartUp Project** tooset it as hello startup project.</span></span> <span data-ttu-id="2cdf5-188">Нажмите клавишу hello **F5** ключа toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-188">Then press hello **F5** key toorun hello application.</span></span>
   
    <span data-ttu-id="2cdf5-189">На всех зарегистрированных устройствах будет получено всплывающее уведомление.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-189">You will receive a toast notification on all registered devices.</span></span> <span data-ttu-id="2cdf5-190">Нажав кнопку баннер всплывающих hello загружает приложение hello.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-190">Clicking or tapping hello toast banner loads hello app.</span></span>

<span data-ttu-id="2cdf5-191">Можно найти все полезные данные hello поддерживается hello [каталога всплывающих], [плитки каталога], и [значок Обзор] разделах в библиотеке MSDN.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-191">You can find all hello supported payloads in hello [toast catalog], [tile catalog], and [badge overview] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2cdf5-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2cdf5-192">Next steps</span></span>
<span data-ttu-id="2cdf5-193">В этом простом примере вы отправили tooall широковещательной рассылки уведомлений устройства Windows с помощью портала hello или консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-193">In this simple example, you sent broadcast notifications tooall your Windows devices using hello portal or a console app.</span></span> <span data-ttu-id="2cdf5-194">Мы рекомендуем hello [toousers уведомления toopush использования концентраторов уведомлений] учебника в качестве следующего шага hello.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-194">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="2cdf5-195">Также будет показано, как уведомления о toosend из серверной части ASP.NET с помощью тегов tootarget конкретных пользователей.</span><span class="sxs-lookup"><span data-stu-id="2cdf5-195">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="2cdf5-196">Если toosegment пользователям по группы интересов, см. [toosend использования концентраторов уведомлений, новости].</span><span class="sxs-lookup"><span data-stu-id="2cdf5-196">If you want toosegment your users by interest groups, see [Use Notification Hubs toosend breaking news].</span></span> 

<span data-ttu-id="2cdf5-197">toolearn. в разделе Общие сведения о концентраторах уведомлений [руководство концентраторы уведомлений](notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2cdf5-197">toolearn more general information about Notification Hubs, see [Notification Hubs Guidance](notification-hubs-push-notification-overview.md).</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

[toousers уведомления toopush использования концентраторов уведомлений]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend использования концентраторов уведомлений, новости]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

[каталога всплывающих]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx
[плитки каталога]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx
[значок Обзор]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx
