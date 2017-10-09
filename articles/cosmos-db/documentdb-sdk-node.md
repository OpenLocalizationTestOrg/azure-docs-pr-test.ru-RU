---
title: "aaaAzure Cosmos DB Node.js API, пакет SDK ре & сурсов | Документы Microsoft"
description: "Узнайте о hello Node.js API и пакет SDK, включая даты выхода, даты выбытия и изменения, выполняемые на каждой версии пакета SDK для Node.js DB Cosmos Azure hello."
services: cosmos-db
documentationcenter: nodejs
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 9d5621fa-0e11-4619-a28b-a19d872bcf37
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d450b9a9ea7b0f4717ddae8940121fc458ea3744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a>Пакет SDK Node.js для Azure Cosmos DB: заметки о выпуске и ресурсы
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [Веб-канал изменений в .NET](documentdb-sdk-dotnet-changefeed.md)
> * [.NET Core](documentdb-sdk-dotnet-core.md)
> * [Node.js](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/documentdb/)
> * [Поставщик ресурсов REST](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td>**Скачать пакет SDK**</td><td>[NPM](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td>**Документация по API**</td><td>[Справочная документация по API Node.js](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td>**Инструкции по установке пакета SDK**</td><td>[Инструкции по установке](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td>**Contribute tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td>**Примеры**</td><td>[Примеры кода Node.js](documentdb-nodejs-samples.md)</td></tr>

<tr><td>**Учебник по началу работы**</td><td>[Приступая к работе с hello пакет SDK для Node.js](documentdb-nodejs-get-started.md)</td></tr>

<tr><td>**Учебник по веб-приложениям**</td><td>[Создание веб-приложения Node.js с использованием Azure Cosmos DB](documentdb-nodejs-application.md)</td></tr>

<tr><td>**Текущая поддерживаемая платформа**</td><td> 
[Node.js v6.x](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[Node.js версии 4.2.0](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[Node.js версии 0.12](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</td></tr>
</table></br>

## <a name="release-notes"></a>Заметки о выпуске

### <a name="1.12.2"/>1.12.2</a>
*   Исправлена документация npm.

### <a name="1.12.1"/>1.12.1</a>
* Исправлена ошибка в executeStoredProcedure, где документы содержали специальные символы Юникода (LS, PS).
* Исправлена ошибка при обработке документов с использованием символов Юникода в ключ раздела hello.
* Фиксированный поддержку для создания коллекций с hello имя носителя. Проблема GitHub 114.
* Исправлена поддержка маркера авторизации разрешений. Проблема GitHub 178.

### <a name="1.12.0"/>1.12.0</a>
* Добавлена поддержка нового [уровня согласованности](consistency-levels.md) с именем ConsistentPrefix.
* Добавлена поддержка UriFactory.
* Исправлена ошибка поддержки Юникода. Проблема GitHub 171.

### <a name="1.11.0"/>1.11.0</a>
* Hello добавлена поддержка статистических запросов (COUNT, MIN, MAX, SUM и AVG).
* Добавлены hello режим управления степень параллелизма для кросс-запросы секций.
* Hello добавлен параметр для отключения проверки SSL при работе с Azure Cosmos DB эмулятора.
* Понижено минимальная пропускная способность для секционированных коллекций из 10,100 единиц Запросов в секунду too2500 единиц Запросов в секунду.
* Фиксированный hello продолжение токена ошибки для коллекции одну секцию. Проблема GitHub 107.
* Ошибка executeStoredProcedure основных hello в обработке 0 как один параметр. Проблема GitHub 155.

### <a name="1.10.2"/>1.10.2</a>
* Версия пакета SDK hello tooinclude заголовок основных агента пользователя.
* Дополнительная очистка кода.

### <a name="1.10.1"/>1.10.1</a>
* Отключение проверки SSL, при использовании hello SDK tootarget hello emulator(hostname=localhost).
* Добавлена поддержка включения ведения журнала сценариев во время выполнения хранимой процедуры.

### <a name="1.10.0"/>1.10.0</a>
* Добавлена поддержка параллельных запросов между секциями.
* Добавлена поддержка запросов TOP и ORDER BY для секционированных коллекций.

### <a name="1.9.0"/>1.9.0</a>
* Добавлена поддержка политики повтора для отрегулированных запросов. (Отрегулированные запросы порождают исключение слишком высокой частоты запросов с кодом ошибки 429.) По умолчанию Azure Cosmos DB повторяет девяти раз для каждого запроса при обнаружении код ошибки 429, учитывая время retryAfter hello в заголовке ответа hello. Интервал повторных попыток основных теперь настраивается как часть hello свойство RetryOptions hello объекта ConnectionPolicy время tooignore hello retryAfter сервер вернул между повторными попытками hello. Теперь Azure Cosmos DB ожидает в течение не более 30 секунд для каждого запроса, который регулируется (независимо от того, число повторных попыток) и возвращает hello ответ с кодом ошибки 429. Это время также могут переопределяться в hello RetryOptions свойство ConnectionPolicy объекта.
* Cosmos DB теперь возвращает x-ms регулирования число повторных попыток и x-ms-throttle-retry-wait-time-ms как заголовки ответа hello в каждый интервал повтора запроса toodenote hello count и hello совокупное время повтора запроса hello ожидания между повторными попытками hello.
* был добавлен класс RetryOptions Hello, предоставление доступа к свойству RetryOptions hello hello ConnectionPolicy класса, который может быть используется toooverride некоторые по умолчанию hello параметры повторных попыток.

### <a name="1.8.0"/>1.8.0</a>
* Hello добавлена поддержка учетные записи базы данных с поддержкой нескольких регионов.

### <a name="1.7.0"/>1.7.0</a>
* Hello добавлена поддержка функция tooLive(TTL) времени для документов.

### <a name="1.6.0"/>1.6.0</a>
* Реализованы [секционированные коллекции](partition-data.md) и [определяемые пользователем уровни производительности](performance-levels.md).

### <a name="1.5.6"/>1.5.6</a>
* Исправлена ошибка RangePartitionResolver.resolveForRead, где он не возвращали ссылки из-за поврежденных concat tooa результатов.

### <a name="1.5.5"/>1.5.5</a>
* Исправлена ошибка метода resolveForRead() hashParitionResolver. Ранее вместо возврата списка всех зарегистрированных ссылок при отсутствии ключа раздела вызвалось исключение.

### <a name="1.5.4"/>1.5.4</a>
* Устраняет проблему, [#100](https://github.com/Azure/azure-documentdb-node/issues/100) -выделенной агента HTTPS: избегать изменения глобального агента hello целях Azure Cosmos DB. Используйте выделенный агента для всех запросов hello lib.

### <a name="1.5.3"/>1.5.3</a>
* Устранена проблема [№ 81](https://github.com/Azure/azure-documentdb-node/issues/81). Правильная обработка тире в идентификаторах носителей.

### <a name="1.5.2"/>1.5.2</a>
* Устранена проблема [№ 95](https://github.com/Azure/azure-documentdb-node/issues/95). Предупреждение об утечке данных прослушивателя EventEmitter.

### <a name="1.5.1"/>1.5.1</a>
* Устраняет проблему, [#92](https://github.com/Azure/azure-documentdb-node/issues/90) -переименовать папку toohash хэш для систем с учетом регистра.

### <a name="1.5.0"/>1.5.0</a>
* Реализация поддержки сегментирования за счет добавления сопоставителей секций хэша и диапазона.

### <a name="1.4.0"/>1.4.0</a>
* Реализована операция Upsert. Новые методы upsertXXX в documentClient.

### <a name="1.3.0"/>1.3.0</a>
* Пропущена toobring номера версий, согласованные с других пакетов SDK.

### <a name="1.2.2"/>1.2.2</a>
* Вопросы разбиения обещания репозитория toonew программы-оболочки.
* Обновите файл toopackage для реестра npm.

### <a name="1.2.1"/>1.2.1</a>
* Реализована маршрутизация на основе идентификатора.
* Устранена проблема [№ 49](https://github.com/Azure/azure-documentdb-node/issues/49) : конфликт текущего свойства с методом current().

### <a name="1.2.0"/>1.2.0</a>
* Добавлена поддержка геопространственного индекса.
* Проверка свойств идентификатора для всех ресурсов. Идентификаторы ресурсов не могут содержать символы ?, /, #, &#47;&#47; или заканчиваться пробелом.
* Добавляет новый tooResourceResponse заголовок «выполняется преобразование индекса».

### <a name="1.1.0"/>1.1.0</a>
* Реализована политика индексации версии 2.

### <a name="1.0.3"/>1.0.3</a>
* Проблема [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - реализации eslint grunt конфигурации ядра hello и promise SDK.

### <a name="1.0.2"/>1.0.2</a>
* Устранена проблема [№ 45](https://github.com/Azure/azure-documentdb-node/issues/45) — оболочка обещаний больше не включает заголовок с ошибкой.

### <a name="1.0.1"/>1.0.1</a>
* Реализована возможность tooquery конфликтов, добавляя readConflicts, readConflictAsync и queryConflicts.
* Обновлена документация по API.
* Проблема [№41](https://github.com/Azure/azure-documentdb-node/issues/41) — ошибка client.createDocumentAsync.

### <a name="1.0.0"/>1.0.0</a>
* Пакет SDK общей доступности.

## <a name="release--retirement-dates"></a>Даты выпуска и выбытия
Корпорация Майкрософт предоставляет уведомления по крайней мере **12 месяцев** до снятия с учета в новой/поддерживаемой версии для hello перехода порядок toosmooth tooa пакет SDK.

Новые функции и функциональные возможности и оптимизацию добавляются только toohello текущего пакета SDK, таким образом, рекомендуется, вы всегда обновления toohello последнюю версию пакета SDK как можно раньше.

Любой запрос, который является tooCosmos базу данных, используя удалено SDK отклонены службой hello.

<br/>

| Version (версия) | Дата выпуска | Дата вывода |
| --- | --- | --- |
| [1.12.2](#1.12.2) |10 августа 2017 г. |--- |
| [1.12.1](#1.12.1) |10 августа 2017 г. |--- |
| [1.12.0](#1.12.0) |10 мая 2017 г. |--- |
| [1.11.0](#1.11.0) |16 марта 2017 г. |--- |
| [1.10.2](#1.10.2) |27 января 2017 г. |--- |
| [1.10.1](#1.10.1) |22 декабря 2016 г. |--- |
| [1.10.0](#1.10.0) |3 октября 2016 г. |--- |
| [1.9.0](#1.9.0) |7 июля 2016 г. |--- |
| [1.8.0](#1.8.0) |14 июня 2016 г. |--- |
| [1.7.0](#1.7.0) |26 апреля 2016 г. |--- |
| [1.6.0](#1.6.0) |29 марта 2016 г. |--- |
| [1.5.6](#1.5.6) |8 марта 2016 г. |--- |
| [1.5.5](#1.5.5) |2 февраля 2016 г. |--- |
| [1.5.4](#1.5.4) |1 февраля 2016 г. |--- |
| [1.5.2](#1.5.2) |26 января 2016 г. |--- |
| [1.5.2](#1.5.2) |22 января 2016 г. |--- |
| [1.5.1](#1.5.1) |4 января 2016 г. |--- |
| [1.5.0](#1.5.0) |31 декабря 2015 г. |--- |
| [1.4.0](#1.4.0) |6 октября 2015 г. |--- |
| [1.3.0](#1.3.0) |6 октября 2015 г. |--- |
| [1.2.2](#1.2.2) |10 сентября 2015 г. |--- |
| [1.2.1](#1.2.1) |15 августа 2015 г. |--- |
| [1.2.0](#1.2.0) |5 августа 2015 г. |--- |
| [1.1.0](#1.1.0) |9 июля 2015 г. |--- |
| [1.0.3](#1.0.3) |4 июня 2015 г. |--- |
| [1.0.2](#1.0.2) |23 мая, 2015 г. |--- |
| [1.0.1](#1.0.1) |15 мая 2015 г. |--- |
| [1.0.0](#1.0.0) |8 апреля 2015 г. |--- |

## <a name="faq"></a>Часто задаваемые вопросы
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>См. также
toolearn Дополнительные сведения о Cosmos DB. в разделе [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) страницы службы.

