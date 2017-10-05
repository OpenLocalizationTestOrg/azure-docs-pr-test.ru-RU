---
title: "Руководство по предварительной версии синонимов в Поиске Azure | Документация Майкрософт"
description: "Добавление предварительной версии функции синонимов в индекс в Поиске Azure."
services: search
manager: jhubbard
documentationcenter: 
author: HeidiSteen
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 03/31/2017
ms.author: heidist
ms.openlocfilehash: 014959ed471f796d2184f0f8ff10d15cdc8a2ec6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="synonym-preview-c-tutorial-for-azure-search"></a><span data-ttu-id="6407b-103">Руководство по C# для синонимов (предварительная версия) в Поиске Azure</span><span class="sxs-lookup"><span data-stu-id="6407b-103">Synonym (preview) C# tutorial for Azure Search</span></span>

<span data-ttu-id="6407b-104">Синонимы позволяют расширить запрос с помощью сопоставления семантически эквивалентных терминов с входными терминами.</span><span class="sxs-lookup"><span data-stu-id="6407b-104">Synonyms expand a query by matching on terms considered semantically equivalent to the input term.</span></span> <span data-ttu-id="6407b-105">Например, вы можете сопоставить термин "машина" с документами, в которых встречается слово "автомобиль" или "транспортное средство".</span><span class="sxs-lookup"><span data-stu-id="6407b-105">For example, you might want "car" to match documents containing the terms "automobile" or "vehicle".</span></span>

<span data-ttu-id="6407b-106">В Поиске Azure синонимы определены в *сопоставлении синонимов* с помощью *правил сопоставления*, связывающих эквивалентные термины.</span><span class="sxs-lookup"><span data-stu-id="6407b-106">In Azure Search, synonyms are defined in a *synonym map*, through *mapping rules* that associate equivalent terms.</span></span> <span data-ttu-id="6407b-107">Вы можете создать несколько сопоставлений синонимов, разместить их как ресурс служб, доступный для любого индекса, а затем указать ссылку на используемый на уровне поля.</span><span class="sxs-lookup"><span data-stu-id="6407b-107">You can create multiple synonym maps, post them as a service-wide resource available to any index, and then reference which one to use at the field level.</span></span> <span data-ttu-id="6407b-108">Во время выполнения запроса, кроме поиска индекса, Поиск Azure обязательно просмотрит сопоставление синонимов, если один из них указан в каком-либо поле, используемом в этом запросе.</span><span class="sxs-lookup"><span data-stu-id="6407b-108">At query time, in addition to searching an index, Azure Search does a lookup in a synonym map, if one is specified on fields used in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="6407b-109">Сейчас возможности синонимов доступны в предварительной версии и поддерживаются только последними предварительными версиями API и пакетов SDK (предварительной версией API — 2016-09-01 и пакета SDK — 4.x).</span><span class="sxs-lookup"><span data-stu-id="6407b-109">The synonyms feature is currently in preview and only supported in the latest preview API and SDK versions (api-version=2016-09-01-Preview, SDK version 4.x-preview).</span></span> <span data-ttu-id="6407b-110">Портал Azure такую поддержку пока не предоставляет.</span><span class="sxs-lookup"><span data-stu-id="6407b-110">There is no Azure portal support at this time.</span></span> <span data-ttu-id="6407b-111">Предварительные версии API не регулируются Соглашением об уровне обслуживания, и так как предварительные возможности могут измениться, мы не рекомендуем использовать их в рабочих приложениях.</span><span class="sxs-lookup"><span data-stu-id="6407b-111">Preview APIs are not under SLA and preview features may change, so we do not recommend using them in production applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6407b-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6407b-112">Prerequisites</span></span>

<span data-ttu-id="6407b-113">Ниже приведены предварительные требования, описанные в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="6407b-113">Tutorial requirements include the following:</span></span>

