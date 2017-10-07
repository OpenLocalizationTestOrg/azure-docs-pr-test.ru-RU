---
title: "AAA» передачи данных (REST API - службы поиска Azure) | Документы Microsoft»"
description: "Узнайте, как индекс tooan tooupload данных в поиске Azure с помощью hello REST API."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: 8d0749fb-6e08-4a17-8cd3-1a215138abc6
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 6ba1336012d1f0f6d6d6c933e16aa879afb9b824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-rest-api"></a>Здравствуйте, передачи данных tooAzure поиска с помощью API-интерфейса REST
> [!div class="op_single_selector"]
>
> * [Обзор](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
>
>

В этой статье будет показано, как toouse hello [REST API поиска Azure](https://docs.microsoft.com/rest/api/searchservice/) tooimport данных в индекс поиска Azure.

Прежде чем приступать к выполнению инструкций из этого руководства, вам нужно [создать индекс службы поиска Azure](search-what-is-an-index.md).

В порядке toopush документов в индекс с помощью API-интерфейса REST hello будут выдаваться конечная точка индекса запрос HTTP POST tooyour URL-адрес. текст Hello hello HTTP-запроса, что текст является объект JSON, содержащий документы hello toobe добавлены, изменены или удалены.

## <a name="identify-your-azure-search-services-admin-api-key"></a>Определение ключа API администратора службы поиска Azure
При выдаче HTTP-запросы к службе с помощью REST API hello *каждого* API запрос должен включать hello api ключ, созданный для hello подготовке службы поиска. Наличие действительного ключа позволяет установить отношения доверия, для каждого запроса, между Отправка запроса hello hello приложения и службы hello, обрабатывает его.

1. toofind ключи api службы, вы сможете войти toohello [портал Azure](https://portal.azure.com/)
2. Перейдите в колонку службы поиска Azure tooyour
3. Щелкните значок «Ключи» hello

Ваша служба получит *ключи администратора* и *ключи запросов*.

* Первичная и Вторичная *ключей администратора* предоставить полные права tooall операций, включая toomanage hello hello возможности службы, создания и удаления индексов, индексаторов и источников данных. Существует два ключа, чтобы продолжить toouse hello вторичный ключ в случае tooregenerate hello первичного ключа и наоборот.
* Ваш *запрос ключей* предоставить доступ только для чтения tooindexes и документы и представляют собой tooclient обычно распределенного приложения, издающие запросы поиска.

Импорт данных в индекс целях hello, можно использовать ключ администратора первичной или вторичной.

## <a name="decide-which-indexing-action-toouse"></a>Решите, какие индексирования toouse действие
При использовании REST API hello, URL-адрес конечной точки JSON запроса тел tooyour индекс поиска Azure будут выдаваться HTTP-запросы POST. объект JSON Hello в тексте запроса HTTP будет содержать один массив JSON с именем «value», содержащий JSON объектов, представляющих документы хотелось бы tooadd tooyour индекс, обновить или удалить.

Каждый объект JSON в массиве «value» hello представляет toobe документа, в индекс. Каждый из этих объектов содержит ключ документа hello и действие hello требуемого индексирования (отправка, слияние, удаление, и т. д). В зависимости от того, какой из hello следующие действия, которые можно выбрать только определенные поля должны быть включены для каждого документа:

| @search.action | Описание | Необходимые поля для каждого документа | Примечания |
| --- | --- | --- | --- |
| `upload` |`upload` Действие — примерно tooan «вставки-обновления» где документ hello будет вставлена, если является новым и обновлен или заменен, если он существует. |ключ, а также другие поля, нужно toodefine |При обновлении или замене существующего документа, любое поле, которое не указано в запросе hello будет иметь слишком его поле`null`. Это происходит даже в том случае, если поле hello было установлено ранее tooa непустое значение. |
| `merge` |Обновления, существующий документ с hello указаны поля. Если документ hello не существует в индексе hello, hello слияния завершится ошибкой. |ключ, а также другие поля, нужно toodefine |Любое поле, указанное для объединения приведет к замене существующего поля hello в документе hello. Это относится и к полям типа `Collection(Edm.String)`. Например, если hello документ содержит поле `tags` со значением `["budget"]` , и вы выполните объединение со значением `["economy", "pool"]` для `tags`, hello окончательное значение hello `tags` поле будет `["economy", "pool"]`. а не `["budget", "economy", "pool"]`. |
| `mergeOrUpload` |Это действие ведет себя как `merge` Если документ с hello заданным ключом уже существует в индексе hello. Если документ hello не существует, он ведет себя как `upload` с новым документом. |ключ, а также другие поля, нужно toodefine |- |
| `delete` |Удаляет указанный документ hello из индекса hello. |Только ключ |Все поля, укажите вместо hello ключевое поле будет игнорироваться. Tooremove отдельного поля из документа, используйте `merge` вместо и просто задать поле hello явно toonull. |

## <a name="construct-your-http-request-and-request-body"></a>Создание HTTP-запроса и текста запроса
Теперь, когда собранные значения hello необходимые поля для действий индекса, будут готовы tooconstruct hello самого запроса HTTP и JSON запроса текст tooimport данных.

#### <a name="request-and-request-headers"></a>Запрос и заголовки запроса
В URL-адрес hello, нужно будет tooprovide на имя службы, имя индекса («гостиницы» в данном случае), а также hello правильную версию API (текущая версия API hello `2016-09-01` во время публикации в этом документе hello). Вам потребуется toodefine hello `Content-Type` и `api-key` заголовки запроса. В последнем hello можно используйте один из ключей администратора службы.

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a>Текст запроса
```JSON
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
            "@search.action": "mergeOrUpload",
            "hotelId": "3",
            "baseRate": 129.99,
            "description": "Close tootown hall and hello river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

В этом примере мы используем операции `upload`, `mergeOrUpload` и `delete` в качестве операций поиска.

Предположим, что пример индекса с именем hotels уже заполнен несколькими документами. Обратите внимание на то, как бы не было toospecify все поля hello возможных документа при использовании `mergeOrUpload` и как мы указан только ключ документа hello (`hotelId`) при использовании `delete`.

Кроме того Обратите внимание, что может включать только документы too1000 (или 16 МБ) в одном запросе индексирования.

## <a name="understand-your-http-response-code"></a>Анализ кода HTTP-ответа
#### <a name="200"></a>200
После успешной отправки запроса на индексирование вы получите HTTP-ответ с кодом состояния `200 OK`. Hello JSON-тексте hello HTTP-ответа будет выглядеть следующим образом:

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": true,
            "errorMessage": null
        },
        ...
    ]
}
```

#### <a name="207"></a>207
Код состояния `207` возвращается, если хотя бы один элемент не удалось проиндексировать. Hello JSON-тексте hello HTTP-ответа будет содержать сведения о неудачных документов hello.

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "hello search service is too busy tooprocess this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> Часто это означает, что hello нагрузки на поиск службы достижение точки, где запросы индексирования начнутся tooreturn `503` ответов. В таком случае мы настоятельно рекомендуем задержать выполнение клиентского кода и повторить попытку позже. Это позволит получить hello системы toorecover некоторое время, увеличить вероятность hello будущие запросы будут выполнены успешно. Быстрое повторение запросов только продлит проблемную ситуацию hello.
>
>

#### <a name="429"></a>429
Код состояния `429` будет возвращаться при превысили квоту на число hello документов в индекс.

#### <a name="503"></a>503
Код состояния `503` будет возвращено, если ни один из элементов hello в запросе hello были успешно проиндексированы. Эта ошибка означает, что является hello системы находящейся под интенсивной нагрузкой, и в настоящее время не удается обработать ваш запрос.

> [!NOTE]
> В таком случае мы настоятельно рекомендуем задержать выполнение клиентского кода и повторить попытку позже. Это позволит получить hello системы toorecover некоторое время, увеличить вероятность hello будущие запросы будут выполнены успешно. Быстрое повторение запросов только продлит проблемную ситуацию hello.
>
>

Дополнительные сведения о действиях с документами и ответах об успешном выполнении и ошибках см. в статье, посвященной [добавлению, обновлению и удалению документов](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents). Дополнительные сведения о других кодах состояния HTTP, которые могут быть возвращены в случае сбоя, см. в статье [Коды состояния HTTP (поиск Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).

## <a name="next-steps"></a>Дальнейшие действия
После заполнения индекса поиска Azure, будет готов toostart выдача запросов toosearch для документов. Дополнительные сведения см. в статье [Запросы в службе поиска Azure](search-query-overview.md).
