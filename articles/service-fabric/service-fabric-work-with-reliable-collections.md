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
# <a name="working-with-reliable-collections"></a><span data-ttu-id="8a2e1-103">Работа с Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="8a2e1-103">Working with Reliable Collections</span></span>
<span data-ttu-id="8a2e1-104">Service Fabric предлагает с отслеживанием состояния, программирование модели разработчики too.NET доступны через надежные коллекций.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-104">Service Fabric offers a stateful programming model available too.NET developers via Reliable Collections.</span></span> <span data-ttu-id="8a2e1-105">В частности, Service Fabric предоставляет такие классы, как Reliable Dictionaries (далее — надежные словари) и Reliable Queues (далее — надежные очереди).</span><span class="sxs-lookup"><span data-stu-id="8a2e1-105">Specifically, Service Fabric provides reliable dictionary and reliable queue classes.</span></span> <span data-ttu-id="8a2e1-106">При использовании этих классов состояние секционируется (для масштабируемости), реплицируется (для доступности) и обрабатывается в ходе транзакции в секции (для семантики ACID).</span><span class="sxs-lookup"><span data-stu-id="8a2e1-106">When you use these classes, your state is partitioned (for scalability), replicated (for availability), and transacted within a partition (for ACID semantics).</span></span> <span data-ttu-id="8a2e1-107">Рассмотрим типичное использование объекта надежного словаря, чтобы узнать, какие функции этот объект выполняет.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-107">Let’s look at a typical usage of a reliable dictionary object and see what its actually doing.</span></span>

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

<span data-ttu-id="8a2e1-108">Для всех операций с объектами надежных словарей (за исключением операции ClearAsync, которая является обратимой) требуется объект ITransaction.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-108">All operations on reliable dictionary objects (except for ClearAsync which is not undoable), require an ITransaction object.</span></span> <span data-ttu-id="8a2e1-109">Этот объект имеет связанные и все изменения, которому toomake tooany надежного словарь и/или надежного queue-объекты в одной секции.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-109">This object has associated with it any and all changes you’re attempting toomake tooany reliable dictionary and/or reliable queue objects within a single partition.</span></span> <span data-ttu-id="8a2e1-110">В случае приобретения ITransaction метод CreateTransaction StateManager этого объекта путем вызова hello секции.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-110">You acquire an ITransaction object by calling hello partition’s StateManager’s CreateTransaction method.</span></span>

<span data-ttu-id="8a2e1-111">В приведенном выше коде hello hello ITransaction объект передается метод AddAsync tooa надежного словаря.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-111">In hello code above, hello ITransaction object is passed tooa reliable dictionary’s AddAsync method.</span></span> <span data-ttu-id="8a2e1-112">На внутреннем уровне словаря, которая принимает ключ получают блокировку чтения и записи, связанные с ключом hello.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-112">Internally, dictionary methods that accepts a key take a reader/writer lock associated with hello key.</span></span> <span data-ttu-id="8a2e1-113">Если метод hello изменяет значение ключа hello, hello метод не выполняет блокировку записи ключа hello и если hello только считывает данные из значение ключа hello, блокировка чтения выполняются на ключ hello.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-113">If hello method modifies hello key’s value, hello method takes a write lock on hello key and if hello method only reads from hello key’s value, then a read lock is taken on hello key.</span></span> <span data-ttu-id="8a2e1-114">Поскольку AddAsync изменяет новый toohello значение ключа hello, переданное значение hello ключ записи блокировка.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-114">Since AddAsync modifies hello key’s value toohello new, passed-in value, hello key’s write lock is taken.</span></span> <span data-ttu-id="8a2e1-115">Таким образом, если 2 (или более) потоков пытаются tooadd значениями hello ключ в hello же времени, один поток будет получить блокировку записи hello и hello другие потоки блокируются.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-115">So, if 2 (or more) threads attempt tooadd values with hello same key at hello same time, one thread will acquire hello write lock and hello other threads will block.</span></span> <span data-ttu-id="8a2e1-116">По умолчанию методы блокировать блокировку too4 секунд tooacquire hello; После 4 секунды методы hello исключение TimeoutException.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-116">By default, methods block for up too4 seconds tooacquire hello lock; after 4 seconds, hello methods throw a TimeoutException.</span></span> <span data-ttu-id="8a2e1-117">Перегрузки метода существует допускающему вы toopass явное значение времени ожидания, если вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-117">Method overloads exist allowing you toopass an explicit timeout value if you’d prefer.</span></span>

