---
title: "Azure Cosmos DB. Создание веб-приложения с проверкой подлинности Xamarin и Facebook | Документация Майкрософт"
description: "Содержит образец кода .NET можно использовать tooconnect tooand запросов Azure Cosmos DB"
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
ms.openlocfilehash: 5f71dddd2b2f5bd117e481c96c17915fc58d2119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a><span data-ttu-id="9fc70-103">Azure Cosmos DB. Создание веб-приложения с проверкой подлинности .NET, Xamarin и Facebook</span><span class="sxs-lookup"><span data-stu-id="9fc70-103">Azure Cosmos DB: Build a web app with .NET, Xamarin, and Facebook authentication</span></span>

<span data-ttu-id="9fc70-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="9fc70-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="9fc70-105">Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД.</span><span class="sxs-lookup"><span data-stu-id="9fc70-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="9fc70-106">В этом кратком руководстве показано, как toocreate учетную запись Azure Cosmos DB документа базы данных и коллекцию с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9fc70-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="9fc70-107">Затем будет построения и развертывания веб-приложения todo список лежит hello [API .NET для DocumentDB](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/)и hello Azure Cosmos авторизации СУБД.</span><span class="sxs-lookup"><span data-stu-id="9fc70-107">You'll then build and deploy a todo list web app built on hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/), and hello Azure Cosmos DB authorization engine.</span></span> <span data-ttu-id="9fc70-108">Hello todo список веб-приложение реализует шаблон данных пользователя, который позволяет toologin пользователей с помощью проверки подлинности Facebook и управлять toodo элементами.</span><span class="sxs-lookup"><span data-stu-id="9fc70-108">hello todo list web app implements a per-user data pattern that enables users toologin using Facebook Auth and manage their own toodo items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fc70-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9fc70-109">Prerequisites</span></span>

