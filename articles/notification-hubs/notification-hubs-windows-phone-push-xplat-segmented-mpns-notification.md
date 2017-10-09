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
# <a name="use-notification-hubs-toosend-breaking-news"></a>Использование концентраторов уведомлений toosend новости
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Обзор
В этом разделе показано, как toouse концентраторов уведомлений Azure toobroadcast критические новостей уведомления tooa Windows Phone 8.0/8.1 приложение Silverlight. Если вы используете магазина Windows или приложения Windows Phone 8.1, можно найти tootoohello [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) версии. После завершения будет быть может tooregister переноса категории новостей нужных вам и получения только push-уведомлений для этих категорий. Этот сценарий представлен общий шаблон для многих приложений, где уведомления состоят из отправленных toobe toogroups пользователей, которым был объявлен ранее интересующих их, например, средство чтения RSS, приложений для вентиляторов музыку и т. д.

Широковещательный сценарии реализуются путем включения одного или нескольких *теги* при создании регистрации в концентраторе уведомлений hello. Отправке уведомлений tooa тегов, все устройства, которые зарегистрированы для тега hello получат уведомление hello. Так как теги являются просто строками, у которых нет toobe заранее подготовлены. Дополнительные сведения о тегах см. в разделе слишком[маршрутизации концентраторов уведомлений и выражения с тегами](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Предварительные требования
В этом разделе основан на приложение hello, созданный в [приступить к работе с концентраторами уведомлений]. Перед началом работы с учебником необходимо пройти задания учебника [приступить к работе с концентраторами уведомлений].

## <a name="add-category-selection-toohello-app"></a>Добавить приложение toohello Выбор категории
Hello первым шагом является tooadd hello пользовательского интерфейса элементы tooyour существующей главной страницы, включить tooregister категории tooselect пользователя hello. выбранные пользователем категории Hello хранятся на устройстве hello. При запуске приложение hello регистрацию устройств создается в концентратор уведомлений с категориями hello выбран как теги.

1. Откройте файл проекта MainPage.xaml hello, а затем заменить hello **сетки** элементы с именем `TitlePanel` и `ContentPanel` с hello, следующий код:
   
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
2. В проекте hello, создайте новый класс с именем **уведомления**, добавить hello **открытый** toohello модификатор определения класса, а затем добавьте следующие hello **с помощью** инструкций toohello новый файл кода:
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. Копирования hello следующий код в новый hello **уведомления** класса:
   
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

    Этот класс использует hello изолированные хранилища toostore hello категории новостей, что устройство является tooreceive. Он также содержит методы tooregister для следующих категорий с помощью [шаблона](notification-hubs-templates-cross-platform-push-messages.md) регистрации уведомлений.


1. Добавьте в файл проекта App.xaml.cs hello hello следующие свойства toohello **приложения** класса. Замените hello `<hub name>` и `<connection string with listen access>` местозаполнителей уведомления имя и hello строку подключения к концентратору для *DefaultListenSharedAccessSignature* , полученный ранее.
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > Так как учетные данные, которые распространяются с помощью клиентского приложения, обычно не безопасны, hello ключ для прослушивания доступа следует распространять только с помощью клиентского приложения. Прослушивать доступа включает tooregister вашего приложения для уведомлений, но существующие регистрации нельзя изменить, и не может отправлять уведомления. Полный доступ Hello используется в защищенной серверной службе для отправки уведомлений и изменять существующие регистрации.
   > 
   > 
2. Добавьте в ваш MainPage.xaml.cs hello, следующей строкой.
   
        using Windows.UI.Popups;
3. В файле проекта MainPage.xaml.cs hello добавьте следующий метод hello:
   
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
   
    Этот метод создает список категорий и использует hello **уведомления** класса toostore список hello в локальном хранилище hello и зарегистрируйте hello соответствующие теги в концентраторе уведомлений. При изменении категории регистрации hello воссоздается при hello новые категории.

Приложение теперь может toostore набор категорий в локальном хранилище на устройстве hello и зарегистрировать с концентратором уведомлений hello всякий раз, когда изменения пользователя hello hello выбора категорий.

## <a name="register-for-notifications"></a>Регистрация для использования уведомлений
Эти шаги зарегистрировать hello концентратора уведомлений при запуске с помощью категорий hello, хранящихся в локальном хранилище.

> [!NOTE]
> URI, присвоенный hello Microsoft Push Notification Service (MPNS) hello канала может меняться в любое время, следует зарегистрировать для получения уведомлений часто tooavoid сбоев уведомлений. В этом примере регистрируется для уведомлений, каждый раз при запуске этого приложения hello. Для приложений, которые часто выполняются более чем один раз в день, возможно, если можно пропустить пропускной способности toopreserve регистрации менее чем за день прошел с момента предыдущей регистрации hello.
> 
> 

1. Откройте файл App.xaml.cs hello и добавьте hello **async** модификатор слишком**Application_Launching** метод и заменить код регистрации hello концентраторов уведомлений, добавленный в [приступить к работе с концентраторами уведомлений] с hello, следующий код:
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    Это гарантирует, что каждый раз при запуске приложение hello он получает hello категорий из локального хранилища и запросов регистрации для следующих категорий.
2. В файле проекта MainPage.xaml.cs hello, добавьте следующий код, который реализует hello hello **OnNavigatedTo** метод:
   
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
   
    Этого обновления hello главной страницы на основе состояния hello ранее сохраненные категорий.

приложение Hello завершен, можно сохранить набор категорий в hello tooregister локального хранилища используется устройством с концентратором уведомлений hello всякий раз, когда изменения пользователя hello hello выбора категорий. Затем мы определим серверной части, можно отправить приложение toothis категории уведомлений.

## <a name="sending-tagged-notifications"></a>Отправка уведомлений с тегами
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a>Запустите приложение hello и создавать уведомления
1. В Visual Studio нажмите клавишу F5 toocompile и запустить приложение hello.
   
    ![][1]
   
    Обратите внимание, что приложение hello пользовательского интерфейса предоставляет набор переключает, позволяет выбрать toosubscribe hello категорий для.
2. Включите переключатели одной или нескольких категорий, затем нажмите **Подписаться**.
   
    приложение Hello преобразует hello выбранной категории в теги и запрашивает новую регистрацию устройств для hello выбранных тегов из концентратора уведомлений hello. Hello зарегистрированных категорий возвращается и отображается в диалоговом окне.
   
    ![][2]
3. После получения подтверждения, что категорий были завершения подписки, запустите уведомления toosend hello консольного приложения для каждой категории. Убедитесь, что только вы получаете уведомление для hello категорий, которые вы подписаны.
   
    ![][3]

Вы завершили эту тему.

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

