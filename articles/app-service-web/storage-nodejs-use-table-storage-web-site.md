---
title: "aaaNode.js веб-приложения с помощью hello службы таблиц Azure"
description: "В этом учебнике показано, как toouse hello таблиц Azure службы toostore данные из приложения Node.js, которая размещается в веб-приложениях службы приложений Azure."
tags: azure-portal
services: app-service\web, storage
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 029e6f46-f586-4309-adbf-71c7b8d537d4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: f6e08335b4c7f62f7b3994287edd586860cb7135
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-using-hello-azure-table-service"></a>Веб-приложение node.js с помощью hello службы таблиц Azure
## <a name="overview"></a>Обзор
В этом учебнике показано, как предоставляемые управление данными Azure toostore и доступ к данным из службы таблиц toouse [узел] приложение, размещенное в [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) веб-приложений. Этот учебный курс разработан для читателей, обладающих определенным опытом использования Node и [Git].

Вы узнаете:

* Как tooinstall npm (узел диспетчера пакетов) toouse hello модулей узла
* Как toowork с hello службы таблицы Azure
* Как toouse hello Azure CLI toocreate веб-приложения.

Руководствуясь этим учебником, вы создадите простое веб-приложение для управления списком дел, позволяющее создавать, извлекать и выполнять задачи. задачи Hello хранятся в hello службы таблиц.

Вот приложение hello завершена.

![Веб-страница, показывающая пустой список задач][node-table-finished]

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

## <a name="prerequisites"></a>Предварительные требования
Перед выполнением инструкции hello в этой статье, убедитесь, что установлены следующие компоненты hello:

* [узел] версии 0.10.24 или выше
* [Git]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a>Создайте учетную запись хранения.
Создайте учетную запись хранения Azure. приложение Hello будет использовать этот счет toostore hello заданий для выполнения.

