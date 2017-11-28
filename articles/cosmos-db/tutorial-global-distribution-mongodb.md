---
title: "Руководство по настройке глобального распределения Azure Cosmos DB с помощью API MongoDB | Документация Майкрософт"
description: "Сведения о настройке глобального распределения Azure Cosmos DB с помощью API MongoDB."
services: cosmos-db
keywords: "глобальное распределение, MongoDB"
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
ms.openlocfilehash: a2747102f4d8cac412b67abc3fd07cfa3661bcee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-mongodb-api"></a><span data-ttu-id="fe3f7-104">Как настроить глобальное распределение Azure Cosmos DB с помощью API MongoDB</span><span class="sxs-lookup"><span data-stu-id="fe3f7-104">How to setup Azure Cosmos DB global distribution using the MongoDB API</span></span>

<span data-ttu-id="fe3f7-105">В этой статье показано, как настроить глобальное распределение базы данных Azure Cosmos DB и подключиться к ней с помощью API MongoDB на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="fe3f7-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the MongoDB API.</span></span>

<span data-ttu-id="fe3f7-106">В этой статье рассматриваются следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="fe3f7-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="fe3f7-107">настройка глобального распределения на портале Azure;</span><span class="sxs-lookup"><span data-stu-id="fe3f7-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="fe3f7-108">настройка глобального распределения с помощью [API MongoDB](mongodb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fe3f7-108">Configure global distribution using the [MongoDB API](mongodb-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-the-mongodb-api"></a><span data-ttu-id="fe3f7-109">Проверка региональных настроек с помощью API MongoDB</span><span class="sxs-lookup"><span data-stu-id="fe3f7-109">Verifying your regional setup using the MongoDB API</span></span>
<span data-ttu-id="fe3f7-110">Самый простой способом еще раз проверить глобальную конфигурацию в API для MongoDB — это выполнить команду *isMaster()* из оболочки Mongo.</span><span class="sxs-lookup"><span data-stu-id="fe3f7-110">The simplest way of double checking your global configuration within API for MongoDB is to run the *isMaster()* command from the Mongo Shell.</span></span>

<span data-ttu-id="fe3f7-111">Из оболочки Mongo:</span><span class="sxs-lookup"><span data-stu-id="fe3f7-111">From your Mongo Shell:</span></span>

   ```
      db.isMaster()
   ```
   
<span data-ttu-id="fe3f7-112">Пример результатов:</span><span class="sxs-lookup"><span data-stu-id="fe3f7-112">Example results:</span></span>

   ```JSON
      {
         "_t": "IsMasterResponse",
         "ok": 1,
         "ismaster": true,
         "maxMessageSizeBytes": 4194304,
         "maxWriteBatchSize": 1000,
         "minWireVersion": 0,
         "maxWireVersion": 2,
         "tags": {
            "region": "South India"
         },
         "hosts": [
            "vishi-api-for-mongodb-southcentralus.documents.azure.com:10255",
            "vishi-api-for-mongodb-westeurope.documents.azure.com:10255",
            "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
         ],
         "setName": "globaldb",
         "setVersion": 1,
         "primary": "vishi-api-for-mongodb-southindia.documents.azure.com:10255",
         "me": "vishi-api-for-mongodb-southindia.documents.azure.com:10255"
      }
   ```

## <a name="connecting-to-a-preferred-region-using-the-mongodb-api"></a><span data-ttu-id="fe3f7-113">Подключение к предпочтительному региону с помощью API MongoDB</span><span class="sxs-lookup"><span data-stu-id="fe3f7-113">Connecting to a preferred region using the MongoDB API</span></span>

<span data-ttu-id="fe3f7-114">API MongoDB позволяет указать параметры чтения коллекции для глобально распределенной базы данных.</span><span class="sxs-lookup"><span data-stu-id="fe3f7-114">The MongoDB API enables you to specify your collection's read preference for a globally distributed database.</span></span> <span data-ttu-id="fe3f7-115">Для выполнения операций чтения с низкой задержкой и обеспечения глобальной высокой доступности рекомендуется задать в параметрах чтения коллекции значение *Nearest* (Ближайший).</span><span class="sxs-lookup"><span data-stu-id="fe3f7-115">For both low latency reads and global high availability, we recommend setting your collection's read preference to *nearest*.</span></span> <span data-ttu-id="fe3f7-116">Параметр *Nearest* означает, что чтение будет выполняться из ближайшего региона.</span><span class="sxs-lookup"><span data-stu-id="fe3f7-116">A read preference of *nearest* is configured to read from the closest region.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

<span data-ttu-id="fe3f7-117">Для приложений, использующих сценарии с основным регионом для операций чтения и записи и дополнительным регионом для аварийного восстановления, рекомендуется задать в параметрах чтения коллекции значение *SecondaryPreferred* (Предпочтительно дополнительный).</span><span class="sxs-lookup"><span data-stu-id="fe3f7-117">For applications with a primary read/write region and a secondary region for disaster recovery (DR) scenarios, we recommend setting your collection's read preference to *secondary preferred*.</span></span> <span data-ttu-id="fe3f7-118">Параметр *SecondaryPreferred* означает, что чтение будет выполняться из дополнительного региона при недоступности основного региона.</span><span class="sxs-lookup"><span data-stu-id="fe3f7-118">A read preference of *secondary preferred* is configured to read from the secondary region when the primary region is unavailable.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

<span data-ttu-id="fe3f7-119">Наконец, вы можете вручную указать регион для чтения.</span><span class="sxs-lookup"><span data-stu-id="fe3f7-119">Lastly, if you would like to manually specify your read regions.</span></span> <span data-ttu-id="fe3f7-120">Для этого задайте в параметрах чтения тег региона.</span><span class="sxs-lookup"><span data-stu-id="fe3f7-120">You can set the region Tag within your read preference.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

<span data-ttu-id="fe3f7-121">На этом руководство завершено.</span><span class="sxs-lookup"><span data-stu-id="fe3f7-121">That's it, that completes this tutorial.</span></span> <span data-ttu-id="fe3f7-122">Сведения об управлении согласованностью глобально реплицируемой учетной записи Azure Cosmos DB см. в [этой статье](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="fe3f7-122">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="fe3f7-123">Сведения о том, как функционирует репликация глобальной базы данных в Azure Cosmos DB, см. в статье о [глобальном распределении данных в Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="fe3f7-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe3f7-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fe3f7-124">Next steps</span></span>

<span data-ttu-id="fe3f7-125">В этом руководстве вы выполнили следующее:</span><span class="sxs-lookup"><span data-stu-id="fe3f7-125">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fe3f7-126">настроили глобальное распределение на портале Azure;</span><span class="sxs-lookup"><span data-stu-id="fe3f7-126">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="fe3f7-127">настроили глобальное распределение с помощью API-интерфейсов DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="fe3f7-127">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="fe3f7-128">Перейдите к следующему руководству, чтобы узнать о разработке в локальной среде с помощью локального эмулятора Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fe3f7-128">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fe3f7-129">Разработка в локальной среде с помощью эмулятора</span><span class="sxs-lookup"><span data-stu-id="fe3f7-129">Develop locally with the emulator</span></span>](local-emulator.md)