* [<span data-ttu-id="6407b-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6407b-114">Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="6407b-115">Служба поиска Azure</span><span class="sxs-lookup"><span data-stu-id="6407b-115">Azure Search service</span></span>](search-create-service-portal.md)
* [<span data-ttu-id="6407b-116">Предварительная версия библиотеки Microsoft.Azure.Search .NET</span><span class="sxs-lookup"><span data-stu-id="6407b-116">Preview version of Microsoft.Azure.Search .NET library</span></span>](https://aka.ms/search-sdk-preview)
* [<span data-ttu-id="6407b-117">Использование службы поиска Azure в приложении .NET</span><span class="sxs-lookup"><span data-stu-id="6407b-117">How to use Azure Search from a .NET Application</span></span>](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a><span data-ttu-id="6407b-118">Обзор</span><span class="sxs-lookup"><span data-stu-id="6407b-118">Overview</span></span>

<span data-ttu-id="6407b-119">Значение синонимов показано в запросах "до" и "после".</span><span class="sxs-lookup"><span data-stu-id="6407b-119">Before-and-after queries demonstrate the value of synonyms.</span></span> <span data-ttu-id="6407b-120">В этом руководстве мы используем пример приложения, выполняющий запросы и возвращающий результаты для примера индекса.</span><span class="sxs-lookup"><span data-stu-id="6407b-120">In this tutorial, we use a sample application that executes queries and returns results on a sample index.</span></span> <span data-ttu-id="6407b-121">Пример приложения создает небольшой индекс с именем hotels с двумя документами.</span><span class="sxs-lookup"><span data-stu-id="6407b-121">The sample application creates a small index named "hotels" populated with two documents.</span></span> <span data-ttu-id="6407b-122">Приложение выполняет поисковые запросы с помощью терминов и фраз, которые отсутствуют в индексе, что вызывает функцию синонимов, и поиск выполняется повторно.</span><span class="sxs-lookup"><span data-stu-id="6407b-122">The application executes search queries using terms and phrases that do not appear in the index, enables the synonyms feature, then issues the same searches again.</span></span> <span data-ttu-id="6407b-123">В примере кода ниже показан общий поток.</span><span class="sxs-lookup"><span data-stu-id="6407b-123">The code below demonstrates the overall flow.</span></span>

```csharp
  static void Main(string[] args)
  {
      SearchServiceClient serviceClient = CreateSearchServiceClient();

      Console.WriteLine("{0}", "Cleaning up resources...\n");
      CleanupResources(serviceClient);

      Console.WriteLine("{0}", "Creating index...\n");
      CreateHotelsIndex(serviceClient);

      ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

      Console.WriteLine("{0}", "Uploading documents...\n");
      UploadDocuments(indexClient);

      ISearchIndexClient indexClientForQueries = CreateSearchIndexClient();

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Adding synonyms...\n");
      UploadSynonyms(serviceClient);
      EnableSynonymsInHotelsIndex(serviceClient);
      Thread.Sleep(10000); // Wait for the changes to propagate

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Complete.  Press any key to end application...\n");

      Console.ReadKey();
  }
```
<span data-ttu-id="6407b-124">В статье [Использование службы поиска Azure в приложении .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk) вы ознакомитесь с действиями по созданию и заполнению примера индекса.</span><span class="sxs-lookup"><span data-stu-id="6407b-124">The steps to create and populate the sample index are explained in [How to use Azure Search from a .NET Application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

## <a name="before-queries"></a><span data-ttu-id="6407b-125">Запросы "до"</span><span class="sxs-lookup"><span data-stu-id="6407b-125">"Before" queries</span></span>

<span data-ttu-id="6407b-126">С помощью `RunQueriesWithNonExistentTermsInIndex` мы отправляли запросы на поиск таких терминов, как "пять звезд", "Интернет" и "отели среднего класса".</span><span class="sxs-lookup"><span data-stu-id="6407b-126">In `RunQueriesWithNonExistentTermsInIndex`, we issue search queries with "five star", "internet", and "economy AND hotel".</span></span>
```csharp
Console.WriteLine("Search the entire index for the phrase \"five star\":\n");
results = indexClient.Documents.Search<Hotel>("\"five star\"", parameters);
WriteDocuments(results);

Console.WriteLine("Search the entire index for the term 'internet':\n");
results = indexClient.Documents.Search<Hotel>("internet", parameters);
WriteDocuments(results);

Console.WriteLine("Search the entire index for the terms 'economy' AND 'hotel':\n");
results = indexClient.Documents.Search<Hotel>("economy AND hotel", parameters);
WriteDocuments(results);
```
<span data-ttu-id="6407b-127">Ни в одном из двух индексированных документов нет этих выражений, поэтому мы используем следующие выходные данные из первой функции `RunQueriesWithNonExistentTermsInIndex`.</span><span class="sxs-lookup"><span data-stu-id="6407b-127">Neither of the two indexed documents contain the terms, so we get the following output from the first `RunQueriesWithNonExistentTermsInIndex`.</span></span>
~~~
Search the entire index for the phrase "five star":

no document matched

Search the entire index for the term 'internet':

no document matched

Search the entire index for the terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a><span data-ttu-id="6407b-128">Включение поиска синонимов</span><span class="sxs-lookup"><span data-stu-id="6407b-128">Enable synonyms</span></span>

<span data-ttu-id="6407b-129">Чтобы включить поиск синонимов, нам потребуется выполнить два действия.</span><span class="sxs-lookup"><span data-stu-id="6407b-129">Enabling synonyms is a two-step process.</span></span> <span data-ttu-id="6407b-130">Сначала нам необходимо определить и отправить правила синонимов, а затем настроить поля для их использования.</span><span class="sxs-lookup"><span data-stu-id="6407b-130">We first define and upload synonym rules and then configure fields to use them.</span></span> <span data-ttu-id="6407b-131">Описание этого процесса вы можете найти в `UploadSynonyms` и `EnableSynonymsInHotelsIndex`.</span><span class="sxs-lookup"><span data-stu-id="6407b-131">The process is outlined in `UploadSynonyms` and `EnableSynonymsInHotelsIndex`.</span></span>

1. <span data-ttu-id="6407b-132">Добавьте сопоставление синонимов в свою службу поиска.</span><span class="sxs-lookup"><span data-stu-id="6407b-132">Add a synonym map to your search service.</span></span> <span data-ttu-id="6407b-133">С помощью `UploadSynonyms` мы определим четыре правила в сопоставлении синонимов desc-synonymmap и добавим его в службу.</span><span class="sxs-lookup"><span data-stu-id="6407b-133">In `UploadSynonyms`, we define four rules in our synonym map 'desc-synonymmap' and upload to the service.</span></span>
```csharp
    var synonymMap = new SynonymMap()
    {
        Name = "desc-synonymmap",
        Format = "solr",
        Synonyms = "hotel, motel\n
                    internet,wifi\n
                    five star=>luxury\n
                    economy,inexpensive=>budget"
    };

    serviceClient.SynonymMaps.CreateOrUpdate(synonymMap);
```
<span data-ttu-id="6407b-134">Сопоставление синонимов должно соответствовать стандартному формату `solr` с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="6407b-134">A synonym map must conform to the open source standard `solr` format.</span></span> <span data-ttu-id="6407b-135">Сведения об этом формате вы найдете в разделе `Apache Solr synonym format` статьи [Synonyms in Azure Search](search-synonyms.md) (Синонимы в Поиске Azure).</span><span class="sxs-lookup"><span data-stu-id="6407b-135">The format is explained in [Synonyms in Azure Search](search-synonyms.md) under the section `Apache Solr synonym format`.</span></span>

2. <span data-ttu-id="6407b-136">Настройте поля, поддерживающие поиск, чтобы использовать сопоставление синонимов в определении индекса.</span><span class="sxs-lookup"><span data-stu-id="6407b-136">Configure searchable fields to use the synonym map in the index definition.</span></span> <span data-ttu-id="6407b-137">С помощью `EnableSynonymsInHotelsIndex` мы можем включить поиск синонимов для двух полей — `category` и `tags`. Для этого необходимо задать свойство `synonymMaps` для имени добавленного сопоставления синонимов.</span><span class="sxs-lookup"><span data-stu-id="6407b-137">In `EnableSynonymsInHotelsIndex`, we enable synonyms on two fields `category` and `tags` by setting the `synonymMaps` property to the name of the newly uploaded synonym map.</span></span>
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
<span data-ttu-id="6407b-138">Когда вы добавите сопоставление синонимов, необходимость в перестроении индексов отпадет.</span><span class="sxs-lookup"><span data-stu-id="6407b-138">When you add a synonym map, index rebuilds are not required.</span></span> <span data-ttu-id="6407b-139">Чтобы использовать новое сопоставление синонимов, вы можете добавить это сопоставление в свою службу, а затем изменить существующие определения полей в любом индексе.</span><span class="sxs-lookup"><span data-stu-id="6407b-139">You can add a synonym map to your service, and then amend existing field definitions in any index to use the new synonym map.</span></span> <span data-ttu-id="6407b-140">Добавление новых атрибутов никак не скажется на доступности индексов.</span><span class="sxs-lookup"><span data-stu-id="6407b-140">The addition of new attributes has no impact on index availability.</span></span> <span data-ttu-id="6407b-141">То же относится и к отключению поиска синонимов для поля.</span><span class="sxs-lookup"><span data-stu-id="6407b-141">The same applies in disabling synonyms for a field.</span></span> <span data-ttu-id="6407b-142">Вы можете просто задать для пустого списка свойство `synonymMaps`.</span><span class="sxs-lookup"><span data-stu-id="6407b-142">You can simply set the `synonymMaps` property to an empty list.</span></span>
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a><span data-ttu-id="6407b-143">Запросы "после"</span><span class="sxs-lookup"><span data-stu-id="6407b-143">"After" queries</span></span>

<span data-ttu-id="6407b-144">После добавления сопоставления синонимов и обновления индекса, необходимых для использования этого сопоставления, мы получаем следующие выходные данные, вызвав функцию `RunQueriesWithNonExistentTermsInIndex` второй раз:</span><span class="sxs-lookup"><span data-stu-id="6407b-144">After the synonym map is uploaded and the index is updated to use the synonym map, the second `RunQueriesWithNonExistentTermsInIndex` call outputs the following:</span></span>

~~~
Search the entire index for the phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search the entire index for the term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search the entire index for the terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
<span data-ttu-id="6407b-145">Первый запрос находит документ из правила `five star=>luxury`.</span><span class="sxs-lookup"><span data-stu-id="6407b-145">The first query finds the document from the rule `five star=>luxury`.</span></span> <span data-ttu-id="6407b-146">Для второго запроса поиск расширяется с помощью термина `internet,wifi`, а для третьего при поиске соответствующих документов используются оба термина запросов — `hotel, motel` и `economy,inexpensive=>budget`.</span><span class="sxs-lookup"><span data-stu-id="6407b-146">The second query expands the search using `internet,wifi` and the third using both `hotel, motel` and `economy,inexpensive=>budget` in finding the documents they matched.</span></span>

<span data-ttu-id="6407b-147">Добавление синонимов полностью изменяет возможности поиска.</span><span class="sxs-lookup"><span data-stu-id="6407b-147">Adding synonyms completely changes the search experience.</span></span> <span data-ttu-id="6407b-148">При работе с этим руководством исходным запросам не удалось вернуть информативные результаты, несмотря на соответствующие документы в индексе.</span><span class="sxs-lookup"><span data-stu-id="6407b-148">In this tutorial, the original queries failed to return meaningful results even though the documents in our index were relevant.</span></span> <span data-ttu-id="6407b-149">Включив поиск синонимов, мы можем расширить индекс, чтобы включить распространенные термины, не изменяя при этом базовые данные в индексе.</span><span class="sxs-lookup"><span data-stu-id="6407b-149">By enabling synonyms, we can expand an index to include terms in common use, with no changes to underlying data in the index.</span></span>

## <a name="sample-application-source-code"></a><span data-ttu-id="6407b-150">Исходный код образца приложения</span><span class="sxs-lookup"><span data-stu-id="6407b-150">Sample application source code</span></span>
<span data-ttu-id="6407b-151">Полный исходный код образца приложения, используемого в этом пошаговом руководстве, см. в репозитории [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span><span class="sxs-lookup"><span data-stu-id="6407b-151">You can find the full source code of the sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6407b-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6407b-152">Next steps</span></span>

* <span data-ttu-id="6407b-153">Ознакомьтесь со сведениями об [использовании синонимов в Поиске Azure](search-synonyms.md).</span><span class="sxs-lookup"><span data-stu-id="6407b-153">Review [How to use synonyms in Azure Search](search-synonyms.md)</span></span>
* <span data-ttu-id="6407b-154">Ознакомьтесь с [документацией по API REST для синонимов](https://aka.ms/rgm6rq).</span><span class="sxs-lookup"><span data-stu-id="6407b-154">Review [Synonyms REST API documentation](https://aka.ms/rgm6rq)</span></span>
* <span data-ttu-id="6407b-155">Изучите справочную информацию о [пакете SDK для .NET](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) и [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="6407b-155">Browse the references for the [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
