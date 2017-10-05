---
title: "Условные выражения обработчика правил Azure CDN | Документация Майкрософт"
description: "Справочная документация по условиям соответствия и функциям обработчика правил Azure CDN."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 57e56c38e003cb83dcf44f455c4451d159db8a59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a><span data-ttu-id="e3ae7-103">Условные выражения обработчика правил Azure CDN</span><span class="sxs-lookup"><span data-stu-id="e3ae7-103">Azure CDN rules engine conditional expressions</span></span>
<span data-ttu-id="e3ae7-104">В этой статье подробно описаны условные выражения для [обработчика правил](cdn-rules-engine.md) сети доставки содержимого (CDN) Azure.</span><span class="sxs-lookup"><span data-stu-id="e3ae7-104">This topic lists detailed descriptions of the Conditional Expressions for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="e3ae7-105">Первая часть правила — это условное выражение.</span><span class="sxs-lookup"><span data-stu-id="e3ae7-105">The first part of a rule is the Conditional Expression.</span></span>

<span data-ttu-id="e3ae7-106">Условное выражение</span><span class="sxs-lookup"><span data-stu-id="e3ae7-106">Conditional Expression</span></span> | <span data-ttu-id="e3ae7-107">Описание</span><span class="sxs-lookup"><span data-stu-id="e3ae7-107">Description</span></span>
-----------------------|-------------
<span data-ttu-id="e3ae7-108">IF</span><span class="sxs-lookup"><span data-stu-id="e3ae7-108">IF</span></span> | <span data-ttu-id="e3ae7-109">Выражение IF всегда входит в первую инструкцию в правиле.</span><span class="sxs-lookup"><span data-stu-id="e3ae7-109">An IF expression is always a part of the first statement in a rule.</span></span> <span data-ttu-id="e3ae7-110">Как и другие условные выражения, инструкция IF должна быть связана с соответствием.</span><span class="sxs-lookup"><span data-stu-id="e3ae7-110">Like all other conditional expressions, this IF statement must be associated with a match.</span></span> <span data-ttu-id="e3ae7-111">Если дополнительные условные выражения не определены, это соответствие определяет условие, которое должно быть выполнено, прежде чем к запросу можно будет применить набор функций.</span><span class="sxs-lookup"><span data-stu-id="e3ae7-111">If no additional conditional expressions are defined, then this match determines the criterion that must be met before a set of features may be applied to a request.</span></span>
<span data-ttu-id="e3ae7-112">AND IF</span><span class="sxs-lookup"><span data-stu-id="e3ae7-112">AND IF</span></span> | <span data-ttu-id="e3ae7-113">Выражение AND IF можно добавлять только после таких условных выражений, как IF и AND IF.</span><span class="sxs-lookup"><span data-stu-id="e3ae7-113">An AND IF expression may only be added after the following types of conditional expressions:IF,AND IF.</span></span> <span data-ttu-id="e3ae7-114">Оно указывает на наличие другого условия, которое должно быть выполнено для первоначальной инструкции IF.</span><span class="sxs-lookup"><span data-stu-id="e3ae7-114">It indicates that there is another condition that must be met for the initial IF statement.</span></span>
<span data-ttu-id="e3ae7-115">ELSE IF</span><span class="sxs-lookup"><span data-stu-id="e3ae7-115">ELSE IF</span></span>| <span data-ttu-id="e3ae7-116">Выражение ELSE IF указывает альтернативное условие, которое должно быть выполнено до выполнения набора определенных функций для этой инструкции ELSE IF.</span><span class="sxs-lookup"><span data-stu-id="e3ae7-116">An ELSE IF expression specifies an alternative condition that must be met before a set of features specific to this ELSE IF statement takes place.</span></span> <span data-ttu-id="e3ae7-117">Инструкция ELSE IF указывает на конец предыдущей инструкции.</span><span class="sxs-lookup"><span data-stu-id="e3ae7-117">The presence of an ELSE IF statement indicates the end of the previous statement.</span></span> <span data-ttu-id="e3ae7-118">После инструкции ELSE IF можно добавить только инструкцию ELSE IF.</span><span class="sxs-lookup"><span data-stu-id="e3ae7-118">The only conditional expression that may be placed after an ELSE IF statement is another ELSE IF statement.</span></span> <span data-ttu-id="e3ae7-119">Это означает, что эту инструкцию можно использовать только для указания одного дополнительного условия, которое должно быть выполнено.</span><span class="sxs-lookup"><span data-stu-id="e3ae7-119">This means that an ELSE IF statement may only be used to specify a single additional condition that has to be met.</span></span>

<span data-ttu-id="e3ae7-120">**Пример**: ![соответствие условию CDN](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span><span class="sxs-lookup"><span data-stu-id="e3ae7-120">**Example**: ![CDN match condition](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span></span>

 > [!TIP]
   > <span data-ttu-id="e3ae7-121">Последующее правило может переопределить действия, заданные предыдущим правилом.</span><span class="sxs-lookup"><span data-stu-id="e3ae7-121">A subsequent rule may override the actions specified by a previous rule.</span></span> <span data-ttu-id="e3ae7-122">Например, универсальное правило защищает все запросы путем аутентификации на основе маркеров.</span><span class="sxs-lookup"><span data-stu-id="e3ae7-122">Example: A catch-all rule secures all requests via Token-Based Authentication.</span></span> <span data-ttu-id="e3ae7-123">Под ним можно создать другое правило, чтобы сделать исключение для некоторых типов запросов.</span><span class="sxs-lookup"><span data-stu-id="e3ae7-123">Another rule may be created directly below it to make an exception for certain types of requests.</span></span>

### <a name="next-steps"></a><span data-ttu-id="e3ae7-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e3ae7-124">Next steps</span></span>
* [<span data-ttu-id="e3ae7-125">Обзор Azure CDN</span><span class="sxs-lookup"><span data-stu-id="e3ae7-125">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="e3ae7-126">Справочник по обработчику правил</span><span class="sxs-lookup"><span data-stu-id="e3ae7-126">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="e3ae7-127">Условия соответствия обработчика правил</span><span class="sxs-lookup"><span data-stu-id="e3ae7-127">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="e3ae7-128">Функции обработчика правил</span><span class="sxs-lookup"><span data-stu-id="e3ae7-128">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="e3ae7-129">Переопределение стандартного поведения через HTTP с помощью обработчика правил</span><span class="sxs-lookup"><span data-stu-id="e3ae7-129">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)
