---
title: "aaaGet запущена с использованием проверки подлинности для мобильных приложений в Xamarin Forms приложения | Документы Microsoft"
description: "Узнайте, каким образом пользователи tooauthenticate toouse мобильные приложения Xamarin Forms приложения с помощью различных поставщиков удостоверений, включая AAD, Google, Facebook, Twitter и Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: panarasi
manager: syntaxc4
editor: 
ms.assetid: 9c55e192-c761-4ff2-8d88-72260e9f6179
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: panarasi
ms.openlocfilehash: 7f6716619f33d9cc4f866c41effba8f048dc49fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarin-forms-app"></a>Добавить приложение Xamarin Forms tooyour проверки подлинности
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a>Обзор
В этом разделе показано, как пользователи tooauthenticate приложение службы мобильных приложений из клиентского приложения. В этом учебнике hello Xamarin Forms быстрый запуск проекта с помощью поставщика удостоверений, который поддерживается службой приложений добавить проверку подлинности. После успешного проверку подлинности или авторизации мобильного приложения, отображается значение идентификатора пользователя hello и будет может tooaccess только табличные данные.

## <a name="prerequisites"></a>Предварительные требования
Для получения оптимальных результатов hello к этому учебнику, рекомендуется сначала выполнить hello [Создание приложения Xamarin Forms] [ 1] учебника. Завершив работу, вы получите проект Xamarin Forms — кроссплатформенное приложение TodoList.

Если вы не используете hello загружен быстрый запуск сервера проекта, необходимо добавить проект tooyour пакета расширения проверки подлинности hello. Дополнительные сведения о пакетах расширения сервера см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure][2].

## <a name="register-your-app-for-authentication-and-configure-app-services"></a>Регистрация приложения для проверки подлинности и настройка служб приложений
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Добавить ваш URL-адреса внешнего перенаправления разрешено toohello для приложений

Для безопасной аутентификации требуется определить новую схему URL-адресов для своего приложения. Это позволяет приложение hello проверки подлинности системы tooredirect задней tooyour после завершения процесса проверки подлинности hello. В этом учебнике мы используем схема URL-адресов hello _appname_ на протяжении. Тем не менее можно использовать любую схему URL-адресов на свой выбор. Он должен быть уникальным tooyour мобильного приложения. tooenable hello перенаправления на стороне сервера hello:

1. В hello [Azure портал] выберите приложение службы.

2. Нажмите кнопку hello **проверки подлинности и авторизации** пункт меню.

3. В hello **допускается внешний URL-адреса перенаправления**, введите `url_scheme_of_your_app://easyauth.callback`.  Hello **url_scheme_of_your_app** в данной строке — hello схема URL-адресов для мобильного приложения.  Она должна соответствовать обычной спецификации URL-адресов для протокола (можно использовать буквы и цифры, и адрес должен начинаться с буквы).  Необходимо записать строку hello, выбранный как он потребуется tooadjust кода приложений для мобильных устройств с hello схема URL-адресов в нескольких местах.

4. Нажмите кнопку **ОК**.

5. Щелкните **Сохранить**.

## <a name="restrict-permissions-tooauthenticated-users"></a>Ограничить разрешения пользователей tooauthenticated
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-toohello-portable-class-library"></a>Добавление проверки подлинности toohello переносимой библиотеки классов
Мобильные приложения использует hello [LoginAsync] [ 3] метод расширения в hello [MobileServiceClient] [ 4] toosign в пользователя службы приложения Проверка подлинности. Этот пример использует поток управляемого сервером проверки подлинности, который отображает интерфейс поставщика hello вход в приложение hello. Дополнительные сведения см. в статье [Управляемая сервером проверка подлинности][5]. Чтобы пользователям было удобнее работать с вашим рабочим приложением, попробуйте использовать [управляемую клиентом аутентификацию][6].

Определение tooauthenticate в проекте Xamarin Forms **IAuthenticate** интерфейса в hello переносимой библиотеки классов для приложения hello. Затем добавьте **входа** кнопку toohello интерфейса, определенные на hello переносимой библиотеки классов, которую можно щелкнуть toostart проверки подлинности. Данные загружаются из внутреннего сервера мобильного приложения hello после успешной проверки подлинности.

Реализуйте hello **IAuthenticate** интерфейс для каждой платформы, поддерживаемые в приложении.

1. В Visual Studio и Xamarin Studio, откройте App.cs из проекта hello с **переносимой** в hello имя, являющееся проекта переносимой библиотеки классов, затем добавьте следующие hello `using` инструкции:

        using System.Threading.Tasks;
