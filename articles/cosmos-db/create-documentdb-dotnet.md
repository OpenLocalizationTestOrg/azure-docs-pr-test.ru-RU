---
title: "Azure Cosmos DB: Построение веб-приложения с помощью .NET и hello DocumentDB API | Документы Microsoft"
description: "Содержит образец кода .NET можно использовать запрос tooand tooconnect hello Azure Cosmos DB DocumentDB API"
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
ms.openlocfilehash: 35517e35d80c48662a51a99814652ffa1121fc5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-hello-azure-portal"></a><span data-ttu-id="b97e5-103">Azure Cosmos DB: Построение веб-приложения с помощью .NET DocumentDB API и hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="b97e5-103">Azure Cosmos DB: Build a DocumentDB API web app with .NET and hello Azure portal</span></span>

<span data-ttu-id="b97e5-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="b97e5-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="b97e5-105">Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД.</span><span class="sxs-lookup"><span data-stu-id="b97e5-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="b97e5-106">В этом кратком руководстве показано, как toocreate учетную запись Azure Cosmos DB документа базы данных и коллекцию с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b97e5-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="b97e5-107">Затем будет построения и развертывания веб-приложения todo список лежит hello [API .NET для DocumentDB](documentdb-sdk-dotnet.md), как показано в следующих экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="b97e5-107">You'll then build and deploy a todo list web app built on hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), as shown in hello following screenshot.</span></span> 

