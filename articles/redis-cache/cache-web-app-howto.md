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
# <a name="how-toocreate-a-web-app-with-redis-cache"></a><span data-ttu-id="81375-103">Как toocreate веб-приложения в кэш Redis</span><span class="sxs-lookup"><span data-stu-id="81375-103">How toocreate a Web App with Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="81375-104">.NET</span><span class="sxs-lookup"><span data-stu-id="81375-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="81375-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="81375-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="81375-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="81375-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="81375-107">Java</span><span class="sxs-lookup"><span data-stu-id="81375-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="81375-108">Python</span><span class="sxs-lookup"><span data-stu-id="81375-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="81375-109">В этом учебнике показано как toocreate и развертывать веб приложения tooa веб-приложение ASP.NET в службе приложений Azure с помощью Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="81375-109">This tutorial shows how toocreate and deploy an ASP.NET web application tooa web app in Azure App Service using Visual Studio 2017.</span></span> <span data-ttu-id="81375-110">Пример приложения Hello отображает список группы статистических данных из базы данных и показывает различные способы toouse кэш Azure Redis toostore и извлечения данных из кэша hello.</span><span class="sxs-lookup"><span data-stu-id="81375-110">hello sample application displays a list of team statistics from a database and shows different ways toouse Azure Redis Cache toostore and retrieve data from hello cache.</span></span> <span data-ttu-id="81375-111">Учебником hello вы получите выполнение веб-приложения, который считывает и записывает tooa базы данных, оптимизированными для кэша Redis для Azure и размещенных в Azure.</span><span class="sxs-lookup"><span data-stu-id="81375-111">When you complete hello tutorial you'll have a running web app that reads and writes tooa database, optimized with Azure Redis Cache, and hosted in Azure.</span></span>

<span data-ttu-id="81375-112">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="81375-112">You'll learn:</span></span>

* <span data-ttu-id="81375-113">Как toocreate ASP.NET MVC 5 веб-приложения в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="81375-113">How toocreate an ASP.NET MVC 5 web application in Visual Studio.</span></span>
* <span data-ttu-id="81375-114">Как tooaccess данных из базы данных, использующий Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="81375-114">How tooaccess data from a database using Entity Framework.</span></span>
* <span data-ttu-id="81375-115">Как tooimprove пропускной способности и снизить нагрузку на базу данных, хранения и извлечения данных с помощью кэша Azure Redis.</span><span class="sxs-lookup"><span data-stu-id="81375-115">How tooimprove data throughput and reduce database load by storing and retrieving data using Azure Redis Cache.</span></span>
* <span data-ttu-id="81375-116">Порядок toouse Redis сортировки набора tooretrieve hello top 5 команд.</span><span class="sxs-lookup"><span data-stu-id="81375-116">How toouse a Redis sorted set tooretrieve hello top 5 teams.</span></span>
* <span data-ttu-id="81375-117">Как tooprovision hello ресурсы Azure для приложения hello, с помощью шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="81375-117">How tooprovision hello Azure resources for hello application using a Resource Manager template.</span></span>
* <span data-ttu-id="81375-118">Как toopublish hello tooAzure приложения с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="81375-118">How toopublish hello application tooAzure using Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81375-119">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="81375-119">Prerequisites</span></span>
<span data-ttu-id="81375-120">toocomplete hello учебника, необходимо иметь hello следующие необходимые условия.</span><span class="sxs-lookup"><span data-stu-id="81375-120">toocomplete hello tutorial, you must have hello following prerequisites.</span></span>

