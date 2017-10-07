---
title: "aaaHow toocreate веб-приложения в кэш Redis | Документы Microsoft"
description: "Узнайте, как toocreate веб-приложения в кэш Redis"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 454e23d7-a99b-4e6e-8dd7-156451d2da7c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: hero-article
ms.date: 05/09/2017
ms.author: sdanie
ms.openlocfilehash: d3e6df97b06fdf9032570dc360944be4bd7715de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-web-app-with-redis-cache"></a>Как toocreate веб-приложения в кэш Redis
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

В этом учебнике показано как toocreate и развертывать веб приложения tooa веб-приложение ASP.NET в службе приложений Azure с помощью Visual Studio 2017 г. Пример приложения Hello отображает список группы статистических данных из базы данных и показывает различные способы toouse кэш Azure Redis toostore и извлечения данных из кэша hello. Учебником hello вы получите выполнение веб-приложения, который считывает и записывает tooa базы данных, оптимизированными для кэша Redis для Azure и размещенных в Azure.

Вы узнаете:

* Как toocreate ASP.NET MVC 5 веб-приложения в Visual Studio.
* Как tooaccess данных из базы данных, использующий Entity Framework.
* Как tooimprove пропускной способности и снизить нагрузку на базу данных, хранения и извлечения данных с помощью кэша Azure Redis.
* Порядок toouse Redis сортировки набора tooretrieve hello top 5 команд.
* Как tooprovision hello ресурсы Azure для приложения hello, с помощью шаблона диспетчера ресурсов.
* Как toopublish hello tooAzure приложения с помощью Visual Studio.

## <a name="prerequisites"></a>Предварительные требования
toocomplete hello учебника, необходимо иметь hello следующие необходимые условия.