<span data-ttu-id="8a2e1-118">Как правило пишутся tooa tooreact ваш код TimeoutException, его перехвату и повторение всей операции hello (как показано в приведенном выше коде hello).</span><span class="sxs-lookup"><span data-stu-id="8a2e1-118">Usually, you write your code tooreact tooa TimeoutException by catching it and retrying hello entire operation (as shown in hello code above).</span></span> <span data-ttu-id="8a2e1-119">Мой простой код вызывает передачу Task.Delay через каждые 100 миллисекунд.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-119">In my simple code, I’m just calling Task.Delay passing 100 milliseconds each time.</span></span> <span data-ttu-id="8a2e1-120">Но на самом деле, возможно, будет лучше использовать экспоненциальную задержку.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-120">But, in reality, you might be better off using some kind of exponential back-off delay instead.</span></span>

<span data-ttu-id="8a2e1-121">После блокировки hello AddAsync добавляет ключ hello и tooan внутренний временный словарь связанный с объектом ITransaction hello, ссылается на объект значения.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-121">Once hello lock is acquired, AddAsync adds hello key and value object references tooan internal temporary dictionary associated with hello ITransaction object.</span></span> <span data-ttu-id="8a2e1-122">Это делается tooprovide вы с семантикой чтения your владельцем-операций записи.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-122">This is done tooprovide you with read-your-own-writes semantics.</span></span> <span data-ttu-id="8a2e1-123">Т. е после вызова метода AddAsync, более поздних tooTryGetValueAsync вызова (с помощью hello объекта же ITransaction) вернет значение hello, даже если еще не зафиксирована транзакция hello.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-123">That is, after you call AddAsync, a later call tooTryGetValueAsync (using hello same ITransaction object) will return hello value even if you have not yet committed hello transaction.</span></span> <span data-ttu-id="8a2e1-124">Затем AddAsync сериализует ключ и значение объектов toobyte массивы и добавляет эти байтов массивы tooa журнал на локальном узле hello.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-124">Next, AddAsync serializes your key and value objects toobyte arrays and appends these byte arrays tooa log file on hello local node.</span></span> <span data-ttu-id="8a2e1-125">Наконец AddAsync отправляет hello байтов массивы tooall hello вторичные реплики, они имеют hello же ключ/значение сведений.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-125">Finally, AddAsync sends hello byte arrays tooall hello secondary replicas so they have hello same key/value information.</span></span> <span data-ttu-id="8a2e1-126">Несмотря на то, что ключ/значение сведений hello записан файл журнала tooa, hello сведения не считается частью словарь hello, пока не будет зафиксирована транзакция hello, связанные с ними.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-126">Even though hello key/value information has been written tooa log file, hello information is not considered part of hello dictionary until hello transaction that they are associated with has been committed.</span></span>

<span data-ttu-id="8a2e1-127">В приведенном выше коде hello tooCommitAsync вызов hello фиксирует все операции hello транзакции.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-127">In hello code above, hello call tooCommitAsync commits all of hello transaction’s operations.</span></span> <span data-ttu-id="8a2e1-128">В частности он добавляет файл журнала toohello фиксации сведения на локальном узле hello, а также отправляет hello фиксации записи tooall hello вторичных реплик.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-128">Specifically, it appends commit information toohello log file on hello local node and also sends hello commit record tooall hello secondary replicas.</span></span> <span data-ttu-id="8a2e1-129">После ответил кворума (большинство) реплик hello, все данные, считается изменений постоянной, а все блокировки, связанные с ключами, которые были управлять с помощью объекта ITransaction hello освобождаются, другие потоки или транзакции можно управлять hello одинаковые ключи и их значения.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-129">Once a quorum (majority) of hello replicas has replied, all data changes are considered permanent and any locks associated with keys that were manipulated via hello ITransaction object are released so other threads/transactions can manipulate hello same keys and their values.</span></span>

