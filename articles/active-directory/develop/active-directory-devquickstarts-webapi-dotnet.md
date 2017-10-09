---
title: "aaaAzure AD .NET, веб-API Приступая к работе | Документы Microsoft"
description: "Как toobuild веб-API .NET MVC, интегрируется с Azure AD для проверки подлинности и авторизации."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 67e74774-1748-43ea-8130-55275a18320f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 91c93e1fe18855f5648076e59e2ccf081eec34bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="help-protect-a-web-api-by-using-bearer-tokens-from-azure-ad"></a>Защита веб-API с помощью токенов носителя из Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

При создании приложения, которое предоставляет доступ tooprotected ресурсы, необходимые tooknow как tooprevent несанкционированному доступ к ресурсам toothose.
Azure Active Directory (Azure AD) позволяет легко и просто toohelp защитить веб-API с помощью маркера доступа OAuth 2.0 носителя с помощью всего нескольких строк кода.

В веб-приложениях ASP.NET такая защита можно выполнить с помощью реализации Microsoft hello hello сообщество ведет по промежуточного слоя OWIN включены в .NET Framework 4.5. Здесь мы будем использовать OWIN toobuild «tooDo список» веб-API:

* указывает, какие API защищены;
* Проверяет, что вызовы веб-API hello содержит действительный маркер доступа.

tooDo hello toobuild список API, сначала необходимо:

1. зарегистрировать приложение в Azure AD;
2. Настройка проверки подлинности конвейер OWIN hello hello приложения toouse.
3. Настройка клиентского приложения toocall hello веб-API.

tooget к работе, [загрузить каркас приложения hello](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/skeleton.zip) или [загрузить образец hello завершения](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip). Каждый из них является решением Visual Studio 2013. Необходимо также клиент Azure AD, в которой tooregister приложения. Если вы их еще нет, [Узнайте, как один tooget](active-directory-howto-tenant.md).

## <a name="step-1-register-an-application-with-azure-ad"></a>Шаг 1. Регистрация приложения в Azure AD
toohelp защитить приложение, сначала нужно toocreate приложения в клиенте и предоставить Azure AD несколько основные сведения.

