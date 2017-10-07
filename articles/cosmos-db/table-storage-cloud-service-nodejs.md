---
title: "приложение aaaWeb с хранилищем таблиц (Node.js) | Документы Microsoft"
description: "Учебник, в котором построена на hello веб-приложения с помощью учебника, экспресс-выпуск службы хранилища Azure и hello модуль Azure."
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: e90959a2-4cb2-4b19-9bfb-aede15b18b1c
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 7eefc09baab61cf44c98183135abe572b11812e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-application-using-storage"></a>Веб-приложение Node.js, использующее хранилище
## <a name="overview"></a>Обзор
В этом учебнике hello приложение, созданное в [Node.js веб-приложения с использованием экспресс-выпуск] учебника расширяется с помощью библиотеки клиента hello Microsoft Azure для Node.js toowork с помощью службы управления данными. Создать список задач в веб-приложение, можно развернуть tooAzure расширения приложения. Список задач Hello позволяет пользователю получить задачи, добавлять новые задачи и пометить задачи как завершенную.

Задача Hello хранятся в хранилище Azure. Хранилище Azure обеспечивает хранение неструктурированных данных с функциями отказоустойчивости и высокой доступности. Служба хранилища Azure включает в себя несколько структур данных, где можно хранить данные и получать к ним доступ. Можно использовать службы хранилища hello из состава hello Azure SDK для Node.js или с помощью API-интерфейсов REST API-интерфейсы hello. Дополнительные сведения см. в статье [Хранилище Azure].

В этом учебнике предполагается, что вы выполнили hello [веб-приложение Node.js] и [Node.js быстрое][Node.js веб-приложения с использованием экспресс-выпуск] учебники.

Он содержит hello следующую информацию:

* Как toowork с hello процессора Jade шаблона
* Как toowork со службами управления данными Azure

Следующий снимок экрана приветствия показано приложение hello завершена:

