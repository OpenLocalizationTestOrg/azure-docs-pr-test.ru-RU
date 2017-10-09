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
# <a name="use-notification-hubs-toosend-localized-breaking-news"></a>Использовать локализованные toosend новости концентраторы уведомлений
> [!div class="op_single_selector"]
> * [C# в Магазине Windows](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [iOS](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a>Обзор
В этом разделе показано, как toouse hello **шаблона** функции концентраторов уведомлений Azure toobroadcast критические уведомления новостей, локализованные языка и устройства. В этом учебнике, запуск приложения магазина Windows hello, созданные в [toosend использования концентраторов уведомлений, новости]. После завершения можно будет tooregister для категорий, которые вас интересуют, указать язык в уведомления, которое tooreceive hello и получать только push-уведомлений для hello выбранных категорий на этом языке.

Существует два сценария toothis частей:

* приложения для магазина Windows Hello позволяет клиентским устройств toospecify язык и toodifferent toosubscribe критические категории новостей;
* Hello внутренней осуществляет широковещательную рассылку уведомлений hello, с использованием hello **тега** и **шаблона** поддержки концентраторов уведомлений Azure.

## <a name="prerequisites"></a>Предварительные требования
Вы должны уже выполнили hello [toosend использования концентраторов уведомлений, новости] учебника и иметь hello кода, так как этот учебник построен непосредственно на этот код.

Также требуется Visual Studio 2012 или более поздняя версия.

## <a name="template-concepts"></a>Основные сведения о шаблонах
В [toosend использования концентраторов уведомлений, новости] построении приложения, которое используется **теги** toonotifications toosubscribe новостей разных категорий.
Однако многие приложения ориентированы на несколько рынков и требуют локализации. Таким образом, содержимое hello hello уведомлений, сами имеют toobe локализованные доставленный toohello правильным набором устройств.
В этом разделе будет показано, как toouse hello **шаблона** функции концентраторов уведомлений tooeasily доставки локализованное уведомлений с последними новостями.

Примечание: один из способов toosend локализованные уведомления является toocreate нескольких версий каждого тега. Для экземпляра toosupport английском, французском и мандаринский, пришлось бы иметь три разные теги Мировые: «world_en», «world_fr» и «world_ch». Мы будет иметь toosend локализованной версии tooeach новостей hello world эти теги. В этом разделе используются шаблоны tooavoid hello увеличением числа теги и требование hello отправка нескольких сообщений.

На высоком уровне шаблоны являются toospecify способом как конкретного устройства следует получать такие уведомления. шаблон Hello указывает формат hello точное полезных данных с помощью ссылки tooproperties, которые являются частью приветственное сообщение, отправленное приложение в серверной части. В нашем случае мы отправим независимое от языка сообщение, которое содержит все поддерживаемые языки:

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

Затем мы гарантируем, что устройства регистрацию с шаблоном, который ссылается свойство правильный toohello. Для экземпляра приложения для магазина Windows, в которой необходимо tooreceive сообщение простое всплывающее уведомление будет зарегистрирован для hello следующий шаблон с любой соответствующие теги:

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



Шаблоны — это очень мощная функция, о них можно узнать больше в нашей статье [Шаблоны](notification-hubs-templates-cross-platform-push-messages.md) . 

## <a name="hello-app-user-interface"></a>пользовательский интерфейс приложения Hello
Теперь мы изменит приложение hello последние новости, созданный в разделе hello [toosend использования концентраторов уведомлений, новости] toosend локализованные новости, с помощью шаблонов.

В приложении Магазина Windows:

Изменение вашей MainPage.xaml tooinclude combobox языкового стандарта.

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

## <a name="building-hello-windows-store-client-app"></a>Построение клиентского приложения для магазина Windows hello
1. В классе уведомления, добавьте параметр языкового стандарта tooyour *StoreCategoriesAndSubscribe* и *SubscribeToCateories* методы.
   
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
   
    Обратите внимание, что вместо вызывающему Привет *RegisterNativeAsync* вызываем метод *RegisterTemplateAsync*: мы регистрации уведомлений формат, в которых hello шаблона зависит от языкового стандарта hello. Мы также предоставляем имя шаблона hello («localizedWNSTemplateExample»), так как может потребоваться tooregister более одного шаблона (например один всплывающих уведомлений) и один для плиток, а нам нужно tooname их в порядке может tooupdate toobe или удалить их.
   
    Обратите внимание, если несколько шаблонов регистрации устройства с таким же тегом при входящего сообщения, предназначенные для тега приведет hello несколько уведомлений доставлено toohello устройства (по одному для каждого шаблона). Это полезно, если hello одного логического сообщения tooresult в нескольких visual уведомлений, например отображение эмблемы и всплывающие в приложения для магазина Windows.
2. Добавьте следующие сохраненного языкового стандарта hello tooretrieve метод hello:
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. В вашей MainPage.xaml.cs вашей кнопка обновления нажмите кнопку обработчика, извлекая hello текущее значение поля со списком hello языкового стандарта и передавая ему класс уведомления toohello toohello вызова, как показано:
   
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
4. Наконец, в файле App.xaml.cs убедитесь, что tooupdate вашей `InitNotificationsAsync` tooretrieve метод hello языкового стандарта и использовать его при подписке:
   
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

## <a name="send-localized-notifications-from-your-back-end"></a>Отправка уведомлений из серверной части
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
