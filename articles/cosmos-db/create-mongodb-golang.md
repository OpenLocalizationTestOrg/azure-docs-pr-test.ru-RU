---
Заголовок: aaa» Azure Cosmos DB: построение консольного приложения MongoDB API с Golang и hello портал Azure | Документы Microsoft» Описание: tooconnect tooand можно использовать образец кода Golang запросы к службам Azure Cosmos DB представляется: cosmos db Автор: диспетчер Durgaprasad Budhwani: jhubbard редактор: mimig1

MS.Service: cosmos db ms.topic: статья героя ms.date: ms.author 07/21/2017 г.: mimig
---

# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-golang-and-hello-azure-portal"></a>Azure Cosmos DB: Построение консольного приложения MongoDB API с Golang и hello портал Azure

Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт. Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД.

Краткое руководство демонстрирует, как toouse существующий [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) приложения, написанного на [Golang](https://golang.org/) и подключите базу данных Azure Cosmos tooyour базы данных, которая поддерживает MongoDB клиентских подключений.

Другими словами приложение Golang знает только подключение tooa базы данных с помощью интерфейсов API MongoDB. Он является прозрачным toohello приложение, которое hello данных хранится в Azure Cosmos DB.

## <a name="prerequisites"></a>Предварительные требования

- Подписка Azure. Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free), прежде чем начинать работу.
- [Go](https://golang.org/dl/) и базовых знаний о hello [Go](https://golang.org/) языка.
- Интегрированная среда разработки: [Gogland](https://www.jetbrains.com/go/), созданная Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) корпорации Майкрософт или [Atom](https://atom.io/). В этом руководстве используется Goglang.

<a id="create-account"></a>
## <a name="create-a-database-account"></a>Создание учетной записи базы данных

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a>Пример приложения hello клонирования

Клонирование пример приложения hello и установите пакеты необходимых hello.

1. Создайте папку с именем CosmosDBSample внутри hello GOROOT\src папку, которая является C:\Go\ по умолчанию.
2. Выполните следующую команду с помощью окно терминала git, например репозиторий git bash tooclone hello образец в папку CosmosDBSample hello hello. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-golang-getting-started.git
    ```
3.  Следующая команда tooget hello mgo пакет выполнения hello. 

    ```
    go get gopkg.in/mgo.v2
    ```

Hello [mgo](http://labix.org/mgo) драйвера (произносится как *mango*) является [MongoDB](http://www.mongodb.org/) драйвер для hello [Go языка](http://golang.org/) , реализует форматированного и проходит тщательного тестирования Выбор функций в следующих стандартных идиом Go очень простой API.

<a id="connection-string"></a>

## <a name="update-your-connection-string"></a>Обновление строки подключения

Теперь вернитесь toohello Azure портала tooget данные строки подключения и скопируйте его в приложение hello.

1. Нажмите кнопку **краткого** в левом меню навигации Здравствуйте и нажмите кнопку **других** tooview hello строка информация о соединении hello Go приложения.

2. В Goglang откройте файл main.go hello в каталоге GOROOT\CosmosDBSample hello и измените следующие строки кода, используя строку подключения hello из hello портал Azure, как показано в следующий снимок экрана приветствия hello. 

    Имя базы данных Hello — префикс hello hello **узла** значение в строку hello Azure портала подключение. Для учетной записи hello, показано в приведенном ниже рисунке hello hello имя базы данных — golang-советы от.

    ```go
    Database: "hello prefix of hello Host value in hello Azure portal",
    Username: "hello Username in hello Azure portal",
    Password: "hello Password in hello Azure portal",
    ```

    ![Краткое руководство области другие вкладки данных строки подключения hello Azure портала отображение hello](./media/create-mongodb-golang/cosmos-db-golang-connection-string.png)

3. Сохраните файл main.go hello.

## <a name="review-hello-code"></a>Проверка кода hello

Убедитесь, что происходит в файле main.go hello быстро ознакомиться. 

### <a name="connecting-hello-go-app-tooazure-cosmos-db"></a>Подключение hello tooAzure Go приложения Cosmos DB

Azure Cosmos DB поддерживает протокол SSL включен MongoDB hello. tooan tooconnect MongoDB протокол SSL включен, необходимо toodefine hello **DialServer** функционировать в [mgo. DialInfo](http://gopkg.in/mgo.v2#DialInfo)и сделать использование hello [tls. *Удаленный* ](http://golang.org/pkg/crypto/tls#Dial) функции tooperform hello соединения.

Следующий фрагмент кода Golang Hello подключается hello Go приложения с Azure Cosmos базы данных MongoDB API. Hello *DialInfo* класс содержит параметры для установки сеанса с кластером MongoDB.

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

Hello **mgo. Dial()** метод используется, когда отсутствует подключение SSL. SSL-соединением, hello **mgo. DialWithInfo()** метод является обязательным.

Экземпляр hello **DialWIthInfo {}** является объектом сеанса используется toocreate hello. После установления сеанса hello доступны hello коллекции с помощью hello, следующий фрагмент кода:

```go
collection := session.DB(“database”).C(“package”)
```

<a id="create-document"></a>

### <a name="create-a-document"></a>Создание документа

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

### <a name="query-or-read-a-document"></a>Запрос к документу или чтение документа

Azure Cosmos DB поддерживает полнофункциональные запросы к документам JSON, хранящимся в каждой коллекции. Hello следующем образце кода показан запрос, который можно запустить с документами hello в коллекции.

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


### <a name="update-a-document"></a>обновление документа;

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

### <a name="delete-a-document"></a>Удаление документа

Azure Cosmos DB поддерживает удаление документов JSON.

```go
// Delete a document
query := bson.M{"_id": result.Id}
err = collection.Remove(query)
if err != nil {
   log.Fatal("Error deleting record: ", err)
   return
}
```
    
## <a name="run-hello-app"></a>Выполните приложение hello

1. Goglang, убедитесь, что в вашей GOPATH (доступен в разделе **файл**, **параметры**, **Go**, **GOPATH**) включить место hello какие hello gopkg был установлен, который является USERPROFILE\go по умолчанию. 
2. Закомментируйте hello строк, удалить документ hello, 91-96 строки, чтобы могли видеть hello документа после выполнения приложения hello.
3. В Goglang выберите команду **Run** (Выполнить), затем нажмите кнопку **Build main.go and run** (Создать main.go и выполнить).

    приложение Hello завершается и отображается описание hello hello документ, созданный в [создать документ](#create-document).
    
    ```
    Description: A framework for building native apps with React.
    
    Process finished with exit code 0
    ```

    ![Отображение выходных данных hello приложение hello Goglang](./media/create-mongodb-golang/goglang-cosmos-db.png)
    
## <a name="review-your-document-in-data-explorer"></a>Просмотр документа в обозревателе данных

Вы можете вернуться toohello Azure портала toosee документа в обозревателе данных.

1. Нажмите кнопку **обозреватель данных (Предварительная версия)** hello меню навигации слева разверните **golang-советы от**, **пакета**и нажмите кнопку **документов**. В hello **документов** щелкните hello \_идентификатор документа hello toodisplay hello правой панели. 

    ![Отображение hello только что созданный данных обозреватель документов](./media/create-mongodb-golang/golang-cosmos-db-data-explorer.png)
    
2. Можно работать со встроенными документа hello и нажмите кнопку **обновление** toosave его. Можно также удалить документ hello или создавать новые документы или запросы.

## <a name="review-slas-in-hello-azure-portal"></a>Просмотрите соглашений об уровне обслуживания в hello портал Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Очистка ресурсов

Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги:

1. Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello. 
2. На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.

## <a name="next-steps"></a>Дальнейшие действия

В этом кратком руководстве вы узнали, как учетную запись Azure Cosmos DB toocreate и выполнения Golang приложения с использованием hello API для MongoDB. Теперь можно импортировать учетной записи Cosmos DB tooyour дополнительные данные. 

> [!div class="nextstepaction"]
> [Импорт данных в базе данных Azure Cosmos для hello MongoDB API](mongodb-migrate.md)
