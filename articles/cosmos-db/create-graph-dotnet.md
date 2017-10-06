---
title: "Здравствуйте, aaaBuild приложения Azure Cosmos DB .NET с помощью Graph API | Документы Microsoft"
description: "Содержит образец кода .NET можно использовать tooconnect tooand запросов Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/28/2017
ms.author: denlee
ms.openlocfilehash: f28790fcb8c9f57c7bb3d844d8276fa04abcc39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-graph-api"></a><span data-ttu-id="8468c-103">Azure Cosmos DB: Сборка приложений .NET, использующих hello Graph API</span><span class="sxs-lookup"><span data-stu-id="8468c-103">Azure Cosmos DB: Build a .NET application using hello Graph API</span></span>

<span data-ttu-id="8468c-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="8468c-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="8468c-105">Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД.</span><span class="sxs-lookup"><span data-stu-id="8468c-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="8468c-106">В этом кратком руководстве показано, как toocreate учетную запись Azure Cosmos DB, базы данных и graph (контейнер) с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8468c-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, database, and graph (container) using hello Azure portal.</span></span> <span data-ttu-id="8468c-107">Затем постройте и запустите консольное приложение, построенных на hello [Graph API](graph-sdk-dotnet.md) (Предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="8468c-107">You then build and run a console app built on hello [Graph API](graph-sdk-dotnet.md) (preview).</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="8468c-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8468c-108">Prerequisites</span></span>

<span data-ttu-id="8468c-109">Если у вас еще нет Visual Studio 2017 г. установлен, можно загрузить и использовать hello **свободного** [2017 г. Visual Studio Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8468c-109">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="8468c-110">Убедитесь, что включен **разработки Azure** во время установки Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="8468c-110">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="8468c-111">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="8468c-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="8468c-112">Добавление графа</span><span class="sxs-lookup"><span data-stu-id="8468c-112">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="8468c-113">Пример приложения hello клонирования</span><span class="sxs-lookup"><span data-stu-id="8468c-113">Clone hello sample application</span></span>

<span data-ttu-id="8468c-114">Теперь давайте клон Graph API приложение из github, задайте строку подключения hello и запустите его.</span><span class="sxs-lookup"><span data-stu-id="8468c-114">Now let's clone a Graph API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="8468c-115">Вы увидите, как просто можно toowork с данными программными средствами.</span><span class="sxs-lookup"><span data-stu-id="8468c-115">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="8468c-116">Откройте окно терминала git, таких как git bash и `cd` tooa рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="8468c-116">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="8468c-117">Выполнения hello следующая команда репозитории примеров tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="8468c-117">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-dotnet-getting-started.git
    ```

3. <span data-ttu-id="8468c-118">Откройте Visual Studio и Привет открыть файл решения.</span><span class="sxs-lookup"><span data-stu-id="8468c-118">Then open Visual Studio and open hello solution file.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="8468c-119">Проверка кода hello</span><span class="sxs-lookup"><span data-stu-id="8468c-119">Review hello code</span></span>

<span data-ttu-id="8468c-120">Убедитесь, что происходит в приложение hello быстро ознакомиться.</span><span class="sxs-lookup"><span data-stu-id="8468c-120">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="8468c-121">Привет открыть файл Program.cs и вы найдете следующие строки кода создать hello Azure Cosmos DB ресурсы.</span><span class="sxs-lookup"><span data-stu-id="8468c-121">Open hello Program.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="8468c-122">Hello DocumentClient инициализируется.</span><span class="sxs-lookup"><span data-stu-id="8468c-122">hello DocumentClient is initialized.</span></span> <span data-ttu-id="8468c-123">В режиме предварительного просмотра hello мы добавили расширение graph API на клиенте Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="8468c-123">In hello preview, we added a graph extension API on hello Azure Cosmos DB client.</span></span> <span data-ttu-id="8468c-124">Мы работаем над автономный клиент графа, связаны с клиентом Azure Cosmos DB hello и ресурсы.</span><span class="sxs-lookup"><span data-stu-id="8468c-124">We are working on a standalone graph client decoupled from hello Azure Cosmos DB client and resources.</span></span>

    ```csharp
    using (DocumentClient client = new DocumentClient(
        new Uri(endpoint),
        authKey,
        new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp }))
    ```

* <span data-ttu-id="8468c-125">Создание базы данных.</span><span class="sxs-lookup"><span data-stu-id="8468c-125">A new database is created.</span></span>

    ```csharp
    Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" });
    ```

* <span data-ttu-id="8468c-126">Создание графа.</span><span class="sxs-lookup"><span data-stu-id="8468c-126">A new graph is created.</span></span>

    ```csharp
    DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync(
        UriFactory.CreateDatabaseUri("graphdb"),
        new DocumentCollection { Id = "graph" },
        new RequestOptions { OfferThroughput = 1000 });
    ```
* <span data-ttu-id="8468c-127">Последовательность шагов Gremlin выполняются с помощью hello `CreateGremlinQuery` метод.</span><span class="sxs-lookup"><span data-stu-id="8468c-127">A series of Gremlin steps are executed using hello `CreateGremlinQuery` method.</span></span>

    ```csharp
    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, "g.V().count()");
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="8468c-128">Обновление строки подключения</span><span class="sxs-lookup"><span data-stu-id="8468c-128">Update your connection string</span></span>

