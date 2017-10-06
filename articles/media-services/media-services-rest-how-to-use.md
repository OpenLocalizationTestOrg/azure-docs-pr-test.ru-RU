---
title: "Общие сведения об операциях служб REST API aaaMedia | Документы Microsoft"
description: "Обзор интерфейса REST API служб мультимедиа"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a5f1c5e7-ec52-4e26-9a44-d9ea699f68d9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b54f4d9123486d6cae832c9817688b0f3da5b401
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-operations-rest-api-overview"></a>Обзор REST API операций служб мультимедиа
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

Hello **REST операции служб мультимедиа** API используется для создания заданий, активы, политики доступа и других операций с объектами в учетную запись служб мультимедиа. Дополнительные сведения см. в статье [Media Services Operations REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference) (Справочник по REST API операций служб мультимедиа).

Службы мультимедиа Microsoft Azure — это службы, которые принимают HTTP-запросы на основе OData и могут отвечать с использованием подробного формата JSON или atom+pub. Поскольку службы мультимедиа соответствует правилам разработки tooAzure, нет набор обязательных заголовков HTTP, которые должен использовать каждый клиент при подключении служб tooMedia, а также ряд дополнительных заголовков, которые можно использовать. Hello следующих разделах описываются заголовки hello и HTTP-команды, которые можно использовать при создании запросов и получения ответов от служб мультимедиа.

В этом разделе приводится обзор toouse v2 REST с помощью служб мультимедиа.

## <a name="considerations"></a>Рекомендации

Привет, следующие рекомендации применимы только при использовании REST.

