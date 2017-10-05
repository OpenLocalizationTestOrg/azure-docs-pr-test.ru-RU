---
title: "Руководство по настройке глобального распределения Azure Cosmos DB с помощью API Graph | Документация Майкрософт"
description: "Сведения о настройке глобального распределения Azure Cosmos DB с помощью API Graph."
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
ms.openlocfilehash: 3c8794fe33c2ff5aa79559ea2c323cf8d92b426a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-graph-api"></a><span data-ttu-id="07c5d-104">Как настроить глобальное распределение Azure Cosmos DB с помощью API Graph</span><span class="sxs-lookup"><span data-stu-id="07c5d-104">How to setup Azure Cosmos DB global distribution using the Graph API</span></span>

<span data-ttu-id="07c5d-105">В этой статье показано, как настроить глобальное распределение базы данных Azure Cosmos DB и подключиться к ней с помощью API Graph (предварительная версия) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="07c5d-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the Graph API (preview).</span></span>

<span data-ttu-id="07c5d-106">В этой статье рассматриваются следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="07c5d-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="07c5d-107">настройка глобального распределения на портале Azure;</span><span class="sxs-lookup"><span data-stu-id="07c5d-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="07c5d-108">настройка глобального распределения с помощью [API-интерфейсов Graph](graph-introduction.md) (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="07c5d-108">Configure global distribution using the [Graph APIs](graph-introduction.md) (preview)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-graph-api-using-the-net-sdk"></a><span data-ttu-id="07c5d-109">Подключение к предпочтительному региону с помощью API Graph и пакета SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="07c5d-109">Connecting to a preferred region using the Graph API using the .NET SDK</span></span>

<span data-ttu-id="07c5d-110">API Graph предоставляется как библиотека расширений на базе пакета SDK для DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="07c5d-110">The Graph API is exposed as an extension library on top of the DocumentDB SDK.</span></span>

<span data-ttu-id="07c5d-111">Чтобы воспользоваться преимуществами [глобального распределения](distribute-data-globally.md), клиентские приложения могут указать упорядоченный список предпочитаемых регионов, который будет использоваться для операций с документами.</span><span class="sxs-lookup"><span data-stu-id="07c5d-111">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="07c5d-112">Это можно сделать, настроив политику подключения.</span><span class="sxs-lookup"><span data-stu-id="07c5d-112">This can be done by setting the connection policy.</span></span> <span data-ttu-id="07c5d-113">Для операций записи и чтения с помощью пакета SDK выбирается наиболее оптимальная конечная точка на основании текущих данных о региональной доступности и списка предпочтений, указанного в конфигурации учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="07c5d-113">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the SDK to perform write and read operations.</span></span>

<span data-ttu-id="07c5d-114">Этот список предпочтений указывается при инициализации подключения с помощью пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="07c5d-114">This preference list is specified when initializing a connection using the SDKs.</span></span> <span data-ttu-id="07c5d-115">Пакеты SDK принимают необязательный параметр PreferredLocations, представляющий собой упорядоченный список регионов Azure.</span><span class="sxs-lookup"><span data-stu-id="07c5d-115">The SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

* <span data-ttu-id="07c5d-116">**Операции записи.** Пакет SDK будет автоматически отправлять все операции записи в текущий регион записи.</span><span class="sxs-lookup"><span data-stu-id="07c5d-116">**Writes**: The SDK will automatically send all writes to the current write region.</span></span>
* <span data-ttu-id="07c5d-117">**Операции чтения.** Все операции чтения будут отправляться в первый доступный регион из списка PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="07c5d-117">**Reads**: All reads will be sent to the first available region in the PreferredLocations list.</span></span> <span data-ttu-id="07c5d-118">Если запрос завершится неудачей, клиент перейдет к следующему региону дальше по списку и так далее.</span><span class="sxs-lookup"><span data-stu-id="07c5d-118">If the request fails, the client will fail down the list to the next region, and so on.</span></span> <span data-ttu-id="07c5d-119">Пакеты SDK будут пытаться выполнять чтение данных из регионов, указанных в PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="07c5d-119">The SDKs will only attempt to read from the regions specified in PreferredLocations.</span></span> <span data-ttu-id="07c5d-120">Например, если учетная запись Cosmos DB доступна в трех регионах, но клиент указывает в PreferredLocations только два региона не для записи, то операции чтения из региона записи не будут обслуживаться даже в случае отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="07c5d-120">So, for example, if the Cosmos DB account is available in three regions, but the client only specifies two of the non-write regions for PreferredLocations, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="07c5d-121">Приложение может проверить текущие конечную точку записи и конечную точку чтения, выбранные пакетом SDK, просмотрев два свойства, WriteEndpoint и ReadEndpoint, доступные в SDK 1.8 и более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="07c5d-121">The application can verify the current write endpoint and read endpoint chosen by the SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span> <span data-ttu-id="07c5d-122">Если свойство PreferredLocations не задано, будут обслуживаться все запросы из текущего региона записи.</span><span class="sxs-lookup"><span data-stu-id="07c5d-122">If the PreferredLocations property is not set, all requests will be served from the current write region.</span></span>

### <a name="using-the-sdk"></a><span data-ttu-id="07c5d-123">Использование пакета SDK</span><span class="sxs-lookup"><span data-stu-id="07c5d-123">Using the SDK</span></span>

<span data-ttu-id="07c5d-124">Например, в пакете SDK для .NET параметр `ConnectionPolicy` для конструктора `DocumentClient` имеет свойство `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="07c5d-124">For example, in the .NET SDK, the `ConnectionPolicy` parameter for the `DocumentClient` constructor has a property called `PreferredLocations`.</span></span> <span data-ttu-id="07c5d-125">В качестве значения этого свойства можно задать список имен регионов.</span><span class="sxs-lookup"><span data-stu-id="07c5d-125">This property can be set to a list of region names.</span></span> <span data-ttu-id="07c5d-126">Отображаемые имена [регионов Azure][regions] можно указать в качестве значений `PreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="07c5d-126">The display names for [Azure Regions][regions] can be specified as part of `PreferredLocations`.</span></span>

> [!NOTE]
> <span data-ttu-id="07c5d-127">Не следует считать URL-адреса конечных точек долговременными константами.</span><span class="sxs-lookup"><span data-stu-id="07c5d-127">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="07c5d-128">Служба может обновить их в любой момент.</span><span class="sxs-lookup"><span data-stu-id="07c5d-128">The service may update these at any point.</span></span> <span data-ttu-id="07c5d-129">Пакет SDK обрабатывает это изменение автоматически.</span><span class="sxs-lookup"><span data-stu-id="07c5d-129">The SDK handles this change automatically.</span></span>
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

// connect to Azure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
```

<span data-ttu-id="07c5d-130">На этом руководство завершено.</span><span class="sxs-lookup"><span data-stu-id="07c5d-130">That's it, that completes this tutorial.</span></span> <span data-ttu-id="07c5d-131">Сведения об управлении согласованностью глобально реплицируемой учетной записи Azure Cosmos DB см. в [этой статье](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="07c5d-131">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="07c5d-132">Сведения о том, как функционирует репликация глобальной базы данных в Azure Cosmos DB, см. в статье о [глобальном распределении данных в Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="07c5d-132">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="07c5d-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="07c5d-133">Next steps</span></span>

<span data-ttu-id="07c5d-134">В этом руководстве вы выполнили следующее:</span><span class="sxs-lookup"><span data-stu-id="07c5d-134">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="07c5d-135">настроили глобальное распределение на портале Azure;</span><span class="sxs-lookup"><span data-stu-id="07c5d-135">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="07c5d-136">настроили глобальное распределение с помощью API-интерфейсов DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="07c5d-136">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="07c5d-137">Перейдите к следующему руководству, чтобы узнать о разработке в локальной среде с помощью локального эмулятора Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="07c5d-137">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="07c5d-138">Разработка в локальной среде с помощью эмулятора</span><span class="sxs-lookup"><span data-stu-id="07c5d-138">Develop locally with the emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

