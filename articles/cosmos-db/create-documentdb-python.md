---
title: "Azure Cosmos DB. Создание приложения с помощью Python и API DocumentDB | Документация Майкрософт"
description: "В этой статье представлен пример кода Python, который можно использовать для подключения и выполнения запросов к API DocumentDB в Azure Cosmos DB."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 51c11be2-af6d-425f-a86a-39cbfe61da29
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 05/13/2017
ms.author: mimig
ms.openlocfilehash: 08d467ea27484e7d1d07d6c21b2e04b6525fbcd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-the-azure-portal"></a><span data-ttu-id="b656f-103">Azure Cosmos DB. Создание приложения API DocumentDB с помощью Python и портала Azure</span><span class="sxs-lookup"><span data-stu-id="b656f-103">Azure Cosmos DB: Build a DocumentDB API app with Python and the Azure portal</span></span>

<span data-ttu-id="b656f-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="b656f-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="b656f-105">Вы можете быстро создавать и запрашивать документы, пары "ключ — значение" и базы данных графов, используя преимущества возможностей глобального распределения и горизонтального масштабирования Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b656f-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="b656f-106">В этом кратком руководстве показано, как создать учетную запись Azure Cosmos DB, базу данных документов и коллекцию с использованием портала Azure.</span><span class="sxs-lookup"><span data-stu-id="b656f-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="b656f-107">Затем вы создадите и запустите консольное приложение на базе [API для DocumentDB на Python](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="b656f-107">You then build and run a console app built on the [DocumentDB Python API](documentdb-sdk-python.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b656f-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b656f-108">Prerequisites</span></span>

