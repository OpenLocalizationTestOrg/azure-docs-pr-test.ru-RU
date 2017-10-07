---
title: "aaaWorking с геопространственных данных в базе данных Azure Cosmos | Документы Microsoft"
description: "Сведения об toocreate, индекс и запрос пространственных объектов с помощью Azure Cosmos DB и hello DocumentDB API."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 82ce2898-a9f9-4acf-af4d-8ca4ba9c7b8f
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/22/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1e40b78cb4595631d845d46c21d07a30c8b972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a>Работа с геопространственными данными и данными расположений GeoJSON в Azure Cosmos DB
В этой статье представлено введение toohello геопространственные функции [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/). После прочтения этого, можно будет tooanswer hello следующие вопросы:

* Как хранить пространственные данные в Azure Cosmos DB?
* Как запрашивать геопространственные данные в Azure Cosmos DB с помощью SQL и LINQ?
* Как включить или отключить пространственное индексирование в Azure Cosmos DB?

В этой статье показано, как toowork с пространственными данными с hello DocumentDB API. Примеры кода можно найти в [следующем проекте GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs).

## <a name="introduction-toospatial-data"></a>Введение toospatial данных
Пространственные данные Описание позиции hello и форме объектов в пространстве. В большинстве приложений они соответствуют tooobjects на Земле hello, т. е. геопространственных данных. Пространственные данные могут быть расположение hello используется toorepresent человека, мест, представляющих интерес или границ hello города или озере. Наиболее распространенные случаи часто включают запросы близости, например "найти все кафе рядом с моим текущим местоположением". 

### <a name="geojson"></a>GeoJSON
Azure Cosmos DB поддерживает индексирование и запросы геопространственных точки данных, которые представляются в виде hello [GeoJSON спецификации](https://tools.ietf.org/html/rfc7946). Структуры данных GeoJSON всегда являются действительными объектами JSON, поэтому их можно сохранять и опрашивать с помощью Azure Cosmos DB без специальных средств или библиотек. Hello пакеты SDK Azure Cosmos DB предоставляют вспомогательные классы и методы, которые позволяют легко toowork с пространственными данными. 

### <a name="points-linestrings-and-polygons"></a>Точки, объекты LineString и многоугольники
**Точка** обозначает одно положение в пространстве. В геопространственные данные точки представляет hello точное расположение, которое может быть адрес продуктового магазина, киоске, автомобиль или города.  В GeoJSON (и Azure Cosmos DB) точка представляется в виде пары координат или широты и долготы. Ниже приведен пример JSON для точки.

**Точки в базе данных Azure Cosmos DB**

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> Спецификация GeoJSON Hello указывает долготы first и широту второй. Как и в других картах, широта и долгота представляют собой углы и выражаются в градусах. Значения долготы измеряются от главного меридиана hello и находятся в диапазоне от -180 и 180.0 градусов и широту значения отсчитываются от экватора hello и находятся в диапазоне от-90.0 до 90.0 градусов. 
> 
> Azure Cosmos DB интерпретирует координаты, представленных в системе ссылок WGS 84 hello. Дополнительные сведения о системах координат см. ниже.
> 
> 

Их можно включить в документ Azure Cosmos DB, как показано в следующем примере профиля пользователя, содержащего данные о местоположении:

**Использование профиля с данными о местоположении, которые хранятся в Azure Cosmos DB**

```json
{
    "id":"documentdb-profile",
    "screen_name":"@CosmosDB",
    "city":"Redmond",
    "topics":[ "global", "distributed" ],
    "location":{
        "type":"Point",
        "coordinates":[ 31.9, -4.8 ]
    }
}
```

Кроме toopoints GeoJSON поддерживает LineStrings и многоугольники. **LineStrings** представляют ряд двух или более точек в пространстве и hello сегменты линии, которые их соединяют. В геопространственных данных LineStrings, часто используемые toorepresent автомагистралях или реки. **Многоугольник** представляет собой область, ограниченную соединенными друг с другом точками, которая образует замкнутый объект LineString. Многоугольники, часто используемые toorepresent естественное структур как Озера или политическая юрисдикции как города и области. Ниже приведен пример многоугольника в Azure Cosmos DB. 

**Многоугольники в GeoJSON**

```json
{
    "type":"Polygon",
    "coordinates":[
        [ 31.8, -5 ],
        [ 31.8, -4.7 ],
        [ 32, -4.7 ],
        [ 32, -5 ],
        [ 31.8, -5 ]
    ]
}
```

> [!NOTE]
> Hello GeoJSON спецификация требует допустимый многоугольников hello последней парой координат предоставленный следует hello же, как первого, toocreate hello замкнутую фигуру.
> 
> Точки внутри многоугольника должны указываться в порядке против часовой стрелки. Многоугольник, указанным в заказе по часовой стрелке представляет обратное hello hello области внутри него.
> 
> 

В дополнение tooPoint, LineString, а также многоугольников, GeoJSON также задает представление hello как toogroup несколько геопространственных, а также tooassociate произвольные свойства с географическом расположении, что **функция**. Так как эти объекты являются действительными объектами JSON, их можно хранить и обрабатывать в Azure Cosmos DB. Однако Azure Cosmos DB поддерживает только автоматическую индексацию точек.

### <a name="coordinate-reference-systems"></a>Системы координат
Поскольку нестандартные фигуры hello hello земли, координаты геопространственных данных представляется во многих системах отсчета координат (CRS), каждый из которых собственных кадров для ссылок и единицы измерения. Например, «National сетки для Великобритании» hello является эталонной системы имеет высокую точность для hello United Kingdom, но не вне его. 

Hello наиболее популярных CRS используется на сегодняшний день является hello системе [WGS 84](http://earth-info.nga.mil/GandG/wgs84/). WGS-84 используют устройства GPS и многие службы географических карт, в том числе Карты Google и API-интерфейсы Карт Bing. Azure Cosmos DB поддерживает индексирование и запросы геопространственных данных с помощью только hello CRS WGS 84. 

## <a name="creating-documents-with-spatial-data"></a>Создание документов с пространственными данными
При создании документов, содержащих GeoJSON значения, они автоматически индексируются в пространственном индексе в политике индексирования toohello пикселями hello коллекции. При работе с пакетом SDK Azure Cosmos DB в динамически типизированных языках программирования, таких как Python или Node.js, необходимо создавать действительные объекты GeoJSON.

**Создание документа с геопространственными данными в Node.js**

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within hello callback
});
```

Можно использовать при работе с hello интерфейсы API DocumentDB hello `Point` и `Polygon` классов внутри hello `Microsoft.Azure.Documents.Spatial` сведения о расположении tooembed пространства имен в пределах объектов приложения. Эти классы упростить hello сериализации и десериализации пространственных данных в GeoJSON.

**Создание документа с геопространственными данными в .NET**

```json
using Microsoft.Azure.Documents.Spatial;

