---
title: "aaaHow toomanage параллельных записывает tooresources в поиске Azure"
description: "Используйте среднего воздуху конфликтов оптимистичного параллелизма tooavoid индексы поиска tooAzure обновления или удаления, индексаторы, источники данных."
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
ms.openlocfilehash: c061d2b5c4d2dbd0fd5633405b01ab2912fbc754
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-concurrency-in-azure-search"></a><span data-ttu-id="0ca42-103">Как toomanage параллелизма в поиске Azure</span><span class="sxs-lookup"><span data-stu-id="0ca42-103">How toomanage concurrency in Azure Search</span></span>

<span data-ttu-id="0ca42-104">При управлении Azure поиск ресурсов, таких как индексы и источники данных, не tooupdate важные ресурсы безопасно, особенно если доступа к ресурсам параллельно разные компоненты приложения.</span><span class="sxs-lookup"><span data-stu-id="0ca42-104">When managing Azure Search resources such as indexes and data sources, it's important tooupdate resources safely, especially if resources are accessed concurrently by different components of your application.</span></span> <span data-ttu-id="0ca42-105">Если два клиента одновременно обновляют ресурс, не координируя свои действия, то могут возникать состояния гонки.</span><span class="sxs-lookup"><span data-stu-id="0ca42-105">When two clients concurrently update a resource without coordination, race conditions are possible.</span></span> <span data-ttu-id="0ca42-106">tooprevent, поиск Azure предлагает *модель оптимистичного параллелизма*.</span><span class="sxs-lookup"><span data-stu-id="0ca42-106">tooprevent this, Azure Search offers an *optimistic concurrency model*.</span></span> <span data-ttu-id="0ca42-107">При этом в отношении ресурса нет никаких блокировок.</span><span class="sxs-lookup"><span data-stu-id="0ca42-107">There are no locks on a resource.</span></span> <span data-ttu-id="0ca42-108">Вместо этого используется значение ETag для каждого ресурса, определяет версии ресурса hello, поэтому можно создавать запросы, которые позволяют избежать случайного перезаписывает.</span><span class="sxs-lookup"><span data-stu-id="0ca42-108">Instead, there is an ETag for every resource that identifies hello resource version so that you can craft requests that avoid accidental overwrites.</span></span>

