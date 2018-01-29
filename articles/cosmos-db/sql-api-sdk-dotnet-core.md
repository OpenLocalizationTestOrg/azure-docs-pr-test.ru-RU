---
title: "Azure Cosmos DB: API Core .NET для SQL SDK и ресурсы | Документы Microsoft"
description: "Дополнительные сведения о SQL .NET Core API и SDK, включая даты выхода, даты выбытия и изменения, выполняемые на каждой версии пакета SDK Azure Cosmos DB .NET Core."
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: f899b314-26ac-4ddb-86b2-bfdf05c2abf2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/17/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f8e3e0e8868c05188d9d6cb26fe6c2bd2891c17d
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/18/2017
---
# <a name="azure-cosmos-db-net-core-sdk-for-sql-api-release-notes-and-resources"></a>Azure SDK Cosmos DB .NET Core для API-Интерфейсы SQL: заметки о выпуске и ресурсы
> [!div class="op_single_selector"]
> * [.NET](sql-api-sdk-dotnet.md)
> * [Веб-канал изменений в .NET](sql-api-sdk-dotnet-changefeed.md)
> * [.NET Core](sql-api-sdk-dotnet-core.md)
> * [Node.js](sql-api-sdk-node.md)
> * [Java](sql-api-sdk-java.md)
> * [Python](sql-api-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/documentdb/)
> * [Поставщик ресурсов REST](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

[!INCLUDE [cosmos-db-sql-api](../../includes/cosmos-db-sql-api.md)]

<table>

<tr><td>**Скачивание пакета SDK**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td>**Документация по API**</td><td>[Справочная документация по API .NET](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td>**Примеры**</td><td>[Примеры кода для .NET](sql-api-dotnet-samples.md)</td></tr>

<tr><td>**Начало работы**</td><td>[Azure Cosmos DB. Приступая к работе с API DocumentDB и .NET Core](sql-api-dotnetcore-get-started.md)</td></tr>

<tr><td>**Учебник по веб-приложениям**</td><td>[Руководство по ASP.NET MVC. Разработка веб-приложений в Azure Cosmos DB](sql-api-dotnet-application.md)</td></tr>

<tr><td>**Текущая поддерживаемая платформа**</td><td>[.NET Standard 1.6 и .NET Standard 1.5](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a>Заметки о выпуске

Пакет SDK .NET Core для Azure Cosmos DB функционально полностью эквивалентен последней версии [пакета SDK .NET для Azure Cosmos DB](sql-api-sdk-dotnet.md).

> [!NOTE] 
> Пакет SDK .NET Core для Azure Cosmos DB пока несовместим с приложениями универсальной платформы Windows (UWP). Чтобы получить пакет SDK для .NET Core, который поддерживает приложения UWP, отправьте сообщение по адресу [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

### <a name="a-name171171"></a><a name="1.7.1"/>1.7.1
 
 * Добавлена возможность указывать уникальные индексы для документов с помощью применения свойства UniqueKeyPolicy к коллекции DocumentCollection.
 * Исправлена ошибка, когда пользовательские параметры JsonSerializer не учитывались при выполнении некоторых запросов и хранимых процедур.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
 
 * Изменена фирменная символика с Azure DocumentDB на Azure Cosmos DB в справочной документации по API, сведениях о метаданных в сборках и пакете NuGet. 
 * Предоставлены данные диагностики и сведения о задержке ответов на запросы, отправленные в режиме прямого соединения. Имена свойств: RequestDiagnosticsString и RequestLatency в классе ResourceResponse.
 * Для этой версии пакета SDK требуется последняя версия эмулятора Azure Cosmos DB. Ее можно скачать по адресу https://aka.ms/cosmosdb-emulator.
 
### <a name="a-name160160"></a><a name="1.6.0"/>1.6.0

* Добавлено несколько исправлений и улучшений для повышения надежности.

### <a name="a-name151151"></a><a name="1.5.1"/>1.5.1 

* Внутренние изменения, связанные с поддержкой [Microsoft.Azure.Graphs](https://docs.microsoft.com/azure/cosmos-db/graph-sdk-dotnet)

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0 

* Добавлена поддержка PartitionKeyRangeId как FeedOption для ограничения области результатов запроса определенным диапазоном ключа секции. 
* Добавлена поддержка StartTime как ChangeFeedOption для поиска изменений после указанного периода. 

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1

*   Устранена проблема в классе JsonSerializable, которая могла порождать исключение переполнения стека.

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0

*   Добавлена поддержка для указания пользовательских параметров JsonSerializerSettings при создании экземпляра [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).

### <a name="a-name132132"></a><a name="1.3.2"/>1.3.2

*   Поддержка .NET Standard 1.5 в качестве одной из требуемых версий .NET Framework.

### <a name="a-name131131"></a><a name="1.3.1"/>1.3.1

*   Устранена проблема, возникающая на компьютерах под управлением 64-разрядной ОС без поддержки инструкций SSE4, которая приводила к исключению SEHException при выполнении запросов Azure Cosmos DB.

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0

*   Добавлена поддержка нового уровня согласованности с именем ConsistentPrefix.
*   Добавлена поддержка запроса метрик отдельных секций.
*   Добавлена поддержка ограничения размера маркера продолжения запросов.
*   Добавлена поддержка более подробной трассировки невыполненных запросов.
*   Внесены некоторые улучшения производительности в пакет SDK.

### <a name="a-name122122"></a><a name="1.2.2"/>1.2.2

* Устранена проблема, когда не учитывалось значение PartitionKey в FeedOptions для статистических запросов.
* Устранена проблема, связанная с прозрачной обработкой управления при промежуточном выполнении запроса Order By между разделами.

### <a name="a-name121121"></a><a name="1.2.1"/>1.2.1

* Исправлена проблема, вызывавшая взаимоблокировки в некоторых асинхронных интерфейсах API при использовании в контексте ASP.NET.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0

* Исправления для повышения устойчивости пакета SDK к автоматической отработке отказа при определенных условиях.

### <a name="a-name112112"></a><a name="1.1.2"/>1.1.2

* Исправление ошибки, приводившей к исключению WebException: "Удаленное имя не удалось разрешить".
* Добавлена поддержка непосредственного считывания типизированного документа путем добавления новых перегрузок в API ReadDocumentAsync.

### <a name="a-name111111"></a><a name="1.1.1"/>1.1.1

* Добавлена поддержка LINQ для статистических запросов (COUNT, MIN, MAX, SUM и AVG).
* Исправление ошибки утечки памяти для объекта ConnectionPolicy, вызываемой использованием обработчика событий.
* Исправление ошибки, из-за которой метод UpsertAttachmentAsync не работал, когда использовался тег ETag.
* Исправление ошибки, из-за которой продолжение запросов orderBy между секциями не работало при сортировке по полю строки.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0

* Добавлена поддержка статистических запросов (COUNT, MIN, MAX, SUM и AVG). Дополнительные сведения см. в разделе [Статистические функции](sql-api-sql-query.md#Aggregates).
* Минимальная пропускная способность секционированных коллекций снижена с 10 100 ЕЗ/с до 2500 ЕЗ/с.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0

Пакет SDK .NET Core для Azure Cosmos DB позволяет создавать быстрые кроссплатформенные приложения [ASP.NET Core](https://www.asp.net/core) и [.NET Core](https://www.microsoft.com/net/core#windows) для Windows, Mac и Linux. Последний выпуск пакета SDK .NET Core для Azure Cosmos DB полностью совместим с [Хamarin](https://www.xamarin.com) и пригоден для создания приложений для iOS, Android и Mono (Linux).  

### <a name="a-name010-preview010-preview"></a><a name="0.1.0-preview"/>0.1.0-preview

Пакет SDK .NET Core для Azure Cosmos DB (предварительная версия) позволяет создавать быстрые кроссплатформенные приложения [ASP.NET Core](https://www.asp.net/core) и [.NET Core](https://www.microsoft.com/net/core#windows) для Windows, Mac и Linux.

Пакет SDK .NET Core для Azure Cosmos DB (предварительная версия) функционально полностью эквивалентен последней версии [пакета SDK .NET для Azure Cosmos DB](sql-api-sdk-dotnet.md) и поддерживает следующие возможности:
* все [режимы подключения](performance-tips.md#networking): режим шлюза, прямые TCP- и HTTP-подключения; 
* все [уровни согласованности](consistency-levels.md): строгая, ограниченное устаревание, согласованность сеанса, окончательная;
* [секционированные коллекции](partition-data.md); 
* [георепликация данных и межрегиональные учетные записи баз данных](distribute-data-globally.md).

Если у вас возникли вопросы об этом пакете SDK, опубликуйте их на форуме сайта [StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb) или сообщите о проблеме в [репозитории GitHub](https://github.com/Azure/azure-documentdb-dotnet/issues). 

## <a name="release--retirement-dates"></a>Даты выпуска и выбытия

| Version (версия) | Дата выпуска | Дата вывода |
| --- | --- | --- |
| [1.7.1](#1.7.1) |16 ноября 2017 г. |--- |
| [1.7.0](#1.7.0) |10 ноября 2017 г. |--- |
| [1.6.0](#1.6.0) |17 октября 2017 г. |--- |
| [1.5.1](#1.5.1) |2 октября 2017 г. |--- |
| [1.5.0](#1.5.0) |10 августа 2017 г. |--- | 
| [1.4.1](#1.4.1) |7 августа 2017 г. |--- |
| [1.4.0](#1.4.0) |2 августа 2017 г. |--- |
| [1.3.2](#1.3.2) |12 июня 2017 г. |--- |
| [1.3.1](#1.3.1) |23 мая 2017 г. |--- |
| [1.3.0](#1.3.0) |10 мая 2017 г. |--- |
| [1.2.2](#1.2.2) |19 апреля 2017 г. |--- |
| [1.2.1](#1.2.1) |29 марта 2017 г. |--- |
| [1.2.0](#1.2.0) |25 марта 2017 г. |--- |
| [1.1.2](#1.1.2) |20 марта 2017 г. |--- |
| [1.1.1](#1.1.1) |14 марта 2017 г. |--- |
| [1.1.0](#1.1.0) |16 февраля 2017 г. |--- |
| [1.0.0](#1.0.0) |21 декабря 2016 г. |--- |
| [0.1.0-preview](#0.1.0-preview) |15 ноября 2016 г. |31 декабря 2016 г. |

## <a name="see-also"></a>См. также
Дополнительные сведения о Cosmos DB см. на странице службы [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/). 

