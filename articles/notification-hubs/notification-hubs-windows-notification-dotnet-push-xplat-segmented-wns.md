---
title: "Концентраторы уведомлений toosend aaaUse, новости (универсальное приложение для Windows)"
description: "Использование концентраторов уведомлений Azure с тегами в toosend регистрации hello критические новостей tooa универсального приложения Windows."
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
ms.openlocfilehash: f102d286d2c7bd387fcfa2c7eab2ba31a0298517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="3f5d5-103">Использование концентраторов уведомлений toosend новости</span><span class="sxs-lookup"><span data-stu-id="3f5d5-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="3f5d5-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="3f5d5-104">Overview</span></span>
<span data-ttu-id="3f5d5-105">В этом разделе показано, как toobroadcast концентраторов уведомлений Azure toouse критические новостей уведомления tooa магазина Windows или приложения Windows Phone 8.1 (отличных от Silverlight).</span><span class="sxs-lookup"><span data-stu-id="3f5d5-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooa Windows Store or Windows Phone 8.1 (non-Silverlight) app.</span></span> <span data-ttu-id="3f5d5-106">Если вы используете Windows Phone 8.1 Silverlight, можно найти toohello [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) версии.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-106">If you are targeting Windows Phone 8.1 Silverlight, please refer toohello [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) version.</span></span> <span data-ttu-id="3f5d5-107">После завершения будет быть может tooregister переноса категории новостей нужных вам и получения только push-уведомлений для этих категорий.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-107">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="3f5d5-108">Этот сценарий представлен общий шаблон для многих приложений, где уведомления состоят из отправленных toobe toogroups пользователей, которым был объявлен ранее интерес в них, например средство чтения RSS, приложений для вентиляторов музыки и т. д.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-108">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, and so on.</span></span> 

