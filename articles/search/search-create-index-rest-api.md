---
title: "AAA «создание индекса (API REST - службы поиска Azure) | Документы Microsoft»"
description: "Создайте индекс в коде с помощью hello HTTP REST API поиска Azure."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: ac6c5fba-ad59-492d-b715-d25a7a7ae051
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 117ab64a9874a443351a8a02a9b959b8f7beb7c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-rest-api"></a>Создание индекса поиска Azure с помощью API-интерфейса REST hello
> [!div class="op_single_selector"]
>
> * [Обзор](search-what-is-an-index.md)
> * [Портал](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
>
>

В этой статье приведена пошаговая процедура hello процесс создания поиска Azure [индекс](https://docs.microsoft.com/rest/api/searchservice/Create-Index) с помощью REST API поиска Azure "hello".

Перед выполнением инструкций, приведенных в этом руководстве, и созданием индекса следует [создать службу поиска Azure](search-create-service-portal.md).

toocreate индекс поиска Azure с помощью API-интерфейса REST hello, будет выдавать один HTTP POST запроса tooyour поиска Azure URL-адрес конечной точки службы. Определение индекса будут содержаться в теле запроса hello правильного формата содержимого в JSON.

## <a name="identify-your-azure-search-services-admin-api-key"></a>Определение ключа API администратора службы поиска Azure
Теперь, когда вы подготовили службы поиска Azure, можно отправлять HTTP-запросы к URL-адрес конечной точки вашей службы, с помощью API-интерфейса REST hello. *Все* запросы API должны содержать hello api ключ, созданный для hello подготовке службы поиска. Наличие действительного ключа позволяет установить отношения доверия, для каждого запроса, между Отправка запроса hello hello приложения и службы hello, обрабатывает его.

1. toofind ключи api службы, необходимо войти в hello [портал Azure](https://portal.azure.com/)
2. Перейдите в колонку службы поиска Azure tooyour
3. Щелкните значок «Ключи» hello

Ваша служба получит *ключи администратора* и *ключи запросов*.

* Первичная и Вторичная *ключей администратора* предоставить полные права tooall операций, включая toomanage hello hello возможности службы, создания и удаления индексов, индексаторов и источников данных. Существует два ключа, чтобы продолжить toouse hello вторичный ключ в случае tooregenerate hello первичного ключа и наоборот.
* Ваш *запрос ключей* предоставить доступ только для чтения tooindexes и документы и представляют собой tooclient обычно распределенного приложения, издающие запросы поиска.

Создание индекса целях hello, можно использовать ключ администратора первичной или вторичной.

## <a name="define-your-azure-search-index-using-well-formed-json"></a>Определение индекса службы поиска Azure с помощью JSON-содержимого правильного формата
Одна служба tooyour запрос HTTP POST будет создать индекс. текст Hello запроса HTTP POST, будет содержать один объект JSON, определяющий индекса поиска Azure.

1. Первое свойство Hello объекта JSON — hello имя индекса.
2. Второе свойство Hello объекта JSON является массивом JSON с именем `fields` , содержащий отдельным объектом JSON для каждого поля в индексе. Каждый из этих объектов JSON содержат несколько пар имя значение для каждого hello полей атрибутов, включая «name», «тип» и т. д.

Очень важно, следует найти качества и бизнес-потребностей организации помнить при проектировании индекса, как каждое поле необходимо назначить hello [правильными атрибутами](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Эти атрибуты выбирать поиск функций (фильтрация, аспекта, сортировка полнотекстового поиска, т. д.) применяются toowhich поля. Для любого атрибута, который не указан по умолчанию hello будет выполняться tooenable hello соответствующей функции поиска, если она специально отключить.

В нашем примере мы присвоили индексу имя hotels и определили поля следующим образом:

```JSON
{
    "name": "hotels",  
    "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false, "sortable": false, "facetable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String", "facetable": false},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean", "sortable": false},
        {"name": "smokingAllowed", "type": "Edm.Boolean", "sortable": false},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
    ]
}
```

Мы выбрали тщательно hello атрибуты индекса для каждого поля, в зависимости от того, как мы думаем, что они будут использоваться в приложении. Например `hotelId` является уникальным ключом людей, поиске гостиницы скорее всего, не будет знать, поэтому мы отключаем полнотекстового поиска для этого поля, задав `searchable` слишком`false`, что экономит место в индексе hello.

Обратите внимание, только одно поле в индексе типа `Edm.String` необходимо hello назначить в качестве поля 'key' hello.

Определение индекса Hello выше использует анализатора языка для hello `description_fr` поле, так как он является предполагаемым toostore текстом на французском языке. В разделе [hello языковой поддержки раздела](https://docs.microsoft.com/rest/api/searchservice/Language-support) а также соответствующий hello [блога](https://azure.microsoft.com/blog/language-support-in-azure-search/) Дополнительные сведения о языковых анализаторов.

## <a name="issue-hello-http-request"></a>Проблема hello HTTP запроса
1. Используя определение индекса в качестве текста запроса hello, выдавать HTTP POST tooyour поиска Azure службы конечной точки URL-адрес запроса. В URL-АДРЕСЕ hello, toouse убедиться, что имя службы, имени узла hello и помещать hello правильную `api-version` как параметр строки запроса (текущая версия API hello `2016-09-01` во время публикации в этом документе hello).
2. В заголовках запроса hello, укажите hello `Content-Type` как `application/json`. Необходимо также tooprovide ключ администратора службы, определенное в шаге I hello `api-key` заголовок.

Tooprovide будет иметь свои собственные службы api и имя ключа tooissue hello запроса ниже:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [api-key]


При успешном выполнении запроса возвращается код состояния 201 (индекс создан). Дополнительные сведения о создании индекса с помощью API-интерфейса REST hello посетите hello [здесь Справочник по API](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Дополнительные сведения о других кодах состояния HTTP, которые могут быть возвращены в случае сбоя, см. в статье [Коды состояния HTTP (поиск Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).

После завершения операции с индексом и хотите toodelete он просто выполните запрос HTTP DELETE. Например это, как мы удалить индекс «гостиницы» hello:

    DELETE https://[service name].search.windows.net/indexes/hotels?api-version=2016-09-01
    api-key: [api-key]


## <a name="next-steps"></a>Дальнейшие действия
После создания индекс поиска Azure, вы будете готовы слишком[отправки содержимого в индекс hello](search-what-is-data-import.md) чтобы вы могли начать поиск данных.
