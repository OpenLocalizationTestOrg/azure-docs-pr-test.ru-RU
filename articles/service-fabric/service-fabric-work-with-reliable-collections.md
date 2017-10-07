---
title: "aaaWorking с коллекциями надежного | Документы Microsoft"
description: "Дополнительные рекомендации по работе с коллекциями надежного hello."
services: service-fabric
documentationcenter: .net
author: rajak
manager: timlt
editor: 
ms.assetid: 39e0cd6b-32c4-4b97-bbcf-33dad93dcad1
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/19/2017
ms.author: rajak
ms.openlocfilehash: 41ba0b257da8493c1fc2e99ad7565593dc7cbcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-reliable-collections"></a>Работа с Reliable Collections
Service Fabric предлагает с отслеживанием состояния, программирование модели разработчики too.NET доступны через надежные коллекций. В частности, Service Fabric предоставляет такие классы, как Reliable Dictionaries (далее — надежные словари) и Reliable Queues (далее — надежные очереди). При использовании этих классов состояние секционируется (для масштабируемости), реплицируется (для доступности) и обрабатывается в ходе транзакции в секции (для семантики ACID). Рассмотрим типичное использование объекта надежного словаря, чтобы узнать, какие функции этот объект выполняет.

```csharp

///retry:

try {
   // Create a new Transaction object for this partition
   using (ITransaction tx = base.StateManager.CreateTransaction()) {
      // AddAsync takes key's write lock; if >4 secs, TimeoutException
      // Key & value put in temp dictionary (read your own writes),
      // serialized, redo/undo record is logged & sent to
      // secondary replicas
      await m_dic.AddAsync(tx, key, value, cancellationToken);

      // CommitAsync sends Commit record toolog & secondary replicas
      // After quorum responds, all locks released
      await tx.CommitAsync();
   }
   // If CommitAsync not called, Dispose sends Abort
   // record toolog & all locks released
}
catch (TimeoutException) {
   await Task.Delay(100, cancellationToken); goto retry;
}
```

Для всех операций с объектами надежных словарей (за исключением операции ClearAsync, которая является обратимой) требуется объект ITransaction. Этот объект имеет связанные и все изменения, которому toomake tooany надежного словарь и/или надежного queue-объекты в одной секции. В случае приобретения ITransaction метод CreateTransaction StateManager этого объекта путем вызова hello секции.

В приведенном выше коде hello hello ITransaction объект передается метод AddAsync tooa надежного словаря. На внутреннем уровне словаря, которая принимает ключ получают блокировку чтения и записи, связанные с ключом hello. Если метод hello изменяет значение ключа hello, hello метод не выполняет блокировку записи ключа hello и если hello только считывает данные из значение ключа hello, блокировка чтения выполняются на ключ hello. Поскольку AddAsync изменяет новый toohello значение ключа hello, переданное значение hello ключ записи блокировка. Таким образом, если 2 (или более) потоков пытаются tooadd значениями hello ключ в hello же времени, один поток будет получить блокировку записи hello и hello другие потоки блокируются. По умолчанию методы блокировать блокировку too4 секунд tooacquire hello; После 4 секунды методы hello исключение TimeoutException. Перегрузки метода существует допускающему вы toopass явное значение времени ожидания, если вы хотите использовать.

Как правило пишутся tooa tooreact ваш код TimeoutException, его перехвату и повторение всей операции hello (как показано в приведенном выше коде hello). Мой простой код вызывает передачу Task.Delay через каждые 100 миллисекунд. Но на самом деле, возможно, будет лучше использовать экспоненциальную задержку.

После блокировки hello AddAsync добавляет ключ hello и tooan внутренний временный словарь связанный с объектом ITransaction hello, ссылается на объект значения. Это делается tooprovide вы с семантикой чтения your владельцем-операций записи. Т. е после вызова метода AddAsync, более поздних tooTryGetValueAsync вызова (с помощью hello объекта же ITransaction) вернет значение hello, даже если еще не зафиксирована транзакция hello. Затем AddAsync сериализует ключ и значение объектов toobyte массивы и добавляет эти байтов массивы tooa журнал на локальном узле hello. Наконец AddAsync отправляет hello байтов массивы tooall hello вторичные реплики, они имеют hello же ключ/значение сведений. Несмотря на то, что ключ/значение сведений hello записан файл журнала tooa, hello сведения не считается частью словарь hello, пока не будет зафиксирована транзакция hello, связанные с ними.

В приведенном выше коде hello tooCommitAsync вызов hello фиксирует все операции hello транзакции. В частности он добавляет файл журнала toohello фиксации сведения на локальном узле hello, а также отправляет hello фиксации записи tooall hello вторичных реплик. После ответил кворума (большинство) реплик hello, все данные, считается изменений постоянной, а все блокировки, связанные с ключами, которые были управлять с помощью объекта ITransaction hello освобождаются, другие потоки или транзакции можно управлять hello одинаковые ключи и их значения.

