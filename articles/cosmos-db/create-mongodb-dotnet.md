---
title: "Создание веб-приложения с использованием .NET и API MongoDB в Azure Cosmos DB | Документация Майкрософт"
description: "В этой статье представлен пример кода .NET, который можно использовать для подключения и выполнения запросов к API MongoDB в Azure Cosmos DB."
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
ms.openlocfilehash: 2d30bec75d701b1fd55355d1e139350b6d828c9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-the-azure-portal"></a><span data-ttu-id="1b00d-103">Azure Cosmos DB. Создание веб-приложения API MongoDB с использованием языка .NET и портала Azure</span><span class="sxs-lookup"><span data-stu-id="1b00d-103">Azure Cosmos DB: Build a MongoDB API web app with .NET and the Azure portal</span></span>

<span data-ttu-id="1b00d-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="1b00d-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="1b00d-105">Вы можете быстро создавать и запрашивать документы, пары "ключ — значение" и базы данных графов, используя преимущества возможностей глобального распределения и горизонтального масштабирования Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1b00d-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="1b00d-106">В этом кратком руководстве показано, как создать учетную запись Azure Cosmos DB, базу данных документов и коллекцию с использованием портала Azure.</span><span class="sxs-lookup"><span data-stu-id="1b00d-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="1b00d-107">Затем вы можете развернуть веб-приложение списка задач, созданное на основе [драйвера .NET MongoDB](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span><span class="sxs-lookup"><span data-stu-id="1b00d-107">You'll then build and deploy a tasks list web app built on the [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1b00d-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1b00d-108">Prerequisites</span></span>

