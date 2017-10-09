---
title: "Концентраторы уведомлений toosend aaaUse, новости (Windows Phone)"
description: "Используйте тег toouse концентраторов уведомлений Azure в критические приложения Windows Phone tooa новостей toosend регистраций."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: 42726bf5-cc82-438d-9eaa-238da3322d80
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 3519a8701105f88198afe288e59e9204420234db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="7c8a2-103">Использование концентраторов уведомлений toosend новости</span><span class="sxs-lookup"><span data-stu-id="7c8a2-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="7c8a2-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="7c8a2-104">Overview</span></span>
<span data-ttu-id="7c8a2-105">В этом разделе показано, как toouse концентраторов уведомлений Azure toobroadcast критические новостей уведомления tooa Windows Phone 8.0/8.1 приложение Silverlight.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooa Windows Phone 8.0/8.1 Silverlight app.</span></span> <span data-ttu-id="7c8a2-106">Если вы используете магазина Windows или приложения Windows Phone 8.1, можно найти tootoohello [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) версии.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-106">If you are targeting Windows Store or Windows Phone 8.1 app, please refer tootoohello [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) version.</span></span> <span data-ttu-id="7c8a2-107">После завершения будет быть может tooregister переноса категории новостей нужных вам и получения только push-уведомлений для этих категорий.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-107">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="7c8a2-108">Этот сценарий представлен общий шаблон для многих приложений, где уведомления состоят из отправленных toobe toogroups пользователей, которым был объявлен ранее интересующих их, например, средство чтения RSS, приложений для вентиляторов музыку и т. д.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-108">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="7c8a2-109">Широковещательный сценарии реализуются путем включения одного или нескольких *теги* при создании регистрации в концентраторе уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="7c8a2-110">Отправке уведомлений tooa тегов, все устройства, которые зарегистрированы для тега hello получат уведомление hello.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-110">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="7c8a2-111">Так как теги являются просто строками, у которых нет toobe заранее подготовлены.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-111">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="7c8a2-112">Дополнительные сведения о тегах см. в разделе слишком[маршрутизации концентраторов уведомлений и выражения с тегами](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="7c8a2-112">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c8a2-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7c8a2-113">Prerequisites</span></span>
<span data-ttu-id="7c8a2-114">В этом разделе основан на приложение hello, созданный в [приступить к работе с концентраторами уведомлений].</span><span class="sxs-lookup"><span data-stu-id="7c8a2-114">This topic builds on hello app you created in [Get started with Notification Hubs].</span></span> <span data-ttu-id="7c8a2-115">Перед началом работы с учебником необходимо пройти задания учебника [приступить к работе с концентраторами уведомлений].</span><span class="sxs-lookup"><span data-stu-id="7c8a2-115">Before starting this tutorial, you must have already completed [Get started with Notification Hubs].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="7c8a2-116">Добавить приложение toohello Выбор категории</span><span class="sxs-lookup"><span data-stu-id="7c8a2-116">Add category selection toohello app</span></span>
<span data-ttu-id="7c8a2-117">Hello первым шагом является tooadd hello пользовательского интерфейса элементы tooyour существующей главной страницы, включить tooregister категории tooselect пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-117">hello first step is tooadd hello UI elements tooyour existing main page that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="7c8a2-118">выбранные пользователем категории Hello хранятся на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-118">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="7c8a2-119">При запуске приложение hello регистрацию устройств создается в концентратор уведомлений с категориями hello выбран как теги.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-119">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="7c8a2-120">Откройте файл проекта MainPage.xaml hello, а затем заменить hello **сетки** элементы с именем `TitlePanel` и `ContentPanel` с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="7c8a2-120">Open hello MainPage.xaml project file, then replace hello **Grid** elements named `TitlePanel` and `ContentPanel` with hello following code:</span></span>
   
        <StackPanel x:Name="TitlePanel" Grid.Row="0" Margin="12,17,0,28">
            <TextBlock Text="Breaking News" Style="{StaticResource PhoneTextNormalStyle}" Margin="12,0"/>
            <TextBlock Text="Categories" Margin="9,-7,0,0" Style="{StaticResource PhoneTextTitle1Style}"/>
        </StackPanel>
   
        <Grid Name="ContentPanel" Grid.Row="1" Margin="12,0,12,0">
            <Grid.RowDefinitions>
                <RowDefinition Height="auto"/>
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition />
                <ColumnDefinition />
            </Grid.ColumnDefinitions>
            <CheckBox Name="WorldCheckBox" Grid.Row="0" Grid.Column="0">World</CheckBox>
            <CheckBox Name="PoliticsCheckBox" Grid.Row="1" Grid.Column="0">Politics</CheckBox>
            <CheckBox Name="BusinessCheckBox" Grid.Row="2" Grid.Column="0">Business</CheckBox>
            <CheckBox Name="TechnologyCheckBox" Grid.Row="0" Grid.Column="1">Technology</CheckBox>
            <CheckBox Name="ScienceCheckBox" Grid.Row="1" Grid.Column="1">Science</CheckBox>
            <CheckBox Name="SportsCheckBox" Grid.Row="2" Grid.Column="1">Sports</CheckBox>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="3" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click" />
        </Grid>
