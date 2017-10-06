---
title: "aaaAzure пользователям уведомления концентраторов уведомлений с помощью серверного приложения .NET"
description: "Узнайте, как безопасные toosend push-уведомления в Azure. Примеры кода на языке C# с использованием hello .NET API."
documentationcenter: windows
author: ysxu
manager: erikre
services: notification-hubs
editor: 
ms.assetid: 012529f2-fdbc-43c4-8634-2698164b5880
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: a366181faa81e78adf4de61435ef2790c3aa29d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a><span data-ttu-id="854d4-104">Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET</span><span class="sxs-lookup"><span data-stu-id="854d4-104">Azure Notification Hubs Notify Users with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="854d4-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="854d4-105">Overview</span></span>
<span data-ttu-id="854d4-106">Поддержка уведомлений Push в Azure позволяет tooaccess к использованию, многоплатформенных и масштабируемых push-инфраструктуру, которая значительно упрощает реализацию hello push-уведомлений для индивидуальных пользователей и корпоративных приложений для мобильных устройств платформы.</span><span class="sxs-lookup"><span data-stu-id="854d4-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="854d4-107">Этот учебник показывает, как toosend toouse концентраторов уведомлений Azure push-уведомления tooa определенное приложение пользователя на конкретном устройстве.</span><span class="sxs-lookup"><span data-stu-id="854d4-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="854d4-108">Внутренний ASP.NET WebAPI — используется tooauthenticate клиентов.</span><span class="sxs-lookup"><span data-stu-id="854d4-108">An ASP.NET WebAPI backend is used tooauthenticate clients.</span></span> <span data-ttu-id="854d4-109">Привет, прошедшие проверку подлинности пользователя клиента и тег, будут автоматически добавляться регистрацией toonotification hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="854d4-109">Using hello authenticated client user, and tag will be automatically added by hello backend toonotification registration.</span></span> <span data-ttu-id="854d4-110">Этот тег будет используется toosend уведомлениями toogenerate hello серверной части для конкретного пользователя.</span><span class="sxs-lookup"><span data-stu-id="854d4-110">This tag will be used toosend by hello backend toogenerate notifications for a specific user.</span></span> <span data-ttu-id="854d4-111">Дополнительные сведения о регистрации для уведомлений с использованием внутреннего сервера приложения см. в разделе hello руководство [регистрации из серверной части приложения](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="854d4-111">For more information on registering for notifications using an app backend, see hello guidance topic [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="854d4-112">Этот учебник построен на концентраторе уведомлений hello и проект, созданный в hello [приступить к работе с концентраторами уведомлений] учебника.</span><span class="sxs-lookup"><span data-stu-id="854d4-112">This tutorial builds on hello notification hub and project that you created in hello [Get started with Notification Hubs] tutorial.</span></span>

<span data-ttu-id="854d4-113">Этот учебник содержит также hello готовности toohello [принудительной защиты] учебника.</span><span class="sxs-lookup"><span data-stu-id="854d4-113">This tutorial is also hello prerequisite toohello [Secure Push] tutorial.</span></span> <span data-ttu-id="854d4-114">После завершения шагов hello в этом учебнике, вы можете перейти toohello [принудительной защиты] руководство, в котором показано, как toomodify hello код в этот учебник toosend push-уведомление безопасно.</span><span class="sxs-lookup"><span data-stu-id="854d4-114">After you have completed hello steps in this tutorial, you can proceed toohello [Secure Push] tutorial, which shows how toomodify hello code in this tutorial toosend a push notification securely.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="854d4-115">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="854d4-115">Before you begin</span></span>
<span data-ttu-id="854d4-116">Мы очень ценим ваши отзывы.</span><span class="sxs-lookup"><span data-stu-id="854d4-116">We do take your feedback seriously.</span></span> <span data-ttu-id="854d4-117">Если возникли проблемы, завершение работы этого раздела или рекомендации по улучшению это содержимое, мы ценим ваши отзывы hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="854d4-117">If you have any difficulties completing this topic, or recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span>

<span data-ttu-id="854d4-118">код завершения Hello в этом учебнике можно найти на GitHub [здесь](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="854d4-118">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="854d4-119">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="854d4-119">Prerequisites</span></span>
<span data-ttu-id="854d4-120">Перед началом работы с этим учебником необходимо изучить следующие учебники по мобильным службам.</span><span class="sxs-lookup"><span data-stu-id="854d4-120">Before you start this tutorial, you must have already completed these Mobile Services tutorials:</span></span>

* <span data-ttu-id="854d4-121">[приступить к работе с концентраторами уведомлений]</span><span class="sxs-lookup"><span data-stu-id="854d4-121">[Get started with Notification Hubs]</span></span><br/><span data-ttu-id="854d4-122">Создать концентратор уведомлений и зарезервировать имя приложения hello и зарегистрировать tooreceive уведомления в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="854d4-122">You create your notification hub and reserve hello app name and register tooreceive notifications in this tutorial.</span></span> <span data-ttu-id="854d4-123">В этом учебнике предполагается, что следующие действия уже были предприняты.</span><span class="sxs-lookup"><span data-stu-id="854d4-123">This tutorial assumes you have already completed these steps.</span></span> <span data-ttu-id="854d4-124">В противном случае следуйте инструкциям hello [Приступая к работе с концентраторами уведомлений (магазин Windows)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); в частности, hello разделы [регистрации приложения для магазина Windows hello](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) и [Настройка Концентратор уведомлений](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="854d4-124">If not, please follow hello steps in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); specifically, hello sections [Register your app for hello Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) and [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="854d4-125">В частности, убедитесь в том, что вы ввели hello **ИД безопасности пакета** и **секрет клиента** значения в hello hello портале **Настройка** вкладке концентратор уведомлений.</span><span class="sxs-lookup"><span data-stu-id="854d4-125">In particular, make sure that you have entered hello **Package SID** and **Client Secret** values in hello portal, in hello **Configure** tab for your notification hub.</span></span> <span data-ttu-id="854d4-126">Эта конфигурация процедура описана в разделе hello [настройки центра уведомлений](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="854d4-126">This configuration procedure is described in hello section [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="854d4-127">Это важный шаг: Если hello учетные данные на портале hello не соответствуют указанной выбрать имя приложения hello, hello push-уведомление не будет выполнено.</span><span class="sxs-lookup"><span data-stu-id="854d4-127">This is an important step: if hello credentials on hello portal do not match those specified for hello app name you choose, hello push notification will not succeed.</span></span>

> [!NOTE]
> <span data-ttu-id="854d4-128">При использовании мобильных приложений в службе приложений Azure как безопасности внутренней службы. в разделе hello [мобильные приложения версии](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) этого учебника.</span><span class="sxs-lookup"><span data-stu-id="854d4-128">If you are using Mobile Apps in Azure App Service as your backend service, see hello [Mobile Apps version](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) of this tutorial.</span></span>
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-hello-code-for-hello-client-project"></a><span data-ttu-id="854d4-129">Обновление кода hello для проекта клиента hello</span><span class="sxs-lookup"><span data-stu-id="854d4-129">Update hello code for hello client project</span></span>
<span data-ttu-id="854d4-130">В этом разделе, при обновлении кода hello в проекте hello, вы выполнили hello [приступить к работе с концентраторами уведомлений] учебника.</span><span class="sxs-lookup"><span data-stu-id="854d4-130">In this section, you update hello code in hello project you completed for hello [Get started with Notification Hubs] tutorial.</span></span> <span data-ttu-id="854d4-131">Hello следует уже связанную с хранилищем hello и настроен для центра уведомлений.</span><span class="sxs-lookup"><span data-stu-id="854d4-131">hello should already be associated with hello store and configured for your notification hub.</span></span> <span data-ttu-id="854d4-132">В этом разделе будет добавить новый внутренний WebAPI кода toocall hello и использовать его для регистрации и отправки уведомлений.</span><span class="sxs-lookup"><span data-stu-id="854d4-132">In this section, you will add code toocall hello new WebAPI backend and use it for registering and sending notifications.</span></span>

1. <span data-ttu-id="854d4-133">В Visual Studio откройте решение hello hello, созданный для hello [приступить к работе с концентраторами уведомлений] учебника.</span><span class="sxs-lookup"><span data-stu-id="854d4-133">In Visual Studio, open hello hello solution you created for hello [Get started with Notification Hubs] tutorial.</span></span>
2. <span data-ttu-id="854d4-134">В обозревателе решений щелкните правой кнопкой мыши hello **(Windows 8.1)** проект и выберите пункт **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="854d4-134">In Solution Explorer, right-click hello **(Windows 8.1)** project and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="854d4-135">В левой части окна hello, выберите **Online**.</span><span class="sxs-lookup"><span data-stu-id="854d4-135">On hello left-hand side, click **Online**.</span></span>
4. <span data-ttu-id="854d4-136">В hello **поиска** введите **HTTP-клиент**.</span><span class="sxs-lookup"><span data-stu-id="854d4-136">In hello **Search** box, type **Http Client**.</span></span>
5. <span data-ttu-id="854d4-137">В списке результатов hello, нажмите кнопку **клиентских библиотек HTTP Майкрософт**, а затем нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="854d4-137">In hello results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="854d4-138">Завершить установку hello.</span><span class="sxs-lookup"><span data-stu-id="854d4-138">Complete hello installation.</span></span>
6. <span data-ttu-id="854d4-139">Вернитесь в hello NuGet **поиска** введите **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="854d4-139">Back in hello NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="854d4-140">Установка hello **Json.NET** пакета и hello закройте окно диспетчера пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="854d4-140">Install hello **Json.NET** package, and then close hello NuGet Package Manager window.</span></span>
7. <span data-ttu-id="854d4-141">Повторите приведенные выше действия hello для hello **(Windows Phone 8.1)** hello проекта tooinstall **JSON.NET** пакет NuGet для проекта Windows Phone hello.</span><span class="sxs-lookup"><span data-stu-id="854d4-141">Repeat hello steps above for hello **(Windows Phone 8.1)** project tooinstall hello **JSON.NET** NuGet package for hello Windows Phone project.</span></span>
8. <span data-ttu-id="854d4-142">В обозревателе решений в hello **(Windows 8.1)** проекта, дважды щелкните **MainPage.xaml** tooopen его в редакторе Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="854d4-142">In Solution Explorer, in hello **(Windows 8.1)** project, double-click **MainPage.xaml** tooopen it in hello Visual Studio editor.</span></span>
9. <span data-ttu-id="854d4-143">В hello **MainPage.xaml** XML-код, замените hello `<Grid>` раздел с hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="854d4-143">In hello **MainPage.xaml** XML code, replace hello `<Grid>` section with hello following code.</span></span> <span data-ttu-id="854d4-144">Этот код добавляет текстовое поле имени пользователя и пароля, Здравствуйте, пользователь будет выполнять проверку подлинности с помощью.</span><span class="sxs-lookup"><span data-stu-id="854d4-144">This code adds a username and password textbox that hello user will authenticate with.</span></span> <span data-ttu-id="854d4-145">Он также добавляет текстовые поля для сообщения уведомления hello и тег hello имя пользователя, который должен получать уведомления hello.</span><span class="sxs-lookup"><span data-stu-id="854d4-145">It also adds textboxes for hello notification message and hello username tag that should receive hello notification:</span></span>
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*"/>
            </Grid.RowDefinitions>
   
            <TextBlock Grid.Row="0" Text="Notify Users" HorizontalAlignment="Center" FontSize="48"/>
   
            <StackPanel Grid.Row="1" VerticalAlignment="Center">
                <Grid>
                    <Grid.RowDefinitions>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                    </Grid.RowDefinitions>
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                    </Grid.ColumnDefinitions>
                    <TextBlock Grid.Row="0" Grid.ColumnSpan="3" Text="Username" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="UsernameTextBox" Grid.Row="1" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
                    <TextBlock Grid.Row="2" Grid.ColumnSpan="3" Text="Password" FontSize="24" Margin="20,0,20,0" />
                    <PasswordBox Name="PasswordTextBox" Grid.Row="3" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
   
                    <Button Grid.Row="4" Grid.ColumnSpan="3" HorizontalAlignment="Center" VerticalAlignment="Center"
                                Content="1. Login and register" Click="LoginAndRegisterClick" Margin="0,0,0,20"/>
   
                    <ToggleButton Name="toggleWNS" Grid.Row="5" Grid.Column="0" HorizontalAlignment="Right" Content="WNS" IsChecked="True" />
                    <ToggleButton Name="toggleGCM" Grid.Row="5" Grid.Column="1" HorizontalAlignment="Center" Content="GCM" />
                    <ToggleButton Name="toggleAPNS" Grid.Row="5" Grid.Column="2" HorizontalAlignment="Left" Content="APNS" />
   
                    <TextBlock Grid.Row="6" Grid.ColumnSpan="3" Text="Username Tag tooSend To" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="ToUserTagTextBox" Grid.Row="7" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <TextBlock Grid.Row="8" Grid.ColumnSpan="3" Text="Enter Notification Message" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="NotificationMessageTextBox" Grid.Row="9" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <Button Grid.Row="10" Grid.ColumnSpan="3" HorizontalAlignment="Center" Content="2. Send push" Click="PushClick" Name="SendPushButton" />
                </Grid>
            </StackPanel>
        </Grid>
10. <span data-ttu-id="854d4-146">В обозревателе решений в hello **(Windows Phone 8.1)** откройте проект **MainPage.xaml** и замените hello Windows Phone 8.1 `<Grid>` раздел с этой же приведенный выше код.</span><span class="sxs-lookup"><span data-stu-id="854d4-146">In Solution Explorer, in hello **(Windows Phone 8.1)** project, open **MainPage.xaml** and replace hello Windows Phone 8.1 `<Grid>` section with that same code above.</span></span> <span data-ttu-id="854d4-147">Hello интерфейс должен выглядеть примерно toowhats, показано ниже.</span><span class="sxs-lookup"><span data-stu-id="854d4-147">hello interface should look similar toowhats shown below.</span></span>
    
    ![][13]
11. <span data-ttu-id="854d4-148">В обозревателе решений откройте hello **MainPage.xaml.cs** файл для hello **(Windows 8.1)** и **(Windows Phone 8.1)** проектов.</span><span class="sxs-lookup"><span data-stu-id="854d4-148">In Solution Explorer, open hello **MainPage.xaml.cs** file for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span> <span data-ttu-id="854d4-149">Добавьте следующее hello `using` инструкции вверху hello оба файла:</span><span class="sxs-lookup"><span data-stu-id="854d4-149">Add hello following `using` statements at hello top of both files:</span></span>
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. <span data-ttu-id="854d4-150">В **MainPage.xaml.cs** для hello **(Windows 8.1)** и **(Windows Phone 8.1)** проектов, добавьте следующий член toohello hello `MainPage` класса.</span><span class="sxs-lookup"><span data-stu-id="854d4-150">In **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects, add hello following member toohello `MainPage` class.</span></span> <span data-ttu-id="854d4-151">Убедиться, что tooreplace быть `<Enter Your Backend Endpoint>` с hello ранее полученный фактическое серверной конечной точки.</span><span class="sxs-lookup"><span data-stu-id="854d4-151">Be sure tooreplace `<Enter Your Backend Endpoint>` with hello your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="854d4-152">Например, `http://mybackend.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="854d4-152">For example, `http://mybackend.azurewebsites.net`.</span></span>
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. <span data-ttu-id="854d4-153">Добавьте код hello ниже класс MainPage toohello в **MainPage.xaml.cs** для hello **(Windows 8.1)** и **(Windows Phone 8.1)** проектов.</span><span class="sxs-lookup"><span data-stu-id="854d4-153">Add hello code below toohello MainPage class in **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span>
    
    <span data-ttu-id="854d4-154">Hello `PushClick` метод — hello обработчика для hello **принудительной отправки** кнопки.</span><span class="sxs-lookup"><span data-stu-id="854d4-154">hello `PushClick` method is hello click handler for hello **Send Push** button.</span></span> <span data-ttu-id="854d4-155">Он вызывает hello серверной tootrigger tooall уведомления устройств с помощью имени пользователя тег, который соответствует hello `to_tag` параметра.</span><span class="sxs-lookup"><span data-stu-id="854d4-155">It calls hello backend tootrigger a notification tooall devices with a username tag that matches hello `to_tag` parameter.</span></span> <span data-ttu-id="854d4-156">Hello отправляется уведомление как содержимое JSON в теле запроса hello.</span><span class="sxs-lookup"><span data-stu-id="854d4-156">hello notification message is sent as JSON content in hello request body.</span></span>
    
    <span data-ttu-id="854d4-157">Hello `LoginAndRegisterClick` метод — hello обработчика для hello **вход и зарегистрируйте** кнопки.</span><span class="sxs-lookup"><span data-stu-id="854d4-157">hello `LoginAndRegisterClick` method is hello click handler for hello **Log in and register** button.</span></span> <span data-ttu-id="854d4-158">Он сохраняет hello basic токена проверки подлинности в локальном хранилище (Обратите внимание, что это касается любого токена, который использует схему проверки подлинности), затем использует `RegisterClient` tooregister для уведомлений с использованием внутреннего hello.</span><span class="sxs-lookup"><span data-stu-id="854d4-158">It stores hello basic authentication token in local storage (note that this represents any token your authentication scheme uses), then uses `RegisterClient` tooregister for notifications using hello backend.</span></span>

        private async void PushClick(object sender, RoutedEventArgs e)
        {
            if (toggleWNS.IsChecked.Value)
            {
                await sendPush("wns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleGCM.IsChecked.Value)
            {
                await sendPush("gcm", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleAPNS.IsChecked.Value)
            {
                await sendPush("apns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);

            }
        }

        private async Task sendPush(string pns, string userTag, string message)
        {
            var POST_URL = BACKEND_ENDPOINT + "/api/notifications?pns=" +
                pns + "&to_tag=" + userTag;

            using (var httpClient = new HttpClient())
            {
                var settings = ApplicationData.Current.LocalSettings.Values;
                httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);

                try
                {
                    await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                        System.Text.Encoding.UTF8, "application/json"));
                }
                catch (Exception ex)
                {
                    MessageDialog alert = new MessageDialog(ex.Message, "Failed toosend " + pns + " message");
                    alert.ShowAsync();
                }
            }
        }

        private async void LoginAndRegisterClick(object sender, RoutedEventArgs e)
        {
            SetAuthenticationTokenInLocalStorage();

            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // hello "username:<user name>" tag gets automatically added by hello message handler in hello backend.
            // hello tag passed here can be whatever other tags you may want toouse.
            try
            {
                // hello device handle used will be different depending on hello device and PNS. 
                // Windows devices use hello channel uri as hello PNS handle.
                await new RegisterClient(BACKEND_ENDPOINT).RegisterAsync(channel.Uri, new string[] { "myTag" });

                var dialog = new MessageDialog("Registered as: " + UsernameTextBox.Text);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
                SendPushButton.IsEnabled = true;
            }
            catch (Exception ex)
            {
                MessageDialog alert = new MessageDialog(ex.Message, "Failed tooregister with RegisterClient");
                alert.ShowAsync();
            }
        }

        private void SetAuthenticationTokenInLocalStorage()
        {
            string username = UsernameTextBox.Text;
            string password = PasswordTextBox.Password;

            var token = Convert.ToBase64String(System.Text.Encoding.UTF8.GetBytes(username + ":" + password));
            ApplicationData.Current.LocalSettings.Values["AuthenticationToken"] = token;
        }



1. <span data-ttu-id="854d4-159">В обозревателе решений в разделе hello **Shared** проект, откройте hello **App.xaml.cs** файла.</span><span class="sxs-lookup"><span data-stu-id="854d4-159">In Solution Explorer, under hello **Shared** project, open hello **App.xaml.cs** file.</span></span> <span data-ttu-id="854d4-160">Поиск вызова hello слишком`InitNotificationsAsync()` в hello `OnLaunched()` обработчика событий.</span><span class="sxs-lookup"><span data-stu-id="854d4-160">Find hello call too`InitNotificationsAsync()` in hello `OnLaunched()` event handler.</span></span> <span data-ttu-id="854d4-161">Закомментируйте или удалите вызов hello слишком`InitNotificationsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="854d4-161">Comment out or delete hello call too`InitNotificationsAsync()`.</span></span> <span data-ttu-id="854d4-162">Обработчик кнопки Hello добавленных выше будет инициализировать регистрации уведомлений.</span><span class="sxs-lookup"><span data-stu-id="854d4-162">hello button handler added above will initialize notification registrations.</span></span>

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. <span data-ttu-id="854d4-163">В обозревателе решений щелкните правой кнопкой мыши hello **Shared** проекта, а затем нажмите кнопку **добавить**, а затем нажмите кнопку **класса**.</span><span class="sxs-lookup"><span data-stu-id="854d4-163">In Solution Explorer, right-click hello **Shared** project, then click **Add**, and then click **Class**.</span></span> <span data-ttu-id="854d4-164">Имя класса hello **RegisterClient.cs**, нажмите кнопку **ОК** toogenerate hello класса.</span><span class="sxs-lookup"><span data-stu-id="854d4-164">Name hello class **RegisterClient.cs**, then click **OK** toogenerate hello class.</span></span>
   
   <span data-ttu-id="854d4-165">Этот класс будет переноситься hello REST вызывает необходимые toocontact hello внутреннего сервера приложения, в порядке tooregister push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="854d4-165">This class will wrap hello REST calls required toocontact hello app backend, in order tooregister for push notifications.</span></span> <span data-ttu-id="854d4-166">Она также локально хранит hello *свойства Registrationid* созданные hello концентратор уведомлений, как описано в [регистрации из серверной части приложения](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="854d4-166">It also locally stores hello *registrationIds* created by hello Notification Hub as detailed in [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="854d4-167">Обратите внимание, что он использует маркер авторизации, хранящихся в локальном хранилище, при нажатии кнопки hello **входа и регистрации** кнопки.</span><span class="sxs-lookup"><span data-stu-id="854d4-167">Note that it uses an authorization token stored in local storage when you click hello **Log in and register** button.</span></span>
2. <span data-ttu-id="854d4-168">Добавьте следующее hello `using` операторы в начале hello hello RegisterClient.cs файла:</span><span class="sxs-lookup"><span data-stu-id="854d4-168">Add hello following `using` statements at hello top of hello RegisterClient.cs file:</span></span>
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. <span data-ttu-id="854d4-169">Добавьте следующий код внутри hello hello `RegisterClient` определения класса.</span><span class="sxs-lookup"><span data-stu-id="854d4-169">Add hello following code inside hello `RegisterClient` class definition.</span></span>
   
       private string POST_URL;
   
       private class DeviceRegistration
       {
           public string Platform { get; set; }
           public string Handle { get; set; }
           public string[] Tags { get; set; }
       }
   
       public RegisterClient(string backendEndpoint)
       {
           POST_URL = backendEndpoint + "/api/register";
       }
   
       public async Task RegisterAsync(string handle, IEnumerable<string> tags)
       {
           var regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
   
           var deviceRegistration = new DeviceRegistration
           {
               Platform = "wns",
               Handle = handle,
               Tags = tags.ToArray<string>()
           };
   
           var statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
   
           if (statusCode == HttpStatusCode.Gone)
           {
               // regId is expired, deleting from local storage & recreating
               var settings = ApplicationData.Current.LocalSettings.Values;
               settings.Remove("__NHRegistrationId");
               regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
               statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
           }
   
           if (statusCode != HttpStatusCode.Accepted)
           {
               // log or throw
               throw new System.Net.WebException(statusCode.ToString());
           }
       }
   
       private async Task<HttpStatusCode> UpdateRegistrationAsync(string regId, DeviceRegistration deviceRegistration)
       {
           using (var httpClient = new HttpClient())
           {
               var settings = ApplicationData.Current.LocalSettings.Values;
               httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string) settings["AuthenticationToken"]);
   
               var putUri = POST_URL + "/" + regId;
   
               string json = JsonConvert.SerializeObject(deviceRegistration);
                               var response = await httpClient.PutAsync(putUri, new StringContent(json, Encoding.UTF8, "application/json"));
               return response.StatusCode;
           }
       }
   
       private async Task<string> RetrieveRegistrationIdOrRequestNewOneAsync()
       {
           var settings = ApplicationData.Current.LocalSettings.Values;
           if (!settings.ContainsKey("__NHRegistrationId"))
           {
               using (var httpClient = new HttpClient())
               {
                   httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                   var response = await httpClient.PostAsync(POST_URL, new StringContent(""));
                   if (response.IsSuccessStatusCode)
                   {
                       string regId = await response.Content.ReadAsStringAsync();
                       regId = regId.Substring(1, regId.Length - 2);
                       settings.Add("__NHRegistrationId", regId);
                   }
                   else
                   {
                       throw new System.Net.WebException(response.StatusCode.ToString());
                   }
               }
           }
           return (string)settings["__NHRegistrationId"];
   
       }
4. <span data-ttu-id="854d4-170">Сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="854d4-170">Save all your changes.</span></span>

## <a name="testing-hello-application"></a><span data-ttu-id="854d4-171">Тестирование приложения hello</span><span class="sxs-lookup"><span data-stu-id="854d4-171">Testing hello Application</span></span>
1. <span data-ttu-id="854d4-172">Запустите приложение hello на Windows 8.1 и Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="854d4-172">Launch hello application on both Windows 8.1 and Windows Phone 8.1.</span></span> <span data-ttu-id="854d4-173">Для Windows Phone 8.1 можно запустить экземпляр hello в эмуляторе hello или само устройство.</span><span class="sxs-lookup"><span data-stu-id="854d4-173">For Windows Phone 8.1 you can run hello instance in hello emulator or an actual device.</span></span>
2. <span data-ttu-id="854d4-174">В экземпляре hello Windows 8.1 приложение hello, введите **Username** и **пароль** как показано ниже экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="854d4-174">In hello Windows 8.1 instance of hello app, enter a **Username** and **Password** as shown in hello screen below.</span></span> <span data-ttu-id="854d4-175">Она должна отличаться от hello имя пользователя и пароль, введенные на Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="854d4-175">It should differ from hello user name and password you enter on Windows Phone.</span></span>
3. <span data-ttu-id="854d4-176">Щелкните **Вход и регистрация** и убедитесь, что в диалоговом окне отображается подтверждение выполнения входа.</span><span class="sxs-lookup"><span data-stu-id="854d4-176">Click **Log in and register** and verify a dialog shows that you have logged in.</span></span> <span data-ttu-id="854d4-177">Это также позволит hello **принудительной отправки** кнопки.</span><span class="sxs-lookup"><span data-stu-id="854d4-177">This will also enable hello **Send Push** button.</span></span>
   
    ![][14]
4. <span data-ttu-id="854d4-178">На экземпляре hello Windows Phone 8.1, введите строку имени пользователя в обоих hello **Username** и **пароль** поля, затем нажмите кнопку **входа и регистрации**.</span><span class="sxs-lookup"><span data-stu-id="854d4-178">On hello Windows Phone 8.1 instance, enter a user name string in both hello **Username** and **Password** fields then click **Login and register**.</span></span>
5. <span data-ttu-id="854d4-179">Затем в hello **тег Username получателя** введите имя пользователя hello, зарегистрированных в Windows 8.1.</span><span class="sxs-lookup"><span data-stu-id="854d4-179">Then in hello **Recipient Username Tag** field, enter hello user name registered on Windows 8.1.</span></span> <span data-ttu-id="854d4-180">Введите сообщение уведомления и нажмите кнопку **Отправить push-уведомление**.</span><span class="sxs-lookup"><span data-stu-id="854d4-180">Enter a notification message and click **Send Push**.</span></span>
   
    ![][16]
6. <span data-ttu-id="854d4-181">Только hello устройства, которые регистрировались hello соответствующий тег username сообщение hello уведомления.</span><span class="sxs-lookup"><span data-stu-id="854d4-181">Only hello devices that have registered with hello matching username tag receive hello notification message.</span></span>
   
    ![][15]

## <a name="next-steps"></a><span data-ttu-id="854d4-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="854d4-182">Next Steps</span></span>
* <span data-ttu-id="854d4-183">Если toosegment пользователям по группы интересов, см. [toosend использования концентраторов уведомлений, новости].</span><span class="sxs-lookup"><span data-stu-id="854d4-183">If you want toosegment your users by interest groups, see [Use Notification Hubs toosend breaking news].</span></span>
* <span data-ttu-id="854d4-184">см. Дополнительные сведения о том, как toolearn toouse концентраторов уведомлений, [руководство концентраторы уведомлений].</span><span class="sxs-lookup"><span data-stu-id="854d4-184">toolearn more about how toouse Notification Hubs, see [Notification Hubs Guidance].</span></span>

[9]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push9.png
[10]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push10.png
[11]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push11.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-ui.png
[14]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-windows-instance-username.png
[15]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-notification-received.png
[16]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-send-message.png



<!-- URLs. -->
[приступить к работе с концентраторами уведомлений]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[принудительной защиты]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md
[toosend использования концентраторов уведомлений, новости]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[руководство концентраторы уведомлений]: http://msdn.microsoft.com/library/jj927170.aspx