public class UserProfile
{
    [JsonProperty("name")]
    public string Name { get; set; }

    [JsonProperty("location")]
    public Point Location { get; set; }

    // More properties
}

await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "profiles"), 
    new UserProfile 
    { 
        Name = "documentdb", 
        Location = new Point (-122.12, 47.66) 
    });
```

Если нет данных широты и долготы hello, но иметь hello физические адреса или имя расположения, например города или страны, фактический координаты hello производить поиск с помощью службы геокодирования, таких как службы Bing Maps REST. Дополнительные сведения о геокодировании в Картах Bing можно найти [здесь](https://msdn.microsoft.com/library/ff701713.aspx).

## <a name="querying-spatial-types"></a>Типы запросов к пространственным данным
Теперь, когда мы воспользовались обсуждается tooinsert геопространственные данные, давайте взглянем на как tooquery эти данные с помощью DB Cosmos Azure с помощью SQL и технологии LINQ.

### <a name="spatial-sql-built-in-functions"></a>Встроенные функции для обработки пространственных данных в SQL
Azure Cosmos DB поддерживает следующие встроенные функции Open Geospatial Consortium (OGC) для выполнения запросов к геопространственных hello. Дополнительные сведения о hello полный набор встроенных функций в hello языка SQL можно найти слишком[запросов Azure Cosmos DB](documentdb-sql-query.md).

<table>
<tr>
  <td><strong>Использование</strong></td>
  <td><strong>Описание</strong></td>
</tr>
<tr>
  <td>ST_DISTANCE (spatial_expr, spatial_expr)</td>
  <td>Возвращает hello расстояние между выражениями hello две точки GeoJSON Polygon и LineString.</td>
</tr>
<tr>
  <td>ST_WITHIN (spatial_expr, spatial_expr)</td>
  <td>Возвращает выражение типа Boolean, показывающего, является hello GeoJSON сперва (точка Polygon и LineString) в рамках hello второй GeoJSON объекта (точка Polygon и LineString).</td>
</tr>
<tr>
  <td>ST_INTERSECTS (spatial_expr, spatial_expr)</td>
  <td>Возвращает логическое выражение, указывающее, пересекается ли hello двух указанных GeoJSON объектов (точка Polygon и LineString).</td>
</tr>
<tr>
  <td>ST_ISVALID</td>
  <td>Возвращает логическое значение, указывающее, является ли hello точки GeoJSON Polygon и LineString выражение допустимо.</td>
</tr>
<tr>
  <td>ST_ISVALIDDETAILED</td>
  <td>Возвращает значение JSON, содержащий логическое значение, указываемое hello точки GeoJSON Polygon и LineString выражение является допустимым и если недействительной, кроме того hello причина как строковое значение.</td>
</tr>
</table>

Пространственные функции могут быть запросами сходству используется tooperform пространственных данных. Например ниже приведен запрос, возвращающий все семейство документы, в течение 30 км hello указанное расположение используется встроенная функция ST_DISTANCE hello. 

**Запрос**

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

**Результаты**

    [{
      "id": "WakefieldFamily"
    }]

При включении пространственное индексирование в политику индексации, затем «расстояние запросы» будет обслуживаться эффективно hello индекса. Дополнительные сведения о пространственных индексирования см. в разделе ниже hello. Если у вас нет пространственного индекса для hello указано пути, по-прежнему выполнять Пространственные запросы, указав `x-ms-documentdb-query-enable-scan` заголовок запроса со значением hello установлен слишком «true». В .NET, это можно сделать путем передачи hello необязательно **FeedOptions** tooqueries аргумент с [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) задать tootrue. 

ST_WITHIN может быть toocheck используется, если точка находится внутри многоугольника. Часто многоугольников, используемые toorepresent границ, например почтовые индексы, состояние границы или естественным структур. Еще раз при включении пространственное индексирование в политику индексации, затем запросов «в» будет обслуживаться эффективно hello индекса. 

Аргументы многоугольника в ST_WITHIN может содержать только один кольцо, т. е. hello многоугольников не должен содержать уязвимости в них. 

**Запрос**

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

**Результаты**

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> Похожих несоответствие toohow работает в Azure Cosmos DB запроса, указываемое значение расположения hello в либо аргумент имеет неправильный формат или является недопустимым, то он будет оценен слишком**не определено** и пропуска toobe документа hello вычисляется из hello результаты запроса. Если запрос не возвращает результатов, запустите toodebug ST_ISVALIDDETAILED, почему имеет недопустимый тип spatail hello.     
> 
> 

Azure Cosmos DB также поддерживает выполнение обратный запросы, т. е. можно индексировать многоугольников и линий в базе данных Azure Cosmos, а затем запросить hello области, которые содержат указанную точку. Этот шаблон обычно используется в tooidentify материально-технического обеспечения например когда грузовик или выходе из указанной области. 

**Запрос**

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


**Результаты**

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

ST_ISVALID и ST_ISVALIDDETAILED могут быть toocheck используется, если пространственный объект является допустимым. Например приветствия при следующем запросе проверяет допустимость hello точки с вне диапазона значений широты (-132.8). ST_ISVALID возвращает логическое значение, и hello ST_ISVALIDDETAILED возвращает логическое значение и строка, содержащая hello причины, почему он считается недопустимым.

** Запрос **

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

**Результаты**

    [{
      "$1": false
    }]

Эти функции также могут быть многоугольниками используется toovalidate. Например здесь мы используем ST_ISVALIDDETAILED toovalidate многоугольник, который не закрывается. 

**Запрос**

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

**Результаты**

    [{
       "$1": { 
            "valid": false, 
            "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a Polygon must have hello same start and end points." 
          }
    }]

### <a name="linq-querying-in-hello-net-sdk"></a>В .NET SDK hello запросов LINQ
Hello DocumentDB .NET SDK также поставщики заглушки методов `Distance()` и `Within()` для использования в выражениях LINQ. Hello DocumentDB LINQ поставщик преобразует эти вызовы toohello эквивалент SQL встроенной функции вызовы методов (ST_DISTANCE и ST_WITHIN соответственно). 

Вот пример запроса LINQ, который находит все документы в коллекции Azure Cosmos DB hello, «местоположение», значение которого в пределах радиуса 30 км hello указывается точки с использованием LINQ.

**Запросы LINQ для определения расстояния**

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

Аналогичным образом ниже приведен запрос для поиска всех документов hello, «местоположение» находится в пределах hello указанное поле или многоугольник. 

**Запросы LINQ для определения принадлежности**

    Polygon rectangularArea = new Polygon(
        new[]
        {
            new LinearRing(new [] {
                new Position(31.8, -5),
                new Position(32, -5),
                new Position(32, -4.7),
                new Position(31.8, -4.7),
                new Position(31.8, -5)
            })
        });

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(a => a.Location.Within(rectangularArea)))
    {
        Console.WriteLine("\t" + user);
    }


Теперь, когда мы воспользовались обсуждается tooquery документы с помощью LINQ и SQL, давайте взглянем на как tooconfigure Azure Cosmos DB для пространственного индексирования.

## <a name="indexing"></a>Индексация
Как было описано в hello [схемы независимой от индексирования с помощью Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) бумаги, мы разработали toobe ядра базы данных Azure Cosmos DB действительно зависит от схемы и обеспечивают превосходную поддержку JSON. Hello записи оптимизированной СУБД Azure Cosmos DB собственными средствами различает Пространственные данные (указывает, многоугольников и линий), представлен в стандартном GeoJSON hello.

По сути, hello geometry спроецировано из геодезические координаты на двумерной плоскости затем постепенно разделить ячеек с помощью **quadtree**. Эти ячейки являются сопоставленных too1D на основе расположения hello hello ячейки **пространства кривой Гильберта**, сохраняющее локальность точек. Кроме того при индексировании данных расположения, он проходит через этот процесс называется **тесселяции**, т. е. все ячейки hello, пересекающих расположение идентифицируются и находящиеся в качестве ключей в индексе hello Azure Cosmos DB. Во время обработки запроса аргументы, такие как точки и многоугольники, также тесселированных tooextract hello диапазоны Идентификаторов соответствующую ячейку, а затем использовать tooretrieve данным из индекса hello.

При указании индексирования политики, которая включает пространственного индекса для / * (все пути), а затем все точки, найденных в коллекции hello индексируются для обеспечения эффективного поиска пространственных (ST_WITHIN и ST_DISTANCE). Пространственные индексы не имеют значения точности и всегда используют значение точности по умолчанию.

> [!NOTE]
> Azure Cosmos DB поддерживает автоматическое индексирование данных типа Point, Polygon и LineString.
> 
> 

Hello следующем фрагменте JSON показан политику индексации с пространственное индексирование включено, т. е. индекс любой точке GeoJSON, найденных в документах для пространственных запросов. При добавлении или изменении с помощью портала Azure hello политика индексирования hello, можно указать hello, следуя JSON для индексирования tooenable политики пространственного индексирования в коллекции.

**JSON политики пространственного индексирования коллекций для точек и многоугольников**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Range",
                   "dataType":"String",
                   "precision":-1
                },
                {
                   "kind":"Range",
                   "dataType":"Number",
                   "precision":-1
                },
                {
                   "kind":"Spatial",
                   "dataType":"Point"
                },
                {
                   "kind":"Spatial",
                   "dataType":"Polygon"
                }                
             ]
          }
       ],
       "excludedPaths":[
       ]
    }

Ниже приведен фрагмент кода в .NET, который показывает, как toocreate пространственное индексирование коллекции установлен в on для всех путей, содержащий точки. 

**Создание коллекции с пространственным индексированием**

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override tooturn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

И вот как можно изменять существующие коллекции tootake преимущество пространственное индексирование через все точки, которые хранятся в документах.

**Изменение коллекции с пространственным индексированием**

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing toocomplete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> Если расположение hello GeoJSON значение в документе hello имеет неправильный формат или является недопустимым, затем его не получить индексироваться для пространственных запросов. Проверить значение расположения можно с помощью ST_ISVALID и ST_ISVALIDDETAILED.
> 
> Если определение коллекции включает ключ секции, информация о ходе выполнения преобразования индекса не предоставляется. 
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали о том, как tooget работы с поддержку геопространственных в базе данных Azure Cosmos, вы можете:

* Начать создание кода с hello [образцы кода геопространственных .NET на GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)
* Получить руки на с геопространственных запросов для hello [площадку запросов DB Cosmos Azure](http://www.documentdb.com/sql/demo#geospatial)
* Дополнительные сведения о запросах Azure Cosmos DB см. [здесь](documentdb-sql-query.md).
* Дополнительные сведения о политиках индексации в Azure Cosmos DB см. в [этой статье](indexing-policies.md).

