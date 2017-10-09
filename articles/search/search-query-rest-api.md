---
title: "AAA» запроса индекса (API REST - службы поиска Azure) | Документы Microsoft»"
description: "Построить запрос поиска в поиске Azure и использовать параметры сортировки и toofilter поиска результатов поиска."
services: search
documentationcenter: 
manager: jhubbard
author: ashmaka
ms.assetid: 8b3ca890-2f5f-44b6-a140-6cb676fc2c9c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/12/2017
ms.author: ashmaka
ms.openlocfilehash: 2f12238b8f4b045f536489cfc8766fb68307bbe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-rest-api"></a>Запросить индекс поиска Azure с помощью API-интерфейса REST hello
> [!div class="op_single_selector"]
>
> * [Обзор](search-query-overview.md)
> * [Портал](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

В этой статье показано, как hello индекса с помощью tooquery [REST API поиска Azure](https://docs.microsoft.com/rest/api/searchservice/).

Прежде чем приступать к выполнению инструкций из этого руководства, необходимо [создать индекс службы поиска Azure](search-what-is-an-index.md) и [заполнить его данными](search-what-is-data-import.md). Общие сведения см. в статье [Как работает полнотекстовый поиск в службе поиска Azure](search-lucene-query-architecture.md).

## <a name="identify-your-azure-search-services-query-api-key"></a>Определение ключа API запроса службы поиска Azure
Ключевым компонентом каждой операции поиска для hello REST API поиска Azure является hello *ключ api* , созданном для службы hello подготовке. Наличие действительного ключа позволяет установить отношения доверия, для каждого запроса, между Отправка запроса hello hello приложения и службы hello, обрабатывает его.

1. toofind ключи api службы, вы сможете войти toohello [портал Azure](https://portal.azure.com/)
2. Перейдите в колонку службы поиска Azure tooyour
3. Щелкните значок «Ключи» hello

Ваша служба получит *ключи администратора* и *ключи запросов*.

* Первичная и Вторичная *ключей администратора* предоставить полные права tooall операций, включая toomanage hello hello возможности службы, создания и удаления индексов, индексаторов и источников данных. Существует два ключа, чтобы продолжить toouse hello вторичный ключ в случае tooregenerate hello первичного ключа и наоборот.
* Ваш *запрос ключей* предоставить доступ только для чтения tooindexes и документы и представляют собой tooclient обычно распределенного приложения, издающие запросы поиска.

Запросы к индексу целях hello можно использовать один из ключей запроса. Ключи администратора также может использоваться для запросов, но ключ запроса следует использовать в коде приложения, как это лучше отвечает hello [принципа наименьших прав доступа](https://en.wikipedia.org/wiki/Principle_of_least_privilege).

## <a name="formulate-your-query"></a>Формулировка запроса
Существует два способа слишком[поиска индекса с помощью API-интерфейса REST hello](https://docs.microsoft.com/rest/api/searchservice/Search-Documents). Один из способов — tooissue запрос HTTP POST, где определяются параметры запроса в объект JSON в теле запроса hello. Hello другим способом является tooissue запрос HTTP GET, где определяются параметры запроса в URL-адрес запроса hello. POST имеет несколько [ослаблены ограничения](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) на размер hello параметров запроса от GET. Поэтому мы рекомендуем использовать запрос POST, за исключением особых случаев, когда удобнее использовать запрос GET.

Для POST и GET требуются tooprovide вашей *имя службы*, *имя индекса*и соответствующие hello *версия API* (hello текущая версия API — `2016-09-01` во время hello публикации в этом документе) URL-адрес запроса hello. GET, hello *строку запроса* hello конец hello URL-адреса является вам необходимо указать параметры запроса hello. Ниже приведена hello формат URL-адреса:

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

Hello формате для БЛОГА Здравствуйте, таким же, но с только api-version в hello параметры строки запроса.

#### <a name="example-queries"></a>Примеры запросов
Вот несколько примеров запросов к индексу с именем hotels. Эти запросы отображаются в формате GET и POST.

Поиск hello термин «бюджет» Привет всем индексом и возвращать только hello `hotelName` поля:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

Применить фильтр toohello индекс toofind гостиницы дешевле, чем 150 за ночь и вернуться hello `hotelId` и `description`:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

Всего индекса поиска hello, упорядочение по определенному полю (`lastRenovationDate`) по убыванию, принимают результаты двух верхних hello и Показать только `hotelName` и `lastRenovationDate`:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$top=2&$orderby=lastRenovationDate desc&$select=hotelName,lastRenovationDate&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "orderby": "lastRenovationDate desc",
    "select": "hotelName,lastRenovationDate",
    "top": 2
}
```

## <a name="submit-your-http-request"></a>Отправка HTTP-запроса
Теперь, когда вы сформулировали запрос как часть URL-адреса HTTP-запроса (для GET) или основного текста (для POST), можно определить заголовки запроса и отправить запрос.

#### <a name="request-and-request-headers"></a>Запрос и заголовки запроса
Необходимо определить два заголовка запроса для GET или три — для POST:

1. Hello `api-key` заголовка должно быть установлено toohello ключа запроса, определенные в действии я выше. Можно также использовать ключ администратора как hello `api-key` заголовок, но рекомендуется использовать ключ запроса, так как он только предоставляет tooindexes доступ только для чтения и документы.
2. Hello `Accept` заголовка должно быть установлено слишком`application/json`.
3. POST, hello `Content-Type` заголовок также должен быть установлен слишком`application/json`.

Ниже приведена HTTP GET запроса toosearch hello «гостиницы» индекса при помощи hello REST API поиска Azure, с помощью простой запрос, который выполняет поиск hello термин «motel»:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

Вот hello же пример запроса, в настоящее время с помощью HTTP POST:

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

Код состояния запроса успешный запрос приведет к `200 OK` и hello результаты поиска возвращаются в виде JSON в теле ответа hello. Вот какие hello результаты для hello выше запрос, как будет выглядеть, при условии, что индекс гостиницы «hello» заполняется данными образец hello в [Здравствуйте, импорт данных в поиске Azure с помощью API-интерфейса REST](search-import-data-rest-api.md) (Обратите внимание, что hello JSON был отформатирован для ясности).

```JSON
{
    "value": [
        {
            "@search.score": 0.59600675,
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags":["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": {
                "type": "Point",
                "coordinates": [-122.131577, 49.678581],
                "crs": {
                    "type":"name",
                    "properties": {
                        "name": "EPSG:4326"
                    }
                }
            }
        }
    ]
}
```

toolearn, посетите раздел «Ответ» hello [поиск документов](https://docs.microsoft.com/rest/api/searchservice/Search-Documents). Дополнительные сведения о других кодах состояния HTTP, которые могут быть возвращены в случае сбоя, см. в статье [Коды состояния HTTP (поиск Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).