1. Войдите в toohello [портал Azure](https://portal.azure.com).

2. На верхней панели hello выберите свою учетную запись. В hello **каталога** выберите клиента hello Azure AD, где требуется tooregister приложения.

3. Нажмите кнопку **более служб** в hello левой панели, а затем выберите **Azure Active Directory**.

4. Щелкните **Регистрация приложений**, а затем выберите **Добавить**.

5. Следуйте инструкциям hello и создайте новый **веб-приложение или веб-API**.
  * **Имя** описывает toousers вашего приложения. Введите **tooDo службы списка**.
  * **Uri перенаправления** представляет собой комбинацию схему и строки, используемый tooreturn все маркеры, запросил приложения Azure AD. Укажите `https://localhost:44321/` для этого параметра.

6. Из hello **параметры** -> **свойства** страницы приложения, обновите URI идентификатора приложения hello. Введите идентификатор конкретного клиента. Например, введите `https://contoso.onmicrosoft.com/TodoListService`.

7. Сохранение конфигурации hello. Не закрывайте портал hello, так как необходимо tooregister клиентского приложения вскоре.

## <a name="step-2-set-up-hello-app-toouse-hello-owin-authentication-pipeline"></a>Шаг 2: Настройка проверки подлинности конвейер OWIN hello hello приложения toouse
toovalidate входящие запросы и токены, необходимо tooset копирование toocommunicate вашего приложения в Azure AD.

1. toobegin, откройте решение hello и добавьте hello NuGet по промежуточного слоя OWIN пакеты проект TodoListService toohello с помощью консоли диспетчера пакетов hello.

    ```
    PM> Install-Package Microsoft.Owin.Security.ActiveDirectory -ProjectName TodoListService
    PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TodoListService
    ```

2. Добавить проект TodoListService запуска OWIN класса toohello вызывается `Startup.cs`.  Щелкните правой кнопкой мыши проект hello, выберите **добавить** > **новый элемент**и выполните поиск **OWIN**. по промежуточного слоя OWIN Hello будет вызывать hello `Configuration(…)` метод при запуске приложения.

3. Измените объявление класса hello слишком`public partial class Startup`. Часть этого класса уже была реализована в другом файле. В hello `Configuration(…)` метод, вызвать слишком`ConfgureAuth(…)` tooset проверку подлинности для веб-приложения.

    ```C#
    public partial class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            ConfigureAuth(app);
        }
    }
    ```

4. Привет открыть файл `App_Start\Startup.Auth.cs` и реализовать hello `ConfigureAuth(…)` метод. Здравствуйте, параметры, указываемые в `WindowsAzureActiveDirectoryBearerAuthenticationOptions` будет служить в качестве координат для toocommunicate вашего приложения в Azure AD.

    ```C#
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseWindowsAzureActiveDirectoryBearerAuthentication(
            new WindowsAzureActiveDirectoryBearerAuthenticationOptions
            {
                Audience = ConfigurationManager.AppSettings["ida:Audience"],
                Tenant = ConfigurationManager.AppSettings["ida:Tenant"]
            });
    }
    ```

5. Теперь вы можете использовать `[Authorize]` toohelp атрибуты защиты контроллеров и действий с помощью проверки подлинности носителя JSON Web Token (JWT). Украшение hello `Controllers\TodoListController.cs` класса с помощью тега authorize. Это заставит toosign пользователя hello в перед получением доступа к этой странице.

    ```C#
    [Authorize]
    public class TodoListController : ApiController
    {
    ```

    Когда вызывающий объект авторизованным успешно вызывает один hello `TodoListController` API-интерфейсы, действие hello может иметь доступа tooinformation о вызывающем модуле hello. OWIN предоставляет доступ toohello утверждения в маркер носителя hello через hello `ClaimsPrincpal` объекта.  

6. Общим требованием для веб-API — hello toovalidate «областей» присутствует в маркере hello. Это гарантирует, что этот пользователь hello согласился toohello разрешений требуется tooaccess hello tooDo службы списка.

    ```C#
    public IEnumerable<TodoItem> Get()
    {
        // user_impersonation is hello default permission exposed by applications in Azure AD
        if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "user_impersonation")
        {
            throw new HttpResponseException(new HttpResponseMessage {
              StatusCode = HttpStatusCode.Unauthorized,
              ReasonPhrase = "hello Scope claim does not contain 'user_impersonation' or scope claim not found"
            });
        }
        ...
    }
    ```

7. Откройте hello `web.config` файл в корне hello проект TodoListService hello и введите значения конфигурации в hello `<appSettings>` раздела.
  * `ida:Tenant`— имя вашего клиента Azure AD — например, contoso.onmicrosoft.com hello.
  * `ida:Audience`hello URI ИД приложения hello, введенного в hello портал Azure.

## <a name="step-3-configure-a-client-application-and-run-hello-service"></a>Шаг 3: Настройте клиентское приложение и запустить службу hello
Перед просмотром hello tooDo службы списка в действии, необходимо tooconfigure hello tooDo список клиентов, чтобы можно было получить токены из Azure AD и сделать службу toohello вызовы.

1. Вернитесь к предыдущему окну toohello [портал Azure](https://portal.azure.com).

2. Создайте новое приложение в клиенте Azure AD и выберите **собственное клиентское приложение** в результирующей строке hello.
  * **Имя** описывает toousers вашего приложения.
  * Введите `http://TodoListClient/` для hello **Uri перенаправления** значение.

3. После завершения регистрации Azure AD присваивает значение приложении tooyour приложения уникальный идентификатор. Это значение необходимо в следующих шагах hello, поэтому скопируйте его на приложение hello в окне.

4. Из hello **параметры** выберите **требуемые разрешения**, а затем выберите **добавить**. Найдите и выберите tooDo hello список служб, добавьте hello **TodoListService доступа** разрешение в списке **делегированные разрешения**, а затем нажмите кнопку **сделать**.

5. В Visual Studio откройте `App.config` в hello TodoListClient проекта, а затем введите значения конфигурации в hello `<appSettings>` раздела.

  * `ida:Tenant`— имя вашего клиента Azure AD — например, contoso.onmicrosoft.com hello.
  * `ida:ClientId`— Идентификатор приложения hello, скопированный из hello портал Azure.
  * `todo:TodoListResourceId`— URI идентификатора приложения hello tooDo приложения службы списка, введенное на портал Azure hello hello.

## <a name="next-steps"></a>Дальнейшие действия
Наконец, выполните очистку и сборку, а затем запустите каждый из проектов. Если это еще не сделано, пришло время toocreate hello нового пользователя в клиенте с *. onmicrosoft.com домена. Войдите в клиент список tooDo toohello с этим пользователем и добавить список дел toohello пользователей некоторые задачи.

Для ссылки, пример hello завершена (без настройки) доступен в [GitHub](https://github.com/AzureADQuickStarts/WebAPI-Bearer-DotNet/archive/complete.zip). Теперь можно переходить на сценариях toomore удостоверений.

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
