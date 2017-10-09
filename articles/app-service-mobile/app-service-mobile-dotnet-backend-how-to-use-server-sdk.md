---
title: "toowork aaaHow с сервера базы данных hello .NET SDK для мобильных приложений | Документы Microsoft"
description: "Узнайте, как toowork с hello внутреннего сервера .NET SDK для мобильных приложений службы приложения Azure."
keywords: "служба приложений, служба приложений azure, мобильное приложение, мобильная служба, масштабировать, масштабируемый, разработка приложений, разработка приложений azure"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0620554f-9590-40a8-9f47-61c48c21076b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2946c5ba4424565ac764e2ce5597bf42362fcedf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-hello-net-backend-server-sdk-for-azure-mobile-apps"></a>Работать с сервера базы данных hello .NET SDK для мобильных приложений Azure
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

В этом разделе показано, как toouse hello внутреннему серверу .NET SDK в основные сценарии мобильные приложения службы приложений Azure. пакет SDK Azure Mobile приложения Hello предназначенный для работы с мобильными клиентами из приложения ASP.NET.

> [!TIP]
> Hello [сервер .NET SDK для мобильных приложений Azure] [ 2] является открытым исходным кодом на сайте GitHub. репозиторий Hello содержит все исходного кода, включая набор модульных тестов hello всего сервера SDK и некоторые образцы проектов.
>
>

## <a name="reference-documentation"></a>Справочная документация
Hello справочную документацию по SDK сервера hello находится здесь: [Справочник по Azure мобильных приложений .NET][1].

## <a name="create-app"></a>Практическое руководство. Создание серверной части мобильного приложения .NET
При запуске нового проекта, можно создать приложение службы приложений с помощью либо hello [портал Azure] или Visual Studio. Можно выполнить локально hello приложения служб приложений или опубликовать hello проекта tooyour облачного приложения-службы мобильного приложения.