* [Учетная запись Azure](#azure-account)
* [Visual Studio 2017 г. с hello Azure SDK для .NET](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a>Учетная запись Azure
Требуется учетная запись Azure toocomplete hello учебника. Вы можете:

* [Открыть бесплатную учетную запись Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero). Вы получаете кредиты, которые могут быть используется tootry out платных служб Azure. Даже после израсходования кредитов hello, можно защитить учетную запись hello и использования бесплатной службы Azure и возможностей.
* [Активировать преимущества подписчика Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero). Ваша подписка MSDN каждый месяц приносит вам кредиты, которые можно использовать для оплаты использования служб Azure.

### <a name="visual-studio-2017-with-hello-azure-sdk-for-net"></a>Visual Studio 2017 г. с hello Azure SDK для .NET
Hello учебник написан для Visual Studio 2017 г. с hello [Azure SDK для .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools). Hello Azure SDK 2.9.5 входит в состав установщика Visual Studio hello.

При наличии Visual Studio 2015, необходимо выполнить hello учебника с hello [Azure SDK для .NET](../dotnet-sdk.md) 2.8.2 или более поздней версии. [Загрузка hello новейшую версию пакета SDK Azure для Visual Studio 2015 здесь](http://go.microsoft.com/fwlink/?linkid=518003). Visual Studio автоматически устанавливается вместе с hello SDK, если его нет. Некоторых окон может отличаться от иллюстраций hello, показанными в данном руководстве.

Если у вас есть Visual Studio 2013, вы можете [загрузки hello новейшую версию пакета SDK Azure для Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322). Некоторых окон может отличаться от иллюстраций hello, показанными в данном руководстве.

## <a name="create-hello-visual-studio-project"></a>Создание проекта Visual Studio hello
1. Откройте Visual Studio и щелкните **Файл**, **Создать**, **Проект**.
2. Разверните hello **Visual C#** узел в hello **шаблоны** выберите **облака**и нажмите кнопку **веб-приложение ASP.NET**. Убедитесь, что выбрана платформа **.NET Framework 4.5.2** или ее более новая версия.  Тип **ContosoTeamStats** в hello **имя** текстовое поле и нажмите кнопку **ОК**.
   
    ![Создание проекта][cache-create-project]
3. Выберите **MVC** hello тип проекта. 

    Убедитесь, что **без проверки подлинности** указан для hello **проверки подлинности** параметры. В зависимости от установленной версии Visual Studio по умолчанию hello может задаваться toosomething else. toochange его, нажмите кнопку **изменить аутентификацию** и выберите **без проверки подлинности**.

    Если вы следуете вместе с Visual Studio 2015, снимите hello **узлов в облаке hello** флажок. Вы будете [подготовки hello ресурсы Azure](#provision-the-azure-resources) и [публикации tooAzure приложения hello](#publish-the-application-to-azure) в последующих шагах учебника hello. Пример подготовки веб-приложение служб приложений из Visual Studio, оставив **узлов в облаке hello** этот флажок установлен, в разделе [Приступая к работе с веб-приложений в службе приложений Azure, с помощью ASP.NET и Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).
   
    ![Выбор шаблона проекта][cache-select-template]
4. Нажмите кнопку **ОК** toocreate hello проекта.

## <a name="create-hello-aspnet-mvc-application"></a>Создание приложения ASP.NET MVC hello
В этом разделе учебника hello вы создадите простое приложение hello, которое считывает и отображает статистические данные группы из базы данных.

* [Добавьте пакет Entity Framework NuGet hello](#add-the-entity-framework-nuget-package)
* [Добавление модели hello](#add-the-model)
* [Добавить контроллер hello](#add-the-controller)
* [Настройка представлений hello](#configure-the-views)

### <a name="add-hello-entity-framework-nuget-package"></a>Добавьте пакет Entity Framework NuGet hello

1. Нажмите кнопку **диспетчера пакетов NuGet**, **консоль диспетчера пакетов** из hello **средства** меню.
2. Выполнения hello следующую команду из hello **консоль диспетчера пакетов** окна.
    
    ```
    Install-Package EntityFramework
    ```

Дополнительные сведения об этом пакете см. в разделе hello [EntityFramework](https://www.nuget.org/packages/EntityFramework/) страница NuGet.

### <a name="add-hello-model"></a>Добавление модели hello
1. В **обозревателе решений** щелкните правой кнопкой мыши папку **Модели**, а затем выберите **Добавить** и **Класс**. 
   
    ![Добавление модели][cache-model-add-class]
2. Введите `Team` для hello имя класса и нажмите кнопку **добавить**.
   
    ![Добавление класса модели][cache-model-add-class-dialog]
3. Замените hello `using` инструкции вверху hello hello `Team.cs` файла следующий hello `using` инструкции.

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. Замените определение hello hello `Team` класса hello, следующий фрагмент кода, который содержит обновленное `Team` класса определения, а также некоторые другие вспомогательные классы платформы Entity Framework. Дополнительные сведения о tooEntity первый подход hello кода платформа, которая используется в этом учебнике см. в разделе [код первого tooa новой базы данных](https://msdn.microsoft.com/data/jj193542).

    ```c#
    public class Team
    {
        public int ID { get; set; }
        public string Name { get; set; }
        public int Wins { get; set; }
        public int Losses { get; set; }
        public int Ties { get; set; }
    
        static public void PlayGames(IEnumerable<Team> teams)
        {
            // Simple random generation of statistics.
            Random r = new Random();
    
            foreach (var t in teams)
            {
                t.Wins = r.Next(33);
                t.Losses = r.Next(33);
                t.Ties = r.Next(0, 5);
            }
        }
    }
    
    public class TeamContext : DbContext
    {
        public TeamContext()
            : base("TeamContext")
        {
        }
    
        public DbSet<Team> Teams { get; set; }
    }
    
    public class TeamInitializer : CreateDatabaseIfNotExists<TeamContext>
    {
        protected override void Seed(TeamContext context)
        {
            var teams = new List<Team>
            {
                new Team{Name="Adventure Works Cycles"},
                new Team{Name="Alpine Ski House"},
                new Team{Name="Blue Yonder Airlines"},
                new Team{Name="Coho Vineyard"},
                new Team{Name="Contoso, Ltd."},
                new Team{Name="Fabrikam, Inc."},
                new Team{Name="Lucerne Publishing"},
                new Team{Name="Northwind Traders"},
                new Team{Name="Consolidated Messenger"},
                new Team{Name="Fourth Coffee"},
                new Team{Name="Graphic Design Institute"},
                new Team{Name="Nod Publishers"}
            };
    
            Team.PlayGames(teams);
    
            teams.ForEach(t => context.Teams.Add(t));
            context.SaveChanges();
        }
    }
    
    public class TeamConfiguration : DbConfiguration
    {
        public TeamConfiguration()
        {
            SetExecutionStrategy("System.Data.SqlClient", () => new SqlAzureExecutionStrategy());
        }
    }
    ```


1. В **обозревателе решений**, дважды щелкните **web.config** tooopen его.
   
    ![Web.config][cache-web-config]
2. Добавьте следующее hello `connectionStrings` раздела. Hello имя строки подключения hello должно соответствовать имя hello hello класс контекста базы данных Entity Framework, что `TeamContext`.

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    Можно добавить новый hello `connectionStrings` статьи таким образом, что `configSections`, как показано в следующий пример hello.

    ```xml
    <configuration>
      <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
      </configSections>
      <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
      </connectionStrings>
      ...
      ```

    > [!NOTE]
    > Строка подключения может отличаться в зависимости от версии Visual Studio hello и toocomplete hello учебника используется выпуск SQL Server Express. шаблон web.config Hello должен настроенных toomatch установку и может содержать `Data Source` операции, например `(LocalDB)\v11.0` (из SQL Server Express 2012) или `Data Source=(LocalDB)\MSSQLLocalDB` (SQL Server Express 2014 и выше). Дополнительные сведения о строках подключения и версиях SQL Express см. в статье о [LocalDB SQL Server 2016 Express](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).

### <a name="add-hello-controller"></a>Добавить контроллер hello
1. Нажмите клавишу **F6** toobuild hello проекта. 
2. В **обозреватель решений**, щелкните правой кнопкой мыши hello **контроллеров** папку и выберите **добавить**, **контроллера**.
   
    ![Добавление контролера][cache-add-controller]
3. Выберите **Контроллер MVC 5 с представлениями, использующий Entity Framework** и нажмите кнопку **Добавить**. Если появляется сообщение об ошибке после нажатия кнопки **добавить**, убедитесь, сначала собран проект hello.
   
    ![Добавление класса контроллера][cache-add-controller-class]
4. Выберите **Team (ContosoTeamStats.Models)** из hello **класс модели** раскрывающегося списка. Выберите **TeamContext (ContosoTeamStats.Models)** из hello **класс контекста данных** раскрывающегося списка. Тип `TeamsController` в hello **контроллера** поле "имя" (если он не заполняется автоматически). Нажмите кнопку **добавить** toocreate hello класс контроллера и добавить представления по умолчанию hello.
   
    ![Настройка контроллера][cache-configure-controller]
5. В **обозревателе решений**, разверните **Global.asax** и дважды щелкните **Global.asax.cs** tooopen его.
   
    ![Global.asax.cs][cache-global-asax]
6. Добавьте следующие два hello `using` инструкций hello верхней части файла hello под hello других `using` инструкции.

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. Добавьте следующие строки кода в конце hello hello hello `Application_Start` метод.

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. В **обозревателе решений** разверните `App_Start` и дважды щелкните `RouteConfig.cs`.
   
    ![RouteConfig.cs.][cache-RouteConfig-cs]
2. Замените `controller = "Home"` в следующий код в hello hello `RegisterRoutes` метод с `controller = "Teams"` как показано в следующий пример hello.

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-hello-views"></a>Настройка представлений hello
1. В **обозревателе решений**, разверните hello **представления** папку, а затем hello **Shared** папку и дважды щелкните **_Layout.cshtml**. 
   
    ![_Layout.cshtml][cache-layout-cshtml]
2. Изменить содержимое hello hello `title` и замените `My ASP.NET Application` с `Contoso Team Stats` как показано в следующий пример hello.

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. В hello `body` статьи, сначала обновить hello `Html.ActionLink` инструкции и замены `Application name` с `Contoso Team Stats` и замените `Home` с `Teams`.
   
   * До: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`
   * После: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`
     
     ![Изменения в коде][cache-layout-cshtml-code]
2. Нажмите клавишу **Ctrl + F5** toobuild и запуск приложения hello. Эта версия приложения hello считывает результаты hello непосредственно из базы данных hello. Примечание hello **создать новый**, **изменить**, **сведения**, и **удалить** действия, которые были автоматически добавлены toohello приложения hello **Контроллер MVC 5 с представлениями, использующий Entity Framework** формирования шаблонов. В следующем разделе hello hello руководства вы добавите доступа к данным hello toooptimize кэша Redis и предоставляют дополнительные возможности toohello приложения.

![Начальное приложение][cache-starter-application]

## <a name="configure-hello-application-toouse-redis-cache"></a>Настройка приложения hello toouse кэша Redis
В этом разделе учебника hello предстоит настроить toostore приложения образец hello и извлекать Contoso Статистика команды из экземпляра кэша Redis для Azure с помощью hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) клиента кэша.

* [Настройка приложения hello toouse StackExchange.Redis](#configure-the-application-to-use-stackexchangeredis)
* [Обновление результатов hello TeamsController класса tooreturn из кэша hello или hello базы данных](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [Hello создание, изменение, обновления и удаления toowork методы с кэшем hello](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [Обновить представление toowork hello индекс команды с кэшем hello](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-hello-application-toouse-stackexchangeredis"></a>Настройка приложения hello toouse StackExchange.Redis
1. Щелкните tooconfigure клиентское приложение в Visual Studio с помощью пакета StackExchange.Redis NuGet hello **диспетчера пакетов NuGet**, **консоль диспетчера пакетов** из hello **средства** меню.
2. Выполнения hello следующую команду из hello `Package Manager Console` окна.
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    Hello NuGet пакет загружает и добавляет hello необходимые ссылки на сборки для вашего клиента приложение tooaccess кэш Azure Redis с клиента кэша StackExchange.Redis hello. Если вы предпочитаете toouse версию со строгими именами hello `StackExchange.Redis` клиентской библиотеки, установка hello `StackExchange.Redis.StrongName` пакета.
3. В **обозревателе решений**, разверните hello **контроллеров** папку и дважды щелкните **TeamsController.cs** tooopen его.
   
    ![Контроллер команд][cache-teamscontroller]
4. Добавьте следующие два hello `using` инструкций слишком**TeamsController.cs**.

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. Добавьте следующие два свойства toohello hello `TeamsController` класса.

    ```c#   
    // Redis Connection string info
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
        return ConnectionMultiplexer.Connect(cacheConnection);
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ```

6. Создайте файл на компьютере с именем `WebAppPlusCacheAppSecrets.config` и поместите его в расположении, которое не будет возвращен с hello исходный код демонстрационного приложения, если вы решите toocheck его в другом. В этом примере hello `AppSettingsSecrets.config` находится в файле `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.
   
    Изменить hello `WebAppPlusCacheAppSecrets.config` и добавьте hello, следуя содержимое файла. При локальном запуске приложения hello эти сведения — экземпляр кэша Redis для Azure используется tooconnect tooyour. Далее в учебнике hello вам подготовить экземпляр кэша Redis для Azure и обновите hello кэша имя и пароль. Если вы не собираетесь пример приложения hello toorun локально можно пропустить hello создания этого файла и hello последующие шаги, которые ссылаются на файл hello, поскольку при развертывании приложения hello tooAzure извлекает сведения о соединении hello кэша из приложение hello значение параметра для hello веб-приложения, а не из этого файла. С момента hello `WebAppPlusCacheAppSecrets.config` развернуто tooAzure вместе с приложением, это не требуется, пока не будет toorun приложения hello локально.

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. В **обозревателе решений**, дважды щелкните **web.config** tooopen его.
   
    ![Web.config][cache-web-config]
2. Добавьте следующее hello `file` атрибута toohello `appSettings` элемента. Если вы использовали другое имя файла или в другом расположении, замените эти значения для тех, которые показаны в примере hello hello.
   
   * До: `<appSettings>`
   * После: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`
     
   Среда выполнения ASP.NET Hello объединяет содержимое hello hello внешнего файла с разметкой hello в hello `<appSettings>` элемента. Среда выполнения Hello игнорирует hello атрибут файла, если не удается найти указанный файл hello. Своих секретов (кэш tooyour строку hello подключений) не включаются в состав hello исходного кода для приложения hello. При развертывании вашей tooAzure web app, hello `WebAppPlusCacheAppSecrests.config` файл не будет развернут (то есть, при необходимости). Существует несколько способов toospecify эти секретные данные в Azure, и в этом учебнике они настраиваются автоматически при вы [подготовки hello ресурсы Azure](#provision-the-azure-resources) в следующем шаге руководства. Дополнительные сведения о работе с секретными данными в Azure см. в разделе [советы и рекомендации по развертыванию пароли и другие конфиденциальные данные tooASP.NET и службе приложений Azure](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).

### <a name="update-hello-teamscontroller-class-tooreturn-results-from-hello-cache-or-hello-database"></a>Обновление результатов hello TeamsController класса tooreturn из кэша hello или hello базы данных
В этом образце Статистика команды можно получить из базы данных hello или из кэша hello. Статистика команды хранятся в кэше hello как сериализованный `List<Team>`, а также как отсортированный набор, используя типы данных Redis. Из отсортированного набора можно извлечь все или некоторые элементы или же запросить определенные элементы. В этом образце запросы будут отсортированы hello набор для 5 команд с верхней hello отсортированные по количеству wins.

> [!NOTE]
> Это не требуется toostore Статистика команды hello в различных форматах в кэше hello в порядке toouse кэша Redis для Azure. В этом учебнике используется несколько форматов toodemonstrate некоторые toocache данные можно использовать различные способы hello и различных типов данных.
> 
> 

1. Добавьте следующее hello `using` toohello инструкций `TeamsController.cs` файла вверху hello с hello других `using` инструкции.

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. Замените текущий hello `public ActionResult Index()` реализации метода с hello следующие реализации.

    ```c#
    // GET: Teams
    public ActionResult Index(string actionType, string resultType)
    {
        List<Team> teams = null;

        switch(actionType)
        {
            case "playGames": // Play a new season of games.
                PlayGames();
                break;

            case "clearCache": // Clear hello results from hello cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild hello database with sample data.
                RebuildDB();
                break;
        }

        // Measure hello time it takes tooretrieve hello results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve hello top 5 teams from hello sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from hello cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from hello database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add hello elapsed time of hello operation toohello ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. Добавьте следующие три метода toohello hello `TeamsController` hello класс tooimplement `playGames`, `clearCache`, и `rebuildDB` типы действий из hello switch можно добавить в предыдущем фрагменте кода hello.
   
    Hello `PlayGames` метод обновляет статистику team hello имитируя сезон игр, сохраняет hello базу данных результатов toohello и очищает hello теперь устаревшие данные из кэша hello.

    ```c#
    void PlayGames()
    {
        ViewBag.msg += "Updating team statistics. ";
        // Play a "season" of games.
        var teams = from t in db.Teams
                    select t;

        Team.PlayGames(teams);

        db.SaveChanges();

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    Hello `RebuildDB` метод повторно hello базы данных по умолчанию hello набор команд, создает статистику для них и очищает hello теперь устаревшие данные из кэша hello.

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize hello database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    Hello `ClearCachedTeams` метод удаляет все статистические данные, кэшированные команды из кэша hello.

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. Добавьте следующие четыре метода toohello hello `TeamsController` класса tooimplement hello различные способы получения Статистика команды hello кэша hello и hello базы данных. Каждый из этих методов возвращает `List<Team>` которого отображается в представлении hello.
   
    Hello `GetFromDB` метод считывает hello Статистика команды из базы данных hello.
   
    ```c#
    List<Team> GetFromDB()
    {
        ViewBag.msg += "Results read from DB. ";
        var results = from t in db.Teams
            orderby t.Wins descending
            select t; 

        return results.ToList<Team>();
    }
    ```

    Hello `GetFromList` метод считывает Статистика команды hello из кэша как сериализованный `List<Team>`. В случае пропуска кэша hello Статистика команды чтения из базы данных hello и затем сохраняются в кэше hello следующего. В этом примере мы используем JSON.NET сериализации tooserialize hello .NET объекты tooand из кэша hello. Дополнительные сведения см. в разделе [toowork в .NET Framework объектов в кэше Redis для Azure](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).

    ```c#
    List<Team> GetFromList()
    {
        List<Team> teams = null;

        IDatabase cache = Connection.GetDatabase();
        string serializedTeams = cache.StringGet("teamsList");
        if (!String.IsNullOrEmpty(serializedTeams))
        {
            teams = JsonConvert.DeserializeObject<List<Team>>(serializedTeams);

            ViewBag.msg += "List read from cache. ";
        }
        else
        {
            ViewBag.msg += "Teams list cache miss. ";
            // Get from database and store in cache
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    Hello `GetFromSortedSet` метод считывает Статистика команды hello из кэшированных отсортированного набора. В случае пропуска кэша hello Статистика команды чтения из базы данных hello и хранящиеся в кэше hello как упорядоченный набор.

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", order: Order.Descending);
        if (teamsSortedSet.Count() > 0)
        {
            ViewBag.msg += "Reading sorted set from cache. ";
            teams = new List<Team>();
            foreach (var t in teamsSortedSet)
            {
                Team tt = JsonConvert.DeserializeObject<Team>(t.Element);
                teams.Add(tt);
            }
        }
        else
        {
            ViewBag.msg += "Teams sorted set cache miss. ";

            // Read from DB
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding toosorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    Hello `GetFromSortedSetTop5` метод считывает hello top набор 5 команд от кэширования hello отсортированы. Он начинает с проверки кэша hello наличие hello hello `teamsSortedSet` ключа. Если этот параметр не указан, hello `GetFromSortedSet` метод вызывается Статистика команды tooread hello и сохранять их в кэш hello. Далее hello кэшированных отсортированный набор отправляет запрос top hello 5 команд, которые возвращаются.

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load hello entire sorted set into hello cache.
            GetFromSortedSet();

            // Retrieve hello top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get hello top 5 teams from hello sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-hello-create-edit-and-delete-methods-toowork-with-hello-cache"></a>Hello создание, изменение, обновления и удаления toowork методы с кэшем hello
Hello формирование шаблонов код, который был создан как части данного примера включает методы tooadd, изменение и удаление групп. Каждый раз, когда добавляется, изменить или удалить команды, hello данные в кэше hello станет устаревшим. В данном разделе, необходимо изменить эти три метода tooclear hello кэшированных команды, чтобы кэш hello не будет синхронизирован с hello базы данных.

1. Обзор toohello `Create(Team team)` метод в hello `TeamsController` класса. Добавить toohello вызов `ClearCachedTeams` метода, как показано в следующий пример hello.

    ```c#
    // POST: Teams/Create
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. Обзор toohello `Edit(Team team)` метод в hello `TeamsController` класса. Добавить toohello вызов `ClearCachedTeams` метода, как показано в следующий пример hello.

    ```c#
    // POST: Teams/Edit/5
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. Обзор toohello `DeleteConfirmed(int id)` метод в hello `TeamsController` класса. Добавить toohello вызов `ClearCachedTeams` метода, как показано в следующий пример hello.

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, hello cache is out of date.
        // Clear hello cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-hello-teams-index-view-toowork-with-hello-cache"></a>Обновить представление toowork hello индекс команды с кэшем hello
1. В **обозревателе решений**, разверните hello **представления** папки, а затем hello **команды** папку и дважды щелкните **Index.cshtml**.
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. Вверху hello файл hello найдите следующий абзац элементом hello.
   
    ![Таблица действий][cache-teams-index-table]
   
    Это toocreate ссылку hello новой команды. Замените элемент абзаца hello hello в следующей таблице. Эта таблица содержит ссылки на действия для создания новых команд, воспроизведение новый сезон игр, очистка кэша hello, извлечение hello команды из кэша hello в нескольких форматах, получении hello команды из базы данных hello и перестроения hello базы данных с данными нового образца.

    ```html
    <table class="table">
        <tr>
            <td>
                @Html.ActionLink("Create New", "Create")
            </td>
            <td>
                @Html.ActionLink("Play Season", "Index", new { actionType = "playGames" })
            </td>
            <td>
                @Html.ActionLink("Clear Cache", "Index", new { actionType = "clearCache" })
            </td>
            <td>
                @Html.ActionLink("List from Cache", "Index", new { resultType = "teamsList" })
            </td>
            <td>
                @Html.ActionLink("Sorted Set from Cache", "Index", new { resultType = "teamsSortedSet" })
            </td>
            <td>
                @Html.ActionLink("Top 5 Teams from Cache", "Index", new { resultType = "teamsSortedSetTop5" })
            </td>
            <td>
                @Html.ActionLink("Load from DB", "Index", new { resultType = "fromDB" })
            </td>
            <td>
                @Html.ActionLink("Rebuild DB", "Index", new { actionType = "rebuildDB" })
            </td>
        </tr>    
    </table>
    ```


1. Прокрутки внизу toohello hello **Index.cshtml** файл и добавьте следующее hello `tr` элемент, чтобы оно было hello последняя строка hello последнего в таблицу файл hello.
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    Эта строка содержит значение hello `ViewBag.Msg` , содержащее отчет о состоянии о hello текущей операции. Hello `ViewBag.Msg` устанавливается при нажатии кнопки ссылки действия hello из предыдущего шага hello.   
   
    ![Сообщение о состоянии][cache-status-message]
2. Нажмите клавишу **F6** toobuild hello проекта.

## <a name="provision-hello-azure-resources"></a>Подготовка к работе hello ресурсы Azure
toohost вашего приложения в Azure, необходимо сначала подготовить hello служб Azure, которые требуются приложению. Пример приложения Hello в этом учебнике используется hello следующих служб Azure.

* кэш Azure Redis
* веб-приложение службы приложений;
* База данных SQL

toodeploy эти группы ресурсов новой или существующей службы tooa по своему усмотрению, щелкните следующие hello **развертывание tooAzure** кнопки.

[! [Развертывание tooAzure] [deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)

Это **развертывание tooAzure** кнопка использует hello [Создание веб-приложения, а также кэша Redis, а также базы данных SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [быстрый запуск Azure](https://github.com/Azure/azure-quickstart-templates) tooprovision шаблона эти службы и набор hello Строка подключения для hello базы данных SQL и hello параметр приложения для hello строку подключения для кэша Redis для Azure.

> [!NOTE]
> Если у вас нет учетной записи Azure, можно [создать бесплатную учетную запись Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) всего за несколько минут.
> 
> 

Выбрав hello **развертывание tooAzure** кнопка позволяет toohello портал Azure и инициирует hello процесс создания ресурсов hello, описываемого hello шаблона.

![Развертывание tooAzure][cache-deploy-to-azure-step-1]

1. В hello **основы** статьи выберите toouse hello подписки Azure и выберите существующую группу ресурсов или создайте новый и указать расположение группы ресурсов hello.
2. В hello **параметры** укажите **входа администратора** (не используйте **администратора**), **пароль входа администратора**и  **Имя базы данных**. Hello других параметров, настроенных для размещения плана и экономичные варианты для hello базы данных SQL и кэша Redis для Azure, которые не входят в состав бесплатный уровень бесплатной службы приложения.

    ![Развертывание tooAzure][cache-deploy-to-azure-step-2]

3. После настройки параметров требуемого hello, прокрутите toohello конец страницы приветствия, чтения hello условий и проверки hello **я принимаю условия, указанных выше, toohello** флажок.
4. Щелкните toobegin подготовки и предоставления ресурсов hello, **покупки**.

tooview hello хода выполнения развертывания, щелкните значок уведомления hello и нажмите кнопку **начато развертывание**.

![Развертывание начато][cache-deployment-started]

Hello состояние развертывания можно посмотреть на hello **Microsoft.Template** колонку.

![Развертывание tooAzure][cache-deploy-to-azure-step-3]

После завершения подготовки можно опубликовать tooAzure вашего приложения из Visual Studio.

> [!NOTE]
> Все ошибки, возникающие во время процесса инициализации hello, отображаются на hello **Microsoft.Template** колонку. Среди распространенных ошибок — слишком много ошибок, связанных с SQL Server или планами размещения служб приложений уровня "Бесплатный" на подписку. Исправьте все ошибки и перезапустите процесс hello, нажав кнопку **повторно развернуть** на hello **Microsoft.Template** колонке или hello **развертывание tooAzure** кнопки в этом учебнике.
> 
> 

## <a name="publish-hello-application-tooazure"></a>Публикация приложения tooAzure hello
На этом шаге учебника hello будет публиковать tooAzure приложения hello и запустите его в облаке hello.

1. Щелкните правой кнопкой мыши hello **ContosoTeamStats** проекта в Visual Studio и выберите **публикации**.
   
    ![Опубликовать][cache-publish-app]
2. Щелкните элемент **Служба приложений Microsoft Azure**, выберите параметр **Выбрать существующую** и нажмите кнопку **Опубликовать**.
   
    ![Опубликовать][cache-publish-to-app-service]
3. Выберите подписку hello, используется при создании hello ресурсы Azure, разверните группу ресурсов hello, содержащий ресурсы hello и выберите hello требуемого веб-приложения. Если вы использовали hello **развертывание tooAzure** кнопка запускает ваше имя веб-приложения с **веб-сайт** следуют некоторые дополнительные символы.
   
    ![Выбор веб-приложения][cache-select-web-app]
4. Нажмите кнопку **ОК** hello toobegin процесс публикации. Через несколько секунд завершает процесс публикации hello и запустить браузер с управлением образец приложения hello. Если возникает ошибка при проверке или публикации DNS, а hello процесс для подготовки hello ресурсы Azure для приложения hello совсем недавно завершена, подождите немного и повторите попытку.
   
    ![Кэш добавлен][cache-added-to-application]

Hello Следующая таблица описывает ссылку каждого действия из образца приложения hello.

| Действие | Описание |
| --- | --- |
| Создать |Создание команды. |
| Воспроизвести сезон |Воспроизведение сезон игр stats команды update hello, и снимите все устаревшие данные из группы данных из кэша hello. |
| Очистить кэш |Статистика команды Очистить hello из кэша hello. |
| List from Cache (Перечислить из кэша) |Получение статистики команды hello из кэша hello. В случае пропуска кэша загрузить hello статистики из базы данных hello и сохранить toohello кэша при следующем. |
| Sorted Set from Cache (Отсортированный набор из кэша) |Получение статистики hello team из кэша hello, с помощью упорядоченного набора. В случае пропуска кэша загрузить hello статистики из базы данных hello и сохранить toohello кэша с помощью упорядоченного набора. |
| Top 5 Teams from Cache (5 лучших команд из кэша) |Получить hello top 5 команды из кэша hello, с использованием упорядоченного набора. В случае пропуска кэша загрузить hello статистики из базы данных hello и сохранить toohello кэша с помощью упорядоченного набора. |
| Load from DB (Загрузить из базы данных) |Получить hello team статистики из базы данных hello. |
| Rebuild DB (Перестроить базу данных) |Перестроение базы данных hello и перезагрузить его с образцами данных команды. |
| Изменить; Сведения; Удалить |Изменение команды, просмотр сведений о команде, удаление команды. |

Щелкните некоторых действиях hello и поэкспериментировать с извлечением hello данных из различных источников hello. Не hello различия в hello время, затрачиваемое toocomplete hello различные способы получения данных hello hello базы данных и кэш hello.

## <a name="delete-hello-resources-when-you-are-finished-with-hello-application"></a>Удалить hello ресурсов при завершении работы с приложением hello
По окончании работы с учебного приложения hello образец hello Azure можно удалить ресурсы, используемые в порядке tooconserve стоимости и ресурсы. При использовании hello **развертывание tooAzure** кнопку в hello [подготовки hello ресурсы Azure](#provision-the-azure-resources) раздел и все ресурсы, содержащиеся в hello же группе ресурсов, их можно удалить вместе в одном Операция, удалив hello группы ресурсов.

1. Войдите в toohello [портал Azure](https://portal.azure.com) и нажмите кнопку **групп ресурсов**.
2. Имя группы ресурсов в hello типа hello **фильтрации элементов...**  текстового поля.
3. Нажмите кнопку **...**  toohello справа от группы ресурсов.
4. Нажмите кнопку **Delete**(Удалить).
   
    ![Удалить][cache-delete-resource-group]
5. Имя группы ресурсов и нажмите кнопку hello типа **удалить**.
   
    ![Подтверждение удаления][cache-delete-confirm]

После нескольких секунд hello ресурсов группы и все ее ресурсы автономной удаляются.

> [!IMPORTANT]
> Обратите внимание, что при удалении группы ресурсов является необратимым, и что группа ресурсов "hello" и все ресурсы hello в нем будут безвозвратно удалены. Убедитесь, что вы случайно не удалите группы hello неправильный ресурсов или ресурсов. Если вы создали hello ресурсов для размещения в этом примере в существующую группу ресурсов, каждый ресурс можно удалить по отдельности из их соответствующих колонок.
> 
> 

## <a name="run-hello-sample-application-on-your-local-machine"></a>Запустить образец приложения hello на локальном компьютере
приложение hello toorun локально на компьютере, необходимо кэш Azure Redis экземпляра в какие toocache данных. 

* Если опубликовали tooAzure вашего приложения, как описано в предыдущем разделе hello, можно использовать экземпляр кэша Redis для Azure hello, который был инициализирован во время выполнения этого шага.
* При наличии другого существующего экземпляра кэша Redis для Azure, можно использовать, toorun в этом примере локально.
* Если вам требуется toocreate экземпляр кэша Redis для Azure, выполните действия hello в [создать кэш](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).

После выбора или создания кэша toouse hello Обзор toohello кэша в hello портал Azure и получить hello [имя узла](cache-configure.md#properties) и [ключи доступа](cache-configure.md#access-keys) своего кэша. Инструкции см. в разделе [Настройка параметров кэша Redis](cache-configure.md#configure-redis-cache-settings).

1. Откройте hello `WebAppPlusCacheAppSecrets.config` файл, созданный во время hello [Настройка toouse приложения hello кэша Redis](#configure-the-application-to-use-redis-cache) шаге этого учебника, используя любой редактор hello.
2. Изменить hello `value` атрибута и замените `MyCache.redis.cache.windows.net` с hello [имя узла](cache-configure.md#properties) кэша и укажите либо hello [первичный или вторичный ключ](cache-configure.md#access-keys) кэша hello паролем.

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. Нажмите клавишу **Ctrl + F5** toorun приложения hello.

> [!NOTE]
> Обратите внимание, что кэш Здравствуйте, так как приложение hello, включая hello базы данных, выполняется локально, а hello кэша Redis размещается в Azure, может появиться toounder-выполнения hello базы данных. Для наилучшей производительности hello клиентское приложение и экземпляр кэша Redis для Azure должны находиться в hello местоположения. 
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о [Приступая к работе с ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) на hello [ASP.NET](http://asp.net/) сайта.
* Дополнительные примеры создания веб-приложение ASP.NET в службе приложений см. в разделе [создать и развернуть веб-приложение ASP.NET в службе приложений Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) из hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [Демонстрация](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).
  * Дополнительные примеры использования из образца hello HealthClinic.biz, в разделе [примеры использования средств разработчика Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).
* Дополнительные сведения о hello [код первого tooa новую базу данных](https://msdn.microsoft.com/data/jj193542) подход tooEntity платформа, которая используется в этом учебнике.
* Узнайте больше о [веб-приложениях в службе приложений Azure](../app-service-web/app-service-web-overview.md).
* Узнайте, каким образом слишком[монитор](cache-how-to-monitor.md) кэш hello портал Azure.
* Изучите возможности кэша Redis для Azure уровня Premium:
  
  * [Как tooconfigure сохраняемости для кэша Redis Azure Premium](cache-how-to-premium-persistence.md)
  * [Как tooconfigure кластеризации для кэша Redis Azure Premium](cache-how-to-premium-clustering.md)
  * [Как поддерживают tooconfigure виртуальной сети для кэша Redis Azure Premium](cache-how-to-premium-vnet.md)
  * В разделе hello [Azure Redis кэша часто задаваемые вопросы о](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) Дополнительные сведения о размере, пропускную способность и пропускную способность с кэши premium.

<!-- IMAGES -->
[cache-starter-application]: ./media/cache-web-app-howto/cache-starter-application.png
[cache-added-to-application]: ./media/cache-web-app-howto/cache-added-to-application.png
[cache-create-project]: ./media/cache-web-app-howto/cache-create-project.png
[cache-select-template]: ./media/cache-web-app-howto/cache-select-template.png
[cache-model-add-class]: ./media/cache-web-app-howto/cache-model-add-class.png
[cache-model-add-class-dialog]: ./media/cache-web-app-howto/cache-model-add-class-dialog.png
[cache-add-controller]: ./media/cache-web-app-howto/cache-add-controller.png
[cache-add-controller-class]: ./media/cache-web-app-howto/cache-add-controller-class.png
[cache-configure-controller]: ./media/cache-web-app-howto/cache-configure-controller.png
[cache-global-asax]: ./media/cache-web-app-howto/cache-global-asax.png
[cache-RouteConfig-cs]: ./media/cache-web-app-howto/cache-RouteConfig-cs.png
[cache-layout-cshtml]: ./media/cache-web-app-howto/cache-layout-cshtml.png
[cache-layout-cshtml-code]: ./media/cache-web-app-howto/cache-layout-cshtml-code.png
[redis-cache-manage-nuget-menu]: ./media/cache-web-app-howto/redis-cache-manage-nuget-menu.png
[redis-cache-stack-exchange-nuget]: ./media/cache-web-app-howto/redis-cache-stack-exchange-nuget.png
[cache-teamscontroller]: ./media/cache-web-app-howto/cache-teamscontroller.png
[cache-web-config]: ./media/cache-web-app-howto/cache-web-config.png
[cache-views-teams-index-cshtml]: ./media/cache-web-app-howto/cache-views-teams-index-cshtml.png
[cache-teams-index-table]: ./media/cache-web-app-howto/cache-teams-index-table.png
[cache-status-message]: ./media/cache-web-app-howto/cache-status-message.png
[deploybutton]: ./media/cache-web-app-howto/deploybutton.png
[cache-deploy-to-azure-step-1]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-1.png
[cache-deploy-to-azure-step-2]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-2.png
[cache-deploy-to-azure-step-3]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-3.png
[cache-deployment-started]: ./media/cache-web-app-howto/cache-deployment-started.png
[cache-publish-app]: ./media/cache-web-app-howto/cache-publish-app.png
[cache-publish-to-app-service]: ./media/cache-web-app-howto/cache-publish-to-app-service.png
[cache-select-web-app]: ./media/cache-web-app-howto/cache-select-web-app.png
[cache-publish]: ./media/cache-web-app-howto/cache-publish.png
[cache-delete-resource-group]: ./media/cache-web-app-howto/cache-delete-resource-group.png
[cache-delete-confirm]: ./media/cache-web-app-howto/cache-delete-confirm.png

