---
title: "aaaCreate базе документа Azure Cosmos DB с Java | Документы Microsoft | Документы Microsoft"
description: "Содержит пример кода Java, можно использовать запрос tooand tooconnect hello Azure Cosmos DB DocumentDB API"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 08/02/2017
ms.author: mimig
ms.openlocfilehash: 400c9e7780034d3e28d749e734786e950edad22f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a>Azure Cosmos DB: Создание базы данных документа с использованием Java и hello портал Azure

Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт. Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД. 

Это краткое руководство создается документ базы данных с помощью hello портала средства Azure для Azure Cosmos DB. Это краткое руководство также показано, как tooquickly создать консольное приложение Java с помощью hello [DocumentDB Java API](documentdb-sdk-java.md). Hello инструкции в этом кратком руководстве можно выполнять в любой операционной системе, поддерживающий работу Java. Выполнив краткого руководства вы будете освоить создание и изменение документа ресурсы базы данных либо hello пользовательского интерфейса или программным путем, что наступит предпочтения.

## <a name="prerequisites"></a>Предварительные требования

* [Комплект разработчика Java (JDK 1.7+)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * В Ubuntu — команду, запустите `apt-get install default-jdk` tooinstall hello JDK.
    * Быть убедиться, что tooset hello JAVA_HOME среды переменной toopoint toohello папка, содержащая hello JDK.
* [Скачайте](http://maven.apache.org/download.cgi) и [установите](http://maven.apache.org/install.html) двоичный архив [Maven](http://maven.apache.org/).
    * Ubuntu, запускаются `apt-get install maven` tooinstall Maven.
* [Git.](https://www.git-scm.com/)
    * Ubuntu, запускаются `sudo apt-get install git` tooinstall Git.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Создание учетной записи базы данных

Перед созданием базы данных документа необходимо toocreate учетную запись базы данных SQL (DocumentDB) с Azure Cosmos DB.

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Добавление коллекции

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a>Добавление демонстрационных данных

Теперь можно добавить новую коллекцию tooyour данных с помощью обозревателя данных.

1. В обозревателе данных hello новой базы данных отображается в области коллекций hello. Разверните hello **задачи** базы данных, разверните hello **элементы** коллекции, нажмите кнопку **документов**и нажмите кнопку **новые документы**. 

   ![Создавать новые документы в обозревателе данных hello портал Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. Теперь можно добавьте коллекцию toohello документа с hello следующие структуры.

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. После добавления hello json toohello **документов** щелкните **Сохранить**.

    ![Копировать данные json и нажмите кнопку Сохранить в обозревателе данных в hello портал Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  Создать и сохранить один дополнительные документ, который вставляются уникальное значение для hello `id` и измените hello других свойств по своему усмотрению. Новые документы могут иметь любую структуру, так как Azure Cosmos DB не устанавливает определенные схемы данных.

     После этого можно использовать запросы в обозреватель данных tooretrieve данных, щелкнув hello **изменение фильтра** и **применить фильтр** кнопки. По умолчанию используется обозреватель данных `SELECT * FROM c` tooretrieve всех документов в коллекции hello, но можно изменить, другой tooa [SQL-запроса](documentdb-sql-query.md), такие как `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn на основе все документы hello в порядке убывания их отметки времени. 
 
     Можно также использовать обозреватель данных toocreate хранимых процедур, определяемых пользователем функций и триггеров tooperform серверных бизнес-логику, также как масштаб пропускной способности. Обозреватель данных предоставляет все hello встроенного программного доступа к данным, доступны в API-интерфейсы hello, но предоставляет простой доступ к данным tooyour hello портал Azure.

## <a name="clone-hello-sample-application"></a>Пример приложения hello клонирования

Теперь давайте переключения tooworking с кодом. Давайте клонировать приложении DocumentDB API из GitHub, задайте строку подключения hello и запустите его. Вы видите, как просто можно toowork с данными программными средствами. 

1. Откройте окно терминала git, таких как git bash и `CD` tooa рабочий каталог.  

2. Выполнения hello следующая команда репозитории примеров tooclone hello. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a>Проверка кода hello

Убедитесь, что происходит в приложение hello быстро ознакомиться. Откройте hello `Program.java` файл из папки \src\GetStarted hello и найдите следующие строки кода, создать ресурсы Azure Cosmos DB hello. 

* Hello `DocumentClient` инициализируется.

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* Создание базы данных.

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* Создание коллекции.

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* Создание нескольких документов.

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* Выполнение запроса SQL через JSON.

    ```java
    FeedOptions queryOptions = new FeedOptions();
    queryOptions.setPageSize(-1);
    queryOptions.setEnableCrossPartitionQuery(true);

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    FeedResponse<Document> queryResults = this.client.queryDocuments(
        collectionLink,
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", queryOptions);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }
    ```    

## <a name="update-your-connection-string"></a>Обновление строки подключения

Теперь вернитесь toohello Azure портала tooget данные строки подключения и скопируйте его в приложение hello. Это позволит toocommunicate вашего приложения с вашей размещенной базе данных.

1. В hello [портал Azure](http://portal.azure.com/), в вашей Azure Cosmos DB учетной записи, в hello навигации слева щелкните **ключей**и нажмите кнопку **чтения и записи ключей**. Кнопки копирования hello будет использоваться на правой стороне hello hello toocopy экрана приветствия URI и первичный ключ в hello `Program.java` файла в следующем шаге hello.

    ![Просмотреть и скопировать ключ доступа в hello портал Azure, ключи колонку](./media/create-documentdb-dotnet/keys.png)

2. В Привет открыть `Program.java` файл, скопируйте значение URI из портала hello (с использованием "Копировать" hello ") и сделать его hello значение конструктор DocumentClient toohello hello конечной точки в `Program.java`. 

    `"https://FILLME.documents.azure.com"`

4. Затем скопируйте значение ПЕРВИЧНОГО ключа из портала hello и вставьте его через «FILLME», что второй параметр в конструкторе DocumentClient hello hello. Теперь вы обновили приложения с все hello сведения учетной записи, он должен toocommunicate с Azure Cosmos DB. 
    
## <a name="run-hello-app"></a>Выполните приложение hello

1. В окне терминала git hello `cd` toohello azure-cosmos-db-documentdb-java-getting-started папки.

2. В окне терминала git hello, введите `mvn package` tooinstall hello необходимые пакеты Java.

3. Выполните в окне терминала git hello, `mvn exec:java -D exec.mainClass=GetStarted.Program` в hello окно терминала toostart работу приложений Java.

    В окне терминала hello вы получите уведомление, которое hello FamilyDB база данных была создана и toopress ключа toocontinue. Нажмите hello toocreate ключа базы данных, затем переключитесь toohello обозреватель данных и вы увидите, что в нем содержится FamilyDB базы данных. Продолжить toopress ключей toocreate hello коллекции и hello документов и выполнить запрос. По завершении проекта hello hello ресурсы будут удалены из вашей учетной записи. 

    ![Просмотреть и скопировать ключ доступа в hello портал Azure, ключи колонку](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a>Просмотрите соглашений об уровне обслуживания в hello портал Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Очистка ресурсов

Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги:

1. Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello. 
2. На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.

## <a name="next-steps"></a>Дальнейшие действия

В этом кратком руководстве вы узнали, как toocreate учетную запись Azure Cosmos DB документа базы данных и коллекции с помощью hello обозреватель данных и запустите приложение toodo hello же программными средствами. Теперь можно импортировать учетной записи Cosmos DB tooyour дополнительные данные. 

> [!div class="nextstepaction"]
> [Импорт данных в DocumentDB с помощью средства миграции базы данных](import-data.md)


