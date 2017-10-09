---
title: "приложение aaaWeb с хранилищем таблиц (Node.js) | Документы Microsoft"
description: "Учебник, в котором построена на hello веб-приложения с помощью учебника, экспресс-выпуск службы хранилища Azure и hello модуль Azure."
services: cloud-services, storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e90959a2-4cb2-4b19-9bfb-aede15b18b1c
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 4eba16f09f8b69cbc135d097e6ca71e08b33733c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="5148d-103">Веб-приложение Node.js, использующее хранилище</span><span class="sxs-lookup"><span data-stu-id="5148d-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="5148d-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="5148d-104">Overview</span></span>
<span data-ttu-id="5148d-105">В этом учебнике будет расширять hello приложение, созданное в [Node.js веб-приложения с использованием экспресс-выпуск] учебника с помощью библиотеки клиента hello Microsoft Azure для Node.js toowork с помощью службы управления данными.</span><span class="sxs-lookup"><span data-stu-id="5148d-105">In this tutorial, you will extend hello application created in the [Node.js Web Application using Express] tutorial by using hello Microsoft Azure Client Libraries for Node.js toowork with data management services.</span></span> <span data-ttu-id="5148d-106">Будет расширить список задач в веб-приложения, что вы можете развернуть tooAzure toocreate вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="5148d-106">You will extend your application toocreate a web-based task-list application that you can deploy tooAzure.</span></span> <span data-ttu-id="5148d-107">Список задач Hello позволяет пользователю получить задачи, добавлять новые задачи и пометить задачи как завершенную.</span><span class="sxs-lookup"><span data-stu-id="5148d-107">hello task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="5148d-108">Задача Hello хранятся в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="5148d-108">hello task items are stored in Azure Storage.</span></span> <span data-ttu-id="5148d-109">Хранилище Azure обеспечивает хранение неструктурированных данных с функциями отказоустойчивости и высокой доступности.</span><span class="sxs-lookup"><span data-stu-id="5148d-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="5148d-110">Хранилище Azure включает в себя несколько структур данных, где можно хранить и получать доступ к данным и могут использовать службы хранилища hello из состава hello Azure SDK для Node.js или с помощью API-интерфейсов REST API-интерфейсы hello.</span><span class="sxs-lookup"><span data-stu-id="5148d-110">Azure Storage includes several data structures where you can store and access data, and you can leverage hello storage services from hello APIs included in hello Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="5148d-111">Дополнительные сведения см. в статье [Хранилище Azure].</span><span class="sxs-lookup"><span data-stu-id="5148d-111">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="5148d-112">В этом учебнике предполагается, что вы выполнили hello [веб-приложение Node.js] и [Node.js быстрое][Node.js веб-приложения с использованием экспресс-выпуск] учебники.</span><span class="sxs-lookup"><span data-stu-id="5148d-112">This tutorial assumes that you have completed hello [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="5148d-113">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="5148d-113">You will learn:</span></span>

* <span data-ttu-id="5148d-114">Как toowork с hello процессора Jade шаблона</span><span class="sxs-lookup"><span data-stu-id="5148d-114">How toowork with hello Jade template engine</span></span>
* <span data-ttu-id="5148d-115">Как toowork со службами управления данными Azure</span><span class="sxs-lookup"><span data-stu-id="5148d-115">How toowork with Azure Data Management services</span></span>

<span data-ttu-id="5148d-116">Снимок экрана приложения hello завершения используется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5148d-116">A screenshot of hello completed application is below:</span></span>

