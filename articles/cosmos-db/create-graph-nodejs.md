---
title: "aaaBuild приложения Azure Cosmos DB Node.js с помощью Graph API | Документы Microsoft"
description: "Содержит образец кода Node.js tooconnect tooand можно использовать запрос Azure Cosmos DB"
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
ms.openlocfilehash: 1445755842bc4e4a84ca2b2f789aadde8467e190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-nodejs-application-by-using-graph-api"></a><span data-ttu-id="fb5ce-103">Azure Cosmos DB. Создание приложения Node.js с помощью API Graph</span><span class="sxs-lookup"><span data-stu-id="fb5ce-103">Azure Cosmos DB: Build a Node.js application by using Graph API</span></span>

<span data-ttu-id="fb5ce-104">Azure Cosmos DB — глобально распределенных hello моделей базы данных службы от корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-104">Azure Cosmos DB is hello globally distributed multi-model database service from Microsoft.</span></span> <span data-ttu-id="fb5ce-105">Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="fb5ce-106">В этой статье краткого руководства показано, как toocreate Cosmos Azure DB записи для Graph API (Предварительная версия), базы данных и диаграммы с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-106">This quick-start article demonstrates how toocreate an Azure Cosmos DB account for Graph API (preview), database, and graph by using hello Azure portal.</span></span> <span data-ttu-id="fb5ce-107">Построить и запустить консольное приложение с открытым исходным кодом hello [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) драйвера.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-107">You then build and run a console app by using hello open-source [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) driver.</span></span>  

> [!NOTE]
> <span data-ttu-id="fb5ce-108">модуль Hello npm `gremlin-secure` является модификацией `gremlin` модуль с поддержкой SSL и необходимые для соединения с Azure Cosmos DB SASL.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-108">hello npm module `gremlin-secure` is a modified version of `gremlin` module, with support for SSL and SASL required for connecting with Azure Cosmos DB.</span></span> <span data-ttu-id="fb5ce-109">Исходный код доступен на сайте [GitHub](https://github.com/CosmosDB/gremlin-javascript).</span><span class="sxs-lookup"><span data-stu-id="fb5ce-109">Source code is available on [GitHub](https://github.com/CosmosDB/gremlin-javascript).</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="fb5ce-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fb5ce-110">Prerequisites</span></span>

