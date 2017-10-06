---
title: "aaaAzure AD B2C | Документы Microsoft"
description: "Как toobuild веб-API .NET с помощью Azure Active Directory B2C безопасность с помощью маркера доступа OAuth 2.0 для проверки подлинности."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: d45364216deda38ef44b60dd11e86d9a089ad509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a>Azure Active Directory B2C: создание веб-API .NET

С помощью Azure Active Directory (Azure AD) B2C можно защитить веб-API с помощью маркера доступа OAuth 2.0. Эти маркеры позволяют ваш клиент toohello tooauthenticate приложения API. В этой статье показано, как toocreate API .NET MVC «список дел», которая позволяет пользователям клиента tooCRUD задач приложения. веб-API Hello защищается с помощью Azure AD B2C и позволяет toomanage прошедшим проверку пользователям только их список дел.

## <a name="create-an-azure-ad-b2c-directory"></a>Создание каталога Azure AD B2C

Перед использованием Azure AD B2C необходимо создать каталог или клиент. Каталог — это контейнер для данных всех ваших пользователей, приложений, групп и т. д. Прежде чем продолжать работу с руководством, [создайте каталог B2C](active-directory-b2c-get-started.md), если вы его еще не создали.

> [!NOTE]
> клиентское приложение Hello и веб-API необходимо использовать каталог B2C hello же Azure AD.
>

## <a name="create-a-web-api"></a>Создание веб-API

Далее необходимо toocreate API веб-приложения в каталоге B2C. Это дает сведения о Azure AD, что его нуждается toosecurely взаимодействовать с приложением. toocreate приложения, выполните [эти инструкции](active-directory-b2c-app-registration.md). Не забудьте сделать следующее.

* Включить **веб-приложения** или **веб-API** в приложение hello.
* Используйте hello **URI перенаправления** `https://localhost:44332/` для веб-приложения hello. Это расположение по умолчанию hello hello веб-приложение клиента для этого примера кода.
* Копировать hello **идентификатор приложения** , назначенный tooyour приложения. Он понадобится вам позднее.
* Введите идентификатор приложения в поле **URI кода приложения**.
* Добавить разрешения с помощью hello **публикации областей** меню.

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Создание политик

В Azure AD B2C любое взаимодействие с пользователем определяется [политикой](active-directory-b2c-reference-policies.md). Вам потребуется toocreate toocommunicate политики с Azure AD B2C. Рекомендуется с помощью hello политики регистрации-повышение или вход в сочетании, как описано в hello [статье политики](active-directory-b2c-reference-policies.md). При создании политики обязательно сделайте следующее:

* В политике укажите **отображаемое имя** и другие атрибуты регистрации.
* В каждой политике в качестве утверждения приложения выберите утверждения **Отображаемое имя** и **Идентификатор объекта**. Можно также выбрать другие утверждения.
* Копировать hello **имя** каждой политики, после его создания. Имя политики hello потребуется позднее.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

После успешного создания политики hello вы будете готовы toobuild приложения.

## <a name="download-hello-code"></a>Загрузка кода hello

Hello кода для этого учебника, сохраняется на [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). Образец hello можно клонировать, выполнив:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

После загрузки кода образца hello запущен tooget файл .sln Visual Studio откройте hello. Hello файл решения содержит два проекта: `TaskWebApp` и `TaskService`. `TaskWebApp`— веб-приложение MVC, hello пользователь взаимодействует с. `TaskService`— приложение hello фоновая веб-API, который хранит список дел каждого пользователя. В этой статье рассматривается hello `TaskService` приложения. toolearn как toobuild `TaskWebApp` с помощью Azure AD B2C, в разделе [наш учебник по .NET web app](active-directory-b2c-devquickstarts-web-dotnet-susi.md).

### <a name="update-hello-azure-ad-b2c-configuration"></a>Обновите конфигурацию hello Azure AD B2C

Выборка — настроенное toouse hello политик и клиент идентификатор нашей демонстрационному клиенту. Если вы хотите toouse клиента, необходимо будет hello toodo следующие:

1. Откройте `web.config` в hello `TaskService` проекта и замените значения hello
    * `ida:Tenant` именем своего клиента;
    * `ida:ClientId` идентификатором клиента для приложения веб-API;
    * `ida:SignUpSignInPolicyId` именем политики регистрации и входа в систему;

