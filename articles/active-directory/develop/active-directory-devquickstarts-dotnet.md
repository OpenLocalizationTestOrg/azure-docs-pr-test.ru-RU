---
title: "Приступая к работе .NET aaaAzure AD | Документы Microsoft"
description: "Как toobuild .NET классическое приложение Windows, интегрируется с Azure AD для входа и вызывает Azure AD защищен с помощью OAuth API-интерфейсы."
services: active-directory
documentationcenter: .net
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: ed33574f-6fa3-402c-b030-fae76fba84e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: c09b358f24c7bfb371b34cf72ca48c0a45042f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a>Интеграция Azure AD в классическое приложение Windows WPF
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Если вы разрабатываете приложение рабочей среды, Azure AD упрощает простыми и понятными для вас tooauthenticate пользователей с их учетными записями Active Directory.  Toosecurely вашего приложения также позволяет использовать любой веб-API, защищенные Azure AD, таких как hello API Office 365 или hello Azure API.

Для .NET собственных клиентов, которым требуется tooaccess защищенные ресурсы Azure AD предоставляет hello библиотеку аутентификации Active Directory или ADAL.  Единственной целью ADAL в жизни является toomake легко и маркеры доступа tooget вашего приложения.  toodemonstrate, насколько просто здесь мы создадим приложение .NET WPF задача список:

* Получает маркеры для вызова API Azure AD Graph hello, с помощью hello доступа [протокол проверки подлинности OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* Осуществляет поиск пользователей в каталоге по псевдониму.
* Обеспечивает функцию выхода пользователя из приложения.

toobuild hello полное рабочее приложение, вам потребуется:

1. Зарегистрировать приложение в Azure AD.
2. установить и настроить ADAL;
3. Используйте ADAL tooget токены из Azure AD.

tooget к работе, [загрузить каркас приложения hello](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) или [загрузить образец hello завершения](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).  Вам также потребуется клиент Azure AD, в котором можно создавать пользователей и регистрировать приложение.  Если у вас еще нет клиента, [Узнайте, как один tooget](active-directory-howto-tenant.md).

## <a name="1-register-hello-directorysearcher-application"></a>1. Регистрация приложения DirectorySearcher hello
tooenable маркеров tooget вашего приложения, сначала необходимо tooregister его в Azure AD клиента и предоставить ему разрешение tooaccess hello API Azure AD Graph:

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. На верхней панели hello, нажмите кнопку в вашей учетной записи, а также в разделе hello **каталога** выберите hello клиента Active Directory, где будут tooregister приложения.
3. Щелкните **более служб** в hello левую панель навигации и выберите **Azure Active Directory**.
4. Щелкните **Регистрация приложений** и нажмите кнопку **Добавить**.
5. Следуйте инструкциям hello и создайте новый **собственное клиентское приложение**.
  * Hello **имя** из hello приложения будет описывать tooend пользователей вашего приложения
  * Hello **Uri перенаправления** представляет собой комбинацию схему и строки, использование маркеров ответы tooreturn Azure AD.  Введите приложении tooyour определенного значения, например `http://DirectorySearcher`.
6. После завершения регистрации служба Azure AD присваивает приложению уникальный идентификатор приложения.  Это значение необходимо в следующих разделах hello, поэтому скопируйте его со страницы приложения hello.
7. Из hello **параметры** выберите **требуемые разрешения** и выберите **добавить**. Выберите hello **Microsoft Graph** как hello API и добавьте hello **чтение данных каталога** разрешение в списке **делегированные разрешения**.  Это позволит вашей hello tooquery приложения Graph API для пользователей.

## <a name="2-install--configure-adal"></a>2. Установка и настройка ADAL
Теперь, когда приложение зарегистрировано в Azure AD, можно установить библиотеку ADAL и написать код для работы с удостоверением.  Чтобы может toocommunicate ADAL toobe с Azure AD, необходимо tooprovide его с некоторые сведения о регистрации приложения.

* Сначала добавьте проект DirectorySearcher ADAL toohello с помощью консоли диспетчера пакетов hello.

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* В проекте DirectorySearcher hello откройте `app.config`.  Замените значения hello элементов hello в hello `<appSettings>` раздел tooreflect hello значения входных данных в hello портала Azure.  Ваш код будет ссылаться на эти значения при каждом использовании ADAL.
  * Hello `ida:Tenant` hello домен вашего клиента Azure AD, например, contoso.onmicrosoft.com
  * Hello `ida:ClientId` — hello clientId приложения скопирован с портала hello.
  * Hello `ida:RedirectUri` — hello зарегистрирован в портале hello URL-адрес перенаправления.

## <a name="3----use-adal-tooget-tokens-from-aad"></a>3.    Использование токенов ADAL tooGet из AAD
Hello базовый принцип ADAL — что всякий раз, когда ваше приложение должно маркер доступа, он просто вызывает `authContext.AcquireTokenAsync(...)`, и ADAL hello rest.  

* В hello `DirectorySearcher` откройте проект `MainWindow.xaml.cs` и найдите hello `MainWindow()` метод.  Hello первым шагом является tooinitialize приложения `AuthenticationContext` -ADAL основной класс.  Это происходит, где передается ADAL hello координаты, он должен toocommunicate с Azure AD и о том, как toocache маркеры.

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* Теперь найдите hello `Search(...)` метод, который вызывается, если пользователь cliks hello hello кнопки «Поиск» в пользовательском Интерфейсе приложения hello.  Этот метод делает tooquery toohello API Azure AD Graph запрос GET для пользователей, имя участника-пользователя начинается с заданного условия поиска hello.  Но в порядке tooquery hello Graph API, необходимо tooinclude access_token в hello `Authorization` заголовок hello запрос — где вступает в дело ADAL.

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate hello Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for hello tooDo item name");
        return;
    }

    // Get an Access Token for hello Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled hello sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* Когда приложение запрашивает маркер путем вызова `AcquireTokenAsync(...)`, ADAL попытается tooreturn маркер без запроса учетных данных пользователя hello.  Если ADAL определит, что данный пользователь hello должен toosign в tooget маркер, оно отображает диалоговое окно входа в систему, собирать hello учетные данные пользователя и возвращает токен после успешной проверки подлинности.  Если не удается tooreturn токен ADAL для какой-либо причине, он будет вызывать `AdalException`.
