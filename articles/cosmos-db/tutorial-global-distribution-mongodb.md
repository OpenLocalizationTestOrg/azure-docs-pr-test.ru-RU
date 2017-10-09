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
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-mongodb-api"></a>Как toosetup Azure Cosmos DB глобального распространителя с помощью MongoDB API hello

В этой статье показано, как toouse hello Azure toosetup портала Azure Cosmos DB глобального распространения, а затем подключитесь с помощью MongoDB API hello.

В этой статье рассматриваются hello следующие задачи: 

> [!div class="checklist"]
> * Настройка глобальных распространения, с помощью портала Azure hello
> * Настройка глобальных распространения, с помощью hello [MongoDB API](mongodb-introduction.md)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]

## <a name="verifying-your-regional-setup-using-hello-mongodb-api"></a>Проверка на региональные настройки, с помощью MongoDB API hello
самым простым способом Hello типа double, проверку глобальной конфигурации в API MongoDB toorun hello *isMaster()* из hello оболочку Mongo.

Из оболочки Mongo:

   ```
      db.isMaster()
   ```
   
Пример результатов:

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

## <a name="connecting-tooa-preferred-region-using-hello-mongodb-api"></a>Подключение tooa предпочтительную область с помощью MongoDB API hello

Hello MongoDB API позволяет вам toospecify вашей коллекции чтения предпочтения для распределенной базы данных. Для обоих низкий задержки операций чтения и глобальные высокого уровня доступности, рекомендуется задать для вашей коллекции чтения предпочтений слишком*ближайшего*. Чтение предпочтение *ближайшего* является настроенным tooread из hello ближайший регион.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Nearest));
```

Для приложений с помощью основного чтения и записи региона и дополнительном регионе для аварийного восстановления (DR) сценарии, рекомендуется задать для вашей коллекции чтения предпочтений слишком*получателя предпочитаемый*. Чтение предпочтение *получателя предпочитаемый* является настроенным tooread из вторичного региона hello при недоступности основного региона hello.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.SecondaryPreferred));
```

Наконец Если как toomanually указывается в области чтения. Вы можете задать область hello тег чтения предпочтения.

```csharp
var collection = database.GetCollection<BsonDocument>(collectionName);
var tag = new Tag("region", "Southeast Asia");
collection = collection.WithReadPreference(new ReadPreference(ReadPreferenceMode.Secondary, new[] { new TagSet(new[] { tag }) }));
```

На этом руководство завершено. Вы узнаете, как toomanage hello согласованности глобально реплицируемым учетной записи пользователя, считывая [уровни согласованности в базе данных Azure Cosmos](consistency-levels.md). Сведения о том, как функционирует репликация глобальной базы данных в Azure Cosmos DB, см. в статье о [глобальном распределении данных в Azure Cosmos DB](distribute-data-globally.md).

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы сделали hello следующее:

> [!div class="checklist"]
> * Настройка глобальных распространения, с помощью портала Azure hello
> * Настройка глобальных распространения, с помощью hello интерфейсы API DocumentDB

Теперь можно перейти далее учебника toolearn toohello как toodevelop локально с помощью hello локальный эмулятор Azure Cosmos DB.

> [!div class="nextstepaction"]
> [Разрабатывать локально в эмуляторе hello](local-emulator.md)
