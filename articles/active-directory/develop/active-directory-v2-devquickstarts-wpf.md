---
title: "Active Directory aaaAzure v2.0 собственное приложение .NET | Документы Microsoft"
description: "Как toobuild собственное приложение .NET, подписывает пользователей обоих личную учетную запись Майкрософт и рабочих учетных записей."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 46d81e09-bad0-44ce-9026-881805976e72
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/30/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 9418eeba02b800feee5cb00219574eb16506f0a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-windows-desktop-app"></a>Добавить tooa входа в приложение рабочего стола Windows
С конечной точкой v2.0 hello hello можно быстро добавлять проверки подлинности tooyour классических приложений с помощью поддержки для обоих личные учетные записи Майкрософт и рабочих учетных записей.  Он также позволяет взаимодействовать toosecurely вашего приложения с серверной части веб-api, а также [hello Microsoft Graph](https://graph.microsoft.io) и несколько hello [API-интерфейсы Office 365 единой](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).

> [!NOTE]
> Не все сценарии Azure Active Directory (AD) и функции поддерживаются hello v2.0 конечной точкой.  toodetermine, если необходимо использовать конечную точку v2.0 hello, прочтите сведения о [ограничения v2.0](active-directory-v2-limitations.md).
> 
> 

Для [.NET собственных приложений на устройстве](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD предоставляет hello библиотеки проверки подлинности удостоверений Microsoft или MSAL.  Единственной целью MSAL элемента в жизни является toomake легким для вашего приложения tooget токены для вызова веб-служб.  toodemonstrate, насколько просто здесь мы создадим приложение .NET WPF задача список:

* Подписывает hello пользователя в & получает доступ к маркеры с помощью hello [протокол проверки подлинности OAuth 2.0](active-directory-v2-protocols.md).
* безопасно вызывает серверную веб-службу списка дел, которая также защищена OAuth 2.0.
* Подписывает hello пользователя.

## <a name="download-sample-code"></a>Скачивание примера кода
поддерживается Hello кода для этого учебника [на GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).  можно toofollow вдоль [загрузить приложение hello основу как .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) или основу hello клона:

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

в конце hello в учебнике также предоставляется приложение Hello завершена.

## <a name="register-an-app"></a>регистрация приложения;
Создайте приложение на странице [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) или выполните [эти подробные указания](active-directory-v2-app-registration.md).  Не забудьте:

* Копировать вниз hello **идентификатор приложения** назначены tooyour приложения, оно понадобится скоро.
* Добавить hello **Mobile** платформы для приложения.

## <a name="install--configure-msal"></a>Установка и настройка MSAL
Ваше приложение зарегистрировано в Майкрософт. Теперь вы можете установить MSAL и написать собственный код для работы с удостоверением.  Чтобы MSAL toobe может toocommunicate hello v2.0 конечной точки, необходимо tooprovide его с некоторые сведения о регистрации приложения.

* Начните с добавления MSAL toohello TodoListClient проекта с помощью консоли диспетчера пакетов hello.

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* В проекте TodoListClient hello откройте `app.config`.  Замените значения hello элементов hello в hello `<appSettings>` раздел tooreflect hello значения входных данных в портал регистрации приложения hello.  Код будет использовать эти значения при каждом обращении к библиотеке MSAL.
  
  * Hello `ida:ClientId` — hello **идентификатор приложения** приложения скопирован с портала hello.
* В проекте hello TodoList службы откройте `web.config` в корневом каталоге hello hello проекта.  
  
  * Замените hello `ida:Audience` значение с hello же **идентификатор приложения** из портала hello.

## <a name="use-msal-tooget-tokens"></a>Использование маркеров tooget MSAL
Hello базовый принцип MSAL — всякий раз, когда ваше приложение должно маркер доступа, просто вызвать метод `app.AcquireToken(...)`, и MSAL hello rest.  

* В hello `TodoListClient` откройте проект `MainWindow.xaml.cs` и найдите hello `OnInitialized(...)` метод.  Hello первым шагом является tooinitialize приложения `PublicClientApplication` -MSAL в основной класс, представляющий приложений в машинном коде.  Это происходит, где передается MSAL hello координаты, он должен toocommunicate с Azure AD и о том, как toocache маркеры.

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* При запуске приложение hello, мы должны toocheck и см. Если hello пользователь уже выполнил вход в приложение hello.  Тем не менее мы не хотим tooinvoke пользовательский Интерфейс входа в систему, пока: мы выполним hello пользователя нажмите кнопку «Вход» toodo таким образом.  Кроме того, в hello `OnInitialized(...)` метод:

```C#
// As hello app starts, we want toocheck toosee if hello user is already signed in.
// You can do so by trying tooget a token from MSAL, using hello method
// AcquireTokenSilent.  This forces MSAL toothrow an exception if it cannot
// get a token for hello user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in hello cache - or MSAL was able tooget a new oen via refresh token.
    // Proceed toofetch hello user's tasks from hello TodoListService via hello GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, hello app should take no action,
        // and simply show hello user hello sign in button.
    }
    else
    {
        // Here, we catch all other MsalExceptions
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
}

```

* Если hello пользователь не выполнил вход и нажатии кнопки «Вход» hello, мы должны tooinvoke пользовательский Интерфейс входа и введите свои учетные данные пользователя hello.  Реализация обработчика кнопки hello вход:

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign hello user out if they clicked hello "Clear Cache" button

// If hello user clicked hello 'Sign-In' button, force
// MSAL tooprompt hello user for credentials by using
// AcquireTokenAsync, a method that is guaranteed tooshow a prompt toohello user.
// MSAL will get a token for hello TodoListService and cache it for you.

AuthenticationResult result = null;
try
{
    result = await app.AcquireTokenAsync(new string[] { clientId });
    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    // If MSAL cannot get a token, it will throw an exception.
    // If hello user canceled hello login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by hello user");
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }

        MessageBox.Show(message);
    }

    return;
}


}
```

* Если hello пользователь успешно выполняет вход, MSAL будет получать и кэшировать маркер для вас и продолжением toocall hello `GetTodoList()` метод уверенно.  Все, что покинул tooget задачи пользователя — tooimplement hello `GetTodoList()` метод.

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try tooget an access token toocall hello TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL toothrow an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show hello user a message
    // and let them click hello Sign-In button.

    if (ex.ErrorCode == "user_interaction_required")
    {
        MessageBox.Show("Please sign in first");
        SignInButton.Content = "Sign In";
    }
    else
    {
        // In any other case, an unexpected error occurred.

        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }

    return;
}

// Once hello token has been returned by MSAL,
// add it toohello http authorization header,
// before making hello call tooaccess hello tooDo list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When hello user is done managing their To-Do List, they may finally sign out of hello app by clicking hello "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If hello user clicked hello 'clear cache' button,
        // clear hello MSAL token cache and show hello user as signed out.
        // It's also necessary tooclear hello cookies from hello browser
        // control so hello next user has a chance toosign in.

        if (SignInButton.Content.ToString() == "Clear Cache")
        {
                TodoList.ItemsSource = string.Empty;
                app.UserTokenCache.Clear(app.ClientId);
                ClearCookies();
                SignInButton.Content = "Sign In";
                return;
        }

        ...
```

