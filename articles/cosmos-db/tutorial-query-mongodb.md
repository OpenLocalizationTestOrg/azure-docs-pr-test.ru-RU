---
title: "Azure Cosmos DB: Как с помощью tooquery hello DocumentDB API? | Документация Майкрософт"
description: "Дополнительные сведения tooquery с hello DocumentDB API для Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: e3e5a49f7510942bcfb15330e5f86c5dd8b1e5d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-api-for-mongodb"></a><span data-ttu-id="cf398-104">Azure Cosmos DB: Как tooquery с API-Интерфейс для MongoDB?</span><span class="sxs-lookup"><span data-stu-id="cf398-104">Azure Cosmos DB: How tooquery with API for MongoDB?</span></span>

<span data-ttu-id="cf398-105">Hello Azure Cosmos DB [API для MongoDB](mongodb-introduction.md) поддерживает [запросы оболочки MongoDB](https://docs.mongodb.com/manual/tutorial/query-documents/).</span><span class="sxs-lookup"><span data-stu-id="cf398-105">hello Azure Cosmos DB [API for MongoDB](mongodb-introduction.md) supports [MongoDB shell queries](https://docs.mongodb.com/manual/tutorial/query-documents/).</span></span> 

<span data-ttu-id="cf398-106">В этой статье рассматриваются hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="cf398-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="cf398-107">Запрос данных с помощью MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cf398-107">Querying data with MongoDB</span></span>

## <a name="sample-document"></a><span data-ttu-id="cf398-108">Пример документа</span><span class="sxs-lookup"><span data-stu-id="cf398-108">Sample document</span></span>

<span data-ttu-id="cf398-109">Hello запросы в этой статье используют следующий образец документа hello.</span><span class="sxs-lookup"><span data-stu-id="cf398-109">hello queries in this article use hello following sample document.</span></span>

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```
## <span data-ttu-id="cf398-110"><a id="examplequery1"></a> Пример запроса 1</span><span class="sxs-lookup"><span data-stu-id="cf398-110"><a id="examplequery1"></a> Example query 1</span></span> 

<span data-ttu-id="cf398-111">Имея hello образец семейства документа выше, hello следующий запрос возвращает документы hello которых соответствует поле id hello `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="cf398-111">Given hello sample family document above, hello following query returns hello documents where hello id field matches `WakefieldFamily`.</span></span>

<span data-ttu-id="cf398-112">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="cf398-112">**Query**</span></span>
    
    db.families.find({ id: “WakefieldFamily”})

<span data-ttu-id="cf398-113">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="cf398-113">**Results**</span></span>

    {
    "_id": "ObjectId(\"58f65e1198f3a12c7090e68c\")",
    "id": "WakefieldFamily",
    "parents": [
      {
        "familyName": "Wakefield",
        "givenName": "Robin"
      },
      {
        "familyName": "Miller",
        "givenName": "Ben"
      }
    ],
    "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
          { "givenName": "Goofy" },
          { "givenName": "Shadow" }
        ]
      },
      {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
      }
    ],
    "address": {
      "state": "NY",
      "county": "Manhattan",
      "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
    }

## <span data-ttu-id="cf398-114"><a id="examplequery2"></a> Пример запроса 2</span><span class="sxs-lookup"><span data-stu-id="cf398-114"><a id="examplequery2"></a>Example query 2</span></span> 

<span data-ttu-id="cf398-115">Hello следующий запрос возвращает все дочерние hello семейства hello.</span><span class="sxs-lookup"><span data-stu-id="cf398-115">hello next query returns all hello children in hello family.</span></span> 

<span data-ttu-id="cf398-116">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="cf398-116">**Query**</span></span>
    
    db.familes.find( { id: “WakefieldFamily” }, { children: true } )

<span data-ttu-id="cf398-117">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="cf398-117">**Results**</span></span>

    {
    "_id": "ObjectId("58f65e1198f3a12c7090e68c")",
    "children": [
      {
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [
          { "givenName": "Goofy" },
          { "givenName": "Shadow" }
        ]
      },
      {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
      }
    ]
    }


## <span data-ttu-id="cf398-118"><a id="examplequery3"></a> Пример запроса 3</span><span class="sxs-lookup"><span data-stu-id="cf398-118"><a id="examplequery3"></a>Example query 3</span></span> 

<span data-ttu-id="cf398-119">Hello следующий запрос возвращает все семейства hello, которые зарегистрированы.</span><span class="sxs-lookup"><span data-stu-id="cf398-119">hello next query returns all hello families which are registered.</span></span> 

<span data-ttu-id="cf398-120">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="cf398-120">**Query**</span></span>
    
    db.families.find( { "isRegistered" : true })
<span data-ttu-id="cf398-121">**Результаты** документ не будет возвращено.</span><span class="sxs-lookup"><span data-stu-id="cf398-121">**Results** No document will be returned.</span></span> 

## <span data-ttu-id="cf398-122"><a id="examplequery4"></a> Пример запроса 4</span><span class="sxs-lookup"><span data-stu-id="cf398-122"><a id="examplequery4"></a>Example query 4</span></span>

