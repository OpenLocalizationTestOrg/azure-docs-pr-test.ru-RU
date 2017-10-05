---
title: "Использование центров уведомлений для передачи экстренных новостей (Windows Phone)"
description: "Использование Центров уведомлений Azure для применения тегов в регистрациях, чтобы передавать экстренные новости в приложение Windows Phone."
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
ms.openlocfilehash: 3a6a69bf555c7267d3fbeb03ff6c03054991960f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="6e693-103">Использование концентраторов уведомлений для передачи экстренных новостей</span><span class="sxs-lookup"><span data-stu-id="6e693-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="6e693-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="6e693-104">Overview</span></span>
<span data-ttu-id="6e693-105">В этом разделе показано, как использовать концентраторы уведомлений Azure для рассылки уведомлений об экстренных новостях в приложение Windows Phone 8.0/8.1 Silverlight.</span><span class="sxs-lookup"><span data-stu-id="6e693-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to a Windows Phone 8.0/8.1 Silverlight app.</span></span> <span data-ttu-id="6e693-106">Если вы используете приложение Windows Store или Windows Phone 8.1, см. версию [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span><span class="sxs-lookup"><span data-stu-id="6e693-106">If you are targeting Windows Store or Windows Phone 8.1 app, please refer to to the [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) version.</span></span> <span data-ttu-id="6e693-107">По завершении вы сможете зарегистрироваться в интересующих вас категориях экстренных новостей и получать push-уведомления только для этих категорий.</span><span class="sxs-lookup"><span data-stu-id="6e693-107">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="6e693-108">Данный сценарий является общеупотребимым шаблоном для многих приложений, где требуется отправлять уведомления группам пользователей, ранее проявивших к ним интерес, например, программы чтения RSS, приложений для музыкальных фанатов и т. д.</span><span class="sxs-lookup"><span data-stu-id="6e693-108">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="6e693-109">Широковещательные сценарии реализуются путем включения одного или нескольких *тегов* при создании регистрации в концентраторе уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6e693-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="6e693-110">Если уведомления отправляются на тег, их получают все устройства, зарегистрированные для данного тега.</span><span class="sxs-lookup"><span data-stu-id="6e693-110">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="6e693-111">Поскольку теги представляют собой обычные строки, их не нужно подготавливать заранее.</span><span class="sxs-lookup"><span data-stu-id="6e693-111">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="6e693-112">Дополнительные сведения о тегах см. в статье [Маршрутизация и выражения тегов](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="6e693-112">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e693-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6e693-113">Prerequisites</span></span>
<span data-ttu-id="6e693-114">Материал данной статьи основан на приложении, созданном в статье [Отправка push-уведомлений в приложения Windows Phone с помощью центров уведомлений Azure].</span><span class="sxs-lookup"><span data-stu-id="6e693-114">This topic builds on the app you created in [Get started with Notification Hubs].</span></span> <span data-ttu-id="6e693-115">Перед началом работы с учебником необходимо пройти задания учебника [Отправка push-уведомлений в приложения Windows Phone с помощью центров уведомлений Azure].</span><span class="sxs-lookup"><span data-stu-id="6e693-115">Before starting this tutorial, you must have already completed [Get started with Notification Hubs].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="6e693-116">Добавление возможности выбора категорий в приложение</span><span class="sxs-lookup"><span data-stu-id="6e693-116">Add category selection to the app</span></span>
<span data-ttu-id="6e693-117">Прежде всего необходимо добавить элементы пользовательского интерфейса для имеющейся главной страницы, позволяющие пользователю выбирать категории для регистрации.</span><span class="sxs-lookup"><span data-stu-id="6e693-117">The first step is to add the UI elements to your existing main page that enable the user to select categories to register.</span></span> <span data-ttu-id="6e693-118">Выбранные пользователем категории хранятся на устройстве.</span><span class="sxs-lookup"><span data-stu-id="6e693-118">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="6e693-119">При запуске приложения в концентраторе уведомлений создается регистрация устройства с выбранными категориями, представленными в форме тегов.</span><span class="sxs-lookup"><span data-stu-id="6e693-119">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="6e693-120">Откройте файл проекта MainPage.xaml, а затем замените элементы **Grid** с именами `TitlePanel` и `ContentPanel` следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="6e693-120">Open the MainPage.xaml project file, then replace the **Grid** elements named `TitlePanel` and `ContentPanel` with the following code:</span></span>
   
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
2. <span data-ttu-id="6e693-121">Создайте в проекте класс **Notifications**, добавьте к определению класса модификатор **public**, а затем добавьте в файл оператор **using**.</span><span class="sxs-lookup"><span data-stu-id="6e693-121">In the project, create a new class named **Notifications**, add the **public** modifier to the class definition, then add the following **using** statements to the new code file:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. <span data-ttu-id="6e693-122">Скопируйте следующий код в новый класс **Notifications** :</span><span class="sxs-lookup"><span data-stu-id="6e693-122">Copy the following code into the new **Notifications** class:</span></span>
   
        private NotificationHub hub;
   
        // Registration task to complete registration in the ChannelUriUpdated event handler
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
   
                // This is optional, used to receive notifications while the app is running.
                channel.ShellToastNotificationReceived += channel_ShellToastNotificationReceived;
            }
   
            // If channel.ChannelUri is not null, we will complete the registrationTask here.  
            // If it is null, the registrationTask will be completed in the ChannelUriUpdated event handler.
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
            // Using a template registration to support notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyMPNS = "<wp:Notification xmlns:wp=\"WPNotification\">" +
                                                "<wp:Toast>" +
                                                    "<wp:Text1>$(messageParam)</wp:Text1>" +
                                                "</wp:Toast>" +
                                            "</wp:Notification>";
   
            // The stored categories tags are passed with the template registration.
   
            registrationTask.SetResult(await hub.RegisterTemplateAsync(channelUri.ToString(), 
                templateBodyMPNS, "simpleMPNSTemplateExample", this.RetrieveCategories()));
   
            return await registrationTask.Task;
        }
   
        // This is optional. It is used to receive notifications while the app is running.
        void channel_ShellToastNotificationReceived(object sender, NotificationEventArgs e)
        {
            StringBuilder message = new StringBuilder();
            string relativeUri = string.Empty;
   
            message.AppendFormat("Received Toast {0}:\n", DateTime.Now.ToShortTimeString());
   
            // Parse out the information that was part of the message.
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
   
            // Display a dialog of all the fields in the toast.
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() => 
            { 
                MessageBox.Show(message.ToString()); 
            });
        }

    <span data-ttu-id="6e693-123">Этот класс использует изолированное хранилище для хранения категорий новостей, которые должно получать данное устройство.</span><span class="sxs-lookup"><span data-stu-id="6e693-123">This class uses the isolated storage to store the categories of news that this device is to receive.</span></span> <span data-ttu-id="6e693-124">Он также содержит методы регистрации в этих категориях с помощью [шаблонной](notification-hubs-templates-cross-platform-push-messages.md) регистрации уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6e693-124">It also contains methods to register for these categories using a [template](notification-hubs-templates-cross-platform-push-messages.md) notification registration.</span></span>