<span data-ttu-id="8a2e1-130">Если CommitAsync не вызывается (обычно из-за tooan исключения), hello объекта ITransaction возвращает ликвидирован.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-130">If CommitAsync is not called (usually due tooan exception being thrown), then hello ITransaction object gets disposed.</span></span> <span data-ttu-id="8a2e1-131">При ликвидации незафиксированных объекта ITransaction Service Fabric добавляет файл журнала abort сведения toohello локального узла, и ничего не должен toobe отправлено tooany из hello вторичных реплик.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-131">When disposing an uncommitted ITransaction object, Service Fabric appends abort information toohello local node’s log file and nothing needs toobe sent tooany of hello secondary replicas.</span></span> <span data-ttu-id="8a2e1-132">И затем освобождаются все блокировки, связанные с ключами, которые были управлять через hello транзакции.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-132">And then, any locks associated with keys that were manipulated via hello transaction are released.</span></span>

## <a name="common-pitfalls-and-how-tooavoid-them"></a><span data-ttu-id="8a2e1-133">Распространенные проблемы и как tooavoid их</span><span class="sxs-lookup"><span data-stu-id="8a2e1-133">Common pitfalls and how tooavoid them</span></span>
<span data-ttu-id="8a2e1-134">Теперь, когда вы знаете, как надежный коллекций hello внутренне работают, давайте рассмотрим некоторые распространенные неправильно из них.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-134">Now that you understand how hello reliable collections work internally, let’s take a look at some common misuses of them.</span></span> <span data-ttu-id="8a2e1-135">См. приведенный ниже код hello:</span><span class="sxs-lookup"><span data-stu-id="8a2e1-135">See hello code below:</span></span>

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

<span data-ttu-id="8a2e1-136">При работе с регулярного словаря .NET, можно добавить toohello словарь ключей и значений, а затем изменить значение свойства (например, LastLogin) hello.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-136">When working with a regular .NET dictionary, you can add a key/value toohello dictionary and then change hello value of a property (such as LastLogin).</span></span> <span data-ttu-id="8a2e1-137">Но этот код не будет правильно работать с надежным словарем.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-137">However, this code will not work correctly with a reliable dictionary.</span></span> <span data-ttu-id="8a2e1-138">Помните из hello предыдущее обсуждение hello вызовов tooAddAsync сериализует hello ключей и значений объектов toobyte массивы, и затем сохраняет hello массивы tooa локального файла, а также отправляет их toohello вторичных реплик.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-138">Remember from hello earlier discussion, hello call tooAddAsync serializes hello key/value objects toobyte arrays and then saves hello arrays tooa local file and also sends them toohello secondary replicas.</span></span> <span data-ttu-id="8a2e1-139">Если впоследствии изменить свойство, меняется значение свойства hello в памяти. он не влияет на локальный файл hello или hello данные, отправляемые toohello реплик.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-139">If you later change a property, this changes hello property’s value in memory only; it does not impact hello local file or hello data sent toohello replicas.</span></span> <span data-ttu-id="8a2e1-140">При сбое процесса hello в памяти отбрасывается.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-140">If hello process crashes, what’s in memory is thrown away.</span></span> <span data-ttu-id="8a2e1-141">При запуске нового процесса, или если другая реплика становится первичной, затем hello старое значение свойства — что можно.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-141">When a new process starts or if another replica becomes primary, then hello old property value is what is available.</span></span>

<span data-ttu-id="8a2e1-142">Не удается выделить достаточно как просто можно toomake hello тип ошибки, показанный выше.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-142">I cannot stress enough how easy it is toomake hello kind of mistake shown above.</span></span> <span data-ttu-id="8a2e1-143">И только рассказывается о hello ошибку если что hello процесс выходит из строя.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-143">And, you will only learn about hello mistake if/when hello process goes down.</span></span> <span data-ttu-id="8a2e1-144">Hello правильно toowrite hello код является просто tooreverse hello две строки:</span><span class="sxs-lookup"><span data-stu-id="8a2e1-144">hello correct way toowrite hello code is simply tooreverse hello two lines:</span></span>


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

<span data-ttu-id="8a2e1-145">Вот другой пример, демонстрирующий распространенную ошибку.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-145">Here is another example showing a common mistake:</span></span>

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