* Обратите внимание, что hello `AuthenticationResult` объект содержит `UserInfo` объект, который может быть toocollect используется информация приложения может потребоваться.  В hello DirectorySearcher `UserInfo` является приложение hello используется toocustomize пользовательского интерфейса с идентификатором hello пользователя.
* Hello пользователь нажимает кнопку «Выйти» hello, мы хотим tooensure, слишком hello следующего вызова`AcquireTokenAsync(...)` запросит toosign пользователя hello в.  С помощью ADAL это так же легко, как очистить кэш токена hello:

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear hello token cache
    authContext.TokenCache.Clear();

    ...
}
```

* Тем не менее если пользователь hello не нажать кнопку hello «Выход», требуется toomaintain hello пользовательский сеанс для hello очередном запуске hello DirectorySearcher.  При запуске приложения hello, могут возвращать кэш токена ADAL для существующего маркера и соответствующим образом обновить hello пользовательского интерфейса.  В hello `CheckForCachedToken()` метода, выполнение другого вызова слишком`AcquireTokenAsync(...)`, на этот раз, передавая hello `PromptBehavior.Never` параметра.  `PromptBehavior.Never`сообщает ADAL hello пользователь не должен появиться запрос для входа, которое ADAL следует вместо создания исключения, если это не удается tooreturn маркер.

```C#
public async void CheckForCachedToken() 
{
    // As hello application starts, try tooget an access token without prompting hello user.  If one exists, show hello user as signed in.
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Never));
    }
    catch (AdalException ex)
    {
        if (ex.ErrorCode != "user_interaction_required")
        {
            // An unexpected error occurred.
            MessageBox.Show(ex.Message);
        }

        // If user interaction is required, proceed toomain page without singing hello user in.
        return;
    }

    // A valid token is in hello cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

Поздравляем! Теперь имеют работающее приложение .NET WPF hello возможность tooauthenticate пользователей, безопасно вызвать веб-API с помощью OAuth 2.0 и получить основные сведения о пользователе hello.  Если это еще не сделано, пришло время toopopulate hello вашего клиента с некоторым пользователям.  Запустите свое приложение DirectorySearcher и войдите под именем одного из таких пользователей.  Осуществите поиск других пользователей по их имени участника-пользователя.  Закройте приложение hello и выполните его повторно.  Обратите внимание на то, как hello пользовательского сеанса остается без изменений.  Выйдите и снова войдите под именем другого пользователя.

ADAL упрощает легко tooincorporate все эти общие функции управления удостоверениями в приложения.  Он отвечает за всю работу dirty hello вам - управления кэша, поддержка протокола OAuth, предоставляя hello пользователя с именем входа пользовательского интерфейса, обновление маркеры с истекшим сроком действия и многое другое.  Действительно требуется tooknow всего в одном вызове API `authContext.AcquireTokenAsync(...)`.

Справочник по образец hello завершена (без настройки) предоставляется [здесь](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).  Теперь можно переходить на tooadditional сценариев.  Вы можете tootry:

[Защита веб-API с помощью Azure AD для .NET >>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

