---
title: "Приступая к работе магазина AD Windows aaaAzure | Документы Microsoft"
description: "Создание приложений Магазина Windows, которые интегрируются с Azure AD для входа в систему и вызывают интерфейсы API, защищенные Azure AD, с помощью OAuth."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 3b96a6d1-270b-4ac1-b9b5-58070c896a68
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 09/16/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 1d12c7b928bc0e94fb823f8db4a09ff416205e2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a>Интеграция Azure AD с приложениями Магазина Windows
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> Проекты для Магазина Windows 8.1 и более ранних версий не поддерживаются в Visual Studio 2017.  Дополнительные сведения см. в статье [Целевая платформа и совместимость для Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

При разработке приложений для магазина Windows hello, Azure Active Directory (Azure AD) упрощает простыми и понятными tooauthenticate пользователей с их учетными записями Active Directory. Путем интеграции с Azure AD, приложения могут безопасно использовать любой веб-API, который защищен службой Azure AD, например hello API Office 365 или hello Azure API.

Для классических приложений для магазина Windows, требующих tooaccess защищенные ресурсы Azure AD предоставляет hello библиотеку проверки подлинности Active Directory (ADAL). Цель Hello ADAL — toomake легко и маркеры доступа tooget приложения hello. примеры, в этой статье показано, как toobuild DirectorySearcher Windows хранения toodemonstrate приложения:

* Получает маркеры для вызова API Azure AD Graph hello с помощью hello доступа [протокол проверки подлинности OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* осуществляет поиск пользователей в каталоге с помощью заданного имени участника-пользователя (UPN);
* Обеспечивает функцию выхода пользователя из приложения.

## <a name="before-you-get-started"></a>Необходимые условия
* Загрузите hello [проект](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), или загрузить hello [полного примера](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip). Каждая из этих загрузок является решением Visual Studio 2015.
* Необходимо также клиент Azure AD в toocreate пользователей и зарегистрировать приложение hello. Если у вас еще нет клиента, [Узнайте, как один tooget](active-directory-howto-tenant.md).

Когда будете готовы, выполните процедуры hello в hello следующих трех разделах.

## <a name="step-1-register-hello-directorysearcher-app"></a>Шаг 1: Регистрация приложения hello DirectorySearcher
токены tooget приложения hello tooenable, необходимо сначала tooregister его в Azure AD для клиента и предоставить ему разрешение tooaccess hello API Azure AD Graph. Этот процесс описывается далее.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. На верхней панели hello выберите свою учетную запись. После этого в разделе hello **каталога** список, клиент Active Directory hello выберите нужное приложение hello tooregister.
3. Нажмите кнопку **более служб** в hello левой панели, а затем выберите **Azure Active Directory**.
4. Щелкните **Регистрация приложений**, а затем выберите **Добавить**.
5. Выполните запросы toocreate hello **собственное клиентское приложение**.
  * **Имя** описывает toousers приложения hello.
  * **URI перенаправления** представляет собой комбинацию схему и строки, Azure AD использует tooreturn маркера ответов. Введите значение заполнителя (например, **http://DirectorySearcher**). Позже вы замените значение hello.
6. После завершения регистрации hello Azure AD присваивает приложение hello уникальный идентификатор приложения. Скопируйте значение hello на hello **приложения** вкладки, так как он потребуется позже.
7. На hello **параметры** выберите **требуемые разрешения**, а затем выберите **добавить**.
8. Для hello **Azure Active Directory** приложения, выберите **Microsoft Graph** как hello API.
9. В разделе **делегированные разрешения**, добавить hello **доступ к каталогу hello как пользователя, выполнившего вход hello** разрешение. Таким образом приложение hello tooquery hello Graph API для пользователей.

## <a name="step-2-install-and-configure-adal"></a>Шаг 2. Установка и настройка ADAL
Теперь, когда приложение зарегистрировано в Azure AD, можно установить библиотеку ADAL и написать код для работы с удостоверением. ADAL toocommunicate tooenable с Azure AD, ей следует присвоить некоторые сведения о регистрации приложения hello.

1. Добавьте проект DirectorySearcher ADAL toohello с помощью консоли диспетчера пакетов hello.

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. В проекте DirectorySearcher hello откройте файл MainPage.xaml.cs.
3. Замените значения hello hello **значения конфигурации** область со значениями hello, введенным в hello портал Azure. Ваш код ссылается toothese значений при каждом использовании ADAL.
  * Hello *клиента* hello домен вашего клиента Azure AD (например, contoso.onmicrosoft.com).
  * Hello *clientId* — hello идентификатор клиента приложения hello, который копируется из портала hello.
4. Теперь необходимо toodiscover hello URI обратного вызова для приложения магазина Windows. Установите точку останова в этой строке в hello `MainPage` метод:
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. Выполните сборку решения hello, убедившись, что будут восстановлены все ссылки на пакет. Если отсутствуют любых пакетов, откройте диспетчер пакетов NuGet hello и восстановить их.
6. Выполните приложение hello и скопируйте значение hello `redirectUri` при попадании в точку останова hello. значение Hello должен выглядеть примерно hello следующим образом:

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. Включите hello **параметры** приложения hello в hello портал Azure, добавьте **RedirectUri** с предшествующей значение hello.  

## <a name="step-3-use-adal-tooget-tokens-from-azure-ad"></a>Шаг 3: Используйте ADAL tooget токены из Azure AD
Hello базовый принцип ADAL —, когда приложение hello требуется маркер доступа, он просто вызывает `authContext.AcquireToken(…)`, и ADAL hello rest.  

1. Инициализировать приложение hello `AuthenticationContext`, который является основной класс hello объекта ADAL. Это действие передает ADAL hello координаты требуются toocommunicate с Azure AD и о том, как toocache маркеры.

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. Найдите hello `Search(...)` метод, который вызывается, когда пользователь щелкает hello **поиска** кнопку в пользовательском Интерфейсе приложения hello. Этот метод делает tooquery toohello API Azure AD Graph запрос get для пользователей, имя участника-пользователя начинается с заданного условия поиска hello. hello tooquery Graph API включают маркер доступа в запросе hello **авторизации** заголовок. Вот где может пригодиться ADAL.

    ```C#
    private async void Search(object sender, RoutedEventArgs e)
    {
        ...
        AuthenticationResult result = null;
        try
        {
            result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectURI, new PlatformParameters(PromptBehavior.Auto, false));
        }
        catch (AdalException ex)
        {
            if (ex.ErrorCode != "authentication_canceled")
            {
                ShowAuthError(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    Когда приложение hello запрашивает маркер путем вызова `AcquireTokenAsync(...)`, ADAL пытается tooreturn маркер без запроса учетных данных пользователя hello. Если ADAL определит, что данный пользователь hello должен toosign в tooget маркера, отображает окно входа в диалоговом окне, собирает учетные данные пользователя hello и возвращает токен после успешной проверки подлинности. Если не удается tooreturn токен ADAL для какой-либо причине, hello *AuthenticationResult* находится в состоянии ошибки.
3. Теперь это маркер доступа hello toouse времени, вы приобрели. Также в hello `Search(...)` метода присоединения hello маркера toohello запроса получения Graph API в hello **авторизации** заголовка:

    ```C#
    // Add hello access token toohello Authorization header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. Можно использовать hello `AuthenticationResult` toodisplay сведения о пользователе hello в приложение hello, например идентификатор пользователя hello объекта:

    ```C#
    // Update hello page UI toorepresent hello signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. Также можно использовать ADAL toosign пользователей вне приложения hello. Когда пользователь hello выбирает hello **выйти** кнопку, убедитесь, что hello следующего вызова слишком`AcquireTokenAsync(...)` показано представление «вход». С ADAL это действие можно так же легко, как очистка кэша маркера hello:

    ```C#
    private void SignOut()
    {
        // Clear session state from hello token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a>Что дальше?
Теперь у вас есть рабочее приложение для магазина Windows, можно проверять подлинность пользователей, безопасно вызывать веб-API, с помощью OAuth 2.0 и получить основные сведения о пользователе hello.

Если уже еще не заполнены вашего клиента с пользователями, пришло время toodo hello таким образом.
1. Запуск приложения DirectorySearcher и затем войдите с помощью одного из пользователей hello.
2. Осуществите поиск других пользователей по их имени участника-пользователя.
3. Закройте приложение hello и перезапустить ее. Обратите внимание на то, как hello пользовательского сеанса остается без изменений.
4. Выйдите из системы, щелкнув правой кнопкой мыши горизонтальную полосу toodisplay hello и затем войдите как другой пользователь.

ADAL упрощает легко tooincorporate всех этих общих идентификаторов функций в приложение hello. Он отвечает за всю работу dirty hello, например для управления кэшем, поддержка протокола OAuth, предоставляя hello пользователя с именем входа пользовательского интерфейса, и обновление истек срок действия маркеров. Необходим вызов tooknow только один API-Интерфейс `authContext.AcquireToken*(…)`.

Для справки, загрузить hello [полного примера](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (без настройки).

Теперь можно переходить на сценариях tooadditional удостоверений. Например, попробуйте использовать [защиту веб-API для .NET с помощью Azure AD](active-directory-devquickstarts-webapi-dotnet.md).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
