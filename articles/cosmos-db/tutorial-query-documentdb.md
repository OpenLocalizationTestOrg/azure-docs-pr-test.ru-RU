---
title: "tooquery aaaHow с помощью SQL в базе данных Azure Cosmos? | Документация Майкрософт"
description: "Узнайте, tooquery с данным DocumentDB с помощью SQL в базе данных Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: tutorial-develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: d3dc51acf92cb78d4f4d9dbac7ec54b1382431cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-using-sql"></a><span data-ttu-id="98c72-104">Azure Cosmos DB: Как tooquery, с помощью SQL?</span><span class="sxs-lookup"><span data-stu-id="98c72-104">Azure Cosmos DB: How tooquery using SQL?</span></span>

<span data-ttu-id="98c72-105">Hello Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) поддерживает запросы документов с помощью SQL.</span><span class="sxs-lookup"><span data-stu-id="98c72-105">hello Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) supports querying documents using SQL.</span></span> <span data-ttu-id="98c72-106">В этой статье содержится пример документа и два примера SQL-запросов и результатов.</span><span class="sxs-lookup"><span data-stu-id="98c72-106">This article provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="98c72-107">В этой статье рассматриваются hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="98c72-107">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="98c72-108">Выполнение запросов к данным с помощью SQL.</span><span class="sxs-lookup"><span data-stu-id="98c72-108">Querying data with SQL</span></span>

## <a name="sample-document"></a><span data-ttu-id="98c72-109">Пример документа</span><span class="sxs-lookup"><span data-stu-id="98c72-109">Sample document</span></span>

<span data-ttu-id="98c72-110">Hello SQL-запросы в этой статье используйте следующий пример документа hello.</span><span class="sxs-lookup"><span data-stu-id="98c72-110">hello SQL queries in this article use hello following sample document.</span></span>

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
## <a name="where-can-i-run-sql-queries"></a><span data-ttu-id="98c72-111">Где могут выполняться SQL-запросы</span><span class="sxs-lookup"><span data-stu-id="98c72-111">Where can I run SQL queries?</span></span>

<span data-ttu-id="98c72-112">Может запускать запросы с использованием hello обозреватель данных в hello портал Azure, через hello [API-Интерфейс REST и пакеты SDK](documentdb-sdk-dotnet.md)и даже hello [площадку запросов](https://www.documentdb.com/sql/demo), который выполняет запросы в существующий набор данных выборки.</span><span class="sxs-lookup"><span data-stu-id="98c72-112">You can run queries using hello Data Explorer in hello Azure portal, via hello [REST API and SDKs](documentdb-sdk-dotnet.md), and even hello [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.</span></span>

<span data-ttu-id="98c72-113">Дополнительные сведения об SQL-запросах см. в статье:</span><span class="sxs-lookup"><span data-stu-id="98c72-113">For more information about SQL queries, see:</span></span>
* [<span data-ttu-id="98c72-114">SQL-запросы и синтаксис SQL в DocumentDB</span><span class="sxs-lookup"><span data-stu-id="98c72-114">SQL query and SQL syntax</span></span>](documentdb-sql-query.md)

## <a name="prerequisites"></a><span data-ttu-id="98c72-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="98c72-115">Prerequisites</span></span>

<span data-ttu-id="98c72-116">В этом руководстве предполагается, что у вас есть учетная запись и коллекция базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="98c72-116">This tutorial assumes you have an Azure Cosmos DB account and collection.</span></span> <span data-ttu-id="98c72-117">У вас их нет?</span><span class="sxs-lookup"><span data-stu-id="98c72-117">Don't have any of those?</span></span> <span data-ttu-id="98c72-118">Полный hello [краткое руководство 5-минутного](create-mongodb-nodejs.md) или hello [учебнике для разработчиков](tutorial-develop-mongodb.md) toocreate учетную запись и коллекции.</span><span class="sxs-lookup"><span data-stu-id="98c72-118">Complete hello [5-minute quickstart](create-mongodb-nodejs.md) or hello [developer tutorial](tutorial-develop-mongodb.md) toocreate an account and collection.</span></span>

## <a name="example-query-1"></a><span data-ttu-id="98c72-119">Пример запроса 1</span><span class="sxs-lookup"><span data-stu-id="98c72-119">Example query 1</span></span>

<span data-ttu-id="98c72-120">Заданы hello образец семейства документа выше, следующий SQL-запрос возвращает документы hello которых соответствует поле id hello `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="98c72-120">Given hello sample family document above, following SQL query returns hello documents where hello id field matches `WakefieldFamily`.</span></span> <span data-ttu-id="98c72-121">Поскольку это `SELECT *` инструкции hello выходных данных запроса hello является весь документ JSON hello:</span><span class="sxs-lookup"><span data-stu-id="98c72-121">Since it's a `SELECT *` statement, hello output of hello query is hello complete JSON document:</span></span>

<span data-ttu-id="98c72-122">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="98c72-122">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

<span data-ttu-id="98c72-123">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="98c72-123">**Results**</span></span>

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

## <a name="example-query-2"></a><span data-ttu-id="98c72-124">Пример запроса 2</span><span class="sxs-lookup"><span data-stu-id="98c72-124">Example query 2</span></span>

<span data-ttu-id="98c72-125">Hello следующий запрос возвращает все имена заданным hello дочерних элементов в hello семейства, идентификатор которого соответствует `WakefieldFamily` упорядоченный по их оценку.</span><span class="sxs-lookup"><span data-stu-id="98c72-125">hello next query returns all hello given names of children in hello family whose id matches `WakefieldFamily` ordered by their grade.</span></span>

<span data-ttu-id="98c72-126">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="98c72-126">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

<span data-ttu-id="98c72-127">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="98c72-127">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a><span data-ttu-id="98c72-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="98c72-128">Next steps</span></span>

<span data-ttu-id="98c72-129">В этом учебнике вы сделали hello следующее:</span><span class="sxs-lookup"><span data-stu-id="98c72-129">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="98c72-130">Узнать, как с помощью SQL tooquery</span><span class="sxs-lookup"><span data-stu-id="98c72-130">Learned how tooquery using SQL</span></span>  

<span data-ttu-id="98c72-131">Вы можете теперь приступить Далее учебника toolearn toohello как toodistribute данных глобально.</span><span class="sxs-lookup"><span data-stu-id="98c72-131">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="98c72-132">Глобальное распределение данных</span><span class="sxs-lookup"><span data-stu-id="98c72-132">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