1. <span data-ttu-id="6e693-125">В файле проекта App.xaml.cs добавьте следующее свойство в класс **App** .</span><span class="sxs-lookup"><span data-stu-id="6e693-125">In the App.xaml.cs project file, add the following property to the **App** class.</span></span> <span data-ttu-id="6e693-126">Замените заполнители `<hub name>` и `<connection string with listen access>` именем центра уведомлений и строкой подключения для *DefaultListenSharedAccessSignature*, полученными ранее.</span><span class="sxs-lookup"><span data-stu-id="6e693-126">Replace the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > <span data-ttu-id="6e693-127">Так как учетные данные, которые распространяются с помощью клиентского приложения, обычно небезопасны, с помощью вашего клиентского приложения следует распространять только ключ для доступа к прослушиванию.</span><span class="sxs-lookup"><span data-stu-id="6e693-127">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="6e693-128">Доступ к прослушиванию позволяет приложению регистрироваться для использования уведомлений, однако при этом нельзя изменять имеющиеся регистрации и отправлять уведомления.</span><span class="sxs-lookup"><span data-stu-id="6e693-128">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="6e693-129">Для отправки уведомлений и изменения существующих регистраций используется ключ полного доступа в защищенной серверной службе.</span><span class="sxs-lookup"><span data-stu-id="6e693-129">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
2. <span data-ttu-id="6e693-130">В MainPage.xaml.cs добавьте следующую строку:</span><span class="sxs-lookup"><span data-stu-id="6e693-130">In your MainPage.xaml.cs, add the following line:</span></span>
   
        using Windows.UI.Popups;
