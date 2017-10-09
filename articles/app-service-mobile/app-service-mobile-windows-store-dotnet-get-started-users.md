---
title: "приложения универсальной платформы Windows (UWP) tooyour authentication aaaAdd | Документы Microsoft"
description: "Узнайте, как пользователи tooauthenticate toouse мобильные приложения службы приложений Azure с помощью различных поставщиков удостоверений, включая приложения универсальной платформы Windows (UWP): AAD, Google, Facebook, Twitter и Майкрософт."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 6cffd951-893e-4ce5-97ac-86e3f5ad9466
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: ad4477e9509f1c40c33e71818e268f6857fe1e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-windows-app"></a>Добавление приложения Windows authentication tooyour
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

В этом разделе показано, как tooadd проверку подлинности на основе облака tooyour мобильного приложения. В этом учебнике добавлении проверки подлинности toohello универсальной платформы Windows (UWP) быстрый запуск проекта для мобильных приложений с помощью поставщика удостоверений, который поддерживается службой приложений Azure. После успешного проверку подлинности и авторизацию серверной части мобильного приложения, отображается значение идентификатора пользователя hello.

Этот учебник основывается на примеры использования мобильные приложения hello. Необходимо сначала пройти учебник hello [начало работы с мобильным приложениям](app-service-mobile-windows-store-dotnet-get-started.md).

## <a name="register"></a>Регистрация приложения для проверки подлинности и настройка hello службы приложений
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Добавить ваш URL-адреса внешнего перенаправления разрешено toohello для приложений

Для безопасной аутентификации требуется определить новую схему URL-адресов для своего приложения. Это позволяет приложение hello проверки подлинности системы tooredirect задней tooyour после завершения процесса проверки подлинности hello. В этом учебнике мы используем схема URL-адресов hello _appname_ на протяжении. Тем не менее можно использовать любую схему URL-адресов на свой выбор. Он должен быть уникальным tooyour мобильного приложения. tooenable hello перенаправления на стороне сервера hello:

1. В hello [Azure портал] выберите приложение службы.

2. Нажмите кнопку hello **проверки подлинности и авторизации** пункт меню.

3. В hello **допускается внешний URL-адреса перенаправления**, введите `url_scheme_of_your_app://easyauth.callback`.  Hello **url_scheme_of_your_app** в данной строке — hello схема URL-адресов для мобильного приложения.  Она должна соответствовать обычной спецификации URL-адресов для протокола (можно использовать буквы и цифры, и адрес должен начинаться с буквы).  Необходимо записать строку hello, выбранный как он потребуется tooadjust кода приложений для мобильных устройств с hello схема URL-адресов в нескольких местах.

4. Нажмите кнопку **ОК**.

5. Щелкните **Сохранить**.

## <a name="permissions"></a>Ограничить разрешения пользователей tooauthenticated
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

Теперь вы можете подтвердить этой серверной tooyour анонимный доступ отключен. Задать в качестве запускаемого проекта hello hello проекта приложения UWP развертывание и запуск приложения hello; Убедитесь, что возникает необработанное исключение с кодом состояния 401 (не санкционировано) после запуска приложение hello. Это происходит потому, что приложение hello пытается tooaccess код мобильного приложения без проверки подлинности пользователя, но hello *TodoItem* таблица теперь требует проверки подлинности.

Затем пользователи tooauthenticate приложения hello обновляете перед запросом ресурсы из приложения службы.

## <a name="add-authentication"></a>Добавить приложение toohello проверки подлинности
1. В проекте приложения UWP hello файл MainPage.xaml.cs и добавьте следующий фрагмент кода hello:
   
        // Define a member variable for storing hello signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs hello authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' toohello name of your MobileServiceClient instance.
                // Sign-in using Facebook authentication.
                user = await App.MobileService
                    .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                message =
                    string.Format("You are now signed in - {0}", user.UserId);
   
                success = true;
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
            return success;
        }
   
    Этот код проверяет подлинность пользователя hello с именем входа для Facebook. При использовании поставщика удостоверений, отличные от Facebook, измените значение hello **MobileServiceAuthenticationProvider** выше значения toohello для поставщика.
