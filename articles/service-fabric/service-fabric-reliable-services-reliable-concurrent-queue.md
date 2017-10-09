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
# <a name="introduction-tooreliableconcurrentqueue-in-azure-service-fabric"></a>TooReliableConcurrentQueue введение в Azure Service Fabric
Надежная параллельная очередь — это асинхронная, транзакционная и реплицируемая очередь, которая обладает высокой степенью параллелизма при операциях постановки в очередь и вывода из нее. Спроектированный toodeliver высокой пропускной способностью и малой задержкой, двухнедельного hello строгого FIFO упорядочение, предоставляемые [надежные очереди](https://msdn.microsoft.com/library/azure/dn971527.aspx) и вместо этого предоставляет возможность заказа по наилучшим образом.

## <a name="apis"></a>Интерфейсы API

|Параллельная очередь                |Надежная параллельная очередь                                         |
|--------------------------------|------------------------------------------------------------------|
| void Enqueue(T item)           | Task EnqueueAsync(ITransaction tx, T item)                       |
| bool TryDequeue(out T result)  | Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)  |
| int Count()                    | long Count()                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a>Сравнение с [надежной очередью](https://msdn.microsoft.com/library/azure/dn971527.aspx)

Надежные параллельной очереди предлагается в качестве альтернативы слишком[надежные очереди](https://msdn.microsoft.com/library/azure/dn971527.aspx). Ее следует использовать в случаях, когда строгое упорядочение FIFO не требуется, так как модель FIFO требует уменьшения степени параллелизма.  [Надежные очереди](https://msdn.microsoft.com/library/azure/dn971527.aspx) использует блокировки tooenforce FIFO упорядочение, с tooenqueue допускается не более одной транзакции и одновременно может выполняться toodequeue более одной транзакции. В отличие от этого надежного параллельной очереди снижает hello упорядочение ограничение позволяет любое число параллельных транзакций toointerleave их постановки в очередь и вывода из очереди операций. Упорядочение усилия предоставляется, однако hello относительный порядок два значения в надежных параллельной очереди может никогда не гарантируется.

Надежная параллельная очередь обеспечивает высокую пропускную способность и более низкую задержку, чем [надежная очередь](https://msdn.microsoft.com/library/azure/dn971527.aspx), во всех случаях, когда имеется несколько параллельных транзакций, выполняющих постановку в очередь и вывод из нее.

Образец Сфера применения hello ReliableConcurrentQueue — hello [очереди сообщений](https://en.wikipedia.org/wiki/Message_queue) сценария. В этом сценарии один или несколько отправителями сообщений создайте и добавьте очередь toohello элементов и один или несколько сообщений потребителям извлекать сообщения из очереди hello и их обработка. Несколько производители и потребители могут работать независимо, с помощью параллельных транзакций в порядке tooprocess hello очереди.

## <a name="usage-guidelines"></a>Рекомендации по использованию
* очереди Hello ожидает, что hello элементы в очереди hello имеют низкий срок. То есть hello элементов будет не остаются в очереди hello в течение долгого времени.
* очередь Hello не гарантирует строгого FIFO упорядочение.
* очередь Hello не считывает свои собственные записи. Если элемент помещается в очередь в рамках транзакции, он не будет видимым tooa dequeuer внутри hello одной транзакции.
* Операции вывода из очереди не изолированы друг от друга. Если элемент *A* удален из очереди транзакций *txnA*, даже если *txnA* не фиксируется, элемент *A* не будет видимым tooa параллельных транзакции *txnB*.  Если *txnA* прерываний, *A* будет видимым слишком*txnB* немедленно.
* *TryPeekAsync* поведение может быть реализован с помощью *TryDequeueAsync* и затем прерывание транзакции hello. Пример этого можно найти в разделе шаблонам программирования hello.
* Число является нетранзакционным. Он может находиться используется tooget представление о hello количество элементов в очереди hello, но представляет на момент времени и нельзя полагаться.
* Ресурсоемкие обработки hello исключенных из очереди элементов не должно выполняться хотя hello транзакция активна, tooavoid длительные транзакции, которые могут негативно повлиять на производительность в системе hello.

## <a name="code-snippets"></a>Фрагменты кода
Рассмотрим несколько фрагментов кода и ожидаемые выходные данные. Обработка исключений не рассматривается в этом разделе.

### <a name="enqueueasync"></a>EnqueueAsync
Вот несколько фрагментов кода по использованию EnqueueAsync, после которых приведены ожидаемые выходные данные.

- *Вариант 1. Одно задание постановки в очередь*

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

Предполагается hello задачи успешно завершена и, было параллельных транзакций нет Изменение очереди hello. Hello пользователь может ожидать toocontain hello hello очередь элементы в одном из следующих заказов hello:

> 10, 20

> 20, 10


- *Вариант 2. Параллельное задание постановки в очередь*

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

Предположим, что задачи hello завершено, что hello задачи выполняются параллельно и то, что существуют другие параллельные транзакции не изменение очереди hello. Без вывода может приниматься о hello порядок элементов в очереди hello. Для этого фрагмента кода отображения элементов hello в любой из hello 4! возможных порядков.  Hello очереди будет tookeep hello элементов в исходном порядке (в очереди) hello, но может быть принудительного tooreorder их из-за операций tooconcurrent или ошибки.


### <a name="dequeueasync"></a>DequeueAsync
Вот несколько фрагментов кода по использованию TryDequeueAsync следуют hello ожидается выходов. Предположим, что эта очередь hello уже заполненные hello следующих элементов в очереди hello:
> 10, 20, 30, 40, 50, 60

- *Вариант 1. Одно задание вывода из очереди*

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

Предполагается hello задачи успешно завершена и, было параллельных транзакций нет Изменение очереди hello. Поскольку можно сделать без вывода о порядке hello hello элементов в очереди hello, любые три hello элементов может быть удален из очереди, в любом порядке. Hello очереди будет tookeep hello элементов в исходном порядке (в очереди) hello, но может быть принудительного tooreorder их из-за операций tooconcurrent или ошибки.  

- *Вариант 2. Параллельное задание вывода из очереди*

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

Предположим, что задачи hello завершено, что hello задачи выполняются параллельно и то, что существуют другие параллельные транзакции не изменение очереди hello. Поскольку можно сделать без вывода о порядке hello hello элементов в очереди hello, hello списки *dequeue1* и *dequeue2* будет каждый из которых содержит любые два элемента в любом порядке.

Hello же элемент будет *не* отображаются в обоих списках. Поэтому если dequeue1 имеет элемент *10*, *30*, то deque2 будет иметь элементы *20*, *40*.

- *Вариант 3. Упорядочение вывода из очереди с прерыванием транзакции*

Прерывание транзакции с лету выводит помещает элементы hello обратно на начало hello hello очереди. Hello порядок, в котором элементы hello помещаются обратно на начало hello hello очереди не гарантируется. Рассмотрим hello, следующий код:

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort hello transaction
    await txn.AbortAsync();
}
```
Предположим, hello элементы были из очереди в hello следующий порядок:
> 10, 20

Когда мы прервать транзакцию hello, hello элементы будут добавлены в любой из следующих заказов hello начало обратной toohello hello очереди:
> 10, 20

> 20, 10

Hello это справедливо для всех случаев, где hello транзакция не была успешно *зафиксировано*.

## <a name="programming-patterns"></a>Шаблоны программирования
В этом разделе мы рассмотрим несколько шаблонов программирования, которые могут быть полезны при использовании надежной параллельной очереди.

### <a name="batch-dequeues"></a>Вывод из очереди в пакетном режиме
Рекомендуемое программирования шаблоном является toobatch задачи потребителя hello его выводит вместо выполнения одного вывода из очереди одновременно. Hello пользователь может выбрать toothrottle задержки между каждого пакета или hello размер пакета. Hello следующий фрагмент кода показывает этой модели программирования.  Обратите внимание, что в этом примере hello обработки выполняется после фиксации, транзакции hello, будто ошибка toooccur при обработке hello необработанные элементы будут потеряны без обработки.  Кроме того, hello обработка может выполняться в пределах области транзакции hello, однако это может оказать отрицательное влияние на производительность и требует обработки элементов hello уже обработано.

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

### <a name="best-effort-notification-based-processing"></a>Оптимальная обработка на основе уведомлений
Другой шаблон интересные программирования использует hello API счетчика. Здесь можно реализовать обработку основанная на уведомлении усилия для очереди hello. очередь Hello число может быть используется toothrottle объект постановки в очередь или задача вывода из очереди.  Обратите внимание, что как в предыдущем примере hello, поскольку обработка hello происходит вне транзакции hello необработанные элементы могут быть потеряны при возникновении ошибки во время обработки.

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

### <a name="best-effort-drain"></a>Оптимальная очистка
Очистку очереди hello не гарантируется из-за одновременных характер toohello hello структуры данных.  Это возможно, что, даже если никакие операции пользователя hello очередь незавершенных, tooTryDequeueAsync конкретный вызов могут не возвращать элемент, который ранее было поставлено в очередь и фиксации.  элемент в очередь Hello гарантируется слишком*со временем* становятся видимыми toodequeue, однако без механизм взаимодействия по каналу потребителя независимых не знает, что очередь hello достигла устойчивого состояния даже в том случае, если все производители были остановлены, и новые операции постановки в очередь разрешены. Таким образом операция очистки hello является наилучшим образом реализация ниже.

пользователь Hello следует остановить все последующие производителем и потребителем задачи и дождитесь любой транзакции на лету toocommit или прерывания, прежде чем toodrain hello очереди.  Если известно пользователю hello hello ожидалось число элементов в очереди hello, их можно настроить уведомления, который сигнализирует, что из очереди все элементы.

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

### <a name="peek"></a>Обзор
ReliableConcurrentQueue не предоставляет hello *TryPeekAsync* api. Пользователи могут получить hello peek семантики с помощью *TryDequeueAsync* и затем прерывание транзакции hello. В этом примере выводит обрабатываются только в том случае, если значение элемента hello больше, чем *10*.

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

## <a name="must-read"></a>Дополнительные сведения
* [Приступая к работе с надежными службами](service-fabric-reliable-services-quick-start.md)
* [Работа с Reliable Collections](service-fabric-work-with-reliable-collections.md)
* [Уведомления Reliable Services](service-fabric-reliable-services-notifications.md)
* [Резервное копирование и восстановление служб Reliable Services и субъектов Reliable Actors](service-fabric-reliable-services-backup-restore.md)
* [Настройка надежных служб с отслеживанием состояния](service-fabric-reliable-services-configuration.md)
* [ASP.NET Core в Service Fabric Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Расширенное использование hello надежная модель программирования служб](service-fabric-reliable-services-advanced-usage.md)
* [Справочник разработчика по надежным коллекциям](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
