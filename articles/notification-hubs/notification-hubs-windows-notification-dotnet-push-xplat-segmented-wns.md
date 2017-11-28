---
title: "Использование центров уведомлений для передачи экстренных новостей (Универсальное приложение Windows)"
description: "Использование центров уведомлений Azure с тегами в регистрации для передачи экстренных новостей в универсальное приложение для Windows."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: 994d2eed-f62e-433c-bf65-4afebf1c0561
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0e945b5626a08fcb428131f2abb465c2c141011a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="b9786-103">Использование концентраторов уведомлений для передачи экстренных новостей</span><span class="sxs-lookup"><span data-stu-id="b9786-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="b9786-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="b9786-104">Overview</span></span>
<span data-ttu-id="b9786-105">В этом разделе рассказывается, как использовать центры уведомлений для отправки уведомлений о важных новостях в магазин Windows и приложение Windows 8.1 (без использования Silverlight).</span><span class="sxs-lookup"><span data-stu-id="b9786-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to a Windows Store or Windows Phone 8.1 (non-Silverlight) app.</span></span> <span data-ttu-id="b9786-106">Если вы намерены использовать Windows Phone 8.1 Silverlight, см. версию статьи для [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md).</span><span class="sxs-lookup"><span data-stu-id="b9786-106">If you are targeting Windows Phone 8.1 Silverlight, please refer to the [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) version.</span></span> <span data-ttu-id="b9786-107">По завершении вы сможете зарегистрироваться в интересующих вас категориях экстренных новостей и получать push-уведомления только для этих категорий.</span><span class="sxs-lookup"><span data-stu-id="b9786-107">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="b9786-108">Этот сценарий является общим шаблоном для многих приложений, где требуется отправлять уведомления группам пользователей, которые ранее проявили к ним интерес (например, средства чтения RSS, приложения для любителей музыки и т. д.).</span><span class="sxs-lookup"><span data-stu-id="b9786-108">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, and so on.</span></span> 

<span data-ttu-id="b9786-109">Широковещательные сценарии реализуются путем включения одного или нескольких *тегов* при создании регистрации в концентраторе уведомлений.</span><span class="sxs-lookup"><span data-stu-id="b9786-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="b9786-110">Если уведомления отправляются на тег, их получают все устройства, зарегистрированные для данного тега.</span><span class="sxs-lookup"><span data-stu-id="b9786-110">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="b9786-111">Поскольку теги представляют собой обычные строки, их не нужно подготавливать заранее.</span><span class="sxs-lookup"><span data-stu-id="b9786-111">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="b9786-112">Дополнительные сведения о тегах см. в статье [Маршрутизация и выражения тегов](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="b9786-112">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b9786-113">Проекты для Магазина Windows и проекты Windows Phone 8.1 и более ранней версии не поддерживаются в Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b9786-113">Windows Store and Windows Phone projects version 8.1 and earlier are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="b9786-114">Дополнительные сведения см. в статье [Целевая платформа и совместимость для Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="b9786-114">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b9786-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b9786-115">Prerequisites</span></span>
<span data-ttu-id="b9786-116">Материал данной статьи основан на приложении, созданном в разделе по [началу работы с центрами уведомлений][get-started].</span><span class="sxs-lookup"><span data-stu-id="b9786-116">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="b9786-117">Перед началом работы с данным руководством необходимо выполнить задания руководства по [началу работы с центрами уведомлений][get-started].</span><span class="sxs-lookup"><span data-stu-id="b9786-117">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="b9786-118">Добавление возможности выбора категорий в приложение</span><span class="sxs-lookup"><span data-stu-id="b9786-118">Add category selection to the app</span></span>
<span data-ttu-id="b9786-119">Прежде всего необходимо добавить элементы пользовательского интерфейса для имеющейся главной страницы, позволяющие пользователю выбирать категории для регистрации.</span><span class="sxs-lookup"><span data-stu-id="b9786-119">The first step is to add the UI elements to your existing main page that enable the user to select categories to register.</span></span> <span data-ttu-id="b9786-120">Выбранные пользователем категории хранятся на устройстве.</span><span class="sxs-lookup"><span data-stu-id="b9786-120">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="b9786-121">При запуске приложения в концентраторе уведомлений создается регистрация устройства с выбранными категориями, представленными в форме тегов.</span><span class="sxs-lookup"><span data-stu-id="b9786-121">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="b9786-122">Откройте файл проекта MainPage.xam и скопируйте следующий код в элемент **Grid** :</span><span class="sxs-lookup"><span data-stu-id="b9786-122">Open the MainPage.xaml project file, then copy the following code in the **Grid** element:</span></span>
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition/>
                <ColumnDefinition/>
            </Grid.ColumnDefinitions>
            <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"  TextWrapping="Wrap" Text="Breaking News" FontSize="42" VerticalAlignment="Top" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="World" Name="WorldToggle" Grid.Row="1" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Politics" Name="PoliticsToggle" Grid.Row="2" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Business" Name="BusinessToggle" Grid.Row="3" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Technology" Name="TechnologyToggle" Grid.Row="1" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Science" Name="ScienceToggle" Grid.Row="2" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Sports" Name="SportsToggle" Grid.Row="3" Grid.Column="1" HorizontalAlignment="Center"/>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="4" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click"/>
        </Grid>
