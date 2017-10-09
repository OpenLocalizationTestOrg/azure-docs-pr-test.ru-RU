---
title: "aaaReliableConcurrentQueue в Azure Service Fabric"
description: "Надежная параллельная очередь — это очередь с высокой пропускной способностью, что позволяет параллельно ставить в очередь и выводить из нее."
services: service-fabric
documentationcenter: .net
author: sangarg
manager: timlt
editor: raja,tyadam,masnider,vturecek
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: sangarg
ms.openlocfilehash: 78a9905996b9ab265c1288d2b49753638d7bc445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliableconcurrentqueue-in-azure-service-fabric"></a><span data-ttu-id="c6dd5-103">TooReliableConcurrentQueue введение в Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c6dd5-103">Introduction tooReliableConcurrentQueue in Azure Service Fabric</span></span>
<span data-ttu-id="c6dd5-104">Надежная параллельная очередь — это асинхронная, транзакционная и реплицируемая очередь, которая обладает высокой степенью параллелизма при операциях постановки в очередь и вывода из нее.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-104">Reliable Concurrent Queue is an asynchronous, transactional, and replicated queue which features high concurrency for enqueue and dequeue operations.</span></span> <span data-ttu-id="c6dd5-105">Спроектированный toodeliver высокой пропускной способностью и малой задержкой, двухнедельного hello строгого FIFO упорядочение, предоставляемые [надежные очереди](https://msdn.microsoft.com/library/azure/dn971527.aspx) и вместо этого предоставляет возможность заказа по наилучшим образом.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-105">It is designed toodeliver high throughput and low latency by relaxing hello strict FIFO ordering provided by [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) and instead provides a best-effort ordering.</span></span>

## <a name="apis"></a><span data-ttu-id="c6dd5-106">Интерфейсы API</span><span class="sxs-lookup"><span data-stu-id="c6dd5-106">APIs</span></span>

