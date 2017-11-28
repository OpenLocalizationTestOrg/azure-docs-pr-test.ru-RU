---
title: "Веб-приложение с хранилищем таблиц (Node.js) | Документация Майкрософт"
description: "В этом коротком уроке вы научитесь создавать веб-приложение посредством добавления служб хранилища Azure и модуля Azure."
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
ms.openlocfilehash: 5d7ee2f529b5127ee60ec8b4f5acaa49e75ddf39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="8d85e-103">Веб-приложение Node.js, использующее хранилище</span><span class="sxs-lookup"><span data-stu-id="8d85e-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="8d85e-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="8d85e-104">Overview</span></span>
<span data-ttu-id="8d85e-105">В этом руководстве мы расширим возможности приложения, создание которого описано в статье [Создание веб-приложения Node.js с использованием модуля Express в облачной службе Azure], с помощью клиентских библиотек Microsoft Azure для Node.js, которые позволяют работать со службами управления данными.</span><span class="sxs-lookup"><span data-stu-id="8d85e-105">In this tutorial, you will extend the application created in the [Node.js Web Application using Express] tutorial by using the Microsoft Azure Client Libraries for Node.js to work with data management services.</span></span> <span data-ttu-id="8d85e-106">Вы расширите возможности приложения за счет создания веб-приложения списка задач, которое можно развернуть в Azure.</span><span class="sxs-lookup"><span data-stu-id="8d85e-106">You will extend your application to create a web-based task-list application that you can deploy to Azure.</span></span> <span data-ttu-id="8d85e-107">Список задач позволяет пользователю извлекать задачи, добавлять новые задачи и помечать задачи как завершенные.</span><span class="sxs-lookup"><span data-stu-id="8d85e-107">The task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="8d85e-108">Элементы задач хранятся в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="8d85e-108">The task items are stored in Azure Storage.</span></span> <span data-ttu-id="8d85e-109">Хранилище Azure обеспечивает хранение неструктурированных данных с функциями отказоустойчивости и высокой доступности.</span><span class="sxs-lookup"><span data-stu-id="8d85e-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="8d85e-110">Хранилище Azure включает в себя несколько структур данных, где можно хранить данные и осуществлять доступ к ним, кроме того, вы можете использовать службы хранилища с помощью API, включенных в состав пакета SDK для Azure для Node.js, или через REST API.</span><span class="sxs-lookup"><span data-stu-id="8d85e-110">Azure Storage includes several data structures where you can store and access data, and you can leverage the storage services from the APIs included in the Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="8d85e-111">Дополнительные сведения см. в статье [Хранилище Azure].</span><span class="sxs-lookup"><span data-stu-id="8d85e-111">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="8d85e-112">Прежде чем приступать к работе с этим руководством, необходимо ознакомиться со статьями [Построение и развертывание приложения Node.js в облачной службе Azure], [Node.js с Express] и [Создание веб-приложения Node.js с использованием модуля Express в облачной службе Azure].</span><span class="sxs-lookup"><span data-stu-id="8d85e-112">This tutorial assumes that you have completed the [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="8d85e-113">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="8d85e-113">You will learn:</span></span>

* <span data-ttu-id="8d85e-114">Как работать с подсистемой шаблонов Jade</span><span class="sxs-lookup"><span data-stu-id="8d85e-114">How to work with the Jade template engine</span></span>
* <span data-ttu-id="8d85e-115">Как работать со службами управления данными Azure</span><span class="sxs-lookup"><span data-stu-id="8d85e-115">How to work with Azure Data Management services</span></span>

<span data-ttu-id="8d85e-116">Снимок экрана завершенного приложения приведен ниже:</span><span class="sxs-lookup"><span data-stu-id="8d85e-116">A screenshot of the completed application is below:</span></span>