2. <span data-ttu-id="b9786-123">Щелкните правой кнопкой мыши проект **Shared** и добавьте новый класс с именем **Notifications**, добавьте в определение класса модификатор **public**, а затем добавьте в новый файл кода следующие операторы **using**:</span><span class="sxs-lookup"><span data-stu-id="b9786-123">Right click the **Shared** project and add a new class named **Notifications**, add the **public** modifier to the class definition, then add the following **using** statements to the new code file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. <span data-ttu-id="b9786-124">Скопируйте следующий код в новый класс **Notifications** :</span><span class="sxs-lookup"><span data-stu-id="b9786-124">Copy the following code into the new **Notifications** class:</span></span>
   
        private NotificationHub hub;
   
        public Notifications(string hubName, string listenConnectionString)
        {
            hub = new NotificationHub(hubName, listenConnectionString);
        }
   
        public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
        {
            ApplicationData.Current.LocalSettings.Values["categories"] = string.Join(",", categories);
            return await SubscribeToCategories(categories);
        }
   
        public IEnumerable<string> RetrieveCategories()
        {
            var categories = (string) ApplicationData.Current.LocalSettings.Values["categories"];
            return categories != null ? categories.Split(','): new string[0];
        }
   
        public async Task<Registration> SubscribeToCategories(IEnumerable<string> categories = null)
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            if (categories == null)
            {
                categories = RetrieveCategories();
            }
   
            // Using a template registration to support notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyWNS = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "simpleWNSTemplateExample",
                    categories);
        }
   
    <span data-ttu-id="b9786-125">Этот класс использует локальное хранилище для хранения категорий новостей, которые данное устройство должно получать.</span><span class="sxs-lookup"><span data-stu-id="b9786-125">This class uses the local storage to store the categories of news that this device has to receive.</span></span> <span data-ttu-id="b9786-126">Обратите внимание, что вместо вызова метода *RegisterNativeAsync* мы вызываем метод *RegisterTemplateAsync* для регистрации в категориях с помощью шаблонной регистрации.</span><span class="sxs-lookup"><span data-stu-id="b9786-126">Note that instead of calling the *RegisterNativeAsync* method we call *RegisterTemplateAsync* to register for the categories using a template registration.</span></span> 
   
    <span data-ttu-id="b9786-127">Мы также предоставляем имя шаблона (simpleWNSTemplateExample), потому что нам может понадобиться зарегистрировать более одного шаблона (например, один для всплывающих уведомлений и один для элементов) и нам нужно назвать их, чтобы иметь возможность обновлять или удалять.</span><span class="sxs-lookup"><span data-stu-id="b9786-127">We also provide a name for the template ("simpleWNSTemplateExample"), because we might want to register more than one template (for instance one for toast notifications and one for tiles) and we need to name them in order to be able to update or delete them.</span></span>
   
    <span data-ttu-id="b9786-128">Обратите внимание, что если устройство регистрирует несколько шаблонов с тем же тегом, одно входящее сообщение для этого тега приведет к передаче нескольких уведомлений на устройство (по одному для каждого шаблона).</span><span class="sxs-lookup"><span data-stu-id="b9786-128">Note that if a device registers multiple templates with the same tag, an incoming message targeting that tag will result in multiple notifications delivered to the device (one for each template).</span></span> <span data-ttu-id="b9786-129">Это полезно, когда одного логическое сообщение должно привести к нескольким визуальным уведомлениям в приложении Магазина Windows, например в виде эмблемы и во всплывающем окне.</span><span class="sxs-lookup"><span data-stu-id="b9786-129">This behavior is useful when the same logical message has to result in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
   
    <span data-ttu-id="b9786-130">Подробнее о шаблонах см. в разделе [Шаблоны](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="b9786-130">For more information on templates, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>
4. <span data-ttu-id="b9786-131">В файле проекта App.xaml.cs добавьте следующее свойство к классу **App** :</span><span class="sxs-lookup"><span data-stu-id="b9786-131">In the App.xaml.cs project file, add the following property to the **App** class:</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    <span data-ttu-id="b9786-132">Это свойство используется для создания экземпляра **Notifications** и доступа к нему.</span><span class="sxs-lookup"><span data-stu-id="b9786-132">This property is used to create and access a **Notifications** instance.</span></span>
   
    <span data-ttu-id="b9786-133">В приведенном выше коде замените заполнители `<hub name>` и `<connection string with listen access>` именем центра уведомлений и строкой подключения для *DefaultListenSharedAccessSignature*, полученными ранее.</span><span class="sxs-lookup"><span data-stu-id="b9786-133">In the above code, replace the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b9786-134">Так как учетные данные, которые распространяются с помощью клиентского приложения, обычно небезопасны, с помощью вашего клиентского приложения следует распространять только ключ для доступа к прослушиванию.</span><span class="sxs-lookup"><span data-stu-id="b9786-134">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="b9786-135">Доступ к прослушиванию позволяет приложению регистрироваться для использования уведомлений, однако при этом нельзя изменять имеющиеся регистрации и отправлять уведомления.</span><span class="sxs-lookup"><span data-stu-id="b9786-135">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="b9786-136">Для отправки уведомлений и изменения существующих регистраций используется ключ полного доступа в защищенной серверной службе.</span><span class="sxs-lookup"><span data-stu-id="b9786-136">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
5. <span data-ttu-id="b9786-137">В MainPage.xaml.cs добавьте следующую строку:</span><span class="sxs-lookup"><span data-stu-id="b9786-137">In your MainPage.xaml.cs, add the following line:</span></span>
   
        using Windows.UI.Popups;
6. <span data-ttu-id="b9786-138">В файле проекта MainPage.xaml.cs добавьте следующий метод:</span><span class="sxs-lookup"><span data-stu-id="b9786-138">In the MainPage.xaml.cs project file, add the following method:</span></span>
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
            var categories = new HashSet<string>();
            if (WorldToggle.IsOn) categories.Add("World");
            if (PoliticsToggle.IsOn) categories.Add("Politics");
            if (BusinessToggle.IsOn) categories.Add("Business");
            if (TechnologyToggle.IsOn) categories.Add("Technology");
            if (ScienceToggle.IsOn) categories.Add("Science");
            if (SportsToggle.IsOn) categories.Add("Sports");
   
            var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);
   
            var dialog = new MessageDialog("Subscribed to: " + string.Join(",", categories) + " on registration Id: " + result.RegistrationId);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
   
    <span data-ttu-id="b9786-139">Этот метод создает список категорий и использует класс **Notifications** класс для хранения списка в локальном хранилище и регистрации соответствующих тегов в концентраторе уведомлений.</span><span class="sxs-lookup"><span data-stu-id="b9786-139">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="b9786-140">При изменении категорий регистрация создается заново с новыми категориями.</span><span class="sxs-lookup"><span data-stu-id="b9786-140">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="b9786-141">Ваше приложение теперь может сохранять набор категорий в локальном хранилище на устройстве и регистрироваться в центре уведомлений всякий раз, когда пользователь изменяет выбранные категории.</span><span class="sxs-lookup"><span data-stu-id="b9786-141">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="b9786-142">Регистрация для использования уведомлений</span><span class="sxs-lookup"><span data-stu-id="b9786-142">Register for notifications</span></span>
