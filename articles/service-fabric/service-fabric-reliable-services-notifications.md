---
title: "Уведомления Reliable Services | Документация Майкрософт"
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
ms.openlocfilehash: c6a53d851510ed5e6eec1f3ac0f636ad034a6d4c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-services-notifications"></a><span data-ttu-id="fa5b4-103">Уведомления Reliable Services</span><span class="sxs-lookup"><span data-stu-id="fa5b4-103">Reliable Services notifications</span></span>
<span data-ttu-id="fa5b4-104">Уведомления позволяют клиентам отслеживать изменения, которые вносятся в интересующий их объект.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-104">Notifications allow clients to track the changes that are being made to an object that they're interested in.</span></span> <span data-ttu-id="fa5b4-105">Существует два типа объектов, поддерживающих уведомления: *диспетчер надежных состояний* и *надежный словарь*.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-105">Two types of objects support notifications: *Reliable State Manager* and *Reliable Dictionary*.</span></span>

<span data-ttu-id="fa5b4-106">Распространенные причины для использования уведомлений:</span><span class="sxs-lookup"><span data-stu-id="fa5b4-106">Common reasons for using notifications are:</span></span>

* <span data-ttu-id="fa5b4-107">Создание материализованных представлений, например вторичных индексов или агрегированных отфильтрованных представлений состояния реплики.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-107">Building materialized views, such as secondary indexes or aggregated filtered views of the replica's state.</span></span> <span data-ttu-id="fa5b4-108">К примеру, это может быть отсортированный индекс всех ключей в надежном словаре.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-108">An example is a sorted index of all keys in Reliable Dictionary.</span></span>
* <span data-ttu-id="fa5b4-109">Отправка данных мониторинга, например количества пользователей, добавленных за последний час.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-109">Sending monitoring data, such as the number of users added in the last hour.</span></span>

<span data-ttu-id="fa5b4-110">Уведомления активируются в ходе применения операций.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-110">Notifications are fired as part of applying operations.</span></span> <span data-ttu-id="fa5b4-111">В связи с этим обработка уведомлений должна быть максимально быстрой и в синхронных событиях не должно быть ресурсоемких операций.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-111">Because of that, notifications should be handled as fast as possible, and synchronous events shouldn't include any expensive operations.</span></span>

## <a name="reliable-state-manager-notifications"></a><span data-ttu-id="fa5b4-112">Уведомления диспетчера надежных состояний</span><span class="sxs-lookup"><span data-stu-id="fa5b4-112">Reliable State Manager notifications</span></span>
<span data-ttu-id="fa5b4-113">Диспетчер надежных состояний предоставляет уведомления для следующих событий:</span><span class="sxs-lookup"><span data-stu-id="fa5b4-113">Reliable State Manager provides notifications for the following events:</span></span>

* <span data-ttu-id="fa5b4-114">транзакция:</span><span class="sxs-lookup"><span data-stu-id="fa5b4-114">Transaction</span></span>
  * <span data-ttu-id="fa5b4-115">Фиксация</span><span class="sxs-lookup"><span data-stu-id="fa5b4-115">Commit</span></span>
* <span data-ttu-id="fa5b4-116">Диспетчер состояний:</span><span class="sxs-lookup"><span data-stu-id="fa5b4-116">State manager</span></span>
  * <span data-ttu-id="fa5b4-117">перестроение;</span><span class="sxs-lookup"><span data-stu-id="fa5b4-117">Rebuild</span></span>
  * <span data-ttu-id="fa5b4-118">добавление надежного состояния;</span><span class="sxs-lookup"><span data-stu-id="fa5b4-118">Addition of a reliable state</span></span>
  * <span data-ttu-id="fa5b4-119">удаление надежного состояния.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-119">Removal of a reliable state</span></span>

<span data-ttu-id="fa5b4-120">Диспетчер надежных состояний отслеживает текущие обрабатываемые транзакции.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-120">Reliable State Manager tracks the current inflight transactions.</span></span> <span data-ttu-id="fa5b4-121">Как только состояние транзакции меняется, при фиксации этой транзакции срабатывает уведомление.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-121">The only change in transaction state that causes a notification to be fired is a transaction being committed.</span></span>

