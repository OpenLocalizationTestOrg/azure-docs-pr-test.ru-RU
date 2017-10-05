---
title: "Создание веб-приложения с использованием .NET и API DocumentDB в Azure Cosmos DB | Документация Майкрософт"
description: "В этой статье представлен пример кода .NET, который можно использовать для подключения и выполнения запросов к API DocumentDB в Azure Cosmos DB."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 9bb863261da64c97f99757d4a0cb3474a7755591
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-the-azure-portal"></a><span data-ttu-id="bf99f-103">Azure Cosmos DB. Создание веб-приложения API DocumentDB с использованием языка .NET и портала Azure</span><span class="sxs-lookup"><span data-stu-id="bf99f-103">Azure Cosmos DB: Build a DocumentDB API web app with .NET and the Azure portal</span></span>

<span data-ttu-id="bf99f-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="bf99f-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="bf99f-105">Вы можете быстро создавать и запрашивать документы, пары "ключ — значение" и базы данных графов, используя преимущества возможностей глобального распределения и горизонтального масштабирования Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bf99f-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="bf99f-106">В этом кратком руководстве показано, как создать учетную запись Azure Cosmos DB, базу данных документов и коллекцию с использованием портала Azure.</span><span class="sxs-lookup"><span data-stu-id="bf99f-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="bf99f-107">Затем вы создадите и развернете веб-приложение со списком дел на основе [API-интерфейса .NET для DocumentDB](documentdb-sdk-dotnet.md), как показано на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="bf99f-107">You'll then build and deploy a todo list web app built on the [DocumentDB .NET API](documentdb-sdk-dotnet.md), as shown in the following screenshot.</span></span> 

