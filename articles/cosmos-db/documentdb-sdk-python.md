---
title: "aaaAzure Cosmos DB Python API пакета SDK ре & сурсов | Документы Microsoft"
description: "Узнайте о hello Python API и SDK, включая даты выхода, даты выбытия и изменения, выполняемые на каждой версии пакета SDK для Python DB Cosmos Azure hello."
services: cosmos-db
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/24/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1a164b72d2bd819de87df0229357b82e2177af2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a>Пакет SDK для Azure Cosmos DB на Python: заметки о выпуске и ресурсы
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

<tr><td>**Скачать пакет SDK**</td><td>[PyPI](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td>**Документация по API**</td><td>[Справочная документация по API Python](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td>**Инструкции по установке пакета SDK**</td><td>[Инструкции по установке пакета SDK для Python](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td>**Contribute tooSDK**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td>**Начало работы**</td><td>[Начало работы с Python SDK hello](documentdb-python-application.md)</td></tr>

<tr><td>**Текущая поддерживаемая платформа**</td><td>[Python 2.7](https://www.python.org/downloads/) и [Python 3.5](https://www.python.org/downloads/)</td></tr>
</table></br>

## <a name="release-notes"></a>Заметки о выпуске
### <a name="a-name220220"></a><a name="2.2.0"/>2.2.0
* Добавлена поддержка нового уровня согласованности с именем ConsistentPrefix.


### <a name="a-name210210"></a><a name="2.1.0"/>2.1.0
* Добавлена поддержка статистических запросов (COUNT, MIN, MAX, SUM и AVG).
* Добавлена возможность отключения проверки SSL при работе с эмулятором Cosmos DB.
* Удалено ограничение hello из зависимых запросов модуля toobe точно 2.10.0.
* Понижено минимальная пропускная способность для секционированных коллекций из 10,100 единиц Запросов в секунду too2500 единиц Запросов в секунду.
* Добавлена поддержка включения ведения журнала сценариев во время выполнения хранимой процедуры.
* Увеличить версию API-интерфейса REST один слишком "2017 г-01-19' в этом выпуске.

### <a name="a-name201201"></a><a name="2.0.1"/>2.0.1
* Внесены редакторские изменения toodocumentation комментарии.

### <a name="a-name200200"></a><a name="2.0.0"/>2.0.0
* Добавлена поддержка Python 3.5.
* Добавлена поддержка пулов подключений с использованием модуля запросов.
* Добавлена поддержка согласованности сеанса.
* Добавлена поддержка запросов TOP и ORDERBY для секционированных коллекций.

### <a name="a-name190190"></a><a name="1.9.0"/>1.9.0
* Добавлена поддержка политики повтора для отрегулированных запросов. (Отрегулированные запросы порождают исключение слишком высокой частоты запросов с кодом ошибки 429.) По умолчанию Azure Cosmos DB повторяет девяти раз для каждого запроса при обнаружении код ошибки 429, учитывая время retryAfter hello в заголовке ответа hello. Интервал повторных попыток основных теперь настраивается как часть hello свойство RetryOptions hello объекта ConnectionPolicy время tooignore hello retryAfter сервер вернул между повторными попытками hello. Теперь Azure Cosmos DB ожидает в течение не более 30 секунд для каждого запроса, который регулируется (независимо от того, число повторных попыток) и возвращает hello ответ с кодом ошибки 429. Это время также может быть переопределен в hello RetryOptions свойство ConnectionPolicy объекта.
* Cosmos DB теперь возвращает x-ms регулирования число повторных попыток и x-ms-throttle-retry-wait-time-ms как заголовки ответа hello в каждый интервал повтора запроса toodenote hello count и hello cummulative время повтора запроса hello ожидания между повторными попытками hello.
* Класс RetryPolicy удален hello и соответствующего свойства hello (retry_policy) для класса document_client hello и вместо этого реализован RetryOptions класса, предоставляющего свойства RetryOptions hello ConnectionPolicy класс, который может быть используется toooverride по умолчанию hello некоторые параметры повторных попыток.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Hello добавлена поддержка учетные записи базы данных с поддержкой нескольких регионов.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Hello добавлена поддержка функция tooLive(TTL) времени для документов.

### <a name="a-name161161"></a><a name="1.6.1"/>1.6.1
* Исправления ошибок, связанных с tooserver стороне секционирование tooallow специальные символы в пути partitionkey.

### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0
* Реализованы [секционированные коллекции](partition-data.md) и [определяемые пользователем уровни производительности](performance-levels.md). 

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Добавить диапазон & хеширования tooassist распознаватели секции с приложениями сегментирования по нескольким секциям.

### <a name="a-name142142"></a><a name="1.4.2"/>1.4.2
* Реализована операция Upsert. Новые методы UpsertXXX добавлена функция toosupport Upsert.
* Реализована маршрутизация на основе идентификатора. Отсутствуют изменения общего API-интерфейса. Все изменения касаются внутреннего интерфейса.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Поддержка геопространственного индекса.
* Проверка свойств идентификатора для всех ресурсов. Идентификаторы ресурсов не могут содержать знаки ?, /, #, \, или заканчиваться пробелом.
* Добавляет новый tooResourceResponse заголовок «выполняется преобразование индекса».

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Реализована политика индексации версии 2.

### <a name="a-name101101"></a><a name="1.0.1"/>1.0.1
* Добавлена поддержка прокси-подключения.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* Пакет SDK общей доступности.

## <a name="release--retirement-dates"></a>Даты выпуска и вывода из эксплуатации
Корпорация Майкрософт предоставляет уведомления по крайней мере **12 месяцев** до снятия с учета в новой/поддерживаемой версии для hello перехода порядок toosmooth tooa пакет SDK.

Новые функции и функциональные возможности и оптимизацию добавляются только toohello текущего пакета SDK, поэтому рекомендуется как можно раньше, вы всегда обновления toohello последнюю версию пакета SDK. 

Любой запрос tooCosmos базу данных, используя удалено SDK будут отклонены службой hello.

> [!WARNING]
> Все версии hello Azure DocumentDB SDK для Python предыдущих tooversion **1.0.0** будет удалено на **29 февраля 2016 г.**. 
> 
> 

<br/>

| Version (версия) | Дата выпуска | Дата вывода |
| --- | --- | --- |
| [2.2.0](#2.2.0) |10 мая 2017 г. |--- |
| [2.1.0](#2.1.0) |1 мая 2017 г. |--- |
| [2.0.1](#2.0.1) |30 октября 2016 г. |--- |
| [2.0.0](#2.0.0) |29 сентября 2016 г. |--- |
| [1.9.0](#1.9.0) |7 июля 2016 г. |--- |
| [1.8.0](#1.8.0) |14 июня 2016 г. |--- |
| [1.7.0](#1.7.0) |26 апреля 2016 г. |--- |
| [1.6.1](#1.6.1) |8 апреля 2016 г. |--- |
| [1.6.0](#1.6.0) |29 марта 2016 г. |--- |
| [1.5.0](#1.5.0) |3 января 2016 г. |--- |
| [1.4.2](#1.4.2) |6 октября 2015 г. |--- |
| [1.4.1](#1.4.1) |6 октября 2015 г. |--- |
| [1.2.0](#1.2.0) |6 августа 2015 г. |--- |
| [1.1.0](#1.1.0) |9 июля 2015 г. |--- |
| [1.0.1](#1.0.1) |25 мая 2015 г. |--- |
| [1.0.0](#1.0.0) |7 апреля 2015 г. |--- |
| 0.9.4-prelease |14 января 2015 г. |29 февраля 2016 г. |
| 0.9.3-prelease |9 декабря 2014 г. |29 февраля 2016 г. |
| 0.9.2-prelease |25 ноября 2014 г. |29 февраля 2016 г. |
| 0.9.1-prelease |23 сентября 2014 г. |29 февраля 2016 г. |
| 0.9.0-prelease |21 августа 2014 г. |29 февраля 2016 г. |

## <a name="faq"></a>Часто задаваемые вопросы
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>См. также
toolearn Дополнительные сведения о Cosmos DB. в разделе [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) страницы службы. 