<span data-ttu-id="fa5b4-122">Диспетчер надежных состояний поддерживает коллекцию надежных состояний, таких как надежный словарь и надежная очередь.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-122">Reliable State Manager maintains a collection of reliable states like Reliable Dictionary and Reliable Queue.</span></span> <span data-ttu-id="fa5b4-123">При изменении этой коллекции он активирует уведомления. Это может быть добавление или удаление надежного состояния, а также перестроение всей коллекции.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-123">Reliable State Manager fires notifications when this collection changes: a reliable state is added or removed, or the entire collection is rebuilt.</span></span>
<span data-ttu-id="fa5b4-124">Перестроение коллекции диспетчера надежных состояний происходит в трех случаях.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-124">The Reliable State Manager collection is rebuilt in three cases:</span></span>

* <span data-ttu-id="fa5b4-125">Восстановление. При запуске реплики ее предыдущее состояние будет восстановлено с диска.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-125">Recovery: When a replica starts, it recovers its previous state from the disk.</span></span> <span data-ttu-id="fa5b4-126">По завершении восстановления активируется событие с экземпляром **NotifyStateManagerChangedEventArgs**, содержащим набор восстановленных надежных состояний.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-126">At the end of recovery, it uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of recovered reliable states.</span></span>
* <span data-ttu-id="fa5b4-127">Полная копия. Прежде чем реплику можно будет присоединить к набору конфигурации, нужно выполнить ее сборку.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-127">Full copy: Before a replica can join the configuration set, it has to be built.</span></span> <span data-ttu-id="fa5b4-128">В некоторых случаях может потребоваться применить к неактивной вторичной реплике полную копию состояния диспетчера надежных состояний из первичной реплики.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-128">Sometimes, this requires a full copy of Reliable State Manager's state from the primary replica to be applied to the idle secondary replica.</span></span> <span data-ttu-id="fa5b4-129">Диспетчер надежных состояний для вторичной реплики использует экземпляр **NotifyStateManagerChangedEventArgs**, чтобы активировать событие, содержащее набор надежных состояний, полученный из первичной реплики.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-129">Reliable State Manager on the secondary replica uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of reliable states that it acquired from the primary replica.</span></span>
* <span data-ttu-id="fa5b4-130">Восстановление. В сценариях аварийного восстановления состояние реплики можно восстановить из резервной копии с помощью **RestoreAsync**.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-130">Restore: In disaster recovery scenarios, the replica's state can be restored from a backup via **RestoreAsync**.</span></span> <span data-ttu-id="fa5b4-131">В таких случаях диспетчер надежных состояний для первичной реплики использует экземпляр **NotifyStateManagerChangedEventArgs**, чтобы активировать событие, содержащее набор надежных состояний, восстановленный из резервной копии.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-131">In such cases, Reliable State Manager on the primary replica uses **NotifyStateManagerChangedEventArgs** to fire an event that contains the set of reliable states that it restored from the backup.</span></span>

<span data-ttu-id="fa5b4-132">Для получения уведомлений о транзакциях и (или) уведомлений диспетчера состояний необходимо выполнить регистрацию в диспетчере надежных состояний, используя событие **TransactionChanged** или **StateManagerChanged**.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-132">To register for transaction notifications and/or state manager notifications, you need to register with the **TransactionChanged** or **StateManagerChanged** events on Reliable State Manager.</span></span> <span data-ttu-id="fa5b4-133">Чаще всего для регистрации в этих обработчиках событий используется конструктор службы с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-133">A common place to register with these event handlers is the constructor of your stateful service.</span></span> <span data-ttu-id="fa5b4-134">Если выполнить регистрацию в конструкторе, вы будете получать все уведомления в связи с изменениями в течение всего времени существования **IReliableStateManager**.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-134">When you register on the constructor, you won't miss any notification that's caused by a change during the lifetime of **IReliableStateManager**.</span></span>

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

<span data-ttu-id="fa5b4-135">Обработчик событий **TransactionChanged** использует **NotifyTransactionChangedEventArgs** для предоставления сведений о событии.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-135">The **TransactionChanged** event handler uses **NotifyTransactionChangedEventArgs** to provide details about the event.</span></span> <span data-ttu-id="fa5b4-136">В этих сведениях содержится свойство Action (например, **NotifyTransactionChangedAction.Commit**), указывающее тип изменения,</span><span class="sxs-lookup"><span data-stu-id="fa5b4-136">It contains the action property (for example, **NotifyTransactionChangedAction.Commit**) that specifies the type of change.</span></span> <span data-ttu-id="fa5b4-137">и свойство Transaction, которое содержит ссылку на измененную транзакцию.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-137">It also contains the transaction property that provides a reference to the transaction that changed.</span></span>