* При запросе сущности, имеется ограничение в 1000 сущностей, возвращаемых одновременно, так как открытые v2 REST ограничивает результаты too1000 результаты запроса. Требуется toouse **пропустить** и **принимать** (.NET) и **верхней** (REST), как описано в [в этом примере .NET](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) и [этот интерфейс API REST Пример](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities). 
* При использовании JSON и указав toouse hello **__metadata** ключевое слово в запросе hello (например, tooreferences связанный объект), необходимо задать hello **Accept** заголовок слишком[JSON в подробном формате ](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/) (см. следующий пример hello). OData не понимает hello **__metadata** запросить свойство в hello, если вы задали tooverbose.  
  
        POST https://media.windows.net/API/Jobs HTTP/1.1
        Content-Type: application/json;odata=verbose
        Accept: application/json;odata=verbose
        DataServiceVersion: 3.0
        MaxDataServiceVersion: 3.0
        x-ms-version: 2.11
        Authorization: Bearer <token> 
        Host: media.windows.net
  
        {
            "Name" : "NewTestJob", 
            "InputMediaAssets" : 
                [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aba5356eb-30ff-4dc6-9e5a-41e4223540e7')"}}]
        . . . 

## <a name="standard-http-request-headers-supported-by-media-services"></a>Стандартные заголовки HTTP-запроса, поддерживаемые службами мультимедиа
Для каждого запроса в службы мультимедиа, имеется ряд обязательных заголовков, необходимо включить в запрос, а также набор необязательных заголовков можно tooinclude. Следующая таблица списки hello Hello необходимые заголовки:

| Заголовок | Тип | Значение |
| --- | --- | --- |
| Авторизация |Носитель |Носителя — hello принимается только механизм авторизации. значение Hello должно включать токен доступа hello, предоставляемое ACS. |
| x-ms-version |Decimal |2.11 |
| DataServiceVersion |Decimal |3.0 |
| MaxDataServiceVersion |Decimal |3.0 |

> [!NOTE]
> Поскольку службы мультимедиа используют OData tooexpose своего базового репозитория метаданных ресурсов через API REST, hello DataServiceVersion и MaxDataServiceVersion заголовки должны быть включены в любой запрос; Тем не менее если это не так, затем в настоящее время Media Services считает hello значение DataServiceVersion 3.0.
> 
> 

Hello ниже приведен набор дополнительных заголовков:

| Заголовок | Тип | Значение |
| --- | --- | --- |
| Дата |RFC 1123 date |Метка времени запроса hello |
| Принять |Тип содержимого |Hello запрошенный тип содержимого для ответа hello hello ниже:<p> application/json;odata=verbose<p> application/atom+xml<p> Ответы могут содержать разные типы содержимого, например больших двоичных объектов, где успешный ответ будет содержать поток больших двоичных объектов hello как hello полезные данные. |
| Accept-Encoding |Gzip, deflate |Кодировка GZIP и, в соответствующих случаях, DEFLATE. Примечание. Для больших ресурсов службы мультимедиа могут пропустить этот заголовок и вернуть несжатые данные. |
| Accept-Language |"en", "ru" и т. д. |Задает hello предпочитаемый язык для ответа hello. |
| Accept-Charset |Тип кодировки, например "UTF-8" |По умолчанию — UTF-8. |
| X-HTTP-Method |Метод HTTP |Позволяет клиентам или брандмауэрам, которые не поддерживают методы HTTP, как PUT или DELETE toouse эти методы, Туннелированные посредством вызова GET. |
| Content-Type |Тип содержимого |Запрашивает тип содержимого текста запроса hello в PUT или POST. |
| client-request-id |Строка |Определяемый вызывающим объектом значение, определяющее hello заданного запроса. Если указано, это значение будет включен в ответное сообщение hello как запрос hello toomap способом. <p><p>**Важно!**<p>Значения должны превышать 2096 Б (2 КБ). |

## <a name="standard-http-response-headers-supported-by-media-services"></a>Стандартные ответы HTTP-запроса, поддерживаемые службами мультимедиа
Hello ниже приведен ряд заголовки, которые могут быть возвращены tooyou в зависимости от ресурсов hello запрошенного и hello предназначен tooperform действие.

| Заголовок | Тип | Значение |
| --- | --- | --- |
| request-id |Строка |Уникальный идентификатор для текущей операции hello, созданной службой. |
| client-request-id |Строка |Идентификатор, указанный вызывающим hello в исходном запросе hello, если он имеется. |
| Дата |RFC 1123 date |Дата Hello, hello запрос был обработан. |
| Content-Type |Varies |Тип содержимого Hello hello текст ответа. |
| Content-Encoding |Varies |Соответственно, Gzip или Deflate. |

## <a name="standard-http-verbs-supported-by-media-services"></a>Стандартные HTTP-команды, поддерживаемые службами мультимедиа
Hello ниже приведен полный список HTTP-команд, которые могут использоваться при отправке запросов HTTP:

| Команда | Описание |
| --- | --- |
| ПОЛУЧЕНИЕ |Возвращает hello текущее значение объекта. |
| ПУБЛИКАЦИЯ |Создает объект на основе предоставленных данных hello или отправляет команду. |
| ОТПРАВКА |Заменяет объект или создает именованный объект (в зависимости от ситуации). |
| УДАЛИТЬ |Удаляет объект. |
| MERGE |Вносит в существующий объект изменения в именованном свойстве. |
| HEAD |Возвращает метаданные объекта для ответа GET. |

## <a name="discover-media-services-model"></a>Обнаружение модели служб мультимедиа
можно использовать toomake Media Services обнаружение объектов, операция hello $metadata. Позволяет tooretrieve все допустимые типы сущностей, свойства сущности, ассоциации, функций, действия и т. д. Hello следующем примере показано, как tooconstruct hello URI: https://media.windows.net/API/$ метаданных.

Должен добавлять «? api-version=2.x» toohello конец hello URI, если tooview hello метаданных в браузере или не включать заголовок x-ms-version hello в запрос.

## <a name="connect-toomedia-services"></a>Подключение служб tooMedia

Сведения о tooconnect toohello AMS API, в статье [hello доступа к API служб мультимедиа Azure с проверкой подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md). После успешного подключения toohttps://media.windows.net, будет получено перенаправление 301 указывающее другой URI служб Media Services. Необходимо внести toohello последующих вызовов новый URI.

## <a name="next-steps"></a>Дальнейшие действия

tooaccess AMS API-интерфейсы с REST, в разделе [tooaccess проверки подлинности используют Azure AD hello API служб мультимедиа Azure с ОСТАЛЬНОЙ](media-services-rest-connect-with-aad.md).

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

