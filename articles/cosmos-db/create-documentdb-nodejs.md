---
title: "Azure Cosmos DB: Сборка приложения с помощью Node.js и hello DocumentDB API | Документы Microsoft"
description: "Представляет запрос tooand tooconnect можно использовать образец кода Node.js hello Azure Cosmos DB DocumentDB API"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 9c0f033c-240e-4fee-8421-08907231087f
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 287d860c7d6f788f05a397b238ef0f841c3c30ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-hello-azure-portal"></a><span data-ttu-id="fddb7-103">Azure Cosmos DB: Создать приложение DocumentDB API с Node.js и hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="fddb7-103">Azure Cosmos DB: Build a DocumentDB API app with Node.js and hello Azure portal</span></span>

<span data-ttu-id="fddb7-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="fddb7-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="fddb7-105">Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД.</span><span class="sxs-lookup"><span data-stu-id="fddb7-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="fddb7-106">В этом кратком руководстве показано, как toocreate учетную запись Azure Cosmos DB документа базы данных и коллекцию с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="fddb7-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="fddb7-107">Затем постройте и запустите консольное приложение, построенных на hello [DocumentDB Node.js API](documentdb-sdk-node.md).</span><span class="sxs-lookup"><span data-stu-id="fddb7-107">You then build and run a console app built on hello [DocumentDB Node.js API](documentdb-sdk-node.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fddb7-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fddb7-108">Prerequisites</span></span>

* <span data-ttu-id="fddb7-109">Перед запуском этого образца необходимо иметь hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="fddb7-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
    * <span data-ttu-id="fddb7-110">[Node.js](https://nodejs.org/en/) версии 0.10.29 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="fddb7-110">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span></span>
    * [<span data-ttu-id="fddb7-111">Git.</span><span class="sxs-lookup"><span data-stu-id="fddb7-111">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="fddb7-112">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="fddb7-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="fddb7-113">Добавление коллекции</span><span class="sxs-lookup"><span data-stu-id="fddb7-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="fddb7-114">Пример приложения hello клонирования</span><span class="sxs-lookup"><span data-stu-id="fddb7-114">Clone hello sample application</span></span>

<span data-ttu-id="fddb7-115">Теперь давайте клонирование DocumentDB API приложений из github, задайте строку подключения hello и запустите его.</span><span class="sxs-lookup"><span data-stu-id="fddb7-115">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="fddb7-116">Вы видите, как просто можно toowork с данными программными средствами.</span><span class="sxs-lookup"><span data-stu-id="fddb7-116">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="fddb7-117">Откройте окно терминала git, таких как git bash и `CD` tooa рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="fddb7-117">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="fddb7-118">Выполнения hello следующая команда репозитории примеров tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="fddb7-118">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="fddb7-119">Проверка кода hello</span><span class="sxs-lookup"><span data-stu-id="fddb7-119">Review hello code</span></span>

<span data-ttu-id="fddb7-120">Убедитесь, что происходит в приложение hello быстро ознакомиться.</span><span class="sxs-lookup"><span data-stu-id="fddb7-120">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="fddb7-121">Откройте hello `app.js` файл а можно найти следующие строки кода создать hello Azure Cosmos DB ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fddb7-121">Open hello `app.js` file and you find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="fddb7-122">Hello `documentClient` инициализируется.</span><span class="sxs-lookup"><span data-stu-id="fddb7-122">hello `documentClient` is initialized.</span></span>

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* <span data-ttu-id="fddb7-123">Создание базы данных.</span><span class="sxs-lookup"><span data-stu-id="fddb7-123">A new database is created.</span></span>

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="fddb7-124">Создание коллекции.</span><span class="sxs-lookup"><span data-stu-id="fddb7-124">A new collection is created.</span></span>

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="fddb7-125">Создание нескольких документов.</span><span class="sxs-lookup"><span data-stu-id="fddb7-125">Some documents are created.</span></span>

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="fddb7-126">Выполнение запроса SQL через JSON.</span><span class="sxs-lookup"><span data-stu-id="fddb7-126">A SQL query over JSON is performed.</span></span>

    ```nodejs
    client.queryDocuments(
        collectionUrl,
        'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
    ).toArray((err, results) => {
        if (err) reject(err)
        else {
            for (var queryResult of results) {
                let resultString = JSON.stringify(queryResult);
                console.log(`\tQuery returned ${resultString}`);
            }
            console.log();
            resolve(results);
        }
    });
    ```    

## <a name="update-your-connection-string"></a><span data-ttu-id="fddb7-127">Обновление строки подключения</span><span class="sxs-lookup"><span data-stu-id="fddb7-127">Update your connection string</span></span>

<span data-ttu-id="fddb7-128">Теперь вернитесь toohello Azure портала tooget данные строки подключения и скопируйте его в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="fddb7-128">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="fddb7-129">В hello [портал Azure](http://portal.azure.com/), в вашей Azure Cosmos DB учетной записи, в hello навигации слева щелкните **ключей**и нажмите кнопку **чтения и записи ключей**.</span><span class="sxs-lookup"><span data-stu-id="fddb7-129">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="fddb7-130">Кнопки копирования hello будет использоваться на правой стороне hello hello toocopy экрана приветствия URI и первичный ключ в hello `config.js` файла в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="fddb7-130">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello `config.js` file in hello next step.</span></span>

    ![Просмотреть и скопировать ключ доступа в hello портал Azure, ключи колонку](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="fddb7-132">В открытых hello `config.js` файла.</span><span class="sxs-lookup"><span data-stu-id="fddb7-132">In Open hello `config.js` file.</span></span> 

3. <span data-ttu-id="fddb7-133">Скопируйте значение URI с портала hello (с использованием "Копировать" hello ") и сделать его hello значение ключа hello конечной точки в `config.js`.</span><span class="sxs-lookup"><span data-stu-id="fddb7-133">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in `config.js`.</span></span> 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="fddb7-134">Затем скопируйте значение ПЕРВИЧНОГО ключа из портала hello и сделать его значение hello hello `config.primaryKey` в `config.js`.</span><span class="sxs-lookup"><span data-stu-id="fddb7-134">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello `config.primaryKey` in `config.js`.</span></span> <span data-ttu-id="fddb7-135">Теперь вы обновили приложения с все hello сведения учетной записи, он должен toocommunicate с Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fddb7-135">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `config.primaryKey "FILLME"`
    
## <a name="run-hello-app"></a><span data-ttu-id="fddb7-136">Выполните приложение hello</span><span class="sxs-lookup"><span data-stu-id="fddb7-136">Run hello app</span></span>
1. <span data-ttu-id="fddb7-137">Запустите `npm install` в терминалов tooinstall необходимые модули npm</span><span class="sxs-lookup"><span data-stu-id="fddb7-137">Run `npm install` in a terminal tooinstall required npm modules</span></span>

2. <span data-ttu-id="fddb7-138">Запустите `node app.js` в терминалов toostart узла приложения.</span><span class="sxs-lookup"><span data-stu-id="fddb7-138">Run `node app.js` in a terminal toostart your node application.</span></span>

<span data-ttu-id="fddb7-139">Теперь можно вернуться tooData обозревателя и запроса в разделе, изменения и работать с новые данные.</span><span class="sxs-lookup"><span data-stu-id="fddb7-139">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="fddb7-140">Просмотрите соглашений об уровне обслуживания в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="fddb7-140">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="fddb7-141">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="fddb7-141">Clean up resources</span></span>

<span data-ttu-id="fddb7-142">Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="fddb7-142">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="fddb7-143">Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="fddb7-143">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="fddb7-144">На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="fddb7-144">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fddb7-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fddb7-145">Next steps</span></span>

<span data-ttu-id="fddb7-146">В этом кратком руководстве вы узнали, как создать коллекцию с помощью hello обозреватель данных toocreate учетную запись Azure Cosmos DB и запуск приложения.</span><span class="sxs-lookup"><span data-stu-id="fddb7-146">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="fddb7-147">Теперь можно импортировать учетной записи Cosmos DB tooyour дополнительные данные.</span><span class="sxs-lookup"><span data-stu-id="fddb7-147">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="fddb7-148">Импорт данных в DocumentDB с помощью средства миграции базы данных</span><span class="sxs-lookup"><span data-stu-id="fddb7-148">Import data into Azure Cosmos DB</span></span>](import-data.md)