<span data-ttu-id="3f5d5-109">Широковещательный сценарии реализуются путем включения одного или нескольких *теги* при создании регистрации в концентраторе уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="3f5d5-110">Отправке уведомлений tooa тегов, все устройства, которые зарегистрированы для тега hello получат уведомление hello.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-110">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="3f5d5-111">Так как теги являются просто строками, у которых нет toobe заранее подготовлены.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-111">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="3f5d5-112">Дополнительные сведения о тегах см. в разделе слишком[маршрутизации концентраторов уведомлений и выражения с тегами](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="3f5d5-112">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3f5d5-113">Проекты для Магазина Windows и проекты Windows Phone 8.1 и более ранней версии не поддерживаются в Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-113">Windows Store and Windows Phone projects version 8.1 and earlier are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="3f5d5-114">Дополнительные сведения см. в статье [Целевая платформа и совместимость для Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="3f5d5-114">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3f5d5-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3f5d5-115">Prerequisites</span></span>
<span data-ttu-id="3f5d5-116">В этом разделе основан на приложение hello, созданный в [приступить к работе с концентраторами уведомлений][get-started].</span><span class="sxs-lookup"><span data-stu-id="3f5d5-116">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="3f5d5-117">Перед началом работы с данным руководством необходимо выполнить задания руководства по [началу работы с центрами уведомлений][get-started].</span><span class="sxs-lookup"><span data-stu-id="3f5d5-117">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="3f5d5-118">Добавить приложение toohello Выбор категории</span><span class="sxs-lookup"><span data-stu-id="3f5d5-118">Add category selection toohello app</span></span>
<span data-ttu-id="3f5d5-119">Hello первым шагом является tooadd hello пользовательского интерфейса элементы tooyour существующей главной страницы, включить tooregister категории tooselect пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-119">hello first step is tooadd hello UI elements tooyour existing main page that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="3f5d5-120">выбранные пользователем категории Hello хранятся на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-120">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="3f5d5-121">При запуске приложение hello регистрацию устройств создается в концентратор уведомлений с категориями hello выбран как теги.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-121">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="3f5d5-122">Откройте файл проекта MainPage.xaml hello, а затем копировать hello, следующий код в hello **сетки** элемента:</span><span class="sxs-lookup"><span data-stu-id="3f5d5-122">Open hello MainPage.xaml project file, then copy hello following code in hello **Grid** element:</span></span>
   
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
2. <span data-ttu-id="3f5d5-123">Щелкните правой кнопкой мыши hello **Shared** проекта и добавьте новый класс с именем **уведомления**, добавить hello **открытый** toohello модификатор определения класса, а затем добавьте следующие hello **с помощью** инструкций toohello новый файл кода:</span><span class="sxs-lookup"><span data-stu-id="3f5d5-123">Right click hello **Shared** project and add a new class named **Notifications**, add hello **public** modifier toohello class definition, then add hello following **using** statements toohello new code file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. <span data-ttu-id="3f5d5-124">Копирования hello следующий код в новый hello **уведомления** класса:</span><span class="sxs-lookup"><span data-stu-id="3f5d5-124">Copy hello following code into hello new **Notifications** class:</span></span>
   
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
   
            // Using a template registration toosupport notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyWNS = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "simpleWNSTemplateExample",
                    categories);
        }
   
    <span data-ttu-id="3f5d5-125">Этот класс использует локальное хранилище hello toostore категории hello новостей, что это устройство имеет tooreceive.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-125">This class uses hello local storage toostore hello categories of news that this device has tooreceive.</span></span> <span data-ttu-id="3f5d5-126">Обратите внимание, что вместо вызывающему Привет *RegisterNativeAsync* вызываем метод *RegisterTemplateAsync* tooregister для категории hello, с помощью регистрацию шаблона.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-126">Note that instead of calling hello *RegisterNativeAsync* method we call *RegisterTemplateAsync* tooregister for hello categories using a template registration.</span></span> 
   
    <span data-ttu-id="3f5d5-127">Мы также предоставляем имя шаблона hello («simpleWNSTemplateExample»), так как может потребоваться tooregister более одного шаблона (например один всплывающих уведомлений) и один для плиток, а нам нужно tooname их в порядке может tooupdate toobe или удалить их.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-127">We also provide a name for hello template ("simpleWNSTemplateExample"), because we might want tooregister more than one template (for instance one for toast notifications and one for tiles) and we need tooname them in order toobe able tooupdate or delete them.</span></span>
   
    <span data-ttu-id="3f5d5-128">Обратите внимание, если несколько шаблонов регистрации устройства с таким же тегом при входящего сообщения, предназначенные для тега приведет hello несколько уведомлений доставлено toohello устройства (по одному для каждого шаблона).</span><span class="sxs-lookup"><span data-stu-id="3f5d5-128">Note that if a device registers multiple templates with hello same tag, an incoming message targeting that tag will result in multiple notifications delivered toohello device (one for each template).</span></span> <span data-ttu-id="3f5d5-129">Это полезно, если hello одного логического сообщения tooresult в нескольких visual уведомлений, например отображение эмблемы и всплывающие в приложения для магазина Windows.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-129">This behavior is useful when hello same logical message has tooresult in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
   
    <span data-ttu-id="3f5d5-130">Подробнее о шаблонах см. в разделе [Шаблоны](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="3f5d5-130">For more information on templates, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>
4. <span data-ttu-id="3f5d5-131">Добавьте в файл проекта App.xaml.cs hello hello следующие свойства toohello **приложения** класса:</span><span class="sxs-lookup"><span data-stu-id="3f5d5-131">In hello App.xaml.cs project file, add hello following property toohello **App** class:</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    <span data-ttu-id="3f5d5-132">Это свойство является используется toocreate и доступа **уведомления** экземпляра.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-132">This property is used toocreate and access a **Notifications** instance.</span></span>
   
    <span data-ttu-id="3f5d5-133">В hello над кодом, замените hello `<hub name>` и `<connection string with listen access>` местозаполнителей уведомления имя и hello строку подключения к концентратору для *DefaultListenSharedAccessSignature* , полученный ранее.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-133">In hello above code, replace hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3f5d5-134">Так как учетные данные, которые распространяются с помощью клиентского приложения, обычно не безопасны, hello ключ для прослушивания доступа следует распространять только с помощью клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-134">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="3f5d5-135">Прослушивать доступа включает tooregister вашего приложения для уведомлений, но существующие регистрации нельзя изменить, и не может отправлять уведомления.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-135">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="3f5d5-136">Полный доступ Hello используется в защищенной серверной службе для отправки уведомлений и изменять существующие регистрации.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-136">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
5. <span data-ttu-id="3f5d5-137">Добавьте в ваш MainPage.xaml.cs hello, следующей строкой.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-137">In your MainPage.xaml.cs, add hello following line:</span></span>
   
        using Windows.UI.Popups;
6. <span data-ttu-id="3f5d5-138">В файле проекта MainPage.xaml.cs hello добавьте следующий метод hello:</span><span class="sxs-lookup"><span data-stu-id="3f5d5-138">In hello MainPage.xaml.cs project file, add hello following method:</span></span>
   
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
   
    <span data-ttu-id="3f5d5-139">Этот метод создает список категорий и использует hello **уведомления** класса toostore список hello в локальном хранилище hello и зарегистрируйте hello соответствующие теги в концентраторе уведомлений.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-139">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="3f5d5-140">При изменении категории регистрации hello воссоздается при hello новые категории.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-140">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="3f5d5-141">Приложение теперь может toostore набор категорий в локальном хранилище на устройстве hello и зарегистрировать с концентратором уведомлений hello всякий раз, когда изменения пользователя hello hello выбора категорий.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-141">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="3f5d5-142">Регистрация для использования уведомлений</span><span class="sxs-lookup"><span data-stu-id="3f5d5-142">Register for notifications</span></span>
<span data-ttu-id="3f5d5-143">Эти шаги зарегистрировать hello концентратора уведомлений при запуске с помощью категорий hello, хранящихся в локальном хранилище.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-143">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="3f5d5-144">URI, присвоенный hello Windows Notification Service (WNS) hello канала может меняться в любое время, следует зарегистрировать для получения уведомлений часто tooavoid сбоев уведомлений.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-144">Because hello channel URI assigned by hello Windows Notification Service (WNS) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="3f5d5-145">В этом примере регистрируется для уведомления каждый раз при запуске этого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-145">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="3f5d5-146">Для приложений, которые часто выполняются более чем один раз в день, возможно, если можно пропустить пропускной способности toopreserve регистрации менее чем за день прошел с момента предыдущей регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-146">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="3f5d5-147">App.xaml.cs Привет открыть файл и обновление hello **InitNotificationsAsync** hello toouse метод `notifications` toosubscribe класс на основе категорий.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-147">Open hello App.xaml.cs file and update hello **InitNotificationsAsync** method toouse hello `notifications` class toosubscribe based on categories.</span></span>
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    <span data-ttu-id="3f5d5-148">Это гарантирует, что каждый раз при запуске приложение hello он получает hello категорий из локального хранилища и запросов регистрации для следующих категорий.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-148">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registeration for these categories.</span></span> <span data-ttu-id="3f5d5-149">Hello **InitNotificationsAsync** метод был создан как часть hello [приступить к работе с концентраторами уведомлений] [ get-started] учебника.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-149">hello **InitNotificationsAsync** method was created as part of hello [Get started with Notification Hubs][get-started] tutorial.</span></span>
2. <span data-ttu-id="3f5d5-150">Добавьте в файл проекта MainPage.xaml.cs hello hello, следующий код toohello *OnNavigatedTo* метод:</span><span class="sxs-lookup"><span data-stu-id="3f5d5-150">In hello MainPage.xaml.cs project file, add hello following code toohello *OnNavigatedTo* method:</span></span>
   
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
   
    <span data-ttu-id="3f5d5-151">Этого обновления hello главной страницы на основе состояния hello ранее сохраненные категорий.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-151">This updates hello main page based on hello status of previously saved categories.</span></span>

<span data-ttu-id="3f5d5-152">приложение Hello завершен, можно сохранить набор категорий в hello tooregister локального хранилища используется устройством с концентратором уведомлений hello всякий раз, когда изменения пользователя hello hello выбора категорий.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-152">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="3f5d5-153">Затем мы определим серверной части, можно отправить приложение toothis категории уведомлений.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-153">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="3f5d5-154">Отправка уведомлений с тегами</span><span class="sxs-lookup"><span data-stu-id="3f5d5-154">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="3f5d5-155">Запустите приложение hello и создавать уведомления</span><span class="sxs-lookup"><span data-stu-id="3f5d5-155">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="3f5d5-156">В Visual Studio нажмите клавишу F5 toocompile и запустить приложение hello.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-156">In Visual Studio, press F5 toocompile and start hello app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="3f5d5-157">Обратите внимание, что приложение hello пользовательского интерфейса предоставляет набор переключает, позволяет выбрать toosubscribe hello категорий для.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-157">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="3f5d5-158">Включите переключатели одной или нескольких категорий, затем нажмите **Подписаться**.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-158">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="3f5d5-159">приложение Hello преобразует hello выбранной категории в теги и запрашивает новую регистрацию устройств для hello выбранных тегов из концентратора уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-159">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="3f5d5-160">Hello зарегистрированных категорий возвращается и отображается в диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-160">hello registered categories are returned and displayed in a dialog.</span></span>
   
    ![][19]
3. <span data-ttu-id="3f5d5-161">Отправьте новое уведомление с сервера hello в одном из следующих способов hello:</span><span class="sxs-lookup"><span data-stu-id="3f5d5-161">Send a new notification from hello backend in one of hello following ways:</span></span>
   
   * <span data-ttu-id="3f5d5-162">**Консольное приложение:** запустить консольное приложение hello.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-162">**Console app:** start hello console app.</span></span>
   * <span data-ttu-id="3f5d5-163">**Java/PHP:** запустите приложение или сценарий.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-163">**Java/PHP:** run your app/script.</span></span>
     
     <span data-ttu-id="3f5d5-164">Уведомления для hello выбранной категории отображаются в виде всплывающих уведомлений.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-164">Notifications for hello selected categories appear as toast notifications.</span></span>
     
     ![][14]

## <a name="next-steps"></a><span data-ttu-id="3f5d5-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3f5d5-165">Next steps</span></span>
<span data-ttu-id="3f5d5-166">В этом учебнике мы узнали, каким образом toobroadcast новости по категориям.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-166">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="3f5d5-167">Рассмотрим, выполнив одну из hello следующие учебники, выделите других расширенных сценариях концентраторов уведомлений.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-167">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="3f5d5-168">[Использовать локализованные toobroadcast новости концентраторы уведомлений]</span><span class="sxs-lookup"><span data-stu-id="3f5d5-168">[Use Notification Hubs toobroadcast localized breaking news]</span></span>
  
    <span data-ttu-id="3f5d5-169">Узнайте, как критические отправки tooenable новостей приложения hello tooexpand локализованные уведомления.</span><span class="sxs-lookup"><span data-stu-id="3f5d5-169">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

<!-- Anchors. -->
[Add category selection toohello app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run hello app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-breakingnews-win1.png

[14]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-toast-2.png


[19]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-reg-2.png

<!-- URLs.-->
[get-started]: /manage/services/notification-hubs/getting-started-windows-dotnet/
[Использовать локализованные toobroadcast новости концентраторы уведомлений]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
