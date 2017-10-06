---
title: "политики индексирования Cosmos DB aaaAzure | Документы Microsoft"
description: "Сведения об осуществлении индексации в Azure Cosmos DB. Узнайте, как tooconfigure и изменение hello политики индексирования для автоматического индексирования и повышения производительности."
keywords: "принцип работы индексирования, автоматическое индексирование, индексирование базы данных"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: d5e8f338-605d-4dff-8a61-7505d5fc46d7
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/17/2017
ms.author: arramac
ms.openlocfilehash: 4f77b352b89382aa3352136038cb0e95c7588aac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-cosmos-db-index-data"></a>Как работает индексирование данных в Azure Cosmos DB?

По умолчанию все данные Azure Cosmos DB индексируются. И хотя многие клиенты довольны toolet Azure Cosmos DB автоматически обрабатывать все аспекты индексирования, Azure Cosmos DB также поддерживает указание пользовательского **политика индексирования** для коллекций во время создания. Политики индексирования в базе данных Azure Cosmos являются более гибкими и мощными, чем вторичные индексы, предлагаемые в других платформах базы данных, поскольку они позволяют проектировать и настраивать форму hello hello индекса без ущерба для гибкости схемы. toolearn как индексирование работает в Azure Cosmos DB, необходимо понимать, управляя политика индексирования, которые можно сделать детально компромисса между затраты на хранение индекса, запись и запросов пропускной способности и согласованности запроса.  

В этой статье мы рассмотрим закрыть базу данных Azure Cosmos политики индексирования, как можно настроить политики индексирования и hello связанную компромиссы. 

После считывания в этой статье, вы будете иметь доступ tooanswer hello следующие вопросы:

* Как можно переопределить свойства tooinclude hello или исключить из индексирования?
* Как настроить hello индекса для окончательной обновлений
* Как настроить индексирования tooperform Order By или диапазон запросов
* Как устанавливать политики индексирования для коллекции tooa изменения?
* Как сравнить затраты на хранение и производительность различных политик индексирования?

## <a id="CustomizingIndexingPolicy"></a>Настройка политики индексирования hello коллекции
Разработчики могут настраивать hello компромисс между хранилищем, записи или запрос производительности и согласованности запроса путем переопределения политика индексирования по умолчанию hello на Azure Cosmos DB коллекции и настройка hello следующие аспекты.

* **Включение документов и путей в индекс и исключение их из него**. Разработчики могут выбрать определенные документы toobe исключены или включены в индекс hello во время hello Вставка или заменить их toohello коллекции. Разработчики также можно выбрать tooinclude или исключить некоторые свойства JSON так называемый индексировать для документов, которые включены в индекс toobe пути (включая шаблоны из подстановочных знаков).
* **Настройка различных типов индекса**. Для каждого из путей hello включены разработчики могут также указать hello тип индекса, которые для них требуется коллекции на основании их данных и ожидаемого запроса рабочей нагрузки и hello числовые или строку «точность» для каждого пути.
* **Настройка режимов обновления индекса**. Azure Cosmos DB поддерживают три режима индексирования, которые можно настроить с помощью hello политика на Azure Cosmos DB коллекцию индексирования: согласованного, Lazy и None. 

Здравствуйте, следующем .NET код фрагменте кода показан способ tooset пользовательскую политику индексации во время создания коллекции hello. Здесь мы задание политики hello с индексом диапазона для строки и числа на максимальной точности hello. Эта политика позволяет выполнять запросы Order By к строкам.

    DocumentCollection collection = new DocumentCollection { Id = "myCollection" };

    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), collection);   


> [!NOTE]
> Hello схему JSON для политики индексирования был изменен с hello выпуска версии API-интерфейса REST 2015-06-03 toosupport диапазона индексов для строк. Пакет SDK для .NET версии 1.2.0 и Java, Python и Node.js SDK 1.1.0 поддерживает новую схему политики hello. Более старые пакеты SDK используют hello версии 2015-04-08 API-Интерфейс REST и поддерживают hello старую схему политики индексирования.
> 
> По умолчанию Azure Cosmos DB согласованно индексирует все свойства строк в документах с помощью хэш-индекса, а числовые свойства — с помощью диапазонного индекса.  
> 
> 

