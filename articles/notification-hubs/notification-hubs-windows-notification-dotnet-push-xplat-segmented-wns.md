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
# <a name="use-notification-hubs-toosend-breaking-news"></a>Использование концентраторов уведомлений toosend новости
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Обзор
В этом разделе показано, как toobroadcast концентраторов уведомлений Azure toouse критические новостей уведомления tooa магазина Windows или приложения Windows Phone 8.1 (отличных от Silverlight). Если вы используете Windows Phone 8.1 Silverlight, можно найти toohello [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) версии. После завершения будет быть может tooregister переноса категории новостей нужных вам и получения только push-уведомлений для этих категорий. Этот сценарий представлен общий шаблон для многих приложений, где уведомления состоят из отправленных toobe toogroups пользователей, которым был объявлен ранее интерес в них, например средство чтения RSS, приложений для вентиляторов музыки и т. д. 

Широковещательный сценарии реализуются путем включения одного или нескольких *теги* при создании регистрации в концентраторе уведомлений hello. Отправке уведомлений tooa тегов, все устройства, которые зарегистрированы для тега hello получат уведомление hello. Так как теги являются просто строками, у которых нет toobe заранее подготовлены. Дополнительные сведения о тегах см. в разделе слишком[маршрутизации концентраторов уведомлений и выражения с тегами](notification-hubs-tags-segment-push-message.md).

> [!NOTE]
> Проекты для Магазина Windows и проекты Windows Phone 8.1 и более ранней версии не поддерживаются в Visual Studio 2017.  Дополнительные сведения см. в статье [Целевая платформа и совместимость для Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs). 

## <a name="prerequisites"></a>Предварительные требования
В этом разделе основан на приложение hello, созданный в [приступить к работе с концентраторами уведомлений][get-started]. Перед началом работы с данным руководством необходимо выполнить задания руководства по [началу работы с центрами уведомлений][get-started].

## <a name="add-category-selection-toohello-app"></a>Добавить приложение toohello Выбор категории
Hello первым шагом является tooadd hello пользовательского интерфейса элементы tooyour существующей главной страницы, включить tooregister категории tooselect пользователя hello. выбранные пользователем категории Hello хранятся на устройстве hello. При запуске приложение hello регистрацию устройств создается в концентратор уведомлений с категориями hello выбран как теги.

1. Откройте файл проекта MainPage.xaml hello, а затем копировать hello, следующий код в hello **сетки** элемента:
   
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
2. Щелкните правой кнопкой мыши hello **Shared** проекта и добавьте новый класс с именем **уведомления**, добавить hello **открытый** toohello модификатор определения класса, а затем добавьте следующие hello **с помощью** инструкций toohello новый файл кода:
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. Копирования hello следующий код в новый hello **уведомления** класса:
   
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
   
    Этот класс использует локальное хранилище hello toostore категории hello новостей, что это устройство имеет tooreceive. Обратите внимание, что вместо вызывающему Привет *RegisterNativeAsync* вызываем метод *RegisterTemplateAsync* tooregister для категории hello, с помощью регистрацию шаблона. 
   
    Мы также предоставляем имя шаблона hello («simpleWNSTemplateExample»), так как может потребоваться tooregister более одного шаблона (например один всплывающих уведомлений) и один для плиток, а нам нужно tooname их в порядке может tooupdate toobe или удалить их.
   
    Обратите внимание, если несколько шаблонов регистрации устройства с таким же тегом при входящего сообщения, предназначенные для тега приведет hello несколько уведомлений доставлено toohello устройства (по одному для каждого шаблона). Это полезно, если hello одного логического сообщения tooresult в нескольких visual уведомлений, например отображение эмблемы и всплывающие в приложения для магазина Windows.
   
    Подробнее о шаблонах см. в разделе [Шаблоны](notification-hubs-templates-cross-platform-push-messages.md).
4. Добавьте в файл проекта App.xaml.cs hello hello следующие свойства toohello **приложения** класса:
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    Это свойство является используется toocreate и доступа **уведомления** экземпляра.
   
    В hello над кодом, замените hello `<hub name>` и `<connection string with listen access>` местозаполнителей уведомления имя и hello строку подключения к концентратору для *DefaultListenSharedAccessSignature* , полученный ранее.
   
   > [!NOTE]
   > Так как учетные данные, которые распространяются с помощью клиентского приложения, обычно не безопасны, hello ключ для прослушивания доступа следует распространять только с помощью клиентского приложения. Прослушивать доступа включает tooregister вашего приложения для уведомлений, но существующие регистрации нельзя изменить, и не может отправлять уведомления. Полный доступ Hello используется в защищенной серверной службе для отправки уведомлений и изменять существующие регистрации.
   > 
   > 
5. Добавьте в ваш MainPage.xaml.cs hello, следующей строкой.
   
        using Windows.UI.Popups;
6. В файле проекта MainPage.xaml.cs hello добавьте следующий метод hello:
   
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
   
    Этот метод создает список категорий и использует hello **уведомления** класса toostore список hello в локальном хранилище hello и зарегистрируйте hello соответствующие теги в концентраторе уведомлений. При изменении категории регистрации hello воссоздается при hello новые категории.

Приложение теперь может toostore набор категорий в локальном хранилище на устройстве hello и зарегистрировать с концентратором уведомлений hello всякий раз, когда изменения пользователя hello hello выбора категорий.

## <a name="register-for-notifications"></a>Регистрация для использования уведомлений
Эти шаги зарегистрировать hello концентратора уведомлений при запуске с помощью категорий hello, хранящихся в локальном хранилище.

> [!NOTE]
> URI, присвоенный hello Windows Notification Service (WNS) hello канала может меняться в любое время, следует зарегистрировать для получения уведомлений часто tooavoid сбоев уведомлений. В этом примере регистрируется для уведомления каждый раз при запуске этого приложения hello. Для приложений, которые часто выполняются более чем один раз в день, возможно, если можно пропустить пропускной способности toopreserve регистрации менее чем за день прошел с момента предыдущей регистрации hello.
> 
> 

1. App.xaml.cs Привет открыть файл и обновление hello **InitNotificationsAsync** hello toouse метод `notifications` toosubscribe класс на основе категорий.
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    Это гарантирует, что каждый раз при запуске приложение hello он получает hello категорий из локального хранилища и запросов регистрации для следующих категорий. Hello **InitNotificationsAsync** метод был создан как часть hello [приступить к работе с концентраторами уведомлений] [ get-started] учебника.
2. Добавьте в файл проекта MainPage.xaml.cs hello hello, следующий код toohello *OnNavigatedTo* метод:
   
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
   
    ![][19]
3. Отправьте новое уведомление с сервера hello в одном из следующих способов hello:
   
   * **Консольное приложение:** запустить консольное приложение hello.
   * **Java/PHP:** запустите приложение или сценарий.
     
     Уведомления для hello выбранной категории отображаются в виде всплывающих уведомлений.
     
     ![][14]

## <a name="next-steps"></a>Дальнейшие действия
В этом учебнике мы узнали, каким образом toobroadcast новости по категориям. Рассмотрим, выполнив одну из hello следующие учебники, выделите других расширенных сценариях концентраторов уведомлений.

* [Использовать локализованные toobroadcast новости концентраторы уведомлений]
  
    Узнайте, как критические отправки tooenable новостей приложения hello tooexpand локализованные уведомления.

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
