---
title: "aaaAzure Cosmos DB шкала и тестирование производительности | Документы Microsoft"
description: "Узнайте, как масштабировать tooperform и тестирование производительности с помощью Azure Cosmos DB"
keywords: "тестирование производительности"
services: cosmos-db
author: arramac
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: arramac
ms.openlocfilehash: 46d1217e11a39ee970a868de9a5c5dfcf52cedf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a><span data-ttu-id="c0e43-104">Проверка производительности и масштабирования с помощью Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c0e43-104">Performance and scale testing with Azure Cosmos DB</span></span>
<span data-ttu-id="c0e43-105">Проверка производительности и масштабирования — ключевой этап в разработке приложения.</span><span class="sxs-lookup"><span data-stu-id="c0e43-105">Performance and scale testing is a key step in application development.</span></span> <span data-ttu-id="c0e43-106">Для многих приложений уровня базы данных hello оказывает существенное влияние hello общей производительности и масштабируемости и является таким образом это важная составляющая производительности тестирования.</span><span class="sxs-lookup"><span data-stu-id="c0e43-106">For many applications, hello database tier has a significant impact on hello overall performance and scalability, and is therefore a critical component of performance testing.</span></span> <span data-ttu-id="c0e43-107">Система [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) разработана с расчетом на эластичное масштабирование и предсказуемую производительность. Поэтому она отлично подходит для приложений, требующих высокую производительность для уровня базы данных.</span><span class="sxs-lookup"><span data-stu-id="c0e43-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is purpose-built for elastic scale and predictable performance, and therefore a great fit for applications that need a high-performance database tier.</span></span> 

<span data-ttu-id="c0e43-108">Эта статья предназначена для специалистов, разрабатывающих наборы тестов производительности для рабочих нагрузок Cosmos DB или оценивающих Cosmos DB для сценариев с высокопроизводительными приложениями.</span><span class="sxs-lookup"><span data-stu-id="c0e43-108">This article is a reference for developers implementing performance test suites for their Cosmos DB workloads, or evaluating Cosmos DB for high-performance application scenarios.</span></span> <span data-ttu-id="c0e43-109">В основном ориентировано на тестирование производительности изолированной hello базы данных, но также содержит рекомендации для производственных приложений.</span><span class="sxs-lookup"><span data-stu-id="c0e43-109">It focuses primarily on isolated performance testing of hello database, but also includes best practices for production applications.</span></span>

<span data-ttu-id="c0e43-110">После считывания в этой статье, можно будет tooanswer hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="c0e43-110">After reading this article, you will be able tooanswer hello following questions:</span></span>   

* <span data-ttu-id="c0e43-111">Где найти образец клиентского приложения .NET для проверки производительности Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="c0e43-111">Where can I find a sample .NET client application for performance testing of Cosmos DB?</span></span> 
* <span data-ttu-id="c0e43-112">Как добиться высокой пропускной способности с помощью Cosmos DB из клиентского приложения?</span><span class="sxs-lookup"><span data-stu-id="c0e43-112">How do I achieve high throughput levels with Cosmos DB from my client application?</span></span>

<span data-ttu-id="c0e43-113">tooget к выполнению кода, загрузите проект hello из [пример тестирование Azure Cosmos DB производительности](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="c0e43-113">tooget started with code, please download hello project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span></span> 

> [!NOTE]
> <span data-ttu-id="c0e43-114">Задача Hello этого приложения — toodemonstrate советы и рекомендации для извлечения более высокую производительность за пределы Cosmos DB с небольшим числом клиентских машин.</span><span class="sxs-lookup"><span data-stu-id="c0e43-114">hello goal of this application is toodemonstrate best practices for extracting better performance out of Cosmos DB with a small number of client machines.</span></span> <span data-ttu-id="c0e43-115">Это не была сделана пиковую hello toodemonstrate hello службы, которая позволяет масштабировать limitlessly.</span><span class="sxs-lookup"><span data-stu-id="c0e43-115">This was not made toodemonstrate hello peak capacity of hello service, which can scale limitlessly.</span></span>
> 
> 

<span data-ttu-id="c0e43-116">Если вы ищете tooimprove параметры конфигурации клиента Cosmos DB производительности, см. раздел [советы по повышению производительности базы данных Azure Cosmos](performance-tips.md).</span><span class="sxs-lookup"><span data-stu-id="c0e43-116">If you're looking for client-side configuration options tooimprove Cosmos DB performance, see [Azure Cosmos DB performance tips](performance-tips.md).</span></span>

## <a name="run-hello-performance-testing-application"></a><span data-ttu-id="c0e43-117">Запустите приложение тестирования производительности, hello</span><span class="sxs-lookup"><span data-stu-id="c0e43-117">Run hello performance testing application</span></span>
<span data-ttu-id="c0e43-118">Здравствуйте, tooget быстрый способ работы — toocompile и образец hello выполнения .NET ниже, как описано в шагах hello ниже.</span><span class="sxs-lookup"><span data-stu-id="c0e43-118">hello quickest way tooget started is toocompile and run hello .NET sample below, as described in hello steps below.</span></span> <span data-ttu-id="c0e43-119">Также можно просмотреть исходный код hello и реализовать аналогичный конфигураций tooyour собственные клиентские приложения.</span><span class="sxs-lookup"><span data-stu-id="c0e43-119">You can also review hello source code and implement similar configurations tooyour own client applications.</span></span>

<span data-ttu-id="c0e43-120">**Шаг 1.** загрузка hello проект из [пример тестирование Azure Cosmos DB производительности](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), или репозитория GitHub hello вилки.</span><span class="sxs-lookup"><span data-stu-id="c0e43-120">**Step 1:** Download hello project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), or fork hello GitHub repository.</span></span>