> [!NOTE]
> <span data-ttu-id="fa5b4-138">Сейчас события **TransactionChanged** порождаются, только если фиксируется транзакция.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-138">Today, **TransactionChanged** events are raised only if the transaction is committed.</span></span> <span data-ttu-id="fa5b4-139">В этом случае свойство Action будет иметь значение **NotifyTransactionChangedAction.Commit**.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-139">The action is then equal to **NotifyTransactionChangedAction.Commit**.</span></span> <span data-ttu-id="fa5b4-140">В будущих обновлениях могут быть добавлены события для других типов изменений состояния транзакции.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-140">But in the future, events might be raised for other types of transaction state changes.</span></span> <span data-ttu-id="fa5b4-141">Таким образом, рекомендуется проверять свойство Action и обрабатывать событие, только если оно ожидается.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-141">We recommend checking the action and processing the event only if it's one that you expect.</span></span>
> 
> 

<span data-ttu-id="fa5b4-142">Ниже приведен пример обработчика событий **TransactionChanged** .</span><span class="sxs-lookup"><span data-stu-id="fa5b4-142">Following is an example **TransactionChanged** event handler.</span></span>

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

<span data-ttu-id="fa5b4-143">Обработчик событий **StateManagerChanged** использует **NotifyStateManagerChangedEventArgs** для предоставления сведений о событии.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-143">The **StateManagerChanged** event handler uses **NotifyStateManagerChangedEventArgs** to provide details about the event.</span></span>
<span data-ttu-id="fa5b4-144">Существуют два подкласса экземпляра **NotifyStateManagerChangedEventArgs**: **NotifyStateManagerRebuildEventArgs** и **NotifyStateManagerSingleEntityChangedEventArgs**.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-144">**NotifyStateManagerChangedEventArgs** has two subclasses: **NotifyStateManagerRebuildEventArgs** and **NotifyStateManagerSingleEntityChangedEventArgs**.</span></span>
<span data-ttu-id="fa5b4-145">Свойство Action в **NotifyStateManagerChangedEventArgs** используется для приведения **NotifyStateManagerChangedEventArgs** к правильному подклассу:</span><span class="sxs-lookup"><span data-stu-id="fa5b4-145">You use the action property in **NotifyStateManagerChangedEventArgs** to cast **NotifyStateManagerChangedEventArgs** to the correct subclass:</span></span>

* <span data-ttu-id="fa5b4-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**;</span><span class="sxs-lookup"><span data-stu-id="fa5b4-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span></span>
* <span data-ttu-id="fa5b4-147">**NotifyStateManagerChangedAction.Add** и **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-147">**NotifyStateManagerChangedAction.Add** and **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span></span>

<span data-ttu-id="fa5b4-148">Ниже приведен пример обработчика уведомлений **StateManagerChanged** .</span><span class="sxs-lookup"><span data-stu-id="fa5b4-148">Following is an example **StateManagerChanged** notification handler.</span></span>

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

## <a name="reliable-dictionary-notifications"></a><span data-ttu-id="fa5b4-149">Уведомления надежного словаря</span><span class="sxs-lookup"><span data-stu-id="fa5b4-149">Reliable Dictionary notifications</span></span>
<span data-ttu-id="fa5b4-150">Надежный словарь предоставляет уведомления для следующих событий:</span><span class="sxs-lookup"><span data-stu-id="fa5b4-150">Reliable Dictionary provides notifications for the following events:</span></span>

* <span data-ttu-id="fa5b4-151">Перестроение. Вызывается при восстановлении состояния **ReliableDictionary** из восстановленного или скопированного локального состояния либо из резервной копии.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-151">Rebuild: Called when **ReliableDictionary** has recovered its state from a recovered or copied local state or backup.</span></span>
* <span data-ttu-id="fa5b4-152">Очистка. Вызывается при очистке состояния **ReliableDictionary** с помощью метода **ClearAsync**.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-152">Clear: Called when the state of **ReliableDictionary** has been cleared through the **ClearAsync** method.</span></span>
* <span data-ttu-id="fa5b4-153">Добавление. Вызывается при добавлении элемента в **ReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-153">Add: Called when an item has been added to **ReliableDictionary**.</span></span>
* <span data-ttu-id="fa5b4-154">Обновление. Вызывается при обновлении элемента в **IReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-154">Update: Called when an item in **IReliableDictionary** has been updated.</span></span>
* <span data-ttu-id="fa5b4-155">Удаление. Вызывается при удалении элемента из **IReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-155">Remove: Called when an item in **IReliableDictionary** has been deleted.</span></span>