* <span data-ttu-id="b656f-109">Для выполнения этого примера вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="b656f-109">Before you can run this sample, you must have the following prerequisites:</span></span>
    * <span data-ttu-id="b656f-110">[Visual Studio 2015 или более поздней версии.](http://www.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="b656f-110">[Visual Studio 2015](http://www.visualstudio.com/) or higher.</span></span>
    * <span data-ttu-id="b656f-111">Средства Python для Visual Studio с сайта [GitHub](http://microsoft.github.io/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="b656f-111">Python Tools for Visual Studio from [GitHub](http://microsoft.github.io/PTVS/).</span></span> <span data-ttu-id="b656f-112">В этом руководстве используются средства Python для VS 2015.</span><span class="sxs-lookup"><span data-stu-id="b656f-112">This tutorial uses Python Tools for VS 2015.</span></span>
    * <span data-ttu-id="b656f-113">Python 2.7 с сайта [python.org](https://www.python.org/downloads/release/python-2712/).</span><span class="sxs-lookup"><span data-stu-id="b656f-113">Python 2.7 from [python.org](https://www.python.org/downloads/release/python-2712/)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="b656f-114">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="b656f-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="b656f-115">Добавление коллекции</span><span class="sxs-lookup"><span data-stu-id="b656f-115">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="b656f-116">Клонирование примера приложения</span><span class="sxs-lookup"><span data-stu-id="b656f-116">Clone the sample application</span></span>

<span data-ttu-id="b656f-117">Теперь необходимо клонировать приложение API DocumentDB из GitHub. Задайте строку подключения и выполните ее.</span><span class="sxs-lookup"><span data-stu-id="b656f-117">Now let's clone a DocumentDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="b656f-118">Вы узнаете, как можно упростить работу с данными программным способом.</span><span class="sxs-lookup"><span data-stu-id="b656f-118">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="b656f-119">Откройте окно терминала Git, например Git Bash, и выполните команду `cd`, чтобы перейти в рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="b656f-119">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="b656f-120">Выполните команду ниже, чтобы клонировать репозиторий с примером.</span><span class="sxs-lookup"><span data-stu-id="b656f-120">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-the-code"></a><span data-ttu-id="b656f-121">Просмотр кода</span><span class="sxs-lookup"><span data-stu-id="b656f-121">Review the code</span></span>

<span data-ttu-id="b656f-122">Сделаем краткий обзор того, что происходит в приложении.</span><span class="sxs-lookup"><span data-stu-id="b656f-122">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="b656f-123">Откройте файл DocumentDBGetStarted.py, и вы увидите, что эти строки кода создают ресурсы Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b656f-123">Open the DocumentDBGetStarted.py file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 


* <span data-ttu-id="b656f-124">Инициализация экземпляра DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="b656f-124">The DocumentClient is initialized.</span></span>

    ```python
    # Initialize the Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* <span data-ttu-id="b656f-125">Создание базы данных.</span><span class="sxs-lookup"><span data-stu-id="b656f-125">A new database is created.</span></span>

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* <span data-ttu-id="b656f-126">Создание коллекции.</span><span class="sxs-lookup"><span data-stu-id="b656f-126">A new collection is created.</span></span>

    ```python
    # Create collection options
    options = {
        'offerEnableRUPerMinuteThroughput': True,
        'offerVersion': "V2",
        'offerThroughput': 400
    }

    # Create a collection
    collection = client.CreateCollection(db['_self'], { 'id': config['DOCUMENTDB_COLLECTION'] }, options)
    ```

* <span data-ttu-id="b656f-127">Создание нескольких документов.</span><span class="sxs-lookup"><span data-stu-id="b656f-127">Some documents are created.</span></span>

    ```python
    # Create some documents
    document1 = client.CreateDocument(collection['_self'],
        { 
            'id': 'server1',
            'Web Site': 0,
            'Cloud Service': 0,
            'Virtual Machine': 0,
            'name': 'some' 
        })
    ```

* <span data-ttu-id="b656f-128">Выполнение запросов с помощью SQL</span><span class="sxs-lookup"><span data-stu-id="b656f-128">A query is performed using SQL</span></span>

    ```python
    # Query them in SQL
    query = { 'query': 'SELECT * FROM server s' }    
            
    options = {} 
    options['enableCrossPartitionQuery'] = True
    options['maxItemCount'] = 2

    result_iterable = client.QueryDocuments(collection['_self'], query, options)
    results = list(result_iterable);

    print(results)
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="b656f-129">Обновление строки подключения</span><span class="sxs-lookup"><span data-stu-id="b656f-129">Update your connection string</span></span>

<span data-ttu-id="b656f-130">Теперь вернитесь на портал Azure, чтобы получить данные строки подключения. Скопируйте эти данные в приложение.</span><span class="sxs-lookup"><span data-stu-id="b656f-130">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="b656f-131">На [портале Azure](http://portal.azure.com/) перейдите к учетной записи базы данных Azure Cosmos DB и на левой панели навигации щелкните **Ключи**, а затем выберите **Ключи записи-чтения**.</span><span class="sxs-lookup"><span data-stu-id="b656f-131">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="b656f-132">На следующем шаге используйте кнопку копирования в правой части экрана, чтобы скопировать универсальный код ресурса (URI) и первичный ключ в файл `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="b656f-132">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the `DocumentDBGetStarted.py` file in the next step.</span></span>

    ![Просмотр и копирование ключа доступа на портале Azure, колонка "Ключи"](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="b656f-134">Откройте файл `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="b656f-134">In Open the `DocumentDBGetStarted.py` file.</span></span> 

3. <span data-ttu-id="b656f-135">Скопируйте значение универсального кода ресурса (URI) на портале (с помощью кнопки копирования) и добавьте его в качестве значения параметра ключа конечной точки в файле `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="b656f-135">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in `DocumentDBGetStarted.py`.</span></span> 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="b656f-136">Затем скопируйте значение первичного ключа с портала и добавьте его в качестве значения параметра `config.MASTERKEY` в файле `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="b656f-136">Then copy your PRIMARY KEY value from the portal and make it the value of the `config.MASTERKEY` in `DocumentDBGetStarted.py`.</span></span> <span data-ttu-id="b656f-137">Теперь приложение со всеми сведениями, необходимыми для взаимодействия с Azure Cosmos DB, обновлено.</span><span class="sxs-lookup"><span data-stu-id="b656f-137">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-the-app"></a><span data-ttu-id="b656f-138">Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="b656f-138">Run the app</span></span>
1. <span data-ttu-id="b656f-139">В Visual Studio щелкните правой кнопкой мыши проект в **обозревателе решений**, выберите текущую среду Python и щелкните ее правой кнопкой мыши.</span><span class="sxs-lookup"><span data-stu-id="b656f-139">In Visual Studio, right-click on the project in **Solution Explorer**, select the current Python environment, then right click.</span></span>

2. <span data-ttu-id="b656f-140">Выберите "Установить пакет Python...", а затем введите **pydocumentdb**</span><span class="sxs-lookup"><span data-stu-id="b656f-140">Select Install Python Package, then type in **pydocumentdb**</span></span>

3. <span data-ttu-id="b656f-141">Нажмите клавишу F5 для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="b656f-141">Run F5 to run the application.</span></span> <span data-ttu-id="b656f-142">Приложение откроется в браузере.</span><span class="sxs-lookup"><span data-stu-id="b656f-142">Your app displays in your browser.</span></span> 

<span data-ttu-id="b656f-143">Вернитесь в обозреватель данных, где вы можете просматривать, запрашивать и изменять новые данные, а также работать с ними.</span><span class="sxs-lookup"><span data-stu-id="b656f-143">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="b656f-144">Просмотр соглашений об уровне обслуживания на портале Azure</span><span class="sxs-lookup"><span data-stu-id="b656f-144">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="b656f-145">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="b656f-145">Clean up resources</span></span>

<span data-ttu-id="b656f-146">Если вы не собираетесь использовать это приложение дальше, удалите все ресурсы, созданные в ходе работы с этим руководством, на портале Azure, сделав следующее:</span><span class="sxs-lookup"><span data-stu-id="b656f-146">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="b656f-147">В меню слева на портале Azure щелкните **Группы ресурсов**, а затем выберите имя созданного ресурса.</span><span class="sxs-lookup"><span data-stu-id="b656f-147">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="b656f-148">На странице группы ресурсов щелкните **Удалить**, в текстовом поле введите имя ресурса для удаления и щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="b656f-148">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b656f-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b656f-149">Next steps</span></span>

<span data-ttu-id="b656f-150">В этом кратком руководстве вы узнали, как создать учетную запись Azure Cosmos DB, коллекцию с помощью обозревателя данных, а также как запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="b656f-150">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run an app.</span></span> <span data-ttu-id="b656f-151">Теперь можно импортировать дополнительные данные в учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b656f-151">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="b656f-152">Импорт данных в DocumentDB с помощью средства миграции базы данных</span><span class="sxs-lookup"><span data-stu-id="b656f-152">Import data into Azure Cosmos DB for the DocumentDB API</span></span>](import-data.md)


