---
title: "Руководство по настройке глобального распределения Azure Cosmos DB с помощью API таблицы | Документация Майкрософт"
description: "Сведения о настройке глобального распределения Azure Cosmos DB с помощью API таблицы."
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
ms.openlocfilehash: 63c9e530a4982e2e6e478fea56e015fc77851e1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-table-api"></a><span data-ttu-id="9a771-104">Как настроить глобальное распределение Azure Cosmos DB с помощью API таблицы</span><span class="sxs-lookup"><span data-stu-id="9a771-104">How to setup Azure Cosmos DB global distribution using the Table API</span></span>

<span data-ttu-id="9a771-105">В этой статье показано, как настроить глобальное распределение базы данных Azure Cosmos DB и подключиться к ней с помощью API таблицы (предварительная версия) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="9a771-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the Table API (preview).</span></span>

<span data-ttu-id="9a771-106">В этой статье рассматриваются следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="9a771-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="9a771-107">настройка глобального распределения на портале Azure;</span><span class="sxs-lookup"><span data-stu-id="9a771-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="9a771-108">настройка глобального распределения с помощью [API таблицы](table-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9a771-108">Configure global distribution using the [Table API](table-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-table-api"></a><span data-ttu-id="9a771-109">Подключение к предпочтительному региону с помощью API таблицы</span><span class="sxs-lookup"><span data-stu-id="9a771-109">Connecting to a preferred region using the Table API</span></span>

<span data-ttu-id="9a771-110">Чтобы воспользоваться преимуществами [глобального распределения](distribute-data-globally.md), клиентские приложения могут указать упорядоченный список предпочитаемых регионов, который будет использоваться для операций с документами.</span><span class="sxs-lookup"><span data-stu-id="9a771-110">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="9a771-111">Это можно сделать, задав значение `TablePreferredLocations` в конфигурации приложения для пакета SDK для службы хранилища Azure (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="9a771-111">This can be done by setting the `TablePreferredLocations` configuration value in the app config for the preview Azure Storage SDK.</span></span> <span data-ttu-id="9a771-112">Для операций записи и чтения с помощью пакета SDK для службы хранилища Azure выбирается наиболее оптимальная конечная точка на основании текущих данных о региональной доступности и списка предпочтений, указанного в конфигурации учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9a771-112">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the Azure Storage SDK to perform write and read operations.</span></span>

<span data-ttu-id="9a771-113">Свойство `TablePreferredLocations` должно содержать разделенный запятыми список предпочтительных расположений (множественная адресация) для операций чтения.</span><span class="sxs-lookup"><span data-stu-id="9a771-113">The `TablePreferredLocations` should contain a comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="9a771-114">Каждый экземпляр клиента может указать подмножество этих регионов в порядке предпочтения, чтобы обеспечить низкую задержку операций чтения.</span><span class="sxs-lookup"><span data-stu-id="9a771-114">Each client instance can specify a subset of these regions in the preferred order for low latency reads.</span></span> <span data-ttu-id="9a771-115">Регионам необходимо присвоить их [отображаемые имена](https://msdn.microsoft.com/library/azure/gg441293.aspx), например `West US`.</span><span class="sxs-lookup"><span data-stu-id="9a771-115">The regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span>

<span data-ttu-id="9a771-116">Все операции чтения будут отправляться в первый доступный регион из списка `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="9a771-116">All reads will be sent to the first available region in the `TablePreferredLocations` list.</span></span> <span data-ttu-id="9a771-117">Если запрос завершится неудачей, клиент перейдет к следующему региону дальше по списку и так далее.</span><span class="sxs-lookup"><span data-stu-id="9a771-117">If the request fails, the client will fail down the list to the next region, and so on.</span></span>

<span data-ttu-id="9a771-118">Пакеты SDK будут пытаться выполнять чтение данных из регионов, указанных в `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="9a771-118">The SDK will only attempt to read from the regions specified in `TablePreferredLocations`.</span></span> <span data-ttu-id="9a771-119">Например, если учетная запись базы данных доступна в трех регионах, но клиент указывает в `TablePreferredLocations` только два региона не для записи, то операции чтения из региона записи не будут обслуживаться даже в случае отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="9a771-119">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for `TablePreferredLocations`, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="9a771-120">Пакет SDK будет автоматически отправлять все операции записи в текущий регион записи.</span><span class="sxs-lookup"><span data-stu-id="9a771-120">The SDK will automatically send all writes to the current write region.</span></span>

<span data-ttu-id="9a771-121">Если свойство `TablePreferredLocations` не задано, будут обслуживаться все запросы из текущего региона записи.</span><span class="sxs-lookup"><span data-stu-id="9a771-121">If the `TablePreferredLocations` property is not set, all requests will be served from the current write region.</span></span>

```xml
    <appSettings>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>           
    </appSettings>
```

<span data-ttu-id="9a771-122">На этом руководство завершено.</span><span class="sxs-lookup"><span data-stu-id="9a771-122">That's it, that completes this tutorial.</span></span> <span data-ttu-id="9a771-123">Сведения об управлении согласованностью глобально реплицируемой учетной записи Azure Cosmos DB см. в [этой статье](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="9a771-123">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="9a771-124">Сведения о том, как функционирует репликация глобальной базы данных в Azure Cosmos DB, см. в статье о [глобальном распределении данных в Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="9a771-124">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a771-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9a771-125">Next steps</span></span>

<span data-ttu-id="9a771-126">В этом руководстве вы выполнили следующее:</span><span class="sxs-lookup"><span data-stu-id="9a771-126">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9a771-127">настроили глобальное распределение на портале Azure;</span><span class="sxs-lookup"><span data-stu-id="9a771-127">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="9a771-128">настроили глобальное распределение с помощью API-интерфейсов DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="9a771-128">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="9a771-129">Перейдите к следующему руководству, чтобы узнать о разработке в локальной среде с помощью локального эмулятора Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9a771-129">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9a771-130">Разработка в локальной среде с помощью эмулятора</span><span class="sxs-lookup"><span data-stu-id="9a771-130">Develop locally with the emulator</span></span>](local-emulator.md)