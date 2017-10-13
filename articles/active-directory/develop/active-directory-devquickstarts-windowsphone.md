---
title: "Приступая к работе с Windows Phone Azure AD | Документация Майкрософт"
description: "Практическое руководство по созданию приложения Windows Phone, которое интегрируется с Azure AD для входа в систему и вызывает программные интерфейсы приложения, защищаемые системой Azure AD с помощью OAuth."
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
ms.openlocfilehash: 03c4b6d225dce99d79ef6c1ba2af43af8dea3eae
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a>Интеграция Azure AD с помощью приложения Windows Phone
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> Проекты для версии Windows Phone 8.1 и более ранних версий не поддерживаются в Visual Studio 2017.  Дополнительные сведения см. в статье [Целевая платформа и совместимость для Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

При разработке приложения Windows Phone 8.1 система Azure AD позволяет легко и просто осуществлять проверку подлинности пользователей с помощью их учетных записей в Active Directory.  Это также позволяет вашему приложению безопасно использовать любые веб-интерфейсы API, защищаемые с помощью Azure AD, например интерфейсы Office 365 API или Azure API.

> [!NOTE]
> Этот пример кода использует ADAL версии 2.0.  С учетом развития новейших технологий, возможно, вы захотите ознакомиться с нашим [учебником по универсальным приложениям Windows, использующим ADAL версии 3.0](active-directory-devquickstarts-windowsstore.md).  Если вы создаете приложение для Windows Phone 8.1, это то, что вам необходимо.  ADAL версии 2.0 по-прежнему полностью поддерживается и является рекомендуемым способом разработки приложений для Windows Phone 8.1 с использованием Azure AD.
> 
> 

Собственным клиентам .NET, которым необходим доступ к защищенным ресурсам, Azure AD предлагает использовать библиотеку проверки подлинности Active Directory (ADAL).  Единственное предназначение ADAL — упростить процесс получения маркеров доступа.  Чтобы продемонстрировать, насколько простой является данная процедура, мы выполним сборку приложения Windows Phone 8.1 «DirectorySearcher», которое:

* получает маркеры доступа для вызова интерфейса Graph API Azure AD с помощью [протокола проверки подлинности OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx);
* осуществляет поиск пользователей в каталоге с помощью заданного UPN;
* Обеспечивает функцию выхода пользователя из приложения.

Для создания полного рабочего приложения необходимо:

1. Зарегистрировать приложение в Azure AD.
2. установить и настроить ADAL;
3. использовать ADAL для получения маркеров из Azure AD.

Чтобы начать работу, [скачайте проект схемы](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) или [готовый пример](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).  Каждый из них является решением Visual Studio 2013.  Вам также потребуется клиент Azure AD, в котором можно создавать пользователей и регистрировать приложение.  Если клиента нет, [узнайте, как его получить](active-directory-howto-tenant.md).

## <a name="1-register-the-directory-searcher-application"></a>1. Регистрация приложения Directory Searcher
Чтобы приложение могло получать маркеры, сначала необходимо его зарегистрировать в клиенте Azure AD и предоставить ему разрешение на доступ к интерфейсу Graph API Azure AD.

1. Войдите на [портал Azure](https://portal.azure.com).
2. На верхней панели щелкните учетную запись и в списке **Каталог** выберите клиент Active Directory, в котором хотите зарегистрировать приложение.
3. В левой области навигации щелкните **Другие службы** и выберите **Azure Active Directory**.
4. Щелкните **Регистрация приложений** и нажмите кнопку **Добавить**.
5. Следуйте инструкциям на экране, а затем создайте новое **Собственное клиентское приложение**.
  * **Имя** приложения отображает его описание конечным пользователям.
  * **Uri перенаправления** представляет собой комбинацию схемы и строки, которую Azure AD будет использовать для возврата ответов на маркеры.  Введите значение заполнителя, например, `http://DirectorySearcher`.  Это значение мы заменим позже.
6. После завершения регистрации служба Azure AD присваивает приложению уникальный идентификатор приложения.  Это значение вам понадобится в следующих разделах, поэтому скопируйте его с вкладки приложения.
7. На странице **Параметры** выберите **Необходимые разрешения** и щелкните **Добавить**. Выберите **Microsoft Graph** в качестве интерфейса API и добавьте разрешение **Чтение данных каталога** в списке **Делегированные разрешения**.  Это позволит приложению запрашивать интерфейс Graph API для пользователей.

## <a name="2-install--configure-adal"></a>2) Установка и настройка ADAL
Теперь, когда приложение зарегистрировано в Azure AD, можно установить библиотеку ADAL и написать код для работы с удостоверением.  Чтобы ADAL могла обмениваться информацией с Azure AD, необходимо предоставить некоторую информацию о регистрации вашего приложения.

* Сначала добавьте ADAL в проект DirectorySearcher с помощью консоли диспетчера пакетов.

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* В проекте DirectorySearcher откройте `MainPage.xaml.cs`.  Замените значения в разделе `Config Values` , чтобы отразить значения, введенные на портале Azure.  Ваш код будет ссылаться на эти значения при каждом использовании ADAL.
  * `tenant` — это домен вашего клиента Azure AD, например contoso.onmicrosoft.com
  * `clientId` — это идентификатор clientId приложения, скопированный с портала.
* Теперь необходимо обнаружить uri обратного вызова для вашего приложения Windows Phone.  Установите точку останова в этой строке в методе `MainPage` :

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* Запустите приложение и скопируйте значение `redirectUri` при попадании в точку останова.  Оно должно иметь примерно следующий вид:

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* Вернитесь на вкладку **Настройка** своего приложения на портале управления Azure и вместо значения **RedirectUri** введите скопированное значение.  

## <a name="3-use-adal-to-get-tokens-from-aad"></a>3. Использование библиотеки ADAL для получения маркеров из AAD
Основной принцип ADAL состоит в следующем: каждый раз, когда вашему приложению необходим маркер доступа, оно будет просто вызывать `authContext.AcquireToken(…)`, а ADAL сделает все остальное.  

* Первый шаг состоит в инициализации `AuthenticationContext` приложения, что является основным классом ADAL.  Здесь вы отправляете в ADAL координаты, которые ему требуются для взаимодействия с Azure AD, и сообщаете о способе кэширования маркеров.

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* Теперь найдите метод `Search(...)` , который будет вызываться при нажатии кнопки "Поиск" в пользовательском интерфейсе приложения.  Этот метод выполняет запрос GET в интерфейс Graph API службы Azure AD для запроса списка пользователей, чьи UPN начинаются с данного слова поиска.  Но для отправки запросов в Graph API необходимо включить access_token в заголовок `Authorization` запроса — именно отсюда ADAL начинает свою работу.

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try to get a token without triggering any user prompt.
    // ADAL will check whether the requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained the QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* Если требуется интерактивная проверка подлинности, для отображения страницы входа в Azure AD ADAL будет использовать брокер веб-проверки подлинности (WAB) приложения Windows Phone и [модель продолжения](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) .  При входе пользователя приложение должно отправлять в ADAL результаты взаимодействия с WAB.  Это простая процедура, идентичная реализации интерфейса `ContinueWebAuthentication` :

```C#
// This method is automatically invoked when the application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass the authentication interaction results to ADAL, which will
    // conclude the token acquisition operation and invoke the callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* Теперь настало время использовать `AuthenticationResult` , которое ADAL вернуло в ваше приложение.  В обратном вызове `QueryGraph(...)` включите полученный маркер access_token в запрос GET в заголовке авторизации:

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If the error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add the access token to the Authorization Header of the call to the Graph API, and call the Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* Для отображения сведений о пользователе в вашем приложении также можно использовать объект `AuthenticationResult` . В методе `QueryGraph(...)` используйте результат для отображения на странице идентификатора пользователя:

```C#
// Update the Page UI to represent the signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* Наконец, для выхода пользователя из приложения также можно использовать ADAL.  Когда пользователь нажимает кнопку "Выход", необходимо убедиться, что при следующем вызове `AcquireTokenSilentAsync(...)` произойдет сбой.  Благодаря применению ADAL это будет так же просто, как и очистка кэша маркера:

```C#
private void SignOut()
{
    // Clear session state from the token cache.
    authContext.TokenCache.Clear();

    ...
}
```

Поздравляем! Теперь у нас есть рабочее приложение Windows Phone, которое позволяет проверять подлинность пользователей, безопасно вызывать веб-интерфейсы API с помощью OAuth 2.0 и получать основные сведения о пользователе.  Если вы это еще не сделали, сейчас можно добавить несколько пользователей вашему клиенту.  Запустите свое приложение DirectorySearcher и войдите под именем одного из таких пользователей.  Осуществите поиск других пользователей по их имени участника-пользователя.  Закройте приложение и снова его запустите.  Обратите внимание на то, что пользовательский сеанс не изменяется.  Выйдите и снова войдите под именем другого пользователя.

ADAL упрощает процесс включения всех этих общих возможностей идентификации в приложение.  Он отвечает за всю грязную работу: управление кэшем, поддержку протокола OAuth, предоставление пользователю пользовательского интерфейса для входа, обновление истекших маркеров и многое другое.  Все, что вам действительно нужно знать, — это вызов интерфейса API `authContext.AcquireToken*(…)`.

Для справки следует отметить, что готовый пример (без ваших значений конфигурации) находится [здесь](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).  Теперь можно приступить к дополнительным сценариям идентификации.  Можно попробовать:

[Защита веб-API с помощью Azure AD для .NET >>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

