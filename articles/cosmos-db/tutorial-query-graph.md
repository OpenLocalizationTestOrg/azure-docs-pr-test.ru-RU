---
title: "Как выполнять запросы к данным графа в базе данных Azure Cosmos DB | Документация Майкрософт"
description: "Узнайте, как выполнять запросы к данным графа в базе данных Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 8bde5c80-581c-4f70-acb4-9578873c92fa
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 81713c72da037f127e81239d214d7a877247dca1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-how-to-query-with-the-graph-api-preview"></a><span data-ttu-id="ac86f-104">Как выполнять запросы к данным в базе данных Azure Cosmos DB с помощью API Graph (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="ac86f-104">Azure Cosmos DB: How to query with the Graph API (preview)?</span></span>

<span data-ttu-id="ac86f-105">[API Graph](graph-introduction.md) (предварительная версия) базы данных Azure Cosmos DB поддерживает запросы [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/).</span><span class="sxs-lookup"><span data-stu-id="ac86f-105">The Azure Cosmos DB [Graph API](graph-introduction.md) (preview) supports [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) queries.</span></span> <span data-ttu-id="ac86f-106">В этой статье приведены примеры документов и запросов, которые помогут вам начать работу.</span><span class="sxs-lookup"><span data-stu-id="ac86f-106">This article provides sample documents and queries to get you started.</span></span> <span data-ttu-id="ac86f-107">Подробная справка по Gremlin содержится в [этой статье](gremlin-support.md).</span><span class="sxs-lookup"><span data-stu-id="ac86f-107">A detailed Gremlin reference is provided in the [Gremlin support](gremlin-support.md) article.</span></span>

<span data-ttu-id="ac86f-108">В этой статье рассматриваются следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="ac86f-108">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="ac86f-109">Выполнение запросов к данным с помощью Gremlin.</span><span class="sxs-lookup"><span data-stu-id="ac86f-109">Querying data with Gremlin</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac86f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ac86f-110">Prerequisites</span></span>

<span data-ttu-id="ac86f-111">Чтобы такие запросы работали, у вас должна быть учетная запись базы данных Azure Cosmos DB и данные графа в контейнере.</span><span class="sxs-lookup"><span data-stu-id="ac86f-111">For these queries to work, you must have an Azure Cosmos DB account and have graph data in the container.</span></span> <span data-ttu-id="ac86f-112">У вас их нет?</span><span class="sxs-lookup"><span data-stu-id="ac86f-112">Don't have any of those?</span></span> <span data-ttu-id="ac86f-113">Завершите [краткое руководство](create-graph-dotnet.md) или [руководство разработчика](tutorial-query-graph.md), чтобы создать учетную запись и заполнить базу данных.</span><span class="sxs-lookup"><span data-stu-id="ac86f-113">Complete the [5-minute quickstart](create-graph-dotnet.md) or the [developer tutorial](tutorial-query-graph.md) to create an account and populate your database.</span></span> <span data-ttu-id="ac86f-114">Вы можете выполнить следующие запросы с помощью [библиотеки графов .NET базы данных Azure Cosmos DB](graph-sdk-dotnet.md), [консоли Gremlin](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) или предпочитаемого драйвера Gremlin.</span><span class="sxs-lookup"><span data-stu-id="ac86f-114">You can run the following queries using the [Azure Cosmos DB .NET graph library](graph-sdk-dotnet.md), [Gremlin console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), or your favorite Gremlin driver.</span></span>

## <a name="count-vertices-in-the-graph"></a><span data-ttu-id="ac86f-115">Подсчет вершин в графе</span><span class="sxs-lookup"><span data-stu-id="ac86f-115">Count vertices in the graph</span></span>

<span data-ttu-id="ac86f-116">В следующем фрагменте показано, как подсчитать количество вершин в графе:</span><span class="sxs-lookup"><span data-stu-id="ac86f-116">The following snippet shows how to count the number of vertices in the graph:</span></span>

```
g.V().count()
```

## <a name="filters"></a><span data-ttu-id="ac86f-117">Фильтры</span><span class="sxs-lookup"><span data-stu-id="ac86f-117">Filters</span></span>

