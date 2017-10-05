---
title: "Управление одновременными операциями записи в ресурсы Поиска Azure"
description: "Узнайте, как использовать оптимистическую блокировку во избежание конфликтов в процессе обновления или удаления индексов, индексаторов и источников данных Поиска Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 
ms.service: search
ms.devlang: 
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: heidist
ms.openlocfilehash: aee1b7376d4829e3e2f5a232525e3c3cb4df9d8e
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="how-to-manage-concurrency-in-azure-search"></a><span data-ttu-id="79786-103">Управление параллелизмом в Поиске Azure</span><span class="sxs-lookup"><span data-stu-id="79786-103">How to manage concurrency in Azure Search</span></span>

<span data-ttu-id="79786-104">При управлении ресурсами Поиска Azure, такими как индексы и источники данных, важно выполнить обновление ресурсов безопасно, особенно если доступ к ним осуществляется параллельно разными компонентами приложения.</span><span class="sxs-lookup"><span data-stu-id="79786-104">When managing Azure Search resources such as indexes and data sources, it's important to update resources safely, especially if resources are accessed concurrently by different components of your application.</span></span> <span data-ttu-id="79786-105">Если два клиента одновременно обновляют ресурс, не координируя свои действия, то могут возникать состояния гонки.</span><span class="sxs-lookup"><span data-stu-id="79786-105">When two clients concurrently update a resource without coordination, race conditions are possible.</span></span> <span data-ttu-id="79786-106">Во избежание таких ситуаций Поиск Azure предлагает *модель оптимистической блокировки*.</span><span class="sxs-lookup"><span data-stu-id="79786-106">To prevent this, Azure Search offers an *optimistic concurrency model*.</span></span> <span data-ttu-id="79786-107">При этом в отношении ресурса нет никаких блокировок.</span><span class="sxs-lookup"><span data-stu-id="79786-107">There are no locks on a resource.</span></span> <span data-ttu-id="79786-108">Для каждого ресурса существует тег ETag, который определяет версию ресурса. Это позволяет создавать запросы, избегая случайных перезаписей.</span><span class="sxs-lookup"><span data-stu-id="79786-108">Instead, there is an ETag for every resource that identifies the resource version so that you can craft requests that avoid accidental overwrites.</span></span>

