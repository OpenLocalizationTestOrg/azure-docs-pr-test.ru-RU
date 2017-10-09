---
title: "aaaNotification концентраторов локализованные критические новостей учебника"
description: "Узнайте, как toosend toouse концентраторов уведомлений Azure локализованные уведомлений с последними новостями."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: c454f5a3-a06b-45ac-91c7-f91210889b25
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: d273a6b384df311dea7b76ca83ccd94d9a989c4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news"></a><span data-ttu-id="3aa8f-103">Использовать локализованные toosend новости концентраторы уведомлений</span><span class="sxs-lookup"><span data-stu-id="3aa8f-103">Use Notification Hubs toosend localized breaking news</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3aa8f-104">C# в Магазине Windows</span><span class="sxs-lookup"><span data-stu-id="3aa8f-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="3aa8f-105">iOS</span><span class="sxs-lookup"><span data-stu-id="3aa8f-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="3aa8f-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="3aa8f-106">Overview</span></span>
<span data-ttu-id="3aa8f-107">В этом разделе показано, как toouse hello **шаблона** функции концентраторов уведомлений Azure toobroadcast критические уведомления новостей, локализованные языка и устройства.</span><span class="sxs-lookup"><span data-stu-id="3aa8f-107">This topic shows you how toouse hello **template** feature of Azure Notification Hubs toobroadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="3aa8f-108">В этом учебнике, запуск приложения магазина Windows hello, созданные в [toosend использования концентраторов уведомлений, новости].</span><span class="sxs-lookup"><span data-stu-id="3aa8f-108">In this tutorial you start with hello Windows Store app created in [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="3aa8f-109">После завершения можно будет tooregister для категорий, которые вас интересуют, указать язык в уведомления, которое tooreceive hello и получать только push-уведомлений для hello выбранных категорий на этом языке.</span><span class="sxs-lookup"><span data-stu-id="3aa8f-109">When complete, you will be able tooregister for categories you are interested in, specify a language in which tooreceive hello notifications, and receive only push notifications for hello selected categories in that language.</span></span>

<span data-ttu-id="3aa8f-110">Существует два сценария toothis частей:</span><span class="sxs-lookup"><span data-stu-id="3aa8f-110">There are two parts toothis scenario:</span></span>

* <span data-ttu-id="3aa8f-111">приложения для магазина Windows Hello позволяет клиентским устройств toospecify язык и toodifferent toosubscribe критические категории новостей;</span><span class="sxs-lookup"><span data-stu-id="3aa8f-111">hello Windows Store app allows client devices toospecify a language, and toosubscribe toodifferent breaking news categories;</span></span>
* <span data-ttu-id="3aa8f-112">Hello внутренней осуществляет широковещательную рассылку уведомлений hello, с использованием hello **тега** и **шаблона** поддержки концентраторов уведомлений Azure.</span><span class="sxs-lookup"><span data-stu-id="3aa8f-112">hello back-end broadcasts hello notifications, using hello **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3aa8f-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3aa8f-113">Prerequisites</span></span>
<span data-ttu-id="3aa8f-114">Вы должны уже выполнили hello [toosend использования концентраторов уведомлений, новости] учебника и иметь hello кода, так как этот учебник построен непосредственно на этот код.</span><span class="sxs-lookup"><span data-stu-id="3aa8f-114">You must have already completed hello [Use Notification Hubs toosend breaking news] tutorial and have hello code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="3aa8f-115">Также требуется Visual Studio 2012 или более поздняя версия.</span><span class="sxs-lookup"><span data-stu-id="3aa8f-115">You also need Visual Studio 2012 or later.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="3aa8f-116">Основные сведения о шаблонах</span><span class="sxs-lookup"><span data-stu-id="3aa8f-116">Template concepts</span></span>
<span data-ttu-id="3aa8f-117">В [toosend использования концентраторов уведомлений, новости] построении приложения, которое используется **теги** toonotifications toosubscribe новостей разных категорий.</span><span class="sxs-lookup"><span data-stu-id="3aa8f-117">In [Use Notification Hubs toosend breaking news] you built an app that used **tags** toosubscribe toonotifications for different news categories.</span></span>
<span data-ttu-id="3aa8f-118">Однако многие приложения ориентированы на несколько рынков и требуют локализации.</span><span class="sxs-lookup"><span data-stu-id="3aa8f-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="3aa8f-119">Таким образом, содержимое hello hello уведомлений, сами имеют toobe локализованные доставленный toohello правильным набором устройств.</span><span class="sxs-lookup"><span data-stu-id="3aa8f-119">This means that hello content of hello notifications themselves have toobe localized and delivered toohello correct set of devices.</span></span>
<span data-ttu-id="3aa8f-120">В этом разделе будет показано, как toouse hello **шаблона** функции концентраторов уведомлений tooeasily доставки локализованное уведомлений с последними новостями.</span><span class="sxs-lookup"><span data-stu-id="3aa8f-120">In this topic we will show how toouse hello **template** feature of Notification Hubs tooeasily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="3aa8f-121">Примечание: один из способов toosend локализованные уведомления является toocreate нескольких версий каждого тега.</span><span class="sxs-lookup"><span data-stu-id="3aa8f-121">Note: one way toosend localized notifications is toocreate multiple versions of each tag.</span></span> <span data-ttu-id="3aa8f-122">Для экземпляра toosupport английском, французском и мандаринский, пришлось бы иметь три разные теги Мировые: «world_en», «world_fr» и «world_ch».</span><span class="sxs-lookup"><span data-stu-id="3aa8f-122">For instance, toosupport English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="3aa8f-123">Мы будет иметь toosend локализованной версии tooeach новостей hello world эти теги.</span><span class="sxs-lookup"><span data-stu-id="3aa8f-123">We would then have toosend a localized version of hello world news tooeach of these tags.</span></span> <span data-ttu-id="3aa8f-124">В этом разделе используются шаблоны tooavoid hello увеличением числа теги и требование hello отправка нескольких сообщений.</span><span class="sxs-lookup"><span data-stu-id="3aa8f-124">In this topic we use templates tooavoid hello proliferation of tags and hello requirement of sending multiple messages.</span></span>

<span data-ttu-id="3aa8f-125">На высоком уровне шаблоны являются toospecify способом как конкретного устройства следует получать такие уведомления.</span><span class="sxs-lookup"><span data-stu-id="3aa8f-125">At a high level, templates are a way toospecify how a specific device should receive a notification.</span></span> <span data-ttu-id="3aa8f-126">шаблон Hello указывает формат hello точное полезных данных с помощью ссылки tooproperties, которые являются частью приветственное сообщение, отправленное приложение в серверной части.</span><span class="sxs-lookup"><span data-stu-id="3aa8f-126">hello template specifies hello exact payload format by referring tooproperties that are part of hello message sent by your app back-end.</span></span> <span data-ttu-id="3aa8f-127">В нашем случае мы отправим независимое от языка сообщение, которое содержит все поддерживаемые языки:</span><span class="sxs-lookup"><span data-stu-id="3aa8f-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="3aa8f-128">Затем мы гарантируем, что устройства регистрацию с шаблоном, который ссылается свойство правильный toohello.</span><span class="sxs-lookup"><span data-stu-id="3aa8f-128">Then we will ensure that devices register with a template that refers toohello correct property.</span></span> <span data-ttu-id="3aa8f-129">Для экземпляра приложения для магазина Windows, в которой необходимо tooreceive сообщение простое всплывающее уведомление будет зарегистрирован для hello следующий шаблон с любой соответствующие теги:</span><span class="sxs-lookup"><span data-stu-id="3aa8f-129">For instance, a Windows Store app that wants tooreceive a simple toast message will register for hello following template with any corresponding tags:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



<span data-ttu-id="3aa8f-130">Шаблоны — это очень мощная функция, о них можно узнать больше в нашей статье [Шаблоны](notification-hubs-templates-cross-platform-push-messages.md) .</span><span class="sxs-lookup"><span data-stu-id="3aa8f-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span> 

## <a name="hello-app-user-interface"></a><span data-ttu-id="3aa8f-131">пользовательский интерфейс приложения Hello</span><span class="sxs-lookup"><span data-stu-id="3aa8f-131">hello app user interface</span></span>
<span data-ttu-id="3aa8f-132">Теперь мы изменит приложение hello последние новости, созданный в разделе hello [toosend использования концентраторов уведомлений, новости] toosend локализованные новости, с помощью шаблонов.</span><span class="sxs-lookup"><span data-stu-id="3aa8f-132">We will now modify hello Breaking News app that you created in hello topic [Use Notification Hubs toosend breaking news] toosend localized breaking news using templates.</span></span>

<span data-ttu-id="3aa8f-133">В приложении Магазина Windows:</span><span class="sxs-lookup"><span data-stu-id="3aa8f-133">In your Windows Store app:</span></span>

<span data-ttu-id="3aa8f-134">Изменение вашей MainPage.xaml tooinclude combobox языкового стандарта.</span><span class="sxs-lookup"><span data-stu-id="3aa8f-134">Change your MainPage.xaml tooinclude a locale combobox:</span></span>

    <Grid Margin="120, 58, 120, 80"  
            Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
        <Grid.RowDefinitions>
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
            <ColumnDefinition />
            <ColumnDefinition />
        </Grid.ColumnDefinitions>
        <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"  TextWrapping="Wrap" Text="Breaking News" FontSize="42" VerticalAlignment="Top"/>
        <ComboBox Name="Locale" HorizontalAlignment="Left" VerticalAlignment="Center" Width="200" Grid.Row="1" Grid.Column="0">
            <x:String>English</x:String>
            <x:String>French</x:String>
            <x:String>Mandarin</x:String>
        </ComboBox>
        <ToggleSwitch Header="World" Name="WorldToggle" Grid.Row="2" Grid.Column="0"/>
        <ToggleSwitch Header="Politics" Name="PoliticsToggle" Grid.Row="3" Grid.Column="0"/>
        <ToggleSwitch Header="Business" Name="BusinessToggle" Grid.Row="4" Grid.Column="0"/>
        <ToggleSwitch Header="Technology" Name="TechnologyToggle" Grid.Row="2" Grid.Column="1"/>
        <ToggleSwitch Header="Science" Name="ScienceToggle" Grid.Row="3" Grid.Column="1"/>
        <ToggleSwitch Header="Sports" Name="SportsToggle" Grid.Row="4" Grid.Column="1"/>
        <Button Content="Subscribe" HorizontalAlignment="Center" Grid.Row="5" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click" />
    </Grid>

## <a name="building-hello-windows-store-client-app"></a><span data-ttu-id="3aa8f-135">Построение клиентского приложения для магазина Windows hello</span><span class="sxs-lookup"><span data-stu-id="3aa8f-135">Building hello Windows Store client app</span></span>
1. <span data-ttu-id="3aa8f-136">В классе уведомления, добавьте параметр языкового стандарта tooyour *StoreCategoriesAndSubscribe* и *SubscribeToCateories* методы.</span><span class="sxs-lookup"><span data-stu-id="3aa8f-136">In your Notifications class, add a locale parameter tooyour  *StoreCategoriesAndSubscribe* and *SubscribeToCateories* methods.</span></span>
   
        public async Task<Registration> StoreCategoriesAndSubscribe(string locale, IEnumerable<string> categories)
        {
            ApplicationData.Current.LocalSettings.Values["categories"] = string.Join(",", categories);
            ApplicationData.Current.LocalSettings.Values["locale"] = locale;
            return await SubscribeToCategories(categories);
        }
   
        public async Task<Registration> SubscribeToCategories(string locale, IEnumerable<string> categories = null)
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            if (categories == null)
            {
                categories = RetrieveCategories();
            }
   
            // Using a template registration. This makes supporting notifications across other platforms much easier.
            // Using hello localized tags based on locale selected.
            string templateBodyWNS = String.Format("<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(News_{0})</text></binding></visual></toast>", locale);
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "localizedWNSTemplateExample", categories);
        }
   
    <span data-ttu-id="3aa8f-137">Обратите внимание, что вместо вызывающему Привет *RegisterNativeAsync* вызываем метод *RegisterTemplateAsync*: мы регистрации уведомлений формат, в которых hello шаблона зависит от языкового стандарта hello.</span><span class="sxs-lookup"><span data-stu-id="3aa8f-137">Note that instead of calling hello *RegisterNativeAsync* method we call *RegisterTemplateAsync*: we are registering a specific notification format in which hello template depends on hello locale.</span></span> <span data-ttu-id="3aa8f-138">Мы также предоставляем имя шаблона hello («localizedWNSTemplateExample»), так как может потребоваться tooregister более одного шаблона (например один всплывающих уведомлений) и один для плиток, а нам нужно tooname их в порядке может tooupdate toobe или удалить их.</span><span class="sxs-lookup"><span data-stu-id="3aa8f-138">We also provide a name for hello template ("localizedWNSTemplateExample"), because we might want tooregister more than one template (for instance one for toast notifications and one for tiles) and we need tooname them in order toobe able tooupdate or delete them.</span></span>
   
    <span data-ttu-id="3aa8f-139">Обратите внимание, если несколько шаблонов регистрации устройства с таким же тегом при входящего сообщения, предназначенные для тега приведет hello несколько уведомлений доставлено toohello устройства (по одному для каждого шаблона).</span><span class="sxs-lookup"><span data-stu-id="3aa8f-139">Note that if a device registers multiple templates with hello same tag, an incoming message targeting that tag will result in multiple notifications delivered toohello device (one for each template).</span></span> <span data-ttu-id="3aa8f-140">Это полезно, если hello одного логического сообщения tooresult в нескольких visual уведомлений, например отображение эмблемы и всплывающие в приложения для магазина Windows.</span><span class="sxs-lookup"><span data-stu-id="3aa8f-140">This behavior is useful when hello same logical message has tooresult in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