![Hello завершения веб-страницы в браузере internet explorer](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a>Настройка учетных данных хранилища в файле Web.Config
Необходимо передать в хранилище учетных данных tooaccess хранилища Azure. Это делается путем использования параметров приложения web.config hello.
параметры файла web.config Hello передаются как tooNode переменные среды, которые затем считываются последующими hello Azure SDK.

> [!NOTE]
> Учетные данные хранилища используются только в том случае, когда приложение hello развернутой tooAzure. При выполнении в эмуляторе hello hello приложению hello эмулятор хранилища.
>
>

Выполните следующие учетные данные учетной записи хранения действия tooretrieve hello hello и добавить их toohello параметры файла web.config:

1. Если он не открыт, запустите hello Azure PowerShell из hello **запустить** меню, развернув **все программы, Azure**, щелкните правой кнопкой мыши **Azure PowerShell**, а затем выберите  **Запуск от имени администратора**.
2. Измените каталоги toohello папку, содержащую приложение. Например, C:\\node\\tasklist\\WebRole1.
3. Из окна Azure Powershell hello введите следующие сведения об учетной записи хранилища командлет tooretrieve hello hello:

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   Hello Предыдущий командлет извлекает hello список учетных записей хранилища и ключи учетной записи, связанные с вашей размещенной службы.

   > [!NOTE]
   > Поскольку hello Azure SDK создает учетную запись хранилища, при развертывании службы, учетную запись хранилища должна уже существовать от развертывания приложения в предыдущих направляющие hello.
   >
   >
4. Откройте hello **ServiceDefinition.csdef** файл, содержащий hello параметров среды, которые используются, когда приложение hello развернутой tooAzure:

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. Блокировать INSERT hello ниже в разделе **среды** элемент, заменив {учетной записи ХРАНИЛИЩА} и {ключ доступа к ХРАНИЛИЩУ} с именем учетной записи hello и hello первичный ключ для учетной записи хранения hello требуется toouse для развертывания:

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![содержимое файла web.cloud.config Hello](./media/table-storage-cloud-service-nodejs/node37.png)

6. Сохраните файл hello и закройте Блокнот.

### <a name="install-additional-modules"></a>Установка дополнительных модулей
1. Используйте hello, следующая команда tooinstall hello [azure], [uuid узел], [nconf] и [асинхронных] модулей локально, а также toosave запись для них toohello **package.json** файла:

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  Hello выходные данные этой команды должен выглядеть примерно toohello следующее:

  ```
  node-uuid@1.4.1 node_modules\node-uuid

  nconf@0.6.9 node_modules\nconf
  ├── ini@1.1.0
  ├── async@0.2.9
  └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.8)

  azure-storage@0.1.0 node_modules\azure-storage
  ├── extend@1.2.1
  ├── xmlbuilder@0.4.3
  ├── mime@1.2.11
  ├── underscore@1.4.4
  ├── validator@3.1.0
  ├── node-uuid@1.4.1
  ├── xml2js@0.2.7 (sax@0.5.2)
  └── request@2.27.0 (json-stringify-safe@5.0.0, tunnel-agent@0.3.0, aws-sign@0.3.0, forever-agent@0.5.2, qs@0.6.6, oauth-sign@0.3.0, cookie-jar@0.3.0, hawk@1.0.0, form-data@0.1.3, http-signature@0.10.0)
  ```

## <a name="using-hello-table-service-in-a-node-application"></a>Использование службы таблиц hello в приложении узла
В этом разделе hello основных приложений, созданных hello **express** команда расширяется путем добавления **task.js** файла, содержащего модель hello для ваших задач. Изменение существующих hello **в файле app.js** файл и создать новую **tasklist.js** файла, который использует модель hello.

### <a name="create-hello-model"></a>Создание модели hello
1. В hello **WebRole1** каталога, создайте новый каталог с именем **моделей**.
2. В hello **моделей** каталога, создайте новый файл с именем **task.js**. Этот файл содержит hello модель для hello задачи, созданные вашим приложением.
3. В начале hello hello **task.js** файл, добавить следующие tooreference необходимые библиотеки кода hello:

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. Затем добавьте код toodefine и экспорт hello объекта задачи. объект задачи Hello отвечает за подключение toohello таблицы.

    ```nodejs
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
    ```

5. Добавьте hello следующие дополнительные методы toodefine кода hello объекта задачи, которые позволяют взаимодействия с данными, хранящимися в таблице hello.

    ```nodejs
    Task.prototype = {
      find: function(query, callback) {
        self = this;
        self.storageClient.queryEntities(query, function entitiesQueried(error, result) {
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
    ```

6. Сохраните и закройте hello **task.js** файла.

### <a name="create-hello-controller"></a>Создание контроллера hello
1. В hello **WebRole1/маршруты** каталога, создайте новый файл с именем **tasklist.js** и откройте его в текстовом редакторе.
2. Добавьте следующий код слишком hello**tasklist.js**. Этот код загружает hello azure и асинхронных модулей, которые используются **tasklist.js** и определяет hello **TaskList** функции, которая передается экземпляр hello **задачи** мы объекта определенные ранее:

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. Продолжайте добавлять toohello **tasklist.js** файла путем добавления методов hello используется слишком**showTasks**, **addTask**, и **completeTasks**:

    ```nodejs
    TaskList.prototype = {
      showTasks: function(req, res) {
        self = this;
        var query = azure.TableQuery()
          .where('completed eq ?', false);
        self.task.find(query, function itemsFound(error, items) {
          res.render('index',{title: 'My ToDo List ', tasks: items});
        });
      },

      addTask: function(req,res) {
        var self = this
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
    ```

4. Сохранить hello **tasklist.js** файла.

### <a name="modify-appjs"></a>Изменение app.js
1. В hello **WebRole1** каталог, откройте hello **в файле app.js** файл в текстовом редакторе.
2. В начале файла hello hello, добавьте следующий модуль hello azure tooload hello и установите ключ имени и секций таблицы hello:

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. В файле в файле app.js hello, прокрутите вниз toowhere вы видите hello следующую строку:

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    Замените hello предыдущих строк с hello, следующий код. Этот код инициализирует новый экземпляр класса <strong>задачи</strong> с учетной записью хранилища tooyour соединения. Hello <strong>задачи</strong> передается toohello <strong>TaskList</strong>, которая использует toocommunicate со службой hello таблицы:

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. Сохранить hello **в файле app.js** файл.

### <a name="modify-hello-index-view"></a>Изменить представление index hello
1. Измените каталоги toohello **представления** каталог и откройте hello **index.jade** файл в текстовом редакторе.
2. Замените содержимое hello hello **index.jade** файл с hello, следующий код. Этот код определяет hello представление для отображения существующих задач, а также определяет форму для добавления новых задач и пометить существующих как завершенное.

    ```
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
          if tasks != []
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
    ```

3. Сохраните и закройте файл **index.jade** .

### <a name="modify-hello-global-layout"></a>Изменить макет глобального hello
Hello **layout.jade** файла в hello **представления** каталог используется как глобальный шаблон для других **.jade** файлов. На этом этапе изменения hello **layout.jade** файл toouse [Twitter начальной загрузки](https://github.com/twbs/bootstrap), который — это набор средств, который позволяет легко toodesign работы с низким приоритетом привлекательных веб-сайта.

1. Загрузите и извлеките файлы hello для [Twitter начальной загрузки](http://getbootstrap.com/). Копировать hello **bootstrap.min.css** файл из hello **начальной загрузки\\dist\\css** toohello папки **открытый\\таблицы стилей** каталог приложения списка задач.
2. Из hello **представления** папки, откройте hello **layout.jade** файл в текстовом редакторе и замените содержимое hello hello следующее:

    doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content

3. Сохранить hello **layout.jade** файла.

### <a name="running-hello-application-in-hello-emulator"></a>Выполнение приложения hello в эмуляторе hello
Используйте следующие команды toostart hello приложения в эмуляторе hello hello.

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

Hello браузер открывается и отображает hello следующие страницы:

![Веб-сайт, разбитых на страницы под названием My списка задач с таблицей, содержащей задачи и поля tooadd новую задачу.](./media/table-storage-cloud-service-nodejs/node44.png)

Использовать элементы tooadd формы hello, или удалить существующие элементы, помечая их как завершенное.

## <a name="publishing-hello-application-tooazure"></a>Публикация tooAzure приложения hello
В окне приветствия Windows PowerShell вызовите hello, выполнив командлет tooredeploy tooAzure вашей размещенной службы.

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

Замените **myuniquename** уникальным именем приложения. Замените **datacentername** с именем hello центр обработки данных Azure, такие как **Запад США**.

По завершении развертывания hello появится ответ аналогичные toohello следующее:

```
  PS C:\node\tasklist> publish-azureserviceproject -servicename tasklist -location "West US"
  WARNING: Publishing tasklist tooMicrosoft Azure. This may take several minutes...
  WARNING: 2:18:42 PM - Preparing runtime deployment for service 'tasklist'
  WARNING: 2:18:42 PM - Verifying storage account 'tasklist'...
  WARNING: 2:18:43 PM - Preparing deployment for tasklist with Subscription ID: 65a1016d-0f67-45d2-b838-b8f373d6d52e...
  WARNING: 2:19:01 PM - Connecting...
  WARNING: 2:19:02 PM - Uploading Package toostorage service larrystore...
  WARNING: 2:19:40 PM - Upgrading...
  WARNING: 2:22:48 PM - Created Deployment ID: b7134ab29b1249ff84ada2bd157f296a.
  WARNING: 2:22:48 PM - Initializing...
  WARNING: 2:22:49 PM - Instance WebRole1_IN_0 of role WebRole1 is ready.
  WARNING: 2:22:50 PM - Created Website URL: http://tasklist.cloudapp.net/.
```

Указав hello **-запустите** параметр в предыдущий командлет hello, hello браузер откроет и отобразит вашего приложения, работающего в Azure, после завершения публикации.

![Окно браузера, отображения страницы приветствия Мой список задач. URL-адрес Hello указывает, что страница приветствия теперь размещенный в Azure.](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a>Остановка и удаление приложения
После развертывания приложения, вы можете toodisable, чтобы избежать расходов или построения и развертывания других приложений в пределах hello бесплатно пробного периода.

Для экземпляров веб-роли Azure выставляет счета за почасовое использование серверного времени.
После развертывания приложения даже в том случае, если экземпляры не запущены и находятся в состоянии остановки hello потребляются времени сервера.

Hello следующие шаги показывают, как toostop и удалить приложение.

1. В окне приветствия Windows PowerShell Остановите развертывание службы hello, созданным в предыдущем разделе hello, hello, выполнив командлет:

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   Остановка службы hello может занять несколько минут. При остановке службы hello, появляется сообщение о том, что он был остановлен.

2. Служба toodelete hello, вызов hello, выполнив командлет:

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   При появлении запроса введите **Y** toodelete hello службы.

   Удаление службы hello может занять несколько минут. После удаления службы hello, вы получите сообщение, указывающее на то, что служба hello была удалена.

[Node.js веб-приложения с использованием экспресс-выпуск]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[Хранилище Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[веб-приложение Node.js]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


