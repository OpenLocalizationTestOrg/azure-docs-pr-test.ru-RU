---
title: "Отправка данных в службу поиска Azure c помощью .NET | Документация Майкрософт"
description: "Сведения о том, как отправлять данные в индекс службы поиска Azure с помощью пакета SDK .NET."
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
ms.openlocfilehash: bdd952869143c6ca6374bb9264db5bcba1f32b50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="upload-data-to-azure-search-using-the-net-sdk"></a><span data-ttu-id="28afe-103">Отправка данных в службу поиска Azure с помощью пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="28afe-103">Upload data to Azure Search using the .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="28afe-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="28afe-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="28afe-105">.NET</span><span class="sxs-lookup"><span data-stu-id="28afe-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="28afe-106">REST</span><span class="sxs-lookup"><span data-stu-id="28afe-106">REST</span></span>](search-import-data-rest-api.md)
> 
> 

<span data-ttu-id="28afe-107">Из этой статьи вы узнаете, как импортировать данные в индекс службы поиска Azure с помощью пакета [SDK .NET для службы поиска Azure](https://aka.ms/search-sdk) .</span><span class="sxs-lookup"><span data-stu-id="28afe-107">This article will show you how to use the [Azure Search .NET SDK](https://aka.ms/search-sdk) to import data into an Azure Search index.</span></span>

<span data-ttu-id="28afe-108">Прежде чем приступать к выполнению инструкций из этого руководства, вам нужно [создать индекс службы поиска Azure](search-what-is-an-index.md).</span><span class="sxs-lookup"><span data-stu-id="28afe-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span> <span data-ttu-id="28afe-109">В статье также предполагается, что вы уже создали объект `SearchServiceClient` , как описано в статье [Создание индекса для службы поиска Azure с помощью .NET](search-create-index-dotnet.md#CreateSearchServiceClient).</span><span class="sxs-lookup"><span data-stu-id="28afe-109">This article also assumes that you have already created a `SearchServiceClient` object, as shown in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span></span>

> [!NOTE]
> <span data-ttu-id="28afe-110">Все приведенные здесь примеры кода написаны на языке C#.</span><span class="sxs-lookup"><span data-stu-id="28afe-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="28afe-111">Полный исходный код можно найти на сайте [GitHub](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="28afe-111">You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="28afe-112">Подробные примеры использования кода см. в сведениях о [пакете SDK .NET для службы поиска Azure](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="28afe-112">You can also read about the [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of the sample code.</span></span>

<span data-ttu-id="28afe-113">Чтобы отправить документы в индекс с помощью пакета SDK для .NET, сделайте вот что.</span><span class="sxs-lookup"><span data-stu-id="28afe-113">In order to push documents into your index using the .NET SDK, you will need to:</span></span>

1. <span data-ttu-id="28afe-114">Создайте объект `SearchIndexClient` , который будет подключен к индексу поиска.</span><span class="sxs-lookup"><span data-stu-id="28afe-114">Create a `SearchIndexClient` object to connect to your search index.</span></span>
2. <span data-ttu-id="28afe-115">Создайте класс `IndexBatch`, содержащий документы, которые должны быть добавлены, изменены или удалены.</span><span class="sxs-lookup"><span data-stu-id="28afe-115">Create an `IndexBatch` containing the documents to be added, modified, or deleted.</span></span>
3. <span data-ttu-id="28afe-116">Вызовите метод `Documents.Index` в объекте `SearchIndexClient`, чтобы отправить `IndexBatch` в индекс поиска.</span><span class="sxs-lookup"><span data-stu-id="28afe-116">Call the `Documents.Index` method of your `SearchIndexClient` to send the `IndexBatch` to your search index.</span></span>

## <a name="create-an-instance-of-the-searchindexclient-class"></a><span data-ttu-id="28afe-117">Создание экземпляра класса SearchIndexClient</span><span class="sxs-lookup"><span data-stu-id="28afe-117">Create an instance of the SearchIndexClient class</span></span>
<span data-ttu-id="28afe-118">Чтобы импортировать данные в индекс с помощью пакета SDK .NET для службы поиска Azure, нужно создать экземпляр класса `SearchIndexClient` .</span><span class="sxs-lookup"><span data-stu-id="28afe-118">To import data into your index using the Azure Search .NET SDK, you will need to create an instance of the `SearchIndexClient` class.</span></span> <span data-ttu-id="28afe-119">Этот экземпляр можно создать самостоятельно, но проще использовать экземпляр `SearchServiceClient`, вызывающий метод `Indexes.GetClient`.</span><span class="sxs-lookup"><span data-stu-id="28afe-119">You can construct this instance yourself, but it's easier if you already have a `SearchServiceClient` instance to call its `Indexes.GetClient` method.</span></span> <span data-ttu-id="28afe-120">Например, получить `SearchIndexClient` для индекса с именем hotels из `SearchServiceClient` с именем `serviceClient` можно следующим образом.</span><span class="sxs-lookup"><span data-stu-id="28afe-120">For example, here is how you would obtain a `SearchIndexClient` for the index named "hotels" from a `SearchServiceClient` named `serviceClient`:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="28afe-121">В типичном поисковом приложении управление индексами и заполнение обрабатываются отдельным компонентом из запросов поиска.</span><span class="sxs-lookup"><span data-stu-id="28afe-121">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="28afe-122">Элемент `Indexes.GetClient` удобен для заполнения индекса, так как он избавляет от необходимости указывать другой элемент `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="28afe-122">`Indexes.GetClient` is convenient for populating an index because it saves you the trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="28afe-123">Это достигается благодаря передачи ключа администратора, который использовался для создания `SearchServiceClient`, в новый элемент `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="28afe-123">It does this by passing the admin key that you used to create the `SearchServiceClient` to the new `SearchIndexClient`.</span></span> <span data-ttu-id="28afe-124">Однако в части приложения, которая выполняет запросы, лучше создать `SearchIndexClient` напрямую, чтобы передать ключ запроса вместо ключа администратора.</span><span class="sxs-lookup"><span data-stu-id="28afe-124">However, in the part of your application that executes queries, it is better to create the `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="28afe-125">Это согласуется с [принципом наименьших прав доступа](https://en.wikipedia.org/wiki/Principle_of_least_privilege) и поможет сделать приложение более безопасным.</span><span class="sxs-lookup"><span data-stu-id="28afe-125">This is consistent with the [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) and will help to make your application more secure.</span></span> <span data-ttu-id="28afe-126">Дополнительные сведения о ключах администратора и ключах запросов см. справочнике [REST API службы поиска Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="28afe-126">You can find out more about admin keys and query keys in the [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
> 
> 

<span data-ttu-id="28afe-127">У класса `SearchIndexClient` есть свойство `Documents`.</span><span class="sxs-lookup"><span data-stu-id="28afe-127">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="28afe-128">Это свойство предоставляет все методы, которые необходимы для добавления, изменения, удаления и запроса документов в индексе.</span><span class="sxs-lookup"><span data-stu-id="28afe-128">This property provides all the methods you need to add, modify, delete, or query documents in your index.</span></span>

## <a name="decide-which-indexing-action-to-use"></a><span data-ttu-id="28afe-129">Выбор операций индексирования</span><span class="sxs-lookup"><span data-stu-id="28afe-129">Decide which indexing action to use</span></span>
<span data-ttu-id="28afe-130">Чтобы импортировать данные с помощью пакета SDK для .NET, необходимо упаковать данные в объект `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="28afe-130">To import data using the .NET SDK, you will need to package up your data into an `IndexBatch` object.</span></span> <span data-ttu-id="28afe-131">`IndexBatch` инкапсулирует коллекцию объектов `IndexAction`, каждый из которых содержит документ и свойство. С помощью этого свойства служба поиска Azure определяет, какое действие необходимо выполнить с соответствующим документом (отправка, объединение, удаление и др.).</span><span class="sxs-lookup"><span data-stu-id="28afe-131">An `IndexBatch` encapsulates a collection of `IndexAction` objects, each of which contains a document and a property that tells Azure Search what action to perform on that document (upload, merge, delete, etc).</span></span> <span data-ttu-id="28afe-132">В зависимости от выбранной операции для каждого документа будут включены только определенные поля.</span><span class="sxs-lookup"><span data-stu-id="28afe-132">Depending on which of the below actions you choose, only certain fields must be included for each document:</span></span>

| <span data-ttu-id="28afe-133">Действие</span><span class="sxs-lookup"><span data-stu-id="28afe-133">Action</span></span> | <span data-ttu-id="28afe-134">Описание</span><span class="sxs-lookup"><span data-stu-id="28afe-134">Description</span></span> | <span data-ttu-id="28afe-135">Необходимые поля для каждого документа</span><span class="sxs-lookup"><span data-stu-id="28afe-135">Necessary fields for each document</span></span> | <span data-ttu-id="28afe-136">Примечания</span><span class="sxs-lookup"><span data-stu-id="28afe-136">Notes</span></span> |
| --- | --- | --- | --- |
| `Upload` |<span data-ttu-id="28afe-137">Операция `Upload` аналогична операции upsert, которая добавляет документ, если он новый, и обновляет либо заменяет его, если он уже существует.</span><span class="sxs-lookup"><span data-stu-id="28afe-137">An `Upload` action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="28afe-138">Поле key, а также другие поля, которые вы хотите определить.</span><span class="sxs-lookup"><span data-stu-id="28afe-138">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="28afe-139">При обновлении или замене существующего документа все поля, не указанные в запросе, получат значение `null`.</span><span class="sxs-lookup"><span data-stu-id="28afe-139">When updating/replacing an existing document, any field that is not specified in the request will have its field set to `null`.</span></span> <span data-ttu-id="28afe-140">Это происходит, даже если для поля указано непустое значение.</span><span class="sxs-lookup"><span data-stu-id="28afe-140">This occurs even when the field was previously set to a non-null value.</span></span> |
| `Merge` |<span data-ttu-id="28afe-141">Обновляет существующий документ с использованием указанных полей.</span><span class="sxs-lookup"><span data-stu-id="28afe-141">Updates an existing document with the specified fields.</span></span> <span data-ttu-id="28afe-142">Если документ не существует в индексе, объединение завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="28afe-142">If the document does not exist in the index, the merge will fail.</span></span> |<span data-ttu-id="28afe-143">Поле key, а также другие поля, которые вы хотите определить.</span><span class="sxs-lookup"><span data-stu-id="28afe-143">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="28afe-144">Поля, указанные в запросе на объединение, заменяют собой существующие поля документа.</span><span class="sxs-lookup"><span data-stu-id="28afe-144">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="28afe-145">Это относится и к полям типа `DataType.Collection(DataType.String)`.</span><span class="sxs-lookup"><span data-stu-id="28afe-145">This includes fields of type `DataType.Collection(DataType.String)`.</span></span> <span data-ttu-id="28afe-146">Например, если документ содержит поле `tags` со значением `["budget"]` и вы выполняете операцию объединения со значением `["economy", "pool"]` для поля `tags`, в итоге поле `tags` примет значение `["economy", "pool"]`,</span><span class="sxs-lookup"><span data-stu-id="28afe-146">For example, if the document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, the final value of the `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="28afe-147">а не `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="28afe-147">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `MergeOrUpload` |<span data-ttu-id="28afe-148">Эта операция аналогична операции `Merge`, если документ с указанным значением ключа уже существует в индексе.</span><span class="sxs-lookup"><span data-stu-id="28afe-148">This action behaves like `Merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="28afe-149">Если документа нет, эта операция выполняется так же, как и операция `Upload` с новым документом.</span><span class="sxs-lookup"><span data-stu-id="28afe-149">If the document does not exist, it behaves like `Upload` with a new document.</span></span> |<span data-ttu-id="28afe-150">Поле key, а также другие поля, которые вы хотите определить.</span><span class="sxs-lookup"><span data-stu-id="28afe-150">key, plus any other fields you wish to define</span></span> |- |
| `Delete` |<span data-ttu-id="28afe-151">Удаление указанного документа из индекса.</span><span class="sxs-lookup"><span data-stu-id="28afe-151">Removes the specified document from the index.</span></span> |<span data-ttu-id="28afe-152">Только ключ</span><span class="sxs-lookup"><span data-stu-id="28afe-152">key only</span></span> |<span data-ttu-id="28afe-153">Все указанные поля, которые отличаются от ключевого поля, будут игнорироваться.</span><span class="sxs-lookup"><span data-stu-id="28afe-153">Any fields you specify other than the key field will be ignored.</span></span> <span data-ttu-id="28afe-154">Чтобы удалить из документа определенное поле, лучше воспользуйтесь операцией `Merge`, явным образом задав для требуемого поля значение NULL.</span><span class="sxs-lookup"><span data-stu-id="28afe-154">If you want to remove an individual field from a document, use `Merge` instead and simply set the field explicitly to null.</span></span> |

<span data-ttu-id="28afe-155">В следующем разделе показано, как можно выбрать действие, которое вы хотите использовать с различными статическими методами классов `IndexBatch` и `IndexAction`.</span><span class="sxs-lookup"><span data-stu-id="28afe-155">You can specify what action you want to use with the various static methods of the `IndexBatch` and `IndexAction` classes, as shown in the next section.</span></span>

## <a name="construct-your-indexbatch"></a><span data-ttu-id="28afe-156">Создание класса IndexBatch</span><span class="sxs-lookup"><span data-stu-id="28afe-156">Construct your IndexBatch</span></span>
<span data-ttu-id="28afe-157">Теперь, когда вы знаете, какие операции можно выполнять с документами, давайте создадим `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="28afe-157">Now that you know which actions to perform on your documents, you are ready to construct the `IndexBatch`.</span></span> <span data-ttu-id="28afe-158">В приведенном ниже примере показано, как создать пакет с несколькими разными операциями.</span><span class="sxs-lookup"><span data-stu-id="28afe-158">The example below shows how to create a batch with a few different actions.</span></span> <span data-ttu-id="28afe-159">Обратите внимание, что в нашем примере используется пользовательский класс с именем `Hotel` , сопоставленный с документом в индексе hotels.</span><span class="sxs-lookup"><span data-stu-id="28afe-159">Note that our example uses a custom class called `Hotel` that maps to a document in the "hotels" index.</span></span>

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
                Description = "Close to town hall and the river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

<span data-ttu-id="28afe-160">В этом случае в качестве операций поиска мы используем `Upload`, `MergeOrUpload` и `Delete`, что соответствует методам, вызываемым для класса `IndexAction`.</span><span class="sxs-lookup"><span data-stu-id="28afe-160">In this case, we are using `Upload`, `MergeOrUpload`, and `Delete` as our search actions, as specified by the methods called on the `IndexAction` class.</span></span>

<span data-ttu-id="28afe-161">Предположим, что пример индекса с именем hotels уже заполнен несколькими документами.</span><span class="sxs-lookup"><span data-stu-id="28afe-161">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="28afe-162">Обратите внимание: нам не понадобилось указывать все поля документа при использовании операции `MergeOrUpload`, а при использовании `Delete` мы указали только ключ документа (`HotelId`).</span><span class="sxs-lookup"><span data-stu-id="28afe-162">Note how we did not have to specify all the possible document fields when using `MergeOrUpload` and how we only specified the document key (`HotelId`) when using `Delete`.</span></span>

<span data-ttu-id="28afe-163">Также помните о том, что в один запрос на индексирование можно включить не более 1000 документов.</span><span class="sxs-lookup"><span data-stu-id="28afe-163">Also, note that you can only include up to 1000 documents in a single indexing request.</span></span>

> [!NOTE]
> <span data-ttu-id="28afe-164">В нашем примере к разным документами применяются разные действия.</span><span class="sxs-lookup"><span data-stu-id="28afe-164">In this example, we are applying different actions to different documents.</span></span> <span data-ttu-id="28afe-165">Если вы хотите выполнить одинаковые действия со всеми документами в пакете, вместо вызова метода `IndexBatch.New` следует использовать другие статические методы класса `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="28afe-165">If you wanted to perform the same actions across all documents in the batch, instead of calling `IndexBatch.New`, you could use the other static methods of `IndexBatch`.</span></span> <span data-ttu-id="28afe-166">Например, можно создать пакеты, вызвав метод `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` или `IndexBatch.Delete`.</span><span class="sxs-lookup"><span data-stu-id="28afe-166">For example, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete`.</span></span> <span data-ttu-id="28afe-167">Эти методы вместо объектов `IndexAction` принимают коллекцию документов (в нашем примере это объекты типа `Hotel`).</span><span class="sxs-lookup"><span data-stu-id="28afe-167">These methods take a collection of documents (objects of type `Hotel` in this example) instead of `IndexAction` objects.</span></span>
> 
> 

## <a name="import-data-to-the-index"></a><span data-ttu-id="28afe-168">Импорт данных в индекс</span><span class="sxs-lookup"><span data-stu-id="28afe-168">Import data to the index</span></span>
<span data-ttu-id="28afe-169">Теперь, когда у нас есть инициализированный объект `IndexBatch`, мы можем отправить его в индекс, вызвав метод `Documents.Index` для объекта `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="28afe-169">Now that you have an initialized `IndexBatch` object, you can send it to the index by calling `Documents.Index` on your `SearchIndexClient` object.</span></span> <span data-ttu-id="28afe-170">В следующем примере показано, как вызвать `Index`, а также выполнить несколько необходимых дополнительных действий.</span><span class="sxs-lookup"><span data-stu-id="28afe-170">The following example shows how to call `Index`, as well as some extra steps you will need to perform:</span></span>

```csharp
try
{
    indexClient.Documents.Index(batch);
}
catch (IndexBatchException e)
{
    // Sometimes when your Search service is under load, indexing will fail for some of the documents in
    // the batch. Depending on your application, you can take compensating actions like delaying and
    // retrying. For this simple demo, we just log the failed document keys and continue.
    Console.WriteLine(
        "Failed to index some of the documents: {0}",
        String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
}

Console.WriteLine("Waiting for documents to be indexed...\n");
Thread.Sleep(2000);
```

<span data-ttu-id="28afe-171">Обратите внимание на фрагмент `try`/`catch`, окружающий вызов метода `Index`.</span><span class="sxs-lookup"><span data-stu-id="28afe-171">Note the `try`/`catch` surrounding the call to the `Index` method.</span></span> <span data-ttu-id="28afe-172">Блок catch обрабатывает важные ошибки, которые могут возникнуть во время индексирования.</span><span class="sxs-lookup"><span data-stu-id="28afe-172">The catch block handles an important error case for indexing.</span></span> <span data-ttu-id="28afe-173">Если службе поиска Azure не удается индексировать некоторые документы в пакете, `Documents.Index` вызывает `IndexBatchException`.</span><span class="sxs-lookup"><span data-stu-id="28afe-173">If your Azure Search service fails to index some of the documents in the batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="28afe-174">Это может произойти, если вы индексируете документы службы при интенсивной нагрузке.</span><span class="sxs-lookup"><span data-stu-id="28afe-174">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="28afe-175">**Настоятельно рекомендуется явно обрабатывать этот случай в коде.**</span><span class="sxs-lookup"><span data-stu-id="28afe-175">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="28afe-176">Вы можете задержать и повторить попытку индексирования соответствующих документов либо занести ошибку в журнал и продолжить работу, как в нашем примере, а также выполнить другие действия в зависимости от требований вашего приложения к целостности данных.</span><span class="sxs-lookup"><span data-stu-id="28afe-176">You can delay and then retry indexing the documents that failed, or you can log and continue like the sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

<span data-ttu-id="28afe-177">В примере выше в коде указана двухсекундная задержка.</span><span class="sxs-lookup"><span data-stu-id="28afe-177">Finally, the code in the example above delays for two seconds.</span></span> <span data-ttu-id="28afe-178">Индексирование в службе поиска Azure происходит асинхронно, поэтому образец приложения должен подождать немного, пока документы не станут доступными для поиска.</span><span class="sxs-lookup"><span data-stu-id="28afe-178">Indexing happens asynchronously in your Azure Search service, so the sample application needs to wait a short time to ensure that the documents are available for searching.</span></span> <span data-ttu-id="28afe-179">Такие задержки обычно необходимы только в демонстрациях, тестах и примерах приложений.</span><span class="sxs-lookup"><span data-stu-id="28afe-179">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

<a name="HotelClass"></a>

### <a name="how-the-net-sdk-handles-documents"></a><span data-ttu-id="28afe-180">Обработка документов пакетом SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="28afe-180">How the .NET SDK handles documents</span></span>
<span data-ttu-id="28afe-181">Вас может интересовать, как пакет SDK для Поиска Azure в .NETможет передавать экземпляры пользовательского класса, например `Hotel` , в индекс.</span><span class="sxs-lookup"><span data-stu-id="28afe-181">You may be wondering how the Azure Search .NET SDK is able to upload instances of a user-defined class like `Hotel` to the index.</span></span> <span data-ttu-id="28afe-182">Чтобы ответить на этот вопрос, давайте рассмотрим класс `Hotel` , который сопоставлен со схемой индекса, определенной в статье [Создание индекса для службы поиска Azure с помощью .NET](search-create-index-dotnet.md#DefineIndex).</span><span class="sxs-lookup"><span data-stu-id="28afe-182">To help answer that question, let's look at the `Hotel` class, which maps to the index schema defined in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#DefineIndex):</span></span>

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

<span data-ttu-id="28afe-183">Прежде всего следует отметить, что каждое общедоступное свойство `Hotel` соответствует полю в определении индекса, но с одним ключевым отличием: имя каждого поля начинается со строчной буквы (нижнего регистра), в то время как имя каждого общего свойства `Hotel` начинается с прописной буквы (верхнего регистра).</span><span class="sxs-lookup"><span data-stu-id="28afe-183">The first thing to notice is that each public property of `Hotel` corresponds to a field in the index definition, but with one crucial difference: The name of each field starts with a lower-case letter ("camel case"), while the name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="28afe-184">Это часто встречается в приложениях .NET, выполняющих привязку данных, если целевая схема не подлежит управлению разработчика приложения.</span><span class="sxs-lookup"><span data-stu-id="28afe-184">This is a common scenario in .NET applications that perform data-binding where the target schema is outside the control of the application developer.</span></span> <span data-ttu-id="28afe-185">Чтобы не нарушать правил присвоения имен .NET, указывая имена свойств в нижнем регистре, вы можете сделать так, чтобы пакет SDK автоматически сопоставлял имена свойств в нижнем регистре, с помощью атрибута `[SerializePropertyNamesAsCamelCase]` .</span><span class="sxs-lookup"><span data-stu-id="28afe-185">Rather than having to violate the .NET naming guidelines by making property names camel-case, you can tell the SDK to map the property names to camel-case automatically with the `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="28afe-186">Пакет SDK службы поиска Azure для .NET использует библиотеку [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) для сериализации и десериализации настраиваемых объектов модели в JSON и обратно.</span><span class="sxs-lookup"><span data-stu-id="28afe-186">The Azure Search .NET SDK uses the [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library to serialize and deserialize your custom model objects to and from JSON.</span></span> <span data-ttu-id="28afe-187">При необходимости эту сериализацию можно настроить.</span><span class="sxs-lookup"><span data-stu-id="28afe-187">You can customize this serialization if needed.</span></span> <span data-ttu-id="28afe-188">Дополнительные сведения см. в разделе [Пользовательская сериализация с помощью JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="28afe-188">You can find more details in [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span></span> <span data-ttu-id="28afe-189">Например, в приведенном выше примере кода в свойстве `DescriptionFr` можно указать атрибут `[JsonProperty]`.</span><span class="sxs-lookup"><span data-stu-id="28afe-189">One example of this is the use of the `[JsonProperty]` attribute on the `DescriptionFr` property in the sample code above.</span></span>
> 
> 

<span data-ttu-id="28afe-190">Вторая важная составляющая класса `Hotel` — типы данных общих свойств.</span><span class="sxs-lookup"><span data-stu-id="28afe-190">The second important thing about the `Hotel` class are the data types of the public properties.</span></span> <span data-ttu-id="28afe-191">Типы .NET этих свойств сопоставляются с эквивалентными типами полей в определении индекса.</span><span class="sxs-lookup"><span data-stu-id="28afe-191">The .NET types of these properties map to their equivalent field types in the index definition.</span></span> <span data-ttu-id="28afe-192">Например, свойство строки `Category` сопоставляется с полем `category`, которое имеет тип `DataType.String`.</span><span class="sxs-lookup"><span data-stu-id="28afe-192">For example, the `Category` string property maps to the `category` field, which is of type `DataType.String`.</span></span> <span data-ttu-id="28afe-193">Аналогичные сопоставления присутствуют между типами `bool?` и `DataType.Boolean`, `DateTimeOffset?` и `DataType.DateTimeOffset` и т. д.</span><span class="sxs-lookup"><span data-stu-id="28afe-193">There are similar type mappings between `bool?` and `DataType.Boolean`, `DateTimeOffset?` and `DataType.DateTimeOffset`, and so forth.</span></span> <span data-ttu-id="28afe-194">Конкретные правила сопоставления типов указаны в описании метода `Documents.Get` в [справочнике по SDK для .NET службы поиска Azure](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="28afe-194">The specific rules for the type mapping are documented with the `Documents.Get` method in the [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span>

<span data-ttu-id="28afe-195">Возможность использовать собственные классы как документы работает и в обратную сторону. Вы также можете получать результаты поиска, настроив пакет SDK на автоматическую десериализацию в выбранный тип, как показано в [следующей статье](search-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="28afe-195">This ability to use your own classes as documents works in both directions; You can also retrieve search results and have the SDK automatically deserialize them to a type of your choice, as shown in the [next article](search-query-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="28afe-196">Пакет SDK для Поиска Azure в .NET также поддерживает документы динамических типов, поддерживающие класс `Document`, то есть сопоставление ключей и значений с именами и значениями полей.</span><span class="sxs-lookup"><span data-stu-id="28afe-196">The Azure Search .NET SDK also supports dynamically-typed documents using the `Document` class, which is a key/value mapping of field names to field values.</span></span> <span data-ttu-id="28afe-197">Это полезно в тех случаях, когда во время разработки вам неизвестна схема индекса или привязка к конкретным классам моделей нецелесообразна.</span><span class="sxs-lookup"><span data-stu-id="28afe-197">This is useful in scenarios where you don't know the index schema at design-time, or where it would be inconvenient to bind to specific model classes.</span></span> <span data-ttu-id="28afe-198">Все методы пакета SDK, связанные с документами, имеют перегрузки, работающие с классом `Document`, а также строго типизированные перегрузки, принимающие параметр универсального типа.</span><span class="sxs-lookup"><span data-stu-id="28afe-198">All the methods in the SDK that deal with documents have overloads that work with the `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="28afe-199">Пример кода в этой статье содержит перегрузки только второго типа.</span><span class="sxs-lookup"><span data-stu-id="28afe-199">Only the latter are used in the sample code in this article.</span></span>
> 
> 

<span data-ttu-id="28afe-200">**Почему следует использовать типы данных, допускающие значение NULL**</span><span class="sxs-lookup"><span data-stu-id="28afe-200">**Why you should use nullable data types**</span></span>

<span data-ttu-id="28afe-201">При разработке собственных классов модели для сопоставления с индексом поиска Azure рекомендуется объявлять свойства типов значений, такие как `bool` и `int`, допускающих нулевое значение (например: `bool?` вместо `bool`).</span><span class="sxs-lookup"><span data-stu-id="28afe-201">When designing your own model classes to map to an Azure Search index, we recommend declaring properties of value types such as `bool` and `int` to be nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="28afe-202">При использовании ненулевого свойства необходимо **гарантировать** , что документы в индексе не будут содержать значение NULL для соответствующего поля.</span><span class="sxs-lookup"><span data-stu-id="28afe-202">If you use a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="28afe-203">Ни пакет SDK, ни служба поиска Azure не помогут вам это обеспечить.</span><span class="sxs-lookup"><span data-stu-id="28afe-203">Neither the SDK nor the Azure Search service will help you to enforce this.</span></span>

<span data-ttu-id="28afe-204">Это не просто гипотетическое соображение. Представьте себе ситуацию, когда вы добавляете новое поле в существующий индекс с типом `DataType.Int32`.</span><span class="sxs-lookup"><span data-stu-id="28afe-204">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `DataType.Int32`.</span></span> <span data-ttu-id="28afe-205">После обновления определения индекса все документы будут иметь значение null для этого нового поля (поскольку все типы допускают значение NULL в службе поиска Azure).</span><span class="sxs-lookup"><span data-stu-id="28afe-205">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="28afe-206">Если затем для этого поля вы используете класс модели со свойством `int`, не допускающим нулевое значение, при попытке получения документов вы получите `JsonSerializationException` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="28afe-206">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="28afe-207">По этой причине по-прежнему рекомендуется использовать типы, допускающие значения NULL, в классах модели.</span><span class="sxs-lookup"><span data-stu-id="28afe-207">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28afe-208">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="28afe-208">Next steps</span></span>
<span data-ttu-id="28afe-209">Заполнив индекс службы поиска Azure, вы можете приступать к отправке запросов на поиск документов.</span><span class="sxs-lookup"><span data-stu-id="28afe-209">After populating your Azure Search index, you will be ready to start issuing queries to search for documents.</span></span> <span data-ttu-id="28afe-210">Дополнительные сведения см. в статье [Запросы в службе поиска Azure](search-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="28afe-210">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>

