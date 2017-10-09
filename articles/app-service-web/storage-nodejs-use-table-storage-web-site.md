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
# <a name="nodejs-web-app-using-hello-azure-table-service"></a><span data-ttu-id="4eb9f-103">Веб-приложение node.js с помощью hello службы таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="4eb9f-103">Node.js web app using hello Azure Table Service</span></span>
## <a name="overview"></a><span data-ttu-id="4eb9f-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="4eb9f-104">Overview</span></span>
<span data-ttu-id="4eb9f-105">В этом учебнике показано, как предоставляемые управление данными Azure toostore и доступ к данным из службы таблиц toouse [узел] приложение, размещенное в [службе приложений Azure](http://go.microsoft.com/fwlink/?LinkId=529714) веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-105">This tutorial shows you how toouse Table service provided by Azure Data Management toostore and access data from a [node] application hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="4eb9f-106">Этот учебный курс разработан для читателей, обладающих определенным опытом использования Node и [Git].</span><span class="sxs-lookup"><span data-stu-id="4eb9f-106">This tutorial assumes that you have some prior experience using node and [Git].</span></span>

<span data-ttu-id="4eb9f-107">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-107">You will learn:</span></span>

* <span data-ttu-id="4eb9f-108">Как tooinstall npm (узел диспетчера пакетов) toouse hello модулей узла</span><span class="sxs-lookup"><span data-stu-id="4eb9f-108">How toouse npm (node package manager) tooinstall hello node modules</span></span>
* <span data-ttu-id="4eb9f-109">Как toowork с hello службы таблицы Azure</span><span class="sxs-lookup"><span data-stu-id="4eb9f-109">How toowork with hello Azure Table service</span></span>
* <span data-ttu-id="4eb9f-110">Как toouse hello Azure CLI toocreate веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-110">How toouse hello Azure CLI toocreate a web app.</span></span>

<span data-ttu-id="4eb9f-111">Руководствуясь этим учебником, вы создадите простое веб-приложение для управления списком дел, позволяющее создавать, извлекать и выполнять задачи.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-111">By following this tutorial, you will build a simple web-based "to-do list" application that allows creating, retrieving and completing tasks.</span></span> <span data-ttu-id="4eb9f-112">задачи Hello хранятся в hello службы таблиц.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-112">hello tasks are stored in hello Table service.</span></span>

<span data-ttu-id="4eb9f-113">Вот приложение hello завершена.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-113">Here is hello completed application:</span></span>

![Веб-страница, показывающая пустой список задач][node-table-finished]

> [!NOTE]
> <span data-ttu-id="4eb9f-115">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-115">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="4eb9f-116">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-116">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="4eb9f-117">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4eb9f-117">Prerequisites</span></span>
<span data-ttu-id="4eb9f-118">Перед выполнением инструкции hello в этой статье, убедитесь, что установлены следующие компоненты hello:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-118">Before following hello instructions in this article, ensure that you have hello following installed:</span></span>

* <span data-ttu-id="4eb9f-119">[узел] версии 0.10.24 или выше</span><span class="sxs-lookup"><span data-stu-id="4eb9f-119">[node] version 0.10.24 or higher</span></span>
* <span data-ttu-id="4eb9f-120">[Git]</span><span class="sxs-lookup"><span data-stu-id="4eb9f-120">[Git]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a><span data-ttu-id="4eb9f-121">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-121">Create a storage account</span></span>
<span data-ttu-id="4eb9f-122">Создайте учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-122">Create an Azure storage account.</span></span> <span data-ttu-id="4eb9f-123">приложение Hello будет использовать этот счет toostore hello заданий для выполнения.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-123">hello app will use this account toostore hello to-do items.</span></span>

1. <span data-ttu-id="4eb9f-124">Войти в hello [портала Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4eb9f-124">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4eb9f-125">Нажмите кнопку hello **New** значок hello нижней левом углу портала hello, нажмите кнопку **данные + хранилище** > **хранения**.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-125">Click hello **New** icon on hello bottom left of hello portal, then click **Data + Storage** > **Storage**.</span></span> <span data-ttu-id="4eb9f-126">Задайте уникальное имя учетной записи хранилища hello и создайте новый [группы ресурсов](../azure-resource-manager/resource-group-overview.md) для него.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-126">Give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Кнопка «Создать»](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    <span data-ttu-id="4eb9f-128">При создании учетной записи хранилища hello hello **уведомления** кнопка будет мигать зеленым **успех** и учетной записи хранилища hello колонке открыт tooshow, что оно принадлежит новый ресурс toohello группы создать.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-128">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="4eb9f-129">В колонке учетной записи хранилища hello щелкните **параметры** > **ключей**.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-129">In hello storage account's blade, click **Settings** > **Keys**.</span></span> <span data-ttu-id="4eb9f-130">Скопировать hello доступа первичного ключа toohello буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-130">Copy hello primary access key toohello clipboard.</span></span>
   
    ![Ключ доступа][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a><span data-ttu-id="4eb9f-132">Установка модулей и создание шаблонов</span><span class="sxs-lookup"><span data-stu-id="4eb9f-132">Install modules and generate scaffolding</span></span>
<span data-ttu-id="4eb9f-133">В этом разделе будет создание нового узла приложения и использовать пакеты модуля tooadd npm.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-133">In this section you will create a new Node application and use npm tooadd module packages.</span></span> <span data-ttu-id="4eb9f-134">Для этого приложения будет использовать hello [Express] и [Azure] модулей.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-134">For this application you will use hello [Express] and [Azure] modules.</span></span> <span data-ttu-id="4eb9f-135">модуль экспресс-выпуск Hello инфраструктура Model View Controller для узла, при hello модули Azure предоставляет таблицу toohello подключения службы.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-135">hello Express module provides a Model View Controller framework for node, while hello Azure modules provides connectivity toohello Table service.</span></span>

### <a name="install-express-and-generate-scaffolding"></a><span data-ttu-id="4eb9f-136">Установка модуля Express и формирование шаблонов</span><span class="sxs-lookup"><span data-stu-id="4eb9f-136">Install express and generate scaffolding</span></span>
1. <span data-ttu-id="4eb9f-137">Из командной строки hello, создайте новый каталог с именем **tasklist** и каталог toothat коммутатора.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-137">From hello command line, create a new directory named **tasklist** and switch toothat directory.</span></span>  
2. <span data-ttu-id="4eb9f-138">Введите следующие команды tooinstall hello Express модуля hello.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-138">Enter hello following command tooinstall hello Express module.</span></span>
   
        npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="4eb9f-139">В зависимости от операционной системы hello может потребоваться tooput «sudo» перед командой hello.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-139">Depending on hello operating system, you may need tooput 'sudo' before hello command:</span></span>
   
        sudo npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="4eb9f-140">Hello выходные данные отображаются как toohello, в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-140">hello output appears similar toohello following example:</span></span>
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > <span data-ttu-id="4eb9f-141">Hello "-g" параметр устанавливает модуль hello глобально.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-141">hello '-g' parameter installs hello module globally.</span></span> <span data-ttu-id="4eb9f-142">Таким образом, мы используем **express** toogenerate формирование приложения без необходимости tootype в Дополнительные сведения о пути.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-142">That way, we can use **express** toogenerate web app scaffolding without having tootype in additional path information.</span></span>
   > 
   > 
3. <span data-ttu-id="4eb9f-143">Формирование шаблонов hello toocreate для приложения hello введите hello **express** команды:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-143">toocreate hello scaffolding for hello application, enter hello **express** command:</span></span>
   
        express
   
    <span data-ttu-id="4eb9f-144">Hello выходные данные этой команды появится примерно toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-144">hello output of this command appears similar toohello following example:</span></span>
   
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
   
    <span data-ttu-id="4eb9f-145">Теперь у вас есть несколько новые каталоги и файлы в hello **tasklist** каталога.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-145">You now have several new directories and files in hello **tasklist** directory.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="4eb9f-146">Установка дополнительных модулей</span><span class="sxs-lookup"><span data-stu-id="4eb9f-146">Install additional modules</span></span>
<span data-ttu-id="4eb9f-147">Один из hello файлов, **express** создает — **package.json**.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-147">One of hello files that **express** creates is **package.json**.</span></span> <span data-ttu-id="4eb9f-148">Этот файл содержит список зависимостей модуля.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-148">This file contains a list of module dependencies.</span></span> <span data-ttu-id="4eb9f-149">Позже при развертывании приложения hello tooApp службы веб-приложений, этот файл определяет, какие модули должны toobe установлен в Azure.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-149">Later, when you deploy hello application tooApp Service Web Apps, this file determines which modules need toobe installed on Azure.</span></span>

<span data-ttu-id="4eb9f-150">Из командной строки hello, введите следующие команды tooinstall hello модулей, описанных в hello hello **package.json** файла.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-150">From hello command-line, enter hello following command tooinstall hello modules described in hello **package.json** file.</span></span> <span data-ttu-id="4eb9f-151">Может потребоваться toouse «sudo».</span><span class="sxs-lookup"><span data-stu-id="4eb9f-151">You may need toouse 'sudo'.</span></span>

    npm install

<span data-ttu-id="4eb9f-152">Hello выходные данные этой команды появится примерно toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-152">hello output of this command appears similar toohello following example:</span></span>

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


<span data-ttu-id="4eb9f-153">Затем введите следующая команда tooinstall hello hello [azure], [узел uuid], [nconf] и [async] модули:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-153">Next, enter hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules:</span></span>

    npm install azure-storage node-uuid async nconf --save

<span data-ttu-id="4eb9f-154">Hello **--Сохранить** флаг добавляет записи для этих модулей toohello **package.json** файла.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-154">hello **--save** flag adds entries for these modules toohello **package.json** file.</span></span>

<span data-ttu-id="4eb9f-155">Hello выходные данные этой команды появится примерно toohello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-155">hello output of this command appears similar toohello following example:</span></span>

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-hello-application"></a><span data-ttu-id="4eb9f-156">Создание приложения hello</span><span class="sxs-lookup"><span data-stu-id="4eb9f-156">Create hello application</span></span>
<span data-ttu-id="4eb9f-157">Теперь мы готовы toobuild приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-157">Now we're ready toobuild hello application.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="4eb9f-158">Создание модели</span><span class="sxs-lookup"><span data-stu-id="4eb9f-158">Create a model</span></span>
<span data-ttu-id="4eb9f-159">Объект *модель* — это объект, представляющий данные hello в приложении.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-159">A *model* is an object that represents hello data in your application.</span></span> <span data-ttu-id="4eb9f-160">Для приложения hello hello только модель — объект задачи, который представляет элемент в список дел hello.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-160">For hello application, hello only model is a task object, which represents an item in hello to-do list.</span></span> <span data-ttu-id="4eb9f-161">Задачи будут иметь hello следующие поля:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-161">Tasks will have hello following fields:</span></span>

* <span data-ttu-id="4eb9f-162">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="4eb9f-162">PartitionKey</span></span>
* <span data-ttu-id="4eb9f-163">RowKey</span><span class="sxs-lookup"><span data-stu-id="4eb9f-163">RowKey</span></span>
* <span data-ttu-id="4eb9f-164">name (строка)</span><span class="sxs-lookup"><span data-stu-id="4eb9f-164">name (string)</span></span>
* <span data-ttu-id="4eb9f-165">category (строка)</span><span class="sxs-lookup"><span data-stu-id="4eb9f-165">category (string)</span></span>
* <span data-ttu-id="4eb9f-166">completed (логическое значение)</span><span class="sxs-lookup"><span data-stu-id="4eb9f-166">completed (Boolean)</span></span>

<span data-ttu-id="4eb9f-167">**PartitionKey** и **RowKey** используются hello службы таблиц как ключи таблицы.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-167">**PartitionKey** and **RowKey** are used by hello Table Service as table keys.</span></span> <span data-ttu-id="4eb9f-168">Дополнительные сведения см. в разделе [модели данных службы таблиц hello основные сведения о](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="4eb9f-168">For more information, see [Understanding hello Table Service data model](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

1. <span data-ttu-id="4eb9f-169">В hello **tasklist** каталога, создайте новый каталог с именем **моделей**.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-169">In hello **tasklist** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="4eb9f-170">В hello **моделей** каталога, создайте новый файл с именем **task.js**.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-170">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="4eb9f-171">Этот файл будет содержать hello модель для hello задачи, созданные вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-171">This file will contain hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="4eb9f-172">В начале hello hello **task.js** файл, добавить следующие tooreference необходимые библиотеки кода hello:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-172">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. <span data-ttu-id="4eb9f-173">Добавьте следующую hello кода toodefine и экспорт hello объекта задачи.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-173">Add hello following code toodefine and export hello Task object.</span></span> <span data-ttu-id="4eb9f-174">Этот объект отвечает за подключение toohello таблицы.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-174">This object is responsible for connecting toohello table.</span></span>
   
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
5. <span data-ttu-id="4eb9f-175">Добавьте hello, следующие дополнительные методы toodefine кода hello объекта задачи, которые позволяют взаимодействия с данными, хранящимися в таблице hello:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-175">Add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>
   
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
6. <span data-ttu-id="4eb9f-176">Сохраните и закройте hello **task.js** файла.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-176">Save and close hello **task.js** file.</span></span>

### <a name="create-a-controller"></a><span data-ttu-id="4eb9f-177">Создание контроллера</span><span class="sxs-lookup"><span data-stu-id="4eb9f-177">Create a controller</span></span>
<span data-ttu-id="4eb9f-178">Объект *контроллера* обрабатывает HTTP-запросы и отображает hello HTML-ответа.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-178">A *controller* handles HTTP requests and renders hello HTML response.</span></span>

1. <span data-ttu-id="4eb9f-179">В hello **tasklist/маршруты** каталога, создайте новый файл с именем **tasklist.js** и откройте его в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-179">In hello **tasklist/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="4eb9f-180">Добавьте следующий код слишком hello**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-180">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="4eb9f-181">Это загружает hello azure и async модули, в которых используются **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-181">This loads hello azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="4eb9f-182">Этот параметр также определяет hello **TaskList** функции, которая передается экземпляр hello **задачи** объекта было определено ранее:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-182">This also defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. <span data-ttu-id="4eb9f-183">Определите объект **TaskList** .</span><span class="sxs-lookup"><span data-stu-id="4eb9f-183">Define a **TaskList** object.</span></span>
   
        function TaskList(task) {
          this.task = task;
        }
4. <span data-ttu-id="4eb9f-184">Добавьте следующие методы слишком hello**TaskList**:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-184">Add hello following methods too**TaskList**:</span></span>
   
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

### <a name="modify-appjs"></a><span data-ttu-id="4eb9f-185">Изменение app.js</span><span class="sxs-lookup"><span data-stu-id="4eb9f-185">Modify app.js</span></span>
1. <span data-ttu-id="4eb9f-186">Из hello **tasklist** каталог, откройте hello **в файле app.js** файл.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-186">From hello **tasklist** directory, open hello **app.js** file.</span></span> <span data-ttu-id="4eb9f-187">Этот файл был создан ранее, запустив hello **express** команды.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-187">This file was created earlier by running hello **express** command.</span></span>
2. <span data-ttu-id="4eb9f-188">В начале файла hello hello, добавьте следующие tooload hello azure модуля, имя таблицы hello набора, ключа секции и набор hello хранилища учетные данные, используемые в этом примере hello:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-188">At hello beginning of hello file, add hello following tooload hello azure module, set hello table name, partition key, and set hello storage credentials used by this example:</span></span>
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > <span data-ttu-id="4eb9f-189">nconf загружает значения конфигурации hello из переменных среды или hello **config.json** файл, который мы создадим позже.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-189">nconf will load hello configuration values from either environment variables or hello **config.json** file, which we will create later.</span></span>
   > 
   > 
3. <span data-ttu-id="4eb9f-190">В файле в файле app.js hello, прокрутите вниз toowhere вы видите hello следующую строку:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-190">In hello app.js file, scroll down toowhere you see hello following line:</span></span>
   
        app.use('/', routes);
        app.use('/users', users);
   
    <span data-ttu-id="4eb9f-191">Замените приведенный ниже код hello hello выше строк.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-191">Replace hello above lines with hello code shown below.</span></span> <span data-ttu-id="4eb9f-192">Это будет инициализировать экземпляр <strong>задачи</strong> с учетной записью хранилища tooyour соединения.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-192">This will initialize an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="4eb9f-193">Аргумент передается toohello <strong>TaskList</strong>, который будет использовать toocommunicate с hello службы таблиц:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-193">This is passed toohello <strong>TaskList</strong>, which will use it toocommunicate with hello Table service:</span></span>
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. <span data-ttu-id="4eb9f-194">Сохранить hello **в файле app.js** файл.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-194">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="4eb9f-195">Изменить представление index hello</span><span class="sxs-lookup"><span data-stu-id="4eb9f-195">Modify hello index view</span></span>
1. <span data-ttu-id="4eb9f-196">Откройте hello **tasklist/views/index.jade** файл в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-196">Open hello **tasklist/views/index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="4eb9f-197">Замените все содержимое файла hello hello hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-197">Replace hello entire contents of hello file with hello following code.</span></span> <span data-ttu-id="4eb9f-198">Он определяет представление, в котором отображаются существующие задачи и содержится форма для добавления новых задач и пометки существующих как завершенных.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-198">This defines a view that displays existing tasks and includes a form for adding new tasks and marking existing ones as completed.</span></span>
   
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
3. <span data-ttu-id="4eb9f-199">Сохраните и закройте файл **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="4eb9f-199">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="4eb9f-200">Изменить макет глобального hello</span><span class="sxs-lookup"><span data-stu-id="4eb9f-200">Modify hello global layout</span></span>
<span data-ttu-id="4eb9f-201">Hello **layout.jade** файла в hello **представления** каталог — это глобальный шаблон для других **.jade** файлов.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-201">hello **layout.jade** file in hello **views** directory is a global template for other **.jade** files.</span></span> <span data-ttu-id="4eb9f-202">На этом этапе вы измените его toouse [Twitter начальной загрузки](https://github.com/twbs/bootstrap), который — это набор средств, который позволяет легко toodesign работы с низким приоритетом привлекательных веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-202">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking web app.</span></span>

<span data-ttu-id="4eb9f-203">Загрузите и извлеките файлы hello для [Twitter начальной загрузки](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="4eb9f-203">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="4eb9f-204">Копировать hello **bootstrap.min.css** файл из hello начальной загрузки **css** папки в hello **public или таблицы стилей** каталога приложения.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-204">Copy hello **bootstrap.min.css** file from hello Bootstrap **css** folder into hello **public/stylesheets** directory of your application.</span></span>

<span data-ttu-id="4eb9f-205">Из hello **представления** откройте **layout.jade** и замените все содержимое hello hello следующее:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-205">From hello **views** folder, open **layout.jade** and replace hello entire contents with hello following:</span></span>

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

### <a name="create-a-config-file"></a><span data-ttu-id="4eb9f-206">Создание файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="4eb9f-206">Create a config file</span></span>
<span data-ttu-id="4eb9f-207">toorun приложение hello локально, мы будем Поместите учетные данные хранилища Azure в файл конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-207">toorun hello app locally, we'll put Azure Storage credentials into a config file.</span></span> <span data-ttu-id="4eb9f-208">Создайте файл с именем **config.json* * с hello, следуя JSON:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-208">Create a file named **config.json* *with hello following JSON:</span></span>

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="4eb9f-209">Замените **имя учетной записи хранения** с именем hello хранилища hello учетную запись, созданную ранее и замените **ключ доступа к хранилищу** с hello первичный ключ доступа для учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-209">Replace **storage account name** with hello name of hello storage account you created earlier, and replace **storage access key** with hello primary access key for your storage account.</span></span> <span data-ttu-id="4eb9f-210">Например:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-210">For example:</span></span>

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="4eb9f-211">Сохраните этот файл *один уровень каталога выше* чем hello **tasklist** каталог следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-211">Save this file *one directory level higher* than hello **tasklist** directory, like this:</span></span>

    parent/
      |-- config.json
      |-- tasklist/

<span data-ttu-id="4eb9f-212">Hello причиной этого является tooavoid проверка файла конфигурации hello в систему управления версиями, где могут стать открытый.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-212">hello reason for doing this is tooavoid checking hello config file into source control, where it might become public.</span></span> <span data-ttu-id="4eb9f-213">При развертывании приложения tooAzure hello, мы будем использовать переменные среды вместо файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-213">When we deploy hello app tooAzure, we will use environment variables instead of a config file.</span></span>

## <a name="run-hello-application-locally"></a><span data-ttu-id="4eb9f-214">Запустите приложение hello локально</span><span class="sxs-lookup"><span data-stu-id="4eb9f-214">Run hello application locally</span></span>
<span data-ttu-id="4eb9f-215">приложения hello tootest на локальном компьютере, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-215">tootest hello application on your local machine, perform hello following steps:</span></span>

1. <span data-ttu-id="4eb9f-216">Из командной строки hello, измените каталоги toohello **tasklist** каталога.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-216">From hello command-line, change directories toohello **tasklist** directory.</span></span>
2. <span data-ttu-id="4eb9f-217">Используйте следующие приложения hello toolaunch команда локально hello.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-217">Use hello following command toolaunch hello application locally:</span></span>
   
        npm start
3. <span data-ttu-id="4eb9f-218">Откройте веб-браузер и перейдите toohttp://127.0.0.1:3000.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-218">Open a web browser and navigate toohttp://127.0.0.1:3000.</span></span>
   
    <span data-ttu-id="4eb9f-219">Появится примерно toohello веб-страницы, следующий пример.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-219">A web page similar toohello following example appears.</span></span>
   
    ![Веб-страница, показывающая пустой список задач][node-table-finished]
4. <span data-ttu-id="4eb9f-221">toocreate новый элемент задачи, введите имя и категории и нажмите кнопку **добавить элемент**.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-221">toocreate a new to-do item, enter a name and category and click **Add Item**.</span></span> 
5. <span data-ttu-id="4eb9f-222">toomark задач как полный, проверьте **завершить** и нажмите кнопку **задачи обновления**.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-222">toomark a task as complete, check **Complete** and click **Update Tasks**.</span></span>
   
    ![Изображение hello новый элемент в списке hello задач][node-table-list-items]

<span data-ttu-id="4eb9f-224">Даже если приложение hello выполняется локально, он хранит данные hello в hello службы таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-224">Even though hello application is running locally, it is storing hello data in hello Azure Table service.</span></span>

## <a name="deploy-your-application-tooazure"></a><span data-ttu-id="4eb9f-225">Развертывание tooAzure вашего приложения</span><span class="sxs-lookup"><span data-stu-id="4eb9f-225">Deploy your application tooAzure</span></span>
<span data-ttu-id="4eb9f-226">Hello шаги в этом разделе Использование средств командной строки Azure hello toocreate новое веб-приложение в службе приложений, а затем использовать Git toodeploy приложения.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-226">hello steps in this section use hello Azure command-line tools toocreate a new web app in App Service, and then use Git toodeploy your application.</span></span> <span data-ttu-id="4eb9f-227">tooperform эти действия, необходимо иметь подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-227">tooperform these steps you must have an Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="4eb9f-228">Эти действия можно также выполнить с помощью hello [портала Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4eb9f-228">These steps can also be performed by using hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="4eb9f-229">См. статью [Начало работы с веб-приложениями Node.js в службе приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="4eb9f-229">See [Build and deploy a Node.js web app in Azure App Service].</span></span>
> 
> <span data-ttu-id="4eb9f-230">Если это первый веб-приложения hello, созданных toodeploy hello портала Azure необходимо использовать это приложение.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-230">If this is hello first web app you have created, you must use hello Azure Portal toodeploy this application.</span></span>
> 
> 

<span data-ttu-id="4eb9f-231">tooget к работе, установите hello [Azure CLI] , введя следующую команду из командной строки hello hello:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-231">tooget started, install hello [Azure CLI] by entering hello following command from hello command line:</span></span>

    npm install azure-cli -g

### <a name="import-publishing-settings"></a><span data-ttu-id="4eb9f-232">Импорт параметров публикации</span><span class="sxs-lookup"><span data-stu-id="4eb9f-232">Import publishing settings</span></span>
<span data-ttu-id="4eb9f-233">На этом шаге вы загрузите файл, содержащий сведения о вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-233">In this step, you will download a file containing information about your subscription.</span></span>

1. <span data-ttu-id="4eb9f-234">Введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-234">Enter hello following command:</span></span>
   
        azure login
   
    <span data-ttu-id="4eb9f-235">Эта команда запускает браузер и переходит на страницу загрузки toohello.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-235">This command launches a browser and navigates toohello download page.</span></span> <span data-ttu-id="4eb9f-236">Если будет предложено, войдите в систему hello учетную запись, связанную с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-236">If prompted, log in with hello account associated with your Azure subscription.</span></span>
   
    <!-- ![hello download page][download-publishing-settings] -->
   
    <span data-ttu-id="4eb9f-237">Загрузка файла Hello начинается автоматически. Если этого не произошло, можно щелкнуть ссылку hello в начале hello файла hello загрузки toomanually страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-237">hello file download begins automatically; if it does not, you can click hello link at hello beginning of hello page toomanually download hello file.</span></span> <span data-ttu-id="4eb9f-238">Сохраните hello файл и отметьте hello путь к файлу.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-238">Save hello file and note hello file path.</span></span>
2. <span data-ttu-id="4eb9f-239">Введите следующие параметры hello tooimport команды hello:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-239">Enter hello following command tooimport hello settings:</span></span>
   
        azure account import <path-to-file>
   
    <span data-ttu-id="4eb9f-240">Укажите hello путь и имя файла для публикации файла параметров, загруженный в предыдущем шаге hello hello.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-240">Specify hello path and file name of hello publishing settings file you downloaded in hello previous step.</span></span>
3. <span data-ttu-id="4eb9f-241">После импорта параметров hello, удалите hello файл параметров публикации.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-241">After hello settings are imported, delete hello publish settings file.</span></span> <span data-ttu-id="4eb9f-242">Он больше не нужен, и при этом он содержит важные сведения о вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-242">It is no longer needed, and contains sensitive information regarding your Azure subscription.</span></span>

### <a name="create-an-app-service-web-app"></a><span data-ttu-id="4eb9f-243">Создание веб-приложения службы приложений</span><span class="sxs-lookup"><span data-stu-id="4eb9f-243">Create an App Service web app</span></span>
1. <span data-ttu-id="4eb9f-244">Из командной строки hello, измените каталоги toohello **tasklist** каталога.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-244">From hello command-line, change directories toohello **tasklist** directory.</span></span>
2. <span data-ttu-id="4eb9f-245">Используйте следующие команды toocreate новое веб-приложение hello.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-245">Use hello following command toocreate a new web app.</span></span>
   
        azure site create --git
   
    <span data-ttu-id="4eb9f-246">Будут запрашиваться имя веб-приложения hello и расположение.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-246">You will be prompted for hello web app name and location.</span></span> <span data-ttu-id="4eb9f-247">Укажите уникальное имя и выберите hello географического местоположения учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-247">Provide a unique name and select hello same geographical location as your Azure Storage account.</span></span>
   
    <span data-ttu-id="4eb9f-248">Hello `--git` параметр создает репозитории в Azure для этого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-248">hello `--git` parameter creates a Git repository on Azure for this web app.</span></span> <span data-ttu-id="4eb9f-249">Он также инициализирует репозитория в текущем каталоге hello, если не существует и добавляет [Git удаленного] с именем «azure», который является tooAzure приложения используется toopublish hello.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-249">It also initializes a Git repository in hello current directory if none exists, and adds a [Git remote] named 'azure', which is used toopublish hello application tooAzure.</span></span> <span data-ttu-id="4eb9f-250">Наконец, он создает **web.config** файл, содержащий параметры, используемые приложениями Azure toohost узла.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-250">Finally, it creates a **web.config** file, which contains settings used by Azure toohost node applications.</span></span> <span data-ttu-id="4eb9f-251">Если опустить hello `--git` параметр, но hello каталог содержит репозитория, команда hello по-прежнему будет создавать удаленного hello «azure».</span><span class="sxs-lookup"><span data-stu-id="4eb9f-251">If you omit hello `--git` parameter but hello directory contains a Git repository, hello command will still create hello 'azure' remote.</span></span>
   
    <span data-ttu-id="4eb9f-252">После завершения этой команды вы увидите примерно toohello следующие выходные данные.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-252">Once this command has completed, you will see output similar toohello following.</span></span> <span data-ttu-id="4eb9f-253">Обратите внимание, что hello строки, начинающиеся с **веб-сайт создан на** содержит hello URL-адрес для веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-253">Note that hello line beginning with **Website created at** contains hello URL for hello web app.</span></span>
   
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
   > <span data-ttu-id="4eb9f-254">Если это hello первого приложения службы веб-приложения для вашей подписки будет веб-приложения hello toocreate соответствии toouse hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-254">If this is hello first App Service web app for your subscription, you will be instructed toouse hello Azure Portal toocreate hello web app.</span></span> <span data-ttu-id="4eb9f-255">Дополнительные сведения см. в разделе [Начало работы с веб-приложениями Node.js в службе приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="4eb9f-255">For more information, see [Build and deploy a Node.js web app in Azure App Service].</span></span>
   > 
   > 

### <a name="set-environment-variables"></a><span data-ttu-id="4eb9f-256">Настройка переменных среды</span><span class="sxs-lookup"><span data-stu-id="4eb9f-256">Set environment variables</span></span>
<span data-ttu-id="4eb9f-257">На этом шаге вы добавите конфигурации приложения web tooyour переменных среды в Azure.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-257">In this step, you will add environment variables tooyour web app configuration on Azure.</span></span>
<span data-ttu-id="4eb9f-258">Из командной строки hello введите hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-258">From hello command line, enter hello following:</span></span>

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


<span data-ttu-id="4eb9f-259">Замените  **<storage account name>**  с именем hello хранилища hello учетную запись, созданную ранее и замените  **<storage access key>**  с hello первичный ключ доступа для учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-259">Replace **<storage account name>** with hello name of hello storage account you created earlier, and replace **<storage access key>** with hello primary access key for your storage account.</span></span> <span data-ttu-id="4eb9f-260">(Используйте hello же значений в виде файла config.json hello, созданного ранее).</span><span class="sxs-lookup"><span data-stu-id="4eb9f-260">(Use hello same values as hello config.json file that you created earlier.)</span></span>

<span data-ttu-id="4eb9f-261">Кроме того, можно задать переменные среды в hello [портала Azure](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="4eb9f-261">Alternatively, you can set environment variables in hello [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="4eb9f-262">Открыть колонку hello веб-приложение, нажав кнопку **Обзор** > **веб-приложений** > имя вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-262">Open hello web app's blade by clicking **Browse** > **Web Apps** > your web app name.</span></span>
2. <span data-ttu-id="4eb9f-263">В колонке веб-приложения щелкните **Все параметры** > **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-263">In your web app's blade, click **All Settings** > **Application Settings**.</span></span>
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. <span data-ttu-id="4eb9f-264">Прокрутите вниз toohello **параметры приложения** статьи и добавьте пары ключ значение hello.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-264">Scroll down toohello **App settings** section and add hello key/value pairs.</span></span>
   
     ![Параметры приложения](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. <span data-ttu-id="4eb9f-266">Щелкните **СОХРАНИТЬ**.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-266">Click **SAVE**.</span></span>

### <a name="publish-hello-application"></a><span data-ttu-id="4eb9f-267">Публикация приложения hello</span><span class="sxs-lookup"><span data-stu-id="4eb9f-267">Publish hello application</span></span>
<span data-ttu-id="4eb9f-268">приложение hello toopublish, зафиксируйте tooGit файлы кода hello и затем отправьте tooazure/master.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-268">toopublish hello app, commit hello code files tooGit and then push tooazure/master.</span></span>

1. <span data-ttu-id="4eb9f-269">Задайте учетные данные развертывания.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-269">Set your deployment credentials.</span></span>
   
        azure site deployment user set <name> <password>
2. <span data-ttu-id="4eb9f-270">Добавьте и зафиксируйте файлы своего приложения.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-270">Add and commit your application files.</span></span>
   
        git add .
        git commit -m "adding files"
3. <span data-ttu-id="4eb9f-271">Принудительной фиксации hello toohello веб-приложения служб приложений:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-271">Push hello commit toohello App Service web app:</span></span>
   
        git push azure master
   
    <span data-ttu-id="4eb9f-272">Используйте **master** как hello целевой ветви.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-272">Use **master** as hello target branch.</span></span> <span data-ttu-id="4eb9f-273">В конце развертывания hello hello появляется примерно toohello оператор, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="4eb9f-273">At hello end of hello deployment, you see a statement similar toohello following example:</span></span>
   
        toohttps://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. <span data-ttu-id="4eb9f-274">После завершения операции принудительной отправки hello Обзор toohello веб-приложения URL, ранее возвращенный hello `azure create site` команды tooview приложения.</span><span class="sxs-lookup"><span data-stu-id="4eb9f-274">Once hello push operation has completed, browse toohello web app URL returned previously by hello `azure create site` command tooview your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4eb9f-275">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4eb9f-275">Next steps</span></span>
<span data-ttu-id="4eb9f-276">При hello действия, описанные в этой статье описывается использование сведения toostore hello службы таблиц, можно также использовать [MongoDB](https://mlab.com/azure/).</span><span class="sxs-lookup"><span data-stu-id="4eb9f-276">While hello steps in this article describe using hello Table Service toostore information, you can also use [MongoDB](https://mlab.com/azure/).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4eb9f-277">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="4eb9f-277">Additional resources</span></span>
<span data-ttu-id="4eb9f-278">[Azure CLI]</span><span class="sxs-lookup"><span data-stu-id="4eb9f-278">[Azure CLI]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="4eb9f-279">Изменения</span><span class="sxs-lookup"><span data-stu-id="4eb9f-279">What's changed</span></span>
* <span data-ttu-id="4eb9f-280">Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="4eb9f-280">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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