3. <span data-ttu-id="6e693-131">В файле проекта MainPage.xaml.cs добавьте следующий метод:</span><span class="sxs-lookup"><span data-stu-id="6e693-131">In the MainPage.xaml.cs project file, add the following method:</span></span>
   
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
   
    <span data-ttu-id="6e693-132">Этот метод создает список категорий и использует класс **Notifications** класс для хранения списка в локальном хранилище и регистрации соответствующих тегов в концентраторе уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6e693-132">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="6e693-133">При изменении категорий регистрация создается заново с новыми категориями.</span><span class="sxs-lookup"><span data-stu-id="6e693-133">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="6e693-134">Ваше приложение теперь может сохранять набор категорий в локальном хранилище на устройстве и регистрироваться в центре уведомлений всякий раз, когда пользователь изменяет выбранные категории.</span><span class="sxs-lookup"><span data-stu-id="6e693-134">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="6e693-135">Регистрация для использования уведомлений</span><span class="sxs-lookup"><span data-stu-id="6e693-135">Register for notifications</span></span>
<span data-ttu-id="6e693-136">Эти действия позволяют зарегистрироваться в концентраторе уведомлений при запуске с использованием категорий, сохраненных в локальном хранилище.</span><span class="sxs-lookup"><span data-stu-id="6e693-136">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="6e693-137">Поскольку URI канала, назначенный службой push-уведомлений Windows (MPNS), может измениться в любое время, следует регулярно производить регистрацию для использования уведомлений, чтобы предотвратить сбои уведомлений.</span><span class="sxs-lookup"><span data-stu-id="6e693-137">Because the channel URI assigned by the Microsoft Push Notification Service (MPNS) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="6e693-138">В этом примере регистрация для использования уведомлений осуществляется при каждом запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="6e693-138">This example registers for notifications every time that the app starts.</span></span> <span data-ttu-id="6e693-139">Для тех приложений, которые запускаются часто, более одного раза в день, возможно, лучше пропустить регистрацию, чтобы сэкономить трафик, если с момента прошлой регистрации прошло меньше суток.</span><span class="sxs-lookup"><span data-stu-id="6e693-139">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="6e693-140">Откройте файл App.xaml.cs, добавьте модификатор **async** в метод **Application_Launching** и замените код регистрации центров уведомлений, добавленный в [Отправка push-уведомлений в приложения Windows Phone с помощью центров уведомлений Azure], следующей строкой кода.</span><span class="sxs-lookup"><span data-stu-id="6e693-140">Open the App.xaml.cs file and add the **async** modifier to **Application_Launching** method and replace the Notification Hubs registration code that you added in [Get started with Notification Hubs] with the following code:</span></span>
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    <span data-ttu-id="6e693-141">Это гарантирует, что при каждом запуске приложения оно извлекает категории из локального хранилища и запрашивает для них регистрацию.</span><span class="sxs-lookup"><span data-stu-id="6e693-141">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registration for these categories.</span></span>
2. <span data-ttu-id="6e693-142">В файле проекта MainPage.xaml.cs добавьте следующий код, который выполняет метод **OnNavigatedTo** :</span><span class="sxs-lookup"><span data-stu-id="6e693-142">In the MainPage.xaml.cs project file, add the following code that implements the **OnNavigatedTo** method:</span></span>
   
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
   
    <span data-ttu-id="6e693-143">При этом главная страница обновляется в зависимости от состояния ранее сохраненных категорий.</span><span class="sxs-lookup"><span data-stu-id="6e693-143">This updates the main page based on the status of previously saved categories.</span></span>