2. <span data-ttu-id="3aa8f-141">Добавьте следующие сохраненного языкового стандарта hello tooretrieve метод hello:</span><span class="sxs-lookup"><span data-stu-id="3aa8f-141">Add hello following method tooretrieve hello stored locale:</span></span>
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. <span data-ttu-id="3aa8f-142">В вашей MainPage.xaml.cs вашей кнопка обновления нажмите кнопку обработчика, извлекая hello текущее значение поля со списком hello языкового стандарта и передавая ему класс уведомления toohello toohello вызова, как показано:</span><span class="sxs-lookup"><span data-stu-id="3aa8f-142">In your MainPage.xaml.cs, update your button click handler by retrieving hello current value of hello Locale combo box and providing it toohello call toohello Notifications class, as shown:</span></span>
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
            var locale = (string)Locale.SelectedItem;
   
            var categories = new HashSet<string>();
            if (WorldToggle.IsOn) categories.Add("World");
            if (PoliticsToggle.IsOn) categories.Add("Politics");
            if (BusinessToggle.IsOn) categories.Add("Business");
            if (TechnologyToggle.IsOn) categories.Add("Technology");
            if (ScienceToggle.IsOn) categories.Add("Science");
            if (SportsToggle.IsOn) categories.Add("Sports");
   
            var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(locale,
                 categories);
   
            var dialog = new MessageDialog("Locale: " + locale + " Subscribed to: " + 
                string.Join(",", categories) + " on registration Id: " + result.RegistrationId);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
