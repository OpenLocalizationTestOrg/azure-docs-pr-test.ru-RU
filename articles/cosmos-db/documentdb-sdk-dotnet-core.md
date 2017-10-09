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
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a><span data-ttu-id="041f1-103">Пакет SDK .NET Core для Azure Cosmos DB: заметки о выпуске и ресурсы</span><span class="sxs-lookup"><span data-stu-id="041f1-103">Azure Cosmos DB .NET Core SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="041f1-104">.NET</span><span class="sxs-lookup"><span data-stu-id="041f1-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="041f1-105">Веб-канал изменений в .NET</span><span class="sxs-lookup"><span data-stu-id="041f1-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="041f1-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="041f1-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="041f1-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="041f1-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="041f1-108">Java</span><span class="sxs-lookup"><span data-stu-id="041f1-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="041f1-109">Python</span><span class="sxs-lookup"><span data-stu-id="041f1-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="041f1-110">REST</span><span class="sxs-lookup"><span data-stu-id="041f1-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="041f1-111">Поставщик ресурсов REST</span><span class="sxs-lookup"><span data-stu-id="041f1-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="041f1-112">SQL</span><span class="sxs-lookup"><span data-stu-id="041f1-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="041f1-113">**Скачивание пакета SDK**</span><span class="sxs-lookup"><span data-stu-id="041f1-113">**SDK download**</span></span></td><td>[<span data-ttu-id="041f1-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="041f1-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td><span data-ttu-id="041f1-115">**Документация по API**</span><span class="sxs-lookup"><span data-stu-id="041f1-115">**API documentation**</span></span></td><td>[<span data-ttu-id="041f1-116">Справочная документация по API .NET</span><span class="sxs-lookup"><span data-stu-id="041f1-116">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="041f1-117">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="041f1-117">**Samples**</span></span></td><td>[<span data-ttu-id="041f1-118">Примеры кода для .NET</span><span class="sxs-lookup"><span data-stu-id="041f1-118">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="041f1-119">**Начало работы**</span><span class="sxs-lookup"><span data-stu-id="041f1-119">**Get started**</span></span></td><td>[<span data-ttu-id="041f1-120">Приступая к работе с hello Azure Cosmos DB .NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="041f1-120">Get started with hello Azure Cosmos DB .NET Core SDK</span></span>](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td><span data-ttu-id="041f1-121">**Учебник по веб-приложениям**</span><span class="sxs-lookup"><span data-stu-id="041f1-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="041f1-122">Руководство по ASP.NET MVC. Разработка веб-приложений в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="041f1-122">Web application development with Azure Cosmos DB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="041f1-123">**Текущая поддерживаемая платформа**</span><span class="sxs-lookup"><span data-stu-id="041f1-123">**Current supported framework**</span></span></td><td>[<span data-ttu-id="041f1-124">.NET Standard 1.6 и .NET Standard 1.5</span><span class="sxs-lookup"><span data-stu-id="041f1-124">.NET Standard 1.6 and .NET Standard 1.5</span></span>](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="041f1-125">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="041f1-125">Release Notes</span></span>

<span data-ttu-id="041f1-126">Hello Azure Cosmos DB .NET Core SDK имеет функционального соответствия с последней версией hello hello [пакета SDK .NET Azure Cosmos DB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="041f1-126">hello Azure Cosmos DB .NET Core SDK has feature parity with hello latest version of hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="041f1-127">Hello Azure Cosmos DB .NET Core SDK не совместим с приложениями универсальной платформы Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="041f1-127">hello Azure Cosmos DB .NET Core SDK is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="041f1-128">Если вы заинтересованы в hello .NET Core SDK, который поддерживает приложения UWP, письмо слишком[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="041f1-128">If you are interested in hello .NET Core SDK that does support UWP apps, send email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

### <a name="a-name150150"></a><span data-ttu-id="041f1-129"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="041f1-129"><a name="1.5.0"/>1.5.0</span></span> 

* <span data-ttu-id="041f1-130">Добавлена поддержка PartitionKeyRangeId как FeedOption для определения областей значение диапазона ключей определенный раздел tooa результаты запроса.</span><span class="sxs-lookup"><span data-stu-id="041f1-130">Added support for PartitionKeyRangeId as a FeedOption for scoping query results tooa specific partition key range value.</span></span> 
* <span data-ttu-id="041f1-131">Добавлена поддержка StartTime как toostart ChangeFeedOption, поиск hello изменения после указанного периода.</span><span class="sxs-lookup"><span data-stu-id="041f1-131">Added support for StartTime as a ChangeFeedOption toostart looking for hello changes after that time.</span></span> 

### <a name="a-name141141"></a><span data-ttu-id="041f1-132"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="041f1-132"><a name="1.4.1"/>1.4.1</span></span>

*   <span data-ttu-id="041f1-133">Устранена проблема в hello JsonSerializable класс, который может вызвать исключение переполнения стека.</span><span class="sxs-lookup"><span data-stu-id="041f1-133">Fixed an issue in hello JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="041f1-134"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="041f1-134"><a name="1.4.0"/>1.4.0</span></span>

*   <span data-ttu-id="041f1-135">Добавлена поддержка для указания пользовательских параметров JsonSerializerSettings при создании экземпляра [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="041f1-135">Added support for specifying custom JsonSerializerSettings while instantiating a [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) instance.</span></span>

### <a name="a-name132132"></a><span data-ttu-id="041f1-136"><a name="1.3.2"/>1.3.2</span><span class="sxs-lookup"><span data-stu-id="041f1-136"><a name="1.3.2"/>1.3.2</span></span>

*   <span data-ttu-id="041f1-137">Поддержка стандартных 1.5 .NET как один из hello целевые платформы.</span><span class="sxs-lookup"><span data-stu-id="041f1-137">Supporting .NET Standard 1.5 as one of hello target frameworks.</span></span>

### <a name="a-name131131"></a><span data-ttu-id="041f1-138"><a name="1.3.1"/>1.3.1</span><span class="sxs-lookup"><span data-stu-id="041f1-138"><a name="1.3.1"/>1.3.1</span></span>

*   <span data-ttu-id="041f1-139">Устранена проблема, возникающая на компьютерах под управлением 64-разрядной ОС без поддержки инструкций SSE4, которая приводила к исключению SEHException при выполнении запросов Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="041f1-139">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw SEHException when running Azure Cosmos DB queries.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="041f1-140"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="041f1-140"><a name="1.3.0"/>1.3.0</span></span>

*   <span data-ttu-id="041f1-141">Добавлена поддержка нового уровня согласованности с именем ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="041f1-141">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="041f1-142">Добавлена поддержка запроса метрик отдельных секций.</span><span class="sxs-lookup"><span data-stu-id="041f1-142">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="041f1-143">Добавлена поддержка ограничений на размер hello hello токен продолжения для запросов.</span><span class="sxs-lookup"><span data-stu-id="041f1-143">Added support for limiting hello size of hello continuation token for queries.</span></span>
*   <span data-ttu-id="041f1-144">Добавлена поддержка более подробной трассировки невыполненных запросов.</span><span class="sxs-lookup"><span data-stu-id="041f1-144">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="041f1-145">Внесены некоторые улучшения производительности в hello SDK.</span><span class="sxs-lookup"><span data-stu-id="041f1-145">Made some performance improvements in hello SDK.</span></span>

### <a name="a-name122122"></a><span data-ttu-id="041f1-146"><a name="1.2.2"/>1.2.2</span><span class="sxs-lookup"><span data-stu-id="041f1-146"><a name="1.2.2"/>1.2.2</span></span>

* <span data-ttu-id="041f1-147">Устранена проблема, учитываются значения PartitionKey hello, предоставляемая в FeedOptions статистические запросы.</span><span class="sxs-lookup"><span data-stu-id="041f1-147">Fixed an issue that ignored hello PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="041f1-148">Устранена проблема, связанная с прозрачной обработкой управления при промежуточном выполнении запроса Order By между разделами.</span><span class="sxs-lookup"><span data-stu-id="041f1-148">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name121121"></a><span data-ttu-id="041f1-149"><a name="1.2.1"/>1.2.1</span><span class="sxs-lookup"><span data-stu-id="041f1-149"><a name="1.2.1"/>1.2.1</span></span>

* <span data-ttu-id="041f1-150">Исправлена проблема, вызвавшая взаимоблокировок в некоторых hello асинхронные интерфейсы API при использовании внутри контекста ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="041f1-150">Fixed an issue which caused deadlocks in some of hello async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="041f1-151"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="041f1-151"><a name="1.2.0"/>1.2.0</span></span>

* <span data-ttu-id="041f1-152">Устраняет toomake SDK более устойчивым tooautomatic отработки отказа при определенных условиях.</span><span class="sxs-lookup"><span data-stu-id="041f1-152">Fixes toomake SDK more resilient tooautomatic failover under certain conditions.</span></span>

### <a name="a-name112112"></a><span data-ttu-id="041f1-153"><a name="1.1.2"/>1.1.2</span><span class="sxs-lookup"><span data-stu-id="041f1-153"><a name="1.1.2"/>1.1.2</span></span>

* <span data-ttu-id="041f1-154">Исправьте проблему, которая вызывает исключение WebException: не удалось разрешить имя удаленного hello.</span><span class="sxs-lookup"><span data-stu-id="041f1-154">Fix for an issue that occasionally causes a WebException: hello remote name could not be resolved.</span></span>
* <span data-ttu-id="041f1-155">Добавлены hello поддержка непосредственно чтения типизированный документа, добавив новый API tooReadDocumentAsync перегрузки.</span><span class="sxs-lookup"><span data-stu-id="041f1-155">Added hello support for directly reading a typed document by adding new overloads tooReadDocumentAsync API.</span></span>

### <a name="a-name111111"></a><span data-ttu-id="041f1-156"><a name="1.1.1"/>1.1.1</span><span class="sxs-lookup"><span data-stu-id="041f1-156"><a name="1.1.1"/>1.1.1</span></span>

* <span data-ttu-id="041f1-157">Добавлена поддержка LINQ для статистических запросов (COUNT, MIN, MAX, SUM и AVG).</span><span class="sxs-lookup"><span data-stu-id="041f1-157">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="041f1-158">Исправьте проблему утечки памяти для объекта ConnectionPolicy hello, вызванные hello использование обработчика событий.</span><span class="sxs-lookup"><span data-stu-id="041f1-158">Fix for a memory leak issue for hello ConnectionPolicy object caused by hello use of event handler.</span></span>
* <span data-ttu-id="041f1-159">Исправление ошибки, из-за которой метод UpsertAttachmentAsync не работал, когда использовался тег ETag.</span><span class="sxs-lookup"><span data-stu-id="041f1-159">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="041f1-160">Исправление ошибки, из-за которой продолжение запросов orderBy между секциями не работало при сортировке по полю строки.</span><span class="sxs-lookup"><span data-stu-id="041f1-160">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="041f1-161"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="041f1-161"><a name="1.1.0"/>1.1.0</span></span>

* <span data-ttu-id="041f1-162">Добавлена поддержка статистических запросов (COUNT, MIN, MAX, SUM и AVG).</span><span class="sxs-lookup"><span data-stu-id="041f1-162">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="041f1-163">Дополнительные сведения см. в разделе [Статистические функции](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="041f1-163">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="041f1-164">Понижено минимальная пропускная способность для секционированных коллекций из 10,100 единиц Запросов в секунду too2500 единиц Запросов в секунду.</span><span class="sxs-lookup"><span data-stu-id="041f1-164">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="041f1-165"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="041f1-165"><a name="1.0.0"/>1.0.0</span></span>

<span data-ttu-id="041f1-166">Hello Azure Cosmos DB .NET Core SDK позволяет быстро, toobuild кросс платформенных [ASP.NET Core](https://www.asp.net/core) и [.NET Core](https://www.microsoft.com/net/core#windows) toorun приложений в Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="041f1-166">hello Azure Cosmos DB .NET Core SDK enables you toobuild fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps toorun on Windows, Mac, and Linux.</span></span> <span data-ttu-id="041f1-167">Hello последний выпуск hello Azure Cosmos DB .NET Core SDK является полностью [Xamarin](https://www.xamarin.com) совместимость и используется toobuild о приложениях, предназначенных для iOS, Android и моно (Linux).</span><span class="sxs-lookup"><span data-stu-id="041f1-167">hello latest release of hello Azure Cosmos DB .NET Core SDK is fully [Xamarin](https://www.xamarin.com) compatible and be used toobuild applications that target iOS, Android, and Mono (Linux).</span></span>  

### <a name="a-name010-preview010-preview"></a><span data-ttu-id="041f1-168"><a name="0.1.0-preview"/>0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="041f1-168"><a name="0.1.0-preview"/>0.1.0-preview</span></span>

<span data-ttu-id="041f1-169">Hello предварительной версии Azure Cosmos DB .NET Core SDK позволяет быстро, toobuild кросс платформенных [ASP.NET Core](https://www.asp.net/core) и [.NET Core](https://www.microsoft.com/net/core#windows) toorun приложений в Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="041f1-169">hello Azure Cosmos DB .NET Core Preview SDK enables you toobuild fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps toorun on Windows, Mac, and Linux.</span></span>

<span data-ttu-id="041f1-170">Hello Azure Cosmos DB .NET Core Preview SDK имеет функционального соответствия с последней версией hello hello [пакета SDK .NET Azure Cosmos DB](documentdb-sdk-dotnet.md) и поддерживает hello ниже:</span><span class="sxs-lookup"><span data-stu-id="041f1-170">hello Azure Cosmos DB .NET Core Preview SDK has feature parity with hello latest version of hello [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) and supports hello following:</span></span>
* <span data-ttu-id="041f1-171">все [режимы подключения](performance-tips.md#networking): режим шлюза, прямые TCP- и HTTP-подключения;</span><span class="sxs-lookup"><span data-stu-id="041f1-171">All [connection modes](performance-tips.md#networking): Gateway mode, Direct TCP, and Direct HTTPs.</span></span> 
* <span data-ttu-id="041f1-172">все [уровни согласованности](consistency-levels.md): строгая, ограниченное устаревание, согласованность сеанса, окончательная;</span><span class="sxs-lookup"><span data-stu-id="041f1-172">All [consistency levels](consistency-levels.md): Strong, Session, Bounded Staleness, and Eventual.</span></span>
* <span data-ttu-id="041f1-173">[секционированные коллекции](partition-data.md);</span><span class="sxs-lookup"><span data-stu-id="041f1-173">[Partitioned collections](partition-data.md).</span></span> 
* <span data-ttu-id="041f1-174">[георепликация данных и межрегиональные учетные записи баз данных](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="041f1-174">[Multi-region database accounts and geo-replication](distribute-data-globally.md).</span></span>

<span data-ttu-id="041f1-175">Если у вас есть вопросы связанные toothis SDK, учет слишком[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), или файл проблему в hello [репозитории github](https://github.com/Azure/azure-documentdb-dotnet/issues).</span><span class="sxs-lookup"><span data-stu-id="041f1-175">If you have questions related toothis SDK, post too[StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), or file an issue in hello [github repository](https://github.com/Azure/azure-documentdb-dotnet/issues).</span></span> 

## <a name="release--retirement-dates"></a><span data-ttu-id="041f1-176">Даты выпуска и выбытия</span><span class="sxs-lookup"><span data-stu-id="041f1-176">Release & Retirement Dates</span></span>

| <span data-ttu-id="041f1-177">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="041f1-177">Version</span></span> | <span data-ttu-id="041f1-178">Дата выпуска</span><span class="sxs-lookup"><span data-stu-id="041f1-178">Release Date</span></span> | <span data-ttu-id="041f1-179">Дата вывода</span><span class="sxs-lookup"><span data-stu-id="041f1-179">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="041f1-180">1.5.0</span><span class="sxs-lookup"><span data-stu-id="041f1-180">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="041f1-181">10 августа 2017 г.</span><span class="sxs-lookup"><span data-stu-id="041f1-181">August 10, 2017</span></span> |--- | 
| [<span data-ttu-id="041f1-182">1.4.1</span><span class="sxs-lookup"><span data-stu-id="041f1-182">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="041f1-183">7 августа 2017 г.</span><span class="sxs-lookup"><span data-stu-id="041f1-183">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="041f1-184">1.4.0</span><span class="sxs-lookup"><span data-stu-id="041f1-184">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="041f1-185">2 августа 2017 г.</span><span class="sxs-lookup"><span data-stu-id="041f1-185">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="041f1-186">1.3.2</span><span class="sxs-lookup"><span data-stu-id="041f1-186">1.3.2</span></span>](#1.3.2) |<span data-ttu-id="041f1-187">12 июня 2017 г.</span><span class="sxs-lookup"><span data-stu-id="041f1-187">June 12, 2017</span></span> |--- |
| [<span data-ttu-id="041f1-188">1.3.1</span><span class="sxs-lookup"><span data-stu-id="041f1-188">1.3.1</span></span>](#1.3.1) |<span data-ttu-id="041f1-189">23 мая 2017 г.</span><span class="sxs-lookup"><span data-stu-id="041f1-189">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="041f1-190">1.3.0</span><span class="sxs-lookup"><span data-stu-id="041f1-190">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="041f1-191">10 мая 2017 г.</span><span class="sxs-lookup"><span data-stu-id="041f1-191">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="041f1-192">1.2.2</span><span class="sxs-lookup"><span data-stu-id="041f1-192">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="041f1-193">19 апреля 2017 г.</span><span class="sxs-lookup"><span data-stu-id="041f1-193">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="041f1-194">1.2.1</span><span class="sxs-lookup"><span data-stu-id="041f1-194">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="041f1-195">29 марта 2017 г.</span><span class="sxs-lookup"><span data-stu-id="041f1-195">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="041f1-196">1.2.0</span><span class="sxs-lookup"><span data-stu-id="041f1-196">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="041f1-197">25 марта 2017 г.</span><span class="sxs-lookup"><span data-stu-id="041f1-197">March 25, 2017</span></span> |--- |
| [<span data-ttu-id="041f1-198">1.1.2</span><span class="sxs-lookup"><span data-stu-id="041f1-198">1.1.2</span></span>](#1.1.2) |<span data-ttu-id="041f1-199">20 марта 2017 г.</span><span class="sxs-lookup"><span data-stu-id="041f1-199">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="041f1-200">1.1.1</span><span class="sxs-lookup"><span data-stu-id="041f1-200">1.1.1</span></span>](#1.1.1) |<span data-ttu-id="041f1-201">14 марта 2017 г.</span><span class="sxs-lookup"><span data-stu-id="041f1-201">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="041f1-202">1.1.0</span><span class="sxs-lookup"><span data-stu-id="041f1-202">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="041f1-203">16 февраля 2017 г.</span><span class="sxs-lookup"><span data-stu-id="041f1-203">February 16, 2017</span></span> |--- |
| [<span data-ttu-id="041f1-204">1.0.0</span><span class="sxs-lookup"><span data-stu-id="041f1-204">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="041f1-205">21 декабря 2016 г.</span><span class="sxs-lookup"><span data-stu-id="041f1-205">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="041f1-206">0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="041f1-206">0.1.0-preview</span></span>](#0.1.0-preview) |<span data-ttu-id="041f1-207">15 ноября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="041f1-207">November 15, 2016</span></span> |<span data-ttu-id="041f1-208">31 декабря 2016 г.</span><span class="sxs-lookup"><span data-stu-id="041f1-208">December 31, 2016</span></span> |

## <a name="see-also"></a><span data-ttu-id="041f1-209">См. также</span><span class="sxs-lookup"><span data-stu-id="041f1-209">See Also</span></span>
<span data-ttu-id="041f1-210">toolearn Дополнительные сведения о Cosmos DB. в разделе [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) страницы службы.</span><span class="sxs-lookup"><span data-stu-id="041f1-210">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

