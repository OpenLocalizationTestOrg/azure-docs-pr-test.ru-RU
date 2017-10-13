---
title: "Обзор REST API операций служб мультимедиа | Документация Майкрософт"
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
ms.openlocfilehash: eada8f2bcd2488d5ed36b0c24aa3d1b917815517
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="media-services-operations-rest-api-overview"></a>Обзор REST API операций служб мультимедиа
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

**REST API операций служб мультимедиа** используется для создания заданий, ресурсов, политик доступа и других операций с объектами в учетной записи службы мультимедиа. Дополнительные сведения см. в статье [Media Services Operations REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference) (Справочник по REST API операций служб мультимедиа).

Службы мультимедиа Microsoft Azure — это службы, которые принимают HTTP-запросы на основе OData и могут отвечать с использованием подробного формата JSON или atom+pub. Так как службы мультимедиа соответствуют правилам проектирования Azure, для них предусмотрен набор обязательных HTTP-заголовков, которые каждый клиент должен использовать при подключении к службам мультимедиа, а также набор дополнительных заголовков, которые можно использовать при необходимости. В следующих разделах описываются заголовки и HTTP-команды, которые можно использовать при создании запросов и получения ответов из служб мультимедиа.

Эта статья содержит общие сведения об использовании REST v2 со службами мультимедиа.

## <a name="considerations"></a>Рекомендации

При использовании REST следует принимать во внимание следующие соображения.

* При запросе сущностей существует ограничение в 1000 сущностей, возвращаемых за один раз, так как в открытой версии 2 REST количество результатов запросов ограничено 1000. Используйте **Skip** и **Take** (.NET) или **top** (REST), как описано в [этом](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) и [этом](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities) примерах. 
* Если вы используете JSON и указываете в запросе ключевое слово **__metadata** (например, для ссылки на связанный объект), вы ДОЛЖНЫ задать для заголовка **Accept** [подробный (Verbose) формат JSON](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/) (см. пример ниже). Odata "не поймет" свойство **__metadata** в запросе, если не задать для него подробный формат.  
  
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
Для каждого вызова, отправляемого в службы мультимедиа, предусмотрен набор обязательных заголовков, которые необходимо включить в запрос, а также набор дополнительных заголовков, которые можно включить при необходимости. Обязательные заголовки перечислены в следующей таблице:

| Заголовок | Тип | Значение |
| --- | --- | --- |
| Авторизация |Носитель |Носитель – единственный принимаемый механизм авторизации. Значение должно содержать маркер доступа, предоставленный службой ACS. |
| x-ms-version |Decimal |2.11 |
| DataServiceVersion |Decimal |3.0 |
| MaxDataServiceVersion |Decimal |3.0 |

> [!NOTE]
> Так как службы мультимедиа используют OData для предоставления своего базового репозитория метаданных ресурсов через REST API, заголовки DataServiceVersion и MaxDataServiceVersion должны быть включены во все запросы. Тем не менее, если они отсутствуют, в настоящее время в службах мультимедиа предполагается, что для DataServiceVersion используется значение 3.0.
> 
> 

Ниже приведен набор дополнительных заголовков.

| Заголовок | Тип | Значение |
| --- | --- | --- |
| Дата |RFC 1123 date |Метка времени запроса |
| Принять |Тип содержимого |Запрошенный тип содержимого для ответа, например:<p> application/json;odata=verbose<p> application/atom+xml<p> Ответы могут принадлежать к разным типам содержимого, например при получении больших двоичных объектов полезными данными в успешном ответе будет поток больших двоичных объектов. |
| Accept-Encoding |Gzip, deflate |Кодировка GZIP и, в соответствующих случаях, DEFLATE. Примечание. Для больших ресурсов службы мультимедиа могут пропустить этот заголовок и вернуть несжатые данные. |
| Accept-Language |"en", "ru" и т. д. |Указывает предпочитаемый язык для ответа. |
| Accept-Charset |Тип кодировки, например "UTF-8" |По умолчанию — UTF-8. |
| X-HTTP-Method |Метод HTTP |Позволяет клиентам или брандмауэрам, которые не поддерживают методы HTTP, например PUT или DELETE, использовать эти методы, туннелированные посредством вызова GET. |
| Content-Type |Тип содержимого |Тип содержимого текста запросов PUT или POST. |
| client-request-id |Строка |Определяемое вызывающим объектом значение, по которому можно идентифицировать данный запрос. Если это значение указано, оно будет включено в ответное сообщении в качестве способа сопоставления запроса. <p><p>**Важно!**<p>Значения должны превышать 2096 Б (2 КБ). |

## <a name="standard-http-response-headers-supported-by-media-services"></a>Стандартные ответы HTTP-запроса, поддерживаемые службами мультимедиа
Ниже приведен набор заголовков, которые могут быть возвращены в зависимости от запрошенного ресурса и действия, которое необходимо выполнить.

| Заголовок | Тип | Значение |
| --- | --- | --- |
| request-id |Строка |Уникальный идентификатор текущей операции, создаваемый службой. |
| client-request-id |Строка |Идентификатор, указанный вызывающим объектом в исходном запросе, если он имеется. |
| Дата |RFC 1123 date |Дата обработки запроса. |
| Content-Type |Varies |Тип содержимого текста ответа. |
| Content-Encoding |Varies |Соответственно, Gzip или Deflate. |

## <a name="standard-http-verbs-supported-by-media-services"></a>Стандартные HTTP-команды, поддерживаемые службами мультимедиа
Ниже приведен полный список HTTP-команд, которые могут использоваться при создании HTTP-запросов:

| Команда | Описание |
| --- | --- |
| ПОЛУЧЕНИЕ |Возвращает текущее значение объекта. |
| ПУБЛИКАЦИЯ |Создает объект на основе предоставленных данных или отправляет команду. |
| ОТПРАВКА |Заменяет объект или создает именованный объект (в зависимости от ситуации). |
| УДАЛИТЬ |Удаляет объект. |
| MERGE |Вносит в существующий объект изменения в именованном свойстве. |
| HEAD |Возвращает метаданные объекта для ответа GET. |

## <a name="discover-media-services-model"></a>Обнаружение модели служб мультимедиа
Чтобы упростить обнаружение сущностей служб мультимедиа, можно использовать операцию $metadata. Она позволяет получать все допустимые типы сущностей, свойства сущностей, ассоциации, функции, действия и т. д. Вот пример формирования универсального кода ресурса (URI): https://media.windows.net/API/$metadata.

Чтобы метаданные можно было просмотреть в браузере, в конце универсального кода ресурса необходимо добавить выражение "?api-version=2.x" или не включать в запрос заголовок x-ms-version.

## <a name="connect-to-media-services"></a>Подключение к службам мультимедиа

Сведения о подключении к API AMS см. в разделе [Доступ к API служб мультимедиа Azure с помощью аутентификации Azure AD](media-services-use-aad-auth-to-access-ams-api.md). После успешного подключения к https://media.windows.net вы получите ошибку 301 (перенаправление), в которой будет указан другой URI служб мультимедиа. Используйте для последующих вызовов новый URI.

## <a name="next-steps"></a>Дальнейшие действия

Чтобы получить доступ к API AMS с помощью REST, см. статью [Использование аутентификации Azure AD для доступа к API служб мультимедиа Azure с помощью .NET](media-services-rest-connect-with-aad.md).

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

