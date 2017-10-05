---
title: "Azure Cosmos DB. Создание веб-приложения с проверкой подлинности Xamarin и Facebook | Документация Майкрософт"
description: "В этой статье представлен пример кода .NET, который можно использовать для подключения и выполнения запросов к Azure Cosmos DB."
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
ms.openlocfilehash: 4ea97c2aca6769843d0210ffeae6f95531a21f10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a><span data-ttu-id="35e55-103">Azure Cosmos DB. Создание веб-приложения с проверкой подлинности .NET, Xamarin и Facebook</span><span class="sxs-lookup"><span data-stu-id="35e55-103">Azure Cosmos DB: Build a web app with .NET, Xamarin, and Facebook authentication</span></span>

<span data-ttu-id="35e55-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="35e55-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="35e55-105">Вы можете быстро создавать и запрашивать документы, пары "ключ — значение" и базы данных графов, используя преимущества возможностей глобального распределения и горизонтального масштабирования Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="35e55-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="35e55-106">В этом кратком руководстве показано, как создать учетную запись Azure Cosmos DB, базу данных документов и коллекцию с использованием портала Azure.</span><span class="sxs-lookup"><span data-stu-id="35e55-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="35e55-107">Затем вы создадите и развернете веб-приложение со списком задач на основе [API-интерфейса .NET для DocumentDB](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/) и обработчика авторизации Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="35e55-107">You'll then build and deploy a todo list web app built on the [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/), and the Azure Cosmos DB authorization engine.</span></span> <span data-ttu-id="35e55-108">Веб-приложение со списком задач реализовывает шаблон данных каждого пользователя, разрешающий им выполнять вход с помощью проверки подлинности Facebook, а также управлять собственными элементами.</span><span class="sxs-lookup"><span data-stu-id="35e55-108">The todo list web app implements a per-user data pattern that enables users to login using Facebook Auth and manage their own to do items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35e55-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="35e55-109">Prerequisites</span></span>

