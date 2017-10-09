---
<span data-ttu-id="83a09-101">Заголовок: aaa» Azure Cosmos DB: построение консольного приложения MongoDB API с Golang и hello портал Azure | Документы Microsoft» Описание: tooconnect tooand можно использовать образец кода Golang запросы к службам Azure Cosmos DB представляется: cosmos db Автор: диспетчер Durgaprasad Budhwani: jhubbard редактор: mimig1</span><span class="sxs-lookup"><span data-stu-id="83a09-101">title: aaa"Azure Cosmos DB: Build a MongoDB API console app with Golang and hello Azure portal | Microsoft Docs" description: Presents a Golang code sample you can use tooconnect tooand query Azure Cosmos DB services: cosmos-db author: Durgaprasad-Budhwani manager: jhubbard editor: mimig1</span></span>

<span data-ttu-id="83a09-102">MS.Service: cosmos db ms.topic: статья героя ms.date: ms.author 07/21/2017 г.: mimig</span><span class="sxs-lookup"><span data-stu-id="83a09-102">ms.service: cosmos-db ms.topic: hero-article ms.date: 07/21/2017 ms.author: mimig</span></span>
---

# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-golang-and-hello-azure-portal"></a><span data-ttu-id="83a09-103">Azure Cosmos DB: Построение консольного приложения MongoDB API с Golang и hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="83a09-103">Azure Cosmos DB: Build a MongoDB API console app with Golang and hello Azure portal</span></span>

<span data-ttu-id="83a09-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="83a09-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="83a09-105">Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД.</span><span class="sxs-lookup"><span data-stu-id="83a09-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span>