<span data-ttu-id="9fc70-110">Если у вас еще нет Visual Studio 2017 г. установлен, можно загрузить и использовать hello **свободного** [2017 г. Visual Studio Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9fc70-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="9fc70-111">Убедитесь, что включен **разработки Azure** во время установки Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="9fc70-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="9fc70-112">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="9fc70-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="9fc70-113">Добавление коллекции</span><span class="sxs-lookup"><span data-stu-id="9fc70-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="9fc70-114">Пример приложения hello клонирования</span><span class="sxs-lookup"><span data-stu-id="9fc70-114">Clone hello sample application</span></span>

<span data-ttu-id="9fc70-115">Теперь давайте клонирование DocumentDB API приложений из github, задайте строку подключения hello и запустите его.</span><span class="sxs-lookup"><span data-stu-id="9fc70-115">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="9fc70-116">Вы увидите, как просто можно toowork с данными программными средствами.</span><span class="sxs-lookup"><span data-stu-id="9fc70-116">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="9fc70-117">Откройте окно терминала git, таких как git bash и `cd` tooa рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="9fc70-117">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="9fc70-118">Выполнения hello следующая команда репозитории примеров tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="9fc70-118">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. <span data-ttu-id="9fc70-119">Затем откройте файл DocumentDBTodo.sln hello из папки samples/xamarin/UserItems/xamarin.forms hello в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9fc70-119">Then open hello DocumentDBTodo.sln file from hello samples/xamarin/UserItems/xamarin.forms folder in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="9fc70-120">Проверка кода hello</span><span class="sxs-lookup"><span data-stu-id="9fc70-120">Review hello code</span></span>

<span data-ttu-id="9fc70-121">Код Hello в папке Xamarin hello содержит:</span><span class="sxs-lookup"><span data-stu-id="9fc70-121">hello code in hello Xamarin folder contains:</span></span>

* <span data-ttu-id="9fc70-122">Приложение Xamarin.</span><span class="sxs-lookup"><span data-stu-id="9fc70-122">Xamarin app.</span></span> <span data-ttu-id="9fc70-123">приложение Hello сохраняет элементов todo пользователя hello в секционированную коллекцию с именем UserItems.</span><span class="sxs-lookup"><span data-stu-id="9fc70-123">hello app stores hello user's todo items in a partitioned collection named UserItems.</span></span>
* <span data-ttu-id="9fc70-124">Брокер маркера ресурса API.</span><span class="sxs-lookup"><span data-stu-id="9fc70-124">Resource token broker API.</span></span> <span data-ttu-id="9fc70-125">Простой веб-API ASP.NET toobroker ресурс Azure Cosmos DB маркеры toohello вход пользователей приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9fc70-125">A simple ASP.NET Web API toobroker Azure Cosmos DB resource tokens toohello logged in users of hello app.</span></span> <span data-ttu-id="9fc70-126">Маркеры ресурсов — маркеры доступа короткоживущими, предоставить приложение hello toohello доступа hello в данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="9fc70-126">Resource tokens are short-lived access tokens that provide hello app with hello access toohello logged in user's data.</span></span>

<span data-ttu-id="9fc70-127">в приведенной ниже схеме hello проиллюстрирован Hello проверки подлинности и потоки данных.</span><span class="sxs-lookup"><span data-stu-id="9fc70-127">hello authentication and data flow is illustrated in hello diagram below.</span></span>

* <span data-ttu-id="9fc70-128">Hello UserItems сбора создается с ключом секции hello "и ИД пользователя".</span><span class="sxs-lookup"><span data-stu-id="9fc70-128">hello UserItems collection is created with hello partition key '/userid'.</span></span> <span data-ttu-id="9fc70-129">Указание ключа секции для коллекции позволяет Azure Cosmos DB tooscale бесконечно hello количества пользователей и элементов возрастает.</span><span class="sxs-lookup"><span data-stu-id="9fc70-129">Specifying a partition key for a collection allows Azure Cosmos DB tooscale infinitely as hello number of users and items grows.</span></span>
* <span data-ttu-id="9fc70-130">приложение Xamarin Hello позволяет toologin пользователей с учетными данными с Facebook.</span><span class="sxs-lookup"><span data-stu-id="9fc70-130">hello Xamarin app allows users toologin with Facebook credentials.</span></span>
* <span data-ttu-id="9fc70-131">приложение Xamarin Hello использует tooauthenticate маркера доступа Facebook с ResourceTokenBroker API</span><span class="sxs-lookup"><span data-stu-id="9fc70-131">hello Xamarin app uses Facebook access token tooauthenticate with ResourceTokenBroker API</span></span>
* <span data-ttu-id="9fc70-132">broker маркера ресурсов Hello API выполняет проверку подлинности с помощью функции проверки подлинности службы приложения запроса hello и запрашивает маркер ресурсов Azure Cosmos DB с документами tooall доступа чтения и записи, прошедший проверку пользователь hello ключ раздела для управления доступом.</span><span class="sxs-lookup"><span data-stu-id="9fc70-132">hello resource token broker API authenticates hello request using App Service Auth feature, and requests an Azure Cosmos DB resource token with read/write access tooall documents sharing hello authenticated user's partition key.</span></span>
* <span data-ttu-id="9fc70-133">Broker маркера ресурсов возвращает hello ресурсов маркера toohello клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="9fc70-133">Resource token broker returns hello resource token toohello client app.</span></span>
* <span data-ttu-id="9fc70-134">приложение Hello обращается к элементов todo пользователя hello, с помощью маркера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="9fc70-134">hello app accesses hello user's todo items using hello resource token.</span></span>

![Приложение со списком задач с демонстрационными данными](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a><span data-ttu-id="9fc70-136">Обновление строки подключения</span><span class="sxs-lookup"><span data-stu-id="9fc70-136">Update your connection string</span></span>

<span data-ttu-id="9fc70-137">Теперь вернитесь toohello Azure портала tooget данные строки подключения и скопируйте его в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="9fc70-137">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="9fc70-138">В hello [портал Azure](http://portal.azure.com/), в вашей Azure Cosmos DB учетной записи, в hello навигации слева щелкните **ключей**и нажмите кнопку **чтения и записи ключей**.</span><span class="sxs-lookup"><span data-stu-id="9fc70-138">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="9fc70-139">Вы будете использовать кнопки копия hello hello правой части hello toocopy экрана приветствия URI и первичный ключ в файл Web.config hello в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="9fc70-139">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello Web.config file in hello next step.</span></span>

    ![Просмотреть и скопировать ключ доступа в hello портал Azure, ключи колонку](./media/create-documentdb-xamarin-dotnet/keys.png)

2. <span data-ttu-id="9fc70-141">В Visual Studio 2017 г. Откройте файл Web.config hello в папке azure-documentdb-dotnet/образцы/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker hello.</span><span class="sxs-lookup"><span data-stu-id="9fc70-141">In Visual Studio 2017, open hello Web.config file in hello azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker folder.</span></span> 

3. <span data-ttu-id="9fc70-142">Скопируйте значение URI с портала hello (с использованием "Копировать" hello ") и сделать его hello значение accountUrl hello в файле Web.config.</span><span class="sxs-lookup"><span data-stu-id="9fc70-142">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello accountUrl in Web.config.</span></span> 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. <span data-ttu-id="9fc70-143">Затем скопируйте значение ПЕРВИЧНОГО ключа из портала hello и сделать его значение accountKey hello в Web.congif hello.</span><span class="sxs-lookup"><span data-stu-id="9fc70-143">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello accountKey in Web.congif.</span></span> 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

<span data-ttu-id="9fc70-144">Теперь вы обновили приложения с все hello сведения учетной записи, он должен toocommunicate с Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9fc70-144">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="build-and-deploy-hello-web-app"></a><span data-ttu-id="9fc70-145">Построение и развертывание веб-приложения hello</span><span class="sxs-lookup"><span data-stu-id="9fc70-145">Build and deploy hello web app</span></span>

1. <span data-ttu-id="9fc70-146">В hello портал Azure создают службы приложений веб-сайта toohost hello ресурсов маркера broker API.</span><span class="sxs-lookup"><span data-stu-id="9fc70-146">In hello Azure portal, create an App Service website toohost hello Resource token broker API.</span></span>
2. <span data-ttu-id="9fc70-147">Hello портал Azure откройте колонку параметров приложения hello брокера маркера ресурсов hello API веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="9fc70-147">In hello Azure portal, open hello App Settings blade of hello Resource token broker API website.</span></span> <span data-ttu-id="9fc70-148">Заполните следующие параметры приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9fc70-148">Fill in hello following app settings:</span></span>

    * <span data-ttu-id="9fc70-149">accountUrl - URL-адрес учетной записи Azure Cosmos DB hello hello вкладки ключи учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9fc70-149">accountUrl - hello Azure Cosmos DB account URL from hello Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="9fc70-150">accountKey - hello Azure Cosmos DB учетной записи главного ключа из hello вкладка ключей учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9fc70-150">accountKey - hello Azure Cosmos DB account master key from hello Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="9fc70-151">databaseId и collectionId созданной базы данных и коллекции.</span><span class="sxs-lookup"><span data-stu-id="9fc70-151">databaseId and collectionId of your created database and collection</span></span>

3. <span data-ttu-id="9fc70-152">Опубликуйте hello tooyour ResourceTokenBroker решения, созданные веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="9fc70-152">Publish hello ResourceTokenBroker solution tooyour created website.</span></span>

4. <span data-ttu-id="9fc70-153">Откройте проект Xamarin hello и перейдите tooTodoItemManager.cs.</span><span class="sxs-lookup"><span data-stu-id="9fc70-153">Open hello Xamarin project, and navigate tooTodoItemManager.cs.</span></span> <span data-ttu-id="9fc70-154">Заполните значения hello accountURL, collectionId, databaseId, а также resourceTokenBrokerURL hello базовый https URL-адрес веб-сайта маркера broker hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9fc70-154">Fill in hello values for accountURL, collectionId, databaseId, as well as resourceTokenBrokerURL as hello base https url for hello resource token broker website.</span></span>

5. <span data-ttu-id="9fc70-155">Полный hello [как tooconfigure имени входа Facebook toouse приложения службы приложений](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) учебника toosetup проверки подлинности Facebook и настроить веб-сайт ResourceTokenBroker hello.</span><span class="sxs-lookup"><span data-stu-id="9fc70-155">Complete hello [How tooconfigure your App Service application toouse Facebook login](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) tutorial toosetup Facebook authentication and configure hello ResourceTokenBroker website.</span></span>

    <span data-ttu-id="9fc70-156">Запустите приложение Xamarin hello.</span><span class="sxs-lookup"><span data-stu-id="9fc70-156">Run hello Xamarin app.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="9fc70-157">Просмотрите соглашений об уровне обслуживания в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="9fc70-157">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="9fc70-158">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="9fc70-158">Clean up resources</span></span>

<span data-ttu-id="9fc70-159">Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="9fc70-159">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="9fc70-160">Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя только что созданный ресурс hello hello.</span><span class="sxs-lookup"><span data-stu-id="9fc70-160">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you just created.</span></span> 
2. <span data-ttu-id="9fc70-161">На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="9fc70-161">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fc70-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9fc70-162">Next steps</span></span>

<span data-ttu-id="9fc70-163">В этом кратком руководстве вы узнали, как toocreate учетную запись Azure Cosmos DB, создайте коллекцию, с помощью hello обозреватель данных и построение приложения Xamarin.</span><span class="sxs-lookup"><span data-stu-id="9fc70-163">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and build and deploy a Xamarin app.</span></span> <span data-ttu-id="9fc70-164">Теперь можно импортировать учетной записи Cosmos DB tooyour дополнительные данные.</span><span class="sxs-lookup"><span data-stu-id="9fc70-164">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="9fc70-165">Импорт данных в DocumentDB с помощью средства миграции базы данных</span><span class="sxs-lookup"><span data-stu-id="9fc70-165">Import data into Azure Cosmos DB</span></span>](import-data.md)
