---
title: "Руководство по NoSQL. Пакет SDK для создания приложения Java с помощью API-интерфейса DocumentDB для Azure Cosmos DB | Документация Майкрософт"
description: "Учебник NoSQL, создает консольное приложение Java с помощью hello DocumentDB API для Azure Cosmos DB и базы данных в сети. Azure DocumentDB — это база данных NoSQL для JSON."
keywords: "руководство nosql, оперативная база данных, консольное приложение java"
services: cosmos-db
documentationcenter: Java
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 75a9efa1-7edd-4fed-9882-c0177274cbb2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 05/22/2017
ms.author: arramac
ms.openlocfilehash: 1a298a15ab911d140b9df30ad52cfe0fa07c55b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a><span data-ttu-id="7372e-105">Руководство по NoSQL. Создание консольного приложения Java с помощью API-интерфейса DocumentDB</span><span class="sxs-lookup"><span data-stu-id="7372e-105">NoSQL tutorial: Build a DocumentDB API Java console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7372e-106">.NET</span><span class="sxs-lookup"><span data-stu-id="7372e-106">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="7372e-107">.NET Core</span><span class="sxs-lookup"><span data-stu-id="7372e-107">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="7372e-108">Node.js для MongoDB</span><span class="sxs-lookup"><span data-stu-id="7372e-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="7372e-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="7372e-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="7372e-110">Java</span><span class="sxs-lookup"><span data-stu-id="7372e-110">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="7372e-111">C++</span><span class="sxs-lookup"><span data-stu-id="7372e-111">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="7372e-112">Вас приветствует toohello NoSQL учебник по API DocumentDB для пакета SDK для Java Azure Cosmos DB hello!</span><span class="sxs-lookup"><span data-stu-id="7372e-112">Welcome toohello NoSQL tutorial for hello DocumentDB API for Azure Cosmos DB Java SDK!</span></span> <span data-ttu-id="7372e-113">После изучения этого руководства у вас будет консольное приложение, которое создает ресурсы Azure Cosmos DB и отправляет запросы к ним.</span><span class="sxs-lookup"><span data-stu-id="7372e-113">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="7372e-114">Мы рассмотрим:</span><span class="sxs-lookup"><span data-stu-id="7372e-114">We cover:</span></span>

* <span data-ttu-id="7372e-115">Создание и подключение учетной записи Azure Cosmos DB tooan</span><span class="sxs-lookup"><span data-stu-id="7372e-115">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="7372e-116">настройка решения Visual Studio;</span><span class="sxs-lookup"><span data-stu-id="7372e-116">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="7372e-117">Создание оперативной базы данных</span><span class="sxs-lookup"><span data-stu-id="7372e-117">Creating an online database</span></span>
* <span data-ttu-id="7372e-118">создание коллекции;</span><span class="sxs-lookup"><span data-stu-id="7372e-118">Creating a collection</span></span>
* <span data-ttu-id="7372e-119">создание документов JSON;</span><span class="sxs-lookup"><span data-stu-id="7372e-119">Creating JSON documents</span></span>
* <span data-ttu-id="7372e-120">Запрос к коллекции hello</span><span class="sxs-lookup"><span data-stu-id="7372e-120">Querying hello collection</span></span>
* <span data-ttu-id="7372e-121">создание документов JSON;</span><span class="sxs-lookup"><span data-stu-id="7372e-121">Creating JSON documents</span></span>
* <span data-ttu-id="7372e-122">Запрос к коллекции hello</span><span class="sxs-lookup"><span data-stu-id="7372e-122">Querying hello collection</span></span>
* <span data-ttu-id="7372e-123">замена документа;</span><span class="sxs-lookup"><span data-stu-id="7372e-123">Replacing a document</span></span>
* <span data-ttu-id="7372e-124">удаление документа;</span><span class="sxs-lookup"><span data-stu-id="7372e-124">Deleting a document</span></span>
* <span data-ttu-id="7372e-125">Удаление базы данных hello</span><span class="sxs-lookup"><span data-stu-id="7372e-125">Deleting hello database</span></span>

<span data-ttu-id="7372e-126">А теперь приступим к работе!</span><span class="sxs-lookup"><span data-stu-id="7372e-126">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7372e-127">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7372e-127">Prerequisites</span></span>
<span data-ttu-id="7372e-128">Убедитесь, что у вас есть следующие hello:</span><span class="sxs-lookup"><span data-stu-id="7372e-128">Make sure you have hello following:</span></span>

