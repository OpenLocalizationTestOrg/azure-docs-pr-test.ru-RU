---
title: "Приступая к работе Windows Phone AD aaaAzure | Документы Microsoft"
description: "Как toobuild приложения Windows Phone, который интегрируется с Azure AD для входа и вызывает Azure AD защищен с помощью OAuth API-интерфейсы."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 66f5ac20-5e1f-4b9d-bb99-9b3305e26416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: e766bfcdfae10483772154f4b5facdec05fc846f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a>Интеграция Azure AD с помощью приложения Windows Phone
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> Проекты для версии Windows Phone 8.1 и более ранних версий не поддерживаются в Visual Studio 2017.  Дополнительные сведения см. в статье [Целевая платформа и совместимость для Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

При разработке приложения Windows Phone 8.1, Azure AD позволяет простым и понятным для вас tooauthenticate пользователей с их учетными записями Active Directory.  Toosecurely вашего приложения также позволяет использовать любой веб-API, защищенные Azure AD, таких как hello API Office 365 или hello Azure API.

> [!NOTE]
> Этот пример кода использует ADAL версии 2.0.  Для hello новейшие технологии, вы можете tooinstead try нашей [универсальной учебника Windows с помощью ADAL v3.0](active-directory-devquickstarts-windowsstore.md).  При построении приложения для Windows Phone 8.1 на самом деле, это подходящее место hello.  ADAL v2.0 по-прежнему полностью поддерживаются, и является hello рекомендуемый способ agianst разработки приложений Windows Phone 8.1 с помощью Azure AD.
> 
> 

Для .NET собственных клиентов, которым требуется tooaccess защищенные ресурсы Azure AD предоставляет hello библиотеку аутентификации Active Directory или ADAL.  Единственной целью ADAL в жизни является toomake легко и маркеры доступа tooget вашего приложения.  toodemonstrate, насколько просто здесь мы выполним сборку «Directory модуль поиска» приложения Windows Phone 8.1:

* Получает маркеры для вызова API Azure AD Graph hello, с помощью hello доступа [протокол проверки подлинности OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* осуществляет поиск пользователей в каталоге с помощью заданного UPN;
* Обеспечивает функцию выхода пользователя из приложения.

toobuild hello полное рабочее приложение, вам потребуется:

1. Зарегистрировать приложение в Azure AD.
2. установить и настроить ADAL;
3. Используйте ADAL tooget токены из Azure AD.

запущена, tooget [загрузить каркас проекта](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) или [загрузить образец hello завершения](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).  Каждый из них является решением Visual Studio 2013.  Вам также потребуется клиент Azure AD, в котором можно создавать пользователей и регистрировать приложение.  Если у вас еще нет клиента, [Узнайте, как один tooget](active-directory-howto-tenant.md).

## <a name="1-register-hello-directory-searcher-application"></a>1. Регистрация hello Directory время приложения
tooenable маркеров tooget вашего приложения, сначала необходимо tooregister его в Azure AD клиента и предоставить ему разрешение tooaccess hello API Azure AD Graph:

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. На верхней панели hello, нажмите кнопку в вашей учетной записи, а также в разделе hello **каталога** выберите hello клиента Active Directory, где будут tooregister приложения.
3. Щелкните **более служб** в hello левую панель навигации и выберите **Azure Active Directory**.
4. Щелкните **Регистрация приложений** и нажмите кнопку **Добавить**.
5. Следуйте инструкциям hello и создайте новый **собственное клиентское приложение**.
  * Hello **имя** из hello приложения будет описывать tooend пользователей вашего приложения
  * Hello **Uri перенаправления** представляет собой комбинацию схему и строки, использование маркеров ответы tooreturn Azure AD.  Введите значение заполнителя, например, `http://DirectorySearcher`.  Это значение мы заменим позже.
6. После завершения регистрации служба Azure AD присваивает приложению уникальный идентификатор приложения.  Это значение необходимо в следующих разделах hello, поэтому скопируйте его с вкладка "приложение" hello.
7. Из hello **параметры** выберите **требуемые разрешения** и выберите **добавить**. Выберите hello **Microsoft Graph** как hello API и добавьте hello **чтение данных каталога** разрешение в списке **делегированные разрешения**.  Это позволит вашей hello tooquery приложения Graph API для пользователей.

## <a name="2-install--configure-adal"></a>2. Установка и настройка ADAL
Теперь, когда приложение зарегистрировано в Azure AD, можно установить библиотеку ADAL и написать код для работы с удостоверением.  Чтобы может toocommunicate ADAL toobe с Azure AD, необходимо tooprovide его с некоторые сведения о регистрации приложения.

* Сначала добавьте проект DirectorySearcher ADAL toohello с помощью консоли диспетчера пакетов hello.

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* В проекте DirectorySearcher hello откройте `MainPage.xaml.cs`.  Замените значения hello hello `Config Values` hello tooreflect области значений входных данных в hello портала Azure.  Ваш код будет ссылаться на эти значения при каждом использовании ADAL.
  * Hello `tenant` hello домен вашего клиента Azure AD, например, contoso.onmicrosoft.com
  * Hello `clientId` — hello clientId приложения скопирован с портала hello.
* Uri обратного вызова hello toodiscover теперь требуется для приложения Windows Phone.  Установите точку останова в этой строке в hello `MainPage` метод:

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* Выполните приложение hello и скопируйте выделенное значение hello `redirectUri` при попадании в точку останова hello.  Оно должно иметь примерно следующий вид:

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* Включите hello **Настройка** вкладка приложения hello портала управления Azure, замените значение hello hello **RedirectUri** с этим значением.  

## <a name="3-use-adal-tooget-tokens-from-aad"></a>3. Использование токенов ADAL tooGet из AAD
Hello базовый принцип ADAL — что всякий раз, когда ваше приложение должно маркер доступа, он просто вызывает `authContext.AcquireToken(…)`, и ADAL hello rest.  

* Hello первым шагом является tooinitialize приложения `AuthenticationContext` -ADAL основной класс.  Это происходит, где передается ADAL hello координаты, он должен toocommunicate с Azure AD и о том, как toocache маркеры.

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* Теперь найдите hello `Search(...)` метод, который вызывается, если пользователь cliks hello hello кнопки «Поиск» в пользовательском Интерфейсе приложения hello.  Этот метод делает tooquery toohello API Azure AD Graph запрос GET для пользователей, имя участника-пользователя начинается с заданного условия поиска hello.  Но в порядке tooquery hello Graph API, необходимо tooinclude access_token в hello `Authorization` заголовок hello запрос — где вступает в дело ADAL.

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try tooget a token without triggering any user prompt.
    // ADAL will check whether hello requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained hello QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* При необходимости в интерактивной проверки подлинности ADAL будет использовать Windows Phone Web Authentication Broker (адресной книги Windows) и [продолжения модели](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) страница входа toodisplay hello Azure AD.  При входе в систему пользователя hello, приложение должно toopass ADAL hello результаты взаимодействия адресной книги Windows hello.  Это сводится реализации hello `ContinueWebAuthentication` интерфейс:

```C#
// This method is automatically invoked when hello application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass hello authentication interaction results tooADAL, which will
    // conclude hello token acquisition operation and invoke hello callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* Теперь настало время hello toouse `AuthenticationResult` , ADAL, возвращается tooyour приложения.  В hello `QueryGraph(...)` обратного вызова, присоединение hello access_token вы приобрели toohello запрос GET в заголовке авторизации hello:

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add hello access token toohello Authorization Header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* Можно также использовать hello `AuthenticationResult` объекта toodisplay сведения о пользователе hello в вашем приложении. В hello `QueryGraph(...)` метод, используйте hello результат tooshow hello идентификатор пользователя на странице приветствия:

```C#
// Update hello Page UI toorepresent hello signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* Наконец можно использовать ADAL toosign hello выход пользователя из приложения, а также.  Hello пользователь нажимает кнопку «Выйти» hello, мы хотим tooensure, слишком hello следующего вызова`AcquireTokenSilentAsync(...)` завершится ошибкой.  С помощью ADAL это так же легко, как очистить кэш токена hello:

```C#
private void SignOut()
{
    // Clear session state from hello token cache.
    authContext.TokenCache.Clear();

    ...
}
```

Поздравляем! Теперь у рабочего приложения Windows Phone hello возможность tooauthenticate пользователей, безопасно вызвать веб-API с помощью OAuth 2.0 и получить основные сведения о пользователе hello.  Если это еще не сделано, пришло время toopopulate hello вашего клиента с некоторым пользователям.  Запустите свое приложение DirectorySearcher и войдите под именем одного из таких пользователей.  Осуществите поиск других пользователей по их имени участника-пользователя.  Закройте приложение hello и выполните его повторно.  Обратите внимание на то, как hello пользовательского сеанса остается без изменений.  Выйдите и снова войдите под именем другого пользователя.

ADAL упрощает легко tooincorporate все эти общие функции управления удостоверениями в приложения.  Он отвечает за всю работу dirty hello вам - управления кэша, поддержка протокола OAuth, предоставляя hello пользователя с именем входа пользовательского интерфейса, обновление маркеры с истекшим сроком действия и многое другое.  Действительно требуется tooknow всего в одном вызове API `authContext.AcquireToken*(…)`.

Справочник по образец hello завершена (без настройки) предоставляется [здесь](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).  Теперь можно переходить на сценариях tooadditional удостоверений.  Вы можете tootry:

[Защита веб-API с помощью Azure AD для .NET >>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

