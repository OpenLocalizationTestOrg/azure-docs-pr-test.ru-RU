---
title: "aaaBuild Node.js веб-приложения для Azure Cosmos DB | Документы Microsoft"
description: "Этот учебник Node.js более подробно рассматривается как toouse Microsoft Azure Cosmos DB toostore и доступ к данным из Node.js Express веб-приложения, размещенного на веб-сайтов Azure."
keywords: "Разработка приложений, учебник по базе данных, изучение node.js, учебник по node.js"
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 9da9e63b-e76a-434e-96dd-195ce2699ef3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: mimig
ms.openlocfilehash: 31194dccf37eef69d2219b0d8328a88d434f79b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="_Toc395783175"></a>Создание веб-приложения Node.js с использованием Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

Этот учебник Node.js показано, как toouse Azure Cosmos DB и DocumentDB API toostore и доступ к данным из Node.js Express приложения hello, размещенных на веб-сайтов Azure. Вы создадите простое веб-приложение для управления задачами (приложение ToDo), позволяющее создавать, извлекать и выполнять задачи. задачи Hello хранятся в виде документов JSON в базе данных Azure Cosmos. Этот учебник поможет выполнить hello Создание и развертывание приложения hello и объясняется, что происходит на каждого фрагмента кода.

![Снимок экрана: hello Мои приложения Todo List в этом учебнике Node.js](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

Нет времени toocomplete hello учебника и просто нужно tooget hello законченное решение? Это не представляет проблему, можно получить полный пример решения hello из [GitHub][GitHub]. Только чтение hello [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) файл инструкции как toorun hello приложения.

## <a name="_Toc395783176"></a>Предварительные требования
> [!TIP]
> Этот учебник по Node.js разработан для читателей, обладающих определенным опытом использования Node.js и веб-сайтов Azure.
> 
> 

Перед выполнением инструкции hello в этой статье, следует убедиться, что имеется следующее hello:

* Активная учетная запись Azure. Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).

   ИЛИ

   Локальная установка hello [DB эмулятор Azure Cosmos](local-emulator.md) (Windows).