<span data-ttu-id="c0e43-121">**Шаг 2.** изменения параметров hello EndpointUrl, AuthorizationKey, CollectionThroughput и DocumentTemplate (необязательно) в файле App.config.</span><span class="sxs-lookup"><span data-stu-id="c0e43-121">**Step 2:** Modify hello settings for EndpointUrl, AuthorizationKey, CollectionThroughput and DocumentTemplate (optional) in App.config.</span></span>

> [!NOTE]
> <span data-ttu-id="c0e43-122">Перед подготовкой коллекции с высокой пропускной способностью, можно найти toohello [цены](https://azure.microsoft.com/pricing/details/cosmos-db/) tooestimate hello затраты на коллекции.</span><span class="sxs-lookup"><span data-stu-id="c0e43-122">Before provisioning collections with high throughput, please refer toohello [Pricing Page](https://azure.microsoft.com/pricing/details/cosmos-db/) tooestimate hello costs per collection.</span></span> <span data-ttu-id="c0e43-123">Azure Cosmos DB выставляет счет за хранение и пропускную способность независимо друг от друга на почасовой основе затрат можно сохранить, удалив или понизить пропускную способность hello вашей коллекции Azure Cosmos DB после тестирования.</span><span class="sxs-lookup"><span data-stu-id="c0e43-123">Azure Cosmos DB bills storage and throughput independently on an hourly basis, so you can save costs by deleting or lowering hello throughput of your Azure Cosmos DB collections after testing.</span></span>
> 
> 

<span data-ttu-id="c0e43-124">**Шаг 3.** скомпилировать и запустить консольное приложение hello из командной строки hello.</span><span class="sxs-lookup"><span data-stu-id="c0e43-124">**Step 3:** Compile and run hello console app from hello command line.</span></span> <span data-ttu-id="c0e43-125">Вы должны увидеть результаты hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c0e43-125">You should see output like hello following:</span></span>

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


<span data-ttu-id="c0e43-126">**Шаг 4 (при необходимости):** hello пропускная способность сообщил (единиц Запросов в секунду) из средства hello должен быть hello же или более поздней версии, чем пропускная способность hello hello коллекции.</span><span class="sxs-lookup"><span data-stu-id="c0e43-126">**Step 4 (if necessary):** hello throughput reported (RU/s) from hello tool should be hello same or higher than hello provisioned throughput of hello collection.</span></span> <span data-ttu-id="c0e43-127">В противном случае возрастающей hello DegreeOfParallelism небольшими шагами могут помочь в достижении предела hello.</span><span class="sxs-lookup"><span data-stu-id="c0e43-127">If not, increasing hello DegreeOfParallelism in small increments may help you reach hello limit.</span></span> <span data-ttu-id="c0e43-128">Plateaus пропускной способности hello из клиентского приложения, запуск нескольких экземпляров приложения hello на hello таким же или разными компьютерами поможет достигнуто hello подготовить через hello различных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="c0e43-128">If hello throughput from your client app plateaus, launching multiple instances of hello app on hello same or different machines will help you reach hello provisioned limit across hello different instances.</span></span> <span data-ttu-id="c0e43-129">Если требуется помощь на этом этапе, напишите сообщение электронной почты tooaskcosmosdb@microsoft.com или файл запрос в службу поддержки hello [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c0e43-129">If you need help with this step, please, write an email tooaskcosmosdb@microsoft.com or file a support ticket from hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="c0e43-130">После выполнения приложения hello, можно попробовать другой [политики индексирования](indexing-policies.md) и [уровни согласованности](consistency-levels.md) toounderstand их влияние на пропускной способности и задержки.</span><span class="sxs-lookup"><span data-stu-id="c0e43-130">Once you have hello app running, you can try different [Indexing policies](indexing-policies.md) and [Consistency levels](consistency-levels.md) toounderstand their impact on throughput and latency.</span></span> <span data-ttu-id="c0e43-131">Также можно просмотреть исходный код hello и реализовать аналогичный конфигураций tooyour собственные наборы или приложений в производственной среде.</span><span class="sxs-lookup"><span data-stu-id="c0e43-131">You can also review hello source code and implement similar configurations tooyour own test suites or production applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0e43-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c0e43-132">Next steps</span></span>
<span data-ttu-id="c0e43-133">В этой статье мы рассмотрели способы тестирования производительности и масштабируемости с помощью консольного приложения .NET Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c0e43-133">In this article, we looked at how you can perform performance and scale testing with Cosmos DB using a .NET console app.</span></span> <span data-ttu-id="c0e43-134">Дополнительные сведения о работе с Azure Cosmos DB см. ниже toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="c0e43-134">Please refer toohello links below for additional information on working with Azure Cosmos DB.</span></span>

* [<span data-ttu-id="c0e43-135">Пример для тестирования производительности Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c0e43-135">Azure Cosmos DB performance testing sample</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [<span data-ttu-id="c0e43-136">Tooimprove параметры конфигурации клиента Azure Cosmos DB производительности</span><span class="sxs-lookup"><span data-stu-id="c0e43-136">Client configuration options tooimprove Azure Cosmos DB performance</span></span>](performance-tips.md)
* [<span data-ttu-id="c0e43-137">Секционирование, ключи секции и масштабирование в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c0e43-137">Server-side partitioning in Azure Cosmos DB</span></span>](partition-data.md)