При добавлении существующего проекта tooan возможности мобильных устройств в разделе hello [загрузки и инициализации hello SDK](#install-sdk) раздела.

### <a name="create-a-net-backend-using-hello-azure-portal"></a>Создание серверной части .NET с помощью портала Azure hello
toocreate мобильного внутреннего сервера приложения службы, либо выполните hello [учебника] [ 3] или выполните следующие действия:

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

В hello *приступить к работе* колонки в разделе **создать таблицу API**, выберите **C#** как вашей **языка серверной**. Нажмите кнопку **загрузки**извлечения локального компьютера проекта сжатые файлы tooyour и откройте решение hello в Visual Studio.

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a>Создание серверной части .NET с помощью Visual Studio 2013 и Visual Studio 2015
Установка hello [Azure SDK для .NET] [ 4] (версии 2.9.0 или более поздней версии) toocreate проект мобильных приложений Azure в Visual Studio. После установки пакета SDK для hello создайте приложения ASP.NET, используя hello следующие шаги:

1. Откройте hello **новый проект** диалоговое окно (из *файл* > **New** > **проект...** ).
2. Разверните раздел **Шаблоны** > **Visual C#** и выберите **Интернет**.
3. Выберите **Веб-приложение ASP.NET**.
4. Введите имя проекта hello. Нажмите кнопку **ОК**.
5. В разделе *ASP.NET 4.5.2 Templates* (Шаблоны ASP.NET 4.5.2) выберите **Мобильное приложение Azure**. Проверьте **узлов в облаке hello** toocreate мобильной серверной части в hello облако toowhich, можно опубликовать этот проект.
6. Нажмите кнопку **ОК**.

## <a name="install-sdk"></a>Как: загрузка и инициализация hello SDK
Hello пакет SDK доступен на [NuGet.org]. Этот пакет содержит базовые функциональные возможности, необходимые tooget hello, работы с использованием пакета SDK для hello. tooinitialize Здравствуйте SDK, необходимо tooperform действий над hello **HttpConfiguration** объекта.

### <a name="install-hello-sdk"></a>Установка пакета SDK для hello
hello tooinstall SDK, щелкните правой кнопкой мыши проект сервера hello в Visual Studio выберите **управление пакетами NuGet**, поиск hello [Microsoft.Azure.Mobile.Server] пакета, а затем нажмите кнопку  **Установить**.

### <a name="server-project-setup"></a>Инициализировать проект сервера hello
Сервер серверного проекта .NET — инициализированный аналогичные проекты tooother ASP.NET, включая класс запуска OWIN. Убедитесь, что ссылка на пакет NuGet hello `Microsoft.Owin.Host.SystemWeb`. tooadd этого класса в Visual Studio, щелкните правой кнопкой мыши проект сервера и выберите **добавить** >
**новый элемент**, затем **Web**  >  ** Общие** > **запуска OWIN класса**.  Класс создается hello следующий атрибут:

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

В hello `Configuration()` метод класса запуска OWIN, используйте **HttpConfiguration** объекта tooconfigure hello мобильных приложений Azure среды.
Следующий пример Hello инициализирует проект сервера hello без добавленных функций:

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

tooenable отдельные компоненты, необходимо вызывать методы расширения для hello **MobileAppConfiguration** объект перед вызовом **ApplyTo**. Например, hello, следующий код добавляет по умолчанию hello направляет tooall API контроллерами, имеющими атрибут hello `[MobileAppController]` во время инициализации:

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

Быстрый запуск сервера Hello из hello Azure портала вызовы **UseDefaultConfiguration()**. Это эквивалент toohello после завершения программы установки:

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from hello Home package
            .MapApiControllers()
            .AddTables(                               // from hello Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from hello Entity package
                )
            .AddPushNotifications()                   // from hello Notifications package
            .MapLegacyCrossDomainController()         // from hello CrossDomain package
            .ApplyTo(config);

методы расширения Hello, используемые являются:

* `AddMobileAppHomeController()`предоставляет Домашняя страница мобильных приложений Azure по умолчанию hello.
* `MapApiControllers()`предоставляет возможности пользовательского интерфейса API для контроллеров WebAPI декорированных hello `[MobileAppController]` атрибута.
* `AddTables()`содержит сопоставления hello `/tables` tootable контроллеров конечных точек.
* `AddTablesWithEntityFramework()`является собирательным для сопоставления hello `/tables` конечные точки, использующие Entity Framework на основе контроллеров.
* `AddPushNotifications()` предоставляет простой способ регистрации устройств в концентраторах уведомлений.
* `MapLegacyCrossDomainController()` предоставляет стандартные заголовки CORS для локальной разработки.

### <a name="sdk-extensions"></a>Расширения пакета SDK
следующие пакеты NuGet основе расширений Hello предоставляют различные возможности мобильных устройств, используемых приложением. Включить расширения во время инициализации с помощью hello **MobileAppConfiguration** объекта.

* [Microsoft.Azure.Mobile.Server.Quickstart] поддерживает hello базовая настройка мобильных приложений. Добавлены toohello конфигурации путем вызова hello **UseDefaultConfiguration** метод расширения во время инициализации. Это расширение включает в себя следующие расширения: пакеты Notifications, Authentication, Entity, Tables, Crossdomain и Home. Этот пакет используется hello на портал Azure hello быстрый запуск приложений мобильных устройств.
* [Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) реализует по умолчанию hello *— это мобильное приложение работает страница* для hello корневого веб-сайта. Добавление конфигурации toohello путем вызова **AddMobileAppHomeController** метода расширения.
* [Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) содержит классы для работы с конвейером данных hello данных и наборы вверх. Добавьте конфигурации toohello, вызывающему Привет **AddTables** метода расширения.
* [Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) данные tooaccess Entity Framework hello hello базы данных SQL. Добавьте конфигурации toohello, вызывающему Привет **AddTablesWithEntityFramework** метода расширения.
* [Microsoft.Azure.Mobile.Server.Authentication] включает проверку подлинности и наборы вверх hello по промежуточного слоя OWIN, как использовать toovalidate токены. Добавьте конфигурации toohello, вызывающему Привет **AddAppServiceAuthentication** и **IAppBuilder**. **UseAppServiceAuthentication** методы расширения.
* [Microsoft.Azure.Mobile.Server.Notifications] включает push-уведомления и определяет их конечную точку регистрации. Добавьте конфигурации toohello, вызывающему Привет **AddPushNotifications** метода расширения.
* [Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) будет создан контроллер, выполняющий toolegacy данных веб-браузеров из мобильного приложения. Добавление конфигурации toohello путем вызова **MapLegacyCrossDomainController** метода расширения.
* [Microsoft.Azure.Mobile.Server.Login] предоставляет метод AppServiceLoginHandler.CreateToken() hello, который представляет собой статический метод, используемый при выполнении сценариев нестандартной проверки подлинности.

## <a name="publish-server-project"></a>Как: публикации проекта сервера hello
В этом разделе показано, как toopublish серверной части .NET из проекта Visual Studio. Можно также развернуть проект базы данных с использованием Git или любой из hello других методов, описанных в hello [документации по развертыванию службы приложений Azure](../app-service-web/web-sites-deploy.md).

1. В Visual Studio перестройте пакетов NuGet toorestore hello проекта.
2. В обозревателе решений щелкните правой кнопкой мыши проект hello, нажмите кнопку **публикации**. Hello публикации, при первом запуске необходимо toodefine профиль публикации. Если профиль уже определен, выделите его и нажмите кнопку **Опубликовать**.
3. При получении запроса tooselect место назначения публикации, нажмите кнопку **службу приложений Microsoft Azure** > **Далее**, а затем (при необходимости) войти, используя свои учетные данные Azure.
   Visual Studio загрузит параметры публикации из Azure и безопасно сохранит их.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. Выберите свою **подписку**, а затем в раскрывающемся списке **Представление** выберите **Тип ресурса**, разверните **Мобильное приложение** и щелкните серверную часть мобильного приложения. После этого нажмите кнопку **ОК**.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. Проверьте hello сведения профиля публикации и нажмите кнопку **публикации**.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    При успешной публикации серверной части мобильного приложения отобразится соответствующая целевая страница.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <a name="define-table-controller"></a> Практическое руководство. Определение контроллера таблиц
Определите tooexpose контроллер таблиц клиенты toomobile таблицы SQL Server.  Настройка контроллера таблиц состоит из трех шагов.

1. Создание класса объекта передачи данных.
2. Настройте ссылку на таблицу в hello класс Mobile DbContext.
3. Создание контроллера таблиц.

Объект передачи данных — это обычный объект C#, наследуемый от `EntityData`.  Например:

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

Hello DTO — используется toodefine hello таблицы в базе данных SQL hello.  toocreate hello входа базы данных, добавьте `DbSet<>` свойства hello DbContext, вы используете.  В шаблоне проекта по умолчанию hello для мобильных приложений Azure, hello DbContext называется `Models\MobileServiceContext.cs`:

    public class MobileServiceContext : DbContext
    {
        private const string connectionStringName = "Name=MS_TableConnectionString";

        public MobileServiceContext() : base(connectionStringName)
        {

        }

        public DbSet<TodoItem> TodoItems { get; set; }

        protected override void OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Conventions.Add(
                new AttributeToColumnAnnotationConvention<TableColumnAttribute, string>(
                    "ServiceColumnTable", (property, attributes) => attributes.Single().ColumnType.ToString()));
        }
    }