<span data-ttu-id="cf398-123">Hello следующий запрос возвращает все семейства hello, которые не зарегистрированы.</span><span class="sxs-lookup"><span data-stu-id="cf398-123">hello next query returns all hello families which are not registered.</span></span> 

<span data-ttu-id="cf398-124">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="cf398-124">**Query**</span></span>
    
    db.families.find( { "isRegistered" : false })
<span data-ttu-id="cf398-125">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="cf398-125">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="cf398-126">}</span><span class="sxs-lookup"><span data-stu-id="cf398-126">}</span></span>

## <span data-ttu-id="cf398-127"><a id="examplequery5"></a> Пример запроса 5</span><span class="sxs-lookup"><span data-stu-id="cf398-127"><a id="examplequery5"></a>Example query 5</span></span>

<span data-ttu-id="cf398-128">Hello следующий запрос возвращает все семейства hello, которые не регистрируются и состояние NY.</span><span class="sxs-lookup"><span data-stu-id="cf398-128">hello next query returns all hello families which are not registered and state is NY.</span></span> 

<span data-ttu-id="cf398-129">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="cf398-129">**Query**</span></span>
    
     db.families.find( { "isRegistered" : false, "address.state" : "NY" })

<span data-ttu-id="cf398-130">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="cf398-130">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="cf398-131">}</span><span class="sxs-lookup"><span data-stu-id="cf398-131">}</span></span>


## <span data-ttu-id="cf398-132"><a id="examplequery6"></a> Пример запроса 6</span><span class="sxs-lookup"><span data-stu-id="cf398-132"><a id="examplequery6"></a>Example query 6</span></span>

<span data-ttu-id="cf398-133">Hello следующий запрос возвращает всех семейств hello которых 8 уровней дочерних элементов.</span><span class="sxs-lookup"><span data-stu-id="cf398-133">hello next query returns all hello families where children grades are 8.</span></span>

<span data-ttu-id="cf398-134">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="cf398-134">**Query**</span></span>
  
     db.families.find( { children : { $elemMatch: { grade : 8 }} } )

<span data-ttu-id="cf398-135">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="cf398-135">**Results**</span></span>

     {
    "_id": ObjectId("58f65e1198f3a12c7090e68c"),
    "id": "WakefieldFamily",
    "parents": [{
        "familyName": "Wakefield",
        "givenName": "Robin"
    }, {
        "familyName": "Miller",
        "givenName": "Ben"
    }],
    "children": [{
        "familyName": "Merriam",
        "givenName": "Jesse",
        "gender": "female",
        "grade": 1,
        "pets": [{
            "givenName": "Goofy"
        }, {
            "givenName": "Shadow"
        }]
    }, {
        "familyName": "Miller",
        "givenName": "Lisa",
        "gender": "female",
        "grade": 8
    }],
    "address": {
        "state": "NY",
        "county": "Manhattan",
        "city": "NY"
    },
    "creationDate": 1431620462,
    "isRegistered": false
<span data-ttu-id="cf398-136">}</span><span class="sxs-lookup"><span data-stu-id="cf398-136">}</span></span>

## <span data-ttu-id="cf398-137"><a id="examplequery7"></a> Пример запроса 7</span><span class="sxs-lookup"><span data-stu-id="cf398-137"><a id="examplequery7"></a>Example query 7</span></span>

<span data-ttu-id="cf398-138">Hello следующий запрос возвращает всех семейств hello, где размер массива дочерние элементы — 3.</span><span class="sxs-lookup"><span data-stu-id="cf398-138">hello next query returns all hello families where size of children array is 3.</span></span>

<span data-ttu-id="cf398-139">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="cf398-139">**Query**</span></span>
  
      db.Family.find( {children: { $size:3} } )

<span data-ttu-id="cf398-140">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="cf398-140">**Results**</span></span>

<span data-ttu-id="cf398-141">Результаты не будут выведены, так как у семей в нашем файле не более 2 детей.</span><span class="sxs-lookup"><span data-stu-id="cf398-141">No results will be returned as we do not have more than 2 children.</span></span> <span data-ttu-id="cf398-142">Только в том случае, если параметр равен 2 этого запроса будет завершиться успешно и вернуть полный документ hello.</span><span class="sxs-lookup"><span data-stu-id="cf398-142">Only when parameter is 2 this query will succeed and return hello full document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf398-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cf398-143">Next steps</span></span>

<span data-ttu-id="cf398-144">В этом учебнике вы сделали hello следующее:</span><span class="sxs-lookup"><span data-stu-id="cf398-144">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cf398-145">Узнать, как с помощью MongoDB tooquery</span><span class="sxs-lookup"><span data-stu-id="cf398-145">Learned how tooquery using MongoDB</span></span> 

<span data-ttu-id="cf398-146">Вы можете теперь приступить Далее учебника toolearn toohello как toodistribute данных глобально.</span><span class="sxs-lookup"><span data-stu-id="cf398-146">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cf398-147">Глобальное распределение данных</span><span class="sxs-lookup"><span data-stu-id="cf398-147">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