> [!Tip]
> <span data-ttu-id="0ca42-109">Концептуальный код в [примере решения C#](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) объясняет, как работает функция управления параллелизмом в Поиске Azure.</span><span class="sxs-lookup"><span data-stu-id="0ca42-109">Conceptual code in a [sample C# solution](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explains how concurrency control works in Azure Search.</span></span> <span data-ttu-id="0ca42-110">Hello код создает условия, которые вызывают управления параллелизмом.</span><span class="sxs-lookup"><span data-stu-id="0ca42-110">hello code creates conditions that invoke concurrency control.</span></span> <span data-ttu-id="0ca42-111">Чтение hello [приведенный ниже фрагмент кода](#samplecode) вероятно, достаточно для большинства разработчиков, но следует toorun его, appsettings.json tooadd редактирования hello-имя службы и ключ api администратора.</span><span class="sxs-lookup"><span data-stu-id="0ca42-111">Reading hello [code fragment below](#samplecode) is probably sufficient for most developers, but if you want toorun it, edit appsettings.json tooadd hello service name and an admin api-key.</span></span> <span data-ttu-id="0ca42-112">Получает URL-адрес службы из `http://myservice.search.windows.net`, имя службы hello `myservice`.</span><span class="sxs-lookup"><span data-stu-id="0ca42-112">Given a service URL of `http://myservice.search.windows.net`, hello service name is `myservice`.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="0ca42-113">Принцип работы</span><span class="sxs-lookup"><span data-stu-id="0ca42-113">How it works</span></span>

<span data-ttu-id="0ca42-114">Оптимистического параллелизма реализуется посредством доступа условие проверяет записи tooindexes, индексаторы, источники данных и ресурсы synonymMap вызовы API.</span><span class="sxs-lookup"><span data-stu-id="0ca42-114">Optimistic concurrency is implemented through access condition checks in API calls writing tooindexes, indexers, datasources, and synonymMap resources.</span></span> 

<span data-ttu-id="0ca42-115">Все ресурсы имеют [*тег сущности (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag), который предоставляет сведения о версии объекта.</span><span class="sxs-lookup"><span data-stu-id="0ca42-115">All resources have an [*entity tag (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) that provides object version information.</span></span> <span data-ttu-id="0ca42-116">Проверяя hello ETag, позволяет избежать одновременных обновлений в обычный рабочий процесс (get, измените локально, обновление), обеспечивая соответствует ETag ресурса hello локальной копии.</span><span class="sxs-lookup"><span data-stu-id="0ca42-116">By checking hello ETag first, you can avoid concurrent updates in a typical workflow (get, modify locally, update) by ensuring hello resource's ETag matches your local copy.</span></span> 

+ <span data-ttu-id="0ca42-117">Hello REST API использует [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) в заголовке запроса hello.</span><span class="sxs-lookup"><span data-stu-id="0ca42-117">hello REST API uses an [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on hello request header.</span></span>
+ <span data-ttu-id="0ca42-118">Hello .NET SDK задает hello ETag через объект accessCondition параметр hello [If-Match | Заголовок If-Match-нет](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) hello ресурса.</span><span class="sxs-lookup"><span data-stu-id="0ca42-118">hello .NET SDK sets hello ETag through an accessCondition object, setting hello [If-Match | If-Match-None header](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on hello resource.</span></span> <span data-ttu-id="0ca42-119">Любой объект, наследуемый из [IResourceWithETag (пакет SDK для .NET)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag), содержит объект accessCondition.</span><span class="sxs-lookup"><span data-stu-id="0ca42-119">Any object inheriting from [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) has an accessCondition object.</span></span>

<span data-ttu-id="0ca42-120">Каждый раз при обновлении ресурса его ETag изменяется автоматически.</span><span class="sxs-lookup"><span data-stu-id="0ca42-120">Every time you update a resource, its ETag changes automatically.</span></span> <span data-ttu-id="0ca42-121">При реализации управления параллелизмом, вы выполняете помещают предусловия на запрос на обновление hello, требующий hello удаленный ресурс toohave hello же ETag, что копии hello hello ресурса, который был изменен на приветствия клиента.</span><span class="sxs-lookup"><span data-stu-id="0ca42-121">When you implement concurrency management, all you're doing is putting a precondition on hello update request that requires hello remote resource toohave hello same ETag as hello copy of hello resource that you modified on hello client.</span></span> <span data-ttu-id="0ca42-122">Если параллельный процесс уже изменен hello удаленному ресурсу, hello ETag не будет соответствовать предусловие hello и hello запрос завершится ошибкой с кодом HTTP 412.</span><span class="sxs-lookup"><span data-stu-id="0ca42-122">If a concurrent process has changed hello remote resource already, hello ETag will not match hello precondition and hello request will fail with HTTP 412.</span></span> <span data-ttu-id="0ca42-123">Если вы используете hello .NET SDK, это проявляющийся как `CloudException` где hello `IsAccessConditionFailed()` возвращает значение true, метод расширения.</span><span class="sxs-lookup"><span data-stu-id="0ca42-123">If you're using hello .NET SDK, this manifests as a `CloudException` where hello `IsAccessConditionFailed()` extension method returns true.</span></span>

> [!Note]
> <span data-ttu-id="0ca42-124">Для параллелизма существует только один механизм.</span><span class="sxs-lookup"><span data-stu-id="0ca42-124">There is only one mechanism for concurrency.</span></span> <span data-ttu-id="0ca42-125">Он всегда используется независимо от того, какой интерфейс API задействован для обновления ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0ca42-125">It's always used regardless of which API is used for resource updates.</span></span> 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a><span data-ttu-id="0ca42-126">Варианты использования и пример кода</span><span class="sxs-lookup"><span data-stu-id="0ca42-126">Use cases and sample code</span></span>

<span data-ttu-id="0ca42-127">Привет, следующий код демонстрирует accessCondition проверок для операций обновления ключа:</span><span class="sxs-lookup"><span data-stu-id="0ca42-127">hello following code demonstrates accessCondition checks for key update operations:</span></span>

+ <span data-ttu-id="0ca42-128">Сбой обновления, если hello ресурс больше не существует.</span><span class="sxs-lookup"><span data-stu-id="0ca42-128">Fail an update if hello resource no longer exists</span></span>
+ <span data-ttu-id="0ca42-129">Сбой обновления, если изменяется версия ресурса hello</span><span class="sxs-lookup"><span data-stu-id="0ca42-129">Fail an update if hello resource version changes</span></span>

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a><span data-ttu-id="0ca42-130">Пример кода из [программы DotNetETagsExplainer](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span><span class="sxs-lookup"><span data-stu-id="0ca42-130">Sample code from [DotNetETagsExplainer program](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span></span>

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
            // of hello resource you're working on. When you first create a resource such as an index, its ETag is
            // empty.
            Index index = DefineTestIndex();
            Console.WriteLine(
                $"Test index hasn't been created yet, so its ETag should be blank. ETag: '{index.ETag}'");

            // Once hello resource exists in Azure Search, its ETag will be populated. Make sure toouse hello object
            // returned by hello SearchServiceClient! Otherwise, you will still have hello old object with the
            // blank ETag.
            Console.WriteLine("Creating index...\n");
            index = serviceClient.Indexes.Create(index);
            
            Console.WriteLine($"Test index created; Its ETag should be populated. ETag: '{index.ETag}'");

            // ETags let you do some useful things you couldn't do otherwise. For example, by using an If-Match
            // condition, we can update an index using CreateOrUpdate and be guaranteed that hello update will only
            // succeed if hello index already exists.
            index.Fields.Add(new Field("name", AnalyzerName.EnMicrosoft));
            index =
                serviceClient.Indexes.CreateOrUpdate(
                    index,
                    accessCondition: AccessCondition.GenerateIfExistsCondition());

            Console.WriteLine(
                $"Test index updated; Its ETag should have changed since it was created. ETag: '{index.ETag}'");

            // More importantly, ETags protect you from concurrent updates toohello same resource. If another
            // client tries tooupdate hello resource, it will fail as long as all clients are using hello right
            // access conditions.
            Index indexForClient1 = index;
            Index indexForClient2 = serviceClient.Indexes.Get("test");

            Console.WriteLine("Simulating concurrent update. toostart, both clients see hello same ETag.");
            Console.WriteLine($"Client 1 ETag: '{indexForClient1.ETag}' Client 2 ETag: '{indexForClient2.ETag}'");

            // Client 1 successfully updates hello index.
            indexForClient1.Fields.Add(new Field("a", DataType.Int32));
            indexForClient1 =
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient1,
                    accessCondition: AccessCondition.IfNotChanged(indexForClient1));

            Console.WriteLine($"Test index updated by client 1; ETag: '{indexForClient1.ETag}'");

            // Client 2 tries tooupdate hello index, but fails, thanks toohello ETag check.
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
                Console.WriteLine("Client 2 failed tooupdate hello index, as expected.");
            }

            // You can also use access conditions with Delete operations. For example, you can implement an
            // atomic version of hello DeleteTestIndexIfExists method from this sample like this:
            Console.WriteLine("Deleting index...\n");
            serviceClient.Indexes.Delete("test", accessCondition: AccessCondition.GenerateIfExistsCondition());

            // This is slightly better than using hello Exists method since it makes only one round trip to
            // Azure Search instead of potentially two. It also avoids an extra Delete request in cases where
            // hello resource is deleted concurrently, but this doesn't matter much since resource deletion in
            // Azure Search is idempotent.

            // And we're done! Bye!
            Console.WriteLine("Complete.  Press any key tooend application...\n");
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

## <a name="design-pattern"></a><span data-ttu-id="0ca42-131">Конструктивный шаблон</span><span class="sxs-lookup"><span data-stu-id="0ca42-131">Design pattern</span></span>

<span data-ttu-id="0ca42-132">Шаблон разработки для реализации оптимистичного параллелизма должно включать цикл, который повторяет проверка условия доступа для hello, тест для hello условие доступа и при необходимости получает обновленный ресурс перед попыткой toore-применить изменения hello.</span><span class="sxs-lookup"><span data-stu-id="0ca42-132">A design pattern for implementing optimistic concurrency should include a loop that retries hello access condition check, a test for hello access condition, and optionally retrieves an updated resource before attempting toore-apply hello changes.</span></span> 

<span data-ttu-id="0ca42-133">Этот фрагмент кода иллюстрирует добавление hello индекса tooan synonymMap, который уже существует.</span><span class="sxs-lookup"><span data-stu-id="0ca42-133">This code snippet illustrates hello addition of a synonymMap tooan index that already exists.</span></span> <span data-ttu-id="0ca42-134">Этот фрагмент кода взят из hello [учебник синонима (Предварительная версия) C# для службы поиска Azure](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span><span class="sxs-lookup"><span data-stu-id="0ca42-134">This code is from hello [Synonym (preview) C# tutorial for Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span></span> 

<span data-ttu-id="0ca42-135">фрагмент кода Hello возвращает индекс гостиницы «hello», проверяет версию hello объекта на операции обновления, вызывает исключение, если hello условие не выполняется, а затем попыток hello операции (времен toothree), начиная с индекса извлечение hello server tooget hello последняя версия Версия.</span><span class="sxs-lookup"><span data-stu-id="0ca42-135">hello snippet gets hello "hotels" index, checks hello object version on an update operation, throws an exception if hello condition fails, and then retries hello operation (up toothree times), starting with index retrieval from hello server tooget hello latest version.</span></span>

        private static void EnableSynonymsInHotelsIndexSafely(SearchServiceClient serviceClient)
        {
            int MaxNumTries = 3;

            for (int i = 0; i < MaxNumTries; ++i)
            {
                try
                {
                    Index index = serviceClient.Indexes.Get("hotels");
                    index = AddSynonymMapsToFields(index);

                    // hello IfNotChanged condition ensures that hello index is updated only if hello ETags match.
                    serviceClient.Indexes.CreateOrUpdate(index, accessCondition: AccessCondition.IfNotChanged(index));

                    Console.WriteLine("Updated hello index successfully.\n");
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


## <a name="next-steps"></a><span data-ttu-id="0ca42-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0ca42-136">Next steps</span></span>

<span data-ttu-id="0ca42-137">Просмотрите hello [синонимы C# образца](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) дополнительный контекст, в том, как toosafely обновить существующий индекс.</span><span class="sxs-lookup"><span data-stu-id="0ca42-137">Review hello [synonyms C# sample](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) for more context on how toosafely update an existing index.</span></span>

<span data-ttu-id="0ca42-138">Рекомендуется изменить одно из следующих hello выборку tooinclude теги eTag или AccessCondition объектов.</span><span class="sxs-lookup"><span data-stu-id="0ca42-138">Try modifying either of hello following samples tooinclude ETags or AccessCondition objects.</span></span>

+ <span data-ttu-id="0ca42-139">[Пример REST API на портале Github](https://github.com/Azure-Samples/search-rest-api-getting-started).</span><span class="sxs-lookup"><span data-stu-id="0ca42-139">[REST API sample on Github](https://github.com/Azure-Samples/search-rest-api-getting-started)</span></span> 
+ <span data-ttu-id="0ca42-140">[Пример пакета SDK для .NET на портале Github](https://github.com/Azure-Samples/search-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="0ca42-140">[.NET SDK sample on Github](https://github.com/Azure-Samples/search-dotnet-getting-started).</span></span> <span data-ttu-id="0ca42-141">Это решение содержит проект «DotNetEtagsExplainer» hello, содержащий код hello, представленные в этой статье.</span><span class="sxs-lookup"><span data-stu-id="0ca42-141">This solution includes hello "DotNetEtagsExplainer" project containing hello code presented in this article.</span></span>

## <a name="see-also"></a><span data-ttu-id="0ca42-142">См. также</span><span class="sxs-lookup"><span data-stu-id="0ca42-142">See also</span></span>

  <span data-ttu-id="0ca42-143">[Common HTTP request and response headers used in Azure Search](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)   (Стандартные заголовки HTTP-запросов и ответов, используемые в Поиске Azure)</span><span class="sxs-lookup"><span data-stu-id="0ca42-143">[Common HTTP request and response headers](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span></span>  
  <span data-ttu-id="0ca42-144">[Коды состояния HTTP](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Операции с индексами (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span><span class="sxs-lookup"><span data-stu-id="0ca42-144">[HTTP status codes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Index operations (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span></span>