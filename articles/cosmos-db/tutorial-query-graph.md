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
# <a name="azure-cosmos-db-how-tooquery-with-hello-graph-api-preview"></a>Azure Cosmos DB: Как tooquery с hello API Graph (Предварительная версия)?

Hello Azure Cosmos DB [Graph API](graph-introduction.md) (Предварительная версия) поддерживает [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) запросов. Эта статья предоставляет образцы документов и запрашивает tooget, которого вы начали. Подробные справочные сведения Gremlin предоставляется в hello [Gremlin поддержки](gremlin-support.md) статьи.

В этой статье рассматриваются hello следующие задачи: 

> [!div class="checklist"]
> * Выполнение запросов к данным с помощью Gremlin.

## <a name="prerequisites"></a>Предварительные требования

Для toowork эти запросы необходимо иметь учетную запись Azure Cosmos DB и иметь графические данные в контейнере hello. У вас их нет? Полный hello [краткое руководство 5-минутного](create-graph-dotnet.md) или hello [учебнике для разработчиков](tutorial-query-graph.md) toocreate учетную запись и заполнить базу данных. Можно выполнить следующие запросы, использующие hello hello [библиотека Azure Cosmos DB .NET graph](graph-sdk-dotnet.md), [Gremlin консоли](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), или избранные Gremlin драйвера.

## <a name="count-vertices-in-hello-graph"></a>Число вершин в hello graph

Следующий фрагмент кода Hello показано, как toocount hello число вершин в hello graph.

```
g.V().count()
```

## <a name="filters"></a>Фильтры

Можно выполнять фильтров с помощью элемента Gremlin `has` и `hasLabel` действия, а затем объедините их с помощью `and`, `or`, и `not` toobuild более сложные фильтры. База данных Azure Cosmos DB предоставляет схемонезависимое индексирование всех свойств в ваших вершинах и степенях для быстрого выполнения запросов:

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a>Проекция

Вы можете проецировать некоторые свойства в hello результатов запроса, с помощью hello `values` шаг:

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a>Поиск связанных ребер и вершин

Пока мы видели только операторы запросов, которые работают в любой базе данных. Графы быстрым и эффективным для обхода операций при необходимости toonavigate toorelated границ и вершин. Давайте найдем всех друзей Томаса. Это делается с помощью элемента Gremlin `outE` шаг все hello исходящей линии Томаса toofind, а затем обходе toohello в вершины с границ с помощью элемента Gremlin `inV` шаг:

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

Hello следующий запрос выполняет два toofind прыжков все Thomas» друзьях друзей», путем вызова `outE` и `inV` два раза. 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

Можно создавать более сложные запросы и реализовать логику обхода мощные graph с помощью Gremlin, включая смешивание фильтра, выражения, выполнение цикла с помощью hello `loop` шаг и реализации условной навигации с помощью hello `choose` шаг. Дополнительные сведения о возможностях, допустимых благодаря поддержке Gremlin, см. в [этой статье](gremlin-support.md).

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы сделали hello следующее:

> [!div class="checklist"]
> * Узнать, как с помощью Graph tooquery 

Вы можете теперь приступить Далее учебника toolearn toohello как toodistribute данных глобально.

> [!div class="nextstepaction"]
> [Глобальное распределение данных](tutorial-global-distribution-documentdb.md)