> [!Tip]
> <span data-ttu-id="79786-109">Концептуальный код в [примере решения C#](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) объясняет, как работает функция управления параллелизмом в Поиске Azure.</span><span class="sxs-lookup"><span data-stu-id="79786-109">Conceptual code in a [sample C# solution](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explains how concurrency control works in Azure Search.</span></span> <span data-ttu-id="79786-110">Код создает условия, которые вызывают управление параллелизмом.</span><span class="sxs-lookup"><span data-stu-id="79786-110">The code creates conditions that invoke concurrency control.</span></span> <span data-ttu-id="79786-111">Большинству разработчиков, скорее всего, достаточно будет прочитать [приведенный ниже фрагмент кода](#samplecode), но если вы хотите выполнить его, то измените файл appsettings.json, добавив имя службы и ключ API администратора.</span><span class="sxs-lookup"><span data-stu-id="79786-111">Reading the [code fragment below](#samplecode) is probably sufficient for most developers, but if you want to run it, edit appsettings.json to add the service name and an admin api-key.</span></span> <span data-ttu-id="79786-112">URL-адрес службы — `http://myservice.search.windows.net`, а имя службы — `myservice`.</span><span class="sxs-lookup"><span data-stu-id="79786-112">Given a service URL of `http://myservice.search.windows.net`, the service name is `myservice`.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="79786-113">Принцип работы</span><span class="sxs-lookup"><span data-stu-id="79786-113">How it works</span></span>

<span data-ttu-id="79786-114">Оптимистическая блокировка реализуется за счет проверки условий доступа в вызовах API при записи в индексы, индексаторы, источники данных и ресурсы synonymMap.</span><span class="sxs-lookup"><span data-stu-id="79786-114">Optimistic concurrency is implemented through access condition checks in API calls writing to indexes, indexers, datasources, and synonymMap resources.</span></span> 

<span data-ttu-id="79786-115">Все ресурсы имеют [*тег сущности (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag), который предоставляет сведения о версии объекта.</span><span class="sxs-lookup"><span data-stu-id="79786-115">All resources have an [*entity tag (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) that provides object version information.</span></span> <span data-ttu-id="79786-116">Если сначала проверить ETag, то можно избежать параллельных обновлений в стандартном рабочем процессе (получение, локальное изменение, обновление), убедившись, что ETag ресурса соответствует локальной копии.</span><span class="sxs-lookup"><span data-stu-id="79786-116">By checking the ETag first, you can avoid concurrent updates in a typical workflow (get, modify locally, update) by ensuring the resource's ETag matches your local copy.</span></span> 

+ <span data-ttu-id="79786-117">Интерфейс REST API использует [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) в заголовке запроса.</span><span class="sxs-lookup"><span data-stu-id="79786-117">The REST API uses an [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on the request header.</span></span>
+ <span data-ttu-id="79786-118">Пакет SDK для .NET задает ETag с помощью объекта accessCondition, устанавливая в ресурсе [заголовок If-Match | If-None-Match](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search).</span><span class="sxs-lookup"><span data-stu-id="79786-118">The .NET SDK sets the ETag through an accessCondition object, setting the [If-Match | If-Match-None header](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on the resource.</span></span> <span data-ttu-id="79786-119">Любой объект, наследуемый из [IResourceWithETag (пакет SDK для .NET)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag), содержит объект accessCondition.</span><span class="sxs-lookup"><span data-stu-id="79786-119">Any object inheriting from [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) has an accessCondition object.</span></span>

<span data-ttu-id="79786-120">Каждый раз при обновлении ресурса его ETag изменяется автоматически.</span><span class="sxs-lookup"><span data-stu-id="79786-120">Every time you update a resource, its ETag changes automatically.</span></span> <span data-ttu-id="79786-121">При реализации управления параллелизмом все, что необходимо сделать, это поместить предварительное условие в запрос на обновление. Этим условием должно быть требование, чтобы удаленный ресурс имел такой же ETag, как и копия ресурса, измененного вами на клиенте.</span><span class="sxs-lookup"><span data-stu-id="79786-121">When you implement concurrency management, all you're doing is putting a precondition on the update request that requires the remote resource to have the same ETag as the copy of the resource that you modified on the client.</span></span> <span data-ttu-id="79786-122">Если параллельный процесс уже изменил удаленный ресурс, то ETag не будет соответствовать предварительному условию и, следовательно, запрос завершится ошибкой HTTP 412.</span><span class="sxs-lookup"><span data-stu-id="79786-122">If a concurrent process has changed the remote resource already, the ETag will not match the precondition and the request will fail with HTTP 412.</span></span> <span data-ttu-id="79786-123">Если используется пакет SDK для .NET, то это объявляется в качестве `CloudException`, где метод расширения `IsAccessConditionFailed()` возвращает значение true.</span><span class="sxs-lookup"><span data-stu-id="79786-123">If you're using the .NET SDK, this manifests as a `CloudException` where the `IsAccessConditionFailed()` extension method returns true.</span></span>

> [!Note]
> <span data-ttu-id="79786-124">Для параллелизма существует только один механизм.</span><span class="sxs-lookup"><span data-stu-id="79786-124">There is only one mechanism for concurrency.</span></span> <span data-ttu-id="79786-125">Он всегда используется независимо от того, какой интерфейс API задействован для обновления ресурсов.</span><span class="sxs-lookup"><span data-stu-id="79786-125">It's always used regardless of which API is used for resource updates.</span></span> 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a><span data-ttu-id="79786-126">Варианты использования и пример кода</span><span class="sxs-lookup"><span data-stu-id="79786-126">Use cases and sample code</span></span>

<span data-ttu-id="79786-127">В следующем коде показано, как проверяется условие accessCondition для операций обновления ключа:</span><span class="sxs-lookup"><span data-stu-id="79786-127">The following code demonstrates accessCondition checks for key update operations:</span></span>

+ <span data-ttu-id="79786-128">Сбой обновления, если ресурс больше не существует</span><span class="sxs-lookup"><span data-stu-id="79786-128">Fail an update if the resource no longer exists</span></span>
+ <span data-ttu-id="79786-129">Сбой обновления, если версия ресурса изменяется</span><span class="sxs-lookup"><span data-stu-id="79786-129">Fail an update if the resource version changes</span></span>

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a><span data-ttu-id="79786-130">Пример кода из [программы DotNetETagsExplainer](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span><span class="sxs-lookup"><span data-stu-id="79786-130">Sample code from [DotNetETagsExplainer program](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span></span>

```
    class Program
    {
        // This sample shows how ETags work by performing conditional updates and deletes
        // on an Azure Search index.
        static void Main(string[] args)
        {
            IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
            IConfigurationRoot configuration = builder.Build();

            SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

            Console.WriteLine("Deleting index...\n");
            DeleteTestIndexIfExists(serviceClient);

            // Every top-level resource in Azure Search has an associated ETag that keeps track of which version
            // of the resource you're working on. When you first create a resource such as an index, its ETag is
            // empty.
            Index index = DefineTestIndex();
            Console.WriteLine(
                $"Test index hasn't been created yet, so its ETag should be blank. ETag: '{index.ETag}'");

            // Once the resource exists in Azure Search, its ETag will be populated. Make sure to use the object
            // returned by the SearchServiceClient! Otherwise, you will still have the old object with the
            // blank ETag.
            Console.WriteLine("Creating index...\n");
            index = serviceClient.Indexes.Create(index);
            
            Console.WriteLine($"Test index created; Its ETag should be populated. ETag: '{index.ETag}'");

            // ETags let you do some useful things you couldn't do otherwise. For example, by using an If-Match
            // condition, we can update an index using CreateOrUpdate and be guaranteed that the update will only
            // succeed if the index already exists.
            index.Fields.Add(new Field("name", AnalyzerName.EnMicrosoft));
            index =
                serviceClient.Indexes.CreateOrUpdate(
                    index,
                    accessCondition: AccessCondition.GenerateIfExistsCondition());

            Console.WriteLine(
                $"Test index updated; Its ETag should have changed since it was created. ETag: '{index.ETag}'");

            // More importantly, ETags protect you from concurrent updates to the same resource. If another
            // client tries to update the resource, it will fail as long as all clients are using the right
            // access conditions.
            Index indexForClient1 = index;
            Index indexForClient2 = serviceClient.Indexes.Get("test");

            Console.WriteLine("Simulating concurrent update. To start, both clients see the same ETag.");
            Console.WriteLine($"Client 1 ETag: '{indexForClient1.ETag}' Client 2 ETag: '{indexForClient2.ETag}'");

            // Client 1 successfully updates the index.
            indexForClient1.Fields.Add(new Field("a", DataType.Int32));
            indexForClient1 =
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient1,
                    accessCondition: AccessCondition.IfNotChanged(indexForClient1));

            Console.WriteLine($"Test index updated by client 1; ETag: '{indexForClient1.ETag}'");

            // Client 2 tries to update the index, but fails, thanks to the ETag check.
            try
            {
                indexForClient2.Fields.Add(new Field("b", DataType.Boolean));
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient2, 
                    accessCondition: AccessCondition.IfNotChanged(indexForClient2));

                Console.WriteLine("Whoops; This shouldn't happen");
                Environment.Exit(1);
            }
            catch (CloudException e) when (e.IsAccessConditionFailed())
            {
                Console.WriteLine("Client 2 failed to update the index, as expected.");
            }

            // You can also use access conditions with Delete operations. For example, you can implement an
            // atomic version of the DeleteTestIndexIfExists method from this sample like this:
            Console.WriteLine("Deleting index...\n");
            serviceClient.Indexes.Delete("test", accessCondition: AccessCondition.GenerateIfExistsCondition());

            // This is slightly better than using the Exists method since it makes only one round trip to
            // Azure Search instead of potentially two. It also avoids an extra Delete request in cases where
            // the resource is deleted concurrently, but this doesn't matter much since resource deletion in
            // Azure Search is idempotent.

            // And we're done! Bye!
            Console.WriteLine("Complete.  Press any key to end application...\n");
            Console.ReadKey();
        }

        private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
        {
            string searchServiceName = configuration["SearchServiceName"];
            string adminApiKey = configuration["SearchServiceAdminApiKey"];

            SearchServiceClient serviceClient =
                new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
            return serviceClient;
        }

        private static void DeleteTestIndexIfExists(SearchServiceClient serviceClient)
        {
            if (serviceClient.Indexes.Exists("test"))
            {
                serviceClient.Indexes.Delete("test");
            }
        }

        private static Index DefineTestIndex() =>
            new Index()
            {
                Name = "test",
                Fields = new[] { new Field("id", DataType.String) { IsKey = true } }
            };
    }
}
```

## <a name="design-pattern"></a><span data-ttu-id="79786-131">Конструктивный шаблон</span><span class="sxs-lookup"><span data-stu-id="79786-131">Design pattern</span></span>

<span data-ttu-id="79786-132">Конструктивный шаблон для реализации оптимистической блокировки должен включать в себя цикл повторных попыток проверки условия доступа, тест для условия доступа и, при необходимости, должен получать обновленный ресурс перед попыткой повторного применения изменений.</span><span class="sxs-lookup"><span data-stu-id="79786-132">A design pattern for implementing optimistic concurrency should include a loop that retries the access condition check, a test for the access condition, and optionally retrieves an updated resource before attempting to re-apply the changes.</span></span> 

<span data-ttu-id="79786-133">В этом фрагменте кода показано добавление synonymMap в индекс, который уже существует.</span><span class="sxs-lookup"><span data-stu-id="79786-133">This code snippet illustrates the addition of a synonymMap to an index that already exists.</span></span> <span data-ttu-id="79786-134">Этот код взят из [руководства по C# для синонимов (предварительная версия) в Поиске Azure](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span><span class="sxs-lookup"><span data-stu-id="79786-134">This code is from the [Synonym (preview) C# tutorial for Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span></span> 

<span data-ttu-id="79786-135">Этот фрагмент получает индекс "hotels", проверяет версию объекта при операции обновления, порождает исключение, если условие не выполняется, а затем совершает повторную попытку операции (до трех раз), начиная с извлечения индекса с сервера, чтобы получить последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="79786-135">The snippet gets the "hotels" index, checks the object version on an update operation, throws an exception if the condition fails, and then retries the operation (up to three times), starting with index retrieval from the server to get the latest version.</span></span>

        private static void EnableSynonymsInHotelsIndexSafely(SearchServiceClient serviceClient)
        {
            int MaxNumTries = 3;

            for (int i = 0; i < MaxNumTries; ++i)
            {
                try
                {
                    Index index = serviceClient.Indexes.Get("hotels");
                    index = AddSynonymMapsToFields(index);

                    // The IfNotChanged condition ensures that the index is updated only if the ETags match.
                    serviceClient.Indexes.CreateOrUpdate(index, accessCondition: AccessCondition.IfNotChanged(index));

                    Console.WriteLine("Updated the index successfully.\n");
                    break;
                }
                catch (CloudException e) when (e.IsAccessConditionFailed())
                {
                    Console.WriteLine($"Index update failed : {e.Message}. Attempt({i}/{MaxNumTries}).\n");
                }
            }
        }
        
        private static Index AddSynonymMapsToFields(Index index)
        {
            index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
            index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };
            return index;
        }


## <a name="next-steps"></a><span data-ttu-id="79786-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="79786-136">Next steps</span></span>

<span data-ttu-id="79786-137">Просмотрите [пример кода C# для синонимов](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms), чтобы получить дополнительные сведения о безопасном обновлении существующего индекса.</span><span class="sxs-lookup"><span data-stu-id="79786-137">Review the [synonyms C# sample](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) for more context on how to safely update an existing index.</span></span>

<span data-ttu-id="79786-138">Попробуйте изменить один из следующих примеров, включив теги ETags или объекты AccessCondition.</span><span class="sxs-lookup"><span data-stu-id="79786-138">Try modifying either of the following samples to include ETags or AccessCondition objects.</span></span>

+ <span data-ttu-id="79786-139">[Пример REST API на портале Github](https://github.com/Azure-Samples/search-rest-api-getting-started).</span><span class="sxs-lookup"><span data-stu-id="79786-139">[REST API sample on Github](https://github.com/Azure-Samples/search-rest-api-getting-started)</span></span> 
+ <span data-ttu-id="79786-140">[Пример пакета SDK для .NET на портале Github](https://github.com/Azure-Samples/search-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="79786-140">[.NET SDK sample on Github](https://github.com/Azure-Samples/search-dotnet-getting-started).</span></span> <span data-ttu-id="79786-141">Это решение включает в себя проект DotNetEtagsExplainer, который содержит код, представленный в этой статье.</span><span class="sxs-lookup"><span data-stu-id="79786-141">This solution includes the "DotNetEtagsExplainer" project containing the code presented in this article.</span></span>

## <a name="see-also"></a><span data-ttu-id="79786-142">См. также</span><span class="sxs-lookup"><span data-stu-id="79786-142">See also</span></span>

  <span data-ttu-id="79786-143">[Common HTTP request and response headers used in Azure Search](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)   (Стандартные заголовки HTTP-запросов и ответов, используемые в Поиске Azure)</span><span class="sxs-lookup"><span data-stu-id="79786-143">[Common HTTP request and response headers](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span></span>  
  <span data-ttu-id="79786-144">[Коды состояния HTTP](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Операции с индексами (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span><span class="sxs-lookup"><span data-stu-id="79786-144">[HTTP status codes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Index operations (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span></span>