### <a name="customizing-hello-indexing-policy-using-hello-portal"></a>Настройка политики индексирования hello, с помощью портала hello

Вы можете изменить hello индексирования политики из коллекции с помощью портала Azure hello. Откройте учетную запись Azure Cosmos DB в hello портал Azure, выберите коллекцию, в hello левой области навигации выберите пункт **параметры**, а затем нажмите кнопку **политики индексирования**. В hello **политики индексирования** колонки, измените политику индексации и нажмите кнопку **ОК** toosave изменения. 

### <a id="indexing-modes"></a>Режимы индексирования базы данных
Azure Cosmos DB поддерживает три индексирования режимов, которые можно настроить с помощью индексирования политики на коллекцию Azure Cosmos DB — hello Consistent и Lazy None.

**Согласованное**: Если политика сбора Azure Cosmos DB используется в качестве «согласованное», hello запросов на данной выполните коллекции Azure Cosmos DB hello уровень согласованности, указанное для hello точке чтения (т. е. надежный, ограниченных устаревание, сеанс или окончательной). Hello индекс обновляется синхронно, в ходе обновления документа hello (т. е. вставки, замены, update и delete документа в коллекции Azure Cosmos DB).  Согласованное индексирования поддерживает согласованное запросы по цене hello возможных уменьшения пропускная способность при записи. Уменьшение является функцией hello уникальных путей, которые необходимо индексировать toobe и hello «уровень согласованности». Режим согласованного индексирования предназначен для рабочих нагрузок типа "быстрая запись, немедленный запрос".

**Отложенная**: tooallow максимальное документа приемом пропускную способность, коллекцию Azure Cosmos DB можно настроить отложенный согласованности; значение запросы согласованным. Hello индекс обновляется асинхронно при коллекцию Azure Cosmos DB замораживания т. е. при пропускной способности hello коллекции не является полностью tooserve пользовательских запросов. Для рабочих нагрузок типа "прием сейчас, запрос позже", требующих беспрепятственного приема документов, может подойти асинхронный режим индексирования.

**None** (Нет). У коллекции с режимом индексирования None нет связанного индекса. Обычно это применимо для тех случаев, когда Azure Cosmos DB используется как хранилище пар "ключ — значение", а доступ к документам осуществляется только по свойству их идентификатора. 

> [!NOTE]
> Настройка hello, политика с «None» индексирования имеет hello побочный эффект удаления любой существующий индекс. Используйте этот режим, если шаблонам доступа требуются только идентификатор и (или) самоссылающаяся ссылка.
> 
> 

Следующий образец Показать как Hello создайте коллекцию Azure Cosmos DB использование hello .NET SDK с согласованной Автоматическое индексирование на все операции вставки в документ.

Hello в следующей таблице показаны hello согласованности для запросов, основанных на hello режим индексирования (Consistent и Lazy) настроен для hello коллекции и hello согласованности уровня, заданного для hello запроса. Это применяется tooqueries внесены с помощью пакетов SDK любой интерфейс — REST API или из хранимых процедур и триггеров. 

|Целостность|Режим индексирования: согласованный|Режим индексирования: асинхронный|
|---|---|---|
|Уровень согласованности Strong (сильная)|Уровень согласованности Strong (сильная)|Уровень согласованности Eventual (в конечном счете)|
|Ограниченное устаревание|Ограниченное устаревание|Уровень согласованности Eventual (в конечном счете)|
|Сеанс|Сеанс|Уровень согласованности Eventual (в конечном счете)|
|В конечном счете|В конечном счете|Уровень согласованности Eventual (в конечном счете)|