<span data-ttu-id="b9786-143">Эти действия позволяют зарегистрироваться в центре уведомлений при запуске с использованием категорий, сохраненных в локальном хранилище.</span><span class="sxs-lookup"><span data-stu-id="b9786-143">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="b9786-144">Так как универсальный код ресурса (URI) канала, назначенный службой push-уведомлений Windows (MPNS), может измениться в любое время, следует регулярно производить регистрацию для использования уведомлений, чтобы предотвратить сбои уведомлений.</span><span class="sxs-lookup"><span data-stu-id="b9786-144">Because the channel URI assigned by the Windows Notification Service (WNS) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="b9786-145">В этом примере регистрация для использования уведомлений осуществляется при каждом запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="b9786-145">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="b9786-146">Для тех приложений, которые запускаются часто, более одного раза в день, возможно, лучше пропустить регистрацию, чтобы сэкономить трафик, если с момента прошлой регистрации прошло меньше суток.</span><span class="sxs-lookup"><span data-stu-id="b9786-146">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="b9786-147">Откройте файл App.xaml.cs и обновите метод **InitNotificationsAsync**, чтобы использовать класс `notifications` для подписки по категориям.</span><span class="sxs-lookup"><span data-stu-id="b9786-147">Open the App.xaml.cs file and update the **InitNotificationsAsync** method to use the `notifications` class to subscribe based on categories.</span></span>
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    <span data-ttu-id="b9786-148">Это гарантирует, что при каждом запуске приложения оно извлекает категории из локального хранилища и запрашивает для них регистрацию.</span><span class="sxs-lookup"><span data-stu-id="b9786-148">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registeration for these categories.</span></span> <span data-ttu-id="b9786-149">Метод **InitNotificationsAsync** был создан в ходе изучения руководства [по началу работы с центрами уведомлений][get-started].</span><span class="sxs-lookup"><span data-stu-id="b9786-149">The **InitNotificationsAsync** method was created as part of the [Get started with Notification Hubs][get-started] tutorial.</span></span>
2. <span data-ttu-id="b9786-150">В файле проекта MainPage.xaml.cs добавьте следующий код в метод *OnNavigatedTo* :</span><span class="sxs-lookup"><span data-stu-id="b9786-150">In the MainPage.xaml.cs project file, add the following code to the *OnNavigatedTo* method:</span></span>
   
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            var categories = ((App)Application.Current).notifications.RetrieveCategories();
   
            if (categories.Contains("World")) WorldToggle.IsOn = true;
            if (categories.Contains("Politics")) PoliticsToggle.IsOn = true;
            if (categories.Contains("Business")) BusinessToggle.IsOn = true;
            if (categories.Contains("Technology")) TechnologyToggle.IsOn = true;
            if (categories.Contains("Science")) ScienceToggle.IsOn = true;
            if (categories.Contains("Sports")) SportsToggle.IsOn = true;
        }
   
    <span data-ttu-id="b9786-151">При этом главная страница обновляется в зависимости от состояния ранее сохраненных категорий.</span><span class="sxs-lookup"><span data-stu-id="b9786-151">This updates the main page based on the status of previously saved categories.</span></span>