2. В App.cs, добавьте следующее hello `IAuthenticate` определением непосредственно перед hello интерфейса `App` определения класса.

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. интерфейс hello tooinitialize с помощью реализации платформой добавлять hello следующие статические члены toohello **приложения** класса.

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. Откройте TodoList.xaml из проекта переносимой библиотеки классов hello, добавьте следующее hello **кнопку** элемент в hello *buttonsPanel* макет элемента, после существующего кнопки hello:

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    Эта кнопка запускает управляемую сервером проверку подлинности с помощью серверной части мобильного приложения.
5. Откройте TodoList.xaml.cs из проекта переносимой библиотеки классов hello, а затем добавьте следующие поля toohello hello `TodoList` класса:

        // Track whether hello user has authenticated.
        bool authenticated = false;
6. Замените hello **OnAppearing** метод с hello, следующий код:

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems tootrue in order toosynchronize hello data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide hello Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    Этот код гарантирует, что только обновления данных из службы hello после вы прошли проверку подлинности.
7. Добавьте следующий обработчик для hello hello **щелчок** toohello событий **TodoList** класса:

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems tootrue toosynchronize hello data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. Сохраните изменения и перестройте проект переносимой библиотеки классов hello проверка без ошибок.

## <a name="add-authentication-toohello-android-app"></a>Добавить приложение Android toohello проверки подлинности
В этом разделе показано, как tooimplement hello **IAuthenticate** интерфейс в проекте Android приложения hello. Пропустите этот раздел, если вы не пользуетесь устройствами Android.

1. В Visual Studio и Xamarin Studio, щелкните правой кнопкой мыши hello **droid** проекта, затем **Назначить запускаемым проектом**.
2. Нажмите клавишу F5 toostart hello проекта в отладчике hello, а затем убедитесь, что необработанное исключение с кодом состояния 401 (не санкционировано) возникает после запуска приложения. код 401 Hello создается, так как доступ к серверной части hello только для пользователей ограниченными tooauthorized.
3. Откройте MainActivity.cs в проект Android hello и добавьте следующее hello `using` инструкции:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. Обновление hello **MainActivity** hello класс tooimplement **IAuthenticate** интерфейс следующим образом:

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. Обновление hello **MainActivity** класс, добавив **MobileServiceUser** поля и **Authenticate** метод, который требуется для hello **IAuthenticate**  интерфейс следующим образом:

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                user = await TodoItemManager.DefaultManager.CurrentClient.LoginAsync(this, 
                    MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                if (user != null)
                {
                    message = string.Format("you are now signed-in as {0}.",
                        user.UserId);
                    success = true;
                }
            }
            catch (Exception ex)
            {
                message = ex.Message;
            }

            // Display hello success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    Если используется поставщик удостоверений, отличающийся от Facebook, выберите другое значение [MobileServiceAuthenticationProvider][7].

6. Добавьте следующий код внутри hello <application> узел AndroidManifest.xml:

```xml
    <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
      <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
      </intent-filter>
    </activity>
```

1. Добавьте следующий код toohello hello **OnCreate** метод hello **MainActivity** класса перед вызовом hello слишком`LoadApplication()`:

        // Initialize hello authenticator before loading hello app.
        App.Init((IAuthenticate)this);

    Этот код гарантирует, что средство проверки подлинности hello инициализируется перед загрузкой приложения hello.
2. Перестройте приложение hello, запустите его, а затем войдите с помощью поставщика проверки подлинности hello выбранным и убедитесь, что заданы может tooaccess данные в виде прошедшего проверку подлинности пользователя.

## <a name="add-authentication-toohello-ios-app"></a>Добавление приложения iOS toohello проверки подлинности
В этом разделе показано, как tooimplement hello **IAuthenticate** интерфейса в проект приложения hello iOS. Пропустите этот раздел, если вы не пользуетесь устройствами iOS.

1. В Visual Studio и Xamarin Studio, щелкните правой кнопкой мыши hello **iOS** проекта, затем **Назначить запускаемым проектом**.
2. Нажмите клавишу F5 toostart hello проекта в отладчике hello, а затем убедитесь, что возникает необработанное исключение с кодом состояния 401 (не санкционировано) после запуска приложение hello. ответ 401 Hello создается, так как доступ к серверной части hello только для пользователей ограниченными tooauthorized.
3. Откройте AppDelegate.cs в проекте iOS hello и добавьте следующее hello `using` инструкции:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. Обновление hello **AppDelegate** hello класс tooimplement **IAuthenticate** интерфейс следующим образом:

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. Обновление hello **AppDelegate** класс, добавив **MobileServiceUser** поля и **Authenticate** метод, который требуется для hello **IAuthenticate**  интерфейс следующим образом:

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(UIApplication.SharedApplication.KeyWindow.RootViewController,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                        success = true;
                    }
                }
            }
            catch (Exception ex)
            {
               message = ex.Message;
            }

            // Display hello success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    Если используется поставщик удостоверений, отличающийся от Facebook, выберите другое значение [MobileServiceAuthenticationProvider].