Azure Cosmos DB возвращает ошибку для запросов к коллекциям, для которых задан режим индексирования None. Запросы по-прежнему могут быть выполнены как просмотров через явную hello `x-ms-documentdb-enable-scan` заголовок в hello API-интерфейса REST или hello `EnableScanInQuery` запроса с помощью параметра hello .NET SDK. Некоторые функции запроса, например ORDER BY, не могут выполняться как сканирование с помощью `EnableScanInQuery`.

Hello следующей таблице показаны hello согласованности для запросов, основанных на режим индексирования hello (Consistent Lazy и None) при указании EnableScanInQuery.

|Целостность|Режим индексирования: согласованный|Режим индексирования: асинхронный|Режим индексирования: нет|
|---|---|---|---|
|Уровень согласованности Strong (сильная)|Уровень согласованности Strong (сильная)|В конечном счете|Уровень согласованности Strong (сильная)|
|Ограниченное устаревание|Ограниченное устаревание|В конечном счете|Ограниченное устаревание|
|Сеанс|Сеанс|В конечном счете|Сеанс|
|Уровень согласованности Eventual (в конечном счете)|В конечном счете|В конечном счете|Уровень согласованности Eventual (в конечном счете)|

Следующий образец кода показывают как Hello создайте коллекцию Azure Cosmos DB использование hello .NET SDK с согласованной индексирование на все операции вставки в документ.

     // Default collection creates a hash index for all string fields and a range index for all numeric    
     // fields. Hash indexes are compact and offer efficient performance for equality queries.

     var collection = new DocumentCollection { Id ="defaultCollection" };

     collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

     collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("mydb"), collection);


### <a name="index-paths"></a>Пути индекса
Azure Cosmos DB моделирует документов JSON и hello индекс как деревья и позволяет toopolicies tootune для путей в пределах дерева hello. В документах вы можете выбрать, какие пути необходимо включить или исключить из индексирования. Это можно предлагать повысить производительность записи и уменьшить хранилище индексирования для сценариев при hello шаблоны запросов известны заранее.

Пути индексов Возьмите hello корневой (/) и обычно заканчиваются на hello? оператор подстановочный знак, означающее, что существует несколько возможных значений для префикса hello. Например, tooserve ВЫБЕРИТЕ * из семейства F F.familyName WHERE = «Андерсен», должен включать путь индексирования для /familyName/? в политике индекса коллекции hello.

Пути индексов также можно использовать hello * поведение hello toospecify оператора подстановочный знак для пути рекурсивно hello префикс. Например, / полезных данных / * может быть используется tooexclude все данные hello полезные данные свойства из индексирования.

Ниже приведены hello Общие шаблоны для указания пути индексов.

