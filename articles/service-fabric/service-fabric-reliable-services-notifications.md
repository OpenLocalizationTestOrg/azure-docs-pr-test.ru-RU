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
# <a name="reliable-services-notifications"></a>Уведомления Reliable Services
Уведомления позволяют клиентам tootrack hello изменения, которые были сделаны tooan объекта, который их интересует. Существует два типа объектов, поддерживающих уведомления: *диспетчер надежных состояний* и *надежный словарь*.

Распространенные причины для использования уведомлений:

* Построение материализованные представления, такие как вторичные индексы или группировка hello реплики состояние представления с фильтрацией. К примеру, это может быть отсортированный индекс всех ключей в надежном словаре.
* Отправка данных мониторинга, например hello число пользователей, добавленных в hello последний час.

Уведомления активируются в ходе применения операций. В связи с этим обработка уведомлений должна быть максимально быстрой и в синхронных событиях не должно быть ресурсоемких операций.

## <a name="reliable-state-manager-notifications"></a>Уведомления диспетчера надежных состояний
Диспетчер состояния надежное предоставляет уведомления о hello следующие события:

* транзакция:
  * Фиксация
* Диспетчер состояний:
  * перестроение;
  * добавление надежного состояния;
  * удаление надежного состояния.

Диспетчер состояния надежное отслеживает текущих транзакций порядковых hello. Hello единственное изменение в состоянии транзакции, которое вызывает уведомление toobe, инициированные состоит фиксации транзакции.

Диспетчер надежных состояний поддерживает коллекцию надежных состояний, таких как надежный словарь и надежная очередь. Диспетчер состояния надежное запускающей уведомления при изменении этой коллекции: надежные состояние добавляется или удаляется или перестраивается вся коллекция hello.
Hello надежного диспетчер состояния коллекции перестраивается в трех случаях:

* Восстановление: При запуске реплики, он восстанавливает предыдущее состояние с диска hello. В конце hello восстановления использует **NotifyStateManagerChangedEventArgs** toofire событие, которое содержит набор hello восстановленные надежного состояний.
* Полная копия: перед реплику можно присоединить hello набора конфигурации, он имеет toobe построения. В некоторых случаях для этого полную копию состояния надежного диспетчер состояний с hello первичная реплика toobe примененных toohello простоя вторичной реплики. Диспетчер состояния надежное на вторичной реплике использует hello **NotifyStateManagerChangedEventArgs** toofire событие, которое содержит набор hello надежного состояний, полученную из первичной реплики hello.
* Восстановление: В сценарии аварийного восстановления, состояние реплики hello можно восстановить из резервной копии через **RestoreAsync**. В таких случаях использует надежного диспетчер состояния в первичной реплике hello **NotifyStateManagerChangedEventArgs** toofire событие, которое содержит набор hello надежного состояний, которые он восстановлен из резервной копии hello.

tooregister для уведомления о транзакции и/или уведомления о состоянии диспетчера необходимо tooregister с hello **TransactionChanged** или **StateManagerChanged** событий на надежный диспетчер состояний. Обычно tooregister с эти обработчики событий является конструктором hello службы с отслеживанием состояния. При регистрации на конструктор hello не пропустить всех уведомлений, вызванным изменением время жизни hello **IReliableStateManager**.

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

Hello **TransactionChanged** обработчик событий использует **NotifyTransactionChangedEventArgs** tooprovide сведений о событии hello. Он содержит свойство hello действие (например, **NotifyTransactionChangedAction.Commit**), указывающий тип hello изменения. Он также содержит свойства транзакции hello, которое предоставляет транзакции toohello ссылку, которая изменила.

> [!NOTE]
> В настоящее время **TransactionChanged** событий только в том случае, если hello транзакция будет зафиксирована. Hello действия равен затем слишком**NotifyTransactionChangedAction.Commit**. Но в будущих hello, события могут возникать для других типов об изменениях состояния транзакции. Мы рекомендуем обработки hello событий только в том случае, если при этом предполагается, что и проверки действие hello.
> 
> 

Ниже приведен пример обработчика событий **TransactionChanged** .

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

Hello **StateManagerChanged** обработчик событий использует **NotifyStateManagerChangedEventArgs** tooprovide сведений о событии hello.
Существуют два подкласса экземпляра **NotifyStateManagerChangedEventArgs**: **NotifyStateManagerRebuildEventArgs** и **NotifyStateManagerSingleEntityChangedEventArgs**.
Использование свойства action hello в **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** правильный подкласс toohello:

