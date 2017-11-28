---
title: "уведомления службы aaaReliable | Документы Microsoft"
description: "Содержательная документация по уведомлениям Reliable Services в Service Fabric"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,vturecek
ms.assetid: cdc918dd-5e81-49c8-a03d-7ddcd12a9a76
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/29/2017
ms.author: mcoskun
ms.openlocfilehash: 8c43190d31dbe82d1dc7fa1c228128bdcc3684f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-notifications"></a><span data-ttu-id="96e80-103">Уведомления Reliable Services</span><span class="sxs-lookup"><span data-stu-id="96e80-103">Reliable Services notifications</span></span>
<span data-ttu-id="96e80-104">Уведомления позволяют клиентам tootrack hello изменения, которые были сделаны tooan объекта, который их интересует.</span><span class="sxs-lookup"><span data-stu-id="96e80-104">Notifications allow clients tootrack hello changes that are being made tooan object that they're interested in.</span></span> <span data-ttu-id="96e80-105">Существует два типа объектов, поддерживающих уведомления: *диспетчер надежных состояний* и *надежный словарь*.</span><span class="sxs-lookup"><span data-stu-id="96e80-105">Two types of objects support notifications: *Reliable State Manager* and *Reliable Dictionary*.</span></span>

<span data-ttu-id="96e80-106">Распространенные причины для использования уведомлений:</span><span class="sxs-lookup"><span data-stu-id="96e80-106">Common reasons for using notifications are:</span></span>

* <span data-ttu-id="96e80-107">Построение материализованные представления, такие как вторичные индексы или группировка hello реплики состояние представления с фильтрацией.</span><span class="sxs-lookup"><span data-stu-id="96e80-107">Building materialized views, such as secondary indexes or aggregated filtered views of hello replica's state.</span></span> <span data-ttu-id="96e80-108">К примеру, это может быть отсортированный индекс всех ключей в надежном словаре.</span><span class="sxs-lookup"><span data-stu-id="96e80-108">An example is a sorted index of all keys in Reliable Dictionary.</span></span>
* <span data-ttu-id="96e80-109">Отправка данных мониторинга, например hello число пользователей, добавленных в hello последний час.</span><span class="sxs-lookup"><span data-stu-id="96e80-109">Sending monitoring data, such as hello number of users added in hello last hour.</span></span>

<span data-ttu-id="96e80-110">Уведомления активируются в ходе применения операций.</span><span class="sxs-lookup"><span data-stu-id="96e80-110">Notifications are fired as part of applying operations.</span></span> <span data-ttu-id="96e80-111">В связи с этим обработка уведомлений должна быть максимально быстрой и в синхронных событиях не должно быть ресурсоемких операций.</span><span class="sxs-lookup"><span data-stu-id="96e80-111">Because of that, notifications should be handled as fast as possible, and synchronous events shouldn't include any expensive operations.</span></span>

## <a name="reliable-state-manager-notifications"></a><span data-ttu-id="96e80-112">Уведомления диспетчера надежных состояний</span><span class="sxs-lookup"><span data-stu-id="96e80-112">Reliable State Manager notifications</span></span>
<span data-ttu-id="96e80-113">Диспетчер состояния надежное предоставляет уведомления о hello следующие события:</span><span class="sxs-lookup"><span data-stu-id="96e80-113">Reliable State Manager provides notifications for hello following events:</span></span>

* <span data-ttu-id="96e80-114">транзакция:</span><span class="sxs-lookup"><span data-stu-id="96e80-114">Transaction</span></span>
  * <span data-ttu-id="96e80-115">Фиксация</span><span class="sxs-lookup"><span data-stu-id="96e80-115">Commit</span></span>
* <span data-ttu-id="96e80-116">Диспетчер состояний:</span><span class="sxs-lookup"><span data-stu-id="96e80-116">State manager</span></span>
  * <span data-ttu-id="96e80-117">перестроение;</span><span class="sxs-lookup"><span data-stu-id="96e80-117">Rebuild</span></span>
  * <span data-ttu-id="96e80-118">добавление надежного состояния;</span><span class="sxs-lookup"><span data-stu-id="96e80-118">Addition of a reliable state</span></span>
  * <span data-ttu-id="96e80-119">удаление надежного состояния.</span><span class="sxs-lookup"><span data-stu-id="96e80-119">Removal of a reliable state</span></span>

