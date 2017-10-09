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
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a><span data-ttu-id="34b4f-103">Azure Cosmos DB: Создание базы данных документа с использованием Java и hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="34b4f-103">Azure Cosmos DB: Create a document database using Java and hello Azure portal</span></span>

<span data-ttu-id="34b4f-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="34b4f-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="34b4f-105">Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД.</span><span class="sxs-lookup"><span data-stu-id="34b4f-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="34b4f-106">Это краткое руководство создается документ базы данных с помощью hello портала средства Azure для Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="34b4f-106">This quickstart creates a document database using hello Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="34b4f-107">Это краткое руководство также показано, как tooquickly создать консольное приложение Java с помощью hello [DocumentDB Java API](documentdb-sdk-java.md).</span><span class="sxs-lookup"><span data-stu-id="34b4f-107">This quickstart also shows you how tooquickly create a Java console app using hello [DocumentDB Java API](documentdb-sdk-java.md).</span></span> <span data-ttu-id="34b4f-108">Hello инструкции в этом кратком руководстве можно выполнять в любой операционной системе, поддерживающий работу Java.</span><span class="sxs-lookup"><span data-stu-id="34b4f-108">hello instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="34b4f-109">Выполнив краткого руководства вы будете освоить создание и изменение документа ресурсы базы данных либо hello пользовательского интерфейса или программным путем, что наступит предпочтения.</span><span class="sxs-lookup"><span data-stu-id="34b4f-109">By completing this quickstart you'll be familiar with creating and modifying document database resources in either hello UI or programatically, whichever is your preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34b4f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="34b4f-110">Prerequisites</span></span>