4. <span data-ttu-id="3aa8f-143">Наконец, в файле App.xaml.cs убедитесь, что tooupdate вашей `InitNotificationsAsync` tooretrieve метод hello языкового стандарта и использовать его при подписке:</span><span class="sxs-lookup"><span data-stu-id="3aa8f-143">Finally, in your App.xaml.cs file, make sure tooupdate your `InitNotificationsAsync` method tooretrieve hello locale and use it when subscribing:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var result = await notifications.SubscribeToCategories(notifications.RetrieveLocale());
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

## <a name="send-localized-notifications-from-your-back-end"></a><span data-ttu-id="3aa8f-144">Отправка уведомлений из серверной части</span><span class="sxs-lookup"><span data-stu-id="3aa8f-144">Send localized notifications from your back-end</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

<!-- Anchors. -->
[Template concepts]: #concepts
[hello app user interface]: #ui
[Building hello Windows Store client app]: #building-client
[Send notifications from your back-end]: #send
[Next Steps]:#next-steps

<!-- Images. -->

<!-- URLs. -->
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users
[toosend использования концентраторов уведомлений, новости]: /manage/services/notification-hubs/breaking-news-dotnet

[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-dotnet
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-dotnet
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-dotnet
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-app-users-dotnet
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-dotnet
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