* [<span data-ttu-id="81375-121">Учетная запись Azure</span><span class="sxs-lookup"><span data-stu-id="81375-121">Azure account</span></span>](#azure-account)
* [<span data-ttu-id="81375-122">Visual Studio 2017 г. с hello Azure SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="81375-122">Visual Studio 2017 with hello Azure SDK for .NET</span></span>](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a><span data-ttu-id="81375-123">Учетная запись Azure</span><span class="sxs-lookup"><span data-stu-id="81375-123">Azure account</span></span>
<span data-ttu-id="81375-124">Требуется учетная запись Azure toocomplete hello учебника.</span><span class="sxs-lookup"><span data-stu-id="81375-124">You need an Azure account toocomplete hello tutorial.</span></span> <span data-ttu-id="81375-125">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="81375-125">You can:</span></span>

* <span data-ttu-id="81375-126">[Открыть бесплатную учетную запись Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="81375-126">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="81375-127">Вы получаете кредиты, которые могут быть используется tootry out платных служб Azure.</span><span class="sxs-lookup"><span data-stu-id="81375-127">You get credits that can be used tootry out paid Azure services.</span></span> <span data-ttu-id="81375-128">Даже после израсходования кредитов hello, можно защитить учетную запись hello и использования бесплатной службы Azure и возможностей.</span><span class="sxs-lookup"><span data-stu-id="81375-128">Even after hello credits are used up, you can keep hello account and use free Azure services and features.</span></span>
* <span data-ttu-id="81375-129">[Активировать преимущества подписчика Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="81375-129">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="81375-130">Ваша подписка MSDN каждый месяц приносит вам кредиты, которые можно использовать для оплаты использования служб Azure.</span><span class="sxs-lookup"><span data-stu-id="81375-130">Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

### <a name="visual-studio-2017-with-hello-azure-sdk-for-net"></a><span data-ttu-id="81375-131">Visual Studio 2017 г. с hello Azure SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="81375-131">Visual Studio 2017 with hello Azure SDK for .NET</span></span>
<span data-ttu-id="81375-132">Hello учебник написан для Visual Studio 2017 г. с hello [Azure SDK для .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span><span class="sxs-lookup"><span data-stu-id="81375-132">hello tutorial is written for Visual Studio 2017 with hello [Azure SDK for .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span></span> <span data-ttu-id="81375-133">Hello Azure SDK 2.9.5 входит в состав установщика Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="81375-133">hello Azure SDK 2.9.5 is included with hello Visual Studio installer.</span></span>

<span data-ttu-id="81375-134">При наличии Visual Studio 2015, необходимо выполнить hello учебника с hello [Azure SDK для .NET](../dotnet-sdk.md) 2.8.2 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="81375-134">If you have Visual Studio 2015, you can follow hello tutorial with hello [Azure SDK for .NET](../dotnet-sdk.md) 2.8.2 or later.</span></span> <span data-ttu-id="81375-135">[Загрузка hello новейшую версию пакета SDK Azure для Visual Studio 2015 здесь](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="81375-135">[Download hello latest Azure SDK for Visual Studio 2015 here](http://go.microsoft.com/fwlink/?linkid=518003).</span></span> <span data-ttu-id="81375-136">Visual Studio автоматически устанавливается вместе с hello SDK, если его нет.</span><span class="sxs-lookup"><span data-stu-id="81375-136">Visual Studio is automatically installed with hello SDK if you don't already have it.</span></span> <span data-ttu-id="81375-137">Некоторых окон может отличаться от иллюстраций hello, показанными в данном руководстве.</span><span class="sxs-lookup"><span data-stu-id="81375-137">Some screens may look different from hello illustrations shown in this tutorial.</span></span>

<span data-ttu-id="81375-138">Если у вас есть Visual Studio 2013, вы можете [загрузки hello новейшую версию пакета SDK Azure для Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span><span class="sxs-lookup"><span data-stu-id="81375-138">If you have Visual Studio 2013, you can [download hello latest Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span></span> <span data-ttu-id="81375-139">Некоторых окон может отличаться от иллюстраций hello, показанными в данном руководстве.</span><span class="sxs-lookup"><span data-stu-id="81375-139">Some screens may look different from hello illustrations shown in this tutorial.</span></span>

## <a name="create-hello-visual-studio-project"></a><span data-ttu-id="81375-140">Создание проекта Visual Studio hello</span><span class="sxs-lookup"><span data-stu-id="81375-140">Create hello Visual Studio project</span></span>
1. <span data-ttu-id="81375-141">Откройте Visual Studio и щелкните **Файл**, **Создать**, **Проект**.</span><span class="sxs-lookup"><span data-stu-id="81375-141">Open Visual Studio and click **File**, **New**, **Project**.</span></span>
2. <span data-ttu-id="81375-142">Разверните hello **Visual C#** узел в hello **шаблоны** выберите **облака**и нажмите кнопку **веб-приложение ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="81375-142">Expand hello **Visual C#** node in hello **Templates** list, select **Cloud**, and click **ASP.NET Web Application**.</span></span> <span data-ttu-id="81375-143">Убедитесь, что выбрана платформа **.NET Framework 4.5.2** или ее более новая версия.</span><span class="sxs-lookup"><span data-stu-id="81375-143">Ensure that **.NET Framework 4.5.2** or higher is selected.</span></span>  <span data-ttu-id="81375-144">Тип **ContosoTeamStats** в hello **имя** текстовое поле и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="81375-144">Type **ContosoTeamStats** into hello **Name** textbox and click **OK**.</span></span>
   
    ![Создание проекта][cache-create-project]
3. <span data-ttu-id="81375-146">Выберите **MVC** hello тип проекта.</span><span class="sxs-lookup"><span data-stu-id="81375-146">Select **MVC** as hello project type.</span></span> 

    <span data-ttu-id="81375-147">Убедитесь, что **без проверки подлинности** указан для hello **проверки подлинности** параметры.</span><span class="sxs-lookup"><span data-stu-id="81375-147">Ensure that **No Authentication** is specified for hello **Authentication** settings.</span></span> <span data-ttu-id="81375-148">В зависимости от установленной версии Visual Studio по умолчанию hello может задаваться toosomething else.</span><span class="sxs-lookup"><span data-stu-id="81375-148">Depending on your version of Visual Studio, hello default may be set toosomething else.</span></span> <span data-ttu-id="81375-149">toochange его, нажмите кнопку **изменить аутентификацию** и выберите **без проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="81375-149">toochange it, click **Change Authentication** and select **No Authentication**.</span></span>

    <span data-ttu-id="81375-150">Если вы следуете вместе с Visual Studio 2015, снимите hello **узлов в облаке hello** флажок.</span><span class="sxs-lookup"><span data-stu-id="81375-150">If you are following along with Visual Studio 2015, clear hello **Host in hello cloud** checkbox.</span></span> <span data-ttu-id="81375-151">Вы будете [подготовки hello ресурсы Azure](#provision-the-azure-resources) и [публикации tooAzure приложения hello](#publish-the-application-to-azure) в последующих шагах учебника hello.</span><span class="sxs-lookup"><span data-stu-id="81375-151">You'll [provision hello Azure resources](#provision-the-azure-resources) and [publish hello application tooAzure](#publish-the-application-to-azure) in subsequent steps in hello tutorial.</span></span> <span data-ttu-id="81375-152">Пример подготовки веб-приложение служб приложений из Visual Studio, оставив **узлов в облаке hello** этот флажок установлен, в разделе [Приступая к работе с веб-приложений в службе приложений Azure, с помощью ASP.NET и Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="81375-152">For an example of provisioning an App Service web app from Visual Studio by leaving **Host in hello cloud** checked, see [Get started with Web Apps in Azure App Service, using ASP.NET and Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
    ![Выбор шаблона проекта][cache-select-template]
4. <span data-ttu-id="81375-154">Нажмите кнопку **ОК** toocreate hello проекта.</span><span class="sxs-lookup"><span data-stu-id="81375-154">Click **OK** toocreate hello project.</span></span>

## <a name="create-hello-aspnet-mvc-application"></a><span data-ttu-id="81375-155">Создание приложения ASP.NET MVC hello</span><span class="sxs-lookup"><span data-stu-id="81375-155">Create hello ASP.NET MVC application</span></span>
<span data-ttu-id="81375-156">В этом разделе учебника hello вы создадите простое приложение hello, которое считывает и отображает статистические данные группы из базы данных.</span><span class="sxs-lookup"><span data-stu-id="81375-156">In this section of hello tutorial, you'll create hello basic application that reads and displays team statistics from a database.</span></span>

* [<span data-ttu-id="81375-157">Добавьте пакет Entity Framework NuGet hello</span><span class="sxs-lookup"><span data-stu-id="81375-157">Add hello Entity Framework NuGet package</span></span>](#add-the-entity-framework-nuget-package)
* [<span data-ttu-id="81375-158">Добавление модели hello</span><span class="sxs-lookup"><span data-stu-id="81375-158">Add hello model</span></span>](#add-the-model)
* [<span data-ttu-id="81375-159">Добавить контроллер hello</span><span class="sxs-lookup"><span data-stu-id="81375-159">Add hello controller</span></span>](#add-the-controller)
* [<span data-ttu-id="81375-160">Настройка представлений hello</span><span class="sxs-lookup"><span data-stu-id="81375-160">Configure hello views</span></span>](#configure-the-views)

### <a name="add-hello-entity-framework-nuget-package"></a><span data-ttu-id="81375-161">Добавьте пакет Entity Framework NuGet hello</span><span class="sxs-lookup"><span data-stu-id="81375-161">Add hello Entity Framework NuGet package</span></span>

1. <span data-ttu-id="81375-162">Нажмите кнопку **диспетчера пакетов NuGet**, **консоль диспетчера пакетов** из hello **средства** меню.</span><span class="sxs-lookup"><span data-stu-id="81375-162">Click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>
2. <span data-ttu-id="81375-163">Выполнения hello следующую команду из hello **консоль диспетчера пакетов** окна.</span><span class="sxs-lookup"><span data-stu-id="81375-163">Run hello following command from hello **Package Manager Console** window.</span></span>
    
    ```
    Install-Package EntityFramework
    ```

<span data-ttu-id="81375-164">Дополнительные сведения об этом пакете см. в разделе hello [EntityFramework](https://www.nuget.org/packages/EntityFramework/) страница NuGet.</span><span class="sxs-lookup"><span data-stu-id="81375-164">For more information about this package, see hello [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet page.</span></span>

### <a name="add-hello-model"></a><span data-ttu-id="81375-165">Добавление модели hello</span><span class="sxs-lookup"><span data-stu-id="81375-165">Add hello model</span></span>
1. <span data-ttu-id="81375-166">В **обозревателе решений** щелкните правой кнопкой мыши папку **Модели**, а затем выберите **Добавить** и **Класс**.</span><span class="sxs-lookup"><span data-stu-id="81375-166">Right-click **Models** in **Solution Explorer**, and choose **Add**, **Class**.</span></span> 
   
    ![Добавление модели][cache-model-add-class]
2. <span data-ttu-id="81375-168">Введите `Team` для hello имя класса и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="81375-168">Enter `Team` for hello class name and click **Add**.</span></span>
   
    ![Добавление класса модели][cache-model-add-class-dialog]
3. <span data-ttu-id="81375-170">Замените hello `using` инструкции вверху hello hello `Team.cs` файла следующий hello `using` инструкции.</span><span class="sxs-lookup"><span data-stu-id="81375-170">Replace hello `using` statements at hello top of hello `Team.cs` file with hello following `using` statements.</span></span>

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. <span data-ttu-id="81375-171">Замените определение hello hello `Team` класса hello, следующий фрагмент кода, который содержит обновленное `Team` класса определения, а также некоторые другие вспомогательные классы платформы Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="81375-171">Replace hello definition of hello `Team` class with hello following code snippet that contains an updated `Team` class definition as well as some other Entity Framework helper classes.</span></span> <span data-ttu-id="81375-172">Дополнительные сведения о tooEntity первый подход hello кода платформа, которая используется в этом учебнике см. в разделе [код первого tooa новой базы данных](https://msdn.microsoft.com/data/jj193542).</span><span class="sxs-lookup"><span data-stu-id="81375-172">For more information on hello code first approach tooEntity Framework that's used in this tutorial, see [Code first tooa new database](https://msdn.microsoft.com/data/jj193542).</span></span>

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


1. <span data-ttu-id="81375-173">В **обозревателе решений**, дважды щелкните **web.config** tooopen его.</span><span class="sxs-lookup"><span data-stu-id="81375-173">In **Solution Explorer**, double-click **web.config** tooopen it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="81375-175">Добавьте следующее hello `connectionStrings` раздела.</span><span class="sxs-lookup"><span data-stu-id="81375-175">Add hello following `connectionStrings` section.</span></span> <span data-ttu-id="81375-176">Hello имя строки подключения hello должно соответствовать имя hello hello класс контекста базы данных Entity Framework, что `TeamContext`.</span><span class="sxs-lookup"><span data-stu-id="81375-176">hello name of hello connection string must match hello name of hello Entity Framework database context class which is `TeamContext`.</span></span>

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="81375-177">Можно добавить новый hello `connectionStrings` статьи таким образом, что `configSections`, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="81375-177">You can add hello new `connectionStrings` section so that it follows `configSections`, as shown in hello following example.</span></span>

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
    > <span data-ttu-id="81375-178">Строка подключения может отличаться в зависимости от версии Visual Studio hello и toocomplete hello учебника используется выпуск SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="81375-178">Your connection string may be different depending on hello version of Visual Studio and SQL Server Express edition used toocomplete hello tutorial.</span></span> <span data-ttu-id="81375-179">шаблон web.config Hello должен настроенных toomatch установку и может содержать `Data Source` операции, например `(LocalDB)\v11.0` (из SQL Server Express 2012) или `Data Source=(LocalDB)\MSSQLLocalDB` (SQL Server Express 2014 и выше).</span><span class="sxs-lookup"><span data-stu-id="81375-179">hello web.config template should be configured toomatch your installation, and may contain `Data Source` entries like `(LocalDB)\v11.0` (from SQL Server Express 2012) or `Data Source=(LocalDB)\MSSQLLocalDB` (from SQL Server Express 2014 and newer).</span></span> <span data-ttu-id="81375-180">Дополнительные сведения о строках подключения и версиях SQL Express см. в статье о [LocalDB SQL Server 2016 Express](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span><span class="sxs-lookup"><span data-stu-id="81375-180">For more information about connection strings and SQL Express versions, see [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) .</span></span>

### <a name="add-hello-controller"></a><span data-ttu-id="81375-181">Добавить контроллер hello</span><span class="sxs-lookup"><span data-stu-id="81375-181">Add hello controller</span></span>
1. <span data-ttu-id="81375-182">Нажмите клавишу **F6** toobuild hello проекта.</span><span class="sxs-lookup"><span data-stu-id="81375-182">Press **F6** toobuild hello project.</span></span> 
2. <span data-ttu-id="81375-183">В **обозреватель решений**, щелкните правой кнопкой мыши hello **контроллеров** папку и выберите **добавить**, **контроллера**.</span><span class="sxs-lookup"><span data-stu-id="81375-183">In **Solution Explorer**, right-click hello **Controllers** folder and choose **Add**, **Controller**.</span></span>
   
    ![Добавление контролера][cache-add-controller]
3. <span data-ttu-id="81375-185">Выберите **Контроллер MVC 5 с представлениями, использующий Entity Framework** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="81375-185">Choose **MVC 5 Controller with views, using Entity Framework**, and click **Add**.</span></span> <span data-ttu-id="81375-186">Если появляется сообщение об ошибке после нажатия кнопки **добавить**, убедитесь, сначала собран проект hello.</span><span class="sxs-lookup"><span data-stu-id="81375-186">If you get an error after clicking **Add**, ensure that you have built hello project first.</span></span>
   
    ![Добавление класса контроллера][cache-add-controller-class]
4. <span data-ttu-id="81375-188">Выберите **Team (ContosoTeamStats.Models)** из hello **класс модели** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="81375-188">Select **Team (ContosoTeamStats.Models)** from hello **Model class** drop-down list.</span></span> <span data-ttu-id="81375-189">Выберите **TeamContext (ContosoTeamStats.Models)** из hello **класс контекста данных** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="81375-189">Select **TeamContext (ContosoTeamStats.Models)** from hello **Data context class** drop-down list.</span></span> <span data-ttu-id="81375-190">Тип `TeamsController` в hello **контроллера** поле "имя" (если он не заполняется автоматически).</span><span class="sxs-lookup"><span data-stu-id="81375-190">Type `TeamsController` in hello **Controller** name textbox (if it is not automatically populated).</span></span> <span data-ttu-id="81375-191">Нажмите кнопку **добавить** toocreate hello класс контроллера и добавить представления по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="81375-191">Click **Add** toocreate hello controller class and add hello default views.</span></span>
   
    ![Настройка контроллера][cache-configure-controller]
5. <span data-ttu-id="81375-193">В **обозревателе решений**, разверните **Global.asax** и дважды щелкните **Global.asax.cs** tooopen его.</span><span class="sxs-lookup"><span data-stu-id="81375-193">In **Solution Explorer**, expand **Global.asax** and double-click **Global.asax.cs** tooopen it.</span></span>
   
    ![Global.asax.cs][cache-global-asax]
6. <span data-ttu-id="81375-195">Добавьте следующие два hello `using` инструкций hello верхней части файла hello под hello других `using` инструкции.</span><span class="sxs-lookup"><span data-stu-id="81375-195">Add hello following two `using` statements at hello top of hello file under hello other `using` statements.</span></span>

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. <span data-ttu-id="81375-196">Добавьте следующие строки кода в конце hello hello hello `Application_Start` метод.</span><span class="sxs-lookup"><span data-stu-id="81375-196">Add hello following line of code at hello end of hello `Application_Start` method.</span></span>

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. <span data-ttu-id="81375-197">В **обозревателе решений** разверните `App_Start` и дважды щелкните `RouteConfig.cs`.</span><span class="sxs-lookup"><span data-stu-id="81375-197">In **Solution Explorer**, expand `App_Start` and double-click `RouteConfig.cs`.</span></span>
   
    ![RouteConfig.cs.][cache-RouteConfig-cs]
2. <span data-ttu-id="81375-199">Замените `controller = "Home"` в следующий код в hello hello `RegisterRoutes` метод с `controller = "Teams"` как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="81375-199">Replace `controller = "Home"` in hello following code in hello `RegisterRoutes` method with `controller = "Teams"` as shown in hello following example.</span></span>

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-hello-views"></a><span data-ttu-id="81375-200">Настройка представлений hello</span><span class="sxs-lookup"><span data-stu-id="81375-200">Configure hello views</span></span>
1. <span data-ttu-id="81375-201">В **обозревателе решений**, разверните hello **представления** папку, а затем hello **Shared** папку и дважды щелкните **_Layout.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="81375-201">In **Solution Explorer**, expand hello **Views** folder and then hello **Shared** folder, and double-click **_Layout.cshtml**.</span></span> 
   
    ![_Layout.cshtml][cache-layout-cshtml]
2. <span data-ttu-id="81375-203">Изменить содержимое hello hello `title` и замените `My ASP.NET Application` с `Contoso Team Stats` как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="81375-203">Change hello contents of hello `title` element and replace `My ASP.NET Application` with `Contoso Team Stats` as shown in hello following example.</span></span>

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. <span data-ttu-id="81375-204">В hello `body` статьи, сначала обновить hello `Html.ActionLink` инструкции и замены `Application name` с `Contoso Team Stats` и замените `Home` с `Teams`.</span><span class="sxs-lookup"><span data-stu-id="81375-204">In hello `body` section, update hello first `Html.ActionLink` statement and replace `Application name` with `Contoso Team Stats` and replace `Home` with `Teams`.</span></span>
   
   * <span data-ttu-id="81375-205">До: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="81375-205">Before: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
   * <span data-ttu-id="81375-206">После: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="81375-206">After: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
     
     ![Изменения в коде][cache-layout-cshtml-code]
2. <span data-ttu-id="81375-208">Нажмите клавишу **Ctrl + F5** toobuild и запуск приложения hello.</span><span class="sxs-lookup"><span data-stu-id="81375-208">Press **Ctrl+F5** toobuild and run hello application.</span></span> <span data-ttu-id="81375-209">Эта версия приложения hello считывает результаты hello непосредственно из базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="81375-209">This version of hello application reads hello results directly from hello database.</span></span> <span data-ttu-id="81375-210">Примечание hello **создать новый**, **изменить**, **сведения**, и **удалить** действия, которые были автоматически добавлены toohello приложения hello **Контроллер MVC 5 с представлениями, использующий Entity Framework** формирования шаблонов.</span><span class="sxs-lookup"><span data-stu-id="81375-210">Note hello **Create New**, **Edit**, **Details**, and **Delete** actions that were automatically added toohello application by hello **MVC 5 Controller with views, using Entity Framework** scaffold.</span></span> <span data-ttu-id="81375-211">В следующем разделе hello hello руководства вы добавите доступа к данным hello toooptimize кэша Redis и предоставляют дополнительные возможности toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="81375-211">In hello next section of hello tutorial you'll add Redis Cache toooptimize hello data access and provide additional features toohello application.</span></span>

![Начальное приложение][cache-starter-application]

## <a name="configure-hello-application-toouse-redis-cache"></a><span data-ttu-id="81375-213">Настройка приложения hello toouse кэша Redis</span><span class="sxs-lookup"><span data-stu-id="81375-213">Configure hello application toouse Redis Cache</span></span>
<span data-ttu-id="81375-214">В этом разделе учебника hello предстоит настроить toostore приложения образец hello и извлекать Contoso Статистика команды из экземпляра кэша Redis для Azure с помощью hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) клиента кэша.</span><span class="sxs-lookup"><span data-stu-id="81375-214">In this section of hello tutorial, you'll configure hello sample application toostore and retrieve Contoso team statistics from an Azure Redis Cache instance by using hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cache client.</span></span>

* [<span data-ttu-id="81375-215">Настройка приложения hello toouse StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="81375-215">Configure hello application toouse StackExchange.Redis</span></span>](#configure-the-application-to-use-stackexchangeredis)
* [<span data-ttu-id="81375-216">Обновление результатов hello TeamsController класса tooreturn из кэша hello или hello базы данных</span><span class="sxs-lookup"><span data-stu-id="81375-216">Update hello TeamsController class tooreturn results from hello cache or hello database</span></span>](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [<span data-ttu-id="81375-217">Hello создание, изменение, обновления и удаления toowork методы с кэшем hello</span><span class="sxs-lookup"><span data-stu-id="81375-217">Update hello Create, Edit, and Delete methods toowork with hello cache</span></span>](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [<span data-ttu-id="81375-218">Обновить представление toowork hello индекс команды с кэшем hello</span><span class="sxs-lookup"><span data-stu-id="81375-218">Update hello Teams Index view toowork with hello cache</span></span>](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-hello-application-toouse-stackexchangeredis"></a><span data-ttu-id="81375-219">Настройка приложения hello toouse StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="81375-219">Configure hello application toouse StackExchange.Redis</span></span>
1. <span data-ttu-id="81375-220">Щелкните tooconfigure клиентское приложение в Visual Studio с помощью пакета StackExchange.Redis NuGet hello **диспетчера пакетов NuGet**, **консоль диспетчера пакетов** из hello **средства** меню.</span><span class="sxs-lookup"><span data-stu-id="81375-220">tooconfigure a client application in Visual Studio using hello StackExchange.Redis NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>
2. <span data-ttu-id="81375-221">Выполнения hello следующую команду из hello `Package Manager Console` окна.</span><span class="sxs-lookup"><span data-stu-id="81375-221">Run hello following command from hello `Package Manager Console` window.</span></span>
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    <span data-ttu-id="81375-222">Hello NuGet пакет загружает и добавляет hello необходимые ссылки на сборки для вашего клиента приложение tooaccess кэш Azure Redis с клиента кэша StackExchange.Redis hello.</span><span class="sxs-lookup"><span data-stu-id="81375-222">hello NuGet package downloads and adds hello required assembly references for your client application tooaccess Azure Redis Cache with hello StackExchange.Redis cache client.</span></span> <span data-ttu-id="81375-223">Если вы предпочитаете toouse версию со строгими именами hello `StackExchange.Redis` клиентской библиотеки, установка hello `StackExchange.Redis.StrongName` пакета.</span><span class="sxs-lookup"><span data-stu-id="81375-223">If you prefer toouse a strong-named version of hello `StackExchange.Redis` client library, install hello `StackExchange.Redis.StrongName` package.</span></span>
3. <span data-ttu-id="81375-224">В **обозревателе решений**, разверните hello **контроллеров** папку и дважды щелкните **TeamsController.cs** tooopen его.</span><span class="sxs-lookup"><span data-stu-id="81375-224">In **Solution Explorer**, expand hello **Controllers** folder and double-click **TeamsController.cs** tooopen it.</span></span>
   
    ![Контроллер команд][cache-teamscontroller]
4. <span data-ttu-id="81375-226">Добавьте следующие два hello `using` инструкций слишком**TeamsController.cs**.</span><span class="sxs-lookup"><span data-stu-id="81375-226">Add hello following two `using` statements too**TeamsController.cs**.</span></span>

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. <span data-ttu-id="81375-227">Добавьте следующие два свойства toohello hello `TeamsController` класса.</span><span class="sxs-lookup"><span data-stu-id="81375-227">Add hello following two properties toohello `TeamsController` class.</span></span>

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

6. <span data-ttu-id="81375-228">Создайте файл на компьютере с именем `WebAppPlusCacheAppSecrets.config` и поместите его в расположении, которое не будет возвращен с hello исходный код демонстрационного приложения, если вы решите toocheck его в другом.</span><span class="sxs-lookup"><span data-stu-id="81375-228">Create a file on your computer named `WebAppPlusCacheAppSecrets.config` and place it in a location that won't be checked in with hello source code of your sample application, should you decide toocheck it in somewhere.</span></span> <span data-ttu-id="81375-229">В этом примере hello `AppSettingsSecrets.config` находится в файле `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span><span class="sxs-lookup"><span data-stu-id="81375-229">In this example hello `AppSettingsSecrets.config` file is located at `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span></span>
   
    <span data-ttu-id="81375-230">Изменить hello `WebAppPlusCacheAppSecrets.config` и добавьте hello, следуя содержимое файла.</span><span class="sxs-lookup"><span data-stu-id="81375-230">Edit hello `WebAppPlusCacheAppSecrets.config` file and add hello following contents.</span></span> <span data-ttu-id="81375-231">При локальном запуске приложения hello эти сведения — экземпляр кэша Redis для Azure используется tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="81375-231">If you run hello application locally this information is used tooconnect tooyour Azure Redis Cache instance.</span></span> <span data-ttu-id="81375-232">Далее в учебнике hello вам подготовить экземпляр кэша Redis для Azure и обновите hello кэша имя и пароль.</span><span class="sxs-lookup"><span data-stu-id="81375-232">Later in hello tutorial you'll provision an Azure Redis Cache instance and update hello cache name and password.</span></span> <span data-ttu-id="81375-233">Если вы не собираетесь пример приложения hello toorun локально можно пропустить hello создания этого файла и hello последующие шаги, которые ссылаются на файл hello, поскольку при развертывании приложения hello tooAzure извлекает сведения о соединении hello кэша из приложение hello значение параметра для hello веб-приложения, а не из этого файла.</span><span class="sxs-lookup"><span data-stu-id="81375-233">If you don't plan toorun hello sample application locally you can skip hello creation of this file and hello subsequent steps that reference hello file, because when you deploy tooAzure hello application retrieves hello cache connection information from hello app setting for hello Web App and not from this file.</span></span> <span data-ttu-id="81375-234">С момента hello `WebAppPlusCacheAppSecrets.config` развернуто tooAzure вместе с приложением, это не требуется, пока не будет toorun приложения hello локально.</span><span class="sxs-lookup"><span data-stu-id="81375-234">Since hello `WebAppPlusCacheAppSecrets.config` is not deployed tooAzure with your application, you don't need it unless you are going toorun hello application locally.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="81375-235">В **обозревателе решений**, дважды щелкните **web.config** tooopen его.</span><span class="sxs-lookup"><span data-stu-id="81375-235">In **Solution Explorer**, double-click **web.config** tooopen it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="81375-237">Добавьте следующее hello `file` атрибута toohello `appSettings` элемента.</span><span class="sxs-lookup"><span data-stu-id="81375-237">Add hello following `file` attribute toohello `appSettings` element.</span></span> <span data-ttu-id="81375-238">Если вы использовали другое имя файла или в другом расположении, замените эти значения для тех, которые показаны в примере hello hello.</span><span class="sxs-lookup"><span data-stu-id="81375-238">If you used a different file name or location, substitute those values for hello ones shown in hello example.</span></span>
   
   * <span data-ttu-id="81375-239">До: `<appSettings>`</span><span class="sxs-lookup"><span data-stu-id="81375-239">Before: `<appSettings>`</span></span>
   * <span data-ttu-id="81375-240">После: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span><span class="sxs-lookup"><span data-stu-id="81375-240">After: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span></span>
     
   <span data-ttu-id="81375-241">Среда выполнения ASP.NET Hello объединяет содержимое hello hello внешнего файла с разметкой hello в hello `<appSettings>` элемента.</span><span class="sxs-lookup"><span data-stu-id="81375-241">hello ASP.NET runtime merges hello contents of hello external file with hello markup in hello `<appSettings>` element.</span></span> <span data-ttu-id="81375-242">Среда выполнения Hello игнорирует hello атрибут файла, если не удается найти указанный файл hello.</span><span class="sxs-lookup"><span data-stu-id="81375-242">hello runtime ignores hello file attribute if hello specified file cannot be found.</span></span> <span data-ttu-id="81375-243">Своих секретов (кэш tooyour строку hello подключений) не включаются в состав hello исходного кода для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="81375-243">Your secrets (hello connection string tooyour cache) are not included as part of hello source code for hello application.</span></span> <span data-ttu-id="81375-244">При развертывании вашей tooAzure web app, hello `WebAppPlusCacheAppSecrests.config` файл не будет развернут (то есть, при необходимости).</span><span class="sxs-lookup"><span data-stu-id="81375-244">When you deploy your web app tooAzure, hello `WebAppPlusCacheAppSecrests.config` file won't be deployed (that's what you want).</span></span> <span data-ttu-id="81375-245">Существует несколько способов toospecify эти секретные данные в Azure, и в этом учебнике они настраиваются автоматически при вы [подготовки hello ресурсы Azure](#provision-the-azure-resources) в следующем шаге руководства.</span><span class="sxs-lookup"><span data-stu-id="81375-245">There are several ways toospecify these secrets in Azure, and in this tutorial they are configured automatically for you when you [provision hello Azure resources](#provision-the-azure-resources) in a subsequent tutorial step.</span></span> <span data-ttu-id="81375-246">Дополнительные сведения о работе с секретными данными в Azure см. в разделе [советы и рекомендации по развертыванию пароли и другие конфиденциальные данные tooASP.NET и службе приложений Azure](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span><span class="sxs-lookup"><span data-stu-id="81375-246">For more information about working with secrets in Azure, see [Best practices for deploying passwords and other sensitive data tooASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span></span>

### <a name="update-hello-teamscontroller-class-tooreturn-results-from-hello-cache-or-hello-database"></a><span data-ttu-id="81375-247">Обновление результатов hello TeamsController класса tooreturn из кэша hello или hello базы данных</span><span class="sxs-lookup"><span data-stu-id="81375-247">Update hello TeamsController class tooreturn results from hello cache or hello database</span></span>
<span data-ttu-id="81375-248">В этом образце Статистика команды можно получить из базы данных hello или из кэша hello.</span><span class="sxs-lookup"><span data-stu-id="81375-248">In this sample, team statistics can be retrieved from hello database or from hello cache.</span></span> <span data-ttu-id="81375-249">Статистика команды хранятся в кэше hello как сериализованный `List<Team>`, а также как отсортированный набор, используя типы данных Redis.</span><span class="sxs-lookup"><span data-stu-id="81375-249">Team statistics are stored in hello cache as a serialized `List<Team>`, and also as a sorted set using Redis data types.</span></span> <span data-ttu-id="81375-250">Из отсортированного набора можно извлечь все или некоторые элементы или же запросить определенные элементы.</span><span class="sxs-lookup"><span data-stu-id="81375-250">When retrieving items from a sorted set, you can retrieve some, all, or query for certain items.</span></span> <span data-ttu-id="81375-251">В этом образце запросы будут отсортированы hello набор для 5 команд с верхней hello отсортированные по количеству wins.</span><span class="sxs-lookup"><span data-stu-id="81375-251">In this sample you'll query hello sorted set for hello top 5 teams ranked by number of wins.</span></span>

> [!NOTE]
> <span data-ttu-id="81375-252">Это не требуется toostore Статистика команды hello в различных форматах в кэше hello в порядке toouse кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="81375-252">It is not required toostore hello team statistics in multiple formats in hello cache in order toouse Azure Redis Cache.</span></span> <span data-ttu-id="81375-253">В этом учебнике используется несколько форматов toodemonstrate некоторые toocache данные можно использовать различные способы hello и различных типов данных.</span><span class="sxs-lookup"><span data-stu-id="81375-253">This tutorial uses multiple formats toodemonstrate some of hello different ways and different data types you can use toocache data.</span></span>
> 
> 

1. <span data-ttu-id="81375-254">Добавьте следующее hello `using` toohello инструкций `TeamsController.cs` файла вверху hello с hello других `using` инструкции.</span><span class="sxs-lookup"><span data-stu-id="81375-254">Add hello following `using` statements toohello `TeamsController.cs` file at hello top with hello other `using` statements.</span></span>

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. <span data-ttu-id="81375-255">Замените текущий hello `public ActionResult Index()` реализации метода с hello следующие реализации.</span><span class="sxs-lookup"><span data-stu-id="81375-255">Replace hello current `public ActionResult Index()` method implementation with hello following implementation.</span></span>

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


1. <span data-ttu-id="81375-256">Добавьте следующие три метода toohello hello `TeamsController` hello класс tooimplement `playGames`, `clearCache`, и `rebuildDB` типы действий из hello switch можно добавить в предыдущем фрагменте кода hello.</span><span class="sxs-lookup"><span data-stu-id="81375-256">Add hello following three methods toohello `TeamsController` class tooimplement hello `playGames`, `clearCache`, and `rebuildDB` action types from hello switch statement added in hello previous code snippet.</span></span>
   
    <span data-ttu-id="81375-257">Hello `PlayGames` метод обновляет статистику team hello имитируя сезон игр, сохраняет hello базу данных результатов toohello и очищает hello теперь устаревшие данные из кэша hello.</span><span class="sxs-lookup"><span data-stu-id="81375-257">hello `PlayGames` method updates hello team statistics by simulating a season of games, saves hello results toohello database, and clears hello now outdated data from hello cache.</span></span>

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

    <span data-ttu-id="81375-258">Hello `RebuildDB` метод повторно hello базы данных по умолчанию hello набор команд, создает статистику для них и очищает hello теперь устаревшие данные из кэша hello.</span><span class="sxs-lookup"><span data-stu-id="81375-258">hello `RebuildDB` method reinitializes hello database with hello default set of teams, generates statistics for them, and clears hello now outdated data from hello cache.</span></span>

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

    <span data-ttu-id="81375-259">Hello `ClearCachedTeams` метод удаляет все статистические данные, кэшированные команды из кэша hello.</span><span class="sxs-lookup"><span data-stu-id="81375-259">hello `ClearCachedTeams` method removes any cached team statistics from hello cache.</span></span>

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. <span data-ttu-id="81375-260">Добавьте следующие четыре метода toohello hello `TeamsController` класса tooimplement hello различные способы получения Статистика команды hello кэша hello и hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="81375-260">Add hello following four methods toohello `TeamsController` class tooimplement hello various ways of retrieving hello team statistics from hello cache and hello database.</span></span> <span data-ttu-id="81375-261">Каждый из этих методов возвращает `List<Team>` которого отображается в представлении hello.</span><span class="sxs-lookup"><span data-stu-id="81375-261">Each of these methods returns a `List<Team>` which is then displayed by hello view.</span></span>
   
    <span data-ttu-id="81375-262">Hello `GetFromDB` метод считывает hello Статистика команды из базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="81375-262">hello `GetFromDB` method reads hello team statistics from hello database.</span></span>
   
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

    <span data-ttu-id="81375-263">Hello `GetFromList` метод считывает Статистика команды hello из кэша как сериализованный `List<Team>`.</span><span class="sxs-lookup"><span data-stu-id="81375-263">hello `GetFromList` method reads hello team statistics from cache as a serialized `List<Team>`.</span></span> <span data-ttu-id="81375-264">В случае пропуска кэша hello Статистика команды чтения из базы данных hello и затем сохраняются в кэше hello следующего.</span><span class="sxs-lookup"><span data-stu-id="81375-264">If there is a cache miss, hello team statistics are read from hello database and then stored in hello cache for next time.</span></span> <span data-ttu-id="81375-265">В этом примере мы используем JSON.NET сериализации tooserialize hello .NET объекты tooand из кэша hello.</span><span class="sxs-lookup"><span data-stu-id="81375-265">In this sample we're using JSON.NET serialization tooserialize hello .NET objects tooand from hello cache.</span></span> <span data-ttu-id="81375-266">Дополнительные сведения см. в разделе [toowork в .NET Framework объектов в кэше Redis для Azure](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span><span class="sxs-lookup"><span data-stu-id="81375-266">For more information, see [How toowork with .NET objects in Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span></span>

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

    <span data-ttu-id="81375-267">Hello `GetFromSortedSet` метод считывает Статистика команды hello из кэшированных отсортированного набора.</span><span class="sxs-lookup"><span data-stu-id="81375-267">hello `GetFromSortedSet` method reads hello team statistics from a cached sorted set.</span></span> <span data-ttu-id="81375-268">В случае пропуска кэша hello Статистика команды чтения из базы данных hello и хранящиеся в кэше hello как упорядоченный набор.</span><span class="sxs-lookup"><span data-stu-id="81375-268">If there is a cache miss, hello team statistics are read from hello database and stored in hello cache as a sorted set.</span></span>

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

    <span data-ttu-id="81375-269">Hello `GetFromSortedSetTop5` метод считывает hello top набор 5 команд от кэширования hello отсортированы.</span><span class="sxs-lookup"><span data-stu-id="81375-269">hello `GetFromSortedSetTop5` method reads hello top 5 teams from hello cached sorted set.</span></span> <span data-ttu-id="81375-270">Он начинает с проверки кэша hello наличие hello hello `teamsSortedSet` ключа.</span><span class="sxs-lookup"><span data-stu-id="81375-270">It starts by checking hello cache for hello existence of hello `teamsSortedSet` key.</span></span> <span data-ttu-id="81375-271">Если этот параметр не указан, hello `GetFromSortedSet` метод вызывается Статистика команды tooread hello и сохранять их в кэш hello.</span><span class="sxs-lookup"><span data-stu-id="81375-271">If this key is not present, hello `GetFromSortedSet` method is called tooread hello team statistics and store them in hello cache.</span></span> <span data-ttu-id="81375-272">Далее hello кэшированных отсортированный набор отправляет запрос top hello 5 команд, которые возвращаются.</span><span class="sxs-lookup"><span data-stu-id="81375-272">Next, hello cached sorted set is queried for hello top 5 teams which are returned.</span></span>

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

### <a name="update-hello-create-edit-and-delete-methods-toowork-with-hello-cache"></a><span data-ttu-id="81375-273">Hello создание, изменение, обновления и удаления toowork методы с кэшем hello</span><span class="sxs-lookup"><span data-stu-id="81375-273">Update hello Create, Edit, and Delete methods toowork with hello cache</span></span>
<span data-ttu-id="81375-274">Hello формирование шаблонов код, который был создан как части данного примера включает методы tooadd, изменение и удаление групп.</span><span class="sxs-lookup"><span data-stu-id="81375-274">hello scaffolding code that was generated as part of this sample includes methods tooadd, edit, and delete teams.</span></span> <span data-ttu-id="81375-275">Каждый раз, когда добавляется, изменить или удалить команды, hello данные в кэше hello станет устаревшим.</span><span class="sxs-lookup"><span data-stu-id="81375-275">Anytime a team is added, edited, or removed, hello data in hello cache becomes outdated.</span></span> <span data-ttu-id="81375-276">В данном разделе, необходимо изменить эти три метода tooclear hello кэшированных команды, чтобы кэш hello не будет синхронизирован с hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="81375-276">In this section you'll modify these three methods tooclear hello cached teams so that hello cache won't be out of sync with hello database.</span></span>

1. <span data-ttu-id="81375-277">Обзор toohello `Create(Team team)` метод в hello `TeamsController` класса.</span><span class="sxs-lookup"><span data-stu-id="81375-277">Browse toohello `Create(Team team)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="81375-278">Добавить toohello вызов `ClearCachedTeams` метода, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="81375-278">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

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


1. <span data-ttu-id="81375-279">Обзор toohello `Edit(Team team)` метод в hello `TeamsController` класса.</span><span class="sxs-lookup"><span data-stu-id="81375-279">Browse toohello `Edit(Team team)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="81375-280">Добавить toohello вызов `ClearCachedTeams` метода, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="81375-280">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

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


1. <span data-ttu-id="81375-281">Обзор toohello `DeleteConfirmed(int id)` метод в hello `TeamsController` класса.</span><span class="sxs-lookup"><span data-stu-id="81375-281">Browse toohello `DeleteConfirmed(int id)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="81375-282">Добавить toohello вызов `ClearCachedTeams` метода, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="81375-282">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

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


### <a name="update-hello-teams-index-view-toowork-with-hello-cache"></a><span data-ttu-id="81375-283">Обновить представление toowork hello индекс команды с кэшем hello</span><span class="sxs-lookup"><span data-stu-id="81375-283">Update hello Teams Index view toowork with hello cache</span></span>
1. <span data-ttu-id="81375-284">В **обозревателе решений**, разверните hello **представления** папки, а затем hello **команды** папку и дважды щелкните **Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="81375-284">In **Solution Explorer**, expand hello **Views** folder, then hello **Teams** folder, and double-click **Index.cshtml**.</span></span>
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. <span data-ttu-id="81375-286">Вверху hello файл hello найдите следующий абзац элементом hello.</span><span class="sxs-lookup"><span data-stu-id="81375-286">Near hello top of hello file, look for hello following paragraph element.</span></span>
   
    ![Таблица действий][cache-teams-index-table]
   
    <span data-ttu-id="81375-288">Это toocreate ссылку hello новой команды.</span><span class="sxs-lookup"><span data-stu-id="81375-288">This is hello link toocreate a new team.</span></span> <span data-ttu-id="81375-289">Замените элемент абзаца hello hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="81375-289">Replace hello paragraph element with hello following table.</span></span> <span data-ttu-id="81375-290">Эта таблица содержит ссылки на действия для создания новых команд, воспроизведение новый сезон игр, очистка кэша hello, извлечение hello команды из кэша hello в нескольких форматах, получении hello команды из базы данных hello и перестроения hello базы данных с данными нового образца.</span><span class="sxs-lookup"><span data-stu-id="81375-290">This table has action links for creating a new team, playing a new season of games, clearing hello cache, retrieving hello teams from hello cache in several formats, retrieving hello teams from hello database, and rebuilding hello database with fresh sample data.</span></span>

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


1. <span data-ttu-id="81375-291">Прокрутки внизу toohello hello **Index.cshtml** файл и добавьте следующее hello `tr` элемент, чтобы оно было hello последняя строка hello последнего в таблицу файл hello.</span><span class="sxs-lookup"><span data-stu-id="81375-291">Scroll toohello bottom of hello **Index.cshtml** file and add hello following `tr` element so that it is hello last row in hello last table in hello file.</span></span>
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    <span data-ttu-id="81375-292">Эта строка содержит значение hello `ViewBag.Msg` , содержащее отчет о состоянии о hello текущей операции.</span><span class="sxs-lookup"><span data-stu-id="81375-292">This row displays hello value of `ViewBag.Msg` which contains a status report about hello current operation.</span></span> <span data-ttu-id="81375-293">Hello `ViewBag.Msg` устанавливается при нажатии кнопки ссылки действия hello из предыдущего шага hello.</span><span class="sxs-lookup"><span data-stu-id="81375-293">hello `ViewBag.Msg` is set when you click any of hello action links from hello previous step.</span></span>   
   
    ![Сообщение о состоянии][cache-status-message]
2. <span data-ttu-id="81375-295">Нажмите клавишу **F6** toobuild hello проекта.</span><span class="sxs-lookup"><span data-stu-id="81375-295">Press **F6** toobuild hello project.</span></span>

## <a name="provision-hello-azure-resources"></a><span data-ttu-id="81375-296">Подготовка к работе hello ресурсы Azure</span><span class="sxs-lookup"><span data-stu-id="81375-296">Provision hello Azure resources</span></span>
<span data-ttu-id="81375-297">toohost вашего приложения в Azure, необходимо сначала подготовить hello служб Azure, которые требуются приложению.</span><span class="sxs-lookup"><span data-stu-id="81375-297">toohost your application in Azure, you must first provision hello Azure services that your application requires.</span></span> <span data-ttu-id="81375-298">Пример приложения Hello в этом учебнике используется hello следующих служб Azure.</span><span class="sxs-lookup"><span data-stu-id="81375-298">hello sample application in this tutorial uses hello following Azure services.</span></span>

* <span data-ttu-id="81375-299">кэш Azure Redis</span><span class="sxs-lookup"><span data-stu-id="81375-299">Azure Redis Cache</span></span>
* <span data-ttu-id="81375-300">веб-приложение службы приложений;</span><span class="sxs-lookup"><span data-stu-id="81375-300">App Service Web App</span></span>
* <span data-ttu-id="81375-301">База данных SQL</span><span class="sxs-lookup"><span data-stu-id="81375-301">SQL Database</span></span>

<span data-ttu-id="81375-302">toodeploy эти группы ресурсов новой или существующей службы tooa по своему усмотрению, щелкните следующие hello **развертывание tooAzure** кнопки.</span><span class="sxs-lookup"><span data-stu-id="81375-302">toodeploy these services tooa new or existing resource group of your choice, click hello following **Deploy tooAzure** button.</span></span>

<span data-ttu-id="81375-303">[! [Развертывание tooAzure] [deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="81375-303">[![Deploy tooAzure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span></span>

<span data-ttu-id="81375-304">Это **развертывание tooAzure** кнопка использует hello [Создание веб-приложения, а также кэша Redis, а также базы данных SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [быстрый запуск Azure](https://github.com/Azure/azure-quickstart-templates) tooprovision шаблона эти службы и набор hello Строка подключения для hello базы данных SQL и hello параметр приложения для hello строку подключения для кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="81375-304">This **Deploy tooAzure** button uses hello [Create a Web App plus Redis Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) template tooprovision these services and set hello connection string for hello SQL Database and hello application setting for hello Azure Redis Cache connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="81375-305">Если у вас нет учетной записи Azure, можно [создать бесплатную учетную запись Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="81375-305">If you don't have an Azure account, you can [create a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in just a couple of minutes.</span></span>
> 
> 

<span data-ttu-id="81375-306">Выбрав hello **развертывание tooAzure** кнопка позволяет toohello портал Azure и инициирует hello процесс создания ресурсов hello, описываемого hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="81375-306">Clicking hello **Deploy tooAzure** button takes you toohello Azure portal and initiates hello process of creating hello resources described by hello template.</span></span>

![Развертывание tooAzure][cache-deploy-to-azure-step-1]

1. <span data-ttu-id="81375-308">В hello **основы** статьи выберите toouse hello подписки Azure и выберите существующую группу ресурсов или создайте новый и указать расположение группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="81375-308">In hello **Basics** section, select hello Azure subscription toouse, and select an existing resource group or create a new one, and specify hello resource group location.</span></span>
2. <span data-ttu-id="81375-309">В hello **параметры** укажите **входа администратора** (не используйте **администратора**), **пароль входа администратора**и  **Имя базы данных**.</span><span class="sxs-lookup"><span data-stu-id="81375-309">In hello **Settings** section, specify an **Administrator Login** (don't use **admin**), **Administrator Login Password**, and **Database Name**.</span></span> <span data-ttu-id="81375-310">Hello других параметров, настроенных для размещения плана и экономичные варианты для hello базы данных SQL и кэша Redis для Azure, которые не входят в состав бесплатный уровень бесплатной службы приложения.</span><span class="sxs-lookup"><span data-stu-id="81375-310">hello other parameters are configured for a free App Service hosting plan, and lower-cost options for hello SQL Database and Azure Redis Cache, which don't come with a free tier.</span></span>

    ![Развертывание tooAzure][cache-deploy-to-azure-step-2]

3. <span data-ttu-id="81375-312">После настройки параметров требуемого hello, прокрутите toohello конец страницы приветствия, чтения hello условий и проверки hello **я принимаю условия, указанных выше, toohello** флажок.</span><span class="sxs-lookup"><span data-stu-id="81375-312">After configuring hello desired settings, scroll toohello end of hello page, read hello terms and conditions, and check hello **I agree toohello terms and conditions stated above** checkbox.</span></span>
4. <span data-ttu-id="81375-313">Щелкните toobegin подготовки и предоставления ресурсов hello, **покупки**.</span><span class="sxs-lookup"><span data-stu-id="81375-313">toobegin provisioning hello resources, click **Purchase**.</span></span>

<span data-ttu-id="81375-314">tooview hello хода выполнения развертывания, щелкните значок уведомления hello и нажмите кнопку **начато развертывание**.</span><span class="sxs-lookup"><span data-stu-id="81375-314">tooview hello progress of your deployment, click hello notification icon and click **Deployment started**.</span></span>

![Развертывание начато][cache-deployment-started]

<span data-ttu-id="81375-316">Hello состояние развертывания можно посмотреть на hello **Microsoft.Template** колонку.</span><span class="sxs-lookup"><span data-stu-id="81375-316">You can view hello status of your deployment on hello **Microsoft.Template** blade.</span></span>

![Развертывание tooAzure][cache-deploy-to-azure-step-3]

<span data-ttu-id="81375-318">После завершения подготовки можно опубликовать tooAzure вашего приложения из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="81375-318">When provisioning is complete, you can publish your application tooAzure from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="81375-319">Все ошибки, возникающие во время процесса инициализации hello, отображаются на hello **Microsoft.Template** колонку.</span><span class="sxs-lookup"><span data-stu-id="81375-319">Any errors that may occur during hello provisioning process are displayed on hello **Microsoft.Template** blade.</span></span> <span data-ttu-id="81375-320">Среди распространенных ошибок — слишком много ошибок, связанных с SQL Server или планами размещения служб приложений уровня "Бесплатный" на подписку.</span><span class="sxs-lookup"><span data-stu-id="81375-320">Common errors are too many SQL Servers or too many Free App Service hosting plans per subscription.</span></span> <span data-ttu-id="81375-321">Исправьте все ошибки и перезапустите процесс hello, нажав кнопку **повторно развернуть** на hello **Microsoft.Template** колонке или hello **развертывание tooAzure** кнопки в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="81375-321">Resolve any errors and restart hello process by clicking **Redeploy** on hello **Microsoft.Template** blade or hello **Deploy tooAzure** button in this tutorial.</span></span>
> 
> 

## <a name="publish-hello-application-tooazure"></a><span data-ttu-id="81375-322">Публикация приложения tooAzure hello</span><span class="sxs-lookup"><span data-stu-id="81375-322">Publish hello application tooAzure</span></span>
<span data-ttu-id="81375-323">На этом шаге учебника hello будет публиковать tooAzure приложения hello и запустите его в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="81375-323">In this step of hello tutorial, you'll publish hello application tooAzure and run it in hello cloud.</span></span>

1. <span data-ttu-id="81375-324">Щелкните правой кнопкой мыши hello **ContosoTeamStats** проекта в Visual Studio и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="81375-324">Right-click hello **ContosoTeamStats** project in Visual Studio and choose **Publish**.</span></span>
   
    ![Опубликовать][cache-publish-app]
2. <span data-ttu-id="81375-326">Щелкните элемент **Служба приложений Microsoft Azure**, выберите параметр **Выбрать существующую** и нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="81375-326">Click **Microsoft Azure App Service**, choose **Select Existing**, and click **Publish**.</span></span>
   
    ![Опубликовать][cache-publish-to-app-service]
3. <span data-ttu-id="81375-328">Выберите подписку hello, используется при создании hello ресурсы Azure, разверните группу ресурсов hello, содержащий ресурсы hello и выберите hello требуемого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="81375-328">Select hello subscription used when creating hello Azure resources, expand hello resource group containing hello resources, and select hello desired Web App.</span></span> <span data-ttu-id="81375-329">Если вы использовали hello **развертывание tooAzure** кнопка запускает ваше имя веб-приложения с **веб-сайт** следуют некоторые дополнительные символы.</span><span class="sxs-lookup"><span data-stu-id="81375-329">If you used hello **Deploy tooAzure** button your Web App name starts with **webSite** followed by some additional characters.</span></span>
   
    ![Выбор веб-приложения][cache-select-web-app]
4. <span data-ttu-id="81375-331">Нажмите кнопку **ОК** hello toobegin процесс публикации.</span><span class="sxs-lookup"><span data-stu-id="81375-331">Click **OK** toobegin hello publishing process.</span></span> <span data-ttu-id="81375-332">Через несколько секунд завершает процесс публикации hello и запустить браузер с управлением образец приложения hello.</span><span class="sxs-lookup"><span data-stu-id="81375-332">After a few moments hello publishing process completes and a browser is launched with hello running sample application.</span></span> <span data-ttu-id="81375-333">Если возникает ошибка при проверке или публикации DNS, а hello процесс для подготовки hello ресурсы Azure для приложения hello совсем недавно завершена, подождите немного и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="81375-333">If you get a DNS error when validating or publishing, and hello provisioning process for hello Azure resources for hello application has just recently completed, wait a moment and try again.</span></span>
   
    ![Кэш добавлен][cache-added-to-application]

<span data-ttu-id="81375-335">Hello Следующая таблица описывает ссылку каждого действия из образца приложения hello.</span><span class="sxs-lookup"><span data-stu-id="81375-335">hello following table describes each action link from hello sample application.</span></span>

| <span data-ttu-id="81375-336">Действие</span><span class="sxs-lookup"><span data-stu-id="81375-336">Action</span></span> | <span data-ttu-id="81375-337">Описание</span><span class="sxs-lookup"><span data-stu-id="81375-337">Description</span></span> |
| --- | --- |
| <span data-ttu-id="81375-338">Создать</span><span class="sxs-lookup"><span data-stu-id="81375-338">Create New</span></span> |<span data-ttu-id="81375-339">Создание команды.</span><span class="sxs-lookup"><span data-stu-id="81375-339">Create a new Team.</span></span> |
| <span data-ttu-id="81375-340">Воспроизвести сезон</span><span class="sxs-lookup"><span data-stu-id="81375-340">Play Season</span></span> |<span data-ttu-id="81375-341">Воспроизведение сезон игр stats команды update hello, и снимите все устаревшие данные из группы данных из кэша hello.</span><span class="sxs-lookup"><span data-stu-id="81375-341">Play a season of games, update hello team stats, and clear any outdated team data from hello cache.</span></span> |
| <span data-ttu-id="81375-342">Очистить кэш</span><span class="sxs-lookup"><span data-stu-id="81375-342">Clear Cache</span></span> |<span data-ttu-id="81375-343">Статистика команды Очистить hello из кэша hello.</span><span class="sxs-lookup"><span data-stu-id="81375-343">Clear hello team stats from hello cache.</span></span> |
| <span data-ttu-id="81375-344">List from Cache (Перечислить из кэша)</span><span class="sxs-lookup"><span data-stu-id="81375-344">List from Cache</span></span> |<span data-ttu-id="81375-345">Получение статистики команды hello из кэша hello.</span><span class="sxs-lookup"><span data-stu-id="81375-345">Retrieve hello team stats from hello cache.</span></span> <span data-ttu-id="81375-346">В случае пропуска кэша загрузить hello статистики из базы данных hello и сохранить toohello кэша при следующем.</span><span class="sxs-lookup"><span data-stu-id="81375-346">If there is a cache miss, load hello stats from hello database and save toohello cache for next time.</span></span> |
| <span data-ttu-id="81375-347">Sorted Set from Cache (Отсортированный набор из кэша)</span><span class="sxs-lookup"><span data-stu-id="81375-347">Sorted Set from Cache</span></span> |<span data-ttu-id="81375-348">Получение статистики hello team из кэша hello, с помощью упорядоченного набора.</span><span class="sxs-lookup"><span data-stu-id="81375-348">Retrieve hello team stats from hello cache using a sorted set.</span></span> <span data-ttu-id="81375-349">В случае пропуска кэша загрузить hello статистики из базы данных hello и сохранить toohello кэша с помощью упорядоченного набора.</span><span class="sxs-lookup"><span data-stu-id="81375-349">If there is a cache miss, load hello stats from hello database and save toohello cache using a sorted set.</span></span> |
| <span data-ttu-id="81375-350">Top 5 Teams from Cache (5 лучших команд из кэша)</span><span class="sxs-lookup"><span data-stu-id="81375-350">Top 5 Teams from Cache</span></span> |<span data-ttu-id="81375-351">Получить hello top 5 команды из кэша hello, с использованием упорядоченного набора.</span><span class="sxs-lookup"><span data-stu-id="81375-351">Retrieve hello top 5 teams from hello cache using a sorted set.</span></span> <span data-ttu-id="81375-352">В случае пропуска кэша загрузить hello статистики из базы данных hello и сохранить toohello кэша с помощью упорядоченного набора.</span><span class="sxs-lookup"><span data-stu-id="81375-352">If there is a cache miss, load hello stats from hello database and save toohello cache using a sorted set.</span></span> |
| <span data-ttu-id="81375-353">Load from DB (Загрузить из базы данных)</span><span class="sxs-lookup"><span data-stu-id="81375-353">Load from DB</span></span> |<span data-ttu-id="81375-354">Получить hello team статистики из базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="81375-354">Retrieve hello team stats from hello database.</span></span> |
| <span data-ttu-id="81375-355">Rebuild DB (Перестроить базу данных)</span><span class="sxs-lookup"><span data-stu-id="81375-355">Rebuild DB</span></span> |<span data-ttu-id="81375-356">Перестроение базы данных hello и перезагрузить его с образцами данных команды.</span><span class="sxs-lookup"><span data-stu-id="81375-356">Rebuild hello database and reload it with sample team data.</span></span> |
| <span data-ttu-id="81375-357">Изменить; Сведения; Удалить</span><span class="sxs-lookup"><span data-stu-id="81375-357">Edit / Details / Delete</span></span> |<span data-ttu-id="81375-358">Изменение команды, просмотр сведений о команде, удаление команды.</span><span class="sxs-lookup"><span data-stu-id="81375-358">Edit a team, view details for a team, delete a team.</span></span> |

<span data-ttu-id="81375-359">Щелкните некоторых действиях hello и поэкспериментировать с извлечением hello данных из различных источников hello.</span><span class="sxs-lookup"><span data-stu-id="81375-359">Click some of hello actions and experiment with retrieving hello data from hello different sources.</span></span> <span data-ttu-id="81375-360">Не hello различия в hello время, затрачиваемое toocomplete hello различные способы получения данных hello hello базы данных и кэш hello.</span><span class="sxs-lookup"><span data-stu-id="81375-360">Not hello differences in hello time it takes toocomplete hello various ways of retrieving hello data from hello database and hello cache.</span></span>

## <a name="delete-hello-resources-when-you-are-finished-with-hello-application"></a><span data-ttu-id="81375-361">Удалить hello ресурсов при завершении работы с приложением hello</span><span class="sxs-lookup"><span data-stu-id="81375-361">Delete hello resources when you are finished with hello application</span></span>
<span data-ttu-id="81375-362">По окончании работы с учебного приложения hello образец hello Azure можно удалить ресурсы, используемые в порядке tooconserve стоимости и ресурсы.</span><span class="sxs-lookup"><span data-stu-id="81375-362">When you are finished with hello sample tutorial application, you can delete hello Azure resources used in order tooconserve cost and resources.</span></span> <span data-ttu-id="81375-363">При использовании hello **развертывание tooAzure** кнопку в hello [подготовки hello ресурсы Azure](#provision-the-azure-resources) раздел и все ресурсы, содержащиеся в hello же группе ресурсов, их можно удалить вместе в одном Операция, удалив hello группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="81375-363">If you use hello **Deploy tooAzure** button in hello [Provision hello Azure resources](#provision-the-azure-resources) section and all of your resources are contained in hello same resource group, you can delete them together in one operation by deleting hello resource group.</span></span>

1. <span data-ttu-id="81375-364">Войдите в toohello [портал Azure](https://portal.azure.com) и нажмите кнопку **групп ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="81375-364">Sign in toohello [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>
2. <span data-ttu-id="81375-365">Имя группы ресурсов в hello типа hello **фильтрации элементов...**  текстового поля.</span><span class="sxs-lookup"><span data-stu-id="81375-365">Type hello name of your resource group into hello **Filter items...** textbox.</span></span>
3. <span data-ttu-id="81375-366">Нажмите кнопку **...**  toohello справа от группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="81375-366">Click **...** toohello right of your resource group.</span></span>
4. <span data-ttu-id="81375-367">Нажмите кнопку **Delete**(Удалить).</span><span class="sxs-lookup"><span data-stu-id="81375-367">Click **Delete**.</span></span>
   
    ![Удалить][cache-delete-resource-group]
5. <span data-ttu-id="81375-369">Имя группы ресурсов и нажмите кнопку hello типа **удалить**.</span><span class="sxs-lookup"><span data-stu-id="81375-369">Type hello name of your resource group and click **Delete**.</span></span>
   
    ![Подтверждение удаления][cache-delete-confirm]

<span data-ttu-id="81375-371">После нескольких секунд hello ресурсов группы и все ее ресурсы автономной удаляются.</span><span class="sxs-lookup"><span data-stu-id="81375-371">After a few moments hello resource group and all of its contained resources are deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="81375-372">Обратите внимание, что при удалении группы ресурсов является необратимым, и что группа ресурсов "hello" и все ресурсы hello в нем будут безвозвратно удалены.</span><span class="sxs-lookup"><span data-stu-id="81375-372">Note that deleting a resource group is irreversible and that hello resource group and all hello resources in it are permanently deleted.</span></span> <span data-ttu-id="81375-373">Убедитесь, что вы случайно не удалите группы hello неправильный ресурсов или ресурсов.</span><span class="sxs-lookup"><span data-stu-id="81375-373">Make sure that you do not accidentally delete hello wrong resource group or resources.</span></span> <span data-ttu-id="81375-374">Если вы создали hello ресурсов для размещения в этом примере в существующую группу ресурсов, каждый ресурс можно удалить по отдельности из их соответствующих колонок.</span><span class="sxs-lookup"><span data-stu-id="81375-374">If you created hello resources for hosting this sample inside an existing resource group, you can delete each resource individually from their respective blades.</span></span>
> 
> 

## <a name="run-hello-sample-application-on-your-local-machine"></a><span data-ttu-id="81375-375">Запустить образец приложения hello на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="81375-375">Run hello sample application on your local machine</span></span>
<span data-ttu-id="81375-376">приложение hello toorun локально на компьютере, необходимо кэш Azure Redis экземпляра в какие toocache данных.</span><span class="sxs-lookup"><span data-stu-id="81375-376">toorun hello application locally on your machine, you need an Azure Redis Cache instance in which toocache your data.</span></span> 

* <span data-ttu-id="81375-377">Если опубликовали tooAzure вашего приложения, как описано в предыдущем разделе hello, можно использовать экземпляр кэша Redis для Azure hello, который был инициализирован во время выполнения этого шага.</span><span class="sxs-lookup"><span data-stu-id="81375-377">If you have published your application tooAzure as described in hello previous section, you can use hello Azure Redis Cache instance that was provisioned during that step.</span></span>
* <span data-ttu-id="81375-378">При наличии другого существующего экземпляра кэша Redis для Azure, можно использовать, toorun в этом примере локально.</span><span class="sxs-lookup"><span data-stu-id="81375-378">If you have another existing Azure Redis Cache instance, you can use that toorun this sample locally.</span></span>
* <span data-ttu-id="81375-379">Если вам требуется toocreate экземпляр кэша Redis для Azure, выполните действия hello в [создать кэш](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="81375-379">If you need toocreate an Azure Redis Cache instance, you can follow hello steps in [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

<span data-ttu-id="81375-380">После выбора или создания кэша toouse hello Обзор toohello кэша в hello портал Azure и получить hello [имя узла](cache-configure.md#properties) и [ключи доступа](cache-configure.md#access-keys) своего кэша.</span><span class="sxs-lookup"><span data-stu-id="81375-380">Once you have selected or created hello cache toouse, browse toohello cache in hello Azure portal and retrieve hello [host name](cache-configure.md#properties) and [access keys](cache-configure.md#access-keys) for your cache.</span></span> <span data-ttu-id="81375-381">Инструкции см. в разделе [Настройка параметров кэша Redis](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="81375-381">For instructions, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

1. <span data-ttu-id="81375-382">Откройте hello `WebAppPlusCacheAppSecrets.config` файл, созданный во время hello [Настройка toouse приложения hello кэша Redis](#configure-the-application-to-use-redis-cache) шаге этого учебника, используя любой редактор hello.</span><span class="sxs-lookup"><span data-stu-id="81375-382">Open hello `WebAppPlusCacheAppSecrets.config` file that you created during hello [Configure hello application toouse Redis Cache](#configure-the-application-to-use-redis-cache) step of this tutorial using hello editor of your choice.</span></span>
2. <span data-ttu-id="81375-383">Изменить hello `value` атрибута и замените `MyCache.redis.cache.windows.net` с hello [имя узла](cache-configure.md#properties) кэша и укажите либо hello [первичный или вторичный ключ](cache-configure.md#access-keys) кэша hello паролем.</span><span class="sxs-lookup"><span data-stu-id="81375-383">Edit hello `value` attribute and replace `MyCache.redis.cache.windows.net` with hello [host name](cache-configure.md#properties) of your cache, and specify either hello [primary or secondary key](cache-configure.md#access-keys) of your cache as hello password.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="81375-384">Нажмите клавишу **Ctrl + F5** toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="81375-384">Press **Ctrl+F5** toorun hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="81375-385">Обратите внимание, что кэш Здравствуйте, так как приложение hello, включая hello базы данных, выполняется локально, а hello кэша Redis размещается в Azure, может появиться toounder-выполнения hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="81375-385">Note that because hello application, including hello database, is running locally and hello Redis Cache is hosted in Azure, hello cache may appear toounder-perform hello database.</span></span> <span data-ttu-id="81375-386">Для наилучшей производительности hello клиентское приложение и экземпляр кэша Redis для Azure должны находиться в hello местоположения.</span><span class="sxs-lookup"><span data-stu-id="81375-386">For best performance, hello client application and Azure Redis Cache instance should be in hello same location.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="81375-387">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="81375-387">Next steps</span></span>
* <span data-ttu-id="81375-388">Дополнительные сведения о [Приступая к работе с ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) на hello [ASP.NET](http://asp.net/) сайта.</span><span class="sxs-lookup"><span data-stu-id="81375-388">Learn more about [Getting Started with ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) on hello [ASP.NET](http://asp.net/) site.</span></span>
* <span data-ttu-id="81375-389">Дополнительные примеры создания веб-приложение ASP.NET в службе приложений см. в разделе [создать и развернуть веб-приложение ASP.NET в службе приложений Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) из hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [Демонстрация](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="81375-389">For more examples of creating an ASP.NET Web App in App Service, see [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) from hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span>
  * <span data-ttu-id="81375-390">Дополнительные примеры использования из образца hello HealthClinic.biz, в разделе [примеры использования средств разработчика Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="81375-390">For more quickstarts from hello HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>
* <span data-ttu-id="81375-391">Дополнительные сведения о hello [код первого tooa новую базу данных](https://msdn.microsoft.com/data/jj193542) подход tooEntity платформа, которая используется в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="81375-391">Learn more about hello [Code first tooa new database](https://msdn.microsoft.com/data/jj193542) approach tooEntity Framework that's used in this tutorial.</span></span>
* <span data-ttu-id="81375-392">Узнайте больше о [веб-приложениях в службе приложений Azure](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="81375-392">Learn more about [web apps in Azure App Service](../app-service-web/app-service-web-overview.md).</span></span>
* <span data-ttu-id="81375-393">Узнайте, каким образом слишком[монитор](cache-how-to-monitor.md) кэш hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="81375-393">Learn how too[monitor](cache-how-to-monitor.md) your cache in hello Azure portal.</span></span>
* <span data-ttu-id="81375-394">Изучите возможности кэша Redis для Azure уровня Premium:</span><span class="sxs-lookup"><span data-stu-id="81375-394">Explore Azure Redis Cache premium features</span></span>
  
  * [<span data-ttu-id="81375-395">Как tooconfigure сохраняемости для кэша Redis Azure Premium</span><span class="sxs-lookup"><span data-stu-id="81375-395">How tooconfigure persistence for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-persistence.md)
  * [<span data-ttu-id="81375-396">Как tooconfigure кластеризации для кэша Redis Azure Premium</span><span class="sxs-lookup"><span data-stu-id="81375-396">How tooconfigure clustering for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-clustering.md)
  * [<span data-ttu-id="81375-397">Как поддерживают tooconfigure виртуальной сети для кэша Redis Azure Premium</span><span class="sxs-lookup"><span data-stu-id="81375-397">How tooconfigure Virtual Network support for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-vnet.md)
  * <span data-ttu-id="81375-398">В разделе hello [Azure Redis кэша часто задаваемые вопросы о](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) Дополнительные сведения о размере, пропускную способность и пропускную способность с кэши premium.</span><span class="sxs-lookup"><span data-stu-id="81375-398">See hello [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) for more details about size, throughput, and bandwidth with premium caches.</span></span>

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

