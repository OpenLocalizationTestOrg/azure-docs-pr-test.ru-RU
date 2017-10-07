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
# <span data-ttu-id="f7f6e-104"><a name="_Toc395783175"></a>Создание веб-приложения Node.js с использованием Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f7f6e-104"><a name="_Toc395783175"></a>Build a Node.js web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f7f6e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f7f6e-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="f7f6e-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="f7f6e-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="f7f6e-107">Java</span><span class="sxs-lookup"><span data-stu-id="f7f6e-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="f7f6e-108">Python</span><span class="sxs-lookup"><span data-stu-id="f7f6e-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="f7f6e-109">Этот учебник Node.js показано, как toouse Azure Cosmos DB и DocumentDB API toostore и доступ к данным из Node.js Express приложения hello, размещенных на веб-сайтов Azure.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-109">This Node.js tutorial shows you how toouse Azure Cosmos DB and hello DocumentDB API toostore and access data from a Node.js Express application hosted on Azure Websites.</span></span> <span data-ttu-id="f7f6e-110">Вы создадите простое веб-приложение для управления задачами (приложение ToDo), позволяющее создавать, извлекать и выполнять задачи.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-110">You build a simple web-based task-management application, a ToDo app, that allows creating, retrieving, and completing tasks.</span></span> <span data-ttu-id="f7f6e-111">задачи Hello хранятся в виде документов JSON в базе данных Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-111">hello tasks are stored as JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="f7f6e-112">Этот учебник поможет выполнить hello Создание и развертывание приложения hello и объясняется, что происходит на каждого фрагмента кода.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-112">This tutorial walks you through hello creation and deployment of hello app and explains what's happening in each snippet.</span></span>