![Приложение со списком задач с демонстрационными данными](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a><span data-ttu-id="b97e5-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b97e5-109">Prerequisites</span></span>

<span data-ttu-id="b97e5-110">Если у вас еще нет Visual Studio 2017 г. установлен, можно загрузить и использовать hello **свободного** [2017 г. Visual Studio Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="b97e5-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="b97e5-111">Убедитесь, что включен **разработки Azure** во время установки Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="b97e5-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="b97e5-112">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="b97e5-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
## <a name="add-a-collection"></a><span data-ttu-id="b97e5-113">Добавление коллекции</span><span class="sxs-lookup"><span data-stu-id="b97e5-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="b97e5-114">Добавление демонстрационных данных</span><span class="sxs-lookup"><span data-stu-id="b97e5-114">Add sample data</span></span>

<span data-ttu-id="b97e5-115">Теперь можно добавить новую коллекцию tooyour данных с помощью обозревателя данных.</span><span class="sxs-lookup"><span data-stu-id="b97e5-115">You can now add data tooyour new collection using Data Explorer.</span></span>

1. <span data-ttu-id="b97e5-116">В обозревателе данных hello новой базы данных отображается в области коллекций hello.</span><span class="sxs-lookup"><span data-stu-id="b97e5-116">In Data Explorer, hello new database appears in hello Collections pane.</span></span> <span data-ttu-id="b97e5-117">Разверните hello **задачи** базы данных, разверните hello **элементы** коллекции, нажмите кнопку **документов**и нажмите кнопку **новые документы**.</span><span class="sxs-lookup"><span data-stu-id="b97e5-117">Expand hello **Tasks** database, expand hello **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Создавать новые документы в обозревателе данных hello портал Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="b97e5-119">Теперь можно добавьте коллекцию toohello документа с hello следующие структуры.</span><span class="sxs-lookup"><span data-stu-id="b97e5-119">Now add a document toohello collection with hello following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="b97e5-120">После добавления hello json toohello **документов** щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b97e5-120">Once you've added hello json toohello **Documents** tab, click **Save**.</span></span>

    ![Копировать данные json и нажмите кнопку Сохранить в обозревателе данных в hello портал Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="b97e5-122">Создать и сохранить один дополнительные документ, который вставляются уникальное значение для hello `id` и измените hello других свойств по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="b97e5-122">Create and save one more document where you insert a unique value for hello `id` property, and change hello other properties as you see fit.</span></span> <span data-ttu-id="b97e5-123">Новые документы могут иметь любую структуру, так как Azure Cosmos DB не устанавливает определенные схемы данных.</span><span class="sxs-lookup"><span data-stu-id="b97e5-123">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="b97e5-124">Теперь можно использовать запросы в обозреватель данных tooretrieve данные.</span><span class="sxs-lookup"><span data-stu-id="b97e5-124">You can now use queries in Data Explorer tooretrieve your data.</span></span> <span data-ttu-id="b97e5-125">По умолчанию используется обозреватель данных `SELECT * FROM c` tooretrieve всех документов в коллекции hello, но можно изменить, другой tooa [SQL-запроса](documentdb-sql-query.md), такие как `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn на основе все документы hello в порядке убывания их отметки времени.</span><span class="sxs-lookup"><span data-stu-id="b97e5-125">By default, Data Explorer uses `SELECT * FROM c` tooretrieve all documents in hello collection, but you can change that tooa different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn all hello documents in descending order based on their timestamp.</span></span>
 
     <span data-ttu-id="b97e5-126">Можно также использовать обозреватель данных toocreate хранимых процедур, определяемых пользователем функций и триггеров tooperform серверных бизнес-логику, также как масштаб пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="b97e5-126">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="b97e5-127">Обозреватель данных предоставляет все hello встроенного программного доступа к данным, доступны в API-интерфейсы hello, но предоставляет простой доступ к данным tooyour hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b97e5-127">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="b97e5-128">Пример приложения hello клонирования</span><span class="sxs-lookup"><span data-stu-id="b97e5-128">Clone hello sample application</span></span>

<span data-ttu-id="b97e5-129">Теперь давайте переключения tooworking с кодом.</span><span class="sxs-lookup"><span data-stu-id="b97e5-129">Now let's switch tooworking with code.</span></span> <span data-ttu-id="b97e5-130">Давайте клонировать приложении DocumentDB API из GitHub, задайте строку подключения hello и запустите его.</span><span class="sxs-lookup"><span data-stu-id="b97e5-130">Let's clone a DocumentDB API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="b97e5-131">Вы увидите, как просто можно toowork с данными программными средствами.</span><span class="sxs-lookup"><span data-stu-id="b97e5-131">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="b97e5-132">Откройте окно терминала git, таких как git bash и `CD` tooa рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="b97e5-132">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="b97e5-133">Выполнения hello следующая команда репозитории примеров tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="b97e5-133">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. <span data-ttu-id="b97e5-134">Затем откройте файл решения todo hello в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b97e5-134">Then open hello todo solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="b97e5-135">Проверка кода hello</span><span class="sxs-lookup"><span data-stu-id="b97e5-135">Review hello code</span></span>

<span data-ttu-id="b97e5-136">Убедитесь, что происходит в приложение hello быстро ознакомиться.</span><span class="sxs-lookup"><span data-stu-id="b97e5-136">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="b97e5-137">Привет открыть файл DocumentDBRepository.cs и вы найдете следующие строки кода создать hello Azure Cosmos DB ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b97e5-137">Open hello DocumentDBRepository.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="b97e5-138">Hello DocumentClient инициализируется в строке 73.</span><span class="sxs-lookup"><span data-stu-id="b97e5-138">hello DocumentClient is initialized on line 73.</span></span>

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* <span data-ttu-id="b97e5-139">База данных создается в строке 88.</span><span class="sxs-lookup"><span data-stu-id="b97e5-139">A new database is created on line 88.</span></span>

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* <span data-ttu-id="b97e5-140">Коллекция создается в строке 107.</span><span class="sxs-lookup"><span data-stu-id="b97e5-140">A new collection is created on line 107.</span></span>

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="b97e5-141">Обновление строки подключения</span><span class="sxs-lookup"><span data-stu-id="b97e5-141">Update your connection string</span></span>

<span data-ttu-id="b97e5-142">Теперь вернитесь toohello Azure портала tooget данные строки подключения и скопируйте его в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="b97e5-142">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="b97e5-143">В hello [портал Azure](http://portal.azure.com/), в вашей Azure Cosmos DB учетной записи, в hello навигации слева щелкните **ключей**и нажмите кнопку **чтения и записи ключей**.</span><span class="sxs-lookup"><span data-stu-id="b97e5-143">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="b97e5-144">Вы будете использовать кнопки копия hello hello правой части hello toocopy экрана приветствия URI и первичный ключ в файл web.config hello в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="b97e5-144">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello web.config file in hello next step.</span></span>

    ![Просмотреть и скопировать ключ доступа в hello портал Azure, ключи колонку](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="b97e5-146">Откройте файл web.config hello в Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="b97e5-146">In Visual Studio 2017, open hello web.config file.</span></span> 

3. <span data-ttu-id="b97e5-147">Скопируйте значение URI с портала hello (с использованием "Копировать" hello ") и сделать его hello значение ключа hello конечной точки в файле web.config.</span><span class="sxs-lookup"><span data-stu-id="b97e5-147">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in web.config.</span></span> 

    `<add key="endpoint" value="FILLME" />`

4. <span data-ttu-id="b97e5-148">Затем скопируйте значение ПЕРВИЧНОГО ключа из портала hello и сделать его hello значение authKey hello в файле web.config. Теперь вы обновили приложения с все hello сведения учетной записи, он должен toocommunicate с Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b97e5-148">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello authKey in web.config. You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-hello-web-app"></a><span data-ttu-id="b97e5-149">Запустите веб-приложение hello</span><span class="sxs-lookup"><span data-stu-id="b97e5-149">Run hello web app</span></span>
1. <span data-ttu-id="b97e5-150">В Visual Studio щелкните правой кнопкой мыши проект hello в **обозревателе решений** и нажмите кнопку **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b97e5-150">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="b97e5-151">В hello NuGet **Обзор** введите *DocumentDB*.</span><span class="sxs-lookup"><span data-stu-id="b97e5-151">In hello NuGet **Browse** box, type *DocumentDB*.</span></span>

3. <span data-ttu-id="b97e5-152">На основе результатов hello установить hello **Microsoft.Azure.DocumentDB** библиотеки.</span><span class="sxs-lookup"><span data-stu-id="b97e5-152">From hello results, install hello **Microsoft.Azure.DocumentDB** library.</span></span> <span data-ttu-id="b97e5-153">При этом устанавливаются hello Microsoft.Azure.DocumentDB пакета, а также все зависимости.</span><span class="sxs-lookup"><span data-stu-id="b97e5-153">This installs hello Microsoft.Azure.DocumentDB package as well as all dependencies.</span></span>

4. <span data-ttu-id="b97e5-154">Нажмите сочетание клавиш CTRL + F5 toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b97e5-154">Click CTRL + F5 toorun hello application.</span></span> <span data-ttu-id="b97e5-155">Приложение откроется в браузере.</span><span class="sxs-lookup"><span data-stu-id="b97e5-155">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="b97e5-156">Нажмите кнопку **создать новый** в hello браузера и создать несколько новых задач в приложении задачи.</span><span class="sxs-lookup"><span data-stu-id="b97e5-156">Click **Create New** in hello browser and create a few new tasks in your to-do app.</span></span>

   ![Приложение со списком задач с демонстрационными данными](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

<span data-ttu-id="b97e5-158">Теперь можно вернуться tooData обозревателя и запроса в разделе, изменения и работать с новые данные.</span><span class="sxs-lookup"><span data-stu-id="b97e5-158">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="b97e5-159">Просмотрите соглашений об уровне обслуживания в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="b97e5-159">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="b97e5-160">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="b97e5-160">Clean up resources</span></span>

<span data-ttu-id="b97e5-161">Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="b97e5-161">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="b97e5-162">Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="b97e5-162">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="b97e5-163">На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="b97e5-163">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b97e5-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b97e5-164">Next steps</span></span>

<span data-ttu-id="b97e5-165">В этом кратком руководстве вы узнали, как создать коллекцию с помощью hello обозреватель данных toocreate учетной записи Azure Cosmos DB и запуска веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="b97e5-165">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run a web app.</span></span> <span data-ttu-id="b97e5-166">Теперь можно импортировать учетной записи Cosmos DB tooyour дополнительные данные.</span><span class="sxs-lookup"><span data-stu-id="b97e5-166">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="b97e5-167">Импорт данных в DocumentDB с помощью средства миграции базы данных</span><span class="sxs-lookup"><span data-stu-id="b97e5-167">Import data into Azure Cosmos DB</span></span>](import-data.md)


