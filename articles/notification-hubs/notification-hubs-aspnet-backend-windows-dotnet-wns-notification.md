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
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a>Уведомление пользователей посредством концентраторов уведомлений с помощью серверной части .NET
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>Обзор
Поддержка уведомлений Push в Azure позволяет tooaccess к использованию, многоплатформенных и масштабируемых push-инфраструктуру, которая значительно упрощает реализацию hello push-уведомлений для индивидуальных пользователей и корпоративных приложений для мобильных устройств платформы. Этот учебник показывает, как toosend toouse концентраторов уведомлений Azure push-уведомления tooa определенное приложение пользователя на конкретном устройстве. Внутренний ASP.NET WebAPI — используется tooauthenticate клиентов. Привет, прошедшие проверку подлинности пользователя клиента и тег, будут автоматически добавляться регистрацией toonotification hello серверной части. Этот тег будет используется toosend уведомлениями toogenerate hello серверной части для конкретного пользователя. Дополнительные сведения о регистрации для уведомлений с использованием внутреннего сервера приложения см. в разделе hello руководство [регистрации из серверной части приложения](http://msdn.microsoft.com/library/dn743807.aspx). Этот учебник построен на концентраторе уведомлений hello и проект, созданный в hello [приступить к работе с концентраторами уведомлений] учебника.

Этот учебник содержит также hello готовности toohello [принудительной защиты] учебника. После завершения шагов hello в этом учебнике, вы можете перейти toohello [принудительной защиты] руководство, в котором показано, как toomodify hello код в этот учебник toosend push-уведомление безопасно.

## <a name="before-you-begin"></a>Перед началом работы
Мы очень ценим ваши отзывы. Если возникли проблемы, завершение работы этого раздела или рекомендации по улучшению это содержимое, мы ценим ваши отзывы hello нижней части страницы приветствия.

код завершения Hello в этом учебнике можно найти на GitHub [здесь](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers). 

## <a name="prerequisites"></a>Предварительные требования
Перед началом работы с этим учебником необходимо изучить следующие учебники по мобильным службам.

* [приступить к работе с концентраторами уведомлений]<br/>Создать концентратор уведомлений и зарезервировать имя приложения hello и зарегистрировать tooreceive уведомления в этом учебнике. В этом учебнике предполагается, что следующие действия уже были предприняты. В противном случае следуйте инструкциям hello [Приступая к работе с концентраторами уведомлений (магазин Windows)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); в частности, hello разделы [регистрации приложения для магазина Windows hello](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) и [Настройка Концентратор уведомлений](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub). В частности, убедитесь в том, что вы ввели hello **ИД безопасности пакета** и **секрет клиента** значения в hello hello портале **Настройка** вкладке концентратор уведомлений. Эта конфигурация процедура описана в разделе hello [настройки центра уведомлений](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub). Это важный шаг: Если hello учетные данные на портале hello не соответствуют указанной выбрать имя приложения hello, hello push-уведомление не будет выполнено.

> [!NOTE]
> При использовании мобильных приложений в службе приложений Azure как безопасности внутренней службы. в разделе hello [мобильные приложения версии](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) этого учебника.
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-hello-code-for-hello-client-project"></a>Обновление кода hello для проекта клиента hello
В этом разделе, при обновлении кода hello в проекте hello, вы выполнили hello [приступить к работе с концентраторами уведомлений] учебника. Hello следует уже связанную с хранилищем hello и настроен для центра уведомлений. В этом разделе будет добавить новый внутренний WebAPI кода toocall hello и использовать его для регистрации и отправки уведомлений.

1. В Visual Studio откройте решение hello hello, созданный для hello [приступить к работе с концентраторами уведомлений] учебника.
2. В обозревателе решений щелкните правой кнопкой мыши hello **(Windows 8.1)** проект и выберите пункт **управление пакетами NuGet**.
3. В левой части окна hello, выберите **Online**.
4. В hello **поиска** введите **HTTP-клиент**.
5. В списке результатов hello, нажмите кнопку **клиентских библиотек HTTP Майкрософт**, а затем нажмите кнопку **установить**. Завершить установку hello.
6. Вернитесь в hello NuGet **поиска** введите **Json.net**. Установка hello **Json.NET** пакета и hello закройте окно диспетчера пакетов NuGet.
7. Повторите приведенные выше действия hello для hello **(Windows Phone 8.1)** hello проекта tooinstall **JSON.NET** пакет NuGet для проекта Windows Phone hello.
8. В обозревателе решений в hello **(Windows 8.1)** проекта, дважды щелкните **MainPage.xaml** tooopen его в редакторе Visual Studio hello.
9. В hello **MainPage.xaml** XML-код, замените hello `<Grid>` раздел с hello, следующий код. Этот код добавляет текстовое поле имени пользователя и пароля, Здравствуйте, пользователь будет выполнять проверку подлинности с помощью. Он также добавляет текстовые поля для сообщения уведомления hello и тег hello имя пользователя, который должен получать уведомления hello.
   
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
10. В обозревателе решений в hello **(Windows Phone 8.1)** откройте проект **MainPage.xaml** и замените hello Windows Phone 8.1 `<Grid>` раздел с этой же приведенный выше код. Hello интерфейс должен выглядеть примерно toowhats, показано ниже.
    
    ![][13]
11. В обозревателе решений откройте hello **MainPage.xaml.cs** файл для hello **(Windows 8.1)** и **(Windows Phone 8.1)** проектов. Добавьте следующее hello `using` инструкции вверху hello оба файла:
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. В **MainPage.xaml.cs** для hello **(Windows 8.1)** и **(Windows Phone 8.1)** проектов, добавьте следующий член toohello hello `MainPage` класса. Убедиться, что tooreplace быть `<Enter Your Backend Endpoint>` с hello ранее полученный фактическое серверной конечной точки. Например, `http://mybackend.azurewebsites.net`.
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. Добавьте код hello ниже класс MainPage toohello в **MainPage.xaml.cs** для hello **(Windows 8.1)** и **(Windows Phone 8.1)** проектов.
    
    Hello `PushClick` метод — hello обработчика для hello **принудительной отправки** кнопки. Он вызывает hello серверной tootrigger tooall уведомления устройств с помощью имени пользователя тег, который соответствует hello `to_tag` параметра. Hello отправляется уведомление как содержимое JSON в теле запроса hello.
    
    Hello `LoginAndRegisterClick` метод — hello обработчика для hello **вход и зарегистрируйте** кнопки. Он сохраняет hello basic токена проверки подлинности в локальном хранилище (Обратите внимание, что это касается любого токена, который использует схему проверки подлинности), затем использует `RegisterClient` tooregister для уведомлений с использованием внутреннего hello.

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



1. В обозревателе решений в разделе hello **Shared** проект, откройте hello **App.xaml.cs** файла. Поиск вызова hello слишком`InitNotificationsAsync()` в hello `OnLaunched()` обработчика событий. Закомментируйте или удалите вызов hello слишком`InitNotificationsAsync()`. Обработчик кнопки Hello добавленных выше будет инициализировать регистрации уведомлений.

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. В обозревателе решений щелкните правой кнопкой мыши hello **Shared** проекта, а затем нажмите кнопку **добавить**, а затем нажмите кнопку **класса**. Имя класса hello **RegisterClient.cs**, нажмите кнопку **ОК** toogenerate hello класса.
   
   Этот класс будет переноситься hello REST вызывает необходимые toocontact hello внутреннего сервера приложения, в порядке tooregister push-уведомления. Она также локально хранит hello *свойства Registrationid* созданные hello концентратор уведомлений, как описано в [регистрации из серверной части приложения](http://msdn.microsoft.com/library/dn743807.aspx). Обратите внимание, что он использует маркер авторизации, хранящихся в локальном хранилище, при нажатии кнопки hello **входа и регистрации** кнопки.
2. Добавьте следующее hello `using` операторы в начале hello hello RegisterClient.cs файла:
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. Добавьте следующий код внутри hello hello `RegisterClient` определения класса.
   
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
4. Сохраните изменения.

## <a name="testing-hello-application"></a>Тестирование приложения hello
1. Запустите приложение hello на Windows 8.1 и Windows Phone 8.1. Для Windows Phone 8.1 можно запустить экземпляр hello в эмуляторе hello или само устройство.
2. В экземпляре hello Windows 8.1 приложение hello, введите **Username** и **пароль** как показано ниже экрана приветствия. Она должна отличаться от hello имя пользователя и пароль, введенные на Windows Phone.
3. Щелкните **Вход и регистрация** и убедитесь, что в диалоговом окне отображается подтверждение выполнения входа. Это также позволит hello **принудительной отправки** кнопки.
   
    ![][14]
4. На экземпляре hello Windows Phone 8.1, введите строку имени пользователя в обоих hello **Username** и **пароль** поля, затем нажмите кнопку **входа и регистрации**.
5. Затем в hello **тег Username получателя** введите имя пользователя hello, зарегистрированных в Windows 8.1. Введите сообщение уведомления и нажмите кнопку **Отправить push-уведомление**.
   
    ![][16]
6. Только hello устройства, которые регистрировались hello соответствующий тег username сообщение hello уведомления.
   
    ![][15]

## <a name="next-steps"></a>Дальнейшие действия
* Если toosegment пользователям по группы интересов, см. [toosend использования концентраторов уведомлений, новости].
* см. Дополнительные сведения о том, как toolearn toouse концентраторов уведомлений, [руководство концентраторы уведомлений].

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
