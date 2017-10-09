---
title: "Поиск службы REST API версия 2015-02-28-Preview aaaAzure | Документы Microsoft"
description: "В версии 2015-02-28-Preview API REST службы поиска Azure реализованы экспериментальные функции, такие как анализаторы естественных языков и запросы moreLikeThis."
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 05/01/2017
ms.author: brjohnst
ms.openlocfilehash: 63cb30b7f43a42552c6744ea087afea947857224
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a>API REST службы поиска Azure, версия 2015-02-28-Preview
Эта статья является hello справочную документацию по `api-version=2015-02-28-Preview`. Этой предварительной версии расширяет hello текущей общедоступной версии, [api-version = 2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), предоставляя следующие экспериментальные функции hello:

* `moreLikeThis`параметр в hello запроса [поиск документов](#SearchDocs) API. Она находит другие документы, соответствующие tooanother конкретный документ.

Несколько дополнительных частей приложения hello `2015-02-28-Preview` API-интерфейса REST описаны отдельно. В частности, описаны такие возможности:

* [Профили оценки](search-api-scoring-profiles-2015-02-28-preview.md)
* [Индексаторы](search-api-indexers-2015-02-28-preview.md)

Существуют различные версии службы поиска Azure. См. слишком[управление версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx) подробные сведения.

## <a name="apis-in-this-document"></a>API, рассматриваемый в этом документе
API службы поиска Azure поддерживает две синтаксические схемы URL, которые можно использовать для операций API: простой синтаксис и синтаксис OData, который описан в статье о [поддержке OData в API службы поиска Azure](http://msdn.microsoft.com/library/azure/dn798932.aspx). Hello следующем списке показан простой синтаксис hello.

[Создание индекса](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[Обновление индекса](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[Получение индекса](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[Получение списка индексов](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[Получение статистических данных индекса](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[Анализатор теста](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[Удаление индекса](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[Добавление, удаление и обновление данных в индексе](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[Поиск документов](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[Запрос документов](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[Подсчет документов](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[Предложения](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a>Операции с индексом
Для создания индексов в службе поиска Azure и управления ими используются простые HTTP-запросы (POST, GET, PUT, DELETE), отправляемые к определенному ресурсу индекса. toocreate индекс первого сообщения документ JSON, описывающий hello схемы индекса. Hello схема определяет поля hello hello индекса, их типы данных, и описание их использования (например, в полнотекстовый поиск, сортировка и фильтры аспекты). Он также определяет профили оценки, средств подбора и другие атрибуты tooconfigure hello поведение hello индекса.

Hello ниже приведен пример схемы, используемый для поиска сведений об отелях с hello поле описания, определенном на двух языках. Обратите внимание на то, как атрибуты определяют, как используется поле hello. Здравствуйте, например `hotelId` используется как ключ документа hello (`"key": true`) и исключается из полнотекстового поиска (`"searchable": false`).

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

После создания индекса hello, вы отправите документы, заполняющие индекс hello. Этот этап описан в разделе [Добавление и обновление документов](#AddOrUpdateDocuments) .

Tooindexing Видеоролик с общими сведениями, в поиске Azure, в разделе hello [Channel 9 Cloud Cover серии о поиске Azure](http://go.microsoft.com/fwlink/p/?LinkId=511509).

<a name="CreateIndex"></a>

## <a name="create-index"></a>Создание индекса
Индекс является основным средством организации и поиска документов в поиске Azure hello, аналогичные toohow таблицы организует записи в базе данных. Каждый индекс имеет коллекцию документов, которые все соответствуют схеме индекса toohello (имена полей, типы данных и свойства), что индексы также указывают дополнительные конструкции (средства подбора смысловых вариантов, профили повышения и параметры CORS), которые определяют поведение других поиска.

Для создания нового индекса в службе поиска Azure используется HTTP-запрос POST или PUT. текст Hello hello запроса является схемой JSON, указывает hello индекс и сведения о конфигурации.

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Кроме того можно использовать PUT и указать имя индекса hello hello URI. Если индекс hello не существует, он будет создан.

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

Создание индекса определяет структуру hello hello документов сохраняются и используются в операциях поиска. Заполнение индекса hello является отдельной операцией. На этом этапе можно использовать [индексатор](https://msdn.microsoft.com/library/azure/mt183328.aspx) (для поддерживаемых источников данных) либо операции [добавления, обновления и удаления документов](https://msdn.microsoft.com/library/azure/dn798930.aspx). Hello инвертированный индекс создается в том случае, когда для публикации документов hello.

**Примечание**: hello максимальное число может быть индексов зависит от ценового уровня. Hello бесплатная служба позволяет создавать копии too3 индексов. В стандартной версии разрешено использовать до 50 индексов на одну службу поиска. Дополнительные сведения см. в статье с описанием [пределов и ограничений](http://msdn.microsoft.com/library/azure/dn798934.aspx).

**Запрос**

Все запросы к службе отправляются по протоколу HTTPS. Hello **Create Index** можно составить запрос с помощью метода POST или PUT. При использовании POST необходимо указать имя индекса в тексте запроса hello, а также определение схемы индекса hello. С помощью метода PUT имя индекса hello является частью URL-адрес hello. Если индекс hello не существует, он создается. Если он уже существует, это новое определение обновленных toohello.

Имя индекса Hello должен состоять из строчных букв, начинаться с буквы или цифры, иметь нет символы косой черты или точек и быть не длиннее 128 символов. После имени индекса hello начиная с буквы или цифры, hello остальная часть имени hello может включать любой буквы, числа и дефисы, при условии, что hello дефисы не являются последовательными.

Hello `api-version` является обязательным. Список доступных версий см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).

**Заголовки запроса**

Hello следующий список описывает hello необходимые и необязательные заголовки запросов.

* `Content-Type`: обязательный параметр. Установите это слишком`application/json`
* `api-key`: обязательный параметр. Hello `api-key` используется для
* Проверка подлинности службы поиска tooyour hello запроса. Это строковое значение, уникальным tooyour службы. Hello **Create Index** запрос должен включать `api-key` заголовок указать ключ администратора tooyour (как противоположность tooa ключа запроса).

Необходимо также hello имя tooconstruct hello запроса URL-адрес службы. Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello. В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.

<a name="RequestData"></a>
**Синтаксис текста запроса**

текст Hello hello запроса содержит определение схемы, включая hello список полей данных в документах, которые будут переданы в этот индекс, типы данных, атрибутов, а также необязательный список профилей оценки, используемые tooscore соответствующие документы в время запроса.

Обратите внимание, что для запроса POST, необходимо указать имя индекса hello в тексте запроса hello.

Может существовать только одно ключевое поле в индексе hello. Он имеет toobe строкового поля. Это поле представляет уникальный идентификатор каждого документа, хранящегося в индексе hello hello.

Hello основные части индекса включить hello следующие:

* `name`
* `fields` — поля, которые будут передаваться в этот индекс, включая имя, тип данных и свойства, определяющие доступные для каждого поля операции.
* `suggesters` — средства подбора, которые используются для автозавершения и упреждающего ввода запросов.
* `scoringProfiles`— профили оценки, которые используются для настраиваемого ранжирования показателей поиска. Дополнительные сведения см. в статье о [добавлении профилей оценки](https://msdn.microsoft.com/library/azure/dn798928.aspx).
* `analyzers`, `charFilters`, `tokenizers`, `tokenFilters` используется toodefine как документы и запросы разбиваются на токены индексируемые или для поиска. Дополнительные сведения см. в статье, посвященной [анализу в службе поиска Azure](https://aka.ms//azsanalysis).
* `defaultScoringProfile`использовать оценки поведений по умолчанию hello toooverwrite.
* `corsOptions`tooallow запросы независимо от источника к индексу.

Hello синтаксис для структуризации полезных данных запроса hello выглядит следующим образом. Далее в этом разделе приведен пример запроса.

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

**Атрибуты индекса**

Hello следующие атрибуты можно задать при создании индекса. Подробные сведения об оценке и профилях см. в статье о [добавлении профилей оценки](https://msdn.microsoft.com/library/azure/dn798928.aspx).

`name`— Задает hello имя поля hello.

`type`— Задает hello типа данных для поля hello.

`searchable`-Помечает hello поле как средство полнотекстового поиска. Это означает, что во время индексирования оно будет включено в анализ (в частности, для разбиения на слова). Если задать `searchable` tooa значение поля «солнечный день», внутренне будет разделить на отдельные токены hello «солнечный» и «день». В результате эти слова смогут участвовать в полнотекстовом поиске. У полей типа `Edm.String` и `Collection(Edm.String)` по умолчанию установлен флаг `searchable`. Для полей других типов установить атрибут `searchable`нельзя.

* **Примечание**: `searchable` поля потребляют дополнительное пространство в индексе, так как поиск Azure будет хранить дополнительную помеченную токенами версию значения поля hello для полнотекстового поиска. Если вы хотите toosave модуль индекс и вы не нужен toobe поля, включенные в поиск, задайте `searchable` слишком`false`.

`filterable`-Позволяет toobe hello поля, на которые ссылается `$filter` запросов. `filterable` отличается от `searchable` тем, как обрабатываются строки. Для полей типа `Edm.String` и `Collection(Edm.String)` с атрибутом `filterable` не выполняется разбиение на слова, поэтому они могут попасть в результаты поиска только по точному совпадению. Например, если задать такому полю `f` слишком «солнечный день» `$filter=f eq 'sunny'` не найдет совпадений, но `$filter=f eq 'sunny day'` будет. По умолчанию атрибут `filterable` устанавливается для всех полей.

`sortable`-По умолчанию hello система упорядочивает результаты по оценкам, но во многих случаях пользователям требуется, чтобы toosort по полям в документах hello. Для полей типа `Collection(Edm.String)` установить атрибут `sortable` нельзя. Для всех остальных полей флаг `sortable` устанавливается по умолчанию.

`facetable` — как правило, используется для представления результатов поиска, в которых указывается количество найденных документов по категориям (например, при поиске цифровых фотоаппаратов можно разделить результаты по производителям, количеству мегапикселей, цене и т. п.). Этот параметр не предназначен для использования с полями типа `Edm.GeographyPoint`. Для всех остальных полей флаг `facetable` устанавливается по умолчанию.

* **Примечание**. Поля типа `Edm.String`, для которых задан атрибут `filterable`, `sortable` или `facetable`, должны иметь длину не больше 32 КБ. Это потому, что такие поля считаются одним условием поиска и hello Максимальная длина условия в поиске Azure составляет 32 КБ. Если вам требуется toostore больше текста, чем в однострочном поле, необходимо будет tooexplicitly задать `filterable`, `sortable`, и `facetable` слишком`false` в определении индекса.
* **Примечание**: Если поля не имеет ни один из hello выше атрибуты значения слишком`true` (`searchable`, `filterable`, `sortable`, или`facetable`) hello поле эффективно исключается из hello инвертированный индекс. Это могут быть поля, которые не используются в запросах, однако нужны в результатах поиска. Исключение подобных полей из hello индекс повышает производительность.

`key`-Метки hello поле как содержащее уникальные идентификаторы для документов в индексе hello. Только одно поле должно быть выбрано в качестве hello `key` поле и он должен иметь тип `Edm.String`. Ключевые поля могут содержать используется toolook документов непосредственно через hello [уточняющего запроса API](#LookupAPI).

`retrievable`— Задает ли hello поля могут быть возвращены в результате поиска.  Это полезно, когда необходимо toouse поля (например, поле) в качестве фильтра, сортировки или оценки механизм, но hello поле toobe toohello видимым для конечного пользователя не требуется. У полей с установленным свойством `true` for `key` .

`analyzer`-Задает имя анализатора toouse hello для поля hello hello во время поиска и индексирования. Привет, допустимые значения см. [анализаторы](https://msdn.microsoft.com/library/mt605304.aspx). Этот параметр можно использовать только с полями `searchable`, а с `searchAnalyzer` или `indexAnalyzer` его установить нельзя.  После выбора анализатора hello, он не может изменяться для поля hello.

`searchAnalyzer`— Задает hello имя анализатора hello, используемые во время поиска для поля hello. Привет, допустимые значения см. [анализаторы](https://msdn.microsoft.com/library/mt605304.aspx). Этот параметр можно использовать только с полями, для которых задан атрибут `searchable`. Она должна быть задана вместе с `indexAnalyzer` и не могут указываться вместе с hello `analyzer` параметр. Этот анализатор можно обновить на существующее поле.

`indexAnalyzer`— Задает hello имя анализатора hello, используемые во время индексирования для поля hello. Привет, допустимые значения см. [анализаторы](https://msdn.microsoft.com/library/mt605304.aspx). Этот параметр можно использовать только с полями, для которых задан атрибут `searchable`. Она должна быть задана вместе с `searchAnalyzer` и не могут указываться вместе с hello `analyzer` параметр. После выбора анализатора hello, он не может изменяться для поля hello.

`suggesters`— Задает hello режим поиска и полей, которые являются источником hello hello содержимого для предложений. Дополнительные сведения см. в разделе [Средства подбора](#Suggesters).

`scoringProfiles` — позволяет настроить механизм оценки, с помощью которого можно влиять на относительную позицию элементов в результатах поиска. Профили оценки состоят из взвешенных полей и функций. В разделе [Добавление профилей оценки](https://msdn.microsoft.com/library/azure/dn798928.aspx) Дополнительные сведения о hello атрибуты, используемые в профиль оценки.

<!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Поддержка языков**

Поля с поддержкой поиска подвергаются анализу, который чаще всего включает разбиение на слова, нормализацию текста и выделение условий поиска. По умолчанию, доступные для поиска поля в поиске Azure анализируются с hello [стандартного анализатора Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) который разбивает текст на элементы, которые следуют[«Сегментация текста Юникод»](http://unicode.org/reports/tr29/) правила. Кроме того hello стандартный анализатор преобразует все символы tootheir нижний регистр. Индексированных документов и условий поиска проходят hello анализа во время индексирования и обработки запросов.

"Поиск Azure" поддерживает различные языки. Для каждого из них необходим нестандартный анализатор текста, который учитывает особенности соответствующего языка. В службе поиска Azure доступны анализаторы двух типов:

* 35 анализаторов на базе технологии Lucene.
* 50 анализаторов на базе собственной технологии Майкрософт для обработки естественных языков, которая используется в приложениях Office и поисковой системе Bing.

Некоторые разработчики могут использовать знакомую проста, открытая решения для Lucene hello. Анализаторы Lucene работают быстрее, но анализаторы Microsoft hello предусмотрены расширенные возможности, такие как лемматизация, decompounding (на языках, таких как немецкий, датский, голландский, шведский, норвежский, эстонский, Готово, венгерский, словацкий) и распознавание сущности (URL-адреса в word сообщения электронной почты, дат, чисел). Если это возможно следует выполнять сравнение обоих hello Майкрософт и Lucene анализаторы toodecide какая оптимален.

***Сравнение***

Анализатор Lucene Hello английского языка расширяет стандартный анализатор hello. Он удаляет из слов признаки принадлежности (символы 's в конце), находит основу слов с помощью [стеммера Портера](http://tartarus.org/~martin/PorterStemmer/) и удаляет английские [стоп-слова](http://en.wikipedia.org/wiki/Stop_words).

В отличие от этого анализатор Microsoft hello выполняет лемматизация вместо морфологический поиск. Это означает, что он гораздо лучше обрабатывает флективные и неправильные словоформы, а также позволяет получить более подходящие результаты поиска (дополнительные сведения см. в модуле 7 [презентации MVA, посвященной службе поиска Azure](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps)).

Индексирование с Microsoft анализаторы составляет в среднем два раза toothree медленнее, чем их эквиваленты Lucene, в зависимости от языка hello. Время выполнения поискового запроса не должно значительно отличаться от запросов средних размеров.

***Конфигурация***

Для каждого поля в определении индекса hello, можно задать hello `analyzer` имя анализатора tooan свойства, которое указывает, какой язык и поставщика. Здравствуйте, анализатор же будут применены при индексирования и поиска для этого поля.
Например, могут быть отдельные поля для описания гостиницы английском, французском и испанском языке, существующие рядом в hello же индекс. Используйте hello [параметр запроса «searchFields»](#SearchQueryParameters) toospecify toosearch какие поля конкретного языка с в запросах. Можно просмотреть примеры запросов, которые включают hello `analyzer` свойство в [поиск документов](#SearchDocs). 

***Список анализаторов***

Ниже приведен список поддерживаемых языков, а также имена анализатор Lucene и Microsoft hello.

<table style="font-size:12">
    <tr>
        <th>Язык</th>
        <th>Название анализатора Майкрософт</th>
        <th>Название анализатора Lucene</th>
    </tr>
    <tr>
        <td>Арабский</td>
        <td>ar.microsoft</td>
        <td>ar.lucene</td>        
    </tr>
    <tr>
        <td>Армянский</td>
        <td></td>
        <td>hy.lucene</td>
      </tr>
    <tr>
        <td>Бенгальский</td>
        <td>bn.microsoft</td>
        <td></td>
    </tr>
      <tr>
        <td>Баскский</td>
        <td></td>
        <td>eu.lucene</td>
    </tr>
      <tr>
         <td>Болгарский</td>
        <td>bg.microsoft</td>
        <td>bg.lucene</td>
      </tr>
      <tr>
        <td>Каталанский</td>
        <td>ca.microsoft</td>
        <td>ca.lucene</td>          
      </tr>
    <tr>
        <td>Китайский (упрощенное письмо)</td>
        <td>zh-Hans.microsoft</td>
        <td>zh-Hans.lucene</td>        
    </tr>
    <tr>
        <td>Китайский (традиционное письмо)</td>
        <td>zh-Hant.microsoft</td>
        <td>zh-Hant.lucene</td>        
    <tr>
    <tr>
        <td>Хорватский</td>
        <td>hr.microsoft</td>
        <td/></td>
    </tr>
    <tr>
        <td>Чешский</td>
        <td>cs.microsoft</td>
        <td>cs.lucene</td>        
    </tr>    
    <tr>
        <td>Датский</td>
        <td>da.microsoft</td>
        <td>da.lucene</td>        
    </tr>    
    <tr>
        <td>Нидерландский</td>
        <td>nl.microsoft</td>
        <td>nl.lucene</td>    
    </tr>    
    <tr>
        <td>Английский</td>        
        <td>en.microsoft</td>
        <td>en.lucene</td>        
    </tr>
    <tr>
        <td>Эстонский</td>
        <td>et.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Финский</td>
        <td>fi.microsoft</td>
        <td>fi.lucene</td>        
    </tr>    
    <tr>
        <td>Французский</td>
        <td>fr.microsoft</td>
        <td>fr.lucene</td>        
    </tr>
    <tr>
        <td>Галисийский</td>
        <td></td>
        <td>gl.lucene</td>        
      </tr>
    <tr>
        <td>Немецкий</td>
        <td>de.microsoft</td>
        <td>de.lucene</td>        
    </tr>
    <tr>
        <td>Греческий</td>
        <td>el.microsoft</td>
        <td>el.lucene</td>        
    </tr>
    <tr>
        <td>Гуджарати</td>
        <td>gu.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Иврит</td>
        <td>he.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Хинди</td>
        <td>hi.microsoft</td>
        <td>hi.lucene</td>        
    </tr>
    <tr>
        <td>Венгерский</td>        
        <td>hu.microsoft</td>
        <td>hu.lucene</td>
    </tr>
    <tr>
        <td>Исландский</td>
        <td>is.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Индонезийский (бахаса)</td>
        <td>id.microsoft</td>
        <td>id.lucene</td>        
    </tr>
    <tr>
        <td>Ирландский</td>
        <td></td>
          <td>ga.lucene</td>
    </tr>
    <tr>
        <td>Итальянский</td>
        <td>it.microsoft</td>
        <td>it.lucene</td>        
    </tr>
    <tr>
        <td>Японский</td>
        <td>ja.microsoft</td>
        <td>ja.lucene</td>

    </tr>
    <tr>
        <td>Каннада</td>
        <td>ka.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Корейский</td>
        <td>ko.microsoft</td>
        <td>ko.lucene</td>
    </tr>
    <tr>
        <td>Латышский</td>        
        <td>lv.microsoft</td>
        <td>lv.lucene</td>    
    </tr>
    <tr>
        <td>Литовский</td>
        <td>lt.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Малаялам</td>
        <td>ml.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Малайский (латиница)</td>
        <td>ms.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Маратхи</td>
        <td>mr.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Норвежский</td>
        <td>nb.microsoft</td>
        <td>no.lucene</td>        
    </tr>
      <tr>
        <td>Персидский</td>
        <td></td>
        <td>fa.lucene</td>        
      </tr>
    <tr>
        <td>Польский</td>
        <td>pl.microsoft</td>
        <td>pl.lucene</td>        
    </tr>
    <tr>
        <td>Португальский (Бразилия)</td>
        <td>pt-Br.microsoft</td>
        <td>pt-Br.lucene</td>        
    </tr>
    <tr>
        <td>Португальский (Португалия)</td>
        <td>pt-Pt.microsoft</td>        
        <td>pt-Pt.lucene</td>
    </tr>
    <tr>
        <td>Панджаби</td>
        <td>pa.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Румынский</td>
        <td>ro.microsoft</td>
        <td>ro.lucene</td>
    </tr>
    <tr>
        <td>Русский</td>
        <td>ru.microsoft</td>
        <td>ru.lucene</td>    
    </tr>
    <tr>
        <td>Сербский (кириллица)</td>
        <td>sr-cyrillic.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Сербский (латиница)</td>
        <td>sr-latin.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Словацкий</td>
        <td>sk.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Словенский</td>
        <td>sl.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Испанский</td>
        <td>es.microsoft</td>
        <td>es.lucene</td>
    </tr>
    <tr>
        <td>Шведский</td>
        <td>sv.microsoft</td>
        <td>sv.lucene</td>
    </tr>

    <tr>
        <td>Тамильский</td>
        <td>ta.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Телугу</td>
        <td>te.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Тайский</td>
        <td>th.microsoft</td>
        <td>th.lucene</td>
    </tr>
    <tr>
        <td>Турецкий</td>
        <td>tr.microsoft</td>
        <td>tr.lucene</td>        
    </tr>
    <tr>
        <td>Украинский</td>
        <td>uk.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Урду</td>
        <td>ur.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Вьетнамский</td>
        <td>vi.microsoft</td>
        <td></td>
    </tr>
    <td colspan="3">Кроме того, в службе поиска Azure доступны независимые от языка конфигурации анализаторов.</td>
    <tr>
        <td>Стандартное приведение к ASCII</td>
        <td>standardasciifolding.lucene</td>
        <td>
        <ul>
            <li>Сегментация текста Юникода (стандартный лексический анализатор)</li>
            <li>Фильтр свертки ASCII - преобразует символы Юникода, не принадлежащих toohello набор первых 127 символов ASCII в их эквиваленты ASCII. Эта функция полезна для удаления диакритических знаков.</li>
        </ul>
        </td>
    </tr>
</table>

Все анализаторы, у которых в названии есть идентификатор <i>lucene</i>, работают на базе [языковых анализаторов Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html). Можно найти дополнительные сведения о фильтре свертки ASCII hello [здесь](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).

**Средства подбора**

Объект `suggester` определяет поля в индексе, используемые toosupport автозавершения в поиске. Обычно отправляются частичные строки поиска toohello [API предложений](#Suggestions) hello пользователь вводит запрос поиска, а hello API возвращает набор предлагаемых фраз. Средства подбора смысловых вариантов, определяемый в индексе hello определяет поля, используемые toobuild hello упреждающих условий. Информацию о настройке см. в разделе [Средства подбора](#Suggesters).

**Профили оценки**

Объект `scoringProfile` определяет пользовательские оценки поведений, которые позволяют влиять на элементы, отображаемые выше в результатах поиска hello. Профили оценки состоят из взвешенных полей и функций. toouse их, необходимо задать профиль по имени в строке запроса hello.

Профиль повышения по умолчанию работает за toocompute сцены hello Оценка поиска для каждого элемента в результирующем наборе. Можно использовать профиль hello имени, внутренней оценки. Можно также задать `defaultScoringProfile` toouse пользовательского профиля по умолчанию hello, вызывается всякий раз, когда пользовательский профиль не указан в строке запроса hello.

В разделе [оценки добавить профили tooa индекса поиска (API REST службы поиска Azure)](search-api-scoring-profiles-2015-02-28-preview.md) подробные сведения.

**Параметры CORS**

Невозможно вызвать интерфейсы API по умолчанию Javascript на стороне клиента, поскольку hello браузер будет предотвращать все запросы независимо от источника. Включить CORS (доступ к ресурсам независимо от источника), установка hello `corsOptions` атрибута tooallow запросы независимо от источника tooyour индекса. Обратите внимание на то, что по соображениям безопасности технологию CORS поддерживают только интерфейсы API запросов. для CORS можно задать следующие параметры Hello.

* `allowedOrigins`(обязательно): это список источников, которым будет предоставлен доступ tooyour индекса. Это означает, что никакой код Javascript, запущенному из этих источников, будет разрешено tooquery индексе (при условии, что указан правильный ключ API hello). Каждый источник обычно имеет форму hello `protocol://fully-qualified-domain-name:port` несмотря на то, что порт hello часто опускается. Дополнительные сведения см. в [этой статье](http://go.microsoft.com/fwlink/?LinkId=330822).
  * Источники tooall tooallow доступа, включить `*` как один элемент hello `allowedOrigins` массива. Напоминаем вам, что **так не рекомендуется делать в рабочих версиях служб поиска**. Однако это может оказаться полезно для целей разработки или отладки.
* `maxAgeInSeconds`(необязательно): браузеры используют это значение toodetermine hello продолжительность (в секундах) toocache предварительных ответов CORS. Это значение должно быть целой неотрицательной величиной. Hello увеличить это значение задано, будет hello более высокую производительность, но hello больше времени, необходимое для эффекта tootake изменений политики CORS. Если это значение не задано, длительность по умолчанию составляет 5 минут.

<a name="CreateUpdateIndexExample"></a>
**Пример тела запроса**

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

**Ответ**

Для успешного запроса: "201 — Создан ресурс".

По умолчанию hello текст ответа будет содержать hello JSON для определения индекса hello, который был создан. Если hello `Prefer` заголовок запроса имеет слишком`return=minimal`, hello текст ответа будет пустым, и код состояния успеха hello будет «204 Нет содержимого» вместо «201 Создано». Это верно независимо от того, было ли PUT или POST используется toocreate hello индекса.

**Примечания**

В настоящее время функции обновления схемы индекса поддерживаются в ограниченном объеме. Обновления схемы, которые требуют переиндексирования (например, изменение типов полей), пока не поддерживаются. Несмотря на то, что существующие поля нельзя изменить или удалить, новые поля добавляются tooan существующего индекса в любое время. При добавлении нового поля все существующие документы в индексе hello автоматически будет иметь значение null для этого поля. Нет дополнительное пространство для хранения будут использоваться, пока новые документы добавляются toohello индекса.

<a name="Suggesters"></a>

## <a name="suggesters"></a>Средства подбора
функция предложений Hello в поиске Azure — это возможность упреждающего ввода или автозавершения запроса, предоставляя список потенциальных условий поиска в ответ toopartial строку входных данных, введенных в поле поиска. Вы, наверняка, замечали предложения запроса при использовании коммерческих поисковых систем в Интернете. Например, если ввести в Bing ".NET", появится список условий для .NET 4.5, .NET Framework 3.5 и т. д. При использовании REST API службы поиска hello, реализация вариантов поиска в настраиваемом приложении поиск Azure требует hello следующее:

* Включите варианты поиска, добавив **средства подбора** конструкция в индекс, задайте имя hello, режим поиска и список полей, для которого упреждающих вызывается. Например если указать «cityName» как поле источника, ввод частичной строки поиска «SEA» приведет к «Seattle», «Seaside» и «Seatac» (все три являются названиями реальных городов) доступно как пользователь toohello предложения запроса.
* Вызовите варианты поиска, вызывающему Привет [API предложений](#Suggestions) в коде приложения. Обычно частичные строки поиска отправляются службе toohello hello пользователь вводит запрос поиска, а этот API возвращает набор предлагаемых фраз.

В этой статье объясняется, как tooconfigure **средства подбора**. Следует также просмотреть hello [API предложений](#Suggestions) подробные сведения об использовании средства подбора.

**Использование**

`Suggesters`создаются в индексе hello и лучше всего работают при использовании определенного toosuggest документах по объектной модели, а не свободных терминов или фраз. названия, имена и другие относительно небольшие фразы, которые могут определить элемент Hello наиболее кандидата поля: Менее эффективно выполняется поиск по таким полям с множеством повторяющихся элементов, как категории и теги, а также по очень длинным полям, таким как описания и комментарии.

Как часть определения индекса hello, можно добавить toohello одного средства подбора `suggesters` коллекции. Свойства, определяющие средства подбора включить hello следующие:

* `name`: имя средства подбора hello hello. Используйте имя средства подбора hello hello при вызове hello `suggest` API.
* `searchMode`: hello toosearch стратегия, используемая фраз кандидатов. Hello в настоящее время поддерживается только режим является `analyzingInfixMatching`, который выполняет гибкое сопоставление фраз в начале hello, или в середине предложений hello.
* `sourceFields`: Список из одного или нескольких полей, которые являются источником hello hello содержимого для предложений. Источниками могут быть только поля типов `Edm.String` и `Collection(Edm.String)`. Можно использовать только поля, для которых не задан настраиваемый языковой анализатор.

**Пример средства подбора**

Средства подбора является частью индекса hello. Может существовать только один средства подбора в hello `suggesters` коллекции поля коллекции в текущей версии hello, наряду с hello и `scoringProfiles`.

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> При использовании общедоступной предварительной версии поиска Azure hello `suggesters` заменяет более старое логическое свойство (`"suggestions": false`), которое поддерживало только предложения префиксов для коротких строк (3 – 25 символов). Его замены `suggesters`, поддерживают инфиксные сопоставления, которые находят совпадающие термины в начале hello, или в середине содержимого поля hello счет улучшенного допуска на ошибки в строках поиска. Начиная с выпуска общедоступной hello, теперь это единственная реализация API предложений hello hello. старые Hello `suggestions` свойства, которая была введена в `api-version=2014-07-31-Preview` продолжается toowork в этой версии, но не работает в hello `2015-02-28` или более поздней версии службы поиска Azure.
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a>Обновление индекса
Обновить существующий индекс в службе поиска Azure можно с помощью HTTP-запроса PUT. Обновления включают добавление новых полей toohello существующей схеме, изменение параметров CORS и изменение профилей оценки. Дополнительную информацию см. в статье о [добавлении профилей оценки](https://msdn.microsoft.com/library/azure/dn798928.aspx). Необходимо указать имя hello tooupdate индекс hello hello URI запроса:

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Важно:** поддержка обновлений схемы индекса является ограниченной toooperations, не требующими перестроения индекса поиска hello. Обновления схемы, которые требуют переиндексирования (например, изменение типов полей), пока не поддерживаются. Новые поля можно добавлять в любой момент, однако изменять и удалять существующие поля пока нельзя. Hello применимо и к слишком`suggesters`. Новые поля, которые могут быть добавлены средства подбора tooa в поля hello hello времени будут добавлены, но нельзя удалить поля из `suggesters` и существующие поля нельзя добавлять слишком`suggesters`.

При добавлении нового индекса tooan поля, все существующие документы в индексе hello автоматически будут иметь значение null для этого поля. Нет дополнительное пространство для хранения будут использоваться, пока новые документы добавляются toohello индекса.

**Запрос**

Все запросы к службе отправляются по протоколу HTTPS. Hello **обновление индекса** запроса создается с помощью HTTP PUT. С помощью метода PUT имя индекса hello является частью URL-адрес hello. Если индекс hello не существует, он создается. Если hello индекс уже существует, это новое определение обновленных toohello.

Имя индекса Hello должен состоять из строчных букв, начинаться с буквы или цифры, иметь нет символы косой черты или точек и быть не длиннее 128 символов. После имени индекса hello начиная с буквы или цифры, hello остальная часть имени hello может включать любой буквы, числа и дефисы, при условии, что hello дефисы не являются последовательными.

`api-version=[string]` (обязательный). Hello предварительной версии — `api-version=2015-02-28-Preview`. Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).

**Заголовки запроса**

Hello следующий список описывает hello необходимые и необязательные заголовки запросов.

* `Content-Type`: обязательный параметр. Установите это слишком`application/json`
* `api-key`: обязательный параметр. Hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска. Это строковое значение, уникальным tooyour службы. Hello **обновление индекса** запрос должен включать `api-key` заголовок указать ключ администратора tooyour (как противоположность tooa ключа запроса).

Необходимо также hello имя tooconstruct hello запроса URL-адрес службы. Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello. В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.

**Синтаксис тела запроса**

При обновлении существующего индекса, текст hello должен содержать исходное определение схемы hello, а также hello новые поля, которые вы добавляете, а также hello изменения профилей оценки, средств подбора и параметры CORS, если таковые имеются. Если профили повышения hello и параметры CORS не изменяются, необходимо включить оригиналов hello из при создании индекса hello. В целом hello наиболее toouse шаблон для обновлений является определение индекса hello tooretrieve с помощью метода GET, измените его, а затем обновить его с помощью метода PUT.

синтаксис схемы Hello использовать toocreate, индекса воспроизводится здесь для удобства. Дополнительные сведения см. в разделе [Создание индекса](#CreateIndex).

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


**Ответ**

Для успешного запроса: "204 — Нет содержимого".

По умолчанию hello текст ответа будет пустым. Тем не менее, если hello `Prefer` задан заголовок запроса слишком`return=representation`, hello текст ответа будет содержать hello JSON для определения индекса hello, который был обновлен. В этом случае будет hello код состояния успеха «200 OK».

**Обновление определения индекса с пользовательскими анализаторами**

После определения анализатора, создателя маркеров, фильтра маркеров или фильтра знаков его нельзя изменить. Новые шаблоны можно добавить существующий индекс tooan только в случае hello `allowIndexDowntime` tootrue установлен флаг в запрос обновления индекса hello: 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

Обратите внимание, что эта операция будет помещена индекса в автономном режиме по крайней мере несколько секунд, вызывая вашей индексирования и запросов запрашивает toofail. Производительность и записи доступности hello индекса может быть несколько минут после обновления индекса hello с ослабленным зрением или больше времени для очень больших индексов.

<a name="ListIndexes"></a>

## <a name="list-indexes"></a>Получение списка индексов
Hello **список индексов** возвращает список индексов hello в данный момент в службе поиска Azure.

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

**Запрос**

Все запросы к службе отправляются по протоколу HTTPS. Hello **список индексов** запрос может быть создан с помощью метода GET hello.

`api-version=[string]` (обязательный). Hello предварительной версии — `api-version=2015-02-28-Preview`. Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).

**Заголовки запроса**

Hello следующий список описывает hello необходимые и необязательные заголовки запросов.

* `api-key`: обязательный параметр. Hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска. Это строковое значение, уникальным tooyour службы. Hello **список индексов** запрос должен включать `api-key` ключ администратора tooan набор (как противоположность tooa ключа запроса).

Необходимо также hello имя tooconstruct hello запроса URL-адрес службы. Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello. В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.

**Тело запроса**

Отсутствует.

**Ответ**

Код состояния: в качестве успешного ответа возвращается код "200 — ОК".

Вот пример тела запроса:

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

Обратите внимание, что можно отфильтровать ответ hello вниз toojust hello свойства, которые вас интересуют. Например, если требуется только список имен индексов используйте hello OData `$select` параметра запроса:

    GET /indexes?api-version=2015-02-28-Preview&$select=name

В этом случае ответ hello hello в приведенном выше примере будет выглядеть следующим образом:

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

Это удобно toosave пропускной способности, если у вас много индексов в службе поиска.

<a name="GetIndex"></a>

## <a name="get-index"></a>Получение индекса
Hello **получить индекс** операция получает hello определение индекса из поиска Azure.

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**Запрос**

Запросы к службе отправляются по протоколу HTTPS. Hello **получить индекс** запрос может быть создан с помощью метода GET hello.

Hello [имя индекса] в URI запроса hello указывает, какой индекс tooreturn из коллекции индексов hello.

`api-version=[string]` (обязательный). Hello предварительной версии — `api-version=2015-02-28-Preview`. Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).

**Заголовки запроса**

Hello следующий список описывает hello необходимые и необязательные заголовки запросов.

* `api-key`: hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска. Это строковое значение, уникальным tooyour службы. Hello **получить индекс** запрос должен включать `api-key` ключ администратора tooan набор (как противоположность tooa ключа запроса).

Необходимо также hello имя tooconstruct hello запроса URL-адрес службы. Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello. В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.

**Тело запроса**

Отсутствует.

**Ответ**

Код состояния: в качестве успешного ответа возвращается код "200 — ОК".

См. пример hello JSON в [создания и обновления индекса](#CreateUpdateIndexExample) пример hello полезные данные ответа.

<a name="DeleteIndex"></a>

## <a name="delete-index"></a>Удаление индекса
Hello **удалить индекс** операция удаляет индекс и связанные документы из службы поиска Azure. Имя индекса hello можно получить из панели мониторинга службы hello в hello портал Azure или hello API. Более подробные сведения см. в разделе [Получение списка индексов](#ListIndexes).

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**Запрос**

Запросы к службе отправляются по протоколу HTTPS. Hello **удалить индекс** запрос может быть создан с помощью метода DELETE hello.

Hello [имя индекса] в URI запроса hello указывает, какой индекс toodelete из коллекции индексов hello.

`api-version=[string]` (обязательный). Hello предварительной версии — `api-version=2015-02-28-Preview`. Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).

**Заголовки запроса**

Hello следующий список описывает hello необходимые и необязательные заголовки запросов.

* `api-key`: обязательный параметр. Hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска. Это строковое значение, URL-адрес службы уникальный tooyour. Hello **удалить индекс** запрос должен включать `api-key` заголовок указать ключ администратора tooyour (как противоположность tooa ключа запроса).

Необходимо также hello имя tooconstruct hello запроса URL-адрес службы. Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello. В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.

**Тело запроса**

Отсутствует.

**Ответ**

Код состояния: в качестве успешного ответа возвращается код "204 — Нет содержимого".

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a>Получение статистических данных индекса
Hello **получить статистику индекса** операция возвращает из поиска Azure количество документов для hello текущий индекс, а также об использовании хранилища.

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> Статистика по количеству документов и размеру хранилища собирается каждые несколько минут, а не в режиме реального времени. Таким образом этот API возвращает статистику hello может не отражать изменения, вызванные последней операции индексирования.
> 
> 

**Запрос**

Все запросы к службе отправляются по протоколу HTTPS. Hello **получить статистику индекса** запрос может быть создан с помощью метода GET hello.

Hello [имя индекса] в URI запроса hello указывает hello службы tooreturn для статистики индекса hello указанному индексу.

`api-version=[string]` (обязательный). Hello предварительной версии — `api-version=2015-02-28-Preview`. Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).

**Заголовки запроса**

Hello следующий список описывает hello необходимые и необязательные заголовки запросов.

* `api-key`: hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска. Это строковое значение, уникальным tooyour службы. Hello **получить статистику индекса** запрос должен включать `api-key` ключ администратора tooan набор (как противоположность tooa ключа запроса).

Необходимо также hello имя tooconstruct hello запроса URL-адрес службы. Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello. В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.

**Тело запроса**

Отсутствует.

**Ответ**

Код состояния: в качестве успешного ответа возвращается код "200 — ОК".

текст ответа Hello имеет hello следующий формат:

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a>Анализатор теста
Hello **анализ API** показано, как анализатор разбивает текст на лексемы.

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Запрос**

Все запросы к службе отправляются по протоколу HTTPS. Hello **анализ API** запрос может быть создан с помощью метода POST hello.

`api-version=[string]` (обязательный). Hello предварительной версии — `api-version=2015-02-28-Preview`. Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).

**Заголовки запроса**

Hello следующий список описывает hello необходимые и необязательные заголовки запросов.

* `api-key`: hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска. Это строковое значение, уникальным tooyour службы. Hello **анализ API** запрос должен включать `api-key` ключ администратора tooan набор (как противоположность tooa ключа запроса).

Также потребуется имя индекса hello и hello имя tooconstruct hello запроса URL-адрес службы. Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello. В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.

**Тело запроса**

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

или

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

Hello `analyzer_name`, `tokenizer_name`, `token_filter_name` и `char_filter_name` необходимых toobe допустимые имена встроенные или настраиваемые анализаторы, анализаторы, маркеров фильтры и фильтры char для индекса hello. toolearn дополнительных сведений о процессе hello лексической анализа в разделе [анализа в поиске Azure](https://aka.ms/azsanalysis).

**Ответ**

Код состояния: в качестве успешного ответа возвращается код "200 — ОК".

текст ответа Hello имеет hello следующий формат:

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of hello first character of hello token),
          "endOffset": number (index of hello last character of hello token),
          "position": number (position of hello token in hello input text)
        },
        ...
      ]
    }

**Пример для API анализа**

**Запрос**

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

**Ответ**

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a>Операции с документами
В поиске Azure индекс хранится в облаке hello и заполняется с помощью документов JSON, передаче toohello службы. Все отправленные документы hello составляют hello совокупность данных поиска. Документы содержат поля, некоторые из которых разбиваются на условия поиска при добавлении. Hello `/docs` сегмент URL-адреса в hello API поиска Azure представляет коллекцию hello документов в индексе. Все операции, выполняемые на hello коллекции, например отправка, объединение, удаление или запроса документов, выполняются в контексте отдельного индекса, поэтому URL-адреса hello hello для этих операций всегда начинаются с `/indexes/[index name]/docs` для имени данного индекса.

Код приложения должен либо создать tooAzure tooupload документы JSON поиска, либо можно использовать [индексатора](https://msdn.microsoft.com/library/dn946891.aspx) tooload документов, если источник данных hello базы данных SQL Azure или Azure Cosmos DB. Как правило, индексы заполняются из одного указанного набора данных.

Необходимо запланировать наличие одного документа для каждого элемента, которое следует toosearch. В приложении для видеопроката можно создать по одному документу для каждого фильма, в приложении для интернет-магазина — по документу для каждого номера SKU, в приложении для электронного обучения — по одному документу для каждого курса, в фирме, которая занимается научными исследованиями, — по документу для каждой научной работы из архива и т. д.

Документы состоят из одного или нескольких полей. Поля могут содержать текст, который разбит службой поиска Azure на условия поиска, а также неразбитые и нетекстовые значения, которые можно использовать в фильтрах и профилях оценки. Hello имена, типы данных и функции поиска, поддерживаемые для каждого поля определяются hello схемы индекса. Одно из полей hello в каждой схеме индекса необходимо назначить в качестве идентификатора, и каждый документ должен иметь значение для поля идентификатора hello, однозначно определяющее этот документ в индексе hello. Все прочие поля документа являются необязательными и будут по умолчанию tooa значение null, если не указано иное. Обратите внимание, что значения null не занимают места в индекс поиска hello.

Перед отправкой документов необходимо hello индекса, уже созданные в службе hello. Подробные сведения о выполнении этого первого этапа см. в разделе [Создание индекса](#CreateIndex).

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a>Добавления, обновления и удаления документов
Для добавления, объединения, объединения/добавления и удаления документов в определенном индексе используются HTTP-запросы POST. Для большого количества обновлений рекомендуется использовать пакетную обработку документов (too1000 документов на пакет) или около 16 МБ в пакете.

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Запрос**

Все запросы к службе отправляются по протоколу HTTPS. Для добавления, объединения, объединения/добавления и удаления документов в определенном индексе используются HTTP-запросы POST.

Hello URI запроса содержит [имя индекса], указав какие документы toopost индекса. Только вы можете публиковать документы tooone индекса одновременно.

`api-version=[string]` (обязательный). Hello предварительной версии — `api-version=2015-02-28-Preview`. Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).

**Заголовки запроса**

Hello следующий список описывает hello необходимые и необязательные заголовки запросов.

* `Content-Type`: обязательный параметр. Установите это слишком`application/json`
* `api-key`: обязательный параметр. Hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска. Это строковое значение, уникальным tooyour службы. Hello **добавьте документы** запрос должен включать `api-key` заголовок указать ключ администратора tooyour (как противоположность tooa ключа запроса).

Необходимо также hello имя tooconstruct hello запроса URL-адрес службы. Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello. В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.

**Тело запроса**

Hello тексте hello запроса содержит один или несколько документов toobe индексированных. Документы идентифицируются уникальным ключом. С каждым документом связывается действие: добавить, объединить, объединить или добавить либо удалить. Отправка запросов должен включать данные документа hello как набор пар «ключ значение».

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> Ключи документа могут содержать только буквы, цифры, дефисы ("–"), знак подчеркивания ("_") и знак равенства ("="). Дополнительные сведения см. в разделе [Правила именования](https://msdn.microsoft.com/library/azure/dn857353.aspx).
> 
> 

**Действия с документами**

* `upload`: Действие отправки — примерно tooan «вставки-обновления» где документ hello будет вставлена, если является новым и обновлен или заменен, если он существует. Обратите внимание, что в случае обновления hello заменяются все поля.
* `merge`: Обновления слияния, существующий документ с hello указаны поля. Если документ hello не существует, объединение hello завершится ошибкой. Любое поле, указанное для объединения приведет к замене существующего поля hello в документе hello. Это относится и к полям типа `Collection(Edm.String)`. Например, если hello документ содержит поле «теги» со значением `["budget"]` , и вы выполните объединение со значением `["economy", "pool"]` для «теги» hello окончательное значение поля hello «теги» будет `["economy", "pool"]`. а **не** `["budget", "economy", "pool"]`.
* `mergeOrUpload`: ведет себя как `merge` Если документ с hello заданным ключом уже существует в индексе hello. Если существует документ hello ведет себя как `upload` с новым документом.
* `delete`: Удалить удаляет hello указанный документ из индекса hello. Обратите внимание, что все поля, укажите в `delete` операции, отличной от hello ключевое поле будет игнорироваться. Tooremove отдельного поля из документа, используйте `merge` вместо и просто задать поле hello явным образом слишком`null`.

**Ответ**

Код состояния: при успешном выполнении возвращается код "200 — ОК", указывающий на то, что все элементы проиндексированы. Это обозначается hello `status` свойство tootrue для всех элементов, а также hello `statusCode` свойство tooeither 201 (для загруженных документов) или 200 (для слияния или удаления документов):

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

Код состояния 207 (множественное состояние) возвращается, если хотя бы один элемент не удалось проиндексировать. Элементы, которые не были проиндексированы имеют hello `status` toofalse набор полей. Hello `errorMessage` и `statusCode` свойства указывают, hello причину ошибки индексирования hello:

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "hello search service is too busy tooprocess this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

Hello в следующей таблице описывается hello различных на уровне документа коды состояния, которые могут быть возвращены в ответе hello. Обратите внимание, что некоторые указывают на проблемы hello запроса, пока другие описания временных ошибок. последний Hello следует повторить через некоторое время.

<table style="font-size:12">
    <tr>
        <th>Код состояния</th>
        <th>Значение</th>
        <th>Возможность повторной попытки</th>
        <th>Примечания</th>
    </tr>
    <tr>
        <td>200</td>
        <td>Документ был успешно изменен или удален.</td>
        <td>Недоступно</td>
        <td>Операции удаления являются <a href="https://en.wikipedia.org/wiki/Idempotence">идемпотентными</a>. То есть даже если ключ документа не существует в индексе hello, попытка операции удаления с этим ключом приведет к код состояния 200.</td>
    </tr>
    <tr>
        <td>201</td>
        <td>Документ создан.</td>
        <td>Недоступно</td>
        <td></td>
    </tr>
    <tr>
        <td>400</td>
        <td>Ошибка в документе hello, препятствующая индексируется.</td>
        <td>Нет</td>
        <td>Hello в ответ hello появится сообщение об неверные hello документа.</td>
    </tr>
    <tr>
        <td>404</td>
        <td>не удалось объединить документ Hello hello ключ не существует в индексе hello.</td>
        <td>Нет</td>
        <td>Эта ошибка не возникает при передаче файлов, так как в этом случае создаются новые документы. Не возникает она и при удалении, так как такие операции являются <a href="https://en.wikipedia.org/wiki/Idempotence">идемпотентными</a>.</td>
    </tr>
    <tr>
        <td>409</td>
        <td>Конфликт версий была обнаружена при попытке tooindex документа.</td>
        <td>Да</td>
        <td>Это может произойти, если вы пытаетесь hello tooindex же документов на более чем один раз одновременно.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>Индекс Hello временно недоступен, так как он был обновлен с too'true набор флаг allowIndexDowntime «hello» ".</td>
        <td>Да</td>
        <td></td>
    </tr>
    <tr>
        <td>503</td>
        <td>Службе поиска временно недоступна, возможно, из-за tooheavy нагрузки.</td>
        <td>Да</td>
        <td>Код должен ожидания перед повтором попытки в данном случае или существует риск недоступности службы hello продление срока.</td>
    </tr>
</table> 

**Примечание**: Если код клиента часто сталкивается 207 ответа, одна из возможных причин является hello системы под нагрузкой. Это можно проверить, проверив hello `statusCode` свойство 503. Если это так hello, мы рекомендуем ***регулирование запросов индексирования***. В противном случае если трафик индексирования не уменьшится, hello системы может начать отклонять все запросы с ошибкой "503".

Код состояния 429 указывает, что вы превысили квоту на число hello документов в индекс. В этом случае нужно создать новый индекс или повысить предельную емкость.

**Пример**

    {
      "value": [
        {
          "@search.action": "upload",
          "hotelId": "1",
          "baseRate": 199.0,
          "description": "Best hotel in town",
          "description_fr": "Meilleur hôtel en ville",
          "hotelName": "Fancy Stay",
          "category": "Luxury",
          "tags": ["pool", "view", "wifi", "concierge"],
          "parkingIncluded": false,
          "smokingAllowed": false,
          "lastRenovationDate": "2010-06-27T00:00:00Z",
          "rating": 5,
          "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
          "@search.action": "upload",
          "hotelId": "2",
          "baseRate": 79.99,
          "description": "Cheapest hotel in town",
          "description_fr": "Hôtel le moins cher en ville",
          "hotelName": "Roach Motel",
          "category": "Budget",
          "tags": ["motel", "budget"],
          "parkingIncluded": true,
          "smokingAllowed": true,
          "lastRenovationDate": "1982-04-28T00:00:00Z",
          "rating": 1,
          "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a>Поиск документов
Объект **поиска** операции выдается как запрос GET или POST и указывает параметры, которые предоставляют hello критерии для отбора соответствующих документов.

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**При УЧЕТЕ toouse вместо GET**

При использовании HTTP GET hello toocall **поиска** API-интерфейса, необходимо помнить, что длина URL-адрес запроса hello hello не может превышать 8 КБ toobe. Для большинства приложений этого достаточно. В то же время некоторые приложения создают очень длинные запросы или выражения фильтров OData. Лучший вариант для этих приложений — использование запроса HTTP POST, так как он позволяет увеличить фильтры и запросы по сравнению с GET. С помощью POST, номер hello из выражений или предложения в запросе hello ограничивается коэффициент не hello размер hello необработанных запросов с момента hello предельного размера запроса для POST — приблизительно 16 МБ.

> [!NOTE]
> Несмотря на то, что ограничение на размер запроса POST hello очень велика, поисковые запросы и выражения фильтра не может быть произвольным и довольно сложным. Дополнительные сведения об ограничениях по сложности для запросов и фильтров поиска см. в статьях, посвященных [синтаксису запросов Lucene](https://msdn.microsoft.com/library/mt589323.aspx) и [синтаксису выражений OData](https://msdn.microsoft.com/library/dn798921.aspx).
> 
> 

**Запрос**

Запросы к службе отправляются по протоколу HTTPS. Hello **поиска** можно составить запрос методы с помощью hello GET или POST.

URI запроса Hello указывает, какие tooquery индекса, для всех документов, соответствующих параметрам hello. Параметры указываются в строке запроса hello в случае hello запросов GET, а в запросе hello запрашивает текст в случае, когда hello POST.

Рекомендуется при создании запросов GET, следует помнить слишком[кодирование URL-адрес](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) конкретного запроса, параметров при вызове hello REST API напрямую. Для операций **поиска** в число таких параметров входят:

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

Кодировка URL рекомендуется только для hello выше параметров запроса. Если вы случайно URL-кодировали hello вся строка запроса (все после hello?), запросы будут нарушены.

Кроме того URL-кодирование необходима только при вызове hello получить напрямую с помощью API-интерфейса REST. Кодировка URL-адрес не является обязательным при вызове **поиска** с помощью запроса POST, или при использовании hello [клиентская библиотека .NET](https://msdn.microsoft.com/library/dn951165.aspx), обрабатывающая для кодирования URL-адрес.

<a name="SearchQueryParameters"></a>
**Параметры запроса**

**Поиск** принимает несколько параметров, которые сообщают условия запроса и определяют способы поиска. Укажите эти параметры в URL-АДРЕСЕ hello строку запроса, при вызове **поиска** через GET, а также как свойства JSON в теле запроса hello при вызове **поиска** помощью POST. синтаксис Hello для некоторых параметров немного отличается от GET и POST. Эти различия описаны ниже.

`search=[string]`(необязательно) — текст toosearch для hello. По умолчанию ведется поиск по всем полям с атрибутом `searchable`, если не задан параметр `searchFields`. При поиске `searchable` поля hello поиска сам текст размечается, поэтому несколько условий может отделяться пробелами (например: `search=hello world`). Используйте любой термин toomatch `*` (это может быть полезно для логической фильтрации запросов). Пропуск этого параметра имеет тот же эффект, как и настройка его слишком hello`*`. В разделе [простой синтаксис запроса](https://msdn.microsoft.com/library/dn798920.aspx) конкретные сведения по синтаксису поиска hello.

* **Примечание**: hello результаты могут оказаться сюрпризом при выполнении запросов через `searchable` поля. Hello разметчик содержит логику toohandle случаях общий tooEnglish текст как апострофы, запятые номера, и т. д. Например `search=123,456` будет соответствовать одному термину 123,456, а не hello отдельным терминам 123 и 456, так как запятые используются в качестве разделителя тысяч для больших чисел в английском языке. По этой причине рекомендуется использовать пробелы, а не знаки пунктуации tooseparate термины в hello `search` параметра.

`searchMode=any|all`(необязательно, по умолчанию слишком`any`) — ли любые или все условия поиска hello в документе hello toocount порядок соответствия должны совпадать.

`searchFields=[string]`(необязательно) — список hello toosearch имена полей с разделителями запятыми для hello указанный текст. Для целевых полей должен быть задан атрибут `searchable`.

`queryType=simple|full`(необязательно, по умолчанию слишком`simple`) — Если текста слишком «простой» поиск набора интерпретируется на любом языке простой запрос, позволяющий символы, такие как +, * и «». Запросы вычисляются для всех полей поиска (или полей, указанных в `searchFields`) в каждом документе по умолчанию. Если тип запроса hello задано слишком`full` поиск текста интерпретируется с использованием языка запросов Lucene hello, который позволяет выполнять поиск конкретных полей и Взвешенное. В разделе [простой синтаксис запроса](https://msdn.microsoft.com/library/dn798920.aspx) и [синтаксис запроса Lucene](https://msdn.microsoft.com/library/mt589323.aspx) приведены конкретные сведения о синтаксисов поиска hello. 

> [!NOTE]
> Диапазон поиска в hello Lucene язык запросов не поддерживается в пользу $filter обеспечивающую аналогичные функциональные возможности.
> 
> 

`moreLikeThis=[key]` (необязательный) **Внимание!** Эта функция доступна только в версии `2015-02-28-Preview`. Этот параметр не может использоваться в запросе, который содержит параметр поиска текста hello, `search=[string]`. Hello `moreLikeThis` параметр находит документы, аналогичные toohello документа, указанного в ключе документа hello. При запросе поиска с `moreLikeThis`, список условий поиска создается на основе частоты hello и rarity терминов в исходном документе hello. Эти термины, то используется toomake hello запроса. По умолчанию hello содержимое всех `searchable` поля считаются в том случае, если не `searchFields` — используется toorestrict вестись какие поля.  

`$skip=#`(необязательно) — hello число поиска результатов tooskip; Не может быть больше 100 000. Если требуется tooscan документов в последовательности, но нельзя использовать `$skip` из-за ограничений toothis, рассмотрите возможность использования `$orderby` с полностью упорядоченным ключом и `$filter` с запросом к диапазону вместо.

> [!NOTE]
> При вызове **поиска** с помощью запроса POST этот параметр называется `skip`, а не `$skip`.
> 
> 

`$top=#`(необязательно) — hello число поиска результатов tooretrieve. Это можно использовать в сочетании с `$skip` постраничный просмотр на стороне клиента tooimplement результатов поиска.

> [!NOTE]
> При вызове **поиска** с помощью запроса POST этот параметр называется `top`, а не `$top`.
> 
> 

`$count=true|false`(необязательно, по умолчанию слишком`false`) — указывает, является ли toofetch hello общее количество результатов. Это число hello все документы, которые соответствуют hello `search` и `$filter` параметров, игнорируя `$top` и `$skip`. Установка этого значения слишком`true` может негативно сказаться на производительности. Обратите внимание, что возврат сведений о количестве hello является приближением.

> [!NOTE]
> При вызове **поиска** с помощью запроса POST этот параметр называется `count`, а не `$count`.
> 
> 

`$orderby=[string]`(необязательно) — список выражений, разделенных запятыми toosort hello результаты по. Каждое выражение может быть именем поля или toohello вызов `geo.distance()` функции. Каждое выражение может следовать `asc` tooindicated по возрастанию, и `desc` tooindicate по убыванию. по умолчанию Hello по возрастанию. Предложение WITH TIES будет нарушено из hello оценки совпадения документов. Если не `$orderby` указан, порядок сортировки по умолчанию hello — по убыванию по оценке совпадения документа. Максимальное количество предложений `$orderby`— 32.

> [!NOTE]
> При вызове **поиска** с помощью запроса POST этот параметр называется `orderby`, а не `$orderby`.
> 
> 

`$select=[string]`(необязательно) — список tooretrieve полей с разделителями запятыми. Если не указан, включаются все поля, помеченные как извлекаемые в схеме hello. Можно также явно запросить все поля, установив этот параметр слишком`*`.

> [!NOTE]
> При вызове **поиска** с помощью запроса POST этот параметр называется `select`, а не `$select`.
> 
> 

`facet=[string]`(ноль или более) - toofacet поле по. При необходимости строка hello может содержать параметры toocustomize hello аспекты выраженное запятыми `name:value` пары. Ниже перечислены возможные параметры.

* `count` (максимальное количество условий аспектирования; значение по умолчанию — 10). Отсутствие максимума, но более высокие значения к снижению соответствующей производительности, особенно в том случае, если поля hello аспекта содержит большое количество уникальных условий.
  * Например: `facet=category,count:5` возвращает hello top пять категорий в результатах аспекта.  
  * **Примечание**: Если hello `count` параметр меньше hello число уникальных слов, hello результатов может оказаться неточным. Это происходит из-за toohello способ распределения запросов аспекта по сегментам. Увеличение `count` обычно повышает hello точность подсчета терминов hello, но ценой падения производительности.
* `sort`(один из `count` toosort *по убыванию* по количеству, `-count` toosort *по возрастанию* по количеству, `value` toosort *по возрастанию* по значению, или `-value` toosort *по убыванию* по значению)
  * Например: `facet=category,count:3,sort:count` возвращает hello тремя верхними категориями в результатах аспекта в убывающем порядке по hello число документов с именем каждого города. Например если тремя верхними категориями hello, бюджет, Motel и Luxury и Budget имеет 5 совпадений, Motel имеет 6, а Luxury имеет 4, затем hello контейнеров будет в порядке hello Motel, Budget, Luxury.
  * Пример. `facet=rating,sort:-value` возвращает контейнеры со всеми возможными значениями оценки rating, отсортированные в убывающем порядке по значению. Например если hello оценок от 1 too5, hello контейнеров будет упорядочен 5, 4, 3, 2, 1, вне зависимости от того, сколько документов соответствует каждой оценке.
* `values` (разделенные символами вертикальной черты числовые значения или значения типа `Edm.DateTimeOffset`, задающие динамический набор значений записей аспектов)
  * Например: `facet=baseRate,values:10|20` создает три сегмента: один для базовой ставки от 0 вверх toobut, не включая 10, один для 10 вверх toobut, не включая 20 и одну для 20 или выше.
  * Пример. `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` возвращает два контейнера: один для гостиниц, отремонтированных до февраля 2010 г., и один — для гостиниц, отремонтированных 1 февраля 2010 г. или позже.
* `interval` (целочисленный интервал больше 0 для числе либо `minute`, `hour`, `day`, `week`, `month`, `quarter` или `year` для значений даты и времени)
  * Пример. `facet=baseRate,interval:100` возвращает контейнеры для диапазонов базового тарифа с интервалом 100. Например, для базовых тарифов от 60 до 600 долларов будут возвращены контейнеры 0–100, 100–200, 200–300, 300–400, 400–500 и 500–600.
  * Пример: `facet=lastRenovationDate,interval:year` возвращает по одному контейнеру для каждого года, в течение которого выполнялся ремонт гостиниц.
* Параметр `timeoffset` ([+-]чч:мм, [+-]ччмм или [+-]чч) `timeoffset` является необязательным. Его можно объединять только с hello `interval` параметр и только если примененные tooa поле типа `Edm.DateTimeOffset`. значение Hello указывает tooaccount смещения времени hello UTC для при задании времени границы.
  * Например: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` использует hello день границу, которая начинается в формате UTC 01:00:00 (полуночи в hello целевой часовой пояс)
* **Примечание**: `count` и `sort` могут быть объединены в hello же спецификации аспекта, но они не могут сочетаться с `interval` или `values`, и `interval` и `values` не может сочетаться друг с другом.
* **Примечание**. Границы интервала для даты и времени вычисляются на основе времени в формате UTC, если не указан параметр `timeoffset`. Например: для `facet=lastRenovationDate,interval:day`, границ hello день начинается в 00:00:00 UTC. 

> [!NOTE]
> При вызове **поиска** с помощью запроса POST этот параметр называется `facets`, а не `facet`. Кроме того, она задается в виде JSON-массива строк, где каждая строка представляет собой отдельное выражение аспектирования.
> 
> 

`$filter=[string]` (необязательный): выражение структурированного поиска в стандартном синтаксисе OData.

> [!NOTE]
> При вызове **поиска** с помощью запроса POST этот параметр называется `filter`, а не `$filter`.
> 
> 

`highlight=[string]` (необязательный): набор имен полей через запятую, используемых для выделения совпадений. Для выделения можно использовать только поля с атрибутом `searchable` .

`highlightPreTag=[string]`(необязательно, по умолчанию слишком`<em>`) — тег toohit выделяет строку. Для него должно быть задано значение `highlightPostTag`.

> [!NOTE]
> При вызове **поиска** GET, зарезервированные символы в URL-АДРЕСЕ hello должна использоваться закодированные (например, % 23 вместо #).
> 
> 

`highlightPostTag=[string]`(необязательно, по умолчанию слишком`</em>`)-строковый тег, который добавляет toohit выделение. Для него должно быть задано значение `highlightPreTag`.

> [!NOTE]
> При вызове **поиска** GET, зарезервированные символы в URL-АДРЕСЕ hello должна использоваться закодированные (например, % 23 вместо #).
> 
> 

`scoringProfile=[string]`(необязательно) — имя hello оценки tooevaluate профиль соответствует оценок для соответствующих документов в результатах hello toosort заказа.

`scoringParameter=[string]`(ноль или более) — указывает hello значения для каждого параметра, определенного в функции оценки (например, `referencePointParameter`) с использованием формата hello `name-value1,value2,...`.

* Например, если профиль оценки hello определена функция с параметр с именем параметра строки запроса «mylocation» hello будет `&scoringParameter=mylocation--122.2,44.8`. Первый тире Hello отделяет hello имя из списка значений hello, во время второго дефиса hello является частью hello первое значение (в данном примере — долгота).
* Для оценки параметров такие, как для тега повышение приоритета, который может содержать запятые, знаки можно экранировать таких значений в списке hello, используя одинарные кавычки. Если значения hello, сами содержат одинарные кавычки, их можно экранировать путем удвоения.
  * Например, если тег повышение параметр с именем «mytag» и требуется tooboost теге hello значения «Hello, о ' Брайен» и «Smith», hello запроса строки из вариантов `&scoringParameter=mytag-'Hello, O''Brien',Smith`. Обратите внимание, что кавычки нужны только для значений, содержащих запятые.

> [!NOTE]
> При вызове **поиска** с помощью запроса POST этот параметр называется `scoringParameters`, а не `scoringParameter`. Кроме того, она задается в виде массива JSON строк, где каждая строка представляет собой отдельную пару `name-values` .
> 
> 

`minimumCoverage`(необязательно, по умолчанию too100) - число от 0 до 100, указывающее процент hello hello индекса, который необходимо рассмотреть в поисковом запросе в порядке для запроса toobe hello сообщить об успешном выполнении. По умолчанию должны быть доступны всем индексом hello или `Search` возвращает код состояния HTTP 503. Если задать `minimumCoverage` и `Search` завершается успешно, он вернет HTTP 200 и включить `@search.coverage` значение, указывающее процент hello hello индекса, который был включен в запрос hello ответа hello.

> [!NOTE]
> Значение параметра tooa ниже, чем 100 может быть полезным для обеспечения доступности поиска даже для служб с только одной реплики. Однако не все соответствующие документы гарантируется toobe присутствуют в результатах поиска hello. Если отзыв поиска является более важным tooyour приложения, чем доступности, то он является наиболее tooleave `minimumCoverage` значение по умолчанию 100.
> 
> 

`api-version=[string]` (обязательный). Hello предварительной версии — `api-version=2015-02-28-Preview`. Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).

Примечание: Для этой операции hello `api-version` указан как параметр запроса в URL-АДРЕСЕ hello независимо от того, вызов **поиска** с GET или POST.

**Заголовки запроса**

Hello следующий список описывает hello необходимые и необязательные заголовки запросов.

* `api-key`: hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска. Это строковое значение, URL-адрес службы уникальный tooyour. Hello **поиска** запроса можно указать ключ администратора либо ключ запроса для `api-key`.

Необходимо также hello имя tooconstruct hello запроса URL-адрес службы. Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello. В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.

**Тело запроса**

Для запроса GET: нет.

Для запроса POST:

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

**Продолжение частичных ответов поиска**

Иногда поиска Azure не может возвращать все hello запрошенные результаты в одном ответе поиска. Это может происходить по разным причинам, например запросы слишком много документов, не указывая hello запроса `$top` или указания значения для `$top` слишком большого объема. В таких случаях службы поиска Azure входят hello `@odata.nextLink` заметки в текст ответа hello и также `@search.nextPageParameters` если бы это был запрос POST. Значения hello tooformulate эти заметки можно использовать другой поиска запроса tooget hello следующая часть ответа на запросы поиска hello. Это называется ***продолжения*** hello исходный запрос для поиска и hello заметки обычно вызываются ***токены продолжения***. В разделе [приведенном ниже примере hello](#SearchResponse) сведения о синтаксисе hello этих заметок и где они отображаются в текст ответа hello. 

Hello причины, почему поиска Azure может возвращать маркеры продолжения: toochange зависит от реализации и подчиняется. Надежные клиенты всегда должен быть готов toohandle случаях возвращаются меньше документов, чем ожидалось, а токен продолжения — включить toocontinue извлечения документов. Также Обратите внимание, что необходимо использовать hello же метод HTTP, как исходный запрос hello в toocontinue порядке. Например, если был отправлен запрос GET, все отправляемые запросы на продолжение должны также использовать GET (это справедливо и для POST).

<a name="SearchResponse"></a>
**Ответ**

Код состояния: в качестве успешного ответа возвращается код "200 — ОК".

    {
      "@odata.count": # (if $count=true was provided in hello query),
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "@search.facets": { (if faceting was specified in hello query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body toofetch hello next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL toofetch hello next page of results if not all results could be returned in this response; Applies tooboth GET and POST)
    }

**Примеры**

Дополнительные примеры можно найти на hello [синтаксис выражений OData для поиска Azure](https://msdn.microsoft.com/library/azure/dn798921.aspx) страницы.

1)    Hello поиска индекса с сортировкой по убыванию по дате.

    GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }

2)    В поиске аспекта поиск в указателе hello и извлекаются аспекты для категорий, оценок, тегов, а также элементы со значениями baseRate в указанных диапазонах:

    GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }

3)    С помощью фильтра, сузить hello предыдущие результаты запроса аспекта после hello пользователь щелкает оценка 3 и категорию «Motel»:

    GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }

4) Установка для результатов аспектного поиска верхнего предела на количество уникальных условий поиска, возвращаемых запросом. по умолчанию Hello равно 10, но можно увеличить или уменьшить это значение с помощью hello `count` параметром hello `facet` атрибута:

    GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }

5)    Hello поиска индекса в пределах определенных полей; Например поле конкретного языка:

    GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }

6) Поиск hello индекс по нескольким полям. Например можно хранить и запроса для поиска полей на нескольких языках в hello же индекс.  Если описания на английском и французском сосуществовать в hello же документа, можно возвращать все hello в результаты запроса:

    GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }

Обратите внимание на то, что запрос можно отправить только к одному индексу. Не следует создавать несколько индексов для каждого языка, если не планируете tooquery одну за другой.

7)    Разбиение на страницы: Get hello первую страницу элементов (размер страницы — 10):

    GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }

8)    Разбиение на страницы: Get hello вторую страницу элементов (размер страницы — 10):

    GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }

9)    Получение определенного набора полей.

    GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }

10)  Получение документов, соответствующих определенному выражению фильтра.

    GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }

11) Индекс поиска hello и возврат фрагментов с выделением попаданий

    GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }

12) Поиск в указателе hello и возвращать документы, отсортированные от ближе toofarther от базового каталога

    GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }

13) Поиск hello индекса при условии, что существует профиля оценки «geo» вместе с двумя функциями оценки расстояния, один из которых определяет параметр с именем «currentLocation», другая определяет параметр с именем «lastLocation»

    GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }

14) Поиск документов с помощью индекса hello [синтаксис простого запроса](https://msdn.microsoft.com/library/dn798920.aspx). Этот запрос возвращает гостиницы, где для поиска поля содержат hello термины «comfort» и «location», но не «motel»:

    GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }

Обратите внимание на использование hello `searchMode=all` выше. Включая этот параметр переопределяет значение по умолчанию hello `searchMode=any`, что гарантирует, `-motel` означает «И не» вместо «Или не». Без `searchMode=all`, вы получаете «Или не», который расширяется, а не ограничивает результаты поиска, и это может быть counter-intuitive toosome пользователей.

15) Поиск документов с помощью индекса hello [синтаксис запроса lucene](https://msdn.microsoft.com/library/mt589323.aspx). Этот запрос возвращает гостиницы, где hello поле категории содержит hello термин «бюджет» и все просматриваемые полей, содержащих hello фразу «недавно отремонтированных». Документы, содержащие фразу hello «недавно отремонтированных» более высоким рангом в результате значение boost термин hello (3)

    GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }

<a name="LookupAPI"></a>

## <a name="lookup-document"></a>Запрос документов
Hello **поиск документов** операция получает документ из поиска Azure. Это полезно в том случае, когда пользователь щелкает определенный результат поиска, и требуется toolook конкретные сведения о документе.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

**Запрос**

Запросы к службе отправляются по протоколу HTTPS. Hello **поиск документов** запрос можно составить следующим образом.

    GET /indexes/[index name]/docs/key?[query parameters]

Кроме того можно использовать традиционный синтаксис OData hello для поиска ключа:

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

Hello URI запроса содержит [имя индекса] и [key], указав какие tooretrieve документ, соответствующий индекс. За один раз можно получить только один документ. Используйте **поиска** tooget несколько документов в одном запросе.

**Параметры запроса**

`$select=[string]`(необязательно) — список tooretrieve полей с разделителями запятыми. Если не задано или имеет слишком`*`, все поля, помеченные в схеме hello извлекаемые, включены в проекцию hello.

`api-version=[string]` (обязательный). Hello предварительной версии — `api-version=2015-02-28-Preview`. Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).

Примечание: Для этой операции hello `api-version` указан как параметр запроса.

**Заголовки запроса**

Hello следующий список описывает hello необходимые и необязательные заголовки запросов.

* `api-key`: hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска. Это строковое значение, URL-адрес службы уникальный tooyour. Hello **поиск документов** запроса можно указать ключ администратора либо ключ запроса для `api-key`.

Необходимо также hello имя tooconstruct hello запроса URL-адрес службы. Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello. В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.

**Тело запроса**

Отсутствует.

**Ответ**

Код состояния: в качестве успешного ответа возвращается код "200 — ОК".

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

**Пример**

Поиск документов hello с ключом "2"

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

Поиск документов hello с ключом "3" с использованием синтаксиса OData:

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a>Подсчет документов
Hello **подсчет документов** операция получает число hello число документов в индекс поиска. Hello `$count` синтаксис является частью hello протокол OData.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

**Запрос**

Запросы к службе отправляются по протоколу HTTPS. Hello **подсчет документов** запрос может быть создан с помощью метода GET hello.

Hello [имя индекса] в URI запроса hello сообщает hello службы tooreturn количество всех элементов в коллекции документов указанного индекса hello hello.

`api-version=[string]` (обязательный). Hello предварительной версии — `api-version=2015-02-28-Preview`. Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).

**Заголовки запроса**

Hello следующий список описывает hello необходимые и необязательные заголовки запросов.

* `Accept`: Это значение должно быть задано слишком`text/plain`.
* `api-key`: hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска. Это строковое значение, URL-адрес службы уникальный tooyour. Hello **подсчет документов** запроса можно указать ключ администратора либо ключ запроса для `api-key`.

Необходимо также hello имя tooconstruct hello запроса URL-адрес службы. Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello. В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.

**Тело запроса**

Отсутствует.

**Ответ**

Код состояния: в качестве успешного ответа возвращается код "200 — ОК".

текст ответа Hello содержит значение числа hello как целое число в формате обычного текста.

<a name="Suggestions"></a>

## <a name="suggestions"></a>Предложения
Hello **предложения** операция получает предложения на основании частичного ввода условия поиска. Он обычно используется в поиск поля tooprovide упреждающих предложений при вводе условия поиска.

Предложения запросов направлены на предложение целевых документов, поэтому предложенные hello, что текст может повторяться, если несколько документов-кандидатов соответствует hello же поиска входных данных. Можно использовать `$select` tooretrieve других документов поля (включая hello ключ документа), чтобы можно было определить, какой документ является источником каждого предложения hello.

Операция **вызова предложений** выполняется как запрос GET или POST.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**При УЧЕТЕ toouse вместо GET**

При использовании HTTP GET hello toocall **предложения** API-интерфейса, необходимо помнить, что длина URL-адрес запроса hello hello не может превышать 8 КБ toobe. Для большинства приложений этого достаточно. В то же время некоторые приложения создают очень длинные запросы, в частности выражения фильтров OData. Лучший вариант для этих приложений — использование запроса HTTP POST, так как он позволяет увеличить фильтры по сравнению с GET. С помощью запроса POST hello количество предложений в фильтре hello ограничивающим фактором, не hello размер строки фильтра необработанные hello, поскольку hello предельного размера запроса для POST — приблизительно 16 МБ.

> [!NOTE]
> Несмотря на то, что ограничение на размер запроса POST hello очень велика, критерии фильтра не может быть произвольным и довольно сложным. Дополнительные сведения об ограничениях сложности фильтров см. в статье, посвященной [синтаксису выражений OData](https://msdn.microsoft.com/library/dn798921.aspx).
> 
> 

**Запрос**

Запросы к службе отправляются по протоколу HTTPS. Hello **предложения** можно составить запрос методы с помощью hello GET или POST.

URI запроса Hello указывает имя hello hello tooquery индекса. Параметры, такие как hello частично введенное условие поиска, указанные в строке запроса hello в случае hello запросов GET, а в запросе hello запрашивает текст в случае, когда hello POST.

Рекомендуется при создании запросов GET, следует помнить слишком[кодирование URL-адрес](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) конкретного запроса, параметров при вызове hello REST API напрямую. Для операций **вызова предложений** эти параметры указаны ниже.

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

Кодировка URL рекомендуется только для hello выше параметров запроса. Если вы случайно URL-кодировали hello вся строка запроса (все после hello?), запросы будут нарушены.

Кроме того URL-кодирование необходима только при вызове hello получить напрямую с помощью API-интерфейса REST. Кодировка URL-адрес не является обязательным при вызове **предложения** с помощью запроса POST, или при использовании hello [клиентская библиотека .NET](https://msdn.microsoft.com/library/dn951165.aspx), обрабатывающая для кодирования URL-адрес.

**Параметры запроса**

**Предложения** принимает несколько параметров, которые сообщают условия запроса и определяют способы поиска. Укажите эти параметры в URL-АДРЕСЕ hello строку запроса, при вызове **предложения** через GET, а также как свойства JSON в теле запроса hello при вызове **предложения** помощью POST. синтаксис Hello для некоторых параметров немного отличается от GET и POST. Эти различия описаны ниже.

`search=[string]`-hello запросы toosuggest toouse полнотекстового поиска. Минимальная длина — 1 символ, максимальная — 100 символов.

`highlightPreTag=[string]`(необязательно) — тег строки toosearch попаданий. Для него должно быть задано значение `highlightPostTag`.

> [!NOTE]
> При вызове **предложения** GET, зарезервированные символы в URL-АДРЕСЕ hello должна использоваться закодированные (например, % 23 вместо #).
> 
> 

`highlightPostTag=[string]`(необязательно) — строковый тег, который добавляет toosearch попаданий. Для него должно быть задано значение `highlightPreTag`.

> [!NOTE]
> При вызове **предложения** GET, зарезервированные символы в URL-АДРЕСЕ hello должна использоваться закодированные (например, % 23 вместо #).
> 
> 

`suggesterName=[string]`— Имя средства подбора hello, как указано в hello hello `suggesters` коллекцию, которая входит в определение индекса hello. `suggester` определяет, в каких полях выполняется поиск предложений по условиям запроса. Дополнительные сведения см. в разделе [Средства подбора](#Suggesters).

`fuzzy=[boolean]`(необязательно, по умолчанию = ложь)-Если для параметра задано tootrue API будет находить предложения даже при наличии замененного или отсутствующего символа в тексте hello поиска. В определенных ситуациях это улучшает результат, однако ведет к снижению производительности, так как запросы по нечеткому соответствию обрабатываются медленнее и потребляют больше ресурсов.

`searchFields=[string]`(необязательно) — список hello toosearch имена полей с разделителями запятыми для hello указанный искомый текст. Для целевых полей должен быть разрешен поиск предложений.

`$top=#`(необязательно, по умолчанию = 5)-число tooretrieve предложения hello. Это значение должно быть в диапазоне от 1 до 100.

> [!NOTE]
> При вызове **предложений** с помощью запроса POST этот параметр называется `top`, а не `$top`.
> 
> 

`$filter=[string]`(необязательно) — выражение, фильтрующее документы hello, рассматриваемые для предложений.

> [!NOTE]
> При вызове **предложений** с помощью запроса POST этот параметр называется `filter`, а не `$filter`.
> 
> 

`$orderby=[string]`(необязательно) — список выражений, разделенных запятыми toosort hello результаты по. Каждое выражение может быть именем поля или toohello вызов `geo.distance()` функции. Каждое выражение может следовать `asc` tooindicated по возрастанию, и `desc` tooindicate по убыванию. по умолчанию Hello по возрастанию. Максимальное количество предложений `$orderby`— 32.

> [!NOTE]
> При вызове **предложений** с помощью запроса POST этот параметр называется `orderby`, а не `$orderby`.
> 
> 

`$select=[string]`(необязательно) — список tooretrieve полей с разделителями запятыми. Если не указано, только hello ключ документа и возвращается текст подсказки. Можно явно запросить все поля, установив этот параметр слишком`*`.

> [!NOTE]
> При вызове **предложений** с помощью запроса POST этот параметр называется `select`, а не `$select`.
> 
> 

`minimumCoverage`(необязательно, по умолчанию too80) - число от 0 до 100, указывающее процент hello hello индекса, который должен быть охвачен предложения запроса в порядке для запроса toobe hello сообщить об успешном выполнении. По умолчанию, должен быть доступен по крайней мере 80% hello индекса или `Suggest` возвращает код состояния HTTP 503. Если задать `minimumCoverage` и `Suggest` завершается успешно, он вернет HTTP 200 и включить `@search.coverage` значение, указывающее процент hello hello индекса, который был включен в запрос hello ответа hello.

> [!NOTE]
> Значение параметра tooa ниже, чем 100 может быть полезным для обеспечения доступности поиска даже для служб с только одной реплики. Однако не все соответствующие предложения гарантируется toobe присутствуют в результатах hello. Если отзыв является более важным tooyour приложения, чем доступности, то он является наилучшим образом не toolower `minimumCoverage` ниже его значение по умолчанию, равное 80.
> 
> 

`api-version=[string]` (обязательный). Hello предварительной версии — `api-version=2015-02-28-Preview`. Подробные сведения, в том числе о других версиях, см. в статье об [управлении версиями службы поиска](http://msdn.microsoft.com/library/azure/dn864560.aspx).

Примечание: Для этой операции hello `api-version` указан как параметр запроса в URL-АДРЕСЕ hello независимо от того, вызов **предложения** с GET или POST.

**Заголовки запроса**

Hello следующий список описывает hello необходимые и необязательные заголовки запросов

* `api-key`: hello `api-key` — tooyour запроса используется tooauthenticate hello службы поиска. Это строковое значение, URL-адрес службы уникальный tooyour. Hello **предложения** запроса можно указать ключ администратора либо ключ запроса как hello `api-key`.

Необходимо также hello имя tooconstruct hello запроса URL-адрес службы. Можно получить имя службы hello и `api-key` из панели мониторинга службы на портале Azure hello. В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) для справки о навигации по странице.

**Тело запроса**

Для запроса GET: нет.

Для запроса POST:

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

**Ответ**

Код состояния: в качестве успешного ответа возвращается код "200 — ОК".

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

Если параметр проекции hello используется tooretrieve поля, они включаются в каждый элемент массива hello:

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

**Пример**

Получение 5 предложений, где «lux» hello частичного ввода условия поиска

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