<span data-ttu-id="fb5ce-111">Перед запуском этого образца необходимо иметь hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="fb5ce-111">Before you can run this sample, you must have hello following prerequisites:</span></span>
* <span data-ttu-id="fb5ce-112">[Node.js](https://nodejs.org/en/) v0.10.29 или более поздней версии;</span><span class="sxs-lookup"><span data-stu-id="fb5ce-112">[Node.js](https://nodejs.org/en/) version v0.10.29 or later</span></span>
* [<span data-ttu-id="fb5ce-113">Git.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-113">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="fb5ce-114">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="fb5ce-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="fb5ce-115">Добавление графа</span><span class="sxs-lookup"><span data-stu-id="fb5ce-115">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="fb5ce-116">Пример приложения hello клонирования</span><span class="sxs-lookup"><span data-stu-id="fb5ce-116">Clone hello sample application</span></span>

<span data-ttu-id="fb5ce-117">Теперь давайте клон Graph API приложение из GitHub, задайте строку подключения hello и запустите его.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-117">Now let's clone a Graph API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="fb5ce-118">Вы увидите, как просто можно toowork с данными программными средствами.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-118">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="fb5ce-119">Откройте окно терминала Git, например Git Bash и измените (через `cd` команда) tooa рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-119">Open a Git terminal window, such as Git Bash, and change (via `cd` command) tooa working directory.</span></span>  

2. <span data-ttu-id="fb5ce-120">Выполнения hello следующая команда репозитории примеров tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-120">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-nodejs-getting-started.git
    ```

3. <span data-ttu-id="fb5ce-121">Откройте файл решения hello в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-121">Open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="fb5ce-122">Проверка кода hello</span><span class="sxs-lookup"><span data-stu-id="fb5ce-122">Review hello code</span></span>

<span data-ttu-id="fb5ce-123">Убедитесь, что происходит в приложение hello быстро ознакомиться.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-123">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="fb5ce-124">Откройте hello `app.js` файл и вы найдете следующие строки кода hello.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-124">Open hello `app.js` file, and you'll find hello following lines of code.</span></span> 

* <span data-ttu-id="fb5ce-125">создается клиент Gremlin Hello.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-125">hello Gremlin client is created.</span></span>

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

  <span data-ttu-id="fb5ce-126">Hello конфигурации находятся в `config.js`, который мы изменения в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-126">hello configurations are all in `config.js`, which we edit in hello following section.</span></span>

* <span data-ttu-id="fb5ce-127">Последовательность шагов Gremlin выполняются с hello `client.execute` метод.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-127">A series of Gremlin steps are executed with hello `client.execute` method.</span></span>

    ```nodejs
    console.log('Running Count'); 
    client.execute("g.V().count()", { }, (err, results) => {
        if (err) return console.error(err);
        console.log(JSON.stringify(results));
        console.log();
    });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="fb5ce-128">Обновление строки подключения</span><span class="sxs-lookup"><span data-stu-id="fb5ce-128">Update your connection string</span></span>

1. <span data-ttu-id="fb5ce-129">Привет открыть файл config.js.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-129">Open hello config.js file.</span></span> 

2. <span data-ttu-id="fb5ce-130">Config.js, заполните в ключ config.endpoint hello с hello **Gremlin URI** значение из hello **Обзор** страница hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-130">In config.js, fill in hello config.endpoint key with hello **Gremlin URI** value from hello **Overview** page of hello Azure portal.</span></span> 

    `config.endpoint = "GRAPHENDPOINT";`

    ![Просмотреть и скопировать ключ доступа в hello портал Azure, ключи колонку](./media/create-graph-nodejs/gremlin-uri.png)

   <span data-ttu-id="fb5ce-132">Если hello **Gremlin URI** имеет пустое значение, можно создать значение hello из hello **ключей** hello портала с помощью hello **URI** значение https:// удаление и изменение toographs документы.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-132">If hello **Gremlin URI** value is blank, you can generate hello value from hello **Keys** page in hello portal, using hello **URI** value, removing https://, and changing documents toographs.</span></span>

   <span data-ttu-id="fb5ce-133">Конечная точка Gremlin Hello должна быть только имя узла hello без номера протокола и порта hello, таких как `mygraphdb.graphs.azure.com` (не `https://mygraphdb.graphs.azure.com` или `mygraphdb.graphs.azure.com:433`).</span><span class="sxs-lookup"><span data-stu-id="fb5ce-133">hello Gremlin endpoint must be only hello host name without hello protocol/port number, like `mygraphdb.graphs.azure.com` (not `https://mygraphdb.graphs.azure.com` or `mygraphdb.graphs.azure.com:433`).</span></span>

3. <span data-ttu-id="fb5ce-134">В config.js, заполните значения config.primaryKey hello вход с помощью hello **первичного ключа** значение из hello **ключей** страница hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-134">In config.js, fill in hello config.primaryKey value in with hello **Primary Key** value from hello **Keys** page of hello Azure portal.</span></span> 

    `config.primaryKey = "PRIMARYKEY";`

   ![Hello Azure портала колонке ключей](./media/create-graph-nodejs/keys.png)

4. <span data-ttu-id="fb5ce-136">Введите имя базы данных hello и имя диаграммы (контейнер) для значения hello config.database и config.collection.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-136">Enter hello database name, and graph (container) name for hello value of config.database and config.collection.</span></span> 

<span data-ttu-id="fb5ce-137">Вот как должен выглядеть файл config.js:</span><span class="sxs-lookup"><span data-stu-id="fb5ce-137">Here is an example of what your completed config.js file should look like:</span></span>

```nodejs
var config = {}

// Note that this must not have HTTPS or hello port number
config.endpoint = "testgraphacct.graphs.azure.com";
config.primaryKey = "Pams6e7LEUS7LJ2Qk0fjZf3eGo65JdMWHmyn65i52w8ozPX2oxY3iP0yu05t9v1WymAHNcMwPIqNAEv3XDFsEg==";
config.database = "graphdb"
config.collection = "Persons"

module.exports = config;
```

## <a name="run-hello-console-app"></a><span data-ttu-id="fb5ce-138">Запустите консольное приложение hello</span><span class="sxs-lookup"><span data-stu-id="fb5ce-138">Run hello console app</span></span>

1. <span data-ttu-id="fb5ce-139">Откройте окно терминала и измените (через `cd` команда) toohello каталог установки для файла package.json hello, включенный в проект hello.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-139">Open a terminal window and change (via `cd` command) toohello installation directory for hello package.json file that's included in hello project.</span></span>  

2. <span data-ttu-id="fb5ce-140">Запустите `npm install` tooinstall hello необходимые модули npm, включая `gremlin-secure`.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-140">Run `npm install` tooinstall hello required npm modules, including `gremlin-secure`.</span></span>

3. <span data-ttu-id="fb5ce-141">Запустите `node app.js` в терминалов toostart узла приложения.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-141">Run `node app.js` in a terminal toostart your node application.</span></span>

## <a name="browse-with-data-explorer"></a><span data-ttu-id="fb5ce-142">Просмотр с помощью обозревателя данных</span><span class="sxs-lookup"><span data-stu-id="fb5ce-142">Browse with Data Explorer</span></span>

<span data-ttu-id="fb5ce-143">Теперь можно вернуться tooData обозревателя в hello Azure tooview портала, запрос, изменить и работы с данными новый график.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-143">You can now go back tooData Explorer in hello Azure portal tooview, query, modify, and work with your new graph data.</span></span>

<span data-ttu-id="fb5ce-144">В обозревателе данных hello новой базы данных отображается в hello **графы** области.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-144">In Data Explorer, hello new database appears in hello **Graphs** pane.</span></span> <span data-ttu-id="fb5ce-145">Hello базы данных, а затем с помощью коллекции hello, а затем выберите пункт **Graph**.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-145">Expand hello database, followed by hello collection, then click **Graph**.</span></span>

<span data-ttu-id="fb5ce-146">созданные hello пример приложения Hello данные отображаются в области далее hello в hello **Graph** вкладке при нажатии кнопки **применить фильтр**.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-146">hello data generated by hello sample app is displayed in hello next pane within hello **Graph** tab when you click **Apply Filter**.</span></span>

<span data-ttu-id="fb5ce-147">Повторите выполнение `g.V()` с `.has('firstName', 'Thomas')` tootest hello фильтра.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-147">Try completing `g.V()` with `.has('firstName', 'Thomas')` tootest hello filter.</span></span> <span data-ttu-id="fb5ce-148">Обратите внимание, что значение hello с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-148">Do note that hello value is case sensitive.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="fb5ce-149">Просмотрите соглашений об уровне обслуживания в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="fb5ce-149">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-your-resources"></a><span data-ttu-id="fb5ce-150">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="fb5ce-150">Clean up your resources</span></span>

<span data-ttu-id="fb5ce-151">Если вы не планируете использовать это приложение toocontinue, удалите все ресурсы, созданные в этой статье, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="fb5ce-151">If you do not plan toocontinue using this app, delete all resources that you created in this article by doing hello following:</span></span> 

1. <span data-ttu-id="fb5ce-152">В hello портал Azure, в меню навигации слева hello, щелкните **групп ресурсов**и щелкните имя hello hello ресурса, который был создан.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-152">In hello Azure portal, on hello left navigation menu, click **Resource groups**, and then click hello name of hello resource that you created.</span></span> 
2. <span data-ttu-id="fb5ce-153">На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toobe ресурсов hello удален и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-153">On your resource group page, click **Delete**, type hello name of hello resource toobe deleted, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb5ce-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fb5ce-154">Next steps</span></span>

<span data-ttu-id="fb5ce-155">В этой статье вы узнали, как создать граф, с помощью данных обозревателя toocreate учетную запись Azure Cosmos DB и запуск приложения.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-155">In this article, you've learned how toocreate an Azure Cosmos DB account, create a graph by using Data Explorer, and run an app.</span></span> <span data-ttu-id="fb5ce-156">Теперь вы можете создавать более сложные запросы и внедрять эффективную логику обхода графа с помощью Gremlin.</span><span class="sxs-lookup"><span data-stu-id="fb5ce-156">You can now build more complex queries and implement powerful graph traversal logic by using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="fb5ce-157">Как выполнять запросы к данным в базе данных Azure Cosmos DB с помощью API Graph (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="fb5ce-157">Query using Gremlin</span></span>](tutorial-query-graph.md)