Если установлен пакет SDK Azure приветствия, вы теперь можно создать контроллер шаблон таблицы следующим образом:

1. Щелкните правой кнопкой мыши папку Controllers hello и выберите **добавить** > **контроллера...** .
2. Выберите hello **контроллер таблицы Azure мобильных приложений** параметр, а затем нажмите кнопку **добавить**.
3. В hello **добавить контроллер** диалогового окна:
   * В hello **класс модели** раскрывающийся список, выберите ваш новый DTO.
   * В hello **DbContext** раскрывающийся список, класс DbContext службы Mobile выберите hello.
   * имя контроллера Hello создается автоматически.
4. Щелкните **Добавить**.

проект сервера Hello краткое руководство содержит пример для простой **TodoItemController**.

### <a name="adjust-pagesize"></a>Как: размер подкачки hello таблицы
По умолчанию мобильные приложения Azure выдают по 50 записей на запрос.  Разбиение на страницы гарантирует, что этот клиент hello не связывать их пользовательского интерфейса потока ни hello сервер слишком долго, обеспечивая эффективное взаимодействие с пользователем. размер разбиение по страницам таблицы toochange hello, размер запроса стороны сервера hello увеличение «разрешено» и hello страницы на стороне клиента размер hello серверной «допустимый размер запроса» настраивается с помощью hello `EnableQuery` атрибута:

    [EnableQuery(PageSize = 500)]