|<span data-ttu-id="c6dd5-107">Параллельная очередь</span><span class="sxs-lookup"><span data-stu-id="c6dd5-107">Concurrent Queue</span></span>                |<span data-ttu-id="c6dd5-108">Надежная параллельная очередь</span><span class="sxs-lookup"><span data-stu-id="c6dd5-108">Reliable Concurrent Queue</span></span>                                         |
|--------------------------------|------------------------------------------------------------------|
| <span data-ttu-id="c6dd5-109">void Enqueue(T item)</span><span class="sxs-lookup"><span data-stu-id="c6dd5-109">void Enqueue(T item)</span></span>           | <span data-ttu-id="c6dd5-110">Task EnqueueAsync(ITransaction tx, T item)</span><span class="sxs-lookup"><span data-stu-id="c6dd5-110">Task EnqueueAsync(ITransaction tx, T item)</span></span>                       |
| <span data-ttu-id="c6dd5-111">bool TryDequeue(out T result)</span><span class="sxs-lookup"><span data-stu-id="c6dd5-111">bool TryDequeue(out T result)</span></span>  | <span data-ttu-id="c6dd5-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span><span class="sxs-lookup"><span data-stu-id="c6dd5-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span></span>  |
| <span data-ttu-id="c6dd5-113">int Count()</span><span class="sxs-lookup"><span data-stu-id="c6dd5-113">int Count()</span></span>                    | <span data-ttu-id="c6dd5-114">long Count()</span><span class="sxs-lookup"><span data-stu-id="c6dd5-114">long Count()</span></span>                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a><span data-ttu-id="c6dd5-115">Сравнение с [надежной очередью](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span><span class="sxs-lookup"><span data-stu-id="c6dd5-115">Comparison with [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span></span>

<span data-ttu-id="c6dd5-116">Надежные параллельной очереди предлагается в качестве альтернативы слишком[надежные очереди](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span><span class="sxs-lookup"><span data-stu-id="c6dd5-116">Reliable Concurrent Queue is offered as an alternative too[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span></span> <span data-ttu-id="c6dd5-117">Ее следует использовать в случаях, когда строгое упорядочение FIFO не требуется, так как модель FIFO требует уменьшения степени параллелизма.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-117">It should be used in cases where strict FIFO ordering is not required, as guaranteeing FIFO requires a tradeoff with concurrency.</span></span>  <span data-ttu-id="c6dd5-118">[Надежные очереди](https://msdn.microsoft.com/library/azure/dn971527.aspx) использует блокировки tooenforce FIFO упорядочение, с tooenqueue допускается не более одной транзакции и одновременно может выполняться toodequeue более одной транзакции.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-118">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) uses locks tooenforce FIFO ordering, with at most one transaction allowed tooenqueue and at most one transaction allowed toodequeue at a time.</span></span> <span data-ttu-id="c6dd5-119">В отличие от этого надежного параллельной очереди снижает hello упорядочение ограничение позволяет любое число параллельных транзакций toointerleave их постановки в очередь и вывода из очереди операций.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-119">In comparison, Reliable Concurrent Queue relaxes hello ordering constraint and allows any number concurrent transactions toointerleave their enqueue and dequeue operations.</span></span> <span data-ttu-id="c6dd5-120">Упорядочение усилия предоставляется, однако hello относительный порядок два значения в надежных параллельной очереди может никогда не гарантируется.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-120">Best-effort ordering is provided, however hello relative ordering of two values in a Reliable Concurrent Queue can never be guaranteed.</span></span>

<span data-ttu-id="c6dd5-121">Надежная параллельная очередь обеспечивает высокую пропускную способность и более низкую задержку, чем [надежная очередь](https://msdn.microsoft.com/library/azure/dn971527.aspx), во всех случаях, когда имеется несколько параллельных транзакций, выполняющих постановку в очередь и вывод из нее.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-121">Reliable Concurrent Queue provides higher throughput and lower latency than [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) whenever there are multiple concurrent transactions performing enqueues and/or dequeues.</span></span>

<span data-ttu-id="c6dd5-122">Образец Сфера применения hello ReliableConcurrentQueue — hello [очереди сообщений](https://en.wikipedia.org/wiki/Message_queue) сценария.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-122">A sample use case for hello ReliableConcurrentQueue is hello [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario.</span></span> <span data-ttu-id="c6dd5-123">В этом сценарии один или несколько отправителями сообщений создайте и добавьте очередь toohello элементов и один или несколько сообщений потребителям извлекать сообщения из очереди hello и их обработка.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-123">In this scenario, one or more message producers create and add items toohello queue, and one or more message consumers pull messages from hello queue and process them.</span></span> <span data-ttu-id="c6dd5-124">Несколько производители и потребители могут работать независимо, с помощью параллельных транзакций в порядке tooprocess hello очереди.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-124">Multiple producers and consumers can work independently, using concurrent transactions in order tooprocess hello queue.</span></span>

## <a name="usage-guidelines"></a><span data-ttu-id="c6dd5-125">Рекомендации по использованию</span><span class="sxs-lookup"><span data-stu-id="c6dd5-125">Usage Guidelines</span></span>
* <span data-ttu-id="c6dd5-126">очереди Hello ожидает, что hello элементы в очереди hello имеют низкий срок.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-126">hello queue expects that hello items in hello queue have a low retention period.</span></span> <span data-ttu-id="c6dd5-127">То есть hello элементов будет не остаются в очереди hello в течение долгого времени.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-127">That is, hello items would not stay in hello queue for a long time.</span></span>
* <span data-ttu-id="c6dd5-128">очередь Hello не гарантирует строгого FIFO упорядочение.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-128">hello queue does not guarantee strict FIFO ordering.</span></span>
* <span data-ttu-id="c6dd5-129">очередь Hello не считывает свои собственные записи.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-129">hello queue does not read its own writes.</span></span> <span data-ttu-id="c6dd5-130">Если элемент помещается в очередь в рамках транзакции, он не будет видимым tooa dequeuer внутри hello одной транзакции.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-130">If an item is enqueued within a transaction, it will not be visible tooa dequeuer within hello same transaction.</span></span>
* <span data-ttu-id="c6dd5-131">Операции вывода из очереди не изолированы друг от друга.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-131">Dequeues are not isolated from each other.</span></span> <span data-ttu-id="c6dd5-132">Если элемент *A* удален из очереди транзакций *txnA*, даже если *txnA* не фиксируется, элемент *A* не будет видимым tooa параллельных транзакции *txnB*.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-132">If item *A* is dequeued in transaction *txnA*, even though *txnA* is not committed, item *A* would not be visible tooa concurrent transaction *txnB*.</span></span>  <span data-ttu-id="c6dd5-133">Если *txnA* прерываний, *A* будет видимым слишком*txnB* немедленно.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-133">If *txnA* aborts, *A* will become visible too*txnB* immediately.</span></span>
* <span data-ttu-id="c6dd5-134">*TryPeekAsync* поведение может быть реализован с помощью *TryDequeueAsync* и затем прерывание транзакции hello.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-134">*TryPeekAsync* behavior can be implemented by using a *TryDequeueAsync* and then aborting hello transaction.</span></span> <span data-ttu-id="c6dd5-135">Пример этого можно найти в разделе шаблонам программирования hello.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-135">An example of this can be found in hello Programming Patterns section.</span></span>
* <span data-ttu-id="c6dd5-136">Число является нетранзакционным.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-136">Count is non-transactional.</span></span> <span data-ttu-id="c6dd5-137">Он может находиться используется tooget представление о hello количество элементов в очереди hello, но представляет на момент времени и нельзя полагаться.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-137">It can be used tooget an idea of hello number of elements in hello queue, but represents a point-in-time and cannot be relied upon.</span></span>
* <span data-ttu-id="c6dd5-138">Ресурсоемкие обработки hello исключенных из очереди элементов не должно выполняться хотя hello транзакция активна, tooavoid длительные транзакции, которые могут негативно повлиять на производительность в системе hello.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-138">Expensive processing on hello dequeued items should not be performed while hello transaction is active, tooavoid long-running transactions which may have a performance impact on hello system.</span></span>

## <a name="code-snippets"></a><span data-ttu-id="c6dd5-139">Фрагменты кода</span><span class="sxs-lookup"><span data-stu-id="c6dd5-139">Code Snippets</span></span>
<span data-ttu-id="c6dd5-140">Рассмотрим несколько фрагментов кода и ожидаемые выходные данные.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-140">Let us look at a few code snippets and their expected outputs.</span></span> <span data-ttu-id="c6dd5-141">Обработка исключений не рассматривается в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-141">Exception handling is ignored in this section.</span></span>

### <a name="enqueueasync"></a><span data-ttu-id="c6dd5-142">EnqueueAsync</span><span class="sxs-lookup"><span data-stu-id="c6dd5-142">EnqueueAsync</span></span>
<span data-ttu-id="c6dd5-143">Вот несколько фрагментов кода по использованию EnqueueAsync, после которых приведены ожидаемые выходные данные.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-143">Here are a few code snippets for using EnqueueAsync followed by their expected outputs.</span></span>

- <span data-ttu-id="c6dd5-144">*Вариант 1. Одно задание постановки в очередь*</span><span class="sxs-lookup"><span data-stu-id="c6dd5-144">*Case 1: Single Enqueue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="c6dd5-145">Предполагается hello задачи успешно завершена и, было параллельных транзакций нет Изменение очереди hello.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-145">Assume that hello task completed successfully, and that there were no concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="c6dd5-146">Hello пользователь может ожидать toocontain hello hello очередь элементы в одном из следующих заказов hello:</span><span class="sxs-lookup"><span data-stu-id="c6dd5-146">hello user can expect hello queue toocontain hello items in any of hello following orders:</span></span>

> <span data-ttu-id="c6dd5-147">10, 20</span><span class="sxs-lookup"><span data-stu-id="c6dd5-147">10, 20</span></span>

> <span data-ttu-id="c6dd5-148">20, 10</span><span class="sxs-lookup"><span data-stu-id="c6dd5-148">20, 10</span></span>


- <span data-ttu-id="c6dd5-149">*Вариант 2. Параллельное задание постановки в очередь*</span><span class="sxs-lookup"><span data-stu-id="c6dd5-149">*Case 2: Parallel Enqueue Task*</span></span>

```
// Parallel Task 1
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}

// Parallel Task 2
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 30, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 40, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="c6dd5-150">Предположим, что задачи hello завершено, что hello задачи выполняются параллельно и то, что существуют другие параллельные транзакции не изменение очереди hello.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-150">Assume that hello tasks completed successfully, that hello tasks ran in parallel, and that there were no other concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="c6dd5-151">Без вывода может приниматься о hello порядок элементов в очереди hello.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-151">No inference can be made about hello order of items in hello queue.</span></span> <span data-ttu-id="c6dd5-152">Для этого фрагмента кода отображения элементов hello в любой из hello 4!</span><span class="sxs-lookup"><span data-stu-id="c6dd5-152">For this code snippet, hello items may appear in any of hello 4!</span></span> <span data-ttu-id="c6dd5-153">возможных порядков.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-153">possible orderings.</span></span>  <span data-ttu-id="c6dd5-154">Hello очереди будет tookeep hello элементов в исходном порядке (в очереди) hello, но может быть принудительного tooreorder их из-за операций tooconcurrent или ошибки.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-154">hello queue will attempt tookeep hello items in hello original (enqueued) order, but may be forced tooreorder them due tooconcurrent operations or faults.</span></span>


### <a name="dequeueasync"></a><span data-ttu-id="c6dd5-155">DequeueAsync</span><span class="sxs-lookup"><span data-stu-id="c6dd5-155">DequeueAsync</span></span>
<span data-ttu-id="c6dd5-156">Вот несколько фрагментов кода по использованию TryDequeueAsync следуют hello ожидается выходов.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-156">Here are a few code snippets for using TryDequeueAsync followed by hello expected outputs.</span></span> <span data-ttu-id="c6dd5-157">Предположим, что эта очередь hello уже заполненные hello следующих элементов в очереди hello:</span><span class="sxs-lookup"><span data-stu-id="c6dd5-157">Assume that hello queue is already populated with hello following items in hello queue:</span></span>
> <span data-ttu-id="c6dd5-158">10, 20, 30, 40, 50, 60</span><span class="sxs-lookup"><span data-stu-id="c6dd5-158">10, 20, 30, 40, 50, 60</span></span>

- <span data-ttu-id="c6dd5-159">*Вариант 1. Одно задание вывода из очереди*</span><span class="sxs-lookup"><span data-stu-id="c6dd5-159">*Case 1: Single Dequeue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="c6dd5-160">Предполагается hello задачи успешно завершена и, было параллельных транзакций нет Изменение очереди hello.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-160">Assume that hello task completed successfully, and that there were no concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="c6dd5-161">Поскольку можно сделать без вывода о порядке hello hello элементов в очереди hello, любые три hello элементов может быть удален из очереди, в любом порядке.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-161">Since no inference can be made about hello order of hello items in hello queue, any three of hello items may be dequeued, in any order.</span></span> <span data-ttu-id="c6dd5-162">Hello очереди будет tookeep hello элементов в исходном порядке (в очереди) hello, но может быть принудительного tooreorder их из-за операций tooconcurrent или ошибки.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-162">hello queue will attempt tookeep hello items in hello original (enqueued) order, but may be forced tooreorder them due tooconcurrent operations or faults.</span></span>  

- <span data-ttu-id="c6dd5-163">*Вариант 2. Параллельное задание вывода из очереди*</span><span class="sxs-lookup"><span data-stu-id="c6dd5-163">*Case 2: Parallel Dequeue Task*</span></span>

```
// Parallel Task 1
List<int> dequeue1;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}

// Parallel Task 2
List<int> dequeue2;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}
```

<span data-ttu-id="c6dd5-164">Предположим, что задачи hello завершено, что hello задачи выполняются параллельно и то, что существуют другие параллельные транзакции не изменение очереди hello.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-164">Assume that hello tasks completed successfully, that hello tasks ran in parallel, and that there were no other concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="c6dd5-165">Поскольку можно сделать без вывода о порядке hello hello элементов в очереди hello, hello списки *dequeue1* и *dequeue2* будет каждый из которых содержит любые два элемента в любом порядке.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-165">Since no inference can be made about hello order of hello items in hello queue, hello lists *dequeue1* and *dequeue2* will each contain any two items, in any order.</span></span>

<span data-ttu-id="c6dd5-166">Hello же элемент будет *не* отображаются в обоих списках.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-166">hello same item will *not* appear in both lists.</span></span> <span data-ttu-id="c6dd5-167">Поэтому если dequeue1 имеет элемент *10*, *30*, то deque2 будет иметь элементы *20*, *40*.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-167">Hence, if dequeue1 has *10*, *30*, then dequeue2 would have *20*, *40*.</span></span>

- <span data-ttu-id="c6dd5-168">*Вариант 3. Упорядочение вывода из очереди с прерыванием транзакции*</span><span class="sxs-lookup"><span data-stu-id="c6dd5-168">*Case 3: Dequeue Ordering With Transaction Abort*</span></span>

<span data-ttu-id="c6dd5-169">Прерывание транзакции с лету выводит помещает элементы hello обратно на начало hello hello очереди.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-169">Aborting a transaction with in-flight dequeues puts hello items back on hello head of hello queue.</span></span> <span data-ttu-id="c6dd5-170">Hello порядок, в котором элементы hello помещаются обратно на начало hello hello очереди не гарантируется.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-170">hello order in which hello items are put back on hello head of hello queue is not guaranteed.</span></span> <span data-ttu-id="c6dd5-171">Рассмотрим hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="c6dd5-171">Let us look at hello following code:</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort hello transaction
    await txn.AbortAsync();
}
```
<span data-ttu-id="c6dd5-172">Предположим, hello элементы были из очереди в hello следующий порядок:</span><span class="sxs-lookup"><span data-stu-id="c6dd5-172">Assume that hello items were dequeued in hello following order:</span></span>
> <span data-ttu-id="c6dd5-173">10, 20</span><span class="sxs-lookup"><span data-stu-id="c6dd5-173">10, 20</span></span>

<span data-ttu-id="c6dd5-174">Когда мы прервать транзакцию hello, hello элементы будут добавлены в любой из следующих заказов hello начало обратной toohello hello очереди:</span><span class="sxs-lookup"><span data-stu-id="c6dd5-174">When we abort hello transaction, hello items would be added back toohello head of hello queue in any of hello following orders:</span></span>
> <span data-ttu-id="c6dd5-175">10, 20</span><span class="sxs-lookup"><span data-stu-id="c6dd5-175">10, 20</span></span>

> <span data-ttu-id="c6dd5-176">20, 10</span><span class="sxs-lookup"><span data-stu-id="c6dd5-176">20, 10</span></span>

<span data-ttu-id="c6dd5-177">Hello это справедливо для всех случаев, где hello транзакция не была успешно *зафиксировано*.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-177">hello same is true for all cases where hello transaction was not successfully *Committed*.</span></span>

## <a name="programming-patterns"></a><span data-ttu-id="c6dd5-178">Шаблоны программирования</span><span class="sxs-lookup"><span data-stu-id="c6dd5-178">Programming Patterns</span></span>
<span data-ttu-id="c6dd5-179">В этом разделе мы рассмотрим несколько шаблонов программирования, которые могут быть полезны при использовании надежной параллельной очереди.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-179">In this section, let us look at a few programming patterns that might be helpful in using ReliableConcurrentQueue.</span></span>

### <a name="batch-dequeues"></a><span data-ttu-id="c6dd5-180">Вывод из очереди в пакетном режиме</span><span class="sxs-lookup"><span data-stu-id="c6dd5-180">Batch Dequeues</span></span>
<span data-ttu-id="c6dd5-181">Рекомендуемое программирования шаблоном является toobatch задачи потребителя hello его выводит вместо выполнения одного вывода из очереди одновременно.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-181">A recommended programming pattern is for hello consumer task toobatch its dequeues instead of performing one dequeue at a time.</span></span> <span data-ttu-id="c6dd5-182">Hello пользователь может выбрать toothrottle задержки между каждого пакета или hello размер пакета.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-182">hello user can choose toothrottle delays between every batch or hello batch size.</span></span> <span data-ttu-id="c6dd5-183">Hello следующий фрагмент кода показывает этой модели программирования.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-183">hello following code snippet shows this programming model.</span></span>  <span data-ttu-id="c6dd5-184">Обратите внимание, что в этом примере hello обработки выполняется после фиксации, транзакции hello, будто ошибка toooccur при обработке hello необработанные элементы будут потеряны без обработки.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-184">Note that in this example, hello processing is done after hello transaction is committed, so if a fault were toooccur while processing, hello unprocessed items will be lost without having been processed.</span></span>  <span data-ttu-id="c6dd5-185">Кроме того, hello обработка может выполняться в пределах области транзакции hello, однако это может оказать отрицательное влияние на производительность и требует обработки элементов hello уже обработано.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-185">Alternatively, hello processing can be done within hello transaction's scope, however this may have a negative impact on performance and requires handling of hello items already processed.</span></span>

```
int batchSize = 5;
long delayMs = 100;

while(!cancellationToken.IsCancellationRequested)
{
    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        for(int i = 0; i < batchSize; ++i)
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
            else
            {
                // else break hello for loop
                break;
            }
        }

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }

    int delayFactor = batchSize - processItems.Count;
    await Task.Delay(TimeSpan.FromMilliseconds(delayMs * delayFactor), cancellationToken);
}
```

### <a name="best-effort-notification-based-processing"></a><span data-ttu-id="c6dd5-186">Оптимальная обработка на основе уведомлений</span><span class="sxs-lookup"><span data-stu-id="c6dd5-186">Best-Effort Notification-Based Processing</span></span>
<span data-ttu-id="c6dd5-187">Другой шаблон интересные программирования использует hello API счетчика.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-187">Another interesting programming pattern uses hello Count API.</span></span> <span data-ttu-id="c6dd5-188">Здесь можно реализовать обработку основанная на уведомлении усилия для очереди hello.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-188">Here, we can implement best-effort notification-based processing for hello queue.</span></span> <span data-ttu-id="c6dd5-189">очередь Hello число может быть используется toothrottle объект постановки в очередь или задача вывода из очереди.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-189">hello queue Count can be used toothrottle an enqueue or a dequeue task.</span></span>  <span data-ttu-id="c6dd5-190">Обратите внимание, что как в предыдущем примере hello, поскольку обработка hello происходит вне транзакции hello необработанные элементы могут быть потеряны при возникновении ошибки во время обработки.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-190">Note that as in hello previous example, since hello processing occurs outside hello transaction, unprocessed items may be lost if a fault occurs during processing.</span></span>

```
int threshold = 5;
long delayMs = 1000;

while(!cancellationToken.IsCancellationRequested)
{
    while (this.Queue.Count < threshold)
    {
        cancellationToken.ThrowIfCancellationRequested();

        // If hello queue does not have hello threshold number of items, delay hello task and check again
        await Task.Delay(TimeSpan.FromMilliseconds(delayMs), cancellationToken);
    }

    // If there are approximately threshold number of items, try and process hello queue

    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
        } while (processItems.Count < threshold && ret.HasValue);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
}
```

### <a name="best-effort-drain"></a><span data-ttu-id="c6dd5-191">Оптимальная очистка</span><span class="sxs-lookup"><span data-stu-id="c6dd5-191">Best-Effort Drain</span></span>
<span data-ttu-id="c6dd5-192">Очистку очереди hello не гарантируется из-за одновременных характер toohello hello структуры данных.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-192">A drain of hello queue cannot be guaranteed due toohello concurrent nature of hello data structure.</span></span>  <span data-ttu-id="c6dd5-193">Это возможно, что, даже если никакие операции пользователя hello очередь незавершенных, tooTryDequeueAsync конкретный вызов могут не возвращать элемент, который ранее было поставлено в очередь и фиксации.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-193">It is possible that, even if no user operations on hello queue are in-flight, a particular call tooTryDequeueAsync may not return an item which was previously enqueued and committed.</span></span>  <span data-ttu-id="c6dd5-194">элемент в очередь Hello гарантируется слишком*со временем* становятся видимыми toodequeue, однако без механизм взаимодействия по каналу потребителя независимых не знает, что очередь hello достигла устойчивого состояния даже в том случае, если все производители были остановлены, и новые операции постановки в очередь разрешены.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-194">hello enqueued item is guaranteed too*eventually* become visible toodequeue, however without an out-of-band communication mechanism, an independent consumer cannot know that hello queue has reached a steady-state even if all producers have been stopped and no new enqueue operations are allowed.</span></span> <span data-ttu-id="c6dd5-195">Таким образом операция очистки hello является наилучшим образом реализация ниже.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-195">Thus, hello drain operation is best-effort as implemented below.</span></span>

<span data-ttu-id="c6dd5-196">пользователь Hello следует остановить все последующие производителем и потребителем задачи и дождитесь любой транзакции на лету toocommit или прерывания, прежде чем toodrain hello очереди.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-196">hello user should stop all further producer and consumer tasks, and wait for any in-flight transactions toocommit or abort, before attempting toodrain hello queue.</span></span>  <span data-ttu-id="c6dd5-197">Если известно пользователю hello hello ожидалось число элементов в очереди hello, их можно настроить уведомления, который сигнализирует, что из очереди все элементы.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-197">If hello user knows hello expected number of items in hello queue, they can set up a notification which signals that all items have been dequeued.</span></span>

```
int numItemsDequeued;
int batchSize = 5;

ConditionalValue ret;

do
{
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if(ret.HasValue)
            {
                // Buffer hello dequeues
                processItems.Add(ret.Value);
            }
        } while (ret.HasValue && processItems.Count < batchSize);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
} while (ret.HasValue);
```

### <a name="peek"></a><span data-ttu-id="c6dd5-198">Обзор</span><span class="sxs-lookup"><span data-stu-id="c6dd5-198">Peek</span></span>
<span data-ttu-id="c6dd5-199">ReliableConcurrentQueue не предоставляет hello *TryPeekAsync* api.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-199">ReliableConcurrentQueue does not provide hello *TryPeekAsync* api.</span></span> <span data-ttu-id="c6dd5-200">Пользователи могут получить hello peek семантики с помощью *TryDequeueAsync* и затем прерывание транзакции hello.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-200">Users can get hello peek semantic by using a *TryDequeueAsync* and then aborting hello transaction.</span></span> <span data-ttu-id="c6dd5-201">В этом примере выводит обрабатываются только в том случае, если значение элемента hello больше, чем *10*.</span><span class="sxs-lookup"><span data-stu-id="c6dd5-201">In this example, dequeues are processed only if hello item's value is greater than *10*.</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    ConditionalValue ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);
    bool valueProcessed = false;

    if (ret.HasValue)
    {
        if (ret.Value > 10)
        {
            // Process hello item
            Console.WriteLine("Value : " + ret.Value);
            valueProcessed = true;
        }
    }

    if (valueProcessed)
    {
        await txn.CommitAsync();    
    }
    else
    {
        await txn.AbortAsync();
    }
}
```

## <a name="must-read"></a><span data-ttu-id="c6dd5-202">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="c6dd5-202">Must Read</span></span>
* [<span data-ttu-id="c6dd5-203">Приступая к работе с надежными службами</span><span class="sxs-lookup"><span data-stu-id="c6dd5-203">Reliable Services Quick Start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="c6dd5-204">Работа с Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="c6dd5-204">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="c6dd5-205">Уведомления Reliable Services</span><span class="sxs-lookup"><span data-stu-id="c6dd5-205">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="c6dd5-206">Резервное копирование и восстановление служб Reliable Services и субъектов Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="c6dd5-206">Reliable Services Backup and Restore (Disaster Recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="c6dd5-207">Настройка надежных служб с отслеживанием состояния</span><span class="sxs-lookup"><span data-stu-id="c6dd5-207">Reliable State Manager Configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="c6dd5-208">ASP.NET Core в Service Fabric Reliable Services</span><span class="sxs-lookup"><span data-stu-id="c6dd5-208">Getting Started with Service Fabric Web API Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="c6dd5-209">Расширенное использование hello надежная модель программирования служб</span><span class="sxs-lookup"><span data-stu-id="c6dd5-209">Advanced Usage of hello Reliable Services Programming Model</span></span>](service-fabric-reliable-services-advanced-usage.md)
* [<span data-ttu-id="c6dd5-210">Справочник разработчика по надежным коллекциям</span><span class="sxs-lookup"><span data-stu-id="c6dd5-210">Developer Reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
