---
title: "aaaSynonyms Предварительный Просмотр учебника в поиске Azure | Документы Microsoft"
description: "Добавьте индекс hello синонимы предварительной версии компонентов tooan в поиске Azure."
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
ms.openlocfilehash: 055c1cbafb945823a3dc4da0c522db236b1d192c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="synonym-preview-c-tutorial-for-azure-search"></a><span data-ttu-id="31e6d-103">Руководство по C# для синонимов (предварительная версия) в Поиске Azure</span><span class="sxs-lookup"><span data-stu-id="31e6d-103">Synonym (preview) C# tutorial for Azure Search</span></span>

<span data-ttu-id="31e6d-104">Синонимы разверните запроса путем сопоставления на условиях, считаются входной термин toohello семантически эквивалентны.</span><span class="sxs-lookup"><span data-stu-id="31e6d-104">Synonyms expand a query by matching on terms considered semantically equivalent toohello input term.</span></span> <span data-ttu-id="31e6d-105">Например может потребоваться документы toomatch «машина», содержащие hello слова «автомобиль» или «машина».</span><span class="sxs-lookup"><span data-stu-id="31e6d-105">For example, you might want "car" toomatch documents containing hello terms "automobile" or "vehicle".</span></span>

<span data-ttu-id="31e6d-106">В Поиске Azure синонимы определены в *сопоставлении синонимов* с помощью *правил сопоставления*, связывающих эквивалентные термины.</span><span class="sxs-lookup"><span data-stu-id="31e6d-106">In Azure Search, synonyms are defined in a *synonym map*, through *mapping rules* that associate equivalent terms.</span></span> <span data-ttu-id="31e6d-107">Создайте несколько карт синоним, задайте их как доступные tooany индекс ресурса службы и затем ссылаться на какие один toouse на уровне полей hello.</span><span class="sxs-lookup"><span data-stu-id="31e6d-107">You can create multiple synonym maps, post them as a service-wide resource available tooany index, and then reference which one toouse at hello field level.</span></span> <span data-ttu-id="31e6d-108">Во время обработки запроса кроме toosearching индекса поиска Azure выполняет поиск в сопоставлении синоним, если он указан на поля, используемые в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="31e6d-108">At query time, in addition toosearching an index, Azure Search does a lookup in a synonym map, if one is specified on fields used in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="31e6d-109">синонимы Hello компонент в настоящий момент в Предварительный просмотр и поддерживается в только hello последнюю предварительную версию API и версии пакета SDK (api-version = 2016-09-01-Preview, версия пакета SDK 4.x-preview).</span><span class="sxs-lookup"><span data-stu-id="31e6d-109">hello synonyms feature is currently in preview and only supported in hello latest preview API and SDK versions (api-version=2016-09-01-Preview, SDK version 4.x-preview).</span></span> <span data-ttu-id="31e6d-110">Портал Azure такую поддержку пока не предоставляет.</span><span class="sxs-lookup"><span data-stu-id="31e6d-110">There is no Azure portal support at this time.</span></span> <span data-ttu-id="31e6d-111">Предварительные версии API не регулируются Соглашением об уровне обслуживания, и так как предварительные возможности могут измениться, мы не рекомендуем использовать их в рабочих приложениях.</span><span class="sxs-lookup"><span data-stu-id="31e6d-111">Preview APIs are not under SLA and preview features may change, so we do not recommend using them in production applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31e6d-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="31e6d-112">Prerequisites</span></span>

<span data-ttu-id="31e6d-113">Учебник требования включают hello следующее:</span><span class="sxs-lookup"><span data-stu-id="31e6d-113">Tutorial requirements include hello following:</span></span>

