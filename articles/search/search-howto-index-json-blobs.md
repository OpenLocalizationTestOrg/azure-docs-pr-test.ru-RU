---
title: "большие двоичные объекты JSON aaaIndexing с индексатор поиска Azure BLOB-объект"
description: "Индексирование BLOB-объектов JSON с помощью индексатора BLOB-объектов службы поиска Azure"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 57e32e51-9286-46da-9d59-31884650ba99
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: 269968714358cd40ea66863b4dbb97766e1d77e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-json-blobs-with-azure-search-blob-indexer"></a>Индексирование BLOB-объектов JSON с помощью индексатора BLOB-объектов службы поиска Azure
В этой статье показано, какую tooconfigure поиска Azure BLOB-объект индексатора tooextract структуру содержимого из BLOB-объектов, содержащих JSON.

## <a name="scenarios"></a>Сценарии
По умолчанию [индексатор больших двоичных объектов Поиска Azure](search-howto-indexing-azure-blob-storage.md) анализирует большие двоичные объекты JSON как один блок текста. Часто требуется структура hello toopreserve документов JSON. Например если документ JSON hello

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

может потребоваться tooparse его в поиске Azure документ с «text», «datePublished» и «теги» полей.

Кроме того, если BLOB-объектов содержат **массив объектов JSON**, вы можете каждый элемент массива hello toobecome отдельный документ поиска Azure. Например, если большой двоичный объект содержит приведенный ниже код JSON:  

    [
        { "id" : "1", "text" : "example 1" },
        { "id" : "2", "text" : "example 2" },
        { "id" : "3", "text" : "example 3" }
    ]

можно заполнить индекс Поиска Azure тремя отдельными документами, каждый из которых содержит поля "id" и "text".

> [!IMPORTANT]
> возможность анализа массив JSON Hello сейчас в предварительной версии. Он доступен только в версии API REST hello **2015-02-28-Preview**. Помните, что предварительные версии API предназначены для тестирования и ознакомления. Они не должны использоваться в рабочей среде.
>
>

## <a name="setting-up-json-indexing"></a>Настройка индексирования JSON
Индексирование больших двоичных объектов JSON является аналогичные извлечения toohello обычный документ. Сначала создайте источник данных hello точно так, как обычно. 

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "optional, my-folder" }
    }   

Если у вас его еще нет, создайте индекс поиска целевой hello. 

Наконец, создайте индексатор и задать hello `parsingMode` параметр слишком`json` (tooindex каждого blob как одного документа) или `jsonArray` (если BLOB-объектов содержат массивы JSON, и необходимо, чтобы каждый элемент массива toobe рассматривается как отдельный документ):

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } }
    }

При необходимости использовать **поля сопоставления** toopick hello свойства JSON документа, использованного hello источника toopopulate целевого индекса поиска, как показано в следующем разделе hello.

> [!IMPORTANT]
> При использовании режима анализа `json` или `jsonArray` служба поиска Azure предполагает, что все большие двоичные объекты в источнике данных содержат JSON. Если требуется toosupport сочетание JSON и не JSON больших двоичных объектов в hello же источник данных, сообщите нам о [нашем сайте UserVoice](https://feedback.azure.com/forums/263029-azure-search).
>
>

## <a name="using-field-mappings-toobuild-search-documents"></a>С помощью поля сопоставления toobuild поиск документов
Сейчас служба поиска Azure не может индексировать произвольные документы JSON напрямую, так как она поддерживает только простые типы данных, строковые массивы и точки GeoJSON. Тем не менее, можно использовать **поля сопоставления** toopick части JSON документов и «точности прогнозов» их в поля верхнего уровня документа поиска hello. toolearn об основах сопоставления полей, в разделе [моста hello различия между источниками данных и индексы поиска для сопоставления полей индексатор поиска Azure](search-indexer-field-mappings.md).

Ожидается tooour пример документа JSON:

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

Предположим, что имеется индекс поиска с hello следующие поля: `text` типа `Edm.String`, `date` типа `Edm.DateTimeOffset`, и `tags` типа `Collection(Edm.String)`. toomap JSON в hello ожидаемая форма, используйте следующие сопоставления полей hello:

    "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
      ]

Hello имена полей источника в сопоставлениях hello задаются с помощью hello [указатель JSON](http://tools.ietf.org/html/rfc6901) нотации. Начинаться с косой черты toorefer toohello корень документа JSON, а затем выбрать hello требуемого свойства (на произвольный уровне вложенности) с помощью прямой путь, разделенных косой черты.

Можно также ссылаться tooindividual элементы массива, используя отсчитываемый от нуля индекс. Например toopick hello первый элемент массива «теги» hello из hello в приведенном выше примере, использовать сопоставление полей следующим образом:

    { "sourceFieldName" : "/article/tags/0", "targetFieldName" : "firstTag" }

> [!NOTE]
> Если имя поля источника в поле сопоставления пути ссылается свойство tooa, которое не существует в JSON, это сопоставление пропускается без ошибок. Это необходимо для поддержки документов с разными схемами (что часто встречается на практике). Поскольку проверка не выполняется, вам потребуется tootake следить за tooavoid опечаток в спецификации сопоставления полей.
>
>

Если документы JSON содержат только простые свойства верхнего уровня, сопоставление полей может вообще не потребоваться. Например если JSON выглядит, свойства верхнего уровня hello «text», «datePublished» и «теги» напрямую сопоставляется toohello соответствующие поля в индекс поиска hello:

    {
       "text" : "A hopefully useful article explaining how tooparse JSON blobs",
       "datePublished" : "2016-04-13"
       "tags" : [ "search", "storage", "howto" ]    
     }

Ниже приведен полный набор данных индексатора с сопоставленными полями.

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } },
      "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
        ]
    }

## <a name="indexing-nested-json-arrays"></a>Индексирование вложенных массивов JSON
Что делать, если вы хотите tooindex массив объектов JSON, но этот массив является вложенным где-нибудь в документе hello? Можно выбрать, какие свойства содержит массив hello, с помощью hello `documentRoot` свойство конфигурации. Например, если большой двоичный объект выглядит следующим образом:

    {
        "level1" : {
            "level2" : [
                { "id" : "1", "text" : "Use hello documentRoot property" },
                { "id" : "2", "text" : "toopluck hello array you want tooindex" },
                { "id" : "3", "text" : "even if it's nested inside hello document" }  
            ]
        }
    }

Используйте этот массив hello tooindex конфигурации, содержащихся в hello `level2` свойство:

    {
        "name" : "my-json-array-indexer",
        ... other indexer properties
        "parameters" : { "configuration" : { "parsingMode" : "jsonArray", "documentRoot" : "/level1/level2" } }
    }

## <a name="help-us-make-azure-search-better"></a>Помогите нам усовершенствовать службу поиска Azure
При наличии запросов компонентов или идеи об улучшениях, направляться toous на нашем [сайт UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
