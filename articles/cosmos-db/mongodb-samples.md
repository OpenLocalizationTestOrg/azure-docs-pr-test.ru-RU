---
title: "aaaUse toobuild MongoDB API-интерфейсы Azure Cosmos DB приложение | Документы Microsoft"
description: "Учебник, который создает базу данных доступной с помощью API-интерфейсы DB Cosmos Azure hello для MongoDB."
keywords: "примеры mongodb"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: fb38bc53-3561-487d-9e03-20f232319a87
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: anhoh
ms.openlocfilehash: 09be4362fe3aac02e0163325f958210be9598383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-azure-cosmos-db-api-for-mongodb-app-using-nodejs"></a><span data-ttu-id="8b67c-104">Создание приложения API для MongoDB в Azure Cosmos DB с помощью Node.js</span><span class="sxs-lookup"><span data-stu-id="8b67c-104">Build an Azure Cosmos DB: API for MongoDB app using Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8b67c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="8b67c-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="8b67c-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="8b67c-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="8b67c-107">Java</span><span class="sxs-lookup"><span data-stu-id="8b67c-107">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="8b67c-108">Node.js для MongoDB</span><span class="sxs-lookup"><span data-stu-id="8b67c-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="8b67c-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="8b67c-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="8b67c-110">C++</span><span class="sxs-lookup"><span data-stu-id="8b67c-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
>

<span data-ttu-id="8b67c-111">В этом примере показано, как toobuild DB Cosmos Azure: API для MongoDB консольного приложения с помощью Node.js.</span><span class="sxs-lookup"><span data-stu-id="8b67c-111">This example shows you how toobuild an Azure Cosmos DB: API for MongoDB console app using Node.js.</span></span>

<span data-ttu-id="8b67c-112">toouse в этом примере вы должны:</span><span class="sxs-lookup"><span data-stu-id="8b67c-112">toouse this example, you must:</span></span>

* <span data-ttu-id="8b67c-113">[Создание](create-mongodb-dotnet.md#create-account) приложения API для MongoDB в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b67c-113">[Create](create-mongodb-dotnet.md#create-account) an Azure Cosmos DB: API for MongoDB account.</span></span>
* <span data-ttu-id="8b67c-114">Получить сведения о [строке подключения](connect-mongodb-account.md) MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8b67c-114">Retrieve your MongoDB [connection string](connect-mongodb-account.md) information.</span></span>

## <a name="create-hello-app"></a><span data-ttu-id="8b67c-115">Создание приложения hello</span><span class="sxs-lookup"><span data-stu-id="8b67c-115">Create hello app</span></span>

1. <span data-ttu-id="8b67c-116">Создание *в файле app.js* файл и скопируйте и вставьте приведенный ниже код hello.</span><span class="sxs-lookup"><span data-stu-id="8b67c-116">Create a *app.js* file and copy & paste hello code below.</span></span>

    ```nodejs
    var MongoClient = require('mongodb').MongoClient;
    var assert = require('assert');
    var ObjectId = require('mongodb').ObjectID;
    var url = 'mongodb://<endpoint>:<password>@<endpoint>.documents.azure.com:10255/?ssl=true';

    var insertDocument = function(db, callback) {
    db.collection('families').insertOne( {
            "id": "AndersenFamily",
            "lastName": "Andersen",
            "parents": [
                { "firstName": "Thomas" },
                { "firstName": "Mary Kay" }
            ],
            "children": [
                { "firstName": "John", "gender": "male", "grade": 7 }
            ],
            "pets": [
                { "givenName": "Fluffy" }
            ],
            "address": { "country": "USA", "state": "WA", "city": "Seattle" }
        }, function(err, result) {
        assert.equal(err, null);
        console.log("Inserted a document into hello families collection.");
        callback();
    });
    };
    
    var findFamilies = function(db, callback) {
    var cursor =db.collection('families').find( );
    cursor.each(function(err, doc) {
        assert.equal(err, null);
        if (doc != null) {
            console.dir(doc);
        } else {
            callback();
        }
    });
    };
    
    var updateFamilies = function(db, callback) {
    db.collection('families').updateOne(
        { "lastName" : "Andersen" },
        {
            $set: { "pets": [
                { "givenName": "Fluffy" },
                { "givenName": "Rocky"}
            ] },
            $currentDate: { "lastModified": true }
        }, function(err, results) {
        console.log(results);
        callback();
    });
    };
    
    var removeFamilies = function(db, callback) {
    db.collection('families').deleteMany(
        { "lastName": "Andersen" },
        function(err, results) {
            console.log(results);
            callback();
        }
    );
    };
    
    MongoClient.connect(url, function(err, db) {
    assert.equal(null, err);
    insertDocument(db, function() {
        findFamilies(db, function() {
        updateFamilies(db, function() {
            removeFamilies(db, function() {
                db.close();
            });
        });
        });
    });
    });
    ```

2. <span data-ttu-id="8b67c-117">Измените следующие переменные в hello hello *в файле app.js* файл на параметры учетной записи (Дополнительные сведения как toofind вашей [строка подключения](connect-mongodb-account.md)):</span><span class="sxs-lookup"><span data-stu-id="8b67c-117">Modify hello following variables in hello *app.js* file per your account settings (Learn how toofind your [connection string](connect-mongodb-account.md)):</span></span>
   
    ```nodejs
    var url = 'mongodb://<endpoint>:<password>@<endpoint>.documents.azure.com:10255/?ssl=true';
    ```
     
3. <span data-ttu-id="8b67c-118">Откройте удобный для вас терминал, выполните команду **npm install mongodb --save**, а затем запустите приложение с помощью **node app.js**.</span><span class="sxs-lookup"><span data-stu-id="8b67c-118">Open your favorite terminal, run **npm install mongodb --save**, then run your app with **node app.js**</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b67c-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8b67c-119">Next steps</span></span>
* <span data-ttu-id="8b67c-120">Узнайте, каким образом слишком[использовать MongoChef](mongodb-mongochef.md) с Cosmos базы данных Azure: API для учетной записи MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8b67c-120">Learn how too[use MongoChef](mongodb-mongochef.md) with your Azure Cosmos DB: API for MongoDB account.</span></span>