* [<span data-ttu-id="34b4f-111">Комплект разработчика Java (JDK 1.7+)</span><span class="sxs-lookup"><span data-stu-id="34b4f-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="34b4f-112">В Ubuntu — команду, запустите `apt-get install default-jdk` tooinstall hello JDK.</span><span class="sxs-lookup"><span data-stu-id="34b4f-112">On Ubuntu, run `apt-get install default-jdk` tooinstall hello JDK.</span></span>
    * <span data-ttu-id="34b4f-113">Быть убедиться, что tooset hello JAVA_HOME среды переменной toopoint toohello папка, содержащая hello JDK.</span><span class="sxs-lookup"><span data-stu-id="34b4f-113">Be sure tooset hello JAVA_HOME environment variable toopoint toohello folder where hello JDK is installed.</span></span>
* <span data-ttu-id="34b4f-114">[Скачайте](http://maven.apache.org/download.cgi) и [установите](http://maven.apache.org/install.html) двоичный архив [Maven](http://maven.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="34b4f-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="34b4f-115">Ubuntu, запускаются `apt-get install maven` tooinstall Maven.</span><span class="sxs-lookup"><span data-stu-id="34b4f-115">On Ubuntu, you can run `apt-get install maven` tooinstall Maven.</span></span>
* [<span data-ttu-id="34b4f-116">Git.</span><span class="sxs-lookup"><span data-stu-id="34b4f-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="34b4f-117">Ubuntu, запускаются `sudo apt-get install git` tooinstall Git.</span><span class="sxs-lookup"><span data-stu-id="34b4f-117">On Ubuntu, you can run `sudo apt-get install git` tooinstall Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="34b4f-118">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="34b4f-118">Create a database account</span></span>

<span data-ttu-id="34b4f-119">Перед созданием базы данных документа необходимо toocreate учетную запись базы данных SQL (DocumentDB) с Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="34b4f-119">Before you can create a document database, you need toocreate a SQL (DocumentDB) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="34b4f-120">Добавление коллекции</span><span class="sxs-lookup"><span data-stu-id="34b4f-120">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="34b4f-121">Добавление демонстрационных данных</span><span class="sxs-lookup"><span data-stu-id="34b4f-121">Add sample data</span></span>

<span data-ttu-id="34b4f-122">Теперь можно добавить новую коллекцию tooyour данных с помощью обозревателя данных.</span><span class="sxs-lookup"><span data-stu-id="34b4f-122">You can now add data tooyour new collection using Data Explorer.</span></span>

1. <span data-ttu-id="34b4f-123">В обозревателе данных hello новой базы данных отображается в области коллекций hello.</span><span class="sxs-lookup"><span data-stu-id="34b4f-123">In Data Explorer, hello new database appears in hello Collections pane.</span></span> <span data-ttu-id="34b4f-124">Разверните hello **задачи** базы данных, разверните hello **элементы** коллекции, нажмите кнопку **документов**и нажмите кнопку **новые документы**.</span><span class="sxs-lookup"><span data-stu-id="34b4f-124">Expand hello **Tasks** database, expand hello **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Создавать новые документы в обозревателе данных hello портал Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="34b4f-126">Теперь можно добавьте коллекцию toohello документа с hello следующие структуры.</span><span class="sxs-lookup"><span data-stu-id="34b4f-126">Now add a document toohello collection with hello following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="34b4f-127">После добавления hello json toohello **документов** щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="34b4f-127">Once you've added hello json toohello **Documents** tab, click **Save**.</span></span>

    ![Копировать данные json и нажмите кнопку Сохранить в обозревателе данных в hello портал Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="34b4f-129">Создать и сохранить один дополнительные документ, который вставляются уникальное значение для hello `id` и измените hello других свойств по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="34b4f-129">Create and save one more document where you insert a unique value for hello `id` property, and change hello other properties as you see fit.</span></span> <span data-ttu-id="34b4f-130">Новые документы могут иметь любую структуру, так как Azure Cosmos DB не устанавливает определенные схемы данных.</span><span class="sxs-lookup"><span data-stu-id="34b4f-130">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="34b4f-131">После этого можно использовать запросы в обозреватель данных tooretrieve данных, щелкнув hello **изменение фильтра** и **применить фильтр** кнопки.</span><span class="sxs-lookup"><span data-stu-id="34b4f-131">You can now use queries in Data Explorer tooretrieve your data by clicking hello **Edit Filter** and **Apply Filter** buttons.</span></span> <span data-ttu-id="34b4f-132">По умолчанию используется обозреватель данных `SELECT * FROM c` tooretrieve всех документов в коллекции hello, но можно изменить, другой tooa [SQL-запроса](documentdb-sql-query.md), такие как `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn на основе все документы hello в порядке убывания их отметки времени.</span><span class="sxs-lookup"><span data-stu-id="34b4f-132">By default, Data Explorer uses `SELECT * FROM c` tooretrieve all documents in hello collection, but you can change that tooa different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn all hello documents in descending order based on their timestamp.</span></span> 
 
     <span data-ttu-id="34b4f-133">Можно также использовать обозреватель данных toocreate хранимых процедур, определяемых пользователем функций и триггеров tooperform серверных бизнес-логику, также как масштаб пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="34b4f-133">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="34b4f-134">Обозреватель данных предоставляет все hello встроенного программного доступа к данным, доступны в API-интерфейсы hello, но предоставляет простой доступ к данным tooyour hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="34b4f-134">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="34b4f-135">Пример приложения hello клонирования</span><span class="sxs-lookup"><span data-stu-id="34b4f-135">Clone hello sample application</span></span>

<span data-ttu-id="34b4f-136">Теперь давайте переключения tooworking с кодом.</span><span class="sxs-lookup"><span data-stu-id="34b4f-136">Now let's switch tooworking with code.</span></span> <span data-ttu-id="34b4f-137">Давайте клонировать приложении DocumentDB API из GitHub, задайте строку подключения hello и запустите его.</span><span class="sxs-lookup"><span data-stu-id="34b4f-137">Let's clone a DocumentDB API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="34b4f-138">Вы видите, как просто можно toowork с данными программными средствами.</span><span class="sxs-lookup"><span data-stu-id="34b4f-138">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="34b4f-139">Откройте окно терминала git, таких как git bash и `CD` tooa рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="34b4f-139">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="34b4f-140">Выполнения hello следующая команда репозитории примеров tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="34b4f-140">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="34b4f-141">Проверка кода hello</span><span class="sxs-lookup"><span data-stu-id="34b4f-141">Review hello code</span></span>

<span data-ttu-id="34b4f-142">Убедитесь, что происходит в приложение hello быстро ознакомиться.</span><span class="sxs-lookup"><span data-stu-id="34b4f-142">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="34b4f-143">Откройте hello `Program.java` файл из папки \src\GetStarted hello и найдите следующие строки кода, создать ресурсы Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="34b4f-143">Open hello `Program.java` file from hello \src\GetStarted folder, and find these lines of code that create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="34b4f-144">Hello `DocumentClient` инициализируется.</span><span class="sxs-lookup"><span data-stu-id="34b4f-144">hello `DocumentClient` is initialized.</span></span>

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* <span data-ttu-id="34b4f-145">Создание базы данных.</span><span class="sxs-lookup"><span data-stu-id="34b4f-145">A new database is created.</span></span>

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* <span data-ttu-id="34b4f-146">Создание коллекции.</span><span class="sxs-lookup"><span data-stu-id="34b4f-146">A new collection is created.</span></span>

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* <span data-ttu-id="34b4f-147">Создание нескольких документов.</span><span class="sxs-lookup"><span data-stu-id="34b4f-147">Some documents are created.</span></span>

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* <span data-ttu-id="34b4f-148">Выполнение запроса SQL через JSON.</span><span class="sxs-lookup"><span data-stu-id="34b4f-148">A SQL query over JSON is performed.</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="34b4f-149">Обновление строки подключения</span><span class="sxs-lookup"><span data-stu-id="34b4f-149">Update your connection string</span></span>

<span data-ttu-id="34b4f-150">Теперь вернитесь toohello Azure портала tooget данные строки подключения и скопируйте его в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="34b4f-150">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span> <span data-ttu-id="34b4f-151">Это позволит toocommunicate вашего приложения с вашей размещенной базе данных.</span><span class="sxs-lookup"><span data-stu-id="34b4f-151">This will enable your app toocommunicate with your hosted database.</span></span>

1. <span data-ttu-id="34b4f-152">В hello [портал Azure](http://portal.azure.com/), в вашей Azure Cosmos DB учетной записи, в hello навигации слева щелкните **ключей**и нажмите кнопку **чтения и записи ключей**.</span><span class="sxs-lookup"><span data-stu-id="34b4f-152">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="34b4f-153">Кнопки копирования hello будет использоваться на правой стороне hello hello toocopy экрана приветствия URI и первичный ключ в hello `Program.java` файла в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="34b4f-153">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and PRIMARY KEY into hello `Program.java` file in hello next step.</span></span>

    ![Просмотреть и скопировать ключ доступа в hello портал Azure, ключи колонку](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="34b4f-155">В Привет открыть `Program.java` файл, скопируйте значение URI из портала hello (с использованием "Копировать" hello ") и сделать его hello значение конструктор DocumentClient toohello hello конечной точки в `Program.java`.</span><span class="sxs-lookup"><span data-stu-id="34b4f-155">In hello open `Program.java` file, copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint toohello DocumentClient constructor in `Program.java`.</span></span> 

    `"https://FILLME.documents.azure.com"`

4. <span data-ttu-id="34b4f-156">Затем скопируйте значение ПЕРВИЧНОГО ключа из портала hello и вставьте его через «FILLME», что второй параметр в конструкторе DocumentClient hello hello.</span><span class="sxs-lookup"><span data-stu-id="34b4f-156">Then copy your PRIMARY KEY value from hello portal and paste it over “FILLME”, making it hello second parameter in hello DocumentClient constructor.</span></span> <span data-ttu-id="34b4f-157">Теперь вы обновили приложения с все hello сведения учетной записи, он должен toocommunicate с Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="34b4f-157">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-app"></a><span data-ttu-id="34b4f-158">Выполните приложение hello</span><span class="sxs-lookup"><span data-stu-id="34b4f-158">Run hello app</span></span>

1. <span data-ttu-id="34b4f-159">В окне терминала git hello `cd` toohello azure-cosmos-db-documentdb-java-getting-started папки.</span><span class="sxs-lookup"><span data-stu-id="34b4f-159">In hello git terminal window, `cd` toohello azure-cosmos-db-documentdb-java-getting-started folder.</span></span>

2. <span data-ttu-id="34b4f-160">В окне терминала git hello, введите `mvn package` tooinstall hello необходимые пакеты Java.</span><span class="sxs-lookup"><span data-stu-id="34b4f-160">In hello git terminal window, type `mvn package` tooinstall hello required Java packages.</span></span>

3. <span data-ttu-id="34b4f-161">Выполните в окне терминала git hello, `mvn exec:java -D exec.mainClass=GetStarted.Program` в hello окно терминала toostart работу приложений Java.</span><span class="sxs-lookup"><span data-stu-id="34b4f-161">In hello git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in hello terminal window toostart your Java application.</span></span>

    <span data-ttu-id="34b4f-162">В окне терминала hello вы получите уведомление, которое hello FamilyDB база данных была создана и toopress ключа toocontinue.</span><span class="sxs-lookup"><span data-stu-id="34b4f-162">In hello terminal window, you'll receive notification that hello FamilyDB database was created, and toopress a key toocontinue.</span></span> <span data-ttu-id="34b4f-163">Нажмите hello toocreate ключа базы данных, затем переключитесь toohello обозреватель данных и вы увидите, что в нем содержится FamilyDB базы данных.</span><span class="sxs-lookup"><span data-stu-id="34b4f-163">Press a key toocreate hello database, then switch toohello Data Explorer and you'll see that it now contains a FamilyDB database.</span></span> <span data-ttu-id="34b4f-164">Продолжить toopress ключей toocreate hello коллекции и hello документов и выполнить запрос.</span><span class="sxs-lookup"><span data-stu-id="34b4f-164">Continue toopress keys toocreate hello collection and hello documents and then perform a query.</span></span> <span data-ttu-id="34b4f-165">По завершении проекта hello hello ресурсы будут удалены из вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="34b4f-165">When hello project completes, hello resources are deleted from your account.</span></span> 

    ![Просмотреть и скопировать ключ доступа в hello портал Azure, ключи колонку](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="34b4f-167">Просмотрите соглашений об уровне обслуживания в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="34b4f-167">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="34b4f-168">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="34b4f-168">Clean up resources</span></span>

<span data-ttu-id="34b4f-169">Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="34b4f-169">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="34b4f-170">Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="34b4f-170">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="34b4f-171">На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="34b4f-171">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34b4f-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="34b4f-172">Next steps</span></span>

<span data-ttu-id="34b4f-173">В этом кратком руководстве вы узнали, как toocreate учетную запись Azure Cosmos DB документа базы данных и коллекции с помощью hello обозреватель данных и запустите приложение toodo hello же программными средствами.</span><span class="sxs-lookup"><span data-stu-id="34b4f-173">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, document database, and collection using hello Data Explorer, and run an app toodo hello same thing programmatically.</span></span> <span data-ttu-id="34b4f-174">Теперь можно импортировать учетной записи Cosmos DB tooyour дополнительные данные.</span><span class="sxs-lookup"><span data-stu-id="34b4f-174">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="34b4f-175">Импорт данных в DocumentDB с помощью средства миграции базы данных</span><span class="sxs-lookup"><span data-stu-id="34b4f-175">Import data into Azure Cosmos DB</span></span>](import-data.md)