<span data-ttu-id="b9786-152">Теперь приложение готово и может сохранять набор категорий в локальном хранилище устройств и использовать его для регистрации в концентраторе уведомлений всякий раз, когда пользователь изменяет выбранные категории.</span><span class="sxs-lookup"><span data-stu-id="b9786-152">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="b9786-153">А сейчас определим серверную часть, которая может отправлять уведомления категорий в это приложение.</span><span class="sxs-lookup"><span data-stu-id="b9786-153">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="b9786-154">Отправка уведомлений с тегами</span><span class="sxs-lookup"><span data-stu-id="b9786-154">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="b9786-155">Запуск приложения и создание уведомлений</span><span class="sxs-lookup"><span data-stu-id="b9786-155">Run the app and generate notifications</span></span>
1. <span data-ttu-id="b9786-156">В Visual Studio нажмите клавишу F5, чтобы скомпилировать и запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b9786-156">In Visual Studio, press F5 to compile and start the app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="b9786-157">Обратите внимание, что в пользовательском интерфейсе присутствует набор переключателей, позволяющий выбрать категории для подписки.</span><span class="sxs-lookup"><span data-stu-id="b9786-157">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="b9786-158">Включите переключатели одной или нескольких категорий, затем нажмите **Подписаться**.</span><span class="sxs-lookup"><span data-stu-id="b9786-158">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="b9786-159">Приложение преобразует выбранные категории в теги и запрашивает у концентратора уведомлений новую регистрацию устройств для выбранных тегов.</span><span class="sxs-lookup"><span data-stu-id="b9786-159">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="b9786-160">Зарегистрированные категории возвращаются и отображаются в диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="b9786-160">The registered categories are returned and displayed in a dialog.</span></span>
   
    ![][19]