Если CommitAsync не вызывается (обычно из-за tooan исключения), hello объекта ITransaction возвращает ликвидирован. При ликвидации незафиксированных объекта ITransaction Service Fabric добавляет файл журнала abort сведения toohello локального узла, и ничего не должен toobe отправлено tooany из hello вторичных реплик. И затем освобождаются все блокировки, связанные с ключами, которые были управлять через hello транзакции.

## <a name="common-pitfalls-and-how-tooavoid-them"></a>Распространенные проблемы и как tooavoid их
Теперь, когда вы знаете, как надежный коллекций hello внутренне работают, давайте рассмотрим некоторые распространенные неправильно из них. См. приведенный ниже код hello:

```csharp
using (ITransaction tx = StateManager.CreateTransaction()) {
   // AddAsync serializes hello name/user, logs hello bytes,
   // & sends hello bytes toohello secondary replicas.
   await m_dic.AddAsync(tx, name, user);

   // hello line below updates hello property’s value in memory only; the
   // new value is NOT serialized, logged, & sent toosecondary replicas.
   user.LastLogin = DateTime.UtcNow;  // Corruption!

   await tx.CommitAsync();
}
```

При работе с регулярного словаря .NET, можно добавить toohello словарь ключей и значений, а затем изменить значение свойства (например, LastLogin) hello. Но этот код не будет правильно работать с надежным словарем. Помните из hello предыдущее обсуждение hello вызовов tooAddAsync сериализует hello ключей и значений объектов toobyte массивы, и затем сохраняет hello массивы tooa локального файла, а также отправляет их toohello вторичных реплик. Если впоследствии изменить свойство, меняется значение свойства hello в памяти. он не влияет на локальный файл hello или hello данные, отправляемые toohello реплик. При сбое процесса hello в памяти отбрасывается. При запуске нового процесса, или если другая реплика становится первичной, затем hello старое значение свойства — что можно.

Не удается выделить достаточно как просто можно toomake hello тип ошибки, показанный выше. И только рассказывается о hello ошибку если что hello процесс выходит из строя. Hello правильно toowrite hello код является просто tooreverse hello две строки:


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

Вот другой пример, демонстрирующий распространенную ошибку.

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use hello user’s name toolook up their data
   ConditionalValue<User> user =
      await m_dic.TryGetValueAsync(tx, name);

   // hello user exists in hello dictionary, update one of their properties.
   if (user.HasValue) {
      // hello line below updates hello property’s value in memory only; the
      // new value is NOT serialized, logged, & sent toosecondary replicas.
      user.Value.LastLogin = DateTime.UtcNow; // Corruption!
      await tx.CommitAsync();
   }
}
```

Еще раз, с помощью обычных словарей .NET, hello выше код хорошо работает и — это общий шаблон: hello разработчик использует ключа toolook значения. Если существует значение hello, hello разработчик меняет значение свойства. Тем не менее, с помощью надежного коллекций этот код видно hello той же проблемой, как описанные: **объекта не следует изменять, как только вы предоставили tooa надежного коллекции.**

способ tooupdate значение в коллекцию надежных tooget значение toohello существующей ссылки а рассмотрите tooby ссылка на объект hello, эта ссылка неизменяемый Hello. Затем создайте новый объект, который является точную копию исходного объекта hello. Теперь можно изменить состояние hello этот новый объект и писать hello новый объект в коллекцию hello таким образом, он сериализуется toobyte массивы, добавленных toohello локальный файл и отправить toohello реплик. После фиксации hello изменения объектов в памяти hello, hello локального файла, и у всех реплик hello hello же точное состояние. Теперь все хорошо.

Hello кода ниже показан правильный способ tooupdate hello значение в надежных коллекции:

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use hello user’s name toolook up their data
   ConditionalValue<User> currentUser =
      await m_dic.TryGetValueAsync(tx, name);

   // hello user exists in hello dictionary, update one of their properties.
   if (currentUser.HasValue) {
      // Create new user object with hello same state as hello current user object.
      // NOTE: This must be a deep copy; not a shallow copy. Specifically, only
      // immutable state can be shared by currentUser & updatedUser object graphs.
      User updatedUser = new User(currentUser);

      // In hello new object, modify any properties you desire
      updatedUser.LastLogin = DateTime.UtcNow;

      // Update hello key’s value toohello updateUser info
      await m_dic.SetValue(tx, name, updatedUser);

      await tx.CommitAsync();
   }
}
```

## <a name="define-immutable-data-types-tooprevent-programmer-error"></a>Определить ошибки программиста tooprevent типы постоянных данных
В идеальном случае мы предлагаем hello компилятора tooreport ошибки, если вы случайно создания кода, который изменяет состояние объекта, вы должны tooconsider неизменяемый. Но hello компилятор C# не поддерживает возможность toodo hello это. В этом случае tooavoid потенциальных программист ошибок, настоятельно рекомендуется, которые вы задаете hello типы, которые должны использоваться с типами неизменяемый toobe надежного коллекций. В частности это означает, что вы будете использовать toocore типы значений (например, номера [Int32, UInt64, т. д.], DateTime, Guid, TimeSpan и hello как). И, конечно, вы также можете использовать тип String. Это свойства коллекции наиболее tooavoid как сериализации и десериализации, их можно часто может вызвать снижение производительности. Однако следует свойства коллекции toouse настоятельно рекомендуется использование hello. Библиотека неизменяемых коллекций NET ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)). Эту библиотеку можно скачать на сайте http://nuget.org. Также рекомендуется запечатывать классы и по возможности предоставлять к полям доступ только для чтения.

