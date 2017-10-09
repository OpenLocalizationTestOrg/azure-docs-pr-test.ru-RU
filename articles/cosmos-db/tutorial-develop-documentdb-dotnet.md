---
title: "Azure Cosmos DB: Разработку с использованием hello API DocumentDB в .NET | Документы Microsoft"
description: "Узнайте, как toodevelop с API Azure Cosmos DB DocumentDB, с помощью .NET"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: 0d3d17afa782054c8fdf3cbac421e5a5d0a6800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmosdb-develop-with-hello-documentdb-api-in-net"></a><span data-ttu-id="17100-103">Azure CosmosDB: Разработку с использованием hello API DocumentDB в .NET</span><span class="sxs-lookup"><span data-stu-id="17100-103">Azure CosmosDB: Develop with hello DocumentDB API in .NET</span></span>

<span data-ttu-id="17100-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="17100-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="17100-105">Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД.</span><span class="sxs-lookup"><span data-stu-id="17100-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="17100-106">В этом учебнике показано, как toocreate Azure Cosmos DB учетной записи с помощью hello портал Azure, а затем создать базу данных документов и коллекции с [ключ раздела](documentdb-partition-data.md#partition-keys) с помощью hello [API .NET для DocumentDB](documentdb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="17100-106">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal, and then create a document database and collection with a [partition key](documentdb-partition-data.md#partition-keys) using hello [DocumentDB .NET API](documentdb-introduction.md).</span></span> <span data-ttu-id="17100-107">Определив ключ раздела при создании коллекции, приложения подготавливается tooscale усилий по мере роста данных.</span><span class="sxs-lookup"><span data-stu-id="17100-107">By defining a partition key when you create a collection, your application is prepared tooscale effortlessly as your data grows.</span></span> 

