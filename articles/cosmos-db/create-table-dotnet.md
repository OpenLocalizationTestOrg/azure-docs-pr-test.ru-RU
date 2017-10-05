---
title: "Создание приложения .NET Azure Cosmos DB с помощью API таблицы | Документация Майкрософт"
description: "Начните работать с API таблицами Azure Cosmos DB, используя приложение .NET"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 66327041-4d5e-4ce6-a394-fee107c18e59
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/22/2017
ms.author: arramac
ms.openlocfilehash: 29e7eebda5177d6e852ef04ad82d9d38a8d30ed8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-the-table-api"></a><span data-ttu-id="7d133-103">Azure Cosmos DB. Создание приложения .NET с помощью API таблицы</span><span class="sxs-lookup"><span data-stu-id="7d133-103">Azure Cosmos DB: Build a .NET application using the Table API</span></span>

<span data-ttu-id="7d133-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="7d133-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="7d133-105">Вы можете быстро создавать и запрашивать документы, пары "ключ — значение" и базы данных графов, используя преимущества возможностей глобального распределения и горизонтального масштабирования Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7d133-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="7d133-106">В этом кратком руководстве описано создание учетной записи Azure Cosmos DB, а также создание таблицы в рамках этой учетной записи с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="7d133-106">This quick start demonstrates how to create an Azure Cosmos DB account, and create a table within that account using the Azure portal.</span></span> <span data-ttu-id="7d133-107">Затем нужно написать код для вставки, обновления и удаления сущностей, а также выполнить некоторые запросы с использованием нового пакета [Таблица службы хранилища Windows Azure класса Premium](https://aka.ms/premiumtablenuget) (предварительная версия) из NuGet.</span><span class="sxs-lookup"><span data-stu-id="7d133-107">You'll then write code to insert, update, and delete entities, and run some queries using the new [Windows Azure Storage Premium Table](https://aka.ms/premiumtablenuget) (preview) package from NuGet.</span></span> <span data-ttu-id="7d133-108">Эта библиотека включает те же классы и подписи методов, что и [пакет SDK для службы хранилища Microsoft Azure](https://www.nuget.org/packages/WindowsAzure.Storage). Кроме того, она может подключаться к учетным записям Azure Cosmos DB через [API таблиц](table-introduction.md) (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="7d133-108">This library has the same classes and method signatures as the public [Windows Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also has the ability to connect to Azure Cosmos DB accounts using the [Table API](table-introduction.md) (preview).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7d133-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7d133-109">Prerequisites</span></span>

<span data-ttu-id="7d133-110">Если вы еще не установили Visual Studio 2017, вы можете скачать и использовать **бесплатный** [выпуск Community для Visual Studio 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="7d133-110">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="7d133-111">При установке Visual Studio необходимо включить возможность **разработки для Azure**.</span><span class="sxs-lookup"><span data-stu-id="7d133-111">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="7d133-112">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="7d133-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a><span data-ttu-id="7d133-113">Добавление таблицы</span><span class="sxs-lookup"><span data-stu-id="7d133-113">Add a table</span></span>

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a><span data-ttu-id="7d133-114">Добавление демонстрационных данных</span><span class="sxs-lookup"><span data-stu-id="7d133-114">Add sample data</span></span>

<span data-ttu-id="7d133-115">Теперь вы можете добавить данные в созданную таблицу с помощью обозревателя данных (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="7d133-115">You can now add data to your new table using Data Explorer (Preview).</span></span>

1. <span data-ttu-id="7d133-116">В обозревателе данных разверните **пример таблицы**, затем щелкните **Сущности** и нажмите кнопку **Добавление сущности**.</span><span class="sxs-lookup"><span data-stu-id="7d133-116">In Data Explorer, expand **sample-table**, click **Entities**, and then click **Add Entity**.</span></span>

   ![Создание сущностей в обозревателе данных на портале Azure](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-document.png)
2. <span data-ttu-id="7d133-118">Теперь добавьте данные в поля значений свойств PartitionKey и RowKey, а затем нажмите кнопку **Добавление сущности**.</span><span class="sxs-lookup"><span data-stu-id="7d133-118">Now add data to the PartitionKey value box and RowKey value box, and click **Add Entity**.</span></span>

   ![Указание ключа секции и ключа строки для новой сущности](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-entity.png)
  
    <span data-ttu-id="7d133-120">Теперь вы можете добавить больше сущностей в свою таблицу, изменить эти сущности или выполнить запрос данных в обозревателе данных.</span><span class="sxs-lookup"><span data-stu-id="7d133-120">You can now add more entities to your table, edit your entities, or query your data in Data Explorer.</span></span> <span data-ttu-id="7d133-121">В обозревателе данных вы можете масштабировать пропускную способность, а также добавлять хранимые процедуры, определенные пользователем функции и триггеры в свою таблицу.</span><span class="sxs-lookup"><span data-stu-id="7d133-121">Data Explorer is also where you can scale your throughput and add stored procedures, user defined functions, and triggers to your table.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="7d133-122">Клонирование примера приложения</span><span class="sxs-lookup"><span data-stu-id="7d133-122">Clone the sample application</span></span>

<span data-ttu-id="7d133-123">Теперь необходимо клонировать приложение "Таблица" из GitHub. Задайте строку подключения и выполните ее.</span><span class="sxs-lookup"><span data-stu-id="7d133-123">Now let's clone a Table app from github, set the connection string, and run it.</span></span> <span data-ttu-id="7d133-124">Вы узнаете, как можно упростить работу с данными программным способом.</span><span class="sxs-lookup"><span data-stu-id="7d133-124">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="7d133-125">Откройте окно терминала Git, например Git Bash, и выполните команду `cd`, чтобы перейти в рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="7d133-125">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="7d133-126">Выполните команду ниже, чтобы клонировать репозиторий с примером.</span><span class="sxs-lookup"><span data-stu-id="7d133-126">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started.git
    ```

3. <span data-ttu-id="7d133-127">Затем откройте файл решения в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7d133-127">Then open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="7d133-128">Просмотр кода</span><span class="sxs-lookup"><span data-stu-id="7d133-128">Review the code</span></span>

<span data-ttu-id="7d133-129">Сделаем краткий обзор того, что происходит в приложении.</span><span class="sxs-lookup"><span data-stu-id="7d133-129">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="7d133-130">Откройте файл Program.cs, и вы увидите, что эти строки кода создают ресурсы Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7d133-130">Open the Program.cs file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="7d133-131">Инициализация CloudTableClient.</span><span class="sxs-lookup"><span data-stu-id="7d133-131">The CloudTableClient is initialized.</span></span>

    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); 
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

* <span data-ttu-id="7d133-132">Создание таблицы, если она не существует.</span><span class="sxs-lookup"><span data-stu-id="7d133-132">A new table is created if it does not exist.</span></span>

    ```csharp
    CloudTable table = tableClient.GetTableReference("people");
    table.CreateIfNotExists();
    ```

* <span data-ttu-id="7d133-133">Создание контейнера таблицы.</span><span class="sxs-lookup"><span data-stu-id="7d133-133">A new Table container is created.</span></span> <span data-ttu-id="7d133-134">Этот код очень похож на код обычного пакета SDK для хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="7d133-134">You will notice this code very similar to regular Azure Table storage SDK.</span></span> 

    ```csharp
    CustomerEntity item = new CustomerEntity()
                {
                    PartitionKey = Guid.NewGuid().ToString(),
                    RowKey = Guid.NewGuid().ToString(),
                    Email = $"{GetRandomString(6)}@contoso.com",
                    PhoneNumber = "425-555-0102",
                    Bio = GetRandomString(1000)
                };
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="7d133-135">Обновление строки подключения</span><span class="sxs-lookup"><span data-stu-id="7d133-135">Update your connection string</span></span>

<span data-ttu-id="7d133-136">Теперь мы обновим данные строки подключения, чтобы приложение могло взаимодействовать с Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7d133-136">Now we'll update the connection string information so your app can talk to Azure Cosmos DB.</span></span> 

1. <span data-ttu-id="7d133-137">В Visual Studio откройте файл app.config.</span><span class="sxs-lookup"><span data-stu-id="7d133-137">In Visual Studio, open the app.config file.</span></span> 

2. <span data-ttu-id="7d133-138">На [портале Azure](http://portal.azure.com/) в меню навигации Azure Cosmos DB слева щелкните **Строка подключения**.</span><span class="sxs-lookup"><span data-stu-id="7d133-138">In the [Azure portal](http://portal.azure.com/), in the Azure Cosmos DB left navigation menu, click **Connection String**.</span></span> <span data-ttu-id="7d133-139">В новой области нажмите кнопку копирования для строки подключения.</span><span class="sxs-lookup"><span data-stu-id="7d133-139">Then in the new pane click the copy button for the connection string.</span></span> 

    ![Просмотр и копирование конечной точки и ключа учетной записи в области данных строки подключения](./media/create-table-dotnet/keys.png)

3. <span data-ttu-id="7d133-141">Вставьте значение в файл app.config для параметра PremiumStorageConnectionString.</span><span class="sxs-lookup"><span data-stu-id="7d133-141">Paste the value into the app.config file as the value of the PremiumStorageConnectionString.</span></span> 

    `<add key="PremiumStorageConnectionString" 
        value="DefaultEndpointsProtocol=https;AccountName=MYSTORAGEACCOUNT;AccountKey=AUTHKEY;TableEndpoint=https://COSMOSDB.documents.azure.com" />`    

    <span data-ttu-id="7d133-142">StandardStorageConnectionString можно оставить без изменений.</span><span class="sxs-lookup"><span data-stu-id="7d133-142">You can leave the StandardStorageConnectionString as is.</span></span>

<span data-ttu-id="7d133-143">Теперь приложение со всеми сведениями, необходимыми для взаимодействия с Azure Cosmos DB, обновлено.</span><span class="sxs-lookup"><span data-stu-id="7d133-143">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

## <a name="run-the-web-app"></a><span data-ttu-id="7d133-144">Запуск веб-приложения</span><span class="sxs-lookup"><span data-stu-id="7d133-144">Run the web app</span></span>

1. <span data-ttu-id="7d133-145">В **обозревателе решений** Visual Studio щелкните проект **PremiumTableGetStarted** правой кнопкой мыши и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="7d133-145">In Visual Studio, right-click on the **PremiumTableGetStarted** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="7d133-146">В поле **Обзор** введите *WindowsAzure.Storage-PremiumTable*.</span><span class="sxs-lookup"><span data-stu-id="7d133-146">In the NuGet **Browse** box, type *WindowsAzure.Storage-PremiumTable*.</span></span>

3. <span data-ttu-id="7d133-147">Установите флажок **Включить предварительные выпуски**.</span><span class="sxs-lookup"><span data-stu-id="7d133-147">Check the **Include prerelease** box.</span></span> 

4. <span data-ttu-id="7d133-148">Получив результаты, установите библиотеку **WindowsAzure.Storage-PremiumTable**.</span><span class="sxs-lookup"><span data-stu-id="7d133-148">From the results, install the **WindowsAzure.Storage-PremiumTable** library.</span></span> <span data-ttu-id="7d133-149">Установится предварительная версия пакета API таблицы Azure Cosmos DB, а также все зависимые компоненты.</span><span class="sxs-lookup"><span data-stu-id="7d133-149">This installs the preview Azure Cosmos DB Table API package as well as all dependencies.</span></span> <span data-ttu-id="7d133-150">Обратите внимание, что этот пакет NuGet отличается от пакета службы хранилища Windows Azure, используемого хранилищем таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="7d133-150">Note that this is a different NuGet package than the Windows Azure Storage package used by Azure Table storage.</span></span> 

5. <span data-ttu-id="7d133-151">Нажмите клавиши CTRL+F5 для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="7d133-151">Click CTRL + F5 to run the application.</span></span>

    <span data-ttu-id="7d133-152">В окне консоли отобразятся добавленные в таблицу, полученные, запрашиваемые, замененные и удаленные из таблицы данные.</span><span class="sxs-lookup"><span data-stu-id="7d133-152">The console window displays the data being added, retrieved, queried, replaced and deleted from the table.</span></span> <span data-ttu-id="7d133-153">После выполнения скрипта закройте окно консоли, нажав любую клавишу.</span><span class="sxs-lookup"><span data-stu-id="7d133-153">When the script completes, press any key to close the console window.</span></span> 
    
    ![Выходные данные этого краткого руководства, отображаемые в консоли](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-console-output.png)

6. <span data-ttu-id="7d133-155">Чтобы увидеть новые сущности в обозревателе данных, закомментируйте строки 188–208 в файле program.cs (так они не будут удалены) и запустите пример снова.</span><span class="sxs-lookup"><span data-stu-id="7d133-155">If you want to see the new entities in Data Explorer, just comment out lines 188-208 in program.cs so they aren't deleted, then run the sample again.</span></span> 

    <span data-ttu-id="7d133-156">Теперь вернитесь в обозреватель данных, нажмите кнопку **Обновить**, разверните таблицу **Пользователи**, щелкните **Сущности** и начинайте работу с новыми данными.</span><span class="sxs-lookup"><span data-stu-id="7d133-156">You can now go back to Data Explorer, click **Refresh**, expand the **people** table and click **Entities**, and then work with this new data.</span></span> 

    ![Новые сущности в обозревателе данных](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-data-explorer.png)

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="7d133-158">Просмотр соглашений об уровне обслуживания на портале Azure</span><span class="sxs-lookup"><span data-stu-id="7d133-158">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="7d133-159">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="7d133-159">Clean up resources</span></span>

<span data-ttu-id="7d133-160">Если вы не собираетесь использовать это приложение дальше, удалите все ресурсы, созданные в ходе работы с этим руководством, на портале Azure, сделав следующее:</span><span class="sxs-lookup"><span data-stu-id="7d133-160">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span> 

1. <span data-ttu-id="7d133-161">В меню слева на портале Azure щелкните **Группы ресурсов**, а затем выберите имя созданного ресурса.</span><span class="sxs-lookup"><span data-stu-id="7d133-161">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="7d133-162">На странице группы ресурсов щелкните **Удалить**, в текстовом поле введите имя ресурса для удаления и щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="7d133-162">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d133-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7d133-163">Next steps</span></span>

<span data-ttu-id="7d133-164">Из этого краткого руководства вы узнали, как создать учетную запись Azure Cosmos DB и таблицу с помощью обозревателя данных, а также как запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="7d133-164">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a table using the Data Explorer, and run an app.</span></span>  <span data-ttu-id="7d133-165">Теперь вы можете выполнить запрос данных с помощью API таблиц.</span><span class="sxs-lookup"><span data-stu-id="7d133-165">Now you can query your data using the Table API.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="7d133-166">Azure Cosmos DB. Выполнение запроса с помощью API таблицы (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="7d133-166">Query using the Table API</span></span>](tutorial-query-table.md)

