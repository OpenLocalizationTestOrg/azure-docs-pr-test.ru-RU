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
# <a name="azure-cosmos-db-net-core-sdk-release-notes-and-resources"></a><span data-ttu-id="e1497-103">Пакет SDK .NET Core для Azure Cosmos DB: заметки о выпуске и ресурсы</span><span class="sxs-lookup"><span data-stu-id="e1497-103">Azure Cosmos DB .NET Core SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e1497-104">.NET</span><span class="sxs-lookup"><span data-stu-id="e1497-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="e1497-105">Веб-канал изменений в .NET</span><span class="sxs-lookup"><span data-stu-id="e1497-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="e1497-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="e1497-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="e1497-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="e1497-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="e1497-108">Java</span><span class="sxs-lookup"><span data-stu-id="e1497-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="e1497-109">Python</span><span class="sxs-lookup"><span data-stu-id="e1497-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="e1497-110">REST</span><span class="sxs-lookup"><span data-stu-id="e1497-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="e1497-111">Поставщик ресурсов REST</span><span class="sxs-lookup"><span data-stu-id="e1497-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="e1497-112">SQL</span><span class="sxs-lookup"><span data-stu-id="e1497-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="e1497-113">**Скачивание пакета SDK**</span><span class="sxs-lookup"><span data-stu-id="e1497-113">**SDK download**</span></span></td><td>[<span data-ttu-id="e1497-114">NuGet</span><span class="sxs-lookup"><span data-stu-id="e1497-114">NuGet</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core/)</td></tr>

<tr><td><span data-ttu-id="e1497-115">**Документация по API**</span><span class="sxs-lookup"><span data-stu-id="e1497-115">**API documentation**</span></span></td><td>[<span data-ttu-id="e1497-116">Справочная документация по API .NET</span><span class="sxs-lookup"><span data-stu-id="e1497-116">.NET API reference documentation</span></span>](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td><span data-ttu-id="e1497-117">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="e1497-117">**Samples**</span></span></td><td>[<span data-ttu-id="e1497-118">Примеры кода для .NET</span><span class="sxs-lookup"><span data-stu-id="e1497-118">.NET code samples</span></span>](documentdb-dotnet-samples.md)</td></tr>

<tr><td><span data-ttu-id="e1497-119">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="e1497-119">**Get started**</span></span></td><td>[<span data-ttu-id="e1497-120">Azure Cosmos DB. Приступая к работе с API DocumentDB и .NET Core</span><span class="sxs-lookup"><span data-stu-id="e1497-120">Get started with the Azure Cosmos DB .NET Core SDK</span></span>](documentdb-dotnetcore-get-started.md)</td></tr>

<tr><td><span data-ttu-id="e1497-121">**Учебник по веб-приложениям**</span><span class="sxs-lookup"><span data-stu-id="e1497-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="e1497-122">Руководство по ASP.NET MVC. Разработка веб-приложений в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e1497-122">Web application development with Azure Cosmos DB</span></span>](documentdb-dotnet-application.md)</td></tr>

