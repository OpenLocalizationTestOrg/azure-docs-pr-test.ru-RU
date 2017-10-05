---
title: "Как создать веб-приложение с использованием кэша Redis | Документация Майкрософт"
description: "Узнайте, как создать веб-приложение с использованием кэша Redis"
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
ms.openlocfilehash: f23f71cc01eccf17d36885f786de9a7517606803
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-web-app-with-redis-cache"></a><span data-ttu-id="059a6-103">Как создать веб-приложение с использованием кэша Redis</span><span class="sxs-lookup"><span data-stu-id="059a6-103">How to create a Web App with Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="059a6-104">.NET</span><span class="sxs-lookup"><span data-stu-id="059a6-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="059a6-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="059a6-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="059a6-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="059a6-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="059a6-107">Java</span><span class="sxs-lookup"><span data-stu-id="059a6-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="059a6-108">Python</span><span class="sxs-lookup"><span data-stu-id="059a6-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="059a6-109">В этом руководстве описано, как создать и развернуть веб-приложение ASP.NET в веб-приложение службы приложений Azure с помощью Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="059a6-109">This tutorial shows how to create and deploy an ASP.NET web application to a web app in Azure App Service using Visual Studio 2017.</span></span> <span data-ttu-id="059a6-110">В примере приложения отображается список статистических данных команды из базы данных и различные способы использования кэша Redis для Azure для хранения и извлечения данных из кэша.</span><span class="sxs-lookup"><span data-stu-id="059a6-110">The sample application displays a list of team statistics from a database and shows different ways to use Azure Redis Cache to store and retrieve data from the cache.</span></span> <span data-ttu-id="059a6-111">Завершив работу с руководством, вы получите рабочее веб-приложение, которое выполняет чтение и запись в базе данных, оптимизировано для работы с кэшем Redis для Azure и размещено в Azure.</span><span class="sxs-lookup"><span data-stu-id="059a6-111">When you complete the tutorial you'll have a running web app that reads and writes to a database, optimized with Azure Redis Cache, and hosted in Azure.</span></span>

<span data-ttu-id="059a6-112">Вы узнаете следующее:</span><span class="sxs-lookup"><span data-stu-id="059a6-112">You'll learn:</span></span>

* <span data-ttu-id="059a6-113">как создать веб-приложение ASP.NET MVC 5 в Visual Studio;</span><span class="sxs-lookup"><span data-stu-id="059a6-113">How to create an ASP.NET MVC 5 web application in Visual Studio.</span></span>
* <span data-ttu-id="059a6-114">как получить доступ к данным из базы данных с использованием Entity Framework;</span><span class="sxs-lookup"><span data-stu-id="059a6-114">How to access data from a database using Entity Framework.</span></span>
* <span data-ttu-id="059a6-115">как улучшить пропускную способность данных и снизить нагрузку на базу данных за счет хранения и извлечения данных с помощью кэша Redis для Azure;</span><span class="sxs-lookup"><span data-stu-id="059a6-115">How to improve data throughput and reduce database load by storing and retrieving data using Azure Redis Cache.</span></span>
* <span data-ttu-id="059a6-116">как получить 5 лучших команд с помощью отсортированного набора Redis;</span><span class="sxs-lookup"><span data-stu-id="059a6-116">How to use a Redis sorted set to retrieve the top 5 teams.</span></span>
* <span data-ttu-id="059a6-117">как подготовить ресурсы Azure к работе для приложения с помощью шаблона Resource Manager;</span><span class="sxs-lookup"><span data-stu-id="059a6-117">How to provision the Azure resources for the application using a Resource Manager template.</span></span>
* <span data-ttu-id="059a6-118">как опубликовать приложение в Azure с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="059a6-118">How to publish the application to Azure using Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="059a6-119">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="059a6-119">Prerequisites</span></span>
<span data-ttu-id="059a6-120">Для работы с этим руководством необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="059a6-120">To complete the tutorial, you must have the following prerequisites.</span></span>

