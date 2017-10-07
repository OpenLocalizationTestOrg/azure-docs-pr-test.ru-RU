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
# <a name="synonym-preview-c-tutorial-for-azure-search"></a>Руководство по C# для синонимов (предварительная версия) в Поиске Azure

Синонимы разверните запроса путем сопоставления на условиях, считаются входной термин toohello семантически эквивалентны. Например может потребоваться документы toomatch «машина», содержащие hello слова «автомобиль» или «машина».

В Поиске Azure синонимы определены в *сопоставлении синонимов* с помощью *правил сопоставления*, связывающих эквивалентные термины. Создайте несколько карт синоним, задайте их как доступные tooany индекс ресурса службы и затем ссылаться на какие один toouse на уровне полей hello. Во время обработки запроса кроме toosearching индекса поиска Azure выполняет поиск в сопоставлении синоним, если он указан на поля, используемые в запросе hello.

> [!NOTE]
> синонимы Hello компонент в настоящий момент в Предварительный просмотр и поддерживается в только hello последнюю предварительную версию API и версии пакета SDK (api-version = 2016-09-01-Preview, версия пакета SDK 4.x-preview). Портал Azure такую поддержку пока не предоставляет. Предварительные версии API не регулируются Соглашением об уровне обслуживания, и так как предварительные возможности могут измениться, мы не рекомендуем использовать их в рабочих приложениях.

## <a name="prerequisites"></a>Предварительные требования

Учебник требования включают hello следующее:

* [Visual Studio](https://www.visualstudio.com/downloads/)
* [Служба поиска Azure](search-create-service-portal.md)
* [Предварительная версия библиотеки Microsoft.Azure.Search .NET](https://aka.ms/search-sdk-preview)
* [Как выполнить поиск Azure toouse из приложения .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a>Обзор

До и после запросов показано значение hello синонимов. В этом руководстве мы используем пример приложения, выполняющий запросы и возвращающий результаты для примера индекса. Пример приложения Hello создает небольшой индекс с именем «гостиницы» заполняется двух документов. приложение Hello выполняет запросов поиска с применением термины и фразы, которые не отображаются в индексе hello, включает hello синонимы, то проблем hello же поиск еще раз. Приведенный ниже код Hello показывает hello общий поток.

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
Здравствуйте toocreate действия и заполнение индекса образец hello приведены в [как toouse Azure поиска из приложения .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).

## <a name="before-queries"></a>Запросы "до"

С помощью `RunQueriesWithNonExistentTermsInIndex` мы отправляли запросы на поиск таких терминов, как "пять звезд", "Интернет" и "отели среднего класса".
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
Ни один из двух индексированных документов hello терминами hello, поэтому мы получаем следующие hello, выходные данные из hello сначала `RunQueriesWithNonExistentTermsInIndex`.
~~~
Search hello entire index for hello phrase "five star":

no document matched

Search hello entire index for hello term 'internet':

no document matched

Search hello entire index for hello terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a>Включение поиска синонимов

Чтобы включить поиск синонимов, нам потребуется выполнить два действия. Мы сначала определить и отправить правила синонима, а затем настройте поля toouse их. описывается процесс Hello в `UploadSynonyms` и `EnableSynonymsInHotelsIndex`.

1. Добавление службы поиска tooyour карты синоним. В `UploadSynonyms`, мы определить четыре правила в нашу карту синоним «desc synonymmap» и toohello служба отправки.
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
Карта синонима должно соответствовать toohello открытого стандарта `solr` формат. Формат Hello описан в [синонимы в поиске Azure](search-synonyms.md) в разделе "hello" `Apache Solr synonym format`.

2. Настройка поля поиска toouse hello синоним схемы в определении индекса hello. В `EnableSynonymsInHotelsIndex`, мы можем добавить синонимы по двум полям `category` и `tags` путем установки hello `synonymMaps` имя свойства toohello hello вновь отправлен карты синоним.
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
Когда вы добавите сопоставление синонимов, необходимость в перестроении индексов отпадет. Добавление службы tooyour синоним карты и затем измените существующие определения полей в любой индекс toouse hello нового синонима карты. Добавление новых атрибутов Hello не оказывает влияния на доступность индекса. Здравствуйте, же правило применяется к выключению синонимы для поля. Достаточно просто задать hello `synonymMaps` свойство tooan пустой список.
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a>Запросы "после"

После отправки карты синоним hello и индекс hello обновленные toouse hello синоним карты, во-вторых hello `RunQueriesWithNonExistentTermsInIndex` вызова выводит hello следующее:

~~~
Search hello entire index for hello phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
первый запрос Hello находит hello документа из правила hello `five star=>luxury`. Hello второй запрос расширяет hello поиска с помощью `internet,wifi` и hello в-третьих, используя оба `hotel, motel` и `economy,inexpensive=>budget` в поиск документов hello их соответствие.

Добавление синонимов полностью изменяет интерфейс поиска hello. В этом учебнике hello исходного запросов не tooreturn значимые результаты, даже если документы hello в наш индекс, соответствовали. Включение синонимы, мы разверните tooinclude индекс часто применяемые условия без данных toounderlying изменения в индекс hello.

## <a name="sample-application-source-code"></a>Исходный код образца приложения
Можно найти hello полный исходный код образца приложения hello, используемые в этом пошагового на [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).

## <a name="next-steps"></a>Дальнейшие действия

* Просмотрите [как синонимы toouse в поиске Azure](search-synonyms.md)
* Ознакомьтесь с [документацией по API REST для синонимов](https://aka.ms/rgm6rq).
* Обзор hello ссылки для hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) и [API-интерфейса REST](https://docs.microsoft.com/rest/api/searchservice/).
