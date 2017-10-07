---
title: "aaaGet запущена с использованием проверки подлинности для мобильных приложений в Xamarin iOS"
description: "Узнайте, каким образом пользователи tooauthenticate toouse мобильные приложения Xamarin приложения iOS с помощью различных поставщиков удостоверений, включая AAD, Google, Facebook, Twitter и Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 180cc61b-19c5-48bf-a16c-7181aef3eacc
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: glenga
ms.openlocfilehash: 6458e9651b03df61c86b88b11953792e04bfa5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinios-app"></a>Добавление приложения Xamarin.iOS tooyour проверки подлинности
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

В этом разделе показано, как пользователи tooauthenticate приложение службы мобильных приложений из клиентского приложения. В этом учебнике добавления проверки подлинности toohello Xamarin.iOS быстрый запуск проекта с помощью поставщика удостоверений, который поддерживается службой приложений. После успешного проверку подлинности или авторизации мобильного приложения, отображается значение идентификатора пользователя hello и будет может tooaccess только табличные данные.

Необходимо сначала пройти учебник hello [Создание приложения Xamarin.iOS]. Если вы не используете hello загружен быстрый запуск сервера проекта, необходимо добавить проект tooyour пакета расширения проверки подлинности hello. Дополнительные сведения о пакетах расширения сервера см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="register-your-app-for-authentication-and-configure-app-services"></a>Регистрация приложения для проверки подлинности и настройка служб приложений
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-toohello-allowed-external-redirect-urls"></a>Добавить ваш URL-адреса внешнего перенаправления разрешено toohello для приложений

Для безопасной аутентификации требуется определить новую схему URL-адресов для своего приложения. Это позволяет приложение hello проверки подлинности системы tooredirect задней tooyour после завершения процесса проверки подлинности hello. В этом учебнике мы используем схема URL-адресов hello _appname_ на протяжении. Тем не менее можно использовать любую схему URL-адресов на свой выбор. Он должен быть уникальным tooyour мобильного приложения. tooenable hello перенаправления на стороне сервера hello:

1. В hello [Azure портал] выберите приложение службы.

2. Нажмите кнопку hello **проверки подлинности и авторизации** пункт меню.

3. В hello **допускается внешний URL-адреса перенаправления**, введите `url_scheme_of_your_app://easyauth.callback`.  Hello **url_scheme_of_your_app** в данной строке — hello схема URL-адресов для мобильного приложения.  Она должна соответствовать обычной спецификации URL-адресов для протокола (можно использовать буквы и цифры, и адрес должен начинаться с буквы).  Необходимо записать строку hello, выбранный как он потребуется tooadjust кода приложений для мобильных устройств с hello схема URL-адресов в нескольких местах.

4. Нажмите кнопку **ОК**.

5. Щелкните **Сохранить**.

## <a name="restrict-permissions-tooauthenticated-users"></a>Ограничить разрешения пользователей tooauthenticated
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

&nbsp;&nbsp;4. В Visual Studio или Xamarin Studio Запустите клиентский проект hello на устройстве или эмуляторе. Убедитесь, что возникает необработанное исключение с кодом состояния 401 (не санкционировано) после запуска приложение hello. Сбой Hello — журнал toohello консоль hello отладчика. Поэтому в Visual Studio, вы увидите сбоя hello в окне вывода hello.

&nbsp;&nbsp;Эта ошибка несанкционированного происходит потому, что приложение hello пытается tooaccess серверной части мобильное приложение от имени пользователя без проверки подлинности. Hello *TodoItem* таблица теперь требует проверки подлинности.

Далее можно обновить ресурсов toorequest hello клиентского приложения из внутреннего сервера мобильного приложения hello с прошедшим проверку пользователем.

## <a name="add-authentication-toohello-app"></a>Добавить приложение toohello проверки подлинности
В этом разделе предстоит изменить приложение hello toodisplay экран входа перед отображением данных. При запуске приложение hello, он будет не подключиться tooyour службы приложений и не отображаются все данные. После hello первый раз hello, выполняемых этим пользователем жестов обновления hello, отобразится экран входа hello. После успешного входа hello список элементов todo отображается.

1. В клиентском проекте hello, откройте файл hello **QSTodoService.cs** и добавьте следующее hello с помощью инструкции и `MobileServiceUser` с toohello доступа QSTodoService класса:
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. Добавьте новый метод с именем **Authenticate** слишком**QSTodoService** с hello следующие определения:

        public async Task Authenticate(UIViewController view)
        {
            try
            {
                AppDelegate.ResumeWithURL = url => url.Scheme == "zumoe2etestapp" && client.ResumeWithURL(url);
                user = await client.LoginAsync(view, MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine (@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
            }
        }

    >[AZURE.NOTE] При использовании поставщика удостоверений, отличные от Facebook, измените значение hello, переданный слишком**LoginAsync** выше tooone hello следующее: _MicrosoftAccount_, _Twitter_, _Google_, или _WindowsAzureActiveDirectory_.

3. Откройте файл **QSTodoListViewController.cs**. Изменить определение метода hello **ViewDidLoad** Удаление вызова hello слишком**RefreshAsync()** скоро истекает hello:
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out hello call tooRefreshAsync
            // await RefreshAsync();
        }
4. Измените метод hello **RefreshAsync** tooauthenticate Если hello **пользователя** свойство имеет значение null. Добавьте после кода hello верхней части определения метода hello hello:
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. Откройте **AppDelegate.cs**, добавьте следующий метод hello:

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. Откройте **Info.plist** файл, перейдите в слишком**типы URL-адрес** в hello **Дополнительно** раздела. Теперь настройка hello **идентификатор** и hello **URL-схем** тип URL-адрес и нажмите кнопку **добавить тип URL-адрес**. **URL-схем** должно быть таким же hello как {url_scheme_of_your_app}.
7. В Visual Studio или Xamarin Studio подключен tooyour узла сборки Xamarin на компьютере Mac Запустите клиентский проект hello, предназначенных для устройства или эмулятора. Убедитесь, что данные не отображаются, приложение hello.
   
    Для выполнения обновления жестов hello перетащите вниз hello список элементов, которые вызовут tooappear экрана входа hello. После успешного ввода действительных учетных данных, приложение hello будет отображать список элементов todo hello и внесении toohello обновляет данные.

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Создание приложения Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md