<span data-ttu-id="fa5b4-156">Для получения уведомлений надежного словаря нужно выполнить регистрацию обработчика событий **DictionaryChanged** для **IReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-156">To get Reliable Dictionary notifications, you need to register with the **DictionaryChanged** event handler on **IReliableDictionary**.</span></span> <span data-ttu-id="fa5b4-157">Чаще всего для регистрации этих обработчиков событий используется уведомление о добавлении **ReliableStateManager.StateManagerChanged** .</span><span class="sxs-lookup"><span data-stu-id="fa5b4-157">A common place to register with these event handlers is in the **ReliableStateManager.StateManagerChanged** add notification.</span></span>
<span data-ttu-id="fa5b4-158">Если вы выполните регистрацию во время добавления **IReliableDictionary** для **IReliableStateManager**, то не пропустите ни одно уведомление.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-158">Registering when **IReliableDictionary** is added to **IReliableStateManager** ensures that you won't miss any notifications.</span></span>

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
> <span data-ttu-id="fa5b4-159">**ProcessStateManagerSingleEntityNotification** — это пример метода, который вызывается **OnStateManagerChangedHandler** в приведенном выше примере.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-159">**ProcessStateManagerSingleEntityNotification** is the sample method that the preceding **OnStateManagerChangedHandler** example calls.</span></span>
> 
> 

<span data-ttu-id="fa5b4-160">Указанный выше код задает интерфейс **IReliableNotificationAsyncCallback**, а также **DictionaryChanged**.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-160">The preceding code sets the **IReliableNotificationAsyncCallback** interface, along with **DictionaryChanged**.</span></span> <span data-ttu-id="fa5b4-161">Так как **NotifyDictionaryRebuildEventArgs** содержит интерфейс **IAsyncEnumerable**, для которого требуется асинхронное перечисление, уведомления о перестроении активируются посредством **RebuildNotificationAsyncCallback** вместо **OnDictionaryChangedHandler**.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-161">Because **NotifyDictionaryRebuildEventArgs** contains an **IAsyncEnumerable** interface--which needs to be enumerated asynchronously--rebuild notifications are fired through **RebuildNotificationAsyncCallback** instead of **OnDictionaryChangedHandler**.</span></span>

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
> <span data-ttu-id="fa5b4-162">В приведенном выше коде в ходе обработки уведомлений о перестроении сначала очищается поддерживаемое агрегированное состояние.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-162">In the preceding code, as part of processing the rebuild notification, first the maintained aggregated state is cleared.</span></span> <span data-ttu-id="fa5b4-163">Так как надежная коллекция перестраивается с новым состоянием, то все прежние уведомления несущественны.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-163">Because the reliable collection is being rebuilt with a new state, all previous notifications are irrelevant.</span></span>
> 
> 

<span data-ttu-id="fa5b4-164">Обработчик событий **DictionaryChanged** использует **NotifyDictionaryChangedEventArgs** для предоставления сведений о событии.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-164">The **DictionaryChanged** event handler uses **NotifyDictionaryChangedEventArgs** to provide details about the event.</span></span>
<span data-ttu-id="fa5b4-165">**NotifyDictionaryChangedEventArgs** .</span><span class="sxs-lookup"><span data-stu-id="fa5b4-165">**NotifyDictionaryChangedEventArgs** has five subclasses.</span></span> <span data-ttu-id="fa5b4-166">Свойство Action в **NotifyDictionaryChangedEventArgs** используется для приведения **NotifyDictionaryChangedEventArgs** к правильному подклассу:</span><span class="sxs-lookup"><span data-stu-id="fa5b4-166">Use the action property in **NotifyDictionaryChangedEventArgs** to cast **NotifyDictionaryChangedEventArgs** to the correct subclass:</span></span>

* <span data-ttu-id="fa5b4-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**;</span><span class="sxs-lookup"><span data-stu-id="fa5b4-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span></span>
* <span data-ttu-id="fa5b4-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**;</span><span class="sxs-lookup"><span data-stu-id="fa5b4-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span></span>
* <span data-ttu-id="fa5b4-169">**NotifyDictionaryChangedAction.Add** и **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**;</span><span class="sxs-lookup"><span data-stu-id="fa5b4-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span></span>
* <span data-ttu-id="fa5b4-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**;</span><span class="sxs-lookup"><span data-stu-id="fa5b4-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span></span>
* <span data-ttu-id="fa5b4-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span></span>

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