<span data-ttu-id="96e80-120">Диспетчер состояния надежное отслеживает текущих транзакций порядковых hello.</span><span class="sxs-lookup"><span data-stu-id="96e80-120">Reliable State Manager tracks hello current inflight transactions.</span></span> <span data-ttu-id="96e80-121">Hello единственное изменение в состоянии транзакции, которое вызывает уведомление toobe, инициированные состоит фиксации транзакции.</span><span class="sxs-lookup"><span data-stu-id="96e80-121">hello only change in transaction state that causes a notification toobe fired is a transaction being committed.</span></span>

<span data-ttu-id="96e80-122">Диспетчер надежных состояний поддерживает коллекцию надежных состояний, таких как надежный словарь и надежная очередь.</span><span class="sxs-lookup"><span data-stu-id="96e80-122">Reliable State Manager maintains a collection of reliable states like Reliable Dictionary and Reliable Queue.</span></span> <span data-ttu-id="96e80-123">Диспетчер состояния надежное запускающей уведомления при изменении этой коллекции: надежные состояние добавляется или удаляется или перестраивается вся коллекция hello.</span><span class="sxs-lookup"><span data-stu-id="96e80-123">Reliable State Manager fires notifications when this collection changes: a reliable state is added or removed, or hello entire collection is rebuilt.</span></span>
<span data-ttu-id="96e80-124">Hello надежного диспетчер состояния коллекции перестраивается в трех случаях:</span><span class="sxs-lookup"><span data-stu-id="96e80-124">hello Reliable State Manager collection is rebuilt in three cases:</span></span>

* <span data-ttu-id="96e80-125">Восстановление: При запуске реплики, он восстанавливает предыдущее состояние с диска hello.</span><span class="sxs-lookup"><span data-stu-id="96e80-125">Recovery: When a replica starts, it recovers its previous state from hello disk.</span></span> <span data-ttu-id="96e80-126">В конце hello восстановления использует **NotifyStateManagerChangedEventArgs** toofire событие, которое содержит набор hello восстановленные надежного состояний.</span><span class="sxs-lookup"><span data-stu-id="96e80-126">At hello end of recovery, it uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of recovered reliable states.</span></span>
* <span data-ttu-id="96e80-127">Полная копия: перед реплику можно присоединить hello набора конфигурации, он имеет toobe построения.</span><span class="sxs-lookup"><span data-stu-id="96e80-127">Full copy: Before a replica can join hello configuration set, it has toobe built.</span></span> <span data-ttu-id="96e80-128">В некоторых случаях для этого полную копию состояния надежного диспетчер состояний с hello первичная реплика toobe примененных toohello простоя вторичной реплики.</span><span class="sxs-lookup"><span data-stu-id="96e80-128">Sometimes, this requires a full copy of Reliable State Manager's state from hello primary replica toobe applied toohello idle secondary replica.</span></span> <span data-ttu-id="96e80-129">Диспетчер состояния надежное на вторичной реплике использует hello **NotifyStateManagerChangedEventArgs** toofire событие, которое содержит набор hello надежного состояний, полученную из первичной реплики hello.</span><span class="sxs-lookup"><span data-stu-id="96e80-129">Reliable State Manager on hello secondary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it acquired from hello primary replica.</span></span>
* <span data-ttu-id="96e80-130">Восстановление: В сценарии аварийного восстановления, состояние реплики hello можно восстановить из резервной копии через **RestoreAsync**.</span><span class="sxs-lookup"><span data-stu-id="96e80-130">Restore: In disaster recovery scenarios, hello replica's state can be restored from a backup via **RestoreAsync**.</span></span> <span data-ttu-id="96e80-131">В таких случаях использует надежного диспетчер состояния в первичной реплике hello **NotifyStateManagerChangedEventArgs** toofire событие, которое содержит набор hello надежного состояний, которые он восстановлен из резервной копии hello.</span><span class="sxs-lookup"><span data-stu-id="96e80-131">In such cases, Reliable State Manager on hello primary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it restored from hello backup.</span></span>

