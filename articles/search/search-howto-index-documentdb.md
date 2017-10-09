---
title: "aaaIndexing Cosmos DB источника данных для службы поиска Azure | Документы Microsoft"
description: "В этой статье показано, как toocreate индексатор поиска Azure с помощью DB Cosmos в качестве источника данных."
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: search
ms.date: 08/10/2017
ms.author: eugenesh
ms.openlocfilehash: 195c9bc026ee1591679dc425ef083a32a3c86be6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-cosmos-db-with-azure-search-using-indexers"></a>Подключение Cosmos DB к службе поиска Azure с помощью индексаторов

Следует tooimplement возникают значительные поиска по данным Cosmos DB данных toopull индексатор поиска Azure можно использовать в индекс поиска Azure. В этой статье мы покажем, как toointegrate DB Cosmos Azure с поиском Azure без необходимости toowrite любой код toomaintain индексирования инфраструктуры.

tooset копирование индексатора Cosmos DB должен иметь [службы поиска Azure](search-create-service-portal.md)и создание индекса, источник данных и наконец hello индексатора. Можно создать эти объекты с помощью hello [портала](search-import-data-portal.md), [.NET SDK](/dotnet/api/microsoft.azure.search), или [API-интерфейса REST](/rest/api/searchservice/) для всех языков, отличных от .NET. 

Здравствуйте, если вы выбрали для портала hello, [мастера импорта данных](search-import-data-portal.md) проводит пользователя через создание hello этих ресурсов.

> [!NOTE]
> Cosmos DB — hello DocumentDB нового поколения. Несмотря на то, что изменения имени продукта hello синтаксис является hello же как и раньше. Продолжайте toospecify `documentdb` как указано в этой статье индексатора. 

> [!TIP]
> Можно запустить hello **импорта данных** мастера из hello Cosmos DB мониторинга toosimplify индексирования для этого источника данных. В левой панели навигации, go слишком**коллекций** > **добавить поиск Azure** tooget работы.

<a name="Concepts"></a>
## <a name="azure-search-indexer-concepts"></a>Понятия индексатора в службе Поиск Azure
Azure поиска поддерживает hello создания и управления источников данных (включая Cosmos DB) и индексаторы, работающих этих источниках данных.

Объект **источника данных** указывает hello tooindex данных, учетные данные и политики обнаружения изменений в данных hello (например, измененных или удаленных документы в коллекции). источник данных Hello определяется как независимый ресурс, чтобы его можно использовать несколько индексаторов.

**Индексатора** описывает hello направление потока данных из источника данных в целевой индекс поиска. Индексатор может использоваться:

* Выполнение однократного копирования данных hello toopopulate индекса.
* Синхронизация индекса с изменениями в источнике данных hello по расписанию. Hello расписание является частью определения индексатора hello.
* Вызовите индекс tooan обновлений по требованию по мере необходимости.

<a name="CreateDataSource"></a>
## <a name="step-1-create-a-data-source"></a>Шаг 1. Создание источника данных
toocreate источника данных, выполните POST.

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId", "query": null },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        }
    }

текст Hello hello запроса содержит определение источника данных hello, который должен содержать следующие поля hello:

* **имя**: выберите любое имя toorepresent Cosmos DB базы данных.
* **type** должно иметь значение `documentdb`.
* **credentials**:
  
  * **connectionString**: обязательное поле. Укажите hello подключения сведения tooyour Azure Cosmos DB базу данных в кодировке hello:`AccountEndpoint=<Cosmos DB endpoint url>;AccountKey=<Cosmos DB auth key>;Database=<Cosmos DB database id>`
* **container**:
  
  * **name**: обязательное поле. Укажите идентификатор hello hello Cosmos DB коллекции toobe проиндексированы.
  * **query**: необязательное поле. Можно указать запрос tooflatten произвольный документа JSON в плоскую схему, поиск Azure можно индексировать.
