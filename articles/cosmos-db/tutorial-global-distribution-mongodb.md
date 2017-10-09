---
title: "Учебник глобального распространения Cosmos DB aaaAzure для MongoDB API | Документы Microsoft"
description: "Узнайте, как toosetup Azure Cosmos DB глобального распространителя с помощью hello MongoDB API."
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
ms.openlocfilehash: 0fc2d670bb4e21ac5f813f9586b407ba06ccf354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-mongodb-api"></a><span data-ttu-id="385fe-104">Как toosetup Azure Cosmos DB глобального распространителя с помощью MongoDB API hello</span><span class="sxs-lookup"><span data-stu-id="385fe-104">How toosetup Azure Cosmos DB global distribution using hello MongoDB API</span></span>

<span data-ttu-id="385fe-105">В этой статье показано, как toouse hello Azure toosetup портала Azure Cosmos DB глобального распространения, а затем подключитесь с помощью MongoDB API hello.</span><span class="sxs-lookup"><span data-stu-id="385fe-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello MongoDB API.</span></span>

<span data-ttu-id="385fe-106">В этой статье рассматриваются hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="385fe-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="385fe-107">Настройка глобальных распространения, с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="385fe-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="385fe-108">Настройка глобальных распространения, с помощью hello [MongoDB API](mongodb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="385fe-108">Configure global distribution using hello [MongoDB API](mongodb-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-hello-mongodb-api"></a><span data-ttu-id="385fe-109">Проверка на региональные настройки, с помощью MongoDB API hello</span><span class="sxs-lookup"><span data-stu-id="385fe-109">Verifying your regional setup using hello MongoDB API</span></span>
<span data-ttu-id="385fe-110">самым простым способом Hello типа double, проверку глобальной конфигурации в API MongoDB toorun hello *isMaster()* из hello оболочку Mongo.</span><span class="sxs-lookup"><span data-stu-id="385fe-110">hello simplest way of double checking your global configuration within API for MongoDB is toorun hello *isMaster()* command from hello Mongo Shell.</span></span>

<span data-ttu-id="385fe-111">Из оболочки Mongo:</span><span class="sxs-lookup"><span data-stu-id="385fe-111">From your Mongo Shell:</span></span>

   ```
      db.isMaster()
   ```
   
<span data-ttu-id="385fe-112">Пример результатов:</span><span class="sxs-lookup"><span data-stu-id="385fe-112">Example results:</span></span>

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

## <a name="connecting-tooa-preferred-region-using-hello-mongodb-api"></a><span data-ttu-id="385fe-113">Подключение tooa предпочтительную область с помощью MongoDB API hello</span><span class="sxs-lookup"><span data-stu-id="385fe-113">Connecting tooa preferred region using hello MongoDB API</span></span>

<span data-ttu-id="385fe-114">Hello MongoDB API позволяет вам toospecify вашей коллекции чтения предпочтения для распределенной базы данных.</span><span class="sxs-lookup"><span data-stu-id="385fe-114">hello MongoDB API enables you toospecify your collection's read preference for a globally distributed database.</span></span> <span data-ttu-id="385fe-115">Для обоих низкий задержки операций чтения и глобальные высокого уровня доступности, рекомендуется задать для вашей коллекции чтения предпочтений слишком*ближайшего*.</span><span class="sxs-lookup"><span data-stu-id="385fe-115">For both low latency reads and global high availability, we recommend setting your collection's read preference too*nearest*.</span></span> <span data-ttu-id="385fe-116">Чтение предпочтение *ближайшего* является настроенным tooread из hello ближайший регион.</span><span class="sxs-lookup"><span data-stu-id="385fe-116">A read preference of *nearest* is configured tooread from hello closest region.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

<span data-ttu-id="385fe-117">Для приложений с помощью основного чтения и записи региона и дополнительном регионе для аварийного восстановления (DR) сценарии, рекомендуется задать для вашей коллекции чтения предпочтений слишком*получателя предпочитаемый*.</span><span class="sxs-lookup"><span data-stu-id="385fe-117">For applications with a primary read/write region and a secondary region for disaster recovery (DR) scenarios, we recommend setting your collection's read preference too*secondary preferred*.</span></span> <span data-ttu-id="385fe-118">Чтение предпочтение *получателя предпочитаемый* является настроенным tooread из вторичного региона hello при недоступности основного региона hello.</span><span class="sxs-lookup"><span data-stu-id="385fe-118">A read preference of *secondary preferred* is configured tooread from hello secondary region when hello primary region is unavailable.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

<span data-ttu-id="385fe-119">Наконец Если как toomanually указывается в области чтения.</span><span class="sxs-lookup"><span data-stu-id="385fe-119">Lastly, if you would like toomanually specify your read regions.</span></span> <span data-ttu-id="385fe-120">Вы можете задать область hello тег чтения предпочтения.</span><span class="sxs-lookup"><span data-stu-id="385fe-120">You can set hello region Tag within your read preference.</span></span>

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

<span data-ttu-id="385fe-121">На этом руководство завершено.</span><span class="sxs-lookup"><span data-stu-id="385fe-121">That's it, that completes this tutorial.</span></span> <span data-ttu-id="385fe-122">Вы узнаете, как toomanage hello согласованности глобально реплицируемым учетной записи пользователя, считывая [уровни согласованности в базе данных Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="385fe-122">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="385fe-123">Сведения о том, как функционирует репликация глобальной базы данных в Azure Cosmos DB, см. в статье о [глобальном распределении данных в Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="385fe-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="385fe-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="385fe-124">Next steps</span></span>

<span data-ttu-id="385fe-125">В этом учебнике вы сделали hello следующее:</span><span class="sxs-lookup"><span data-stu-id="385fe-125">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="385fe-126">Настройка глобальных распространения, с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="385fe-126">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="385fe-127">Настройка глобальных распространения, с помощью hello интерфейсы API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="385fe-127">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="385fe-128">Теперь можно перейти далее учебника toolearn toohello как toodevelop локально с помощью hello локальный эмулятор Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="385fe-128">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="385fe-129">Разрабатывать локально в эмуляторе hello</span><span class="sxs-lookup"><span data-stu-id="385fe-129">Develop locally with hello emulator</span></span>](local-emulator.md)
