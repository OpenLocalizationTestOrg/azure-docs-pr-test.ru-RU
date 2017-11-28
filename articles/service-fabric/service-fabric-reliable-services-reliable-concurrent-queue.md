---
title: "Надежная параллельная очередь в Azure Service Fabric"
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
ms.openlocfilehash: 122cb48149477f295a65b8ee623c647b6db10a86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-reliableconcurrentqueue-in-azure-service-fabric"></a><span data-ttu-id="78653-103">Введение в надежные параллельные очереди в Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="78653-103">Introduction to ReliableConcurrentQueue in Azure Service Fabric</span></span>
<span data-ttu-id="78653-104">Надежная параллельная очередь — это асинхронная, транзакционная и реплицируемая очередь, которая обладает высокой степенью параллелизма при операциях постановки в очередь и вывода из нее.</span><span class="sxs-lookup"><span data-stu-id="78653-104">Reliable Concurrent Queue is an asynchronous, transactional, and replicated queue which features high concurrency for enqueue and dequeue operations.</span></span> <span data-ttu-id="78653-105">Она предназначена для обеспечения высокой пропускной способности и низкой задержки. Она ослабляет строгое упорядочение FIFO, гарантируемое [надежной очередью](https://msdn.microsoft.com/library/azure/dn971527.aspx), и вместо этого обеспечивает упорядочение наилучшим возможным образом.</span><span class="sxs-lookup"><span data-stu-id="78653-105">It is designed to deliver high throughput and low latency by relaxing the strict FIFO ordering provided by [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) and instead provides a best-effort ordering.</span></span>

## <a name="apis"></a><span data-ttu-id="78653-106">Интерфейсы API</span><span class="sxs-lookup"><span data-stu-id="78653-106">APIs</span></span>

|<span data-ttu-id="78653-107">Параллельная очередь</span><span class="sxs-lookup"><span data-stu-id="78653-107">Concurrent Queue</span></span>                |<span data-ttu-id="78653-108">Надежная параллельная очередь</span><span class="sxs-lookup"><span data-stu-id="78653-108">Reliable Concurrent Queue</span></span>                                         |
|--------------------------------|------------------------------------------------------------------|
| <span data-ttu-id="78653-109">void Enqueue(T item)</span><span class="sxs-lookup"><span data-stu-id="78653-109">void Enqueue(T item)</span></span>           | <span data-ttu-id="78653-110">Task EnqueueAsync(ITransaction tx, T item)</span><span class="sxs-lookup"><span data-stu-id="78653-110">Task EnqueueAsync(ITransaction tx, T item)</span></span>                       |
| <span data-ttu-id="78653-111">bool TryDequeue(out T result)</span><span class="sxs-lookup"><span data-stu-id="78653-111">bool TryDequeue(out T result)</span></span>  | <span data-ttu-id="78653-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span><span class="sxs-lookup"><span data-stu-id="78653-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span></span>  |
| <span data-ttu-id="78653-113">int Count()</span><span class="sxs-lookup"><span data-stu-id="78653-113">int Count()</span></span>                    | <span data-ttu-id="78653-114">long Count()</span><span class="sxs-lookup"><span data-stu-id="78653-114">long Count()</span></span>                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a><span data-ttu-id="78653-115">Сравнение с [надежной очередью](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span><span class="sxs-lookup"><span data-stu-id="78653-115">Comparison with [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span></span>

<span data-ttu-id="78653-116">Надежная параллельная очередь предлагается в качестве альтернативы [надежной очереди](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span><span class="sxs-lookup"><span data-stu-id="78653-116">Reliable Concurrent Queue is offered as an alternative to [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span></span> <span data-ttu-id="78653-117">Ее следует использовать в случаях, когда строгое упорядочение FIFO не требуется, так как модель FIFO требует уменьшения степени параллелизма.</span><span class="sxs-lookup"><span data-stu-id="78653-117">It should be used in cases where strict FIFO ordering is not required, as guaranteeing FIFO requires a tradeoff with concurrency.</span></span>  <span data-ttu-id="78653-118">[Надежная очередь](https://msdn.microsoft.com/library/azure/dn971527.aspx) использует блокировки для принудительного упорядочивания FIFO, разрешая ставить в очередь и выводить из нее одновременно максимум одну транзакцию за раз.</span><span class="sxs-lookup"><span data-stu-id="78653-118">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) uses locks to enforce FIFO ordering, with at most one transaction allowed to enqueue and at most one transaction allowed to dequeue at a time.</span></span> <span data-ttu-id="78653-119">Для сравнения надежная параллельная очередь снижает ограничения упорядочивания и позволяет чередовать операции постановки в очередь и вывода из нее любому количеству параллельных транзакций.</span><span class="sxs-lookup"><span data-stu-id="78653-119">In comparison, Reliable Concurrent Queue relaxes the ordering constraint and allows any number concurrent transactions to interleave their enqueue and dequeue operations.</span></span> <span data-ttu-id="78653-120">Так обеспечивается упорядочивание наилучшим возможным образом, однако относительный порядок двух значений в надежной параллельной очереди не гарантируется.</span><span class="sxs-lookup"><span data-stu-id="78653-120">Best-effort ordering is provided, however the relative ordering of two values in a Reliable Concurrent Queue can never be guaranteed.</span></span>

<span data-ttu-id="78653-121">Надежная параллельная очередь обеспечивает высокую пропускную способность и более низкую задержку, чем [надежная очередь](https://msdn.microsoft.com/library/azure/dn971527.aspx), во всех случаях, когда имеется несколько параллельных транзакций, выполняющих постановку в очередь и вывод из нее.</span><span class="sxs-lookup"><span data-stu-id="78653-121">Reliable Concurrent Queue provides higher throughput and lower latency than [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) whenever there are multiple concurrent transactions performing enqueues and/or dequeues.</span></span>

<span data-ttu-id="78653-122">Пример использования надежной параллельной очереди — это сценарий с [очередью сообщений](https://en.wikipedia.org/wiki/Message_queue).</span><span class="sxs-lookup"><span data-stu-id="78653-122">A sample use case for the ReliableConcurrentQueue is the [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario.</span></span> <span data-ttu-id="78653-123">В этом сценарии один или несколько отправителей создают и добавляют элементы в очередь и один или несколько получателей извлекают сообщения из очереди и обрабатывают их.</span><span class="sxs-lookup"><span data-stu-id="78653-123">In this scenario, one or more message producers create and add items to the queue, and one or more message consumers pull messages from the queue and process them.</span></span> <span data-ttu-id="78653-124">Несколько отправителей и получателей могут работать независимо, используя параллельные транзакции для обработки очередей.</span><span class="sxs-lookup"><span data-stu-id="78653-124">Multiple producers and consumers can work independently, using concurrent transactions in order to process the queue.</span></span>

## <a name="usage-guidelines"></a><span data-ttu-id="78653-125">Рекомендации по использованию</span><span class="sxs-lookup"><span data-stu-id="78653-125">Usage Guidelines</span></span>
* <span data-ttu-id="78653-126">Очередь предполагает, что элементы в ней имеют низкий период удержания.</span><span class="sxs-lookup"><span data-stu-id="78653-126">The queue expects that the items in the queue have a low retention period.</span></span> <span data-ttu-id="78653-127">То есть элементы не будут оставаться в очереди в течение длительного времени.</span><span class="sxs-lookup"><span data-stu-id="78653-127">That is, the items would not stay in the queue for a long time.</span></span>
* <span data-ttu-id="78653-128">Очередь не гарантирует строгий порядок FIFO.</span><span class="sxs-lookup"><span data-stu-id="78653-128">The queue does not guarantee strict FIFO ordering.</span></span>
* <span data-ttu-id="78653-129">Очередь не считывает свои собственные записи.</span><span class="sxs-lookup"><span data-stu-id="78653-129">The queue does not read its own writes.</span></span> <span data-ttu-id="78653-130">Если элемент поставлен в очередь внутри транзакции, он не будет виден для средства вывода из очереди внутри той же транзакции.</span><span class="sxs-lookup"><span data-stu-id="78653-130">If an item is enqueued within a transaction, it will not be visible to a dequeuer within the same transaction.</span></span>
* <span data-ttu-id="78653-131">Операции вывода из очереди не изолированы друг от друга.</span><span class="sxs-lookup"><span data-stu-id="78653-131">Dequeues are not isolated from each other.</span></span> <span data-ttu-id="78653-132">Если элемент *A* выведен из очереди в транзакции *txnA*, тогда как *txnA* не зафиксирована, элемент *A* не будет виден параллельной транзакции *txnB*.</span><span class="sxs-lookup"><span data-stu-id="78653-132">If item *A* is dequeued in transaction *txnA*, even though *txnA* is not committed, item *A* would not be visible to a concurrent transaction *txnB*.</span></span>  <span data-ttu-id="78653-133">Если транзакция *txnA* прервется, элемент *A* немедленно станет видимым для транзакции *txnB*.</span><span class="sxs-lookup"><span data-stu-id="78653-133">If *txnA* aborts, *A* will become visible to *txnB* immediately.</span></span>
* <span data-ttu-id="78653-134">Поведение *TryPeekAsync* может быть реализовано с использонием метода *TryDequeueAsync* с последующим прерыванием транзакции.</span><span class="sxs-lookup"><span data-stu-id="78653-134">*TryPeekAsync* behavior can be implemented by using a *TryDequeueAsync* and then aborting the transaction.</span></span> <span data-ttu-id="78653-135">Пример можно найти в разделе "Шаблоны программирования".</span><span class="sxs-lookup"><span data-stu-id="78653-135">An example of this can be found in the Programming Patterns section.</span></span>
* <span data-ttu-id="78653-136">Число является нетранзакционным.</span><span class="sxs-lookup"><span data-stu-id="78653-136">Count is non-transactional.</span></span> <span data-ttu-id="78653-137">Это число позволяет получить представление о количестве элементов в очереди, но так как оно представляет данные на определенный момент времени, на него нельзя положиться.</span><span class="sxs-lookup"><span data-stu-id="78653-137">It can be used to get an idea of the number of elements in the queue, but represents a point-in-time and cannot be relied upon.</span></span>
* <span data-ttu-id="78653-138">Ресурсоемкая обработка выведенных из очереди элементов не должна выполняться во время транзакции, чтобы избежать продолжительных транзакций, которые могут оказывать влияние на работу системы.</span><span class="sxs-lookup"><span data-stu-id="78653-138">Expensive processing on the dequeued items should not be performed while the transaction is active, to avoid long-running transactions which may have a performance impact on the system.</span></span>

## <a name="code-snippets"></a><span data-ttu-id="78653-139">Фрагменты кода</span><span class="sxs-lookup"><span data-stu-id="78653-139">Code Snippets</span></span>
<span data-ttu-id="78653-140">Рассмотрим несколько фрагментов кода и ожидаемые выходные данные.</span><span class="sxs-lookup"><span data-stu-id="78653-140">Let us look at a few code snippets and their expected outputs.</span></span> <span data-ttu-id="78653-141">Обработка исключений не рассматривается в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="78653-141">Exception handling is ignored in this section.</span></span>

### <a name="enqueueasync"></a><span data-ttu-id="78653-142">EnqueueAsync</span><span class="sxs-lookup"><span data-stu-id="78653-142">EnqueueAsync</span></span>
<span data-ttu-id="78653-143">Вот несколько фрагментов кода по использованию EnqueueAsync, после которых приведены ожидаемые выходные данные.</span><span class="sxs-lookup"><span data-stu-id="78653-143">Here are a few code snippets for using EnqueueAsync followed by their expected outputs.</span></span>

- <span data-ttu-id="78653-144">*Вариант 1. Одно задание постановки в очередь*</span><span class="sxs-lookup"><span data-stu-id="78653-144">*Case 1: Single Enqueue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="78653-145">Предположим, что задача выполнена успешно и одновременные транзакции, изменяющие очередь, отсутствовали.</span><span class="sxs-lookup"><span data-stu-id="78653-145">Assume that the task completed successfully, and that there were no concurrent transactions modifying the queue.</span></span> <span data-ttu-id="78653-146">Очередь может содержать элементы в любом из следующих порядков:</span><span class="sxs-lookup"><span data-stu-id="78653-146">The user can expect the queue to contain the items in any of the following orders:</span></span>

> <span data-ttu-id="78653-147">10, 20</span><span class="sxs-lookup"><span data-stu-id="78653-147">10, 20</span></span>

> <span data-ttu-id="78653-148">20, 10</span><span class="sxs-lookup"><span data-stu-id="78653-148">20, 10</span></span>


- <span data-ttu-id="78653-149">*Вариант 2. Параллельное задание постановки в очередь*</span><span class="sxs-lookup"><span data-stu-id="78653-149">*Case 2: Parallel Enqueue Task*</span></span>

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

<span data-ttu-id="78653-150">Предположим, что задачи успешно завершены, они выполнялись параллельно и не было других одновременных транзакций, изменяющих очередь.</span><span class="sxs-lookup"><span data-stu-id="78653-150">Assume that the tasks completed successfully, that the tasks ran in parallel, and that there were no other concurrent transactions modifying the queue.</span></span> <span data-ttu-id="78653-151">Невозможно сделать вывод о порядке элементов в очереди.</span><span class="sxs-lookup"><span data-stu-id="78653-151">No inference can be made about the order of items in the queue.</span></span> <span data-ttu-id="78653-152">В этом фрагменте кода элементы могут отображаться в любом из 4</span><span class="sxs-lookup"><span data-stu-id="78653-152">For this code snippet, the items may appear in any of the 4!</span></span> <span data-ttu-id="78653-153">возможных порядков.</span><span class="sxs-lookup"><span data-stu-id="78653-153">possible orderings.</span></span>  <span data-ttu-id="78653-154">Очередь попытается разместить элементы в первоначальном порядке (постановки в очередь), но может быть вынуждена переупорядочить их из-за одновременных операций или сбоев.</span><span class="sxs-lookup"><span data-stu-id="78653-154">The queue will attempt to keep the items in the original (enqueued) order, but may be forced to reorder them due to concurrent operations or faults.</span></span>


### <a name="dequeueasync"></a><span data-ttu-id="78653-155">DequeueAsync</span><span class="sxs-lookup"><span data-stu-id="78653-155">DequeueAsync</span></span>
<span data-ttu-id="78653-156">Вот несколько фрагментов кода по использованию метода TryDequeueAsync, за которыми следуют ожидаемые выходные данные.</span><span class="sxs-lookup"><span data-stu-id="78653-156">Here are a few code snippets for using TryDequeueAsync followed by the expected outputs.</span></span> <span data-ttu-id="78653-157">Предположим, что очередь уже заполнена следующими элементами:</span><span class="sxs-lookup"><span data-stu-id="78653-157">Assume that the queue is already populated with the following items in the queue:</span></span>
> <span data-ttu-id="78653-158">10, 20, 30, 40, 50, 60</span><span class="sxs-lookup"><span data-stu-id="78653-158">10, 20, 30, 40, 50, 60</span></span>

- <span data-ttu-id="78653-159">*Вариант 1. Одно задание вывода из очереди*</span><span class="sxs-lookup"><span data-stu-id="78653-159">*Case 1: Single Dequeue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="78653-160">Предположим, что задача выполнена успешно и одновременные транзакции, изменяющие очередь, отсутствовали.</span><span class="sxs-lookup"><span data-stu-id="78653-160">Assume that the task completed successfully, and that there were no concurrent transactions modifying the queue.</span></span> <span data-ttu-id="78653-161">Так как нельзя сделать вывод о порядке элементов в очереди, любые три элемента могут быть выведены из нее в любом порядке.</span><span class="sxs-lookup"><span data-stu-id="78653-161">Since no inference can be made about the order of the items in the queue, any three of the items may be dequeued, in any order.</span></span> <span data-ttu-id="78653-162">Очередь попытается разместить элементы в первоначальном порядке (постановки в очередь), но может быть вынуждена переупорядочить их из-за одновременных операций или сбоев.</span><span class="sxs-lookup"><span data-stu-id="78653-162">The queue will attempt to keep the items in the original (enqueued) order, but may be forced to reorder them due to concurrent operations or faults.</span></span>  

- <span data-ttu-id="78653-163">*Вариант 2. Параллельное задание вывода из очереди*</span><span class="sxs-lookup"><span data-stu-id="78653-163">*Case 2: Parallel Dequeue Task*</span></span>

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

<span data-ttu-id="78653-164">Предположим, что задачи успешно завершены, они выполнялись параллельно и не было других одновременных транзакций, изменяющих очередь.</span><span class="sxs-lookup"><span data-stu-id="78653-164">Assume that the tasks completed successfully, that the tasks ran in parallel, and that there were no other concurrent transactions modifying the queue.</span></span> <span data-ttu-id="78653-165">Так как невозможно сделать вывод о порядке элементов в очереди, списки *dequeue1* и *dequeue2* будут содержать любые два элемента в любом порядке.</span><span class="sxs-lookup"><span data-stu-id="78653-165">Since no inference can be made about the order of the items in the queue, the lists *dequeue1* and *dequeue2* will each contain any two items, in any order.</span></span>

<span data-ttu-id="78653-166">Один и тот же элемент *не будет содержаться* в обоих списках.</span><span class="sxs-lookup"><span data-stu-id="78653-166">The same item will *not* appear in both lists.</span></span> <span data-ttu-id="78653-167">Поэтому если dequeue1 имеет элемент *10*, *30*, то deque2 будет иметь элементы *20*, *40*.</span><span class="sxs-lookup"><span data-stu-id="78653-167">Hence, if dequeue1 has *10*, *30*, then dequeue2 would have *20*, *40*.</span></span>

- <span data-ttu-id="78653-168">*Вариант 3. Упорядочение вывода из очереди с прерыванием транзакции*</span><span class="sxs-lookup"><span data-stu-id="78653-168">*Case 3: Dequeue Ordering With Transaction Abort*</span></span>

<span data-ttu-id="78653-169">Прерывание транзакции во время вывода из очереди возвращает элементы обратно в начало очереди.</span><span class="sxs-lookup"><span data-stu-id="78653-169">Aborting a transaction with in-flight dequeues puts the items back on the head of the queue.</span></span> <span data-ttu-id="78653-170">Порядок, в котором элементы возвращаются в начало очереди, не гарантируется.</span><span class="sxs-lookup"><span data-stu-id="78653-170">The order in which the items are put back on the head of the queue is not guaranteed.</span></span> <span data-ttu-id="78653-171">Рассмотрим следующий пример:</span><span class="sxs-lookup"><span data-stu-id="78653-171">Let us look at the following code:</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort the transaction
    await txn.AbortAsync();
}
```
<span data-ttu-id="78653-172">Предположим, что элементы выводились из очереди в следующем порядке:</span><span class="sxs-lookup"><span data-stu-id="78653-172">Assume that the items were dequeued in the following order:</span></span>
> <span data-ttu-id="78653-173">10, 20</span><span class="sxs-lookup"><span data-stu-id="78653-173">10, 20</span></span>

<span data-ttu-id="78653-174">Когда мы прервем транзакцию, элементы будут добавлены обратно в начало очереди в одном из следующих порядков:</span><span class="sxs-lookup"><span data-stu-id="78653-174">When we abort the transaction, the items would be added back to the head of the queue in any of the following orders:</span></span>
> <span data-ttu-id="78653-175">10, 20</span><span class="sxs-lookup"><span data-stu-id="78653-175">10, 20</span></span>

> <span data-ttu-id="78653-176">20, 10</span><span class="sxs-lookup"><span data-stu-id="78653-176">20, 10</span></span>

<span data-ttu-id="78653-177">То же самое верно для всех случаев, когда транзакция не была успешно *зафиксирована*.</span><span class="sxs-lookup"><span data-stu-id="78653-177">The same is true for all cases where the transaction was not successfully *Committed*.</span></span>

## <a name="programming-patterns"></a><span data-ttu-id="78653-178">Шаблоны программирования</span><span class="sxs-lookup"><span data-stu-id="78653-178">Programming Patterns</span></span>
<span data-ttu-id="78653-179">В этом разделе мы рассмотрим несколько шаблонов программирования, которые могут быть полезны при использовании надежной параллельной очереди.</span><span class="sxs-lookup"><span data-stu-id="78653-179">In this section, let us look at a few programming patterns that might be helpful in using ReliableConcurrentQueue.</span></span>

### <a name="batch-dequeues"></a><span data-ttu-id="78653-180">Вывод из очереди в пакетном режиме</span><span class="sxs-lookup"><span data-stu-id="78653-180">Batch Dequeues</span></span>
<span data-ttu-id="78653-181">Этот шаблон программирования подразумевает, что задача получателя выполняет вывод из очереди в пакетном режиме, вместо того чтобы выполнять один вывод за раз.</span><span class="sxs-lookup"><span data-stu-id="78653-181">A recommended programming pattern is for the consumer task to batch its dequeues instead of performing one dequeue at a time.</span></span> <span data-ttu-id="78653-182">Пользователь может регулировать задержки между пакетами и размеры пакетов.</span><span class="sxs-lookup"><span data-stu-id="78653-182">The user can choose to throttle delays between every batch or the batch size.</span></span> <span data-ttu-id="78653-183">В следующем фрагменте кода показана эта модель программирования.</span><span class="sxs-lookup"><span data-stu-id="78653-183">The following code snippet shows this programming model.</span></span>  <span data-ttu-id="78653-184">Обратите внимание, что в этом примере обработка выполняется после фиксирования транзакции, поэтому, если во время обработки произойдет ошибка, необработанные элементы будут потеряны.</span><span class="sxs-lookup"><span data-stu-id="78653-184">Note that in this example, the processing is done after the transaction is committed, so if a fault were to occur while processing, the unprocessed items will be lost without having been processed.</span></span>  <span data-ttu-id="78653-185">Кроме того, обработка может быть выполнена в пределах области транзакции, однако это может отрицательно сказаться на производительности и требует обработки уже обработанных элементов.</span><span class="sxs-lookup"><span data-stu-id="78653-185">Alternatively, the processing can be done within the transaction's scope, however this may have a negative impact on performance and requires handling of the items already processed.</span></span>

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
                // If an item was dequeued, add to the buffer for processing
                processItems.Add(ret.Value);
            }
            else
            {
                // else break the for loop
                break;
            }
        }

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }

    int delayFactor = batchSize - processItems.Count;
    await Task.Delay(TimeSpan.FromMilliseconds(delayMs * delayFactor), cancellationToken);
}
```

### <a name="best-effort-notification-based-processing"></a><span data-ttu-id="78653-186">Оптимальная обработка на основе уведомлений</span><span class="sxs-lookup"><span data-stu-id="78653-186">Best-Effort Notification-Based Processing</span></span>
<span data-ttu-id="78653-187">Другой интересный шаблон программирования использует API подсчета.</span><span class="sxs-lookup"><span data-stu-id="78653-187">Another interesting programming pattern uses the Count API.</span></span> <span data-ttu-id="78653-188">Здесь мы можем реализовать обработку на основе уведомлений для очереди.</span><span class="sxs-lookup"><span data-stu-id="78653-188">Here, we can implement best-effort notification-based processing for the queue.</span></span> <span data-ttu-id="78653-189">Число элементов в очереди может использоваться для регулирования заданий постановки в очередь и вывода из нее.</span><span class="sxs-lookup"><span data-stu-id="78653-189">The queue Count can be used to throttle an enqueue or a dequeue task.</span></span>  <span data-ttu-id="78653-190">Обратите внимание, что, как и в предыдущем примере, так как обработка происходит за пределами транзакции, необработанные элементы могут быть потеряны, если во время обработки возникнет ошибка.</span><span class="sxs-lookup"><span data-stu-id="78653-190">Note that as in the previous example, since the processing occurs outside the transaction, unprocessed items may be lost if a fault occurs during processing.</span></span>

```
int threshold = 5;
long delayMs = 1000;

while(!cancellationToken.IsCancellationRequested)
{
    while (this.Queue.Count < threshold)
    {
        cancellationToken.ThrowIfCancellationRequested();

        // If the queue does not have the threshold number of items, delay the task and check again
        await Task.Delay(TimeSpan.FromMilliseconds(delayMs), cancellationToken);
    }

    // If there are approximately threshold number of items, try and process the queue

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
                // If an item was dequeued, add to the buffer for processing
                processItems.Add(ret.Value);
            }
        } while (processItems.Count < threshold && ret.HasValue);

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
}
```

### <a name="best-effort-drain"></a><span data-ttu-id="78653-191">Оптимальная очистка</span><span class="sxs-lookup"><span data-stu-id="78653-191">Best-Effort Drain</span></span>
<span data-ttu-id="78653-192">Очистка очереди не гарантируется из-за свойства параллельности структуры данных.</span><span class="sxs-lookup"><span data-stu-id="78653-192">A drain of the queue cannot be guaranteed due to the concurrent nature of the data structure.</span></span>  <span data-ttu-id="78653-193">Вполне возможно, что даже если никакие пользовательские операции в очереди не выполняются, конкретный вызов метода TryDequeueAsync не сможет вернуть элемент, который ранее был поставлен в очередь и зафиксирован.</span><span class="sxs-lookup"><span data-stu-id="78653-193">It is possible that, even if no user operations on the queue are in-flight, a particular call to TryDequeueAsync may not return an item which was previously enqueued and committed.</span></span>  <span data-ttu-id="78653-194">Поставленный в очередь элемент *в конечном счете* станет видимым для операции вывода из очереди, но без внешнего механизма обмена данными независимый получатель не узнает, что очередь достигла устойчивого состояния, даже если все процедуры были остановлены, а новые операции ввода в очередь запрещены.</span><span class="sxs-lookup"><span data-stu-id="78653-194">The enqueued item is guaranteed to *eventually* become visible to dequeue, however without an out-of-band communication mechanism, an independent consumer cannot know that the queue has reached a steady-state even if all producers have been stopped and no new enqueue operations are allowed.</span></span> <span data-ttu-id="78653-195">Таким образом операция очистки выполняется наилучшим возможным образом, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="78653-195">Thus, the drain operation is best-effort as implemented below.</span></span>

<span data-ttu-id="78653-196">Прежде чем попытаться очистить очередь, пользователь должен остановить все последующие задачи отправителя и получателя и ожидать подтверждения или прерывания любых выполняемых транзакций.</span><span class="sxs-lookup"><span data-stu-id="78653-196">The user should stop all further producer and consumer tasks, and wait for any in-flight transactions to commit or abort, before attempting to drain the queue.</span></span>  <span data-ttu-id="78653-197">Если пользователь знает предполагаемое количество элементов в очереди, он может настроить уведомление, которое сигнализирует о том, что все элементы выведены из очереди.</span><span class="sxs-lookup"><span data-stu-id="78653-197">If the user knows the expected number of items in the queue, they can set up a notification which signals that all items have been dequeued.</span></span>

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
                // Buffer the dequeues
                processItems.Add(ret.Value);
            }
        } while (ret.HasValue && processItems.Count < batchSize);

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
} while (ret.HasValue);
```

### <a name="peek"></a><span data-ttu-id="78653-198">Обзор</span><span class="sxs-lookup"><span data-stu-id="78653-198">Peek</span></span>
<span data-ttu-id="78653-199">Надежная параллельная очередь не предоставляет API *TryPeekAsync*.</span><span class="sxs-lookup"><span data-stu-id="78653-199">ReliableConcurrentQueue does not provide the *TryPeekAsync* api.</span></span> <span data-ttu-id="78653-200">Пользователи могут получить семантику обзора с помощью метода *TryDequeueAsync* и прерывания транзакции.</span><span class="sxs-lookup"><span data-stu-id="78653-200">Users can get the peek semantic by using a *TryDequeueAsync* and then aborting the transaction.</span></span> <span data-ttu-id="78653-201">В этом примере вывод из очереди обрабатывается только в том случае, если значение элемента больше чем *10*.</span><span class="sxs-lookup"><span data-stu-id="78653-201">In this example, dequeues are processed only if the item's value is greater than *10*.</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    ConditionalValue ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);
    bool valueProcessed = false;

    if (ret.HasValue)
    {
        if (ret.Value > 10)
        {
            // Process the item
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

## <a name="must-read"></a><span data-ttu-id="78653-202">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="78653-202">Must Read</span></span>
* [<span data-ttu-id="78653-203">Приступая к работе с надежными службами</span><span class="sxs-lookup"><span data-stu-id="78653-203">Reliable Services Quick Start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="78653-204">Работа с Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="78653-204">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="78653-205">Уведомления Reliable Services</span><span class="sxs-lookup"><span data-stu-id="78653-205">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="78653-206">Резервное копирование и восстановление служб Reliable Services и субъектов Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="78653-206">Reliable Services Backup and Restore (Disaster Recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="78653-207">Настройка надежных служб с отслеживанием состояния</span><span class="sxs-lookup"><span data-stu-id="78653-207">Reliable State Manager Configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="78653-208">ASP.NET Core в Service Fabric Reliable Services</span><span class="sxs-lookup"><span data-stu-id="78653-208">Getting Started with Service Fabric Web API Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="78653-209">Дополнительные возможности использования модели программирования надежных служб</span><span class="sxs-lookup"><span data-stu-id="78653-209">Advanced Usage of the Reliable Services Programming Model</span></span>](service-fabric-reliable-services-advanced-usage.md)
* [<span data-ttu-id="78653-210">Справочник разработчика по надежным коллекциям</span><span class="sxs-lookup"><span data-stu-id="78653-210">Developer Reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
