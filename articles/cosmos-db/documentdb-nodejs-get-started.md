---
title: "Учебник aaaNode.js для hello API DocumentDB для Azure Cosmos DB | Документы Microsoft"
description: "Node.js учебник, в котором создается Cosmos DB с hello DocumentDB API."
keywords: "node.js, руководство, база данных node"
services: cosmos-db
documentationcenter: node.js
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: 14d52110-1dce-4ac0-9dd9-f936afccd550
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: node
ms.topic: article
ms.date: 08/14/2017
ms.author: anhoh
ms.openlocfilehash: fce244c6a5f321608e82ca51a2c987e84b98bffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-tutorial-use-hello-documentdb-api-in-azure-cosmos-db-toocreate-a-nodejs-console-application"></a><span data-ttu-id="c77b3-104">Учебник по node.js: hello использования DocumentDB API в базу данных Azure Cosmos toocreate консольное приложение Node.js</span><span class="sxs-lookup"><span data-stu-id="c77b3-104">Node.js tutorial: Use hello DocumentDB API in Azure Cosmos DB toocreate a Node.js console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c77b3-105">.NET</span><span class="sxs-lookup"><span data-stu-id="c77b3-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="c77b3-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="c77b3-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="c77b3-107">Node.js для MongoDB</span><span class="sxs-lookup"><span data-stu-id="c77b3-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="c77b3-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="c77b3-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="c77b3-109">Java</span><span class="sxs-lookup"><span data-stu-id="c77b3-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="c77b3-110">C++</span><span class="sxs-lookup"><span data-stu-id="c77b3-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="c77b3-111">Вас приветствует учебник toohello Node.js для пакета SDK для Node.js DB Cosmos Azure hello!</span><span class="sxs-lookup"><span data-stu-id="c77b3-111">Welcome toohello Node.js tutorial for hello Azure Cosmos DB Node.js SDK!</span></span> <span data-ttu-id="c77b3-112">После изучения этого руководства у вас будет консольное приложение, которое создает ресурсы Azure Cosmos DB и отправляет запросы к ним.</span><span class="sxs-lookup"><span data-stu-id="c77b3-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="c77b3-113">Мы рассмотрим следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="c77b3-113">We'll cover:</span></span>

* <span data-ttu-id="c77b3-114">Создание и подключение учетной записи Azure Cosmos DB tooan</span><span class="sxs-lookup"><span data-stu-id="c77b3-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="c77b3-115">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="c77b3-115">Setting up your application</span></span>
* <span data-ttu-id="c77b3-116">Создание базы данных Node</span><span class="sxs-lookup"><span data-stu-id="c77b3-116">Creating a node database</span></span>
* <span data-ttu-id="c77b3-117">создание коллекции;</span><span class="sxs-lookup"><span data-stu-id="c77b3-117">Creating a collection</span></span>
* <span data-ttu-id="c77b3-118">создание документов JSON;</span><span class="sxs-lookup"><span data-stu-id="c77b3-118">Creating JSON documents</span></span>
* <span data-ttu-id="c77b3-119">Запрос к коллекции hello</span><span class="sxs-lookup"><span data-stu-id="c77b3-119">Querying hello collection</span></span>
* <span data-ttu-id="c77b3-120">замена документа;</span><span class="sxs-lookup"><span data-stu-id="c77b3-120">Replacing a document</span></span>
* <span data-ttu-id="c77b3-121">удаление документа;</span><span class="sxs-lookup"><span data-stu-id="c77b3-121">Deleting a document</span></span>
* <span data-ttu-id="c77b3-122">Удаление базы данных узла hello</span><span class="sxs-lookup"><span data-stu-id="c77b3-122">Deleting hello node database</span></span>

