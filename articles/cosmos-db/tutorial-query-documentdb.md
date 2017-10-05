---
title: "Как выполнять запросы с помощью SQL в базе данных Azure Cosmos DB | Документация Майкрософт"
description: "Узнайте, как выполнять запросы с данными DocumentDB с помощью SQL в базе данных Azure Cosmos DB"
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
ms.openlocfilehash: a2a562c06c6302b9548e758b4c6754ec13b6001d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-using-sql"></a><span data-ttu-id="bb120-104">Как выполнять запросы с помощью SQL в базе данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bb120-104">Azure Cosmos DB: How to query using SQL?</span></span>

<span data-ttu-id="bb120-105">[API DocumentDB](documentdb-introduction.md) базы данных Azure Cosmos DB поддерживает запросы к документам с помощью SQL.</span><span class="sxs-lookup"><span data-stu-id="bb120-105">The Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) supports querying documents using SQL.</span></span> <span data-ttu-id="bb120-106">В этой статье содержится пример документа и два примера SQL-запросов и результатов.</span><span class="sxs-lookup"><span data-stu-id="bb120-106">This article provides a sample document and two sample SQL queries and results.</span></span>

<span data-ttu-id="bb120-107">В этой статье рассматриваются следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="bb120-107">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="bb120-108">Выполнение запросов к данным с помощью SQL.</span><span class="sxs-lookup"><span data-stu-id="bb120-108">Querying data with SQL</span></span>

## <a name="sample-document"></a><span data-ttu-id="bb120-109">Пример документа</span><span class="sxs-lookup"><span data-stu-id="bb120-109">Sample document</span></span>

<span data-ttu-id="bb120-110">Запросы SQL в этой статье используют следующий пример документа.</span><span class="sxs-lookup"><span data-stu-id="bb120-110">The SQL queries in this article use the following sample document.</span></span>

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
## <a name="where-can-i-run-sql-queries"></a><span data-ttu-id="bb120-111">Где могут выполняться SQL-запросы</span><span class="sxs-lookup"><span data-stu-id="bb120-111">Where can I run SQL queries?</span></span>

<span data-ttu-id="bb120-112">Вы можете выполнять запросы с помощью обозревателя данных на портале Azure, через [REST API и пакеты SDK](documentdb-sdk-dotnet.md) и даже через [площадку для запросов](https://www.documentdb.com/sql/demo), которая выполняет запросы с использованием существующего набора примера данных.</span><span class="sxs-lookup"><span data-stu-id="bb120-112">You can run queries using the Data Explorer in the Azure portal, via the [REST API and SDKs](documentdb-sdk-dotnet.md), and even the [Query playground](https://www.documentdb.com/sql/demo), which runs queries on an existing set of sample data.</span></span>

<span data-ttu-id="bb120-113">Дополнительные сведения об SQL-запросах см. в статье:</span><span class="sxs-lookup"><span data-stu-id="bb120-113">For more information about SQL queries, see:</span></span>
* [<span data-ttu-id="bb120-114">SQL-запросы и синтаксис SQL в DocumentDB</span><span class="sxs-lookup"><span data-stu-id="bb120-114">SQL query and SQL syntax</span></span>](documentdb-sql-query.md)

## <a name="prerequisites"></a><span data-ttu-id="bb120-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bb120-115">Prerequisites</span></span>

<span data-ttu-id="bb120-116">В этом руководстве предполагается, что у вас есть учетная запись и коллекция базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bb120-116">This tutorial assumes you have an Azure Cosmos DB account and collection.</span></span> <span data-ttu-id="bb120-117">У вас их нет?</span><span class="sxs-lookup"><span data-stu-id="bb120-117">Don't have any of those?</span></span> <span data-ttu-id="bb120-118">Завершите [краткое руководство](create-mongodb-nodejs.md) или [руководство разработчика](tutorial-develop-mongodb.md), чтобы создать учетную запись и коллекцию.</span><span class="sxs-lookup"><span data-stu-id="bb120-118">Complete the [5-minute quickstart](create-mongodb-nodejs.md) or the [developer tutorial](tutorial-develop-mongodb.md) to create an account and collection.</span></span>

## <a name="example-query-1"></a><span data-ttu-id="bb120-119">Пример запроса 1</span><span class="sxs-lookup"><span data-stu-id="bb120-119">Example query 1</span></span>

<span data-ttu-id="bb120-120">С учетом приведенного выше образца документа со сведениями о семье следующий SQL-запрос возвращает документы, в которых поле идентификатора соответствует `WakefieldFamily`.</span><span class="sxs-lookup"><span data-stu-id="bb120-120">Given the sample family document above, following SQL query returns the documents where the id field matches `WakefieldFamily`.</span></span> <span data-ttu-id="bb120-121">Так как это инструкция `SELECT *`, результатом выполнения запроса является сформированный документ JSON:</span><span class="sxs-lookup"><span data-stu-id="bb120-121">Since it's a `SELECT *` statement, the output of the query is the complete JSON document:</span></span>

<span data-ttu-id="bb120-122">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="bb120-122">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

<span data-ttu-id="bb120-123">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="bb120-123">**Results**</span></span>

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

## <a name="example-query-2"></a><span data-ttu-id="bb120-124">Пример запроса 2</span><span class="sxs-lookup"><span data-stu-id="bb120-124">Example query 2</span></span>

<span data-ttu-id="bb120-125">Следующий запрос возвращает все заданные имена детей в семье, идентификатор которых соответствует `WakefieldFamily`, упорядоченные по классу обучения.</span><span class="sxs-lookup"><span data-stu-id="bb120-125">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by their grade.</span></span>

<span data-ttu-id="bb120-126">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="bb120-126">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

<span data-ttu-id="bb120-127">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="bb120-127">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a><span data-ttu-id="bb120-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bb120-128">Next steps</span></span>

<span data-ttu-id="bb120-129">В этом руководстве вы выполнили следующее:</span><span class="sxs-lookup"><span data-stu-id="bb120-129">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bb120-130">Вы научились выполнять запросы с помощью SQL.</span><span class="sxs-lookup"><span data-stu-id="bb120-130">Learned how to query using SQL</span></span>  

<span data-ttu-id="bb120-131">Теперь вы можете приступать к следующему руководству, чтобы узнать, как глобально распределять данные.</span><span class="sxs-lookup"><span data-stu-id="bb120-131">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bb120-132">Глобальное распределение данных</span><span class="sxs-lookup"><span data-stu-id="bb120-132">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)