<span data-ttu-id="8468c-129">Теперь вернитесь toohello Azure портала tooget данные строки подключения и скопируйте его в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="8468c-129">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="8468c-130">Откройте файл App.config hello в Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="8468c-130">In Visual Studio 2017, open hello App.config file.</span></span> 

2. <span data-ttu-id="8468c-131">В hello в учетной записи Azure Cosmos DB портала Azure щелкните **ключей** в hello навигации слева.</span><span class="sxs-lookup"><span data-stu-id="8468c-131">In hello Azure portal, in your Azure Cosmos DB account, click **Keys** in hello left navigation.</span></span> 

    ![Просмотр и копирование первичного ключа в hello портал Azure, на странице приветствия ключей](./media/create-graph-dotnet/keys.png)

3. <span data-ttu-id="8468c-133">Копия вашего **URI** из портала hello и сделать его hello значение ключа hello конечной точки в файле App.config. Можно использовать "Копировать" hello ", как показано в предшествующих значение hello toocopy экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="8468c-133">Copy your **URI** value from hello portal and make it hello value of hello Endpoint key in App.config. You can use hello copy button as shown in hello preceding screenshot toocopy hello value.</span></span>

    `<add key="Endpoint" value="https://FILLME.documents.azure.com:443" />`

4. <span data-ttu-id="8468c-134">Копия вашего **ПЕРВИЧНОГО ключа** из портала hello и сделать его hello значение ключа AuthKey hello в файл App.config, а затем сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="8468c-134">Copy your **PRIMARY KEY** value from hello portal, and make it hello value of hello AuthKey key in App.config, then save your changes.</span></span> 

    `<add key="AuthKey" value="FILLME" />`

<span data-ttu-id="8468c-135">Теперь вы обновили приложения с все hello сведения учетной записи, он должен toocommunicate с Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8468c-135">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="run-hello-console-app"></a><span data-ttu-id="8468c-136">Запустите консольное приложение hello</span><span class="sxs-lookup"><span data-stu-id="8468c-136">Run hello console app</span></span>

1. <span data-ttu-id="8468c-137">В Visual Studio щелкните правой кнопкой мыши на hello **GraphGetStarted** проекта в **обозревателе решений** и нажмите кнопку **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="8468c-137">In Visual Studio, right-click on hello **GraphGetStarted** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="8468c-138">В hello NuGet **Обзор** введите *Microsoft.Azure.Graphs* и проверьте hello **включает предварительный выпуск** поле.</span><span class="sxs-lookup"><span data-stu-id="8468c-138">In hello NuGet **Browse** box, type *Microsoft.Azure.Graphs* and check hello **Includes prerelease** box.</span></span> 

3. <span data-ttu-id="8468c-139">На основе результатов hello установить hello **Microsoft.Azure.Graphs** библиотеки.</span><span class="sxs-lookup"><span data-stu-id="8468c-139">From hello results, install hello **Microsoft.Azure.Graphs** library.</span></span> <span data-ttu-id="8468c-140">При этом устанавливаются пакет библиотеки расширения graph Azure Cosmos DB hello и все зависимости.</span><span class="sxs-lookup"><span data-stu-id="8468c-140">This installs hello Azure Cosmos DB graph extension library package and all dependencies.</span></span>

    <span data-ttu-id="8468c-141">Если вы получите сообщение о рецензировании решения toohello изменения, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8468c-141">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="8468c-142">Если появится сообщение о принятии условий лицензионного соглашения, щелкните **Принимаю**.</span><span class="sxs-lookup"><span data-stu-id="8468c-142">If you get a message about license acceptance, click **I accept**.</span></span>