<span data-ttu-id="c77b3-123">У вас нет времени?</span><span class="sxs-lookup"><span data-stu-id="c77b3-123">Don't have time?</span></span> <span data-ttu-id="c77b3-124">Не беспокойтесь!</span><span class="sxs-lookup"><span data-stu-id="c77b3-124">Don't worry!</span></span> <span data-ttu-id="c77b3-125">законченное решение Hello можно найти в [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="c77b3-125">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span> <span data-ttu-id="c77b3-126">В разделе [получить комплексное решение hello](#GetSolution) быстрого инструкции.</span><span class="sxs-lookup"><span data-stu-id="c77b3-126">See [Get hello complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="c77b3-127">После прохождения учебника Node.js hello, пожалуйста голосования hello используйте кнопки в hello верхней и нижней части этой страницы toogive нам отзыв.</span><span class="sxs-lookup"><span data-stu-id="c77b3-127">After you've completed hello Node.js tutorial, please use hello voting buttons at hello top and bottom of this page toogive us feedback.</span></span> <span data-ttu-id="c77b3-128">Если вы хотите нам toocontact напрямую, если вам свободного tooinclude адрес вашей электронной почты в комментарии.</span><span class="sxs-lookup"><span data-stu-id="c77b3-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="c77b3-129">А теперь приступим к работе!</span><span class="sxs-lookup"><span data-stu-id="c77b3-129">Now let's get started!</span></span>

## <a name="prerequisites-for-hello-nodejs-tutorial"></a><span data-ttu-id="c77b3-130">Необходимые условия для учебника Node.js hello</span><span class="sxs-lookup"><span data-stu-id="c77b3-130">Prerequisites for hello Node.js tutorial</span></span>
<span data-ttu-id="c77b3-131">Убедитесь, что у вас есть следующие hello:</span><span class="sxs-lookup"><span data-stu-id="c77b3-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="c77b3-132">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="c77b3-132">An active Azure account.</span></span> <span data-ttu-id="c77b3-133">Если у вас нет такой учетной записи, вы можете зарегистрироваться для использования [бесплатной пробной версии Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c77b3-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
    * <span data-ttu-id="c77b3-134">Кроме того, можно использовать hello [DB эмулятор Azure Cosmos](local-emulator.md) для этого учебника.</span><span class="sxs-lookup"><span data-stu-id="c77b3-134">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="c77b3-135">[Node.js](https://nodejs.org/) версии v0.10.29 или выше.</span><span class="sxs-lookup"><span data-stu-id="c77b3-135">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="c77b3-136">Шаг 1. Создание учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c77b3-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="c77b3-137">Давайте создадим учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c77b3-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="c77b3-138">При наличии учетной записи требуется toouse можно сразу перейти слишком[настроить приложение Node.js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="c77b3-138">If you already have an account you want toouse, you can skip ahead too[Set up your Node.js application](#SetupNode).</span></span> <span data-ttu-id="c77b3-139">Если вы используете hello Azure Cosmos DB эмулятор, выполните действия hello в [DB эмулятор Azure Cosmos](local-emulator.md) toosetup hello эмулятора и пропускать слишком[настроить приложение Node.js](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="c77b3-139">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Node.js application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="c77b3-140"><a id="SetupNode"></a>Шаг 2. Настройка приложения Node.js</span><span class="sxs-lookup"><span data-stu-id="c77b3-140"><a id="SetupNode"></a>Step 2: Set up your Node.js application</span></span>
1. <span data-ttu-id="c77b3-141">Откройте удобный для вас терминал.</span><span class="sxs-lookup"><span data-stu-id="c77b3-141">Open your favorite terminal.</span></span>
2. <span data-ttu-id="c77b3-142">Найдите папку hello или каталог, куда toosave приложение Node.js.</span><span class="sxs-lookup"><span data-stu-id="c77b3-142">Locate hello folder or directory where you'd like toosave your Node.js application.</span></span>
3. <span data-ttu-id="c77b3-143">Создайте две пустые файлы JavaScript с hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="c77b3-143">Create two empty JavaScript files with hello following commands:</span></span>
   * <span data-ttu-id="c77b3-144">Windows:</span><span class="sxs-lookup"><span data-stu-id="c77b3-144">Windows:</span></span>
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * <span data-ttu-id="c77b3-145">Linux или OS X:</span><span class="sxs-lookup"><span data-stu-id="c77b3-145">Linux/OS X:</span></span>
     * ```touch app.js```
     * ```touch config.js```
4. <span data-ttu-id="c77b3-146">Установите модуль hello documentdb через npm.</span><span class="sxs-lookup"><span data-stu-id="c77b3-146">Install hello documentdb module via npm.</span></span> <span data-ttu-id="c77b3-147">Hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c77b3-147">Use hello following command:</span></span>
   * ```npm install documentdb --save```

<span data-ttu-id="c77b3-148">Отлично!</span><span class="sxs-lookup"><span data-stu-id="c77b3-148">Great!</span></span> <span data-ttu-id="c77b3-149">Теперь, когда настройка завершена, можно начать писать код.</span><span class="sxs-lookup"><span data-stu-id="c77b3-149">Now that you've finished setting up, let's start writing some code.</span></span>

## <span data-ttu-id="c77b3-150"><a id="Config"></a>Шаг 3. Настройка конфигурации приложения</span><span class="sxs-lookup"><span data-stu-id="c77b3-150"><a id="Config"></a>Step 3: Set your app's configurations</span></span>
<span data-ttu-id="c77b3-151">Откройте файл ```config.js``` в предпочитаемом текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="c77b3-151">Open ```config.js``` in your favorite text editor.</span></span>

<span data-ttu-id="c77b3-152">Затем скопировать и вставить hello Приведенный далее фрагмент кода и задайте свойства ```config.endpoint``` и ```config.primaryKey``` tooyour Azure Cosmos DB uri конечной точки и первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="c77b3-152">Then, copy and paste hello code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` tooyour Azure Cosmos DB endpoint uri and primary key.</span></span> <span data-ttu-id="c77b3-153">Оба эти конфигурации можно найти в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c77b3-153">Both these configurations can be found in hello [Azure portal](https://portal.azure.com).</span></span>

![Учебник node.js — снимок экрана приветствия портал Azure, показывающая Azure Cosmos DB учетная запись, с hello общаются выделяются hello ключи кнопки выделены на hello Azure Cosmos DB учетной записи и, при необходимости hello URI, первичный ключ и ВТОРИЧНЫЙ ключ значения, которые выделены на hello Ключи колонке - узел базы данных][keys]

    // ADD THIS PART tooYOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

<span data-ttu-id="c77b3-155">Скопируйте и вставьте hello ```database id```, ```collection id```, и ```JSON documents``` tooyour ```config``` объект ниже задаются вашей ```config.endpoint``` и ```config.authKey``` свойства.</span><span class="sxs-lookup"><span data-stu-id="c77b3-155">Copy and paste hello ```database id```, ```collection id```, and ```JSON documents``` tooyour ```config``` object below where you set your ```config.endpoint``` and ```config.authKey``` properties.</span></span> <span data-ttu-id="c77b3-156">При наличии данных, отсылаемых toostore в базе данных можно использовать базу данных Cosmos Azure [средство переноса данных](import-data.md) вместо добавления определения hello документа.</span><span class="sxs-lookup"><span data-stu-id="c77b3-156">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) rather than adding hello document definitions.</span></span>

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART tooYOUR CODE
    config.database = {
        "id": "FamilyDB"
    };

    config.collection = {
        "id": "FamilyColl"
    };

    config.documents = {
        "Andersen": {
            "id": "Anderson.1",
            "lastName": "Andersen",
            "parents": [{
                "firstName": "Thomas"
            }, {
                    "firstName": "Mary Kay"
                }],
            "children": [{
                "firstName": "Henriette Thaulow",
                "gender": "female",
                "grade": 5,
                "pets": [{
                    "givenName": "Fluffy"
                }]
            }],
            "address": {
                "state": "WA",
                "county": "King",
                "city": "Seattle"
            }
        },
        "Wakefield": {
            "id": "Wakefield.7",
            "parents": [{
                "familyName": "Wakefield",
                "firstName": "Robin"
            }, {
                    "familyName": "Miller",
                    "firstName": "Ben"
                }],
            "children": [{
                "familyName": "Merriam",
                "firstName": "Jesse",
                "gender": "female",
                "grade": 8,
                "pets": [{
                    "givenName": "Goofy"
                }, {
                        "givenName": "Shadow"
                    }]
            }, {
                    "familyName": "Miller",
                    "firstName": "Lisa",
                    "gender": "female",
                    "grade": 1
                }],
            "address": {
                "state": "NY",
                "county": "Manhattan",
                "city": "NY"
            },
            "isRegistered": false
        }
    };


<span data-ttu-id="c77b3-157">Hello базы данных, коллекции и определения документов будет выступать в качестве базы данных Azure Cosmos ```database id```, ```collection id```и данные документа.</span><span class="sxs-lookup"><span data-stu-id="c77b3-157">hello database, collection, and document definitions will act as your Azure Cosmos DB ```database id```, ```collection id```, and documents' data.</span></span>

<span data-ttu-id="c77b3-158">Наконец, экспортировать вашей ```config``` объекта, чтобы на него можно ссылаться в hello ```app.js``` файла.</span><span class="sxs-lookup"><span data-stu-id="c77b3-158">Finally, export your ```config``` object, so that you can reference it within hello ```app.js``` file.</span></span>

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART tooYOUR CODE
    module.exports = config;

## <span data-ttu-id="c77b3-159"><a id="Connect"></a>Шаг 4: Учетная запись Azure Cosmos DB tooan подключения</span><span class="sxs-lookup"><span data-stu-id="c77b3-159"><a id="Connect"></a> Step 4: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="c77b3-160">Откройте ваш пустым ```app.js``` файл в текстовом редакторе hello.</span><span class="sxs-lookup"><span data-stu-id="c77b3-160">Open your empty ```app.js``` file in hello text editor.</span></span> <span data-ttu-id="c77b3-161">Скопируйте и вставьте код hello ниже tooimport hello ```documentdb``` модуль и только что созданный ```config``` модуля.</span><span class="sxs-lookup"><span data-stu-id="c77b3-161">Copy and paste hello code below tooimport hello ```documentdb``` module and your newly created ```config``` module.</span></span>

    // ADD THIS PART tooYOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

<span data-ttu-id="c77b3-162">Скопируйте и вставьте hello кода toouse hello ранее сохраненные ```config.endpoint``` и ```config.primaryKey``` toocreate новый DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="c77b3-162">Copy and paste hello code toouse hello previously saved ```config.endpoint``` and ```config.primaryKey``` toocreate a new DocumentClient.</span></span>

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART tooYOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

<span data-ttu-id="c77b3-163">Теперь, когда имеется hello кода tooinitialize hello Azure Cosmos DB клиента, давайте рассмотрим работы с ресурсами Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c77b3-163">Now that you have hello code tooinitialize hello Azure Cosmos DB client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <a name="step-5-create-a-node-database"></a><span data-ttu-id="c77b3-164">Шаг 5. Создание базы данных Node</span><span class="sxs-lookup"><span data-stu-id="c77b3-164">Step 5: Create a Node database</span></span>
<span data-ttu-id="c77b3-165">Скопируйте и вставьте код hello ниже hello tooset код состояния HTTP не найден, URL-адрес hello базы данных и URL-адрес коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="c77b3-165">Copy and paste hello code below tooset hello HTTP status for Not Found, hello database url, and hello collection url.</span></span> <span data-ttu-id="c77b3-166">Эти URL-адреса — это процесс поиска клиента Azure Cosmos DB hello, hello подходящей базы данных и коллекции.</span><span class="sxs-lookup"><span data-stu-id="c77b3-166">These urls are how hello Azure Cosmos DB client will find hello right database and collection.</span></span>

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART tooYOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

<span data-ttu-id="c77b3-167">Объект [базы данных](documentdb-resources.md#databases) могут быть созданы с помощью hello [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) функции hello **DocumentClient** класса.</span><span class="sxs-lookup"><span data-stu-id="c77b3-167">A [database](documentdb-resources.md#databases) can be created by using hello [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="c77b3-168">База данных находится hello логический контейнер для хранения документов, секционированный по коллекциям.</span><span class="sxs-lookup"><span data-stu-id="c77b3-168">A database is hello logical container of document storage partitioned across collections.</span></span>

<span data-ttu-id="c77b3-169">Скопируйте и вставьте hello **getDatabase** функции для создания новой базы данных в файле в файле app.js hello с hello ```id``` , указываемой hello ```config``` объекта.</span><span class="sxs-lookup"><span data-stu-id="c77b3-169">Copy and paste hello **getDatabase** function for creating your new database in hello app.js file with hello ```id``` specified in hello ```config``` object.</span></span> <span data-ttu-id="c77b3-170">Hello функция будет проверять при hello базы данных с hello же ```FamilyRegistry``` идентификатор еще не существует.</span><span class="sxs-lookup"><span data-stu-id="c77b3-170">hello function will check if hello database with hello same ```FamilyRegistry``` id does not already exist.</span></span> <span data-ttu-id="c77b3-171">Если она существует, мы вернем ее вместо создания новой базы данных.</span><span class="sxs-lookup"><span data-stu-id="c77b3-171">If it does exist, we'll return that database instead of creating a new one.</span></span>

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART tooYOUR CODE
    function getDatabase() {
        console.log(`Getting database:\n${config.database.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDatabase(databaseUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDatabase(config.database, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

<span data-ttu-id="c77b3-172">Скопируйте и вставьте приведенный ниже код hello задаются hello **getDatabase** функции tooadd hello вспомогательную функцию **выхода** , будет печататься приветственное сообщение выхода и вызов hello слишком**getDatabase** функции.</span><span class="sxs-lookup"><span data-stu-id="c77b3-172">Copy and paste hello code below where you set hello **getDatabase** function tooadd hello helper function **exit** that will print hello exit message and hello call too**getDatabase** function.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key tooexit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="c77b3-173">Найдите в окне терминала вашей ```app.js``` файл и выполните команду hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="c77b3-173">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="c77b3-174">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="c77b3-174">Congratulations!</span></span> <span data-ttu-id="c77b3-175">Вы успешно создали базу данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c77b3-175">You have successfully created an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="c77b3-176"><a id="CreateColl"></a>Шаг 6. Создание коллекции</span><span class="sxs-lookup"><span data-stu-id="c77b3-176"><a id="CreateColl"></a>Step 6: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="c77b3-177">Элемент **CreateDocumentCollectionAsync** создаст коллекцию, с которой связаны ценовые требования.</span><span class="sxs-lookup"><span data-stu-id="c77b3-177">**CreateDocumentCollectionAsync** will create a new collection, which has pricing implications.</span></span> <span data-ttu-id="c77b3-178">Дополнительные сведения см. на нашей [странице цен](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="c77b3-178">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="c77b3-179">Объект [коллекции](documentdb-resources.md#collections) могут быть созданы с помощью hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) функции hello **DocumentClient** класса.</span><span class="sxs-lookup"><span data-stu-id="c77b3-179">A [collection](documentdb-resources.md#collections) can be created by using hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="c77b3-180">Коллекция представляет собой контейнер документов JSON и связанную с ними логику в виде приложения JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c77b3-180">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="c77b3-181">Скопируйте и вставьте hello **getCollection** функция под hello **getDatabase** функции в файл toocreate hello в файле app.js новой коллекции с hello ```id``` указан в hello ```config```объекта.</span><span class="sxs-lookup"><span data-stu-id="c77b3-181">Copy and paste hello **getCollection** function underneath hello **getDatabase** function in hello app.js file toocreate your new collection with hello ```id``` specified in hello ```config``` object.</span></span> <span data-ttu-id="c77b3-182">Опять же, мы проверим toomake убедитесь, что коллекция с таким же hello ```FamilyCollection``` идентификатор еще не существует.</span><span class="sxs-lookup"><span data-stu-id="c77b3-182">Again, we'll check toomake sure a collection with hello same ```FamilyCollection``` id does not already exist.</span></span> <span data-ttu-id="c77b3-183">Если она существует, мы вернем ее вместо создания новой коллекции.</span><span class="sxs-lookup"><span data-stu-id="c77b3-183">If it does exist, we'll return that collection instead of creating a new one.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getCollection() {
        console.log(`Getting collection:\n${config.collection.id}\n`);

        return new Promise((resolve, reject) => {
            client.readCollection(collectionUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

<span data-ttu-id="c77b3-184">Скопируйте и вставьте код hello вызова hello слишком**getDatabase** tooexecute hello **getCollection** функции.</span><span class="sxs-lookup"><span data-stu-id="c77b3-184">Copy and paste hello code below hello call too**getDatabase** tooexecute hello **getCollection** function.</span></span>

    getDatabase()

    // ADD THIS PART tooYOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="c77b3-185">Найдите в окне терминала вашей ```app.js``` файл и выполните команду hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="c77b3-185">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="c77b3-186">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="c77b3-186">Congratulations!</span></span> <span data-ttu-id="c77b3-187">Вы успешно создали коллекцию Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c77b3-187">You have successfully created an Azure Cosmos DB collection.</span></span>

## <span data-ttu-id="c77b3-188"><a id="CreateDoc"></a>Шаг 7. Создание документа</span><span class="sxs-lookup"><span data-stu-id="c77b3-188"><a id="CreateDoc"></a>Step 7: Create a document</span></span>
<span data-ttu-id="c77b3-189">Объект [документа](documentdb-resources.md#documents) могут быть созданы с помощью hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) функции hello **DocumentClient** класса.</span><span class="sxs-lookup"><span data-stu-id="c77b3-189">A [document](documentdb-resources.md#documents) can be created by using hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="c77b3-190">Документы относятся к пользовательскому (произвольному) содержимому JSON.</span><span class="sxs-lookup"><span data-stu-id="c77b3-190">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="c77b3-191">Теперь можно вставить документ в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c77b3-191">You can now insert a document into Azure Cosmos DB.</span></span>

<span data-ttu-id="c77b3-192">Скопируйте и вставьте hello **getFamilyDocument** функция под hello **getCollection** функции для создания hello документы, содержащие данные JSON hello, сохраненные в hello ```config``` объекта.</span><span class="sxs-lookup"><span data-stu-id="c77b3-192">Copy and paste hello **getFamilyDocument** function underneath hello **getCollection** function for creating hello documents containing hello JSON data saved in hello ```config``` object.</span></span> <span data-ttu-id="c77b3-193">Опять же, мы проверим toomake убедитесь, что документ с таким же идентификатором уже существует hello.</span><span class="sxs-lookup"><span data-stu-id="c77b3-193">Again, we'll check toomake sure a document with hello same id does not already exist.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Getting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDocument(documentUrl, { partitionKey: document.district }, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDocument(collectionUrl, document, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="c77b3-194">Скопируйте и вставьте код hello вызова hello слишком**getCollection** tooexecute hello **getFamilyDocument** функции.</span><span class="sxs-lookup"><span data-stu-id="c77b3-194">Copy and paste hello code below hello call too**getCollection** tooexecute hello **getFamilyDocument** function.</span></span>

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="c77b3-195">Найдите в окне терминала вашей ```app.js``` файл и выполните команду hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="c77b3-195">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="c77b3-196">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="c77b3-196">Congratulations!</span></span> <span data-ttu-id="c77b3-197">Вы успешно создали документ Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c77b3-197">You have successfully created an Azure Cosmos DB document.</span></span>

![Node.js в учебной базе данных - диаграмма, иллюстрирующая hello иерархическую связь между hello учетной записи, hello базы данных, коллекции hello и документы hello - узла](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <span data-ttu-id="c77b3-199"><a id="Query"></a>Шаг 8. Запрос ресурсов Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c77b3-199"><a id="Query"></a>Step 8: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="c77b3-200">Azure Cosmos DB поддерживает [полнофункциональные запросы](documentdb-sql-query.md) к документам JSON, хранящимся в каждой коллекции.</span><span class="sxs-lookup"><span data-stu-id="c77b3-200">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="c77b3-201">Hello следующем образце кода показан запрос, который можно запустить с документами hello в коллекции.</span><span class="sxs-lookup"><span data-stu-id="c77b3-201">hello following sample code shows a query that you can run against hello documents in your collection.</span></span>

<span data-ttu-id="c77b3-202">Скопируйте и вставьте hello **queryCollection** функция под hello **getFamilyDocument** функции в файле в файле app.js hello.</span><span class="sxs-lookup"><span data-stu-id="c77b3-202">Copy and paste hello **queryCollection** function underneath hello **getFamilyDocument** function in hello app.js file.</span></span> <span data-ttu-id="c77b3-203">Azure Cosmos DB поддерживает SQL-подобные запросы, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="c77b3-203">Azure Cosmos DB supports SQL-like queries as shown below.</span></span> <span data-ttu-id="c77b3-204">Дополнительные сведения о построении сложных запросов извлечь hello [площадку запросов](https://www.documentdb.com/sql/demo) и hello [запрос документации](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="c77b3-204">For more information on building complex queries, check out hello [Query Playground](https://www.documentdb.com/sql/demo) and hello [query documentation](documentdb-sql-query.md).</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function queryCollection() {
        console.log(`Querying collection through index:\n${config.collection.id}`);

        return new Promise((resolve, reject) => {
            client.queryDocuments(
                collectionUrl,
                'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
            ).toArray((err, results) => {
                if (err) reject(err)
                else {
                    for (var queryResult of results) {
                        let resultString = JSON.stringify(queryResult);
                        console.log(`\tQuery returned ${resultString}`);
                    }
                    console.log();
                    resolve(results);
                }
            });
        });
    };


<span data-ttu-id="c77b3-205">Hello, следующая диаграмма иллюстрирует, как hello базы данных SQL Azure Cosmos синтаксис называется с коллекцией hello созданный запрос.</span><span class="sxs-lookup"><span data-stu-id="c77b3-205">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created.</span></span>

![Node.js в учебной базе данных - схеме наглядного области hello и это означает запроса hello - узла](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

<span data-ttu-id="c77b3-207">Hello [FROM](documentdb-sql-query.md#FromClause) ключевое слово является необязательным в hello запроса, так как запросы Azure Cosmos DB уже области tooa одну коллекцию.</span><span class="sxs-lookup"><span data-stu-id="c77b3-207">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="c77b3-208">Поэтому слова "FROM Families f" можно заменить на "FROM root r" или любое другое имя переменной.</span><span class="sxs-lookup"><span data-stu-id="c77b3-208">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="c77b3-209">Azure Cosmos DB определит, что семейств, корень или имя переменной hello выбрана, ссылка hello текущей коллекции по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c77b3-209">Azure Cosmos DB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

<span data-ttu-id="c77b3-210">Скопируйте и вставьте код hello вызова hello слишком**getFamilyDocument** tooexecute hello **queryCollection** функции.</span><span class="sxs-lookup"><span data-stu-id="c77b3-210">Copy and paste hello code below hello call too**getFamilyDocument** tooexecute hello **queryCollection** function.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART tooYOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="c77b3-211">Найдите в окне терминала вашей ```app.js``` файл и выполните команду hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="c77b3-211">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="c77b3-212">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="c77b3-212">Congratulations!</span></span> <span data-ttu-id="c77b3-213">Вы успешно выполнили запрос к базе данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c77b3-213">You have successfully queried Azure Cosmos DB documents.</span></span>

## <span data-ttu-id="c77b3-214"><a id="ReplaceDocument"></a>Шаг 9. Замена документа</span><span class="sxs-lookup"><span data-stu-id="c77b3-214"><a id="ReplaceDocument"></a>Step 9: Replace a document</span></span>
<span data-ttu-id="c77b3-215">Azure Cosmos DB поддерживает замену документов JSON.</span><span class="sxs-lookup"><span data-stu-id="c77b3-215">Azure Cosmos DB supports replacing JSON documents.</span></span>

<span data-ttu-id="c77b3-216">Скопируйте и вставьте hello **replaceFamilyDocument** функция под hello **queryCollection** функции в файле в файле app.js hello.</span><span class="sxs-lookup"><span data-stu-id="c77b3-216">Copy and paste hello **replaceFamilyDocument** function underneath hello **queryCollection** function in hello app.js file.</span></span>

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function replaceFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Replacing document:\n${document.id}\n`);
        document.children[0].grade = 6;

        return new Promise((resolve, reject) => {
            client.replaceDocument(documentUrl, document, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="c77b3-217">Скопируйте и вставьте код hello вызова hello слишком**queryCollection** tooexecute hello **replaceDocument** функции.</span><span class="sxs-lookup"><span data-stu-id="c77b3-217">Copy and paste hello code below hello call too**queryCollection** tooexecute hello **replaceDocument** function.</span></span> <span data-ttu-id="c77b3-218">Кроме того, добавьте toocall кода hello **queryCollection** снова tooverify hello документ успешно изменен.</span><span class="sxs-lookup"><span data-stu-id="c77b3-218">Also, add hello code toocall **queryCollection** again tooverify that hello document had successfully changed.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="c77b3-219">Найдите в окне терминала вашей ```app.js``` файл и выполните команду hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="c77b3-219">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="c77b3-220">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="c77b3-220">Congratulations!</span></span> <span data-ttu-id="c77b3-221">Вы успешно заменили документ Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c77b3-221">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="c77b3-222"><a id="DeleteDocument"></a>Шаг 10. Удаление документа</span><span class="sxs-lookup"><span data-stu-id="c77b3-222"><a id="DeleteDocument"></a>Step 10: Delete a document</span></span>
<span data-ttu-id="c77b3-223">Azure Cosmos DB поддерживает удаление документов JSON.</span><span class="sxs-lookup"><span data-stu-id="c77b3-223">Azure Cosmos DB supports deleting JSON documents.</span></span>

<span data-ttu-id="c77b3-224">Скопируйте и вставьте hello **deleteFamilyDocument** функция под hello **replaceFamilyDocument** функции.</span><span class="sxs-lookup"><span data-stu-id="c77b3-224">Copy and paste hello **deleteFamilyDocument** function underneath hello **replaceFamilyDocument** function.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function deleteFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Deleting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.deleteDocument(documentUrl, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="c77b3-225">Скопируйте и вставьте код hello ниже hello вызовов toohello второй **queryCollection** tooexecute hello **deleteDocument** функции.</span><span class="sxs-lookup"><span data-stu-id="c77b3-225">Copy and paste hello code below hello call toohello second **queryCollection** tooexecute hello **deleteDocument** function.</span></span>

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="c77b3-226">Найдите в окне терминала вашей ```app.js``` файл и выполните команду hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="c77b3-226">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="c77b3-227">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="c77b3-227">Congratulations!</span></span> <span data-ttu-id="c77b3-228">Вы успешно удалили документ Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c77b3-228">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="c77b3-229"><a id="DeleteDatabase"></a>Шаг 11: Удалите базу данных узла hello</span><span class="sxs-lookup"><span data-stu-id="c77b3-229"><a id="DeleteDatabase"></a>Step 11: Delete hello Node database</span></span>
<span data-ttu-id="c77b3-230">Идет удаление hello создана база данных приведет к удалению hello базы данных и все дочерние ресурсы (коллекции, документы, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="c77b3-230">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="c77b3-231">Скопируйте и вставьте hello **очистки** функция под hello **deleteFamilyDocument** функции базы данных tooremove hello и все дочерние ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="c77b3-231">Copy and paste hello **cleanup** function underneath hello **deleteFamilyDocument** function tooremove hello database and all hello children resources.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

<span data-ttu-id="c77b3-232">Скопируйте и вставьте код hello вызова hello слишком**deleteFamilyDocument** tooexecute hello **очистки** функции.</span><span class="sxs-lookup"><span data-stu-id="c77b3-232">Copy and paste hello code below hello call too**deleteFamilyDocument** tooexecute hello **cleanup** function.</span></span>

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART tooYOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <span data-ttu-id="c77b3-233"><a id="Run"></a> Шаг 12. Запуск приложения Node.js</span><span class="sxs-lookup"><span data-stu-id="c77b3-233"><a id="Run"></a>Step 12: Run your Node.js application all together!</span></span>
<span data-ttu-id="c77b3-234">В общей сложности для вызова функций hello последовательности должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c77b3-234">Altogether, hello sequence for calling your functions should look like this:</span></span>

    getDatabase()
    .then(() => getCollection())
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    .then(() => cleanup())
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="c77b3-235">Найдите в окне терминала вашей ```app.js``` файл и выполните команду hello:```node app.js```</span><span class="sxs-lookup"><span data-stu-id="c77b3-235">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="c77b3-236">Вы увидите выходные данные get работы приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c77b3-236">You should see hello output of your get started app.</span></span> <span data-ttu-id="c77b3-237">Hello выходные данные должны соответствовать hello пример текста ниже.</span><span class="sxs-lookup"><span data-stu-id="c77b3-237">hello output should match hello example text below.</span></span>

    Getting database:
    FamilyDB

    Getting collection:
    FamilyColl

    Getting document:
    Anderson.1

    Getting document:
    Wakefield.7

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":5,"pets":[{"givenName":"Fluffy"}]}]

    Replacing document:
    Anderson.1

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":6,"pets":[{"givenName":"Fluffy"}]}]

    Deleting document:
    Anderson.1

    Cleaning up by deleting database FamilyDB
    Completed successfully
    Press any key tooexit

<span data-ttu-id="c77b3-238">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="c77b3-238">Congratulations!</span></span> <span data-ttu-id="c77b3-239">Вы создали после завершения Node.js учебника hello и иметь первого приложения консоли Azure Cosmos DB!</span><span class="sxs-lookup"><span data-stu-id="c77b3-239">You've created you've completed hello Node.js tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="c77b3-240"><a id="GetSolution"></a>Получить комплексное решение учебника hello Node.js</span><span class="sxs-lookup"><span data-stu-id="c77b3-240"><a id="GetSolution"></a>Get hello complete Node.js tutorial solution</span></span>
<span data-ttu-id="c77b3-241">Если бы не было времени toocomplete hello шаги в этом учебнике, или просто toodownload hello кода, можно получить его из [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span><span class="sxs-lookup"><span data-stu-id="c77b3-241">If you didn't have time toocomplete hello steps in this tutorial, or just want toodownload hello code, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span>

<span data-ttu-id="c77b3-242">решение GetStarted toorun hello, содержащий все образцы hello в этой статье, вам потребуется hello следующее:</span><span class="sxs-lookup"><span data-stu-id="c77b3-242">toorun hello GetStarted solution that contains all hello samples in this article, you will need hello following:</span></span>

* <span data-ttu-id="c77b3-243">[Учетная запись Azure Cosmos DB][create-account].</span><span class="sxs-lookup"><span data-stu-id="c77b3-243">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="c77b3-244">Hello [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) решения на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="c77b3-244">hello [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="c77b3-245">Установка hello **documentdb** модуль через npm.</span><span class="sxs-lookup"><span data-stu-id="c77b3-245">Install hello **documentdb** module via npm.</span></span> <span data-ttu-id="c77b3-246">Hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c77b3-246">Use hello following command:</span></span>

* ```npm install documentdb --save```

<span data-ttu-id="c77b3-247">Затем в hello ```config.js``` файла обновления hello config.endpoint и config.authKey значений как описано в [шаг 3: задать настройки приложения](#Config).</span><span class="sxs-lookup"><span data-stu-id="c77b3-247">Next, in hello ```config.js``` file, update hello config.endpoint and config.authKey values as described in [Step 3: Set your app's configurations](#Config).</span></span> 

<span data-ttu-id="c77b3-248">В окне терминала найдите вашей ```app.js``` файл и выполните команду hello: ```node app.js```.</span><span class="sxs-lookup"><span data-stu-id="c77b3-248">Then in your terminal, locate your ```app.js``` file and run hello command: ```node app.js```.</span></span>

<span data-ttu-id="c77b3-249">Теперь все готово. Выполните сборку и начинайте работу с решением.</span><span class="sxs-lookup"><span data-stu-id="c77b3-249">That's it, build it and you're on your way!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c77b3-250">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c77b3-250">Next steps</span></span>
* <span data-ttu-id="c77b3-251">Требуется более сложный пример Node.js?</span><span class="sxs-lookup"><span data-stu-id="c77b3-251">Want a more complex Node.js sample?</span></span> <span data-ttu-id="c77b3-252">См. статью о [создании веб-приложения Node.js с использованием Azure Cosmos DB](documentdb-nodejs-application.md).</span><span class="sxs-lookup"><span data-stu-id="c77b3-252">See [Build a Node.js web application using Azure Cosmos DB](documentdb-nodejs-application.md).</span></span>
* <span data-ttu-id="c77b3-253">Узнайте, каким образом слишком[мониторинг учетной записи Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="c77b3-253">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="c77b3-254">Выполнять запросы к нашей образец набора данных в hello [площадку запросов](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="c77b3-254">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="c77b3-255">Дополнительные сведения о модели программирования hello в разделе Разработка hello hello [страницы документации Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="c77b3-255">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
