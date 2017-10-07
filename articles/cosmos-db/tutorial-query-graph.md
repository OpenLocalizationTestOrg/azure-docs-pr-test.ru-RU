---
title: "aaaHow tooquery графические данные в базе данных Azure Cosmos? | Документация Майкрософт"
description: "Дополнительные сведения tooquery графические данные в базе данных Azure Cosmos"
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
ms.openlocfilehash: fdde881edd6c488e2fea51e5c9665e1d736009fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-hello-graph-api-preview"></a><span data-ttu-id="aff6f-104">Azure Cosmos DB: Как tooquery с hello API Graph (Предварительная версия)?</span><span class="sxs-lookup"><span data-stu-id="aff6f-104">Azure Cosmos DB: How tooquery with hello Graph API (preview)?</span></span>

<span data-ttu-id="aff6f-105">Hello Azure Cosmos DB [Graph API](graph-introduction.md) (Предварительная версия) поддерживает [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) запросов.</span><span class="sxs-lookup"><span data-stu-id="aff6f-105">hello Azure Cosmos DB [Graph API](graph-introduction.md) (preview) supports [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) queries.</span></span> <span data-ttu-id="aff6f-106">Эта статья предоставляет образцы документов и запрашивает tooget, которого вы начали.</span><span class="sxs-lookup"><span data-stu-id="aff6f-106">This article provides sample documents and queries tooget you started.</span></span> <span data-ttu-id="aff6f-107">Подробные справочные сведения Gremlin предоставляется в hello [Gremlin поддержки](gremlin-support.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="aff6f-107">A detailed Gremlin reference is provided in hello [Gremlin support](gremlin-support.md) article.</span></span>

<span data-ttu-id="aff6f-108">В этой статье рассматриваются hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="aff6f-108">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="aff6f-109">Выполнение запросов к данным с помощью Gremlin.</span><span class="sxs-lookup"><span data-stu-id="aff6f-109">Querying data with Gremlin</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aff6f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="aff6f-110">Prerequisites</span></span>

<span data-ttu-id="aff6f-111">Для toowork эти запросы необходимо иметь учетную запись Azure Cosmos DB и иметь графические данные в контейнере hello.</span><span class="sxs-lookup"><span data-stu-id="aff6f-111">For these queries toowork, you must have an Azure Cosmos DB account and have graph data in hello container.</span></span> <span data-ttu-id="aff6f-112">У вас их нет?</span><span class="sxs-lookup"><span data-stu-id="aff6f-112">Don't have any of those?</span></span> <span data-ttu-id="aff6f-113">Полный hello [краткое руководство 5-минутного](create-graph-dotnet.md) или hello [учебнике для разработчиков](tutorial-query-graph.md) toocreate учетную запись и заполнить базу данных.</span><span class="sxs-lookup"><span data-stu-id="aff6f-113">Complete hello [5-minute quickstart](create-graph-dotnet.md) or hello [developer tutorial](tutorial-query-graph.md) toocreate an account and populate your database.</span></span> <span data-ttu-id="aff6f-114">Можно выполнить следующие запросы, использующие hello hello [библиотека Azure Cosmos DB .NET graph](graph-sdk-dotnet.md), [Gremlin консоли](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), или избранные Gremlin драйвера.</span><span class="sxs-lookup"><span data-stu-id="aff6f-114">You can run hello following queries using hello [Azure Cosmos DB .NET graph library](graph-sdk-dotnet.md), [Gremlin console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), or your favorite Gremlin driver.</span></span>

## <a name="count-vertices-in-hello-graph"></a><span data-ttu-id="aff6f-115">Число вершин в hello graph</span><span class="sxs-lookup"><span data-stu-id="aff6f-115">Count vertices in hello graph</span></span>

<span data-ttu-id="aff6f-116">Следующий фрагмент кода Hello показано, как toocount hello число вершин в hello graph.</span><span class="sxs-lookup"><span data-stu-id="aff6f-116">hello following snippet shows how toocount hello number of vertices in hello graph:</span></span>

```
g.V().count()
```

## <a name="filters"></a><span data-ttu-id="aff6f-117">Фильтры</span><span class="sxs-lookup"><span data-stu-id="aff6f-117">Filters</span></span>

<span data-ttu-id="aff6f-118">Можно выполнять фильтров с помощью элемента Gremlin `has` и `hasLabel` действия, а затем объедините их с помощью `and`, `or`, и `not` toobuild более сложные фильтры.</span><span class="sxs-lookup"><span data-stu-id="aff6f-118">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` toobuild more complex filters.</span></span> <span data-ttu-id="aff6f-119">База данных Azure Cosmos DB предоставляет схемонезависимое индексирование всех свойств в ваших вершинах и степенях для быстрого выполнения запросов:</span><span class="sxs-lookup"><span data-stu-id="aff6f-119">Azure Cosmos DB provides schema-agnostic indexing of all properties within your vertices and degrees for fast queries:</span></span>

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a><span data-ttu-id="aff6f-120">Проекция</span><span class="sxs-lookup"><span data-stu-id="aff6f-120">Projection</span></span>

<span data-ttu-id="aff6f-121">Вы можете проецировать некоторые свойства в hello результатов запроса, с помощью hello `values` шаг:</span><span class="sxs-lookup"><span data-stu-id="aff6f-121">You can project certain properties in hello query results using hello `values` step:</span></span>

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a><span data-ttu-id="aff6f-122">Поиск связанных ребер и вершин</span><span class="sxs-lookup"><span data-stu-id="aff6f-122">Find related edges and vertices</span></span>

<span data-ttu-id="aff6f-123">Пока мы видели только операторы запросов, которые работают в любой базе данных.</span><span class="sxs-lookup"><span data-stu-id="aff6f-123">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="aff6f-124">Графы быстрым и эффективным для обхода операций при необходимости toonavigate toorelated границ и вершин.</span><span class="sxs-lookup"><span data-stu-id="aff6f-124">Graphs are fast and efficient for traversal operations when you need toonavigate toorelated edges and vertices.</span></span> <span data-ttu-id="aff6f-125">Давайте найдем всех друзей Томаса.</span><span class="sxs-lookup"><span data-stu-id="aff6f-125">Let's find all friends of Thomas.</span></span> <span data-ttu-id="aff6f-126">Это делается с помощью элемента Gremlin `outE` шаг все hello исходящей линии Томаса toofind, а затем обходе toohello в вершины с границ с помощью элемента Gremlin `inV` шаг:</span><span class="sxs-lookup"><span data-stu-id="aff6f-126">We do this by using Gremlin's `outE` step toofind all hello out-edges from Thomas, then traversing toohello in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="aff6f-127">Hello следующий запрос выполняет два toofind прыжков все Thomas» друзьях друзей», путем вызова `outE` и `inV` два раза.</span><span class="sxs-lookup"><span data-stu-id="aff6f-127">hello next query performs two hops toofind all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="aff6f-128">Можно создавать более сложные запросы и реализовать логику обхода мощные graph с помощью Gremlin, включая смешивание фильтра, выражения, выполнение цикла с помощью hello `loop` шаг и реализации условной навигации с помощью hello `choose` шаг.</span><span class="sxs-lookup"><span data-stu-id="aff6f-128">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using hello `loop` step, and implementing conditional navigation using hello `choose` step.</span></span> <span data-ttu-id="aff6f-129">Дополнительные сведения о возможностях, допустимых благодаря поддержке Gremlin, см. в [этой статье](gremlin-support.md).</span><span class="sxs-lookup"><span data-stu-id="aff6f-129">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

## <a name="next-steps"></a><span data-ttu-id="aff6f-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aff6f-130">Next steps</span></span>

<span data-ttu-id="aff6f-131">В этом учебнике вы сделали hello следующее:</span><span class="sxs-lookup"><span data-stu-id="aff6f-131">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aff6f-132">Узнать, как с помощью Graph tooquery</span><span class="sxs-lookup"><span data-stu-id="aff6f-132">Learned how tooquery using Graph</span></span> 

<span data-ttu-id="aff6f-133">Вы можете теперь приступить Далее учебника toolearn toohello как toodistribute данных глобально.</span><span class="sxs-lookup"><span data-stu-id="aff6f-133">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aff6f-134">Глобальное распределение данных</span><span class="sxs-lookup"><span data-stu-id="aff6f-134">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)