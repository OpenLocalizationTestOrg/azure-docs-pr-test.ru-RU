---
title: "Руководство по NoSQL. Пакет SDK для создания приложения Java с помощью API-интерфейса DocumentDB для Azure Cosmos DB | Документация Майкрософт"
description: "Руководство по NoSQL, в котором создается оперативная база данных и консольное приложение Java с помощью API-интерфейса DocumentDB для Azure Cosmos DB. Azure DocumentDB — это база данных NoSQL для JSON."
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
ms.openlocfilehash: 5c4bcda308f001572e1c34e991616fc209250a02
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a><span data-ttu-id="2ffb6-105">Руководство по NoSQL. Создание консольного приложения Java с помощью API-интерфейса DocumentDB</span><span class="sxs-lookup"><span data-stu-id="2ffb6-105">NoSQL tutorial: Build a DocumentDB API Java console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2ffb6-106">.NET</span><span class="sxs-lookup"><span data-stu-id="2ffb6-106">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="2ffb6-107">.NET Core</span><span class="sxs-lookup"><span data-stu-id="2ffb6-107">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="2ffb6-108">Node.js для MongoDB</span><span class="sxs-lookup"><span data-stu-id="2ffb6-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="2ffb6-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="2ffb6-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="2ffb6-110">Java</span><span class="sxs-lookup"><span data-stu-id="2ffb6-110">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="2ffb6-111">C++</span><span class="sxs-lookup"><span data-stu-id="2ffb6-111">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="2ffb6-112">Приветствуем вас в разделе руководства по NoSQL, посвященного пакету SDK для создания консольного приложения Java с помощью API-интерфейса DocumentDB для Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-112">Welcome to the NoSQL tutorial for the DocumentDB API for Azure Cosmos DB Java SDK!</span></span> <span data-ttu-id="2ffb6-113">После изучения этого руководства у вас будет консольное приложение, которое создает ресурсы Azure Cosmos DB и отправляет запросы к ним.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-113">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="2ffb6-114">Мы рассмотрим:</span><span class="sxs-lookup"><span data-stu-id="2ffb6-114">We cover:</span></span>

* <span data-ttu-id="2ffb6-115">создание учетной записи Azure Cosmos DB и подключение к ней;</span><span class="sxs-lookup"><span data-stu-id="2ffb6-115">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="2ffb6-116">настройка решения Visual Studio;</span><span class="sxs-lookup"><span data-stu-id="2ffb6-116">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="2ffb6-117">Создание оперативной базы данных</span><span class="sxs-lookup"><span data-stu-id="2ffb6-117">Creating an online database</span></span>
* <span data-ttu-id="2ffb6-118">создание коллекции;</span><span class="sxs-lookup"><span data-stu-id="2ffb6-118">Creating a collection</span></span>
* <span data-ttu-id="2ffb6-119">создание документов JSON;</span><span class="sxs-lookup"><span data-stu-id="2ffb6-119">Creating JSON documents</span></span>
* <span data-ttu-id="2ffb6-120">выполнение запросов к коллекции;</span><span class="sxs-lookup"><span data-stu-id="2ffb6-120">Querying the collection</span></span>
* <span data-ttu-id="2ffb6-121">создание документов JSON;</span><span class="sxs-lookup"><span data-stu-id="2ffb6-121">Creating JSON documents</span></span>
* <span data-ttu-id="2ffb6-122">выполнение запросов к коллекции;</span><span class="sxs-lookup"><span data-stu-id="2ffb6-122">Querying the collection</span></span>
* <span data-ttu-id="2ffb6-123">замена документа;</span><span class="sxs-lookup"><span data-stu-id="2ffb6-123">Replacing a document</span></span>
* <span data-ttu-id="2ffb6-124">удаление документа;</span><span class="sxs-lookup"><span data-stu-id="2ffb6-124">Deleting a document</span></span>
* <span data-ttu-id="2ffb6-125">удаление базы данных.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-125">Deleting the database</span></span>