* [<span data-ttu-id="31e6d-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="31e6d-114">Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="31e6d-115">Служба поиска Azure</span><span class="sxs-lookup"><span data-stu-id="31e6d-115">Azure Search service</span></span>](search-create-service-portal.md)
* [<span data-ttu-id="31e6d-116">Предварительная версия библиотеки Microsoft.Azure.Search .NET</span><span class="sxs-lookup"><span data-stu-id="31e6d-116">Preview version of Microsoft.Azure.Search .NET library</span></span>](https://aka.ms/search-sdk-preview)
* [<span data-ttu-id="31e6d-117">Как выполнить поиск Azure toouse из приложения .NET</span><span class="sxs-lookup"><span data-stu-id="31e6d-117">How toouse Azure Search from a .NET Application</span></span>](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a><span data-ttu-id="31e6d-118">Обзор</span><span class="sxs-lookup"><span data-stu-id="31e6d-118">Overview</span></span>

<span data-ttu-id="31e6d-119">До и после запросов показано значение hello синонимов.</span><span class="sxs-lookup"><span data-stu-id="31e6d-119">Before-and-after queries demonstrate hello value of synonyms.</span></span> <span data-ttu-id="31e6d-120">В этом руководстве мы используем пример приложения, выполняющий запросы и возвращающий результаты для примера индекса.</span><span class="sxs-lookup"><span data-stu-id="31e6d-120">In this tutorial, we use a sample application that executes queries and returns results on a sample index.</span></span> <span data-ttu-id="31e6d-121">Пример приложения Hello создает небольшой индекс с именем «гостиницы» заполняется двух документов.</span><span class="sxs-lookup"><span data-stu-id="31e6d-121">hello sample application creates a small index named "hotels" populated with two documents.</span></span> <span data-ttu-id="31e6d-122">приложение Hello выполняет запросов поиска с применением термины и фразы, которые не отображаются в индексе hello, включает hello синонимы, то проблем hello же поиск еще раз.</span><span class="sxs-lookup"><span data-stu-id="31e6d-122">hello application executes search queries using terms and phrases that do not appear in hello index, enables hello synonyms feature, then issues hello same searches again.</span></span> <span data-ttu-id="31e6d-123">Приведенный ниже код Hello показывает hello общий поток.</span><span class="sxs-lookup"><span data-stu-id="31e6d-123">hello code below demonstrates hello overall flow.</span></span>

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
      Thread.Sleep(10000); // Wait for hello changes toopropagate

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");

      Console.ReadKey();
  }
```
<span data-ttu-id="31e6d-124">Здравствуйте toocreate действия и заполнение индекса образец hello приведены в [как toouse Azure поиска из приложения .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span><span class="sxs-lookup"><span data-stu-id="31e6d-124">hello steps toocreate and populate hello sample index are explained in [How toouse Azure Search from a .NET Application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

## <a name="before-queries"></a><span data-ttu-id="31e6d-125">Запросы "до"</span><span class="sxs-lookup"><span data-stu-id="31e6d-125">"Before" queries</span></span>

<span data-ttu-id="31e6d-126">С помощью `RunQueriesWithNonExistentTermsInIndex` мы отправляли запросы на поиск таких терминов, как "пять звезд", "Интернет" и "отели среднего класса".</span><span class="sxs-lookup"><span data-stu-id="31e6d-126">In `RunQueriesWithNonExistentTermsInIndex`, we issue search queries with "five star", "internet", and "economy AND hotel".</span></span>
```csharp
Console.WriteLine("Search hello entire index for hello phrase \"five star\":\n");
results = indexClient.Documents.Search<Hotel>("\"five star\"", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello term 'internet':\n");
results = indexClient.Documents.Search<Hotel>("internet", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello terms 'economy' AND 'hotel':\n");
results = indexClient.Documents.Search<Hotel>("economy AND hotel", parameters);
WriteDocuments(results);
```
<span data-ttu-id="31e6d-127">Ни один из двух индексированных документов hello терминами hello, поэтому мы получаем следующие hello, выходные данные из hello сначала `RunQueriesWithNonExistentTermsInIndex`.</span><span class="sxs-lookup"><span data-stu-id="31e6d-127">Neither of hello two indexed documents contain hello terms, so we get hello following output from hello first `RunQueriesWithNonExistentTermsInIndex`.</span></span>
~~~
Search hello entire index for hello phrase "five star":

no document matched

Search hello entire index for hello term 'internet':

no document matched

Search hello entire index for hello terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a><span data-ttu-id="31e6d-128">Включение поиска синонимов</span><span class="sxs-lookup"><span data-stu-id="31e6d-128">Enable synonyms</span></span>

<span data-ttu-id="31e6d-129">Чтобы включить поиск синонимов, нам потребуется выполнить два действия.</span><span class="sxs-lookup"><span data-stu-id="31e6d-129">Enabling synonyms is a two-step process.</span></span> <span data-ttu-id="31e6d-130">Мы сначала определить и отправить правила синонима, а затем настройте поля toouse их.</span><span class="sxs-lookup"><span data-stu-id="31e6d-130">We first define and upload synonym rules and then configure fields toouse them.</span></span> <span data-ttu-id="31e6d-131">описывается процесс Hello в `UploadSynonyms` и `EnableSynonymsInHotelsIndex`.</span><span class="sxs-lookup"><span data-stu-id="31e6d-131">hello process is outlined in `UploadSynonyms` and `EnableSynonymsInHotelsIndex`.</span></span>

1. <span data-ttu-id="31e6d-132">Добавление службы поиска tooyour карты синоним.</span><span class="sxs-lookup"><span data-stu-id="31e6d-132">Add a synonym map tooyour search service.</span></span> <span data-ttu-id="31e6d-133">В `UploadSynonyms`, мы определить четыре правила в нашу карту синоним «desc synonymmap» и toohello служба отправки.</span><span class="sxs-lookup"><span data-stu-id="31e6d-133">In `UploadSynonyms`, we define four rules in our synonym map 'desc-synonymmap' and upload toohello service.</span></span>
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
<span data-ttu-id="31e6d-134">Карта синонима должно соответствовать toohello открытого стандарта `solr` формат.</span><span class="sxs-lookup"><span data-stu-id="31e6d-134">A synonym map must conform toohello open source standard `solr` format.</span></span> <span data-ttu-id="31e6d-135">Формат Hello описан в [синонимы в поиске Azure](search-synonyms.md) в разделе "hello" `Apache Solr synonym format`.</span><span class="sxs-lookup"><span data-stu-id="31e6d-135">hello format is explained in [Synonyms in Azure Search](search-synonyms.md) under hello section `Apache Solr synonym format`.</span></span>

2. <span data-ttu-id="31e6d-136">Настройка поля поиска toouse hello синоним схемы в определении индекса hello.</span><span class="sxs-lookup"><span data-stu-id="31e6d-136">Configure searchable fields toouse hello synonym map in hello index definition.</span></span> <span data-ttu-id="31e6d-137">В `EnableSynonymsInHotelsIndex`, мы можем добавить синонимы по двум полям `category` и `tags` путем установки hello `synonymMaps` имя свойства toohello hello вновь отправлен карты синоним.</span><span class="sxs-lookup"><span data-stu-id="31e6d-137">In `EnableSynonymsInHotelsIndex`, we enable synonyms on two fields `category` and `tags` by setting hello `synonymMaps` property toohello name of hello newly uploaded synonym map.</span></span>
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
<span data-ttu-id="31e6d-138">Когда вы добавите сопоставление синонимов, необходимость в перестроении индексов отпадет.</span><span class="sxs-lookup"><span data-stu-id="31e6d-138">When you add a synonym map, index rebuilds are not required.</span></span> <span data-ttu-id="31e6d-139">Добавление службы tooyour синоним карты и затем измените существующие определения полей в любой индекс toouse hello нового синонима карты.</span><span class="sxs-lookup"><span data-stu-id="31e6d-139">You can add a synonym map tooyour service, and then amend existing field definitions in any index toouse hello new synonym map.</span></span> <span data-ttu-id="31e6d-140">Добавление новых атрибутов Hello не оказывает влияния на доступность индекса.</span><span class="sxs-lookup"><span data-stu-id="31e6d-140">hello addition of new attributes has no impact on index availability.</span></span> <span data-ttu-id="31e6d-141">Здравствуйте, же правило применяется к выключению синонимы для поля.</span><span class="sxs-lookup"><span data-stu-id="31e6d-141">hello same applies in disabling synonyms for a field.</span></span> <span data-ttu-id="31e6d-142">Достаточно просто задать hello `synonymMaps` свойство tooan пустой список.</span><span class="sxs-lookup"><span data-stu-id="31e6d-142">You can simply set hello `synonymMaps` property tooan empty list.</span></span>
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a><span data-ttu-id="31e6d-143">Запросы "после"</span><span class="sxs-lookup"><span data-stu-id="31e6d-143">"After" queries</span></span>

<span data-ttu-id="31e6d-144">После отправки карты синоним hello и индекс hello обновленные toouse hello синоним карты, во-вторых hello `RunQueriesWithNonExistentTermsInIndex` вызова выводит hello следующее:</span><span class="sxs-lookup"><span data-stu-id="31e6d-144">After hello synonym map is uploaded and hello index is updated toouse hello synonym map, hello second `RunQueriesWithNonExistentTermsInIndex` call outputs hello following:</span></span>

~~~
Search hello entire index for hello phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
<span data-ttu-id="31e6d-145">первый запрос Hello находит hello документа из правила hello `five star=>luxury`.</span><span class="sxs-lookup"><span data-stu-id="31e6d-145">hello first query finds hello document from hello rule `five star=>luxury`.</span></span> <span data-ttu-id="31e6d-146">Hello второй запрос расширяет hello поиска с помощью `internet,wifi` и hello в-третьих, используя оба `hotel, motel` и `economy,inexpensive=>budget` в поиск документов hello их соответствие.</span><span class="sxs-lookup"><span data-stu-id="31e6d-146">hello second query expands hello search using `internet,wifi` and hello third using both `hotel, motel` and `economy,inexpensive=>budget` in finding hello documents they matched.</span></span>

<span data-ttu-id="31e6d-147">Добавление синонимов полностью изменяет интерфейс поиска hello.</span><span class="sxs-lookup"><span data-stu-id="31e6d-147">Adding synonyms completely changes hello search experience.</span></span> <span data-ttu-id="31e6d-148">В этом учебнике hello исходного запросов не tooreturn значимые результаты, даже если документы hello в наш индекс, соответствовали.</span><span class="sxs-lookup"><span data-stu-id="31e6d-148">In this tutorial, hello original queries failed tooreturn meaningful results even though hello documents in our index were relevant.</span></span> <span data-ttu-id="31e6d-149">Включение синонимы, мы разверните tooinclude индекс часто применяемые условия без данных toounderlying изменения в индекс hello.</span><span class="sxs-lookup"><span data-stu-id="31e6d-149">By enabling synonyms, we can expand an index tooinclude terms in common use, with no changes toounderlying data in hello index.</span></span>

## <a name="sample-application-source-code"></a><span data-ttu-id="31e6d-150">Исходный код образца приложения</span><span class="sxs-lookup"><span data-stu-id="31e6d-150">Sample application source code</span></span>
<span data-ttu-id="31e6d-151">Можно найти hello полный исходный код образца приложения hello, используемые в этом пошагового на [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span><span class="sxs-lookup"><span data-stu-id="31e6d-151">You can find hello full source code of hello sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span></span>

## <a name="next-steps"></a><span data-ttu-id="31e6d-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="31e6d-152">Next steps</span></span>

* <span data-ttu-id="31e6d-153">Просмотрите [как синонимы toouse в поиске Azure](search-synonyms.md)</span><span class="sxs-lookup"><span data-stu-id="31e6d-153">Review [How toouse synonyms in Azure Search](search-synonyms.md)</span></span>
* <span data-ttu-id="31e6d-154">Ознакомьтесь с [документацией по API REST для синонимов](https://aka.ms/rgm6rq).</span><span class="sxs-lookup"><span data-stu-id="31e6d-154">Review [Synonyms REST API documentation](https://aka.ms/rgm6rq)</span></span>
* <span data-ttu-id="31e6d-155">Обзор hello ссылки для hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) и [API-интерфейса REST](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="31e6d-155">Browse hello references for hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
