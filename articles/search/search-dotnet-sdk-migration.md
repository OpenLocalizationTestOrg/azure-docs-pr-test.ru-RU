---
title: "aaaUpgrading toohello поиска Azure .NET SDK версии 1.1 | Документы Microsoft"
description: "Обновление toohello поиска Azure .NET SDK версии 1.1"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 66f89958-a320-4a24-87f9-69315848909f
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 291ae5731546e47b3c22c721d3552a79bdea80c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-net-sdk-version-3"></a>Обновление toohello поиска Azure .NET SDK версии 3
Если вы используете версию предварительной версии 2.0 или более hello [пакет SDK Azure Search .NET](https://aka.ms/search-sdk), эта статья поможет вам обновить версию приложения toouse 3.

Более общие Пошаговое руководство по hello SDK включая примеры, см. в [как toouse Azure поиска из приложения .NET](search-howto-dotnet-sdk.md).

Пакет SDK Azure Search .NET hello версии 3 содержит некоторые изменения из более ранних версий. Эти отличия в основном незначительные, поэтому изменение кода потребует минимальных усилий. В разделе [tooupgrade действия](#UpgradeSteps) инструкции toochange новой версии пакета SDK кода toouse hello.

> [!NOTE]
> Если вы используете версию 1.0.2-preview или более ранней версии, необходимо сначала обновить tooversion 1.1, а затем обновите tooversion 3. В разделе [приложение: tooversion tooupgrade действия 1.1](#UpgradeStepsV1) инструкции.
>
> Экземпляр службы поиска Azure поддерживает несколько версий API-Интерфейс REST, включая hello последнюю версию. Вы можете продолжить toouse версии, когда он больше не hello последнюю версию, но рекомендуется перейти к toouse кода hello последнюю версию. При использовании hello REST API, необходимо указать версию API hello в каждом запросе через параметр api-version hello. При использовании hello .NET SDK, версия hello hello SDK вы используете определяет соответствующую версию hello hello REST API. При использовании старых SDK можно продолжить toorun без изменения кода, даже если служба hello версии обновленных toosupport новых API.

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a>Новые возможности в версии 3
Версии 3 hello целевых объектов пакет SDK Azure Search .NET hello последней общедоступной версии hello REST API поиска Azure, в частности 2016-09-01. В результате возможно toouse множество новых функций поиска Azure из приложения .NET, включая hello следующее:

* [Пользовательские анализаторы](https://aka.ms/customanalyzers)
* поддержка индексатора [хранилища BLOB-объектов Azure](search-howto-indexing-azure-blob-storage.md) и [хранилища таблиц Azure](search-howto-indexing-azure-tables.md);
* настройка индексатора посредством [сопоставления полей](search-indexer-field-mappings.md)
* Теги eTag поддерживает tooenable безопасном параллельных обновление индекса определений, индексаторов и источников данных
* Поддержка создания определения полей индекса декларативно декорирования классе модели и используя hello новый `FieldBuilder` класса.
* поддержка .NET Core и .NET Portable Profile 111.

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a>Tooupgrade действия
Во-первых, обновите NuGet справочной информации для `Microsoft.Azure.Search` либо hello консоль диспетчера пакетов NuGet с помощью или путем щелкнув ссылки проекта и выбрав «Управление... пакеты NuGet» в Visual Studio.

После загрузки NuGet hello новые пакеты и их зависимости, перестройте проект. Сборка может быть выполнена успешно — в зависимости от того, как структурирован ваш код. В этом случае вы будете готовы toogo!

Если сборку не удается, появится ошибка сборки hello следующим образом:

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' too'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

Hello следующим шагом является toofix ошибки построения. В разделе [критические изменения в версии 3](#ListOfChanges) сведения о том, что вызывает ошибку hello и как toofix его.

Вы можете увидеть дополнительные сборки tooobsolete методов и свойств, связанных с предупреждениями. Hello предупреждения будут включены инструкции по какой toouse вместо из hello нерекомендуемая функция. Например, если приложение использует hello `IndexingParameters.Base64EncodeKeys` следует получать предупреждение об ошибке`"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`

После устранения ошибки сборки можно внести изменения tooyour приложения tootake преимуществами новых функций, при необходимости. Новые возможности в hello SDK подробно описаны в [новые возможности в версии 3](#WhatsNew).

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a>Критические изменения в версии 3
Существует небольшое количество критические изменения в версии 3, которые могут потребовать код изменяет Кроме toorebuilding приложения.

### <a name="indexesgetclient-return-type"></a>Тип возвращаемого значения Indexes.GetClient
Hello `Indexes.GetClient` метод имеет новый тип возвращаемого значения. Раньше он возвращал `SearchIndexClient`, но он был изменен слишком`ISearchIndexClient` в предварительной версии версии 2.0, которые передает изменения по tooversion 3. Это toosupport клиентов, которые хотите toomock hello `GetClient` метод для модульных тестов, возвращая макетной реализации `ISearchIndexClient`.

#### <a name="example"></a>Пример
Если код выглядит следующим образом:

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

Его можно изменить toothis toofix все ошибки построения:

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-toostrings"></a>AnalyzerName, тип данных и другие больше не могут быть неявно преобразованы toostrings
Существует много типов в пакет SDK Azure Search .NET являются производными от hello `ExtensibleEnum`. Ранее эти типы были все неявно преобразовываться tootype `string`. Тем не менее, ошибка была обнаружена на hello `Object.Equals` реализации этих классов и исправление hello ошибки требуется отключить это неявное преобразование. Явное преобразование слишком`string` по-прежнему разрешено.

#### <a name="example"></a>Пример
Если код выглядит следующим образом:

```csharp
var customTokenizerName = TokenizerName.Create("my_tokenizer"); 
var customTokenFilterName = TokenFilterName.Create("my_tokenfilter"); 
var customCharFilterName = CharFilterName.Create("my_charfilter"); 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        customTokenizerName,  
        new[] { customTokenFilterName },  
        new[] { customCharFilterName }), 
}; 
```

Его можно изменить toothis toofix все ошибки построения:

```csharp
const string CustomTokenizerName = "my_tokenizer"; 
const string CustomTokenFilterName = "my_tokenfilter"; 
const string CustomCharFilterName = "my_charfilter"; 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        CustomTokenizerName,  
        new TokenFilterName[] { CustomTokenFilterName },  
        new CharFilterName[] { CustomCharFilterName })
}; 
```

### <a name="removed-obsolete-members"></a>Удалены устаревшие члены

Можно просматривать связанные toomethods ошибки сборки или свойства, которые были помечены как устаревшие в предварительной версии версии 2.0, а затем удаляется в версии 3. При возникновении таких ошибок, вот как tooresolve их:

- Если вы использовали конструктор `ScoringParameter(string name, string value)`, то вместо него воспользуйтесь этим: `ScoringParameter(string name, IEnumerable<string> values)`.
- Если вы использовали hello `ScoringParameter.Value` свойство, используйте hello `ScoringParameter.Values` свойства или hello `ToString` метод вместо.
- Если вы использовали hello `SearchRequestOptions.RequestId` свойство, используйте hello `ClientRequestId` свойство вместо него.

### <a name="removed-preview-features"></a>Удалены функции предварительной версии

При обновлении от tooversion предварительной версии 2.0 версии 3, имейте в виду, что JSON и CSV при синтаксическом анализе поддержки для индексаторов большой двоичный объект был удален, так как эти возможности все еще находятся в предварительной версии. Здравствуйте, в частности, следующие методы hello `IndexingParametersExtensions` класса будут удалены:

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

Если приложение имеет жесткие зависимости от этих функций, нельзя будет tooupgrade tooversion 3 из hello пакет SDK Azure Search .NET. Вы можете продолжить toouse версии 2.0-preview. Однако необходимо учитывать, что **использовать предварительные версии пакетов SDK в рабочих приложениях не рекомендуется**. Предварительные версии функций предназначены исключительно для оценки и могут изменяться.

## <a name="conclusion"></a>Заключение
Если требуются дополнительные сведения об использовании hello пакет SDK Azure Search .NET, см. раздел последние обновленные [руководства, посвященные](search-howto-dotnet-sdk.md).

Мы будем рады вашим отзывам на hello SDK. Если возникли проблемы, вы бесплатно tooask нам для получения справки по hello [форум MSDN поиска Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch). При обнаружении ошибки можно зарегистрировать ошибку в hello [репозитории Azure .NET SDK GitHub](https://github.com/Azure/azure-sdk-for-net/issues). Убедитесь, что tooprefix название вашей проблемы с «пакет SDK для поиска: «.

Благодарим вас за использование поиска Azure!

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-tooupgrade-tooversion-11"></a>Приложение: Действия tooupgrade tooversion 1.1
> [!NOTE]
> Этот раздел применим только toousers из версии 1.0.2-preview hello пакет SDK Azure Search .NET и более ранних версий.
> 
> 

Во-первых, обновите NuGet справочной информации для `Microsoft.Azure.Search` либо hello консоль диспетчера пакетов NuGet с помощью или путем щелкнув ссылки проекта и выбрав «Управление... пакеты NuGet» в Visual Studio.

После загрузки NuGet hello новые пакеты и их зависимости, перестройте проект.

Если ранее с помощью построения hello версии 1.0.0-preview, 1.0.1-preview или 1.0.2-preview, должны выполняться успешно, и вы будете готовы toogo!

Если вы ранее использовали версии 0.13.0-preview или более ранней версии, вы увидите построения ошибки hello следующим образом:

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: hello type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

Hello следующий шаг — ошибки сборки hello toofix по одному. Большинство требует изменения некоторых имен классов и методов, которые были переименованы в hello SDK. [Список критических изменений в версии 1.1](#ListOfChangesV1) содержит список этих изменений имен.

Если вы используете toomodel пользовательские классы документов и эти классы имеют свойства, не допускающим простых типов (например, `int` или `bool` в C#), отсутствует исправления ошибки в версии hello 1.1 hello пакета SDK, из которых следует иметь в виду. Дополнительные сведения см. в разделе [Исправления в версии 1.1](#BugFixesV1).

Наконец после устранения ошибки сборки можно внести изменения tooyour приложения tootake преимуществами новых функциональных возможностей при необходимости.

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a>Список критических изменений в версии 1.1
Hello следующий список упорядочен по вероятности hello, изменение hello может повлиять на код приложения.

#### <a name="indexbatch-and-indexaction-changes"></a>Изменения IndexBatch и IndexAction
`IndexBatch.Create`был переименован слишком`IndexBatch.New` и больше не имеет `params` аргумент. Можно использовать `IndexBatch.New` для пакетов, сочетающих в себе различные типы действий (слияние, удаление и т. д.). Кроме того, существуют новые статические методы для создания пакетов где все действия hello являются одинаковыми hello: `Delete`, `Merge`, `MergeOrUpload`, и `Upload`.

`IndexAction` больше не имеет открытых конструкторов, и его свойства теперь являются неизменяемыми. Следует использовать hello новые статические методы для создания действий для разных целей: `Delete`, `Merge`, `MergeOrUpload`, и `Upload`. `IndexAction.Create` был удален. При использовании hello перегрузку, которая принимает только документа, убедитесь, что toouse `Upload` вместо него.

##### <a name="example"></a>Пример
Если код выглядит следующим образом:

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

Его можно изменить toothis toofix все ошибки построения:

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

Если требуется, можно дополнительно упростить его toothis.

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a>Изменения IndexBatchException
Hello `IndexBatchException.IndexResponse` свойство было изменено слишком`IndexingResults`, а его тип — теперь `IList<IndexingResult>`.

##### <a name="example"></a>Пример
Если код выглядит следующим образом:

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

Его можно изменить toothis toofix все ошибки построения:

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a>Изменение метода операции
Каждая операция hello пакет SDK Azure Search .NET представляется как набор перегруженных версий метода синхронные и асинхронные вызовы. Hello подписи и разбиение эти перегрузки метода изменено в версии 1.1.

Например операция «Получить статистика индекса» в более ранних версиях пакета SDK для hello hello предоставлено следующими сигнатурами:

В `IIndexOperations` добавьте:

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

В `IndexOperationsExtensions` добавьте:

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

сигнатуры методов Hello для hello одной операции в версии 1.1 выглядят следующим образом:

В `IIndexesOperations` добавьте:

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

В `IndexesOperationsExtensions` добавьте:

    // Simplified asynchronous operation
    public static Task<IndexGetStatisticsResult> GetStatisticsAsync(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        CancellationToken cancellationToken = default(CancellationToken));

    // Simplified synchronous operation
    public static IndexGetStatisticsResult GetStatistics(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions));

Начиная с версии 1.1 hello пакет SDK Azure Search .NET классифицирует методы операций по-разному.

* Необязательные параметры теперь моделируются как параметры по умолчанию, а не как дополнительные перегрузки метода. Это иногда значительно сокращает hello число перегрузок метода.
* методы расширения Hello теперь скрыть много hello лишние сведений HTTP вызывающего hello. Например, более старые версии пакета SDK вернул объект ответа с кодом состояния HTTP, который вы часто hello не требуется toocheck, так как операция методы создают исключение `CloudException` для любой код состояния, отображается сообщение об ошибке. Здравствуйте, новые объекты модели только возвращаемым методы расширения, сохранение вы hello трудностей toounwrap их в коде.
* И наоборот hello базовых интерфейсов теперь предоставляют методы, которые помогают управлять на уровне hello HTTP при необходимости. Теперь можно передавать в пользовательских toobe заголовки HTTP, входящие в запросы и новый hello `AzureOperationResponse<T>` возвращают тип предоставляет прямой доступ toohello `HttpRequestMessage` и `HttpResponseMessage` для операции hello. `AzureOperationResponse`определен в hello `Microsoft.Rest.Azure` пространства имен и заменяет `Hyak.Common.OperationResponse`.

#### <a name="scoringparameters-changes"></a>Изменения в параметрах оценки
Новый класс с именем `ScoringParameter` был добавлен в последней toomake SDK hello его проще tooprovide tooscoring профилей параметры в запросе поиска. Здравствуйте, ранее `ScoringProfiles` свойство hello `SearchParameters` был типом класса `IList<string>`; Теперь типизируется как `IList<ScoringParameter>`.

##### <a name="example"></a>Пример
Если код выглядит следующим образом:

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

Его можно изменить toothis toofix все ошибки построения: 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a>Изменение классов модели
Из-за изменения подписи toohello, описанные в [изменение метода операции](#OperationMethodChanges), во многих классах в hello `Microsoft.Azure.Search.Models` пространство имен был переименован или удален. Например:

* `IndexDefinitionResponse` был заменен на `AzureOperationResponse<Index>`.
* `DocumentSearchResponse`был переименован слишком`DocumentSearchResult`
* `IndexResult`был переименован слишком`IndexingResult`
* `Documents.Count()`Теперь возвращает `long` с числом документов hello вместо`DocumentCountResponse`
* `IndexGetStatisticsResponse`был переименован слишком`IndexGetStatisticsResult`
* `IndexListResponse`был переименован слишком`IndexListResult`

toosummarize, `OperationResponse`-производные классы, которые существовали только toowrap объекта модели будут удалены. Hello остальные классы имели их суффикс изменилось с `Response` слишком`Result`.

##### <a name="example"></a>Пример
Если код выглядит следующим образом:

    IndexerGetStatusResponse statusResponse = null;

    try
    {
        statusResponse = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = statusResponse.ExecutionInfo.LastResult;

Его можно изменить toothis toofix все ошибки построения:

    IndexerExecutionInfo status = null;

    try
    {
        status = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = status.LastResult;

##### <a name="response-classes-and-ienumerable"></a>Классы ответа и IEnumerable
Дополнительное изменение, которое может повлиять на код, состоит в том, что классы ответов, содержащие коллекции, больше не реализуют `IEnumerable<T>`. Вместо этого свойство коллекции hello можно работать напрямую. Например, если код выглядит следующим образом:

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

Его можно изменить toothis toofix все ошибки построения:

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a>Исключение, касающееся веб-приложений
Если у вас есть веб-приложения, который выполняет сериализацию `DocumentSearchResponse` напрямую результаты поиска toosend toohello браузера, необходимо будет toochange кода или hello результаты не будут правильно сериализовать. Например, если код выглядит следующим образом:

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

Его можно изменить путем получения hello `.Results` свойство hello поиска ответа toofix поиска результат подготовки к просмотру:

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

Необходимо будет toolook в таких случаях в коде самостоятельно; **компилятора hello не выдаст** из-за `JsonResult.Data` относится к типу `object`.

#### <a name="cloudexception-changes"></a>Изменения CloudException
Hello `CloudException` класс перемещен из hello `Hyak.Common` toohello имен `Microsoft.Rest.Azure` пространства имен. Кроме того его `Error` свойство было изменено слишком`Body`.

#### <a name="searchserviceclient-and-searchindexclient-changes"></a>Изменения SearchServiceClient и SearchIndexClient
Здравствуйте, тип hello `Credentials` изменилось свойство с `SearchCredentials` tooits базового класса, `ServiceClientCredentials`. Если вам требуется tooaccess hello `SearchCredentials` из `SearchIndexClient` или `SearchServiceClient`, используйте новый hello `SearchCredentials` свойство.

В более ранних версиях пакета SDK, hello `SearchServiceClient` и `SearchIndexClient` конструкторов, потребовалось бы `HttpClient` параметра. Они были заменены конструкторами, принимающими `HttpClientHandler` и массив объектов `DelegatingHandler`. Это позволяет упростить tooinstall пользовательские обработчики toopre процесса HTTP-запросов при необходимости.

Наконец, hello конструкторы, которое ушло `Uri` и `SearchCredentials` были изменены. Например, если у вас есть код, который выглядит следующим образом:

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

Его можно изменить toothis toofix все ошибки построения:

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

Также Обратите внимание, что тип hello hello учетные данные параметра изменилось слишком`ServiceClientCredentials`. Это маловероятно, что tooaffect кода с момента `SearchCredentials` является производным от `ServiceClientCredentials`.

#### <a name="passing-a-request-id"></a>Передача идентификатора запроса
В предыдущих версиях пакета SDK для hello, можно задать идентификатор запроса на hello `SearchServiceClient` или `SearchIndexClient` и он будет включен в каждый запрос toohello API-интерфейса REST. Это полезно для устранения неполадок со службой поиска, если требуется поддержка toocontact. Однако это более полезным tooset уникальный идентификатор запроса для каждой операции, а не toouse hello таким же Идентификатором для всех операций. По этой причине hello `SetClientRequestId` методы `SearchServiceClient` и `SearchIndexClient` были удалены. Вместо этого можно передать в метод операции tooeach идентификатор запроса через hello необязательно `SearchRequestOptions` параметра.

> [!NOTE]
> В следующем выпуске пакета SDK для hello мы добавим новый механизм для ИД запроса глобально на клиенте hello объектам параметров, согласованной с hello, который используется в других пакетах SDK Azure.
> 
> 

#### <a name="example"></a>Пример
Если у вас есть код, который выглядит следующим образом:

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

Его можно изменить toothis toofix все ошибки построения:

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a>Изменение имени интерфейса
имена интерфейсов Hello операции группы имеют все измененные toobe согласуется с их соответствующих именах свойств:

* Здравствуйте, тип `ISearchServiceClient.Indexes` было изменено с `IIndexOperations` слишком`IIndexesOperations`.
* Здравствуйте, тип `ISearchServiceClient.Indexers` было изменено с `IIndexerOperations` слишком`IIndexersOperations`.
* Здравствуйте, тип `ISearchServiceClient.DataSources` было изменено с `IDataSourceOperations` слишком`IDataSourcesOperations`.
* Здравствуйте, тип `ISearchIndexClient.Documents` было изменено с `IDocumentOperations` слишком`IDocumentsOperations`.

Это изменение — tooaffect маловероятно, что ваш код, если вы создали макеты этих интерфейсов для целей тестирования.

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a>Исправления в версии 1.1
Произошла ошибка в более старых версиях tooserialization связанные пакет SDK Azure Search .NET hello классов пользовательскую модель. Hello ошибка может произойти, если создан класс пользовательскую модель со свойством типа не допускающим значения.

#### <a name="steps-tooreproduce"></a>Tooreproduce действия
Создайте класс пользовательской модели со свойством типа значения, не допускающего нуля. Например, добавьте открытое свойство `UnitCount` типа `int` вместо `int?`.

Если индекс со значением по умолчанию hello этого типа документа (например, 0 для `int`), hello поле будет иметь значение null, если в службе поиска Azure. Если впоследствии вы ищете этого документа, hello `Search` вызова вызывает исключение `JsonSerializationException` обнаруживших, она не может преобразовать `null` слишком`int`.

Кроме того фильтры могут не работать должным образом, поскольку null был написан toohello индекса вместо значения предназначен hello.

#### <a name="fix-details"></a>Сведения об исправлении
Эта проблема устранена в версии 1.1 hello SDK. Теперь, если имеется такой класс модели:

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

и задать `IntValue` too0, что значение теперь правильно сериализуется как 0 сети hello и сохраняется как "0" в индексе hello. Циклы обработки также работают ожидаемым образом.

Имеется один toobe потенциальные проблемы, учитывать при таком подходе: при использовании типа модели с запретом свойством, у вас есть слишком**гарантирует** что документов в индексе не будет содержать значение null для соответствующего поля hello. Hello SDK ни hello REST API поиска Azure поможет вам tooenforce это.

Это не относится только к гипотетической: представьте себе ситуацию, когда Добавление нового поля tooan существующего индекса, тип которого `Edm.Int32`. После обновления определения индекса hello, все документы будет иметь значение null для этого нового поля (поскольку все типы допускают значение NULL, если в службе поиска Azure). При использовании модели с запретом `int` свойства для этого поля, вы получите `JsonSerializationException` при попытке документы tooretrieve следующим образом:

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

По этой причине по-прежнему рекомендуется использовать типы, допускающие значения NULL, в классах модели.

Дополнительные сведения о исправления ошибок и hello см. в разделе [эту проблему на GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).

