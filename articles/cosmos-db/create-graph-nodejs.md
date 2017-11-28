---
title: "Создание приложения Azure Cosmos DB на платформе Node.js с помощью API Graph | Документация Майкрософт"
description: "В этой статье представлен пример кода Node.js, который можно использовать для подключения и выполнения запросов к Azure Cosmos DB."
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
ms.date: 07/14/2017
ms.author: denlee
ms.openlocfilehash: 6d14719938af0ce825955389824441e111024869
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-build-a-nodejs-application-by-using-graph-api"></a><span data-ttu-id="7dd01-103">Azure Cosmos DB. Создание приложения Node.js с помощью API Graph</span><span class="sxs-lookup"><span data-stu-id="7dd01-103">Azure Cosmos DB: Build a Node.js application by using Graph API</span></span>

<span data-ttu-id="7dd01-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="7dd01-104">Azure Cosmos DB is the globally distributed multi-model database service from Microsoft.</span></span> <span data-ttu-id="7dd01-105">Вы можете быстро создавать и запрашивать документы, пары "ключ — значение" и базы данных графов, используя преимущества возможностей глобального распределения и горизонтального масштабирования базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7dd01-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="7dd01-106">В этом кратком руководстве объясняется, как создать учетную запись Azure Cosmos DB для API Graph (предварительная версия), базу данных и граф с использованием портала Azure.</span><span class="sxs-lookup"><span data-stu-id="7dd01-106">This quick-start article demonstrates how to create an Azure Cosmos DB account for Graph API (preview), database, and graph by using the Azure portal.</span></span> <span data-ttu-id="7dd01-107">Затем вы можете создать и запустить консольное приложение, используя драйвер [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="7dd01-107">You then build and run a console app by using the open-source [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) driver.</span></span>  

> [!NOTE]
> <span data-ttu-id="7dd01-108">Модуль npm `gremlin-secure` — это модифицированная версия модуля `gremlin` с поддержкой SSL и SASL, необходимой для подключения к Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7dd01-108">The npm module `gremlin-secure` is a modified version of `gremlin` module, with support for SSL and SASL required for connecting with Azure Cosmos DB.</span></span> <span data-ttu-id="7dd01-109">Исходный код доступен на сайте [GitHub](https://github.com/CosmosDB/gremlin-javascript).</span><span class="sxs-lookup"><span data-stu-id="7dd01-109">Source code is available on [GitHub](https://github.com/CosmosDB/gremlin-javascript).</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="7dd01-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7dd01-110">Prerequisites</span></span>

