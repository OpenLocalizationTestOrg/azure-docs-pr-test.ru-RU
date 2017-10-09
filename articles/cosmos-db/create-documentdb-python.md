---
title: "Azure Cosmos DB: Сборка приложения с помощью Python и hello DocumentDB API | Документы Microsoft"
description: "Содержит пример кода Python, можно использовать запрос tooand tooconnect hello Azure Cosmos DB DocumentDB API"
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
ms.openlocfilehash: e66965ab493c6ef693e88a3767a401d39e1bde2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-hello-azure-portal"></a><span data-ttu-id="41012-103">Azure Cosmos DB: Создать приложение DocumentDB API с Python и hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="41012-103">Azure Cosmos DB: Build a DocumentDB API app with Python and hello Azure portal</span></span>

<span data-ttu-id="41012-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="41012-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="41012-105">Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД.</span><span class="sxs-lookup"><span data-stu-id="41012-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="41012-106">В этом кратком руководстве показано, как toocreate учетную запись Azure Cosmos DB документа базы данных и коллекцию с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="41012-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="41012-107">Затем постройте и запустите консольное приложение, построенных на hello [DocumentDB Python API](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="41012-107">You then build and run a console app built on hello [DocumentDB Python API](documentdb-sdk-python.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41012-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="41012-108">Prerequisites</span></span>

* <span data-ttu-id="41012-109">Перед запуском этого образца необходимо иметь hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="41012-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
    * <span data-ttu-id="41012-110">[Visual Studio 2015 или более поздней версии.](http://www.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="41012-110">[Visual Studio 2015](http://www.visualstudio.com/) or higher.</span></span>
    * <span data-ttu-id="41012-111">Средства Python для Visual Studio с сайта [GitHub](http://microsoft.github.io/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="41012-111">Python Tools for Visual Studio from [GitHub](http://microsoft.github.io/PTVS/).</span></span> <span data-ttu-id="41012-112">В этом руководстве используются средства Python для VS 2015.</span><span class="sxs-lookup"><span data-stu-id="41012-112">This tutorial uses Python Tools for VS 2015.</span></span>
    * <span data-ttu-id="41012-113">Python 2.7 с сайта [python.org](https://www.python.org/downloads/release/python-2712/).</span><span class="sxs-lookup"><span data-stu-id="41012-113">Python 2.7 from [python.org](https://www.python.org/downloads/release/python-2712/)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="41012-114">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="41012-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="41012-115">Добавление коллекции</span><span class="sxs-lookup"><span data-stu-id="41012-115">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="41012-116">Пример приложения hello клонирования</span><span class="sxs-lookup"><span data-stu-id="41012-116">Clone hello sample application</span></span>

<span data-ttu-id="41012-117">Теперь давайте клонирование DocumentDB API приложений из github, задайте строку подключения hello и запустите его.</span><span class="sxs-lookup"><span data-stu-id="41012-117">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="41012-118">Вы видите, как просто можно toowork с данными программными средствами.</span><span class="sxs-lookup"><span data-stu-id="41012-118">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="41012-119">Откройте окно терминала git, таких как git bash и `cd` tooa рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="41012-119">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="41012-120">Выполнения hello следующая команда репозитории примеров tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="41012-120">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-hello-code"></a><span data-ttu-id="41012-121">Проверка кода hello</span><span class="sxs-lookup"><span data-stu-id="41012-121">Review hello code</span></span>

<span data-ttu-id="41012-122">Убедитесь, что происходит в приложение hello быстро ознакомиться.</span><span class="sxs-lookup"><span data-stu-id="41012-122">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="41012-123">Привет открыть файл DocumentDBGetStarted.py и вы найдете следующие строки кода создать hello Azure Cosmos DB ресурсы.</span><span class="sxs-lookup"><span data-stu-id="41012-123">Open hello DocumentDBGetStarted.py file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 


* <span data-ttu-id="41012-124">Hello DocumentClient инициализируется.</span><span class="sxs-lookup"><span data-stu-id="41012-124">hello DocumentClient is initialized.</span></span>

    ```python
    # Initialize hello Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* <span data-ttu-id="41012-125">Создание базы данных.</span><span class="sxs-lookup"><span data-stu-id="41012-125">A new database is created.</span></span>

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* <span data-ttu-id="41012-126">Создание коллекции.</span><span class="sxs-lookup"><span data-stu-id="41012-126">A new collection is created.</span></span>

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

* <span data-ttu-id="41012-127">Создание нескольких документов.</span><span class="sxs-lookup"><span data-stu-id="41012-127">Some documents are created.</span></span>

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

* <span data-ttu-id="41012-128">Выполнение запросов с помощью SQL</span><span class="sxs-lookup"><span data-stu-id="41012-128">A query is performed using SQL</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="41012-129">Обновление строки подключения</span><span class="sxs-lookup"><span data-stu-id="41012-129">Update your connection string</span></span>

<span data-ttu-id="41012-130">Теперь вернитесь toohello Azure портала tooget данные строки подключения и скопируйте его в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="41012-130">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="41012-131">В hello [портал Azure](http://portal.azure.com/), в вашей Azure Cosmos DB учетной записи, в hello навигации слева щелкните **ключей**и нажмите кнопку **чтения и записи ключей**.</span><span class="sxs-lookup"><span data-stu-id="41012-131">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="41012-132">Кнопки копирования hello будет использоваться на правой стороне hello hello toocopy экрана приветствия URI и первичный ключ в hello `DocumentDBGetStarted.py` файла в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="41012-132">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello `DocumentDBGetStarted.py` file in hello next step.</span></span>

    ![Просмотреть и скопировать ключ доступа в hello портал Azure, ключи колонку](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="41012-134">В открытых hello `DocumentDBGetStarted.py` файла.</span><span class="sxs-lookup"><span data-stu-id="41012-134">In Open hello `DocumentDBGetStarted.py` file.</span></span> 

3. <span data-ttu-id="41012-135">Скопируйте значение URI с портала hello (с использованием "Копировать" hello ") и сделать его hello значение ключа hello конечной точки в `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="41012-135">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in `DocumentDBGetStarted.py`.</span></span> 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="41012-136">Затем скопируйте значение ПЕРВИЧНОГО ключа из портала hello и сделать его значение hello hello `config.MASTERKEY` в `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="41012-136">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello `config.MASTERKEY` in `DocumentDBGetStarted.py`.</span></span> <span data-ttu-id="41012-137">Теперь вы обновили приложения с все hello сведения учетной записи, он должен toocommunicate с Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="41012-137">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-hello-app"></a><span data-ttu-id="41012-138">Выполните приложение hello</span><span class="sxs-lookup"><span data-stu-id="41012-138">Run hello app</span></span>
1. <span data-ttu-id="41012-139">В Visual Studio щелкните правой кнопкой мыши проект hello в **обозревателе решений**, выберите hello текущей среды Python, а затем щелкните правой кнопкой мыши.</span><span class="sxs-lookup"><span data-stu-id="41012-139">In Visual Studio, right-click on hello project in **Solution Explorer**, select hello current Python environment, then right click.</span></span>

2. <span data-ttu-id="41012-140">Выберите "Установить пакет Python...", а затем введите **pydocumentdb**</span><span class="sxs-lookup"><span data-stu-id="41012-140">Select Install Python Package, then type in **pydocumentdb**</span></span>

3. <span data-ttu-id="41012-141">Запустите приложение hello toorun F5.</span><span class="sxs-lookup"><span data-stu-id="41012-141">Run F5 toorun hello application.</span></span> <span data-ttu-id="41012-142">Приложение откроется в браузере.</span><span class="sxs-lookup"><span data-stu-id="41012-142">Your app displays in your browser.</span></span> 

<span data-ttu-id="41012-143">Теперь можно вернуться tooData обозревателя и запроса в разделе, изменения и работать с новые данные.</span><span class="sxs-lookup"><span data-stu-id="41012-143">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="41012-144">Просмотрите соглашений об уровне обслуживания в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="41012-144">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="41012-145">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="41012-145">Clean up resources</span></span>

<span data-ttu-id="41012-146">Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="41012-146">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="41012-147">Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="41012-147">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="41012-148">На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="41012-148">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41012-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="41012-149">Next steps</span></span>

<span data-ttu-id="41012-150">В этом кратком руководстве вы узнали, как создать коллекцию с помощью hello обозреватель данных toocreate учетную запись Azure Cosmos DB и запуск приложения.</span><span class="sxs-lookup"><span data-stu-id="41012-150">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="41012-151">Теперь можно импортировать учетной записи Cosmos DB tooyour дополнительные данные.</span><span class="sxs-lookup"><span data-stu-id="41012-151">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="41012-152">Импорт данных в базе данных Azure Cosmos для hello DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="41012-152">Import data into Azure Cosmos DB for hello DocumentDB API</span></span>](import-data.md)