<span data-ttu-id="8a2e1-146">Еще раз, с помощью обычных словарей .NET, hello выше код хорошо работает и — это общий шаблон: hello разработчик использует ключа toolook значения.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-146">Again, with regular .NET dictionaries, hello code above works fine and is a common pattern: hello developer uses a key toolook up a value.</span></span> <span data-ttu-id="8a2e1-147">Если существует значение hello, hello разработчик меняет значение свойства.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-147">If hello value exists, hello developer changes a property’s value.</span></span> <span data-ttu-id="8a2e1-148">Тем не менее, с помощью надежного коллекций этот код видно hello той же проблемой, как описанные: **объекта не следует изменять, как только вы предоставили tooa надежного коллекции.**</span><span class="sxs-lookup"><span data-stu-id="8a2e1-148">However, with reliable collections, this code exhibits hello same problem as already discussed: **you MUST not modify an object once you have given it tooa reliable collection.**</span></span>

<span data-ttu-id="8a2e1-149">способ tooupdate значение в коллекцию надежных tooget значение toohello существующей ссылки а рассмотрите tooby ссылка на объект hello, эта ссылка неизменяемый Hello.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-149">hello correct way tooupdate a value in a reliable collection, is tooget a reference toohello existing value and consider hello object referred tooby this reference immutable.</span></span> <span data-ttu-id="8a2e1-150">Затем создайте новый объект, который является точную копию исходного объекта hello.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-150">Then, create a new object which is an exact copy of hello original object.</span></span> <span data-ttu-id="8a2e1-151">Теперь можно изменить состояние hello этот новый объект и писать hello новый объект в коллекцию hello таким образом, он сериализуется toobyte массивы, добавленных toohello локальный файл и отправить toohello реплик.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-151">Now, you can modify hello state of this new object and write hello new object into hello collection so that it gets serialized toobyte arrays, appended toohello local file and sent toohello replicas.</span></span> <span data-ttu-id="8a2e1-152">После фиксации hello изменения объектов в памяти hello, hello локального файла, и у всех реплик hello hello же точное состояние.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-152">After committing hello change(s), hello in-memory objects, hello local file, and all hello replicas have hello same exact state.</span></span> <span data-ttu-id="8a2e1-153">Теперь все хорошо.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-153">All is good!</span></span>

<span data-ttu-id="8a2e1-154">Hello кода ниже показан правильный способ tooupdate hello значение в надежных коллекции:</span><span class="sxs-lookup"><span data-stu-id="8a2e1-154">hello code below shows hello correct way tooupdate a value in a reliable collection:</span></span>

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

## <a name="define-immutable-data-types-tooprevent-programmer-error"></a><span data-ttu-id="8a2e1-155">Определить ошибки программиста tooprevent типы постоянных данных</span><span class="sxs-lookup"><span data-stu-id="8a2e1-155">Define immutable data types tooprevent programmer error</span></span>
<span data-ttu-id="8a2e1-156">В идеальном случае мы предлагаем hello компилятора tooreport ошибки, если вы случайно создания кода, который изменяет состояние объекта, вы должны tooconsider неизменяемый.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-156">Ideally, we’d like hello compiler tooreport errors when you accidentally produce code that mutates state of an object that you are supposed tooconsider immutable.</span></span> <span data-ttu-id="8a2e1-157">Но hello компилятор C# не поддерживает возможность toodo hello это.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-157">But, hello C# compiler does not have hello ability toodo this.</span></span> <span data-ttu-id="8a2e1-158">В этом случае tooavoid потенциальных программист ошибок, настоятельно рекомендуется, которые вы задаете hello типы, которые должны использоваться с типами неизменяемый toobe надежного коллекций.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-158">So, tooavoid potential programmer bugs, we highly recommend that you define hello types you use with reliable collections toobe immutable types.</span></span> <span data-ttu-id="8a2e1-159">В частности это означает, что вы будете использовать toocore типы значений (например, номера [Int32, UInt64, т. д.], DateTime, Guid, TimeSpan и hello как).</span><span class="sxs-lookup"><span data-stu-id="8a2e1-159">Specifically, this means that you stick toocore value types (such as numbers [Int32, UInt64, etc.], DateTime, Guid, TimeSpan, and hello like).</span></span> <span data-ttu-id="8a2e1-160">И, конечно, вы также можете использовать тип String.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-160">And, of course, you can also use String.</span></span> <span data-ttu-id="8a2e1-161">Это свойства коллекции наиболее tooavoid как сериализации и десериализации, их можно часто может вызвать снижение производительности.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-161">It is best tooavoid collection properties as serializing and deserializing them can frequently can hurt performance.</span></span> <span data-ttu-id="8a2e1-162">Однако следует свойства коллекции toouse настоятельно рекомендуется использование hello. Библиотека неизменяемых коллекций NET ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span><span class="sxs-lookup"><span data-stu-id="8a2e1-162">However, if you want toouse collection properties, we highly recommend hello use of .NET’s immutable collections library ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span></span> <span data-ttu-id="8a2e1-163">Эту библиотеку можно скачать на сайте http://nuget.org. Также рекомендуется запечатывать классы и по возможности предоставлять к полям доступ только для чтения.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-163">This library is available for download from http://nuget.org. We also recommend sealing your classes and making fields read-only whenever possible.</span></span>

