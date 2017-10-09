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
# <a name="upload-data-tooazure-search-using-hello-net-sdk"></a>Здравствуйте, передачи данных tooAzure поиска с помощью пакета SDK для .NET
> [!div class="op_single_selector"]
> * [Обзор](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
> 
> 

В этой статье будет показано, как toouse hello [пакет SDK Azure Search .NET](https://aka.ms/search-sdk) tooimport данных в индекс поиска Azure.

Прежде чем приступать к выполнению инструкций из этого руководства, вам нужно [создать индекс службы поиска Azure](search-what-is-an-index.md). В этой статье также предполагается, что вы уже создали `SearchServiceClient` объекта, как показано в [создать индекс поиска Azure с помощью hello .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).

> [!NOTE]
> Все приведенные здесь примеры кода написаны на языке C#. Можно найти полный исходный код hello [на GitHub](http://aka.ms/search-dotnet-howto). Вы также можете прочесть об hello [пакет SDK Azure Search .NET](search-howto-dotnet-sdk.md) для более подробные руководства по hello примеров кода.

В порядке toopush документов в индекс с помощью hello .NET SDK необходимо:

1. Создание `SearchIndexClient` объекта tooconnect tooyour поиска индекса.
2. Создание `IndexBatch` содержащий toobe документы hello добавлены, изменены или удалены.
3. Вызовите hello `Documents.Index` метод вашей `SearchIndexClient` toosend hello `IndexBatch` tooyour индекс поиска.

## <a name="create-an-instance-of-hello-searchindexclient-class"></a>Создайте экземпляр класса SearchIndexClient hello
tooimport данных в индекс с помощью hello пакет SDK Azure Search .NET, вам понадобится toocreate экземпляр hello `SearchIndexClient` класса. Можно создать этот экземпляр самостоятельно, но он проще, если у вас уже есть `SearchServiceClient` toocall экземпляра его `Indexes.GetClient` метод. Например, вот как можно будет получить `SearchIndexClient` для hello индекса с именем «гостиницы» из `SearchServiceClient` с именем `serviceClient`:

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> В типичном поисковом приложении управление индексами и заполнение обрабатываются отдельным компонентом из запросов поиска. `Indexes.GetClient`удобный для заполнения индекса, так как избавляет вас hello проблемы предоставления другой `SearchCredentials`. Это делается путем передачи ключа администратора hello, то используется toocreate hello `SearchServiceClient` toohello новый `SearchIndexClient`. Однако в hello части приложения, которое выполняет запросы, это лучше toocreate hello `SearchIndexClient` напрямую, что можно передавать ключ запроса вместо ключа администратора. Это согласуется с hello [принципа наименьших прав доступа](https://en.wikipedia.org/wiki/Principle_of_least_privilege) и поможет toomake более безопасные приложения. Можно найти дополнительные сведения о ключи администратора и ключи запроса в hello [Справочник по REST API поиска Azure](https://docs.microsoft.com/rest/api/searchservice/).
> 
> 

У класса `SearchIndexClient` есть свойство `Documents`. Это свойство предоставляет все методы hello требуется tooadd, изменить, удалить или запрос документов в индексе.

## <a name="decide-which-indexing-action-toouse"></a>Решите, какие индексирования toouse действие
tooimport данных с помощью hello .NET SDK, необходимо будет toopackage копирование данных в `IndexBatch` объекта. `IndexBatch` Инкапсулирует коллекцию `IndexAction` объектов, каждый из которых включает документ и свойство, определяющее поиска Azure, какие действия tooperform для этого документа (отправка, слияние, удаление, и т. д). В зависимости от того, какой из hello следующие действия, которые можно выбрать только определенные поля должны быть включены для каждого документа:

| Действие | Описание | Необходимые поля для каждого документа | Примечания |
| --- | --- | --- | --- |
| `Upload` |`Upload` Действие — примерно tooan «вставки-обновления» где документ hello будет вставлена, если является новым и обновлен или заменен, если он существует. |ключ, а также другие поля, нужно toodefine |При обновлении или замене существующего документа, любое поле, которое не указано в запросе hello будет иметь слишком его поле`null`. Это происходит даже в том случае, если поле hello было установлено ранее tooa непустое значение. |
| `Merge` |Обновления, существующий документ с hello указаны поля. Если документ hello не существует в индексе hello, hello слияния завершится ошибкой. |ключ, а также другие поля, нужно toodefine |Любое поле, указанное для объединения приведет к замене существующего поля hello в документе hello. Это относится и к полям типа `DataType.Collection(DataType.String)`. Например, если hello документ содержит поле `tags` со значением `["budget"]` , и вы выполните объединение со значением `["economy", "pool"]` для `tags`, hello окончательное значение hello `tags` поле будет `["economy", "pool"]`. а не `["budget", "economy", "pool"]`. |
| `MergeOrUpload` |Это действие ведет себя как `Merge` Если документ с hello заданным ключом уже существует в индексе hello. Если документ hello не существует, он ведет себя как `Upload` с новым документом. |ключ, а также другие поля, нужно toodefine |- |
| `Delete` |Удаляет указанный документ hello из индекса hello. |Только ключ |Все поля, укажите вместо hello ключевое поле будет игнорироваться. Tooremove отдельного поля из документа, используйте `Merge` вместо и просто задать поле hello явно toonull. |

Можно указать, какое действие должно toouse с hello различных статических методов hello `IndexBatch` и `IndexAction` классов, как показано в следующем разделе hello.

## <a name="construct-your-indexbatch"></a>Создание класса IndexBatch
Теперь, когда вы знаете, какие tooperform действия с документами, вы являетесь hello готов tooconstruct `IndexBatch`. Здравствуйте в следующем примере показано, как toocreate пакет с несколько различных действий. Обратите внимание, что наш пример использует пользовательский класс с именем `Hotel` сопоставляемого tooa документов в индексе «гостиницы» hello.

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

В этом случае мы используем `Upload`, `MergeOrUpload`, и `Delete` как наши действия поиска, в соответствии с hello методы, вызываемые на hello `IndexAction` класса.

Предположим, что пример индекса с именем hotels уже заполнен несколькими документами. Обратите внимание на то, как бы не было toospecify все поля hello возможных документа при использовании `MergeOrUpload` и как мы указан только ключ документа hello (`HotelId`) при использовании `Delete`.

Кроме того Обратите внимание, что может включать только too1000 документов в одном запросе индексирования.

> [!NOTE]
> В этом примере применяется документы toodifferent разные действия. Если вы хотите, чтобы tooperform hello же действия для всех документов в пакете hello, вместо вызова метода `IndexBatch.New`, можно использовать hello других статических методов `IndexBatch`. Например, можно создать пакеты, вызвав метод `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` или `IndexBatch.Delete`. Эти методы вместо объектов `IndexAction` принимают коллекцию документов (в нашем примере это объекты типа `Hotel`).
> 
> 

## <a name="import-data-toohello-index"></a>Индекс toohello импорта данных
Теперь, когда имеется инициализированная `IndexBatch` объекта, вы можете отправить ее toohello индекс путем вызова `Documents.Index` на ваш `SearchIndexClient` объекта. Следующий пример показывает как Hello toocall `Index`, также как некоторые дополнительные действия, вам потребуется tooperform:

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

Примечание hello `try` / `catch` вокруг вызова toohello hello `Index` метод. Hello блок catch обрабатывает такие важные ошибки для индексирования. Службе поиска Azure в случае некоторые hello документов в пакете hello tooindex `IndexBatchException` вызванное `Documents.Index`. Это может произойти, если вы индексируете документы службы при интенсивной нагрузке. **Настоятельно рекомендуется явно обрабатывать этот случай в коде.** Можно отложить и повторите попытку индексирования отказавших документов hello или пользователь может входить и продолжить как образец hello работает, можно сделать что-нибудь другое в зависимости от требований к согласованности данных приложения.

Наконец hello кода в примере hello выше задержки в течение двух секунд. Индексирование работает асинхронно в службе поиска Azure, поэтому пример приложения hello должен toowait tooensure короткое время, что hello документы доступны для поиска. Такие задержки обычно необходимы только в демонстрациях, тестах и примерах приложений.

<a name="HotelClass"></a>

### <a name="how-hello-net-sdk-handles-documents"></a>Как hello пакета SDK для .NET обрабатывает документы
Может возникнуть вопрос как hello пакет SDK Azure Search .NET — может tooupload экземпляры класса определяемого пользователем как `Hotel` toohello индекса. toohelp ответа на этот вопрос, давайте взглянем на hello `Hotel` класс, который сопоставляет определенной в схеме индекса toohello [создать индекс поиска Azure с помощью hello .NET SDK](search-create-index-dotnet.md#DefineIndex):

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

Hello первое, что toonotice является, каждое общее свойство `Hotel` соответствует tooa поля в определение индекса hello, но с одним ключевым отличием: hello имя каждого поля начинается с букв нижнего регистра («верблюжий»), тогда hello имя каждого открытых Свойство `Hotel` начинается с буквы верхнего регистра («стиле Pascal»). Это распространенный сценарий в приложениях .NET и выполнить привязку данных, где управление внешними hello разработчик приложения hello hello целевой схемы. Вместо того чтобы использовать .NET hello tooviolate правила именования, делая прописной имена свойств, чтобы узнать hello SDK toomap hello свойство имена toocamel регистре автоматически с помощью hello `[SerializePropertyNamesAsCamelCase]` атрибута.

> [!NOTE]
> пакет SDK Azure Search .NET Hello использует hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize библиотеки и десериализации tooand объектов в пользовательскую модель из JSON. При необходимости эту сериализацию можно настроить. Дополнительные сведения см. в разделе [Пользовательская сериализация с помощью JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet). Примером этого является использование hello hello `[JsonProperty]` атрибут hello `DescriptionFr` свойство в приведенном выше примере кода hello.
> 
> 

Hello второй важным преимуществом hello `Hotel` класса являются типами данных hello hello открытые свойства. типы tootheir эквивалент полей в определение индекса hello сопоставление типов Hello из этих свойств. Здравствуйте, например, `Category` строковое свойство сопоставляется toohello `category` поле, которое относится к типу `DataType.String`. Аналогичные сопоставления присутствуют между типами `bool?` и `DataType.Boolean`, `DateTimeOffset?` и `DataType.DateTimeOffset` и т. д. Hello определенные правила для сопоставления типа hello описаны с hello `Documents.Get` метод в hello [ссылку на пакет SDK Azure Search .NET](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).

Это возможность toouse собственные классы как документы работает в обоих направлениях; Можно также получать результаты поиска и hello SDK автоматически выполнить десериализацию их tooa типа по своему усмотрению, как показано в hello [следующей статье](search-query-dotnet.md).

> [!NOTE]
> пакет SDK Azure Search .NET Hello также поддерживает динамически типизированные документы с помощью hello `Document` класс, который представляет собой сопоставление значений toofield имена полей ключ значение. Это полезно в сценариях, которых вы не знаете hello схемы индекса во время разработки, или было бы неудобно toobind toospecific модель классов. Все методы hello hello SDK, обрабатывающих документы имеют перегрузки, которые работают с hello `Document` класса, а также строго типизированных перегрузки, принимающие параметр универсального типа. Последний hello используются в примере кода hello в этой статье.
> 
> 

**Почему следует использовать типы данных, допускающие значение NULL**

При разработке собственных индекс поиска Azure классы toomap модели tooan, мы рекомендуем, например, объявление свойств типов значений `bool` и `int` toobe допускает значение NULL (например, `bool?` вместо `bool`). При использовании свойство не допускающим имеется слишком**гарантирует** что документов в индексе не будет содержать значение null для соответствующего поля hello. Hello SDK ни hello службы поиска Azure поможет вам tooenforce это.

Это не относится только к гипотетической: представьте себе ситуацию, когда Добавление нового поля tooan существующего индекса, тип которого `DataType.Int32`. После обновления определения индекса hello, все документы будет иметь значение null для этого нового поля (поскольку все типы допускают значение NULL, если в службе поиска Azure). При использовании модели с запретом `int` свойства для этого поля, вы получите `JsonSerializationException` при попытке документы tooretrieve следующим образом:

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

По этой причине по-прежнему рекомендуется использовать типы, допускающие значения NULL, в классах модели.

## <a name="next-steps"></a>Дальнейшие действия
После заполнения индекса поиска Azure, будет готов toostart выдача запросов toosearch для документов. Дополнительные сведения см. в статье [Запросы в службе поиска Azure](search-query-overview.md).

