---
title: "aaaAdd tooa входа в веб-API .NET MVC с помощью hello конечная точка Azure AD v2.0 | Документы Microsoft"
description: "Как toobuild веб-Api .NET MVC, который принимает токены из обоих личную учетную запись Майкрософт и рабочих учетных записей."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: e77bc4e0-d0c9-4075-a3f6-769e2c810206
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 4e517145422bb6e9368e82a7eef4a5c57cce530a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-mvc-web-api"></a>Безопасность веб-API MVC
С конечной точкой v2.0 hello Azure Active Directory, чтобы защитить веб-API с помощью [OAuth 2.0](active-directory-v2-protocols.md) маркеры доступа, позволяя пользователей с обоих личную учетную запись Майкрософт и рабочих учетных записей toosecurely доступ к веб-API.

> [!NOTE]
> Не все сценарии Azure Active Directory и возможности поддерживаются hello v2.0 конечной точкой.  toodetermine, если необходимо использовать конечную точку v2.0 hello, прочтите сведения о [ограничения v2.0](active-directory-v2-limitations.md).
>
>

В веб-API ASP.NET это можно делать с помощью ПО промежуточного уровня OWIN корпорации Microsoft, включенного в .NET Framework 4.5.  Здесь мы будем использовать OWIN toobuild веб-API MVC «tooDo списка», позволяющую клиентам toocreate и чтения задачи в список дел пользователя.  Hello веб-API будет проверять входящие запросы содержат действительный маркер доступа и отклонять запросы, которые не прошли проверку на защищенном маршрут.  Этот пример создан с помощью Visual Studio 2015.

## <a name="download"></a>Загрузить
поддерживается Hello кода для этого учебника [на GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet).  можно toofollow вдоль [загрузить приложение hello основу как .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) или основу hello клона:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

каркас приложение Hello включает все hello стандартный код для простой API-Интерфейс, но не удалось обнаружить все компоненты, связанные с идентификаторами hello. Если вы не хотите toofollow вдоль, вместо этого можно клонировать или [загрузить образец hello завершения](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip).

```
git clone https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git
```

## <a name="register-an-app"></a>регистрация приложения;
Создайте приложение на странице [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) или выполните [эти подробные указания](active-directory-v2-app-registration.md).  Не забудьте:

* Копировать вниз hello **идентификатор приложения** назначены tooyour приложения, оно понадобится скоро.

В этом решении Visual Studio также содержится клиент TodoListClient, который представляет собой простое приложение WPF.  Hello TodoListClient является toodemonstrate используется как пользователь выполняет вход и каким образом клиент может выдавать запросы tooyour веб-API.  В этом случае hello TodoListClient и hello TodoListService представляются hello то же приложение.  tooconfigure Здравствуйте TodoListClient, также следует:

* Добавить hello **Mobile** платформы для приложения.

## <a name="install-owin"></a>Установка OWIN
Теперь, после регистрации приложения, нужно tooset копирование toocommunicate вашего приложения с конечной точкой v2.0 hello в порядке toovalidate входящие запросы и ответы маркеры.

* toobegin, откройте решение hello и добавьте hello OWIN по промежуточного слоя NuGet пакеты toohello TodoListService проекта с помощью консоли диспетчера пакетов hello.

```
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TodoListService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
PM> Install-Package Microsoft.IdentityModel.Protocol.Extensions -ProjectName TodoListService
```

## <a name="configure-oauth-authentication"></a>Настройка аутентификации OAuth 2.0
* Добавить проект TodoListService запуска OWIN класса toohello вызывается `Startup.cs`.  Щелкните правой кнопкой мыши на проекте hello--> **добавить** --> **новый элемент** --> Поиск «OWIN».  по промежуточного слоя OWIN Hello будет вызывать hello `Configuration(…)` метод при запуске приложения.
* Измените объявление класса hello слишком`public partial class Startup` -мы уже реализовали часть этого класса для вас в другом файле.  В hello `Configuration(…)` метод, сделать tooset tooConfgureAuth(...) вызов проверку подлинности для веб-приложения.

```C#
public partial class Startup
{
    public void Configuration(IAppBuilder app)
    {
        ConfigureAuth(app);
    }
}
```

* Привет открыть файл `App_Start\Startup.Auth.cs` и реализовать hello `ConfigureAuth(…)` метод, который будет Настройка маркеров tooaccept hello веб-API от конечной точки v2.0 hello.