* [<span data-ttu-id="059a6-121">Учетная запись Azure</span><span class="sxs-lookup"><span data-stu-id="059a6-121">Azure account</span></span>](#azure-account)
* [<span data-ttu-id="059a6-122">Visual Studio 2017 с пакетом Azure SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="059a6-122">Visual Studio 2017 with the Azure SDK for .NET</span></span>](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a><span data-ttu-id="059a6-123">Учетная запись Azure</span><span class="sxs-lookup"><span data-stu-id="059a6-123">Azure account</span></span>
<span data-ttu-id="059a6-124">Для работы с этим руководством требуется учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="059a6-124">You need an Azure account to complete the tutorial.</span></span> <span data-ttu-id="059a6-125">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="059a6-125">You can:</span></span>

* <span data-ttu-id="059a6-126">[Открыть бесплатную учетную запись Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="059a6-126">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="059a6-127">Вы получаете кредиты, которые можно использовать, чтобы попробовать платные службы Azure.</span><span class="sxs-lookup"><span data-stu-id="059a6-127">You get credits that can be used to try out paid Azure services.</span></span> <span data-ttu-id="059a6-128">После израсходования кредитов ваша учетная запись не исчезнет. Вы сможете использовать ее для работы с бесплатными службами и функциями Azure.</span><span class="sxs-lookup"><span data-stu-id="059a6-128">Even after the credits are used up, you can keep the account and use free Azure services and features.</span></span>
* <span data-ttu-id="059a6-129">[Активировать преимущества подписчика Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="059a6-129">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="059a6-130">Ваша подписка MSDN каждый месяц приносит вам кредиты, которые можно использовать для оплаты использования служб Azure.</span><span class="sxs-lookup"><span data-stu-id="059a6-130">Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

### <a name="visual-studio-2017-with-the-azure-sdk-for-net"></a><span data-ttu-id="059a6-131">Visual Studio 2017 с пакетом Azure SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="059a6-131">Visual Studio 2017 with the Azure SDK for .NET</span></span>
<span data-ttu-id="059a6-132">Это руководство написано для использования с Visual Studio 2017 с пакетом [Azure SDK для .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span><span class="sxs-lookup"><span data-stu-id="059a6-132">The tutorial is written for Visual Studio 2017 with the [Azure SDK for .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span></span> <span data-ttu-id="059a6-133">Пакет Azure SDK 2.9.5 входит в состав установщика Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="059a6-133">The Azure SDK 2.9.5 is included with the Visual Studio installer.</span></span>

<span data-ttu-id="059a6-134">Если у вас есть Visual Studio 2015, вы можете следовать инструкциям по использованию [пакета Azure SDK для .NET](../dotnet-sdk.md) 2.8.2 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="059a6-134">If you have Visual Studio 2015, you can follow the tutorial with the [Azure SDK for .NET](../dotnet-sdk.md) 2.8.2 or later.</span></span> <span data-ttu-id="059a6-135">[Скачайте последний пакет Azure SDK для Visual Studio 2015 отсюда](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="059a6-135">[Download the latest Azure SDK for Visual Studio 2015 here](http://go.microsoft.com/fwlink/?linkid=518003).</span></span> <span data-ttu-id="059a6-136">Будет автоматически установлена программа Visual Studio с пакетом SDK (если она еще не установлена).</span><span class="sxs-lookup"><span data-stu-id="059a6-136">Visual Studio is automatically installed with the SDK if you don't already have it.</span></span> <span data-ttu-id="059a6-137">Некоторые снимки экранов, приведенные в этом руководстве, могут отличаться от реальных.</span><span class="sxs-lookup"><span data-stu-id="059a6-137">Some screens may look different from the illustrations shown in this tutorial.</span></span>

<span data-ttu-id="059a6-138">Если на вашем компьютере установлена версия Visual Studio 2013, можно [скачать последнюю версию пакета Azure SDK для Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span><span class="sxs-lookup"><span data-stu-id="059a6-138">If you have Visual Studio 2013, you can [download the latest Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span></span> <span data-ttu-id="059a6-139">Некоторые снимки экранов, приведенные в этом руководстве, могут отличаться от реальных.</span><span class="sxs-lookup"><span data-stu-id="059a6-139">Some screens may look different from the illustrations shown in this tutorial.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="059a6-140">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="059a6-140">Create the Visual Studio project</span></span>
1. <span data-ttu-id="059a6-141">Откройте Visual Studio и щелкните **Файл**, **Создать**, **Проект**.</span><span class="sxs-lookup"><span data-stu-id="059a6-141">Open Visual Studio and click **File**, **New**, **Project**.</span></span>
2. <span data-ttu-id="059a6-142">Разверните узел **Visual C#** в списке **Шаблоны**, выберите **Облако** и щелкните **Веб-приложение ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="059a6-142">Expand the **Visual C#** node in the **Templates** list, select **Cloud**, and click **ASP.NET Web Application**.</span></span> <span data-ttu-id="059a6-143">Убедитесь, что выбрана платформа **.NET Framework 4.5.2** или ее более новая версия.</span><span class="sxs-lookup"><span data-stu-id="059a6-143">Ensure that **.NET Framework 4.5.2** or higher is selected.</span></span>  <span data-ttu-id="059a6-144">В текстовом поле **Имя** введите **ContosoTeamStats** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="059a6-144">Type **ContosoTeamStats** into the **Name** textbox and click **OK**.</span></span>
   
    ![Создание проекта][cache-create-project]
3. <span data-ttu-id="059a6-146">Выберите тип проекта **MVC**.</span><span class="sxs-lookup"><span data-stu-id="059a6-146">Select **MVC** as the project type.</span></span> 

    <span data-ttu-id="059a6-147">Для параметра **Проверка подлинности** обязательно укажите значение **Без проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="059a6-147">Ensure that **No Authentication** is specified for the **Authentication** settings.</span></span> <span data-ttu-id="059a6-148">В зависимости от установленной версии Visual Studio значение по умолчанию может быть другим.</span><span class="sxs-lookup"><span data-stu-id="059a6-148">Depending on your version of Visual Studio, the default may be set to something else.</span></span> <span data-ttu-id="059a6-149">Чтобы изменить его, щелкните **Изменить проверку подлинности** и выберите **Без проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="059a6-149">To change it, click **Change Authentication** and select **No Authentication**.</span></span>

    <span data-ttu-id="059a6-150">Если вы работаете в Visual Studio 2015, снимите флажок **Разместить в облаке**.</span><span class="sxs-lookup"><span data-stu-id="059a6-150">If you are following along with Visual Studio 2015, clear the **Host in the cloud** checkbox.</span></span> <span data-ttu-id="059a6-151">На следующих шагах руководства вы [подготовите ресурсы Azure к работе](#provision-the-azure-resources) и [опубликуете приложение в Azure](#publish-the-application-to-azure).</span><span class="sxs-lookup"><span data-stu-id="059a6-151">You'll [provision the Azure resources](#provision-the-azure-resources) and [publish the application to Azure](#publish-the-application-to-azure) in subsequent steps in the tutorial.</span></span> <span data-ttu-id="059a6-152">Пример подготовки веб-приложения службы приложений в Visual Studio с установленным флажком **Разместить в облаке** см. в статье [Развертывание веб-приложения ASP.NET в службе приложений Azure с помощью Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="059a6-152">For an example of provisioning an App Service web app from Visual Studio by leaving **Host in the cloud** checked, see [Get started with Web Apps in Azure App Service, using ASP.NET and Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
    ![Выбор шаблона проекта][cache-select-template]
4. <span data-ttu-id="059a6-154">Нажмите кнопку **ОК** , чтобы создать проект.</span><span class="sxs-lookup"><span data-stu-id="059a6-154">Click **OK** to create the project.</span></span>

## <a name="create-the-aspnet-mvc-application"></a><span data-ttu-id="059a6-155">Создание приложения ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="059a6-155">Create the ASP.NET MVC application</span></span>
<span data-ttu-id="059a6-156">В этом разделе руководства описывается создание базового приложения, которое выполняет чтение статистики команды из базы данных и отображает ее.</span><span class="sxs-lookup"><span data-stu-id="059a6-156">In this section of the tutorial, you'll create the basic application that reads and displays team statistics from a database.</span></span>

* [<span data-ttu-id="059a6-157">Добавление пакета Entity Framework NuGet</span><span class="sxs-lookup"><span data-stu-id="059a6-157">Add the Entity Framework NuGet package</span></span>](#add-the-entity-framework-nuget-package)
* [<span data-ttu-id="059a6-158">Добавление модели</span><span class="sxs-lookup"><span data-stu-id="059a6-158">Add the model</span></span>](#add-the-model)
* [<span data-ttu-id="059a6-159">Добавление контроллера</span><span class="sxs-lookup"><span data-stu-id="059a6-159">Add the controller</span></span>](#add-the-controller)
* [<span data-ttu-id="059a6-160">Настройка представлений</span><span class="sxs-lookup"><span data-stu-id="059a6-160">Configure the views</span></span>](#configure-the-views)

### <a name="add-the-entity-framework-nuget-package"></a><span data-ttu-id="059a6-161">Добавление пакета Entity Framework NuGet</span><span class="sxs-lookup"><span data-stu-id="059a6-161">Add the Entity Framework NuGet package</span></span>

1. <span data-ttu-id="059a6-162">В меню **Сервис** выберите **Диспетчер пакетов NuGet**, а затем — **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="059a6-162">Click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>
2. <span data-ttu-id="059a6-163">В окне **консоли диспетчера пакетов** запустите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="059a6-163">Run the following command from the **Package Manager Console** window.</span></span>
    
    ```
    Install-Package EntityFramework
    ```

<span data-ttu-id="059a6-164">Дополнительные сведения об этом пакете см. в документации [EntityFramework](https://www.nuget.org/packages/EntityFramework/).</span><span class="sxs-lookup"><span data-stu-id="059a6-164">For more information about this package, see the [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet page.</span></span>

### <a name="add-the-model"></a><span data-ttu-id="059a6-165">Добавление модели</span><span class="sxs-lookup"><span data-stu-id="059a6-165">Add the model</span></span>
1. <span data-ttu-id="059a6-166">В **обозревателе решений** щелкните правой кнопкой мыши папку **Модели**, а затем выберите **Добавить** и **Класс**.</span><span class="sxs-lookup"><span data-stu-id="059a6-166">Right-click **Models** in **Solution Explorer**, and choose **Add**, **Class**.</span></span> 
   
    ![Добавление модели][cache-model-add-class]
2. <span data-ttu-id="059a6-168">Введите `Team` в качестве имени класса и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="059a6-168">Enter `Team` for the class name and click **Add**.</span></span>
   
    ![Добавление класса модели][cache-model-add-class-dialog]
3. <span data-ttu-id="059a6-170">В начале файла `Team.cs` замените операторы `using` следующими операторами `using`:</span><span class="sxs-lookup"><span data-stu-id="059a6-170">Replace the `using` statements at the top of the `Team.cs` file with the following `using` statements.</span></span>

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. <span data-ttu-id="059a6-171">Замените определение класса `Team` приведенным ниже фрагментом кода с обновлением определения класса `Team`, а также некоторыми другими вспомогательными классами Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="059a6-171">Replace the definition of the `Team` class with the following code snippet that contains an updated `Team` class definition as well as some other Entity Framework helper classes.</span></span> <span data-ttu-id="059a6-172">Для дополнительных сведений о подходе Code First в Entity Framework, использованном в этом руководстве, см. видео в статье [Использование Code First для создания базы данных](https://msdn.microsoft.com/data/jj193542).</span><span class="sxs-lookup"><span data-stu-id="059a6-172">For more information on the code first approach to Entity Framework that's used in this tutorial, see [Code first to a new database](https://msdn.microsoft.com/data/jj193542).</span></span>

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


1. <span data-ttu-id="059a6-173">В **обозревателе решений** дважды щелкните файл **web.config**, чтобы открыть его.</span><span class="sxs-lookup"><span data-stu-id="059a6-173">In **Solution Explorer**, double-click **web.config** to open it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="059a6-175">Добавьте следующий раздел `connectionStrings`.</span><span class="sxs-lookup"><span data-stu-id="059a6-175">Add the following `connectionStrings` section.</span></span> <span data-ttu-id="059a6-176">Имя строки подключения должно соответствовать имени класса контекста базы данных Entity Framework ( `TeamContext`).</span><span class="sxs-lookup"><span data-stu-id="059a6-176">The name of the connection string must match the name of the Entity Framework database context class which is `TeamContext`.</span></span>

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="059a6-177">Вы можете добавить новый раздел `connectionStrings`, чтобы он следовал за разделом `configSections`, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="059a6-177">You can add the new `connectionStrings` section so that it follows `configSections`, as shown in the following example.</span></span>

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
    > <span data-ttu-id="059a6-178">Ваша строка подключения может отличаться. Это зависит от версии Visual Studio и выпуска SQL Server Express, используемых для завершения работы с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="059a6-178">Your connection string may be different depending on the version of Visual Studio and SQL Server Express edition used to complete the tutorial.</span></span> <span data-ttu-id="059a6-179">Шаблон web.config необходимо настроить в соответствии с установкой. Он может содержать записи `Data Source`, например `(LocalDB)\v11.0` (из SQL Server Express 2012) или `Data Source=(LocalDB)\MSSQLLocalDB` (из SQL Server Express 2014 и более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="059a6-179">The web.config template should be configured to match your installation, and may contain `Data Source` entries like `(LocalDB)\v11.0` (from SQL Server Express 2012) or `Data Source=(LocalDB)\MSSQLLocalDB` (from SQL Server Express 2014 and newer).</span></span> <span data-ttu-id="059a6-180">Дополнительные сведения о строках подключения и версиях SQL Express см. в статье о [LocalDB SQL Server 2016 Express](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span><span class="sxs-lookup"><span data-stu-id="059a6-180">For more information about connection strings and SQL Express versions, see [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) .</span></span>

### <a name="add-the-controller"></a><span data-ttu-id="059a6-181">Добавление контроллера</span><span class="sxs-lookup"><span data-stu-id="059a6-181">Add the controller</span></span>
1. <span data-ttu-id="059a6-182">Нажмите клавишу **F6** , чтобы скомпилировать проект.</span><span class="sxs-lookup"><span data-stu-id="059a6-182">Press **F6** to build the project.</span></span> 
2. <span data-ttu-id="059a6-183">В **обозревателе решений** щелкните правой кнопкой мыши папку **Контроллеры**, а затем выберите **Добавить** и **Контроллер**.</span><span class="sxs-lookup"><span data-stu-id="059a6-183">In **Solution Explorer**, right-click the **Controllers** folder and choose **Add**, **Controller**.</span></span>
   
    ![Добавление контролера][cache-add-controller]
3. <span data-ttu-id="059a6-185">Выберите **Контроллер MVC 5 с представлениями, использующий Entity Framework** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="059a6-185">Choose **MVC 5 Controller with views, using Entity Framework**, and click **Add**.</span></span> <span data-ttu-id="059a6-186">Если после нажатия кнопки **Добавить**появилась ошибка, убедитесь, что вы сначала скомпилировали проект.</span><span class="sxs-lookup"><span data-stu-id="059a6-186">If you get an error after clicking **Add**, ensure that you have built the project first.</span></span>
   
    ![Добавление класса контроллера][cache-add-controller-class]
4. <span data-ttu-id="059a6-188">В раскрывающемся списке **Класс модели** выберите **Team (ContosoTeamStats.Models)**.</span><span class="sxs-lookup"><span data-stu-id="059a6-188">Select **Team (ContosoTeamStats.Models)** from the **Model class** drop-down list.</span></span> <span data-ttu-id="059a6-189">В раскрывающемся списке **Класс контекста данных** выберите **TeamContext (ContosoTeamStats.Models)**.</span><span class="sxs-lookup"><span data-stu-id="059a6-189">Select **TeamContext (ContosoTeamStats.Models)** from the **Data context class** drop-down list.</span></span> <span data-ttu-id="059a6-190">Введите `TeamsController` в текстовое поле **Имя контроллера** (если оно не будет заполнено автоматически).</span><span class="sxs-lookup"><span data-stu-id="059a6-190">Type `TeamsController` in the **Controller** name textbox (if it is not automatically populated).</span></span> <span data-ttu-id="059a6-191">Нажмите кнопку **Добавить** , чтобы создать класс контроллера и добавить представления по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="059a6-191">Click **Add** to create the controller class and add the default views.</span></span>
   
    ![Настройка контроллера][cache-configure-controller]
5. <span data-ttu-id="059a6-193">В **обозревателе решений** разверните **Global.asax** и дважды щелкните файл **Global.asax.cs**, чтобы открыть его.</span><span class="sxs-lookup"><span data-stu-id="059a6-193">In **Solution Explorer**, expand **Global.asax** and double-click **Global.asax.cs** to open it.</span></span>
   
    ![Global.asax.cs][cache-global-asax]
6. <span data-ttu-id="059a6-195">В начале файла добавьте следующие два оператора `using` после остальных операторов `using`.</span><span class="sxs-lookup"><span data-stu-id="059a6-195">Add the following two `using` statements at the top of the file under the other `using` statements.</span></span>

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. <span data-ttu-id="059a6-196">В конце метода `Application_Start` добавьте следующую строку кода:</span><span class="sxs-lookup"><span data-stu-id="059a6-196">Add the following line of code at the end of the `Application_Start` method.</span></span>

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. <span data-ttu-id="059a6-197">В **обозревателе решений** разверните `App_Start` и дважды щелкните `RouteConfig.cs`.</span><span class="sxs-lookup"><span data-stu-id="059a6-197">In **Solution Explorer**, expand `App_Start` and double-click `RouteConfig.cs`.</span></span>
   
    ![RouteConfig.cs.][cache-RouteConfig-cs]
2. <span data-ttu-id="059a6-199">В приведенном ниже коде в методе `RegisterRoutes` замените `controller = "Home"` на `controller = "Teams"`, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="059a6-199">Replace `controller = "Home"` in the following code in the `RegisterRoutes` method with `controller = "Teams"` as shown in the following example.</span></span>

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-the-views"></a><span data-ttu-id="059a6-200">Настройка представлений</span><span class="sxs-lookup"><span data-stu-id="059a6-200">Configure the views</span></span>
1. <span data-ttu-id="059a6-201">В **обозревателе решений** разверните папку **Представления**, а затем — папку **Общее** и дважды щелкните файл **_Layout.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="059a6-201">In **Solution Explorer**, expand the **Views** folder and then the **Shared** folder, and double-click **_Layout.cshtml**.</span></span> 
   
    ![_Layout.cshtml][cache-layout-cshtml]
2. <span data-ttu-id="059a6-203">Измените содержимое элемента `title` и замените `My ASP.NET Application` на `Contoso Team Stats`, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="059a6-203">Change the contents of the `title` element and replace `My ASP.NET Application` with `Contoso Team Stats` as shown in the following example.</span></span>

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. <span data-ttu-id="059a6-204">В разделе `body` обновите первый оператор `Html.ActionLink`, а также замените `Application name` на `Contoso Team Stats` и `Home` на `Teams`.</span><span class="sxs-lookup"><span data-stu-id="059a6-204">In the `body` section, update the first `Html.ActionLink` statement and replace `Application name` with `Contoso Team Stats` and replace `Home` with `Teams`.</span></span>
   
   * <span data-ttu-id="059a6-205">До: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="059a6-205">Before: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
   * <span data-ttu-id="059a6-206">После: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="059a6-206">After: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
     
     ![Изменения в коде][cache-layout-cshtml-code]
2. <span data-ttu-id="059a6-208">Нажмите клавиши **CTRL+F5** , чтобы создать и запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="059a6-208">Press **Ctrl+F5** to build and run the application.</span></span> <span data-ttu-id="059a6-209">В этой версии приложения результаты считываются непосредственно из базы данных.</span><span class="sxs-lookup"><span data-stu-id="059a6-209">This version of the application reads the results directly from the database.</span></span> <span data-ttu-id="059a6-210">Примечание. Действия **Создать**, **Изменить**, **Сведения** и **Удалить** автоматически добавлены в приложение с помощью шаблона **Контроллер MVC 5 с представлениями, использующий Entity Framework**.</span><span class="sxs-lookup"><span data-stu-id="059a6-210">Note the **Create New**, **Edit**, **Details**, and **Delete** actions that were automatically added to the application by the **MVC 5 Controller with views, using Entity Framework** scaffold.</span></span> <span data-ttu-id="059a6-211">В следующем разделе руководства будет добавлен кэш Redis для оптимизации доступа к данным и добавления дополнительных функций в приложение.</span><span class="sxs-lookup"><span data-stu-id="059a6-211">In the next section of the tutorial you'll add Redis Cache to optimize the data access and provide additional features to the application.</span></span>

![Начальное приложение][cache-starter-application]

## <a name="configure-the-application-to-use-redis-cache"></a><span data-ttu-id="059a6-213">Настройка приложения для использования кэша Redis</span><span class="sxs-lookup"><span data-stu-id="059a6-213">Configure the application to use Redis Cache</span></span>
<span data-ttu-id="059a6-214">В этом разделе руководства будет настроен пример приложения для хранения и извлечения статистики команды Contoso из экземпляра кэша Redis для Azure с помощью клиента кэша [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) .</span><span class="sxs-lookup"><span data-stu-id="059a6-214">In this section of the tutorial, you'll configure the sample application to store and retrieve Contoso team statistics from an Azure Redis Cache instance by using the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cache client.</span></span>

* [<span data-ttu-id="059a6-215">Настройка приложения для использования StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="059a6-215">Configure the application to use StackExchange.Redis</span></span>](#configure-the-application-to-use-stackexchangeredis)
* [<span data-ttu-id="059a6-216">Обновление класса TeamsController для возвращения результатов из кэша или базы данных</span><span class="sxs-lookup"><span data-stu-id="059a6-216">Update the TeamsController class to return results from the cache or the database</span></span>](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [<span data-ttu-id="059a6-217">Обновление методов создания, изменения и удаления для работы с кэшем</span><span class="sxs-lookup"><span data-stu-id="059a6-217">Update the Create, Edit, and Delete methods to work with the cache</span></span>](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [<span data-ttu-id="059a6-218">Обновление представления индекса команд для работы с кэшем</span><span class="sxs-lookup"><span data-stu-id="059a6-218">Update the Teams Index view to work with the cache</span></span>](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-the-application-to-use-stackexchangeredis"></a><span data-ttu-id="059a6-219">Настройка приложения для использования StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="059a6-219">Configure the application to use StackExchange.Redis</span></span>
1. <span data-ttu-id="059a6-220">Чтобы настроить клиентское приложение в Visual Studio, используя пакет StackExchange.Redis из NuGet, выберите в меню **Сервис** последовательно элементы **Диспетчер пакетов NuGet** и **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="059a6-220">To configure a client application in Visual Studio using the StackExchange.Redis NuGet package, click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>
2. <span data-ttu-id="059a6-221">Выполните следующую команду в окне `Package Manager Console`:</span><span class="sxs-lookup"><span data-stu-id="059a6-221">Run the following command from the `Package Manager Console` window.</span></span>
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    <span data-ttu-id="059a6-222">Пакет NuGet загружает и добавляет необходимые ссылки на сборки в клиентском приложении для доступа к кэшу Azure Redis из клиента кэша StackExchange.Redis.</span><span class="sxs-lookup"><span data-stu-id="059a6-222">The NuGet package downloads and adds the required assembly references for your client application to access Azure Redis Cache with the StackExchange.Redis cache client.</span></span> <span data-ttu-id="059a6-223">Если вы предпочитаете использовать версию клиентской библиотеки `StackExchange.Redis` со строгими именами, установите пакет `StackExchange.Redis.StrongName`.</span><span class="sxs-lookup"><span data-stu-id="059a6-223">If you prefer to use a strong-named version of the `StackExchange.Redis` client library, install the `StackExchange.Redis.StrongName` package.</span></span>
3. <span data-ttu-id="059a6-224">В **обозревателе решений** разверните папку **Контроллеры** и дважды щелкните файл **TeamsController.cs**, чтобы открыть его.</span><span class="sxs-lookup"><span data-stu-id="059a6-224">In **Solution Explorer**, expand the **Controllers** folder and double-click **TeamsController.cs** to open it.</span></span>
   
    ![Контроллер команд][cache-teamscontroller]
4. <span data-ttu-id="059a6-226">Добавьте в файл **TeamsController.cs** следующие два оператора `using`:</span><span class="sxs-lookup"><span data-stu-id="059a6-226">Add the following two `using` statements to **TeamsController.cs**.</span></span>

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. <span data-ttu-id="059a6-227">Добавьте в класс `TeamsController` следующие два свойства:</span><span class="sxs-lookup"><span data-stu-id="059a6-227">Add the following two properties to the `TeamsController` class.</span></span>

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

6. <span data-ttu-id="059a6-228">Создайте на компьютере файл с именем `WebAppPlusCacheAppSecrets.config` и поместите его в расположение, которое не будет записано после изменения с исходным кодом примера приложения, если его нужно будет записать где-нибудь после изменения.</span><span class="sxs-lookup"><span data-stu-id="059a6-228">Create a file on your computer named `WebAppPlusCacheAppSecrets.config` and place it in a location that won't be checked in with the source code of your sample application, should you decide to check it in somewhere.</span></span> <span data-ttu-id="059a6-229">В этом примере файл `AppSettingsSecrets.config` находится в папке `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span><span class="sxs-lookup"><span data-stu-id="059a6-229">In this example the `AppSettingsSecrets.config` file is located at `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span></span>
   
    <span data-ttu-id="059a6-230">Измените файл `WebAppPlusCacheAppSecrets.config` и добавьте содержимое, приведенное ниже.</span><span class="sxs-lookup"><span data-stu-id="059a6-230">Edit the `WebAppPlusCacheAppSecrets.config` file and add the following contents.</span></span> <span data-ttu-id="059a6-231">При локальном запуске приложения эти сведения используются для подключения к экземпляру кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="059a6-231">If you run the application locally this information is used to connect to your Azure Redis Cache instance.</span></span> <span data-ttu-id="059a6-232">Далее в этом руководстве будет подготовлен к работе экземпляр кэша Redis для Azure и обновлены имя и пароль для него.</span><span class="sxs-lookup"><span data-stu-id="059a6-232">Later in the tutorial you'll provision an Azure Redis Cache instance and update the cache name and password.</span></span> <span data-ttu-id="059a6-233">Если пример приложения не планируется запускать локально, создавать этот файл необязательно. В таком случае можно пропустить последующие шаги, в которых он указан, так как при развертывании в Azure приложение получает сведения о подключении кэша из параметра приложения для веб-приложения, а не из этого файла.</span><span class="sxs-lookup"><span data-stu-id="059a6-233">If you don't plan to run the sample application locally you can skip the creation of this file and the subsequent steps that reference the file, because when you deploy to Azure the application retrieves the cache connection information from the app setting for the Web App and not from this file.</span></span> <span data-ttu-id="059a6-234">Так как файл `WebAppPlusCacheAppSecrets.config` не развертывается в Azure с приложением, он не нужен, если приложение не будет запускаться локально.</span><span class="sxs-lookup"><span data-stu-id="059a6-234">Since the `WebAppPlusCacheAppSecrets.config` is not deployed to Azure with your application, you don't need it unless you are going to run the application locally.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="059a6-235">В **обозревателе решений** дважды щелкните файл **web.config**, чтобы открыть его.</span><span class="sxs-lookup"><span data-stu-id="059a6-235">In **Solution Explorer**, double-click **web.config** to open it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="059a6-237">Добавьте атрибут `file` в элемент `appSettings`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="059a6-237">Add the following `file` attribute to the `appSettings` element.</span></span> <span data-ttu-id="059a6-238">Если использовалось другое имя файла или расположение, замените эти значения на представленные в примере.</span><span class="sxs-lookup"><span data-stu-id="059a6-238">If you used a different file name or location, substitute those values for the ones shown in the example.</span></span>
   
   * <span data-ttu-id="059a6-239">До: `<appSettings>`</span><span class="sxs-lookup"><span data-stu-id="059a6-239">Before: `<appSettings>`</span></span>
   * <span data-ttu-id="059a6-240">После: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span><span class="sxs-lookup"><span data-stu-id="059a6-240">After: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span></span>
     
   <span data-ttu-id="059a6-241">Среда выполнения ASP.NET объединяет содержимое внешнего файла с разметкой в элементе `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="059a6-241">The ASP.NET runtime merges the contents of the external file with the markup in the `<appSettings>` element.</span></span> <span data-ttu-id="059a6-242">Если указанный файл не удается найти, среда выполнения игнорирует атрибут файла.</span><span class="sxs-lookup"><span data-stu-id="059a6-242">The runtime ignores the file attribute if the specified file cannot be found.</span></span> <span data-ttu-id="059a6-243">Секреты (строка подключения к вашему кэшу) не включаются в исходный код приложения.</span><span class="sxs-lookup"><span data-stu-id="059a6-243">Your secrets (the connection string to your cache) are not included as part of the source code for the application.</span></span> <span data-ttu-id="059a6-244">При развертывании веб-приложения в Azure файл `WebAppPlusCacheAppSecrests.config` не будет развернут (как и нужно).</span><span class="sxs-lookup"><span data-stu-id="059a6-244">When you deploy your web app to Azure, the `WebAppPlusCacheAppSecrests.config` file won't be deployed (that's what you want).</span></span> <span data-ttu-id="059a6-245">Существует несколько способов указать эти секреты в Azure. В этом руководстве они настраиваются автоматически при [подготовке ресурсов Azure к работе](#provision-the-azure-resources) на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="059a6-245">There are several ways to specify these secrets in Azure, and in this tutorial they are configured automatically for you when you [provision the Azure resources](#provision-the-azure-resources) in a subsequent tutorial step.</span></span> <span data-ttu-id="059a6-246">Дополнительные сведения о работе с секретами в Azure см. в статье [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure) (Рекомендации по развертыванию паролей и других конфиденциальных данных в ASP.NET и в службе приложений Azure).</span><span class="sxs-lookup"><span data-stu-id="059a6-246">For more information about working with secrets in Azure, see [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span></span>

### <a name="update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database"></a><span data-ttu-id="059a6-247">Обновление класса TeamsController для возвращения результатов из кэша или базы данных</span><span class="sxs-lookup"><span data-stu-id="059a6-247">Update the TeamsController class to return results from the cache or the database</span></span>
<span data-ttu-id="059a6-248">В этом примере статистику команды можно получить из базы данных или из кэша.</span><span class="sxs-lookup"><span data-stu-id="059a6-248">In this sample, team statistics can be retrieved from the database or from the cache.</span></span> <span data-ttu-id="059a6-249">Статистика команды сохраняется в кэше в качестве сериализованного элемента `List<Team>`, а также в качестве отсортированного набора с помощью типов данных Redis.</span><span class="sxs-lookup"><span data-stu-id="059a6-249">Team statistics are stored in the cache as a serialized `List<Team>`, and also as a sorted set using Redis data types.</span></span> <span data-ttu-id="059a6-250">Из отсортированного набора можно извлечь все или некоторые элементы или же запросить определенные элементы.</span><span class="sxs-lookup"><span data-stu-id="059a6-250">When retrieving items from a sorted set, you can retrieve some, all, or query for certain items.</span></span> <span data-ttu-id="059a6-251">В этом примере из отсортированного набора будут запрашиваться 5 лучших команд, упорядоченных по количеству положительных результатов.</span><span class="sxs-lookup"><span data-stu-id="059a6-251">In this sample you'll query the sorted set for the top 5 teams ranked by number of wins.</span></span>

> [!NOTE]
> <span data-ttu-id="059a6-252">Чтобы использовать кэш Redis для Azure, не обязательно хранить статистику команды в нескольких форматах в кэше.</span><span class="sxs-lookup"><span data-stu-id="059a6-252">It is not required to store the team statistics in multiple formats in the cache in order to use Azure Redis Cache.</span></span> <span data-ttu-id="059a6-253">В этом руководстве несколько форматов используется для демонстрации различных способов кэширования данных и различных типов данных, используемых для этой операции.</span><span class="sxs-lookup"><span data-stu-id="059a6-253">This tutorial uses multiple formats to demonstrate some of the different ways and different data types you can use to cache data.</span></span>
> 
> 

1. <span data-ttu-id="059a6-254">В начале файла `TeamsController.cs` добавьте следующие операторы `using` к остальным операторам `using`:</span><span class="sxs-lookup"><span data-stu-id="059a6-254">Add the following `using` statements to the `TeamsController.cs` file at the top with the other `using` statements.</span></span>

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. <span data-ttu-id="059a6-255">Замените текущую реализацию метода `public ActionResult Index()` следующей реализацией:</span><span class="sxs-lookup"><span data-stu-id="059a6-255">Replace the current `public ActionResult Index()` method implementation with the following implementation.</span></span>

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

            case "clearCache": // Clear the results from the cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild the database with sample data.
                RebuildDB();
                break;
        }

        // Measure the time it takes to retrieve the results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve the top 5 teams from the sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from the cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from the database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add the elapsed time of the operation to the ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. <span data-ttu-id="059a6-256">Добавьте приведенные ниже три метода из оператора switch, добавленного в предыдущем фрагменте кода, в класс `TeamsController` для реализации типов действий `playGames`, `clearCache` и `rebuildDB`.</span><span class="sxs-lookup"><span data-stu-id="059a6-256">Add the following three methods to the `TeamsController` class to implement the `playGames`, `clearCache`, and `rebuildDB` action types from the switch statement added in the previous code snippet.</span></span>
   
    <span data-ttu-id="059a6-257">Метод `PlayGames` обновляет статистику команды, имитируя сезон игр, сохраняет результаты в базу данных и удаляет устаревшие данные из кэша.</span><span class="sxs-lookup"><span data-stu-id="059a6-257">The `PlayGames` method updates the team statistics by simulating a season of games, saves the results to the database, and clears the now outdated data from the cache.</span></span>

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

    <span data-ttu-id="059a6-258">Метод `RebuildDB` повторно инициализирует базу данных с набором команд по умолчанию, создает для них статистику и удаляет устаревшие данные из кэша.</span><span class="sxs-lookup"><span data-stu-id="059a6-258">The `RebuildDB` method reinitializes the database with the default set of teams, generates statistics for them, and clears the now outdated data from the cache.</span></span>

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize the database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="059a6-259">Метод `ClearCachedTeams` удаляет всю кэшированную статистику команды из кэша.</span><span class="sxs-lookup"><span data-stu-id="059a6-259">The `ClearCachedTeams` method removes any cached team statistics from the cache.</span></span>

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. <span data-ttu-id="059a6-260">Добавьте приведенные ниже четыре метода в класс `TeamsController` , чтобы реализовать различные способы получения статистики команды из кэша и базы данных.</span><span class="sxs-lookup"><span data-stu-id="059a6-260">Add the following four methods to the `TeamsController` class to implement the various ways of retrieving the team statistics from the cache and the database.</span></span> <span data-ttu-id="059a6-261">Каждый из этих методов возвращает элемент `List<Team>` , который затем отображается в представлении.</span><span class="sxs-lookup"><span data-stu-id="059a6-261">Each of these methods returns a `List<Team>` which is then displayed by the view.</span></span>
   
    <span data-ttu-id="059a6-262">Метод `GetFromDB` считывает статистику команды из базы данных.</span><span class="sxs-lookup"><span data-stu-id="059a6-262">The `GetFromDB` method reads the team statistics from the database.</span></span>
   
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

    <span data-ttu-id="059a6-263">Метод `GetFromList` считывает статистику команды из кэша в качестве сериализованного элемента `List<Team>`.</span><span class="sxs-lookup"><span data-stu-id="059a6-263">The `GetFromList` method reads the team statistics from cache as a serialized `List<Team>`.</span></span> <span data-ttu-id="059a6-264">В случае промаха кэша статистика команды считывается из базы данных и сохраняется в кэше для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="059a6-264">If there is a cache miss, the team statistics are read from the database and then stored in the cache for next time.</span></span> <span data-ttu-id="059a6-265">В этом примере мы сериализуем объекты .NET из кэша и в кэш, используя сериализацию JSON.NET.</span><span class="sxs-lookup"><span data-stu-id="059a6-265">In this sample we're using JSON.NET serialization to serialize the .NET objects to and from the cache.</span></span> <span data-ttu-id="059a6-266">Дополнительные сведения см. в разделе [Работа с объектами .NET в кэше](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span><span class="sxs-lookup"><span data-stu-id="059a6-266">For more information, see [How to work with .NET objects in Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span></span>

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

            ViewBag.msg += "Storing results to cache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    <span data-ttu-id="059a6-267">Метод `GetFromSortedSet` считывает статистику команды из кэшированного отсортированного набора.</span><span class="sxs-lookup"><span data-stu-id="059a6-267">The `GetFromSortedSet` method reads the team statistics from a cached sorted set.</span></span> <span data-ttu-id="059a6-268">В случае промаха кэша статистика команды считывается из базы данных и сохраняется в кэше в качестве отсортированного набора.</span><span class="sxs-lookup"><span data-stu-id="059a6-268">If there is a cache miss, the team statistics are read from the database and stored in the cache as a sorted set.</span></span>

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If the key teamsSortedSet is not present, this method returns a 0 length collection.
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

            ViewBag.msg += "Storing results to cache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding to sorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    <span data-ttu-id="059a6-269">Метод `GetFromSortedSetTop5` считывает 5 лучших команд из кэшированного отсортированного набора.</span><span class="sxs-lookup"><span data-stu-id="059a6-269">The `GetFromSortedSetTop5` method reads the top 5 teams from the cached sorted set.</span></span> <span data-ttu-id="059a6-270">Сначала проверяется наличие ключа `teamsSortedSet` в кэше.</span><span class="sxs-lookup"><span data-stu-id="059a6-270">It starts by checking the cache for the existence of the `teamsSortedSet` key.</span></span> <span data-ttu-id="059a6-271">Если этот ключ не указан, вызывается метод `GetFromSortedSet` для считывания статистики команды и ее сохранения в кэше.</span><span class="sxs-lookup"><span data-stu-id="059a6-271">If this key is not present, the `GetFromSortedSet` method is called to read the team statistics and store them in the cache.</span></span> <span data-ttu-id="059a6-272">Затем в кэшированном отсортированном наборе запрашивается 5 первых команд, которые возвращаются.</span><span class="sxs-lookup"><span data-stu-id="059a6-272">Next, the cached sorted set is queried for the top 5 teams which are returned.</span></span>

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If the key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load the entire sorted set into the cache.
            GetFromSortedSet();

            // Retrieve the top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get the top 5 teams from the sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-the-create-edit-and-delete-methods-to-work-with-the-cache"></a><span data-ttu-id="059a6-273">Обновление методов создания, изменения и удаления для работы с кэшем</span><span class="sxs-lookup"><span data-stu-id="059a6-273">Update the Create, Edit, and Delete methods to work with the cache</span></span>
<span data-ttu-id="059a6-274">Код для формирования шаблонов, созданный в этом примере, содержит методы для добавления, изменения и удаления команд.</span><span class="sxs-lookup"><span data-stu-id="059a6-274">The scaffolding code that was generated as part of this sample includes methods to add, edit, and delete teams.</span></span> <span data-ttu-id="059a6-275">При каждом добавлении, изменении или удалении команды данные в кэше устаревают.</span><span class="sxs-lookup"><span data-stu-id="059a6-275">Anytime a team is added, edited, or removed, the data in the cache becomes outdated.</span></span> <span data-ttu-id="059a6-276">В этом разделе приведенные метода будут изменены, чтобы очистить кэшированные команды. Это поможет синхронизировать кэш с базой данных.</span><span class="sxs-lookup"><span data-stu-id="059a6-276">In this section you'll modify these three methods to clear the cached teams so that the cache won't be out of sync with the database.</span></span>

1. <span data-ttu-id="059a6-277">Перейдите к методу `Create(Team team)` в классе `TeamsController`.</span><span class="sxs-lookup"><span data-stu-id="059a6-277">Browse to the `Create(Team team)` method in the `TeamsController` class.</span></span> <span data-ttu-id="059a6-278">Добавьте вызов в метод `ClearCachedTeams` , как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="059a6-278">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Create
    // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, the cache is out of date.
            // Clear the cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. <span data-ttu-id="059a6-279">Перейдите к методу `Edit(Team team)` в классе `TeamsController`.</span><span class="sxs-lookup"><span data-stu-id="059a6-279">Browse to the `Edit(Team team)` method in the `TeamsController` class.</span></span> <span data-ttu-id="059a6-280">Добавьте вызов в метод `ClearCachedTeams` , как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="059a6-280">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Edit/5
    // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, the cache is out of date.
            // Clear the cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. <span data-ttu-id="059a6-281">Перейдите к методу `DeleteConfirmed(int id)` в классе `TeamsController`.</span><span class="sxs-lookup"><span data-stu-id="059a6-281">Browse to the `DeleteConfirmed(int id)` method in the `TeamsController` class.</span></span> <span data-ttu-id="059a6-282">Добавьте вызов в метод `ClearCachedTeams` , как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="059a6-282">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, the cache is out of date.
        // Clear the cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-the-teams-index-view-to-work-with-the-cache"></a><span data-ttu-id="059a6-283">Обновление представления индекса команд для работы с кэшем</span><span class="sxs-lookup"><span data-stu-id="059a6-283">Update the Teams Index view to work with the cache</span></span>
1. <span data-ttu-id="059a6-284">В **обозревателе решений** разверните папку **Представления**, а затем — папку **Команды** и дважды щелкните файл **Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="059a6-284">In **Solution Explorer**, expand the **Views** folder, then the **Teams** folder, and double-click **Index.cshtml**.</span></span>
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. <span data-ttu-id="059a6-286">Найдите следующий элемент абзаца в начале файла.</span><span class="sxs-lookup"><span data-stu-id="059a6-286">Near the top of the file, look for the following paragraph element.</span></span>
   
    ![Таблица действий][cache-teams-index-table]
   
    <span data-ttu-id="059a6-288">Это ссылка, позволяющая создать команду.</span><span class="sxs-lookup"><span data-stu-id="059a6-288">This is the link to create a new team.</span></span> <span data-ttu-id="059a6-289">Замените элемент абзаца таблицей, приведенной ниже.</span><span class="sxs-lookup"><span data-stu-id="059a6-289">Replace the paragraph element with the following table.</span></span> <span data-ttu-id="059a6-290">Эта таблица содержит ссылки на действия для создания новой команды, воспроизведения нового сезона игр, очистки кэша, получения команды из кэша в нескольких форматах, получения команд из базы данных и повторной сборки базы данных с использованием нового примера данных.</span><span class="sxs-lookup"><span data-stu-id="059a6-290">This table has action links for creating a new team, playing a new season of games, clearing the cache, retrieving the teams from the cache in several formats, retrieving the teams from the database, and rebuilding the database with fresh sample data.</span></span>

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


1. <span data-ttu-id="059a6-291">Перейдите в конец файла **Index.cshtml** и добавьте элемент `tr` в последнюю строку последней таблицы.</span><span class="sxs-lookup"><span data-stu-id="059a6-291">Scroll to the bottom of the **Index.cshtml** file and add the following `tr` element so that it is the last row in the last table in the file.</span></span>
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    <span data-ttu-id="059a6-292">В этой строке отображаются значение `ViewBag.Msg`, которое содержит отчет о состоянии о текущей операции.</span><span class="sxs-lookup"><span data-stu-id="059a6-292">This row displays the value of `ViewBag.Msg` which contains a status report about the current operation.</span></span> <span data-ttu-id="059a6-293">Значение `ViewBag.Msg` устанавливается при выборе ссылки на любое действия предыдущего шага.</span><span class="sxs-lookup"><span data-stu-id="059a6-293">The `ViewBag.Msg` is set when you click any of the action links from the previous step.</span></span>   
   
    ![Сообщение о состоянии][cache-status-message]
2. <span data-ttu-id="059a6-295">Нажмите клавишу **F6** , чтобы скомпилировать проект.</span><span class="sxs-lookup"><span data-stu-id="059a6-295">Press **F6** to build the project.</span></span>

## <a name="provision-the-azure-resources"></a><span data-ttu-id="059a6-296">Подготовка ресурсов Azure к работе</span><span class="sxs-lookup"><span data-stu-id="059a6-296">Provision the Azure resources</span></span>
<span data-ttu-id="059a6-297">Чтобы разместить приложение в Azure, сначала нужно подготовить к работе службы Azure, требуемые для приложения.</span><span class="sxs-lookup"><span data-stu-id="059a6-297">To host your application in Azure, you must first provision the Azure services that your application requires.</span></span> <span data-ttu-id="059a6-298">В примере приложения в этом руководстве используются следующие службы Azure:</span><span class="sxs-lookup"><span data-stu-id="059a6-298">The sample application in this tutorial uses the following Azure services.</span></span>

* <span data-ttu-id="059a6-299">кэш Azure Redis</span><span class="sxs-lookup"><span data-stu-id="059a6-299">Azure Redis Cache</span></span>
* <span data-ttu-id="059a6-300">веб-приложение службы приложений;</span><span class="sxs-lookup"><span data-stu-id="059a6-300">App Service Web App</span></span>
* <span data-ttu-id="059a6-301">База данных SQL</span><span class="sxs-lookup"><span data-stu-id="059a6-301">SQL Database</span></span>

<span data-ttu-id="059a6-302">Чтобы развернуть эти службы в выбранной новой или имеющейся группе ресурсов, нажмите кнопку **Deploy to Azure** (Развернуть в Azure).</span><span class="sxs-lookup"><span data-stu-id="059a6-302">To deploy these services to a new or existing resource group of your choice, click the following **Deploy to Azure** button.</span></span>

<span data-ttu-id="059a6-303">[![Развернуть в Azure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="059a6-303">[![Deploy to Azure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span></span>

<span data-ttu-id="059a6-304">Кнопка **Deploy to Azure** (Развернуть в Azure) использует шаблон [быстрого запуска Azure](https://github.com/Azure/azure-quickstart-templates) [Create a Web App plus Redis Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) (Создание веб-приложения, кэша Redis и базы данных SQL), чтобы подготовить эти службы к работе, а также задать строку подключения для базы данных SQL и параметр приложения для строки подключения кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="059a6-304">This **Deploy to Azure** button uses the [Create a Web App plus Redis Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) template to provision these services and set the connection string for the SQL Database and the application setting for the Azure Redis Cache connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="059a6-305">Если у вас нет учетной записи Azure, можно [создать бесплатную учетную запись Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="059a6-305">If you don't have an Azure account, you can [create a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in just a couple of minutes.</span></span>
> 
> 

<span data-ttu-id="059a6-306">Нажав кнопку **Deploy to Azure** (Развернуть в Azure), вы перейдете на портал Azure, где запустится создание ресурсов, описанных в шаблоне.</span><span class="sxs-lookup"><span data-stu-id="059a6-306">Clicking the **Deploy to Azure** button takes you to the Azure portal and initiates the process of creating the resources described by the template.</span></span>

![Развернуть в Azure][cache-deploy-to-azure-step-1]

1. <span data-ttu-id="059a6-308">В разделе **основных сведений** выберите подписку Azure, которую следует использовать, и имеющуюся группу ресурсов или создайте группу ресурсов и укажите ее расположение.</span><span class="sxs-lookup"><span data-stu-id="059a6-308">In the **Basics** section, select the Azure subscription to use, and select an existing resource group or create a new one, and specify the resource group location.</span></span>
2. <span data-ttu-id="059a6-309">В разделе **Параметры** укажите **имя учетной записи администратора** (не используйте **admin**), **пароль для входа администратора** и **имя базы данных**.</span><span class="sxs-lookup"><span data-stu-id="059a6-309">In the **Settings** section, specify an **Administrator Login** (don't use **admin**), **Administrator Login Password**, and **Database Name**.</span></span> <span data-ttu-id="059a6-310">Другие параметры настраиваются для плана размещения службы приложений (ценовая категория "Бесплатный") и более экономичных компонентов для базы данных SQL и кэша Redis для Azure, которые не предусмотрены на уровне "Бесплатный".</span><span class="sxs-lookup"><span data-stu-id="059a6-310">The other parameters are configured for a free App Service hosting plan, and lower-cost options for the SQL Database and Azure Redis Cache, which don't come with a free tier.</span></span>

    ![Развернуть в Azure][cache-deploy-to-azure-step-2]

3. <span data-ttu-id="059a6-312">Настроив нужные параметры, прокрутите страницу до конца, ознакомьтесь с условиями и установите флажок **Я принимаю указанные выше условия**.</span><span class="sxs-lookup"><span data-stu-id="059a6-312">After configuring the desired settings, scroll to the end of the page, read the terms and conditions, and check the **I agree to the terms and conditions stated above** checkbox.</span></span>
4. <span data-ttu-id="059a6-313">Чтобы начать подготовку ресурсов, нажмите кнопку **Приобрести**.</span><span class="sxs-lookup"><span data-stu-id="059a6-313">To begin provisioning the resources, click **Purchase**.</span></span>

<span data-ttu-id="059a6-314">Чтобы просмотреть ход выполнения развертывания, щелкните значок уведомления и сообщение **Развертывание начато**.</span><span class="sxs-lookup"><span data-stu-id="059a6-314">To view the progress of your deployment, click the notification icon and click **Deployment started**.</span></span>

![Развертывание начато][cache-deployment-started]

<span data-ttu-id="059a6-316">Состояние развертывания можно просмотреть в колонке **Microsoft.Template** .</span><span class="sxs-lookup"><span data-stu-id="059a6-316">You can view the status of your deployment on the **Microsoft.Template** blade.</span></span>

![Deploy to Azure][cache-deploy-to-azure-step-3]

<span data-ttu-id="059a6-318">После завершения подготовки к работе можно опубликовать приложение Azure из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="059a6-318">When provisioning is complete, you can publish your application to Azure from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="059a6-319">Все ошибки, возникающие при подготовке, отображаются в колонке **Microsoft.Template**.</span><span class="sxs-lookup"><span data-stu-id="059a6-319">Any errors that may occur during the provisioning process are displayed on the **Microsoft.Template** blade.</span></span> <span data-ttu-id="059a6-320">Среди распространенных ошибок — слишком много ошибок, связанных с SQL Server или планами размещения служб приложений уровня "Бесплатный" на подписку.</span><span class="sxs-lookup"><span data-stu-id="059a6-320">Common errors are too many SQL Servers or too many Free App Service hosting plans per subscription.</span></span> <span data-ttu-id="059a6-321">Устраните ошибки и начните процедуру заново, нажав кнопку **Повторить развертывание** в колонке **Microsoft.Template** или кнопку **Deploy to Azure** (Развернуть в Azure), как описано в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="059a6-321">Resolve any errors and restart the process by clicking **Redeploy** on the **Microsoft.Template** blade or the **Deploy to Azure** button in this tutorial.</span></span>
> 
> 

## <a name="publish-the-application-to-azure"></a><span data-ttu-id="059a6-322">Публикация приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="059a6-322">Publish the application to Azure</span></span>
<span data-ttu-id="059a6-323">На этом шаге руководства приложение будет опубликовано в Azure и запущено в облаке.</span><span class="sxs-lookup"><span data-stu-id="059a6-323">In this step of the tutorial, you'll publish the application to Azure and run it in the cloud.</span></span>

1. <span data-ttu-id="059a6-324">В Visual Studio щелкните правой кнопкой мыши проект **ContosoTeamStats** и выберите пункт **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="059a6-324">Right-click the **ContosoTeamStats** project in Visual Studio and choose **Publish**.</span></span>
   
    ![Опубликовать][cache-publish-app]
2. <span data-ttu-id="059a6-326">Щелкните элемент **Служба приложений Microsoft Azure**, выберите параметр **Выбрать существующую** и нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="059a6-326">Click **Microsoft Azure App Service**, choose **Select Existing**, and click **Publish**.</span></span>
   
    ![Опубликовать][cache-publish-to-app-service]
3. <span data-ttu-id="059a6-328">Выберите подписку, использованную при создании ресурсов Azure, разверните группу ресурсов, содержащую ресурсы и выберите нужное веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="059a6-328">Select the subscription used when creating the Azure resources, expand the resource group containing the resources, and select the desired Web App.</span></span> <span data-ttu-id="059a6-329">Если использовалась кнопка **Deploy to Azure** (Развернуть в Azure), имя веб-приложения будет начинаться с **webSite** и содержать некоторые дополнительные символы.</span><span class="sxs-lookup"><span data-stu-id="059a6-329">If you used the **Deploy to Azure** button your Web App name starts with **webSite** followed by some additional characters.</span></span>
   
    ![Выбор веб-приложения][cache-select-web-app]
4. <span data-ttu-id="059a6-331">Нажмите кнопку **ОК**, чтобы начать процесс публикации.</span><span class="sxs-lookup"><span data-stu-id="059a6-331">Click **OK** to begin the publishing process.</span></span> <span data-ttu-id="059a6-332">Через некоторое время публикация завершится, после чего будет запущен браузер с выполняющимся примером приложения.</span><span class="sxs-lookup"><span data-stu-id="059a6-332">After a few moments the publishing process completes and a browser is launched with the running sample application.</span></span> <span data-ttu-id="059a6-333">Если при проверке или публикации возникает ошибка DNS, а подготовка ресурсов Azure к работе для приложения недавно завершилась, подождите немного и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="059a6-333">If you get a DNS error when validating or publishing, and the provisioning process for the Azure resources for the application has just recently completed, wait a moment and try again.</span></span>
   
    ![Кэш добавлен][cache-added-to-application]

<span data-ttu-id="059a6-335">В следующей таблице описана каждая ссылка на действие из примера приложения.</span><span class="sxs-lookup"><span data-stu-id="059a6-335">The following table describes each action link from the sample application.</span></span>

| <span data-ttu-id="059a6-336">Действие</span><span class="sxs-lookup"><span data-stu-id="059a6-336">Action</span></span> | <span data-ttu-id="059a6-337">Описание</span><span class="sxs-lookup"><span data-stu-id="059a6-337">Description</span></span> |
| --- | --- |
| <span data-ttu-id="059a6-338">Создать</span><span class="sxs-lookup"><span data-stu-id="059a6-338">Create New</span></span> |<span data-ttu-id="059a6-339">Создание команды.</span><span class="sxs-lookup"><span data-stu-id="059a6-339">Create a new Team.</span></span> |
| <span data-ttu-id="059a6-340">Воспроизвести сезон</span><span class="sxs-lookup"><span data-stu-id="059a6-340">Play Season</span></span> |<span data-ttu-id="059a6-341">Воспроизведение сезона игр, обновление статистики команды и удаление всех устаревших данных из кэша команды.</span><span class="sxs-lookup"><span data-stu-id="059a6-341">Play a season of games, update the team stats, and clear any outdated team data from the cache.</span></span> |
| <span data-ttu-id="059a6-342">Очистить кэш</span><span class="sxs-lookup"><span data-stu-id="059a6-342">Clear Cache</span></span> |<span data-ttu-id="059a6-343">Удаление статистики команды из кэша.</span><span class="sxs-lookup"><span data-stu-id="059a6-343">Clear the team stats from the cache.</span></span> |
| <span data-ttu-id="059a6-344">List from Cache (Перечислить из кэша)</span><span class="sxs-lookup"><span data-stu-id="059a6-344">List from Cache</span></span> |<span data-ttu-id="059a6-345">Получение статистики команды из кэша.</span><span class="sxs-lookup"><span data-stu-id="059a6-345">Retrieve the team stats from the cache.</span></span> <span data-ttu-id="059a6-346">В случае промаха кэша статистика загружается из базы данных и сохраняется в кэше для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="059a6-346">If there is a cache miss, load the stats from the database and save to the cache for next time.</span></span> |
| <span data-ttu-id="059a6-347">Sorted Set from Cache (Отсортированный набор из кэша)</span><span class="sxs-lookup"><span data-stu-id="059a6-347">Sorted Set from Cache</span></span> |<span data-ttu-id="059a6-348">Получение статистики команды из кэша с использованием отсортированного набора.</span><span class="sxs-lookup"><span data-stu-id="059a6-348">Retrieve the team stats from the cache using a sorted set.</span></span> <span data-ttu-id="059a6-349">В случае промаха кэша статистика загружается из базы данных и сохраняется в кэше с использованием отсортированного набора.</span><span class="sxs-lookup"><span data-stu-id="059a6-349">If there is a cache miss, load the stats from the database and save to the cache using a sorted set.</span></span> |
| <span data-ttu-id="059a6-350">Top 5 Teams from Cache (5 лучших команд из кэша)</span><span class="sxs-lookup"><span data-stu-id="059a6-350">Top 5 Teams from Cache</span></span> |<span data-ttu-id="059a6-351">Получение 5 лучших команд из кэша с использованием отсортированного набора.</span><span class="sxs-lookup"><span data-stu-id="059a6-351">Retrieve the top 5 teams from the cache using a sorted set.</span></span> <span data-ttu-id="059a6-352">В случае промаха кэша статистика загружается из базы данных и сохраняется в кэше с использованием отсортированного набора.</span><span class="sxs-lookup"><span data-stu-id="059a6-352">If there is a cache miss, load the stats from the database and save to the cache using a sorted set.</span></span> |
| <span data-ttu-id="059a6-353">Load from DB (Загрузить из базы данных)</span><span class="sxs-lookup"><span data-stu-id="059a6-353">Load from DB</span></span> |<span data-ttu-id="059a6-354">Получение статистики команды из базы данных.</span><span class="sxs-lookup"><span data-stu-id="059a6-354">Retrieve the team stats from the database.</span></span> |
| <span data-ttu-id="059a6-355">Rebuild DB (Перестроить базу данных)</span><span class="sxs-lookup"><span data-stu-id="059a6-355">Rebuild DB</span></span> |<span data-ttu-id="059a6-356">Повторная сборка базы данных и ее перезагрузка с использованием примера данных команды.</span><span class="sxs-lookup"><span data-stu-id="059a6-356">Rebuild the database and reload it with sample team data.</span></span> |
| <span data-ttu-id="059a6-357">Изменить; Сведения; Удалить</span><span class="sxs-lookup"><span data-stu-id="059a6-357">Edit / Details / Delete</span></span> |<span data-ttu-id="059a6-358">Изменение команды, просмотр сведений о команде, удаление команды.</span><span class="sxs-lookup"><span data-stu-id="059a6-358">Edit a team, view details for a team, delete a team.</span></span> |

<span data-ttu-id="059a6-359">Выполните некоторые действия и попробуйте получить данные из различных источников.</span><span class="sxs-lookup"><span data-stu-id="059a6-359">Click some of the actions and experiment with retrieving the data from the different sources.</span></span> <span data-ttu-id="059a6-360">Обратите внимание на разницу во времени при получении данных из базы данных и кэша разными способами.</span><span class="sxs-lookup"><span data-stu-id="059a6-360">Not the differences in the time it takes to complete the various ways of retrieving the data from the database and the cache.</span></span>

## <a name="delete-the-resources-when-you-are-finished-with-the-application"></a><span data-ttu-id="059a6-361">Удаление ресурсов после завершения работы с приложением</span><span class="sxs-lookup"><span data-stu-id="059a6-361">Delete the resources when you are finished with the application</span></span>
<span data-ttu-id="059a6-362">По окончании работы с примером приложения в руководстве можно удалить использованные ресурсы Azure, чтобы сократить затраты и сэкономить ресурсы.</span><span class="sxs-lookup"><span data-stu-id="059a6-362">When you are finished with the sample tutorial application, you can delete the Azure resources used in order to conserve cost and resources.</span></span> <span data-ttu-id="059a6-363">Если при работе с разделом **Подготовка ресурсов Azure к работе** использовалась кнопка [Deploy to Azure](#provision-the-azure-resources) (Развернуть в Azure) и все ресурсы находятся в одной группе ресурсов, их можно полностью удалить, удалив группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="059a6-363">If you use the **Deploy to Azure** button in the [Provision the Azure resources](#provision-the-azure-resources) section and all of your resources are contained in the same resource group, you can delete them together in one operation by deleting the resource group.</span></span>

1. <span data-ttu-id="059a6-364">Войдите на [портал Azure](https://portal.azure.com) и щелкните **Группы ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="059a6-364">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>
2. <span data-ttu-id="059a6-365">Введите имя группы ресурсов в текстовое поле **Фильтровать элементы…** .</span><span class="sxs-lookup"><span data-stu-id="059a6-365">Type the name of your resource group into the **Filter items...** textbox.</span></span>
3. <span data-ttu-id="059a6-366">Щелкните **…** справа от группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="059a6-366">Click **...** to the right of your resource group.</span></span>
4. <span data-ttu-id="059a6-367">Нажмите кнопку **Delete**(Удалить).</span><span class="sxs-lookup"><span data-stu-id="059a6-367">Click **Delete**.</span></span>
   
    ![Delete][cache-delete-resource-group]
5. <span data-ttu-id="059a6-369">Введите имя группы ресурсов и нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="059a6-369">Type the name of your resource group and click **Delete**.</span></span>
   
    ![Подтверждение удаления][cache-delete-confirm]

<span data-ttu-id="059a6-371">Через некоторое время группа ресурсов и все ее ресурсы будут удалены.</span><span class="sxs-lookup"><span data-stu-id="059a6-371">After a few moments the resource group and all of its contained resources are deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="059a6-372">Обратите внимание, что удаление группы ресурсов — необратимая операция, и все соответствующие ресурсы удаляются окончательно.</span><span class="sxs-lookup"><span data-stu-id="059a6-372">Note that deleting a resource group is irreversible and that the resource group and all the resources in it are permanently deleted.</span></span> <span data-ttu-id="059a6-373">Будьте внимательны, чтобы случайно не удалить не ту группу ресурсов или не те ресурсы.</span><span class="sxs-lookup"><span data-stu-id="059a6-373">Make sure that you do not accidentally delete the wrong resource group or resources.</span></span> <span data-ttu-id="059a6-374">Если ресурсы для размещения этого примера созданы в существующей группе ресурсов, можно удалить каждый ресурс отдельно в соответствующих колонках.</span><span class="sxs-lookup"><span data-stu-id="059a6-374">If you created the resources for hosting this sample inside an existing resource group, you can delete each resource individually from their respective blades.</span></span>
> 
> 

## <a name="run-the-sample-application-on-your-local-machine"></a><span data-ttu-id="059a6-375">Запуск примера приложения на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="059a6-375">Run the sample application on your local machine</span></span>
<span data-ttu-id="059a6-376">Чтобы запустить приложение локально на компьютере, необходим экземпляр кэша Redis для Azure, в котором следует кэшировать данные.</span><span class="sxs-lookup"><span data-stu-id="059a6-376">To run the application locally on your machine, you need an Azure Redis Cache instance in which to cache your data.</span></span> 

* <span data-ttu-id="059a6-377">Если приложение опубликовано в Azure, как описано в предыдущем разделе, можно использовать экземпляр кэша Redis для Azure, подготовленный к работе на этом шаге.</span><span class="sxs-lookup"><span data-stu-id="059a6-377">If you have published your application to Azure as described in the previous section, you can use the Azure Redis Cache instance that was provisioned during that step.</span></span>
* <span data-ttu-id="059a6-378">При наличии другого существующего экземпляра кэша Redis для Azure его можно использовать для локального запуска этого примера.</span><span class="sxs-lookup"><span data-stu-id="059a6-378">If you have another existing Azure Redis Cache instance, you can use that to run this sample locally.</span></span>
* <span data-ttu-id="059a6-379">Если необходимо создать экземпляр кэша Redis для Azure, следует выполнить действия, описанные в разделе [Создание кэша](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="059a6-379">If you need to create an Azure Redis Cache instance, you can follow the steps in [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

<span data-ttu-id="059a6-380">После выбора или создания кэша перейдите к нему на портале Azure и извлеките соответствующие [имя узла](cache-configure.md#properties) и [ключи доступа](cache-configure.md#access-keys).</span><span class="sxs-lookup"><span data-stu-id="059a6-380">Once you have selected or created the cache to use, browse to the cache in the Azure portal and retrieve the [host name](cache-configure.md#properties) and [access keys](cache-configure.md#access-keys) for your cache.</span></span> <span data-ttu-id="059a6-381">Инструкции см. в разделе [Настройка параметров кэша Redis](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="059a6-381">For instructions, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

1. <span data-ttu-id="059a6-382">Откройте файл `WebAppPlusCacheAppSecrets.config` , созданный на шаге [Настройка приложения для использования кэша Redis](#configure-the-application-to-use-redis-cache) этого руководства при помощи выбранного редактора.</span><span class="sxs-lookup"><span data-stu-id="059a6-382">Open the `WebAppPlusCacheAppSecrets.config` file that you created during the [Configure the application to use Redis Cache](#configure-the-application-to-use-redis-cache) step of this tutorial using the editor of your choice.</span></span>
2. <span data-ttu-id="059a6-383">Измените атрибут `value`, замените `MyCache.redis.cache.windows.net` [именем узла](cache-configure.md#properties) кэша и укажите [первичный или вторичный ключ](cache-configure.md#access-keys) кэша в качестве пароля.</span><span class="sxs-lookup"><span data-stu-id="059a6-383">Edit the `value` attribute and replace `MyCache.redis.cache.windows.net` with the [host name](cache-configure.md#properties) of your cache, and specify either the [primary or secondary key](cache-configure.md#access-keys) of your cache as the password.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="059a6-384">Для запуска приложения нажмите сочетание клавиш **Ctrl+F5** .</span><span class="sxs-lookup"><span data-stu-id="059a6-384">Press **Ctrl+F5** to run the application.</span></span>

> [!NOTE]
> <span data-ttu-id="059a6-385">Обратите внимание: так как приложение вместе с базой данных выполняется локально, а кэш Redis размещен в Azure, производительность кэша может быть ниже производительности базы данных.</span><span class="sxs-lookup"><span data-stu-id="059a6-385">Note that because the application, including the database, is running locally and the Redis Cache is hosted in Azure, the cache may appear to under-perform the database.</span></span> <span data-ttu-id="059a6-386">Чтобы повысить производительность, следует разместить клиентское приложение и экземпляр кэша Redis для Azure в одном расположении.</span><span class="sxs-lookup"><span data-stu-id="059a6-386">For best performance, the client application and Azure Redis Cache instance should be in the same location.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="059a6-387">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="059a6-387">Next steps</span></span>
* <span data-ttu-id="059a6-388">Дополнительные сведения о [начале работы с ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) можно получить на сайте [ASP.NET](http://asp.net/).</span><span class="sxs-lookup"><span data-stu-id="059a6-388">Learn more about [Getting Started with ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) on the [ASP.NET](http://asp.net/) site.</span></span>
* <span data-ttu-id="059a6-389">Дополнительные примеры создания веб-приложения ASP.NET в службе приложений см. в статье [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) (Создание и развертывание веб-приложения ASP.NET в службе приложений Azure), описывающей [демоверсию](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/) [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect.</span><span class="sxs-lookup"><span data-stu-id="059a6-389">For more examples of creating an ASP.NET Web App in App Service, see [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) from the [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span>
  * <span data-ttu-id="059a6-390">Дополнительные инструкции по быстрому началу работы с помощью средств разработчика Azure из демонстрационного проекта HealthClinic.biz см. [здесь](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="059a6-390">For more quickstarts from the HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>
* <span data-ttu-id="059a6-391">Узнайте больше о подходе [Code First для создания базы данных](https://msdn.microsoft.com/data/jj193542) в Entity Framework, использованном в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="059a6-391">Learn more about the [Code first to a new database](https://msdn.microsoft.com/data/jj193542) approach to Entity Framework that's used in this tutorial.</span></span>
* <span data-ttu-id="059a6-392">Узнайте больше о [веб-приложениях в службе приложений Azure](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="059a6-392">Learn more about [web apps in Azure App Service](../app-service-web/app-service-web-overview.md).</span></span>
* <span data-ttu-id="059a6-393">Узнайте, как [выполнять мониторинг](cache-how-to-monitor.md) кэша на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="059a6-393">Learn how to [monitor](cache-how-to-monitor.md) your cache in the Azure portal.</span></span>
* <span data-ttu-id="059a6-394">Изучите возможности кэша Redis для Azure уровня Premium:</span><span class="sxs-lookup"><span data-stu-id="059a6-394">Explore Azure Redis Cache premium features</span></span>
  
  * [<span data-ttu-id="059a6-395">Настройка сохраняемости для кэша Redis для Azure уровня Премиум</span><span class="sxs-lookup"><span data-stu-id="059a6-395">How to configure persistence for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-persistence.md)
  * [<span data-ttu-id="059a6-396">Настройка кластеризации для кэша Redis для Azure уровня Премиум</span><span class="sxs-lookup"><span data-stu-id="059a6-396">How to configure clustering for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-clustering.md)
  * [<span data-ttu-id="059a6-397">Настройка поддержки виртуальной сети для кэша Redis для Azure уровня Премиум</span><span class="sxs-lookup"><span data-stu-id="059a6-397">How to configure Virtual Network support for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-vnet.md)
  * <span data-ttu-id="059a6-398">Дополнительные сведения о размере, пропускной способности и полосе пропускания для кэшей уровня "Премиум" см. в статье [Кэш Redis для Azure. Вопросы и ответы](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span><span class="sxs-lookup"><span data-stu-id="059a6-398">See the [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) for more details about size, throughput, and bandwidth with premium caches.</span></span>

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