2. <span data-ttu-id="7c8a2-121">В проекте hello, создайте новый класс с именем **уведомления**, добавить hello **открытый** toohello модификатор определения класса, а затем добавьте следующие hello **с помощью** инструкций toohello новый файл кода:</span><span class="sxs-lookup"><span data-stu-id="7c8a2-121">In hello project, create a new class named **Notifications**, add hello **public** modifier toohello class definition, then add hello following **using** statements toohello new code file:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. <span data-ttu-id="7c8a2-122">Копирования hello следующий код в новый hello **уведомления** класса:</span><span class="sxs-lookup"><span data-stu-id="7c8a2-122">Copy hello following code into hello new **Notifications** class:</span></span>
   
        private NotificationHub hub;
   
        // Registration task toocomplete registration in hello ChannelUriUpdated event handler
        private TaskCompletionSource<Registration> registrationTask;
   
        public Notifications(string hubName, string listenConnectionString)
        {
            hub = new NotificationHub(hubName, listenConnectionString);
        }
   
        public IEnumerable<string> RetrieveCategories()
        {
            var categories = (string)IsolatedStorageSettings.ApplicationSettings["categories"];
            return categories != null ? categories.Split(',') : new string[0];
        }
   
        public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
        {
            var categoriesAsString = string.Join(",", categories);
            var settings = IsolatedStorageSettings.ApplicationSettings;
            if (!settings.Contains("categories"))
            {
                settings.Add("categories", categoriesAsString);
            }
            else
            {
                settings["categories"] = categoriesAsString;
            }
            settings.Save();
   
            return await SubscribeToCategories();
        }
   
        public async Task<Registration> SubscribeToCategories()
        {
            registrationTask = new TaskCompletionSource<Registration>();
   
            var channel = HttpNotificationChannel.Find("MyPushChannel");
   
            if (channel == null)
            {
                channel = new HttpNotificationChannel("MyPushChannel");
                channel.Open();
                channel.BindToShellToast();
                channel.ChannelUriUpdated += channel_ChannelUriUpdated;
   
                // This is optional, used tooreceive notifications while hello app is running.
                channel.ShellToastNotificationReceived += channel_ShellToastNotificationReceived;
            }
   
            // If channel.ChannelUri is not null, we will complete hello registrationTask here.  
            // If it is null, hello registrationTask will be completed in hello ChannelUriUpdated event handler.
            if (channel.ChannelUri != null)
            {
                await RegisterTemplate(channel.ChannelUri);
            }
   
            return await registrationTask.Task;
        }
   
        async void channel_ChannelUriUpdated(object sender, NotificationChannelUriEventArgs e)
        {
            await RegisterTemplate(e.ChannelUri);
        }
   
        async Task<Registration> RegisterTemplate(Uri channelUri)
        {
            // Using a template registration toosupport notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyMPNS = "<wp:Notification xmlns:wp=\"WPNotification\">" +
                                                "<wp:Toast>" +
                                                    "<wp:Text1>$(messageParam)</wp:Text1>" +
                                                "</wp:Toast>" +
                                            "</wp:Notification>";
   
            // hello stored categories tags are passed with hello template registration.
   
            registrationTask.SetResult(await hub.RegisterTemplateAsync(channelUri.ToString(), 
                templateBodyMPNS, "simpleMPNSTemplateExample", this.RetrieveCategories()));
   
            return await registrationTask.Task;
        }
   
        // This is optional. It is used tooreceive notifications while hello app is running.
        void channel_ShellToastNotificationReceived(object sender, NotificationEventArgs e)
        {
            StringBuilder message = new StringBuilder();
            string relativeUri = string.Empty;
   
            message.AppendFormat("Received Toast {0}:\n", DateTime.Now.ToShortTimeString());
   
            // Parse out hello information that was part of hello message.
            foreach (string key in e.Collection.Keys)
            {
                message.AppendFormat("{0}: {1}\n", key, e.Collection[key]);
   
                if (string.Compare(
                    key,
                    "wp:Param",
                    System.Globalization.CultureInfo.InvariantCulture,
                    System.Globalization.CompareOptions.IgnoreCase) == 0)
                {
                    relativeUri = e.Collection[key];
                }
            }
   
            // Display a dialog of all hello fields in hello toast.
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() => 
            { 
                MessageBox.Show(message.ToString()); 
            });
        }

    <span data-ttu-id="7c8a2-123">Этот класс использует hello изолированные хранилища toostore hello категории новостей, что устройство является tooreceive.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-123">This class uses hello isolated storage toostore hello categories of news that this device is tooreceive.</span></span> <span data-ttu-id="7c8a2-124">Он также содержит методы tooregister для следующих категорий с помощью [шаблона](notification-hubs-templates-cross-platform-push-messages.md) регистрации уведомлений.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-124">It also contains methods tooregister for these categories using a [template](notification-hubs-templates-cross-platform-push-messages.md) notification registration.</span></span>