| Путь                | Описание/вариант использования                                                                                                                                                                                                                                                                                         |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| /                   | Путь коллекции по умолчанию. Рекурсивные и применяет toowhole дерева документов.                                                                                                                                                                                                                                   |
| /prop/?             | Путь индексирования, необходимый запросы tooserve hello следующим образом (с типами Hash или диапазона соответственно):<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop > 5<br><br>SELECT FROM collection c ORDER BY c.prop                                                                       |
| /prop/*             | Путь индексирования для всех путей hello указанной меткой. Работает с hello, следующие запросы<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop.subprop > 5<br><br>SELECT FROM collection c WHERE c.prop.subprop.nextprop = "value"<br><br>SELECT FROM collection c ORDER BY c.prop         |
| /props/[]/?         | Путь индексирования, необходимый tooserve итерации и запросов JOIN к массивам скалярных значений вида [«a», «b», «c»]:<br><br>SELECT tag FROM tag IN collection.props WHERE tag = "value"<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag > 5                                                                         |
| /props/[]/subprop/? | Путь индексирования, необходимый tooserve итерации и запросов JOIN к массивам объектов, например [{subprop: «»}, {subprop: «b»}]:<br><br>SELECT tag FROM tag IN collection.props WHERE tag.subprop = "value"<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag.subprop = "value"                                  |
| /prop/subprop/?     | Путь индексирования, необходимый tooserve запросов (с типами Hash или диапазона соответственно):<br><br>SELECT FROM collection c WHERE c.prop.subprop = "value"<br><br>SELECT FROM collection c WHERE c.prop.subprop > 5                                                                                                                    |

> [!NOTE]
> При задании пути пользовательский индекс, являются индексирования правило необходимые toospecify hello по умолчанию для всего документа дерева hello, обозначается hello специальный путь «/ *». 
> 
> 

Hello следующий пример настраивает определенный путь с индексированием диапазон и точность пользовательских значение 20 байт:

    var collection = new DocumentCollection { Id = "rangeSinglePathCollection" };    

    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/Title/?", 
            Indexes = new Collection<Index> { 
                new RangeIndex(DataType.String) { Precision = 20 } } 
            });

    // Default for everything else
    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/*" ,
            Indexes = new Collection<Index> {
                new HashIndex(DataType.String) { Precision = 3 }, 
                new RangeIndex(DataType.Number) { Precision = -1 } 
            }
        });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), pathRange);


### <a name="index-data-types-kinds-and-precisions"></a>Типы данных, виды и степени точности индекса
Теперь, когда мы воспользовались обсуждается toospecify пути, давайте взглянем на параметры hello, мы можем использовать tooconfigure hello политики индексирования для пути. Можно указать одно или несколько определений индексирования для каждого пути.

* Тип данных: **String**, **Number**, **Point**, **Polygon** или **LineString** (может содержать только одну запись для каждого типа данных и пути).
* Вид индекса: **хэш-индекс** (запросы равенства), **диапазонный индекс** (запросы равенства, диапазона или ORDER BY) или **пространственный индекс** (пространственные запросы). 
* Точность: Для хэш-индекса это отличается от 1 too8 для строки и числа по умолчанию как 3. В индексе диапазона может использоваться значение -1 (максимальная точность). Для строк и чисел значение может меняться в диапазоне от 1 до 100 (максимальная точность).

#### <a name="index-kind"></a>Вид индекса
Azure Cosmos DB поддерживает хэш-индексы и диапазонные индексы для каждого пути (их можно настроить для чисел, строк или и того и другого).

* **Хэш-индекс** поддерживает эффективные запросы равенства и запросы JOIN. В большинстве случаев использования хэш-индексов не требуется более высокой точностью, чем значение по умолчанию hello 3 байта. DataType может иметь значение String или Number.
* **Диапазонный индекс** поддерживает эффективные запросы равенства, запросы диапазона (с использованием >, <, >=, <=, !=) и запросы ORDER BY. Запросы Order By по умолчанию также требуют максимальной точности индекса (-1). DataType может иметь значение String или Number.

Azure Cosmos DB также поддерживает hello тип пространственного индекса для каждого пути, который может быть задан для типов данных hello точки Polygon и LineString. значение Hello по указанному пути hello должно быть допустимым GeoJSON фрагмент как `{"type": "Point", "coordinates": [0.0, 10.0]}`.

* **Пространственный** индекс обеспечивает эффективность выполнения пространственных запросов (запросов нахождения в пределах и расстояния). DataType может иметь значение Point, Polygon или LineString.

> [!NOTE]
> Azure Cosmos DB поддерживает автоматическое индексирование данных типа Point, Polygon и LineString.
> 
> 

Ниже приведены типы индекса hello поддерживается, а также примеры запросов, их можно использовать tooserve.

| Вид индекса | Описание/вариант использования                                                                                                                                                                                                                                                                                                                                                                                                              |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Хэш       | Хэш-индекс по over/prop/? (или /) может быть hello используется tooserve следующие запросы эффективно:<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>Хэш-индекс по over /props/[]/? (или / или/свойства /) может быть hello используется tooserve следующие запросы эффективно:<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag = 5                                                                                                                       |
| Диапазонный индекс      | Диапазонный индекс по /prop/? (или /) может быть hello используется tooserve следующие запросы эффективно:<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop > 5<br><br>SELECT FROM collection c ORDER BY c.prop                                                                                                                                                                                                              |
| пространственный индекс     | Диапазонный индекс по /prop/? (или /) может быть hello используется tooserve следующие запросы эффективно:<br><br>SELECT FROM collection c<br><br>WHERE ST_DISTANCE(c.prop, {"type": "Point", "coordinates": [0.0, 10.0]}) < 40<br><br>SELECT FROM collection c WHERE ST_WITHIN(c.prop, {"type": "Polygon", ... }) --с индексированием точек<br><br>SELECT FROM collection c WHERE ST_WITHIN({"type": "Point", ... }, c.prop) --с индексированием многоугольников              |

По умолчанию возвращается сообщение об ошибке для запросов с помощью диапазона операторы, такие как > =, если отсутствует индекс диапазона (от любого точности) в порядке toosignal, проверки может быть необходимости tooserve hello запроса. Без диапазона индекса с помощью заголовка x-ms-documentdb-enable сканирования hello в hello API-интерфейса REST или параметр запроса EnableScanInQuery hello, с помощью hello .NET SDK могут выполняться запросы диапазона. Если в запросе hello, Azure Cosmos DB можно использовать toofilter hello индекса для других фильтров, будет возвращен без ошибок.

Hello и те же правила применяются для пространственных запросов. По умолчанию ошибка возвращается для пространственных запросов, если нет пространственного индекса, а не другие фильтры, которые могут быть получены из индекса hello. Они могут выполняться как сканирование с использованием x-ms-documentdb-enable-scan/EnableScanInQuery.

#### <a name="index-precision"></a>Точность индекса
Точность индекса обеспечивает компромисс между дополнительными затратами на хранение индекса и производительностью запросов. Для чисел рекомендуется использовать конфигурацию точность по умолчанию hello-1 («максимум»). Поскольку цифры 8 байт в формате JSON, это эквивалент tooa конфигурация размером 8 байт. Подбор меньшее значение точности, например 1-7, означает, что значения в некоторых toohello карты диапазоны же элемент указателя. Таким образом, Вы сократите место хранения индекса, но выполнение запроса может tooprocess дополнительные документы и т. е. как следствие использования более высокая пропускная способность единиц запросов.

Конфигурацию точности индекса практичнее использовать с диапазонами строки. Поскольку строки могут содержать любой произвольной длины, выбор hello hello индекс точности может повлиять на производительность hello строки запросов в диапазоне и влияние hello индекс хранилища необходимый объем. Для индексов диапазона строки можно настроить значения 1–100 или -1 (максимум). При желании tooperform Order By запросы к свойства строки необходимо указать точность-1 для hello соответствующие пути.

Пространственные индексы всегда используется точность индекса hello по умолчанию для всех типов (точки, LineStrings и многоугольники) и не может быть переопределен. 

Hello в следующем примере показано, как точность hello tooincrease для диапазона индексов в коллекции, используя hello .NET SDK. 

**Создание коллекции с пользовательской точностью индекса**

    var rangeDefault = new DocumentCollection { Id = "rangeCollection" };

    // Override hello default policy for Strings toorange indexing and "max" (-1) precision
    rangeDefault.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), rangeDefault);   


> [!NOTE]
> Azure Cosmos DB возвращает ошибку, если запрос использует Order By, но не имеет индекс диапазона для запрашиваемого пути hello с наибольшей точностью hello. 
> 
> 

Аналогичным образом пути можно полностью исключить из индексации. Hello следующем примере показано, как tooexclude целый раздел hello документы (так) поддерево) из индексирования с помощью hello «*» подстановочный знак.

    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*" });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);



## <a name="opting-in-and-opting-out-of-indexing"></a>Включение индексирования и отказ от него
Можно выбрать, следует ли индекс tooautomatically коллекции hello все документы. По умолчанию все документы индексируются автоматически, но вы можете tooturn его отключения. При выключенном индексировании документы могут быть доступны только через свои собственные ссылки или запросы, использующие идентификатор.

Автоматическое индексирование отключено, по-прежнему выборочно можно добавить только индекс toohello конкретных документов. И наоборот можно оставить автоматическое индексирование и выбирать tooexclude только конкретных документов. Индексирование и отключение конфигурации полезны при наличии только подмножество документов, которые необходимо запросить toobe.

Например, hello следующем образце показано, как tooinclude документа явным образом с помощью hello [пакет SDK .NET API DocumentDB](https://docs.microsoft.com/en-us/azure/cosmos-db/documentdb-sdk-dotnet) и hello [RequestOptions.IndexingDirective](http://msdn.microsoft.com/library/microsoft.azure.documents.client.requestoptions.indexingdirective.aspx) свойство.

    // If you want toooverride hello default collection behavior tooeither
    // exclude (or include) a Document from indexing,
    // use hello RequestOptions.IndexingDirective property.
    client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        new { id = "AndersenFamily", isRegistered = true },
        new RequestOptions { IndexingDirective = IndexingDirective.Include });

## <a name="modifying-hello-indexing-policy-of-a-collection"></a>Изменение политики индексирования hello коллекции
Azure Cosmos DB позволяет toomake изменения toohello политика индексирования коллекции на лету hello. Изменение в политике на Azure Cosmos DB коллекцию индексирования может привести tooa изменений в форме hello hello индекса, включая приветствия пути могут быть проиндексированы, их точность, а также модель согласованности hello самого индекса hello. Таким образом изменений в политике индексирования, фактически требует преобразования Здравствуй, старый индекс в новую. 

**Преобразование индексов в сети**

![Как работает индексирование — преобразование индексов Azure Cosmos DB в сети](./media/indexing-policies/index-transformations.png)

Индекс преобразования выполняются online, это означает, что документы hello индексируемых в старая политика hello эффективно преобразуются в каждой новой политики hello **без влияния на доступность записи hello или подготовленная пропускная способность hello** из Коллекция Hello. Здравствуйте, согласованность чтения и записи операций, выполняемых с помощью hello REST API, пакеты SDK или из внутри хранимых процедур и триггеров не влияет на во время преобразования индекса. Это означает, что не производительности приложений tooyour снижение или времени простоя при внесении изменений индексирования политики.

Однако во время hello, выполняется преобразование индекса, выполнение запросов, согласованным независимо от hello индексирования конфигурации режима (Consistent и Lazy). Это также касается tooqueries из всех интерфейсов — REST API, пакеты SDK и из хранимых процедур и триггеров. Так же, как с Lazy индексирования индекс преобразования выполняются асинхронно в фоновом режиме hello в репликах hello, с помощью hello запасные ресурсы, доступные для данной реплики. 

Индекс преобразования также выполняются **в месте** (на месте), т. е. Azure Cosmos DB не поддерживает две копии индекса hello и замены hello старый индекс out с hello новый. Это означает, что при выполнении преобразования индекса не требуется использовать дополнительное место на диске или в коллекции.

При изменении политики индексирования, как изменения hello, примененные toomove из hello старый индекс toohello новый один зависят главным образом hello индексирования конфигураций в режиме более, чем hello другие значения, такие как включенные или исключенные пути, типов индекса и точности. Если в старой и новой политике используется согласованное индексирование, то Azure Cosmos DB выполняет преобразование индекса в сети. Не удается применить другой индексирования изменение политики с согласованный режим индексирования во время выполнения преобразование «hello».

Тем не менее, можно переместить tooLazy или None режим индексирования во время преобразования выполняется в данный момент. 

* При перемещении tooLazy hello индекс политики изменения действующие немедленно и Azure Cosmos DB запускает повторное создание индекса hello асинхронно. 
* При перемещении tooNone затем hello индекс удаляется силу немедленно. Перемещение tooNone полезно, когда требуется toocancel выполняемое преобразования и запуск нового с другой политикой индексирования. 

Если вы используете hello .NET SDK, может запускаться индексирования изменение политики, с помощью нового hello **ReplaceDocumentCollectionAsync** метод и отслеживать hello процент ход выполнения преобразования hello индекс, с помощью hello  **IndexTransformationProgress** свойство ответа из **ReadDocumentCollectionAsync** вызова. Другие пакеты SDK и hello REST API поддерживают эквивалентные свойства и методы для внесения изменений в политике индексирования.

Ниже приведен фрагмент кода, показывающий, как политика из согласованного индексирования tooLazy режиме индексирования toomodify коллекции.

**Изменение политики индексирования из согласованного tooLazy**

    // Switch toolazy indexing.
    Console.WriteLine("Changing from Default tooLazy IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.Lazy;

    await client.ReplaceDocumentCollectionAsync(collection);


Ход выполнения hello преобразование индекса путем вызова ReadDocumentCollectionAsync, например, можно проверить, как показано ниже.

**Отслеживание хода выполнения преобразования индекса**

    long smallWaitTimeMilliseconds = 1000;
    long progress = 0;

    while (progress < 100)
    {
        ResourceResponse<DocumentCollection> collectionReadResponse = await client.ReadDocumentCollectionAsync(
            UriFactory.CreateDocumentCollectionUri("db", "coll"));

        progress = collectionReadResponse.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromMilliseconds(smallWaitTimeMilliseconds));
    }

Hello индекс для коллекции можно удалить путем перемещения toohello ни один режим индексирования. Это может быть полезным инструментом оперативной toocancel преобразования в процессе выполнения и немедленно запускает новый.

**Удаление индекса hello для коллекции**

    // Switch toolazy indexing.
    Console.WriteLine("Dropping index by changing tootoohello None IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.None;

    await client.ReplaceDocumentCollectionAsync(collection);

После бы внесения изменений в политике индексирования коллекции tooyour Azure Cosmos DB? Здесь представлены Hello hello наиболее распространенных вариантов использования:

* Использовать согласованные результаты во время обычной работы, но откат toolazy индексации во время массового импорта данных
* Начать использовать новые возможности индексирования в текущей базе данных Azure Cosmos коллекций, например, как и геопространственных запросов к которой требуется тип пространственного индекса hello или Order By и строки диапазона запросы, которые требуют строка hello тип диапазона индекса
* Передать индексированных toobe свойства выберите hello и со временем меняться
* Настройки производительности запросов tooimprove индексирования точности или уменьшите занятого хранилища

> [!NOTE]
> toomodify политика индексирования с помощью ReplaceDocumentCollectionAsync, требуется версия > = 1.3.0 из hello .NET SDK
> 
> Для преобразования toocomplete индекс успешно, убедитесь, что доступно достаточно свободного пространства на коллекцию hello. Если коллекция hello достигнет квоты хранилища, преобразование hello индекс будет приостановлена. Преобразование индекса автоматически возобновится при появлении доступного места, например, если вы удалите некоторые документы.
> 
> 

## <a name="performance-tuning"></a>Настройка производительности
Hello интерфейсы API DocumentDB предоставляют сведения о метриках производительности используется для хранения индекса hello, а пропускная способность hello стоимость (запроса ед.) для каждой операции. Эти сведения можно использовать toocompare различные политики индексирования и настройки производительности.

Квота хранилища hello toocheck использования коллекции, запустить запрос HEAD или GET для ресурса коллекции hello и проверять hello x-ms запрос quota и заголовки x-ms запрос usage hello. В hello .NET SDK, hello [DocumentSizeQuota](http://msdn.microsoft.com/library/dn850325.aspx) и [DocumentSizeUsage](http://msdn.microsoft.com/library/azure/dn850324.aspx) свойства в [ResourceResponse < T\> ](http://msdn.microsoft.com/library/dn799209.aspx) содержат эти соответствующие значения .

     // Measure hello document size usage (which includes hello index size) against   
     // different policies.
     ResourceResponse<DocumentCollection> collectionInfo = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));  
     Console.WriteLine("Document size quota: {0}, usage: {1}", collectionInfo.DocumentQuota, collectionInfo.DocumentUsage);


издержки hello toomeasure индексирования на каждой операции записи (Создание, обновление или удаление), проверьте заголовок x-ms запрос платы hello (или эквивалентное hello [RequestCharge](http://msdn.microsoft.com/library/dn799099.aspx) свойство в [ResourceResponse < T\> ](http://msdn.microsoft.com/library/dn799209.aspx) в hello .NET SDK) toomeasure hello количество единиц запроса, используемые в этих операций.

     // Measure hello performance (request units) of writes.     
     ResourceResponse<Document> response = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), myDocument);              
     Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);

     // Measure hello performance (request units) of queries.    
     IDocumentQuery<dynamic> queryable =  client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"), queryString).AsDocumentQuery();

     double totalRequestCharge = 0;
     while (queryable.HasMoreResults)
     {
        FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>(); 
        Console.WriteLine("Query batch consumed {0} request units",queryResponse.RequestCharge);
        totalRequestCharge += queryResponse.RequestCharge;
     }

     Console.WriteLine("Query consumed {0} request units in total", totalRequestCharge);

## <a name="changes-toohello-indexing-policy-specification"></a>Toohello изменения политики спецификация индексирования
7 июля 2015 г. с помощью API REST версии 2015-06-03 появилась на изменения в схеме hello для политики индексирования. соответствующие классы Hello в пакете SDK версии hello имеют новую схему hello toomatch реализации. 

следующие отличия Hello были реализованы в hello спецификации JSON:

* Политика индексации поддерживает диапазонные индексы для строк.
* Каждый путь может иметь несколько определений индекса, по одному для каждого типа данных.
* Поддерживаемая точность индексации: 1–8 для чисел, 1–100 для строк и –1 (максимальная точность).
* Сегменты пути, не требуют tooescape двойных кавычек каждого пути. Например, вы можете добавить путь для /title/? вместо /"title"/?
* путь к корневому Hello, представляющих «все пути» может быть представлено как / * (кроме слишком /)

Если у вас есть код, который подготавливает коллекций с помощью настраиваемой политики индексирования, написанным с использованием версии 1.1.0 hello .NET SDK или более ранних версий, необходимо будет toochange приложения code toohandle эти изменения в порядке toomove tooSDK версии 1.2.0. Если не имеется код, предназначенный для настройки политики индексирования или планирование toocontinue старую версию пакета SDK, изменения не требуются.

Для практического сравнения ниже приведен один пример настраиваемой политики индексирования, написанные с использованием hello API REST версия 2015-06-03, а также hello предыдущей версии 2015-04-08.

**Предыдущая политика индексации JSON**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "IncludedPaths":[
          {
             "IndexType":"Hash",
             "Path":"/",
             "NumericPrecision":7,
             "StringPrecision":3
          }
       ],
       "ExcludedPaths":[
          "/\"nonIndexedContent\"/*"
       ]
    }

**Текущая политика индексации JSON**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Hash",
                   "dataType":"String",
                   "precision":3
                },
                {
                   "kind":"Hash",
                   "dataType":"Number",
                   "precision":7
                }
             ]
          }
       ],
       "ExcludedPaths":[
          {
             "path":"/nonIndexedContent/*"
          }
       ]
    }

## <a name="next-steps"></a>Дальнейшие действия
Выполните hello ссылках ниже примеры управления политики индекса и toolearn Дополнительные сведения о языке запросов Azure Cosmos DB.

1. [Примеры кода управления индексами для API DocumentDB .NET](https://github.com/Azure/azure-documentdb-net/blob/master/samples/code-samples/IndexManagement/Program.cs)
2. [Collections](https://msdn.microsoft.com/library/azure/dn782195.aspx) (Коллекции)
3. [SQL-запросы для API DocumentDB в Azure Cosmos DB](documentdb-sql-query.md)

