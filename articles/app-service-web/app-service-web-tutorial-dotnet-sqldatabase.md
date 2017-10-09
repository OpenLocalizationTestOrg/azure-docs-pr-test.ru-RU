---
title: "aaaBuild приложения ASP.NET в Azure с базой данных SQL | Документы Microsoft"
description: "Узнайте, как tooget ASP.NET приложения работают в Azure, с tooa подключения базы данных SQL."
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
ms.openlocfilehash: d21c2bc404bfe038608c17e5a94d96847153002c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a><span data-ttu-id="82682-103">Создание приложения ASP.NET в Azure с подключением к базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="82682-103">Build an ASP.NET app in Azure with SQL Database</span></span>

<span data-ttu-id="82682-104">[Веб-приложения Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="82682-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="82682-105">В этом учебнике показано, как toodeploy ASP.NET, управляемые данными веб-приложения в Azure и подключите его слишком[базы данных SQL Azure](../sql-database/sql-database-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="82682-105">This tutorial shows you how toodeploy a data-driven ASP.NET web app in Azure and connect it too[Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span></span> <span data-ttu-id="82682-106">Когда закончите, у вас есть приложения ASP.NET, работающего в [службе приложений Azure](../app-service/app-service-value-prop-what-is.md) и подключен tooSQL базы данных.</span><span class="sxs-lookup"><span data-stu-id="82682-106">When you're finished, you have a ASP.NET app running in [Azure App Service](../app-service/app-service-value-prop-what-is.md) and connected tooSQL Database.</span></span>

![Опубликованное приложение ASP.NET в веб-приложении Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="82682-108">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="82682-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="82682-109">Создание базы данных SQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="82682-109">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="82682-110">Подключение tooSQL приложения ASP.NET базы данных</span><span class="sxs-lookup"><span data-stu-id="82682-110">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="82682-111">Развертывание tooAzure приложения hello</span><span class="sxs-lookup"><span data-stu-id="82682-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="82682-112">Обновить модель данных hello и повторно развернуть приложение hello</span><span class="sxs-lookup"><span data-stu-id="82682-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="82682-113">Журналы Azure tooyour терминалов потока</span><span class="sxs-lookup"><span data-stu-id="82682-113">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="82682-114">Управление приложение hello в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="82682-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82682-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="82682-115">Prerequisites</span></span>

<span data-ttu-id="82682-116">toocomplete этого учебника:</span><span class="sxs-lookup"><span data-stu-id="82682-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="82682-117">Установка [2017 г. Visual Studio](https://www.visualstudio.com/downloads/) с hello следующие рабочие нагрузки:</span><span class="sxs-lookup"><span data-stu-id="82682-117">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello following workloads:</span></span>
  - <span data-ttu-id="82682-118">**ASP.NET и веб-разработка;**</span><span class="sxs-lookup"><span data-stu-id="82682-118">**ASP.NET and web development**</span></span>
  - <span data-ttu-id="82682-119">**разработка Azure.**</span><span class="sxs-lookup"><span data-stu-id="82682-119">**Azure development**</span></span>

  ![ASP.NET и веб-разработка, разработка Azure (в разделе Web & Cloud (Сеть и облако))](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a><span data-ttu-id="82682-121">Загрузить образец hello</span><span class="sxs-lookup"><span data-stu-id="82682-121">Download hello sample</span></span>

<span data-ttu-id="82682-122">[Загрузите образец проекта hello](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="82682-122">[Download hello sample project](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span></span>

<span data-ttu-id="82682-123">Извлечение (Распакуйте) hello *dotnet sqldb учебника master.zip* файл.</span><span class="sxs-lookup"><span data-stu-id="82682-123">Extract (unzip) hello  *dotnet-sqldb-tutorial-master.zip* file.</span></span>

<span data-ttu-id="82682-124">Образец Hello проекта содержит базовый [ASP.NET MVC](https://www.asp.net/mvc) CRUD (Создание чтение обновления и удаления) приложения с использованием [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="82682-124">hello sample project contains a basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-read-update-delete) app using [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="run-hello-app"></a><span data-ttu-id="82682-125">Выполните приложение hello</span><span class="sxs-lookup"><span data-stu-id="82682-125">Run hello app</span></span>

<span data-ttu-id="82682-126">Откройте hello *dotnet-sqldb учебник master/DotNetAppSqlDb.sln* файл в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82682-126">Open hello *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* file in Visual Studio.</span></span> 

<span data-ttu-id="82682-127">Тип `Ctrl+F5` toorun приложение hello без отладки.</span><span class="sxs-lookup"><span data-stu-id="82682-127">Type `Ctrl+F5` toorun hello app without debugging.</span></span> <span data-ttu-id="82682-128">приложение Hello отображается в браузере по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="82682-128">hello app is displayed in your default browser.</span></span> <span data-ttu-id="82682-129">Выберите hello **создать новый** связь и создать несколько *задачи* элементов.</span><span class="sxs-lookup"><span data-stu-id="82682-129">Select hello **Create New** link and create a couple *to-do* items.</span></span> 

![Диалоговое окно "Новый проект ASP.NET"](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

<span data-ttu-id="82682-131">Тест hello **изменить**, **сведения**, и **удалить** ссылки.</span><span class="sxs-lookup"><span data-stu-id="82682-131">Test hello **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="82682-132">приложение Hello использует tooconnect контекст базы данных с базой данных hello.</span><span class="sxs-lookup"><span data-stu-id="82682-132">hello app uses a database context tooconnect with hello database.</span></span> <span data-ttu-id="82682-133">В этом образце hello контекст базы данных использует строку подключения с именем `MyDbConnection`.</span><span class="sxs-lookup"><span data-stu-id="82682-133">In this sample, hello database context uses a connection string named `MyDbConnection`.</span></span> <span data-ttu-id="82682-134">задана строка соединения Hello в hello *Web.config* файл и на которую ссылается hello *Models/MyDatabaseContext.cs* файла.</span><span class="sxs-lookup"><span data-stu-id="82682-134">hello connection string is set in hello *Web.config* file and referenced in hello *Models/MyDatabaseContext.cs* file.</span></span> <span data-ttu-id="82682-135">Имя строки соединения Hello используется далее в tooan hello учебника tooconnect hello Azure web app базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="82682-135">hello connection string name is used later in hello tutorial tooconnect hello Azure web app tooan Azure SQL Database.</span></span> 

## <a name="publish-tooazure-with-sql-database"></a><span data-ttu-id="82682-136">Публикация tooAzure с базой данных SQL</span><span class="sxs-lookup"><span data-stu-id="82682-136">Publish tooAzure with SQL Database</span></span>

<span data-ttu-id="82682-137">В hello **обозревателе решений**, щелкните правой кнопкой мыши ваш **DotNetAppSqlDb** проект и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="82682-137">In hello **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![Публикация в обозревателе решений](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="82682-139">Выберите **Служба приложений Microsoft Azure** и нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="82682-139">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![Публикация с помощью страницы обзора проекта](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

<span data-ttu-id="82682-141">Публикация открывает hello **Создание приложения службы** диалоговое окно, в которых служит для создания всех hello Azure ресурсы, необходимые toorun веб-приложения ASP.NET в Azure.</span><span class="sxs-lookup"><span data-stu-id="82682-141">Publishing opens hello **Create App Service** dialog, which helps you create all hello Azure resources you need toorun your ASP.NET web app in Azure.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="82682-142">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="82682-142">Sign in tooAzure</span></span>

<span data-ttu-id="82682-143">В hello **Создание приложения службы** диалоговое окно, нажмите кнопку **добавить учетную запись**, а затем войдите в tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="82682-143">In hello **Create App Service** dialog, click **Add an account**, and then sign in tooyour Azure subscription.</span></span> <span data-ttu-id="82682-144">Если вы уже вошли в учетную запись Майкрософт, проверьте, содержит ли она подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="82682-144">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="82682-145">Если hello вход в учетную запись Майкрософт нет подписки Azure, щелкните его правильную учетную запись hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="82682-145">If hello signed-in Microsoft account doesn't have your Azure subscription, click it tooadd hello correct account.</span></span>
   
![Войдите в tooAzure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

<span data-ttu-id="82682-147">После входа вы готовы toocreate Здравствуйте, все ресурсы, необходимые для вашего веб-приложение Azure в этом диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="82682-147">Once signed in, you're ready toocreate all hello resources you need for your Azure web app in this dialog.</span></span>

### <a name="configure-hello-web-app-name"></a><span data-ttu-id="82682-148">Настройте имя веб-приложения hello</span><span class="sxs-lookup"><span data-stu-id="82682-148">Configure hello web app name</span></span>

<span data-ttu-id="82682-149">Можно сохранить имя веб-приложения создается hello, или изменить его уникальное имя tooanother (допустимые символы — `a-z`, `0-9`, и `-`).</span><span class="sxs-lookup"><span data-stu-id="82682-149">You can keep hello generated web app name, or change it tooanother unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="82682-150">Имя веб-приложения Hello используется как часть URL-адрес по умолчанию hello в приложении (`<app_name>.azurewebsites.net`, где `<app_name>` является имя вашего веб-приложения).</span><span class="sxs-lookup"><span data-stu-id="82682-150">hello web app name is used as part of hello default URL for your app (`<app_name>.azurewebsites.net`, where `<app_name>` is your web app name).</span></span> <span data-ttu-id="82682-151">Имя веб-приложения Hello должен toobe уникальным для всех приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="82682-151">hello web app name needs toobe unique across all apps in Azure.</span></span> 

![Диалоговое окно "Создание службы приложений"](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a><span data-ttu-id="82682-153">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="82682-153">Create a resource group</span></span>

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="82682-154">Далее слишком**группы ресурсов**, нажмите кнопку **New**.</span><span class="sxs-lookup"><span data-stu-id="82682-154">Next too**Resource Group**, click **New**.</span></span>

![Далее tooResource группы, нажмите кнопку Создать.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

<span data-ttu-id="82682-156">Имя группы ресурсов hello **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="82682-156">Name hello resource group **myResourceGroup**.</span></span>

> [!NOTE]
> <span data-ttu-id="82682-157">Не нажимайте кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="82682-157">Do not click **Create**.</span></span> <span data-ttu-id="82682-158">Необходимо сначала tooset копии базы данных SQL на более позднем этапе.</span><span class="sxs-lookup"><span data-stu-id="82682-158">You first need tooset up a SQL Database in a later step.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="82682-159">Создание плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="82682-159">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="82682-160">Далее слишком**план служб приложений**, нажмите кнопку **New**.</span><span class="sxs-lookup"><span data-stu-id="82682-160">Next too**App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="82682-161">В hello **настройте план обслуживания приложений** диалогового окна, Настройка hello новый план служб приложений с hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="82682-161">In hello **Configure App Service Plan** dialog, configure hello new App Service plan with hello following settings:</span></span>

![Создание плана службы приложений](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| <span data-ttu-id="82682-163">Настройка</span><span class="sxs-lookup"><span data-stu-id="82682-163">Setting</span></span>  | <span data-ttu-id="82682-164">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="82682-164">Suggested value</span></span> | <span data-ttu-id="82682-165">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="82682-165">For more information</span></span> |
| ----------------- | ------------ | ----|
|<span data-ttu-id="82682-166">**План службы приложений**</span><span class="sxs-lookup"><span data-stu-id="82682-166">**App Service Plan**</span></span>| <span data-ttu-id="82682-167">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="82682-167">myAppServicePlan</span></span> | [<span data-ttu-id="82682-168">Планы службы приложений</span><span class="sxs-lookup"><span data-stu-id="82682-168">App Service plans</span></span>](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|<span data-ttu-id="82682-169">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="82682-169">**Location**</span></span>| <span data-ttu-id="82682-170">Западная Европа</span><span class="sxs-lookup"><span data-stu-id="82682-170">West Europe</span></span> | [<span data-ttu-id="82682-171">Регионы Azure</span><span class="sxs-lookup"><span data-stu-id="82682-171">Azure regions</span></span>](https://azure.microsoft.com/regions/) |
|<span data-ttu-id="82682-172">**Размер**</span><span class="sxs-lookup"><span data-stu-id="82682-172">**Size**</span></span>| <span data-ttu-id="82682-173">Free</span><span class="sxs-lookup"><span data-stu-id="82682-173">Free</span></span> | [<span data-ttu-id="82682-174">Ценовые категории</span><span class="sxs-lookup"><span data-stu-id="82682-174">Pricing tiers</span></span>](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a><span data-ttu-id="82682-175">Создание экземпляра SQL Server</span><span class="sxs-lookup"><span data-stu-id="82682-175">Create a SQL Server instance</span></span>

<span data-ttu-id="82682-176">Перед созданием базы данных необходимо сначала создать [логический сервер базы данных SQL Azure](../sql-database/sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="82682-176">Before creating a database, you need an [Azure SQL Database logical server](../sql-database/sql-database-features.md).</span></span> <span data-ttu-id="82682-177">Логический сервер содержит группу баз данных, которыми можно управлять как группой.</span><span class="sxs-lookup"><span data-stu-id="82682-177">A logical server contains a group of databases managed as a group.</span></span>

<span data-ttu-id="82682-178">Выберите **Обзор дополнительных служб Azure**.</span><span class="sxs-lookup"><span data-stu-id="82682-178">Select **Explore additional Azure services**.</span></span>

![Настройка имени веб-приложения](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

<span data-ttu-id="82682-180">В hello **службы** щелкните hello  **+**  значок Далее слишком**базы данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="82682-180">In hello **Services** tab, click hello **+** icon next too**SQL Database**.</span></span> 

![На вкладке службы hello, щелкните значок + hello Далее tooSQL базы данных.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

<span data-ttu-id="82682-182">В hello **Настройка базы данных SQL** диалоговое окно, нажмите кнопку **New** Далее слишком**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="82682-182">In hello **Configure SQL Database** dialog, click **New** next too**SQL Server**.</span></span> 

<span data-ttu-id="82682-183">Создается уникальное имя сервера.</span><span class="sxs-lookup"><span data-stu-id="82682-183">A unique server name is generated.</span></span> <span data-ttu-id="82682-184">Это имя используется как часть URL-адрес по умолчанию hello для логического сервера, `<server_name>.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="82682-184">This name is used as part of hello default URL for your logical server, `<server_name>.database.windows.net`.</span></span> <span data-ttu-id="82682-185">Оно должно быть уникальным для всех экземпляров логических серверов в Azure.</span><span class="sxs-lookup"><span data-stu-id="82682-185">It must be unique across all logical server instances in Azure.</span></span> <span data-ttu-id="82682-186">Можно изменить имя сервера hello, но для этого учебника оставьте значение hello создан.</span><span class="sxs-lookup"><span data-stu-id="82682-186">You can change hello server name, but for this tutorial, keep hello generated value.</span></span>

<span data-ttu-id="82682-187">Добавьте имя пользователя и пароль администратора, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="82682-187">Add an administrator username and password, and then select **OK**.</span></span> <span data-ttu-id="82682-188">Требования к сложности пароля см. в статье [Политика паролей](/sql/relational-databases/security/password-policy).</span><span class="sxs-lookup"><span data-stu-id="82682-188">For password complexity requirements, see [Password Policy](/sql/relational-databases/security/password-policy).</span></span>

<span data-ttu-id="82682-189">Запомните это имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="82682-189">Remember this username and password.</span></span> <span data-ttu-id="82682-190">Они необходимы toomanage hello логического сервера экземпляр более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="82682-190">You need them toomanage hello logical server instance later.</span></span>

![Создание экземпляра SQL Server](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a><span data-ttu-id="82682-192">Создание базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="82682-192">Create a SQL Database</span></span>

<span data-ttu-id="82682-193">В hello **Настройка базы данных SQL** диалогового окна:</span><span class="sxs-lookup"><span data-stu-id="82682-193">In hello **Configure SQL Database** dialog:</span></span> 

* <span data-ttu-id="82682-194">Сохранить создаются по умолчанию hello **имя базы данных**.</span><span class="sxs-lookup"><span data-stu-id="82682-194">Keep hello default generated **Database Name**.</span></span>
* <span data-ttu-id="82682-195">В поле **Имя строки подключения** введите *MyDbConnection*.</span><span class="sxs-lookup"><span data-stu-id="82682-195">In **Connection String Name**, type *MyDbConnection*.</span></span> <span data-ttu-id="82682-196">Это имя должно соответствовать hello строку подключения, которая ссылается на *Models/MyDatabaseContext.cs*.</span><span class="sxs-lookup"><span data-stu-id="82682-196">This name must match hello connection string that is referenced in *Models/MyDatabaseContext.cs*.</span></span>
* <span data-ttu-id="82682-197">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="82682-197">Select **OK**.</span></span>

![Настройка базы данных SQL](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

<span data-ttu-id="82682-199">Hello **Создание приложения службы** диалоговое окно показывает hello ресурсов, вы создали.</span><span class="sxs-lookup"><span data-stu-id="82682-199">hello **Create App Service** dialog shows hello resources you've created.</span></span> <span data-ttu-id="82682-200">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="82682-200">Click **Create**.</span></span> 

![Hello ресурсы, которые вы создали](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

<span data-ttu-id="82682-202">После завершения выполнения мастера hello, создание hello ресурсы Azure, он публикует вашей tooAzure приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="82682-202">Once hello wizard finishes creating hello Azure resources, it  publishes your ASP.NET app tooAzure.</span></span> <span data-ttu-id="82682-203">Браузер по умолчанию запускается с toohello развернуть приложение hello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="82682-203">Your default browser is launched with hello URL toohello deployed app.</span></span> 

<span data-ttu-id="82682-204">Добавьте несколько элементов списка дел.</span><span class="sxs-lookup"><span data-stu-id="82682-204">Add a few to-do items.</span></span>

![Опубликованное приложение ASP.NET в веб-приложении Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="82682-206">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="82682-206">Congratulations!</span></span> <span data-ttu-id="82682-207">Вы запустили управляемое данными приложение ASP.NET в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="82682-207">Your data-driven ASP.NET application is running live in Azure App Service.</span></span>

## <a name="access-hello-sql-database-locally"></a><span data-ttu-id="82682-208">Доступ к локально hello базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="82682-208">Access hello SQL Database locally</span></span>

<span data-ttu-id="82682-209">Visual Studio позволяет просматривать и управлять ими новой базы данных SQL в hello **обозреватель объектов SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="82682-209">Visual Studio lets you explore and manage your new SQL Database easily in hello **SQL Server Object Explorer**.</span></span>

### <a name="create-a-database-connection"></a><span data-ttu-id="82682-210">Создание подключения к базе данных</span><span class="sxs-lookup"><span data-stu-id="82682-210">Create a database connection</span></span>

<span data-ttu-id="82682-211">Из hello **представление** последовательно выберите пункты **обозреватель объектов SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="82682-211">From hello **View** menu, select **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="82682-212">Вверху hello **обозреватель объектов SQL Server**, нажмите кнопку hello **добавить SQL Server** кнопку.</span><span class="sxs-lookup"><span data-stu-id="82682-212">At hello top of **SQL Server Object Explorer**, click hello **Add SQL Server** button.</span></span>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="82682-213">Подключение к базе данных hello</span><span class="sxs-lookup"><span data-stu-id="82682-213">Configure hello database connection</span></span>

<span data-ttu-id="82682-214">В hello **Connect** диалогового окна разверните hello **Azure** узла.</span><span class="sxs-lookup"><span data-stu-id="82682-214">In hello **Connect** dialog, expand hello **Azure** node.</span></span> <span data-ttu-id="82682-215">Здесь перечислены все экземпляры базы данных SQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="82682-215">All your SQL Database instances in Azure are listed here.</span></span>

<span data-ttu-id="82682-216">Выберите hello `DotNetAppSqlDb` базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="82682-216">Select hello `DotNetAppSqlDb` SQL Database.</span></span> <span data-ttu-id="82682-217">внизу hello автоматически заполняется Hello подключение, которое было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="82682-217">hello connection you created earlier is automatically filled at hello bottom.</span></span>

<span data-ttu-id="82682-218">Введите пароль администратора hello базы данных, созданной ранее и нажмите кнопку **Connect**.</span><span class="sxs-lookup"><span data-stu-id="82682-218">Type hello database administrator password you created earlier and click **Connect**.</span></span>

![Настройка подключения к базе данных из Visual Studio](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a><span data-ttu-id="82682-220">Разрешение клиентских подключений с вашего компьютера</span><span class="sxs-lookup"><span data-stu-id="82682-220">Allow client connection from your computer</span></span>

<span data-ttu-id="82682-221">Hello **Создание нового правила брандмауэра** открыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="82682-221">hello **Create a new firewall rule** dialog is opened.</span></span> <span data-ttu-id="82682-222">По умолчанию к экземпляру базы данных SQL могут подключаться только службы Azure, такие как ваше веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="82682-222">By default, your SQL Database instance only allows connections from Azure services, such as your Azure web app.</span></span> <span data-ttu-id="82682-223">tooconnect tooyour базы данных, необходимо создать правила брандмауэра в экземпляр базы данных SQL hello.</span><span class="sxs-lookup"><span data-stu-id="82682-223">tooconnect tooyour database, create a firewall rule in hello SQL Database instance.</span></span> <span data-ttu-id="82682-224">правило брандмауэра Hello допускает hello общедоступный IP-адрес локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="82682-224">hello firewall rule allows hello public IP address of your local computer.</span></span>

<span data-ttu-id="82682-225">диалоговое окно приветствия, уже заполненный общедоступный IP-адрес вашего компьютера.</span><span class="sxs-lookup"><span data-stu-id="82682-225">hello dialog is already filled with your computer's public IP address.</span></span>

<span data-ttu-id="82682-226">Убедитесь, что флажок **Добавить IP-адрес моего клиента** установлен, и щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="82682-226">Make sure that **Add my client IP** is selected and click **OK**.</span></span> 

![Задание правила брандмауэра для экземпляра базы данных SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

<span data-ttu-id="82682-228">После завершения выполнения Visual Studio, создав hello параметр брандмауэра для экземпляра базы данных SQL, подключение отображается в **обозреватель объектов SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="82682-228">Once Visual Studio finishes creating hello firewall setting for your SQL Database instance, your connection shows up in **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="82682-229">Здесь можно выполнять создание hello наиболее распространенные базы данных операций, например выполнения запросов, представлений и хранимых процедур и многое другое.</span><span class="sxs-lookup"><span data-stu-id="82682-229">Here, you can perform hello most common database operations, such as run queries, create views and stored procedures, and more.</span></span> 

<span data-ttu-id="82682-230">Щелкните правой кнопкой мыши на hello `Todoes` таблицы и выберите **данные представления**.</span><span class="sxs-lookup"><span data-stu-id="82682-230">Right-click on hello `Todoes` table and select **View Data**.</span></span> 

![Просмотр объектов базы данных SQL](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a><span data-ttu-id="82682-232">Изменение приложения с помощью Code First Migrations</span><span class="sxs-lookup"><span data-stu-id="82682-232">Update app with Code First Migrations</span></span>

<span data-ttu-id="82682-233">Можно использовать знакомые средства hello в Visual Studio tooupdate базы данных и веб-приложения, в Azure.</span><span class="sxs-lookup"><span data-stu-id="82682-233">You can use hello familiar tools in Visual Studio tooupdate your database and web app in Azure.</span></span> <span data-ttu-id="82682-234">На этом шаге можно использовать миграции Code First в Entity Framework toomake изменение tooyour схемы базы данных, а также опубликовать tooAzure.</span><span class="sxs-lookup"><span data-stu-id="82682-234">In this step, you use Code First Migrations in Entity Framework toomake a change tooyour database schema and publish it tooAzure.</span></span>

<span data-ttu-id="82682-235">Дополнительные сведения об использовании Entity Framework Code First Migrations см. в статье [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application) (Начало работы с Entity Framework 6 Code First с помощью MVC 5).</span><span class="sxs-lookup"><span data-stu-id="82682-235">For more information about using Entity Framework Code First Migrations, see [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="82682-236">Обновление модели данных</span><span class="sxs-lookup"><span data-stu-id="82682-236">Update your data model</span></span>

<span data-ttu-id="82682-237">Откройте _Models\Todo.cs_ в редакторе кода hello.</span><span class="sxs-lookup"><span data-stu-id="82682-237">Open _Models\Todo.cs_ in hello code editor.</span></span> <span data-ttu-id="82682-238">Добавьте следующие свойства toohello hello `ToDo` класса:</span><span class="sxs-lookup"><span data-stu-id="82682-238">Add hello following property toohello `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="82682-239">Локальный запуск Code First Migrations</span><span class="sxs-lookup"><span data-stu-id="82682-239">Run Code First Migrations locally</span></span>

<span data-ttu-id="82682-240">Запустите несколько команд toomake обновления tooyour локальной базы данных.</span><span class="sxs-lookup"><span data-stu-id="82682-240">Run a few commands toomake updates tooyour local database.</span></span> 

<span data-ttu-id="82682-241">Из hello **средства** меню, нажмите кнопку **диспетчера пакетов NuGet** > **консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="82682-241">From hello **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="82682-242">В hello в окне консоли диспетчера пакетов включите Code First Migrations:</span><span class="sxs-lookup"><span data-stu-id="82682-242">In hello Package Manager Console window, enable Code First Migrations:</span></span>

```PowerShell
Enable-Migrations
```

<span data-ttu-id="82682-243">Добавьте миграцию:</span><span class="sxs-lookup"><span data-stu-id="82682-243">Add a migration:</span></span>

```PowerShell
Add-Migration AddProperty
```

<span data-ttu-id="82682-244">Обновление hello локальной базы данных:</span><span class="sxs-lookup"><span data-stu-id="82682-244">Update hello local database:</span></span>

```PowerShell
Update-Database
```

<span data-ttu-id="82682-245">Тип `Ctrl+F5` toorun приложение hello.</span><span class="sxs-lookup"><span data-stu-id="82682-245">Type `Ctrl+F5` toorun hello app.</span></span> <span data-ttu-id="82682-246">Тест hello, редактирования и создать связи.</span><span class="sxs-lookup"><span data-stu-id="82682-246">Test hello edit, details, and create links.</span></span>

<span data-ttu-id="82682-247">Если приложение hello загружается без ошибок, Code First Migrations завершилась успешно.</span><span class="sxs-lookup"><span data-stu-id="82682-247">If hello application loads without errors, then Code First Migrations has succeeded.</span></span> <span data-ttu-id="82682-248">Тем не менее содержатся в электронной таблице страницы по-прежнему hello таким же, так как логика приложения еще не использует это новое свойство.</span><span class="sxs-lookup"><span data-stu-id="82682-248">However, your page still looks hello same because your application logic is not using this new property yet.</span></span> 

### <a name="use-hello-new-property"></a><span data-ttu-id="82682-249">Использовать новое свойство hello</span><span class="sxs-lookup"><span data-stu-id="82682-249">Use hello new property</span></span>

<span data-ttu-id="82682-250">Внести некоторые изменения в ваш код toouse hello `Done` свойство.</span><span class="sxs-lookup"><span data-stu-id="82682-250">Make some changes in your code toouse hello `Done` property.</span></span> <span data-ttu-id="82682-251">Для простоты в этом учебнике только ты toochange hello `Index` и `Create` представления hello свойство toosee в действие.</span><span class="sxs-lookup"><span data-stu-id="82682-251">For simplicity in this tutorial, you're only going toochange hello `Index` and `Create` views toosee hello property in action.</span></span>

<span data-ttu-id="82682-252">Откройте файл _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="82682-252">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="82682-253">Найти hello `Create()` метода и добавьте `Done` toohello список свойств в hello `Bind` атрибута.</span><span class="sxs-lookup"><span data-stu-id="82682-253">Find hello `Create()` method and add `Done` toohello list of properties in hello `Bind` attribute.</span></span> <span data-ttu-id="82682-254">Когда закончите, ваш `Create()` сигнатура метода выглядит hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="82682-254">When you're done, your `Create()` method signature looks like hello following code:</span></span>

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="82682-255">Откройте файл _Views\Todos\Create.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="82682-255">Open _Views\Todos\Create.cshtml_.</span></span>

<span data-ttu-id="82682-256">В hello кода Razor, вы увидите `<div class="form-group">` элемент, который использует `model.Description`и еще один `<div class="form-group">` элемент, который использует `model.CreatedDate`.</span><span class="sxs-lookup"><span data-stu-id="82682-256">In hello Razor code, you should see a `<div class="form-group">` element that uses `model.Description`, and then another `<div class="form-group">` element that uses `model.CreatedDate`.</span></span> <span data-ttu-id="82682-257">Сразу после этих двух элементов добавьте еще один элемент `<div class="form-group">`, который использует `model.Done`:</span><span class="sxs-lookup"><span data-stu-id="82682-257">Immediately following these two elements, add another `<div class="form-group">` element that uses `model.Done`:</span></span>

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

<span data-ttu-id="82682-258">Откройте файл _Views\Todos\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="82682-258">Open _Views\Todos\Index.cshtml_.</span></span>

<span data-ttu-id="82682-259">Поиск hello пустой `<th></th>` элемента.</span><span class="sxs-lookup"><span data-stu-id="82682-259">Search for hello empty `<th></th>` element.</span></span> <span data-ttu-id="82682-260">Только что выше этого элемента добавьте после кода Razor hello:</span><span class="sxs-lookup"><span data-stu-id="82682-260">Just above this element, add hello following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="82682-261">Найти hello `<td>` элемент, содержащий hello `Html.ActionLink()` вспомогательные методы.</span><span class="sxs-lookup"><span data-stu-id="82682-261">Find hello `<td>` element that contains hello `Html.ActionLink()` helper methods.</span></span> <span data-ttu-id="82682-262">Только что выше этого элемента добавьте после кода Razor hello:</span><span class="sxs-lookup"><span data-stu-id="82682-262">Just above this element, add hello following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="82682-263">Вот и все необходимые изменения toosee hello в hello `Index` и `Create` представления.</span><span class="sxs-lookup"><span data-stu-id="82682-263">That's all you need toosee hello changes in hello `Index` and `Create` views.</span></span> 

<span data-ttu-id="82682-264">Тип `Ctrl+F5` toorun приложение hello.</span><span class="sxs-lookup"><span data-stu-id="82682-264">Type `Ctrl+F5` toorun hello app.</span></span>

<span data-ttu-id="82682-265">Теперь вы сможете добавить элемент списка дел и установить флажок **Готово**.</span><span class="sxs-lookup"><span data-stu-id="82682-265">You can now add a to-do item and check **Done**.</span></span> <span data-ttu-id="82682-266">После этого задание должно появиться на главной странице как выполненное.</span><span class="sxs-lookup"><span data-stu-id="82682-266">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="82682-267">Помните, что hello `Edit` представления не показывает hello `Done` поле, так как не были изменены hello `Edit` представления.</span><span class="sxs-lookup"><span data-stu-id="82682-267">Remember that hello `Edit` view doesn't show hello `Done` field, because you didn't change hello `Edit` view.</span></span>

### <a name="enable-code-first-migrations-in-azure"></a><span data-ttu-id="82682-268">Включение Code First Migrations в Azure</span><span class="sxs-lookup"><span data-stu-id="82682-268">Enable Code First Migrations in Azure</span></span>

<span data-ttu-id="82682-269">Теперь, когда код работает, включая перенос базы данных изменений публикации его tooyour Azure веб-приложения и обновления базы данных SQL с помощью Code First Migrations слишком.</span><span class="sxs-lookup"><span data-stu-id="82682-269">Now that your code change works, including database migration, you publish it tooyour Azure web app and update your SQL Database with Code First Migrations too.</span></span>

<span data-ttu-id="82682-270">Как и прежде, щелкните правой кнопкой мыши свой проект и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="82682-270">Just like before, right-click your project and select **Publish**.</span></span>

<span data-ttu-id="82682-271">Нажмите кнопку **параметры** tooopen hello мастер публикации.</span><span class="sxs-lookup"><span data-stu-id="82682-271">Click **Settings** tooopen hello publish wizard.</span></span>

![Открытие параметров публикации](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

<span data-ttu-id="82682-273">В мастере приветствия щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="82682-273">In hello wizard, click **Next**.</span></span>

<span data-ttu-id="82682-274">Убедитесь, что эта строка подключения hello для заполнения базы данных SQL в **MyDatabaseContext (MyDbConnection)**.</span><span class="sxs-lookup"><span data-stu-id="82682-274">Make sure that hello connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span></span> <span data-ttu-id="82682-275">Может потребоваться tooselect hello **myToDoAppDb** базы данных из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="82682-275">You may need tooselect hello **myToDoAppDb** database from hello dropdown.</span></span> 

<span data-ttu-id="82682-276">Установите флажок **Выполнять Code First Migrations (при запуске приложения)** и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="82682-276">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span></span>

![Включение Code First Migrations в веб-приложении Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a><span data-ttu-id="82682-278">Публикация изменений</span><span class="sxs-lookup"><span data-stu-id="82682-278">Publish your changes</span></span>

<span data-ttu-id="82682-279">Включив Code First Migrations в веб-приложении Azure, опубликуйте изменения кода.</span><span class="sxs-lookup"><span data-stu-id="82682-279">Now that you enabled Code First Migrations in your Azure web app, publish your code changes.</span></span>

<span data-ttu-id="82682-280">Страница "Публикация" hello, щелкните **публикации**.</span><span class="sxs-lookup"><span data-stu-id="82682-280">In hello publish page, click **Publish**.</span></span>

<span data-ttu-id="82682-281">Попробуйте добавить новые задачи, устанавливая флажок **Готово**. Эти задачи должны появляться на главной странице как выполненные.</span><span class="sxs-lookup"><span data-stu-id="82682-281">Try adding to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span></span>

![Веб-приложение Azure после включения Code First Migrations](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

<span data-ttu-id="82682-283">Все имеющиеся элементы списка дел по-прежнему отображаются.</span><span class="sxs-lookup"><span data-stu-id="82682-283">All your existing to-do items are still displayed.</span></span> <span data-ttu-id="82682-284">При повторной публикации приложения ASP.NET существующие данные в базе данных SQL не теряются.</span><span class="sxs-lookup"><span data-stu-id="82682-284">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="82682-285">Кроме того, Code First Migrations только изменения схемы данных hello и оставляет без изменений существующих данных.</span><span class="sxs-lookup"><span data-stu-id="82682-285">Also, Code First Migrations only changes hello data schema and leaves your existing data intact.</span></span>


## <a name="stream-application-logs"></a><span data-ttu-id="82682-286">Потоковая передача журналов приложений</span><span class="sxs-lookup"><span data-stu-id="82682-286">Stream application logs</span></span>

<span data-ttu-id="82682-287">Можно осуществлять потоковую передачу сообщений трассировки непосредственно из вашего Azure web app tooVisual Studio.</span><span class="sxs-lookup"><span data-stu-id="82682-287">You can stream tracing messages directly from your Azure web app tooVisual Studio.</span></span>

<span data-ttu-id="82682-288">Откройте файл _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="82682-288">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="82682-289">Каждое действие начинается с метода `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="82682-289">Each action starts with a `Trace.WriteLine()` method.</span></span> <span data-ttu-id="82682-290">Этот код добавляется tooshow вы способ трассировки tooadd сообщений tooyour веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="82682-290">This code is added tooshow you how tooadd trace messages tooyour Azure web app.</span></span>

### <a name="open-server-explorer"></a><span data-ttu-id="82682-291">Откройте обозреватель сервера</span><span class="sxs-lookup"><span data-stu-id="82682-291">Open Server Explorer</span></span>

<span data-ttu-id="82682-292">Из hello **представление** последовательно выберите пункты **обозревателя серверов**.</span><span class="sxs-lookup"><span data-stu-id="82682-292">From hello **View** menu, select **Server Explorer**.</span></span> <span data-ttu-id="82682-293">Ведение журнала для веб-приложения Azure можно включить в **обозревателе сервера**.</span><span class="sxs-lookup"><span data-stu-id="82682-293">You can configure logging for your Azure web app in **Server Explorer**.</span></span> 

### <a name="enable-log-streaming"></a><span data-ttu-id="82682-294">Включение потоковой передачи журналов</span><span class="sxs-lookup"><span data-stu-id="82682-294">Enable log streaming</span></span>

<span data-ttu-id="82682-295">В **обозревателе сервера** выберите **Azure** > **Служба приложений**.</span><span class="sxs-lookup"><span data-stu-id="82682-295">In **Server Explorer**, expand **Azure** > **App Service**.</span></span>

<span data-ttu-id="82682-296">Разверните hello **myResourceGroup** группы ресурсов, созданный при первом создании hello Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="82682-296">Expand hello **myResourceGroup** resource group, you created when you first created hello Azure web app.</span></span>

<span data-ttu-id="82682-297">Щелкните веб-приложение правой кнопкой мыши и выберите **Просмотреть журналы потоковой передачи**.</span><span class="sxs-lookup"><span data-stu-id="82682-297">Right-click your Azure web app and select **View Streaming Logs**.</span></span>

![Включение потоковой передачи журналов](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

<span data-ttu-id="82682-299">Hello журналы теперь потока можно добиться hello **вывода** окна.</span><span class="sxs-lookup"><span data-stu-id="82682-299">hello logs are now streamed into hello **Output** window.</span></span> 

![Потоковая передача журналов в окне "Выходные данные"](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

<span data-ttu-id="82682-301">Тем не менее вы не видите сообщения трассировки hello еще.</span><span class="sxs-lookup"><span data-stu-id="82682-301">However, you don't see any of hello trace messages yet.</span></span> <span data-ttu-id="82682-302">Который так, как при первом обращении **Просмотр журналов потоковой передачи**, Azure веб-приложение задает уровень трассировки hello слишком`Error`, какие только журналы событий ошибок (с hello `Trace.TraceError()` метода).</span><span class="sxs-lookup"><span data-stu-id="82682-302">That's because when you first select **View Streaming Logs**, your Azure web app sets hello trace level too`Error`, which only logs error events (with hello `Trace.TraceError()` method).</span></span>

### <a name="change-trace-levels"></a><span data-ttu-id="82682-303">Изменение уровней трассировки</span><span class="sxs-lookup"><span data-stu-id="82682-303">Change trace levels</span></span>

<span data-ttu-id="82682-304">трассировки hello toochange уровни toooutput другие сообщения трассировки, перейдите назад слишком**обозревателя серверов**.</span><span class="sxs-lookup"><span data-stu-id="82682-304">toochange hello trace levels toooutput other trace messages, go back too**Server Explorer**.</span></span>

<span data-ttu-id="82682-305">Снова щелкните веб-приложение правой кнопкой мыши и выберите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="82682-305">Right-click your Azure web app again and select **Settings**.</span></span>

<span data-ttu-id="82682-306">В hello **ведение журнала приложения (файловая система)** раскрывающийся список, выберите **Verbose**.</span><span class="sxs-lookup"><span data-stu-id="82682-306">In hello **Application Logging (File System)** dropdown, select **Verbose**.</span></span> <span data-ttu-id="82682-307">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="82682-307">Click **Save**.</span></span>

![Изменение уровня tooVerbose трассировки](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> <span data-ttu-id="82682-309">Можно поэкспериментировать с toosee уровни трассировки разные каких типов сообщений отображаются для каждого уровня.</span><span class="sxs-lookup"><span data-stu-id="82682-309">You can experiment with different trace levels toosee what types of messages are displayed for each level.</span></span> <span data-ttu-id="82682-310">Здравствуйте, например, **сведения** уровень включает все журналы, созданные `Trace.TraceInformation()`, `Trace.TraceWarning()`, и `Trace.TraceError()`, но не журналы, созданные `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="82682-310">For example, hello **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span></span>
>
>

<span data-ttu-id="82682-311">В браузере щелкните правой кнопкой мыши вокруг приложения список дел hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="82682-311">In your browser, try clicking around hello to-do list application in Azure.</span></span> <span data-ttu-id="82682-312">сообщения трассировки Hello теперь потоком toohello **выходной** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82682-312">hello trace messages are now streamed toohello **Output** window in Visual Studio.</span></span>

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a><span data-ttu-id="82682-313">Выключение потоковой передачи журналов</span><span class="sxs-lookup"><span data-stu-id="82682-313">Stop log streaming</span></span>

<span data-ttu-id="82682-314">toostop Здравствуйте потоковой передачи журнала службы, нажмите кнопку hello **Остановить наблюдение** кнопку в hello **вывода** окна.</span><span class="sxs-lookup"><span data-stu-id="82682-314">toostop hello log-streaming service, click hello **Stop monitoring** button in hello **Output** window.</span></span>

![Выключение потоковой передачи журналов](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="82682-316">Управление веб-приложением Azure</span><span class="sxs-lookup"><span data-stu-id="82682-316">Manage your Azure web app</span></span>

<span data-ttu-id="82682-317">Go toohello [портал Azure](https://portal.azure.com) toosee hello веб-приложения был создан.</span><span class="sxs-lookup"><span data-stu-id="82682-317">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span> 



<span data-ttu-id="82682-318">Hello в левом меню, щелкните **службы приложений**, затем щелкните имя hello Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="82682-318">From hello left menu, click **App Service**, then click hello name of your Azure web app.</span></span>

![Веб-приложения портала навигации tooAzure](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

<span data-ttu-id="82682-320">Вы попадете на страницу веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="82682-320">You have landed in your web app's page.</span></span> 

<span data-ttu-id="82682-321">По умолчанию hello портал отображает hello **Обзор** страницы.</span><span class="sxs-lookup"><span data-stu-id="82682-321">By default, hello portal shows hello **Overview** page.</span></span> <span data-ttu-id="82682-322">Здесь вы можете наблюдать за работой приложения.</span><span class="sxs-lookup"><span data-stu-id="82682-322">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="82682-323">Вы также можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление.</span><span class="sxs-lookup"><span data-stu-id="82682-323">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="82682-324">Hello вкладках hello левой части страницы приветствия отображаются страницы hello другой конфигурации, которые можно открыть.</span><span class="sxs-lookup"><span data-stu-id="82682-324">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span> 

![Страница службы приложений на портале Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="82682-326">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="82682-326">Next steps</span></span>

<span data-ttu-id="82682-327">Из этого руководства вы узнали, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="82682-327">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="82682-328">Создание базы данных SQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="82682-328">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="82682-329">Подключение tooSQL приложения ASP.NET базы данных</span><span class="sxs-lookup"><span data-stu-id="82682-329">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="82682-330">Развертывание tooAzure приложения hello</span><span class="sxs-lookup"><span data-stu-id="82682-330">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="82682-331">Обновить модель данных hello и повторно развернуть приложение hello</span><span class="sxs-lookup"><span data-stu-id="82682-331">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="82682-332">Журналы Azure tooyour терминалов потока</span><span class="sxs-lookup"><span data-stu-id="82682-332">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="82682-333">Управление приложение hello в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="82682-333">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="82682-334">Переместить следующий учебник toolearn toohello как toomap пользовательские DNS имя toohello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="82682-334">Advance toohello next tutorial toolearn how toomap a custom DNS name toohello web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="82682-335">Сопоставьте существующий пользовательский DNS имя tooAzure веб-приложений</span><span class="sxs-lookup"><span data-stu-id="82682-335">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
