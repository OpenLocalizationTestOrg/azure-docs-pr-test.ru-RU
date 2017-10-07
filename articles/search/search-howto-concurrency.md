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
# <a name="how-toomanage-concurrency-in-azure-search"></a>Как toomanage параллелизма в поиске Azure

При управлении Azure поиск ресурсов, таких как индексы и источники данных, не tooupdate важные ресурсы безопасно, особенно если доступа к ресурсам параллельно разные компоненты приложения. Если два клиента одновременно обновляют ресурс, не координируя свои действия, то могут возникать состояния гонки. tooprevent, поиск Azure предлагает *модель оптимистичного параллелизма*. При этом в отношении ресурса нет никаких блокировок. Вместо этого используется значение ETag для каждого ресурса, определяет версии ресурса hello, поэтому можно создавать запросы, которые позволяют избежать случайного перезаписывает.

> [!Tip]
> Концептуальный код в [примере решения C#](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) объясняет, как работает функция управления параллелизмом в Поиске Azure. Hello код создает условия, которые вызывают управления параллелизмом. Чтение hello [приведенный ниже фрагмент кода](#samplecode) вероятно, достаточно для большинства разработчиков, но следует toorun его, appsettings.json tooadd редактирования hello-имя службы и ключ api администратора. Получает URL-адрес службы из `http://myservice.search.windows.net`, имя службы hello `myservice`.

## <a name="how-it-works"></a>Принцип работы

Оптимистического параллелизма реализуется посредством доступа условие проверяет записи tooindexes, индексаторы, источники данных и ресурсы synonymMap вызовы API. 

Все ресурсы имеют [*тег сущности (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag), который предоставляет сведения о версии объекта. Проверяя hello ETag, позволяет избежать одновременных обновлений в обычный рабочий процесс (get, измените локально, обновление), обеспечивая соответствует ETag ресурса hello локальной копии. 

+ Hello REST API использует [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) в заголовке запроса hello.
+ Hello .NET SDK задает hello ETag через объект accessCondition параметр hello [If-Match | Заголовок If-Match-нет](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) hello ресурса. Любой объект, наследуемый из [IResourceWithETag (пакет SDK для .NET)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag), содержит объект accessCondition.

Каждый раз при обновлении ресурса его ETag изменяется автоматически. При реализации управления параллелизмом, вы выполняете помещают предусловия на запрос на обновление hello, требующий hello удаленный ресурс toohave hello же ETag, что копии hello hello ресурса, который был изменен на приветствия клиента. Если параллельный процесс уже изменен hello удаленному ресурсу, hello ETag не будет соответствовать предусловие hello и hello запрос завершится ошибкой с кодом HTTP 412. Если вы используете hello .NET SDK, это проявляющийся как `CloudException` где hello `IsAccessConditionFailed()` возвращает значение true, метод расширения.

> [!Note]
> Для параллелизма существует только один механизм. Он всегда используется независимо от того, какой интерфейс API задействован для обновления ресурсов. 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a>Варианты использования и пример кода

Привет, следующий код демонстрирует accessCondition проверок для операций обновления ключа:

+ Сбой обновления, если hello ресурс больше не существует.
+ Сбой обновления, если изменяется версия ресурса hello

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a>Пример кода из [программы DotNetETagsExplainer](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)

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

## <a name="design-pattern"></a>Конструктивный шаблон

Шаблон разработки для реализации оптимистичного параллелизма должно включать цикл, который повторяет проверка условия доступа для hello, тест для hello условие доступа и при необходимости получает обновленный ресурс перед попыткой toore-применить изменения hello. 

Этот фрагмент кода иллюстрирует добавление hello индекса tooan synonymMap, который уже существует. Этот фрагмент кода взят из hello [учебник синонима (Предварительная версия) C# для службы поиска Azure](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk). 

фрагмент кода Hello возвращает индекс гостиницы «hello», проверяет версию hello объекта на операции обновления, вызывает исключение, если hello условие не выполняется, а затем попыток hello операции (времен toothree), начиная с индекса извлечение hello server tooget hello последняя версия Версия.

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


## <a name="next-steps"></a>Дальнейшие действия

Просмотрите hello [синонимы C# образца](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) дополнительный контекст, в том, как toosafely обновить существующий индекс.

Рекомендуется изменить одно из следующих hello выборку tooinclude теги eTag или AccessCondition объектов.

+ [Пример REST API на портале Github](https://github.com/Azure-Samples/search-rest-api-getting-started). 
+ [Пример пакета SDK для .NET на портале Github](https://github.com/Azure-Samples/search-dotnet-getting-started). Это решение содержит проект «DotNetEtagsExplainer» hello, содержащий код hello, представленные в этой статье.

## <a name="see-also"></a>См. также

  [Common HTTP request and response headers used in Azure Search](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)   (Стандартные заголовки HTTP-запросов и ответов, используемые в Поиске Azure)  
  [Коды состояния HTTP](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Операции с индексами (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)