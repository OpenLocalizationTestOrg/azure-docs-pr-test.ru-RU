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
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a>Руководство по NoSQL. Создание консольного приложения Java с помощью API-интерфейса DocumentDB
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js для MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Вас приветствует toohello NoSQL учебник по API DocumentDB для пакета SDK для Java Azure Cosmos DB hello! После изучения этого руководства у вас будет консольное приложение, которое создает ресурсы Azure Cosmos DB и отправляет запросы к ним.

Мы рассмотрим:

* Создание и подключение учетной записи Azure Cosmos DB tooan
* настройка решения Visual Studio;
* Создание оперативной базы данных
* создание коллекции;
* создание документов JSON;
* Запрос к коллекции hello
* создание документов JSON;
* Запрос к коллекции hello
* замена документа;
* удаление документа;
* Удаление базы данных hello

А теперь приступим к работе!

## <a name="prerequisites"></a>Предварительные требования
Убедитесь, что у вас есть следующие hello:

* Активная учетная запись Azure. Если у вас ее нет, зарегистрируйте [бесплатную учетную запись](https://azure.microsoft.com/free/). Кроме того, можно использовать hello [DB эмулятор Azure Cosmos](local-emulator.md) для этого учебника.
* [Git.](https://git-scm.com/downloads)
* [Комплект разработчика Java (JDK 7 +)](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
* [Maven](http://maven.apache.org/download.cgi).

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Шаг 1. Создание учетной записи Azure Cosmos DB
Давайте создадим учетную запись Azure Cosmos DB. При наличии учетной записи требуется toouse можно сразу перейти слишком[клон hello GitHub проекта](#GitClone). При использовании hello Azure Cosmos DB эмулятор, выполните действия hello в [DB эмулятор Azure Cosmos](local-emulator.md) tooset Настройка эмулятора hello и пропускать слишком[клон hello GitHub проекта](#GitClone).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="GitClone"></a>Шаг 2: Клонирование hello GitHub проекта
Вы можете начать клонированием репозитория GitHub hello для [Приступая к работе с Azure Cosmos DB и Java](https://github.com/Azure-Samples/documentdb-java-getting-started). Например из локального каталога выполните следующие tooretrieve hello образец проекта локально hello.

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

каталог Hello содержит `pom.xml` для проекта hello и `src` папку, содержащую Java исходного кода включая `Program.java` котором показывается, как выполнять простые операции с Azure DB Cosmos, таких как создание документов и запроса данных в Коллекция. Hello `pom.xml` включает зависимость от hello [DocumentDB Java SDK на Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <a id="Connect"></a>Шаг 3: Учетная запись Azure Cosmos DB tooan подключения
Далее head резервное toohello [портала Azure](https://portal.azure.com) tooretrieve конечной точки и основного главного ключа. Hello Azure Cosmos DB конечной точки и первичный ключ необходимы для вашего приложения toounderstand где tooconnect, а для Azure Cosmos DB tootrust подключения вашего приложения.

В hello портал Azure, перейдите учетная запись Azure Cosmos DB tooyour и нажмите кнопку **ключей**. Скопируйте hello URI с портала hello и вставьте его в `https://FILLME.documents.azure.com` в файле Program.java hello. Затем копировать hello первичный ключ с портала hello и вставьте его в `FILLME`.

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Снимок экрана: hello hello NoSQL учебника toocreate консольное приложение Java портал Azure. Показывает Cosmos Azure DB учетной записи, с hello общаются выделен, hello выделенной колонке учетная запись Azure Cosmos DB hello кнопкой ключи и значения URI, первичный ключ и ВТОРИЧНЫЙ ключ hello выделены на hello колонке ключей][keys]

## <a name="step-4-create-a-database"></a>Этап 4: создание базы данных
Базы данных Azure Cosmos [базы данных](documentdb-resources.md#databases) могут быть созданы с помощью hello [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) метод hello **DocumentClient** класса. База данных находится hello логический контейнер для хранения документов JSON, секционированный по коллекциям.

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <a id="CreateColl"></a>Этап 5: создание коллекции
> [!WARNING]
> Элемент **createCollection** создает коллекцию с зарезервированной пропускной способностью и соответствующей ценой. Дополнительные сведения см. на [странице цен](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

Объект [коллекции](documentdb-resources.md#collections) могут быть созданы с помощью hello [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) метод hello **DocumentClient** класса. Коллекция представляет собой контейнер документов JSON и связанную с ними логику в виде приложения JavaScript.


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <a id="CreateDoc"></a>Шаг 6. Создание документов JSON
Объект [документа](documentdb-resources.md#documents) могут быть созданы с помощью hello [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) метод hello **DocumentClient** класса. Документы относятся к пользовательскому (произвольному) содержимому JSON. Теперь мы можем добавить один или несколько документов. При наличии данных, отсылаемых toostore в базе данных можно использовать базу данных Cosmos Azure [средство переноса данных](import-data.md) tooimport hello данных в базу данных.

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

## <a id="Query"></a>Шаг 7. Запрос ресурсов Azure Cosmos DB
Azure Cosmos DB поддерживает [полнофункциональные запросы](documentdb-sql-query.md) к документам JSON, хранящимся в каждой коллекции.  Hello, следующий пример кода показывает, как tooquery документов в базу данных Cosmos Azure с помощью синтаксиса SQL с hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) метод.

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <a id="ReplaceDocument"></a>Шаг 8. Замена документа JSON
Azure Cosmos DB поддерживает обновление документов JSON, с помощью hello [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) метод.

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <a id="DeleteDocument"></a>Шаг 9. Удаление документа JSON
Аналогичным образом Azure Cosmos DB поддерживает удаление документов JSON, с помощью hello [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) метод.  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <a id="DeleteDatabase"></a>Шаг 10: Удаление hello базы данных
Удаление базы данных создана hello удаляет hello базы данных и все дочерние ресурсы (коллекции, документы, и т. д.).

    this.client.deleteDatabase("/dbs/familydb", null);

## <a id="Run"></a>Этап 11. Запуск консольного приложения Java
приложения hello toorun из консоли hello, перейдите в папку проекта toohello и компиляции с помощью Maven:
    
    mvn package

Под управлением `mvn package` загружает последние библиотеки Azure Cosmos DB hello из Maven и создает `GetStarted-0.0.1-SNAPSHOT.jar`. Затем запустите приложение hello, выполнив:

    mvn exec:java -D exec.mainClass=GetStarted.Program

Поздравляем! Вы завершили работу с руководством по NoSQL и создали работающее консольное приложение Java.

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о создании веб-приложения Java См. сведения в статье о [создании веб-приложения Java с использованием Azure Cosmos DB](documentdb-java-application.md).
* Узнайте, каким образом слишком[мониторинг учетной записи Azure Cosmos DB](monitor-accounts.md).
* Выполнять запросы к нашей образец набора данных в hello [площадку запросов](https://www.documentdb.com/sql/demo).
* Дополнительные сведения о модели программирования hello в разделе Разработка hello hello [страницы документации Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