<span data-ttu-id="96e80-132">tooregister для уведомления о транзакции и/или уведомления о состоянии диспетчера необходимо tooregister с hello **TransactionChanged** или **StateManagerChanged** событий на надежный диспетчер состояний.</span><span class="sxs-lookup"><span data-stu-id="96e80-132">tooregister for transaction notifications and/or state manager notifications, you need tooregister with hello **TransactionChanged** or **StateManagerChanged** events on Reliable State Manager.</span></span> <span data-ttu-id="96e80-133">Обычно tooregister с эти обработчики событий является конструктором hello службы с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="96e80-133">A common place tooregister with these event handlers is hello constructor of your stateful service.</span></span> <span data-ttu-id="96e80-134">При регистрации на конструктор hello не пропустить всех уведомлений, вызванным изменением время жизни hello **IReliableStateManager**.</span><span class="sxs-lookup"><span data-stu-id="96e80-134">When you register on hello constructor, you won't miss any notification that's caused by a change during hello lifetime of **IReliableStateManager**.</span></span>

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

<span data-ttu-id="96e80-135">Hello **TransactionChanged** обработчик событий использует **NotifyTransactionChangedEventArgs** tooprovide сведений о событии hello.</span><span class="sxs-lookup"><span data-stu-id="96e80-135">hello **TransactionChanged** event handler uses **NotifyTransactionChangedEventArgs** tooprovide details about hello event.</span></span> <span data-ttu-id="96e80-136">Он содержит свойство hello действие (например, **NotifyTransactionChangedAction.Commit**), указывающий тип hello изменения.</span><span class="sxs-lookup"><span data-stu-id="96e80-136">It contains hello action property (for example, **NotifyTransactionChangedAction.Commit**) that specifies hello type of change.</span></span> <span data-ttu-id="96e80-137">Он также содержит свойства транзакции hello, которое предоставляет транзакции toohello ссылку, которая изменила.</span><span class="sxs-lookup"><span data-stu-id="96e80-137">It also contains hello transaction property that provides a reference toohello transaction that changed.</span></span>

> [!NOTE]
> <span data-ttu-id="96e80-138">В настоящее время **TransactionChanged** событий только в том случае, если hello транзакция будет зафиксирована.</span><span class="sxs-lookup"><span data-stu-id="96e80-138">Today, **TransactionChanged** events are raised only if hello transaction is committed.</span></span> <span data-ttu-id="96e80-139">Hello действия равен затем слишком**NotifyTransactionChangedAction.Commit**.</span><span class="sxs-lookup"><span data-stu-id="96e80-139">hello action is then equal too**NotifyTransactionChangedAction.Commit**.</span></span> <span data-ttu-id="96e80-140">Но в будущих hello, события могут возникать для других типов об изменениях состояния транзакции.</span><span class="sxs-lookup"><span data-stu-id="96e80-140">But in hello future, events might be raised for other types of transaction state changes.</span></span> <span data-ttu-id="96e80-141">Мы рекомендуем обработки hello событий только в том случае, если при этом предполагается, что и проверки действие hello.</span><span class="sxs-lookup"><span data-stu-id="96e80-141">We recommend checking hello action and processing hello event only if it's one that you expect.</span></span>
> 
> 

<span data-ttu-id="96e80-142">Ниже приведен пример обработчика событий **TransactionChanged** .</span><span class="sxs-lookup"><span data-stu-id="96e80-142">Following is an example **TransactionChanged** event handler.</span></span>

```C#
private void OnTransactionChangedHandler(object sender, NotifyTransactionChangedEventArgs e)
{
    if (e.Action == NotifyTransactionChangedAction.Commit)
    {
        this.lastCommitLsn = e.Transaction.CommitSequenceNumber;
        this.lastTransactionId = e.Transaction.TransactionId;

        this.lastCommittedTransactionList.Add(e.Transaction.TransactionId);
    }
}
```