* [Node.js][Node.js] версии 0.10.29 или более поздней.
* [Генератор Express](http://www.expressjs.com/starter/generator.html) (его можно установить через `npm install express-generator -g`).
* [Git][Git].

## <a name="_Toc395637761"></a>Шаг 1. Создание учетной записи базы данных Azure Cosmos DB
Давайте сначала создадим учетную запись Azure Cosmos DB. Если уже есть учетная запись, или при использовании hello эмулятор DB Cosmos Azure для этого учебника, можно пропустить слишком[шаг 2: Создание нового приложения Node.js](#_Toc395783178).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <a name="_Toc395783178"></a>Шаг 2. Создание приложения Node.js
Теперь давайте узнать toocreate базовый проект Hello World Node.js с помощью hello [Express](http://expressjs.com/) framework.

1. Откройте избранные терминала, например hello Node.js командной строки.
2. Перейдите в каталог toohello, в которой требуется новое приложение hello toostore.
3. Использовать новое приложение вызвало toogenerate express генератор hello **todo**.
   
        express todo
4. Откройте новый каталог **todo** и установите зависимости.
   
        cd todo
        npm install
5. Запустите новое приложение.
   
        npm start
6. Можно просмотреть нового приложения, навигация обозревателя слишком[http://localhost:3000](http://localhost:3000).
   
    ![Дополнительные сведения Node.js — снимок экрана приветствия приложения Hello World в окне браузера](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    Затем toostop hello приложения, нажмите клавиши CTRL + C в окне терминала hello и нажмите кнопку **y** tooterminate hello пакетного задания.

## <a name="_Toc395783179"></a>Шаг 3. Установка дополнительных модулей
Hello **package.json** файл является одним из hello файлы, созданные в корневой hello hello проекта. Этот файл содержит список дополнительных модулей, необходимых для приложения Node.js. Позже при развертывании этого приложения tooAzure веб-сайтов, этот файл является используется toodetermine toobe необходимость какие модули на Azure toosupport приложение установлено. По-прежнему необходимы tooinstall две дополнительные пакеты для этого учебника.

1. В hello терминалов, установите hello **async** модуль через npm.
   
        npm install async --save
2. Установка hello **documentdb** модуль через npm. Это модуль hello, где происходит все magic hello Azure Cosmos DB.
   
        npm install documentdb --save
3. Быстрая проверка hello **package.json** файл приложения hello должны показывать hello дополнительных модулей. Этот файл будет сообщить Azure, какие пакеты toodownload и устанавливать при запуске приложения. Она должна иметь вид hello приведенном ниже примере.
   
        {
          "name": "todo",
          "version": "0.0.0",
          "private": true,
          "scripts": {
            "start": "node ./bin/www"
          },
          "dependencies": {
            "async": "^2.1.4",
            "body-parser": "~1.15.2",
            "cookie-parser": "~1.4.3",
            "debug": "~2.2.0",
            "documentdb": "^1.10.0",
            "express": "~4.14.0",
            "jade": "~1.11.0",
            "morgan": "~1.7.0",
            "serve-favicon": "~2.3.0"
          }
        }
   
    Это сообщает Node (и позже Azure), что ваше приложение зависит от указанных дополнительных модулей.

## <a name="_Toc395783180"></a>Шаг 4: Использование службы Azure Cosmos DB hello в приложении узла
Который берет на себя все hello начальной установки и конфигурации, теперь давайте get вниз toowhy мы здесь, и это toowrite некоторые код с использованием Azure Cosmos DB.

### <a name="create-hello-model"></a>Создание модели hello
1. В каталоге проекта hello, создайте новый каталог с именем **моделей** в hello одной папке с файлом package.json hello.
2. В hello **моделей** каталога, создайте новый файл с именем **taskDao.js**. Этот файл будет содержать hello модель для hello задачам, созданным нашего приложения.
3. В hello же **моделей** каталога, создайте еще один новый файл с именем **docdbUtils.js**. Этот файл будет содержать некоторый полезный многократно используемый код, который будет задействован на протяжении нашего приложения. 
4. Копирования hello следующий код в слишком**docdbUtils.js**
   
        var DocumentDBClient = require('documentdb').DocumentClient;
   
        var DocDBUtils = {
            getOrCreateDatabase: function (client, databaseId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id= @id',
                    parameters: [{
                        name: '@id',
                        value: databaseId
                    }]
                };
   
                client.queryDatabases(querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        if (results.length === 0) {
                            var databaseSpec = {
                                id: databaseId
                            };
   
                            client.createDatabase(databaseSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            },
   
            getOrCreateCollection: function (client, databaseLink, collectionId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id=@id',
                    parameters: [{
                        name: '@id',
                        value: collectionId
                    }]
                };               
   
                client.queryCollections(databaseLink, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {        
                        if (results.length === 0) {
                            var collectionSpec = {
                                id: collectionId
                            };
   
                            client.createCollection(databaseLink, collectionSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            }
        };
   
        module.exports = DocDBUtils;
   
5. Сохраните и закройте hello **docdbUtils.js** файла.
6. В начале hello hello **taskDao.js** файл, добавьте следующий код tooreference hello hello **DocumentDBClient** и hello **docdbUtils.js** созданных ранее:
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. Далее необходимо добавить код toodefine и экспорт hello объекта задачи. Это отвечает за инициализации объекта нашей задачи и настройка hello базы данных и мы будем использовать коллекции документов.
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. Добавьте hello следующие дополнительные методы toodefine кода hello объекта задачи, которые позволяют взаимодействия с данными, хранящимися в базе данных Azure Cosmos.
   
        TaskDao.prototype = {
            init: function (callback) {
                var self = this;
   
                docdbUtils.getOrCreateDatabase(self.client, self.databaseId, function (err, db) {
                    if (err) {
                        callback(err);
                    } else {
                        self.database = db;
                        docdbUtils.getOrCreateCollection(self.client, self.database._self, self.collectionId, function (err, coll) {
                            if (err) {
                                callback(err);
   
                            } else {
                                self.collection = coll;
                            }
                        });
                    }
                });
            },
   
            find: function (querySpec, callback) {
                var self = this;
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results);
                    }
                });
            },
   
            addItem: function (item, callback) {
                var self = this;
   
                item.date = Date.now();
                item.completed = false;
   
                self.client.createDocument(self.collection._self, item, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, doc);
                    }
                });
            },
   
            updateItem: function (itemId, callback) {
                var self = this;
   
                self.getItem(itemId, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        doc.completed = true;
   
                        self.client.replaceDocument(doc._self, doc, function (err, replaced) {
                            if (err) {
                                callback(err);
   
                            } else {
                                callback(null, replaced);
                            }
                        });
                    }
                });
            },
   
            getItem: function (itemId, callback) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id = @id',
                    parameters: [{
                        name: '@id',
                        value: itemId
                    }]
                };
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results[0]);
                    }
                });
            }
        };
9. Сохраните и закройте hello **taskDao.js** файла. 

