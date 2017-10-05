---
title: "API-интерфейс, пакет SDK и ресурсы для .NET Core (Azure Cosmos DB) | Документация Майкрософт"
description: "Сведения об API-интерфейсе и пакете SDK для .NET Core, в том числе даты выхода, даты прекращения использования и внесенные изменения по каждой версии пакета SDK .NET Core для Azure Cosmos DB."
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
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a7ce4d771e9c655687f72f4b46c7405cf64aeb74
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a>Пакет SDK .NET Core для Azure Cosmos DB: заметки о выпуске и ресурсы
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

<tr><td>**Скачивание пакета SDK**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td>**Документация по API**</td><td>[Справочная документация по API .NET](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td>**Примеры**</td><td>[Примеры кода для .NET](documentdb-dotnet-samples.md)</td></tr>

<tr><td>**Приступая к работе**</td><td>[Azure Cosmos DB. Приступая к работе с API DocumentDB и .NET Core](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td>**Учебник по веб-приложениям**</td><td>[Руководство по ASP.NET MVC. Разработка веб-приложений в Azure Cosmos DB](documentdb-dotnet-application.md)</td></tr>

<tr><td>**Текущая поддерживаемая платформа**</td><td>[.NET Standard 1.6 и .NET Standard 1.5](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a>Заметки о выпуске

Пакет SDK .NET Core для Azure Cosmos DB функционально полностью эквивалентен последней версии [пакета SDK .NET для Azure Cosmos DB](documentdb-sdk-dotnet.md).

> [!NOTE] 
> Пакет SDK .NET Core для Azure Cosmos DB пока несовместим с приложениями универсальной платформы Windows (UWP). Чтобы получить пакет SDK для .NET Core, который поддерживает приложения UWP, отправьте сообщение по адресу [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

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

* Добавлена поддержка статистических запросов (COUNT, MIN, MAX, SUM и AVG). Дополнительные сведения см. в разделе [Статистические функции](documentdb-sql-query.md#Aggregates).
* Минимальная пропускная способность секционированных коллекций снижена с 10 100 ЕЗ/с до 2500 ЕЗ/с.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0

Пакет SDK .NET Core для Azure Cosmos DB позволяет создавать быстрые кроссплатформенные приложения [ASP.NET Core](https://www.asp.net/core) и [.NET Core](https://www.microsoft.com/net/core#windows) для Windows, Mac и Linux. Последний выпуск пакета SDK .NET Core для Azure Cosmos DB полностью совместим с [Хamarin](https://www.xamarin.com) и пригоден для создания приложений для iOS, Android и Mono (Linux).  

### <a name="a-name010-preview010-preview"></a><a name="0.1.0-preview"/>0.1.0-preview

Пакет SDK .NET Core для Azure Cosmos DB (предварительная версия) позволяет создавать быстрые кроссплатформенные приложения [ASP.NET Core](https://www.asp.net/core) и [.NET Core](https://www.microsoft.com/net/core#windows) для Windows, Mac и Linux.

Пакет SDK .NET Core для Azure Cosmos DB (предварительная версия) функционально полностью эквивалентен последней версии [пакета SDK .NET для Azure Cosmos DB](documentdb-sdk-dotnet.md) и поддерживает следующие возможности:
* все [режимы подключения](performance-tips.md#networking): режим шлюза, прямые TCP- и HTTP-подключения; 
* все [уровни согласованности](consistency-levels.md): строгая, ограниченное устаревание, согласованность сеанса, окончательная;
* [секционированные коллекции](partition-data.md); 
* [георепликация данных и межрегиональные учетные записи баз данных](distribute-data-globally.md).

Если у вас возникли вопросы об этом пакете SDK, опубликуйте их на форуме сайта [StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb) или сообщите о проблеме в [репозитории GitHub](https://github.com/Azure/azure-documentdb-dotnet/issues). 

## <a name="release--retirement-dates"></a>Даты выпуска и выбытия

| Version (версия) | Дата выпуска | Дата вывода |
| --- | --- | --- |
| [1.5.0](#1.5.0) |10 августа 2017 г. |--- | 
| [1.4.1](#1.4.1) |7 августа 2017 г. |--- |
| [1.4.0](#1.4.0) |2 августа 2017 г. |--- |
| [1.3.2](#1.3.2) |12 июня 2017 г. |--- |
| [1.3.1](#1.3.1) |23 мая 2017 г. |--- |
| [1.3.0](#1.3.0) |10 мая 2017 г. |--- |
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

