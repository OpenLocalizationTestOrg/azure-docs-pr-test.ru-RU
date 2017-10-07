---
title: "Здравствуйте, aaaBuild приложения Azure Cosmos DB .NET с помощью API-Интерфейс таблиц | Документы Microsoft"
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
ms.openlocfilehash: bdd4f8ec45407962b3d2cb26aa814a20cfc62173
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-table-api"></a><span data-ttu-id="de3ae-103">Azure Cosmos DB: Сборка приложений .NET, использующих hello API таблиц</span><span class="sxs-lookup"><span data-stu-id="de3ae-103">Azure Cosmos DB: Build a .NET application using hello Table API</span></span>

<span data-ttu-id="de3ae-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="de3ae-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="de3ae-105">Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД.</span><span class="sxs-lookup"><span data-stu-id="de3ae-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="de3ae-106">В этом кратком руководстве показано, как toocreate Cosmos Azure DB учетную запись, а также создать таблицу в этой учетной записи, с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="de3ae-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, and create a table within that account using hello Azure portal.</span></span> <span data-ttu-id="de3ae-107">Вы затем написать код tooinsert, обновления и удаления сущностей, а также выполнение некоторых запросов, с помощью hello новый [таблиц Premium хранилища Windows Azure](https://aka.ms/premiumtablenuget) (Предварительная версия) пакета из NuGet.</span><span class="sxs-lookup"><span data-stu-id="de3ae-107">You'll then write code tooinsert, update, and delete entities, and run some queries using hello new [Windows Azure Storage Premium Table](https://aka.ms/premiumtablenuget) (preview) package from NuGet.</span></span> <span data-ttu-id="de3ae-108">Эта библиотека имеет hello же классах и подписях методов как hello public [пакет SDK хранилища Windows Azure](https://www.nuget.org/packages/WindowsAzure.Storage), но также имеет hello возможности tooconnect tooAzure Cosmos DB учетным записям hello [API таблиц](table-introduction.md) (Предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="de3ae-108">This library has hello same classes and method signatures as hello public [Windows Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also has hello ability tooconnect tooAzure Cosmos DB accounts using hello [Table API](table-introduction.md) (preview).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="de3ae-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="de3ae-109">Prerequisites</span></span>

<span data-ttu-id="de3ae-110">Если у вас еще нет Visual Studio 2017 г. установлен, можно загрузить и использовать hello **свободного** [2017 г. Visual Studio Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="de3ae-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="de3ae-111">Убедитесь, что включен **разработки Azure** во время установки Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="de3ae-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="de3ae-112">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="de3ae-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a><span data-ttu-id="de3ae-113">Добавление таблицы</span><span class="sxs-lookup"><span data-stu-id="de3ae-113">Add a table</span></span>

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a><span data-ttu-id="de3ae-114">Добавление демонстрационных данных</span><span class="sxs-lookup"><span data-stu-id="de3ae-114">Add sample data</span></span>

<span data-ttu-id="de3ae-115">Теперь можно добавить новую таблицу данных tooyour с помощью данных обозревателя (Предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="de3ae-115">You can now add data tooyour new table using Data Explorer (Preview).</span></span>

1. <span data-ttu-id="de3ae-116">В обозревателе данных разверните **пример таблицы**, затем щелкните **Сущности** и нажмите кнопку **Добавление сущности**.</span><span class="sxs-lookup"><span data-stu-id="de3ae-116">In Data Explorer, expand **sample-table**, click **Entities**, and then click **Add Entity**.</span></span>

   ![Создавайте новые сущности в обозревателе данных в hello портал Azure](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-document.png)
2. <span data-ttu-id="de3ae-118">Теперь добавьте поле значений данных toohello PartitionKey и RowKey значение поле и нажмите **Добавление сущности**.</span><span class="sxs-lookup"><span data-stu-id="de3ae-118">Now add data toohello PartitionKey value box and RowKey value box, and click **Add Entity**.</span></span>

   ![Задать hello ключ секции и ключа строки для новой сущности](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-entity.png)
  
    <span data-ttu-id="de3ae-120">Теперь можно добавить дополнительные таблицы tooyour сущностей, изменение сущности или запроса данных в обозревателе данных.</span><span class="sxs-lookup"><span data-stu-id="de3ae-120">You can now add more entities tooyour table, edit your entities, or query your data in Data Explorer.</span></span> <span data-ttu-id="de3ae-121">Обозреватель данных — также, где можно масштабировать пропускную способность и добавить хранимые процедуры, определяемые пользователем функции и триггеры tooyour таблицы.</span><span class="sxs-lookup"><span data-stu-id="de3ae-121">Data Explorer is also where you can scale your throughput and add stored procedures, user defined functions, and triggers tooyour table.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="de3ae-122">Пример приложения hello клонирования</span><span class="sxs-lookup"><span data-stu-id="de3ae-122">Clone hello sample application</span></span>

<span data-ttu-id="de3ae-123">Теперь давайте клонировать приложении таблицы из github, задайте строку подключения hello и запустите его.</span><span class="sxs-lookup"><span data-stu-id="de3ae-123">Now let's clone a Table app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="de3ae-124">Вы увидите, как просто можно toowork с данными программными средствами.</span><span class="sxs-lookup"><span data-stu-id="de3ae-124">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="de3ae-125">Откройте окно терминала git, таких как git bash и `cd` tooa рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="de3ae-125">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="de3ae-126">Выполнения hello следующая команда репозитории примеров tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="de3ae-126">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started.git
    ```

3. <span data-ttu-id="de3ae-127">Затем откройте файл решения hello в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="de3ae-127">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="de3ae-128">Проверка кода hello</span><span class="sxs-lookup"><span data-stu-id="de3ae-128">Review hello code</span></span>

<span data-ttu-id="de3ae-129">Убедитесь, что происходит в приложение hello быстро ознакомиться.</span><span class="sxs-lookup"><span data-stu-id="de3ae-129">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="de3ae-130">Привет открыть файл Program.cs и вы найдете следующие строки кода создать hello Azure Cosmos DB ресурсы.</span><span class="sxs-lookup"><span data-stu-id="de3ae-130">Open hello Program.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="de3ae-131">Hello CloudTableClient инициализируется.</span><span class="sxs-lookup"><span data-stu-id="de3ae-131">hello CloudTableClient is initialized.</span></span>

    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); 
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

* <span data-ttu-id="de3ae-132">Создание таблицы, если она не существует.</span><span class="sxs-lookup"><span data-stu-id="de3ae-132">A new table is created if it does not exist.</span></span>

    ```csharp
    CloudTable table = tableClient.GetTableReference("people");
    table.CreateIfNotExists();
    ```

* <span data-ttu-id="de3ae-133">Создание контейнера таблицы.</span><span class="sxs-lookup"><span data-stu-id="de3ae-133">A new Table container is created.</span></span> <span data-ttu-id="de3ae-134">Вы увидите этот код очень похож tooregular хранилище таблиц Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="de3ae-134">You will notice this code very similar tooregular Azure Table storage SDK.</span></span> 

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

## <a name="update-your-connection-string"></a><span data-ttu-id="de3ae-135">Обновление строки подключения</span><span class="sxs-lookup"><span data-stu-id="de3ae-135">Update your connection string</span></span>

<span data-ttu-id="de3ae-136">Теперь строку hello подключения будет обновлена, приложения могут взаимодействовать tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de3ae-136">Now we'll update hello connection string information so your app can talk tooAzure Cosmos DB.</span></span> 

1. <span data-ttu-id="de3ae-137">В Visual Studio откройте файл app.config hello.</span><span class="sxs-lookup"><span data-stu-id="de3ae-137">In Visual Studio, open hello app.config file.</span></span> 

2. <span data-ttu-id="de3ae-138">В hello [портал Azure](http://portal.azure.com/)в hello Azure Cosmos DB влево меню навигации, нажмите кнопку **строка подключения**.</span><span class="sxs-lookup"><span data-stu-id="de3ae-138">In hello [Azure portal](http://portal.azure.com/), in hello Azure Cosmos DB left navigation menu, click **Connection String**.</span></span> <span data-ttu-id="de3ae-139">В новой области hello нажмите кнопку hello копирования для строки подключения hello.</span><span class="sxs-lookup"><span data-stu-id="de3ae-139">Then in hello new pane click hello copy button for hello connection string.</span></span> 

    ![Просмотр и копирование hello конечную точку и ключ учетной записи в области hello строки подключения](./media/create-table-dotnet/keys.png)

3. <span data-ttu-id="de3ae-141">Вставьте значение hello в файл app.config hello в качестве значения hello PremiumStorageConnectionString hello.</span><span class="sxs-lookup"><span data-stu-id="de3ae-141">Paste hello value into hello app.config file as hello value of hello PremiumStorageConnectionString.</span></span> 

    `<add key="PremiumStorageConnectionString" 
        value="DefaultEndpointsProtocol=https;AccountName=MYSTORAGEACCOUNT;AccountKey=AUTHKEY;TableEndpoint=https://COSMOSDB.documents.azure.com" />`    

    <span data-ttu-id="de3ae-142">Можно оставить hello StandardStorageConnectionString как есть.</span><span class="sxs-lookup"><span data-stu-id="de3ae-142">You can leave hello StandardStorageConnectionString as is.</span></span>

<span data-ttu-id="de3ae-143">Теперь вы обновили приложения с все hello сведения учетной записи, он должен toocommunicate с Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="de3ae-143">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="run-hello-web-app"></a><span data-ttu-id="de3ae-144">Запустите веб-приложение hello</span><span class="sxs-lookup"><span data-stu-id="de3ae-144">Run hello web app</span></span>

1. <span data-ttu-id="de3ae-145">В Visual Studio щелкните правой кнопкой мыши на hello **PremiumTableGetStarted** проекта в **обозревателе решений** и нажмите кнопку **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="de3ae-145">In Visual Studio, right-click on hello **PremiumTableGetStarted** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="de3ae-146">В hello NuGet **Обзор** введите *WindowsAzure.Storage PremiumTable*.</span><span class="sxs-lookup"><span data-stu-id="de3ae-146">In hello NuGet **Browse** box, type *WindowsAzure.Storage-PremiumTable*.</span></span>

3. <span data-ttu-id="de3ae-147">Проверьте hello **включить предварительный выпуск** поле.</span><span class="sxs-lookup"><span data-stu-id="de3ae-147">Check hello **Include prerelease** box.</span></span> 

4. <span data-ttu-id="de3ae-148">На основе результатов hello установить hello **WindowsAzure.Storage PremiumTable** библиотеки.</span><span class="sxs-lookup"><span data-stu-id="de3ae-148">From hello results, install hello **WindowsAzure.Storage-PremiumTable** library.</span></span> <span data-ttu-id="de3ae-149">При этом устанавливаются hello предварительной версии пакета Azure Cosmos DB таблицы API, а также все зависимости.</span><span class="sxs-lookup"><span data-stu-id="de3ae-149">This installs hello preview Azure Cosmos DB Table API package as well as all dependencies.</span></span> <span data-ttu-id="de3ae-150">Обратите внимание, что в другой пакет NuGet, чем пакет hello хранилища Windows Azure, используемые хранилищем таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="de3ae-150">Note that this is a different NuGet package than hello Windows Azure Storage package used by Azure Table storage.</span></span> 

5. <span data-ttu-id="de3ae-151">Нажмите сочетание клавиш CTRL + F5 toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="de3ae-151">Click CTRL + F5 toorun hello application.</span></span>

    <span data-ttu-id="de3ae-152">окно консоли Hello отображаются данные hello добавляемыми, извлечь, запрашивать, заменить и удалены из таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="de3ae-152">hello console window displays hello data being added, retrieved, queried, replaced and deleted from hello table.</span></span> <span data-ttu-id="de3ae-153">После завершения скрипта hello, нажмите клавишу любого окна консоли ключа tooclose hello.</span><span class="sxs-lookup"><span data-stu-id="de3ae-153">When hello script completes, press any key tooclose hello console window.</span></span> 
    
    ![Выходные данные консоли hello краткое руководство](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-console-output.png)

6. <span data-ttu-id="de3ae-155">Если требуется, чтобы новые сущности toosee hello в обозреватель данных, точно так же, закомментируйте строки 188 208 в файле program.cs, поэтому они не удаляются, запустите образец hello еще раз.</span><span class="sxs-lookup"><span data-stu-id="de3ae-155">If you want toosee hello new entities in Data Explorer, just comment out lines 188-208 in program.cs so they aren't deleted, then run hello sample again.</span></span> 

    <span data-ttu-id="de3ae-156">Теперь вы можете перейти обратно tooData Explorer, нажмите кнопку **обновление**, разверните hello **людей** таблицы и нажмите кнопку **сущностей**и затем работать с новые данные.</span><span class="sxs-lookup"><span data-stu-id="de3ae-156">You can now go back tooData Explorer, click **Refresh**, expand hello **people** table and click **Entities**, and then work with this new data.</span></span> 

    ![Новые сущности в обозревателе данных](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-data-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="de3ae-158">Просмотрите соглашений об уровне обслуживания в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="de3ae-158">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="de3ae-159">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="de3ae-159">Clean up resources</span></span>

<span data-ttu-id="de3ae-160">Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="de3ae-160">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="de3ae-161">Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="de3ae-161">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="de3ae-162">На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="de3ae-162">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de3ae-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="de3ae-163">Next steps</span></span>

<span data-ttu-id="de3ae-164">В этом кратком руководстве вы узнали, как создать таблицу с помощью hello обозреватель данных toocreate учетную запись Azure Cosmos DB и запуск приложения.</span><span class="sxs-lookup"><span data-stu-id="de3ae-164">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a table using hello Data Explorer, and run an app.</span></span>  <span data-ttu-id="de3ae-165">Теперь вы можете запрашивать данные с помощью API таблиц hello.</span><span class="sxs-lookup"><span data-stu-id="de3ae-165">Now you can query your data using hello Table API.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="de3ae-166">Запрос с использованием hello API таблиц</span><span class="sxs-lookup"><span data-stu-id="de3ae-166">Query using hello Table API</span></span>](tutorial-query-table.md)