* **dataChangeDetectionPolicy** — рекомендуемое поле. Ознакомьтесь с разделом [Индексация измененных документов](#DataChangeDetectionPolicy).
* **dataDeletionDetectionPolicy**: необязательное поле. Ознакомьтесь с разделом [удаленных документов](#DataDeletionDetectionPolicy).

### <a name="using-queries-tooshape-indexed-data"></a>С помощью запросов tooshape индексированных данных
Можно указать tooflatten запроса Cosmos DB вложенные свойства или массивов JSON свойства проекта, а также фильтровать индексированных toobe данных hello. 

Пример документа:

    {
        "userId": 10001,
        "contact": {
            "firstName": "andy",
            "lastName": "hoh"
        },
        "company": "microsoft",
        "tags": ["azure", "documentdb", "search"]
    }

Запрос на фильтрацию:

    SELECT * FROM c WHERE c.company = "microsoft" and c._ts >= @HighWaterMark ORDER BY c._ts

Преобразование запросов:

    SELECT c.id, c.userId, c.contact.firstName, c.contact.lastName, c.company, c._ts FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts
    
    
Запрос на проектирование:

    SELECT VALUE { "id":c.id, "Name":c.contact.firstName, "Company":c.company, "_ts":c._ts } FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts


Массив преобразованных запросов:

    SELECT c.id, c.userId, tag, c._ts FROM c JOIN tag IN c.tags WHERE c._ts >= @HighWaterMark ORDER BY c._ts

<a name="CreateIndex"></a>
## <a name="step-2-create-an-index"></a>Шаг 2. Создание индекса
Создайте целевой индекс поиска Azure, если это еще не сделано. Можно создать индекс с помощью hello [портал Azure пользовательского интерфейса](search-create-index-portal.md), hello [создать индекс API-интерфейса REST](/rest/api/searchservice/create-index) или [класс Index](/dotnet/api/microsoft.azure.search.models.index).

Следующий пример Hello создает индекс с идентификатором и описанием поля:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
       "name": "mysearchindex",
       "fields": [{
         "name": "id",
         "type": "Edm.String",
         "key": true,
         "searchable": false
       }, {
         "name": "description",
         "type": "Edm.String",
         "filterable": false,
         "sortable": false,
         "facetable": false,
         "suggestions": true
       }]
     }

Убедитесь, что hello схемы целевого индекса совместима с hello схема hello исходные документы JSON или вывода hello проекции вашего пользовательского запроса.

> [!NOTE]
> Для секционированных коллекций hello ключ документа по умолчанию представляет собой Cosmos DB `_rid` свойство, которое возвращает переименован слишком`rid` в поиске Azure. Кроме того, значения `_rid` Cosmos DB содержат символы, недопустимые в ключах службы поиска Azure. По этой причине hello `_rid` значения, закодированные методом Base64.
> 
> 

### <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>Сопоставление типов данных JSON и типов данных службы поиска Azure
| ТИП ДАННЫХ JSON | СОВМЕСТИМЫЕ ТИПЫ ПОЛЕЙ ЦЕЛЕВОГО ИНДЕКСА |
| --- | --- |
| Bool |Edm.Boolean, Edm.String |
| Числа, которые выглядят как целые числа |Edm.Int32, Edm.Int64, Edm.String |
| Числа, которые выглядят как числа с плавающей запятой |Edm.Double, Edm.String |
| Строка |Edm.String |
| Массивы типов-примитивов, например [a, b, c] |Collection(Edm.String) |
| Строки, которые выглядят как даты |Edm.DateTimeOffset, Edm.String |
| Геообъекты JSON, например { "тип": "Точка", "координаты": [ долгота, широта ] } |Edm.GeographyPoint |
| Другие объекты JSON |Недоступно |

<a name="CreateIndexer"></a>
## <a name="step-3-create-an-indexer"></a>Шаг 3. Создание индексатора

После создания hello индекс и источник данных вы будете готовы toocreate hello индексатора:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "mydocdbindexer",
      "dataSourceName" : "mydocdbdatasource",
      "targetIndexName" : "mysearchindex",
      "schedule" : { "interval" : "PT2H" }
    }

Этот индексатор запускается каждые два часа (интервал расписания задано слишком «PT2H»). toorun индексатор каждые 30 минут для интервала hello слишком «PT30M». Hello минимально поддерживаемые интервал составляет 5 минут. Hello расписания необязательно — Если не указано, индексатор, который выполняется только один раз, при его создании. Однако индексатор можно запустить по запросу в любое время.   