![Приложение со списком задач с демонстрационными данными](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a><span data-ttu-id="bf99f-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bf99f-109">Prerequisites</span></span>

<span data-ttu-id="bf99f-110">Если вы еще не установили Visual Studio 2017, вы можете скачать и использовать **бесплатный** [выпуск Community для Visual Studio 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="bf99f-110">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="bf99f-111">При установке Visual Studio необходимо включить возможность **разработки для Azure**.</span><span class="sxs-lookup"><span data-stu-id="bf99f-111">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="bf99f-112">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="bf99f-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
## <a name="add-a-collection"></a><span data-ttu-id="bf99f-113">Добавление коллекции</span><span class="sxs-lookup"><span data-stu-id="bf99f-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="bf99f-114">Добавление демонстрационных данных</span><span class="sxs-lookup"><span data-stu-id="bf99f-114">Add sample data</span></span>

<span data-ttu-id="bf99f-115">Теперь вы можете добавить данные в новую коллекцию с помощью обозревателя данных.</span><span class="sxs-lookup"><span data-stu-id="bf99f-115">You can now add data to your new collection using Data Explorer.</span></span>

1. <span data-ttu-id="bf99f-116">В обозревателе данных новая база данных отображается в области "Коллекции".</span><span class="sxs-lookup"><span data-stu-id="bf99f-116">In Data Explorer, the new database appears in the Collections pane.</span></span> <span data-ttu-id="bf99f-117">Разверните базу данных **Задачи** и коллекцию **Элементы**, выберите **Документы**, а затем щелкните **Новые документы**.</span><span class="sxs-lookup"><span data-stu-id="bf99f-117">Expand the **Tasks** database, expand the **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Создание документов в обозревателе данных на портале Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="bf99f-119">Теперь можно добавить документ в коллекцию со следующей структурой:</span><span class="sxs-lookup"><span data-stu-id="bf99f-119">Now add a document to the collection with the following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="bf99f-120">Добавив данные JSON на вкладке **Документы**, щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bf99f-120">Once you've added the json to the **Documents** tab, click **Save**.</span></span>

    ![Копирование данных JSON и нажатие кнопки "Сохранить" в обозревателе данных на портале Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="bf99f-122">Создайте и сохраните один или несколько документов, задав уникальное значение для свойства `id`, и измените другие свойства по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="bf99f-122">Create and save one more document where you insert a unique value for the `id` property, and change the other properties as you see fit.</span></span> <span data-ttu-id="bf99f-123">Новые документы могут иметь любую структуру, так как Azure Cosmos DB не устанавливает определенные схемы данных.</span><span class="sxs-lookup"><span data-stu-id="bf99f-123">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="bf99f-124">Теперь в обозревателе данных можно выполнить запросы на получение данных.</span><span class="sxs-lookup"><span data-stu-id="bf99f-124">You can now use queries in Data Explorer to retrieve your data.</span></span> <span data-ttu-id="bf99f-125">Чтобы получить все документы в коллекции, обозреватель данных по умолчанию использует запрос `SELECT * FROM c`. Но вы можете изменить его на другой [запрос SQL](documentdb-sql-query.md), например `SELECT * FROM c ORDER BY c._ts DESC`, который возвращает все документы в убывающем порядке по метке времени.</span><span class="sxs-lookup"><span data-stu-id="bf99f-125">By default, Data Explorer uses `SELECT * FROM c` to retrieve all documents in the collection, but you can change that to a different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, to return all the documents in descending order based on their timestamp.</span></span>
 
     <span data-ttu-id="bf99f-126">В обозревателе данных также можно создавать хранимые процедуры, триггеры и определяемые пользователем функции, чтобы реализовать бизнес-логику на стороне сервера и масштабировать пропускную способность.</span><span class="sxs-lookup"><span data-stu-id="bf99f-126">You can also use Data Explorer to create stored procedures, UDFs, and triggers to perform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="bf99f-127">Это средство позволяет использовать все встроенные возможности программного доступа к данным, доступные в API-интерфейсах, к которым вы можете быстро получить доступ на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="bf99f-127">Data Explorer exposes all of the built-in programmatic data access available in the APIs, but provides easy access to your data in the Azure portal.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="bf99f-128">Клонирование примера приложения</span><span class="sxs-lookup"><span data-stu-id="bf99f-128">Clone the sample application</span></span>

<span data-ttu-id="bf99f-129">Теперь перейдем к работе с кодом.</span><span class="sxs-lookup"><span data-stu-id="bf99f-129">Now let's switch to working with code.</span></span> <span data-ttu-id="bf99f-130">Давайте клонируем приложение API DocumentDB из GitHub, зададим строку подключения и выполним ее.</span><span class="sxs-lookup"><span data-stu-id="bf99f-130">Let's clone a DocumentDB API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="bf99f-131">Вы узнаете, как можно упростить работу с данными программным способом.</span><span class="sxs-lookup"><span data-stu-id="bf99f-131">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="bf99f-132">Откройте окно терминала Git, например Git Bash, и выполните команду `CD`, чтобы перейти в рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="bf99f-132">Open a git terminal window, such as git bash, and `CD` to a working directory.</span></span>  

2. <span data-ttu-id="bf99f-133">Выполните команду ниже, чтобы клонировать репозиторий с примером.</span><span class="sxs-lookup"><span data-stu-id="bf99f-133">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. <span data-ttu-id="bf99f-134">Затем откройте файл решения в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bf99f-134">Then open the todo solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="bf99f-135">Просмотр кода</span><span class="sxs-lookup"><span data-stu-id="bf99f-135">Review the code</span></span>

<span data-ttu-id="bf99f-136">Сделаем краткий обзор того, что происходит в приложении.</span><span class="sxs-lookup"><span data-stu-id="bf99f-136">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="bf99f-137">Откройте файл DocumentDBRepository.cs, и вы увидите, что эти строки кода создают ресурсы Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bf99f-137">Open the DocumentDBRepository.cs file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="bf99f-138">Экземпляр DocumentClient инициализируется в строке 73.</span><span class="sxs-lookup"><span data-stu-id="bf99f-138">The DocumentClient is initialized on line 73.</span></span>

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* <span data-ttu-id="bf99f-139">База данных создается в строке 88.</span><span class="sxs-lookup"><span data-stu-id="bf99f-139">A new database is created on line 88.</span></span>

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* <span data-ttu-id="bf99f-140">Коллекция создается в строке 107.</span><span class="sxs-lookup"><span data-stu-id="bf99f-140">A new collection is created on line 107.</span></span>

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="bf99f-141">Обновление строки подключения</span><span class="sxs-lookup"><span data-stu-id="bf99f-141">Update your connection string</span></span>

<span data-ttu-id="bf99f-142">Теперь вернитесь на портал Azure, чтобы получить данные строки подключения. Скопируйте эти данные в приложение.</span><span class="sxs-lookup"><span data-stu-id="bf99f-142">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="bf99f-143">На [портале Azure](http://portal.azure.com/) перейдите к учетной записи базы данных Azure Cosmos DB и на левой панели навигации щелкните **Ключи**, а затем выберите **Ключи записи-чтения**.</span><span class="sxs-lookup"><span data-stu-id="bf99f-143">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="bf99f-144">На следующем шаге используйте кнопку копирования в правой части экрана, чтобы скопировать универсальный код ресурса (URI) и первичный ключ в файл web.config.</span><span class="sxs-lookup"><span data-stu-id="bf99f-144">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the web.config file in the next step.</span></span>

    ![Просмотр и копирование ключа доступа на портале Azure, колонка "Ключи"](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="bf99f-146">В Visual Studio 2017 откройте файл web.config.</span><span class="sxs-lookup"><span data-stu-id="bf99f-146">In Visual Studio 2017, open the web.config file.</span></span> 

3. <span data-ttu-id="bf99f-147">Скопируйте значение универсального кода ресурса (URI) на портале (с помощью кнопки копирования) и добавьте его в качестве значения параметра ключа конечной точки в файле web.config.</span><span class="sxs-lookup"><span data-stu-id="bf99f-147">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in web.config.</span></span> 

    `<add key="endpoint" value="FILLME" />`

4. <span data-ttu-id="bf99f-148">Затем скопируйте значение первичного ключа с портала и добавьте его в качестве значения параметра authKey в файле web.config. Теперь приложение со всеми сведениями, необходимыми для взаимодействия с Azure Cosmos DB, обновлено.</span><span class="sxs-lookup"><span data-stu-id="bf99f-148">Then copy your PRIMARY KEY value from the portal and make it the value of the authKey in web.config. You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-the-web-app"></a><span data-ttu-id="bf99f-149">Запуск веб-приложения</span><span class="sxs-lookup"><span data-stu-id="bf99f-149">Run the web app</span></span>
1. <span data-ttu-id="bf99f-150">В Visual Studio в **обозревателе решений** щелкните проект правой кнопкой мыши и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="bf99f-150">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="bf99f-151">В окне NuGet в поле **Обзор** введите *DocumentDB*.</span><span class="sxs-lookup"><span data-stu-id="bf99f-151">In the NuGet **Browse** box, type *DocumentDB*.</span></span>

3. <span data-ttu-id="bf99f-152">В результатах поиска найдите библиотеку **Microsoft.Azure.DocumentDB** и установите ее.</span><span class="sxs-lookup"><span data-stu-id="bf99f-152">From the results, install the **Microsoft.Azure.DocumentDB** library.</span></span> <span data-ttu-id="bf99f-153">При этом будет установлен пакет Microsoft.Azure.DocumentDB, а также все зависимые компоненты.</span><span class="sxs-lookup"><span data-stu-id="bf99f-153">This installs the Microsoft.Azure.DocumentDB package as well as all dependencies.</span></span>

4. <span data-ttu-id="bf99f-154">Нажмите клавиши CTRL+F5 для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="bf99f-154">Click CTRL + F5 to run the application.</span></span> <span data-ttu-id="bf99f-155">Приложение откроется в браузере.</span><span class="sxs-lookup"><span data-stu-id="bf99f-155">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="bf99f-156">Щелкните **Создать** в браузере и создайте несколько задач в приложении со списком задач.</span><span class="sxs-lookup"><span data-stu-id="bf99f-156">Click **Create New** in the browser and create a few new tasks in your to-do app.</span></span>

   ![Приложение со списком задач с демонстрационными данными](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

<span data-ttu-id="bf99f-158">Вернитесь в обозреватель данных, где вы можете просматривать, запрашивать и изменять новые данные, а также работать с ними.</span><span class="sxs-lookup"><span data-stu-id="bf99f-158">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="bf99f-159">Просмотр соглашений об уровне обслуживания на портале Azure</span><span class="sxs-lookup"><span data-stu-id="bf99f-159">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="bf99f-160">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="bf99f-160">Clean up resources</span></span>

<span data-ttu-id="bf99f-161">Если вы не собираетесь использовать это приложение дальше, удалите все ресурсы, созданные в ходе работы с этим руководством, на портале Azure, сделав следующее:</span><span class="sxs-lookup"><span data-stu-id="bf99f-161">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="bf99f-162">В меню слева на портале Azure щелкните **Группы ресурсов**, а затем выберите имя созданного ресурса.</span><span class="sxs-lookup"><span data-stu-id="bf99f-162">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="bf99f-163">На странице группы ресурсов щелкните **Удалить**, в текстовом поле введите имя ресурса для удаления и щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="bf99f-163">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf99f-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bf99f-164">Next steps</span></span>

<span data-ttu-id="bf99f-165">В этом кратком руководстве вы узнали, как создать учетную запись Azure Cosmos DB, коллекцию с помощью обозревателя данных, а также как запустить веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="bf99f-165">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run a web app.</span></span> <span data-ttu-id="bf99f-166">Теперь можно импортировать дополнительные данные в учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bf99f-166">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="bf99f-167">Импорт данных в DocumentDB с помощью средства миграции базы данных</span><span class="sxs-lookup"><span data-stu-id="bf99f-167">Import data into Azure Cosmos DB</span></span>](import-data.md)