<span data-ttu-id="8a2e1-164">Hello UserInfo типа ниже показано, как toodefine на постоянные тип преимуществ рекомендаций, упомянутых выше.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-164">hello UserInfo type below demonstrates how toodefine an immutable type taking advantage of aforementioned recommendations.</span></span>

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

<span data-ttu-id="8a2e1-165">Hello ItemId типа также является неизменяемым типом, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="8a2e1-165">hello ItemId type is also an immutable type as shown here:</span></span>

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

## <a name="schema-versioning-upgrades"></a><span data-ttu-id="8a2e1-166">Управление версиями схемы (обновления)</span><span class="sxs-lookup"><span data-stu-id="8a2e1-166">Schema versioning (upgrades)</span></span>
<span data-ttu-id="8a2e1-167">На внутреннем уровне коллекции Reliable Collections сериализуют объекты с помощью DataContractSerializer .NET.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-167">Internally, Reliable Collections serialize your objects using .NET’s DataContractSerializer.</span></span> <span data-ttu-id="8a2e1-168">Hello сериализовать объекты являются первичная реплика сохраненного toohello локального диска и — передаваемых toohello вторичных реплик.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-168">hello serialized objects are persisted toohello primary replica’s local disk and are also transmitted toohello secondary replicas.</span></span> <span data-ttu-id="8a2e1-169">Мере разработки службы, вполне вероятно, будет необходимо toochange hello тип данных (схему), службе требуется.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-169">As your service matures, it’s likely you’ll want toochange hello kind of data (schema) your service requires.</span></span> <span data-ttu-id="8a2e1-170">Управлять версиями данных необходимо предельно осторожно.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-170">You must approach versioning of your data with great care.</span></span> <span data-ttu-id="8a2e1-171">Первое и самое главное всегда должен быть доступ toodeserialize старые данные.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-171">First and foremost, you must always be able toodeserialize old data.</span></span> <span data-ttu-id="8a2e1-172">В частности, это означает десериализации код должен быть бесконечно обладает обратной совместимостью: 333 версии кода службы должен быть доступ toooperate на данные, помещенные в коллекцию надежных версии 1 код службы 5 лет назад.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-172">Specifically, this means your deserialization code must be infinitely backward compatible: Version 333 of your service code must be able toooperate on data placed in a reliable collection by version 1 of your service code 5 years ago.</span></span>

<span data-ttu-id="8a2e1-173">Кроме того, код службы обновляет один домен обновления одновременно.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-173">Furthermore, service code is upgraded one upgrade domain at a time.</span></span> <span data-ttu-id="8a2e1-174">Таким образом, во время обновления одновременно работают две различные версии кода службы.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-174">So, during an upgrade, you have two different versions of your service code running simultaneously.</span></span> <span data-ttu-id="8a2e1-175">Вам необходимо не hello новой версии кода службы служит старых версий код службы может быть новая схема будет toohandle hello hello новой схемы.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-175">You must avoid having hello new version of your service code use hello new schema as old versions of your service code might not be able toohandle hello new schema.</span></span> <span data-ttu-id="8a2e1-176">Если это возможно, следует разрабатывать каждой версии прямой совместимостью toobe service версии 1.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-176">When possible, you should design each version of your service toobe forward compatible by 1 version.</span></span> <span data-ttu-id="8a2e1-177">В частности, это означает V1 кода службы должны обеспечивать toosimply игнорировать все элементы схемы, не обрабатывается явно.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-177">Specifically, this means that V1 of your service code should be able toosimply ignore any schema elements it does not explicitly handle.</span></span> <span data-ttu-id="8a2e1-178">Тем не менее необходимо будет toosave, все данные, она не будет явно сведения и просто написать отката при обновлении словарь ключ или значение.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-178">However, it must be able toosave any data it doesn’t explicitly know about and simply write it back out when updating a dictionary key or value.</span></span>

