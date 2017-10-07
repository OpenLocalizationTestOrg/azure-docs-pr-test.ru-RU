---
title: "Azure Cosmos DB: Построение веб-приложения с помощью .NET и hello MongoDB API | Документы Microsoft"
description: "Содержит образец кода .NET можно использовать запрос tooand tooconnect hello Azure Cosmos базы данных MongoDB API"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: c85cc47f772a19aaa7181611b75a8acaedbc4c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-hello-azure-portal"></a><span data-ttu-id="e2215-103">Azure Cosmos DB: Построение MongoDB API веб-приложения с помощью .NET и hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="e2215-103">Azure Cosmos DB: Build a MongoDB API web app with .NET and hello Azure portal</span></span>

<span data-ttu-id="e2215-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="e2215-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="e2215-105">Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД.</span><span class="sxs-lookup"><span data-stu-id="e2215-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="e2215-106">В этом кратком руководстве показано, как toocreate учетную запись Azure Cosmos DB документа базы данных и коллекцию с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e2215-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="e2215-107">Затем будет построение и развертывание веб-приложения списка задач, построенные на hello [драйвер MongoDB .NET](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span><span class="sxs-lookup"><span data-stu-id="e2215-107">You'll then build and deploy a tasks list web app built on hello [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e2215-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e2215-108">Prerequisites</span></span>