4. <span data-ttu-id="8468c-143">Нажмите сочетание клавиш CTRL + F5 toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8468c-143">Click CTRL + F5 toorun hello application.</span></span>

   <span data-ttu-id="8468c-144">окно консоли Hello отображает hello вершин и ребра, добавляемом toohello графа.</span><span class="sxs-lookup"><span data-stu-id="8468c-144">hello console window displays hello vertexes and edges being added toohello graph.</span></span> <span data-ttu-id="8468c-145">После завершения скрипта hello, нажмите клавишу ВВОД дважды tooclose окна консоли hello.</span><span class="sxs-lookup"><span data-stu-id="8468c-145">When hello script completes, press ENTER twice tooclose hello console window.</span></span> 

## <a name="browse-using-hello-data-explorer"></a><span data-ttu-id="8468c-146">Просмотр с помощью hello обозреватель данных</span><span class="sxs-lookup"><span data-stu-id="8468c-146">Browse using hello Data Explorer</span></span>

<span data-ttu-id="8468c-147">Теперь можно будет вернуться tooData обозревателя в hello портал Azure и просматривать и запрашивать данные новой диаграммы.</span><span class="sxs-lookup"><span data-stu-id="8468c-147">You can now go back tooData Explorer in hello Azure portal and browse and query your new graph data.</span></span>

1. <span data-ttu-id="8468c-148">В обозревателе данных hello новой базы данных отображается в области диаграмм hello.</span><span class="sxs-lookup"><span data-stu-id="8468c-148">In Data Explorer, hello new database appears in hello Graphs pane.</span></span> <span data-ttu-id="8468c-149">Разверните **graphdb** и **graphcollz**, а затем щелкните **График**.</span><span class="sxs-lookup"><span data-stu-id="8468c-149">Expand **graphdb**, **graphcollz**, and then click **Graph**.</span></span>

2. <span data-ttu-id="8468c-150">Нажмите кнопку hello **применить фильтр** по умолчанию hello toouse кнопку запрос tooview все verticies hello графике hello.</span><span class="sxs-lookup"><span data-stu-id="8468c-150">Click hello **Apply Filter** button toouse hello default query tooview all hello verticies in hello graph.</span></span> <span data-ttu-id="8468c-151">созданные hello пример приложения Hello данные отображаются в области диаграмм hello.</span><span class="sxs-lookup"><span data-stu-id="8468c-151">hello data generated by hello sample app is displayed in hello Graphs pane.</span></span>

    <span data-ttu-id="8468c-152">Вы можете увеличить и из него hello диаграммы, можно развернуть места на экране приветствия graph, добавить дополнительные verticies и перемещать поверхность отображения verticies на hello.</span><span class="sxs-lookup"><span data-stu-id="8468c-152">You can zoom in and out of hello graph, you can expand hello graph display space, add additional verticies, and move verticies on hello display surface.</span></span>

    ![Просмотр графика hello в обозревателе данных в hello портал Azure](./media/create-graph-dotnet/graph-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="8468c-154">Просмотрите соглашений об уровне обслуживания в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="8468c-154">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="8468c-155">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="8468c-155">Clean up resources</span></span>

<span data-ttu-id="8468c-156">Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="8468c-156">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="8468c-157">Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="8468c-157">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="8468c-158">На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="8468c-158">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8468c-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8468c-159">Next steps</span></span>

<span data-ttu-id="8468c-160">В этом кратком руководстве вы узнали, как создать граф, с помощью hello обозреватель данных toocreate учетную запись Azure Cosmos DB и запуск приложения.</span><span class="sxs-lookup"><span data-stu-id="8468c-160">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a graph using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="8468c-161">Теперь вы можете создавать более сложные запросы и внедрять эффективную логику обхода графа с помощью Gremlin.</span><span class="sxs-lookup"><span data-stu-id="8468c-161">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="8468c-162">Как выполнять запросы к данным в базе данных Azure Cosmos DB с помощью API Graph (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="8468c-162">Query using Gremlin</span></span>](tutorial-query-graph.md)

