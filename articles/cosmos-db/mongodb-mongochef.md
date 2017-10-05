---
title: "Использование MongoChef c Azure Cosmos DB | Документация Майкрософт"
description: "Узнайте, как использовать MongoChef с учетной записью API для MongoDB в Azure Cosmos DB"
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
ms.openlocfilehash: 54c9799bd646b827f602e2ea2f9a15a4fc853f00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="8b82a-104">Использование MongoChef с учетной записью API для MongoDB в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8b82a-104">Use MongoChef with an Azure Cosmos DB: API for MongoDB account</span></span>

<span data-ttu-id="8b82a-105">Чтобы подключиться к учетной записи API для MongoDB в Azure Cosmos DB, необходимо:</span><span class="sxs-lookup"><span data-stu-id="8b82a-105">To connect to an Azure Cosmos DB: API for MongoDB account, you must:</span></span>

* <span data-ttu-id="8b82a-106">скачать и установить [MongoChef](http://3t.io/mongochef)</span><span class="sxs-lookup"><span data-stu-id="8b82a-106">Download and install [MongoChef](http://3t.io/mongochef)</span></span>
* <span data-ttu-id="8b82a-107">Подготовить сведения о [строке подключения](connect-mongodb-account.md) для учетной записи API для MongoDB в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b82a-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="create-the-connection-in-mongochef"></a><span data-ttu-id="8b82a-108">создать подключение в MongoChef.</span><span class="sxs-lookup"><span data-stu-id="8b82a-108">Create the connection in MongoChef</span></span>
<span data-ttu-id="8b82a-109">Чтобы добавить в диспетчер подключений MongoChef учетную запись API для MongoDB в Azure Cosmos DB, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8b82a-109">To add your Azure Cosmos DB: API for MongoDB account to the MongoChef connection manager, perform the following steps.</span></span>

1. <span data-ttu-id="8b82a-110">Извлеките сведения о подключении API для MongoDB в Azure Cosmos DB. Ознакомьтесь с инструкциями [здесь](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="8b82a-110">Retrieve your Azure Cosmos DB: API for MongoDB connection information using the instructions [here](connect-mongodb-account.md).</span></span>

    ![Снимок экрана, колонка строки подключения](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. <span data-ttu-id="8b82a-112">Щелкните **Connect** (Подключиться), чтобы открыть диспетчер подключений, и нажмите кнопку **New Connection** (Новое подключение).</span><span class="sxs-lookup"><span data-stu-id="8b82a-112">Click **Connect** to open the Connection Manager, then click **New Connection**</span></span>

    ![Снимок экрана диспетчера подключений MongoChef](./media/mongodb-mongochef/ConnectionManager.png)
3. <span data-ttu-id="8b82a-114">В окне **Новое подключение** на вкладке **Сервер** введите узел (полное доменное имя) учетной записи API для MongoDB в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b82a-114">In the **New Connection** window, on the **Server** tab, enter the HOST (FQDN) of the Azure Cosmos DB: API for MongoDB account and the PORT.</span></span>

    ![Снимок экрана диспетчера подключений MongoChef, вкладка серверов](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. <span data-ttu-id="8b82a-116">В окне **New Connection** (Новое подключение) на вкладке **Authentication** (Аутентификация) выберите режим аутентификации **Standard (MONGODB-CR or SCARM-SHA-1)** (Стандартная (MONGODB CR или SCARM-SHA-1)), а также введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="8b82a-116">In the **New Connection** window, on the **Authentication** tab, choose Authentication Mode **Standard (MONGODB-CR or SCARM-SHA-1)** and enter the USERNAME and PASSWORD.</span></span>  <span data-ttu-id="8b82a-117">Подтвердите базу данных по умолчанию для проверки подлинности (admin) или укажите другое значение.</span><span class="sxs-lookup"><span data-stu-id="8b82a-117">Accept the default authentication db (admin) or provide your own value.</span></span>

    ![Снимок экрана диспетчера подключений MongoChef, вкладка проверки подлинности](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. <span data-ttu-id="8b82a-119">В окне **New Connection** (Новое подключение) на вкладке **SSL** установите флажок **Use SSL protocol to connect** (Использовать для подключения протокол SSL) и переключатель **Accept server self-signed SSL certificates** (Принимать самозаверяющие SSL-сертификаты сервера).</span><span class="sxs-lookup"><span data-stu-id="8b82a-119">In the **New Connection** window, on the **SSL** tab, check the **Use SSL protocol to connect** check box and the **Accept server self-signed SSL certificates** radio button.</span></span>

    ![Снимок экрана диспетчера подключений MongoChef, вкладка SSL](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. <span data-ttu-id="8b82a-121">Нажмите кнопку **Test Connection** (Проверить подключение), чтобы проверить сведения о подключении. Затем нажмите кнопку **ОК**, чтобы вернуться в окно "New Connection" (Новое подключение), а затем нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="8b82a-121">Click the **Test Connection** button to validate the connection information, click **OK** to return to the New Connection window, and then click **Save**.</span></span>

    ![Снимок экрана окна тестового подключения MongoChef](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-to-create-a-database-collection-and-documents"></a><span data-ttu-id="8b82a-123">Использование MongoChef для создания базы данных, коллекции и документов</span><span class="sxs-lookup"><span data-stu-id="8b82a-123">Use MongoChef to create a database, collection, and documents</span></span>
<span data-ttu-id="8b82a-124">Чтобы создать базу данных, коллекцию и документы с помощью MongoChef, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8b82a-124">To create a database, collection, and documents using MongoChef, perform the following steps.</span></span>

1. <span data-ttu-id="8b82a-125">В **диспетчере подключений** выделите нужное подключение и щелкните **Connect** (Подключиться).</span><span class="sxs-lookup"><span data-stu-id="8b82a-125">In **Connection Manager**, highlight the connection and click **Connect**.</span></span>

    ![Снимок экрана диспетчера подключений MongoChef](./media/mongodb-mongochef/ConnectToAccount.png)
2. <span data-ttu-id="8b82a-127">Щелкните узел правой кнопкой мыши и выберите **Добавить базу данных**.</span><span class="sxs-lookup"><span data-stu-id="8b82a-127">Right click the host and choose **Add Database**.</span></span>  <span data-ttu-id="8b82a-128">Укажите имя базы данных и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8b82a-128">Provide a database name and click **OK**.</span></span>

    ![Снимок экрана MongoChef, параметр "Добавление базы данных"](./media/mongodb-mongochef/AddDatabase1.png)
3. <span data-ttu-id="8b82a-130">Щелкните правой кнопкой мыши базу данных и выберите **Добавить коллекцию**.</span><span class="sxs-lookup"><span data-stu-id="8b82a-130">Right click the database and choose **Add Collection**.</span></span>  <span data-ttu-id="8b82a-131">Укажите имя коллекции и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8b82a-131">Provide a collection name and click **Create**.</span></span>

    ![Снимок экрана MongoChef, параметр "Добавление коллекции"](./media/mongodb-mongochef/AddCollection.png)
4. <span data-ttu-id="8b82a-133">Щелкните пункт меню **Collection** (Коллекция), затем щелкните **Add Document** (Добавить документ).</span><span class="sxs-lookup"><span data-stu-id="8b82a-133">Click the **Collection** menu item, then click **Add Document**.</span></span>

    ![Снимок экрана MongoChef, элемент меню "Добавление документа"](./media/mongodb-mongochef/AddDocument1.png)
5. <span data-ttu-id="8b82a-135">В диалоговом окне "Добавление документа" вставьте следующий текст и щелкните **Добавить документ**.</span><span class="sxs-lookup"><span data-stu-id="8b82a-135">In the Add Document dialog, paste the following and then click **Add Document**.</span></span>

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
6. <span data-ttu-id="8b82a-136">Добавьте еще один документ со следующим содержимым.</span><span class="sxs-lookup"><span data-stu-id="8b82a-136">Add another document, this time with the following content.</span></span>

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
7. <span data-ttu-id="8b82a-137">Выполните пробный запрос.</span><span class="sxs-lookup"><span data-stu-id="8b82a-137">Execute a sample query.</span></span> <span data-ttu-id="8b82a-138">Например, попробуйте найти семьи с фамилией Andersen и вернуть для них поля parents и state.</span><span class="sxs-lookup"><span data-stu-id="8b82a-138">For example, search for families with the last name 'Andersen' and return the parents and state fields.</span></span>

    ![Снимок экрана Mongo Chef, результаты запроса](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a><span data-ttu-id="8b82a-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8b82a-140">Next steps</span></span>
* <span data-ttu-id="8b82a-141">Ознакомьтесь с [примерами](mongodb-samples.md) API для MongoDB в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8b82a-141">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