Hello UserInfo типа ниже показано, как toodefine на постоянные тип преимуществ рекомендаций, упомянутых выше.

```csharp

[DataContract]
// If you don’t seal, you must ensure that any derived classes are also immutable
public sealed class UserInfo {
   private static readonly IEnumerable<ItemId> NoBids = ImmutableList<ItemId>.Empty;

   public UserInfo(String email, IEnumerable<ItemId> itemsBidding = null) {
      Email = email;
      ItemsBidding = (itemsBidding == null) ? NoBids : itemsBidding.ToImmutableList();
   }

   [OnDeserialized]
   private void OnDeserialized(StreamingContext context) {
      // Convert hello deserialized collection tooan immutable collection
      ItemsBidding = ItemsBidding.ToImmutableList();
   }

   [DataMember]
   public readonly String Email;

   // Ideally, this would be a readonly field but it can't be because OnDeserialized
   // has tooset it. So instead, hello getter is public and hello setter is private.
   [DataMember]
   public IEnumerable<ItemId> ItemsBidding { get; private set; }

   // Since each UserInfo object is immutable, we add a new ItemId toohello ItemsBidding
   // collection by creating a new immutable UserInfo object with hello added ItemId.
   public UserInfo AddItemBidding(ItemId itemId) {
      return new UserInfo(Email, ((ImmutableList<ItemId>)ItemsBidding).Add(itemId));
   }
}
```

Hello ItemId типа также является неизменяемым типом, как показано ниже:

```csharp

[DataContract]
public struct ItemId {

   [DataMember] public readonly String Seller;
   [DataMember] public readonly String ItemName;
   public ItemId(String seller, String itemName) {
      Seller = seller;
      ItemName = itemName;
   }
}
```

## <a name="schema-versioning-upgrades"></a>Управление версиями схемы (обновления)
На внутреннем уровне коллекции Reliable Collections сериализуют объекты с помощью DataContractSerializer .NET. Hello сериализовать объекты являются первичная реплика сохраненного toohello локального диска и — передаваемых toohello вторичных реплик. Мере разработки службы, вполне вероятно, будет необходимо toochange hello тип данных (схему), службе требуется. Управлять версиями данных необходимо предельно осторожно. Первое и самое главное всегда должен быть доступ toodeserialize старые данные. В частности, это означает десериализации код должен быть бесконечно обладает обратной совместимостью: 333 версии кода службы должен быть доступ toooperate на данные, помещенные в коллекцию надежных версии 1 код службы 5 лет назад.

Кроме того, код службы обновляет один домен обновления одновременно. Таким образом, во время обновления одновременно работают две различные версии кода службы. Вам необходимо не hello новой версии кода службы служит старых версий код службы может быть новая схема будет toohandle hello hello новой схемы. Если это возможно, следует разрабатывать каждой версии прямой совместимостью toobe service версии 1. В частности, это означает V1 кода службы должны обеспечивать toosimply игнорировать все элементы схемы, не обрабатывается явно. Тем не менее необходимо будет toosave, все данные, она не будет явно сведения и просто написать отката при обновлении словарь ключ или значение.

> [!WARNING]
> При изменении схемы hello ключа, необходимо убедиться, являются стабильными алгоритмы equals и ваш ключ хэш-код. При изменении любого из этих алгоритмов работу нельзя будет toolook копирование hello ключ в словаре надежного hello когда-либо еще раз.
>
>

Кроме того можно выполнить, что является tooas обычно ссылка на этапе 2 обновления. Обновления этапа 2, обновите службу из V1 tooV2: hello код, который знает, как выполнить toodeal с hello новое изменение схемы, но этот код не содержит V2. При hello V2 кода считывает данные V1, он обрабатывает его и записывает данные V1. Затем по завершении обновления hello во всех доменах обновления может каким-либо образом сигнал toohello запущенные экземпляры V2 обновления hello выполнена. (Одним из способов toosignal это tooroll ожидания обновления конфигурации; именно это и делает это обновление этап 2.) Теперь экземпляры V2 hello можно считывать данные V1, преобразовать его tooV2 данных, работать с ней и записать его как данные V2. При считывании данных V2 других экземпляров tooconvert не требуются, они просто работать с ней и запись данных V2.

## <a name="next-steps"></a>Дальнейшие действия
toolearn о создании контрактов прямой совместимых данных. в разделе [прямой совместимостью контракты данных](https://msdn.microsoft.com/library/ms731083.aspx).

см. рекомендации по управлению версиями контрактов данных, toolearn [управление версиями контракта данных](https://msdn.microsoft.com/library/ms731138.aspx).

toolearn нечувствительного к ошибкам данные tooimplement версии контрактов, разделе [обратных вызовов независимой от версий сериализации](https://msdn.microsoft.com/library/ms733734.aspx).

tooprovide структуру данных, могут взаимодействовать для нескольких версий в статье toolearn [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).