1. Войти в hello [портала Azure](https://portal.azure.com/).
2. Нажмите кнопку hello **New** значок hello нижней левом углу портала hello, нажмите кнопку **данные + хранилище** > **хранения**. Задайте уникальное имя учетной записи хранилища hello и создайте новый [группы ресурсов](../azure-resource-manager/resource-group-overview.md) для него.
   
      ![Кнопка «Создать»](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    При создании учетной записи хранилища hello hello **уведомления** кнопка будет мигать зеленым **успех** и учетной записи хранилища hello колонке открыт tooshow, что оно принадлежит новый ресурс toohello группы создать.
3. В колонке учетной записи хранилища hello щелкните **параметры** > **ключей**. Скопировать hello доступа первичного ключа toohello буфер обмена.
   
    ![Ключ доступа][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a>Установка модулей и создание шаблонов
В этом разделе будет создание нового узла приложения и использовать пакеты модуля tooadd npm. Для этого приложения будет использовать hello [Express] и [Azure] модулей. модуль экспресс-выпуск Hello инфраструктура Model View Controller для узла, при hello модули Azure предоставляет таблицу toohello подключения службы.

### <a name="install-express-and-generate-scaffolding"></a>Установка модуля Express и формирование шаблонов
1. Из командной строки hello, создайте новый каталог с именем **tasklist** и каталог toothat коммутатора.  
2. Введите следующие команды tooinstall hello Express модуля hello.
   
        npm install express-generator@4.2.0 -g
   
    В зависимости от операционной системы hello может потребоваться tooput «sudo» перед командой hello.
   
        sudo npm install express-generator@4.2.0 -g
   
    Hello выходные данные отображаются как toohello, в следующем примере:
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > Hello "-g" параметр устанавливает модуль hello глобально. Таким образом, мы используем **express** toogenerate формирование приложения без необходимости tootype в Дополнительные сведения о пути.
   > 
   > 
3. Формирование шаблонов hello toocreate для приложения hello введите hello **express** команды:
   
        express
   
    Hello выходные данные этой команды появится примерно toohello в следующем примере:
   
           create : .
           create : ./package.json
           create : ./app.js
           create : ./public
           create : ./public/images
           create : ./routes
           create : ./routes/index.js
           create : ./routes/users.js
           create : ./public/stylesheets
           create : ./public/stylesheets/style.css
           create : ./views
           create : ./views/index.jade
           create : ./views/layout.jade
           create : ./views/error.jade
           create : ./public/javascripts
           create : ./bin
           create : ./bin/www
   
           install dependencies:
             $ cd . && npm install
   
           run hello app:
             $ DEBUG=my-application ./bin/www
   
    Теперь у вас есть несколько новые каталоги и файлы в hello **tasklist** каталога.

### <a name="install-additional-modules"></a>Установка дополнительных модулей
Один из hello файлов, **express** создает — **package.json**. Этот файл содержит список зависимостей модуля. Позже при развертывании приложения hello tooApp службы веб-приложений, этот файл определяет, какие модули должны toobe установлен в Azure.

Из командной строки hello, введите следующие команды tooinstall hello модулей, описанных в hello hello **package.json** файла. Может потребоваться toouse «sudo».

    npm install

Hello выходные данные этой команды появится примерно toohello в следующем примере:

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


Затем введите следующая команда tooinstall hello hello [azure], [узел uuid], [nconf] и [async] модули:

    npm install azure-storage node-uuid async nconf --save

Hello **--Сохранить** флаг добавляет записи для этих модулей toohello **package.json** файла.

Hello выходные данные этой команды появится примерно toohello в следующем примере:

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-hello-application"></a>Создание приложения hello
Теперь мы готовы toobuild приложения hello.

### <a name="create-a-model"></a>Создание модели
Объект *модель* — это объект, представляющий данные hello в приложении. Для приложения hello hello только модель — объект задачи, который представляет элемент в список дел hello. Задачи будут иметь hello следующие поля:

* PartitionKey
* RowKey
* name (строка)
* category (строка)
* completed (логическое значение)

**PartitionKey** и **RowKey** используются hello службы таблиц как ключи таблицы. Дополнительные сведения см. в разделе [модели данных службы таблиц hello основные сведения о](https://msdn.microsoft.com/library/azure/dd179338.aspx).

1. В hello **tasklist** каталога, создайте новый каталог с именем **моделей**.
2. В hello **моделей** каталога, создайте новый файл с именем **task.js**. Этот файл будет содержать hello модель для hello задачи, созданные вашим приложением.
3. В начале hello hello **task.js** файл, добавить следующие tooreference необходимые библиотеки кода hello:
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. Добавьте следующую hello кода toodefine и экспорт hello объекта задачи. Этот объект отвечает за подключение toohello таблицы.
   
          module.exports = Task;
   
        function Task(storageClient, tableName, partitionKey) {
          this.storageClient = storageClient;
          this.tableName = tableName;
          this.partitionKey = partitionKey;
          this.storageClient.createTableIfNotExists(tableName, function tableCreated(error) {
            if(error) {
              throw error;
            }
          });
        };
5. Добавьте hello, следующие дополнительные методы toodefine кода hello объекта задачи, которые позволяют взаимодействия с данными, хранящимися в таблице hello:
   
        Task.prototype = {
          find: function(query, callback) {
            self = this;
            self.storageClient.queryEntities(this.tableName, query, null, function entitiesQueried(error, result) {
              if(error) {
                callback(error);
              } else {
                callback(null, result.entries);
              }
            });
          },
   
          addItem: function(item, callback) {
            self = this;
            // use entityGenerator tooset types
            // NOTE: RowKey must be a string type, even though
            // it contains a GUID in this example.
            var itemDescriptor = {
              PartitionKey: entityGen.String(self.partitionKey),
              RowKey: entityGen.String(uuid()),
              name: entityGen.String(item.name),
              category: entityGen.String(item.category),
              completed: entityGen.Boolean(false)
            };
            self.storageClient.insertEntity(self.tableName, itemDescriptor, function entityInserted(error) {
              if(error){  
                callback(error);
              }
              callback(null);
            });
          },
   
          updateItem: function(rKey, callback) {
            self = this;
            self.storageClient.retrieveEntity(self.tableName, self.partitionKey, rKey, function entityQueried(error, entity) {
              if(error) {
                callback(error);
              }
              entity.completed._ = true;
              self.storageClient.updateEntity(self.tableName, entity, function entityUpdated(error) {
                if(error) {
                  callback(error);
                }
                callback(null);
              });
            });
          }
        }
6. Сохраните и закройте hello **task.js** файла.

### <a name="create-a-controller"></a>Создание контроллера
Объект *контроллера* обрабатывает HTTP-запросы и отображает hello HTML-ответа.

1. В hello **tasklist/маршруты** каталога, создайте новый файл с именем **tasklist.js** и откройте его в текстовом редакторе.
2. Добавьте следующий код слишком hello**tasklist.js**. Это загружает hello azure и async модули, в которых используются **tasklist.js**. Этот параметр также определяет hello **TaskList** функции, которая передается экземпляр hello **задачи** объекта было определено ранее:
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. Определите объект **TaskList** .
   
        function TaskList(task) {
          this.task = task;
        }
4. Добавьте следующие методы слишком hello**TaskList**:
   
        TaskList.prototype = {
          showTasks: function(req, res) {
            self = this;
            var query = new azure.TableQuery()
              .where('completed eq ?', false);
            self.task.find(query, function itemsFound(error, items) {
              res.render('index',{title: 'My ToDo List ', tasks: items});
            });
          },
   
          addTask: function(req,res) {
            var self = this;
            var item = req.body.item;
            self.task.addItem(item, function itemAdded(error) {
              if(error) {
                throw error;
              }
              res.redirect('/');
            });
          },
   
          completeTask: function(req,res) {
            var self = this;
            var completedTasks = Object.keys(req.body);
            async.forEach(completedTasks, function taskIterator(completedTask, callback) {
              self.task.updateItem(completedTask, function itemsUpdated(error) {
                if(error){
                  callback(error);
                } else {
                  callback(null);
                }
              });
            }, function goHome(error){
              if(error) {
                throw error;
              } else {
               res.redirect('/');
              }
            });
          }
        }

### <a name="modify-appjs"></a>Изменение app.js
1. Из hello **tasklist** каталог, откройте hello **в файле app.js** файл. Этот файл был создан ранее, запустив hello **express** команды.
2. В начале файла hello hello, добавьте следующие tooload hello azure модуля, имя таблицы hello набора, ключа секции и набор hello хранилища учетные данные, используемые в этом примере hello:
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > nconf загружает значения конфигурации hello из переменных среды или hello **config.json** файл, который мы создадим позже.
   > 
   > 
3. В файле в файле app.js hello, прокрутите вниз toowhere вы видите hello следующую строку:
   
        app.use('/', routes);
        app.use('/users', users);
   
    Замените приведенный ниже код hello hello выше строк. Это будет инициализировать экземпляр <strong>задачи</strong> с учетной записью хранилища tooyour соединения. Аргумент передается toohello <strong>TaskList</strong>, который будет использовать toocommunicate с hello службы таблиц:
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. Сохранить hello **в файле app.js** файл.

### <a name="modify-hello-index-view"></a>Изменить представление index hello
1. Откройте hello **tasklist/views/index.jade** файл в текстовом редакторе.
2. Замените все содержимое файла hello hello hello, следующий код. Он определяет представление, в котором отображаются существующие задачи и содержится форма для добавления новых задач и пометки существующих как завершенных.
   
        extends layout
   
        block content
          h1= title
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
                    td #{task.name._}
                    td #{task.category._}
                    - var day   = task.Timestamp._.getDate();
                    - var month = task.Timestamp._.getMonth() + 1;
                    - var year  = task.Timestamp._.getFullYear();
                    td #{month + "/" + day + "/" + year}
                    td
                      input(type="checkbox", name="#{task.RowKey._}", value="#{!task.completed._}", checked=task.completed._)
            button.btn(type="submit") Update tasks
          hr
          form.well(action="/addtask", method="post")
            label Item Name:
            input(name="item[name]", type="textbox")
            label Item Category:
            input(name="item[category]", type="textbox")
            br
            button.btn(type="submit") Add item
3. Сохраните и закройте файл **index.jade** .

### <a name="modify-hello-global-layout"></a>Изменить макет глобального hello
Hello **layout.jade** файла в hello **представления** каталог — это глобальный шаблон для других **.jade** файлов. На этом этапе вы измените его toouse [Twitter начальной загрузки](https://github.com/twbs/bootstrap), который — это набор средств, который позволяет легко toodesign работы с низким приоритетом привлекательных веб-приложения.

Загрузите и извлеките файлы hello для [Twitter начальной загрузки](http://getbootstrap.com/). Копировать hello **bootstrap.min.css** файл из hello начальной загрузки **css** папки в hello **public или таблицы стилей** каталога приложения.

Из hello **представления** откройте **layout.jade** и замените все содержимое hello hello следующее:

    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body.app
        nav.navbar.navbar-default
          div.navbar-header
          a.navbar-brand(href='/') My Tasks
        block content

### <a name="create-a-config-file"></a>Создание файла конфигурации
toorun приложение hello локально, мы будем Поместите учетные данные хранилища Azure в файл конфигурации. Создайте файл с именем **config.json* * с hello, следуя JSON:

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Замените **имя учетной записи хранения** с именем hello хранилища hello учетную запись, созданную ранее и замените **ключ доступа к хранилищу** с hello первичный ключ доступа для учетной записи хранилища. Например:

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

Сохраните этот файл *один уровень каталога выше* чем hello **tasklist** каталог следующим образом:

    parent/
      |-- config.json
      |-- tasklist/

Hello причиной этого является tooavoid проверка файла конфигурации hello в систему управления версиями, где могут стать открытый. При развертывании приложения tooAzure hello, мы будем использовать переменные среды вместо файла конфигурации.

## <a name="run-hello-application-locally"></a>Запустите приложение hello локально
приложения hello tootest на локальном компьютере, выполните следующие шаги hello.

1. Из командной строки hello, измените каталоги toohello **tasklist** каталога.
2. Используйте следующие приложения hello toolaunch команда локально hello.
   
        npm start
3. Откройте веб-браузер и перейдите toohttp://127.0.0.1:3000.
   
    Появится примерно toohello веб-страницы, следующий пример.
   
    ![Веб-страница, показывающая пустой список задач][node-table-finished]
4. toocreate новый элемент задачи, введите имя и категории и нажмите кнопку **добавить элемент**. 
5. toomark задач как полный, проверьте **завершить** и нажмите кнопку **задачи обновления**.
   
    ![Изображение hello новый элемент в списке hello задач][node-table-list-items]

Даже если приложение hello выполняется локально, он хранит данные hello в hello службы таблиц Azure.

## <a name="deploy-your-application-tooazure"></a>Развертывание tooAzure вашего приложения
Hello шаги в этом разделе Использование средств командной строки Azure hello toocreate новое веб-приложение в службе приложений, а затем использовать Git toodeploy приложения. tooperform эти действия, необходимо иметь подписку Azure.

> [!NOTE]
> Эти действия можно также выполнить с помощью hello [портала Azure](https://portal.azure.com/). См. статью [Начало работы с веб-приложениями Node.js в службе приложений Azure].
> 
> Если это первый веб-приложения hello, созданных toodeploy hello портала Azure необходимо использовать это приложение.
> 
> 

tooget к работе, установите hello [Azure CLI] , введя следующую команду из командной строки hello hello:

    npm install azure-cli -g

### <a name="import-publishing-settings"></a>Импорт параметров публикации
На этом шаге вы загрузите файл, содержащий сведения о вашей подписке.

1. Введите следующую команду hello:
   
        azure login
   
    Эта команда запускает браузер и переходит на страницу загрузки toohello. Если будет предложено, войдите в систему hello учетную запись, связанную с подпиской Azure.
   
    <!-- ![hello download page][download-publishing-settings] -->
   
    Загрузка файла Hello начинается автоматически. Если этого не произошло, можно щелкнуть ссылку hello в начале hello файла hello загрузки toomanually страницы приветствия. Сохраните hello файл и отметьте hello путь к файлу.
2. Введите следующие параметры hello tooimport команды hello:
   
        azure account import <path-to-file>
   
    Укажите hello путь и имя файла для публикации файла параметров, загруженный в предыдущем шаге hello hello.
3. После импорта параметров hello, удалите hello файл параметров публикации. Он больше не нужен, и при этом он содержит важные сведения о вашей подписки Azure.

### <a name="create-an-app-service-web-app"></a>Создание веб-приложения службы приложений
1. Из командной строки hello, измените каталоги toohello **tasklist** каталога.
2. Используйте следующие команды toocreate новое веб-приложение hello.
   
        azure site create --git
   
    Будут запрашиваться имя веб-приложения hello и расположение. Укажите уникальное имя и выберите hello географического местоположения учетной записи хранилища Azure.
   
    Hello `--git` параметр создает репозитории в Azure для этого веб-приложения. Он также инициализирует репозитория в текущем каталоге hello, если не существует и добавляет [Git удаленного] с именем «azure», который является tooAzure приложения используется toopublish hello. Наконец, он создает **web.config** файл, содержащий параметры, используемые приложениями Azure toohost узла. Если опустить hello `--git` параметр, но hello каталог содержит репозитория, команда hello по-прежнему будет создавать удаленного hello «azure».
   
    После завершения этой команды вы увидите примерно toohello следующие выходные данные. Обратите внимание, что hello строки, начинающиеся с **веб-сайт создан на** содержит hello URL-адрес для веб-приложения hello.
   
        info:   Executing command site create
        help:   Need a site name
        Name: TableTasklist
        info:   Using location southcentraluswebspace
        info:   Executing `git init`
        info:   Creating default .gitignore file
        info:   Creating a new web site
        info:   Created web site at  tabletasklist.azurewebsites.net
        info:   Initializing repository
        info:   Repository initialized
        info:   Executing `git remote add azure https://username@tabletasklist.azurewebsites.net/TableTasklist.git`
        info:   site create command OK
   
   > [!NOTE]
   > Если это hello первого приложения службы веб-приложения для вашей подписки будет веб-приложения hello toocreate соответствии toouse hello портала Azure. Дополнительные сведения см. в разделе [Начало работы с веб-приложениями Node.js в службе приложений Azure].
   > 
   > 

### <a name="set-environment-variables"></a>Настройка переменных среды
На этом шаге вы добавите конфигурации приложения web tooyour переменных среды в Azure.
Из командной строки hello введите hello следующие данные:

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


Замените  **<storage account name>**  с именем hello хранилища hello учетную запись, созданную ранее и замените  **<storage access key>**  с hello первичный ключ доступа для учетной записи хранилища. (Используйте hello же значений в виде файла config.json hello, созданного ранее).

Кроме того, можно задать переменные среды в hello [портала Azure](https://portal.azure.com/):

1. Открыть колонку hello веб-приложение, нажав кнопку **Обзор** > **веб-приложений** > имя вашего веб-приложения.
2. В колонке веб-приложения щелкните **Все параметры** > **Параметры приложения**.
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. Прокрутите вниз toohello **параметры приложения** статьи и добавьте пары ключ значение hello.
   
     ![Параметры приложения](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. Щелкните **СОХРАНИТЬ**.

### <a name="publish-hello-application"></a>Публикация приложения hello
приложение hello toopublish, зафиксируйте tooGit файлы кода hello и затем отправьте tooazure/master.

1. Задайте учетные данные развертывания.
   
        azure site deployment user set <name> <password>
2. Добавьте и зафиксируйте файлы своего приложения.
   
        git add .
        git commit -m "adding files"
3. Принудительной фиксации hello toohello веб-приложения служб приложений:
   
        git push azure master
   
    Используйте **master** как hello целевой ветви. В конце развертывания hello hello появляется примерно toohello оператор, следующий пример:
   
        toohttps://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. После завершения операции принудительной отправки hello Обзор toohello веб-приложения URL, ранее возвращенный hello `azure create site` команды tooview приложения.

## <a name="next-steps"></a>Дальнейшие действия
При hello действия, описанные в этой статье описывается использование сведения toostore hello службы таблиц, можно также использовать [MongoDB](https://mlab.com/azure/). 

## <a name="additional-resources"></a>Дополнительные ресурсы
[Azure CLI]

## <a name="whats-changed"></a>Изменения
* Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- URLs -->

[Начало работы с веб-приложениями Node.js в службе приложений Azure]: app-service-web-get-started-nodejs.md
[Azure Developer Center]: /develop/nodejs/

[узел]: http://nodejs.org
[Git]: http://git-scm.com
[Express]: http://expressjs.com
[for free]: http://windowsazure.com
[Git удаленного]: http://git-scm.com/docs/git-remote

[Azure CLI]:../cli-install-nodejs.md

[azure]: https://github.com/Azure/azure-sdk-for-node
[узел uuid]: https://www.npmjs.com/package/node-uuid
[nconf]: https://www.npmjs.com/package/nconf
[async]: https://www.npmjs.com/package/async

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application tooan Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