* **NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**;
* **NotifyStateManagerChangedAction.Add** и **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**.

Ниже приведен пример обработчика уведомлений **StateManagerChanged** .

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

## <a name="reliable-dictionary-notifications"></a>Уведомления надежного словаря
Надежные словарь предоставляет уведомления о hello следующие события:

* Перестроение. Вызывается при восстановлении состояния **ReliableDictionary** из восстановленного или скопированного локального состояния либо из резервной копии.
* Очистить: Вызывается, когда hello состояние **ReliableDictionary** очищен через hello **ClearAsync** метод.
* Добавьте: Вызывается, когда элемент был добавлен слишком**ReliableDictionary**.
* Обновление. Вызывается при обновлении элемента в **IReliableDictionary**.
* Удаление. Вызывается при удалении элемента из **IReliableDictionary**.

tooget надежного словарь уведомления, необходимо tooregister с hello **DictionaryChanged** обработчику событий в **IReliableDictionary**. Обычно является tooregister с эти обработчики событий в hello **ReliableStateManager.StateManagerChanged** добавить уведомление.
При регистрации **IReliableDictionary** добавляется слишком**IReliableStateManager** гарантирует, что не будет пропускать любые уведомления.

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
> **ProcessStateManagerSingleEntityNotification** — метод образец hello, "hello" Предыдущий **OnStateManagerChangedHandler** пример вызывает.
> 
> 

Hello предыдущий код задает hello **IReliableNotificationAsyncCallback** интерфейс вместе с **DictionaryChanged**. Поскольку **NotifyDictionaryRebuildEventArgs** содержит **IAsyncEnumerable** интерфейс--которого необходимо перечислить асинхронно--toobe уведомления перестроения запускаются через  **RebuildNotificationAsyncCallback** вместо **OnDictionaryChangedHandler**.

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
> В hello предшествующий код, как часть обработки hello перестроения уведомления первый hello ведет агрегированных состояние будет очищено. Так как надежный коллекции hello восстанавливается с использованием нового состояния, все предыдущие уведомления не имеют значения.
> 
> 

Hello **DictionaryChanged** обработчик событий использует **NotifyDictionaryChangedEventArgs** tooprovide сведений о событии hello.
**NotifyDictionaryChangedEventArgs** . Использование свойства action hello в **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** правильный подкласс toohello:

* **NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**;
* **NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**;
* **NotifyDictionaryChangedAction.Add** и **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**;
* **NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**;
* **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**.

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

## <a name="recommendations"></a>Рекомендации
* *Завершайте* события уведомлений максимально быстро.
* *Не* выполняйте какие-либо ресурсоемкие операции (например, операции ввода-вывода) в составе синхронных событий.
* *Сделать* Проверьте тип действия hello перед обработкой событий hello. Новые типы действий могут быть добавлены в будущем hello.

Ниже приведены некоторые вещи tookeep в виду.

* Уведомления запускаются как часть hello выполнения операции. Например уведомление восстановления создается в качестве последнего шага hello операции восстановления. Восстановление не будет завершено до момента обработки события уведомления hello.
* Поскольку уведомления запускаются в рамках применения операций hello, клиенты могут видеть только уведомления для локально зафиксированных операций. А поскольку операций гарантируется только toobe зафиксированных локально (другими словами, регистрируется), они могут поддерживать или не могут быть отменены в будущих hello.
* По пути повтора hello одно уведомление создается для каждого примененного операции. Это означает, что если транзакция T1 включает Create(X), Delete(X) и Create(X), вы сможете получить одно уведомление для создания hello X, один для удаления hello и один для создания hello еще раз, в указанном порядке.
* Для транзакций, которые содержат несколько операций в порядке hello, в котором они были получены в первичной реплике hello hello пользователя применяются операции.
* При обработке хода выполнения с результатом false некоторые операции могут быть отменены. Уведомления возникают для таких операций отмены отката hello состояние hello реплики задней tooa стабильный точки. Одно важное отличие уведомлений об отмене — события с повторяющимися ключами агрегируются. Например если выполняется откат транзакции Т1, вы увидите tooDelete(X) одно уведомление.

## <a name="next-steps"></a>Дальнейшие действия
* [Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Краткое руководство по надежным службам Reliable Services](service-fabric-reliable-services-quick-start.md)
* [Архивация и восстановление (аварийное восстановление) надежных служб](service-fabric-reliable-services-backup-restore.md)
* [Справочник разработчика по надежным коллекциям](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