6. Обновить класс AppDelegate hello, добавив перегруженный метод OpenUrl (параметры NSDictionary UIApplication NSUrl URL-адрес приложения)

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. Добавьте следующие строки кода toohello hello **FinishedLaunching** слишком вызов метода перед hello`LoadApplication()`:

        App.Init(this);

    Этот код гарантирует, что средство проверки подлинности hello инициализируется перед загрузкой приложение hello.

6. Добавить **{url_scheme_of_your_app}** tooURL схемы в файле Info.plist.

7. Перестройте приложение hello, запустите его, а затем войдите с помощью поставщика проверки подлинности hello выбранным и убедитесь, что заданы может tooaccess данные в виде прошедшего проверку подлинности пользователя.

## <a name="add-authentication-toowindows-10-including-phone-app-projects"></a>Добавление проверки подлинности tooWindows 10 (включая телефон) проекты приложений
В этом разделе показано, как tooimplement hello **IAuthenticate** интерфейса в проектах приложений Windows 10 hello. используется проекты универсальной платформы Windows (UWP), но с использованием hello Hello **UWP** проекта (с помощью указанных изменений). Пропустите этот раздел, если вы не пользуетесь устройствами Windows.

1. «В Visual Studio щелкните правой кнопкой мыши либо hello **UWP** проекта, затем **Назначить запускаемым проектом**.
2. Нажмите клавишу F5 toostart hello проекта в отладчике hello, а затем убедитесь, что возникает необработанное исключение с кодом состояния 401 (не санкционировано) после запуска приложение hello. ответ 401 Hello происходит потому, что доступ к серверной части hello — только для пользователей ограниченными tooauthorized.
3. Откройте файл MainPage.xaml.cs для проекта приложения Windows hello и добавьте следующее hello `using` инструкции:

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    Замените `<your_Portable_Class_Library_namespace>` с пространством имен hello вашей переносимой библиотеки классов.
4. Обновление hello **MainPage** hello класс tooimplement **IAuthenticate** интерфейс следующим образом:

        public sealed partial class MainPage : IAuthenticate
5. Обновление hello **MainPage** класс, добавив **MobileServiceUser** поля и **Authenticate** метод, который требуется для hello **IAuthenticate** интерфейс следующим образом:

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            string message = string.Empty;
            var success = false;

            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        success = true;
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                    }
                }

            }
            catch (Exception ex)
            {
                message = string.Format("Authentication Failed: {0}", ex.Message);
            }

            // Display hello success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    Если используется поставщик удостоверений, отличающийся от Facebook, выберите другое значение [MobileServiceAuthenticationProvider].

1. Добавьте следующие строки кода в конструкторе hello для hello hello **MainPage** класса перед вызовом hello слишком`LoadApplication()`:

        // Initialize hello authenticator before loading hello app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    Замените `<your_Portable_Class_Library_namespace>` с пространством имен hello вашей переносимой библиотеки классов.

3. Если вы используете **UWP**, добавьте следующее hello **OnActivated** toohello переопределение метода **приложения** класса:

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   Переопределение метода hello уже существует, добавьте условного кода hello из предшествующий фрагмент кода hello.  Этот код не требуется для универсальных проектов Windows.

3. Добавьте **{схема_URL-адреса_вашего_приложения}** в файл Package.appxmanifest. 

4. Перестройте приложение hello, запустите его, а затем войдите с помощью поставщика проверки подлинности hello выбранным и убедитесь, что заданы может tooaccess данные в виде прошедшего проверку подлинности пользователя.

## <a name="next-steps"></a>Дальнейшие действия
Завершения этого учебника обычной проверки подлинности, рассмотрите возможность продолжить на tooone из hello следующие учебники:

* [Добавить приложение tooyour уведомлений push](app-service-mobile-xamarin-forms-get-started-push.md)

  Узнайте, как push-уведомления tooadd поддерживают tooyour приложения и настройки вашего мобильного приложения серверной toouse концентраторов уведомлений Azure toosend push-уведомлений.
* [Включение автономной синхронизации для приложения](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  Узнайте, как автономные tooadd поддерживают приложения с помощью мобильного приложения серверной части. Автономная синхронизация позволяет конечным пользователям toointeract с мобильным приложением — Просмотр, добавление или изменение данных — даже в том случае, если нет сетевого соединения.

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