* <span data-ttu-id="7372e-129">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="7372e-129">An active Azure account.</span></span> <span data-ttu-id="7372e-130">Если у вас ее нет, зарегистрируйте [бесплатную учетную запись](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="7372e-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="7372e-131">Кроме того, можно использовать hello [DB эмулятор Azure Cosmos](local-emulator.md) для этого учебника.</span><span class="sxs-lookup"><span data-stu-id="7372e-131">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="7372e-132">Git.</span><span class="sxs-lookup"><span data-stu-id="7372e-132">Git</span></span>](https://git-scm.com/downloads)
* <span data-ttu-id="7372e-133">[Комплект разработчика Java (JDK 7 +)](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="7372e-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="7372e-134">[Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="7372e-134">[Maven](http://maven.apache.org/download.cgi).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="7372e-135">Шаг 1. Создание учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7372e-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="7372e-136">Давайте создадим учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7372e-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="7372e-137">При наличии учетной записи требуется toouse можно сразу перейти слишком[клон hello GitHub проекта](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="7372e-137">If you already have an account you want toouse, you can skip ahead too[Clone hello GitHub project](#GitClone).</span></span> <span data-ttu-id="7372e-138">При использовании hello Azure Cosmos DB эмулятор, выполните действия hello в [DB эмулятор Azure Cosmos](local-emulator.md) tooset Настройка эмулятора hello и пропускать слишком[клон hello GitHub проекта](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="7372e-138">If you are using hello Azure Cosmos DB Emulator, follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) tooset up hello emulator and skip ahead too[Clone hello GitHub project](#GitClone).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="7372e-139"><a id="GitClone"></a>Шаг 2: Клонирование hello GitHub проекта</span><span class="sxs-lookup"><span data-stu-id="7372e-139"><a id="GitClone"></a>Step 2: Clone hello GitHub project</span></span>
<span data-ttu-id="7372e-140">Вы можете начать клонированием репозитория GitHub hello для [Приступая к работе с Azure Cosmos DB и Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="7372e-140">You can get started by cloning hello GitHub repository for [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span></span> <span data-ttu-id="7372e-141">Например из локального каталога выполните следующие tooretrieve hello образец проекта локально hello.</span><span class="sxs-lookup"><span data-stu-id="7372e-141">For example, from a local directory run hello following tooretrieve hello sample project locally.</span></span>

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

<span data-ttu-id="7372e-142">каталог Hello содержит `pom.xml` для проекта hello и `src` папку, содержащую Java исходного кода включая `Program.java` котором показывается, как выполнять простые операции с Azure DB Cosmos, таких как создание документов и запроса данных в Коллекция.</span><span class="sxs-lookup"><span data-stu-id="7372e-142">hello directory contains a `pom.xml` for hello project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure Cosmos DB like creating documents and querying data within a collection.</span></span> <span data-ttu-id="7372e-143">Hello `pom.xml` включает зависимость от hello [DocumentDB Java SDK на Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span><span class="sxs-lookup"><span data-stu-id="7372e-143">hello `pom.xml` includes a dependency on hello [DocumentDB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span></span>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <span data-ttu-id="7372e-144"><a id="Connect"></a>Шаг 3: Учетная запись Azure Cosmos DB tooan подключения</span><span class="sxs-lookup"><span data-stu-id="7372e-144"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="7372e-145">Далее head резервное toohello [портала Azure](https://portal.azure.com) tooretrieve конечной точки и основного главного ключа.</span><span class="sxs-lookup"><span data-stu-id="7372e-145">Next, head back toohello [Azure Portal](https://portal.azure.com) tooretrieve your endpoint and primary master key.</span></span> <span data-ttu-id="7372e-146">Hello Azure Cosmos DB конечной точки и первичный ключ необходимы для вашего приложения toounderstand где tooconnect, а для Azure Cosmos DB tootrust подключения вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="7372e-146">hello Azure Cosmos DB endpoint and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="7372e-147">В hello портал Azure, перейдите учетная запись Azure Cosmos DB tooyour и нажмите кнопку **ключей**.</span><span class="sxs-lookup"><span data-stu-id="7372e-147">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span> <span data-ttu-id="7372e-148">Скопируйте hello URI с портала hello и вставьте его в `https://FILLME.documents.azure.com` в файле Program.java hello.</span><span class="sxs-lookup"><span data-stu-id="7372e-148">Copy hello URI from hello portal and paste it into `https://FILLME.documents.azure.com` in hello Program.java file.</span></span> <span data-ttu-id="7372e-149">Затем копировать hello первичный ключ с портала hello и вставьте его в `FILLME`.</span><span class="sxs-lookup"><span data-stu-id="7372e-149">Then copy hello PRIMARY KEY from hello portal and paste it into `FILLME`.</span></span>

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Снимок экрана: hello hello NoSQL учебника toocreate консольное приложение Java портал Azure.][keys]

## <a name="step-4-create-a-database"></a><span data-ttu-id="7372e-152">Этап 4: создание базы данных</span><span class="sxs-lookup"><span data-stu-id="7372e-152">Step 4: Create a database</span></span>
<span data-ttu-id="7372e-153">Базы данных Azure Cosmos [базы данных](documentdb-resources.md#databases) могут быть созданы с помощью hello [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) метод hello **DocumentClient** класса.</span><span class="sxs-lookup"><span data-stu-id="7372e-153">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="7372e-154">База данных находится hello логический контейнер для хранения документов JSON, секционированный по коллекциям.</span><span class="sxs-lookup"><span data-stu-id="7372e-154">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <span data-ttu-id="7372e-155"><a id="CreateColl"></a>Этап 5: создание коллекции</span><span class="sxs-lookup"><span data-stu-id="7372e-155"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="7372e-156">Элемент **createCollection** создает коллекцию с зарезервированной пропускной способностью и соответствующей ценой.</span><span class="sxs-lookup"><span data-stu-id="7372e-156">**createCollection** creates a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="7372e-157">Дополнительные сведения см. на [странице цен](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="7372e-157">For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="7372e-158">Объект [коллекции](documentdb-resources.md#collections) могут быть созданы с помощью hello [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) метод hello **DocumentClient** класса.</span><span class="sxs-lookup"><span data-stu-id="7372e-158">A [collection](documentdb-resources.md#collections) can be created by using hello [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="7372e-159">Коллекция представляет собой контейнер документов JSON и связанную с ними логику в виде приложения JavaScript.</span><span class="sxs-lookup"><span data-stu-id="7372e-159">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <span data-ttu-id="7372e-160"><a id="CreateDoc"></a>Шаг 6. Создание документов JSON</span><span class="sxs-lookup"><span data-stu-id="7372e-160"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="7372e-161">Объект [документа](documentdb-resources.md#documents) могут быть созданы с помощью hello [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) метод hello **DocumentClient** класса.</span><span class="sxs-lookup"><span data-stu-id="7372e-161">A [document](documentdb-resources.md#documents) can be created by using hello [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="7372e-162">Документы относятся к пользовательскому (произвольному) содержимому JSON.</span><span class="sxs-lookup"><span data-stu-id="7372e-162">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="7372e-163">Теперь мы можем добавить один или несколько документов.</span><span class="sxs-lookup"><span data-stu-id="7372e-163">We can now insert one or more documents.</span></span> <span data-ttu-id="7372e-164">При наличии данных, отсылаемых toostore в базе данных можно использовать базу данных Cosmos Azure [средство переноса данных](import-data.md) tooimport hello данных в базу данных.</span><span class="sxs-lookup"><span data-stu-id="7372e-164">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) tooimport hello data into a database.</span></span>

    // Insert your Java objects as documents 
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen")

    // More initialization skipped for brevity. You can have nested references
    andersenFamily.setParents(new Parent[] { parent1, parent2 });
    andersenFamily.setDistrict("WA5");
    Address address = new Address();
    address.setCity("Seattle");
    address.setCounty("King");
    address.setState("WA");

    andersenFamily.setAddress(address);
    andersenFamily.setRegistered(true);

    this.client.createDocument("/dbs/familydb/colls/familycoll", family, new RequestOptions(), true);

![Схема, иллюстрирующая hello иерархическую связь между hello учетной записи, hello оперативную базу данных, коллекции hello и hello документов, созданных hello NoSQL учебника toocreate консольное приложение Java](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="7372e-166"><a id="Query"></a>Шаг 7. Запрос ресурсов Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7372e-166"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="7372e-167">Azure Cosmos DB поддерживает [полнофункциональные запросы](documentdb-sql-query.md) к документам JSON, хранящимся в каждой коллекции.</span><span class="sxs-lookup"><span data-stu-id="7372e-167">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="7372e-168">Hello, следующий пример кода показывает, как tooquery документов в базу данных Cosmos Azure с помощью синтаксиса SQL с hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) метод.</span><span class="sxs-lookup"><span data-stu-id="7372e-168">hello following sample code shows how tooquery documents in Azure Cosmos DB using SQL syntax with hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) method.</span></span>

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <span data-ttu-id="7372e-169"><a id="ReplaceDocument"></a>Шаг 8. Замена документа JSON</span><span class="sxs-lookup"><span data-stu-id="7372e-169"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="7372e-170">Azure Cosmos DB поддерживает обновление документов JSON, с помощью hello [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) метод.</span><span class="sxs-lookup"><span data-stu-id="7372e-170">Azure Cosmos DB supports updating JSON documents using hello [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) method.</span></span>

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <span data-ttu-id="7372e-171"><a id="DeleteDocument"></a>Шаг 9. Удаление документа JSON</span><span class="sxs-lookup"><span data-stu-id="7372e-171"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="7372e-172">Аналогичным образом Azure Cosmos DB поддерживает удаление документов JSON, с помощью hello [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) метод.</span><span class="sxs-lookup"><span data-stu-id="7372e-172">Similarly, Azure Cosmos DB supports deleting JSON documents using hello [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) method.</span></span>  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <span data-ttu-id="7372e-173"><a id="DeleteDatabase"></a>Шаг 10: Удаление hello базы данных</span><span class="sxs-lookup"><span data-stu-id="7372e-173"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="7372e-174">Удаление базы данных создана hello удаляет hello базы данных и все дочерние ресурсы (коллекции, документы, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="7372e-174">Deleting hello created database removes hello database and all children resources (collections, documents, etc.).</span></span>

    this.client.deleteDatabase("/dbs/familydb", null);

## <span data-ttu-id="7372e-175"><a id="Run"></a>Этап 11. Запуск консольного приложения Java</span><span class="sxs-lookup"><span data-stu-id="7372e-175"><a id="Run"></a>Step 11: Run your Java console application all together!</span></span>
<span data-ttu-id="7372e-176">приложения hello toorun из консоли hello, перейдите в папку проекта toohello и компиляции с помощью Maven:</span><span class="sxs-lookup"><span data-stu-id="7372e-176">toorun hello application from hello console, navigate toohello project folder and compile using Maven:</span></span>
    
    mvn package

<span data-ttu-id="7372e-177">Под управлением `mvn package` загружает последние библиотеки Azure Cosmos DB hello из Maven и создает `GetStarted-0.0.1-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="7372e-177">Running `mvn package` downloads hello latest Azure Cosmos DB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span></span> <span data-ttu-id="7372e-178">Затем запустите приложение hello, выполнив:</span><span class="sxs-lookup"><span data-stu-id="7372e-178">Then run hello app by running:</span></span>

    mvn exec:java -D exec.mainClass=GetStarted.Program

<span data-ttu-id="7372e-179">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="7372e-179">Congratulations!</span></span> <span data-ttu-id="7372e-180">Вы завершили работу с руководством по NoSQL и создали работающее консольное приложение Java.</span><span class="sxs-lookup"><span data-stu-id="7372e-180">You've completed this NoSQL tutorial and have a working Java console application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="7372e-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7372e-181">Next steps</span></span>
* <span data-ttu-id="7372e-182">Дополнительные сведения о создании веб-приложения Java</span><span class="sxs-lookup"><span data-stu-id="7372e-182">Want a Java web app tutorial?</span></span> <span data-ttu-id="7372e-183">См. сведения в статье о [создании веб-приложения Java с использованием Azure Cosmos DB](documentdb-java-application.md).</span><span class="sxs-lookup"><span data-stu-id="7372e-183">See [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md).</span></span>
* <span data-ttu-id="7372e-184">Узнайте, каким образом слишком[мониторинг учетной записи Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="7372e-184">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="7372e-185">Выполнять запросы к нашей образец набора данных в hello [площадку запросов](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="7372e-185">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="7372e-186">Дополнительные сведения о модели программирования hello в разделе Разработка hello hello [страницы документации Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="7372e-186">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
