---
title: "Учебник глобального распространения Cosmos DB aaaAzure для таблицы API | Документы Microsoft"
description: "Узнайте, как toosetup Azure Cosmos DB глобального распространителя с помощью hello API таблиц."
services: cosmos-db
keywords: "глобальное распределение, таблица"
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: d2a995e09c37f9449856aef2ab707e95eb8a540c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-table-api"></a><span data-ttu-id="ee946-104">Как toosetup Azure Cosmos DB глобального распространителя с помощью hello API таблиц</span><span class="sxs-lookup"><span data-stu-id="ee946-104">How toosetup Azure Cosmos DB global distribution using hello Table API</span></span>

<span data-ttu-id="ee946-105">В этой статье показано, как toouse hello Azure toosetup портала Azure Cosmos DB глобального распространения, а затем подключитесь с помощью hello API таблиц (Предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="ee946-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello Table API (preview).</span></span>

<span data-ttu-id="ee946-106">В этой статье рассматриваются hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="ee946-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="ee946-107">Настройка глобальных распространения, с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="ee946-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="ee946-108">Настройка глобальных распространения, с помощью hello [API таблиц](table-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="ee946-108">Configure global distribution using hello [Table API](table-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-table-api"></a><span data-ttu-id="ee946-109">Подключение tooa предпочтительную область с помощью hello API таблиц</span><span class="sxs-lookup"><span data-stu-id="ee946-109">Connecting tooa preferred region using hello Table API</span></span>

<span data-ttu-id="ee946-110">В порядке tootake преимуществами [глобального распространения](distribute-data-globally.md), клиентских приложений можно указать hello упорядоченный список предпочтения toobe области используется tooperform операции с документом.</span><span class="sxs-lookup"><span data-stu-id="ee946-110">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="ee946-111">Это можно сделать путем установки hello `TablePreferredLocations` значение конфигурации в файле конфигурации приложения hello для предварительного просмотра hello пакет SDK хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="ee946-111">This can be done by setting hello `TablePreferredLocations` configuration value in hello app config for hello preview Azure Storage SDK.</span></span> <span data-ttu-id="ee946-112">В зависимости от конфигурации учетной записи Azure Cosmos DB hello текущий язык доступности указан, список предпочтения hello приветствия большинство оптимальной конечной точки будет выбрана по tooperform пакет SDK хранилища Azure hello записи и операций чтения.</span><span class="sxs-lookup"><span data-stu-id="ee946-112">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello Azure Storage SDK tooperform write and read operations.</span></span>

<span data-ttu-id="ee946-113">Hello `TablePreferredLocations` должен содержать список разделенных запятыми предпочтительный расположения (множественной адресацией) для операций чтения.</span><span class="sxs-lookup"><span data-stu-id="ee946-113">hello `TablePreferredLocations` should contain a comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="ee946-114">Каждый экземпляр клиента можно указать подмножество этих областей в порядке hello предпочтительный для операций чтения с небольшой задержкой.</span><span class="sxs-lookup"><span data-stu-id="ee946-114">Each client instance can specify a subset of these regions in hello preferred order for low latency reads.</span></span> <span data-ttu-id="ee946-115">Hello областей должны иметь имена с помощью их [отображаемые имена](https://msdn.microsoft.com/library/azure/gg441293.aspx), например `West US`.</span><span class="sxs-lookup"><span data-stu-id="ee946-115">hello regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span>

<span data-ttu-id="ee946-116">Все операции чтения будут передаваться первой доступной области toohello hello `TablePreferredLocations` списка.</span><span class="sxs-lookup"><span data-stu-id="ee946-116">All reads will be sent toohello first available region in hello `TablePreferredLocations` list.</span></span> <span data-ttu-id="ee946-117">Если hello запрос завершается неудачно, клиент hello ошибкой вниз область Далее toohello списка hello и так далее.</span><span class="sxs-lookup"><span data-stu-id="ee946-117">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span>

<span data-ttu-id="ee946-118">Hello SDK предпринимает попытку tooread из регионов hello, указанный в `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="ee946-118">hello SDK will only attempt tooread from hello regions specified in `TablePreferredLocations`.</span></span> <span data-ttu-id="ee946-119">Таким образом, например, hello учетной записи базы данных доступен в трех регионах, когда клиент hello только задает два hello записи областей для `TablePreferredLocations`, то никаких операций чтения будет обслуживается hello записи области, даже в случае hello перехода на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="ee946-119">So, for example, if hello Database Account is available in three regions, but hello client only specifies two of hello non-write regions for `TablePreferredLocations`, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="ee946-120">пакет SDK для Hello будет автоматически отправлять все записи toohello текущей записи области.</span><span class="sxs-lookup"><span data-stu-id="ee946-120">hello SDK will automatically send all writes toohello current write region.</span></span>

<span data-ttu-id="ee946-121">Если hello `TablePreferredLocations` свойство не задано, все запросы будут поступать из hello текущей записи области.</span><span class="sxs-lookup"><span data-stu-id="ee946-121">If hello `TablePreferredLocations` property is not set, all requests will be served from hello current write region.</span></span>

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

<span data-ttu-id="ee946-122">На этом руководство завершено.</span><span class="sxs-lookup"><span data-stu-id="ee946-122">That's it, that completes this tutorial.</span></span> <span data-ttu-id="ee946-123">Вы узнаете, как toomanage hello согласованности глобально реплицируемым учетной записи пользователя, считывая [уровни согласованности в базе данных Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="ee946-123">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="ee946-124">Сведения о том, как функционирует репликация глобальной базы данных в Azure Cosmos DB, см. в статье о [глобальном распределении данных в Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="ee946-124">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee946-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ee946-125">Next steps</span></span>

<span data-ttu-id="ee946-126">В этом учебнике вы сделали hello следующее:</span><span class="sxs-lookup"><span data-stu-id="ee946-126">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ee946-127">Настройка глобальных распространения, с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="ee946-127">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="ee946-128">Настройка глобальных распространения, с помощью hello интерфейсы API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="ee946-128">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="ee946-129">Теперь можно перейти далее учебника toolearn toohello как toodevelop локально с помощью hello локальный эмулятор Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ee946-129">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ee946-130">Разрабатывать локально в эмуляторе hello</span><span class="sxs-lookup"><span data-stu-id="ee946-130">Develop locally with hello emulator</span></span>](local-emulator.md)