<span data-ttu-id="ac86f-118">Вы можете выполнять фильтрацию с помощью шагов Gremlin `has` и `hasLabel`, а также объединять их с помощью операторов `and`, `or` и `not` для создания более сложных фильтров.</span><span class="sxs-lookup"><span data-stu-id="ac86f-118">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` to build more complex filters.</span></span> <span data-ttu-id="ac86f-119">База данных Azure Cosmos DB предоставляет схемонезависимое индексирование всех свойств в ваших вершинах и степенях для быстрого выполнения запросов:</span><span class="sxs-lookup"><span data-stu-id="ac86f-119">Azure Cosmos DB provides schema-agnostic indexing of all properties within your vertices and degrees for fast queries:</span></span>

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a><span data-ttu-id="ac86f-120">Проекция</span><span class="sxs-lookup"><span data-stu-id="ac86f-120">Projection</span></span>

<span data-ttu-id="ac86f-121">Вы можете проецировать некоторые свойства в результатах запроса с помощью шага `values`:</span><span class="sxs-lookup"><span data-stu-id="ac86f-121">You can project certain properties in the query results using the `values` step:</span></span>

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a><span data-ttu-id="ac86f-122">Поиск связанных ребер и вершин</span><span class="sxs-lookup"><span data-stu-id="ac86f-122">Find related edges and vertices</span></span>

<span data-ttu-id="ac86f-123">Пока мы видели только операторы запросов, которые работают в любой базе данных.</span><span class="sxs-lookup"><span data-stu-id="ac86f-123">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="ac86f-124">Графы способны быстро и эффективно выполнять операции обхода, когда вам необходимо перейти к связанным ребрам и вершинам.</span><span class="sxs-lookup"><span data-stu-id="ac86f-124">Graphs are fast and efficient for traversal operations when you need to navigate to related edges and vertices.</span></span> <span data-ttu-id="ac86f-125">Давайте найдем всех друзей Томаса.</span><span class="sxs-lookup"><span data-stu-id="ac86f-125">Let's find all friends of Thomas.</span></span> <span data-ttu-id="ac86f-126">Мы сделаем это с помощью шага Gremlin `outE`, чтобы найти все исходящие от Томаса ребра, а затем переместимся к вершинам исходящих ребер с помощью шага Gremlin `inV`:</span><span class="sxs-lookup"><span data-stu-id="ac86f-126">We do this by using Gremlin's `outE` step to find all the out-edges from Thomas, then traversing to the in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="ac86f-127">Следующий запрос выполняет два прыжка, чтобы найти всех друзей друзей Томаса, вызвав `outE` и `inV` два раза.</span><span class="sxs-lookup"><span data-stu-id="ac86f-127">The next query performs two hops to find all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="ac86f-128">Вы можете создавать более сложные запросы и внедрять эффективную логику обхода графа с помощью Gremlin, включая сочетание выражений фильтров, выполнение цикла с помощью шага `loop` и реализацию условной навигации с помощью шага `choose`.</span><span class="sxs-lookup"><span data-stu-id="ac86f-128">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using the `loop` step, and implementing conditional navigation using the `choose` step.</span></span> <span data-ttu-id="ac86f-129">Дополнительные сведения о возможностях, допустимых благодаря поддержке Gremlin, см. в [этой статье](gremlin-support.md).</span><span class="sxs-lookup"><span data-stu-id="ac86f-129">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac86f-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ac86f-130">Next steps</span></span>

<span data-ttu-id="ac86f-131">В этом руководстве вы выполнили следующее:</span><span class="sxs-lookup"><span data-stu-id="ac86f-131">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ac86f-132">Вы научились выполнять запросы с помощью Graph.</span><span class="sxs-lookup"><span data-stu-id="ac86f-132">Learned how to query using Graph</span></span> 

<span data-ttu-id="ac86f-133">Теперь вы можете приступать к следующему руководству, чтобы узнать, как глобально распределять данные.</span><span class="sxs-lookup"><span data-stu-id="ac86f-133">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ac86f-134">Глобальное распределение данных</span><span class="sxs-lookup"><span data-stu-id="ac86f-134">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)