![Hello завершения веб-страницы в браузере internet explorer](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="5148d-118">Настройка учетных данных хранилища в файле Web.Config</span><span class="sxs-lookup"><span data-stu-id="5148d-118">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="5148d-119">tooaccess хранилища Azure, вы должны toopass в хранилище учетных данных.</span><span class="sxs-lookup"><span data-stu-id="5148d-119">tooaccess Azure Storage, you need toopass in storage credentials.</span></span> <span data-ttu-id="5148d-120">toodo это, можно использовать параметры приложения web.config.</span><span class="sxs-lookup"><span data-stu-id="5148d-120">toodo this, you utilize web.config application settings.</span></span>
<span data-ttu-id="5148d-121">Эти параметры передаются как tooNode переменные среды, который затем прочитан hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="5148d-121">Those settings will be passed as environment variables tooNode, which are then read by hello Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="5148d-122">Учетные данные хранилища используются только в том случае, когда приложение hello развернутой tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5148d-122">Storage credentials are only used when hello application is deployed tooAzure.</span></span> <span data-ttu-id="5148d-123">При выполнении в эмуляторе hello hello приложение будет использовать эмулятор хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="5148d-123">When running in hello emulator, hello application will use hello storage emulator.</span></span>
>
>

<span data-ttu-id="5148d-124">Выполните следующие учетные данные учетной записи хранения действия tooretrieve hello hello и добавить их toohello параметры файла web.config:</span><span class="sxs-lookup"><span data-stu-id="5148d-124">Perform hello following steps tooretrieve hello storage account credentials and add them toohello web.config settings:</span></span>

1. <span data-ttu-id="5148d-125">Если он не открыт, запустите hello Azure PowerShell из hello **запустить** меню, развернув **все программы, Azure**, щелкните правой кнопкой мыши **Azure PowerShell**, а затем выберите  **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="5148d-125">If it is not already open, start hello Azure PowerShell from hello **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="5148d-126">Измените каталоги toohello папку, содержащую приложение.</span><span class="sxs-lookup"><span data-stu-id="5148d-126">Change directories toohello folder containing your application.</span></span> <span data-ttu-id="5148d-127">Например, C:\\node\\tasklist\\WebRole1.</span><span class="sxs-lookup"><span data-stu-id="5148d-127">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="5148d-128">Hello окна Azure Powershell введите следующие сведения об учетной записи хранилища командлет tooretrieve hello hello:</span><span class="sxs-lookup"><span data-stu-id="5148d-128">From hello Azure Powershell window enter hello following cmdlet tooretrieve hello storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="5148d-129">Это возвращает hello список учетных записей хранилища и ключи, связанные с вашей размещенной службой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="5148d-129">This retrieves hello list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5148d-130">Поскольку hello Azure SDK создает учетную запись хранилища, при развертывании службы, учетную запись хранилища должна уже существовать от развертывания приложения в предыдущих направляющие hello.</span><span class="sxs-lookup"><span data-stu-id="5148d-130">Since hello Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in hello previous guides.</span></span>
   >
   >
4. <span data-ttu-id="5148d-131">Откройте hello **ServiceDefinition.csdef** файл, содержащий hello параметров среды, которые используются, когда приложение hello развернутой tooAzure:</span><span class="sxs-lookup"><span data-stu-id="5148d-131">Open hello **ServiceDefinition.csdef** file containing hello environment settings that are used when hello application is deployed tooAzure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="5148d-132">Блокировать INSERT hello ниже в разделе **среды** элемент, заменив {учетной записи ХРАНИЛИЩА} и {ключ доступа к ХРАНИЛИЩУ} с именем учетной записи hello и hello первичный ключ для учетной записи хранения hello требуется toouse для развертывания:</span><span class="sxs-lookup"><span data-stu-id="5148d-132">Insert hello following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with hello account name and hello primary key for hello storage account you want toouse for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![содержимое файла web.cloud.config Hello](./media/storage-nodejs-use-table-storage-cloud-service-app/node37.png)

6. <span data-ttu-id="5148d-134">Сохраните файл hello и закройте Блокнот.</span><span class="sxs-lookup"><span data-stu-id="5148d-134">Save hello file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="5148d-135">Установка дополнительных модулей</span><span class="sxs-lookup"><span data-stu-id="5148d-135">Install additional modules</span></span>
1. <span data-ttu-id="5148d-136">Используйте hello, следующая команда tooinstall hello [azure], [uuid узел], [nconf] и [асинхронных] модулей локально, а также toosave запись для них toohello **package.json** файла:</span><span class="sxs-lookup"><span data-stu-id="5148d-136">Use hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules locally as well as toosave an entry for them toohello **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="5148d-137">Hello выходные данные этой команды должен выглядеть примерно toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="5148d-137">hello output of this command should appear similar toohello following:</span></span>

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

## <a name="using-hello-table-service-in-a-node-application"></a><span data-ttu-id="5148d-138">Использование службы таблиц hello в приложении узла</span><span class="sxs-lookup"><span data-stu-id="5148d-138">Using hello Table service in a node application</span></span>
<span data-ttu-id="5148d-139">В этом разделе можно расширить hello основных приложений, созданных hello **express** команду, добавив **task.js** файл, содержащий модель hello для ваших задач.</span><span class="sxs-lookup"><span data-stu-id="5148d-139">In this section you will extend hello basic application created by hello **express** command by adding a **task.js** file which contains hello model for your tasks.</span></span> <span data-ttu-id="5148d-140">Вы также измените существующие hello **в файле app.js** и создайте новый **tasklist.js** файла, который использует модель hello.</span><span class="sxs-lookup"><span data-stu-id="5148d-140">You will also modify hello existing **app.js** and create a new **tasklist.js** file that uses hello model.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="5148d-141">Создание модели hello</span><span class="sxs-lookup"><span data-stu-id="5148d-141">Create hello model</span></span>
1. <span data-ttu-id="5148d-142">В hello **WebRole1** каталога, создайте новый каталог с именем **моделей**.</span><span class="sxs-lookup"><span data-stu-id="5148d-142">In hello **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="5148d-143">В hello **моделей** каталога, создайте новый файл с именем **task.js**.</span><span class="sxs-lookup"><span data-stu-id="5148d-143">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="5148d-144">Этот файл будет содержать hello модель для hello задачи, созданные вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="5148d-144">This file will contain hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="5148d-145">В начале hello hello **task.js** файл, добавить следующие tooreference необходимые библиотеки кода hello:</span><span class="sxs-lookup"><span data-stu-id="5148d-145">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="5148d-146">Далее необходимо добавить код toodefine и экспорт hello объекта задачи.</span><span class="sxs-lookup"><span data-stu-id="5148d-146">Next, you will add code toodefine and export hello Task object.</span></span> <span data-ttu-id="5148d-147">Этот объект отвечает за подключение toohello таблицы.</span><span class="sxs-lookup"><span data-stu-id="5148d-147">This object is responsible for connecting toohello table.</span></span>

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

5. <span data-ttu-id="5148d-148">Добавьте hello следующие дополнительные методы toodefine кода hello объекта задачи, которые позволяют взаимодействия с данными, хранящимися в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="5148d-148">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>

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

6. <span data-ttu-id="5148d-149">Сохраните и закройте hello **task.js** файла.</span><span class="sxs-lookup"><span data-stu-id="5148d-149">Save and close hello **task.js** file.</span></span>

### <a name="create-hello-controller"></a><span data-ttu-id="5148d-150">Создание контроллера hello</span><span class="sxs-lookup"><span data-stu-id="5148d-150">Create hello controller</span></span>
1. <span data-ttu-id="5148d-151">В hello **WebRole1/маршруты** каталога, создайте новый файл с именем **tasklist.js** и откройте его в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="5148d-151">In hello **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="5148d-152">Добавьте следующий код слишком hello**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="5148d-152">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="5148d-153">Это загружает hello azure и async модули, в которых используются **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="5148d-153">This loads hello azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="5148d-154">Этот параметр также определяет hello **TaskList** функции, которая передается экземпляр hello **задачи** объекта было определено ранее:</span><span class="sxs-lookup"><span data-stu-id="5148d-154">This also defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="5148d-155">Продолжайте добавлять toohello **tasklist.js** файла путем добавления методов hello используется слишком**showTasks**, **addTask**, и **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="5148d-155">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks**, **addTask**, and **completeTasks**:</span></span>

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

4. <span data-ttu-id="5148d-156">Сохранить hello **tasklist.js** файла.</span><span class="sxs-lookup"><span data-stu-id="5148d-156">Save hello **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="5148d-157">Изменение app.js</span><span class="sxs-lookup"><span data-stu-id="5148d-157">Modify app.js</span></span>
1. <span data-ttu-id="5148d-158">В hello **WebRole1** каталог, откройте hello **в файле app.js** файл в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="5148d-158">In hello **WebRole1** directory, open hello **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="5148d-159">В начале файла hello hello, добавьте следующий модуль hello azure tooload hello и установите ключ имени и секций таблицы hello:</span><span class="sxs-lookup"><span data-stu-id="5148d-159">At hello beginning of hello file, add hello following tooload hello azure module and set hello table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="5148d-160">В файле в файле app.js hello, прокрутите вниз toowhere вы видите hello следующую строку:</span><span class="sxs-lookup"><span data-stu-id="5148d-160">In hello app.js file, scroll down toowhere you see hello following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="5148d-161">Замените приведенный ниже код hello hello выше строк.</span><span class="sxs-lookup"><span data-stu-id="5148d-161">Replace hello above lines with hello code shown below.</span></span> <span data-ttu-id="5148d-162">Это будет инициализировать экземпляр <strong>задачи</strong> с учетной записью хранилища tooyour соединения.</span><span class="sxs-lookup"><span data-stu-id="5148d-162">This will initialize an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="5148d-163">Аргумент передается toohello <strong>TaskList</strong>, который будет использовать toocommunicate с hello службы таблиц:</span><span class="sxs-lookup"><span data-stu-id="5148d-163">This is passed toohello <strong>TaskList</strong>, which will use it toocommunicate with hello Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="5148d-164">Сохранить hello **в файле app.js** файл.</span><span class="sxs-lookup"><span data-stu-id="5148d-164">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="5148d-165">Изменить представление index hello</span><span class="sxs-lookup"><span data-stu-id="5148d-165">Modify hello index view</span></span>
1. <span data-ttu-id="5148d-166">Измените каталоги toohello **представления** каталог и откройте hello **index.jade** файл в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="5148d-166">Change directories toohello **views** directory and open hello **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="5148d-167">Замените содержимое hello hello **index.jade** файл hello код, приведенный ниже.</span><span class="sxs-lookup"><span data-stu-id="5148d-167">Replace hello contents of hello **index.jade** file with hello code below.</span></span> <span data-ttu-id="5148d-168">Этот параметр определяет hello представление для отображения существующих задач, а также форму для добавления новых задач и пометить существующих как завершенное.</span><span class="sxs-lookup"><span data-stu-id="5148d-168">This defines hello view for displaying existing tasks, as well as a form for adding new tasks and marking existing ones as completed.</span></span>

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

3. <span data-ttu-id="5148d-169">Сохраните и закройте файл **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="5148d-169">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="5148d-170">Изменить макет глобального hello</span><span class="sxs-lookup"><span data-stu-id="5148d-170">Modify hello global layout</span></span>
<span data-ttu-id="5148d-171">Hello **layout.jade** файла в hello **представления** каталог используется как глобальный шаблон для других **.jade** файлов.</span><span class="sxs-lookup"><span data-stu-id="5148d-171">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="5148d-172">На этом этапе вы измените его toouse [Twitter начальной загрузки](https://github.com/twbs/bootstrap), который — это набор средств, который позволяет легко toodesign работы с низким приоритетом привлекательных веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="5148d-172">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span>

1. <span data-ttu-id="5148d-173">Загрузите и извлеките файлы hello для [Twitter начальной загрузки](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="5148d-173">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="5148d-174">Копировать hello **bootstrap.min.css** файл из hello **начальной загрузки\\dist\\css** toohello папки **открытый\\таблицы стилей** каталог приложения списка задач.</span><span class="sxs-lookup"><span data-stu-id="5148d-174">Copy hello **bootstrap.min.css** file from hello **bootstrap\\dist\\css** folder toohello **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="5148d-175">Из hello **представления** папки, откройте hello **layout.jade** в текстовый редактор и замены hello содержимое вашего hello следующее:</span><span class="sxs-lookup"><span data-stu-id="5148d-175">From hello **views** folder, open hello **layout.jade** in your text editor and replace hello contents with hello following:</span></span>

    <span data-ttu-id="5148d-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span><span class="sxs-lookup"><span data-stu-id="5148d-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="5148d-177">Сохранить hello **layout.jade** файла.</span><span class="sxs-lookup"><span data-stu-id="5148d-177">Save hello **layout.jade** file.</span></span>

### <a name="running-hello-application-in-hello-emulator"></a><span data-ttu-id="5148d-178">Выполнение приложения hello в эмуляторе hello</span><span class="sxs-lookup"><span data-stu-id="5148d-178">Running hello Application in hello Emulator</span></span>
<span data-ttu-id="5148d-179">Используйте следующие команды toostart hello приложения в эмуляторе hello hello.</span><span class="sxs-lookup"><span data-stu-id="5148d-179">Use hello following command toostart hello application in hello emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="5148d-180">Hello браузера открывается и отображает hello следующие страницы:</span><span class="sxs-lookup"><span data-stu-id="5148d-180">hello browser will open and displays hello following page:</span></span>

![Веб-сайт, разбитых на страницы под названием My списка задач с таблицей, содержащей задачи и поля tooadd новую задачу.](./media/storage-nodejs-use-table-storage-cloud-service-app/node44.png)

<span data-ttu-id="5148d-182">Использовать элементы tooadd формы hello, или удалить существующие элементы, помечая их как завершенное.</span><span class="sxs-lookup"><span data-stu-id="5148d-182">Use hello form tooadd items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="5148d-183">Публикация tooAzure приложения hello</span><span class="sxs-lookup"><span data-stu-id="5148d-183">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="5148d-184">В окне приветствия Windows PowerShell вызовите hello, выполнив командлет tooredeploy tooAzure вашей размещенной службы.</span><span class="sxs-lookup"><span data-stu-id="5148d-184">In hello Windows PowerShell window, call hello following cmdlet tooredeploy your hosted service tooAzure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="5148d-185">Замените **myuniquename** уникальным именем приложения.</span><span class="sxs-lookup"><span data-stu-id="5148d-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="5148d-186">Замените **datacentername** с именем hello центр обработки данных Azure, такие как **Запад США**.</span><span class="sxs-lookup"><span data-stu-id="5148d-186">Replace **datacentername** with hello name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="5148d-187">По завершении развертывания hello появится ответ аналогичные toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="5148d-187">After hello deployment is complete, you should see a response similar toohello following:</span></span>

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

<span data-ttu-id="5148d-188">Как и раньше так как указан hello **-запустите** параметр hello браузер открывается и отображает вашего приложения, работающего в Azure, после завершения публикации.</span><span class="sxs-lookup"><span data-stu-id="5148d-188">As before, because you specified hello **-launch** option, hello browser opens and displays your application running in Azure when publishing is completed.</span></span>

![Окно браузера, отображения страницы приветствия Мой список задач.](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="5148d-191">Остановка и удаление приложения</span><span class="sxs-lookup"><span data-stu-id="5148d-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="5148d-192">После развертывания приложения, вы можете toodisable, чтобы избежать расходов или построения и развертывания других приложений в пределах hello бесплатно пробного периода.</span><span class="sxs-lookup"><span data-stu-id="5148d-192">After deploying your application, you may want toodisable it so you can avoid costs or build and deploy other applications within hello free trial time period.</span></span>

<span data-ttu-id="5148d-193">Для экземпляров веб-роли Azure выставляет счета за почасовое использование серверного времени.</span><span class="sxs-lookup"><span data-stu-id="5148d-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="5148d-194">После развертывания приложения даже в том случае, если экземпляры не запущены и находятся в состоянии остановки hello потребляются времени сервера.</span><span class="sxs-lookup"><span data-stu-id="5148d-194">Server time is consumed once your application is deployed, even if the instances are not running and are in hello stopped state.</span></span>

<span data-ttu-id="5148d-195">Hello следующие шаги показывают, как toostop и удалить приложение.</span><span class="sxs-lookup"><span data-stu-id="5148d-195">hello following steps show you how toostop and delete your application.</span></span>

1. <span data-ttu-id="5148d-196">В окне приветствия Windows PowerShell Остановите развертывание службы hello, созданным в предыдущем разделе hello, hello, выполнив командлет:</span><span class="sxs-lookup"><span data-stu-id="5148d-196">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="5148d-197">Остановка службы hello может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="5148d-197">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="5148d-198">При остановке службы hello, появляется сообщение о том, что он был остановлен.</span><span class="sxs-lookup"><span data-stu-id="5148d-198">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="5148d-199">Служба toodelete hello, вызов hello, выполнив командлет:</span><span class="sxs-lookup"><span data-stu-id="5148d-199">toodelete hello service, call hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="5148d-200">При появлении запроса введите **Y** toodelete hello службы.</span><span class="sxs-lookup"><span data-stu-id="5148d-200">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="5148d-201">Удаление службы hello может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="5148d-201">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="5148d-202">После удаления службы hello появится сообщение, указывающее на то, что служба hello была удалена.</span><span class="sxs-lookup"><span data-stu-id="5148d-202">After hello service has been deleted you receive a message indicating that hello service was deleted.</span></span>

[Node.js веб-приложения с использованием экспресс-выпуск]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[Хранилище Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[веб-приложение Node.js]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