<span data-ttu-id="1b00d-109">Если вы еще не установили Visual Studio 2017, вы можете скачать и использовать **бесплатный** [выпуск Community для Visual Studio 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1b00d-109">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="1b00d-110">При установке Visual Studio необходимо включить возможность **разработки для Azure**.</span><span class="sxs-lookup"><span data-stu-id="1b00d-110">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="1b00d-111">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="1b00d-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="1b00d-112">Клонирование примера приложения</span><span class="sxs-lookup"><span data-stu-id="1b00d-112">Clone the sample application</span></span>

<span data-ttu-id="1b00d-113">Теперь необходимо клонировать приложение API MongoDB из GitHub. Задайте строку подключения и выполните ее.</span><span class="sxs-lookup"><span data-stu-id="1b00d-113">Now let's clone a MongoDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="1b00d-114">Вы узнаете, как можно упростить работу с данными программным способом.</span><span class="sxs-lookup"><span data-stu-id="1b00d-114">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="1b00d-115">Откройте окно терминала Git, например Git Bash, и выполните команду `cd`, чтобы перейти в рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="1b00d-115">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="1b00d-116">Выполните команду ниже, чтобы клонировать репозиторий с примером.</span><span class="sxs-lookup"><span data-stu-id="1b00d-116">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. <span data-ttu-id="1b00d-117">Затем откройте файл решения в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1b00d-117">Then open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="1b00d-118">Просмотр кода</span><span class="sxs-lookup"><span data-stu-id="1b00d-118">Review the code</span></span>

<span data-ttu-id="1b00d-119">Сделаем краткий обзор того, что происходит в приложении.</span><span class="sxs-lookup"><span data-stu-id="1b00d-119">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="1b00d-120">Откройте файл **Dal.cs** в каталоге **DAL**, и вы увидите, что эти строки кода создают ресурсы Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1b00d-120">Open the **Dal.cs** file under the **DAL** directory and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="1b00d-121">Инициализация клиента Mongo.</span><span class="sxs-lookup"><span data-stu-id="1b00d-121">Initialize the Mongo Client.</span></span>

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

* <span data-ttu-id="1b00d-122">Получение базы данных и коллекции.</span><span class="sxs-lookup"><span data-stu-id="1b00d-122">Retrieve the database and the collection.</span></span>

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* <span data-ttu-id="1b00d-123">Получение всех документов.</span><span class="sxs-lookup"><span data-stu-id="1b00d-123">Retrieve all documents.</span></span>

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="1b00d-124">Обновление строки подключения</span><span class="sxs-lookup"><span data-stu-id="1b00d-124">Update your connection string</span></span>

<span data-ttu-id="1b00d-125">Теперь вернитесь на портал Azure, чтобы получить данные строки подключения. Скопируйте эти данные в приложение.</span><span class="sxs-lookup"><span data-stu-id="1b00d-125">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="1b00d-126">На [портале Azure](http://portal.azure.com/) перейдите к учетной записи базы данных Azure Cosmos DB и на левой панели навигации щелкните **Строка подключения**, а затем выберите **Ключи записи-чтения**.</span><span class="sxs-lookup"><span data-stu-id="1b00d-126">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Connection String**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="1b00d-127">На следующем шаге используйте кнопку копирования в правой части экрана, чтобы скопировать имя пользователя, пароль и узел в файл Dal.cs.</span><span class="sxs-lookup"><span data-stu-id="1b00d-127">You'll use the copy buttons on the right side of the screen to copy the Username, Password, and Host into the Dal.cs file in the next step.</span></span>

2. <span data-ttu-id="1b00d-128">Откройте файл **Dal.cs** в каталоге **DAL**.</span><span class="sxs-lookup"><span data-stu-id="1b00d-128">Open the **Dal.cs** file in the **DAL** directory.</span></span> 

3. <span data-ttu-id="1b00d-129">Скопируйте **имя пользователя** c портала (с помощью кнопки копирования) и добавьте его в качестве значения параметра **username** в файле **Dal.cs**.</span><span class="sxs-lookup"><span data-stu-id="1b00d-129">Copy your **username** value from the portal (using the copy button) and make it the value of the **username** in your **Dal.cs** file.</span></span> 

4. <span data-ttu-id="1b00d-130">Затем скопируйте значение **узла** с портала и добавьте его в качестве значения параметра **host** в файле **Dal.cs**.</span><span class="sxs-lookup"><span data-stu-id="1b00d-130">Then copy your **host** value from the portal and make it the value of the **host** in your **Dal.cs** file.</span></span> 

5. <span data-ttu-id="1b00d-131">И наконец, скопируйте **пароль** с портала и добавьте его в качестве значения параметра **password** в файле **Dal.cs**.</span><span class="sxs-lookup"><span data-stu-id="1b00d-131">Finally copy your **password** value from the portal and make it the value of the **password** in your **Dal.cs** file.</span></span> 

<span data-ttu-id="1b00d-132">Теперь приложение со всеми сведениями, необходимыми для взаимодействия с Azure Cosmos DB, обновлено.</span><span class="sxs-lookup"><span data-stu-id="1b00d-132">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-the-web-app"></a><span data-ttu-id="1b00d-133">Запуск веб-приложения</span><span class="sxs-lookup"><span data-stu-id="1b00d-133">Run the web app</span></span>

1. <span data-ttu-id="1b00d-134">В Visual Studio в **обозревателе решений** щелкните проект правой кнопкой мыши и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="1b00d-134">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="1b00d-135">В окне NuGet в поле **Обзор** введите *MongoDB.Driver*.</span><span class="sxs-lookup"><span data-stu-id="1b00d-135">In the NuGet **Browse** box, type *MongoDB.Driver*.</span></span>

3. <span data-ttu-id="1b00d-136">В результатах поиска найдите библиотеку **MongoDB.Driver** и установите ее.</span><span class="sxs-lookup"><span data-stu-id="1b00d-136">From the results, install the **MongoDB.Driver** library.</span></span> <span data-ttu-id="1b00d-137">При этом будет установлен пакет MongoDB.Driver, а также все зависимости.</span><span class="sxs-lookup"><span data-stu-id="1b00d-137">This installs the MongoDB.Driver package as well as all dependencies.</span></span>

4. <span data-ttu-id="1b00d-138">Нажмите клавиши CTRL+F5 для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="1b00d-138">Click CTRL + F5 to run the application.</span></span> <span data-ttu-id="1b00d-139">Приложение откроется в браузере.</span><span class="sxs-lookup"><span data-stu-id="1b00d-139">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="1b00d-140">Щелкните **Создать** в браузере и создайте несколько задач в приложении списка задач.</span><span class="sxs-lookup"><span data-stu-id="1b00d-140">Click **Create** in the browser and create a few new tasks in your task list app.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="1b00d-141">Просмотр соглашений об уровне обслуживания на портале Azure</span><span class="sxs-lookup"><span data-stu-id="1b00d-141">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="1b00d-142">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="1b00d-142">Clean up resources</span></span>

<span data-ttu-id="1b00d-143">Если вы не собираетесь использовать это приложение дальше, удалите все ресурсы, созданные в ходе работы с этим руководством, на портале Azure, сделав следующее:</span><span class="sxs-lookup"><span data-stu-id="1b00d-143">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="1b00d-144">В меню слева на портале Azure щелкните **Группы ресурсов**, а затем выберите имя созданного ресурса.</span><span class="sxs-lookup"><span data-stu-id="1b00d-144">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="1b00d-145">На странице группы ресурсов щелкните **Удалить**, в текстовом поле введите имя ресурса для удаления и щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="1b00d-145">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b00d-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1b00d-146">Next steps</span></span>

<span data-ttu-id="1b00d-147">В этом кратком руководстве вы узнали, как создать учетную запись Azure Cosmos DB и запустить веб-приложение, используя API MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1b00d-147">In this quickstart, you've learned how to create an Azure Cosmos DB account and run a web app using the API for MongoDB.</span></span> <span data-ttu-id="1b00d-148">Теперь можно импортировать дополнительные данные в учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1b00d-148">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="1b00d-149">Перенос данных в DocumentDB с помощью mongoimport и mongorestore</span><span class="sxs-lookup"><span data-stu-id="1b00d-149">Import data into Azure Cosmos DB for the MongoDB API</span></span>](mongodb-migrate.md)