```C#
public void ConfigureAuth(IAppBuilder app)
{
        var tvps = new TokenValidationParameters
        {
                // In this app, hello TodoListClient and TodoListService
                // are represented using hello same Application Id - we use
                // hello Application Id toorepresent hello audience, or the
                // intended recipient of tokens.

                ValidAudience = clientId,

                // In a real applicaiton, you might use issuer validation to
                // verify that hello user's organization (if applicable) has
                // signed up for hello app.  Here, we'll just turn it off.

                ValidateIssuer = false,
        };

        // Set up hello OWIN pipeline toouse OAuth 2.0 Bearer authentication.
        // hello options provided here tell hello middleware about hello type of tokens
        // that will be recieved, which are JWTs for hello v2.0 endpoint.

        // NOTE: hello usual WindowsAzureActiveDirectoryBearerAuthenticaitonMiddleware uses a
        // metadata endpoint which is not supported by hello v2.0 endpoint.  Instead, this
        // OpenIdConenctCachingSecurityTokenProvider can be used toofetch & use hello OpenIdConnect
        // metadata document.

        app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
        {
                AccessTokenFormat = new Microsoft.Owin.Security.Jwt.JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider("https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration")),
        });
}
```

* Теперь вы можете использовать `[Authorize]` атрибуты tooprotect контроллеров и действий с помощью проверки подлинности носителя OAuth 2.0.  Украшение hello `Controllers\TodoListController.cs` класса с помощью тега authorize.  Это заставит toosign пользователя hello в перед получением доступа к этой странице.

```C#
[Authorize]
public class TodoListController : ApiController
{
```

* Когда вызывающий объект авторизованным успешно вызывает один hello `TodoListController` API-интерфейсы, действие hello может иметь доступа tooinformation о вызывающем модуле hello.  OWIN предоставляет доступ toohello утверждения в маркер носителя hello через hello `ClaimsPrincpal` объекта.  

```C#
public IEnumerable<TodoItem> Get()
{
    // You can use hello ClaimsPrincipal tooaccess information about the
    // user making hello call.  In this case, we use hello 'sub' or
    // NameIdentifier claim tooserve as a key for hello tasks in hello data store.

    Claim subject = ClaimsPrincipal.Current.FindFirst(ClaimTypes.NameIdentifier);

    return from todo in todoBag
           where todo.Owner == subject.Value
           select todo;
}
```

* Наконец, откройте hello `web.config` файл в корне hello проект TodoListService hello и введите значения конфигурации в hello `<appSettings>` раздела.
  * Ваш `ida:Audience` — hello **идентификатор приложения** приложения hello, введенное на портале hello.

## <a name="configure-hello-client-app"></a>Настройка клиентского приложения hello
Чтобы увидеть hello службы Todo List в действии, необходимо tooconfigure hello Todo List Client, чтобы можно было получить токены из конечной точки v2.0 hello и сделать службу toohello вызовы.

* В проекте TodoListClient hello откройте `App.config` и введите значения конфигурации в hello `<appSettings>` раздела.
  * Ваш `ida:ClientId` идентификатор приложения, скопированные из портала hello.

Наконец, выполните очистку, соберите и запустите каждый из проектов.  Теперь у вас есть веб-API .NET MVC, принимающий маркеры доступа личных учетных записей Майкрософт, а также рабочих и учебных учетных записей.  Вход в hello TodoListClient и вызовите список дел web api tooadd задачи toohello конечных пользователей.

Справочник по hello выполнить пример (без настройки) [предоставляется как .zip здесь](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/complete.zip), или вы можете клонировать из GitHub:

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet.git```

## <a name="next-steps"></a>Дальнейшие действия
Теперь можно приступить к изучению других разделов.  Вы можете tootry:

[Вызов веб-API из веб-приложения >>](active-directory-v2-devquickstarts-webapp-webapi-dotnet.md)

Дополнительные ресурсы:

* [Руководство разработчика v2.0 Hello >>](active-directory-appmodel-v2-overview.md)
* [Тег StackOverflow "azure-active-directory" >>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a>Получение обновлений системы безопасности для наших продуктов
Мы рекомендуем вам уведомления при возникновении события безопасности, посетив tooget [эту страницу](https://technet.microsoft.com/security/dd252948) и подписка tooSecurity рекомендация предупреждения.