<span data-ttu-id="83a09-106">Краткое руководство демонстрирует, как toouse существующий [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) приложения, написанного на [Golang](https://golang.org/) и подключите базу данных Azure Cosmos tooyour базы данных, которая поддерживает MongoDB клиентских подключений.</span><span class="sxs-lookup"><span data-stu-id="83a09-106">This quick-start demonstrates how toouse an existing [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) app written in [Golang](https://golang.org/) and connect it tooyour Azure Cosmos DB database, which supports MongoDB client connections.</span></span>

<span data-ttu-id="83a09-107">Другими словами приложение Golang знает только подключение tooa базы данных с помощью интерфейсов API MongoDB.</span><span class="sxs-lookup"><span data-stu-id="83a09-107">In other words, your Golang application only knows that it's connecting tooa database using MongoDB APIs.</span></span> <span data-ttu-id="83a09-108">Он является прозрачным toohello приложение, которое hello данных хранится в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="83a09-108">It is transparent toohello application that hello data is stored in Azure Cosmos DB.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83a09-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="83a09-109">Prerequisites</span></span>

- <span data-ttu-id="83a09-110">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="83a09-110">An Azure subscription.</span></span> <span data-ttu-id="83a09-111">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="83a09-111">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free) before you begin.</span></span>
- <span data-ttu-id="83a09-112">[Go](https://golang.org/dl/) и базовых знаний о hello [Go](https://golang.org/) языка.</span><span class="sxs-lookup"><span data-stu-id="83a09-112">[Go](https://golang.org/dl/) and a basic knowledge of hello [Go](https://golang.org/) language.</span></span>
- <span data-ttu-id="83a09-113">Интегрированная среда разработки: [Gogland](https://www.jetbrains.com/go/), созданная Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) корпорации Майкрософт или [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="83a09-113">An IDE — [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span> <span data-ttu-id="83a09-114">В этом руководстве используется Goglang.</span><span class="sxs-lookup"><span data-stu-id="83a09-114">In this tutorial, I'm using Goglang.</span></span>

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="83a09-115">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="83a09-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="83a09-116">Пример приложения hello клонирования</span><span class="sxs-lookup"><span data-stu-id="83a09-116">Clone hello sample application</span></span>

<span data-ttu-id="83a09-117">Клонирование пример приложения hello и установите пакеты необходимых hello.</span><span class="sxs-lookup"><span data-stu-id="83a09-117">Clone hello sample application and install hello required packages.</span></span>

1. <span data-ttu-id="83a09-118">Создайте папку с именем CosmosDBSample внутри hello GOROOT\src папку, которая является C:\Go\ по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="83a09-118">Create a folder named CosmosDBSample inside hello GOROOT\src folder, which is C:\Go\ by default.</span></span>
2. <span data-ttu-id="83a09-119">Выполните следующую команду с помощью окно терминала git, например репозиторий git bash tooclone hello образец в папку CosmosDBSample hello hello.</span><span class="sxs-lookup"><span data-stu-id="83a09-119">Run hello following command using a git terminal window such as git bash tooclone hello sample repository into hello CosmosDBSample folder.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-golang-getting-started.git
    ```
3.  <span data-ttu-id="83a09-120">Следующая команда tooget hello mgo пакет выполнения hello.</span><span class="sxs-lookup"><span data-stu-id="83a09-120">Run hello following command tooget hello mgo package.</span></span> 

    ```
    go get gopkg.in/mgo.v2
    ```

<span data-ttu-id="83a09-121">Hello [mgo](http://labix.org/mgo) драйвера (произносится как *mango*) является [MongoDB](http://www.mongodb.org/) драйвер для hello [Go языка](http://golang.org/) , реализует форматированного и проходит тщательного тестирования Выбор функций в следующих стандартных идиом Go очень простой API.</span><span class="sxs-lookup"><span data-stu-id="83a09-121">hello [mgo](http://labix.org/mgo) driver (pronounced as *mango*) is a [MongoDB](http://www.mongodb.org/) driver for hello [Go language](http://golang.org/) that implements a rich and well tested selection of features under a very simple API following standard Go idioms.</span></span>

<a id="connection-string"></a>

## <a name="update-your-connection-string"></a><span data-ttu-id="83a09-122">Обновление строки подключения</span><span class="sxs-lookup"><span data-stu-id="83a09-122">Update your connection string</span></span>

<span data-ttu-id="83a09-123">Теперь вернитесь toohello Azure портала tooget данные строки подключения и скопируйте его в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="83a09-123">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="83a09-124">Нажмите кнопку **краткого** в левом меню навигации Здравствуйте и нажмите кнопку **других** tooview hello строка информация о соединении hello Go приложения.</span><span class="sxs-lookup"><span data-stu-id="83a09-124">Click **Quick start** in hello left navigation menu, and then click **Other** tooview hello connection string information required by hello Go application.</span></span>

2. <span data-ttu-id="83a09-125">В Goglang откройте файл main.go hello в каталоге GOROOT\CosmosDBSample hello и измените следующие строки кода, используя строку подключения hello из hello портал Azure, как показано в следующий снимок экрана приветствия hello.</span><span class="sxs-lookup"><span data-stu-id="83a09-125">In Goglang, open hello main.go file in hello GOROOT\CosmosDBSample directory and update hello following lines of code using hello connection string information from hello Azure portal as shown in hello following screenshot.</span></span> 

    <span data-ttu-id="83a09-126">Имя базы данных Hello — префикс hello hello **узла** значение в строку hello Azure портала подключение.</span><span class="sxs-lookup"><span data-stu-id="83a09-126">hello Database name is hello prefix of hello **Host** value in hello Azure portal connection string pane.</span></span> <span data-ttu-id="83a09-127">Для учетной записи hello, показано в приведенном ниже рисунке hello hello имя базы данных — golang-советы от.</span><span class="sxs-lookup"><span data-stu-id="83a09-127">For hello account shown in hello image below, hello Database name is golang-coach.</span></span>

    ```go
    Database: "hello prefix of hello Host value in hello Azure portal",
    Username: "hello Username in hello Azure portal",
    Password: "hello Password in hello Azure portal",
    ```

    ![Краткое руководство области другие вкладки данных строки подключения hello Azure портала отображение hello](./media/create-mongodb-golang/cosmos-db-golang-connection-string.png)

3. <span data-ttu-id="83a09-129">Сохраните файл main.go hello.</span><span class="sxs-lookup"><span data-stu-id="83a09-129">Save hello main.go file.</span></span>

## <a name="review-hello-code"></a><span data-ttu-id="83a09-130">Проверка кода hello</span><span class="sxs-lookup"><span data-stu-id="83a09-130">Review hello code</span></span>

<span data-ttu-id="83a09-131">Убедитесь, что происходит в файле main.go hello быстро ознакомиться.</span><span class="sxs-lookup"><span data-stu-id="83a09-131">Let's make a quick review of what's happening in hello main.go file.</span></span> 

### <a name="connecting-hello-go-app-tooazure-cosmos-db"></a><span data-ttu-id="83a09-132">Подключение hello tooAzure Go приложения Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="83a09-132">Connecting hello Go app tooAzure Cosmos DB</span></span>

<span data-ttu-id="83a09-133">Azure Cosmos DB поддерживает протокол SSL включен MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="83a09-133">Azure Cosmos DB supports hello SSL-enabled MongoDB.</span></span> <span data-ttu-id="83a09-134">tooan tooconnect MongoDB протокол SSL включен, необходимо toodefine hello **DialServer** функционировать в [mgo. DialInfo](http://gopkg.in/mgo.v2#DialInfo)и сделать использование hello [tls. *Удаленный* ](http://golang.org/pkg/crypto/tls#Dial) функции tooperform hello соединения.</span><span class="sxs-lookup"><span data-stu-id="83a09-134">tooconnect tooan SSL-enabled MongoDB, you need toodefine hello **DialServer** function in [mgo.DialInfo](http://gopkg.in/mgo.v2#DialInfo), and make use of hello [tls.*Dial*](http://golang.org/pkg/crypto/tls#Dial) function tooperform hello connection.</span></span>

<span data-ttu-id="83a09-135">Следующий фрагмент кода Golang Hello подключается hello Go приложения с Azure Cosmos базы данных MongoDB API.</span><span class="sxs-lookup"><span data-stu-id="83a09-135">hello following Golang code snippet connects hello Go app with Azure Cosmos DB MongoDB API.</span></span> <span data-ttu-id="83a09-136">Hello *DialInfo* класс содержит параметры для установки сеанса с кластером MongoDB.</span><span class="sxs-lookup"><span data-stu-id="83a09-136">hello *DialInfo* class holds options for establishing a session with a MongoDB cluster.</span></span>

```go
// DialInfo holds options for establishing a session with a MongoDB cluster.
dialInfo := &mgo.DialInfo{
    Addrs:    []string{"golang-couch.documents.azure.com:10255"}, // Get HOST + PORT
    Timeout:  60 * time.Second,
    Database: "database", // It can be anything
    Username: "username", // Username
    Password: "Azure database connect password from Azure Portal", // PASSWORD
    DialServer: func(addr *mgo.ServerAddr) (net.Conn, error) {
        return tls.Dial("tcp", addr.String(), &tls.Config{})
    },
}

// Create a session which maintains a pool of socket connections
// tooour Azure Cosmos DB MongoDB database.
session, err := mgo.DialWithInfo(dialInfo)

if err != nil {
    fmt.Printf("Can't connect toomongo, go error %v\n", err)
    os.Exit(1)
}

defer session.Close()

// SetSafe changes hello session safety mode.
// If hello safe parameter is nil, hello session is put in unsafe mode, 
// and writes become fire-and-forget,
// without error checking. hello unsafe mode is faster since operations won't hold on waiting for a confirmation.
// 
session.SetSafe(&mgo.Safe{})
```

<span data-ttu-id="83a09-137">Hello **mgo. Dial()** метод используется, когда отсутствует подключение SSL.</span><span class="sxs-lookup"><span data-stu-id="83a09-137">hello **mgo.Dial()** method is used when there is no SSL connection.</span></span> <span data-ttu-id="83a09-138">SSL-соединением, hello **mgo. DialWithInfo()** метод является обязательным.</span><span class="sxs-lookup"><span data-stu-id="83a09-138">For an SSL connection, hello **mgo.DialWithInfo()** method is required.</span></span>

<span data-ttu-id="83a09-139">Экземпляр hello **DialWIthInfo {}** является объектом сеанса используется toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="83a09-139">An instance of hello **DialWIthInfo{}** object is used toocreate hello session object.</span></span> <span data-ttu-id="83a09-140">После установления сеанса hello доступны hello коллекции с помощью hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="83a09-140">Once hello session is established, you can access hello collection by using hello following code snippet:</span></span>

```go
collection := session.DB(“database”).C(“package”)
```

<a id="create-document"></a>

### <a name="create-a-document"></a><span data-ttu-id="83a09-141">Создание документа</span><span class="sxs-lookup"><span data-stu-id="83a09-141">Create a document</span></span>

```go
// Model
type Package struct {
    Id bson.ObjectId  `bson:"_id,omitempty"`
    FullName      string
    Description   string
    StarsCount    int
    ForksCount    int
    LastUpdatedBy string
}

// insert Document in collection
err = collection.Insert(&Package{
    FullName:"react",
    Description:"A framework for building native apps with React.",
    ForksCount: 11392,
    StarsCount:48794,
    LastUpdatedBy:"shergin",

})

if err != nil {
    log.Fatal("Problem inserting data: ", err)
    return
}
```

### <a name="query-or-read-a-document"></a><span data-ttu-id="83a09-142">Запрос к документу или чтение документа</span><span class="sxs-lookup"><span data-stu-id="83a09-142">Query or read a document</span></span>

<span data-ttu-id="83a09-143">Azure Cosmos DB поддерживает полнофункциональные запросы к документам JSON, хранящимся в каждой коллекции.</span><span class="sxs-lookup"><span data-stu-id="83a09-143">Azure Cosmos DB supports rich queries against JSON documents stored in each collection.</span></span> <span data-ttu-id="83a09-144">Hello следующем образце кода показан запрос, который можно запустить с документами hello в коллекции.</span><span class="sxs-lookup"><span data-stu-id="83a09-144">hello following sample code shows a query that you can run against hello documents in your collection.</span></span>

```go
// Get a Document from hello collection
result := Package{}
err = collection.Find(bson.M{"fullname": "react"}).One(&result)
if err != nil {
    log.Fatal("Error finding record: ", err)
    return
}

fmt.Println("Description:", result.Description)
```


### <a name="update-a-document"></a><span data-ttu-id="83a09-145">обновление документа;</span><span class="sxs-lookup"><span data-stu-id="83a09-145">Update a document</span></span>

```go
// Update a document
updateQuery := bson.M{"_id": result.Id}
change := bson.M{"$set": bson.M{"fullname": "react-native"}}
err = collection.Update(updateQuery, change)
if err != nil {
    log.Fatal("Error updating record: ", err)
    return
}
```

### <a name="delete-a-document"></a><span data-ttu-id="83a09-146">Удаление документа</span><span class="sxs-lookup"><span data-stu-id="83a09-146">Delete a document</span></span>

<span data-ttu-id="83a09-147">Azure Cosmos DB поддерживает удаление документов JSON.</span><span class="sxs-lookup"><span data-stu-id="83a09-147">Azure Cosmos DB supports deleting JSON documents.</span></span>

```go
// Delete a document
query := bson.M{"_id": result.Id}
err = collection.Remove(query)
if err != nil {
   log.Fatal("Error deleting record: ", err)
   return
}
```
    
## <a name="run-hello-app"></a><span data-ttu-id="83a09-148">Выполните приложение hello</span><span class="sxs-lookup"><span data-stu-id="83a09-148">Run hello app</span></span>

1. <span data-ttu-id="83a09-149">Goglang, убедитесь, что в вашей GOPATH (доступен в разделе **файл**, **параметры**, **Go**, **GOPATH**) включить место hello какие hello gopkg был установлен, который является USERPROFILE\go по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="83a09-149">In Goglang, ensure that your GOPATH (available under **File**, **Settings**, **Go**, **GOPATH**) include hello location in which hello gopkg was installed, which is USERPROFILE\go by default.</span></span> 
2. <span data-ttu-id="83a09-150">Закомментируйте hello строк, удалить документ hello, 91-96 строки, чтобы могли видеть hello документа после выполнения приложения hello.</span><span class="sxs-lookup"><span data-stu-id="83a09-150">Comment out hello lines that delete hello document, lines 91-96, so that you can see hello document after running hello app.</span></span>
3. <span data-ttu-id="83a09-151">В Goglang выберите команду **Run** (Выполнить), затем нажмите кнопку **Build main.go and run** (Создать main.go и выполнить).</span><span class="sxs-lookup"><span data-stu-id="83a09-151">In Goglang, click **Run**, and then click **Run 'Build main.go and run'**.</span></span>

    <span data-ttu-id="83a09-152">приложение Hello завершается и отображается описание hello hello документ, созданный в [создать документ](#create-document).</span><span class="sxs-lookup"><span data-stu-id="83a09-152">hello app finishes and displays hello description of hello document created in [Create a document](#create-document).</span></span>
    
    ```
    Description: A framework for building native apps with React.
    
    Process finished with exit code 0
    ```

    ![Отображение выходных данных hello приложение hello Goglang](./media/create-mongodb-golang/goglang-cosmos-db.png)
    
## <a name="review-your-document-in-data-explorer"></a><span data-ttu-id="83a09-154">Просмотр документа в обозревателе данных</span><span class="sxs-lookup"><span data-stu-id="83a09-154">Review your document in Data Explorer</span></span>

<span data-ttu-id="83a09-155">Вы можете вернуться toohello Azure портала toosee документа в обозревателе данных.</span><span class="sxs-lookup"><span data-stu-id="83a09-155">Go back toohello Azure portal toosee your document in Data Explorer.</span></span>

1. <span data-ttu-id="83a09-156">Нажмите кнопку **обозреватель данных (Предварительная версия)** hello меню навигации слева разверните **golang-советы от**, **пакета**и нажмите кнопку **документов**.</span><span class="sxs-lookup"><span data-stu-id="83a09-156">Click **Data Explorer (Preview)** in hello left navigation menu, expand **golang-coach**, **package**, and then click **Documents**.</span></span> <span data-ttu-id="83a09-157">В hello **документов** щелкните hello \_идентификатор документа hello toodisplay hello правой панели.</span><span class="sxs-lookup"><span data-stu-id="83a09-157">In hello **Documents** tab, click hello \_id toodisplay hello document in hello right pane.</span></span> 

    ![Отображение hello только что созданный данных обозреватель документов](./media/create-mongodb-golang/golang-cosmos-db-data-explorer.png)
    
2. <span data-ttu-id="83a09-159">Можно работать со встроенными документа hello и нажмите кнопку **обновление** toosave его.</span><span class="sxs-lookup"><span data-stu-id="83a09-159">You can then work with hello document inline and click **Update** toosave it.</span></span> <span data-ttu-id="83a09-160">Можно также удалить документ hello или создавать новые документы или запросы.</span><span class="sxs-lookup"><span data-stu-id="83a09-160">You can also delete hello document, or create new documents or queries.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="83a09-161">Просмотрите соглашений об уровне обслуживания в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="83a09-161">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="83a09-162">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="83a09-162">Clean up resources</span></span>

<span data-ttu-id="83a09-163">Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="83a09-163">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="83a09-164">Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="83a09-164">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="83a09-165">На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="83a09-165">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83a09-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="83a09-166">Next steps</span></span>

<span data-ttu-id="83a09-167">В этом кратком руководстве вы узнали, как учетную запись Azure Cosmos DB toocreate и выполнения Golang приложения с использованием hello API для MongoDB.</span><span class="sxs-lookup"><span data-stu-id="83a09-167">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and run a Golang app using hello API for MongoDB.</span></span> <span data-ttu-id="83a09-168">Теперь можно импортировать учетной записи Cosmos DB tooyour дополнительные данные.</span><span class="sxs-lookup"><span data-stu-id="83a09-168">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="83a09-169">Импорт данных в базе данных Azure Cosmos для hello MongoDB API</span><span class="sxs-lookup"><span data-stu-id="83a09-169">Import data into Azure Cosmos DB for hello MongoDB API</span></span>](mongodb-migrate.md)