Дополнительные сведения о hello создания API индексатора, ознакомьтесь с [Создание индексатора](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

<a id="RunIndexer"></a>
### <a name="running-indexer-on-demand"></a>Запуск индексатора по требованию
В дополнение toorunning периодически по расписанию индексатор, который также может вызываться по требованию:

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=2016-09-01
    api-key: [Search service admin key]

> [!NOTE]
> По возвращении запуска API вызове индексатора hello было запланировано, но hello Фактическая обработка происходит асинхронно. 

Можно отслеживать состояние индексатора hello hello портала или с помощью hello получение индексатора состояние интерфейса API, который рассматривается далее. 

<a name="GetIndexerStatus"></a>
### <a name="getting-indexer-status"></a>Получение состояния индексатора
Можно получить hello состояние и журнал выполнений индексатора.

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=2016-09-01
    api-key: [Search service admin key]

Hello ответ содержит общее состояние индексатора, вызове индексатора последний (или выполняющихся) hello и hello журнал последних вызовов индексатора.

    {
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
         },
        "executionHistory":[ {
            "status":"success",
             "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        }]
    }

Журнал выполнения содержит до toohello 50 последних выполнение, которые сортируются в обратном хронологическом порядке (в этом последнем выполнении hello идет первой в ответ hello).

<a name="DataChangeDetectionPolicy"></a>
## <a name="indexing-changed-documents"></a>Индексация измененных документов
Назначение данных Hello политику обнаружения изменения tooefficiently определения измененных элементов данных. В настоящее время поддерживается только hello политики — hello `High Water Mark` политики с помощью hello `_ts` свойство (отметка времени), предоставляемые Cosmos DB, который указывается следующим образом:

    {
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "_ts"
    }

Tooensure индексатора хорошей производительности настоятельно рекомендуется использовать эту политику. 

При использовании пользовательского запроса, убедитесь в том, что hello `_ts` свойство проецируется запросом hello.

<a name="IncrementalProgress"></a>
### <a name="incremental-progress-and-custom-queries"></a>Инкрементное индексирование и пользовательские запросы
В ходе во время индексирования позволяет при прерывании выполнения индексатора временные сбои или ограничение времени выполнения, hello индексатора можно обнаружить прерванную следующий раз он выполняется вместо индекса toore hello всю коллекцию с нуля. Это особенно важно для индексации больших коллекций. 

в ходе tooenable при использовании пользовательского запроса, убедитесь, что запрос упорядочивает результаты hello по hello `_ts` столбца. Это позволяет периодически контрольных точек, поиск Azure использует tooprovide хода в присутствии hello сбоев.   

В некоторых случаях даже в том случае, если запрос содержит `ORDER BY [collection alias]._ts` предложение, поиск Azure может не определить, hello запрос упорядочен по hello `_ts`. Можно определить поиска Azure, что результаты сортируются с помощью hello `assumeOrderByHighWaterMarkColumn` свойство конфигурации. toospecify это указание создать или обновить индексатор следующим образом: 

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "assumeOrderByHighWaterMarkColumn" : true } }
    } 

<a name="DataDeletionDetectionPolicy"></a>
## <a name="indexing-deleted-documents"></a>Индексация удаленных документов
Когда строки удаляются из коллекции hello, обычно требуется toodelete те строки из индекса поиска hello также. Hello политику обнаружения удалений данных предназначена tooefficiently определения удаленных элементов данных. В настоящее время поддерживается только hello политики — hello `Soft Delete` политики (удаление помечен флаг определенного рода), что указывается следующим образом:

    {
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello property that specifies whether a document was deleted",
        "softDeleteMarkerValue" : "hello value that identifies a document as deleted"
    }

При использовании пользовательского запроса, убедитесь, что это свойство hello ссылается `softDeleteColumnName` проецируется запросом hello.

Следующий пример Hello создает источник данных с помощью политики обратимого удаления:

    POST https://[Search service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId" },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        },
        "dataDeletionDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName": "isDeleted",
            "softDeleteMarkerValue": "true"
        }
    }

## <a name="NextSteps"></a>Дальнейшие действия
Поздравляем! Вы узнали, каким образом toointegrate Azure Cosmos DB с помощью поиска Azure hello индексатора для Cosmos DB.

* toolearn как Дополнительные сведения о базе данных Azure Cosmos, в разделе hello [страница службы Cosmos DB](https://azure.microsoft.com/services/documentdb/).
* toolearn как Дополнительные сведения о поиске Azure, в разделе hello [страницы службы поиска](https://azure.microsoft.com/services/search/).