2. Откройте `web.config` в hello `TaskWebApp` проекта и замените значения hello
    * `ida:Tenant` именем своего клиента;
    * `ida:ClientId` идентификатором клиента для веб-приложения;
    * `ida:ClientSecret` секретным ключом веб-приложения;
    * `ida:SignUpSignInPolicyId` именем политики регистрации и входа в систему;
    * `ida:EditProfilePolicyId` именем политики "Изменение профиля";
    * `ida:ResetPasswordPolicyId` именем политики "Сброс профиля".


## <a name="secure-hello-api"></a>Защита hello API

Теперь, когда у вас есть клиент, который вызывает API, можно защитить API (например, `TaskService`) с помощью токенов носителя OAuth 2.0. Это гарантирует, что каждый запрос tooyour API будет действителен только если hello запрос содержит токен носителя. API может принимать и проверять токены носителя с помощью библиотеки OWIN от Майкрософт.

### <a name="install-owin"></a>Установка OWIN

Перед началом установки hello конвейера проверки подлинности OWIN OAuth с помощью hello консоль диспетчера пакетов Visual Studio.

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

Будет выполнена установка hello OWIN по промежуточного слоя, будут приниматься и проверяться токены носителя.

### <a name="add-an-owin-startup-class"></a>Добавление класса запуска OWIN

Добавление toohello класс запуска OWIN API с именем `Startup.cs`.  Правой кнопкой мыши проект hello, выберите **добавить** и **новый элемент**и выполните поиск OWIN. по промежуточного слоя OWIN Hello будет вызывать hello `Configuration(…)` метод при запуске приложения.

В нашем примере мы изменили объявление класса hello слишком`public partial class Startup` и реализации hello hello класса в другой части `App_Start\Startup.Auth.cs`. Внутри hello `Configuration` метод, мы добавили вызов слишком`ConfigureAuth`, которая определена в `Startup.Auth.cs`. После изменения hello `Startup.cs` выглядит как hello следующее:

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a>Настройка проверки подлинности OAuth 2.0

Привет открыть файл `App_Start\Startup.Auth.cs`и реализовать hello `ConfigureAuth(...)` метод. Например он может выглядеть hello следующим образом:

```CSharp
// App_Start\Startup.Auth.cs

 public partial class Startup
    {
        // These values are pulled from web.config
        public static string AadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
        public static string Tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        public static string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
        public static string SignUpSignInPolicy = ConfigurationManager.AppSettings["ida:SignUpSignInPolicyId"];
        public static string DefaultPolicy = SignUpSignInPolicy;

        /*
         * Configure hello authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where hello audience of hello token is equal toohello client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches hello Azure AD B2C metadata & signing keys from hello OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-hello-task-controller"></a>Контроллер задач безопасного hello

После проверки подлинности настроенных toouse OAuth 2.0, приложение hello можно защитить web API, добавив `[Authorize]` контроллер задач toohello тег. Это контроллер hello, где все операции списка задач выполняется, поэтому необходимо обеспечить безопасность всей контроллера hello на уровне класса hello. Можно также добавить hello `[Authorize]` тег действия tooindividual для более точное управление.

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a>Получение сведений о пользователе из hello маркера

`TasksController`сохраняет задачи в базе данных, где каждый объект имеет связанный пользователь «владеет» задачу hello. Владелец Hello идентифицируется hello пользователя **идентификатор объекта**. (Вот почему требуется идентификатор tooadd hello объекта, как приложение утверждения во всех политик.)

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a>Проверки разрешений hello в маркере hello

Общим требованием для веб-API — hello toovalidate «областей» присутствует в маркере hello. Это гарантирует, что этой hello пользователь согласился службы списка дел hello необходимые tooaccess toohello разрешения.

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "hello Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-hello-sample-app"></a>Запуск образца приложения hello

Наконец, выполните сборку и запустите `TaskWebApp` и `TaskService`. Создавать некоторые задачи в список дел пользователя hello и обратите внимание на то, как они сохраняются в hello API даже после остановки и перезапуска hello клиента.

## <a name="edit-your-policies"></a>Изменение политик

После защиты API с помощью Azure AD B2C можно поэкспериментировать с знак в-регистрации-повышение политики и представления эффекты hello (или его отсутствие) на hello API. Можно управлять утверждений приложения hello в политиках hello и изменение сведений о пользователе hello, доступные в hello веб-API. Все добавленные утверждения будут доступных tooyour .NET MVC веб-API в hello `ClaimsPrincipal` объекта, как описано ранее в этой статье.