Убедитесь, что hello PageSize hello же или больше, чем размер hello, необходимая для клиента hello.  Дополнительную информацию по изменению размера страницы приветствия клиента см. в документации HOWTO toohello конкретного клиента.

## <a name="how-to-define-a-custom-api-controller"></a>Практическое руководство. Определение настраиваемого контроллера API
Hello пользовательского API устройства предоставляет hello основные функциональные возможности tooyour мобильного внутреннего сервера приложения путем предоставления конечной точки. Можно зарегистрировать контроллер API зависящие от мобильных устройств, с помощью атрибута [MobileAppController] hello. Hello `MobileAppController` атрибут регистрирует маршрут hello, настраивает сериализатор JSON мобильного приложения hello и включает [проверке версии](app-service-mobile-client-and-server-versioning.md).

1. В Visual Studio, щелкните правой кнопкой мыши hello контроллеров папка, а затем нажмите **добавить** > **контроллера**выберите **Web API 2 контроллера&mdash;пустой** и Нажмите кнопку **добавить**.
2. Укажите **имя контроллера**, например `CustomController`, и щелкните **Добавить**.
3. В hello новый файл класса контроллера, добавьте следующее hello с помощью инструкции:

        using Microsoft.Azure.Mobile.Server.Config;
4. Применить hello **[MobileAppController]** определения класса контроллера toohello API, как следующий пример hello атрибута:

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. Добавьте в файл App_Start/Startup.MobileApp.cs toohello вызов **MapApiControllers** методом расширения, как следующий пример hello:

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

Можно также использовать hello `UseDefaultConfiguration()` расширения вместо метода `MapApiControllers()`. Клиенты могут получить доступ к любому контроллеру, к которому не применен атрибут **MobileAppControllerAttribute**. Однако клиенты, использующие любой пакет SDK для клиента мобильного приложения, не смогут правильно использовать этот контроллер.

## <a name="how-to-work-with-authentication"></a>Практическое руководство: работа с проверкой подлинности
Мобильные приложения Azure использует проверку подлинности службы для приложения / toosecure авторизации серверной части мобильных устройств.  В этом разделе показано, как hello tooperform следующие задачи, связанные с проверки подлинности в проекте .NET внутреннего сервера:

