---
title: "Веб-приложение Node.js, использующее службу таблиц Azure"
description: "В этом учебнике объясняется, как использовать службу таблиц Azure для сохранения данных из приложения Node.js, которое размещено в веб-приложениях службы приложений Azure."
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
ms.openlocfilehash: 3252914934c1084a165fa39ee983d3039e04d567
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="nodejs-web-app-using-the-azure-table-service"></a><span data-ttu-id="ffb06-103">Веб-приложение Node.js, использующее службу таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="ffb06-103">Node.js web app using the Azure Table Service</span></span>
## <a name="overview"></a><span data-ttu-id="ffb06-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="ffb06-104">Overview</span></span>
<span data-ttu-id="ffb06-105">В этом руководстве показано, как использовать службу таблиц на базе службы управления данными Azure для хранения данных и доступа к ним из приложения [node], размещенного в среде веб-приложений [службы приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="ffb06-105">This tutorial shows you how to use Table service provided by Azure Data Management to store and access data from a [node] application hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="ffb06-106">Этот учебный курс разработан для читателей, обладающих определенным опытом использования Node и [Git].</span><span class="sxs-lookup"><span data-stu-id="ffb06-106">This tutorial assumes that you have some prior experience using node and [Git].</span></span>

<span data-ttu-id="ffb06-107">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="ffb06-107">You will learn:</span></span>

* <span data-ttu-id="ffb06-108">как использовать для установки модулей Node диспетчер npm (node package manager);</span><span class="sxs-lookup"><span data-stu-id="ffb06-108">How to use npm (node package manager) to install the node modules</span></span>
* <span data-ttu-id="ffb06-109">как работать со службой таблиц Azure;</span><span class="sxs-lookup"><span data-stu-id="ffb06-109">How to work with the Azure Table service</span></span>
* <span data-ttu-id="ffb06-110">как использовать Azure CLI для создания веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ffb06-110">How to use the Azure CLI to create a web app.</span></span>

<span data-ttu-id="ffb06-111">Руководствуясь этим учебником, вы создадите простое веб-приложение для управления списком дел, позволяющее создавать, извлекать и выполнять задачи.</span><span class="sxs-lookup"><span data-stu-id="ffb06-111">By following this tutorial, you will build a simple web-based "to-do list" application that allows creating, retrieving and completing tasks.</span></span> <span data-ttu-id="ffb06-112">Задачи хранятся в службе таблиц.</span><span class="sxs-lookup"><span data-stu-id="ffb06-112">The tasks are stored in the Table service.</span></span>

<span data-ttu-id="ffb06-113">Вот готовое приложение:</span><span class="sxs-lookup"><span data-stu-id="ffb06-113">Here is the completed application:</span></span>

![Веб-страница, показывающая пустой список задач][node-table-finished]

> [!NOTE]
> <span data-ttu-id="ffb06-115">Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="ffb06-115">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ffb06-116">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="ffb06-116">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ffb06-117">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ffb06-117">Prerequisites</span></span>
<span data-ttu-id="ffb06-118">Перед выполнением инструкций, приведенных в этой статье, следует убедиться, что установлены следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="ffb06-118">Before following the instructions in this article, ensure that you have the following installed:</span></span>

* <span data-ttu-id="ffb06-119">[node] версии 0.10.24 или выше</span><span class="sxs-lookup"><span data-stu-id="ffb06-119">[node] version 0.10.24 or higher</span></span>
* <span data-ttu-id="ffb06-120">[Git]</span><span class="sxs-lookup"><span data-stu-id="ffb06-120">[Git]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a><span data-ttu-id="ffb06-121">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="ffb06-121">Create a storage account</span></span>
<span data-ttu-id="ffb06-122">Создайте учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb06-122">Create an Azure storage account.</span></span> <span data-ttu-id="ffb06-123">Это приложение использует ее для хранения списка дел.</span><span class="sxs-lookup"><span data-stu-id="ffb06-123">The app will use this account to store the to-do items.</span></span>

1. <span data-ttu-id="ffb06-124">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ffb06-124">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ffb06-125">Щелкните значок **Создать** в левом нижнем углу портала, затем выберите **Данные + хранилище** > **Хранилище**.</span><span class="sxs-lookup"><span data-stu-id="ffb06-125">Click the **New** icon on the bottom left of the portal, then click **Data + Storage** > **Storage**.</span></span> <span data-ttu-id="ffb06-126">Присвойте учетной записи хранения уникальное имя и создайте для нее новую [группу ресурсов](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ffb06-126">Give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Кнопка «Создать»](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    <span data-ttu-id="ffb06-128">После создания новой учетной записи на кнопке **Уведомления** начнет мигать зеленым слово **Успешно** и откроется колонка учетной записи хранения, в которой будет видно, что учетная запись принадлежит к созданной вами группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ffb06-128">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span></span>
3. <span data-ttu-id="ffb06-129">В колонке учетной записи хранения выберите **Параметры** > **Ключи**.</span><span class="sxs-lookup"><span data-stu-id="ffb06-129">In the storage account's blade, click **Settings** > **Keys**.</span></span> <span data-ttu-id="ffb06-130">Скопируйте первичный ключ доступа в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="ffb06-130">Copy the primary access key to the clipboard.</span></span>
   
    ![Ключ доступа][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a><span data-ttu-id="ffb06-132">Установка модулей и создание шаблонов</span><span class="sxs-lookup"><span data-stu-id="ffb06-132">Install modules and generate scaffolding</span></span>
<span data-ttu-id="ffb06-133">В этом разделе вы создадите новое приложение Node и добавите пакеты модулей с помощью npm.</span><span class="sxs-lookup"><span data-stu-id="ffb06-133">In this section you will create a new Node application and use npm to add module packages.</span></span> <span data-ttu-id="ffb06-134">Для этого приложения вы используете модули [Express] и [Azure].</span><span class="sxs-lookup"><span data-stu-id="ffb06-134">For this application you will use the [Express] and [Azure] modules.</span></span> <span data-ttu-id="ffb06-135">Модуль Express предоставляет платформу Model View Controller (Контроллер представления модели) для Node, а модули Azure предоставляют возможность подключения к службе таблиц.</span><span class="sxs-lookup"><span data-stu-id="ffb06-135">The Express module provides a Model View Controller framework for node, while the Azure modules provides connectivity to the Table service.</span></span>

### <a name="install-express-and-generate-scaffolding"></a><span data-ttu-id="ffb06-136">Установка модуля Express и формирование шаблонов</span><span class="sxs-lookup"><span data-stu-id="ffb06-136">Install express and generate scaffolding</span></span>
1. <span data-ttu-id="ffb06-137">Из командной строки создайте новый каталог **tasklist** и перейдите в него.</span><span class="sxs-lookup"><span data-stu-id="ffb06-137">From the command line, create a new directory named **tasklist** and switch to that directory.</span></span>  
2. <span data-ttu-id="ffb06-138">Введите следующую команду для установки модуля Express.</span><span class="sxs-lookup"><span data-stu-id="ffb06-138">Enter the following command to install the Express module.</span></span>
   
        npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="ffb06-139">В зависимости от операционной системы вам может потребоваться указать «sudo» перед командой:</span><span class="sxs-lookup"><span data-stu-id="ffb06-139">Depending on the operating system, you may need to put 'sudo' before the command:</span></span>
   
        sudo npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="ffb06-140">Выходные данные выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ffb06-140">The output appears similar to the following example:</span></span>
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > <span data-ttu-id="ffb06-141">Параметр -g указывает на то, что модуль устанавливается глобально.</span><span class="sxs-lookup"><span data-stu-id="ffb06-141">The '-g' parameter installs the module globally.</span></span> <span data-ttu-id="ffb06-142">В результате мы сможем использовать **express** для создания шаблонов веб-приложения без необходимости вводить дополнительные сведения о пути.</span><span class="sxs-lookup"><span data-stu-id="ffb06-142">That way, we can use **express** to generate web app scaffolding without having to type in additional path information.</span></span>
   > 
   > 
3. <span data-ttu-id="ffb06-143">Чтобы создать шаблоны для этого приложения, введите команду **express** :</span><span class="sxs-lookup"><span data-stu-id="ffb06-143">To create the scaffolding for the application, enter the **express** command:</span></span>
   
        express
   
    <span data-ttu-id="ffb06-144">Выходные данные этой команды выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ffb06-144">The output of this command appears similar to the following example:</span></span>
   
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
   
           run the app:
             $ DEBUG=my-application ./bin/www
   
    <span data-ttu-id="ffb06-145">В каталоге **tasklist** появится несколько новых папок и файлов.</span><span class="sxs-lookup"><span data-stu-id="ffb06-145">You now have several new directories and files in the **tasklist** directory.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="ffb06-146">Установка дополнительных модулей</span><span class="sxs-lookup"><span data-stu-id="ffb06-146">Install additional modules</span></span>
<span data-ttu-id="ffb06-147">Модуль **express**, в частности, создает файл **package.json**.</span><span class="sxs-lookup"><span data-stu-id="ffb06-147">One of the files that **express** creates is **package.json**.</span></span> <span data-ttu-id="ffb06-148">Этот файл содержит список зависимостей модуля.</span><span class="sxs-lookup"><span data-stu-id="ffb06-148">This file contains a list of module dependencies.</span></span> <span data-ttu-id="ffb06-149">Позднее, при развертывании приложения в веб-приложениях службы приложений, этот файл будет определять, какие модули должны быть установлены в Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb06-149">Later, when you deploy the application to App Service Web Apps, this file determines which modules need to be installed on Azure.</span></span>

<span data-ttu-id="ffb06-150">В командной строке введите следующую команду, чтобы установить модули, описанные в файле **package.json**.</span><span class="sxs-lookup"><span data-stu-id="ffb06-150">From the command-line, enter the following command to install the modules described in the **package.json** file.</span></span> <span data-ttu-id="ffb06-151">Может потребоваться использовать «sudo» в командной строке.</span><span class="sxs-lookup"><span data-stu-id="ffb06-151">You may need to use 'sudo'.</span></span>

    npm install

<span data-ttu-id="ffb06-152">Выходные данные этой команды выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ffb06-152">The output of this command appears similar to the following example:</span></span>

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


<span data-ttu-id="ffb06-153">Теперь введите следующую команду, чтобы установить модули [azure], [node-uuid], [nconf] и [async]:</span><span class="sxs-lookup"><span data-stu-id="ffb06-153">Next, enter the following command to install the [azure], [node-uuid], [nconf] and [async] modules:</span></span>

    npm install azure-storage node-uuid async nconf --save

<span data-ttu-id="ffb06-154">Флаг **--save** добавляет записи для этих модулей в файл **package.json**.</span><span class="sxs-lookup"><span data-stu-id="ffb06-154">The **--save** flag adds entries for these modules to the **package.json** file.</span></span>

<span data-ttu-id="ffb06-155">Выходные данные этой команды выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ffb06-155">The output of this command appears similar to the following example:</span></span>

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-the-application"></a><span data-ttu-id="ffb06-156">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="ffb06-156">Create the application</span></span>
<span data-ttu-id="ffb06-157">Теперь все готово к созданию приложения.</span><span class="sxs-lookup"><span data-stu-id="ffb06-157">Now we're ready to build the application.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="ffb06-158">Создание модели</span><span class="sxs-lookup"><span data-stu-id="ffb06-158">Create a model</span></span>
<span data-ttu-id="ffb06-159">*Модель* — это объект, который представляет данные в приложении.</span><span class="sxs-lookup"><span data-stu-id="ffb06-159">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="ffb06-160">В нашем приложении единственной моделью является объект задачи, который представляет собой элемент списка дел.</span><span class="sxs-lookup"><span data-stu-id="ffb06-160">For the application, the only model is a task object, which represents an item in the to-do list.</span></span> <span data-ttu-id="ffb06-161">У каждой задачи есть следующие поля:</span><span class="sxs-lookup"><span data-stu-id="ffb06-161">Tasks will have the following fields:</span></span>

* <span data-ttu-id="ffb06-162">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="ffb06-162">PartitionKey</span></span>
* <span data-ttu-id="ffb06-163">RowKey</span><span class="sxs-lookup"><span data-stu-id="ffb06-163">RowKey</span></span>
* <span data-ttu-id="ffb06-164">name (строка)</span><span class="sxs-lookup"><span data-stu-id="ffb06-164">name (string)</span></span>
* <span data-ttu-id="ffb06-165">category (строка)</span><span class="sxs-lookup"><span data-stu-id="ffb06-165">category (string)</span></span>
* <span data-ttu-id="ffb06-166">completed (логическое значение)</span><span class="sxs-lookup"><span data-stu-id="ffb06-166">completed (Boolean)</span></span>

<span data-ttu-id="ffb06-167">Поля **PartitionKey** и **RowKey** используются службой таблиц в качестве ключей таблиц.</span><span class="sxs-lookup"><span data-stu-id="ffb06-167">**PartitionKey** and **RowKey** are used by the Table Service as table keys.</span></span> <span data-ttu-id="ffb06-168">Дополнительные сведения см. в статье [Understanding the Table Service Data Model](https://msdn.microsoft.com/library/azure/dd179338.aspx) (Общие сведения о модели данных службы таблиц).</span><span class="sxs-lookup"><span data-stu-id="ffb06-168">For more information, see [Understanding the Table Service data model](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

1. <span data-ttu-id="ffb06-169">В каталоге **tasklist** создайте каталог с именем **models**.</span><span class="sxs-lookup"><span data-stu-id="ffb06-169">In the **tasklist** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="ffb06-170">В каталоге **models** создайте файл с именем **task.js**.</span><span class="sxs-lookup"><span data-stu-id="ffb06-170">In the **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="ffb06-171">Этот файл будет содержать модель для задач, создаваемых приложением.</span><span class="sxs-lookup"><span data-stu-id="ffb06-171">This file will contain the model for the tasks created by your application.</span></span>
3. <span data-ttu-id="ffb06-172">В начале файла **task.js** добавьте следующий код для ссылки на необходимые библиотеки:</span><span class="sxs-lookup"><span data-stu-id="ffb06-172">At the beginning of the **task.js** file, add the following code to reference required libraries:</span></span>
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. <span data-ttu-id="ffb06-173">Добавьте приведенный ниже код, чтобы определить и экспортировать объект Task.</span><span class="sxs-lookup"><span data-stu-id="ffb06-173">Add the following code to define and export the Task object.</span></span> <span data-ttu-id="ffb06-174">Этот объект отвечает за подключение к таблице.</span><span class="sxs-lookup"><span data-stu-id="ffb06-174">This object is responsible for connecting to the table.</span></span>
   
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
5. <span data-ttu-id="ffb06-175">Добавьте следующий код, определяющий для объекта Task дополнительные методы, которые позволяют взаимодействовать с данными, хранящимися в таблице:</span><span class="sxs-lookup"><span data-stu-id="ffb06-175">Add the following code to define additional methods on the Task object, which allow interactions with data stored in the table:</span></span>
   
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
6. <span data-ttu-id="ffb06-176">Сохраните и закройте файл **task.js** .</span><span class="sxs-lookup"><span data-stu-id="ffb06-176">Save and close the **task.js** file.</span></span>

### <a name="create-a-controller"></a><span data-ttu-id="ffb06-177">Создание контроллера</span><span class="sxs-lookup"><span data-stu-id="ffb06-177">Create a controller</span></span>
<span data-ttu-id="ffb06-178">*Контроллер* обрабатывает HTTP-запросы и отображает HTML-ответ.</span><span class="sxs-lookup"><span data-stu-id="ffb06-178">A *controller* handles HTTP requests and renders the HTML response.</span></span>

1. <span data-ttu-id="ffb06-179">В каталоге **tasklist/routes** создайте файл с именем **tasklist.js** и откройте его в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="ffb06-179">In the **tasklist/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="ffb06-180">Добавьте в **tasklist.js**следующий код.</span><span class="sxs-lookup"><span data-stu-id="ffb06-180">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="ffb06-181">Он загружает модули azure и async, используемые **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="ffb06-181">This loads the azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="ffb06-182">Он также определяет функцию **TaskList**, передающую экземпляр объекта **Task**, определенного ранее:</span><span class="sxs-lookup"><span data-stu-id="ffb06-182">This also defines the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. <span data-ttu-id="ffb06-183">Определите объект **TaskList** .</span><span class="sxs-lookup"><span data-stu-id="ffb06-183">Define a **TaskList** object.</span></span>
   
        function TaskList(task) {
          this.task = task;
        }
4. <span data-ttu-id="ffb06-184">Добавьте в объект **TaskList**следующие методы:</span><span class="sxs-lookup"><span data-stu-id="ffb06-184">Add the following methods to **TaskList**:</span></span>
   
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

### <a name="modify-appjs"></a><span data-ttu-id="ffb06-185">Изменение app.js</span><span class="sxs-lookup"><span data-stu-id="ffb06-185">Modify app.js</span></span>
1. <span data-ttu-id="ffb06-186">В каталоге **tasklist** откройте файл **app.js**.</span><span class="sxs-lookup"><span data-stu-id="ffb06-186">From the **tasklist** directory, open the **app.js** file.</span></span> <span data-ttu-id="ffb06-187">Этот файл был создан ранее с помощью команды **express** .</span><span class="sxs-lookup"><span data-stu-id="ffb06-187">This file was created earlier by running the **express** command.</span></span>
2. <span data-ttu-id="ffb06-188">В начале файла добавьте следующий код для загрузки модуля azure, задайте имя таблицы, ключ раздела, а также учетные данные хранения, используемые в этом примере:</span><span class="sxs-lookup"><span data-stu-id="ffb06-188">At the beginning of the file, add the following to load the azure module, set the table name, partition key, and set the storage credentials used by this example:</span></span>
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > <span data-ttu-id="ffb06-189">nconf загружает значения конфигурации либо из переменных среды, либо из файла **config.json** , который мы создадим позднее.</span><span class="sxs-lookup"><span data-stu-id="ffb06-189">nconf will load the configuration values from either environment variables or the **config.json** file, which we will create later.</span></span>
   > 
   > 
3. <span data-ttu-id="ffb06-190">Прокрутите файл app.js вниз до появления следующей строки:</span><span class="sxs-lookup"><span data-stu-id="ffb06-190">In the app.js file, scroll down to where you see the following line:</span></span>
   
        app.use('/', routes);
        app.use('/users', users);
   
    <span data-ttu-id="ffb06-191">Замените вышеприведенные строки на код, приведенный ниже.</span><span class="sxs-lookup"><span data-stu-id="ffb06-191">Replace the above lines with the code shown below.</span></span> <span data-ttu-id="ffb06-192">Код инициализирует экземпляр <strong>Task</strong> , используя подключение к вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="ffb06-192">This will initialize an instance of <strong>Task</strong> with a connection to your storage account.</span></span> <span data-ttu-id="ffb06-193">Он передается в <strong>TaskList</strong>, где будет использоваться для обмена данными со службой таблиц:</span><span class="sxs-lookup"><span data-stu-id="ffb06-193">This is passed to the <strong>TaskList</strong>, which will use it to communicate with the Table service:</span></span>
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. <span data-ttu-id="ffb06-194">Сохраните файл **app.js** .</span><span class="sxs-lookup"><span data-stu-id="ffb06-194">Save the **app.js** file.</span></span>

### <a name="modify-the-index-view"></a><span data-ttu-id="ffb06-195">Изменение представления индекса</span><span class="sxs-lookup"><span data-stu-id="ffb06-195">Modify the index view</span></span>
1. <span data-ttu-id="ffb06-196">Откройте файл **tasklist/views/index.jade** в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="ffb06-196">Open the **tasklist/views/index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="ffb06-197">Замените все содержимое файла следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="ffb06-197">Replace the entire contents of the file with the following code.</span></span> <span data-ttu-id="ffb06-198">Он определяет представление, в котором отображаются существующие задачи и содержится форма для добавления новых задач и пометки существующих как завершенных.</span><span class="sxs-lookup"><span data-stu-id="ffb06-198">This defines a view that displays existing tasks and includes a form for adding new tasks and marking existing ones as completed.</span></span>
   
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
3. <span data-ttu-id="ffb06-199">Сохраните и закройте файл **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="ffb06-199">Save and close **index.jade** file.</span></span>

### <a name="modify-the-global-layout"></a><span data-ttu-id="ffb06-200">Изменение глобального макета</span><span class="sxs-lookup"><span data-stu-id="ffb06-200">Modify the global layout</span></span>
<span data-ttu-id="ffb06-201">Файл **layout.jade** в каталоге **views** используется как глобальный шаблон для других **JADE**-файлов.</span><span class="sxs-lookup"><span data-stu-id="ffb06-201">The **layout.jade** file in the **views** directory is a global template for other **.jade** files.</span></span> <span data-ttu-id="ffb06-202">На этом шаге он будет изменен таким образом, чтобы использовать [Twitter Bootstrap](https://github.com/twbs/bootstrap)— набор средств, с помощью которых можно легко создать привлекательный веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="ffb06-202">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking web app.</span></span>

<span data-ttu-id="ffb06-203">Загрузите и извлеките файлы [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="ffb06-203">Download and extract the files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="ffb06-204">Скопируйте файл **bootstrap.min.css** из папки Bootstrap **css** в каталог **public/stylesheets** своего приложения.</span><span class="sxs-lookup"><span data-stu-id="ffb06-204">Copy the **bootstrap.min.css** file from the Bootstrap **css** folder into the **public/stylesheets** directory of your application.</span></span>

<span data-ttu-id="ffb06-205">В папке **views** откройте файл **layout.jade** и замените его содержимое следующим:</span><span class="sxs-lookup"><span data-stu-id="ffb06-205">From the **views** folder, open **layout.jade** and replace the entire contents with the following:</span></span>

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

### <a name="create-a-config-file"></a><span data-ttu-id="ffb06-206">Создание файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="ffb06-206">Create a config file</span></span>
<span data-ttu-id="ffb06-207">Для локального запуска приложения мы поместим учетные данные службы хранилища Azure в файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ffb06-207">To run the app locally, we'll put Azure Storage credentials into a config file.</span></span> <span data-ttu-id="ffb06-208">Создайте файл **config.json** со следующим кодом JSON:</span><span class="sxs-lookup"><span data-stu-id="ffb06-208">Create a file named **config.json* *with the following JSON:</span></span>

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="ffb06-209">Замените **storage account name** именем учетной записи хранения, созданной ранее, а **storage access key** — первичным ключом доступа к своей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="ffb06-209">Replace **storage account name** with the name of the storage account you created earlier, and replace **storage access key** with the primary access key for your storage account.</span></span> <span data-ttu-id="ffb06-210">Например:</span><span class="sxs-lookup"><span data-stu-id="ffb06-210">For example:</span></span>

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="ffb06-211">Сохраните этот файл *на один уровень выше* каталога **tasklist** , как показано в ниже:</span><span class="sxs-lookup"><span data-stu-id="ffb06-211">Save this file *one directory level higher* than the **tasklist** directory, like this:</span></span>

    parent/
      |-- config.json
      |-- tasklist/

<span data-ttu-id="ffb06-212">Это позволит избежать включения файла конфигурации в исходный элемент управления, в результате чего он может оказаться общедоступным.</span><span class="sxs-lookup"><span data-stu-id="ffb06-212">The reason for doing this is to avoid checking the config file into source control, where it might become public.</span></span> <span data-ttu-id="ffb06-213">При развертывании приложения в среде Azure вместо файла конфигурации мы будем использовать переменные среды.</span><span class="sxs-lookup"><span data-stu-id="ffb06-213">When we deploy the app to Azure, we will use environment variables instead of a config file.</span></span>

## <a name="run-the-application-locally"></a><span data-ttu-id="ffb06-214">Локальный запуск приложения</span><span class="sxs-lookup"><span data-stu-id="ffb06-214">Run the application locally</span></span>
<span data-ttu-id="ffb06-215">Для проверки приложения на локальном компьютере выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ffb06-215">To test the application on your local machine, perform the following steps:</span></span>

1. <span data-ttu-id="ffb06-216">В командной строке измените каталоги на каталог **tasklist** .</span><span class="sxs-lookup"><span data-stu-id="ffb06-216">From the command-line, change directories to the **tasklist** directory.</span></span>
2. <span data-ttu-id="ffb06-217">Используйте следующую команду для локального запуска приложения:</span><span class="sxs-lookup"><span data-stu-id="ffb06-217">Use the following command to launch the application locally:</span></span>
   
        npm start
3. <span data-ttu-id="ffb06-218">Откройте браузер и перейдите по адресу http://127.0.0.1:3000.</span><span class="sxs-lookup"><span data-stu-id="ffb06-218">Open a web browser and navigate to http://127.0.0.1:3000.</span></span>
   
    <span data-ttu-id="ffb06-219">Появится веб-страница, как в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="ffb06-219">A web page similar to the following example appears.</span></span>
   
    ![Веб-страница, показывающая пустой список задач][node-table-finished]
4. <span data-ttu-id="ffb06-221">Чтобы создать новый элемент списка, введите имя и категорию и щелкните **Add Item**(Добавить элемент).</span><span class="sxs-lookup"><span data-stu-id="ffb06-221">To create a new to-do item, enter a name and category and click **Add Item**.</span></span> 
5. <span data-ttu-id="ffb06-222">Чтобы пометить задачу как выполненную, установите флажок **Выполнено** и щелкните **Обновить задачи**.</span><span class="sxs-lookup"><span data-stu-id="ffb06-222">To mark a task as complete, check **Complete** and click **Update Tasks**.</span></span>
   
    ![Изображение нового элемента в списке задач][node-table-list-items]

<span data-ttu-id="ffb06-224">Хотя приложение выполняется локально, его данные хранятся в службе таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb06-224">Even though the application is running locally, it is storing the data in the Azure Table service.</span></span>

## <a name="deploy-your-application-to-azure"></a><span data-ttu-id="ffb06-225">Развертывание приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="ffb06-225">Deploy your application to Azure</span></span>
<span data-ttu-id="ffb06-226">В действиях, описанных в этом разделе, для создания веб-приложения в службе приложений используются средства командной строки Azure, а затем для развертывания приложения применяется Git.</span><span class="sxs-lookup"><span data-stu-id="ffb06-226">The steps in this section use the Azure command-line tools to create a new web app in App Service, and then use Git to deploy your application.</span></span> <span data-ttu-id="ffb06-227">Для выполнения этих действий необходима подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb06-227">To perform these steps you must have an Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="ffb06-228">Эти действия также можно выполнить с помощью [портала Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ffb06-228">These steps can also be performed by using the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="ffb06-229">См. статью [Начало работы с веб-приложениями Node.js в службе приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="ffb06-229">See [Build and deploy a Node.js web app in Azure App Service].</span></span>
> 
> <span data-ttu-id="ffb06-230">Если это первое созданное вами веб-приложение, для его развертывания необходимо использовать портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb06-230">If this is the first web app you have created, you must use the Azure Portal to deploy this application.</span></span>
> 
> 

<span data-ttu-id="ffb06-231">Сначала установите [интерфейс командной строки Azure] , выполнив в командной строке следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ffb06-231">To get started, install the [Azure CLI] by entering the following command from the command line:</span></span>

    npm install azure-cli -g

### <a name="import-publishing-settings"></a><span data-ttu-id="ffb06-232">Импорт параметров публикации</span><span class="sxs-lookup"><span data-stu-id="ffb06-232">Import publishing settings</span></span>
<span data-ttu-id="ffb06-233">На этом шаге вы загрузите файл, содержащий сведения о вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="ffb06-233">In this step, you will download a file containing information about your subscription.</span></span>

1. <span data-ttu-id="ffb06-234">Введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ffb06-234">Enter the following command:</span></span>
   
        azure login
   
    <span data-ttu-id="ffb06-235">Эта команда запускает браузер и открывает страницу загрузки.</span><span class="sxs-lookup"><span data-stu-id="ffb06-235">This command launches a browser and navigates to the download page.</span></span> <span data-ttu-id="ffb06-236">Если появится соответствующий запрос, войдите с помощью учетной записи, которая связана с вашей подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb06-236">If prompted, log in with the account associated with your Azure subscription.</span></span>
   
    <!-- ![The download page][download-publishing-settings] -->
   
    <span data-ttu-id="ffb06-237">Скачивание файла должно начаться автоматически. Если этого не произошло, можно щелкнуть ссылку в начале страницы, чтобы скачать файл вручную.</span><span class="sxs-lookup"><span data-stu-id="ffb06-237">The file download begins automatically; if it does not, you can click the link at the beginning of the page to manually download the file.</span></span> <span data-ttu-id="ffb06-238">Сохраните файл и запомните путь к нему.</span><span class="sxs-lookup"><span data-stu-id="ffb06-238">Save the file and note the file path.</span></span>
2. <span data-ttu-id="ffb06-239">Введите следующую команду, чтобы импортировать параметры.</span><span class="sxs-lookup"><span data-stu-id="ffb06-239">Enter the following command to import the settings:</span></span>
   
        azure account import <path-to-file>
   
    <span data-ttu-id="ffb06-240">Укажите путь и имя файла параметров публикации, загруженного на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="ffb06-240">Specify the path and file name of the publishing settings file you downloaded in the previous step.</span></span>
3. <span data-ttu-id="ffb06-241">После импорта параметров удалите файл параметров публикации.</span><span class="sxs-lookup"><span data-stu-id="ffb06-241">After the settings are imported, delete the publish settings file.</span></span> <span data-ttu-id="ffb06-242">Он больше не нужен, и при этом он содержит важные сведения о вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb06-242">It is no longer needed, and contains sensitive information regarding your Azure subscription.</span></span>

### <a name="create-an-app-service-web-app"></a><span data-ttu-id="ffb06-243">Создание веб-приложения службы приложений</span><span class="sxs-lookup"><span data-stu-id="ffb06-243">Create an App Service web app</span></span>
1. <span data-ttu-id="ffb06-244">В командной строке измените каталоги на каталог **tasklist** .</span><span class="sxs-lookup"><span data-stu-id="ffb06-244">From the command-line, change directories to the **tasklist** directory.</span></span>
2. <span data-ttu-id="ffb06-245">Создайте веб-приложение, используя следующую команду.</span><span class="sxs-lookup"><span data-stu-id="ffb06-245">Use the following command to create a new web app.</span></span>
   
        azure site create --git
   
    <span data-ttu-id="ffb06-246">Вам будет предложено указать имя и расположение веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ffb06-246">You will be prompted for the web app name and location.</span></span> <span data-ttu-id="ffb06-247">Введите уникальное имя и выберите то же географическое расположение, что и у вашей учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb06-247">Provide a unique name and select the same geographical location as your Azure Storage account.</span></span>
   
    <span data-ttu-id="ffb06-248">Параметр `--git` создает в Azure репозиторий Git для этого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ffb06-248">The `--git` parameter creates a Git repository on Azure for this web app.</span></span> <span data-ttu-id="ffb06-249">Он также инициализирует репозиторий Git в текущем каталоге, если его там нет, и добавляет [удаленный репозиторий Git] с именем «azure», которое используется для публикации приложения в среде Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb06-249">It also initializes a Git repository in the current directory if none exists, and adds a [Git remote] named 'azure', which is used to publish the application to Azure.</span></span> <span data-ttu-id="ffb06-250">Наконец, он создает файл **web.config** , который содержит параметры, используемые средой Azure для размещения приложений Node.</span><span class="sxs-lookup"><span data-stu-id="ffb06-250">Finally, it creates a **web.config** file, which contains settings used by Azure to host node applications.</span></span> <span data-ttu-id="ffb06-251">Если параметр `--git` не указан, но в каталоге есть репозиторий Git, то данная команда все равно создаст удаленный репозиторий «azure».</span><span class="sxs-lookup"><span data-stu-id="ffb06-251">If you omit the `--git` parameter but the directory contains a Git repository, the command will still create the 'azure' remote.</span></span>
   
    <span data-ttu-id="ffb06-252">После выполнения этой команды должен появиться результат, похожий на следующий.</span><span class="sxs-lookup"><span data-stu-id="ffb06-252">Once this command has completed, you will see output similar to the following.</span></span> <span data-ttu-id="ffb06-253">Обратите внимание на то, что строка, начинающаяся с **Website created at** (Веб-сайт, созданный по адресу), содержит URL-адрес веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ffb06-253">Note that the line beginning with **Website created at** contains the URL for the web app.</span></span>
   
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
   > <span data-ttu-id="ffb06-254">Если это первое веб-приложение службы приложений для вашей подписки, вам будет рекомендовано использовать портал Azure для создания этого приложения.</span><span class="sxs-lookup"><span data-stu-id="ffb06-254">If this is the first App Service web app for your subscription, you will be instructed to use the Azure Portal to create the web app.</span></span> <span data-ttu-id="ffb06-255">Дополнительные сведения см. в разделе [Начало работы с веб-приложениями Node.js в службе приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="ffb06-255">For more information, see [Build and deploy a Node.js web app in Azure App Service].</span></span>
   > 
   > 

### <a name="set-environment-variables"></a><span data-ttu-id="ffb06-256">Настройка переменных среды</span><span class="sxs-lookup"><span data-stu-id="ffb06-256">Set environment variables</span></span>
<span data-ttu-id="ffb06-257">На этом шаге в конфигурацию веб-приложения в Azure добавляются переменные среды.</span><span class="sxs-lookup"><span data-stu-id="ffb06-257">In this step, you will add environment variables to your web app configuration on Azure.</span></span>
<span data-ttu-id="ffb06-258">В командной строке введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="ffb06-258">From the command line, enter the following:</span></span>

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


<span data-ttu-id="ffb06-259">Замените **<storage account name>** именем учетной записи хранения, созданной ранее, а **<storage access key>** — первичным ключом доступа к учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="ffb06-259">Replace **<storage account name>** with the name of the storage account you created earlier, and replace **<storage access key>** with the primary access key for your storage account.</span></span> <span data-ttu-id="ffb06-260">(Используйте те же значения, что и в файле config.json, который создали ранее.)</span><span class="sxs-lookup"><span data-stu-id="ffb06-260">(Use the same values as the config.json file that you created earlier.)</span></span>

<span data-ttu-id="ffb06-261">Переменные среды также можно задать на [портале Azure](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="ffb06-261">Alternatively, you can set environment variables in the [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="ffb06-262">Откройте колонку веб-приложения, выбрав **Обзор** > **Веб-приложения** > имя вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ffb06-262">Open the web app's blade by clicking **Browse** > **Web Apps** > your web app name.</span></span>
2. <span data-ttu-id="ffb06-263">В колонке веб-приложения щелкните **Все параметры** > **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="ffb06-263">In your web app's blade, click **All Settings** > **Application Settings**.</span></span>
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. <span data-ttu-id="ffb06-264">Прокрутите содержимое вниз до раздела **Параметры приложения** и добавьте пары «ключ-значение».</span><span class="sxs-lookup"><span data-stu-id="ffb06-264">Scroll down to the **App settings** section and add the key/value pairs.</span></span>
   
     ![Параметры приложения](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. <span data-ttu-id="ffb06-266">Щелкните **СОХРАНИТЬ**.</span><span class="sxs-lookup"><span data-stu-id="ffb06-266">Click **SAVE**.</span></span>

### <a name="publish-the-application"></a><span data-ttu-id="ffb06-267">Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="ffb06-267">Publish the application</span></span>
<span data-ttu-id="ffb06-268">Чтобы опубликовать приложение, зафиксируйте файлы с кодом в репозитории Git и отправьте их в azure/master.</span><span class="sxs-lookup"><span data-stu-id="ffb06-268">To publish the app, commit the code files to Git and then push to azure/master.</span></span>

1. <span data-ttu-id="ffb06-269">Задайте учетные данные развертывания.</span><span class="sxs-lookup"><span data-stu-id="ffb06-269">Set your deployment credentials.</span></span>
   
        azure site deployment user set <name> <password>
2. <span data-ttu-id="ffb06-270">Добавьте и зафиксируйте файлы своего приложения.</span><span class="sxs-lookup"><span data-stu-id="ffb06-270">Add and commit your application files.</span></span>
   
        git add .
        git commit -m "adding files"
3. <span data-ttu-id="ffb06-271">Отправьте зафиксированные данные в веб-приложение службы приложений:</span><span class="sxs-lookup"><span data-stu-id="ffb06-271">Push the commit to the App Service web app:</span></span>
   
        git push azure master
   
    <span data-ttu-id="ffb06-272">В качестве целевой ветви используйте **master** .</span><span class="sxs-lookup"><span data-stu-id="ffb06-272">Use **master** as the target branch.</span></span> <span data-ttu-id="ffb06-273">В конце развертывания должно появиться заявление, похожее на следующее:</span><span class="sxs-lookup"><span data-stu-id="ffb06-273">At the end of the deployment, you see a statement similar to the following example:</span></span>
   
        To https://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. <span data-ttu-id="ffb06-274">После завершения операции отправки перейдите по полученному ранее URL-адресу веб-приложения с помощью команды `azure create site` , чтобы просмотреть приложение.</span><span class="sxs-lookup"><span data-stu-id="ffb06-274">Once the push operation has completed, browse to the web app URL returned previously by the `azure create site` command to view your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffb06-275">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ffb06-275">Next steps</span></span>
<span data-ttu-id="ffb06-276">Хотя в действиях этой статьи описывается использование службы таблиц для хранения информации, можно также использовать [MongoDB](https://mlab.com/azure/).</span><span class="sxs-lookup"><span data-stu-id="ffb06-276">While the steps in this article describe using the Table Service to store information, you can also use [MongoDB](https://mlab.com/azure/).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ffb06-277">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ffb06-277">Additional resources</span></span>
<span data-ttu-id="ffb06-278">[интерфейс командной строки Azure]</span><span class="sxs-lookup"><span data-stu-id="ffb06-278">[Azure CLI]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="ffb06-279">Изменения</span><span class="sxs-lookup"><span data-stu-id="ffb06-279">What's changed</span></span>
* <span data-ttu-id="ffb06-280">Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="ffb06-280">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- URLs -->

<span data-ttu-id="ffb06-281">[Начало работы с веб-приложениями Node.js в службе приложений Azure]: app-service-web-get-started-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="ffb06-281">[Build and deploy a Node.js web app in Azure App Service]: app-service-web-get-started-nodejs.md</span></span>
[Azure Developer Center]: /develop/nodejs/

<span data-ttu-id="ffb06-282">[node]: http://nodejs.org</span><span class="sxs-lookup"><span data-stu-id="ffb06-282">[node]: http://nodejs.org</span></span>
<span data-ttu-id="ffb06-283">[Git]: http://git-scm.com</span><span class="sxs-lookup"><span data-stu-id="ffb06-283">[Git]: http://git-scm.com</span></span>
<span data-ttu-id="ffb06-284">[Express]: http://expressjs.com</span><span class="sxs-lookup"><span data-stu-id="ffb06-284">[Express]: http://expressjs.com</span></span>
[for free]: http://windowsazure.com
<span data-ttu-id="ffb06-285">[удаленный репозиторий Git]: http://git-scm.com/docs/git-remote</span><span class="sxs-lookup"><span data-stu-id="ffb06-285">[Git remote]: http://git-scm.com/docs/git-remote</span></span>

<span data-ttu-id="ffb06-286">[интерфейс командной строки Azure]:../cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="ffb06-286">[Azure CLI]:../cli-install-nodejs.md</span></span>

<span data-ttu-id="ffb06-287">[azure]: https://github.com/Azure/azure-sdk-for-node</span><span class="sxs-lookup"><span data-stu-id="ffb06-287">[azure]: https://github.com/Azure/azure-sdk-for-node</span></span>
<span data-ttu-id="ffb06-288">[node-uuid]: https://www.npmjs.com/package/node-uuid</span><span class="sxs-lookup"><span data-stu-id="ffb06-288">[node-uuid]: https://www.npmjs.com/package/node-uuid</span></span>
<span data-ttu-id="ffb06-289">[nconf]: https://www.npmjs.com/package/nconf</span><span class="sxs-lookup"><span data-stu-id="ffb06-289">[nconf]: https://www.npmjs.com/package/nconf</span></span>
<span data-ttu-id="ffb06-290">[async]: https://www.npmjs.com/package/async</span><span class="sxs-lookup"><span data-stu-id="ffb06-290">[async]: https://www.npmjs.com/package/async</span></span>

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application to an Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
