---
title: "Приступая к работе AD Xamarin aaaAzure | Документы Microsoft"
description: "Создание приложений Xamarin, которые интегрируются с Azure AD для входа в систему и вызывают программные интерфейсы, защищенные Azure AD, с помощью OAuth."
services: active-directory
documentationcenter: xamarin
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 198cd2c3-f7c8-4ec2-b59d-dfdea9fe7d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 6a0d189648b7071558ac1cf2b908808668960a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a>Интеграция Azure AD с приложениями Xamarin
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Среда Xamarin позволяет создавать мобильные приложения на C#, которые могут работать в iOS, Android и Windows (на мобильных устройствах и ПК). При создании приложения с помощью Xamarin Azure Active Directory (Azure AD) позволяет пользователям простой tooauthenticate с их учетными записями Azure AD. приложение Hello может безопасно использовать любой веб-API, защищенные Azure AD, например hello API Office 365 или hello Azure API.

Для приложений Xamarin, требуется tooaccess защищенных ресурсов Azure AD предоставляет hello библиотеку проверки подлинности Active Directory (ADAL). Цель Hello ADAL — toomake легко и маркеры доступа tooget приложений. Это, в этой статье показано, как просто toodemonstrate как toobuild DirectorySearcher приложений:

* выполняются в iOS, Android, Windows Desktop, Windows Phone и Магазине Windows;
* Используйте отдельный класс переносимой библиотеки tooauthenticate пользователей и получить маркеры для hello API Azure AD Graph.
* осуществляют поиск пользователей в каталоге с помощью заданного имени участника-пользователя.

## <a name="before-you-get-started"></a>Необходимые условия
* Загрузите hello [проект](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), или загрузить hello [полного примера](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip). Каждая из этих загрузок является решением Visual Studio 2013.
* Необходимо также клиент Azure AD в toocreate пользователей и зарегистрировать приложение hello. Если у вас еще нет клиента, [Узнайте, как один tooget](active-directory-howto-tenant.md).

Когда будете готовы, выполните процедуры hello в hello рядом в четырех разделах.

## <a name="step-1-set-up-your-xamarin-development-environment"></a>Шаг 1. Настройка среды разработки Xamarin
Это руководство содержит проекты для iOS, Android и Windows, поэтому вам потребуются Visual Studio и Xamarin. toocreate hello необходимые среде процесс завершения hello в [задать Настройка и установка Visual Studio и Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) на сайте MSDN. Hello инструкциях содержатся материалы, вы можете просмотреть дополнительные сведения о Xamarin toolearn во время ожидания для завершения toobe установок hello.

После завершения установки hello, откройте hello решение в Visual Studio. Вы увидите шесть проектов: пять проектов для конкретной платформы и одну переносимую библиотеку классов DirectorySearcher.cs, которая будет общей для всех платформ.