<tr><td><span data-ttu-id="e1497-123">**Текущая поддерживаемая платформа**</span><span class="sxs-lookup"><span data-stu-id="e1497-123">**Current supported framework**</span></span></td><td>[<span data-ttu-id="e1497-124">.NET Standard 1.6 и .NET Standard 1.5</span><span class="sxs-lookup"><span data-stu-id="e1497-124">.NET Standard 1.6 and .NET Standard 1.5</span></span>](https://www.nuget.org/packages/NETStandard.Library)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="e1497-125">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="e1497-125">Release Notes</span></span>

<span data-ttu-id="e1497-126">Пакет SDK .NET Core для Azure Cosmos DB функционально полностью эквивалентен последней версии [пакета SDK .NET для Azure Cosmos DB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="e1497-126">The Azure Cosmos DB .NET Core SDK has feature parity with the latest version of the [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="e1497-127">Пакет SDK .NET Core для Azure Cosmos DB пока несовместим с приложениями универсальной платформы Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="e1497-127">The Azure Cosmos DB .NET Core SDK is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="e1497-128">Чтобы получить пакет SDK для .NET Core, который поддерживает приложения UWP, отправьте сообщение по адресу [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e1497-128">If you are interested in the .NET Core SDK that does support UWP apps, send email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

### <a name="a-name150150"></a><span data-ttu-id="e1497-129"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="e1497-129"><a name="1.5.0"/>1.5.0</span></span> 

* <span data-ttu-id="e1497-130">Добавлена поддержка PartitionKeyRangeId как FeedOption для ограничения области результатов запроса определенным диапазоном ключа секции.</span><span class="sxs-lookup"><span data-stu-id="e1497-130">Added support for PartitionKeyRangeId as a FeedOption for scoping query results to a specific partition key range value.</span></span> 
* <span data-ttu-id="e1497-131">Добавлена поддержка StartTime как ChangeFeedOption для поиска изменений после указанного периода.</span><span class="sxs-lookup"><span data-stu-id="e1497-131">Added support for StartTime as a ChangeFeedOption to start looking for the changes after that time.</span></span> 

### <a name="a-name141141"></a><span data-ttu-id="e1497-132"><a name="1.4.1"/>1.4.1</span><span class="sxs-lookup"><span data-stu-id="e1497-132"><a name="1.4.1"/>1.4.1</span></span>

*   <span data-ttu-id="e1497-133">Устранена проблема в классе JsonSerializable, которая могла порождать исключение переполнения стека.</span><span class="sxs-lookup"><span data-stu-id="e1497-133">Fixed an issue in the JsonSerializable class that may cause a stack overflow exception.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="e1497-134"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="e1497-134"><a name="1.4.0"/>1.4.0</span></span>

*   <span data-ttu-id="e1497-135">Добавлена поддержка для указания пользовательских параметров JsonSerializerSettings при создании экземпляра [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="e1497-135">Added support for specifying custom JsonSerializerSettings while instantiating a [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) instance.</span></span>

### <a name="a-name132132"></a><span data-ttu-id="e1497-136"><a name="1.3.2"/>1.3.2</span><span class="sxs-lookup"><span data-stu-id="e1497-136"><a name="1.3.2"/>1.3.2</span></span>

*   <span data-ttu-id="e1497-137">Поддержка .NET Standard 1.5 в качестве одной из требуемых версий .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="e1497-137">Supporting .NET Standard 1.5 as one of the target frameworks.</span></span>

### <a name="a-name131131"></a><span data-ttu-id="e1497-138"><a name="1.3.1"/>1.3.1</span><span class="sxs-lookup"><span data-stu-id="e1497-138"><a name="1.3.1"/>1.3.1</span></span>

*   <span data-ttu-id="e1497-139">Устранена проблема, возникающая на компьютерах под управлением 64-разрядной ОС без поддержки инструкций SSE4, которая приводила к исключению SEHException при выполнении запросов Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e1497-139">Fixed an issue that affected x64 machines that don’t support SSE4 instruction and throw SEHException when running Azure Cosmos DB queries.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="e1497-140"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="e1497-140"><a name="1.3.0"/>1.3.0</span></span>

*   <span data-ttu-id="e1497-141">Добавлена поддержка нового уровня согласованности с именем ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="e1497-141">Added support for a new consistency level called ConsistentPrefix.</span></span>
*   <span data-ttu-id="e1497-142">Добавлена поддержка запроса метрик отдельных секций.</span><span class="sxs-lookup"><span data-stu-id="e1497-142">Added support for query metrics for individual partitions.</span></span>
*   <span data-ttu-id="e1497-143">Добавлена поддержка ограничения размера маркера продолжения запросов.</span><span class="sxs-lookup"><span data-stu-id="e1497-143">Added support for limiting the size of the continuation token for queries.</span></span>
*   <span data-ttu-id="e1497-144">Добавлена поддержка более подробной трассировки невыполненных запросов.</span><span class="sxs-lookup"><span data-stu-id="e1497-144">Added support for more detailed tracing for failed requests.</span></span>
*   <span data-ttu-id="e1497-145">Внесены некоторые улучшения производительности в пакет SDK.</span><span class="sxs-lookup"><span data-stu-id="e1497-145">Made some performance improvements in the SDK.</span></span>

### <a name="a-name122122"></a><span data-ttu-id="e1497-146"><a name="1.2.2"/>1.2.2</span><span class="sxs-lookup"><span data-stu-id="e1497-146"><a name="1.2.2"/>1.2.2</span></span>

* <span data-ttu-id="e1497-147">Устранена проблема, когда не учитывалось значение PartitionKey в FeedOptions для статистических запросов.</span><span class="sxs-lookup"><span data-stu-id="e1497-147">Fixed an issue that ignored the PartitionKey value provided in FeedOptions for aggregate queries.</span></span>
* <span data-ttu-id="e1497-148">Устранена проблема, связанная с прозрачной обработкой управления при промежуточном выполнении запроса Order By между разделами.</span><span class="sxs-lookup"><span data-stu-id="e1497-148">Fixed an issue in transparent handling of partition management during mid-flight cross-partition Order By query execution.</span></span>

### <a name="a-name121121"></a><span data-ttu-id="e1497-149"><a name="1.2.1"/>1.2.1</span><span class="sxs-lookup"><span data-stu-id="e1497-149"><a name="1.2.1"/>1.2.1</span></span>

* <span data-ttu-id="e1497-150">Исправлена проблема, вызывавшая взаимоблокировки в некоторых асинхронных интерфейсах API при использовании в контексте ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e1497-150">Fixed an issue which caused deadlocks in some of the async APIs when used inside ASP.NET context.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="e1497-151"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="e1497-151"><a name="1.2.0"/>1.2.0</span></span>

* <span data-ttu-id="e1497-152">Исправления для повышения устойчивости пакета SDK к автоматической отработке отказа при определенных условиях.</span><span class="sxs-lookup"><span data-stu-id="e1497-152">Fixes to make SDK more resilient to automatic failover under certain conditions.</span></span>

### <a name="a-name112112"></a><span data-ttu-id="e1497-153"><a name="1.1.2"/>1.1.2</span><span class="sxs-lookup"><span data-stu-id="e1497-153"><a name="1.1.2"/>1.1.2</span></span>

* <span data-ttu-id="e1497-154">Исправление ошибки, приводившей к исключению WebException: "Удаленное имя не удалось разрешить".</span><span class="sxs-lookup"><span data-stu-id="e1497-154">Fix for an issue that occasionally causes a WebException: The remote name could not be resolved.</span></span>
* <span data-ttu-id="e1497-155">Добавлена поддержка непосредственного считывания типизированного документа путем добавления новых перегрузок в API ReadDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="e1497-155">Added the support for directly reading a typed document by adding new overloads to ReadDocumentAsync API.</span></span>

### <a name="a-name111111"></a><span data-ttu-id="e1497-156"><a name="1.1.1"/>1.1.1</span><span class="sxs-lookup"><span data-stu-id="e1497-156"><a name="1.1.1"/>1.1.1</span></span>

* <span data-ttu-id="e1497-157">Добавлена поддержка LINQ для статистических запросов (COUNT, MIN, MAX, SUM и AVG).</span><span class="sxs-lookup"><span data-stu-id="e1497-157">Added LINQ support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="e1497-158">Исправление ошибки утечки памяти для объекта ConnectionPolicy, вызываемой использованием обработчика событий.</span><span class="sxs-lookup"><span data-stu-id="e1497-158">Fix for a memory leak issue for the ConnectionPolicy object caused by the use of event handler.</span></span>
* <span data-ttu-id="e1497-159">Исправление ошибки, из-за которой метод UpsertAttachmentAsync не работал, когда использовался тег ETag.</span><span class="sxs-lookup"><span data-stu-id="e1497-159">Fix for an issue wherein UpsertAttachmentAsync was not working when ETag was used.</span></span>
* <span data-ttu-id="e1497-160">Исправление ошибки, из-за которой продолжение запросов orderBy между секциями не работало при сортировке по полю строки.</span><span class="sxs-lookup"><span data-stu-id="e1497-160">Fix for an issue wherein cross partition order-by query continuation was not working when sorting on string field.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="e1497-161"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="e1497-161"><a name="1.1.0"/>1.1.0</span></span>

* <span data-ttu-id="e1497-162">Добавлена поддержка статистических запросов (COUNT, MIN, MAX, SUM и AVG).</span><span class="sxs-lookup"><span data-stu-id="e1497-162">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="e1497-163">Дополнительные сведения см. в разделе [Статистические функции](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="e1497-163">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="e1497-164">Минимальная пропускная способность секционированных коллекций снижена с 10 100 ЕЗ/с до 2500 ЕЗ/с.</span><span class="sxs-lookup"><span data-stu-id="e1497-164">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="e1497-165"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="e1497-165"><a name="1.0.0"/>1.0.0</span></span>

<span data-ttu-id="e1497-166">Пакет SDK .NET Core для Azure Cosmos DB позволяет создавать быстрые кроссплатформенные приложения [ASP.NET Core](https://www.asp.net/core) и [.NET Core](https://www.microsoft.com/net/core#windows) для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="e1497-166">The Azure Cosmos DB .NET Core SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span></span> <span data-ttu-id="e1497-167">Последний выпуск пакета SDK .NET Core для Azure Cosmos DB полностью совместим с [Хamarin](https://www.xamarin.com) и пригоден для создания приложений для iOS, Android и Mono (Linux).</span><span class="sxs-lookup"><span data-stu-id="e1497-167">The latest release of the Azure Cosmos DB .NET Core SDK is fully [Xamarin](https://www.xamarin.com) compatible and be used to build applications that target iOS, Android, and Mono (Linux).</span></span>  

### <a name="a-name010-preview010-preview"></a><span data-ttu-id="e1497-168"><a name="0.1.0-preview"/>0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="e1497-168"><a name="0.1.0-preview"/>0.1.0-preview</span></span>

<span data-ttu-id="e1497-169">Пакет SDK .NET Core для Azure Cosmos DB (предварительная версия) позволяет создавать быстрые кроссплатформенные приложения [ASP.NET Core](https://www.asp.net/core) и [.NET Core](https://www.microsoft.com/net/core#windows) для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="e1497-169">The Azure Cosmos DB .NET Core Preview SDK enables you to build fast, cross-platform [ASP.NET Core](https://www.asp.net/core) and [.NET Core](https://www.microsoft.com/net/core#windows) apps to run on Windows, Mac, and Linux.</span></span>

<span data-ttu-id="e1497-170">Пакет SDK .NET Core для Azure Cosmos DB (предварительная версия) функционально полностью эквивалентен последней версии [пакета SDK .NET для Azure Cosmos DB](documentdb-sdk-dotnet.md) и поддерживает следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="e1497-170">The Azure Cosmos DB .NET Core Preview SDK has feature parity with the latest version of the [Azure Cosmos DB .NET SDK](documentdb-sdk-dotnet.md) and supports the following:</span></span>
* <span data-ttu-id="e1497-171">все [режимы подключения](performance-tips.md#networking): режим шлюза, прямые TCP- и HTTP-подключения;</span><span class="sxs-lookup"><span data-stu-id="e1497-171">All [connection modes](performance-tips.md#networking): Gateway mode, Direct TCP, and Direct HTTPs.</span></span> 
* <span data-ttu-id="e1497-172">все [уровни согласованности](consistency-levels.md): строгая, ограниченное устаревание, согласованность сеанса, окончательная;</span><span class="sxs-lookup"><span data-stu-id="e1497-172">All [consistency levels](consistency-levels.md): Strong, Session, Bounded Staleness, and Eventual.</span></span>
* <span data-ttu-id="e1497-173">[секционированные коллекции](partition-data.md);</span><span class="sxs-lookup"><span data-stu-id="e1497-173">[Partitioned collections](partition-data.md).</span></span> 
* <span data-ttu-id="e1497-174">[георепликация данных и межрегиональные учетные записи баз данных](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="e1497-174">[Multi-region database accounts and geo-replication](distribute-data-globally.md).</span></span>

<span data-ttu-id="e1497-175">Если у вас возникли вопросы об этом пакете SDK, опубликуйте их на форуме сайта [StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb) или сообщите о проблеме в [репозитории GitHub](https://github.com/Azure/azure-documentdb-dotnet/issues).</span><span class="sxs-lookup"><span data-stu-id="e1497-175">If you have questions related to this SDK, post to [StackOverflow](http://stackoverflow.com/questions/tagged/azure-documentdb), or file an issue in the [github repository](https://github.com/Azure/azure-documentdb-dotnet/issues).</span></span> 

## <a name="release--retirement-dates"></a><span data-ttu-id="e1497-176">Даты выпуска и выбытия</span><span class="sxs-lookup"><span data-stu-id="e1497-176">Release & Retirement Dates</span></span>

| <span data-ttu-id="e1497-177">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="e1497-177">Version</span></span> | <span data-ttu-id="e1497-178">Дата выпуска</span><span class="sxs-lookup"><span data-stu-id="e1497-178">Release Date</span></span> | <span data-ttu-id="e1497-179">Дата вывода</span><span class="sxs-lookup"><span data-stu-id="e1497-179">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="e1497-180">1.5.0</span><span class="sxs-lookup"><span data-stu-id="e1497-180">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="e1497-181">10 августа 2017 г.</span><span class="sxs-lookup"><span data-stu-id="e1497-181">August 10, 2017</span></span> |--- | 
| [<span data-ttu-id="e1497-182">1.4.1</span><span class="sxs-lookup"><span data-stu-id="e1497-182">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="e1497-183">7 августа 2017 г.</span><span class="sxs-lookup"><span data-stu-id="e1497-183">August 07, 2017</span></span> |--- |
| [<span data-ttu-id="e1497-184">1.4.0</span><span class="sxs-lookup"><span data-stu-id="e1497-184">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="e1497-185">2 августа 2017 г.</span><span class="sxs-lookup"><span data-stu-id="e1497-185">August 02, 2017</span></span> |--- |
| [<span data-ttu-id="e1497-186">1.3.2</span><span class="sxs-lookup"><span data-stu-id="e1497-186">1.3.2</span></span>](#1.3.2) |<span data-ttu-id="e1497-187">12 июня 2017 г.</span><span class="sxs-lookup"><span data-stu-id="e1497-187">June 12, 2017</span></span> |--- |
| [<span data-ttu-id="e1497-188">1.3.1</span><span class="sxs-lookup"><span data-stu-id="e1497-188">1.3.1</span></span>](#1.3.1) |<span data-ttu-id="e1497-189">23 мая 2017 г.</span><span class="sxs-lookup"><span data-stu-id="e1497-189">May 23, 2017</span></span> |--- |
| [<span data-ttu-id="e1497-190">1.3.0</span><span class="sxs-lookup"><span data-stu-id="e1497-190">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="e1497-191">10 мая 2017 г.</span><span class="sxs-lookup"><span data-stu-id="e1497-191">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="e1497-192">1.2.2</span><span class="sxs-lookup"><span data-stu-id="e1497-192">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="e1497-193">19 апреля 2017 г.</span><span class="sxs-lookup"><span data-stu-id="e1497-193">April 19, 2017</span></span> |--- |
| [<span data-ttu-id="e1497-194">1.2.1</span><span class="sxs-lookup"><span data-stu-id="e1497-194">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="e1497-195">29 марта 2017 г.</span><span class="sxs-lookup"><span data-stu-id="e1497-195">March 29, 2017</span></span> |--- |
| [<span data-ttu-id="e1497-196">1.2.0</span><span class="sxs-lookup"><span data-stu-id="e1497-196">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="e1497-197">25 марта 2017 г.</span><span class="sxs-lookup"><span data-stu-id="e1497-197">March 25, 2017</span></span> |--- |
| [<span data-ttu-id="e1497-198">1.1.2</span><span class="sxs-lookup"><span data-stu-id="e1497-198">1.1.2</span></span>](#1.1.2) |<span data-ttu-id="e1497-199">20 марта 2017 г.</span><span class="sxs-lookup"><span data-stu-id="e1497-199">March 20, 2017</span></span> |--- |
| [<span data-ttu-id="e1497-200">1.1.1</span><span class="sxs-lookup"><span data-stu-id="e1497-200">1.1.1</span></span>](#1.1.1) |<span data-ttu-id="e1497-201">14 марта 2017 г.</span><span class="sxs-lookup"><span data-stu-id="e1497-201">March 14, 2017</span></span> |--- |
| [<span data-ttu-id="e1497-202">1.1.0</span><span class="sxs-lookup"><span data-stu-id="e1497-202">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="e1497-203">16 февраля 2017 г.</span><span class="sxs-lookup"><span data-stu-id="e1497-203">February 16, 2017</span></span> |--- |
| [<span data-ttu-id="e1497-204">1.0.0</span><span class="sxs-lookup"><span data-stu-id="e1497-204">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="e1497-205">21 декабря 2016 г.</span><span class="sxs-lookup"><span data-stu-id="e1497-205">December 21, 2016</span></span> |--- |
| [<span data-ttu-id="e1497-206">0.1.0-preview</span><span class="sxs-lookup"><span data-stu-id="e1497-206">0.1.0-preview</span></span>](#0.1.0-preview) |<span data-ttu-id="e1497-207">15 ноября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="e1497-207">November 15, 2016</span></span> |<span data-ttu-id="e1497-208">31 декабря 2016 г.</span><span class="sxs-lookup"><span data-stu-id="e1497-208">December 31, 2016</span></span> |

## <a name="see-also"></a><span data-ttu-id="e1497-209">См. также</span><span class="sxs-lookup"><span data-stu-id="e1497-209">See Also</span></span>
<span data-ttu-id="e1497-210">Дополнительные сведения о Cosmos DB см. на странице службы [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="e1497-210">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

