---
title: "aaaAzure Cosmos DB .NET Core API пакета SDK ре & сурсов | Документы Microsoft"
description: "Узнайте о hello .NET Core API и пакета SDK, включая даты выхода, даты выбытия и изменения, выполняемые на каждой версии hello Azure Cosmos DB .NET Core SDK."
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
ms.openlocfilehash: 1269cafe0ea1caaa871404d507b12632dbb3ed82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
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

<tr><td>**Начало работы**</td><td>[Приступая к работе с hello Azure Cosmos DB .NET Core SDK](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td>**Учебник по веб-приложениям**</td><td>[Руководство по ASP.NET MVC. Разработка веб-приложений в Azure Cosmos DB](documentdb-dotnet-application.md)</td></tr>

<tr><td>**Текущая поддерживаемая платформа**</td><td>[.NET Standard 1.6 и .NET Standard 1.5](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a>Заметки о выпуске

Hello Azure Cosmos DB .NET Core SDK имеет функционального соответствия с последней версией hello hello [пакета SDK .NET Azure Cosmos DB](documentdb-sdk-dotnet.md).

> [!NOTE] 
> Hello Azure Cosmos DB .NET Core SDK не совместим с приложениями универсальной платформы Windows (UWP). Если вы заинтересованы в hello .NET Core SDK, который поддерживает приложения UWP, письмо слишком[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0 

* Добавлена поддержка PartitionKeyRangeId как FeedOption для определения областей значение диапазона ключей определенный раздел tooa результаты запроса. 
* Добавлена поддержка StartTime как toostart ChangeFeedOption, поиск hello изменения после указанного периода. 

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1

*   Устранена проблема в hello JsonSerializable класс, который может вызвать исключение переполнения стека.

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0

*   Добавлена поддержка для указания пользовательских параметров JsonSerializerSettings при создании экземпляра [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).

### <a name="a-name132132"></a><a name="1.3.2"/>1.3.2

*   Поддержка стандартных 1.5 .NET как один из hello целевые платформы.

### <a name="a-name131131"></a><a name="1.3.1"/>1.3.1

*   Устранена проблема, возникающая на компьютерах под управлением 64-разрядной ОС без поддержки инструкций SSE4, которая приводила к исключению SEHException при выполнении запросов Azure Cosmos DB.

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0

*   Добавлена поддержка нового уровня согласованности с именем ConsistentPrefix.
*   Добавлена поддержка запроса метрик отдельных секций.
*   Добавлена поддержка ограничений на размер hello hello токен продолжения для запросов.
*   Добавлена поддержка более подробной трассировки невыполненных запросов.
*   Внесены некоторые улучшения производительности в hello SDK.

### <a name="a-name122122"></a><a name="1.2.2"/>1.2.2

* Устранена проблема, учитываются значения PartitionKey hello, предоставляемая в FeedOptions статистические запросы.
* Устранена проблема, связанная с прозрачной обработкой управления при промежуточном выполнении запроса Order By между разделами.

### <a name="a-name121121"></a><a name="1.2.1"/>1.2.1

* Исправлена проблема, вызвавшая взаимоблокировок в некоторых hello асинхронные интерфейсы API при использовании внутри контекста ASP.NET.

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0

* Устраняет toomake SDK более устойчивым tooautomatic отработки отказа при определенных условиях.

### <a name="a-name112112"></a><a name="1.1.2"/>1.1.2

* Исправьте проблему, которая вызывает исключение WebException: не удалось разрешить имя удаленного hello.
* Добавлены hello поддержка непосредственно чтения типизированный документа, добавив новый API tooReadDocumentAsync перегрузки.

### <a name="a-name111111"></a><a name="1.1.1"/>1.1.1

* Добавлена поддержка LINQ для статистических запросов (COUNT, MIN, MAX, SUM и AVG).
* Исправьте проблему утечки памяти для объекта ConnectionPolicy hello, вызванные hello использование обработчика событий.
* Исправление ошибки, из-за которой метод UpsertAttachmentAsync не работал, когда использовался тег ETag.
* Исправление ошибки, из-за которой продолжение запросов orderBy между секциями не работало при сортировке по полю строки.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0

* Добавлена поддержка статистических запросов (COUNT, MIN, MAX, SUM и AVG). Дополнительные сведения см. в разделе [Статистические функции](documentdb-sql-query.md#Aggregates).
* Понижено минимальная пропускная способность для секционированных коллекций из 10,100 единиц Запросов в секунду too2500 единиц Запросов в секунду.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0

Hello Azure Cosmos DB .NET Core SDK позволяет быстро, toobuild кросс платформенных [ASP.NET Core](https://www.asp.net/core) и [.NET Core](https://www.microsoft.com/net/core#windows) toorun приложений в Windows, Mac и Linux. Hello последний выпуск hello Azure Cosmos DB .NET Core SDK является полностью [Xamarin](https://www.xamarin.com) совместимость и используется toobuild о приложениях, предназначенных для iOS, Android и моно (Linux).  

### <a name="a-name010-preview010-preview"></a><a name="0.1.0-preview"/>0.1.0-preview

Hello предварительной версии Azure Cosmos DB .NET Core SDK позволяет быстро, toobuild кросс платформенных [ASP.NET Core](https://www.asp.net/core) и [.NET Core](https://www.microsoft.com/net/core#windows) toorun приложений в Windows, Mac и Linux.

Hello Azure Cosmos DB .NET Core Preview SDK имеет функционального соответствия с последней версией hello hello [пакета SDK .NET Azure Cosmos DB](documentdb-sdk-dotnet.md) и поддерживает hello ниже:
* все [режимы подключения](performance-tips.md#networking): режим шлюза, прямые TCP- и HTTP-подключения; 
* все [уровни согласованности](consistency-levels.md): строгая, ограниченное устаревание, согласованность сеанса, окончательная;
* [секционированные коллекции](partition-data.md); 
* [георепликация данных и межрегиональные учетные записи баз данных](distribute-data-globally.md).

Если у вас есть вопросы связанные toothis SDK, учет слишком[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), или файл проблему в hello [репозитории github](https://github.com/Azure/azure-documentdb-dotnet/issues). 

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
toolearn Дополнительные сведения о Cosmos DB. в разделе [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) страницы службы. 