![Снимок экрана: hello Мои приложения Todo List в этом учебнике Node.js](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

<span data-ttu-id="f7f6e-114">Нет времени toocomplete hello учебника и просто нужно tooget hello законченное решение?</span><span class="sxs-lookup"><span data-stu-id="f7f6e-114">Don't have time toocomplete hello tutorial and just want tooget hello complete solution?</span></span> <span data-ttu-id="f7f6e-115">Это не представляет проблему, можно получить полный пример решения hello из [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="f7f6e-115">Not a problem, you can get hello complete sample solution from [GitHub][GitHub].</span></span> <span data-ttu-id="f7f6e-116">Только чтение hello [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) файл инструкции как toorun hello приложения.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-116">Just read hello [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file for instructions on how toorun hello app.</span></span>

## <span data-ttu-id="f7f6e-117"><a name="_Toc395783176"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f7f6e-117"><a name="_Toc395783176"></a>Prerequisites</span></span>
> [!TIP]
> <span data-ttu-id="f7f6e-118">Этот учебник по Node.js разработан для читателей, обладающих определенным опытом использования Node.js и веб-сайтов Azure.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-118">This Node.js tutorial assumes that you have some prior experience using Node.js and Azure Websites.</span></span>
> 
> 

<span data-ttu-id="f7f6e-119">Перед выполнением инструкции hello в этой статье, следует убедиться, что имеется следующее hello:</span><span class="sxs-lookup"><span data-stu-id="f7f6e-119">Before following hello instructions in this article, you should ensure that you have hello following:</span></span>

* <span data-ttu-id="f7f6e-120">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-120">An active Azure account.</span></span> <span data-ttu-id="f7f6e-121">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f7f6e-122">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f7f6e-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

   <span data-ttu-id="f7f6e-123">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="f7f6e-123">OR</span></span>

   <span data-ttu-id="f7f6e-124">Локальная установка hello [DB эмулятор Azure Cosmos](local-emulator.md) (Windows).</span><span class="sxs-lookup"><span data-stu-id="f7f6e-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md) (Windows only).</span></span>
* <span data-ttu-id="f7f6e-125">[Node.js][Node.js] версии 0.10.29 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-125">[Node.js][Node.js] version v0.10.29 or higher.</span></span>
* <span data-ttu-id="f7f6e-126">[Генератор Express](http://www.expressjs.com/starter/generator.html) (его можно установить через `npm install express-generator -g`).</span><span class="sxs-lookup"><span data-stu-id="f7f6e-126">[Express generator](http://www.expressjs.com/starter/generator.html) (you can install this via `npm install express-generator -g`)</span></span>
* <span data-ttu-id="f7f6e-127">[Git][Git].</span><span class="sxs-lookup"><span data-stu-id="f7f6e-127">[Git][Git].</span></span>

## <span data-ttu-id="f7f6e-128"><a name="_Toc395637761"></a>Шаг 1. Создание учетной записи базы данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f7f6e-128"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="f7f6e-129">Давайте сначала создадим учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-129">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="f7f6e-130">Если уже есть учетная запись, или при использовании hello эмулятор DB Cosmos Azure для этого учебника, можно пропустить слишком[шаг 2: Создание нового приложения Node.js](#_Toc395783178).</span><span class="sxs-lookup"><span data-stu-id="f7f6e-130">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create a new Node.js application](#_Toc395783178).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="f7f6e-131"><a name="_Toc395783178"></a>Шаг 2. Создание приложения Node.js</span><span class="sxs-lookup"><span data-stu-id="f7f6e-131"><a name="_Toc395783178"></a>Step 2: Create a new Node.js application</span></span>
<span data-ttu-id="f7f6e-132">Теперь давайте узнать toocreate базовый проект Hello World Node.js с помощью hello [Express](http://expressjs.com/) framework.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-132">Now let's learn toocreate a basic Hello World Node.js project using hello [Express](http://expressjs.com/) framework.</span></span>

1. <span data-ttu-id="f7f6e-133">Откройте избранные терминала, например hello Node.js командной строки.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-133">Open your favorite terminal, such as hello Node.js command prompt.</span></span>
2. <span data-ttu-id="f7f6e-134">Перейдите в каталог toohello, в которой требуется новое приложение hello toostore.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-134">Navigate toohello directory in which you'd like toostore hello new application.</span></span>
3. <span data-ttu-id="f7f6e-135">Использовать новое приложение вызвало toogenerate express генератор hello **todo**.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-135">Use hello express generator toogenerate a new application called **todo**.</span></span>
   
        express todo
4. <span data-ttu-id="f7f6e-136">Откройте новый каталог **todo** и установите зависимости.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-136">Open your new **todo** directory and install dependencies.</span></span>
   
        cd todo
        npm install
5. <span data-ttu-id="f7f6e-137">Запустите новое приложение.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-137">Run your new application.</span></span>
   
        npm start
6. <span data-ttu-id="f7f6e-138">Можно просмотреть нового приложения, навигация обозревателя слишком[http://localhost:3000](http://localhost:3000).</span><span class="sxs-lookup"><span data-stu-id="f7f6e-138">You can view your new application by navigating your browser too[http://localhost:3000](http://localhost:3000).</span></span>
   
    ![Дополнительные сведения Node.js — снимок экрана приветствия приложения Hello World в окне браузера](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    <span data-ttu-id="f7f6e-140">Затем toostop hello приложения, нажмите клавиши CTRL + C в окне терминала hello и нажмите кнопку **y** tooterminate hello пакетного задания.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-140">Then, toostop hello application, press CTRL+C in hello terminal window and then click **y** tooterminate hello batch job.</span></span>

## <span data-ttu-id="f7f6e-141"><a name="_Toc395783179"></a>Шаг 3. Установка дополнительных модулей</span><span class="sxs-lookup"><span data-stu-id="f7f6e-141"><a name="_Toc395783179"></a>Step 3: Install additional modules</span></span>
<span data-ttu-id="f7f6e-142">Hello **package.json** файл является одним из hello файлы, созданные в корневой hello hello проекта.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-142">hello **package.json** file is one of hello files created in hello root of hello project.</span></span> <span data-ttu-id="f7f6e-143">Этот файл содержит список дополнительных модулей, необходимых для приложения Node.js.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-143">This file contains a list of additional modules that are required for your Node.js application.</span></span> <span data-ttu-id="f7f6e-144">Позже при развертывании этого приложения tooAzure веб-сайтов, этот файл является используется toodetermine toobe необходимость какие модули на Azure toosupport приложение установлено.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-144">Later, when you deploy this application tooAzure Websites, this file is used toodetermine which modules need toobe installed on Azure toosupport your application.</span></span> <span data-ttu-id="f7f6e-145">По-прежнему необходимы tooinstall две дополнительные пакеты для этого учебника.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-145">We still need tooinstall two more packages for this tutorial.</span></span>

1. <span data-ttu-id="f7f6e-146">В hello терминалов, установите hello **async** модуль через npm.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-146">Back in hello terminal, install hello **async** module via npm.</span></span>
   
        npm install async --save
2. <span data-ttu-id="f7f6e-147">Установка hello **documentdb** модуль через npm.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-147">Install hello **documentdb** module via npm.</span></span> <span data-ttu-id="f7f6e-148">Это модуль hello, где происходит все magic hello Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-148">This is hello module where all hello Azure Cosmos DB magic happens.</span></span>
   
        npm install documentdb --save
3. <span data-ttu-id="f7f6e-149">Быстрая проверка hello **package.json** файл приложения hello должны показывать hello дополнительных модулей.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-149">A quick check of hello **package.json** file of hello application should show hello additional modules.</span></span> <span data-ttu-id="f7f6e-150">Этот файл будет сообщить Azure, какие пакеты toodownload и устанавливать при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-150">This file will tell Azure which packages toodownload and install when running your application.</span></span> <span data-ttu-id="f7f6e-151">Она должна иметь вид hello приведенном ниже примере.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-151">It should resemble hello example below.</span></span>
   
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
   
    <span data-ttu-id="f7f6e-152">Это сообщает Node (и позже Azure), что ваше приложение зависит от указанных дополнительных модулей.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-152">This tells Node (and Azure later) that your application depends on these additional modules.</span></span>

## <span data-ttu-id="f7f6e-153"><a name="_Toc395783180"></a>Шаг 4: Использование службы Azure Cosmos DB hello в приложении узла</span><span class="sxs-lookup"><span data-stu-id="f7f6e-153"><a name="_Toc395783180"></a>Step 4: Using hello Azure Cosmos DB service in a node application</span></span>
<span data-ttu-id="f7f6e-154">Который берет на себя все hello начальной установки и конфигурации, теперь давайте get вниз toowhy мы здесь, и это toowrite некоторые код с использованием Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-154">That takes care of all hello initial setup and configuration, now let’s get down toowhy we’re here, and that’s toowrite some code using Azure Cosmos DB.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="f7f6e-155">Создание модели hello</span><span class="sxs-lookup"><span data-stu-id="f7f6e-155">Create hello model</span></span>
1. <span data-ttu-id="f7f6e-156">В каталоге проекта hello, создайте новый каталог с именем **моделей** в hello одной папке с файлом package.json hello.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-156">In hello project directory, create a new directory named **models** in hello same directory as hello package.json file.</span></span>
2. <span data-ttu-id="f7f6e-157">В hello **моделей** каталога, создайте новый файл с именем **taskDao.js**.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-157">In hello **models** directory, create a new file named **taskDao.js**.</span></span> <span data-ttu-id="f7f6e-158">Этот файл будет содержать hello модель для hello задачам, созданным нашего приложения.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-158">This file will contain hello model for hello tasks created by our application.</span></span>
3. <span data-ttu-id="f7f6e-159">В hello же **моделей** каталога, создайте еще один новый файл с именем **docdbUtils.js**.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-159">In hello same **models** directory, create another new file named **docdbUtils.js**.</span></span> <span data-ttu-id="f7f6e-160">Этот файл будет содержать некоторый полезный многократно используемый код, который будет задействован на протяжении нашего приложения.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-160">This file will contain some useful, reusable, code that we will use throughout our application.</span></span> 
4. <span data-ttu-id="f7f6e-161">Копирования hello следующий код в слишком**docdbUtils.js**</span><span class="sxs-lookup"><span data-stu-id="f7f6e-161">Copy hello following code in too**docdbUtils.js**</span></span>
   
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
   
5. <span data-ttu-id="f7f6e-162">Сохраните и закройте hello **docdbUtils.js** файла.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-162">Save and close hello **docdbUtils.js** file.</span></span>
6. <span data-ttu-id="f7f6e-163">В начале hello hello **taskDao.js** файл, добавьте следующий код tooreference hello hello **DocumentDBClient** и hello **docdbUtils.js** созданных ранее:</span><span class="sxs-lookup"><span data-stu-id="f7f6e-163">At hello beginning of hello **taskDao.js** file, add hello following code tooreference hello **DocumentDBClient** and hello **docdbUtils.js** we created above:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. <span data-ttu-id="f7f6e-164">Далее необходимо добавить код toodefine и экспорт hello объекта задачи.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-164">Next, you will add code toodefine and export hello Task object.</span></span> <span data-ttu-id="f7f6e-165">Это отвечает за инициализации объекта нашей задачи и настройка hello базы данных и мы будем использовать коллекции документов.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-165">This is responsible for initializing our Task object and setting up hello Database and Document Collection we will use.</span></span>
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. <span data-ttu-id="f7f6e-166">Добавьте hello следующие дополнительные методы toodefine кода hello объекта задачи, которые позволяют взаимодействия с данными, хранящимися в базе данных Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-166">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in Azure Cosmos DB.</span></span>
   
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
9. <span data-ttu-id="f7f6e-167">Сохраните и закройте hello **taskDao.js** файла.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-167">Save and close hello **taskDao.js** file.</span></span> 

### <a name="create-hello-controller"></a><span data-ttu-id="f7f6e-168">Создание контроллера hello</span><span class="sxs-lookup"><span data-stu-id="f7f6e-168">Create hello controller</span></span>
1. <span data-ttu-id="f7f6e-169">В hello **маршруты** каталог проекта, создайте новый файл с именем **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-169">In hello **routes** directory of your project, create a new file named **tasklist.js**.</span></span> 
2. <span data-ttu-id="f7f6e-170">Добавьте следующий код слишком hello**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-170">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="f7f6e-171">Это загружает hello DocumentDBClient и async модули, в которых используются **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-171">This loads hello DocumentDBClient and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="f7f6e-172">Это также определены hello **TaskList** функции, которая передается экземпляр hello **задачи** объекта было определено ранее:</span><span class="sxs-lookup"><span data-stu-id="f7f6e-172">This also defined hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. <span data-ttu-id="f7f6e-173">Продолжайте добавлять toohello **tasklist.js** файла путем добавления методов hello используется слишком**showTasks addTask**, и **completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="f7f6e-173">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks, addTask**, and **completeTasks**:</span></span>
   
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
4. <span data-ttu-id="f7f6e-174">Сохраните и закройте hello **tasklist.js** файла.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-174">Save and close hello **tasklist.js** file.</span></span>

### <a name="add-configjs"></a><span data-ttu-id="f7f6e-175">Добавление config.js</span><span class="sxs-lookup"><span data-stu-id="f7f6e-175">Add config.js</span></span>
1. <span data-ttu-id="f7f6e-176">В каталоге проекта создайте новый файл с именем **config.js**.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-176">In your project directory create a new file named **config.js**.</span></span>
2. <span data-ttu-id="f7f6e-177">Добавьте hello следующие слишком**config.js**.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-177">Add hello following too**config.js**.</span></span> <span data-ttu-id="f7f6e-178">Он определяет значения и параметры конфигурации, необходимые нашему приложению.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-178">This defines configuration settings and values needed for our application.</span></span>
   
        var config = {}
   
        config.host = process.env.HOST || "[hello URI value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[hello PRIMARY KEY value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. <span data-ttu-id="f7f6e-179">В hello **config.js** файла обновления hello значения узла и значениями hello в колонке hello ключи учетной записи Azure Cosmos DB hello AUTH_KEY [портал Microsoft Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f7f6e-179">In hello **config.js** file, update hello values of HOST and AUTH_KEY using hello values found in hello Keys blade of your Azure Cosmos DB account on hello [Microsoft Azure portal](https://portal.azure.com).</span></span>
4. <span data-ttu-id="f7f6e-180">Сохраните и закройте hello **config.js** файла.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-180">Save and close hello **config.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="f7f6e-181">Изменение app.js</span><span class="sxs-lookup"><span data-stu-id="f7f6e-181">Modify app.js</span></span>
1. <span data-ttu-id="f7f6e-182">В каталоге проекта hello, откройте hello **в файле app.js** файл.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-182">In hello project directory, open hello **app.js** file.</span></span> <span data-ttu-id="f7f6e-183">Этот файл был создан ранее, при создании веб-приложения hello, экспресс-выпуск.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-183">This file was created earlier when hello Express web application was created.</span></span>
2. <span data-ttu-id="f7f6e-184">Добавьте следующий код toohello вверху hello **в файле app.js**</span><span class="sxs-lookup"><span data-stu-id="f7f6e-184">Add hello following code toohello top of **app.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. <span data-ttu-id="f7f6e-185">Этот код определяет hello конфигурации файла toobe использовать, после чего выполняется tooread значений из этого файла в некоторые переменные, которые скоро будут использоваться.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-185">This code defines hello config file toobe used, and proceeds tooread values out of this file into some variables we will use soon.</span></span>
4. <span data-ttu-id="f7f6e-186">Замените следующие две строки в hello **в файле app.js** файла:</span><span class="sxs-lookup"><span data-stu-id="f7f6e-186">Replace hello following two lines in **app.js** file:</span></span>
   
        app.use('/', index);
        app.use('/users', users); 
   
      <span data-ttu-id="f7f6e-187">с hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="f7f6e-187">with hello following snippet:</span></span>
   
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
5. <span data-ttu-id="f7f6e-188">Эти строки определяют новый экземпляр нашей **TaskDao** объект с новой tooAzure подключения Cosmos DB (с использованием значений hello считываться hello **config.js**), инициализировать объект задачи hello, а затем привязать действий формы toomethods на нашем **TaskList** контроллера.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-188">These lines define a new instance of our **TaskDao** object, with a new connection tooAzure Cosmos DB (using hello values read from hello **config.js**), initialize hello task object and then bind form actions toomethods on our **TaskList** controller.</span></span> 
6. <span data-ttu-id="f7f6e-189">Наконец, сохраните и закройте hello **в файле app.js** файл, почти готово.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-189">Finally, save and close hello **app.js** file, we're just about done.</span></span>

## <span data-ttu-id="f7f6e-190"><a name="_Toc395783181"></a>Шаг 5. Построение пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="f7f6e-190"><a name="_Toc395783181"></a>Step 5: Build a user interface</span></span>
<span data-ttu-id="f7f6e-191">Теперь давайте рассмотрим наши внимания toobuilding hello пользовательского интерфейса, фактически взаимодействие пользователя с помощью нашего приложения.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-191">Now let’s turn our attention toobuilding hello user interface so a user can actually interact with our application.</span></span> <span data-ttu-id="f7f6e-192">Здравствуйте, экспресс-выпуск приложения мы создали использует **Jade** как обработчик представлений hello.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-192">hello Express application we created uses **Jade** as hello view engine.</span></span> <span data-ttu-id="f7f6e-193">Дополнительные сведения о Jade см. слишком[http://jade-lang.com/](http://jade-lang.com/).</span><span class="sxs-lookup"><span data-stu-id="f7f6e-193">For more information on Jade please refer too[http://jade-lang.com/](http://jade-lang.com/).</span></span>

1. <span data-ttu-id="f7f6e-194">Hello **layout.jade** файла в hello **представления** каталог используется как глобальный шаблон для других **.jade** файлов.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-194">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="f7f6e-195">На этом этапе вы измените его toouse [Twitter начальной загрузки](https://github.com/twbs/bootstrap), который — это набор средств, который позволяет легко toodesign работы с низким приоритетом привлекательных веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-195">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span> 
2. <span data-ttu-id="f7f6e-196">Откройте hello **layout.jade** файл найден в hello **представления** папки и заменить содержимое hello hello следующее:</span><span class="sxs-lookup"><span data-stu-id="f7f6e-196">Open hello **layout.jade** file found in hello **views** folder and replace hello contents with hello following:</span></span>

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

    <span data-ttu-id="f7f6e-197">Это фактически означает hello **Jade** ядра toorender HTML для нашего приложения и создает **блок** вызывается **содержимого** где можно указать hello макета для содержимое веб-узла страницы.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-197">This effectively tells hello **Jade** engine toorender some HTML for our application and creates a **block** called **content** where we can supply hello layout for our content pages.</span></span>

    <span data-ttu-id="f7f6e-198">Сохраните и закройте файл **layout.jade** .</span><span class="sxs-lookup"><span data-stu-id="f7f6e-198">Save and close this **layout.jade** file.</span></span>

3. <span data-ttu-id="f7f6e-199">Теперь откройте hello **index.jade** файл, hello представление, которое будет использоваться нашего приложения и замените hello содержимое файла hello hello следующее:</span><span class="sxs-lookup"><span data-stu-id="f7f6e-199">Now open hello **index.jade** file, hello view that will be used by our application, and replace hello content of hello file with hello following:</span></span>
   
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
   

<span data-ttu-id="f7f6e-200">Это расширяет возможности макета и приводятся сведения для hello **содержимого** заполнителя, мы видели в hello **layout.jade** файлов более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-200">This extends layout, and provides content for hello **content** placeholder we saw in hello **layout.jade** file earlier.</span></span>
   
<span data-ttu-id="f7f6e-201">В макете мы создали две формы HTML.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-201">In this layout we created two HTML forms.</span></span>

<span data-ttu-id="f7f6e-202">Первая форма Hello содержит таблицу для наших данных и кнопки, которая позволяет нам tooupdate элементов путем учета слишком**/completetask** метод нашей контроллера.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-202">hello first form contains a table for our data and a button that allows us tooupdate items by posting too**/completetask** method of our controller.</span></span>
    
<span data-ttu-id="f7f6e-203">Вторая форма Hello содержит два поля ввода и кнопку, которая позволяет нам toocreate новый элемент путем учета слишком**/addtask** метод нашей контроллера.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-203">hello second form contains two input fields and a button that allows us toocreate a new item by posting too**/addtask** method of our controller.</span></span>

<span data-ttu-id="f7f6e-204">Это должна быть все, что нужно для наших toowork приложения.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-204">This should be all that we need for our application toowork.</span></span>

## <span data-ttu-id="f7f6e-205"><a name="_Toc395783181"></a>Шаг 6. Локальный запуск приложения</span><span class="sxs-lookup"><span data-stu-id="f7f6e-205"><a name="_Toc395783181"></a>Step 6: Run your application locally</span></span>
1. <span data-ttu-id="f7f6e-206">приложение hello tootest на локальном компьютере, запустите `npm start` в hello терминалов toostart приложения, а затем обновите ваш [http://localhost:3000](http://localhost:3000) страницы браузера.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-206">tootest hello application on your local machine, run `npm start` in hello terminal toostart your application, then refresh your [http://localhost:3000](http://localhost:3000) browser page.</span></span> <span data-ttu-id="f7f6e-207">Страница приветствия должен выглядеть так hello изображения ниже:</span><span class="sxs-lookup"><span data-stu-id="f7f6e-207">hello page should now look like hello image below:</span></span>
   
    ![Снимок экрана: hello приложение MyTodo списка в окне браузера](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > <span data-ttu-id="f7f6e-209">Получив ошибку о hello отступ в файл layout.jade hello или index.jade hello, убедитесь, что первые две строки hello в обоих файлах выравнивается по левому краю, без пробелов.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-209">If you receive an error about hello indent in hello layout.jade file or hello index.jade file, ensure that hello first two lines in both files is left justified, with no spaces.</span></span> <span data-ttu-id="f7f6e-210">При наличии пробелов перед hello первые две строки, удалите их, сохраните оба файла, а затем обновите окно браузера.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-210">If there are spaces before hello first two lines, remove them, save both files, then refresh your browser window.</span></span> 

2. <span data-ttu-id="f7f6e-211">Использовать hello элемент, имя элемента и категории поля tooenter новую задачу и нажмите кнопку **добавить элемент**.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-211">Use hello Item, Item Name and Category fields tooenter a new task and then click **Add Item**.</span></span> <span data-ttu-id="f7f6e-212">Будет создан документ в Azure Cosmos DB с заданными свойствами.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-212">This creates a document in Azure Cosmos DB with those properties.</span></span> 
3. <span data-ttu-id="f7f6e-213">Страница приветствия следует обновить hello toodisplay недавно созданном элемента в список ToDo hello.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-213">hello page should update toodisplay hello newly created item in hello ToDo list.</span></span>
   
    ![Снимок экрана: hello приложения с помощью нового элемента в список ToDo hello](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. <span data-ttu-id="f7f6e-215">просто установите флажок "hello" в столбце завершения hello toocomplete задачу и нажмите кнопку **обновление задач**.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-215">toocomplete a task, simply check hello checkbox in hello Complete column, and then click **Update tasks**.</span></span> <span data-ttu-id="f7f6e-216">Этот документ hello обновлений, уже созданы.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-216">This updates hello document you already created.</span></span>

5. <span data-ttu-id="f7f6e-217">приложение hello toostop, нажмите клавиши CTRL + C в окне терминала hello и нажмите кнопку **Y** tooterminate hello пакетного задания.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-217">toostop hello application, press CTRL+C in hello terminal window and then click **Y** tooterminate hello batch job.</span></span>

## <span data-ttu-id="f7f6e-218"><a name="_Toc395783182"></a>Шаг 7: Развертывание вашего приложения tooAzure проект разработки веб-сайтов</span><span class="sxs-lookup"><span data-stu-id="f7f6e-218"><a name="_Toc395783182"></a>Step 7: Deploy your application development project tooAzure Websites</span></span>
1. <span data-ttu-id="f7f6e-219">Если это еще не сделано, включите репозиторий git для веб-сайта Azure.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-219">If you haven't already, enable a git repository for your Azure Website.</span></span> <span data-ttu-id="f7f6e-220">Инструкции о том, как можно найти toodo в hello [tooAzure локальное развертывание Git службы приложений](../app-service-web/app-service-deploy-local-git.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-220">You can find instructions on how toodo this in hello [Local Git Deployment tooAzure App Service](../app-service-web/app-service-deploy-local-git.md) topic.</span></span>
2. <span data-ttu-id="f7f6e-221">Добавьте веб-сайт Azure в качестве удаленного репозитория git.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-221">Add your Azure Website as a git remote.</span></span>
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. <span data-ttu-id="f7f6e-222">Развертывание с помощью принудительной отправки toohello удаленной.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-222">Deploy by pushing toohello remote.</span></span>
   
        git push azure master
4. <span data-ttu-id="f7f6e-223">Через несколько секунд Visual Studio завершит публикацию вашего веб-приложения и запустит браузер, где вы увидите свое творение, запущенное в Azure!</span><span class="sxs-lookup"><span data-stu-id="f7f6e-223">In a few seconds, git will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>

    <span data-ttu-id="f7f6e-224">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="f7f6e-224">Congratulations!</span></span> <span data-ttu-id="f7f6e-225">Только первый Node.js Express веб-приложения с помощью Azure Cosmos DB создания и публикации tooAzure веб-сайтов.</span><span class="sxs-lookup"><span data-stu-id="f7f6e-225">You have just built your first Node.js Express Web Application using Azure Cosmos DB and published it tooAzure Websites.</span></span>

    <span data-ttu-id="f7f6e-226">Если требуется toodownload или toohello полный перечень приложений см. в этом учебнике, ее можно загрузить из [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="f7f6e-226">If you want toodownload or refer toohello complete reference application for this tutorial, it can be downloaded from [GitHub][GitHub].</span></span>

## <span data-ttu-id="f7f6e-227"><a name="_Toc395637775"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f7f6e-227"><a name="_Toc395637775"></a>Next steps</span></span>

* <span data-ttu-id="f7f6e-228">Требуется tooperform масштаб и производительность, тестирование с помощью Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="f7f6e-228">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="f7f6e-229">Дополнительные сведения см. в статье о [проверке производительности и масштабирования с помощью Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="f7f6e-229">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="f7f6e-230">Узнайте, каким образом слишком[мониторинг учетной записи Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="f7f6e-230">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="f7f6e-231">Выполнять запросы к нашей образец набора данных в hello [площадку запросов](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="f7f6e-231">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="f7f6e-232">Просмотр hello [документации Azure Cosmos DB](https://docs.microsoft.com/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="f7f6e-232">Explore hello [Azure Cosmos DB documentation](https://docs.microsoft.com/azure/documentdb/).</span></span>

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

