---
title: "aaaJava учебников по разработке приложений с использованием Azure Cosmos DB | Документы Microsoft"
description: "Это Java веб приложения учебнике рассказывается, как toouse hello Azure Cosmos DB и hello toostore DocumentDB API и доступа к данным из приложения Java, размещенных на веб-сайтов Azure."
keywords: "Разработка приложений, учебник по базе данных, приложение java, учебник по веб-приложениям java, documentdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: java
author: dennyglee
manager: jhubbard
editor: mimig
ms.assetid: 0867a4a2-4bf5-4898-a1f4-44e3868f8725
ms.service: cosmos-db
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 08/22/2017
ms.author: denlee
ms.openlocfilehash: e073de23beb0037ee1e37b48a69e8fe7cdc3fc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-hello-documentdb-api"></a>Построение веб-приложения Java, используя Azure Cosmos DB и hello DocumentDB API
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

В этом учебнике приложения web Java показано как toouse hello [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) службы toostore и доступ к данным из приложения Java, размещенных на веб-приложениях службы приложений Azure. Из этой статьи вы узнаете:

* Как toobuild простое приложение JavaServer страниц (JSP) в Eclipse.
* Как toowork с hello Azure Cosmos DB службы с использованием hello [пакета SDK для Java Azure Cosmos DB](https://github.com/Azure/azure-documentdb-java).

Этот учебник приложения Java показано выполнение задач по toocreate веб сервера управления задачами приложения, которое позволяет вам toocreate, получение и пометить завершена, как показано в hello после изображения. Каждая из задач hello в список ToDo hello хранятся в виде документов JSON в базе данных Azure Cosmos.

![Приложение My ToDo List на Java](./media/documentdb-java-application/image1.png)

> [!TIP]
> В данном учебнике по разработке приложения предполагается, что у вас имеется некоторый опыт использования Java. Новый tooJava или hello [готовности к установке средства](#Prerequisites), рекомендуется загрузить полный hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) проекта из GitHub и построения с помощью [hello инструкции в конце hello объекта статья](#GetProject). После построения, можно просмотреть hello статьи toogain и подробные сведения о кода hello в контексте hello hello проекта.  
> 
> 

## <a id="Prerequisites"></a>Необходимые условия для изучения этого учебника по разработке веб-приложения Java
Перед началом этого учебника разработки приложения, необходимо иметь следующие hello.

* Активная учетная запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. на странице [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/pricing/free-trial/).

    ИЛИ

    Локальная установка hello [DB эмулятор Azure Cosmos](local-emulator.md).
* [Комплект разработчика Java (JDK 7 +)](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
* [Интегрированная среда разработки Eclipse для разработчиков Java EE.](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [Открытый веб-сайт Azure со средой выполнения Java (например, Tomcat или Jetty).](../app-service-web/web-sites-java-get-started.md)

При установке этих средств для hello первый раз, coreservlets.com предоставляет пошаговое руководство процесса установки hello раздела hello быстрого запуска их [учебника: Установка TomCat7 и его использование с Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) статьи.

## <a id="CreateDB"></a>Шаг 1. Создание учетной записи Azure Cosmos DB
Давайте сначала создадим учетную запись Azure Cosmos DB. Если уже есть учетная запись, или при использовании hello эмулятор DB Cosmos Azure для этого учебника, можно пропустить слишком[шаг 2: Создание приложения hello Java JSP](#CreateJSP).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <a id="CreateJSP"></a>Шаг 2: Создание приложения hello Java JSP
hello toocreate JSP приложения:

1. Во-первых, необходимо создать проект Java. В меню Eclipse выберите **File** (Файл), щелкните **New** (Создать), а затем выберите **Dynamic Web Project** (Динамический веб-проект). Если вы не видите **динамический веб-проект** в списке доступных проектов, hello следующие: щелкните **файл**, нажмите кнопку **New**, нажмите кнопку **проекта**..., разверните **Web**, нажмите кнопку **динамический веб-проект**и нажмите кнопку **Далее**.
   
    ![Разработка приложений JSP Java](./media/documentdb-java-application/image10.png)
2. Введите имя проекта в hello **имя проекта** поле, а в hello **целевой среды выполнения** раскрывающееся меню, при необходимости выберите значение (например, Apache Tomcat v7.0) и нажмите кнопку **Готово**. Выбор целевой среды выполнения включает toorun вы проекте локально через Eclipse.
3. В Eclipse в представлении обозревателя проектов hello, разверните проект. Щелкните правой кнопкой мыши **WebContent**, выберите **Создать**, затем щелкните **JSP File** (JSP-файл).
4. В hello **Создание JSP-файла** диалоговое окно, имя файла hello **index.jsp**. Сохранить hello родительскую папку как **WebContent**, как показано в hello следующие иллюстрации и нажмите кнопку **Далее**.
   
    ![Создание файла JSP — учебник по разработке веб-приложений Java](./media/documentdb-java-application/image11.png)
5. В hello **Выбор шаблона JSP** диалоговом выберите время проведения hello **новый JSP-файл (html)**, а затем нажмите кнопку **Готово**.
6. При открытии файла index.jsp hello в Eclipse добавьте текст toodisplay **Здравствуй, мир!** в существующих hello <body> элемента. Обновленный <body> содержимое должно выглядеть hello, следующий код:
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. Сохраните файл index.jsp hello.
8. Если значение целевой среды выполнения на шаге 2, можно щелкнуть **проекта** и затем **запуска** toorun приложения JSP локально:
   
    ![Привет, мир! — учебник по разработке приложений Java](./media/documentdb-java-application/image12.png)

## <a id="InstallSDK"></a>Шаг 3: Установка пакета DocumentDB Java SDK hello
Hello простым способом toopull в DocumentDB Java SDK hello и его зависимостей выполняется с помощью [Apache Maven](http://maven.apache.org/).

toodo это, необходимо будет tooconvert проекта maven tooa проекта, выполнив следующие шаги hello:

1. Щелкните правой кнопкой мыши проект в обозревателе проектов hello, щелкните **Настройка**, нажмите кнопку **преобразовать проект tooMaven**.
2. В hello **создать новый POM** , примите значения по умолчанию hello и выберите команду **Готово**.
3. В **обозревателя проектов**, откройте файл pom.xml hello.
4. На hello **зависимости** hello на вкладке **зависимости** области, нажмите кнопку **добавить**.
5. В hello **выберите зависимостей** окне hello следующие:
   
   * В hello **идентификатор группы** введите com.microsoft.azure.
   * В hello **идентификатор артефакта** введите azure documentdb.
   * В hello **версии** введите 1.5.1.
     
   ![Установка пакета DocumentDB Java Application SDK](./media/documentdb-java-application/image13.png)
     
   * Или добавить зависимость hello XML для группы кода и идентификатор артефакта непосредственно toohello pom.xml через текстовый редактор:
     
        <dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency>
6. Нажмите кнопку **ОК** и Maven установит hello DocumentDB Java SDK.
7. Сохраните файл pom.xml hello.

## <a id="UseService"></a>Шаг 4: Использование служб Azure Cosmos DB hello в приложение Java
1. Во-первых определим hello объекта TodoItem в TodoItem.java:
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    В этом проекте мы используем [Lombok проекта](http://projectlombok.org/) toogenerate hello конструктор, методы получения, задания и конструктор. Кроме того, можно вручную записать этот код или он сформирован hello интегрированной среды разработки.
2. Служба Azure Cosmos DB tooinvoke hello, необходимо создать экземпляр нового **DocumentClient**. Как правило, это лучший hello tooreuse **DocumentClient** — вместо создания нового клиента для каждого последующего запроса, чем. Мы повторно использовать hello клиента путем заключения клиента hello в **DocumentClientFactory**. В DocumentClientFactory.java, необходимо получить toopaste hello URI и ПЕРВИЧНОГО ключа значение был сохранен в буфер обмена tooyour в [шаг 1](#CreateDB). Замените [YOUR\_ENDPOINT\_HERE] на универсальный код ресурса, а [YOUR\_KEY\_HERE] — на первичный ключ.
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. Теперь давайте создадим tooabstract объекта доступа к данным (DAO), сохранение нашей tooAzure элементы ToDo Cosmos DB.
   
    Чтобы элементов ToDo toosave tooa коллекции, hello клиенту tooknow какие базы данных и коллекция toopersist слишком (ссылается ссылки SELF-Link). Как правило, это лучший hello toocache базы данных и коллекции, если это возможно дополнительных циклов приема-передачи tooavoid toohello-базы данных.
   
    Hello следующий код показывает, как tooretrieve наши базы данных и коллекции, если он существует, или создать новый, если он не существует:
   
        public class DocDbDao implements TodoDao {
            // hello name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // hello name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // hello Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for hello database object, so we don't have tooquery for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for hello collection object, so we don't have tooquery for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get hello database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache hello database object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create hello database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get hello collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache hello collection object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create hello collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. Hello следующим шагом является toowrite некоторые hello toopersist кода TodoItems toohello коллекции. В этом примере мы будем использовать [Gson](https://code.google.com/p/google-gson/) tooserialize и десериализацию документы tooJSON TodoItem простых старых объектов Java (POJOs).
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize hello TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate hello document as a TodoItem for retrieval (so that we can
            // store multiple entity types in hello collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist hello document using hello DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. Подобно используемым базам данных Azure Cosmos DB и коллекциям, документы также связываются с помощью самостоятельных ссылок. Здравствуйте, следующие вспомогательные функции позволяет нам получить документы по другой атрибут (например, «id»), а не ссылкой:
   
        private Document getDocumentById(String id) {
            // Retrieve hello document using hello DocumentClient.
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.id='" + id + "'", null)
                    .getQueryIterable().toList();
   
            if (documentList.size() > 0) {
                return documentList.get(0);
            } else {
                return null;
            }
        }
6. Мы можно использовать вспомогательный метод hello в шаге 5 tooretrieve документ TodoItem JSON по идентификатору и затем десериализовать tooa POJO:
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve hello document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize hello document in tooa TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. Также можно использовать hello DocumentClient tooget коллекции или список TodoItems DocumentDB SQL с помощью:
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve hello TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize hello documents in tooTodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. Существует много способов tooupdate документ с hello DocumentClient. В нашем приложения списка задач нам нужно будет tootoggle toobe ли TodoItem. Это можно сделать путем обновления атрибута «выполнено» hello в документе hello:
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve hello document from hello database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update hello document as a JSON document directly.
            // For more complex operations - you could de-serialize hello document in
            // tooa POJO, update hello POJO, and then re-serialize hello POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace hello updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. Наконец мы хотим toodelete возможность hello TodoItem из нашего списка. toodo это, можно использовать вспомогательный метод hello мы писали ранее tooretrieve hello ссылкой и затем сообщить toodelete hello клиента он:
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers toodocuments by self link rather than id.
   
            // Query for hello document tooretrieve hello self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete hello document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <a id="Wire"></a>Шаг 5: Вместе подключения hello остальной части hello проекта разработки приложения Java
Теперь, когда мы закончено hello fun bits - осталось — это быстрый пользовательский интерфейс toobuild и подключить tooour DAO.

1. Во-первых давайте начнем с созданием нашей DAO toocall контроллера:
   
        public class TodoItemController {
            public static TodoItemController getInstance() {
                if (todoItemController == null) {
                    todoItemController = new TodoItemController(TodoDaoFactory.getDao());
                }
                return todoItemController;
            }
   
            private static TodoItemController todoItemController;
   
            private final TodoDao todoDao;
   
            TodoItemController(TodoDao todoDao) {
                this.todoDao = todoDao;
            }
   
            public TodoItem createTodoItem(@NonNull String name,
                    @NonNull String category, boolean isComplete) {
                TodoItem todoItem = TodoItem.builder().name(name).category(category)
                        .complete(isComplete).build();
                return todoDao.createTodoItem(todoItem);
            }
   
            public boolean deleteTodoItem(@NonNull String id) {
                return todoDao.deleteTodoItem(id);
            }
   
            public TodoItem getTodoItemById(@NonNull String id) {
                return todoDao.readTodoItem(id);
            }
   
            public List<TodoItem> getTodoItems() {
                return todoDao.readTodoItems();
            }
   
            public TodoItem updateTodoItem(@NonNull String id, boolean isComplete) {
                return todoDao.updateTodoItem(id, isComplete);
            }
        }
   
    В более сложных приложений hello контроллер может разместить сложной бизнес-логики поверх hello DAO.
2. Далее мы создадим сервлетов tooroute HTTP-запросы toohello контроллер:
   
        public class TodoServlet extends HttpServlet {
            // API Keys
            public static final String API_METHOD = "method";
   
            // API Methods
            public static final String CREATE_TODO_ITEM = "createTodoItem";
            public static final String GET_TODO_ITEMS = "getTodoItems";
            public static final String UPDATE_TODO_ITEM = "updateTodoItem";
   
            // API Parameters
            public static final String TODO_ITEM_ID = "todoItemId";
            public static final String TODO_ITEM_NAME = "todoItemName";
            public static final String TODO_ITEM_CATEGORY = "todoItemCategory";
            public static final String TODO_ITEM_COMPLETE = "todoItemComplete";
   
            public static final String MESSAGE_ERROR_INVALID_METHOD = "{'error': 'Invalid method'}";
   
            private static final long serialVersionUID = 1L;
            private static final Gson gson = new Gson();
   
            @Override
            protected void doGet(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
   
                String apiResponse = MESSAGE_ERROR_INVALID_METHOD;
   
                TodoItemController todoItemController = TodoItemController
                        .getInstance();
   
                String id = request.getParameter(TODO_ITEM_ID);
                String name = request.getParameter(TODO_ITEM_NAME);
                String category = request.getParameter(TODO_ITEM_CATEGORY);
                boolean isComplete = StringUtils.equalsIgnoreCase("true",
                        request.getParameter(TODO_ITEM_COMPLETE)) ? true : false;
   
                switch (request.getParameter(API_METHOD)) {
                case CREATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.createTodoItem(name,
                            category, isComplete));
                    break;
                case GET_TODO_ITEMS:
                    apiResponse = gson.toJson(todoItemController.getTodoItems());
                    break;
                case UPDATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.updateTodoItem(id,
                            isComplete));
                    break;
                default:
                    break;
                }
   
                response.getWriter().println(apiResponse);
            }
   
            @Override
            protected void doPost(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
                doGet(request, response);
            }
        }
3. Он понадобится toohello веб-интерфейса пользователя toodisplay пользователя. Давайте перепишите hello index.jsp, что созданный ранее:
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding toobody for fixed nav bar */
            body {
              padding-top: 50px;
            }
          </style>
        </head>
        <body>
          <!-- Nav Bar -->
          <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
            <div class="container">
              <div class="navbar-header">
                <a class="navbar-brand" href="#">My Tasks</a>
              </div>
            </div>
          </div>
   
          <!-- Body -->
          <div class="container">
            <h1>My ToDo List</h1>
   
            <hr/>
   
            <!-- hello ToDo List -->
            <div class = "todoList">
              <table class="table table-bordered table-striped" id="todoItems">
                <thead>
                  <tr>
                    <th>Name</th>
                    <th>Category</th>
                    <th>Complete</th>
                  </tr>
                </thead>
                <tbody>
                </tbody>
              </table>
   
              <!-- Update Button -->
              <div class="todoUpdatePanel">
                <form class="form-horizontal" role="form">
                  <button type="button" class="btn btn-primary">Update Tasks</button>
                </form>
              </div>
   
            </div>
   
            <hr/>
   
            <!-- Item Input Form -->
            <div class="todoForm">
              <form class="form-horizontal" role="form">
                <div class="form-group">
                  <label for="inputItemName" class="col-sm-2">Task Name</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemName" placeholder="Enter name">
                  </div>
                </div>
   
                <div class="form-group">
                  <label for="inputItemCategory" class="col-sm-2">Task Category</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemCategory" placeholder="Enter category">
                  </div>
                </div>
   
                <button type="button" class="btn btn-primary">Add Task</button>
              </form>
            </div>
   
          </div>
   
          <!-- Placed at hello end of hello document so hello pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. И наконец, написание некоторые клиентские hello tootie JavaScript веб-интерфейсом и hello сервлетов вместе.
   
        var todoApp = {
          /*
           * API methods toocall Java backend.
           */
          apiEndpoint: "api",
   
          createTodoItem: function(name, category, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "createTodoItem",
                "todoItemName": name,
                "todoItemCategory": category,
                "todoItemComplete": isComplete
              },
              function(data) {
                var todoItem = data;
                todoApp.addTodoItemToTable(todoItem.id, todoItem.name, todoItem.category, todoItem.complete);
              },
              "json");
          },
   
          getTodoItems: function() {
            $.post(todoApp.apiEndpoint, {
                "method": "getTodoItems"
              },
              function(data) {
                var todoItemArr = data;
                $.each(todoItemArr, function(index, value) {
                  todoApp.addTodoItemToTable(value.id, value.name, value.category, value.complete);
                });
              },
              "json");
          },
   
          updateTodoItem: function(id, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "updateTodoItem",
                "todoItemId": id,
                "todoItemComplete": isComplete
              },
              function(data) {},
              "json");
          },
   
          /*
           * UI Methods
           */
          addTodoItemToTable: function(id, name, category, isComplete) {
            var rowColor = isComplete ? "active" : "warning";
   
            todoApp.ui_table().append($("<tr>")
              .append($("<td>").text(name))
              .append($("<td>").text(category))
              .append($("<td>")
                .append($("<input>")
                  .attr("type", "checkbox")
                  .attr("id", id)
                  .attr("checked", isComplete)
                  .attr("class", "isComplete")
                ))
              .addClass(rowColor)
            );
          },
   
          /*
           * UI Bindings
           */
          bindCreateButton: function() {
            todoApp.ui_createButton().click(function() {
              todoApp.createTodoItem(todoApp.ui_createNameInput().val(), todoApp.ui_createCategoryInput().val(), false);
              todoApp.ui_createNameInput().val("");
              todoApp.ui_createCategoryInput().val("");
            });
          },
   
          bindUpdateButton: function() {
            todoApp.ui_updateButton().click(function() {
              // Disable button temporarily.
              var myButton = $(this);
              var originalText = myButton.text();
              $(this).text("Updating...");
              $(this).prop("disabled", true);
   
              // Call api tooupdate todo items.
              $.each(todoApp.ui_updateId(), function(index, value) {
                todoApp.updateTodoItem(value.name, value.value);
                $(value).remove();
              });
   
              // Re-enable button.
              setTimeout(function() {
                myButton.prop("disabled", false);
                myButton.text(originalText);
              }, 500);
            });
          },
   
          bindUpdateCheckboxes: function() {
            todoApp.ui_table().on("click", ".isComplete", function(event) {
              var checkboxElement = $(event.currentTarget);
              var rowElement = $(event.currentTarget).parents('tr');
              var id = checkboxElement.attr('id');
              var isComplete = checkboxElement.is(':checked');
   
              // Toggle table row color
              if (isComplete) {
                rowElement.addClass("active");
                rowElement.removeClass("warning");
              } else {
                rowElement.removeClass("active");
                rowElement.addClass("warning");
              }
   
              // Update hidden inputs for update panel.
              todoApp.ui_updateForm().children("input[name='" + id + "']").remove();
   
              todoApp.ui_updateForm().append($("<input>")
                .attr("type", "hidden")
                .attr("class", "updateComplete")
                .attr("name", id)
                .attr("value", isComplete));
   
            });
          },
   
          /*
           * UI Elements
           */
          ui_createNameInput: function() {
            return $(".todoForm #inputItemName");
          },
   
          ui_createCategoryInput: function() {
            return $(".todoForm #inputItemCategory");
          },
   
          ui_createButton: function() {
            return $(".todoForm button");
          },
   
          ui_table: function() {
            return $(".todoList table tbody");
          },
   
          ui_updateButton: function() {
            return $(".todoUpdatePanel button");
          },
   
          ui_updateForm: function() {
            return $(".todoUpdatePanel form");
          },
   
          ui_updateId: function() {
            return $(".todoUpdatePanel .updateComplete");
          },
   
          /*
           * Install hello TodoApp
           */
          install: function() {
            todoApp.bindCreateButton();
            todoApp.bindUpdateButton();
            todoApp.bindUpdateCheckboxes();
   
            todoApp.getTodoItems();
          }
        };
   
        $(document).ready(function() {
          todoApp.install();
        });
5. Отлично! Теперь осталось — приложение hello tootest. Запустите приложение hello локально и добавьте несколько элементов Todo, заполнив имя элемента hello и категории команду **добавить задачу**.
6. После отображения элемента hello, можно обновить ли это будет выполнено при снятии флажка hello и щелкнув **обновление задачи**.

## <a id="Deploy"></a>Шаг 6: Развертывание вашей tooAzure приложения Java веб-сайтов
Веб-сайты Azure упрощают развертывание приложений Java с помощью простого экспорта приложения в виде WAR-файла либо с помощью загрузки через систему управления версиями (например, GIT) или через клиент FTP.

1. tooexport приложения как WAR-файл, щелкните правой кнопкой мыши проект в **обозревателя проектов**, нажмите кнопку **Экспорт**, а затем нажмите кнопку **WAR-файл**.
2. В hello **Экспорт WAR** окне hello следующие:
   
   * В hello Web проекта введите documentdb-java пример azure.
   * В поле назначения hello выберите целевой toosave hello WAR-файл.
   * Нажмите кнопку **Готово**
3. Теперь, когда вы располагаете WAR-файл в, можно просто передать его tooyour веб-сайта Azure **веб-приложений** каталога. Инструкции по передаче файла hello см. в разделе [добавить tooAzure приложения Java веб-приложений служб приложения](../app-service-web/web-sites-java-add-app.md).
   
    После hello WAR-файл каталога toohello загруженного веб-приложений, среда выполнения hello обнаружит добавили его и автоматически загружает его.
4. tooview ГП, перейдите toohttp://YOUR\_САЙТА\_NAME.azurewebsites.net/azure-java-sample/ и начать добавлять задач!

## <a id="GetProject"></a>Получить проект hello из GitHub
Все образцы hello в этом учебнике, включаются в hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) проекта на GitHub. проект todo tooimport hello в Eclipse, убедитесь, имеются hello программного обеспечения и ресурсах, перечисленных в hello [необходимые компоненты](#Prerequisites) статьи, а затем hello следующие:

1. Установите [проект Lombok](http://projectlombok.org/). Lombok — используется toogenerate конструкторы, методы получения, задания в проект hello. После загрузки файла lombok.jar hello, дважды щелкните его tooinstall его или установите его из командной строки hello.
2. Если Eclipse открыт, закройте его и перезапустите его tooload Lombok.
3. В Eclipse на hello **файл** меню, нажмите кнопку **импорта**.
4. В hello **импорта** окно, нажмите кнопку **Git**, нажмите кнопку **проекты из Git**, а затем нажмите кнопку **Далее**.
5. На hello **Выбор источника репозитория** щелкните **клон URI**.
6. На hello **исходный репозиторий Git** экрана в hello **URI** введите https://github.com/Azure-Samples/java-todo-app.git и нажмите кнопку **Далее**.
7. На hello **ветвь выбора** экране, убедитесь, что **master** выбран и нажмите кнопку **Далее**.
8. На hello **локальной целевой** щелкните **Обзор** tooselect папке, можно скопировать hello репозитория, а затем нажмите кнопку **Далее**.
9. На hello **toouse мастер импорта проектов выберите** экране, убедитесь, что **импортировать существующие проекты** выбран и нажмите кнопку **Далее**.
10. На hello **импорта проектов** экрана, отмените выбор hello **DocumentDB** проекта, а затем нажмите кнопку **Готово**. Hello DocumentDB проект содержит hello Azure Cosmos DB Java пакета SDK, который мы будем добавлять как зависимость.
11. В **обозревателя проектов**перейдите tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java и замените значения узла и MASTER_KEY hello hello URI и первичный ключ для вашей учетной записи Azure Cosmos DB, а затем сохранить файл hello. Дополнительные сведения см. в инструкции [Шаг 1. Создание учетной записи базы данных Azure Cosmos DB](#CreateDB).
12. В **обозревателя проектов**, щелкните правой кнопкой мыши hello **-documentdb-java пример azure**, нажмите кнопку **путь построения**, а затем нажмите кнопку **настроить путь построения**.
13. На hello **путь построения Java** экрана приветствия правой панели выберите hello **библиотеки** , а затем щелкните **добавить внешний JAR-файлов**. Перейдите toohello расположение файла lombok.jar hello и нажмите кнопку **откройте**, а затем нажмите кнопку **ОК**.
14. Используйте шаг 12 tooopen hello **свойства** окно и hello левой панели нажмите кнопку **целевых сред выполнения**.
15. На hello **целевых сред выполнения** щелкните **New**выберите **v7.0 Apache Tomcat**и нажмите кнопку **ОК**.
16. Используйте шаг 12 tooopen hello **свойства** окно и hello левой панели нажмите кнопку **аспекты проекта**.
17. На hello **аспекты проекта** выберите **динамических веб-модуля** и **Java**и нажмите кнопку **ОК**.
18. На hello **серверы** hello нижней части экрана приветствия щелкните правой кнопкой мыши **Tomcat v7.0 Server в localhost** и нажмите кнопку **добавлять и удалять**.
19. На hello **добавлять и удалять** окна, переместите **-documentdb-java пример azure** toohello **настроенный** , а затем щелкните **Готово**.
20. В hello **серверы** щелкните правой кнопкой мыши **Tomcat v7.0 Server в localhost**, а затем нажмите кнопку **перезапустите**.
21. В браузере перейдите toohttp://localhost:8080 / azure-documentdb-java образец и и приступите к добавлению tooyour списка задач. Обратите внимание, что если вы изменили свои значения порта по умолчанию, измените выбранное значение toohello 8080.
22. toodeploy tooan вашего проекта веб-сайте Azure в разделе [шаг 6. Развертывание вашего приложения tooAzure веб-сайтов](#Deploy).

[1]: media/documentdb-java-application/keys.png