* [Способ: добавить проект сервера tooa проверки подлинности](#add-auth)
* [Практическое руководство. Использование пользовательской проверки подлинности для приложения](#custom-auth)
* [Практическое руководство. Получение сведений о пользователе, прошедшем проверку подлинности](#user-info)
* [Практическое руководство. Ограничение доступа к данным для авторизованных пользователей](#authorize)

### <a name="add-auth"></a>Способ: добавить проект сервера tooa проверки подлинности
Проект сервера tooyour проверки подлинности можно расширить за счет hello **MobileAppConfiguration** объекта и настройки по промежуточного слоя OWIN. При установке hello [Microsoft.Azure.Mobile.Server.Quickstart] пакета и вызова hello **UseDefaultConfiguration** метод расширения, можно пропустить toostep 3.

1. В Visual Studio, установите hello [Microsoft.Azure.Mobile.Server.Authentication] пакета.
2. Добавьте в файл проекта файла Startup.cs hello hello, следующей строкой кода в начале hello hello **конфигурации** метод:

        app.UseAppServiceAuthentication(config);

    Этот компонент по промежуточного слоя OWIN проверки токенов, выданных hello связанного приложения службы шлюза.
3. Добавить hello `[Authorize]` атрибута tooany контроллеру или методу, который требует проверки подлинности.

toolearn о том, как клиенты tooauthenticate tooyour внутренней мобильные приложения, см. [приложение tooyour authentication добавить](app-service-mobile-ios-get-started-users.md).

### <a name="custom-auth"></a>Практическое руководство. Использование пользовательской проверки подлинности для приложения
Если toouse одного из поставщиков проверки подлинности и авторизации службы приложения hello не готовы, можно реализовать собственную систему для имени входа. Установка hello [Microsoft.Azure.Mobile.Server.Login] пакета tooassist с создания токенов проверки подлинности.  Предоставьте свой собственный код для проверки учетных данных пользователя. Например, можно выполнять проверку с помощью дополненных случайными данными и хэшированных паролей в базе данных. В следующем примере hello, hello `isValidAssertion()` метод (определенный в другом месте) отвечает за эти проверки.

Нестандартная проверка подлинности Hello предоставляется путем создания ApiController и предоставление доступа к `register` и `login` действия. Hello клиенту следует использовать пользовательские данные пользовательского интерфейса toocollect hello hello пользователя.  Hello сведения можно затем вызвать отправленной toohello API с помощью стандартных HTTP POST. После hello server проверяет утверждения hello, выдает маркер с помощью hello `AppServiceLoginHandler.CreateToken()` метод.  Hello ApiController **не должны** использовать hello `[MobileAppController]` атрибута.

Пример действия `login` :

        public IHttpActionResult Post([FromBody] JObject assertion)
        {
            if (isValidAssertion(assertion)) // user-defined function, checks against a database
            {
                JwtSecurityToken token = AppServiceLoginHandler.CreateToken(new Claim[] { new Claim(JwtRegisteredClaimNames.Sub, assertion["username"]) },
                    mySigningKey,
                    myAppURL,
                    myAppURL,
                    TimeSpan.FromHours(24) );
                return Ok(new LoginResult()
                {
                    AuthenticationToken = token.RawData,
                    User = new LoginResultUser() { UserId = userName.ToString() }
                });
            }
            else // user assertion was not valid
            {
                return this.Request.CreateUnauthorizedResponse();
            }
        }

В предыдущих пример hello LoginResult и LoginResultUser являются сериализуемые объекты, содержащие необходимые свойства. Hello клиент ожидает ответы toobe входа, возвращаются в виде объектов JSON hello формы:

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

Hello `AppServiceLoginHandler.CreateToken()` метод включает *аудитории* и *издателя* параметра. Оба этих параметра задаются toohello URL-адрес корневой каталог приложения с помощью hello схему HTTPS. Аналогично следует задать *secretKey* toobe hello значение приложении подписывающий ключ. Не распространяйте hello ключ в клиенте подписи, как можно использовать toomint ключи и олицетворять пользователей. Вы можете получить ключ во время размещенных в службе приложений с помощью ссылки на hello подписи hello *веб-САЙТ\_AUTH\_ПОДПИСЫВАНИЕ\_ключ* переменной среды. При необходимости в локальном контексте, отладки, следуйте инструкциям hello hello [локальной отладки с использованием проверки подлинности](#local-debug) статьи tooretrieve hello ключ и сохранить ее в качестве параметра приложения.

Hello выданный маркер может также включать другие утверждения и дату окончания действия.  Как минимум, hello выданный маркер должен включать тему (**sub**) утверждения.

Может поддерживать стандартную клиентскую hello `loginAsync()` метод путем перегрузки hello способа проверки подлинности.  Если клиент hello вызывает `client.loginAsync('custom');` toolog в маршрута должно быть `/.auth/login/custom`.  Можно задать hello маршрут для hello контроллер нестандартной проверки подлинности с помощью `MapHttpRoute()`:

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> С помощью hello `loginAsync()` подход гарантирует присоединен этот маркер проверки подлинности hello tooevery последующий вызов toohello службы.
>
>

### <a name="user-info"></a>Практическое руководство. Получение сведений о пользователе, прошедшем проверку подлинности
При проверке подлинности пользователя службой приложений можно получить доступ к hello назначенный идентификатор пользователя и другие сведения в свой код серверной части .NET. сведения о пользователе Hello можно использовать для принятия решения об авторизации в серверном hello. Hello следующий код получает идентификатор пользователя hello, связанный с запросом:

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

Hello SID является производным от ИД пользователя поставщика hello и статический объект для указанного пользователя и поставщик входа в систему.  Hello SID имеет значение null для маркеров недействительная проверка подлинности.

Кроме того, служба приложений позволяет запрашивать конкретные утверждения от поставщика входа в систему. Каждый поставщик удостоверений может предоставлять больше сведений с помощью пакета SDK поставщика удостоверений.  Например можно использовать hello Facebook Graph API сведения друзей.  Можно указать утверждения, которые запрашиваются в колонке поставщика hello в hello портал Azure. Некоторые утверждения требуют дополнительной настройки с помощью поставщика удостоверений hello.

Hello следующий код вызывает hello **GetAppServiceIdentityAsync** расширение метода tooget hello учетные данные входа, включая hello запросов маркера необходимые toomake доступ к hello Facebook Graph API:

    // Get hello credentials for hello logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with hello Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request hello current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with hello Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

Добавить с помощью инструкции для `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** метода расширения.

### <a name="authorize"></a>Практическое руководство. Ограничение доступа к данным для авторизованных пользователей
В предыдущем разделе hello мы показали, как tooretrieve hello идентификатор пользователя, прошедшего проверку подлинности пользователя. Вы можете ограничить доступ toodata и другие ресурсы, на основе этого значения. Например добавление столбца userId tootables и фильтрация результатов запроса hello по Идентификатору пользователя hello — toolimit удобное средство, возвращаются только пользователи tooauthorized данных. Hello следующий код возвращает строки данных только в том случае, если hello SID соответствует значению в столбце таблицы TodoItem hello UserId hello:

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong toohello current user.
    return Query().Where(t => t.UserId == sid);

Hello `Query()` возвращает метод `IQueryable` , можно управлять с помощью фильтрации toohandle LINQ.

## <a name="how-to-add-push-notifications-tooa-server-project"></a>Способ: добавить проект сервера tooa уведомлений push
Добавление push уведомления tooyour server проекта, расширяя hello **MobileAppConfiguration** объекта и создание концентраторов уведомлений клиента.

1. В Visual Studio, щелкните правой кнопкой мыши проект сервера hello и нажмите кнопку **управление пакетами NuGet**, поиск `Microsoft.Azure.Mobile.Server.Notifications`, нажмите кнопку **установить**.
2. Повторите этот шаг tooinstall hello `Microsoft.Azure.NotificationHubs` пакет, который включает клиентскую библиотеку hello концентраторов уведомлений.
3. В App_Start/Startup.MobileApp.cs и добавьте toohello вызов **AddPushNotifications()** метод расширения во время инициализации:

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. Добавьте следующий код, который создает клиент, концентраторы уведомлений hello:

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

Теперь можно использовать hello концентраторы уведомлений клиента toosend принудительной уведомления tooregistered устройств. Дополнительные сведения см. в разделе [уведомления tooyour добавить push приложения](app-service-mobile-ios-get-started-push.md). toolearn Дополнительные сведения о концентраторах уведомлений см [Обзор концентраторов уведомлений](../notification-hubs/notification-hubs-push-notification-overview.md).

## <a name="tags"></a>Практическое руководство. Включение принудительной отправки push-уведомлений с использованием тегов
Концентраторы уведомлений позволяет отправлять уведомления о целевых toospecific регистрации с помощью тегов. Несколько тегов создаются автоматически.

* Hello код установки идентифицирует определенное устройство.
* Hello идентификатор пользователя на основе проверки подлинности hello ИД безопасности определяет конкретного пользователя.

Здравствуйте, установки, код может осуществляться из hello **installationId** свойство hello **MobileServiceClient**.  Hello в примере показано использование tooadd идентификатор установки конкретного экземпляра tooa тег в концентраторах уведомлений:

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

При создании hello установки серверной hello игнорируются все теги, полученных от клиента hello во время регистрации push-уведомлений. tooenable tooadd клиента теги toohello установки, необходимо создать пользовательский API, который добавляет теги с помощью hello предшествующий шаблон.

В разделе [теги уведомления клиента добавлены принудительной] [ 5] в hello мобильные приложения службы приложений завершенного примеров использования в качестве примера.

## <a name="push-user"></a>Как: tooan уведомления принудительной отправки, проверку подлинности пользователя
Когда прошедший проверку пользователь регистрируется для push-уведомлений, тег ИД пользователя автоматически добавляется toohello регистрации. Используя этот тег, вы можете отправлять push уведомления tooall устройств, зарегистрированных этим пользователем. Hello следующий код возвращает hello идентификатор SID пользователя, выполняющего запрос и отправляет шаблон регистрации push-уведомлений tooevery устройства пользователем:

    // Get hello current user SID and create a tag for hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for hello template with hello item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification toohello user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

При регистрации для работы с push-уведомлениями на клиенте, прошедшем проверку подлинности, убедитесь, что проверка подлинности завершена, и только после этого начинайте регистрацию. Дополнительные сведения см. в разделе [Push toousers] [ 6] в hello мобильные приложения службы приложений завершенного примеров для серверного приложения .NET.

## <a name="how-to-debug-and-troubleshoot-hello-net-server-sdk"></a>Как: отладки и устранения неполадок hello Server .NET SDK
Служба приложений Azure предоставляет несколько методов отладки и устранения неполадок в приложениях ASP.NET.

* [Мониторинг службы приложений Azure](../app-service-web/web-sites-monitor.md)
* [Включение ведения журналов диагностики в службе приложений Azure](../app-service-web/web-sites-enable-diagnostic-log.md)
* [Диагностика службы приложений Azure в Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a>Ведение журналов
Журналы диагностики службы tooApp можно создавать с помощью hello Стандартная ASP.NET трассировки записи. Перед написанием toohello журналы диагностики необходимо включить в серверной части мобильного приложения.

журналы toohello по tooenable диагностики и записи:

1. Следуйте указаниям hello [как диагностики tooenable](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).
2. Добавьте следующее hello с помощью оператора в файл кода:

        using System.Web.Http.Tracing;
3. Создайте toowrite записи трассировки из hello .NET серверной toohello журналы диагностики, следующим образом:

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. Повторная публикация проекта сервера и доступа hello мобильное приложение серверной tooexecute hello путь кода, включив ведение hello.
5. Загрузите и оцените hello журналы, как описано в [как: загрузка журналов](../app-service-web/web-sites-enable-diagnostic-log.md#download).

### <a name="local-debug"></a>Локальная отладка с проверкой подлинности
Приложение можно запустить локально tootest изменения перед их публикацией toohello облака. Для большинства серверных систем мобильных приложений Azure нажмите клавишу *F5* во время работы в Visual Studio. Однако при проверке подлинности следует учитывать некоторые дополнительные рекомендации.

Необходимо иметь облачного мобильное приложение с приложение службы проверки подлинности и авторизации настроены и клиент должен иметь конечную точку облака hello указан как hello альтернативных имен узлов. Hello документации для вашей платформы клиента для hello определенные шаги.

Убедитесь, что в мобильном внутреннем сервере установлен пакет [Microsoft.Azure.Mobile.Server.Authentication] . В классе запуска приложения OWIN, добавьте следующее hello после `MobileAppConfiguration` был применен tooyour `HttpConfiguration`:

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

В предыдущих пример hello, следует настроить hello *authAudience* и *authIssuer* файла параметров приложения в файл Web.config tooeach быть URL-адрес корневой каталог приложения с помощью hello HTTPS схема. Аналогично следует задать *authSigningKey* toobe hello значение приложении подписывающий ключ.
ключ подписывания hello tooobtain:

1. Перейдите tooyour приложения в hello [портал Azure]
2. Щелкните **Инструменты**, **Kudu**, **Перейти**.
3. В узле управления Kudu hello, щелкните **среды**.
4. Найти значение hello *веб-САЙТ\_AUTH\_ПОДПИСЫВАНИЕ\_ключ*.

Ключ для hello подписи hello используйте *authSigningKey* параметр в файле config локального приложения.  Серверной части мобильных устройств теперь является токены мощной toovalidate при выполнении локально, какие hello клиент получает маркер hello из конечной точки облачного hello.

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
[портал Azure]: https://portal.azure.com
[NuGet.org]: http://www.nuget.org/
[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/
[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/
[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/
[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/
[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