### <a name="create-hello-controller"></a>Создание контроллера hello
1. В hello **маршруты** каталог проекта, создайте новый файл с именем **tasklist.js**. 
2. Добавьте следующий код слишком hello**tasklist.js**. Это загружает hello DocumentDBClient и async модули, в которых используются **tasklist.js**. Это также определены hello **TaskList** функции, которая передается экземпляр hello **задачи** объекта было определено ранее:
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. Продолжайте добавлять toohello **tasklist.js** файла путем добавления методов hello используется слишком**showTasks addTask**, и **completeTasks**:
   
        TaskList.prototype = {
            showTasks: function (req, res) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.completed=@completed',
                    parameters: [{
                        name: '@completed',
                        value: false
                    }]
                };
   
                self.taskDao.find(querySpec, function (err, items) {
                    if (err) {
                        throw (err);
                    }
   
                    res.render('index', {
                        title: 'My ToDo List ',
                        tasks: items
                    });
                });
            },
   
            addTask: function (req, res) {
                var self = this;
                var item = req.body;
   
                self.taskDao.addItem(item, function (err) {
                    if (err) {
                        throw (err);
                    }
   
                    res.redirect('/');
                });
            },
   
            completeTask: function (req, res) {
                var self = this;
                var completedTasks = Object.keys(req.body);
   
                async.forEach(completedTasks, function taskIterator(completedTask, callback) {
                    self.taskDao.updateItem(completedTask, function (err) {
                        if (err) {
                            callback(err);
                        } else {
                            callback(null);
                        }
                    });
                }, function goHome(err) {
                    if (err) {
                        throw err;
                    } else {
                        res.redirect('/');
                    }
                });
            }
        };
4. Сохраните и закройте hello **tasklist.js** файла.

### <a name="add-configjs"></a>Добавление config.js
1. В каталоге проекта создайте новый файл с именем **config.js**.
2. Добавьте hello следующие слишком**config.js**. Он определяет значения и параметры конфигурации, необходимые нашему приложению.
   
        var config = {}
   
        config.host = process.env.HOST || "[hello URI value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[hello PRIMARY KEY value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. В hello **config.js** файла обновления hello значения узла и значениями hello в колонке hello ключи учетной записи Azure Cosmos DB hello AUTH_KEY [портал Microsoft Azure](https://portal.azure.com).
4. Сохраните и закройте hello **config.js** файла.

### <a name="modify-appjs"></a>Изменение app.js
1. В каталоге проекта hello, откройте hello **в файле app.js** файл. Этот файл был создан ранее, при создании веб-приложения hello, экспресс-выпуск.
2. Добавьте следующий код toohello вверху hello **в файле app.js**
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. Этот код определяет hello конфигурации файла toobe использовать, после чего выполняется tooread значений из этого файла в некоторые переменные, которые скоро будут использоваться.
4. Замените следующие две строки в hello **в файле app.js** файла:
   
        app.use('/', index);
        app.use('/users', users); 
   
      с hello, следующий фрагмент кода:
   
        var docDbClient = new DocumentDBClient(config.host, {
            masterKey: config.authKey
        });
        var taskDao = new TaskDao(docDbClient, config.databaseId, config.collectionId);
        var taskList = new TaskList(taskDao);
        taskDao.init();
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
        app.set('view engine', 'jade');
5. Эти строки определяют новый экземпляр нашей **TaskDao** объект с новой tooAzure подключения Cosmos DB (с использованием значений hello считываться hello **config.js**), инициализировать объект задачи hello, а затем привязать действий формы toomethods на нашем **TaskList** контроллера. 
6. Наконец, сохраните и закройте hello **в файле app.js** файл, почти готово.

