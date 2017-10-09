---
title: "aaaHow toouse поиска Azure из приложения .NET | Документы Microsoft"
description: "Как выполнить поиск Azure toouse из приложения .NET"
services: search
documentationcenter: 
author: brjohnstmsft
manager: jlembicz
editor: 
ms.assetid: 93653341-c05f-4cfd-be45-bb877f964fcb
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 8e13fbe5549547d65941b856ce5a90611261388f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-search-from-a-net-application"></a><span data-ttu-id="3120c-103">Как выполнить поиск Azure toouse из приложения .NET</span><span class="sxs-lookup"><span data-stu-id="3120c-103">How toouse Azure Search from a .NET Application</span></span>
<span data-ttu-id="3120c-104">Эта статья является tooget пошагового руководства вы работающий с hello [пакет SDK Azure Search .NET](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="3120c-104">This article is a walkthrough tooget you up and running with hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span> <span data-ttu-id="3120c-105">Можно использовать .NET SDK tooimplement hello форматированного функции поиска в приложении с помощью поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="3120c-105">You can use hello .NET SDK tooimplement a rich search experience in your application using Azure Search.</span></span>

## <a name="whats-in-hello-azure-search-sdk"></a><span data-ttu-id="3120c-106">Что такое hello поиска Azure SDK</span><span class="sxs-lookup"><span data-stu-id="3120c-106">What's in hello Azure Search SDK</span></span>
<span data-ttu-id="3120c-107">Hello SDK состоит из клиентской библиотеки, `Microsoft.Azure.Search`.</span><span class="sxs-lookup"><span data-stu-id="3120c-107">hello SDK consists of a client library, `Microsoft.Azure.Search`.</span></span> <span data-ttu-id="3120c-108">Он позволяет вам toomanage вашей индексов, источники данных и индексаторы, а также передать управление документами и выполнения запросов, не требуя toodeal с подробными сведениями hello HTTP и JSON.</span><span class="sxs-lookup"><span data-stu-id="3120c-108">It enables you toomanage your indexes, data sources, and indexers, as well as upload and manage documents, and execute queries, all without having toodeal with hello details of HTTP and JSON.</span></span>

<span data-ttu-id="3120c-109">Клиентская библиотека Hello определяет классы, такие как `Index`, `Field`, и `Document`, а также операции, такие как `Indexes.Create` и `Documents.Search` на hello `SearchServiceClient` и `SearchIndexClient` классы.</span><span class="sxs-lookup"><span data-stu-id="3120c-109">hello client library defines classes like `Index`, `Field`, and `Document`, as well as operations like `Indexes.Create` and `Documents.Search` on hello `SearchServiceClient` and `SearchIndexClient` classes.</span></span> <span data-ttu-id="3120c-110">Эти классы организованы в следующие пространства имен hello:</span><span class="sxs-lookup"><span data-stu-id="3120c-110">These classes are organized into hello following namespaces:</span></span>

* [<span data-ttu-id="3120c-111">Microsoft.Azure.Search;</span><span class="sxs-lookup"><span data-stu-id="3120c-111">Microsoft.Azure.Search</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [<span data-ttu-id="3120c-112">Microsoft.Azure.Search.Models</span><span class="sxs-lookup"><span data-stu-id="3120c-112">Microsoft.Azure.Search.Models</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

<span data-ttu-id="3120c-113">Текущая версия Hello hello пакет SDK Azure Search .NET теперь стал общедоступным.</span><span class="sxs-lookup"><span data-stu-id="3120c-113">hello current version of hello Azure Search .NET SDK is now generally available.</span></span> <span data-ttu-id="3120c-114">При желании отзыв tooprovide нам tooincorporate в следующей версии hello, посетите наш [страницу обратной связи](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="3120c-114">If you would like tooprovide feedback for us tooincorporate in hello next version, please visit our [feedback page](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

<span data-ttu-id="3120c-115">Hello .NET SDK поддерживает версию `2016-09-01` из hello [REST API поиска Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="3120c-115">hello .NET SDK supports version `2016-09-01` of hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span> <span data-ttu-id="3120c-116">Эта версия поддерживает пользовательские анализаторы, а также индексаторы больших двоичных объектов Azure и таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="3120c-116">This version now includes support for custom analyzers and Azure Blob and Azure Table indexer support.</span></span> <span data-ttu-id="3120c-117">Предварительный просмотр компонентов, которые являются *не* частью текущей версии, такие как поддержка индексирования JSON и CSV-файлы, находящиеся в [предварительного просмотра](search-api-2015-02-28-preview.md) и доступны через hello старые [2.0 предварительной версии .NET SDK hello ](https://aka.ms/search-sdk-preview).</span><span class="sxs-lookup"><span data-stu-id="3120c-117">Preview features that are *not* part of this version, such as support for indexing JSON and CSV files, are in [preview](search-api-2015-02-28-preview.md) and available via hello older [2.0-preview version of hello .NET SDK](https://aka.ms/search-sdk-preview).</span></span>

<span data-ttu-id="3120c-118">Этот пакет SDK не поддерживает такие [операции управления](https://docs.microsoft.com/rest/api/searchmanagement/), как создание и масштабирование служб поиска или управление ключами API.</span><span class="sxs-lookup"><span data-stu-id="3120c-118">This SDK does not support [Management Operations](https://docs.microsoft.com/rest/api/searchmanagement/) such as creating and scaling Search services and managing API keys.</span></span> <span data-ttu-id="3120c-119">Если вам требуется toomanage поиска ресурсов в приложении .NET, можно использовать hello [пакет SDK Azure Search .NET управления](https://aka.ms/search-mgmt-sdk).</span><span class="sxs-lookup"><span data-stu-id="3120c-119">If you need toomanage your Search resources from a .NET application, you can use hello [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span></span>

## <a name="upgrading-toohello-latest-version-of-hello-sdk"></a><span data-ttu-id="3120c-120">Обновление toohello последнюю версию пакета SDK для hello</span><span class="sxs-lookup"><span data-stu-id="3120c-120">Upgrading toohello latest version of hello SDK</span></span>
<span data-ttu-id="3120c-121">Если вы уже используете более старую версию hello пакет SDK Azure Search .NET и хотелось бы tooupgrade toohello новой общедоступной версии, [в этой статье](search-dotnet-sdk-migration.md) объясняется, каким образом.</span><span class="sxs-lookup"><span data-stu-id="3120c-121">If you're already using an older version of hello Azure Search .NET SDK and you'd like tooupgrade toohello new generally available version, [this article](search-dotnet-sdk-migration.md) explains how.</span></span>

## <a name="requirements-for-hello-sdk"></a><span data-ttu-id="3120c-122">Требования для hello SDK</span><span class="sxs-lookup"><span data-stu-id="3120c-122">Requirements for hello SDK</span></span>
1. <span data-ttu-id="3120c-123">Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="3120c-123">Visual Studio 2017.</span></span>
2. <span data-ttu-id="3120c-124">Ваша личная служба поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="3120c-124">Your own Azure Search service.</span></span> <span data-ttu-id="3120c-125">В порядке toouse hello SDK необходимо будет hello имя службы и один или несколько ключей API.</span><span class="sxs-lookup"><span data-stu-id="3120c-125">In order toouse hello SDK, you will need hello name of your service and one or more API keys.</span></span> <span data-ttu-id="3120c-126">[Создание службы на портале hello](search-create-service-portal.md) поможет вам выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3120c-126">[Create a service in hello portal](search-create-service-portal.md) will help you through these steps.</span></span>
3. <span data-ttu-id="3120c-127">Загрузите пакет SDK Azure Search .NET hello [пакет NuGet](http://www.nuget.org/packages/Microsoft.Azure.Search) с помощью «Управление пакетами NuGet» в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3120c-127">Download hello Azure Search .NET SDK [NuGet package](http://www.nuget.org/packages/Microsoft.Azure.Search) by using "Manage NuGet Packages" in Visual Studio.</span></span> <span data-ttu-id="3120c-128">Просто найти имя пакета hello `Microsoft.Azure.Search` на NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="3120c-128">Just search for hello package name `Microsoft.Azure.Search` on NuGet.org.</span></span>

<span data-ttu-id="3120c-129">Hello пакет SDK Azure Search .NET поддерживает приложения, предназначенные для .NET Framework 4.6 hello и .NET Core.</span><span class="sxs-lookup"><span data-stu-id="3120c-129">hello Azure Search .NET SDK supports applications targeting hello .NET Framework 4.6 and .NET Core.</span></span>

## <a name="core-scenarios"></a><span data-ttu-id="3120c-130">Основные сценарии</span><span class="sxs-lookup"><span data-stu-id="3120c-130">Core scenarios</span></span>
<span data-ttu-id="3120c-131">Существует несколько моментов, которые необходимо toodo в приложении поиска.</span><span class="sxs-lookup"><span data-stu-id="3120c-131">There are several things you'll need toodo in your search application.</span></span> <span data-ttu-id="3120c-132">В данном руководстве мы обсудим эти основные сценарии:</span><span class="sxs-lookup"><span data-stu-id="3120c-132">In this tutorial, we'll cover these core scenarios:</span></span>

* <span data-ttu-id="3120c-133">Создание индекса</span><span class="sxs-lookup"><span data-stu-id="3120c-133">Creating an index</span></span>
* <span data-ttu-id="3120c-134">Заполнение индекса hello с документами</span><span class="sxs-lookup"><span data-stu-id="3120c-134">Populating hello index with documents</span></span>
* <span data-ttu-id="3120c-135">Поиск документов с помощью полнотекстового поиска и фильтров</span><span class="sxs-lookup"><span data-stu-id="3120c-135">Searching for documents using full-text search and filters</span></span>

<span data-ttu-id="3120c-136">Далее образце кода Hello демонстрируется каждый из них.</span><span class="sxs-lookup"><span data-stu-id="3120c-136">hello sample code that follows illustrates each of these.</span></span> <span data-ttu-id="3120c-137">При желании вы свободного toouse фрагменты кода hello в приложении.</span><span class="sxs-lookup"><span data-stu-id="3120c-137">Feel free toouse hello code snippets in your own application.</span></span>

### <a name="overview"></a><span data-ttu-id="3120c-138">Обзор</span><span class="sxs-lookup"><span data-stu-id="3120c-138">Overview</span></span>
<span data-ttu-id="3120c-139">Hello образец приложения, мы будем изучать создает новый индекс с именем «гостиницы» заполняет несколько документов, а затем выполняет некоторые запросы поиска.</span><span class="sxs-lookup"><span data-stu-id="3120c-139">hello sample application we'll be exploring creates a new index named "hotels", populates it with a few documents, then executes some search queries.</span></span> <span data-ttu-id="3120c-140">Вот основной программы hello, показывающая hello Общая последовательность действий:</span><span class="sxs-lookup"><span data-stu-id="3120c-140">Here is hello main program, showing hello overall flow:</span></span>

```csharp
// This sample shows how toodelete, create, upload documents and query an index
static void Main(string[] args)
{
    IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
    IConfigurationRoot configuration = builder.Build();

    SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

    Console.WriteLine("{0}", "Deleting index...\n");
    DeleteHotelsIndexIfExists(serviceClient);

    Console.WriteLine("{0}", "Creating index...\n");
    CreateHotelsIndex(serviceClient);

    ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

    Console.WriteLine("{0}", "Uploading documents...\n");
    UploadDocuments(indexClient);

    ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

    RunQueries(indexClientForQueries);

    Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> <span data-ttu-id="3120c-141">Можно найти hello полный исходный код образца приложения hello, используемые в этом пошагового на [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="3120c-141">You can find hello full source code of hello sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>
> 
>

<span data-ttu-id="3120c-142">Мы рассмотрим ее шаг за шагом.</span><span class="sxs-lookup"><span data-stu-id="3120c-142">We'll walk through this step by step.</span></span> <span data-ttu-id="3120c-143">Сначала мы должны toocreate новый `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="3120c-143">First we need toocreate a new `SearchServiceClient`.</span></span> <span data-ttu-id="3120c-144">Этот объект позволяет toomanage индексов.</span><span class="sxs-lookup"><span data-stu-id="3120c-144">This object allows you toomanage indexes.</span></span> <span data-ttu-id="3120c-145">В порядке tooconstruct один необходим tooprovide имя службы поиска Azure, а также ключ API администратора.</span><span class="sxs-lookup"><span data-stu-id="3120c-145">In order tooconstruct one, you need tooprovide your Azure Search service name as well as an admin API key.</span></span> <span data-ttu-id="3120c-146">Эти сведения можно ввести в hello `appsettings.json` файл hello [образец приложения](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="3120c-146">You can enter this information in hello `appsettings.json` file of hello [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

> [!NOTE]
> <span data-ttu-id="3120c-147">Здравствуйте, если указан неверный ключ (например, запрос ключа, где требовалось ключа администратора), `SearchServiceClient` вызовет `CloudException` с hello ошибки, сообщение «Запрещенных» hello первый раз метод операции, такие как `Indexes.Create`.</span><span class="sxs-lookup"><span data-stu-id="3120c-147">If you provide an incorrect key (for example, a query key where an admin key was required), hello `SearchServiceClient` will throw a `CloudException` with hello error message "Forbidden" hello first time you call an operation method on it, such as `Indexes.Create`.</span></span> <span data-ttu-id="3120c-148">В этом случае tooyou следует внимательно нашей ключ API.</span><span class="sxs-lookup"><span data-stu-id="3120c-148">If this happens tooyou, double-check our API key.</span></span>
> 
> 

<span data-ttu-id="3120c-149">Hello следующие несколько строк вызовите методы toocreate индекс с именем «гостиницы», его удаление сначала, если он уже существует.</span><span class="sxs-lookup"><span data-stu-id="3120c-149">hello next few lines call methods toocreate an index named "hotels", deleting it first if it already exists.</span></span> <span data-ttu-id="3120c-150">Мы рассмотрим эти методы немного позже.</span><span class="sxs-lookup"><span data-stu-id="3120c-150">We will walk through these methods a little later.</span></span>

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

<span data-ttu-id="3120c-151">Далее индекс hello должен toobe заполнено.</span><span class="sxs-lookup"><span data-stu-id="3120c-151">Next, hello index needs toobe populated.</span></span> <span data-ttu-id="3120c-152">toodo, нам нужно будет `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="3120c-152">toodo this, we will need a `SearchIndexClient`.</span></span> <span data-ttu-id="3120c-153">Существует два способа tooobtain одно:, создав его или вызвав `Indexes.GetClient` на hello `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="3120c-153">There are two ways tooobtain one: by constructing it, or by calling `Indexes.GetClient` on hello `SearchServiceClient`.</span></span> <span data-ttu-id="3120c-154">Для удобства мы используем последний hello.</span><span class="sxs-lookup"><span data-stu-id="3120c-154">We use hello latter for convenience.</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="3120c-155">В типичном поисковом приложении управление индексами и заполнение обрабатываются отдельным компонентом из запросов поиска.</span><span class="sxs-lookup"><span data-stu-id="3120c-155">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="3120c-156">`Indexes.GetClient`удобный для заполнения индекса, так как избавляет вас hello проблемы предоставления другой `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="3120c-156">`Indexes.GetClient` is convenient for populating an index because it saves you hello trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="3120c-157">Это делается путем передачи ключа администратора hello, то используется toocreate hello `SearchServiceClient` toohello новый `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="3120c-157">It does this by passing hello admin key that you used toocreate hello `SearchServiceClient` toohello new `SearchIndexClient`.</span></span> <span data-ttu-id="3120c-158">Однако в hello части приложения, которое выполняет запросы, это лучше toocreate hello `SearchIndexClient` напрямую, что можно передавать ключ запроса вместо ключа администратора.</span><span class="sxs-lookup"><span data-stu-id="3120c-158">However, in hello part of your application that executes queries, it is better toocreate hello `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="3120c-159">Это согласуется с hello принципа наименьших прав доступа и поможет toomake более безопасные приложения.</span><span class="sxs-lookup"><span data-stu-id="3120c-159">This is consistent with hello principle of least privilege and will help toomake your application more secure.</span></span> <span data-ttu-id="3120c-160">Дополнительные сведения о ключах администраторов и запросов см. [здесь](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span><span class="sxs-lookup"><span data-stu-id="3120c-160">You can find out more about admin keys and query keys [here](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span></span>
> 
> 

<span data-ttu-id="3120c-161">Теперь, когда у нас есть `SearchIndexClient`, мы можно заполнить индекс hello.</span><span class="sxs-lookup"><span data-stu-id="3120c-161">Now that we have a `SearchIndexClient`, we can populate hello index.</span></span> <span data-ttu-id="3120c-162">Это делает другой метод, который мы рассмотрим позже.</span><span class="sxs-lookup"><span data-stu-id="3120c-162">This is done by another method that we will walk through later.</span></span>

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

<span data-ttu-id="3120c-163">Наконец мы выполните несколько запросов поиска и отображения результатов hello.</span><span class="sxs-lookup"><span data-stu-id="3120c-163">Finally, we execute a few search queries and display hello results.</span></span> <span data-ttu-id="3120c-164">На этот раз мы используем другой метод `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="3120c-164">This time we use a different `SearchIndexClient`:</span></span>

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

<span data-ttu-id="3120c-165">Использовано более подробно рассмотрим hello `RunQueries` метод позже.</span><span class="sxs-lookup"><span data-stu-id="3120c-165">We will take a closer look at hello `RunQueries` method later.</span></span> <span data-ttu-id="3120c-166">Вот новый hello toocreate кода hello `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="3120c-166">Here is hello code toocreate hello new `SearchIndexClient`:</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="3120c-167">Это время, мы используем ключ запроса, так как не требуется доступ на запись toohello индекса.</span><span class="sxs-lookup"><span data-stu-id="3120c-167">This time we use a query key since we do not need write access toohello index.</span></span> <span data-ttu-id="3120c-168">Эти сведения можно ввести в hello `appsettings.json` файл hello [образец приложения](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="3120c-168">You can enter this information in hello `appsettings.json` file of hello [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

<span data-ttu-id="3120c-169">При запуске этого приложения с правильное имя службы и ключи API hello вывод должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3120c-169">If you run this application with a valid service name and API keys, hello output should look like this:</span></span>

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents toobe indexed...
    
    Search hello entire index for hello term 'budget' and return only hello hotelName field:
    
    Name: Roach Motel
    
    Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello hotelId and description:
    
    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river
    
    Search hello entire index, order by a specific field (lastRenovationDate) in descending order, take hello top two results, and show only hotelName and lastRenovationDate:
    
    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00
    
    Search hello entire index for hello term 'motel':
    
    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
    
    Complete.  Press any key tooend application...

<span data-ttu-id="3120c-170">в конце hello в этой статье предоставляется Hello полный исходный код приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3120c-170">hello full source code of hello application is provided at hello end of this article.</span></span>

<span data-ttu-id="3120c-171">Далее будет принимать более подробно рассмотрим каждый из методов hello вызывается `Main`.</span><span class="sxs-lookup"><span data-stu-id="3120c-171">Next, we will take a closer look at each of hello methods called by `Main`.</span></span>

### <a name="creating-an-index"></a><span data-ttu-id="3120c-172">Создание индекса</span><span class="sxs-lookup"><span data-stu-id="3120c-172">Creating an index</span></span>
<span data-ttu-id="3120c-173">После создания `SearchServiceClient`, следующий этап hello `Main` does — delete hello» гостиницы» индекс, если он уже существует.</span><span class="sxs-lookup"><span data-stu-id="3120c-173">After creating a `SearchServiceClient`, hello next thing `Main` does is delete hello "hotels" index if it already exists.</span></span> <span data-ttu-id="3120c-174">Для этого по hello следующий метод:</span><span class="sxs-lookup"><span data-stu-id="3120c-174">That is done by hello following method:</span></span>

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

<span data-ttu-id="3120c-175">Этот метод использует заданный hello `SearchServiceClient` toocheck Если hello индекс уже существует и если да, удалите его.</span><span class="sxs-lookup"><span data-stu-id="3120c-175">This method uses hello given `SearchServiceClient` toocheck if hello index exists, and if so, delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="3120c-176">пример кода Hello в этой статье использует синхронные методы hello hello пакет SDK Azure Search .NET для простоты.</span><span class="sxs-lookup"><span data-stu-id="3120c-176">hello example code in this article uses hello synchronous methods of hello Azure Search .NET SDK for simplicity.</span></span> <span data-ttu-id="3120c-177">Рекомендуется использовать асинхронные методы hello в собственных приложениях tookeep их быстрые и масштабируемые.</span><span class="sxs-lookup"><span data-stu-id="3120c-177">We recommend that you use hello asynchronous methods in your own applications tookeep them scalable and responsive.</span></span> <span data-ttu-id="3120c-178">Например, в hello метод выше использовать `ExistsAsync` и `DeleteAsync` вместо `Exists` и `Delete`.</span><span class="sxs-lookup"><span data-stu-id="3120c-178">For example, in hello method above you could use `ExistsAsync` and `DeleteAsync` instead of `Exists` and `Delete`.</span></span>
> 
> 

<span data-ttu-id="3120c-179">Затем `Main` создает новый индекс hotels, вызывая следующий метод:</span><span class="sxs-lookup"><span data-stu-id="3120c-179">Next, `Main` creates a new "hotels" index by calling this method:</span></span>

```csharp
private static void CreateHotelsIndex(SearchServiceClient serviceClient)
{
    var definition = new Index()
    {
        Name = "hotels",
        Fields = FieldBuilder.BuildForType<Hotel>()
    };

    serviceClient.Indexes.Create(definition);
}
```

<span data-ttu-id="3120c-180">Этот метод создает новый `Index` объекта со списком `Field` объектов, который определяет схему нового индекса hello hello.</span><span class="sxs-lookup"><span data-stu-id="3120c-180">This method creates a new `Index` object with a list of `Field` objects that defines hello schema of hello new index.</span></span> <span data-ttu-id="3120c-181">Каждое поле имеет имя, тип данных и несколько атрибутов, которые определяют его поведение при поиске.</span><span class="sxs-lookup"><span data-stu-id="3120c-181">Each field has a name, data type, and several attributes that define its search behavior.</span></span> <span data-ttu-id="3120c-182">Hello `FieldBuilder` класс использует отражение toocreate список `Field` объектов для hello индекса с помощью проверки hello общие свойства и атрибуты hello заданному `Hotel` класс модели.</span><span class="sxs-lookup"><span data-stu-id="3120c-182">hello `FieldBuilder` class uses reflection toocreate a list of `Field` objects for hello index by examining hello public properties and attributes of hello given `Hotel` model class.</span></span> <span data-ttu-id="3120c-183">Перейти на более подробно рассмотрим hello `Hotel` класса позже.</span><span class="sxs-lookup"><span data-stu-id="3120c-183">We'll take a closer look at hello `Hotel` class later on.</span></span>

> [!NOTE]
> <span data-ttu-id="3120c-184">Всегда можно создать список hello `Field` объекты напрямую, а не с помощью `FieldBuilder` при необходимости.</span><span class="sxs-lookup"><span data-stu-id="3120c-184">You can always create hello list of `Field` objects directly instead of using `FieldBuilder` if needed.</span></span> <span data-ttu-id="3120c-185">Например может потребоваться не toouse класс модели или может потребоваться toouse существующий класс модели, вы не хотите toomodify путем добавления атрибутов.</span><span class="sxs-lookup"><span data-stu-id="3120c-185">For example, you may not want toouse a model class or you may need toouse an existing model class that you don't want toomodify by adding attributes.</span></span>
>
> 

<span data-ttu-id="3120c-186">В дополнение к этому toofields, также добавляются профилей оценки, средств подбора или toohello CORS параметры индекса (они удаляются из образца «hello» для краткости).</span><span class="sxs-lookup"><span data-stu-id="3120c-186">In addition toofields, you can also add scoring profiles, suggesters, or CORS options toohello Index (these are omitted from hello sample for brevity).</span></span> <span data-ttu-id="3120c-187">Дополнительные сведения о hello объекта индекса и ее составных частей можно найти в hello [ссылки на пакет SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), а также в hello [Справочник по REST API поиска Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="3120c-187">You can find more information about hello Index object and its constituent parts in hello [SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), as well as in hello [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

### <a name="populating-hello-index"></a><span data-ttu-id="3120c-188">Заполнение индекса hello</span><span class="sxs-lookup"><span data-stu-id="3120c-188">Populating hello index</span></span>
<span data-ttu-id="3120c-189">следующим шагом Hello в `Main` — индекс вновь созданного toopopulate hello.</span><span class="sxs-lookup"><span data-stu-id="3120c-189">hello next step in `Main` is toopopulate hello newly-created index.</span></span> <span data-ttu-id="3120c-190">Это делается в hello следующий метод:</span><span class="sxs-lookup"><span data-stu-id="3120c-190">This is done in hello following method:</span></span>

```csharp
private static void UploadDocuments(ISearchIndexClient indexClient)
{
    var hotels = new Hotel[]
    {
        new Hotel()
        { 
            HotelId = "1", 
            BaseRate = 199.0, 
            Description = "Best hotel in town",
            DescriptionFr = "Meilleur hôtel en ville",
            HotelName = "Fancy Stay",
            Category = "Luxury", 
            Tags = new[] { "pool", "view", "wifi", "concierge" },
            ParkingIncluded = false, 
            SmokingAllowed = false,
            LastRenovationDate = new DateTimeOffset(2010, 6, 27, 0, 0, 0, TimeSpan.Zero), 
            Rating = 5, 
            Location = GeographyPoint.Create(47.678581, -122.131577)
        },
        new Hotel()
        { 
            HotelId = "2", 
            BaseRate = 79.99,
            Description = "Cheapest hotel in town",
            DescriptionFr = "Hôtel le moins cher en ville",
            HotelName = "Roach Motel",
            Category = "Budget",
            Tags = new[] { "motel", "budget" },
            ParkingIncluded = true,
            SmokingAllowed = true,
            LastRenovationDate = new DateTimeOffset(1982, 4, 28, 0, 0, 0, TimeSpan.Zero),
            Rating = 1,
            Location = GeographyPoint.Create(49.678581, -122.131577)
        },
        new Hotel() 
        { 
            HotelId = "3", 
            BaseRate = 129.99,
            Description = "Close tootown hall and hello river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

    try
    {
        indexClient.Documents.Index(batch);
    }
    catch (IndexBatchException e)
    {
        // Sometimes when your Search service is under load, indexing will fail for some of hello documents in
        // hello batch. Depending on your application, you can take compensating actions like delaying and
        // retrying. For this simple demo, we just log hello failed document keys and continue.
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

    Console.WriteLine("Waiting for documents toobe indexed...\n");
    Thread.Sleep(2000);
}
```

<span data-ttu-id="3120c-191">Этот метод состоит из четырех частей.</span><span class="sxs-lookup"><span data-stu-id="3120c-191">This method has four parts.</span></span> <span data-ttu-id="3120c-192">Hello сначала создает массив из `Hotel` объекты, которые будет использоваться в качестве индекса toohello tooupload входных данных.</span><span class="sxs-lookup"><span data-stu-id="3120c-192">hello first creates an array of `Hotel` objects that will serve as our input data tooupload toohello index.</span></span> <span data-ttu-id="3120c-193">Эти данные жестко запрограммированы для простоты.</span><span class="sxs-lookup"><span data-stu-id="3120c-193">This data is hard-coded for simplicity.</span></span> <span data-ttu-id="3120c-194">В вашем приложении данные скорее всего будут поступать из внешнего источника, например базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="3120c-194">In your own application, your data will likely come from an external data source such as a SQL database.</span></span>

<span data-ttu-id="3120c-195">Вторая часть Hello создает `IndexBatch` содержащую документы hello.</span><span class="sxs-lookup"><span data-stu-id="3120c-195">hello second part creates an `IndexBatch` containing hello documents.</span></span> <span data-ttu-id="3120c-196">Укажите операцию hello требуется tooapply toohello пакета во время hello его создания, в этом случае путем вызова `IndexBatch.Upload`.</span><span class="sxs-lookup"><span data-stu-id="3120c-196">You specify hello operation you want tooapply toohello batch at hello time you create it, in this case by calling `IndexBatch.Upload`.</span></span> <span data-ttu-id="3120c-197">Hello пакета происходит, то переданные toohello поиска Azure индекс по hello `Documents.Index` метод.</span><span class="sxs-lookup"><span data-stu-id="3120c-197">hello batch is then uploaded toohello Azure Search index by hello `Documents.Index` method.</span></span>

> [!NOTE]
> <span data-ttu-id="3120c-198">В этом примере мы просто отправляем документы.</span><span class="sxs-lookup"><span data-stu-id="3120c-198">In this example, we are just uploading documents.</span></span> <span data-ttu-id="3120c-199">Если требуется toomerge изменения в существующих документов или удаления документов, можно создать путем вызова пакетов `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, или `IndexBatch.Delete` вместо него.</span><span class="sxs-lookup"><span data-stu-id="3120c-199">If you wanted toomerge changes into existing documents or delete documents, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete` instead.</span></span> <span data-ttu-id="3120c-200">Вы можете сочетать различные операции в одном пакете, вызвав `IndexBatch.New`, который принимает коллекцию `IndexAction` объектов, каждый из которых указывает tooperform поиска Azure конкретной операции в документе.</span><span class="sxs-lookup"><span data-stu-id="3120c-200">You can also mix different operations in a single batch by calling `IndexBatch.New`, which takes a collection of `IndexAction` objects, each of which tells Azure Search tooperform a particular operation on a document.</span></span> <span data-ttu-id="3120c-201">Можно создать каждый `IndexAction` с отдельной операции путем вызова соответствующего метода hello, например `IndexAction.Merge`, `IndexAction.Upload`, и т. д.</span><span class="sxs-lookup"><span data-stu-id="3120c-201">You can create each `IndexAction` with its own operation by calling hello corresponding method such as `IndexAction.Merge`, `IndexAction.Upload`, and so on.</span></span>
> 
> 

<span data-ttu-id="3120c-202">Третья часть Hello этого метода является блок catch, который обрабатывает важные ошибки для индексирования.</span><span class="sxs-lookup"><span data-stu-id="3120c-202">hello third part of this method is a catch block that handles an important error case for indexing.</span></span> <span data-ttu-id="3120c-203">Службе поиска Azure в случае некоторые hello документов в пакете hello tooindex `IndexBatchException` вызванное `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="3120c-203">If your Azure Search service fails tooindex some of hello documents in hello batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="3120c-204">Это может произойти, если вы индексируете документы службы при интенсивной нагрузке.</span><span class="sxs-lookup"><span data-stu-id="3120c-204">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="3120c-205">**Настоятельно рекомендуется явно обрабатывать этот случай в коде.**</span><span class="sxs-lookup"><span data-stu-id="3120c-205">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="3120c-206">Можно отложить и повторите попытку индексирования отказавших документов hello или пользователь может входить и продолжить как образец hello работает, можно сделать что-нибудь другое в зависимости от требований к согласованности данных приложения.</span><span class="sxs-lookup"><span data-stu-id="3120c-206">You can delay and then retry indexing hello documents that failed, or you can log and continue like hello sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="3120c-207">Можно использовать hello `FindFailedActionsToRetry` tooconstruct метод новый пакет, содержащий только hello действия, которые не удалось выполнить в предыдущем вызове слишком`Index`.</span><span class="sxs-lookup"><span data-stu-id="3120c-207">You can use hello `FindFailedActionsToRetry` method tooconstruct a new batch containing only hello actions that failed in a previous call too`Index`.</span></span> <span data-ttu-id="3120c-208">метод Hello задокументирован [здесь](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) и обсуждение tooproperly его использовании [на StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span><span class="sxs-lookup"><span data-stu-id="3120c-208">hello method is documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) and there is a discussion of how tooproperly use it [on StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span></span>
>
>

<span data-ttu-id="3120c-209">Здравствуйте, и, наконец, `UploadDocuments` метод задержки для двух секунд.</span><span class="sxs-lookup"><span data-stu-id="3120c-209">Finally, hello `UploadDocuments` method delays for two seconds.</span></span> <span data-ttu-id="3120c-210">Индексирование работает асинхронно в службе поиска Azure, поэтому пример приложения hello должен toowait tooensure короткое время, что hello документы доступны для поиска.</span><span class="sxs-lookup"><span data-stu-id="3120c-210">Indexing happens asynchronously in your Azure Search service, so hello sample application needs toowait a short time tooensure that hello documents are available for searching.</span></span> <span data-ttu-id="3120c-211">Такие задержки обычно необходимы только в демонстрациях, тестах и примерах приложений.</span><span class="sxs-lookup"><span data-stu-id="3120c-211">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

#### <a name="how-hello-net-sdk-handles-documents"></a><span data-ttu-id="3120c-212">Как hello пакета SDK для .NET обрабатывает документы</span><span class="sxs-lookup"><span data-stu-id="3120c-212">How hello .NET SDK handles documents</span></span>
<span data-ttu-id="3120c-213">Может возникнуть вопрос как hello пакет SDK Azure Search .NET — может tooupload экземпляры класса определяемого пользователем как `Hotel` toohello индекса.</span><span class="sxs-lookup"><span data-stu-id="3120c-213">You may be wondering how hello Azure Search .NET SDK is able tooupload instances of a user-defined class like `Hotel` toohello index.</span></span> <span data-ttu-id="3120c-214">toohelp ответа на этот вопрос, давайте взглянем на hello `Hotel` класса:</span><span class="sxs-lookup"><span data-stu-id="3120c-214">toohelp answer that question, let's look at hello `Hotel` class:</span></span>

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// hello SerializePropertyNamesAsCamelCase attribute is defined in hello Azure Search .NET SDK.
// It ensures that Pascal-case property names in hello model class are mapped toocamel-case
// field names in hello index.
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [System.ComponentModel.DataAnnotations.Key]
    [IsFilterable]
    public string HotelId { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public double? BaseRate { get; set; }

    [IsSearchable]
    public string Description { get; set; }

    [IsSearchable]
    [Analyzer(AnalyzerName.AsString.FrLucene)]
    [JsonProperty("description_fr")]
    public string DescriptionFr { get; set; }

    [IsSearchable, IsFilterable, IsSortable]
    public string HotelName { get; set; }

    [IsSearchable, IsFilterable, IsSortable, IsFacetable]
    public string Category { get; set; }

    [IsSearchable, IsFilterable, IsFacetable]
    public string[] Tags { get; set; }

    [IsFilterable, IsFacetable]
    public bool? ParkingIncluded { get; set; }

    [IsFilterable, IsFacetable]
    public bool? SmokingAllowed { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public DateTimeOffset? LastRenovationDate { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public int? Rating { get; set; }

    [IsFilterable, IsSortable]
    public GeographyPoint Location { get; set; }
}
```

<span data-ttu-id="3120c-215">Hello первое, что toonotice является, каждое общее свойство `Hotel` соответствует tooa поля в определение индекса hello, но с одним ключевым отличием: hello имя каждого поля начинается с букв нижнего регистра («верблюжий»), тогда hello имя каждого открытых Свойство `Hotel` начинается с буквы верхнего регистра («стиле Pascal»).</span><span class="sxs-lookup"><span data-stu-id="3120c-215">hello first thing toonotice is that each public property of `Hotel` corresponds tooa field in hello index definition, but with one crucial difference: hello name of each field starts with a lower-case letter ("camel case"), while hello name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="3120c-216">Это распространенный сценарий в приложениях .NET и выполнить привязку данных, где управление внешними hello разработчик приложения hello hello целевой схемы.</span><span class="sxs-lookup"><span data-stu-id="3120c-216">This is a common scenario in .NET applications that perform data-binding where hello target schema is outside hello control of hello application developer.</span></span> <span data-ttu-id="3120c-217">Вместо того чтобы использовать .NET hello tooviolate правила именования, делая прописной имена свойств, чтобы узнать hello SDK toomap hello свойство имена toocamel регистре автоматически с помощью hello `[SerializePropertyNamesAsCamelCase]` атрибута.</span><span class="sxs-lookup"><span data-stu-id="3120c-217">Rather than having tooviolate hello .NET naming guidelines by making property names camel-case, you can tell hello SDK toomap hello property names toocamel-case automatically with hello `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="3120c-218">пакет SDK Azure Search .NET Hello использует hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize библиотеки и десериализации tooand объектов в пользовательскую модель из JSON.</span><span class="sxs-lookup"><span data-stu-id="3120c-218">hello Azure Search .NET SDK uses hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library tooserialize and deserialize your custom model objects tooand from JSON.</span></span> <span data-ttu-id="3120c-219">При необходимости эту сериализацию можно настроить.</span><span class="sxs-lookup"><span data-stu-id="3120c-219">You can customize this serialization if needed.</span></span> <span data-ttu-id="3120c-220">Дополнительные сведения см. в разделе [Пользовательская сериализация с помощью JSON.NET](#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="3120c-220">For more details, see [Custom Serialization with JSON.NET](#JsonDotNet).</span></span>
> 
> 

<span data-ttu-id="3120c-221">Hello второй toonotice самое являются hello атрибутами, такими как `IsFilterable`, `IsSearchable`, `Key`, и `Analyzer` , добавьте каждое открытое свойство.</span><span class="sxs-lookup"><span data-stu-id="3120c-221">hello second thing toonotice are hello attributes such as `IsFilterable`, `IsSearchable`, `Key`, and `Analyzer` that decorate each public property.</span></span> <span data-ttu-id="3120c-222">Эти атрибуты непосредственно сопоставляются toohello [соответствующих атрибутов индекс поиска Azure hello](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span><span class="sxs-lookup"><span data-stu-id="3120c-222">These attributes map directly toohello [corresponding attributes of hello Azure Search index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span></span> <span data-ttu-id="3120c-223">Hello `FieldBuilder` класс использует эти определения полей tooconstruct для индекса hello.</span><span class="sxs-lookup"><span data-stu-id="3120c-223">hello `FieldBuilder` class uses these tooconstruct field definitions for hello index.</span></span>

<span data-ttu-id="3120c-224">Hello третий важным преимуществом hello `Hotel` класса являются типами данных hello hello открытые свойства.</span><span class="sxs-lookup"><span data-stu-id="3120c-224">hello third important thing about hello `Hotel` class are hello data types of hello public properties.</span></span> <span data-ttu-id="3120c-225">типы tootheir эквивалент полей в определение индекса hello сопоставление типов Hello из этих свойств.</span><span class="sxs-lookup"><span data-stu-id="3120c-225">hello .NET types of  these properties map tootheir equivalent field types in hello index definition.</span></span> <span data-ttu-id="3120c-226">Здравствуйте, например, `Category` строковое свойство сопоставляется toohello `category` поле, которое относится к типу `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="3120c-226">For example, hello `Category` string property maps toohello `category` field, which is of type `Edm.String`.</span></span> <span data-ttu-id="3120c-227">Существуют аналогичные сопоставление типов между `bool?` и `Edm.Boolean`, `DateTimeOffset?` и `Edm.DateTimeOffset`, т. д. hello определенные правила для сопоставления типа hello описаны с hello `Documents.Get` метод в hello [пакет SDK Azure Search .NET Справочник по](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="3120c-227">There are similar type mappings between `bool?` and `Edm.Boolean`, `DateTimeOffset?` and `Edm.DateTimeOffset`, etc. hello specific rules for hello type mapping are documented with hello `Documents.Get` method in hello [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span> <span data-ttu-id="3120c-228">Hello `FieldBuilder` класс берет на себя такое сопоставление для вас, но может оказаться полезным toounderstand на случай необходимости tootroubleshoot проблемы сериализации.</span><span class="sxs-lookup"><span data-stu-id="3120c-228">hello `FieldBuilder` class takes care of this mapping for you, but it can still be helpful toounderstand in case you need tootroubleshoot any serialization issues.</span></span>

<span data-ttu-id="3120c-229">Это возможность toouse собственные классы как документы работает в обоих направлениях; Можно также получать результаты поиска и hello SDK автоматически выполнить десериализацию их tooa типа по своему усмотрению, как будет показано в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="3120c-229">This ability toouse your own classes as documents works in both directions; You can also retrieve search results and have hello SDK automatically deserialize them tooa type of your choice, as we will see in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="3120c-230">пакет SDK Azure Search .NET Hello также поддерживает динамически типизированные документы с помощью hello `Document` класс, который представляет собой сопоставление значений toofield имена полей ключ значение.</span><span class="sxs-lookup"><span data-stu-id="3120c-230">hello Azure Search .NET SDK also supports dynamically-typed documents using hello `Document` class, which is a key/value mapping of field names toofield values.</span></span> <span data-ttu-id="3120c-231">Это полезно в сценариях, которых вы не знаете hello схемы индекса во время разработки, или было бы неудобно toobind toospecific модель классов.</span><span class="sxs-lookup"><span data-stu-id="3120c-231">This is useful in scenarios where you don't know hello index schema at design-time, or where it would be inconvenient toobind toospecific model classes.</span></span> <span data-ttu-id="3120c-232">Все методы hello hello SDK, обрабатывающих документы имеют перегрузки, которые работают с hello `Document` класса, а также строго типизированных перегрузки, принимающие параметр универсального типа.</span><span class="sxs-lookup"><span data-stu-id="3120c-232">All hello methods in hello SDK that deal with documents have overloads that work with hello `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="3120c-233">Последний hello используются в примере кода hello в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="3120c-233">Only hello latter are used in hello sample code in this tutorial.</span></span> <span data-ttu-id="3120c-234">Hello `Document` класс наследует от `Dictionary<string, object>`.</span><span class="sxs-lookup"><span data-stu-id="3120c-234">hello `Document` class inherits from `Dictionary<string, object>`.</span></span> <span data-ttu-id="3120c-235">Дополнительные сведения см. [здесь](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span><span class="sxs-lookup"><span data-stu-id="3120c-235">You can find other details [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span></span>
> 
> 

<span data-ttu-id="3120c-236">**Почему следует использовать типы данных, допускающие значение NULL**</span><span class="sxs-lookup"><span data-stu-id="3120c-236">**Why you should use nullable data types**</span></span>

<span data-ttu-id="3120c-237">При разработке собственных индекс поиска Azure классы toomap модели tooan, мы рекомендуем, например, объявление свойств типов значений `bool` и `int` toobe допускает значение NULL (например, `bool?` вместо `bool`).</span><span class="sxs-lookup"><span data-stu-id="3120c-237">When designing your own model classes toomap tooan Azure Search index, we recommend declaring properties of value types such as `bool` and `int` toobe nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="3120c-238">При использовании свойство не допускающим имеется слишком**гарантирует** что документов в индексе не будет содержать значение null для соответствующего поля hello.</span><span class="sxs-lookup"><span data-stu-id="3120c-238">If you use a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="3120c-239">Hello SDK ни hello службы поиска Azure поможет вам tooenforce это.</span><span class="sxs-lookup"><span data-stu-id="3120c-239">Neither hello SDK nor hello Azure Search service will help you tooenforce this.</span></span>

<span data-ttu-id="3120c-240">Это не относится только к гипотетической: представьте себе ситуацию, когда Добавление нового поля tooan существующего индекса, тип которого `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="3120c-240">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="3120c-241">После обновления определения индекса hello, все документы будет иметь значение null для этого нового поля (поскольку все типы допускают значение NULL, если в службе поиска Azure).</span><span class="sxs-lookup"><span data-stu-id="3120c-241">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="3120c-242">При использовании модели с запретом `int` свойства для этого поля, вы получите `JsonSerializationException` при попытке документы tooretrieve следующим образом:</span><span class="sxs-lookup"><span data-stu-id="3120c-242">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="3120c-243">По этой причине по-прежнему рекомендуется использовать типы, допускающие значения NULL, в классах модели.</span><span class="sxs-lookup"><span data-stu-id="3120c-243">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a><span data-ttu-id="3120c-244">Пользовательская сериализация с помощью JSON.NET</span><span class="sxs-lookup"><span data-stu-id="3120c-244">Custom Serialization with JSON.NET</span></span>
<span data-ttu-id="3120c-245">Hello SDK использует JSON.NET для сериализации и десериализации документов.</span><span class="sxs-lookup"><span data-stu-id="3120c-245">hello SDK uses JSON.NET for serializing and deserializing documents.</span></span> <span data-ttu-id="3120c-246">Можно настроить сериализацию и десериализацию при необходимости путем определения собственных `JsonConverter` или `IContractResolver` (в разделе hello [JSON.NET документации](http://www.newtonsoft.com/json/help/html/Introduction.htm) для получения дополнительных сведений).</span><span class="sxs-lookup"><span data-stu-id="3120c-246">You can customize serialization and deserialization if needed by defining your own `JsonConverter` or `IContractResolver` (see hello [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) for more details).</span></span> <span data-ttu-id="3120c-247">Это может быть полезным при необходимости tooadapt существующий класс модели из приложения для использования с поиска Azure и других более сложных сценариев.</span><span class="sxs-lookup"><span data-stu-id="3120c-247">This can be useful when you want tooadapt an existing model class from your application for use with Azure Search, and other more advanced scenarios.</span></span> <span data-ttu-id="3120c-248">Например, с помощью пользовательской сериализации можно делать следующее.</span><span class="sxs-lookup"><span data-stu-id="3120c-248">For example, with custom serialization you can:</span></span>

* <span data-ttu-id="3120c-249">Включить или исключить определенные свойства класса модели с сохранением в виде поля документа.</span><span class="sxs-lookup"><span data-stu-id="3120c-249">Include or exclude certain properties of your model class from being stored as document fields.</span></span>
* <span data-ttu-id="3120c-250">Реализовать сопоставление между именами свойств в коде и именами полей в индексе.</span><span class="sxs-lookup"><span data-stu-id="3120c-250">Map between property names in your code and field names in your index.</span></span>
* <span data-ttu-id="3120c-251">Создание настраиваемых атрибутов, которые могут использоваться для сопоставления полей toodocument свойств.</span><span class="sxs-lookup"><span data-stu-id="3120c-251">Create custom attributes that can be used for mapping properties toodocument fields.</span></span>

<span data-ttu-id="3120c-252">Можно найти примеры реализации пользовательской сериализации в hello модульных тестов для hello пакет SDK Azure Search .NET, на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="3120c-252">You can find examples of implementing custom serialization in hello unit tests for hello Azure Search .NET SDK on GitHub.</span></span> <span data-ttu-id="3120c-253">Хорошей отправной точкой будет [эта папка](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span><span class="sxs-lookup"><span data-stu-id="3120c-253">A good starting point is [this folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span></span> <span data-ttu-id="3120c-254">Он содержит классы, используемые с пользовательской сериализации тестов hello.</span><span class="sxs-lookup"><span data-stu-id="3120c-254">It contains classes that are used by hello custom serialization tests.</span></span>

### <a name="searching-for-documents-in-hello-index"></a><span data-ttu-id="3120c-255">Поиск документов в индексе hello</span><span class="sxs-lookup"><span data-stu-id="3120c-255">Searching for documents in hello index</span></span>
<span data-ttu-id="3120c-256">Последний шаг Hello в пример приложения hello — toosearch для некоторых документов в индексе hello.</span><span class="sxs-lookup"><span data-stu-id="3120c-256">hello last step in hello sample application is toosearch for some documents in hello index.</span></span> <span data-ttu-id="3120c-257">Следующий метод Hello делает это:</span><span class="sxs-lookup"><span data-stu-id="3120c-257">hello following method does this:</span></span>

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
    SearchParameters parameters;
    DocumentSearchResult<Hotel> results;

    Console.WriteLine("Search hello entire index for hello term 'budget' and return only hello hotelName field:\n");

    parameters =
        new SearchParameters()
        {
            Select = new[] { "hotelName" }
        };

    results = indexClient.Documents.Search<Hotel>("budget", parameters);

    WriteDocuments(results);

    Console.Write("Apply a filter toohello index toofind hotels cheaper than $150 per night, ");
    Console.WriteLine("and return hello hotelId and description:\n");

    parameters =
        new SearchParameters()
        {
            Filter = "baseRate lt 150",
            Select = new[] { "hotelId", "description" }
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.Write("Search hello entire index, order by a specific field (lastRenovationDate) ");
    Console.Write("in descending order, take hello top two results, and show only hotelName and ");
    Console.WriteLine("lastRenovationDate:\n");

    parameters =
        new SearchParameters()
        {
            OrderBy = new[] { "lastRenovationDate desc" },
            Select = new[] { "hotelName", "lastRenovationDate" },
            Top = 2
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.WriteLine("Search hello entire index for hello term 'motel':\n");

    parameters = new SearchParameters();
    results = indexClient.Documents.Search<Hotel>("motel", parameters);

    WriteDocuments(results);
}
```

<span data-ttu-id="3120c-258">При каждом выполнении запроса этот метод прежде всего создает объект `SearchParameters`.</span><span class="sxs-lookup"><span data-stu-id="3120c-258">Each time it executes a query, this method first creates a new `SearchParameters` object.</span></span> <span data-ttu-id="3120c-259">Это используется toospecify Дополнительные параметры для запроса hello, таких как сортировка, фильтрация, разбиение на страницы и аспекты.</span><span class="sxs-lookup"><span data-stu-id="3120c-259">This is used toospecify additional options for hello query such as sorting, filtering, paging, and faceting.</span></span> <span data-ttu-id="3120c-260">В этом методе задаются значения hello `Filter`, `Select`, `OrderBy`, и `Top` свойство для различных запросов.</span><span class="sxs-lookup"><span data-stu-id="3120c-260">In this method, we're setting hello `Filter`, `Select`, `OrderBy`, and `Top` property for different queries.</span></span> <span data-ttu-id="3120c-261">Все hello `SearchParameters` свойства документируются [здесь](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span><span class="sxs-lookup"><span data-stu-id="3120c-261">All hello `SearchParameters` properties are documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span></span>

<span data-ttu-id="3120c-262">Hello следующим шагом является tooactually выполнение hello поискового запроса.</span><span class="sxs-lookup"><span data-stu-id="3120c-262">hello next step is tooactually execute hello search query.</span></span> <span data-ttu-id="3120c-263">Это делается с помощью hello `Documents.Search` метод.</span><span class="sxs-lookup"><span data-stu-id="3120c-263">This is done using hello `Documents.Search` method.</span></span> <span data-ttu-id="3120c-264">Для каждого запроса toouse текст hello поиска передается как строка (или `"*"` при отсутствии поиска текста), плюс hello созданную ранее параметров поиска.</span><span class="sxs-lookup"><span data-stu-id="3120c-264">For each query, we pass hello search text toouse as a string (or `"*"` if there is no search text), plus hello search parameters created earlier.</span></span> <span data-ttu-id="3120c-265">Также укажите `Hotel` как параметр типа hello для `Documents.Search`, который сообщает hello SDK toodeserialize документов в результатах поиска hello в объекты типа `Hotel`.</span><span class="sxs-lookup"><span data-stu-id="3120c-265">We also specify `Hotel` as hello type parameter for `Documents.Search`, which tells hello SDK toodeserialize documents in hello search results into objects of type `Hotel`.</span></span>

> [!NOTE]
> <span data-ttu-id="3120c-266">Можно найти дополнительные сведения о синтаксисе выражений запросов поиска hello [здесь](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="3120c-266">You can find more information about hello search query expression syntax [here](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span></span>
> 
> 

<span data-ttu-id="3120c-267">Наконец после каждого запроса этот метод выполняет перебор всех hello совпадений в результатах поиска hello, печать каждой консоли toohello документа:</span><span class="sxs-lookup"><span data-stu-id="3120c-267">Finally, after each query this method iterates through all hello matches in hello search results, printing each document toohello console:</span></span>

```csharp
private static void WriteDocuments(DocumentSearchResult<Hotel> searchResults)
{
    foreach (SearchResult<Hotel> result in searchResults.Results)
    {
        Console.WriteLine(result.Document);
    }

    Console.WriteLine();
}
```

<span data-ttu-id="3120c-268">Давайте более подробно рассмотрим hello запросы, в свою очередь.</span><span class="sxs-lookup"><span data-stu-id="3120c-268">Let's take a closer look at each of hello queries in turn.</span></span> <span data-ttu-id="3120c-269">Вот первый запрос tooexecute кода hello hello.</span><span class="sxs-lookup"><span data-stu-id="3120c-269">Here is hello code tooexecute hello first query:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

<span data-ttu-id="3120c-270">В этом случае мы ищем гостиницы, слово hello «бюджет», и мы хотим tooget обратно только hello гостиницы имен, определяемое параметром hello `Select` параметра.</span><span class="sxs-lookup"><span data-stu-id="3120c-270">In this case, we're searching for hotels that match hello word "budget", and we want tooget back only hello hotel names, as specified by hello `Select` parameter.</span></span> <span data-ttu-id="3120c-271">Ниже приведены результаты hello.</span><span class="sxs-lookup"><span data-stu-id="3120c-271">Here are hello results:</span></span>

    Name: Roach Motel

<span data-ttu-id="3120c-272">Далее мы toofind hello гостиницы с частотой не более 150 каждую ночь и вернуть только hello гостиницы Идентификатором и описанием:</span><span class="sxs-lookup"><span data-stu-id="3120c-272">Next, we want toofind hello hotels with a nightly rate of less than $150, and return only hello hotel ID and description:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

<span data-ttu-id="3120c-273">Этот запрос использует OData `$filter` выражение, `baseRate lt 150`, toofilter hello документов в индексе hello.</span><span class="sxs-lookup"><span data-stu-id="3120c-273">This query uses an OData `$filter` expression, `baseRate lt 150`, toofilter hello documents in hello index.</span></span> <span data-ttu-id="3120c-274">Дополнительные сведения о hello синтаксис OData, поддерживающего поиск Azure можно найти [здесь](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="3120c-274">You can find out more about hello OData syntax that Azure Search supports [here](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span></span>

<span data-ttu-id="3120c-275">Ниже приведены результаты hello hello запроса.</span><span class="sxs-lookup"><span data-stu-id="3120c-275">Here are hello results of hello query:</span></span>

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river

<span data-ttu-id="3120c-276">Далее мы хотим toofind hello top два гостиницы, недавно отремонтированных и показывать название отеля hello и Дата последней модернизации.</span><span class="sxs-lookup"><span data-stu-id="3120c-276">Next, we want toofind hello top two hotels that have been most recently renovated, and show hello hotel name and last renovation date.</span></span> <span data-ttu-id="3120c-277">Ниже приведен код hello.</span><span class="sxs-lookup"><span data-stu-id="3120c-277">Here is hello code:</span></span> 

```csharp
parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

<span data-ttu-id="3120c-278">В этом случае мы снова использовать hello toospecify синтаксис OData `OrderBy` параметр как `lastRenovationDate desc`.</span><span class="sxs-lookup"><span data-stu-id="3120c-278">In this case, we again use OData syntax toospecify hello `OrderBy` parameter as `lastRenovationDate desc`.</span></span> <span data-ttu-id="3120c-279">Мы также настроить `Top` too2 tooensure мы получить только первые две документы hello.</span><span class="sxs-lookup"><span data-stu-id="3120c-279">We also set `Top` too2 tooensure we only get hello top two documents.</span></span> <span data-ttu-id="3120c-280">Как и прежде, мы устанавливаем `Select` toospecify, какие поля должны быть возвращены.</span><span class="sxs-lookup"><span data-stu-id="3120c-280">As before, we set `Select` toospecify which fields should be returned.</span></span>

<span data-ttu-id="3120c-281">Ниже приведены результаты hello.</span><span class="sxs-lookup"><span data-stu-id="3120c-281">Here are hello results:</span></span>

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

<span data-ttu-id="3120c-282">Наконец мы хотим toofind все гостиницы, слово hello «motel»:</span><span class="sxs-lookup"><span data-stu-id="3120c-282">Finally, we want toofind all hotels that match hello word "motel":</span></span>

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

<span data-ttu-id="3120c-283">А вот hello результатов, которые включают все поля, поскольку не был указан hello `Select` свойство:</span><span class="sxs-lookup"><span data-stu-id="3120c-283">And here are hello results, which include all fields since we did not specify hello `Select` property:</span></span>

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

<span data-ttu-id="3120c-284">Этот шаг завершает учебник hello, но не останавливает здесь.</span><span class="sxs-lookup"><span data-stu-id="3120c-284">This step completes hello tutorial, but don't stop here.</span></span> <span data-ttu-id="3120c-285">**Дальнейшие действия** представлены дополнительные материалы о Поиске Azure.</span><span class="sxs-lookup"><span data-stu-id="3120c-285">**Next steps** provides additional resources for learning more about Azure Search.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3120c-286">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3120c-286">Next steps</span></span>
* <span data-ttu-id="3120c-287">Обзор hello ссылки для hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) и [API-интерфейса REST](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="3120c-287">Browse hello references for hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
* <span data-ttu-id="3120c-288">Дополнительные сведения можно получить из [видео, а также других примеров и руководств](search-video-demo-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="3120c-288">Deepen your knowledge through [videos and other samples and tutorials](search-video-demo-tutorial-list.md).</span></span>
* <span data-ttu-id="3120c-289">Просмотрите [соглашения об именовании](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn hello правила выбора имен для различных объектов.</span><span class="sxs-lookup"><span data-stu-id="3120c-289">Review [naming conventions](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn hello rules for naming various objects.</span></span>
* <span data-ttu-id="3120c-290">Изучите [поддерживаемые типы данных](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) в службе поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="3120c-290">Review [supported data types](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span></span>