<span data-ttu-id="96e80-143">Hello **StateManagerChanged** обработчик событий использует **NotifyStateManagerChangedEventArgs** tooprovide сведений о событии hello.</span><span class="sxs-lookup"><span data-stu-id="96e80-143">hello **StateManagerChanged** event handler uses **NotifyStateManagerChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="96e80-144">Существуют два подкласса экземпляра **NotifyStateManagerChangedEventArgs**: **NotifyStateManagerRebuildEventArgs** и **NotifyStateManagerSingleEntityChangedEventArgs**.</span><span class="sxs-lookup"><span data-stu-id="96e80-144">**NotifyStateManagerChangedEventArgs** has two subclasses: **NotifyStateManagerRebuildEventArgs** and **NotifyStateManagerSingleEntityChangedEventArgs**.</span></span>
<span data-ttu-id="96e80-145">Использование свойства action hello в **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** правильный подкласс toohello:</span><span class="sxs-lookup"><span data-stu-id="96e80-145">You use hello action property in **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="96e80-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**;</span><span class="sxs-lookup"><span data-stu-id="96e80-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span></span>
* <span data-ttu-id="96e80-147">**NotifyStateManagerChangedAction.Add** и **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**.</span><span class="sxs-lookup"><span data-stu-id="96e80-147">**NotifyStateManagerChangedAction.Add** and **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span></span>

<span data-ttu-id="96e80-148">Ниже приведен пример обработчика уведомлений **StateManagerChanged** .</span><span class="sxs-lookup"><span data-stu-id="96e80-148">Following is an example **StateManagerChanged** notification handler.</span></span>

```C#
public void OnStateManagerChangedHandler(object sender, NotifyStateManagerChangedEventArgs e)
{
    if (e.Action == NotifyStateManagerChangedAction.Rebuild)
    {
        this.ProcessStataManagerRebuildNotification(e);

        return;
    }

    this.ProcessStateManagerSingleEntityNotification(e);
}
```

## <a name="reliable-dictionary-notifications"></a><span data-ttu-id="96e80-149">Уведомления надежного словаря</span><span class="sxs-lookup"><span data-stu-id="96e80-149">Reliable Dictionary notifications</span></span>
<span data-ttu-id="96e80-150">Надежные словарь предоставляет уведомления о hello следующие события:</span><span class="sxs-lookup"><span data-stu-id="96e80-150">Reliable Dictionary provides notifications for hello following events:</span></span>

* <span data-ttu-id="96e80-151">Перестроение. Вызывается при восстановлении состояния **ReliableDictionary** из восстановленного или скопированного локального состояния либо из резервной копии.</span><span class="sxs-lookup"><span data-stu-id="96e80-151">Rebuild: Called when **ReliableDictionary** has recovered its state from a recovered or copied local state or backup.</span></span>
* <span data-ttu-id="96e80-152">Очистить: Вызывается, когда hello состояние **ReliableDictionary** очищен через hello **ClearAsync** метод.</span><span class="sxs-lookup"><span data-stu-id="96e80-152">Clear: Called when hello state of **ReliableDictionary** has been cleared through hello **ClearAsync** method.</span></span>
* <span data-ttu-id="96e80-153">Добавьте: Вызывается, когда элемент был добавлен слишком**ReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="96e80-153">Add: Called when an item has been added too**ReliableDictionary**.</span></span>
* <span data-ttu-id="96e80-154">Обновление. Вызывается при обновлении элемента в **IReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="96e80-154">Update: Called when an item in **IReliableDictionary** has been updated.</span></span>
* <span data-ttu-id="96e80-155">Удаление. Вызывается при удалении элемента из **IReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="96e80-155">Remove: Called when an item in **IReliableDictionary** has been deleted.</span></span>