<span data-ttu-id="2ffb6-126">А теперь приступим к работе!</span><span class="sxs-lookup"><span data-stu-id="2ffb6-126">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ffb6-127">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2ffb6-127">Prerequisites</span></span>
<span data-ttu-id="2ffb6-128">Вам потребуются:</span><span class="sxs-lookup"><span data-stu-id="2ffb6-128">Make sure you have the following:</span></span>

* <span data-ttu-id="2ffb6-129">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-129">An active Azure account.</span></span> <span data-ttu-id="2ffb6-130">Если у вас ее нет, зарегистрируйте [бесплатную учетную запись](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="2ffb6-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="2ffb6-131">Кроме того, в этом руководстве можно использовать [эмулятор Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="2ffb6-131">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="2ffb6-132">Git.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-132">Git</span></span>](https://git-scm.com/downloads)
* <span data-ttu-id="2ffb6-133">[Комплект разработчика Java (JDK 7 +)](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="2ffb6-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="2ffb6-134">[Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="2ffb6-134">[Maven](http://maven.apache.org/download.cgi).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="2ffb6-135">Шаг 1. Создание учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2ffb6-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="2ffb6-136">Давайте создадим учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="2ffb6-137">Если у вас уже есть учетная запись, которую вы собираетесь использовать, можно перейти к [клонированию проекта GitHub](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="2ffb6-137">If you already have an account you want to use, you can skip ahead to [Clone the GitHub project](#GitClone).</span></span> <span data-ttu-id="2ffb6-138">При использовании эмулятора Azure Cosmos DB выполните действия, описанные в [этой статье](local-emulator.md), чтобы настроить эмулятор и сразу перейти к [клонированию проекта GitHub](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="2ffb6-138">If you are using the Azure Cosmos DB Emulator, follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to set up the emulator and skip ahead to [Clone the GitHub project](#GitClone).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="2ffb6-139"><a id="GitClone"></a>Этап 2. Клонирование проекта GitHub</span><span class="sxs-lookup"><span data-stu-id="2ffb6-139"><a id="GitClone"></a>Step 2: Clone the GitHub project</span></span>
<span data-ttu-id="2ffb6-140">[Чтобы приступить к работе с Azure Cosmos DB и Java](https://github.com/Azure-Samples/documentdb-java-getting-started), сначала клонируйте репозиторий GitHub.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-140">You can get started by cloning the GitHub repository for [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span></span> <span data-ttu-id="2ffb6-141">Например, чтобы получить образец проекта в локальной среде, в локальном каталоге выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-141">For example, from a local directory run the following to retrieve the sample project locally.</span></span>

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

<span data-ttu-id="2ffb6-142">В этом каталоге находится файл проекта `pom.xml` и папка с исходным кодом Java, `src`. Кроме того, здесь также находится файл `Program.java` с инструкциями по выполнению простых операций с Azure Cosmos DB, таких как создание документов и запрос данных в коллекции.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-142">The directory contains a `pom.xml` for the project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure Cosmos DB like creating documents and querying data within a collection.</span></span> <span data-ttu-id="2ffb6-143">В файле `pom.xml` содержится зависимость от [пакета Java SDK для DocumentDB в Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span><span class="sxs-lookup"><span data-stu-id="2ffb6-143">The `pom.xml` includes a dependency on the [DocumentDB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span></span>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <span data-ttu-id="2ffb6-144"><a id="Connect"></a>Шаг 3. Подключение к учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2ffb6-144"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="2ffb6-145">Далее вернитесь на [портал Azure](https://portal.azure.com), чтобы получить конечную точку и первичный главный ключ.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-145">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint and primary master key.</span></span> <span data-ttu-id="2ffb6-146">Конечная точка и первичный ключ Azure Cosmos DB позволяют приложению предоставлять данные о расположении, в котором будет устанавливаться подключение, делая подключение вашего приложения доверенным для Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-146">The Azure Cosmos DB endpoint and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="2ffb6-147">На портале Azure перейдите к учетной записи Azure Cosmos DB, а затем щелкните **Ключи**.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-147">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span> <span data-ttu-id="2ffb6-148">Скопируйте универсальный код ресурса (URI) с портала и вставьте его в параметр `https://FILLME.documents.azure.com` в файле Program.java.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-148">Copy the URI from the portal and paste it into `https://FILLME.documents.azure.com` in the Program.java file.</span></span> <span data-ttu-id="2ffb6-149">Затем скопируйте на портале значение поля "Первичный ключ" и вставьте его в параметр `FILLME`.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-149">Then copy the PRIMARY KEY from the portal and paste it into `FILLME`.</span></span>

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Снимок экрана портала Azure в ходе работы с руководством по NoSQL при создании консольного приложения Java.][keys]

## <a name="step-4-create-a-database"></a><span data-ttu-id="2ffb6-152">Этап 4: создание базы данных</span><span class="sxs-lookup"><span data-stu-id="2ffb6-152">Step 4: Create a database</span></span>
<span data-ttu-id="2ffb6-153">[Базу данных](documentdb-resources.md#databases) Azure Cosmos DB можно создать с помощью метода [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) класса **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-153">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) method of the **DocumentClient** class.</span></span> <span data-ttu-id="2ffb6-154">База данных представляет собой логический контейнер для хранения документов JSON, разделенных между коллекциями.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-154">A database is the logical container of JSON document storage partitioned across collections.</span></span>

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <span data-ttu-id="2ffb6-155"><a id="CreateColl"></a>Этап 5: создание коллекции</span><span class="sxs-lookup"><span data-stu-id="2ffb6-155"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="2ffb6-156">Элемент **createCollection** создает коллекцию с зарезервированной пропускной способностью и соответствующей ценой.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-156">**createCollection** creates a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="2ffb6-157">Дополнительные сведения см. на [странице цен](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="2ffb6-157">For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="2ffb6-158">Вы можете создать [коллекцию](documentdb-resources.md#collections), используя метод [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) класса **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-158">A [collection](documentdb-resources.md#collections) can be created by using the [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) method of the **DocumentClient** class.</span></span> <span data-ttu-id="2ffb6-159">Коллекция представляет собой контейнер документов JSON и связанную с ними логику в виде приложения JavaScript.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-159">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <span data-ttu-id="2ffb6-160"><a id="CreateDoc"></a>Шаг 6. Создание документов JSON</span><span class="sxs-lookup"><span data-stu-id="2ffb6-160"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="2ffb6-161">[Документ](documentdb-resources.md#documents) можно создать с помощью метода [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) класса **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-161">A [document](documentdb-resources.md#documents) can be created by using the [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) method of the **DocumentClient** class.</span></span> <span data-ttu-id="2ffb6-162">Документы относятся к пользовательскому (произвольному) содержимому JSON.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-162">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="2ffb6-163">Теперь мы можем добавить один или несколько документов.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-163">We can now insert one or more documents.</span></span> <span data-ttu-id="2ffb6-164">Если у вас уже есть данные, которые вы хотите хранить в базе данных, вы можете использовать [средство миграции данных](import-data.md) Azure Cosmos DB, чтобы импортировать эти данные в базу данных.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-164">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) to import the data into a database.</span></span>

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

![На схеме представлены иерархические отношения между учетной записью, оперативной базой данных, коллекцией и документами, используемыми в руководстве по NoSQL при создании консольного приложения Java.](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="2ffb6-166"><a id="Query"></a>Шаг 7. Запрос ресурсов Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2ffb6-166"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="2ffb6-167">Azure Cosmos DB поддерживает [полнофункциональные запросы](documentdb-sql-query.md) к документам JSON, хранящимся в каждой коллекции.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-167">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="2ffb6-168">Ниже приведен образец кода, который позволяет запросить документы в Azure Cosmos DB, используя синтаксис SQL с методом [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments).</span><span class="sxs-lookup"><span data-stu-id="2ffb6-168">The following sample code shows how to query documents in Azure Cosmos DB using SQL syntax with the [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) method.</span></span>

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <span data-ttu-id="2ffb6-169"><a id="ReplaceDocument"></a>Шаг 8. Замена документа JSON</span><span class="sxs-lookup"><span data-stu-id="2ffb6-169"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="2ffb6-170">Azure Cosmos DB поддерживает обновление документов JSON с помощью метода [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument).</span><span class="sxs-lookup"><span data-stu-id="2ffb6-170">Azure Cosmos DB supports updating JSON documents using the [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) method.</span></span>

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <span data-ttu-id="2ffb6-171"><a id="DeleteDocument"></a>Шаг 9. Удаление документа JSON</span><span class="sxs-lookup"><span data-stu-id="2ffb6-171"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="2ffb6-172">Аналогичным образом Azure Cosmos DB поддерживает удаление документов JSON с помощью метода [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument).</span><span class="sxs-lookup"><span data-stu-id="2ffb6-172">Similarly, Azure Cosmos DB supports deleting JSON documents using the [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) method.</span></span>  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <span data-ttu-id="2ffb6-173"><a id="DeleteDatabase"></a>Шаг 10. Удаление базы данных</span><span class="sxs-lookup"><span data-stu-id="2ffb6-173"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="2ffb6-174">Удаление созданной базы данных влечет удаление всех ее дочерних ресурсов (коллекций, документов и т. д.).</span><span class="sxs-lookup"><span data-stu-id="2ffb6-174">Deleting the created database removes the database and all children resources (collections, documents, etc.).</span></span>

    this.client.deleteDatabase("/dbs/familydb", null);

## <span data-ttu-id="2ffb6-175"><a id="Run"></a>Этап 11. Запуск консольного приложения Java</span><span class="sxs-lookup"><span data-stu-id="2ffb6-175"><a id="Run"></a>Step 11: Run your Java console application all together!</span></span>
<span data-ttu-id="2ffb6-176">Чтобы запустить приложение из консоли, перейдите в папку проекта и выполните компиляцию с помощью Maven:</span><span class="sxs-lookup"><span data-stu-id="2ffb6-176">To run the application from the console, navigate to the project folder and compile using Maven:</span></span>
    
    mvn package

<span data-ttu-id="2ffb6-177">Команда `mvn package` позволяет скачать последнюю версию библиотеки Azure Cosmos DB из Maven и возвращает `GetStarted-0.0.1-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-177">Running `mvn package` downloads the latest Azure Cosmos DB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span></span> <span data-ttu-id="2ffb6-178">Затем запустите приложение, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2ffb6-178">Then run the app by running:</span></span>

    mvn exec:java -D exec.mainClass=GetStarted.Program

<span data-ttu-id="2ffb6-179">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="2ffb6-179">Congratulations!</span></span> <span data-ttu-id="2ffb6-180">Вы завершили работу с руководством по NoSQL и создали работающее консольное приложение Java.</span><span class="sxs-lookup"><span data-stu-id="2ffb6-180">You've completed this NoSQL tutorial and have a working Java console application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ffb6-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2ffb6-181">Next steps</span></span>
* <span data-ttu-id="2ffb6-182">Дополнительные сведения о создании веб-приложения Java</span><span class="sxs-lookup"><span data-stu-id="2ffb6-182">Want a Java web app tutorial?</span></span> <span data-ttu-id="2ffb6-183">См. сведения в статье о [создании веб-приложения Java с использованием Azure Cosmos DB](documentdb-java-application.md).</span><span class="sxs-lookup"><span data-stu-id="2ffb6-183">See [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md).</span></span>
* <span data-ttu-id="2ffb6-184">Узнайте, как выполнять [мониторинг учетной записи Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="2ffb6-184">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="2ffb6-185">Отправьте запросы образцу набора данных в [Площадке для запросов](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="2ffb6-185">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="2ffb6-186">Дополнительные сведения о модели программирования см. в разделе "Разработка" [на странице документации Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="2ffb6-186">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