## <a name="run"></a>Выполнить
Поздравляем! Теперь есть рабочее приложение .NET WPF hello возможность tooauthenticate пользователей & безопасно вызывать веб-API с помощью OAuth 2.0.  Запустите оба проекта и выполните вход с личной учетной записью Майкрософт, рабочей или учебной учетной записью.  Добавьте список дел задачи toothat пользователя.  Выйдите из системы и войти как другой пользователь tooview их список дел.  Закройте приложение hello и выполните его повторно.  Обратите внимание на то, как hello пользовательского сеанса остается без изменений — это потому, что приложение hello кэширует маркеры в локальном файле.

MSAL позволяет легко tooincorporate общие функции управления удостоверениями в приложения, использование личных и рабочих учетных записей.  Он отвечает за всю работу dirty hello вам - управления кэша, поддержка протокола OAuth, предоставляя hello пользователя с именем входа пользовательского интерфейса, обновление маркеры с истекшим сроком действия и многое другое.  Действительно требуется tooknow всего в одном вызове API `app.AcquireTokenAsync(...)`.

Справочник по hello выполнить пример (без настройки) [предоставляется как .zip здесь](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), или вы можете клонировать из GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a>Дальнейшие действия
Теперь можно перейти к более сложным темам.  Вы можете tootry:

* [Обеспечение безопасности hello TodoListService веб-API с конечной точкой v2.0 hello](active-directory-v2-devquickstarts-dotnet-api.md)

Дополнительные ресурсы:  

* [Руководство разработчика v2.0 Hello >>](active-directory-appmodel-v2-overview.md)
* [Тег "msal" на StackOverflow >>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a>Получение обновлений системы безопасности для наших продуктов
Мы рекомендуем вам уведомления при возникновении события безопасности, посетив tooget [эту страницу](https://technet.microsoft.com/security/dd252948) и подписка tooSecurity рекомендация предупреждения.

