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
# <a name="how-toouse-azure-search-from-a-net-application"></a>Как выполнить поиск Azure toouse из приложения .NET
Эта статья является tooget пошагового руководства вы работающий с hello [пакет SDK Azure Search .NET](https://aka.ms/search-sdk). Можно использовать .NET SDK tooimplement hello форматированного функции поиска в приложении с помощью поиска Azure.

## <a name="whats-in-hello-azure-search-sdk"></a>Что такое hello поиска Azure SDK
Hello SDK состоит из клиентской библиотеки, `Microsoft.Azure.Search`. Он позволяет вам toomanage вашей индексов, источники данных и индексаторы, а также передать управление документами и выполнения запросов, не требуя toodeal с подробными сведениями hello HTTP и JSON.

Клиентская библиотека Hello определяет классы, такие как `Index`, `Field`, и `Document`, а также операции, такие как `Indexes.Create` и `Documents.Search` на hello `SearchServiceClient` и `SearchIndexClient` классы. Эти классы организованы в следующие пространства имен hello:

* [Microsoft.Azure.Search;](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [Microsoft.Azure.Search.Models](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

Текущая версия Hello hello пакет SDK Azure Search .NET теперь стал общедоступным. При желании отзыв tooprovide нам tooincorporate в следующей версии hello, посетите наш [страницу обратной связи](https://feedback.azure.com/forums/263029-azure-search/).

Hello .NET SDK поддерживает версию `2016-09-01` из hello [REST API поиска Azure](https://docs.microsoft.com/rest/api/searchservice/). Эта версия поддерживает пользовательские анализаторы, а также индексаторы больших двоичных объектов Azure и таблиц Azure. Предварительный просмотр компонентов, которые являются *не* частью текущей версии, такие как поддержка индексирования JSON и CSV-файлы, находящиеся в [предварительного просмотра](search-api-2015-02-28-preview.md) и доступны через hello старые [2.0 предварительной версии .NET SDK hello ](https://aka.ms/search-sdk-preview).

Этот пакет SDK не поддерживает такие [операции управления](https://docs.microsoft.com/rest/api/searchmanagement/), как создание и масштабирование служб поиска или управление ключами API. Если вам требуется toomanage поиска ресурсов в приложении .NET, можно использовать hello [пакет SDK Azure Search .NET управления](https://aka.ms/search-mgmt-sdk).

## <a name="upgrading-toohello-latest-version-of-hello-sdk"></a>Обновление toohello последнюю версию пакета SDK для hello
Если вы уже используете более старую версию hello пакет SDK Azure Search .NET и хотелось бы tooupgrade toohello новой общедоступной версии, [в этой статье](search-dotnet-sdk-migration.md) объясняется, каким образом.

## <a name="requirements-for-hello-sdk"></a>Требования для hello SDK
1. Visual Studio 2017.
2. Ваша личная служба поиска Azure. В порядке toouse hello SDK необходимо будет hello имя службы и один или несколько ключей API. [Создание службы на портале hello](search-create-service-portal.md) поможет вам выполнить следующие действия.
3. Загрузите пакет SDK Azure Search .NET hello [пакет NuGet](http://www.nuget.org/packages/Microsoft.Azure.Search) с помощью «Управление пакетами NuGet» в Visual Studio. Просто найти имя пакета hello `Microsoft.Azure.Search` на NuGet.org.

Hello пакет SDK Azure Search .NET поддерживает приложения, предназначенные для .NET Framework 4.6 hello и .NET Core.

## <a name="core-scenarios"></a>Основные сценарии
Существует несколько моментов, которые необходимо toodo в приложении поиска. В данном руководстве мы обсудим эти основные сценарии:

* Создание индекса
* Заполнение индекса hello с документами
* Поиск документов с помощью полнотекстового поиска и фильтров

Далее образце кода Hello демонстрируется каждый из них. При желании вы свободного toouse фрагменты кода hello в приложении.

### <a name="overview"></a>Обзор
Hello образец приложения, мы будем изучать создает новый индекс с именем «гостиницы» заполняет несколько документов, а затем выполняет некоторые запросы поиска. Вот основной программы hello, показывающая hello Общая последовательность действий:

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
> Можно найти hello полный исходный код образца приложения hello, используемые в этом пошагового на [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).
> 
>

Мы рассмотрим ее шаг за шагом. Сначала мы должны toocreate новый `SearchServiceClient`. Этот объект позволяет toomanage индексов. В порядке tooconstruct один необходим tooprovide имя службы поиска Azure, а также ключ API администратора. Эти сведения можно ввести в hello `appsettings.json` файл hello [образец приложения](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).

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
> Здравствуйте, если указан неверный ключ (например, запрос ключа, где требовалось ключа администратора), `SearchServiceClient` вызовет `CloudException` с hello ошибки, сообщение «Запрещенных» hello первый раз метод операции, такие как `Indexes.Create`. В этом случае tooyou следует внимательно нашей ключ API.
> 
> 

Hello следующие несколько строк вызовите методы toocreate индекс с именем «гостиницы», его удаление сначала, если он уже существует. Мы рассмотрим эти методы немного позже.

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

Далее индекс hello должен toobe заполнено. toodo, нам нужно будет `SearchIndexClient`. Существует два способа tooobtain одно:, создав его или вызвав `Indexes.GetClient` на hello `SearchServiceClient`. Для удобства мы используем последний hello.

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> В типичном поисковом приложении управление индексами и заполнение обрабатываются отдельным компонентом из запросов поиска. `Indexes.GetClient`удобный для заполнения индекса, так как избавляет вас hello проблемы предоставления другой `SearchCredentials`. Это делается путем передачи ключа администратора hello, то используется toocreate hello `SearchServiceClient` toohello новый `SearchIndexClient`. Однако в hello части приложения, которое выполняет запросы, это лучше toocreate hello `SearchIndexClient` напрямую, что можно передавать ключ запроса вместо ключа администратора. Это согласуется с hello принципа наименьших прав доступа и поможет toomake более безопасные приложения. Дополнительные сведения о ключах администраторов и запросов см. [здесь](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).
> 
> 

Теперь, когда у нас есть `SearchIndexClient`, мы можно заполнить индекс hello. Это делает другой метод, который мы рассмотрим позже.

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

Наконец мы выполните несколько запросов поиска и отображения результатов hello. На этот раз мы используем другой метод `SearchIndexClient`:

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

Использовано более подробно рассмотрим hello `RunQueries` метод позже. Вот новый hello toocreate кода hello `SearchIndexClient`:

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

Это время, мы используем ключ запроса, так как не требуется доступ на запись toohello индекса. Эти сведения можно ввести в hello `appsettings.json` файл hello [образец приложения](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).

При запуске этого приложения с правильное имя службы и ключи API hello вывод должен выглядеть следующим образом:

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

в конце hello в этой статье предоставляется Hello полный исходный код приложения hello.

Далее будет принимать более подробно рассмотрим каждый из методов hello вызывается `Main`.

### <a name="creating-an-index"></a>Создание индекса
После создания `SearchServiceClient`, следующий этап hello `Main` does — delete hello» гостиницы» индекс, если он уже существует. Для этого по hello следующий метод:

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

Этот метод использует заданный hello `SearchServiceClient` toocheck Если hello индекс уже существует и если да, удалите его.

> [!NOTE]
> пример кода Hello в этой статье использует синхронные методы hello hello пакет SDK Azure Search .NET для простоты. Рекомендуется использовать асинхронные методы hello в собственных приложениях tookeep их быстрые и масштабируемые. Например, в hello метод выше использовать `ExistsAsync` и `DeleteAsync` вместо `Exists` и `Delete`.
> 
> 

Затем `Main` создает новый индекс hotels, вызывая следующий метод:

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

Этот метод создает новый `Index` объекта со списком `Field` объектов, который определяет схему нового индекса hello hello. Каждое поле имеет имя, тип данных и несколько атрибутов, которые определяют его поведение при поиске. Hello `FieldBuilder` класс использует отражение toocreate список `Field` объектов для hello индекса с помощью проверки hello общие свойства и атрибуты hello заданному `Hotel` класс модели. Перейти на более подробно рассмотрим hello `Hotel` класса позже.

> [!NOTE]
> Всегда можно создать список hello `Field` объекты напрямую, а не с помощью `FieldBuilder` при необходимости. Например может потребоваться не toouse класс модели или может потребоваться toouse существующий класс модели, вы не хотите toomodify путем добавления атрибутов.
>
> 

В дополнение к этому toofields, также добавляются профилей оценки, средств подбора или toohello CORS параметры индекса (они удаляются из образца «hello» для краткости). Дополнительные сведения о hello объекта индекса и ее составных частей можно найти в hello [ссылки на пакет SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), а также в hello [Справочник по REST API поиска Azure](https://docs.microsoft.com/rest/api/searchservice/).

### <a name="populating-hello-index"></a>Заполнение индекса hello
следующим шагом Hello в `Main` — индекс вновь созданного toopopulate hello. Это делается в hello следующий метод:

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

Этот метод состоит из четырех частей. Hello сначала создает массив из `Hotel` объекты, которые будет использоваться в качестве индекса toohello tooupload входных данных. Эти данные жестко запрограммированы для простоты. В вашем приложении данные скорее всего будут поступать из внешнего источника, например базы данных SQL.

Вторая часть Hello создает `IndexBatch` содержащую документы hello. Укажите операцию hello требуется tooapply toohello пакета во время hello его создания, в этом случае путем вызова `IndexBatch.Upload`. Hello пакета происходит, то переданные toohello поиска Azure индекс по hello `Documents.Index` метод.

> [!NOTE]
> В этом примере мы просто отправляем документы. Если требуется toomerge изменения в существующих документов или удаления документов, можно создать путем вызова пакетов `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, или `IndexBatch.Delete` вместо него. Вы можете сочетать различные операции в одном пакете, вызвав `IndexBatch.New`, который принимает коллекцию `IndexAction` объектов, каждый из которых указывает tooperform поиска Azure конкретной операции в документе. Можно создать каждый `IndexAction` с отдельной операции путем вызова соответствующего метода hello, например `IndexAction.Merge`, `IndexAction.Upload`, и т. д.
> 
> 

Третья часть Hello этого метода является блок catch, который обрабатывает важные ошибки для индексирования. Службе поиска Azure в случае некоторые hello документов в пакете hello tooindex `IndexBatchException` вызванное `Documents.Index`. Это может произойти, если вы индексируете документы службы при интенсивной нагрузке. **Настоятельно рекомендуется явно обрабатывать этот случай в коде.** Можно отложить и повторите попытку индексирования отказавших документов hello или пользователь может входить и продолжить как образец hello работает, можно сделать что-нибудь другое в зависимости от требований к согласованности данных приложения.

> [!NOTE]
> Можно использовать hello `FindFailedActionsToRetry` tooconstruct метод новый пакет, содержащий только hello действия, которые не удалось выполнить в предыдущем вызове слишком`Index`. метод Hello задокументирован [здесь](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) и обсуждение tooproperly его использовании [на StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).
>
>

Здравствуйте, и, наконец, `UploadDocuments` метод задержки для двух секунд. Индексирование работает асинхронно в службе поиска Azure, поэтому пример приложения hello должен toowait tooensure короткое время, что hello документы доступны для поиска. Такие задержки обычно необходимы только в демонстрациях, тестах и примерах приложений.

#### <a name="how-hello-net-sdk-handles-documents"></a>Как hello пакета SDK для .NET обрабатывает документы
Может возникнуть вопрос как hello пакет SDK Azure Search .NET — может tooupload экземпляры класса определяемого пользователем как `Hotel` toohello индекса. toohelp ответа на этот вопрос, давайте взглянем на hello `Hotel` класса:

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

Hello первое, что toonotice является, каждое общее свойство `Hotel` соответствует tooa поля в определение индекса hello, но с одним ключевым отличием: hello имя каждого поля начинается с букв нижнего регистра («верблюжий»), тогда hello имя каждого открытых Свойство `Hotel` начинается с буквы верхнего регистра («стиле Pascal»). Это распространенный сценарий в приложениях .NET и выполнить привязку данных, где управление внешними hello разработчик приложения hello hello целевой схемы. Вместо того чтобы использовать .NET hello tooviolate правила именования, делая прописной имена свойств, чтобы узнать hello SDK toomap hello свойство имена toocamel регистре автоматически с помощью hello `[SerializePropertyNamesAsCamelCase]` атрибута.

> [!NOTE]
> пакет SDK Azure Search .NET Hello использует hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize библиотеки и десериализации tooand объектов в пользовательскую модель из JSON. При необходимости эту сериализацию можно настроить. Дополнительные сведения см. в разделе [Пользовательская сериализация с помощью JSON.NET](#JsonDotNet).
> 
> 

Hello второй toonotice самое являются hello атрибутами, такими как `IsFilterable`, `IsSearchable`, `Key`, и `Analyzer` , добавьте каждое открытое свойство. Эти атрибуты непосредственно сопоставляются toohello [соответствующих атрибутов индекс поиска Azure hello](https://docs.microsoft.com/rest/api/searchservice/create-index#request). Hello `FieldBuilder` класс использует эти определения полей tooconstruct для индекса hello.

Hello третий важным преимуществом hello `Hotel` класса являются типами данных hello hello открытые свойства. типы tootheir эквивалент полей в определение индекса hello сопоставление типов Hello из этих свойств. Здравствуйте, например, `Category` строковое свойство сопоставляется toohello `category` поле, которое относится к типу `Edm.String`. Существуют аналогичные сопоставление типов между `bool?` и `Edm.Boolean`, `DateTimeOffset?` и `Edm.DateTimeOffset`, т. д. hello определенные правила для сопоставления типа hello описаны с hello `Documents.Get` метод в hello [пакет SDK Azure Search .NET Справочник по](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_). Hello `FieldBuilder` класс берет на себя такое сопоставление для вас, но может оказаться полезным toounderstand на случай необходимости tootroubleshoot проблемы сериализации.

Это возможность toouse собственные классы как документы работает в обоих направлениях; Можно также получать результаты поиска и hello SDK автоматически выполнить десериализацию их tooa типа по своему усмотрению, как будет показано в следующем разделе hello.

> [!NOTE]
> пакет SDK Azure Search .NET Hello также поддерживает динамически типизированные документы с помощью hello `Document` класс, который представляет собой сопоставление значений toofield имена полей ключ значение. Это полезно в сценариях, которых вы не знаете hello схемы индекса во время разработки, или было бы неудобно toobind toospecific модель классов. Все методы hello hello SDK, обрабатывающих документы имеют перегрузки, которые работают с hello `Document` класса, а также строго типизированных перегрузки, принимающие параметр универсального типа. Последний hello используются в примере кода hello в этом учебнике. Hello `Document` класс наследует от `Dictionary<string, object>`. Дополнительные сведения см. [здесь](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).
> 
> 

**Почему следует использовать типы данных, допускающие значение NULL**

При разработке собственных индекс поиска Azure классы toomap модели tooan, мы рекомендуем, например, объявление свойств типов значений `bool` и `int` toobe допускает значение NULL (например, `bool?` вместо `bool`). При использовании свойство не допускающим имеется слишком**гарантирует** что документов в индексе не будет содержать значение null для соответствующего поля hello. Hello SDK ни hello службы поиска Azure поможет вам tooenforce это.

Это не относится только к гипотетической: представьте себе ситуацию, когда Добавление нового поля tooan существующего индекса, тип которого `Edm.Int32`. После обновления определения индекса hello, все документы будет иметь значение null для этого нового поля (поскольку все типы допускают значение NULL, если в службе поиска Azure). При использовании модели с запретом `int` свойства для этого поля, вы получите `JsonSerializationException` при попытке документы tooretrieve следующим образом:

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

По этой причине по-прежнему рекомендуется использовать типы, допускающие значения NULL, в классах модели.

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a>Пользовательская сериализация с помощью JSON.NET
Hello SDK использует JSON.NET для сериализации и десериализации документов. Можно настроить сериализацию и десериализацию при необходимости путем определения собственных `JsonConverter` или `IContractResolver` (в разделе hello [JSON.NET документации](http://www.newtonsoft.com/json/help/html/Introduction.htm) для получения дополнительных сведений). Это может быть полезным при необходимости tooadapt существующий класс модели из приложения для использования с поиска Azure и других более сложных сценариев. Например, с помощью пользовательской сериализации можно делать следующее.

* Включить или исключить определенные свойства класса модели с сохранением в виде поля документа.
* Реализовать сопоставление между именами свойств в коде и именами полей в индексе.
* Создание настраиваемых атрибутов, которые могут использоваться для сопоставления полей toodocument свойств.

Можно найти примеры реализации пользовательской сериализации в hello модульных тестов для hello пакет SDK Azure Search .NET, на сайте GitHub. Хорошей отправной точкой будет [эта папка](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models). Он содержит классы, используемые с пользовательской сериализации тестов hello.

### <a name="searching-for-documents-in-hello-index"></a>Поиск документов в индексе hello
Последний шаг Hello в пример приложения hello — toosearch для некоторых документов в индексе hello. Следующий метод Hello делает это:

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

При каждом выполнении запроса этот метод прежде всего создает объект `SearchParameters`. Это используется toospecify Дополнительные параметры для запроса hello, таких как сортировка, фильтрация, разбиение на страницы и аспекты. В этом методе задаются значения hello `Filter`, `Select`, `OrderBy`, и `Top` свойство для различных запросов. Все hello `SearchParameters` свойства документируются [здесь](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).

Hello следующим шагом является tooactually выполнение hello поискового запроса. Это делается с помощью hello `Documents.Search` метод. Для каждого запроса toouse текст hello поиска передается как строка (или `"*"` при отсутствии поиска текста), плюс hello созданную ранее параметров поиска. Также укажите `Hotel` как параметр типа hello для `Documents.Search`, который сообщает hello SDK toodeserialize документов в результатах поиска hello в объекты типа `Hotel`.

> [!NOTE]
> Можно найти дополнительные сведения о синтаксисе выражений запросов поиска hello [здесь](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).
> 
> 

Наконец после каждого запроса этот метод выполняет перебор всех hello совпадений в результатах поиска hello, печать каждой консоли toohello документа:

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

Давайте более подробно рассмотрим hello запросы, в свою очередь. Вот первый запрос tooexecute кода hello hello.

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

В этом случае мы ищем гостиницы, слово hello «бюджет», и мы хотим tooget обратно только hello гостиницы имен, определяемое параметром hello `Select` параметра. Ниже приведены результаты hello.

    Name: Roach Motel

Далее мы toofind hello гостиницы с частотой не более 150 каждую ночь и вернуть только hello гостиницы Идентификатором и описанием:

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

Этот запрос использует OData `$filter` выражение, `baseRate lt 150`, toofilter hello документов в индексе hello. Дополнительные сведения о hello синтаксис OData, поддерживающего поиск Azure можно найти [здесь](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).

Ниже приведены результаты hello hello запроса.

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river

Далее мы хотим toofind hello top два гостиницы, недавно отремонтированных и показывать название отеля hello и Дата последней модернизации. Ниже приведен код hello. 

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

В этом случае мы снова использовать hello toospecify синтаксис OData `OrderBy` параметр как `lastRenovationDate desc`. Мы также настроить `Top` too2 tooensure мы получить только первые две документы hello. Как и прежде, мы устанавливаем `Select` toospecify, какие поля должны быть возвращены.

Ниже приведены результаты hello.

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Наконец мы хотим toofind все гостиницы, слово hello «motel»:

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

А вот hello результатов, которые включают все поля, поскольку не был указан hello `Select` свойство:

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

Этот шаг завершает учебник hello, но не останавливает здесь. **Дальнейшие действия** представлены дополнительные материалы о Поиске Azure.

## <a name="next-steps"></a>Дальнейшие действия
* Обзор hello ссылки для hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) и [API-интерфейса REST](https://docs.microsoft.com/rest/api/searchservice/).
* Дополнительные сведения можно получить из [видео, а также других примеров и руководств](search-video-demo-tutorial-list.md).
* Просмотрите [соглашения об именовании](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn hello правила выбора имен для различных объектов.
* Изучите [поддерживаемые типы данных](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) в службе поиска Azure.