## <a name="step-2-register-hello-directorysearcher-app"></a>Шаг 2: Регистрация приложения hello DirectorySearcher
токены tooget приложения hello tooenable, необходимо сначала tooregister его в Azure AD для клиента и предоставить ему разрешение tooaccess hello API Azure AD Graph. Этот процесс описывается далее.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. На верхней панели hello выберите свою учетную запись. После этого в разделе hello **каталога** список, клиент Active Directory hello выберите нужное приложение hello tooregister.
3. Нажмите кнопку **более служб** в hello левой панели, а затем выберите **Azure Active Directory**.
4. Щелкните **Регистрация приложений**, а затем выберите **Добавить**.
5. toocreate новый **собственное клиентское приложение**, следуйте инструкциям hello.
  * **Имя** описывает toousers приложения hello.
  * **URI перенаправления** представляет собой комбинацию схему и строки, Azure AD использует tooreturn маркера ответов. Введите значение (например, http://DirectorySearcher).
6. После завершения регистрации Azure AD присваивает приложение hello уникальный идентификатор приложения. Скопируйте значение hello из hello **приложения** вкладки, так как он потребуется позже.
7. На hello **параметры** выберите **требуемые разрешения**, а затем выберите **добавить**.
8. Выберите **Microsoft Graph** как hello API. В разделе **делегированные разрешения**, добавить hello **чтение данных каталога** разрешение.  
Это действие активирует приложение hello tooquery hello Graph API для пользователей.

## <a name="step-3-install-and-configure-adal"></a>Шаг 3. Установка и настройка ADAL
Теперь, когда приложение зарегистрировано в Azure AD, можно установить библиотеку ADAL и написать код для работы с удостоверением. ADAL toocommunicate tooenable с Azure AD, ей следует присвоить некоторые сведения о регистрации приложения hello.

1. Добавьте проект DirectorySearcher ADAL toohello с помощью консоли диспетчера пакетов hello.

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirectorySearcherLib
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Android
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Desktop
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-iOS
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Universal
    `

    Обратите внимание, что две ссылки на библиотеки добавлены tooeach проекта: hello PCL часть ADAL и часть, специфический для платформы.
2. В проекте DirectorySearcherLib hello откройте DirectorySearcher.cs.
3. Замените значения членов класса hello hello значениями, указанными в hello портал Azure. Ваш код ссылается toothese значений при каждом использовании ADAL.

  * Hello *клиента* hello домен вашего клиента Azure AD (например, contoso.onmicrosoft.com).
  * Hello *clientId* — hello идентификатор клиента приложения hello, который копируется из портала hello.
  * Hello *returnUri* hello перенаправления URI, введенное на портале hello (например, http://DirectorySearcher).

## <a name="step-4-use-adal-tooget-tokens-from-azure-ad"></a>Шаг 4: Используйте ADAL tooget токены из Azure AD
Большая часть логики проверки подлинности приложение hello заключается в `DirectorySearcher.SearchByAlias(...)`. Все, что является необходимым в проекты под конкретные платформы hello — toopass toohello параметра `DirectorySearcher` PCL.

1. Откройте DirectorySearcher.cs, а затем добавьте новый параметр toohello `SearchByAlias(...)` метод. `IPlatformParameters`является hello параметра, инкапсулирующий hello платформой объекты, что проверка подлинности ADAL потребности tooperform hello.

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. Инициализировать `AuthenticationContext`, который является основной класс hello объекта ADAL.  
Это ADAL hello передает действие координат его toocommunicate потребности в Azure AD.
3. Вызовите `AcquireTokenAsync(...)`, который принимает hello `IPlatformParameters` объекта и вызывает hello поток проверки подлинности, необходимые tooreturn приложения маркера toohello.

    ```C#
    ...
        AuthenticationResult authResult = null;
        try
        {
            AuthenticationContext authContext = new AuthenticationContext(authority);
            authResult = await authContext.AcquireTokenAsync(graphResourceUri, clientId, returnUri, parent);
        }
        catch (Exception ee)
        {
            results.Add(new User { error = ee.Message });
            return results;
        }
    ...
    ```

    `AcquireTokenAsync(...)`Первый tooreturn попыток маркер для hello запрашиваемый ресурс (hello Graph API в данном случае) без запроса учетных данных (через кэширование или обновление старых токены) tooenter пользователей. При необходимости он показывает пользователей hello Azure AD на странице входа перед установкой hello запрошенного токена.
4. Присоединение hello запрос Graph API toohello токена доступа в hello **авторизации** заголовка:

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

Вот и все для hello `DirectorySearcher` PCL и hello код приложения связанные с идентификаторами. Осталось toocall hello `SearchByAlias(...)` метод в представлениях для каждой платформы и, при необходимости, tooadd кода для правильной обработки hello жизненного цикла пользовательского интерфейса.

### <a name="android"></a>Android
1. В MainActivity.cs, добавьте вызов слишком`SearchByAlias(...)` обработчика щелчка кнопки hello:

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. Переопределить hello `OnActivityResult` tooforward жизненного цикла метод проверки подлинности перенаправляет задней toohello соответствующий метод. Для этого ADAL предоставляет вспомогательный метод в Android:

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a>Классические приложения
В MainWindow.xaml.cs звонок слишком`SearchByAlias(...)` , передав `WindowInteropHelper` в hello desktop `PlatformParameters` объекта:

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a>iOS
Здравствуйте, операций ввода-вывода в DirSearchClient_iOSViewController.cs, `PlatformParameters` объект принимает ссылку toohello View Controller:

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a>Windows Universal
В универсальное приложение для Windows, откройте файл MainPage.xaml.cs, а затем реализуйте hello `Search` метод. Этот метод использует вспомогательный метод в общий проект tooupdate пользовательского интерфейса, при необходимости.

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a>Что дальше?
Теперь у нас есть рабочее приложение Xamarin, которое позволяет проверять подлинность пользователей и безопасным образом вызывать веб-интерфейсы API с помощью OAuth 2.0 на пяти различных платформах.

Если уже еще не заполнены вашего клиента с пользователями, пришло время toodo hello таким образом.

1. Запуск приложения DirectorySearcher и затем войдите с помощью одного из пользователей hello.
2. Осуществите поиск других пользователей по их имени участника-пользователя.

ADAL упрощает легко tooincorporate общие функции управления удостоверениями в приложение hello. Он отвечает за всю работу dirty hello, например для управления кэшем, поддержка протокола OAuth, предоставляя hello пользователя с именем входа пользовательского интерфейса, и обновление истек срок действия маркеров. Необходим вызов tooknow только один API-Интерфейс `authContext.AcquireToken*(…)`.

Для справки, загрузить hello [полного примера](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (без настройки).

Теперь можно переходить на сценариях tooadditional удостоверений. Например, попробуйте использовать [защиту веб-API для .NET с помощью Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
