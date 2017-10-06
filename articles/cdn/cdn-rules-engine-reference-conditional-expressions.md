---
title: "условные выражения обработчик правил aaaAzure CDN | Документы Microsoft"
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
ms.openlocfilehash: 39d0754c34a577f77ca87b6fd92e2b6a9e4ff8fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a><span data-ttu-id="fc1ae-103">Условные выражения обработчика правил Azure CDN</span><span class="sxs-lookup"><span data-stu-id="fc1ae-103">Azure CDN rules engine conditional expressions</span></span>
<span data-ttu-id="fc1ae-104">В этом разделе приводятся подробные описания hello условные выражения для Azure доставки содержимого сети (CDN) [обработчик правил](cdn-rules-engine.md).</span><span class="sxs-lookup"><span data-stu-id="fc1ae-104">This topic lists detailed descriptions of hello Conditional Expressions for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="fc1ae-105">Первая часть Hello правила — hello условного выражения.</span><span class="sxs-lookup"><span data-stu-id="fc1ae-105">hello first part of a rule is hello Conditional Expression.</span></span>

<span data-ttu-id="fc1ae-106">Условное выражение</span><span class="sxs-lookup"><span data-stu-id="fc1ae-106">Conditional Expression</span></span> | <span data-ttu-id="fc1ae-107">Описание</span><span class="sxs-lookup"><span data-stu-id="fc1ae-107">Description</span></span>
-----------------------|-------------
<span data-ttu-id="fc1ae-108">IF</span><span class="sxs-lookup"><span data-stu-id="fc1ae-108">IF</span></span> | <span data-ttu-id="fc1ae-109">Если выражения всегда является частью hello первой инструкции в правиле.</span><span class="sxs-lookup"><span data-stu-id="fc1ae-109">An IF expression is always a part of hello first statement in a rule.</span></span> <span data-ttu-id="fc1ae-110">Как и другие условные выражения, инструкция IF должна быть связана с соответствием.</span><span class="sxs-lookup"><span data-stu-id="fc1ae-110">Like all other conditional expressions, this IF statement must be associated with a match.</span></span> <span data-ttu-id="fc1ae-111">Если не определены никакие дополнительные условного выражения, это совпадение определяет hello условий, которые должны быть выполнены перед набор возможностей, может быть применен tooa запросом.</span><span class="sxs-lookup"><span data-stu-id="fc1ae-111">If no additional conditional expressions are defined, then this match determines hello criterion that must be met before a set of features may be applied tooa request.</span></span>
<span data-ttu-id="fc1ae-112">AND IF</span><span class="sxs-lookup"><span data-stu-id="fc1ae-112">AND IF</span></span> | <span data-ttu-id="fc1ae-113">Выражение и если могут быть добавлены только после следующие типы условного выражения: Если, и если hello.</span><span class="sxs-lookup"><span data-stu-id="fc1ae-113">An AND IF expression may only be added after hello following types of conditional expressions:IF,AND IF.</span></span> <span data-ttu-id="fc1ae-114">Он указывает на наличие других проблем, которые должны быть выполнены для hello начальной инструкции IF.</span><span class="sxs-lookup"><span data-stu-id="fc1ae-114">It indicates that there is another condition that must be met for hello initial IF statement.</span></span>
<span data-ttu-id="fc1ae-115">ELSE IF</span><span class="sxs-lookup"><span data-stu-id="fc1ae-115">ELSE IF</span></span>| <span data-ttu-id="fc1ae-116">Выражение ELSE IF условие альтернативных, должны быть выполнены перед выполняется ряд определенных toothis возможности инструкции ELSE IF.</span><span class="sxs-lookup"><span data-stu-id="fc1ae-116">An ELSE IF expression specifies an alternative condition that must be met before a set of features specific toothis ELSE IF statement takes place.</span></span> <span data-ttu-id="fc1ae-117">наличие инструкции ELSE IF Здравствуй указывает hello конец предыдущей инструкции hello.</span><span class="sxs-lookup"><span data-stu-id="fc1ae-117">hello presence of an ELSE IF statement indicates hello end of hello previous statement.</span></span> <span data-ttu-id="fc1ae-118">Hello только условное выражение, которое можно поместить после инструкции ELSE IF другой инструкции ELSE IF.</span><span class="sxs-lookup"><span data-stu-id="fc1ae-118">hello only conditional expression that may be placed after an ELSE IF statement is another ELSE IF statement.</span></span> <span data-ttu-id="fc1ae-119">Это означает, что инструкции ELSE IF может быть только toospecify используется один дополнительное условие, которое имеет toobe выполнены.</span><span class="sxs-lookup"><span data-stu-id="fc1ae-119">This means that an ELSE IF statement may only be used toospecify a single additional condition that has toobe met.</span></span>

<span data-ttu-id="fc1ae-120">**Пример**: ![соответствие условию CDN](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span><span class="sxs-lookup"><span data-stu-id="fc1ae-120">**Example**: ![CDN match condition](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span></span>

 > [!TIP]
   > <span data-ttu-id="fc1ae-121">Последующие правила могут переопределять hello действия, указанные с помощью предыдущего правила.</span><span class="sxs-lookup"><span data-stu-id="fc1ae-121">A subsequent rule may override hello actions specified by a previous rule.</span></span> <span data-ttu-id="fc1ae-122">Например, универсальное правило защищает все запросы путем аутентификации на основе маркеров.</span><span class="sxs-lookup"><span data-stu-id="fc1ae-122">Example: A catch-all rule secures all requests via Token-Based Authentication.</span></span> <span data-ttu-id="fc1ae-123">Другое правило могут быть созданы непосредственно под toomake исключения для определенных типов запросов.</span><span class="sxs-lookup"><span data-stu-id="fc1ae-123">Another rule may be created directly below it toomake an exception for certain types of requests.</span></span>

### <a name="next-steps"></a><span data-ttu-id="fc1ae-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fc1ae-124">Next steps</span></span>
* [<span data-ttu-id="fc1ae-125">Обзор Azure CDN</span><span class="sxs-lookup"><span data-stu-id="fc1ae-125">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="fc1ae-126">Справочник по обработчику правил</span><span class="sxs-lookup"><span data-stu-id="fc1ae-126">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="fc1ae-127">Условия соответствия обработчика правил</span><span class="sxs-lookup"><span data-stu-id="fc1ae-127">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="fc1ae-128">Функции обработчика правил</span><span class="sxs-lookup"><span data-stu-id="fc1ae-128">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="fc1ae-129">Переопределение поведения по умолчанию HTTP с помощью модуля правил hello</span><span class="sxs-lookup"><span data-stu-id="fc1ae-129">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)