<span data-ttu-id="e2215-109">Если у вас еще нет Visual Studio 2017 г. установлен, можно загрузить и использовать hello **свободного** [2017 г. Visual Studio Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e2215-109">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="e2215-110">Убедитесь, что включен **разработки Azure** во время установки Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="e2215-110">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="e2215-111">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="e2215-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="e2215-112">Пример приложения hello клонирования</span><span class="sxs-lookup"><span data-stu-id="e2215-112">Clone hello sample application</span></span>

<span data-ttu-id="e2215-113">Теперь давайте клонирование MongoDB API приложений из github, задайте строку подключения hello и запустите его.</span><span class="sxs-lookup"><span data-stu-id="e2215-113">Now let's clone a MongoDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="e2215-114">Вы увидите, как просто можно toowork с данными программными средствами.</span><span class="sxs-lookup"><span data-stu-id="e2215-114">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="e2215-115">Откройте окно терминала git, таких как git bash и `cd` tooa рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="e2215-115">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="e2215-116">Выполнения hello следующая команда репозитории примеров tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="e2215-116">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. <span data-ttu-id="e2215-117">Затем откройте файл решения hello в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e2215-117">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="e2215-118">Проверка кода hello</span><span class="sxs-lookup"><span data-stu-id="e2215-118">Review hello code</span></span>

<span data-ttu-id="e2215-119">Убедитесь, что происходит в приложение hello быстро ознакомиться.</span><span class="sxs-lookup"><span data-stu-id="e2215-119">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="e2215-120">Откройте hello **Dal.cs** файл в папке hello **DAL** каталог и вы найдете следующие строки кода создать hello Azure Cosmos DB ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e2215-120">Open hello **Dal.cs** file under hello **DAL** directory and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="e2215-121">Инициализируйте hello Mongo клиента.</span><span class="sxs-lookup"><span data-stu-id="e2215-121">Initialize hello Mongo Client.</span></span>

    ```cs
        MongoClientSettings settings = new MongoClientSettings();
        settings.Server = new MongoServerAddress(host, 10255);
        settings.UseSsl = true;
        settings.SslSettings = new SslSettings();
        settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;

        MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
        MongoIdentityEvidence evidence = new PasswordEvidence(password);

        settings.Credentials = new List<MongoCredential>()
        {
            new MongoCredential("SCRAM-SHA-1", identity, evidence)
        };

        MongoClient client = new MongoClient(settings);
    ```

* <span data-ttu-id="e2215-122">Получить hello базу данных и коллекцию hello.</span><span class="sxs-lookup"><span data-stu-id="e2215-122">Retrieve hello database and hello collection.</span></span>

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* <span data-ttu-id="e2215-123">Получение всех документов.</span><span class="sxs-lookup"><span data-stu-id="e2215-123">Retrieve all documents.</span></span>

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="e2215-124">Обновление строки подключения</span><span class="sxs-lookup"><span data-stu-id="e2215-124">Update your connection string</span></span>

<span data-ttu-id="e2215-125">Теперь вернитесь toohello Azure портала tooget данные строки подключения и скопируйте его в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="e2215-125">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="e2215-126">В hello [портал Azure](http://portal.azure.com/), в вашей Azure Cosmos DB учетной записи, в hello навигации слева щелкните **строка подключения**и нажмите кнопку **чтения и записи ключей**.</span><span class="sxs-lookup"><span data-stu-id="e2215-126">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Connection String**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="e2215-127">В файл Dal.cs hello в hello следующим шагом будет использоваться кнопки копия hello hello правой части hello toocopy экрана приветствия имя пользователя, пароль и узла.</span><span class="sxs-lookup"><span data-stu-id="e2215-127">You'll use hello copy buttons on hello right side of hello screen toocopy hello Username, Password, and Host into hello Dal.cs file in hello next step.</span></span>

2. <span data-ttu-id="e2215-128">Откройте hello **Dal.cs** файла в hello **DAL** каталога.</span><span class="sxs-lookup"><span data-stu-id="e2215-128">Open hello **Dal.cs** file in hello **DAL** directory.</span></span> 

3. <span data-ttu-id="e2215-129">Копировать вашей **имя пользователя** из портала hello (с использованием "Копировать" hello ") и сделать его hello значение hello **username** в вашей **Dal.cs** файла.</span><span class="sxs-lookup"><span data-stu-id="e2215-129">Copy your **username** value from hello portal (using hello copy button) and make it hello value of hello **username** in your **Dal.cs** file.</span></span> 

4. <span data-ttu-id="e2215-130">Затем скопируйте вашей **узла** из портала hello и сделать его hello значение hello **узла** в ваш **Dal.cs** файла.</span><span class="sxs-lookup"><span data-stu-id="e2215-130">Then copy your **host** value from hello portal and make it hello value of hello **host** in your **Dal.cs** file.</span></span> 

5. <span data-ttu-id="e2215-131">Наконец, скопируйте вашей **пароль** из портала hello и сделать его hello значение hello **пароль** в вашей **Dal.cs** файла.</span><span class="sxs-lookup"><span data-stu-id="e2215-131">Finally copy your **password** value from hello portal and make it hello value of hello **password** in your **Dal.cs** file.</span></span> 

<span data-ttu-id="e2215-132">Теперь вы обновили приложения с все hello сведения учетной записи, он должен toocommunicate с Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e2215-132">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-web-app"></a><span data-ttu-id="e2215-133">Запустите веб-приложение hello</span><span class="sxs-lookup"><span data-stu-id="e2215-133">Run hello web app</span></span>

1. <span data-ttu-id="e2215-134">В Visual Studio щелкните правой кнопкой мыши проект hello в **обозревателе решений** и нажмите кнопку **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e2215-134">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="e2215-135">В hello NuGet **Обзор** введите *MongoDB.Driver*.</span><span class="sxs-lookup"><span data-stu-id="e2215-135">In hello NuGet **Browse** box, type *MongoDB.Driver*.</span></span>

3. <span data-ttu-id="e2215-136">На основе результатов hello установить hello **MongoDB.Driver** библиотеки.</span><span class="sxs-lookup"><span data-stu-id="e2215-136">From hello results, install hello **MongoDB.Driver** library.</span></span> <span data-ttu-id="e2215-137">При этом устанавливаются hello MongoDB.Driver пакета, а также все зависимости.</span><span class="sxs-lookup"><span data-stu-id="e2215-137">This installs hello MongoDB.Driver package as well as all dependencies.</span></span>

4. <span data-ttu-id="e2215-138">Нажмите сочетание клавиш CTRL + F5 toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e2215-138">Click CTRL + F5 toorun hello application.</span></span> <span data-ttu-id="e2215-139">Приложение откроется в браузере.</span><span class="sxs-lookup"><span data-stu-id="e2215-139">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="e2215-140">Нажмите кнопку **создать** в hello браузера и создать несколько новых задач в приложение списка задач.</span><span class="sxs-lookup"><span data-stu-id="e2215-140">Click **Create** in hello browser and create a few new tasks in your task list app.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="e2215-141">Просмотрите соглашений об уровне обслуживания в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="e2215-141">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="e2215-142">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="e2215-142">Clean up resources</span></span>

<span data-ttu-id="e2215-143">Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="e2215-143">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="e2215-144">Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="e2215-144">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="e2215-145">На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="e2215-145">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2215-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e2215-146">Next steps</span></span>

<span data-ttu-id="e2215-147">В этом кратком руководстве вы узнали, как учетную запись Azure Cosmos DB toocreate и выполнения веб-приложения с использованием hello API для MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e2215-147">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and run a web app using hello API for MongoDB.</span></span> <span data-ttu-id="e2215-148">Теперь можно импортировать учетной записи Cosmos DB tooyour дополнительные данные.</span><span class="sxs-lookup"><span data-stu-id="e2215-148">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="e2215-149">Импорт данных в базе данных Azure Cosmos для hello MongoDB API</span><span class="sxs-lookup"><span data-stu-id="e2215-149">Import data into Azure Cosmos DB for hello MongoDB API</span></span>](mongodb-migrate.md)

