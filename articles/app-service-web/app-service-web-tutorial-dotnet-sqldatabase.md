---
title: "Создание приложения ASP.NET в Azure с подключением к базе данных SQL | Документация Майкрософт"
description: "Узнайте, как создать в Azure приложение ASP.NET с подключением к базе данных SQL."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 06/09/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: c22b8ef4866fe2f1ae32c7cb9158fc7866788b26
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a><span data-ttu-id="e25b5-103">Создание приложения ASP.NET в Azure с подключением к базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="e25b5-103">Build an ASP.NET app in Azure with SQL Database</span></span>

<span data-ttu-id="e25b5-104">[Веб-приложения Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="e25b5-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="e25b5-105">В этом руководстве показано, как развернуть управляемое данными веб-приложение ASP.NET в Azure, а затем подключить его к [базе данных SQL Azure](../sql-database/sql-database-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e25b5-105">This tutorial shows you how to deploy a data-driven ASP.NET web app in Azure and connect it to [Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span></span> <span data-ttu-id="e25b5-106">Выполнив описанные здесь действия, вы получите приложение ASP.NET, запущенное в [службе приложений Azure](../app-service/app-service-value-prop-what-is.md) и подключенное к базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="e25b5-106">When you're finished, you have a ASP.NET app running in [Azure App Service](../app-service/app-service-value-prop-what-is.md) and connected to SQL Database.</span></span>

![Опубликованное приложение ASP.NET в веб-приложении Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="e25b5-108">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="e25b5-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e25b5-109">Создание базы данных SQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="e25b5-109">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="e25b5-110">Подключение приложения ASP.NET к базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="e25b5-110">Connect an ASP.NET app to SQL Database</span></span>
> * <span data-ttu-id="e25b5-111">Развертывание приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="e25b5-111">Deploy the app to Azure</span></span>
> * <span data-ttu-id="e25b5-112">Обновление модели данных и повторное развертывание приложения.</span><span class="sxs-lookup"><span data-stu-id="e25b5-112">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="e25b5-113">Потоковая передача журналов из Azure в окно терминала.</span><span class="sxs-lookup"><span data-stu-id="e25b5-113">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="e25b5-114">Управление приложением на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e25b5-114">Manage the app in the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e25b5-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e25b5-115">Prerequisites</span></span>

<span data-ttu-id="e25b5-116">Для работы с этим руководством:</span><span class="sxs-lookup"><span data-stu-id="e25b5-116">To complete this tutorial:</span></span>

* <span data-ttu-id="e25b5-117">Установите [Visual Studio 2017](https://www.visualstudio.com/downloads/) с указанными ниже рабочими нагрузками:</span><span class="sxs-lookup"><span data-stu-id="e25b5-117">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span></span>
  - <span data-ttu-id="e25b5-118">**ASP.NET и веб-разработка;**</span><span class="sxs-lookup"><span data-stu-id="e25b5-118">**ASP.NET and web development**</span></span>
  - <span data-ttu-id="e25b5-119">**разработка Azure.**</span><span class="sxs-lookup"><span data-stu-id="e25b5-119">**Azure development**</span></span>

  ![ASP.NET и веб-разработка, разработка Azure (в разделе Web & Cloud (Сеть и облако))](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample"></a><span data-ttu-id="e25b5-121">Скачивание примера приложения</span><span class="sxs-lookup"><span data-stu-id="e25b5-121">Download the sample</span></span>

<span data-ttu-id="e25b5-122">[Загрузите пример проекта](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="e25b5-122">[Download the sample project](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span></span>

<span data-ttu-id="e25b5-123">Извлеките (распакуйте) файл *dotnet-sqldb-tutorial-master.zip*.</span><span class="sxs-lookup"><span data-stu-id="e25b5-123">Extract (unzip) the  *dotnet-sqldb-tutorial-master.zip* file.</span></span>

<span data-ttu-id="e25b5-124">Этот пример проекта содержит простое MVC-приложение CRUD [ASP.NET](https://www.asp.net/mvc), созданное на основе [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="e25b5-124">The sample project contains a basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-read-update-delete) app using [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="run-the-app"></a><span data-ttu-id="e25b5-125">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="e25b5-125">Run the app</span></span>

<span data-ttu-id="e25b5-126">Откройте файл *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e25b5-126">Open the *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* file in Visual Studio.</span></span> 

<span data-ttu-id="e25b5-127">Введите `Ctrl+F5`, чтобы запустить приложение без отладки.</span><span class="sxs-lookup"><span data-stu-id="e25b5-127">Type `Ctrl+F5` to run the app without debugging.</span></span> <span data-ttu-id="e25b5-128">Это приложение откроется в браузере по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e25b5-128">The app is displayed in your default browser.</span></span> <span data-ttu-id="e25b5-129">Щелкните ссылку **Создать**, чтобы создать несколько элементов *списка дел*.</span><span class="sxs-lookup"><span data-stu-id="e25b5-129">Select the **Create New** link and create a couple *to-do* items.</span></span> 

![Диалоговое окно "Новый проект ASP.NET"](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

<span data-ttu-id="e25b5-131">Проверьте ссылки **Изменить**, **Сведения** и **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-131">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="e25b5-132">Чтобы подключиться к базе данных, приложение использует контекст базы данных.</span><span class="sxs-lookup"><span data-stu-id="e25b5-132">The app uses a database context to connect with the database.</span></span> <span data-ttu-id="e25b5-133">В этом примере контекст базы данных использует строку подключения `MyDbConnection`.</span><span class="sxs-lookup"><span data-stu-id="e25b5-133">In this sample, the database context uses a connection string named `MyDbConnection`.</span></span> <span data-ttu-id="e25b5-134">Строка подключения определена в файле *Web.config*. Ссылка на нее также имеется в файле *Models/MyDatabaseContext.cs*.</span><span class="sxs-lookup"><span data-stu-id="e25b5-134">The connection string is set in the *Web.config* file and referenced in the *Models/MyDatabaseContext.cs* file.</span></span> <span data-ttu-id="e25b5-135">Имя строки подключения потребуется далее в этом руководстве при подключении веб-приложения Azure к базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="e25b5-135">The connection string name is used later in the tutorial to connect the Azure web app to an Azure SQL Database.</span></span> 

## <a name="publish-to-azure-with-sql-database"></a><span data-ttu-id="e25b5-136">Публикация в Azure с базой данных SQL</span><span class="sxs-lookup"><span data-stu-id="e25b5-136">Publish to Azure with SQL Database</span></span>

<span data-ttu-id="e25b5-137">В **обозревателе решений** щелкните правой кнопкой мыши проект **DotNetAppSqlDb** и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-137">In the **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![Публикация в обозревателе решений](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="e25b5-139">Выберите **Служба приложений Microsoft Azure** и нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-139">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![Публикация с помощью страницы обзора проекта](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

<span data-ttu-id="e25b5-141">Во время публикации откроется диалоговое окно **Создать службу приложений**, с помощью которого вы можете создать все ресурсы Azure, необходимые для запуска веб-приложения ASP.NET в Azure.</span><span class="sxs-lookup"><span data-stu-id="e25b5-141">Publishing opens the **Create App Service** dialog, which helps you create all the Azure resources you need to run your ASP.NET web app in Azure.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="e25b5-142">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="e25b5-142">Sign in to Azure</span></span>

<span data-ttu-id="e25b5-143">В диалоговом окне **Создать службу приложений** щелкните **Добавить новую учетную запись**, а затем выполните вход в подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="e25b5-143">In the **Create App Service** dialog, click **Add an account**, and then sign in to your Azure subscription.</span></span> <span data-ttu-id="e25b5-144">Если вы уже вошли в учетную запись Майкрософт, проверьте, содержит ли она подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="e25b5-144">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="e25b5-145">Если подписки нет, щелкните ее, чтобы добавить правильную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="e25b5-145">If the signed-in Microsoft account doesn't have your Azure subscription, click it to add the correct account.</span></span>
   
![Вход в Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

<span data-ttu-id="e25b5-147">После того как вы войдете в систему, вы будете готовы создать все ресурсы, необходимые для веб-приложения Azure в этом диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="e25b5-147">Once signed in, you're ready to create all the resources you need for your Azure web app in this dialog.</span></span>

### <a name="configure-the-web-app-name"></a><span data-ttu-id="e25b5-148">Настройка имени веб-приложения</span><span class="sxs-lookup"><span data-stu-id="e25b5-148">Configure the web app name</span></span>

<span data-ttu-id="e25b5-149">Вы можете использовать созданное имя веб-приложения или присвоить ему уникальное имя (допустимые символы: `a-z`, `0-9` и `-`).</span><span class="sxs-lookup"><span data-stu-id="e25b5-149">You can keep the generated web app name, or change it to another unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="e25b5-150">Это имя используется как часть URL-адреса по умолчанию для приложения (`<app_name>.azurewebsites.net`, где `<app_name>` — имя вашего веб-приложения).</span><span class="sxs-lookup"><span data-stu-id="e25b5-150">The web app name is used as part of the default URL for your app (`<app_name>.azurewebsites.net`, where `<app_name>` is your web app name).</span></span> <span data-ttu-id="e25b5-151">Оно должно быть глобально уникальным среди всех приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="e25b5-151">The web app name needs to be unique across all apps in Azure.</span></span> 

![Диалоговое окно "Создание службы приложений"](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a><span data-ttu-id="e25b5-153">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="e25b5-153">Create a resource group</span></span>

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="e25b5-154">Рядом с **группой ресурсов** щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-154">Next to **Resource Group**, click **New**.</span></span>

![Рядом с группой ресурсов щелкните "Создать".](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

<span data-ttu-id="e25b5-156">Присвойте группе ресурсов имя **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-156">Name the resource group **myResourceGroup**.</span></span>

> [!NOTE]
> <span data-ttu-id="e25b5-157">Не нажимайте кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-157">Do not click **Create**.</span></span> <span data-ttu-id="e25b5-158">Сначала необходимо настроить базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="e25b5-158">You first need to set up a SQL Database in a later step.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="e25b5-159">Создание плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="e25b5-159">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="e25b5-160">Рядом с **планом службы приложений** щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-160">Next to **App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="e25b5-161">В диалоговом окне **Настроить план службы приложений** настройте новый план службы приложений, задав приведенные ниже параметры.</span><span class="sxs-lookup"><span data-stu-id="e25b5-161">In the **Configure App Service Plan** dialog, configure the new App Service plan with the following settings:</span></span>

![Создание плана службы приложений](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| <span data-ttu-id="e25b5-163">Настройка</span><span class="sxs-lookup"><span data-stu-id="e25b5-163">Setting</span></span>  | <span data-ttu-id="e25b5-164">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="e25b5-164">Suggested value</span></span> | <span data-ttu-id="e25b5-165">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="e25b5-165">For more information</span></span> |
| ----------------- | ------------ | ----|
|<span data-ttu-id="e25b5-166">**План службы приложений**</span><span class="sxs-lookup"><span data-stu-id="e25b5-166">**App Service Plan**</span></span>| <span data-ttu-id="e25b5-167">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="e25b5-167">myAppServicePlan</span></span> | [<span data-ttu-id="e25b5-168">Планы службы приложений</span><span class="sxs-lookup"><span data-stu-id="e25b5-168">App Service plans</span></span>](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|<span data-ttu-id="e25b5-169">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="e25b5-169">**Location**</span></span>| <span data-ttu-id="e25b5-170">Западная Европа</span><span class="sxs-lookup"><span data-stu-id="e25b5-170">West Europe</span></span> | [<span data-ttu-id="e25b5-171">Регионы Azure</span><span class="sxs-lookup"><span data-stu-id="e25b5-171">Azure regions</span></span>](https://azure.microsoft.com/regions/) |
|<span data-ttu-id="e25b5-172">**Размер**</span><span class="sxs-lookup"><span data-stu-id="e25b5-172">**Size**</span></span>| <span data-ttu-id="e25b5-173">Free</span><span class="sxs-lookup"><span data-stu-id="e25b5-173">Free</span></span> | [<span data-ttu-id="e25b5-174">Ценовые категории</span><span class="sxs-lookup"><span data-stu-id="e25b5-174">Pricing tiers</span></span>](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a><span data-ttu-id="e25b5-175">Создание экземпляра SQL Server</span><span class="sxs-lookup"><span data-stu-id="e25b5-175">Create a SQL Server instance</span></span>

<span data-ttu-id="e25b5-176">Перед созданием базы данных необходимо сначала создать [логический сервер базы данных SQL Azure](../sql-database/sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="e25b5-176">Before creating a database, you need an [Azure SQL Database logical server](../sql-database/sql-database-features.md).</span></span> <span data-ttu-id="e25b5-177">Логический сервер содержит группу баз данных, которыми можно управлять как группой.</span><span class="sxs-lookup"><span data-stu-id="e25b5-177">A logical server contains a group of databases managed as a group.</span></span>

<span data-ttu-id="e25b5-178">Выберите **Обзор дополнительных служб Azure**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-178">Select **Explore additional Azure services**.</span></span>

![Настройка имени веб-приложения](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

<span data-ttu-id="e25b5-180">На вкладке **Службы** щелкните значок **+** рядом с **базой данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-180">In the **Services** tab, click the **+** icon next to **SQL Database**.</span></span> 

![На вкладке "Службы" щелкните значок "плюс" (+) рядом с базой данных SQL.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

<span data-ttu-id="e25b5-182">В окне **Настройка базы данных SQL** нажмите кнопку **Создать** рядом с **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-182">In the **Configure SQL Database** dialog, click **New** next to **SQL Server**.</span></span> 

<span data-ttu-id="e25b5-183">Создается уникальное имя сервера.</span><span class="sxs-lookup"><span data-stu-id="e25b5-183">A unique server name is generated.</span></span> <span data-ttu-id="e25b5-184">Это имя используется как часть URL-адрес по умолчанию для логического сервера (`<server_name>.database.windows.net`).</span><span class="sxs-lookup"><span data-stu-id="e25b5-184">This name is used as part of the default URL for your logical server, `<server_name>.database.windows.net`.</span></span> <span data-ttu-id="e25b5-185">Оно должно быть уникальным для всех экземпляров логических серверов в Azure.</span><span class="sxs-lookup"><span data-stu-id="e25b5-185">It must be unique across all logical server instances in Azure.</span></span> <span data-ttu-id="e25b5-186">Имя сервера можно изменить, но в рамках этого руководства используйте созданное значение.</span><span class="sxs-lookup"><span data-stu-id="e25b5-186">You can change the server name, but for this tutorial, keep the generated value.</span></span>

<span data-ttu-id="e25b5-187">Добавьте имя пользователя и пароль администратора, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-187">Add an administrator username and password, and then select **OK**.</span></span> <span data-ttu-id="e25b5-188">Требования к сложности пароля см. в статье [Политика паролей](/sql/relational-databases/security/password-policy).</span><span class="sxs-lookup"><span data-stu-id="e25b5-188">For password complexity requirements, see [Password Policy](/sql/relational-databases/security/password-policy).</span></span>

<span data-ttu-id="e25b5-189">Запомните это имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="e25b5-189">Remember this username and password.</span></span> <span data-ttu-id="e25b5-190">Они потребуются позже для управления экземпляром логического сервера.</span><span class="sxs-lookup"><span data-stu-id="e25b5-190">You need them to manage the logical server instance later.</span></span>

![Создание экземпляра SQL Server](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a><span data-ttu-id="e25b5-192">Создание базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="e25b5-192">Create a SQL Database</span></span>

<span data-ttu-id="e25b5-193">В диалоговом окне **Настроить базу данных SQL**:</span><span class="sxs-lookup"><span data-stu-id="e25b5-193">In the **Configure SQL Database** dialog:</span></span> 

* <span data-ttu-id="e25b5-194">В поле **Имя базы данных** не изменяйте созданное по умолчанию имя.</span><span class="sxs-lookup"><span data-stu-id="e25b5-194">Keep the default generated **Database Name**.</span></span>
* <span data-ttu-id="e25b5-195">В поле **Имя строки подключения** введите *MyDbConnection*.</span><span class="sxs-lookup"><span data-stu-id="e25b5-195">In **Connection String Name**, type *MyDbConnection*.</span></span> <span data-ttu-id="e25b5-196">Это имя должно совпадать с именем строки подключения, указанном в *Models\MyDatabaseContext.cs*.</span><span class="sxs-lookup"><span data-stu-id="e25b5-196">This name must match the connection string that is referenced in *Models/MyDatabaseContext.cs*.</span></span>
* <span data-ttu-id="e25b5-197">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-197">Select **OK**.</span></span>

![Настройка базы данных SQL](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

<span data-ttu-id="e25b5-199">В диалоговом окне **Создать службу приложений** отобразятся созданные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e25b5-199">The **Create App Service** dialog shows the resources you've created.</span></span> <span data-ttu-id="e25b5-200">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-200">Click **Create**.</span></span> 

![Созданные ресурсы](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

<span data-ttu-id="e25b5-202">Когда мастер завершит создание ресурсов Azure, он опубликует приложение ASP.NET в Azure.</span><span class="sxs-lookup"><span data-stu-id="e25b5-202">Once the wizard finishes creating the Azure resources, it  publishes your ASP.NET app to Azure.</span></span> <span data-ttu-id="e25b5-203">Откроется браузер по умолчанию с URL-адресом развернутого приложения.</span><span class="sxs-lookup"><span data-stu-id="e25b5-203">Your default browser is launched with the URL to the deployed app.</span></span> 

<span data-ttu-id="e25b5-204">Добавьте несколько элементов списка дел.</span><span class="sxs-lookup"><span data-stu-id="e25b5-204">Add a few to-do items.</span></span>

![Опубликованное приложение ASP.NET в веб-приложении Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="e25b5-206">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="e25b5-206">Congratulations!</span></span> <span data-ttu-id="e25b5-207">Вы запустили управляемое данными приложение ASP.NET в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="e25b5-207">Your data-driven ASP.NET application is running live in Azure App Service.</span></span>

## <a name="access-the-sql-database-locally"></a><span data-ttu-id="e25b5-208">Локальный доступ к базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="e25b5-208">Access the SQL Database locally</span></span>

<span data-ttu-id="e25b5-209">В **обозревателе объектов SQL Server** Visual Studio вы сможете легко просматривать свою базу данных SQL и управлять ею.</span><span class="sxs-lookup"><span data-stu-id="e25b5-209">Visual Studio lets you explore and manage your new SQL Database easily in the **SQL Server Object Explorer**.</span></span>

### <a name="create-a-database-connection"></a><span data-ttu-id="e25b5-210">Создание подключения к базе данных</span><span class="sxs-lookup"><span data-stu-id="e25b5-210">Create a database connection</span></span>

<span data-ttu-id="e25b5-211">В меню **Представление** выберите **Обозреватель объектов SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-211">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="e25b5-212">В верхней части **обозревателя объектов SQL Server** нажмите кнопку **Добавить SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-212">At the top of **SQL Server Object Explorer**, click the **Add SQL Server** button.</span></span>

### <a name="configure-the-database-connection"></a><span data-ttu-id="e25b5-213">Настройка подключения к базе данных</span><span class="sxs-lookup"><span data-stu-id="e25b5-213">Configure the database connection</span></span>

<span data-ttu-id="e25b5-214">В диалоговом окне **Подключение** разверните узел **Azure**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-214">In the **Connect** dialog, expand the **Azure** node.</span></span> <span data-ttu-id="e25b5-215">Здесь перечислены все экземпляры базы данных SQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="e25b5-215">All your SQL Database instances in Azure are listed here.</span></span>

<span data-ttu-id="e25b5-216">Выберите базу данных SQL `DotNetAppSqlDb`.</span><span class="sxs-lookup"><span data-stu-id="e25b5-216">Select the `DotNetAppSqlDb` SQL Database.</span></span> <span data-ttu-id="e25b5-217">В нижней части автоматически появится созданное ранее подключение.</span><span class="sxs-lookup"><span data-stu-id="e25b5-217">The connection you created earlier is automatically filled at the bottom.</span></span>

<span data-ttu-id="e25b5-218">Введите созданный ранее пароль администратора базы данных и нажмите кнопку **Подключиться**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-218">Type the database administrator password you created earlier and click **Connect**.</span></span>

![Настройка подключения к базе данных из Visual Studio](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a><span data-ttu-id="e25b5-220">Разрешение клиентских подключений с вашего компьютера</span><span class="sxs-lookup"><span data-stu-id="e25b5-220">Allow client connection from your computer</span></span>

<span data-ttu-id="e25b5-221">Откроется диалоговое окно **Создать новое правило брандмауэра**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-221">The **Create a new firewall rule** dialog is opened.</span></span> <span data-ttu-id="e25b5-222">По умолчанию к экземпляру базы данных SQL могут подключаться только службы Azure, такие как ваше веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="e25b5-222">By default, your SQL Database instance only allows connections from Azure services, such as your Azure web app.</span></span> <span data-ttu-id="e25b5-223">Чтобы подключиться к базе данных, создайте правило брандмауэра в экземпляре базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="e25b5-223">To connect to your database, create a firewall rule in the SQL Database instance.</span></span> <span data-ttu-id="e25b5-224">Это правило разрешает подключения с общедоступного IP-адреса вашего локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="e25b5-224">The firewall rule allows the public IP address of your local computer.</span></span>

<span data-ttu-id="e25b5-225">В диалоговом окне уже указан общедоступный IP-адрес компьютера.</span><span class="sxs-lookup"><span data-stu-id="e25b5-225">The dialog is already filled with your computer's public IP address.</span></span>

<span data-ttu-id="e25b5-226">Убедитесь, что флажок **Добавить IP-адрес моего клиента** установлен, и щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-226">Make sure that **Add my client IP** is selected and click **OK**.</span></span> 

![Задание правила брандмауэра для экземпляра базы данных SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

<span data-ttu-id="e25b5-228">После окончания настройки брандмауэра для экземпляра базы данных SQL ваше подключение появится в **обозревателе объектов SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-228">Once Visual Studio finishes creating the firewall setting for your SQL Database instance, your connection shows up in **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="e25b5-229">В нем вы можете выполнять большинство распространенных операций с базой данных: выполнять запросы, создавать представления и хранимые процедуры и многое другое.</span><span class="sxs-lookup"><span data-stu-id="e25b5-229">Here, you can perform the most common database operations, such as run queries, create views and stored procedures, and more.</span></span> 

<span data-ttu-id="e25b5-230">Щелкните таблицу `Todoes` правой кнопкой мыши и выберите **Просмотреть данные**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-230">Right-click on the `Todoes` table and select **View Data**.</span></span> 

![Просмотр объектов базы данных SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a><span data-ttu-id="e25b5-232">Изменение приложения с помощью Code First Migrations</span><span class="sxs-lookup"><span data-stu-id="e25b5-232">Update app with Code First Migrations</span></span>

<span data-ttu-id="e25b5-233">Обновить базу данных и веб-приложение в Azure можно с помощью знакомых инструментов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e25b5-233">You can use the familiar tools in Visual Studio to update your database and web app in Azure.</span></span> <span data-ttu-id="e25b5-234">На этом шаге вы измените схему базы данных с помощью Code First Migrations в Entity Framework и опубликуете ее в Azure.</span><span class="sxs-lookup"><span data-stu-id="e25b5-234">In this step, you use Code First Migrations in Entity Framework to make a change to your database schema and publish it to Azure.</span></span>

<span data-ttu-id="e25b5-235">Дополнительные сведения об использовании Entity Framework Code First Migrations см. в статье [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application) (Начало работы с Entity Framework 6 Code First с помощью MVC 5).</span><span class="sxs-lookup"><span data-stu-id="e25b5-235">For more information about using Entity Framework Code First Migrations, see [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="e25b5-236">Обновление модели данных</span><span class="sxs-lookup"><span data-stu-id="e25b5-236">Update your data model</span></span>

<span data-ttu-id="e25b5-237">Откройте файл _Models\Todo.cs_ в редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="e25b5-237">Open _Models\Todo.cs_ in the code editor.</span></span> <span data-ttu-id="e25b5-238">Добавьте в класс `ToDo` следующее свойство:</span><span class="sxs-lookup"><span data-stu-id="e25b5-238">Add the following property to the `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="e25b5-239">Локальный запуск Code First Migrations</span><span class="sxs-lookup"><span data-stu-id="e25b5-239">Run Code First Migrations locally</span></span>

<span data-ttu-id="e25b5-240">Выполните несколько команд, чтобы обновить локальную базу данных.</span><span class="sxs-lookup"><span data-stu-id="e25b5-240">Run a few commands to make updates to your local database.</span></span> 

<span data-ttu-id="e25b5-241">В меню **Инструменты** выберите **Диспетчер пакетов NuGet** > **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-241">From the **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="e25b5-242">В окне консоли диспетчера пакетов включите Code First Migrations:</span><span class="sxs-lookup"><span data-stu-id="e25b5-242">In the Package Manager Console window, enable Code First Migrations:</span></span>

```PowerShell
Enable-Migrations
```

<span data-ttu-id="e25b5-243">Добавьте миграцию:</span><span class="sxs-lookup"><span data-stu-id="e25b5-243">Add a migration:</span></span>

```PowerShell
Add-Migration AddProperty
```

<span data-ttu-id="e25b5-244">Обновите локальную базу данных:</span><span class="sxs-lookup"><span data-stu-id="e25b5-244">Update the local database:</span></span>

```PowerShell
Update-Database
```

<span data-ttu-id="e25b5-245">Введите `Ctrl+F5`, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="e25b5-245">Type `Ctrl+F5` to run the app.</span></span> <span data-ttu-id="e25b5-246">Проверьте ссылки "Изменить", "Сведения" и "Создать".</span><span class="sxs-lookup"><span data-stu-id="e25b5-246">Test the edit, details, and create links.</span></span>

<span data-ttu-id="e25b5-247">Если приложение загружается без ошибок, Code First Migrations успешно включен.</span><span class="sxs-lookup"><span data-stu-id="e25b5-247">If the application loads without errors, then Code First Migrations has succeeded.</span></span> <span data-ttu-id="e25b5-248">Однако ваша страница не изменилась, так как новое свойство все еще не используется в логике приложения.</span><span class="sxs-lookup"><span data-stu-id="e25b5-248">However, your page still looks the same because your application logic is not using this new property yet.</span></span> 

### <a name="use-the-new-property"></a><span data-ttu-id="e25b5-249">Использование нового свойства</span><span class="sxs-lookup"><span data-stu-id="e25b5-249">Use the new property</span></span>

<span data-ttu-id="e25b5-250">Внесите некоторые изменения в код, чтобы использовалось свойство `Done`.</span><span class="sxs-lookup"><span data-stu-id="e25b5-250">Make some changes in your code to use the `Done` property.</span></span> <span data-ttu-id="e25b5-251">Для простоты мы изменим только представления `Index` и `Create`, чтобы просмотреть свойство в действии.</span><span class="sxs-lookup"><span data-stu-id="e25b5-251">For simplicity in this tutorial, you're only going to change the `Index` and `Create` views to see the property in action.</span></span>

<span data-ttu-id="e25b5-252">Откройте файл _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="e25b5-252">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="e25b5-253">Найдите метод `Create()` и добавьте `Done` в список свойств атрибута `Bind`.</span><span class="sxs-lookup"><span data-stu-id="e25b5-253">Find the `Create()` method and add `Done` to the list of properties in the `Bind` attribute.</span></span> <span data-ttu-id="e25b5-254">Когда все будет готово, сигнатура метода `Create()` должна выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e25b5-254">When you're done, your `Create()` method signature looks like the following code:</span></span>

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="e25b5-255">Откройте файл _Views\Todos\Create.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="e25b5-255">Open _Views\Todos\Create.cshtml_.</span></span>

<span data-ttu-id="e25b5-256">В коде Razor вы должны увидеть элемент `<div class="form-group">`, который использует `model.Description`, и еще один элемент `<div class="form-group">`, который использует `model.CreatedDate`.</span><span class="sxs-lookup"><span data-stu-id="e25b5-256">In the Razor code, you should see a `<div class="form-group">` element that uses `model.Description`, and then another `<div class="form-group">` element that uses `model.CreatedDate`.</span></span> <span data-ttu-id="e25b5-257">Сразу после этих двух элементов добавьте еще один элемент `<div class="form-group">`, который использует `model.Done`:</span><span class="sxs-lookup"><span data-stu-id="e25b5-257">Immediately following these two elements, add another `<div class="form-group">` element that uses `model.Done`:</span></span>

```csharp
<div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>
```

<span data-ttu-id="e25b5-258">Откройте файл _Views\Todos\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="e25b5-258">Open _Views\Todos\Index.cshtml_.</span></span>

<span data-ttu-id="e25b5-259">Найдите пустой элемент `<th></th>`.</span><span class="sxs-lookup"><span data-stu-id="e25b5-259">Search for the empty `<th></th>` element.</span></span> <span data-ttu-id="e25b5-260">Добавьте следующий код Razor над этим элементом:</span><span class="sxs-lookup"><span data-stu-id="e25b5-260">Just above this element, add the following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="e25b5-261">Найдите элемент `<td>`, который содержит вспомогательные методы `Html.ActionLink()`.</span><span class="sxs-lookup"><span data-stu-id="e25b5-261">Find the `<td>` element that contains the `Html.ActionLink()` helper methods.</span></span> <span data-ttu-id="e25b5-262">Добавьте следующий код Razor над этим элементом:</span><span class="sxs-lookup"><span data-stu-id="e25b5-262">Just above this element, add the following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="e25b5-263">Это все, что нужно сделать, чтобы увидеть изменения в представлениях `Index` и `Create`.</span><span class="sxs-lookup"><span data-stu-id="e25b5-263">That's all you need to see the changes in the `Index` and `Create` views.</span></span> 

<span data-ttu-id="e25b5-264">Введите `Ctrl+F5`, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="e25b5-264">Type `Ctrl+F5` to run the app.</span></span>

<span data-ttu-id="e25b5-265">Теперь вы сможете добавить элемент списка дел и установить флажок **Готово**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-265">You can now add a to-do item and check **Done**.</span></span> <span data-ttu-id="e25b5-266">После этого задание должно появиться на главной странице как выполненное.</span><span class="sxs-lookup"><span data-stu-id="e25b5-266">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="e25b5-267">Помните, что в представлении `Edit` не отображается поле `Done`, так как вы не изменили представление `Edit`.</span><span class="sxs-lookup"><span data-stu-id="e25b5-267">Remember that the `Edit` view doesn't show the `Done` field, because you didn't change the `Edit` view.</span></span>

### <a name="enable-code-first-migrations-in-azure"></a><span data-ttu-id="e25b5-268">Включение Code First Migrations в Azure</span><span class="sxs-lookup"><span data-stu-id="e25b5-268">Enable Code First Migrations in Azure</span></span>

<span data-ttu-id="e25b5-269">Теперь, когда изменения в коде, включая миграцию базы данных, выполнены успешно, можно опубликовать изменения в веб-приложение Azure, а также обновить базу данных SQL для использования Code First Migrations.</span><span class="sxs-lookup"><span data-stu-id="e25b5-269">Now that your code change works, including database migration, you publish it to your Azure web app and update your SQL Database with Code First Migrations too.</span></span>

<span data-ttu-id="e25b5-270">Как и прежде, щелкните правой кнопкой мыши свой проект и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-270">Just like before, right-click your project and select **Publish**.</span></span>

<span data-ttu-id="e25b5-271">Щелкните **Параметры**, чтобы открыть мастер публикации.</span><span class="sxs-lookup"><span data-stu-id="e25b5-271">Click **Settings** to open the publish wizard.</span></span>

![Открытие параметров публикации](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

<span data-ttu-id="e25b5-273">В мастере нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-273">In the wizard, click **Next**.</span></span>

<span data-ttu-id="e25b5-274">Убедитесь, что строка подключения для базы данных SQL в контексте **MyDatabaseContext (MyDbConnection)** заполнена.</span><span class="sxs-lookup"><span data-stu-id="e25b5-274">Make sure that the connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span></span> <span data-ttu-id="e25b5-275">Возможно, вам потребуется выбрать базу данных **myToDoAppDb** из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="e25b5-275">You may need to select the **myToDoAppDb** database from the dropdown.</span></span> 

<span data-ttu-id="e25b5-276">Установите флажок **Выполнять Code First Migrations (при запуске приложения)** и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-276">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span></span>

![Включение Code First Migrations в веб-приложении Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a><span data-ttu-id="e25b5-278">Публикация изменений</span><span class="sxs-lookup"><span data-stu-id="e25b5-278">Publish your changes</span></span>

<span data-ttu-id="e25b5-279">Включив Code First Migrations в веб-приложении Azure, опубликуйте изменения кода.</span><span class="sxs-lookup"><span data-stu-id="e25b5-279">Now that you enabled Code First Migrations in your Azure web app, publish your code changes.</span></span>

<span data-ttu-id="e25b5-280">На странице публикации щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-280">In the publish page, click **Publish**.</span></span>

<span data-ttu-id="e25b5-281">Попробуйте добавить новые задачи, устанавливая флажок **Готово**. Эти задачи должны появляться на главной странице как выполненные.</span><span class="sxs-lookup"><span data-stu-id="e25b5-281">Try adding to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span></span>

![Веб-приложение Azure после включения Code First Migrations](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

<span data-ttu-id="e25b5-283">Все имеющиеся элементы списка дел по-прежнему отображаются.</span><span class="sxs-lookup"><span data-stu-id="e25b5-283">All your existing to-do items are still displayed.</span></span> <span data-ttu-id="e25b5-284">При повторной публикации приложения ASP.NET существующие данные в базе данных SQL не теряются.</span><span class="sxs-lookup"><span data-stu-id="e25b5-284">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="e25b5-285">Кроме того, Code First Migrations изменяет только схему данных, оставляя существующие данные нетронутыми.</span><span class="sxs-lookup"><span data-stu-id="e25b5-285">Also, Code First Migrations only changes the data schema and leaves your existing data intact.</span></span>


## <a name="stream-application-logs"></a><span data-ttu-id="e25b5-286">Потоковая передача журналов приложений</span><span class="sxs-lookup"><span data-stu-id="e25b5-286">Stream application logs</span></span>

<span data-ttu-id="e25b5-287">Сообщения трассировки можно передавать прямо из веб-приложения Azure в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e25b5-287">You can stream tracing messages directly from your Azure web app to Visual Studio.</span></span>

<span data-ttu-id="e25b5-288">Откройте файл _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="e25b5-288">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="e25b5-289">Каждое действие начинается с метода `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="e25b5-289">Each action starts with a `Trace.WriteLine()` method.</span></span> <span data-ttu-id="e25b5-290">Этот код добавлен, чтобы показать, как добавить сообщения трассировки в веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="e25b5-290">This code is added to show you how to add trace messages to your Azure web app.</span></span>

### <a name="open-server-explorer"></a><span data-ttu-id="e25b5-291">Откройте обозреватель сервера</span><span class="sxs-lookup"><span data-stu-id="e25b5-291">Open Server Explorer</span></span>

<span data-ttu-id="e25b5-292">В меню **Представление** выберите **Обозреватель серверов**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-292">From the **View** menu, select **Server Explorer**.</span></span> <span data-ttu-id="e25b5-293">Ведение журнала для веб-приложения Azure можно включить в **обозревателе сервера**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-293">You can configure logging for your Azure web app in **Server Explorer**.</span></span> 

### <a name="enable-log-streaming"></a><span data-ttu-id="e25b5-294">Включение потоковой передачи журналов</span><span class="sxs-lookup"><span data-stu-id="e25b5-294">Enable log streaming</span></span>

<span data-ttu-id="e25b5-295">В **обозревателе сервера** выберите **Azure** > **Служба приложений**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-295">In **Server Explorer**, expand **Azure** > **App Service**.</span></span>

<span data-ttu-id="e25b5-296">Разверните группу ресурсов **myResourceGroup**, которая была создана при создании веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e25b5-296">Expand the **myResourceGroup** resource group, you created when you first created the Azure web app.</span></span>

<span data-ttu-id="e25b5-297">Щелкните веб-приложение правой кнопкой мыши и выберите **Просмотреть журналы потоковой передачи**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-297">Right-click your Azure web app and select **View Streaming Logs**.</span></span>

![Включение потоковой передачи журналов](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

<span data-ttu-id="e25b5-299">Теперь журналы передаются в окно **Выходные данные**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-299">The logs are now streamed into the **Output** window.</span></span> 

![Потоковая передача журналов в окне "Выходные данные"](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

<span data-ttu-id="e25b5-301">Однако сообщения трассировки пока не отображаются.</span><span class="sxs-lookup"><span data-stu-id="e25b5-301">However, you don't see any of the trace messages yet.</span></span> <span data-ttu-id="e25b5-302">Это объясняется тем, что когда вы в первый раз выбираете пункт меню **Просмотр журналов потоковой передачи**, веб-приложение устанавливает уровень трассировки в `Error`, при котором в журнал записываются только события ошибок (с помощью метода `Trace.TraceError()`).</span><span class="sxs-lookup"><span data-stu-id="e25b5-302">That's because when you first select **View Streaming Logs**, your Azure web app sets the trace level to `Error`, which only logs error events (with the `Trace.TraceError()` method).</span></span>

### <a name="change-trace-levels"></a><span data-ttu-id="e25b5-303">Изменение уровней трассировки</span><span class="sxs-lookup"><span data-stu-id="e25b5-303">Change trace levels</span></span>

<span data-ttu-id="e25b5-304">Чтобы изменить уровень трассировки для вывода других сообщений трассировки, вернитесь в **обозреватель сервера**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-304">To change the trace levels to output other trace messages, go back to **Server Explorer**.</span></span>

<span data-ttu-id="e25b5-305">Снова щелкните веб-приложение правой кнопкой мыши и выберите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-305">Right-click your Azure web app again and select **Settings**.</span></span>

<span data-ttu-id="e25b5-306">В раскрывающемся списке **Ведение журнала приложения (файловая система)** выберите **Подробно**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-306">In the **Application Logging (File System)** dropdown, select **Verbose**.</span></span> <span data-ttu-id="e25b5-307">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-307">Click **Save**.</span></span>

![Измените уровень трассировки на "Подробно"](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> <span data-ttu-id="e25b5-309">Вы можете поэкспериментировать с различными уровнями трассировки, чтобы посмотреть, какие типы сообщений отображаются для каждого уровня.</span><span class="sxs-lookup"><span data-stu-id="e25b5-309">You can experiment with different trace levels to see what types of messages are displayed for each level.</span></span> <span data-ttu-id="e25b5-310">Например, уровень **Информация** включает все журналы, созданные `Trace.TraceInformation()`, `Trace.TraceWarning()`, и `Trace.TraceError()`, но не включает журналы, созданные `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="e25b5-310">For example, the **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span></span>
>
>

<span data-ttu-id="e25b5-311">В браузере попробуйте щелкнуть мышью рядом со списком задач в Azure.</span><span class="sxs-lookup"><span data-stu-id="e25b5-311">In your browser, try clicking around the to-do list application in Azure.</span></span> <span data-ttu-id="e25b5-312">Теперь сообщения трассировки передаются в окно **Выходные данные** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e25b5-312">The trace messages are now streamed to the **Output** window in Visual Studio.</span></span>

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a><span data-ttu-id="e25b5-313">Выключение потоковой передачи журналов</span><span class="sxs-lookup"><span data-stu-id="e25b5-313">Stop log streaming</span></span>

<span data-ttu-id="e25b5-314">Чтобы остановить службу потоковой передачи журналов, нажмите кнопку **Остановить наблюдение** в окне **Выходные данные**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-314">To stop the log-streaming service, click the **Stop monitoring** button in the **Output** window.</span></span>

![Выключение потоковой передачи журналов](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="e25b5-316">Управление веб-приложением Azure</span><span class="sxs-lookup"><span data-stu-id="e25b5-316">Manage your Azure web app</span></span>

<span data-ttu-id="e25b5-317">Перейдите на [портал Azure](https://portal.azure.com), чтобы увидеть созданное веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="e25b5-317">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span> 



<span data-ttu-id="e25b5-318">В меню слева выберите **Служба приложений**, а затем щелкните имя своего веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="e25b5-318">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

![Переход к веб-приложению Azure на портале](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

<span data-ttu-id="e25b5-320">Вы попадете на страницу веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e25b5-320">You have landed in your web app's page.</span></span> 

<span data-ttu-id="e25b5-321">По умолчанию на портале отображается страница **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="e25b5-321">By default, the portal shows the **Overview** page.</span></span> <span data-ttu-id="e25b5-322">Здесь вы можете наблюдать за работой приложения.</span><span class="sxs-lookup"><span data-stu-id="e25b5-322">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="e25b5-323">Вы также можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление.</span><span class="sxs-lookup"><span data-stu-id="e25b5-323">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="e25b5-324">На вкладках в левой части страницы отображаются различные страницы конфигурации, которые можно открыть.</span><span class="sxs-lookup"><span data-stu-id="e25b5-324">The tabs on the left side of the page show the different configuration pages you can open.</span></span> 

![Страница службы приложений на портале Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="e25b5-326">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e25b5-326">Next steps</span></span>

<span data-ttu-id="e25b5-327">Из этого руководства вы узнали, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="e25b5-327">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e25b5-328">Создание базы данных SQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="e25b5-328">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="e25b5-329">Подключение приложения ASP.NET к базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="e25b5-329">Connect an ASP.NET app to SQL Database</span></span>
> * <span data-ttu-id="e25b5-330">Развертывание приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="e25b5-330">Deploy the app to Azure</span></span>
> * <span data-ttu-id="e25b5-331">Обновление модели данных и повторное развертывание приложения.</span><span class="sxs-lookup"><span data-stu-id="e25b5-331">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="e25b5-332">Потоковая передача журналов из Azure в окно терминала.</span><span class="sxs-lookup"><span data-stu-id="e25b5-332">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="e25b5-333">Управление приложением на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e25b5-333">Manage the app in the Azure portal</span></span>

<span data-ttu-id="e25b5-334">Перейдите к следующему руководству, чтобы научиться сопоставлять пользовательские DNS-имена с веб-приложением.</span><span class="sxs-lookup"><span data-stu-id="e25b5-334">Advance to the next tutorial to learn how to map a custom DNS name to the web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e25b5-335">Сопоставление существующего настраиваемого DNS-имени с веб-приложениями Azure</span><span class="sxs-lookup"><span data-stu-id="e25b5-335">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
