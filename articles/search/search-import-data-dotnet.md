---
title: "AAA» передачи данных (.NET - поиска Azure) | Документы Microsoft»"
description: "Узнайте, как индекс tooan tooupload данных в поиске Azure с помощью hello .NET SDK."
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: 
ms.assetid: 0e0e7e7b-7178-4c26-95c6-2fd1e8015aca
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/13/2017
ms.author: brjohnst
ms.openlocfilehash: 78ddbefb522884d1f61cb275c25c091487aee639
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-net-sdk"></a><span data-ttu-id="40a55-103">Здравствуйте, передачи данных tooAzure поиска с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="40a55-103">Upload data tooAzure Search using hello .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="40a55-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="40a55-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="40a55-105">.NET</span><span class="sxs-lookup"><span data-stu-id="40a55-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="40a55-106">REST</span><span class="sxs-lookup"><span data-stu-id="40a55-106">REST</span></span>](search-import-data-rest-api.md)
> 
> 

<span data-ttu-id="40a55-107">В этой статье будет показано, как toouse hello [пакет SDK Azure Search .NET](https://aka.ms/search-sdk) tooimport данных в индекс поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="40a55-107">This article will show you how toouse hello [Azure Search .NET SDK](https://aka.ms/search-sdk) tooimport data into an Azure Search index.</span></span>

<span data-ttu-id="40a55-108">Прежде чем приступать к выполнению инструкций из этого руководства, вам нужно [создать индекс службы поиска Azure](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="40a55-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span> <span data-ttu-id="40a55-109">В этой статье также предполагается, что вы уже создали `SearchServiceClient` объекта, как показано в [создать индекс поиска Azure с помощью hello .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span><span class="sxs-lookup"><span data-stu-id="40a55-109">This article also assumes that you have already created a `SearchServiceClient` object, as shown in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span></span>

> [!NOTE]
> <span data-ttu-id="40a55-110">Все приведенные здесь примеры кода написаны на языке C#.</span><span class="sxs-lookup"><span data-stu-id="40a55-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="40a55-111">Можно найти полный исходный код hello [на GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="40a55-111">You can find hello full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="40a55-112">Вы также можете прочесть об hello [пакет SDK Azure Search .NET](search-howto-dotnet-sdk.md) для более подробные руководства по hello примеров кода.</span><span class="sxs-lookup"><span data-stu-id="40a55-112">You can also read about hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of hello sample code.</span></span>

<span data-ttu-id="40a55-113">В порядке toopush документов в индекс с помощью hello .NET SDK необходимо:</span><span class="sxs-lookup"><span data-stu-id="40a55-113">In order toopush documents into your index using hello .NET SDK, you will need to:</span></span>

1. <span data-ttu-id="40a55-114">Создание `SearchIndexClient` объекта tooconnect tooyour поиска индекса.</span><span class="sxs-lookup"><span data-stu-id="40a55-114">Create a `SearchIndexClient` object tooconnect tooyour search index.</span></span>
2. <span data-ttu-id="40a55-115">Создание `IndexBatch` содержащий toobe документы hello добавлены, изменены или удалены.</span><span class="sxs-lookup"><span data-stu-id="40a55-115">Create an `IndexBatch` containing hello documents toobe added, modified, or deleted.</span></span>
3. <span data-ttu-id="40a55-116">Вызовите hello `Documents.Index` метод вашей `SearchIndexClient` toosend hello `IndexBatch` tooyour индекс поиска.</span><span class="sxs-lookup"><span data-stu-id="40a55-116">Call hello `Documents.Index` method of your `SearchIndexClient` toosend hello `IndexBatch` tooyour search index.</span></span>

## <a name="create-an-instance-of-hello-searchindexclient-class"></a><span data-ttu-id="40a55-117">Создайте экземпляр класса SearchIndexClient hello</span><span class="sxs-lookup"><span data-stu-id="40a55-117">Create an instance of hello SearchIndexClient class</span></span>
<span data-ttu-id="40a55-118">tooimport данных в индекс с помощью hello пакет SDK Azure Search .NET, вам понадобится toocreate экземпляр hello `SearchIndexClient` класса.</span><span class="sxs-lookup"><span data-stu-id="40a55-118">tooimport data into your index using hello Azure Search .NET SDK, you will need toocreate an instance of hello `SearchIndexClient` class.</span></span> <span data-ttu-id="40a55-119">Можно создать этот экземпляр самостоятельно, но он проще, если у вас уже есть `SearchServiceClient` toocall экземпляра его `Indexes.GetClient` метод.</span><span class="sxs-lookup"><span data-stu-id="40a55-119">You can construct this instance yourself, but it's easier if you already have a `SearchServiceClient` instance toocall its `Indexes.GetClient` method.</span></span> <span data-ttu-id="40a55-120">Например, вот как можно будет получить `SearchIndexClient` для hello индекса с именем «гостиницы» из `SearchServiceClient` с именем `serviceClient`:</span><span class="sxs-lookup"><span data-stu-id="40a55-120">For example, here is how you would obtain a `SearchIndexClient` for hello index named "hotels" from a `SearchServiceClient` named `serviceClient`:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="40a55-121">В типичном поисковом приложении управление индексами и заполнение обрабатываются отдельным компонентом из запросов поиска.</span><span class="sxs-lookup"><span data-stu-id="40a55-121">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="40a55-122">`Indexes.GetClient`удобный для заполнения индекса, так как избавляет вас hello проблемы предоставления другой `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="40a55-122">`Indexes.GetClient` is convenient for populating an index because it saves you hello trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="40a55-123">Это делается путем передачи ключа администратора hello, то используется toocreate hello `SearchServiceClient` toohello новый `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="40a55-123">It does this by passing hello admin key that you used toocreate hello `SearchServiceClient` toohello new `SearchIndexClient`.</span></span> <span data-ttu-id="40a55-124">Однако в hello части приложения, которое выполняет запросы, это лучше toocreate hello `SearchIndexClient` напрямую, что можно передавать ключ запроса вместо ключа администратора.</span><span class="sxs-lookup"><span data-stu-id="40a55-124">However, in hello part of your application that executes queries, it is better toocreate hello `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="40a55-125">Это согласуется с hello [принципа наименьших прав доступа](https://en.wikipedia.org/wiki/Principle_of_least_privilege) и поможет toomake более безопасные приложения.</span><span class="sxs-lookup"><span data-stu-id="40a55-125">This is consistent with hello [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) and will help toomake your application more secure.</span></span> <span data-ttu-id="40a55-126">Можно найти дополнительные сведения о ключи администратора и ключи запроса в hello [Справочник по REST API поиска Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="40a55-126">You can find out more about admin keys and query keys in hello [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
> 
> 

<span data-ttu-id="40a55-127">У класса `SearchIndexClient` есть свойство `Documents`.</span><span class="sxs-lookup"><span data-stu-id="40a55-127">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="40a55-128">Это свойство предоставляет все методы hello требуется tooadd, изменить, удалить или запрос документов в индексе.</span><span class="sxs-lookup"><span data-stu-id="40a55-128">This property provides all hello methods you need tooadd, modify, delete, or query documents in your index.</span></span>

## <a name="decide-which-indexing-action-toouse"></a><span data-ttu-id="40a55-129">Решите, какие индексирования toouse действие</span><span class="sxs-lookup"><span data-stu-id="40a55-129">Decide which indexing action toouse</span></span>
<span data-ttu-id="40a55-130">tooimport данных с помощью hello .NET SDK, необходимо будет toopackage копирование данных в `IndexBatch` объекта.</span><span class="sxs-lookup"><span data-stu-id="40a55-130">tooimport data using hello .NET SDK, you will need toopackage up your data into an `IndexBatch` object.</span></span> <span data-ttu-id="40a55-131">`IndexBatch` Инкапсулирует коллекцию `IndexAction` объектов, каждый из которых включает документ и свойство, определяющее поиска Azure, какие действия tooperform для этого документа (отправка, слияние, удаление, и т. д).</span><span class="sxs-lookup"><span data-stu-id="40a55-131">An `IndexBatch` encapsulates a collection of `IndexAction` objects, each of which contains a document and a property that tells Azure Search what action tooperform on that document (upload, merge, delete, etc).</span></span> <span data-ttu-id="40a55-132">В зависимости от того, какой из hello следующие действия, которые можно выбрать только определенные поля должны быть включены для каждого документа:</span><span class="sxs-lookup"><span data-stu-id="40a55-132">Depending on which of hello below actions you choose, only certain fields must be included for each document:</span></span>

| <span data-ttu-id="40a55-133">Действие</span><span class="sxs-lookup"><span data-stu-id="40a55-133">Action</span></span> | <span data-ttu-id="40a55-134">Описание</span><span class="sxs-lookup"><span data-stu-id="40a55-134">Description</span></span> | <span data-ttu-id="40a55-135">Необходимые поля для каждого документа</span><span class="sxs-lookup"><span data-stu-id="40a55-135">Necessary fields for each document</span></span> | <span data-ttu-id="40a55-136">Примечания</span><span class="sxs-lookup"><span data-stu-id="40a55-136">Notes</span></span> |
| --- | --- | --- | --- |
| `Upload` |<span data-ttu-id="40a55-137">`Upload` Действие — примерно tooan «вставки-обновления» где документ hello будет вставлена, если является новым и обновлен или заменен, если он существует.</span><span class="sxs-lookup"><span data-stu-id="40a55-137">An `Upload` action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="40a55-138">ключ, а также другие поля, нужно toodefine</span><span class="sxs-lookup"><span data-stu-id="40a55-138">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="40a55-139">При обновлении или замене существующего документа, любое поле, которое не указано в запросе hello будет иметь слишком его поле`null`.</span><span class="sxs-lookup"><span data-stu-id="40a55-139">When updating/replacing an existing document, any field that is not specified in hello request will have its field set too`null`.</span></span> <span data-ttu-id="40a55-140">Это происходит даже в том случае, если поле hello было установлено ранее tooa непустое значение.</span><span class="sxs-lookup"><span data-stu-id="40a55-140">This occurs even when hello field was previously set tooa non-null value.</span></span> |
| `Merge` |<span data-ttu-id="40a55-141">Обновления, существующий документ с hello указаны поля.</span><span class="sxs-lookup"><span data-stu-id="40a55-141">Updates an existing document with hello specified fields.</span></span> <span data-ttu-id="40a55-142">Если документ hello не существует в индексе hello, hello слияния завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="40a55-142">If hello document does not exist in hello index, hello merge will fail.</span></span> |<span data-ttu-id="40a55-143">ключ, а также другие поля, нужно toodefine</span><span class="sxs-lookup"><span data-stu-id="40a55-143">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="40a55-144">Любое поле, указанное для объединения приведет к замене существующего поля hello в документе hello.</span><span class="sxs-lookup"><span data-stu-id="40a55-144">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="40a55-145">Это относится и к полям типа `DataType.Collection(DataType.String)`.</span><span class="sxs-lookup"><span data-stu-id="40a55-145">This includes fields of type `DataType.Collection(DataType.String)`.</span></span> <span data-ttu-id="40a55-146">Например, если hello документ содержит поле `tags` со значением `["budget"]` , и вы выполните объединение со значением `["economy", "pool"]` для `tags`, hello окончательное значение hello `tags` поле будет `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="40a55-146">For example, if hello document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, hello final value of hello `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="40a55-147">а не `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="40a55-147">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `MergeOrUpload` |<span data-ttu-id="40a55-148">Это действие ведет себя как `Merge` Если документ с hello заданным ключом уже существует в индексе hello.</span><span class="sxs-lookup"><span data-stu-id="40a55-148">This action behaves like `Merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="40a55-149">Если документ hello не существует, он ведет себя как `Upload` с новым документом.</span><span class="sxs-lookup"><span data-stu-id="40a55-149">If hello document does not exist, it behaves like `Upload` with a new document.</span></span> |<span data-ttu-id="40a55-150">ключ, а также другие поля, нужно toodefine</span><span class="sxs-lookup"><span data-stu-id="40a55-150">key, plus any other fields you wish toodefine</span></span> |- |
| `Delete` |<span data-ttu-id="40a55-151">Удаляет указанный документ hello из индекса hello.</span><span class="sxs-lookup"><span data-stu-id="40a55-151">Removes hello specified document from hello index.</span></span> |<span data-ttu-id="40a55-152">Только ключ</span><span class="sxs-lookup"><span data-stu-id="40a55-152">key only</span></span> |<span data-ttu-id="40a55-153">Все поля, укажите вместо hello ключевое поле будет игнорироваться.</span><span class="sxs-lookup"><span data-stu-id="40a55-153">Any fields you specify other than hello key field will be ignored.</span></span> <span data-ttu-id="40a55-154">Tooremove отдельного поля из документа, используйте `Merge` вместо и просто задать поле hello явно toonull.</span><span class="sxs-lookup"><span data-stu-id="40a55-154">If you want tooremove an individual field from a document, use `Merge` instead and simply set hello field explicitly toonull.</span></span> |

<span data-ttu-id="40a55-155">Можно указать, какое действие должно toouse с hello различных статических методов hello `IndexBatch` и `IndexAction` классов, как показано в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="40a55-155">You can specify what action you want toouse with hello various static methods of hello `IndexBatch` and `IndexAction` classes, as shown in hello next section.</span></span>

## <a name="construct-your-indexbatch"></a><span data-ttu-id="40a55-156">Создание класса IndexBatch</span><span class="sxs-lookup"><span data-stu-id="40a55-156">Construct your IndexBatch</span></span>
<span data-ttu-id="40a55-157">Теперь, когда вы знаете, какие tooperform действия с документами, вы являетесь hello готов tooconstruct `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="40a55-157">Now that you know which actions tooperform on your documents, you are ready tooconstruct hello `IndexBatch`.</span></span> <span data-ttu-id="40a55-158">Здравствуйте в следующем примере показано, как toocreate пакет с несколько различных действий.</span><span class="sxs-lookup"><span data-stu-id="40a55-158">hello example below shows how toocreate a batch with a few different actions.</span></span> <span data-ttu-id="40a55-159">Обратите внимание, что наш пример использует пользовательский класс с именем `Hotel` сопоставляемого tooa документов в индексе «гостиницы» hello.</span><span class="sxs-lookup"><span data-stu-id="40a55-159">Note that our example uses a custom class called `Hotel` that maps tooa document in hello "hotels" index.</span></span>

```csharp
var actions =
    new IndexAction<Hotel>[]
    {
        IndexAction.Upload(
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
            }),
        IndexAction.Upload(
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
            }),
        IndexAction.MergeOrUpload(
            new Hotel()
            {
                HotelId = "3",
                BaseRate = 129.99,
                Description = "Close tootown hall and hello river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

<span data-ttu-id="40a55-160">В этом случае мы используем `Upload`, `MergeOrUpload`, и `Delete` как наши действия поиска, в соответствии с hello методы, вызываемые на hello `IndexAction` класса.</span><span class="sxs-lookup"><span data-stu-id="40a55-160">In this case, we are using `Upload`, `MergeOrUpload`, and `Delete` as our search actions, as specified by hello methods called on hello `IndexAction` class.</span></span>

<span data-ttu-id="40a55-161">Предположим, что пример индекса с именем hotels уже заполнен несколькими документами.</span><span class="sxs-lookup"><span data-stu-id="40a55-161">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="40a55-162">Обратите внимание на то, как бы не было toospecify все поля hello возможных документа при использовании `MergeOrUpload` и как мы указан только ключ документа hello (`HotelId`) при использовании `Delete`.</span><span class="sxs-lookup"><span data-stu-id="40a55-162">Note how we did not have toospecify all hello possible document fields when using `MergeOrUpload` and how we only specified hello document key (`HotelId`) when using `Delete`.</span></span>

<span data-ttu-id="40a55-163">Кроме того Обратите внимание, что может включать только too1000 документов в одном запросе индексирования.</span><span class="sxs-lookup"><span data-stu-id="40a55-163">Also, note that you can only include up too1000 documents in a single indexing request.</span></span>

> [!NOTE]
> <span data-ttu-id="40a55-164">В этом примере применяется документы toodifferent разные действия.</span><span class="sxs-lookup"><span data-stu-id="40a55-164">In this example, we are applying different actions toodifferent documents.</span></span> <span data-ttu-id="40a55-165">Если вы хотите, чтобы tooperform hello же действия для всех документов в пакете hello, вместо вызова метода `IndexBatch.New`, можно использовать hello других статических методов `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="40a55-165">If you wanted tooperform hello same actions across all documents in hello batch, instead of calling `IndexBatch.New`, you could use hello other static methods of `IndexBatch`.</span></span> <span data-ttu-id="40a55-166">Например, можно создать пакеты, вызвав метод `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` или `IndexBatch.Delete`.</span><span class="sxs-lookup"><span data-stu-id="40a55-166">For example, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete`.</span></span> <span data-ttu-id="40a55-167">Эти методы вместо объектов `IndexAction` принимают коллекцию документов (в нашем примере это объекты типа `Hotel`).</span><span class="sxs-lookup"><span data-stu-id="40a55-167">These methods take a collection of documents (objects of type `Hotel` in this example) instead of `IndexAction` objects.</span></span>
> 
> 

## <a name="import-data-toohello-index"></a><span data-ttu-id="40a55-168">Индекс toohello импорта данных</span><span class="sxs-lookup"><span data-stu-id="40a55-168">Import data toohello index</span></span>
<span data-ttu-id="40a55-169">Теперь, когда имеется инициализированная `IndexBatch` объекта, вы можете отправить ее toohello индекс путем вызова `Documents.Index` на ваш `SearchIndexClient` объекта.</span><span class="sxs-lookup"><span data-stu-id="40a55-169">Now that you have an initialized `IndexBatch` object, you can send it toohello index by calling `Documents.Index` on your `SearchIndexClient` object.</span></span> <span data-ttu-id="40a55-170">Следующий пример показывает как Hello toocall `Index`, также как некоторые дополнительные действия, вам потребуется tooperform:</span><span class="sxs-lookup"><span data-stu-id="40a55-170">hello following example shows how toocall `Index`, as well as some extra steps you will need tooperform:</span></span>

```csharp
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
```

<span data-ttu-id="40a55-171">Примечание hello `try` / `catch` вокруг вызова toohello hello `Index` метод.</span><span class="sxs-lookup"><span data-stu-id="40a55-171">Note hello `try`/`catch` surrounding hello call toohello `Index` method.</span></span> <span data-ttu-id="40a55-172">Hello блок catch обрабатывает такие важные ошибки для индексирования.</span><span class="sxs-lookup"><span data-stu-id="40a55-172">hello catch block handles an important error case for indexing.</span></span> <span data-ttu-id="40a55-173">Службе поиска Azure в случае некоторые hello документов в пакете hello tooindex `IndexBatchException` вызванное `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="40a55-173">If your Azure Search service fails tooindex some of hello documents in hello batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="40a55-174">Это может произойти, если вы индексируете документы службы при интенсивной нагрузке.</span><span class="sxs-lookup"><span data-stu-id="40a55-174">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="40a55-175">**Настоятельно рекомендуется явно обрабатывать этот случай в коде.**</span><span class="sxs-lookup"><span data-stu-id="40a55-175">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="40a55-176">Можно отложить и повторите попытку индексирования отказавших документов hello или пользователь может входить и продолжить как образец hello работает, можно сделать что-нибудь другое в зависимости от требований к согласованности данных приложения.</span><span class="sxs-lookup"><span data-stu-id="40a55-176">You can delay and then retry indexing hello documents that failed, or you can log and continue like hello sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

<span data-ttu-id="40a55-177">Наконец hello кода в примере hello выше задержки в течение двух секунд.</span><span class="sxs-lookup"><span data-stu-id="40a55-177">Finally, hello code in hello example above delays for two seconds.</span></span> <span data-ttu-id="40a55-178">Индексирование работает асинхронно в службе поиска Azure, поэтому пример приложения hello должен toowait tooensure короткое время, что hello документы доступны для поиска.</span><span class="sxs-lookup"><span data-stu-id="40a55-178">Indexing happens asynchronously in your Azure Search service, so hello sample application needs toowait a short time tooensure that hello documents are available for searching.</span></span> <span data-ttu-id="40a55-179">Такие задержки обычно необходимы только в демонстрациях, тестах и примерах приложений.</span><span class="sxs-lookup"><span data-stu-id="40a55-179">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

<a name="HotelClass"></a>

### <a name="how-hello-net-sdk-handles-documents"></a><span data-ttu-id="40a55-180">Как hello пакета SDK для .NET обрабатывает документы</span><span class="sxs-lookup"><span data-stu-id="40a55-180">How hello .NET SDK handles documents</span></span>
<span data-ttu-id="40a55-181">Может возникнуть вопрос как hello пакет SDK Azure Search .NET — может tooupload экземпляры класса определяемого пользователем как `Hotel` toohello индекса.</span><span class="sxs-lookup"><span data-stu-id="40a55-181">You may be wondering how hello Azure Search .NET SDK is able tooupload instances of a user-defined class like `Hotel` toohello index.</span></span> <span data-ttu-id="40a55-182">toohelp ответа на этот вопрос, давайте взглянем на hello `Hotel` класс, который сопоставляет определенной в схеме индекса toohello [создать индекс поиска Azure с помощью hello .NET SDK](search-create-index-dotnet.md#DefineIndex):</span><span class="sxs-lookup"><span data-stu-id="40a55-182">toohelp answer that question, let's look at hello `Hotel` class, which maps toohello index schema defined in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#DefineIndex):</span></span>

```csharp
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [Key]
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

    // ToString() method omitted for brevity...
}
```

<span data-ttu-id="40a55-183">Hello первое, что toonotice является, каждое общее свойство `Hotel` соответствует tooa поля в определение индекса hello, но с одним ключевым отличием: hello имя каждого поля начинается с букв нижнего регистра («верблюжий»), тогда hello имя каждого открытых Свойство `Hotel` начинается с буквы верхнего регистра («стиле Pascal»).</span><span class="sxs-lookup"><span data-stu-id="40a55-183">hello first thing toonotice is that each public property of `Hotel` corresponds tooa field in hello index definition, but with one crucial difference: hello name of each field starts with a lower-case letter ("camel case"), while hello name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="40a55-184">Это распространенный сценарий в приложениях .NET и выполнить привязку данных, где управление внешними hello разработчик приложения hello hello целевой схемы.</span><span class="sxs-lookup"><span data-stu-id="40a55-184">This is a common scenario in .NET applications that perform data-binding where hello target schema is outside hello control of hello application developer.</span></span> <span data-ttu-id="40a55-185">Вместо того чтобы использовать .NET hello tooviolate правила именования, делая прописной имена свойств, чтобы узнать hello SDK toomap hello свойство имена toocamel регистре автоматически с помощью hello `[SerializePropertyNamesAsCamelCase]` атрибута.</span><span class="sxs-lookup"><span data-stu-id="40a55-185">Rather than having tooviolate hello .NET naming guidelines by making property names camel-case, you can tell hello SDK toomap hello property names toocamel-case automatically with hello `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="40a55-186">пакет SDK Azure Search .NET Hello использует hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize библиотеки и десериализации tooand объектов в пользовательскую модель из JSON.</span><span class="sxs-lookup"><span data-stu-id="40a55-186">hello Azure Search .NET SDK uses hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library tooserialize and deserialize your custom model objects tooand from JSON.</span></span> <span data-ttu-id="40a55-187">При необходимости эту сериализацию можно настроить.</span><span class="sxs-lookup"><span data-stu-id="40a55-187">You can customize this serialization if needed.</span></span> <span data-ttu-id="40a55-188">Дополнительные сведения см. в разделе [Пользовательская сериализация с помощью JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="40a55-188">You can find more details in [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span></span> <span data-ttu-id="40a55-189">Примером этого является использование hello hello `[JsonProperty]` атрибут hello `DescriptionFr` свойство в приведенном выше примере кода hello.</span><span class="sxs-lookup"><span data-stu-id="40a55-189">One example of this is hello use of hello `[JsonProperty]` attribute on hello `DescriptionFr` property in hello sample code above.</span></span>
> 
> 

<span data-ttu-id="40a55-190">Hello второй важным преимуществом hello `Hotel` класса являются типами данных hello hello открытые свойства.</span><span class="sxs-lookup"><span data-stu-id="40a55-190">hello second important thing about hello `Hotel` class are hello data types of hello public properties.</span></span> <span data-ttu-id="40a55-191">типы tootheir эквивалент полей в определение индекса hello сопоставление типов Hello из этих свойств.</span><span class="sxs-lookup"><span data-stu-id="40a55-191">hello .NET types of these properties map tootheir equivalent field types in hello index definition.</span></span> <span data-ttu-id="40a55-192">Здравствуйте, например, `Category` строковое свойство сопоставляется toohello `category` поле, которое относится к типу `DataType.String`.</span><span class="sxs-lookup"><span data-stu-id="40a55-192">For example, hello `Category` string property maps toohello `category` field, which is of type `DataType.String`.</span></span> <span data-ttu-id="40a55-193">Аналогичные сопоставления присутствуют между типами `bool?` и `DataType.Boolean`, `DateTimeOffset?` и `DataType.DateTimeOffset` и т. д.</span><span class="sxs-lookup"><span data-stu-id="40a55-193">There are similar type mappings between `bool?` and `DataType.Boolean`, `DateTimeOffset?` and `DataType.DateTimeOffset`, and so forth.</span></span> <span data-ttu-id="40a55-194">Hello определенные правила для сопоставления типа hello описаны с hello `Documents.Get` метод в hello [ссылку на пакет SDK Azure Search .NET](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="40a55-194">hello specific rules for hello type mapping are documented with hello `Documents.Get` method in hello [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span>

<span data-ttu-id="40a55-195">Это возможность toouse собственные классы как документы работает в обоих направлениях; Можно также получать результаты поиска и hello SDK автоматически выполнить десериализацию их tooa типа по своему усмотрению, как показано в hello [следующей статье](search-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="40a55-195">This ability toouse your own classes as documents works in both directions; You can also retrieve search results and have hello SDK automatically deserialize them tooa type of your choice, as shown in hello [next article](search-query-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="40a55-196">пакет SDK Azure Search .NET Hello также поддерживает динамически типизированные документы с помощью hello `Document` класс, который представляет собой сопоставление значений toofield имена полей ключ значение.</span><span class="sxs-lookup"><span data-stu-id="40a55-196">hello Azure Search .NET SDK also supports dynamically-typed documents using hello `Document` class, which is a key/value mapping of field names toofield values.</span></span> <span data-ttu-id="40a55-197">Это полезно в сценариях, которых вы не знаете hello схемы индекса во время разработки, или было бы неудобно toobind toospecific модель классов.</span><span class="sxs-lookup"><span data-stu-id="40a55-197">This is useful in scenarios where you don't know hello index schema at design-time, or where it would be inconvenient toobind toospecific model classes.</span></span> <span data-ttu-id="40a55-198">Все методы hello hello SDK, обрабатывающих документы имеют перегрузки, которые работают с hello `Document` класса, а также строго типизированных перегрузки, принимающие параметр универсального типа.</span><span class="sxs-lookup"><span data-stu-id="40a55-198">All hello methods in hello SDK that deal with documents have overloads that work with hello `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="40a55-199">Последний hello используются в примере кода hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="40a55-199">Only hello latter are used in hello sample code in this article.</span></span>
> 
> 

<span data-ttu-id="40a55-200">**Почему следует использовать типы данных, допускающие значение NULL**</span><span class="sxs-lookup"><span data-stu-id="40a55-200">**Why you should use nullable data types**</span></span>

<span data-ttu-id="40a55-201">При разработке собственных индекс поиска Azure классы toomap модели tooan, мы рекомендуем, например, объявление свойств типов значений `bool` и `int` toobe допускает значение NULL (например, `bool?` вместо `bool`).</span><span class="sxs-lookup"><span data-stu-id="40a55-201">When designing your own model classes toomap tooan Azure Search index, we recommend declaring properties of value types such as `bool` and `int` toobe nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="40a55-202">При использовании свойство не допускающим имеется слишком**гарантирует** что документов в индексе не будет содержать значение null для соответствующего поля hello.</span><span class="sxs-lookup"><span data-stu-id="40a55-202">If you use a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="40a55-203">Hello SDK ни hello службы поиска Azure поможет вам tooenforce это.</span><span class="sxs-lookup"><span data-stu-id="40a55-203">Neither hello SDK nor hello Azure Search service will help you tooenforce this.</span></span>

<span data-ttu-id="40a55-204">Это не относится только к гипотетической: представьте себе ситуацию, когда Добавление нового поля tooan существующего индекса, тип которого `DataType.Int32`.</span><span class="sxs-lookup"><span data-stu-id="40a55-204">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `DataType.Int32`.</span></span> <span data-ttu-id="40a55-205">После обновления определения индекса hello, все документы будет иметь значение null для этого нового поля (поскольку все типы допускают значение NULL, если в службе поиска Azure).</span><span class="sxs-lookup"><span data-stu-id="40a55-205">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="40a55-206">При использовании модели с запретом `int` свойства для этого поля, вы получите `JsonSerializationException` при попытке документы tooretrieve следующим образом:</span><span class="sxs-lookup"><span data-stu-id="40a55-206">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="40a55-207">По этой причине по-прежнему рекомендуется использовать типы, допускающие значения NULL, в классах модели.</span><span class="sxs-lookup"><span data-stu-id="40a55-207">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40a55-208">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="40a55-208">Next steps</span></span>
<span data-ttu-id="40a55-209">После заполнения индекса поиска Azure, будет готов toostart выдача запросов toosearch для документов.</span><span class="sxs-lookup"><span data-stu-id="40a55-209">After populating your Azure Search index, you will be ready toostart issuing queries toosearch for documents.</span></span> <span data-ttu-id="40a55-210">Дополнительные сведения см. в статье [Запросы в службе поиска Azure](search-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="40a55-210">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>