![Готовая веб-страница в Internet Explorer](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="8d85e-118">Настройка учетных данных хранилища в файле Web.Config</span><span class="sxs-lookup"><span data-stu-id="8d85e-118">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="8d85e-119">Для доступа к службе хранилища Azure необходимо передать учетные данные хранилища.</span><span class="sxs-lookup"><span data-stu-id="8d85e-119">To access Azure Storage, you need to pass in storage credentials.</span></span> <span data-ttu-id="8d85e-120">Для этого используются параметры приложения web.config.</span><span class="sxs-lookup"><span data-stu-id="8d85e-120">To do this, you utilize web.config application settings.</span></span>
<span data-ttu-id="8d85e-121">Эти параметры передаются в качестве переменных среды в Node, которые затем считываются пакетом SDK для Azure.</span><span class="sxs-lookup"><span data-stu-id="8d85e-121">Those settings will be passed as environment variables to Node, which are then read by the Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="8d85e-122">Учетные данные хранилища используются только при развертывании приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="8d85e-122">Storage credentials are only used when the application is deployed to Azure.</span></span> <span data-ttu-id="8d85e-123">При запуске в эмуляторе приложение будет использовать эмулятор хранения.</span><span class="sxs-lookup"><span data-stu-id="8d85e-123">When running in the emulator, the application will use the storage emulator.</span></span>
>
>

<span data-ttu-id="8d85e-124">Выполните следующие действия, чтобы получить учетные данные учетной записи хранения и добавить их в параметры web.config:</span><span class="sxs-lookup"><span data-stu-id="8d85e-124">Perform the following steps to retrieve the storage account credentials and add them to the web.config settings:</span></span>

1. <span data-ttu-id="8d85e-125">Если это еще не сделано, запустите Azure PowerShell из меню **Пуск**. Для этого разверните пункты **Все программы, Azure**, щелкните правой кнопкой мыши **Azure PowerShell** и выберите **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="8d85e-125">If it is not already open, start the Azure PowerShell from the **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="8d85e-126">Перейдите к папке, содержащей ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="8d85e-126">Change directories to the folder containing your application.</span></span> <span data-ttu-id="8d85e-127">Например, C:\\node\\tasklist\\WebRole1.</span><span class="sxs-lookup"><span data-stu-id="8d85e-127">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="8d85e-128">В окне Azure Powershell введите следующий командлет, чтобы получить сведения об учетной записи хранения:</span><span class="sxs-lookup"><span data-stu-id="8d85e-128">From the Azure Powershell window enter the following cmdlet to retrieve the storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="8d85e-129">При этом извлекается список учетных записей хранилища и ключей учетной записи, связанных с вашей размещенной службой.</span><span class="sxs-lookup"><span data-stu-id="8d85e-129">This retrieves the list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8d85e-130">Поскольку пакет Azure SDK создает учетную запись хранения при развертывании службы, учетная запись хранения должна уже существовать в связи с развертыванием приложения в предыдущих руководствах.</span><span class="sxs-lookup"><span data-stu-id="8d85e-130">Since the Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in the previous guides.</span></span>
   >
   >
4. <span data-ttu-id="8d85e-131">Откройте файл **ServiceDefinition.csdef**, содержащий параметры среды, которые используются при развертывании приложения в Azure:</span><span class="sxs-lookup"><span data-stu-id="8d85e-131">Open the **ServiceDefinition.csdef** file containing the environment settings that are used when the application is deployed to Azure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="8d85e-132">Вставьте следующий блок под элементом **Environment**, заменив {STORAGE ACCOUNT} и {STORAGE ACCESS KEY} именем учетной записи и первичным ключом для учетной записи хранения, которые будут использоваться для развертывания:</span><span class="sxs-lookup"><span data-stu-id="8d85e-132">Insert the following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with the account name and the primary key for the storage account you want to use for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![Содержимое файла web.cloud.config](./media/storage-nodejs-use-table-storage-cloud-service-app/node37.png)

6. <span data-ttu-id="8d85e-134">Сохраните файл и закройте Блокнот.</span><span class="sxs-lookup"><span data-stu-id="8d85e-134">Save the file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="8d85e-135">Установка дополнительных модулей</span><span class="sxs-lookup"><span data-stu-id="8d85e-135">Install additional modules</span></span>
1. <span data-ttu-id="8d85e-136">Используйте следующую команду, чтобы установить модули [azure], [node-uuid], [nconf] и [async] локально, а также чтобы сохранить запись для них в файле **package.json**:</span><span class="sxs-lookup"><span data-stu-id="8d85e-136">Use the following command to install the [azure], [node-uuid], [nconf] and [async] modules locally as well as to save an entry for them to the **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="8d85e-137">Результат этой команды должен выглядеть аналогично следующему:</span><span class="sxs-lookup"><span data-stu-id="8d85e-137">The output of this command should appear similar to the following:</span></span>

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

## <a name="using-the-table-service-in-a-node-application"></a><span data-ttu-id="8d85e-138">Использование службы таблиц в приложении Node</span><span class="sxs-lookup"><span data-stu-id="8d85e-138">Using the Table service in a node application</span></span>
<span data-ttu-id="8d85e-139">В этом разделе базовое приложение, созданное командой **express**, будет расширено при добавлении файла **task.js**, который содержит модель для ваших задач.</span><span class="sxs-lookup"><span data-stu-id="8d85e-139">In this section you will extend the basic application created by the **express** command by adding a **task.js** file which contains the model for your tasks.</span></span> <span data-ttu-id="8d85e-140">Также будет изменен существующий файл **app.js** и создан новый файл **tasklist.js**, который использует эту модель.</span><span class="sxs-lookup"><span data-stu-id="8d85e-140">You will also modify the existing **app.js** and create a new **tasklist.js** file that uses the model.</span></span>

### <a name="create-the-model"></a><span data-ttu-id="8d85e-141">Создание модели</span><span class="sxs-lookup"><span data-stu-id="8d85e-141">Create the model</span></span>
1. <span data-ttu-id="8d85e-142">В каталоге **WebRole1** создайте каталог с именем **models**.</span><span class="sxs-lookup"><span data-stu-id="8d85e-142">In the **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="8d85e-143">В каталоге **models** создайте файл с именем **task.js**.</span><span class="sxs-lookup"><span data-stu-id="8d85e-143">In the **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="8d85e-144">Этот файл будет содержать модель для задач, создаваемых приложением.</span><span class="sxs-lookup"><span data-stu-id="8d85e-144">This file will contain the model for the tasks created by your application.</span></span>
3. <span data-ttu-id="8d85e-145">В начале файла **task.js** добавьте следующий код для ссылки на необходимые библиотеки:</span><span class="sxs-lookup"><span data-stu-id="8d85e-145">At the beginning of the **task.js** file, add the following code to reference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="8d85e-146">Далее будет добавлен код для определения и экспорта объекта Task.</span><span class="sxs-lookup"><span data-stu-id="8d85e-146">Next, you will add code to define and export the Task object.</span></span> <span data-ttu-id="8d85e-147">Этот объект отвечает за подключение к таблице.</span><span class="sxs-lookup"><span data-stu-id="8d85e-147">This object is responsible for connecting to the table.</span></span>

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

5. <span data-ttu-id="8d85e-148">Затем добавьте следующий код, чтобы определить дополнительные методы для объекта Task, обеспечивающего взаимодействие с данными, хранящимися в таблице:</span><span class="sxs-lookup"><span data-stu-id="8d85e-148">Next, add the following code to define additional methods on the Task object, which allow interactions with data stored in the table:</span></span>

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
        // use entityGenerator to set types
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

6. <span data-ttu-id="8d85e-149">Сохраните и закройте файл **task.js** .</span><span class="sxs-lookup"><span data-stu-id="8d85e-149">Save and close the **task.js** file.</span></span>

### <a name="create-the-controller"></a><span data-ttu-id="8d85e-150">Создание контроллера</span><span class="sxs-lookup"><span data-stu-id="8d85e-150">Create the controller</span></span>
1. <span data-ttu-id="8d85e-151">В каталоге **WebRole1/routes** создайте файл с именем **tasklist.js** и откройте его в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="8d85e-151">In the **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="8d85e-152">Добавьте в **tasklist.js**следующий код.</span><span class="sxs-lookup"><span data-stu-id="8d85e-152">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="8d85e-153">Он загружает модули azure и async, используемые **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="8d85e-153">This loads the azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="8d85e-154">Он также определяет функцию **TaskList**, передающую экземпляр объекта **Task**, определенного ранее:</span><span class="sxs-lookup"><span data-stu-id="8d85e-154">This also defines the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="8d85e-155">Продолжайте добавление в файл **tasklist.js** методов, используемых для **showTasks**, **addTask** и **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="8d85e-155">Continue adding to the **tasklist.js** file by adding the methods used to **showTasks**, **addTask**, and **completeTasks**:</span></span>

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

4. <span data-ttu-id="8d85e-156">Сохраните файл **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="8d85e-156">Save the **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="8d85e-157">Изменение app.js</span><span class="sxs-lookup"><span data-stu-id="8d85e-157">Modify app.js</span></span>
1. <span data-ttu-id="8d85e-158">В каталоге **WebRole1** откройте файл **app.js** в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="8d85e-158">In the **WebRole1** directory, open the **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="8d85e-159">В начале файла добавьте следующий код для загрузки модуля Аzure, а также задания имение таблицы и ключа раздела (partitionKey):</span><span class="sxs-lookup"><span data-stu-id="8d85e-159">At the beginning of the file, add the following to load the azure module and set the table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="8d85e-160">Прокрутите файл app.js вниз до появления следующей строки:</span><span class="sxs-lookup"><span data-stu-id="8d85e-160">In the app.js file, scroll down to where you see the following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="8d85e-161">Замените вышеприведенные строки на код, приведенный ниже.</span><span class="sxs-lookup"><span data-stu-id="8d85e-161">Replace the above lines with the code shown below.</span></span> <span data-ttu-id="8d85e-162">Код инициализирует экземпляр <strong>Task</strong> , используя подключение к вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="8d85e-162">This will initialize an instance of <strong>Task</strong> with a connection to your storage account.</span></span> <span data-ttu-id="8d85e-163">Он передается в <strong>TaskList</strong>, где будет использоваться для обмена данными со службой таблиц:</span><span class="sxs-lookup"><span data-stu-id="8d85e-163">This is passed to the <strong>TaskList</strong>, which will use it to communicate with the Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="8d85e-164">Сохраните файл **app.js** .</span><span class="sxs-lookup"><span data-stu-id="8d85e-164">Save the **app.js** file.</span></span>

### <a name="modify-the-index-view"></a><span data-ttu-id="8d85e-165">Изменение представления индекса</span><span class="sxs-lookup"><span data-stu-id="8d85e-165">Modify the index view</span></span>
1. <span data-ttu-id="8d85e-166">Измените каталоги на каталог **views** и откройте файл **index.jade** в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="8d85e-166">Change directories to the **views** directory and open the **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="8d85e-167">Заменит содержимое файла **index.jade** кодом, приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="8d85e-167">Replace the contents of the **index.jade** file with the code below.</span></span> <span data-ttu-id="8d85e-168">Он определяет представление для отображения существующих задач, а также форму для добавления новых задач и пометки существующих задач как завершенных.</span><span class="sxs-lookup"><span data-stu-id="8d85e-168">This defines the view for displaying existing tasks, as well as a form for adding new tasks and marking existing ones as completed.</span></span>

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

3. <span data-ttu-id="8d85e-169">Сохраните и закройте файл **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="8d85e-169">Save and close **index.jade** file.</span></span>

### <a name="modify-the-global-layout"></a><span data-ttu-id="8d85e-170">Изменение глобального макета</span><span class="sxs-lookup"><span data-stu-id="8d85e-170">Modify the global layout</span></span>
<span data-ttu-id="8d85e-171">Файл **layout.jade** в каталоге **views** используется как глобальный шаблон для других файлов **.jade**.</span><span class="sxs-lookup"><span data-stu-id="8d85e-171">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="8d85e-172">На этом шаге он будет изменен для использования [Twitter Bootstrap](https://github.com/twbs/bootstrap)— набора средств, упрощающих разработку привлекательного веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="8d85e-172">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span></span>

1. <span data-ttu-id="8d85e-173">Загрузите и извлеките файлы [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="8d85e-173">Download and extract the files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="8d85e-174">Скопируйте файл **bootstrap.min.css** из папки **bootstrap\\dist\\css** в каталог **public\\stylesheets** своего приложения tasklist.</span><span class="sxs-lookup"><span data-stu-id="8d85e-174">Copy the **bootstrap.min.css** file from the **bootstrap\\dist\\css** folder to the **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="8d85e-175">В папке **views** откройте файл **layout.jade** в текстовом редакторе и замените его содержимое следующим:</span><span class="sxs-lookup"><span data-stu-id="8d85e-175">From the **views** folder, open the **layout.jade** in your text editor and replace the contents with the following:</span></span>

    <span data-ttu-id="8d85e-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span><span class="sxs-lookup"><span data-stu-id="8d85e-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="8d85e-177">Сохраните файл **layout.jade**.</span><span class="sxs-lookup"><span data-stu-id="8d85e-177">Save the **layout.jade** file.</span></span>

### <a name="running-the-application-in-the-emulator"></a><span data-ttu-id="8d85e-178">Запуск приложения в эмуляторе</span><span class="sxs-lookup"><span data-stu-id="8d85e-178">Running the Application in the Emulator</span></span>
<span data-ttu-id="8d85e-179">Выполните следующую команду, чтобы проверить приложение в эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="8d85e-179">Use the following command to start the application in the emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="8d85e-180">Браузер открывается и отображает следующую страницу:</span><span class="sxs-lookup"><span data-stu-id="8d85e-180">The browser will open and displays the following page:</span></span>

![Веб-страница под названием My Task List ("Мой список задач") с таблицей, содержащей задачи, и поля для добавления новой задачи](./media/storage-nodejs-use-table-storage-cloud-service-app/node44.png)

<span data-ttu-id="8d85e-182">Используйте форму для добавления или удаления существующих элементом, помечая их как завершенные.</span><span class="sxs-lookup"><span data-stu-id="8d85e-182">Use the form to add items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-the-application-to-azure"></a><span data-ttu-id="8d85e-183">Публикация приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="8d85e-183">Publishing the Application to Azure</span></span>
<span data-ttu-id="8d85e-184">В окне Windows PowerShell вызовите следующий командлет, чтобы повторно развернуть размещенную службу в Azure.</span><span class="sxs-lookup"><span data-stu-id="8d85e-184">In the Windows PowerShell window, call the following cmdlet to redeploy your hosted service to Azure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="8d85e-185">Замените **myuniquename** уникальным именем приложения.</span><span class="sxs-lookup"><span data-stu-id="8d85e-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="8d85e-186">Замените **datacentername** именем центра обработки данных Azure, например **West US**.</span><span class="sxs-lookup"><span data-stu-id="8d85e-186">Replace **datacentername** with the name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="8d85e-187">После завершения развертывания должен появиться ответ, похожий на следующий:</span><span class="sxs-lookup"><span data-stu-id="8d85e-187">After the deployment is complete, you should see a response similar to the following:</span></span>

```
  PS C:\node\tasklist> publish-azureserviceproject -servicename tasklist -location "West US"
  WARNING: Publishing tasklist to Microsoft Azure. This may take several minutes...
  WARNING: 2:18:42 PM - Preparing runtime deployment for service 'tasklist'
  WARNING: 2:18:42 PM - Verifying storage account 'tasklist'...
  WARNING: 2:18:43 PM - Preparing deployment for tasklist with Subscription ID: 65a1016d-0f67-45d2-b838-b8f373d6d52e...
  WARNING: 2:19:01 PM - Connecting...
  WARNING: 2:19:02 PM - Uploading Package to storage service larrystore...
  WARNING: 2:19:40 PM - Upgrading...
  WARNING: 2:22:48 PM - Created Deployment ID: b7134ab29b1249ff84ada2bd157f296a.
  WARNING: 2:22:48 PM - Initializing...
  WARNING: 2:22:49 PM - Instance WebRole1_IN_0 of role WebRole1 is ready.
  WARNING: 2:22:50 PM - Created Website URL: http://tasklist.cloudapp.net/.
```

<span data-ttu-id="8d85e-188">Как и раньше, благодаря указанию параметра **-launch**, после завершения публикации браузер открывает и отображает приложение, запущенное в Azure.</span><span class="sxs-lookup"><span data-stu-id="8d85e-188">As before, because you specified the **-launch** option, the browser opens and displays your application running in Azure when publishing is completed.</span></span>

![В окне браузера отображается страница «Мой список задач».](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="8d85e-191">Остановка и удаление приложения</span><span class="sxs-lookup"><span data-stu-id="8d85e-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="8d85e-192">После развертывания приложения может потребоваться отключить его, чтобы сократить затраты или построить и развернуть другие приложения в течение периода бесплатного пробного использования.</span><span class="sxs-lookup"><span data-stu-id="8d85e-192">After deploying your application, you may want to disable it so you can avoid costs or build and deploy other applications within the free trial time period.</span></span>

<span data-ttu-id="8d85e-193">Для экземпляров веб-роли Azure выставляет счета за почасовое использование серверного времени.</span><span class="sxs-lookup"><span data-stu-id="8d85e-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="8d85e-194">Время использования сервера отсчитывается с момента развертывания приложения, даже если экземпляры не запущены и пребывают в остановленном состоянии.</span><span class="sxs-lookup"><span data-stu-id="8d85e-194">Server time is consumed once your application is deployed, even if the instances are not running and are in the stopped state.</span></span>

<span data-ttu-id="8d85e-195">Ниже показано, как остановить и удалить приложение.</span><span class="sxs-lookup"><span data-stu-id="8d85e-195">The following steps show you how to stop and delete your application.</span></span>

1. <span data-ttu-id="8d85e-196">В окне Windows PowerShell остановите развертывание службы, созданное в предыдущем разделе со следующего командлета:</span><span class="sxs-lookup"><span data-stu-id="8d85e-196">In the Windows PowerShell window, stop the service deployment created in the previous section with the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="8d85e-197">Остановка службы может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="8d85e-197">Stopping the service may take several minutes.</span></span> <span data-ttu-id="8d85e-198">Если эта служба остановлена, появится сообщение, указывающее на то, что она была остановлена.</span><span class="sxs-lookup"><span data-stu-id="8d85e-198">When the service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="8d85e-199">Чтобы удалить службу, вызовите следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="8d85e-199">To delete the service, call the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="8d85e-200">При появлении запроса введите **Y** , чтобы удалить службу.</span><span class="sxs-lookup"><span data-stu-id="8d85e-200">When prompted, enter **Y** to delete the service.</span></span>

   <span data-ttu-id="8d85e-201">Удаление службы может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="8d85e-201">Deleting the service may take several minutes.</span></span> <span data-ttu-id="8d85e-202">После удаления службы появится сообщение, указывающее, что служба была удалена.</span><span class="sxs-lookup"><span data-stu-id="8d85e-202">After the service has been deleted you receive a message indicating that the service was deleted.</span></span>

<span data-ttu-id="8d85e-203">[Создание веб-приложения Node.js с использованием модуля Express в облачной службе Azure]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/</span><span class="sxs-lookup"><span data-stu-id="8d85e-203">[Node.js Web Application using Express]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/</span></span>
<span data-ttu-id="8d85e-204">[Хранилище Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx</span><span class="sxs-lookup"><span data-stu-id="8d85e-204">[Storing and Accessing Data in Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx</span></span>
<span data-ttu-id="8d85e-205">[Построение и развертывание приложения Node.js в облачной службе Azure]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/</span><span class="sxs-lookup"><span data-stu-id="8d85e-205">[Node.js Web Application]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/</span></span>