1. <span data-ttu-id="7c8a2-125">Добавьте в файл проекта App.xaml.cs hello hello следующие свойства toohello **приложения** класса.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-125">In hello App.xaml.cs project file, add hello following property toohello **App** class.</span></span> <span data-ttu-id="7c8a2-126">Замените hello `<hub name>` и `<connection string with listen access>` местозаполнителей уведомления имя и hello строку подключения к концентратору для *DefaultListenSharedAccessSignature* , полученный ранее.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-126">Replace hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > <span data-ttu-id="7c8a2-127">Так как учетные данные, которые распространяются с помощью клиентского приложения, обычно не безопасны, hello ключ для прослушивания доступа следует распространять только с помощью клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-127">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="7c8a2-128">Прослушивать доступа включает tooregister вашего приложения для уведомлений, но существующие регистрации нельзя изменить, и не может отправлять уведомления.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-128">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="7c8a2-129">Полный доступ Hello используется в защищенной серверной службе для отправки уведомлений и изменять существующие регистрации.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-129">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
2. <span data-ttu-id="7c8a2-130">Добавьте в ваш MainPage.xaml.cs hello, следующей строкой.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-130">In your MainPage.xaml.cs, add hello following line:</span></span>
   
        using Windows.UI.Popups;
3. <span data-ttu-id="7c8a2-131">В файле проекта MainPage.xaml.cs hello добавьте следующий метод hello:</span><span class="sxs-lookup"><span data-stu-id="7c8a2-131">In hello MainPage.xaml.cs project file, add hello following method:</span></span>
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
          var categories = new HashSet<string>();
          if (WorldCheckBox.IsChecked == true) categories.Add("World");
          if (PoliticsCheckBox.IsChecked == true) categories.Add("Politics");
          if (BusinessCheckBox.IsChecked == true) categories.Add("Business");
          if (TechnologyCheckBox.IsChecked == true) categories.Add("Technology");
          if (ScienceCheckBox.IsChecked == true) categories.Add("Science");
          if (SportsCheckBox.IsChecked == true) categories.Add("Sports");
   
          var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);
   
          MessageBox.Show("Subscribed to: " + string.Join(",", categories) + " on registration id : " +
             result.RegistrationId);
        }
   
    <span data-ttu-id="7c8a2-132">Этот метод создает список категорий и использует hello **уведомления** класса toostore список hello в локальном хранилище hello и зарегистрируйте hello соответствующие теги в концентраторе уведомлений.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-132">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="7c8a2-133">При изменении категории регистрации hello воссоздается при hello новые категории.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-133">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="7c8a2-134">Приложение теперь может toostore набор категорий в локальном хранилище на устройстве hello и зарегистрировать с концентратором уведомлений hello всякий раз, когда изменения пользователя hello hello выбора категорий.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-134">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="7c8a2-135">Регистрация для использования уведомлений</span><span class="sxs-lookup"><span data-stu-id="7c8a2-135">Register for notifications</span></span>