<span data-ttu-id="35e55-110">Если вы еще не установили Visual Studio 2017, вы можете скачать и использовать **бесплатный** [выпуск Community для Visual Studio 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="35e55-110">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="35e55-111">При установке Visual Studio необходимо включить возможность **разработки для Azure**.</span><span class="sxs-lookup"><span data-stu-id="35e55-111">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="35e55-112">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="35e55-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="35e55-113">Добавление коллекции</span><span class="sxs-lookup"><span data-stu-id="35e55-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="35e55-114">Клонирование примера приложения</span><span class="sxs-lookup"><span data-stu-id="35e55-114">Clone the sample application</span></span>

<span data-ttu-id="35e55-115">Теперь необходимо клонировать приложение API DocumentDB из GitHub. Задайте строку подключения и выполните ее.</span><span class="sxs-lookup"><span data-stu-id="35e55-115">Now let's clone a DocumentDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="35e55-116">Вы узнаете, как можно упростить работу с данными программным способом.</span><span class="sxs-lookup"><span data-stu-id="35e55-116">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="35e55-117">Откройте окно терминала Git, например Git Bash, и выполните команду `cd`, чтобы перейти в рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="35e55-117">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="35e55-118">Выполните команду ниже, чтобы клонировать репозиторий с примером.</span><span class="sxs-lookup"><span data-stu-id="35e55-118">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. <span data-ttu-id="35e55-119">Затем откройте файл DocumentDBTodo.sln из папки samples/xamarin/UserItems/xamarin.forms в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="35e55-119">Then open the DocumentDBTodo.sln file from the samples/xamarin/UserItems/xamarin.forms folder in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="35e55-120">Просмотр кода</span><span class="sxs-lookup"><span data-stu-id="35e55-120">Review the code</span></span>

<span data-ttu-id="35e55-121">Код в папке Xamarin содержит:</span><span class="sxs-lookup"><span data-stu-id="35e55-121">The code in the Xamarin folder contains:</span></span>

* <span data-ttu-id="35e55-122">Приложение Xamarin.</span><span class="sxs-lookup"><span data-stu-id="35e55-122">Xamarin app.</span></span> <span data-ttu-id="35e55-123">Приложение хранит элементы списка задач пользователя в секционированной коллекции UserItems.</span><span class="sxs-lookup"><span data-stu-id="35e55-123">The app stores the user's todo items in a partitioned collection named UserItems.</span></span>
* <span data-ttu-id="35e55-124">Брокер маркера ресурса API.</span><span class="sxs-lookup"><span data-stu-id="35e55-124">Resource token broker API.</span></span> <span data-ttu-id="35e55-125">Простой веб-API ASP.NET в качестве брокера токенов ресурсов Azure Cosmos DB в приложении пользователей, вошедших в систему.</span><span class="sxs-lookup"><span data-stu-id="35e55-125">A simple ASP.NET Web API to broker Azure Cosmos DB resource tokens to the logged in users of the app.</span></span> <span data-ttu-id="35e55-126">Токены ресурсов — это токены кратковременного доступа, предоставляющие приложению доступ к данным пользователя, вошедшего в систему.</span><span class="sxs-lookup"><span data-stu-id="35e55-126">Resource tokens are short-lived access tokens that provide the app with the access to the logged in user's data.</span></span>

<span data-ttu-id="35e55-127">На схеме ниже показана процедура проверки подлинности и обработки данных.</span><span class="sxs-lookup"><span data-stu-id="35e55-127">The authentication and data flow is illustrated in the diagram below.</span></span>

* <span data-ttu-id="35e55-128">Коллекция UserItems создается с ключом раздела /userid.</span><span class="sxs-lookup"><span data-stu-id="35e55-128">The UserItems collection is created with the partition key '/userid'.</span></span> <span data-ttu-id="35e55-129">Если указать ключ раздела для коллекции, Azure Cosmos DB сможет осуществлять неограниченное масштабирование по мере того, как растет количество пользователей и элементов.</span><span class="sxs-lookup"><span data-stu-id="35e55-129">Specifying a partition key for a collection allows Azure Cosmos DB to scale infinitely as the number of users and items grows.</span></span>
* <span data-ttu-id="35e55-130">Приложение Xamarin позволяет пользователям выполнять вход с учетными данными Facebook.</span><span class="sxs-lookup"><span data-stu-id="35e55-130">The Xamarin app allows users to login with Facebook credentials.</span></span>
* <span data-ttu-id="35e55-131">Оно использует маркер доступа Facebook для проверки подлинности с помощью ResourceTokenBroker API.</span><span class="sxs-lookup"><span data-stu-id="35e55-131">The Xamarin app uses Facebook access token to authenticate with ResourceTokenBroker API</span></span>
* <span data-ttu-id="35e55-132">API брокера токена ресурса проверяет подлинность запроса с помощью функции проверки подлинности службы приложений и запрашивает токен ресурса Azure Cosmos DB с доступом на чтение и запись для всех документов, совместно использующих ключ раздела прошедшего проверку подлинности пользователя.</span><span class="sxs-lookup"><span data-stu-id="35e55-132">The resource token broker API authenticates the request using App Service Auth feature, and requests an Azure Cosmos DB resource token with read/write access to all documents sharing the authenticated user's partition key.</span></span>
* <span data-ttu-id="35e55-133">Брокер токена ресурса возвращает токен ресурса в клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="35e55-133">Resource token broker returns the resource token to the client app.</span></span>
* <span data-ttu-id="35e55-134">Приложение получает доступ к элементам списка задач пользователя с помощью токена ресурса.</span><span class="sxs-lookup"><span data-stu-id="35e55-134">The app accesses the user's todo items using the resource token.</span></span>

![Приложение со списком задач с демонстрационными данными](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a><span data-ttu-id="35e55-136">Обновление строки подключения</span><span class="sxs-lookup"><span data-stu-id="35e55-136">Update your connection string</span></span>

<span data-ttu-id="35e55-137">Теперь вернитесь на портал Azure, чтобы получить данные строки подключения. Скопируйте эти данные в приложение.</span><span class="sxs-lookup"><span data-stu-id="35e55-137">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="35e55-138">На [портале Azure](http://portal.azure.com/) перейдите к учетной записи Azure Cosmos DB и на левой панели навигации щелкните **Ключи**, а затем выберите **Ключи записи-чтения**.</span><span class="sxs-lookup"><span data-stu-id="35e55-138">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="35e55-139">На следующем шаге используйте кнопку копирования в правой части экрана, чтобы скопировать универсальный код ресурса (URI) и первичный ключ в файл Web.config.</span><span class="sxs-lookup"><span data-stu-id="35e55-139">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the Web.config file in the next step.</span></span>

    ![Просмотр и копирование ключа доступа на портале Azure, колонка "Ключи"](./media/create-documentdb-xamarin-dotnet/keys.png)

2. <span data-ttu-id="35e55-141">В Visual Studio 2017 откройте файл Web.config в папке azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker.</span><span class="sxs-lookup"><span data-stu-id="35e55-141">In Visual Studio 2017, open the Web.config file in the azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker folder.</span></span> 

3. <span data-ttu-id="35e55-142">Скопируйте значение универсального кода ресурса (URI) c портала (с помощью кнопки копирования) и добавьте его в качестве значения параметра accountUrl в файле Web.config.</span><span class="sxs-lookup"><span data-stu-id="35e55-142">Copy your URI value from the portal (using the copy button) and make it the value of the accountUrl in Web.config.</span></span> 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. <span data-ttu-id="35e55-143">Затем скопируйте значение первичного ключа с портала и добавьте его в качестве значения параметра accountKey в файле Web.congif.</span><span class="sxs-lookup"><span data-stu-id="35e55-143">Then copy your PRIMARY KEY value from the portal and make it the value of the accountKey in Web.congif.</span></span> 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

<span data-ttu-id="35e55-144">Теперь приложение со всеми сведениями, необходимыми для взаимодействия с Azure Cosmos DB, обновлено.</span><span class="sxs-lookup"><span data-stu-id="35e55-144">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

## <a name="build-and-deploy-the-web-app"></a><span data-ttu-id="35e55-145">Создание и развертывание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="35e55-145">Build and deploy the web app</span></span>

1. <span data-ttu-id="35e55-146">Создайте на портале Azure веб-сайт службы приложений для размещения API брокера токена ресурса.</span><span class="sxs-lookup"><span data-stu-id="35e55-146">In the Azure portal, create an App Service website to host the Resource token broker API.</span></span>
2. <span data-ttu-id="35e55-147">На портале Azure откройте колонку "Параметры приложения" веб-сайта API брокера токена ресурса.</span><span class="sxs-lookup"><span data-stu-id="35e55-147">In the Azure portal, open the App Settings blade of the Resource token broker API website.</span></span> <span data-ttu-id="35e55-148">Заполните следующие параметры приложения:</span><span class="sxs-lookup"><span data-stu-id="35e55-148">Fill in the following app settings:</span></span>

    * <span data-ttu-id="35e55-149">accountUrl — URL-адрес учетной записи Azure Cosmos DB на вкладке "Ключи".</span><span class="sxs-lookup"><span data-stu-id="35e55-149">accountUrl - The Azure Cosmos DB account URL from the Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="35e55-150">accountKey — главный ключ учетной записи Azure Cosmos DB на вкладке "Ключи".</span><span class="sxs-lookup"><span data-stu-id="35e55-150">accountKey - The Azure Cosmos DB account master key from the Keys tab of your Azure Cosmos DB account.</span></span>
    * <span data-ttu-id="35e55-151">databaseId и collectionId созданной базы данных и коллекции.</span><span class="sxs-lookup"><span data-stu-id="35e55-151">databaseId and collectionId of your created database and collection</span></span>

3. <span data-ttu-id="35e55-152">Опубликуйте решение ResourceTokenBroker на созданном веб-сайте.</span><span class="sxs-lookup"><span data-stu-id="35e55-152">Publish the ResourceTokenBroker solution to your created website.</span></span>

4. <span data-ttu-id="35e55-153">Откройте проект Xamarin, а затем файл TodoItemManager.cs.</span><span class="sxs-lookup"><span data-stu-id="35e55-153">Open the Xamarin project, and navigate to TodoItemManager.cs.</span></span> <span data-ttu-id="35e55-154">Присвойте необходимые значения параметрам accountURL, collectionId, databaseId, а также укажите resourceTokenBrokerURL как базовый URL-адрес HTTPS для веб-сайта брокера токена ресурса.</span><span class="sxs-lookup"><span data-stu-id="35e55-154">Fill in the values for accountURL, collectionId, databaseId, as well as resourceTokenBrokerURL as the base https url for the resource token broker website.</span></span>

5. <span data-ttu-id="35e55-155">Чтобы настроить проверку подлинности Facebook и веб-сайт ResourceTokenBroker, ознакомьтесь со статьей [Как настроить приложение службы приложений для использования имени для входа Facebook](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="35e55-155">Complete the [How to configure your App Service application to use Facebook login](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) tutorial to setup Facebook authentication and configure the ResourceTokenBroker website.</span></span>

    <span data-ttu-id="35e55-156">Запустите приложение Xamarin.</span><span class="sxs-lookup"><span data-stu-id="35e55-156">Run the Xamarin app.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="35e55-157">Просмотр соглашений об уровне обслуживания на портале Azure</span><span class="sxs-lookup"><span data-stu-id="35e55-157">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="35e55-158">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="35e55-158">Clean up resources</span></span>

<span data-ttu-id="35e55-159">Если вы не собираетесь использовать это приложение дальше, удалите все ресурсы, созданные в ходе работы с этим руководством, на портале Azure, сделав следующее:</span><span class="sxs-lookup"><span data-stu-id="35e55-159">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span> 

1. <span data-ttu-id="35e55-160">В меню слева на портале Azure щелкните **Группы ресурсов**, а затем выберите имя созданного ресурса.</span><span class="sxs-lookup"><span data-stu-id="35e55-160">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you just created.</span></span> 
2. <span data-ttu-id="35e55-161">На странице группы ресурсов щелкните **Удалить**, в текстовом поле введите имя ресурса для удаления и щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="35e55-161">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35e55-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="35e55-162">Next steps</span></span>

<span data-ttu-id="35e55-163">В этом кратком руководстве вы узнали, как создать учетную запись Azure Cosmos DB, коллекцию с помощью обозревателя данных, а также как создать и развернуть приложение Xamarin.</span><span class="sxs-lookup"><span data-stu-id="35e55-163">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and build and deploy a Xamarin app.</span></span> <span data-ttu-id="35e55-164">Теперь можно импортировать дополнительные данные в учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="35e55-164">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="35e55-165">Импорт данных в DocumentDB с помощью средства миграции базы данных</span><span class="sxs-lookup"><span data-stu-id="35e55-165">Import data into Azure Cosmos DB</span></span>](import-data.md)