<span data-ttu-id="17100-108">Hello этого учебника описаны следующие задачи с помощью hello [API .NET для DocumentDB](documentdb-sdk-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="17100-108">This tutorial covers hello following tasks by using hello [DocumentDB .NET API](documentdb-sdk-dotnet.md):</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="17100-109">создание учетной записи Azure Cosmos DB;</span><span class="sxs-lookup"><span data-stu-id="17100-109">Create an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="17100-110">создание базы данных и коллекции с ключом секции;</span><span class="sxs-lookup"><span data-stu-id="17100-110">Create a database and collection with a partition key</span></span>
> * <span data-ttu-id="17100-111">создание документов JSON;</span><span class="sxs-lookup"><span data-stu-id="17100-111">Create JSON documents</span></span>
> * <span data-ttu-id="17100-112">обновление документа;</span><span class="sxs-lookup"><span data-stu-id="17100-112">Update a document</span></span>
> * <span data-ttu-id="17100-113">запрос секционированных коллекций;</span><span class="sxs-lookup"><span data-stu-id="17100-113">Query partitioned collections</span></span>
> * <span data-ttu-id="17100-114">выполнение хранимых процедур;</span><span class="sxs-lookup"><span data-stu-id="17100-114">Run stored procedures</span></span>
> * <span data-ttu-id="17100-115">Удаление документа</span><span class="sxs-lookup"><span data-stu-id="17100-115">Delete a document</span></span>
> * <span data-ttu-id="17100-116">удаление базы данных.</span><span class="sxs-lookup"><span data-stu-id="17100-116">Delete a database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17100-117">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="17100-117">Prerequisites</span></span>
<span data-ttu-id="17100-118">Убедитесь, что у вас есть следующие hello:</span><span class="sxs-lookup"><span data-stu-id="17100-118">Please make sure you have hello following:</span></span>

* <span data-ttu-id="17100-119">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="17100-119">An active Azure account.</span></span> <span data-ttu-id="17100-120">Если у вас ее нет, зарегистрируйте [бесплатную учетную запись](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="17100-120">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="17100-121">Кроме того, можно использовать hello [DB эмулятор Azure Cosmos](local-emulator.md) для этого учебника, если вы хотите toouse локальную среду, эмулирующую службы Azure DocumentDB hello в целях разработки.</span><span class="sxs-lookup"><span data-stu-id="17100-121">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial if you'd like toouse a local environment that emulates hello Azure DocumentDB service for development purposes.</span></span>
* <span data-ttu-id="17100-122">[Visual Studio](http://www.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="17100-122">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="17100-123">создание учетной записи Azure Cosmos DB;</span><span class="sxs-lookup"><span data-stu-id="17100-123">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="17100-124">Давайте начнем с создания учетной записи Azure Cosmos DB в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="17100-124">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>

> [!TIP]
> * <span data-ttu-id="17100-125">Уже есть учетная запись Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="17100-125">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="17100-126">Если Да, пропустить слишком[Настройка решения Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="17100-126">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="17100-127">У вас была учетная запись Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="17100-127">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="17100-128">Если таким образом, учетной записи теперь учетную запись Azure Cosmos DB и можно сразу перейти слишком[Настройка решения Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="17100-128">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="17100-129">Если вы используете hello Azure Cosmos DB эмулятор, выполните действия hello в [DB эмулятор Azure Cosmos](local-emulator.md) toosetup hello эмулятора и пропускать слишком[настроить решение Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="17100-129">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="17100-130"><a id="SetupVS"></a>Настройка решения Visual Studio</span><span class="sxs-lookup"><span data-stu-id="17100-130"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="17100-131">Откройте **Visual Studio** у себя на компьютере.</span><span class="sxs-lookup"><span data-stu-id="17100-131">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="17100-132">На hello **файл** последовательно выберите пункты **New**и нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="17100-132">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="17100-133">В hello **новый проект** диалогового окна выберите **шаблоны** / **Visual C#** / **консольного приложения (.NET Framework)**, имя проекта и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="17100-133">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="17100-134">![Снимок экрана: hello окно нового проекта](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="17100-134">![Screen shot of hello New Project window](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span></span>

4. <span data-ttu-id="17100-135">В hello **обозревателе решений**, щелкните правой кнопкой мыши новое консольное приложение, который находится под управлением решения Visual Studio, и нажмите кнопку **управление пакетами NuGet...**</span><span class="sxs-lookup"><span data-stu-id="17100-135">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Снимок hello справа щелчок меню для проекта hello](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="17100-137">В hello **NuGet** щелкните **Обзор**и тип **documentdb** в поле поиска hello.</span><span class="sxs-lookup"><span data-stu-id="17100-137">In hello **NuGet** tab, click **Browse**, and type **documentdb** in hello search box.</span></span>
<!---stopped here--->
6. <span data-ttu-id="17100-138">В результатах поиска hello, найти **Microsoft.Azure.DocumentDB** и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="17100-138">Within hello results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="17100-139">Идентификатор пакета Hello hello клиентской библиотеки DB Cosmos Azure [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="17100-139">hello package ID for hello Azure Cosmos DB Client Library is [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span></span>
   <span data-ttu-id="17100-140">![Снимок экрана: hello меню NuGet для поиска Azure SDK клиента DB Cosmos](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="17100-140">![Screen shot of hello NuGet Menu for finding Azure Cosmos DB Client SDK](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="17100-141">Если вы получите сообщение о рецензировании решения toohello изменения, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="17100-141">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="17100-142">Если появится сообщение о принятии условий лицензионного соглашения, щелкните **Принимаю**.</span><span class="sxs-lookup"><span data-stu-id="17100-142">If you get a message about license acceptance, click **I accept**.</span></span>

## <span data-ttu-id="17100-143"><a id="Connect"></a>Добавьте ссылки на проект tooyour</span><span class="sxs-lookup"><span data-stu-id="17100-143"><a id="Connect"></a>Add references tooyour project</span></span>
<span data-ttu-id="17100-144">Hello оставшихся шагов этого учебника укажите hello DocumentDB API код фрагменты необходимые toocreate и обновления Azure Cosmos DB ресурсов в проекте.</span><span class="sxs-lookup"><span data-stu-id="17100-144">hello remaining steps in this tutorial provide hello DocumentDB API code snippets required toocreate and update Azure Cosmos DB resources in your project.</span></span>

<span data-ttu-id="17100-145">Во-первых добавьте эти ссылки tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="17100-145">First, add these references tooyour application.</span></span>
<!---These aren't added by default when you install hello pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <span data-ttu-id="17100-146"><a id="add-references"></a>Подключение приложения</span><span class="sxs-lookup"><span data-stu-id="17100-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="17100-147">Добавьте эти две константы и переменную *client* в приложение.</span><span class="sxs-lookup"><span data-stu-id="17100-147">Next, add these two constants and your *client* variable in your application.</span></span>

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

<span data-ttu-id="17100-148">Затем, head обратно toohello [портал Azure](https://portal.azure.com) tooretrieve URL-адрес конечной точки и первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="17100-148">Then, head back toohello [Azure portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="17100-149">URL-адрес конечной точки Hello и первичный ключ, необходимые для вашего приложения toounderstand где tooconnect, а для Azure Cosmos DB tootrust подключения вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="17100-149">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="17100-150">В hello портал Azure, перейдите учетная запись Azure Cosmos DB tooyour, щелкните **ключи**, а затем нажмите кнопку **ключи для чтения и записи**.</span><span class="sxs-lookup"><span data-stu-id="17100-150">In hello Azure portal, navigate tooyour Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span>

<span data-ttu-id="17100-151">Скопируйте hello URI с портала hello и вставьте его через `<your endpoint URL>` в файл program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="17100-151">Copy hello URI from hello portal and paste it over `<your endpoint URL>` in hello program.cs file.</span></span> <span data-ttu-id="17100-152">Затем копирования hello первичный ключ с портала hello и вставьте его поверх `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="17100-152">Then copy hello PRIMARY KEY from hello portal and paste it over `<your primary key>`.</span></span> <span data-ttu-id="17100-153">Быть убедиться, что hello tooremove `<` и `>` из этих значений.</span><span class="sxs-lookup"><span data-stu-id="17100-153">Be sure tooremove hello `<` and `>` from your values.</span></span>

![Снимок экрана: hello портал Azure используется hello NoSQL учебника toocreate консольное приложение C#.](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <span data-ttu-id="17100-156"><a id="instantiate"></a>Создать экземпляр hello DocumentClient</span><span class="sxs-lookup"><span data-stu-id="17100-156"><a id="instantiate"></a>Instantiate hello DocumentClient</span></span>

<span data-ttu-id="17100-157">Теперь создайте новый экземпляр hello **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="17100-157">Now, create a new instance of hello **DocumentClient**.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <span data-ttu-id="17100-158"><a id="create-database"></a>Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="17100-158"><a id="create-database"></a>Create a database</span></span>

<span data-ttu-id="17100-159">Создайте базу данных Azure Cosmos [базы данных](documentdb-resources.md#databases) с помощью hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) метода или [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) метод hello  **DocumentClient** класс из hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="17100-159">Next, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class from hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="17100-160">База данных находится hello логический контейнер для хранения документов JSON, секционированный по коллекциям.</span><span class="sxs-lookup"><span data-stu-id="17100-160">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a><span data-ttu-id="17100-161">Выбор ключа секции</span><span class="sxs-lookup"><span data-stu-id="17100-161">Decide on a partition key</span></span> 

<span data-ttu-id="17100-162">Коллекции — это контейнеры для хранения документов.</span><span class="sxs-lookup"><span data-stu-id="17100-162">Collections are containers for storing documents.</span></span> <span data-ttu-id="17100-163">Они являются логическими ресурсами и [могут включать в себя одну или несколько физических секций](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="17100-163">They are logical resources and can [span one or more physical partitions](partition-data.md).</span></span> <span data-ttu-id="17100-164">Объект [ключ раздела](documentdb-partition-data.md) является свойства (или пути) в документы, используемые toodistribute данных между серверами hello или секций.</span><span class="sxs-lookup"><span data-stu-id="17100-164">A [partition key](documentdb-partition-data.md) is a property (or path) within your documents that is used toodistribute your data among hello servers or partitions.</span></span> <span data-ttu-id="17100-165">Все документы с одинаковым ключом секции хранятся в hello hello одной секции.</span><span class="sxs-lookup"><span data-stu-id="17100-165">All documents with hello same partition key are stored in hello same partition.</span></span> 

<span data-ttu-id="17100-166">Очень важное решение toomake определить ключ раздела, перед тем как создать коллекцию.</span><span class="sxs-lookup"><span data-stu-id="17100-166">Determining a partition key is an important decision toomake before you create a collection.</span></span> <span data-ttu-id="17100-167">Ключи секций представляют собой свойства (или пути) в документах, которые могут быть используемые toodistribute Azure Cosmos DB данных между несколькими серверами или секций.</span><span class="sxs-lookup"><span data-stu-id="17100-167">Partition keys are a property (or path) within your documents that can be used by Azure Cosmos DB toodistribute your data among multiple servers or partitions.</span></span> <span data-ttu-id="17100-168">Cosmos DB хэширует значение ключа секции hello и использует секции hello toodetermine результат hello хэшируются в какой документ toostore hello.</span><span class="sxs-lookup"><span data-stu-id="17100-168">Cosmos DB hashes hello partition key value and uses hello hashed result toodetermine hello partition in which toostore hello document.</span></span> <span data-ttu-id="17100-169">Все документы с одинаковым ключом секции хранятся в hello hello одной секции и ключи разделов нельзя изменять после создания коллекции.</span><span class="sxs-lookup"><span data-stu-id="17100-169">All documents with hello same partition key are stored in hello same partition, and partition keys cannot be changed once a collection is created.</span></span> 

<span data-ttu-id="17100-170">В этом учебнике мы создадим ключ раздела hello tooset слишком`/deviceId` таким образом, hello все данные hello для одного устройства хранится в одной секции.</span><span class="sxs-lookup"><span data-stu-id="17100-170">For this tutorial, we're going tooset hello partition key too`/deviceId` so that hello all hello data for a single device is stored in a single partition.</span></span> <span data-ttu-id="17100-171">Вы хотите toochoose ключа раздела, который имеет большое количество значений, каждое из которых используются в о hello же частотой tooensure Cosmos DB может выполнять балансировку нагрузки при расширении данных, что добиться hello пропускную способность коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="17100-171">You want toochoose a partition key that has a large number of values, each of which are used at about hello same frequency tooensure Cosmos DB can load balance as your data grows and achieve hello full throughput of hello collection.</span></span> 

<span data-ttu-id="17100-172">Дополнительные сведения о секционировании см. в разделе [как toopartition и масштабирования в Azure Cosmos DB?](partition-data.md)</span><span class="sxs-lookup"><span data-stu-id="17100-172">For more information about partitioning, see [How toopartition and scale in Azure Cosmos DB?](partition-data.md)</span></span> 

## <span data-ttu-id="17100-173"><a id="CreateColl"></a>Создание коллекции</span><span class="sxs-lookup"><span data-stu-id="17100-173"><a id="CreateColl"></a>Create a collection</span></span> 

<span data-ttu-id="17100-174">Теперь, когда мы знаем, нашей ключ раздела `/deviceId`, позволяет создавать [коллекции](documentdb-resources.md#collections) с помощью hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) метода или [ CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) метод hello **DocumentClient** класса.</span><span class="sxs-lookup"><span data-stu-id="17100-174">Now that we know our partition key, `/deviceId`, lets create a [collection](documentdb-resources.md#collections) by using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="17100-175">Коллекция представляет собой контейнер документов JSON и любую связанную с ними логику в виде приложения JavaScript.</span><span class="sxs-lookup"><span data-stu-id="17100-175">A collection is a container of JSON documents and any associated JavaScript application logic.</span></span> 

> [!WARNING]
> <span data-ttu-id="17100-176">Создание коллекции имеет цены последствия, как при резервировании пропускной способности для hello toocommunicate приложений с Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="17100-176">Creating a collection has pricing implications, as you are reserving throughput for hello application toocommunicate with Azure Cosmos DB.</span></span> <span data-ttu-id="17100-177">Дополнительные сведения см. на нашей [странице цен](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="17100-177">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

```csharp
// Collection for device telemetry. Here hello JSON property deviceId is used  
// as hello partition key toospread across partitions. Configured for 2500 RU/s  
// throughput and an indexing policy that supports sorting against any  
// number or string property. .
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 2500 });
```

<span data-ttu-id="17100-178">Этот метод делает REST API вызовите tooAzure Cosmos DB и hello Подготовка службы число секций, основанных на запрошенный hello пропускную способность.</span><span class="sxs-lookup"><span data-stu-id="17100-178">This method makes a REST API call tooAzure Cosmos DB, and hello service provisions a number of partitions based on hello requested throughput.</span></span> <span data-ttu-id="17100-179">Пропускная способность hello коллекции можно изменить, как производительность должна развиваться, с помощью пакета SDK для hello или hello [портал Azure](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="17100-179">You can change hello throughput of a collection as your performance needs evolve using hello SDK or hello [Azure portal](set-throughput.md).</span></span>

## <span data-ttu-id="17100-180"><a id="CreateDoc"></a>Создание документов JSON</span><span class="sxs-lookup"><span data-stu-id="17100-180"><a id="CreateDoc"></a>Create JSON documents</span></span>
<span data-ttu-id="17100-181">Вставьте несколько документов JSON в базу данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="17100-181">Let's insert some JSON documents into Azure Cosmos DB.</span></span> <span data-ttu-id="17100-182">Объект [документа](documentdb-resources.md#documents) могут быть созданы с помощью hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) метод hello **DocumentClient** класса.</span><span class="sxs-lookup"><span data-stu-id="17100-182">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="17100-183">Документы относятся к пользовательскому (произвольному) содержимому JSON.</span><span class="sxs-lookup"><span data-stu-id="17100-183">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="17100-184">Этот пример класса содержит чтения устройства и вызова tooCreateDocumentAsync tooinsert новое устройство чтения в коллекцию.</span><span class="sxs-lookup"><span data-stu-id="17100-184">This sample class contains a device reading, and a call tooCreateDocumentAsync tooinsert a new device reading into a collection.</span></span>

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here hello partition key is extracted 
// as "XMS-0001" based on hello collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```
## <a name="read-data"></a><span data-ttu-id="17100-185">Считывание данных</span><span class="sxs-lookup"><span data-stu-id="17100-185">Read data</span></span>

<span data-ttu-id="17100-186">Давайте чтения документа hello вместе с ключом раздела и идентификатор, с помощью метода ReadDocumentAsync hello.</span><span class="sxs-lookup"><span data-stu-id="17100-186">Let's read hello document by its partition key and Id using hello ReadDocumentAsync method.</span></span> <span data-ttu-id="17100-187">Обратите внимание, что операции чтения hello включать значение PartitionKey (соответствующий toohello `x-ms-documentdb-partitionkey` заголовок запроса в hello REST API).</span><span class="sxs-lookup"><span data-stu-id="17100-187">Note that hello reads include a PartitionKey value (corresponding toohello `x-ms-documentdb-partitionkey` request header in hello REST API).</span></span>

```csharp
// Read document. Needs hello partition key and hello Id toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a><span data-ttu-id="17100-188">Обновление данных</span><span class="sxs-lookup"><span data-stu-id="17100-188">Update data</span></span>

<span data-ttu-id="17100-189">Теперь давайте обновление некоторых данных с использованием метода ReplaceDocumentAsync hello.</span><span class="sxs-lookup"><span data-stu-id="17100-189">Now let's update some data using hello ReplaceDocumentAsync method.</span></span>

```csharp
// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a><span data-ttu-id="17100-190">Удаление данных</span><span class="sxs-lookup"><span data-stu-id="17100-190">Delete data</span></span>

<span data-ttu-id="17100-191">Позволяет удалить документа с ключом раздела и идентификатор с помощью метода DeleteDocumentAsync hello.</span><span class="sxs-lookup"><span data-stu-id="17100-191">Now lets delete a document by partition key and id by using hello DeleteDocumentAsync method.</span></span>

```csharp
// Delete a document. hello partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a><span data-ttu-id="17100-192">Запрос секционированных коллекций</span><span class="sxs-lookup"><span data-stu-id="17100-192">Query partitioned collections</span></span>

<span data-ttu-id="17100-193">При запросе данных в секционированных коллекций Azure Cosmos DB автоматически маршруты hello секций toohello запросов соответствующие значения ключа раздела toohello, указанных в фильтре hello (если таковые имеются).</span><span class="sxs-lookup"><span data-stu-id="17100-193">When you query data in partitioned collections, Azure Cosmos DB automatically routes hello query toohello partitions corresponding toohello partition key values specified in hello filter (if there are any).</span></span> <span data-ttu-id="17100-194">Например этот запрос является перенаправленное toojust hello содержащего hello секции ключ раздела «XMS-0001».</span><span class="sxs-lookup"><span data-stu-id="17100-194">For example, this query is routed toojust hello partition containing hello partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="17100-195">Hello следующий запрос не имеет фильтр на ключ секционирования hello (DeviceId) и fanned out tooall секций, где он выполняется для hello секционирования индекса.</span><span class="sxs-lookup"><span data-stu-id="17100-195">hello following query does not have a filter on hello partition key (DeviceId) and is fanned out tooall partitions where it is executed against hello partition's index.</span></span> <span data-ttu-id="17100-196">Обратите внимание, что toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` в hello REST API) toohave hello SDK tooexecute запросов в секциях.</span><span class="sxs-lookup"><span data-stu-id="17100-196">Note that you have toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello REST API) toohave hello SDK tooexecute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a><span data-ttu-id="17100-197">Параллельное выполнение запросов</span><span class="sxs-lookup"><span data-stu-id="17100-197">Parallel query execution</span></span>
<span data-ttu-id="17100-198">Hello Azure пакеты SDK DocumentDB DB Cosmos 1.9.0 и выше поддерживается параметры выполнения параллельных запросов, позволяющих tooperform низкой задержкой запросов в секционированных коллекций даже в том случае, если они должны tootouch большее число секций.</span><span class="sxs-lookup"><span data-stu-id="17100-198">hello Azure Cosmos DB DocumentDB SDKs 1.9.0 and above support parallel query execution options, which allow you tooperform low latency queries against partitioned collections, even when they need tootouch a large number of partitions.</span></span> <span data-ttu-id="17100-199">Например приветствия при следующем запросе является настроенным toorun параллельно в секциях.</span><span class="sxs-lookup"><span data-stu-id="17100-199">For example, hello following query is configured toorun in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="17100-200">Вы можете управлять параллельного выполнения запросов, настроив hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="17100-200">You can manage parallel query execution by tuning hello following parameters:</span></span>

* <span data-ttu-id="17100-201">Установив `MaxDegreeOfParallelism`, можно управлять степенью параллелизма, т. е. hello максимального количества одновременных сетевых подключений toohello коллекцию секций hello.</span><span class="sxs-lookup"><span data-stu-id="17100-201">By setting `MaxDegreeOfParallelism`, you can control hello degree of parallelism i.e., hello maximum number of simultaneous network connections toohello collection's partitions.</span></span> <span data-ttu-id="17100-202">Если присвоить этому слишком 1 hello SDK управляет hello степень параллелизма.</span><span class="sxs-lookup"><span data-stu-id="17100-202">If you set this too-1, hello degree of parallelism is managed by hello SDK.</span></span> <span data-ttu-id="17100-203">Если hello `MaxDegreeOfParallelism` не задан или имеет too0, которое является значением по умолчанию hello, будет коллекции соединений одного сетевого toohello секций.</span><span class="sxs-lookup"><span data-stu-id="17100-203">If hello `MaxDegreeOfParallelism` is not specified or set too0, which is hello default value, there will be a single network connection toohello collection's partitions.</span></span>
* <span data-ttu-id="17100-204">Параметр `MaxBufferedItemCount` обеспечивает баланс между задержкой запросов и использованием памяти на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="17100-204">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="17100-205">Если этот параметр не указан или задайте слишком 1 hello SDK управляет hello количество элементов в буфер во время выполнения параллельных запросов.</span><span class="sxs-lookup"><span data-stu-id="17100-205">If you omit this parameter or set this too-1, hello number of items buffered during parallel query execution is managed by hello SDK.</span></span>

<span data-ttu-id="17100-206">Учитывая hello такое же состояние коллекции hello, параллельный запрос возвращает результаты hello порядок таким же как и последовательного выполнения.</span><span class="sxs-lookup"><span data-stu-id="17100-206">Given hello same state of hello collection, a parallel query will return results in hello same order as in serial execution.</span></span> <span data-ttu-id="17100-207">При выполнении запроса между разделами, включающего Сортировка (ORDER BY и TOP), hello DocumentDB SDK выдает запрос hello параллельно в секциях и выполняет слияние частично отсортированные результаты в hello клиента стороне tooproduce глобально упорядочиваются результаты.</span><span class="sxs-lookup"><span data-stu-id="17100-207">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), hello DocumentDB SDK issues hello query in parallel across partitions and merges partially sorted results in hello client side tooproduce globally ordered results.</span></span>

## <a name="execute-stored-procedures"></a><span data-ttu-id="17100-208">Выполнение хранимых процедур</span><span class="sxs-lookup"><span data-stu-id="17100-208">Execute stored procedures</span></span>
<span data-ttu-id="17100-209">Наконец, можно выполнять атомарные транзакции с документами с hello таким же Идентификатором устройства, например если обслуживание статистических выражений или hello последнее состояние устройств в одном документе, добавив следующий проект tooyour кода hello.</span><span class="sxs-lookup"><span data-stu-id="17100-209">Lastly, you can execute atomic transactions against documents with hello same device ID, e.g. if you're maintaining aggregates or hello latest state of a device in a single document by adding hello following code tooyour project.</span></span>

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

<span data-ttu-id="17100-210">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="17100-210">And that's it!</span></span> <span data-ttu-id="17100-211">Это основные компоненты hello Azure Cosmos DB приложение, использующее масштаб данных секции tooefficiently ключа распределения по секциям.</span><span class="sxs-lookup"><span data-stu-id="17100-211">those are hello main components of an Azure Cosmos DB application that uses a partition key tooefficiently scale data distribution across partitions.</span></span>  

## <a name="clean-up-resources"></a><span data-ttu-id="17100-212">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="17100-212">Clean up resources</span></span>

<span data-ttu-id="17100-213">Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом учебнике в hello портал Azure с hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="17100-213">If you're not going toocontinue toouse this app, delete all resources created by this tutorial in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="17100-214">Hello слева в меню портала Azure hello, пункт **групп ресурсов** и нажмите кнопку hello уникальное имя созданного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="17100-214">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello unique name of hello resource you created.</span></span> 
2. <span data-ttu-id="17100-215">На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="17100-215">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17100-216">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="17100-216">Next steps</span></span>

<span data-ttu-id="17100-217">В этом учебнике вы сделали hello следующее:</span><span class="sxs-lookup"><span data-stu-id="17100-217">In this tutorial, you've done hello following:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="17100-218">создали учетную запись Azure Cosmos DB;</span><span class="sxs-lookup"><span data-stu-id="17100-218">Created an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="17100-219">создали базу данных и коллекцию с ключом секции;</span><span class="sxs-lookup"><span data-stu-id="17100-219">Created a database and collection with a partition key</span></span>
> * <span data-ttu-id="17100-220">создали документы JSON;</span><span class="sxs-lookup"><span data-stu-id="17100-220">Created JSON documents</span></span>
> * <span data-ttu-id="17100-221">обновили документ;</span><span class="sxs-lookup"><span data-stu-id="17100-221">Updated a document</span></span>
> * <span data-ttu-id="17100-222">запросили секционированные коллекции;</span><span class="sxs-lookup"><span data-stu-id="17100-222">Queried partitioned collections</span></span>
> * <span data-ttu-id="17100-223">выполнили хранимую процедуру;</span><span class="sxs-lookup"><span data-stu-id="17100-223">Ran a stored procedure</span></span>
> * <span data-ttu-id="17100-224">удалили документ;</span><span class="sxs-lookup"><span data-stu-id="17100-224">Deleted a document</span></span>
> * <span data-ttu-id="17100-225">удалили базу данных.</span><span class="sxs-lookup"><span data-stu-id="17100-225">Deleted a database</span></span>

<span data-ttu-id="17100-226">Теперь можно продолжить toohello следующее руководство и импортировать учетную запись Cosmos DB tooyour дополнительные данные.</span><span class="sxs-lookup"><span data-stu-id="17100-226">You can now proceed toohello next tutorial and import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="17100-227">Импорт данных в DocumentDB с помощью средства миграции базы данных</span><span class="sxs-lookup"><span data-stu-id="17100-227">Import data into Azure Cosmos DB</span></span>](import-data.md)