<span data-ttu-id="7c8a2-136">Эти шаги зарегистрировать hello концентратора уведомлений при запуске с помощью категорий hello, хранящихся в локальном хранилище.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-136">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="7c8a2-137">URI, присвоенный hello Microsoft Push Notification Service (MPNS) hello канала может меняться в любое время, следует зарегистрировать для получения уведомлений часто tooavoid сбоев уведомлений.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-137">Because hello channel URI assigned by hello Microsoft Push Notification Service (MPNS) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="7c8a2-138">В этом примере регистрируется для уведомлений, каждый раз при запуске этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-138">This example registers for notifications every time that hello app starts.</span></span> <span data-ttu-id="7c8a2-139">Для приложений, которые часто выполняются более чем один раз в день, возможно, если можно пропустить пропускной способности toopreserve регистрации менее чем за день прошел с момента предыдущей регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-139">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="7c8a2-140">Откройте файл App.xaml.cs hello и добавьте hello **async** модификатор слишком**Application_Launching** метод и заменить код регистрации hello концентраторов уведомлений, добавленный в [приступить к работе с концентраторами уведомлений] с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="7c8a2-140">Open hello App.xaml.cs file and add hello **async** modifier too**Application_Launching** method and replace hello Notification Hubs registration code that you added in [Get started with Notification Hubs] with hello following code:</span></span>
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    <span data-ttu-id="7c8a2-141">Это гарантирует, что каждый раз при запуске приложение hello он получает hello категорий из локального хранилища и запросов регистрации для следующих категорий.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-141">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registration for these categories.</span></span>
2. <span data-ttu-id="7c8a2-142">В файле проекта MainPage.xaml.cs hello, добавьте следующий код, который реализует hello hello **OnNavigatedTo** метод:</span><span class="sxs-lookup"><span data-stu-id="7c8a2-142">In hello MainPage.xaml.cs project file, add hello following code that implements hello **OnNavigatedTo** method:</span></span>
   
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            var categories = ((App)Application.Current).notifications.RetrieveCategories();
   
            if (categories.Contains("World")) WorldCheckBox.IsChecked = true;
            if (categories.Contains("Politics")) PoliticsCheckBox.IsChecked = true;
            if (categories.Contains("Business")) BusinessCheckBox.IsChecked = true;
            if (categories.Contains("Technology")) TechnologyCheckBox.IsChecked = true;
            if (categories.Contains("Science")) ScienceCheckBox.IsChecked = true;
            if (categories.Contains("Sports")) SportsCheckBox.IsChecked = true;
        }
   
    <span data-ttu-id="7c8a2-143">Этого обновления hello главной страницы на основе состояния hello ранее сохраненные категорий.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-143">This updates hello main page based on hello status of previously saved categories.</span></span>

<span data-ttu-id="7c8a2-144">приложение Hello завершен, можно сохранить набор категорий в hello tooregister локального хранилища используется устройством с концентратором уведомлений hello всякий раз, когда изменения пользователя hello hello выбора категорий.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-144">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="7c8a2-145">Затем мы определим серверной части, можно отправить приложение toothis категории уведомлений.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-145">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="7c8a2-146">Отправка уведомлений с тегами</span><span class="sxs-lookup"><span data-stu-id="7c8a2-146">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="7c8a2-147">Запустите приложение hello и создавать уведомления</span><span class="sxs-lookup"><span data-stu-id="7c8a2-147">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="7c8a2-148">В Visual Studio нажмите клавишу F5 toocompile и запустить приложение hello.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-148">In Visual Studio, press F5 toocompile and start hello app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="7c8a2-149">Обратите внимание, что приложение hello пользовательского интерфейса предоставляет набор переключает, позволяет выбрать toosubscribe hello категорий для.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-149">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="7c8a2-150">Включите переключатели одной или нескольких категорий, затем нажмите **Подписаться**.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-150">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="7c8a2-151">приложение Hello преобразует hello выбранной категории в теги и запрашивает новую регистрацию устройств для hello выбранных тегов из концентратора уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-151">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="7c8a2-152">Hello зарегистрированных категорий возвращается и отображается в диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-152">hello registered categories are returned and displayed in a dialog.</span></span>
   
    ![][2]
3. <span data-ttu-id="7c8a2-153">После получения подтверждения, что категорий были завершения подписки, запустите уведомления toosend hello консольного приложения для каждой категории.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-153">After receiving a confirmation that your categories were subscription completed, run hello console app toosend notifications for each categories.</span></span> <span data-ttu-id="7c8a2-154">Убедитесь, что только вы получаете уведомление для hello категорий, которые вы подписаны.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-154">Verify you only receive a notification for hello categories you have subscribed to.</span></span>
   
    ![][3]

<span data-ttu-id="7c8a2-155">Вы завершили эту тему.</span><span class="sxs-lookup"><span data-stu-id="7c8a2-155">You have completed this topic.</span></span>

<!--##Next steps

In this tutorial we learned how toobroadcast breaking news by category. Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:

+ [Use Notification Hubs toobroadcast localized breaking news]

    Learn how tooexpand hello breaking news app tooenable sending localized notifications.

+ [Notify users with Notification Hubs]

    Learn how toopush notifications toospecific authenticated users. This is a good solution for sending notifications only toospecific users.
-->

<!-- Anchors. -->
[Add category selection toohello app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run hello app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-breakingnews.png
[2]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-registration.png
[3]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-toast.png



<!-- URLs.-->
[приступить к работе с концентраторами уведомлений]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/
[Use Notification Hubs toobroadcast localized breaking news]: ../breakingnews-localized-wp8.md
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users/
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Phone]: ??