## <a name="_Toc395783181"></a>Шаг 5. Построение пользовательского интерфейса
Теперь давайте рассмотрим наши внимания toobuilding hello пользовательского интерфейса, фактически взаимодействие пользователя с помощью нашего приложения. Здравствуйте, экспресс-выпуск приложения мы создали использует **Jade** как обработчик представлений hello. Дополнительные сведения о Jade см. слишком[http://jade-lang.com/](http://jade-lang.com/).

1. Hello **layout.jade** файла в hello **представления** каталог используется как глобальный шаблон для других **.jade** файлов. На этом этапе вы измените его toouse [Twitter начальной загрузки](https://github.com/twbs/bootstrap), который — это набор средств, который позволяет легко toodesign работы с низким приоритетом привлекательных веб-сайта. 
2. Откройте hello **layout.jade** файл найден в hello **представления** папки и заменить содержимое hello hello следующее:

    ```
    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body
        nav.navbar.navbar-inverse.navbar-fixed-top
          div.navbar-header
            a.navbar-brand(href='#') My Tasks
        block content
        script(src='//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js')
        script(src='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js')
    ```

    Это фактически означает hello **Jade** ядра toorender HTML для нашего приложения и создает **блок** вызывается **содержимого** где можно указать hello макета для содержимое веб-узла страницы.

    Сохраните и закройте файл **layout.jade** .

3. Теперь откройте hello **index.jade** файл, hello представление, которое будет использоваться нашего приложения и замените hello содержимое файла hello hello следующее:
   
        extends layout
        block content
           h1 #{title}
           br
        
           form(action="/completetask", method="post")
             table.table.table-striped.table-bordered
               tr
                 td Name
                 td Category
                 td Date
                 td Complete
               if (typeof tasks === "undefined")
                 tr
                   td
               else
                 each task in tasks
                   tr
                     td #{task.name}
                     td #{task.category}
                     - var date  = new Date(task.date);
                     - var day   = date.getDate();
                     - var month = date.getMonth() + 1;
                     - var year  = date.getFullYear();
                     td #{month + "/" + day + "/" + year}
                     td
                       input(type="checkbox", name="#{task.id}", value="#{!task.completed}", checked=task.completed)
             button.btn.btn-primary(type="submit") Update tasks
           hr
           form.well(action="/addtask", method="post")
             .form-group
               label(for="name") Item Name:
               input.form-control(name="name", type="textbox")
             .form-group
               label(for="category") Item Category:
               input.form-control(name="category", type="textbox")
             br
             button.btn(type="submit") Add item
   

Это расширяет возможности макета и приводятся сведения для hello **содержимого** заполнителя, мы видели в hello **layout.jade** файлов более ранних версий.
   
В макете мы создали две формы HTML.

Первая форма Hello содержит таблицу для наших данных и кнопки, которая позволяет нам tooupdate элементов путем учета слишком**/completetask** метод нашей контроллера.
    
Вторая форма Hello содержит два поля ввода и кнопку, которая позволяет нам toocreate новый элемент путем учета слишком**/addtask** метод нашей контроллера.

Это должна быть все, что нужно для наших toowork приложения.

## <a name="_Toc395783181"></a>Шаг 6. Локальный запуск приложения
1. приложение hello tootest на локальном компьютере, запустите `npm start` в hello терминалов toostart приложения, а затем обновите ваш [http://localhost:3000](http://localhost:3000) страницы браузера. Страница приветствия должен выглядеть так hello изображения ниже:
   
    ![Снимок экрана: hello приложение MyTodo списка в окне браузера](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > Получив ошибку о hello отступ в файл layout.jade hello или index.jade hello, убедитесь, что первые две строки hello в обоих файлах выравнивается по левому краю, без пробелов. При наличии пробелов перед hello первые две строки, удалите их, сохраните оба файла, а затем обновите окно браузера. 

2. Использовать hello элемент, имя элемента и категории поля tooenter новую задачу и нажмите кнопку **добавить элемент**. Будет создан документ в Azure Cosmos DB с заданными свойствами. 
3. Страница приветствия следует обновить hello toodisplay недавно созданном элемента в список ToDo hello.
   
    ![Снимок экрана: hello приложения с помощью нового элемента в список ToDo hello](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. просто установите флажок "hello" в столбце завершения hello toocomplete задачу и нажмите кнопку **обновление задач**. Этот документ hello обновлений, уже созданы.

5. приложение hello toostop, нажмите клавиши CTRL + C в окне терминала hello и нажмите кнопку **Y** tooterminate hello пакетного задания.

## <a name="_Toc395783182"></a>Шаг 7: Развертывание вашего приложения tooAzure проект разработки веб-сайтов
1. Если это еще не сделано, включите репозиторий git для веб-сайта Azure. Инструкции о том, как можно найти toodo в hello [tooAzure локальное развертывание Git службы приложений](../app-service-web/app-service-deploy-local-git.md) раздела.
2. Добавьте веб-сайт Azure в качестве удаленного репозитория git.
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. Развертывание с помощью принудительной отправки toohello удаленной.
   
        git push azure master
4. Через несколько секунд Visual Studio завершит публикацию вашего веб-приложения и запустит браузер, где вы увидите свое творение, запущенное в Azure!

    Поздравляем! Только первый Node.js Express веб-приложения с помощью Azure Cosmos DB создания и публикации tooAzure веб-сайтов.

    Если требуется toodownload или toohello полный перечень приложений см. в этом учебнике, ее можно загрузить из [GitHub][GitHub].

## <a name="_Toc395637775"></a>Дальнейшие действия

* Требуется tooperform масштаб и производительность, тестирование с помощью Azure Cosmos DB? Дополнительные сведения см. в статье о [проверке производительности и масштабирования с помощью Azure Cosmos DB](performance-testing.md).
* Узнайте, каким образом слишком[мониторинг учетной записи Azure Cosmos DB](monitor-accounts.md).
* Выполнять запросы к нашей образец набора данных в hello [площадку запросов](https://www.documentdb.com/sql/demo).
* Просмотр hello [документации Azure Cosmos DB](https://docs.microsoft.com/azure/documentdb/).

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

