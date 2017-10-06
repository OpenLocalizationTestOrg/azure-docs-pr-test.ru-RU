---
title: "aaaAzure Cosmos DB глобального распространения учебник по Graph API | Документы Microsoft"
description: "Узнайте, как hello toosetup Azure Cosmos DB глобального распространителя с помощью Graph API."
services: cosmos-db
keywords: "глобальное распределение, graph, gremlin"
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 1629a31e12a18079f63e07c4909862b36b5f4c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-graph-api"></a><span data-ttu-id="c77a6-104">Как hello toosetup Azure Cosmos DB глобального распространителя с помощью Graph API</span><span class="sxs-lookup"><span data-stu-id="c77a6-104">How toosetup Azure Cosmos DB global distribution using hello Graph API</span></span>

<span data-ttu-id="c77a6-105">В этой статье показано, как toouse hello Azure toosetup портала Azure Cosmos DB глобального распространения, а затем подключитесь с помощью hello API Graph (Предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="c77a6-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello Graph API (preview).</span></span>

<span data-ttu-id="c77a6-106">В этой статье рассматриваются hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="c77a6-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="c77a6-107">Настройка глобальных распространения, с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="c77a6-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="c77a6-108">Настройка глобальных распространения, с помощью hello [Graph API-интерфейсы](graph-introduction.md) (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="c77a6-108">Configure global distribution using hello [Graph APIs](graph-introduction.md) (preview)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-graph-api-using-hello-net-sdk"></a><span data-ttu-id="c77a6-109">Подключение tooa предпочтительную область с помощью API Graph hello, с помощью hello .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c77a6-109">Connecting tooa preferred region using hello Graph API using hello .NET SDK</span></span>

<span data-ttu-id="c77a6-110">Hello Graph API указывается в виде библиотеки расширений на основе hello DocumentDB SDK.</span><span class="sxs-lookup"><span data-stu-id="c77a6-110">hello Graph API is exposed as an extension library on top of hello DocumentDB SDK.</span></span>

<span data-ttu-id="c77a6-111">В порядке tootake преимуществами [глобального распространения](distribute-data-globally.md), клиентских приложений можно указать hello упорядоченный список предпочтения toobe области используется tooperform операции с документом.</span><span class="sxs-lookup"><span data-stu-id="c77a6-111">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="c77a6-112">Это можно сделать, задав политику подключений hello.</span><span class="sxs-lookup"><span data-stu-id="c77a6-112">This can be done by setting hello connection policy.</span></span> <span data-ttu-id="c77a6-113">В зависимости от конфигурации учетной записи Azure Cosmos DB hello доступности текущий язык и список предпочтения hello указана, hello большинство оптимальной конечная точка будет выбранные записи tooperform SDK hello и операции чтения.</span><span class="sxs-lookup"><span data-stu-id="c77a6-113">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello SDK tooperform write and read operations.</span></span>

<span data-ttu-id="c77a6-114">Этот список предпочтения указывается при инициализации подключения с помощью пакетов SDK hello.</span><span class="sxs-lookup"><span data-stu-id="c77a6-114">This preference list is specified when initializing a connection using hello SDKs.</span></span> <span data-ttu-id="c77a6-115">Необязательный параметр «PreferredLocations» примите Hello пакеты SDK, упорядоченный список регионов Azure.</span><span class="sxs-lookup"><span data-stu-id="c77a6-115">hello SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

* <span data-ttu-id="c77a6-116">**Записывает**: hello SDK будет автоматически отправлять все записывает toohello текущей записи области.</span><span class="sxs-lookup"><span data-stu-id="c77a6-116">**Writes**: hello SDK will automatically send all writes toohello current write region.</span></span>
* <span data-ttu-id="c77a6-117">**Считывает**: все операции чтения будут отправляться toohello первой доступной области, в списке PreferredLocations hello.</span><span class="sxs-lookup"><span data-stu-id="c77a6-117">**Reads**: All reads will be sent toohello first available region in hello PreferredLocations list.</span></span> <span data-ttu-id="c77a6-118">Если hello запрос завершается неудачно, клиент hello ошибкой вниз область Далее toohello списка hello и так далее.</span><span class="sxs-lookup"><span data-stu-id="c77a6-118">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span> <span data-ttu-id="c77a6-119">предпринимает попытку tooread из регионов hello, указанный в PreferredLocations Hello пакеты SDK.</span><span class="sxs-lookup"><span data-stu-id="c77a6-119">hello SDKs will only attempt tooread from hello regions specified in PreferredLocations.</span></span> <span data-ttu-id="c77a6-120">Таким образом например, если hello Cosmos DB учетная запись доступна в трех регионах, но клиент hello только задает два hello записи областей для PreferredLocations, затем никаких операций чтения будет предоставляться вне области записи hello, даже в случае hello перехода на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="c77a6-120">So, for example, if hello Cosmos DB account is available in three regions, but hello client only specifies two of hello non-write regions for PreferredLocations, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="c77a6-121">приложение Hello можно проверить hello текущей конечной точки записи и чтения конечная точка выбрана по hello SDK путем проверки два свойства: WriteEndpoint и ReadEndpoint, доступные в пакете SDK версии 1.8 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="c77a6-121">hello application can verify hello current write endpoint and read endpoint chosen by hello SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span> <span data-ttu-id="c77a6-122">Если hello PreferredLocations свойство не задано, все запросы будут поступать из hello текущей записи области.</span><span class="sxs-lookup"><span data-stu-id="c77a6-122">If hello PreferredLocations property is not set, all requests will be served from hello current write region.</span></span>

### <a name="using-hello-sdk"></a><span data-ttu-id="c77a6-123">С помощью пакета SDK для hello</span><span class="sxs-lookup"><span data-stu-id="c77a6-123">Using hello SDK</span></span>

<span data-ttu-id="c77a6-124">Например, в hello .NET SDK, hello `ConnectionPolicy` параметр hello `DocumentClient` конструктор имеет свойство с именем `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="c77a6-124">For example, in hello .NET SDK, hello `ConnectionPolicy` parameter for hello `DocumentClient` constructor has a property called `PreferredLocations`.</span></span> <span data-ttu-id="c77a6-125">Это свойство можно задать список tooa имена областей.</span><span class="sxs-lookup"><span data-stu-id="c77a6-125">This property can be set tooa list of region names.</span></span> <span data-ttu-id="c77a6-126">экран приветствия имен для [регионы Azure] [ regions] может быть указан как часть `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="c77a6-126">hello display names for [Azure Regions][regions] can be specified as part of `PreferredLocations`.</span></span>

> [!NOTE]
> <span data-ttu-id="c77a6-127">Hello URL-адресов для конечных точек hello не может считаться долгоживущие константы.</span><span class="sxs-lookup"><span data-stu-id="c77a6-127">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="c77a6-128">Hello службы может обновить в любой момент.</span><span class="sxs-lookup"><span data-stu-id="c77a6-128">hello service may update these at any point.</span></span> <span data-ttu-id="c77a6-129">Это изменение автоматически обрабатывает Hello SDK.</span><span class="sxs-lookup"><span data-stu-id="c77a6-129">hello SDK handles this change automatically.</span></span>
>
>

```cs
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;

ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect tooAzure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
```

<span data-ttu-id="c77a6-130">На этом руководство завершено.</span><span class="sxs-lookup"><span data-stu-id="c77a6-130">That's it, that completes this tutorial.</span></span> <span data-ttu-id="c77a6-131">Вы узнаете, как toomanage hello согласованности глобально реплицируемым учетной записи пользователя, считывая [уровни согласованности в базе данных Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="c77a6-131">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="c77a6-132">Сведения о том, как функционирует репликация глобальной базы данных в Azure Cosmos DB, см. в статье о [глобальном распределении данных в Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="c77a6-132">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c77a6-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c77a6-133">Next steps</span></span>

<span data-ttu-id="c77a6-134">В этом учебнике вы сделали hello следующее:</span><span class="sxs-lookup"><span data-stu-id="c77a6-134">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c77a6-135">Настройка глобальных распространения, с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="c77a6-135">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="c77a6-136">Настройка глобальных распространения, с помощью hello интерфейсы API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="c77a6-136">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="c77a6-137">Теперь можно перейти далее учебника toolearn toohello как toodevelop локально с помощью hello локальный эмулятор Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c77a6-137">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c77a6-138">Разрабатывать локально в эмуляторе hello</span><span class="sxs-lookup"><span data-stu-id="c77a6-138">Develop locally with hello emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