3. <span data-ttu-id="b9786-161">Отправьте новое уведомление из серверной части одним из следующих способов:</span><span class="sxs-lookup"><span data-stu-id="b9786-161">Send a new notification from the backend in one of the following ways:</span></span>
   
   * <span data-ttu-id="b9786-162">**Консольное приложение:** запустите консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="b9786-162">**Console app:** start the console app.</span></span>
   * <span data-ttu-id="b9786-163">**Java/PHP:** запустите приложение или сценарий.</span><span class="sxs-lookup"><span data-stu-id="b9786-163">**Java/PHP:** run your app/script.</span></span>
     
     <span data-ttu-id="b9786-164">Уведомления для выбранных категорий отображаются в виде всплывающих уведомлений.</span><span class="sxs-lookup"><span data-stu-id="b9786-164">Notifications for the selected categories appear as toast notifications.</span></span>
     
     ![][14]

## <a name="next-steps"></a><span data-ttu-id="b9786-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b9786-165">Next steps</span></span>
<span data-ttu-id="b9786-166">В этом учебнике мы рассмотрели, как производить рассылку экстренных новостей по категориям.</span><span class="sxs-lookup"><span data-stu-id="b9786-166">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="b9786-167">Далее вам рекомендуется изучить один из следующих учебников, в которых рассматриваются более сложные сценарии использования концентраторов уведомлений:</span><span class="sxs-lookup"><span data-stu-id="b9786-167">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="b9786-168">[Использование центров уведомлений для передачи локализованных экстренных новостей]</span><span class="sxs-lookup"><span data-stu-id="b9786-168">[Use Notification Hubs to broadcast localized breaking news]</span></span>
  
    <span data-ttu-id="b9786-169">Как расширить возможности приложения экстренных новостей для отправки локализованных уведомлений.</span><span class="sxs-lookup"><span data-stu-id="b9786-169">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Anchors. -->
[Add category selection to the app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run the app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-breakingnews-win1.png

[14]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-toast-2.png


[19]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-reg-2.png

<!-- URLs.-->
[get-started]: /manage/services/notification-hubs/getting-started-windows-dotnet/
<span data-ttu-id="b9786-170">[Использование центров уведомлений для передачи локализованных экстренных новостей]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span><span class="sxs-lookup"><span data-stu-id="b9786-170">[Use Notification Hubs to broadcast localized breaking news]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span></span>
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