> [!WARNING]
> <span data-ttu-id="8a2e1-179">При изменении схемы hello ключа, необходимо убедиться, являются стабильными алгоритмы equals и ваш ключ хэш-код.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-179">While you can modify hello schema of a key, you must ensure that your key’s hash code and equals algorithms are stable.</span></span> <span data-ttu-id="8a2e1-180">При изменении любого из этих алгоритмов работу нельзя будет toolook копирование hello ключ в словаре надежного hello когда-либо еще раз.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-180">If you change how either of these algorithms operate, you will not be able toolook up hello key within hello reliable dictionary ever again.</span></span>
>
>

<span data-ttu-id="8a2e1-181">Кроме того можно выполнить, что является tooas обычно ссылка на этапе 2 обновления.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-181">Alternatively, you can perform what is typically referred tooas a 2-phase upgrade.</span></span> <span data-ttu-id="8a2e1-182">Обновления этапа 2, обновите службу из V1 tooV2: hello код, который знает, как выполнить toodeal с hello новое изменение схемы, но этот код не содержит V2.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-182">With a 2-phase upgrade, you upgrade your service from V1 tooV2: V2 contains hello code that knows how toodeal with hello new schema change but this code doesn’t execute.</span></span> <span data-ttu-id="8a2e1-183">При hello V2 кода считывает данные V1, он обрабатывает его и записывает данные V1.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-183">When hello V2 code reads V1 data, it operates on it and writes V1 data.</span></span> <span data-ttu-id="8a2e1-184">Затем по завершении обновления hello во всех доменах обновления может каким-либо образом сигнал toohello запущенные экземпляры V2 обновления hello выполнена.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-184">Then, after hello upgrade is complete across all upgrade domains, you can somehow signal toohello running V2 instances that hello upgrade is complete.</span></span> <span data-ttu-id="8a2e1-185">(Одним из способов toosignal это tooroll ожидания обновления конфигурации; именно это и делает это обновление этап 2.) Теперь экземпляры V2 hello можно считывать данные V1, преобразовать его tooV2 данных, работать с ней и записать его как данные V2.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-185">(One way toosignal this is tooroll out a configuration upgrade; this is what makes this a 2-phase upgrade.) Now, hello V2 instances can read V1 data, convert it tooV2 data, operate on it, and write it out as V2 data.</span></span> <span data-ttu-id="8a2e1-186">При считывании данных V2 других экземпляров tooconvert не требуются, они просто работать с ней и запись данных V2.</span><span class="sxs-lookup"><span data-stu-id="8a2e1-186">When other instances read V2 data, they do not need tooconvert it, they just operate on it, and write out V2 data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a2e1-187">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8a2e1-187">Next Steps</span></span>
<span data-ttu-id="8a2e1-188">toolearn о создании контрактов прямой совместимых данных. в разделе [прямой совместимостью контракты данных](https://msdn.microsoft.com/library/ms731083.aspx).</span><span class="sxs-lookup"><span data-stu-id="8a2e1-188">toolearn about creating forward compatible data contracts, see [Forward-Compatible Data Contracts](https://msdn.microsoft.com/library/ms731083.aspx).</span></span>

<span data-ttu-id="8a2e1-189">см. рекомендации по управлению версиями контрактов данных, toolearn [управление версиями контракта данных](https://msdn.microsoft.com/library/ms731138.aspx).</span><span class="sxs-lookup"><span data-stu-id="8a2e1-189">toolearn best practices on versioning data contracts, see [Data Contract Versioning](https://msdn.microsoft.com/library/ms731138.aspx).</span></span>

<span data-ttu-id="8a2e1-190">toolearn нечувствительного к ошибкам данные tooimplement версии контрактов, разделе [обратных вызовов независимой от версий сериализации](https://msdn.microsoft.com/library/ms733734.aspx).</span><span class="sxs-lookup"><span data-stu-id="8a2e1-190">toolearn how tooimplement version tolerant data contracts, see [Version-Tolerant Serialization Callbacks](https://msdn.microsoft.com/library/ms733734.aspx).</span></span>

<span data-ttu-id="8a2e1-191">tooprovide структуру данных, могут взаимодействовать для нескольких версий в статье toolearn [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="8a2e1-191">toolearn how tooprovide a data structure that can interoperate across multiple versions, see [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span></span>