<span data-ttu-id="7dd01-111">Для выполнения этого примера вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="7dd01-111">Before you can run this sample, you must have the following prerequisites:</span></span>
* <span data-ttu-id="7dd01-112">[Node.js](https://nodejs.org/en/) v0.10.29 или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="7dd01-112">[Node.js](https://nodejs.org/en/) version v0.10.29 or later</span></span>
* [<span data-ttu-id="7dd01-113">Git.</span><span class="sxs-lookup"><span data-stu-id="7dd01-113">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="7dd01-114">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="7dd01-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="7dd01-115">Добавление графа</span><span class="sxs-lookup"><span data-stu-id="7dd01-115">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="7dd01-116">Клонирование примера приложения</span><span class="sxs-lookup"><span data-stu-id="7dd01-116">Clone the sample application</span></span>

<span data-ttu-id="7dd01-117">Теперь необходимо клонировать приложение API Graph из GitHub. Задайте строку подключения и выполните ее.</span><span class="sxs-lookup"><span data-stu-id="7dd01-117">Now let's clone a Graph API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="7dd01-118">Вы узнаете, как можно упростить работу с данными программным способом.</span><span class="sxs-lookup"><span data-stu-id="7dd01-118">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="7dd01-119">Откройте окно терминала Git (например, Git Bash) и перейдите в рабочий каталог, выполнив команду `cd`.</span><span class="sxs-lookup"><span data-stu-id="7dd01-119">Open a Git terminal window, such as Git Bash, and change (via `cd` command) to a working directory.</span></span>  

2. <span data-ttu-id="7dd01-120">Выполните команду ниже, чтобы клонировать репозиторий с примером.</span><span class="sxs-lookup"><span data-stu-id="7dd01-120">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-nodejs-getting-started.git
    ```

3. <span data-ttu-id="7dd01-121">Откройте файл решения в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7dd01-121">Open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="7dd01-122">Просмотр кода</span><span class="sxs-lookup"><span data-stu-id="7dd01-122">Review the code</span></span>

<span data-ttu-id="7dd01-123">Сделаем краткий обзор того, что происходит в приложении.</span><span class="sxs-lookup"><span data-stu-id="7dd01-123">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="7dd01-124">Откройте файл `app.js`, и вы увидите приведенные ниже строки кода.</span><span class="sxs-lookup"><span data-stu-id="7dd01-124">Open the `app.js` file, and you'll find the following lines of code.</span></span> 

* <span data-ttu-id="7dd01-125">Создание клиента Gremlin.</span><span class="sxs-lookup"><span data-stu-id="7dd01-125">The Gremlin client is created.</span></span>

    ```nodejs
    const client = Gremlin.createClient(
        443, 
        config.endpoint, 
        { 
            "session": false, 
            "ssl": true, 
            "user": `/dbs/${config.database}/colls/${config.collection}`,
            "password": config.primaryKey
        });
    ```

  <span data-ttu-id="7dd01-126">Все конфигурации находятся в файле `config.js`, который мы изменим в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="7dd01-126">The configurations are all in `config.js`, which we edit in the following section.</span></span>

* <span data-ttu-id="7dd01-127">Выполнение шагов Gremlin с использованием метода `client.execute`.</span><span class="sxs-lookup"><span data-stu-id="7dd01-127">A series of Gremlin steps are executed with the `client.execute` method.</span></span>

    ```nodejs
    console.log('Running Count'); 
    client.execute("g.V().count()", { }, (err, results) => {
        if (err) return console.error(err);
        console.log(JSON.stringify(results));
        console.log();
    });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="7dd01-128">Обновление строки подключения</span><span class="sxs-lookup"><span data-stu-id="7dd01-128">Update your connection string</span></span>

1. <span data-ttu-id="7dd01-129">Откройте файл config.js.</span><span class="sxs-lookup"><span data-stu-id="7dd01-129">Open the config.js file.</span></span> 

2. <span data-ttu-id="7dd01-130">В файле сonfig.js заполните значения ключа config.endpoint значением **Gremlin URI** со страницы **обзора** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7dd01-130">In config.js, fill in the config.endpoint key with the **Gremlin URI** value from the **Overview** page of the Azure portal.</span></span> 

    `config.endpoint = "GRAPHENDPOINT";`

    ![Просмотр и копирование ключа доступа на портале Azure, колонка "Ключи"](./media/create-graph-nodejs/gremlin-uri.png)

   <span data-ttu-id="7dd01-132">Если значение **Gremlin URI** не указано, можно создать значение на странице **Ключи** на портале с помощью значения **URI**, удалив https:// и изменив документы на графы.</span><span class="sxs-lookup"><span data-stu-id="7dd01-132">If the **Gremlin URI** value is blank, you can generate the value from the **Keys** page in the portal, using the **URI** value, removing https://, and changing documents to graphs.</span></span>

   <span data-ttu-id="7dd01-133">Конечная точка Gremlin должна состоять из имени узла без имени протокола или номера порта, например `mygraphdb.graphs.azure.com` (а не `https://mygraphdb.graphs.azure.com` или `mygraphdb.graphs.azure.com:433`).</span><span class="sxs-lookup"><span data-stu-id="7dd01-133">The Gremlin endpoint must be only the host name without the protocol/port number, like `mygraphdb.graphs.azure.com` (not `https://mygraphdb.graphs.azure.com` or `mygraphdb.graphs.azure.com:433`).</span></span>

3. <span data-ttu-id="7dd01-134">В файле config.js заполните значения параметра config.primaryKey значением **первичного ключа** на странице **Ключи** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7dd01-134">In config.js, fill in the config.primaryKey value in with the **Primary Key** value from the **Keys** page of the Azure portal.</span></span> 

    `config.primaryKey = "PRIMARYKEY";`

   ![Колонка "Ключи" на портале Azure](./media/create-graph-nodejs/keys.png)

4. <span data-ttu-id="7dd01-136">Введите имя базы данных и графа (контейнера) для значения config.database и config.collection.</span><span class="sxs-lookup"><span data-stu-id="7dd01-136">Enter the database name, and graph (container) name for the value of config.database and config.collection.</span></span> 

<span data-ttu-id="7dd01-137">Вот как должен выглядеть файл config.js:</span><span class="sxs-lookup"><span data-stu-id="7dd01-137">Here is an example of what your completed config.js file should look like:</span></span>

```nodejs
var config = {}

// Note that this must not have HTTPS or the port number
config.endpoint = "testgraphacct.graphs.azure.com";
config.primaryKey = "Pams6e7LEUS7LJ2Qk0fjZf3eGo65JdMWHmyn65i52w8ozPX2oxY3iP0yu05t9v1WymAHNcMwPIqNAEv3XDFsEg==";
config.database = "graphdb"
config.collection = "Persons"

module.exports = config;
```

## <a name="run-the-console-app"></a><span data-ttu-id="7dd01-138">Запуск консольного приложения</span><span class="sxs-lookup"><span data-stu-id="7dd01-138">Run the console app</span></span>

1. <span data-ttu-id="7dd01-139">Откройте окно терминала. С помощью команды `cd` перейдите в каталог установки файла package.json, включенного в проект.</span><span class="sxs-lookup"><span data-stu-id="7dd01-139">Open a terminal window and change (via `cd` command) to the installation directory for the package.json file that's included in the project.</span></span>  

2. <span data-ttu-id="7dd01-140">Запустите `npm install`, чтобы установить необходимые модули npm, включая `gremlin-secure`.</span><span class="sxs-lookup"><span data-stu-id="7dd01-140">Run `npm install` to install the required npm modules, including `gremlin-secure`.</span></span>

3. <span data-ttu-id="7dd01-141">Запустите `node app.js` в окне терминала, чтобы запустить приложение Node.</span><span class="sxs-lookup"><span data-stu-id="7dd01-141">Run `node app.js` in a terminal to start your node application.</span></span>

## <a name="browse-with-data-explorer"></a><span data-ttu-id="7dd01-142">Просмотр с помощью обозревателя данных</span><span class="sxs-lookup"><span data-stu-id="7dd01-142">Browse with Data Explorer</span></span>

<span data-ttu-id="7dd01-143">Теперь вернитесь в обозреватель данных на портале Azure. Здесь вы можете просматривать, запрашивать и изменять новые данные графа, а также работать с ними.</span><span class="sxs-lookup"><span data-stu-id="7dd01-143">You can now go back to Data Explorer in the Azure portal to view, query, modify, and work with your new graph data.</span></span>

<span data-ttu-id="7dd01-144">В обозревателе данных новая база данных отображается в области **Графы**.</span><span class="sxs-lookup"><span data-stu-id="7dd01-144">In Data Explorer, the new database appears in the **Graphs** pane.</span></span> <span data-ttu-id="7dd01-145">Разверните базу данных, а затем коллекцию и щелкните **График**.</span><span class="sxs-lookup"><span data-stu-id="7dd01-145">Expand the database, followed by the collection, then click **Graph**.</span></span>

<span data-ttu-id="7dd01-146">Данные, созданные в примере приложения, отображаются в следующей области в пределах вкладки **График** при щелчке **Применить фильтр**.</span><span class="sxs-lookup"><span data-stu-id="7dd01-146">The data generated by the sample app is displayed in the next pane within the **Graph** tab when you click **Apply Filter**.</span></span>

<span data-ttu-id="7dd01-147">Повторите выполнение `g.V()` с `.has('firstName', 'Thomas')` для тестирования фильтра.</span><span class="sxs-lookup"><span data-stu-id="7dd01-147">Try completing `g.V()` with `.has('firstName', 'Thomas')` to test the filter.</span></span> <span data-ttu-id="7dd01-148">Обратите внимание, что значение учитывает регистр.</span><span class="sxs-lookup"><span data-stu-id="7dd01-148">Do note that the value is case sensitive.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="7dd01-149">Просмотр соглашений об уровне обслуживания на портале Azure</span><span class="sxs-lookup"><span data-stu-id="7dd01-149">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-your-resources"></a><span data-ttu-id="7dd01-150">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="7dd01-150">Clean up your resources</span></span>

<span data-ttu-id="7dd01-151">Если вы не планируете использовать это приложение в дальнейшем, удалите все ресурсы, созданные в рамках работы с этой статьей, сделав следующее:</span><span class="sxs-lookup"><span data-stu-id="7dd01-151">If you do not plan to continue using this app, delete all resources that you created in this article by doing the following:</span></span> 

1. <span data-ttu-id="7dd01-152">На портале Azure в меню навигации слева щелкните **Группы ресурсов**, а затем выберите имя созданного ресурса.</span><span class="sxs-lookup"><span data-stu-id="7dd01-152">In the Azure portal, on the left navigation menu, click **Resource groups**, and then click the name of the resource that you created.</span></span> 
2. <span data-ttu-id="7dd01-153">На странице группы ресурсов щелкните **Удалить**, введите имя ресурса для удаления и щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="7dd01-153">On your resource group page, click **Delete**, type the name of the resource to be deleted, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7dd01-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7dd01-154">Next steps</span></span>

<span data-ttu-id="7dd01-155">Из этой статьи вы узнали, как создать учетную запись Azure Cosmos DB, как создать граф с помощью обозревателя данных, а также как запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="7dd01-155">In this article, you've learned how to create an Azure Cosmos DB account, create a graph by using Data Explorer, and run an app.</span></span> <span data-ttu-id="7dd01-156">Теперь вы можете создавать более сложные запросы и внедрять эффективную логику обхода графа с помощью Gremlin.</span><span class="sxs-lookup"><span data-stu-id="7dd01-156">You can now build more complex queries and implement powerful graph traversal logic by using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="7dd01-157">Как выполнять запросы к данным в базе данных Azure Cosmos DB с помощью API Graph (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="7dd01-157">Query using Gremlin</span></span>](tutorial-query-graph.md)