<span data-ttu-id="96e80-156">tooget надежного словарь уведомления, необходимо tooregister с hello **DictionaryChanged** обработчику событий в **IReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="96e80-156">tooget Reliable Dictionary notifications, you need tooregister with hello **DictionaryChanged** event handler on **IReliableDictionary**.</span></span> <span data-ttu-id="96e80-157">Обычно является tooregister с эти обработчики событий в hello **ReliableStateManager.StateManagerChanged** добавить уведомление.</span><span class="sxs-lookup"><span data-stu-id="96e80-157">A common place tooregister with these event handlers is in hello **ReliableStateManager.StateManagerChanged** add notification.</span></span>
<span data-ttu-id="96e80-158">При регистрации **IReliableDictionary** добавляется слишком**IReliableStateManager** гарантирует, что не будет пропускать любые уведомления.</span><span class="sxs-lookup"><span data-stu-id="96e80-158">Registering when **IReliableDictionary** is added too**IReliableStateManager** ensures that you won't miss any notifications.</span></span>

```C#
private void ProcessStateManagerSingleEntityNotification(NotifyStateManagerChangedEventArgs e)
{
    var operation = e as NotifyStateManagerSingleEntityChangedEventArgs;

    if (operation.Action == NotifyStateManagerChangedAction.Add)
    {
        if (operation.ReliableState is IReliableDictionary<TKey, TValue>)
        {
            var dictionary = (IReliableDictionary<TKey, TValue>)operation.ReliableState;
            dictionary.RebuildNotificationAsyncCallback = this.OnDictionaryRebuildNotificationHandlerAsync;
            dictionary.DictionaryChanged += this.OnDictionaryChangedHandler;
            }
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="96e80-159">**ProcessStateManagerSingleEntityNotification** — метод образец hello, "hello" Предыдущий **OnStateManagerChangedHandler** пример вызывает.</span><span class="sxs-lookup"><span data-stu-id="96e80-159">**ProcessStateManagerSingleEntityNotification** is hello sample method that hello preceding **OnStateManagerChangedHandler** example calls.</span></span>
> 
> 

<span data-ttu-id="96e80-160">Hello предыдущий код задает hello **IReliableNotificationAsyncCallback** интерфейс вместе с **DictionaryChanged**.</span><span class="sxs-lookup"><span data-stu-id="96e80-160">hello preceding code sets hello **IReliableNotificationAsyncCallback** interface, along with **DictionaryChanged**.</span></span> <span data-ttu-id="96e80-161">Поскольку **NotifyDictionaryRebuildEventArgs** содержит **IAsyncEnumerable** интерфейс--которого необходимо перечислить асинхронно--toobe уведомления перестроения запускаются через  **RebuildNotificationAsyncCallback** вместо **OnDictionaryChangedHandler**.</span><span class="sxs-lookup"><span data-stu-id="96e80-161">Because **NotifyDictionaryRebuildEventArgs** contains an **IAsyncEnumerable** interface--which needs toobe enumerated asynchronously--rebuild notifications are fired through **RebuildNotificationAsyncCallback** instead of **OnDictionaryChangedHandler**.</span></span>

```C#
public async Task OnDictionaryRebuildNotificationHandlerAsync(
    IReliableDictionary<TKey, TValue> origin,
    NotifyDictionaryRebuildEventArgs<TKey, TValue> rebuildNotification)
{
    this.secondaryIndex.Clear();

    var enumerator = e.State.GetAsyncEnumerator();
    while (await enumerator.MoveNextAsync(CancellationToken.None))
    {
        this.secondaryIndex.Add(enumerator.Current.Key, enumerator.Current.Value);
    }
}
```

> [!NOTE]
> <span data-ttu-id="96e80-162">В hello предшествующий код, как часть обработки hello перестроения уведомления первый hello ведет агрегированных состояние будет очищено.</span><span class="sxs-lookup"><span data-stu-id="96e80-162">In hello preceding code, as part of processing hello rebuild notification, first hello maintained aggregated state is cleared.</span></span> <span data-ttu-id="96e80-163">Так как надежный коллекции hello восстанавливается с использованием нового состояния, все предыдущие уведомления не имеют значения.</span><span class="sxs-lookup"><span data-stu-id="96e80-163">Because hello reliable collection is being rebuilt with a new state, all previous notifications are irrelevant.</span></span>
> 
> 

<span data-ttu-id="96e80-164">Hello **DictionaryChanged** обработчик событий использует **NotifyDictionaryChangedEventArgs** tooprovide сведений о событии hello.</span><span class="sxs-lookup"><span data-stu-id="96e80-164">hello **DictionaryChanged** event handler uses **NotifyDictionaryChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="96e80-165">**NotifyDictionaryChangedEventArgs** .</span><span class="sxs-lookup"><span data-stu-id="96e80-165">**NotifyDictionaryChangedEventArgs** has five subclasses.</span></span> <span data-ttu-id="96e80-166">Использование свойства action hello в **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** правильный подкласс toohello:</span><span class="sxs-lookup"><span data-stu-id="96e80-166">Use hello action property in **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="96e80-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**;</span><span class="sxs-lookup"><span data-stu-id="96e80-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span></span>
* <span data-ttu-id="96e80-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**;</span><span class="sxs-lookup"><span data-stu-id="96e80-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span></span>
* <span data-ttu-id="96e80-169">**NotifyDictionaryChangedAction.Add** и **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**;</span><span class="sxs-lookup"><span data-stu-id="96e80-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span></span>
* <span data-ttu-id="96e80-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**;</span><span class="sxs-lookup"><span data-stu-id="96e80-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span></span>
* <span data-ttu-id="96e80-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**.</span><span class="sxs-lookup"><span data-stu-id="96e80-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span></span>

```C#
public void OnDictionaryChangedHandler(object sender, NotifyDictionaryChangedEventArgs<TKey, TValue> e)
{
    switch (e.Action)
    {
        case NotifyDictionaryChangedAction.Clear:
            var clearEvent = e as NotifyDictionaryClearEventArgs<TKey, TValue>;
            this.ProcessClearNotification(clearEvent);
            return;

        case NotifyDictionaryChangedAction.Add:
            var addEvent = e as NotifyDictionaryItemAddedEventArgs<TKey, TValue>;
            this.ProcessAddNotification(addEvent);
            return;

        case NotifyDictionaryChangedAction.Update:
            var updateEvent = e as NotifyDictionaryItemUpdatedEventArgs<TKey, TValue>;
            this.ProcessUpdateNotification(updateEvent);
            return;

        case NotifyDictionaryChangedAction.Remove:
            var deleteEvent = e as NotifyDictionaryItemRemovedEventArgs<TKey, TValue>;
            this.ProcessRemoveNotification(deleteEvent);
            return;

        default:
            break;
    }
}
```

## <a name="recommendations"></a><span data-ttu-id="96e80-172">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="96e80-172">Recommendations</span></span>
* <span data-ttu-id="96e80-173">*Завершайте* события уведомлений максимально быстро.</span><span class="sxs-lookup"><span data-stu-id="96e80-173">*Do* complete notification events as fast as possible.</span></span>
* <span data-ttu-id="96e80-174">*Не* выполняйте какие-либо ресурсоемкие операции (например, операции ввода-вывода) в составе синхронных событий.</span><span class="sxs-lookup"><span data-stu-id="96e80-174">*Do not* execute any expensive operations (for example, I/O operations) as part of synchronous events.</span></span>
* <span data-ttu-id="96e80-175">*Сделать* Проверьте тип действия hello перед обработкой событий hello.</span><span class="sxs-lookup"><span data-stu-id="96e80-175">*Do* check hello action type before you process hello event.</span></span> <span data-ttu-id="96e80-176">Новые типы действий могут быть добавлены в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="96e80-176">New action types might be added in hello future.</span></span>

<span data-ttu-id="96e80-177">Ниже приведены некоторые вещи tookeep в виду.</span><span class="sxs-lookup"><span data-stu-id="96e80-177">Here are some things tookeep in mind:</span></span>

* <span data-ttu-id="96e80-178">Уведомления запускаются как часть hello выполнения операции.</span><span class="sxs-lookup"><span data-stu-id="96e80-178">Notifications are fired as part of hello execution of an operation.</span></span> <span data-ttu-id="96e80-179">Например уведомление восстановления создается в качестве последнего шага hello операции восстановления.</span><span class="sxs-lookup"><span data-stu-id="96e80-179">For example, a restore notification is fired as hello last step of a restore operation.</span></span> <span data-ttu-id="96e80-180">Восстановление не будет завершено до момента обработки события уведомления hello.</span><span class="sxs-lookup"><span data-stu-id="96e80-180">A restore will not finish until hello notification event is processed.</span></span>
* <span data-ttu-id="96e80-181">Поскольку уведомления запускаются в рамках применения операций hello, клиенты могут видеть только уведомления для локально зафиксированных операций.</span><span class="sxs-lookup"><span data-stu-id="96e80-181">Because notifications are fired as part of hello applying operations, clients see only notifications for locally committed operations.</span></span> <span data-ttu-id="96e80-182">А поскольку операций гарантируется только toobe зафиксированных локально (другими словами, регистрируется), они могут поддерживать или не могут быть отменены в будущих hello.</span><span class="sxs-lookup"><span data-stu-id="96e80-182">And because operations are guaranteed only toobe locally committed (in other words, logged), they might or might not be undone in hello future.</span></span>
* <span data-ttu-id="96e80-183">По пути повтора hello одно уведомление создается для каждого примененного операции.</span><span class="sxs-lookup"><span data-stu-id="96e80-183">On hello redo path, a single notification is fired for each applied operation.</span></span> <span data-ttu-id="96e80-184">Это означает, что если транзакция T1 включает Create(X), Delete(X) и Create(X), вы сможете получить одно уведомление для создания hello X, один для удаления hello и один для создания hello еще раз, в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="96e80-184">This means that if transaction T1 includes Create(X), Delete(X), and Create(X), you'll get one notification for hello creation of X, one for hello deletion, and one for hello creation again, in that order.</span></span>
* <span data-ttu-id="96e80-185">Для транзакций, которые содержат несколько операций в порядке hello, в котором они были получены в первичной реплике hello hello пользователя применяются операции.</span><span class="sxs-lookup"><span data-stu-id="96e80-185">For transactions that contain multiple operations, operations are applied in hello order in which they were received on hello primary replica from hello user.</span></span>
* <span data-ttu-id="96e80-186">При обработке хода выполнения с результатом false некоторые операции могут быть отменены.</span><span class="sxs-lookup"><span data-stu-id="96e80-186">As part of processing false progress, some operations might be undone.</span></span> <span data-ttu-id="96e80-187">Уведомления возникают для таких операций отмены отката hello состояние hello реплики задней tooa стабильный точки.</span><span class="sxs-lookup"><span data-stu-id="96e80-187">Notifications are raised for such undo operations, rolling hello state of hello replica back tooa stable point.</span></span> <span data-ttu-id="96e80-188">Одно важное отличие уведомлений об отмене — события с повторяющимися ключами агрегируются.</span><span class="sxs-lookup"><span data-stu-id="96e80-188">One important difference of undo notifications is that events that have duplicate keys are aggregated.</span></span> <span data-ttu-id="96e80-189">Например если выполняется откат транзакции Т1, вы увидите tooDelete(X) одно уведомление.</span><span class="sxs-lookup"><span data-stu-id="96e80-189">For example, if transaction T1 is being undone, you'll see a single notification tooDelete(X).</span></span>

## <a name="next-steps"></a><span data-ttu-id="96e80-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="96e80-190">Next steps</span></span>
* [<span data-ttu-id="96e80-191">Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="96e80-191">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="96e80-192">Краткое руководство по надежным службам Reliable Services</span><span class="sxs-lookup"><span data-stu-id="96e80-192">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="96e80-193">Архивация и восстановление (аварийное восстановление) надежных служб</span><span class="sxs-lookup"><span data-stu-id="96e80-193">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="96e80-194">Справочник разработчика по надежным коллекциям</span><span class="sxs-lookup"><span data-stu-id="96e80-194">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

