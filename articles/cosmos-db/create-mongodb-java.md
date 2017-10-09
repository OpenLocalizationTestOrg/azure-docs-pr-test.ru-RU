---
title: "Azure Cosmos DB: Построение консольного приложения с помощью Java и hello MongoDB API | Документы Microsoft"
description: "Содержит пример кода Java, можно использовать запрос tooand tooconnect hello Azure Cosmos базы данных MongoDB API"
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
ms.devlang: java
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fbe416f6b20ed2bb83a1d41eb70ffc6e3cee2b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-hello-azure-portal"></a><span data-ttu-id="3a451-103">Azure Cosmos DB: Построение MongoDB API консольного приложения с использованием Java и hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="3a451-103">Azure Cosmos DB: Build a MongoDB API console app with Java and hello Azure portal</span></span>

<span data-ttu-id="3a451-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3a451-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="3a451-105">Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД.</span><span class="sxs-lookup"><span data-stu-id="3a451-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="3a451-106">В этом кратком руководстве показано, как toocreate учетную запись Azure Cosmos DB документа базы данных и коллекцию с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3a451-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="3a451-107">Вы будете затем постройте и разверните консольного приложения, построенные на hello [драйвер MongoDB Java](https://docs.mongodb.com/ecosystem/drivers/java/).</span><span class="sxs-lookup"><span data-stu-id="3a451-107">You'll then build and deploy a console app built on hello [MongoDB Java driver](https://docs.mongodb.com/ecosystem/drivers/java/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3a451-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3a451-108">Prerequisites</span></span>

* <span data-ttu-id="3a451-109">Перед запуском этого образца необходимо иметь hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="3a451-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
   * <span data-ttu-id="3a451-110">JDK 1.7+ (если у вас нет JDK, выполните `apt-get install default-jdk`);</span><span class="sxs-lookup"><span data-stu-id="3a451-110">JDK 1.7+ (Run `apt-get install default-jdk` if you don't have JDK)</span></span>
   * <span data-ttu-id="3a451-111">Maven (если у вас нет Maven, выполните `apt-get install maven`).</span><span class="sxs-lookup"><span data-stu-id="3a451-111">Maven (Run `apt-get install maven` if you don't have Maven)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="3a451-112">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="3a451-112">Create a database account</span></span>

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a><span data-ttu-id="3a451-113">Добавление коллекции</span><span class="sxs-lookup"><span data-stu-id="3a451-113">Add a collection</span></span>

<span data-ttu-id="3a451-114">Присвойте новой базе данных имя **db**, а новой коллекции — **coll**.</span><span class="sxs-lookup"><span data-stu-id="3a451-114">Name your new database, **db**, and your new collection, **coll**.</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="3a451-115">Пример приложения hello клонирования</span><span class="sxs-lookup"><span data-stu-id="3a451-115">Clone hello sample application</span></span>

<span data-ttu-id="3a451-116">Теперь давайте клонирование MongoDB API приложений из github, задайте строку подключения hello и запустите его.</span><span class="sxs-lookup"><span data-stu-id="3a451-116">Now let's clone a MongoDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="3a451-117">Вы увидите, как просто можно toowork с данными программными средствами.</span><span class="sxs-lookup"><span data-stu-id="3a451-117">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="3a451-118">Откройте окно терминала git, таких как git bash и `cd` tooa рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="3a451-118">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="3a451-119">Выполнения hello следующая команда репозитории примеров tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="3a451-119">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. <span data-ttu-id="3a451-120">Затем откройте файл решения hello в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3a451-120">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="3a451-121">Проверка кода hello</span><span class="sxs-lookup"><span data-stu-id="3a451-121">Review hello code</span></span>

<span data-ttu-id="3a451-122">Убедитесь, что происходит в приложение hello быстро ознакомиться.</span><span class="sxs-lookup"><span data-stu-id="3a451-122">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="3a451-123">Откройте hello `Program.cs` файл и вы найдете следующие строки кода создать hello Azure Cosmos DB ресурсы.</span><span class="sxs-lookup"><span data-stu-id="3a451-123">Open hello `Program.cs` file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="3a451-124">Hello DocumentClient инициализируется.</span><span class="sxs-lookup"><span data-stu-id="3a451-124">hello DocumentClient is initialized.</span></span>

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* <span data-ttu-id="3a451-125">Создание базы данных и коллекции.</span><span class="sxs-lookup"><span data-stu-id="3a451-125">A new database and collection are created.</span></span>

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* <span data-ttu-id="3a451-126">Вставка документов с использованием `MongoCollection.insertOne`.</span><span class="sxs-lookup"><span data-stu-id="3a451-126">Some documents are inserted using `MongoCollection.insertOne`</span></span>

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* <span data-ttu-id="3a451-127">Выполнение запросов с использованием `MongoCollection.find`.</span><span class="sxs-lookup"><span data-stu-id="3a451-127">Some queries are performed using `MongoCollection.find`</span></span>

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="3a451-128">Обновление строки подключения</span><span class="sxs-lookup"><span data-stu-id="3a451-128">Update your connection string</span></span>

<span data-ttu-id="3a451-129">Теперь вернитесь toohello Azure портала tooget данные строки подключения и скопируйте его в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="3a451-129">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="3a451-130">Hello учетной записи, выберите **быстрый запуск**выберите Java, а затем скопируйте hello строка подключения tooyour, буфер обмена</span><span class="sxs-lookup"><span data-stu-id="3a451-130">From hello Account, select **Quick Start**, select Java, then copy hello connection string tooyour clipboard</span></span>

2. <span data-ttu-id="3a451-131">Откройте hello `Program.java` файла, замените конструктор MongoClientURI toohello аргументом hello hello строкой подключения.</span><span class="sxs-lookup"><span data-stu-id="3a451-131">Open hello `Program.java` file, replace hello argument toohello MongoClientURI constructor with hello connection string.</span></span> <span data-ttu-id="3a451-132">Теперь вы обновили приложения с все hello сведения учетной записи, он должен toocommunicate с Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3a451-132">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-console-app"></a><span data-ttu-id="3a451-133">Запустите консольное приложение hello</span><span class="sxs-lookup"><span data-stu-id="3a451-133">Run hello console app</span></span>

1. <span data-ttu-id="3a451-134">Запустите `mvn package` в терминалов tooinstall необходимые модули npm</span><span class="sxs-lookup"><span data-stu-id="3a451-134">Run `mvn package` in a terminal tooinstall required npm modules</span></span>

2. <span data-ttu-id="3a451-135">Запустите `mvn exec:java -D exec.mainClass=GetStarted.Program` в терминалов toostart работу приложений Java.</span><span class="sxs-lookup"><span data-stu-id="3a451-135">Run `mvn exec:java -D exec.mainClass=GetStarted.Program` in a terminal toostart your Java application.</span></span>

<span data-ttu-id="3a451-136">Теперь вы можете использовать [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery, изменения и работать с новые данные.</span><span class="sxs-lookup"><span data-stu-id="3a451-136">You can now use [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery, modify, and work with this new data.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="3a451-137">Просмотрите соглашений об уровне обслуживания в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="3a451-137">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="3a451-138">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="3a451-138">Clean up resources</span></span>

<span data-ttu-id="3a451-139">Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="3a451-139">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="3a451-140">Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="3a451-140">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="3a451-141">На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="3a451-141">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a451-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3a451-142">Next steps</span></span>

<span data-ttu-id="3a451-143">В этом кратком руководстве вы узнали, как создать коллекцию с помощью hello обозреватель данных toocreate учетную запись Azure Cosmos DB, и запустите консольное приложение.</span><span class="sxs-lookup"><span data-stu-id="3a451-143">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run a console app.</span></span> <span data-ttu-id="3a451-144">Теперь можно импортировать учетной записи Cosmos DB tooyour дополнительные данные.</span><span class="sxs-lookup"><span data-stu-id="3a451-144">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="3a451-145">Перенос данных в DocumentDB с помощью mongoimport и mongorestore</span><span class="sxs-lookup"><span data-stu-id="3a451-145">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)