<span data-ttu-id="6e693-144">Теперь приложение готово и может сохранять набор категорий в локальном хранилище устройств и использовать его для регистрации в концентраторе уведомлений всякий раз, когда пользователь изменяет выбранные категории.</span><span class="sxs-lookup"><span data-stu-id="6e693-144">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="6e693-145">А сейчас определим серверную часть, которая может отправлять уведомления категорий в это приложение.</span><span class="sxs-lookup"><span data-stu-id="6e693-145">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="6e693-146">Отправка уведомлений с тегами</span><span class="sxs-lookup"><span data-stu-id="6e693-146">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="6e693-147">Запуск приложения и создание уведомлений</span><span class="sxs-lookup"><span data-stu-id="6e693-147">Run the app and generate notifications</span></span>
1. <span data-ttu-id="6e693-148">В Visual Studio нажмите клавишу F5, чтобы скомпилировать и запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="6e693-148">In Visual Studio, press F5 to compile and start the app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="6e693-149">Обратите внимание, что в пользовательском интерфейсе присутствует набор переключателей, позволяющий выбрать категории для подписки.</span><span class="sxs-lookup"><span data-stu-id="6e693-149">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="6e693-150">Включите переключатели одной или нескольких категорий, затем нажмите **Подписаться**.</span><span class="sxs-lookup"><span data-stu-id="6e693-150">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="6e693-151">Приложение преобразует выбранные категории в теги и запрашивает у концентратора уведомлений новую регистрацию устройств для выбранных тегов.</span><span class="sxs-lookup"><span data-stu-id="6e693-151">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="6e693-152">Зарегистрированные категории возвращаются и отображаются в диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="6e693-152">The registered categories are returned and displayed in a dialog.</span></span>
   
    ![][2]
3. <span data-ttu-id="6e693-153">После получения подтверждения того, что подписка на категории была завершена, запустите консольное приложение для отправки уведомлений для каждой категории.</span><span class="sxs-lookup"><span data-stu-id="6e693-153">After receiving a confirmation that your categories were subscription completed, run the console app to send notifications for each categories.</span></span> <span data-ttu-id="6e693-154">Убедитесь, что получены только уведомления для категорий, на которые вы подписаны.</span><span class="sxs-lookup"><span data-stu-id="6e693-154">Verify you only receive a notification for the categories you have subscribed to.</span></span>
   
    ![][3]

<span data-ttu-id="6e693-155">Вы завершили эту тему.</span><span class="sxs-lookup"><span data-stu-id="6e693-155">You have completed this topic.</span></span>

<!--##Next steps

In this tutorial we learned how to broadcast breaking news by category. Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:

+ [Use Notification Hubs to broadcast localized breaking news]

    Learn how to expand the breaking news app to enable sending localized notifications.

+ [Notify users with Notification Hubs]

    Learn how to push notifications to specific authenticated users. This is a good solution for sending notifications only to specific users.
-->

<!-- Anchors. -->
[Add category selection to the app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run the app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-breakingnews.png
[2]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-registration.png
[3]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-toast.png



<!-- URLs.-->
<span data-ttu-id="6e693-156">[Отправка push-уведомлений в приложения Windows Phone с помощью центров уведомлений Azure]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/</span><span class="sxs-lookup"><span data-stu-id="6e693-156">[Get started with Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/</span></span>
[Use Notification Hubs to broadcast localized breaking news]: ../breakingnews-localized-wp8.md
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users/
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Phone]: ??