## <a name="recommendations"></a><span data-ttu-id="fa5b4-172">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="fa5b4-172">Recommendations</span></span>
* <span data-ttu-id="fa5b4-173">*Завершайте* события уведомлений максимально быстро.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-173">*Do* complete notification events as fast as possible.</span></span>
* <span data-ttu-id="fa5b4-174">*Не* выполняйте какие-либо ресурсоемкие операции (например, операции ввода-вывода) в составе синхронных событий.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-174">*Do not* execute any expensive operations (for example, I/O operations) as part of synchronous events.</span></span>
* <span data-ttu-id="fa5b4-175">*Проверяйте* тип действия перед обработкой события.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-175">*Do* check the action type before you process the event.</span></span> <span data-ttu-id="fa5b4-176">Новые типы действий могут быть добавлены в будущем.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-176">New action types might be added in the future.</span></span>

<span data-ttu-id="fa5b4-177">При этом нужно помнить о следующем:</span><span class="sxs-lookup"><span data-stu-id="fa5b4-177">Here are some things to keep in mind:</span></span>

* <span data-ttu-id="fa5b4-178">Уведомления срабатывают в ходе выполнения операции.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-178">Notifications are fired as part of the execution of an operation.</span></span> <span data-ttu-id="fa5b4-179">Например, уведомление о восстановлении срабатывает на последнем этапе восстановления.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-179">For example, a restore notification is fired as the last step of a restore operation.</span></span> <span data-ttu-id="fa5b4-180">Восстановление не будет завершено, пока это уведомление не будет обработано.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-180">A restore will not finish until the notification event is processed.</span></span>
* <span data-ttu-id="fa5b4-181">Так как уведомления активируются при применении операций, клиенты будут видеть только уведомления для локально зафиксированных операций.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-181">Because notifications are fired as part of the applying operations, clients see only notifications for locally committed operations.</span></span> <span data-ttu-id="fa5b4-182">Обратите внимание, что так как гарантируется только локальная фиксация операций (другими словами, ведение их журнала), то возможность в дальнейшем отменить их может быть как доступна, так и недоступна.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-182">And because operations are guaranteed only to be locally committed (in other words, logged), they might or might not be undone in the future.</span></span>
* <span data-ttu-id="fa5b4-183">На пути повтора для каждой примененной операции активируется одно уведомление.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-183">On the redo path, a single notification is fired for each applied operation.</span></span> <span data-ttu-id="fa5b4-184">Это означает, что если транзакция T1 содержит операции Create(X), Delete(X), Create(X), то вы получите одно уведомление о создании X, одно — об удалении и еще одно — о создании, причем в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-184">This means that if transaction T1 includes Create(X), Delete(X), and Create(X), you'll get one notification for the creation of X, one for the deletion, and one for the creation again, in that order.</span></span>
* <span data-ttu-id="fa5b4-185">Для транзакций, которые содержат несколько операций, эти операции будут применены в порядке, в котором они были получены от пользователя в первичной реплике.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-185">For transactions that contain multiple operations, operations are applied in the order in which they were received on the primary replica from the user.</span></span>
* <span data-ttu-id="fa5b4-186">При обработке хода выполнения с результатом false некоторые операции могут быть отменены.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-186">As part of processing false progress, some operations might be undone.</span></span> <span data-ttu-id="fa5b4-187">Для таких операций отмены будут создаваться уведомления и выполнен откат состояния реплики до стабильный точки.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-187">Notifications are raised for such undo operations, rolling the state of the replica back to a stable point.</span></span> <span data-ttu-id="fa5b4-188">Одно важное отличие уведомлений об отмене — события с повторяющимися ключами агрегируются.</span><span class="sxs-lookup"><span data-stu-id="fa5b4-188">One important difference of undo notifications is that events that have duplicate keys are aggregated.</span></span> <span data-ttu-id="fa5b4-189">Например, если упомянутая выше транзакция T1 отменяется, то пользователь увидит одно уведомление для операции Delete(X).</span><span class="sxs-lookup"><span data-stu-id="fa5b4-189">For example, if transaction T1 is being undone, you'll see a single notification to Delete(X).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa5b4-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fa5b4-190">Next steps</span></span>
* [<span data-ttu-id="fa5b4-191">Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="fa5b4-191">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="fa5b4-192">Краткое руководство по надежным службам Reliable Services</span><span class="sxs-lookup"><span data-stu-id="fa5b4-192">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="fa5b4-193">Архивация и восстановление (аварийное восстановление) надежных служб</span><span class="sxs-lookup"><span data-stu-id="fa5b4-193">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="fa5b4-194">Справочник разработчика по надежным коллекциям</span><span class="sxs-lookup"><span data-stu-id="fa5b4-194">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