2. Замените hello **OnNavigatedTo()** метод в файле MainPage.xaml.cs. Далее вы добавите **вход** кнопку toohello приложение, запускающее проверку подлинности.

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. Добавьте следующий фрагмент кода toohello MainPage.xaml.cs hello:
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login hello user and then load data from hello mobile app.
            if (await AuthenticateAsync())
            {
                // Switch hello buttons and load items from hello mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. Откройте файл проекта MainPage.xaml hello, найдите элемент hello, определяющий hello **Сохранить** кнопку и заменить ее именем hello, следующий код:
   
        <Button Name="ButtonSave" Visibility="Collapsed" Margin="0,8,8,0" 
                Click="ButtonSave_Click">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Add"/>
                <TextBlock Margin="5">Save</TextBlock>
            </StackPanel>
        </Button>
        <Button Name="ButtonLogin" Visibility="Visible" Margin="0,8,8,0" 
                Click="ButtonLogin_Click" TabIndex="0">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Permissions"/>
                <TextBlock Margin="5">Sign in</TextBlock> 
            </StackPanel>
        </Button>
5. Добавьте следующий фрагмент кода toohello App.xaml.cs hello:

        protected override void OnActivated(IActivatedEventArgs args)
        {
            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                Frame content = Window.Current.Content as Frame;
                if (content.Content.GetType() == typeof(MainPage))
                {
                    content.Navigate(typeof(MainPage), protocolArgs.Uri);
                }
            }
            Window.Current.Activate();
            base.OnActivated(args);
        }
6. Откройте файл Package.appxmanifest, перейдите в каталог слишком**объявления**в **доступные объявления** раскрывающегося списка выберите **протокола** и нажмите кнопку **добавить** кнопки. Теперь настройка hello **свойства** из hello **протокола** объявления. В **отображаемое имя**, добавьте имя hello нужно toousers toodisplay приложения. В поле **Имя** добавьте {url_scheme_of_your_app}.
7. Нажмите клавиши приложение hello ключа toorun hello F5, щелкните hello **вход** кнопки и вход в приложение hello с поставщиком удостоверений выбранной. Вход в систему после успешного завершения, приложение hello выполняется без ошибок, и вы могли tooquery серверной части и производить toodata обновлений.

## <a name="tokens"></a>Маркер проверки подлинности hello хранилища на приветствия клиента
Предыдущий пример Hello показал стандартный вход, требующий toocontact клиента hello оба поставщика удостоверений hello и hello службы приложений, каждый раз при запуске этого приложения hello. Не только неэффективен этот метод, можно запустить в использовании относится проблемы следует пробовать многие клиенты toostart приложения на hello то же время. Лучшим подходом является toocache hello авторизации токен, возвращенный вашей службы приложений и повторите toouse это перед использованием сначала вход на основе поставщика.

> [!NOTE]
> Можно кэшировать маркер hello, выдаваемые службой приложения независимо от того, используется ли-управляемый клиент или служба проверки подлинности. Этот учебник использует управляемую сервером проверку подлинности.
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a>Дальнейшие действия
Завершения этого учебника обычной проверки подлинности, рассмотрите возможность продолжить на tooone из hello следующие учебники:

* [Добавить приложение tooyour уведомлений push](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  Узнайте, как push-уведомления tooadd поддерживают tooyour приложения и настройки вашего мобильного приложения серверной toouse концентраторов уведомлений Azure toosend push-уведомлений.
* [Включение автономной синхронизации для приложения](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Узнайте, как автономные tooadd поддерживают приложения с помощью внутреннего сервера мобильного приложения. Автономная синхронизация позволяет конечным пользователям toointeract с мобильным приложением&mdash;Просмотр, добавление или изменение данных&mdash;даже в том случае, если нет сетевого соединения.

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
