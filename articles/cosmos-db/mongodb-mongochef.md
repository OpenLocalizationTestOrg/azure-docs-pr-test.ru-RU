---
title: "aaaUse MongoChef для Azure Cosmos DB | Документы Microsoft"
description: "Узнайте, как toouse MongoChef с Azure DB Cosmos: API для MongoDB учетной записи"
keywords: MongoChef
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 4b047797b231c34ccc6f2ed02416525c6228d596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="c4a76-104">Использование MongoChef с учетной записью API для MongoDB в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c4a76-104">Use MongoChef with an Azure Cosmos DB: API for MongoDB account</span></span>

<span data-ttu-id="c4a76-105">tooconnect tooan Azure Cosmos DB: API для MongoDB учетной записи, необходимо:</span><span class="sxs-lookup"><span data-stu-id="c4a76-105">tooconnect tooan Azure Cosmos DB: API for MongoDB account, you must:</span></span>

* <span data-ttu-id="c4a76-106">скачать и установить [MongoChef](http://3t.io/mongochef)</span><span class="sxs-lookup"><span data-stu-id="c4a76-106">Download and install [MongoChef](http://3t.io/mongochef)</span></span>
* <span data-ttu-id="c4a76-107">Подготовить сведения о [строке подключения](connect-mongodb-account.md) для учетной записи API для MongoDB в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c4a76-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="create-hello-connection-in-mongochef"></a><span data-ttu-id="c4a76-108">Создание соединения hello в MongoChef</span><span class="sxs-lookup"><span data-stu-id="c4a76-108">Create hello connection in MongoChef</span></span>
<span data-ttu-id="c4a76-109">tooadd Cosmos базы данных Azure: API для MongoDB учетной записи toohello MongoChef диспетчера подключений, выполнения hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="c4a76-109">tooadd your Azure Cosmos DB: API for MongoDB account toohello MongoChef connection manager, perform hello following steps.</span></span>

1. <span data-ttu-id="c4a76-110">Получить Cosmos базы данных Azure: API для MongoDB сведений о соединении с помощью инструкций hello [здесь](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="c4a76-110">Retrieve your Azure Cosmos DB: API for MongoDB connection information using hello instructions [here](connect-mongodb-account.md).</span></span>

    ![Снимок экрана: колонка строка подключения hello](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. <span data-ttu-id="c4a76-112">Нажмите кнопку **Connect** tooopen hello диспетчера соединений, а затем щелкните **нового подключения**</span><span class="sxs-lookup"><span data-stu-id="c4a76-112">Click **Connect** tooopen hello Connection Manager, then click **New Connection**</span></span>

    ![Снимок экрана диспетчера соединений MongoChef hello](./media/mongodb-mongochef/ConnectionManager.png)
3. <span data-ttu-id="c4a76-114">В hello **новое подключение** в hello окна **сервера** введите hello узла (полное доменное имя) hello Azure Cosmos DB: API для учетной записи и hello порта MongoDB.</span><span class="sxs-lookup"><span data-stu-id="c4a76-114">In hello **New Connection** window, on hello **Server** tab, enter hello HOST (FQDN) of hello Azure Cosmos DB: API for MongoDB account and hello PORT.</span></span>

    ![Снимок экрана: вкладка hello MongoChef подключение диспетчера сервера](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. <span data-ttu-id="c4a76-116">В hello **новое подключение** в hello окна **проверки подлинности** выберите режим проверки подлинности **Standard (MONGODB CR или SCARM-SHA-1)** и введите имя пользователя hello и ПАРОЛЬ.</span><span class="sxs-lookup"><span data-stu-id="c4a76-116">In hello **New Connection** window, on hello **Authentication** tab, choose Authentication Mode **Standard (MONGODB-CR or SCARM-SHA-1)** and enter hello USERNAME and PASSWORD.</span></span>  <span data-ttu-id="c4a76-117">Оставьте db проверки подлинности по умолчанию hello (администратор) или введите другое значение.</span><span class="sxs-lookup"><span data-stu-id="c4a76-117">Accept hello default authentication db (admin) or provide your own value.</span></span>

    ![Снимок экрана: вкладка hello MongoChef подключение диспетчер проверки подлинности](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. <span data-ttu-id="c4a76-119">В hello **новое подключение** в hello окна **SSL** проверьте hello **tooconnect протокол SSL используется** флажок и hello **server принимать самозаверяющие SSL Сертификаты** переключатель.</span><span class="sxs-lookup"><span data-stu-id="c4a76-119">In hello **New Connection** window, on hello **SSL** tab, check hello **Use SSL protocol tooconnect** check box and hello **Accept server self-signed SSL certificates** radio button.</span></span>

    ![Снимок экрана MongoChef hello на вкладке SSL диспетчер соединений](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. <span data-ttu-id="c4a76-121">Нажмите кнопку hello **проверить подключение** toovalidate сведения о соединении hello, выберите элемент **ОК** tooreturn toohello новое подключение окна и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c4a76-121">Click hello **Test Connection** button toovalidate hello connection information, click **OK** tooreturn toohello New Connection window, and then click **Save**.</span></span>

    ![Снимок экрана: окно hello MongoChef тестирования подключения](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-toocreate-a-database-collection-and-documents"></a><span data-ttu-id="c4a76-123">Используйте MongoChef toocreate базы данных, коллекции и документов</span><span class="sxs-lookup"><span data-stu-id="c4a76-123">Use MongoChef toocreate a database, collection, and documents</span></span>
<span data-ttu-id="c4a76-124">toocreate базы данных, коллекции и документов с помощью MongoChef, выполнить следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="c4a76-124">toocreate a database, collection, and documents using MongoChef, perform hello following steps.</span></span>

1. <span data-ttu-id="c4a76-125">В **диспетчера соединений**, выделите hello соединения и нажмите кнопку **Connect**.</span><span class="sxs-lookup"><span data-stu-id="c4a76-125">In **Connection Manager**, highlight hello connection and click **Connect**.</span></span>

    ![Снимок экрана диспетчера соединений MongoChef hello](./media/mongodb-mongochef/ConnectToAccount.png)
2. <span data-ttu-id="c4a76-127">Щелкните правой кнопкой мыши узел hello и выберите **добавления базы данных**.</span><span class="sxs-lookup"><span data-stu-id="c4a76-127">Right click hello host and choose **Add Database**.</span></span>  <span data-ttu-id="c4a76-128">Укажите имя базы данных и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c4a76-128">Provide a database name and click **OK**.</span></span>

    ![Снимок экрана: hello параметр MongoChef добавления базы данных](./media/mongodb-mongochef/AddDatabase1.png)
3. <span data-ttu-id="c4a76-130">Щелкните правой кнопкой мыши базу данных hello и выберите **добавить коллекцию**.</span><span class="sxs-lookup"><span data-stu-id="c4a76-130">Right click hello database and choose **Add Collection**.</span></span>  <span data-ttu-id="c4a76-131">Укажите имя коллекции и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c4a76-131">Provide a collection name and click **Create**.</span></span>

    ![Снимок экрана: hello параметр MongoChef добавить коллекцию](./media/mongodb-mongochef/AddCollection.png)
4. <span data-ttu-id="c4a76-133">Нажмите кнопку hello **коллекции** меню элемента, затем щелкните **добавить документ**.</span><span class="sxs-lookup"><span data-stu-id="c4a76-133">Click hello **Collection** menu item, then click **Add Document**.</span></span>

    ![Снимок экрана: hello MongoChef добавить элемент меню](./media/mongodb-mongochef/AddDocument1.png)
5. <span data-ttu-id="c4a76-135">В диалоговом окне Добавить документ hello, вставьте следующую hello и нажмите кнопку **добавить документ**.</span><span class="sxs-lookup"><span data-stu-id="c4a76-135">In hello Add Document dialog, paste hello following and then click **Add Document**.</span></span>

        {
        "_id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
               { "firstName": "Thomas" },
               { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "isRegistered": true
        }
6. <span data-ttu-id="c4a76-136">Добавьте другой документ теперь hello после содержимого.</span><span class="sxs-lookup"><span data-stu-id="c4a76-136">Add another document, this time with hello following content.</span></span>

        {
        "_id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam",
                 "givenName": "Jesse",
                "gender": "female", "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            {
                "familyName": "Miller",
                 "givenName": "Lisa",
                 "gender": "female",
                 "grade": 8 }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
        }
7. <span data-ttu-id="c4a76-137">Выполните пробный запрос.</span><span class="sxs-lookup"><span data-stu-id="c4a76-137">Execute a sample query.</span></span> <span data-ttu-id="c4a76-138">Например поиск семейства с Фамилия «Андерсен» hello и возврата hello родительских элементов, а также состояние поля.</span><span class="sxs-lookup"><span data-stu-id="c4a76-138">For example, search for families with hello last name 'Andersen' and return hello parents and state fields.</span></span>

    ![Снимок экрана Mongo Chef, результаты запроса](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a><span data-ttu-id="c4a76-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c4a76-140">Next steps</span></span>
* <span data-ttu-id="c4a76-141">Ознакомьтесь с [примерами](mongodb-samples.md) API для MongoDB в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c4a76-141">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
