---
title: "aaaStart и stop tootest узлы кластера Azure микрослужбами | Документы Microsoft"
description: "Узнайте, как toouse fault tootest внедрение приложения Service Fabric, запуск и остановка узлов кластера."
services: service-fabric
documentationcenter: .net
author: LMWF
manager: rsinha
editor: 
ms.assetid: f4e70f6f-cad9-4a3e-9655-009b4db09c6d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/12/2017
ms.author: lemai
ms.openlocfilehash: 7d3f5147328e6233a67533fbfb2a525aa5fc060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replacing-hello-start-node-and-stop-node-apis-with-hello-node-transition-api"></a><span data-ttu-id="c2083-103">Заменив hello узла перехода API hello начального узла и остановка узла API-интерфейсы</span><span class="sxs-lookup"><span data-stu-id="c2083-103">Replacing hello Start Node and Stop node APIs with hello Node Transition API</span></span>

## <a name="what-do-hello-stop-node-and-start-node-apis-do"></a><span data-ttu-id="c2083-104">Что hello остановить узел и запуск узла интерфейсы API?</span><span class="sxs-lookup"><span data-stu-id="c2083-104">What do hello Stop Node and Start Node APIs do?</span></span>

<span data-ttu-id="c2083-105">Остановить узел API Hello (управляемые: [StopNodeAsync()][stopnode], PowerShell: [Stop ServiceFabricNode][stopnodeps]) останавливает узел Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c2083-105">hello Stop Node API (managed: [StopNodeAsync()][stopnode], PowerShell: [Stop-ServiceFabricNode][stopnodeps]) stops a Service Fabric node.</span></span>  <span data-ttu-id="c2083-106">Узел Service Fabric — процесс, виртуальная машина или машины — hello виртуальная машина или машины по-прежнему будут выполняться.</span><span class="sxs-lookup"><span data-stu-id="c2083-106">A Service Fabric node is process, not a VM or machine – hello VM or machine will still be running.</span></span>  <span data-ttu-id="c2083-107">Hello оставшейся части документа hello «узла» будет означать узел Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c2083-107">For hello rest of hello document "node" will mean Service Fabric node.</span></span>  <span data-ttu-id="c2083-108">Остановка узла помещает его в *остановлена* состоянии, которое он не является членом кластера hello невозможно разместить службы, что позволяет имитировать *работу* узла.</span><span class="sxs-lookup"><span data-stu-id="c2083-108">Stopping a node puts it into a *stopped* state where it is not a member of hello cluster and cannot host services, thus simulating a *down* node.</span></span>  <span data-ttu-id="c2083-109">Это полезно для добавления ошибок в системе tootest hello приложения.</span><span class="sxs-lookup"><span data-stu-id="c2083-109">This is useful for injecting faults into hello system tootest your application.</span></span>  <span data-ttu-id="c2083-110">Hello запустить узел API (управляемые: [StartNodeAsync()][startnode], PowerShell: [начала ServiceFabricNode][startnodeps]]) отменяет hello API остановить узел  вызывает hello узел задней tooa нормальное состояние.</span><span class="sxs-lookup"><span data-stu-id="c2083-110">hello Start Node API (managed: [StartNodeAsync()][startnode], PowerShell: [Start-ServiceFabricNode][startnodeps]]) reverses hello Stop Node API,  which brings hello node back tooa normal state.</span></span>

## <a name="why-are-we-replacing-these"></a><span data-ttu-id="c2083-111">Зачем их заменять?</span><span class="sxs-lookup"><span data-stu-id="c2083-111">Why are we replacing these?</span></span>

<span data-ttu-id="c2083-112">Как было сказано выше, *остановлена* Service Fabric узел является узлом намеренно целевые с помощью hello API остановить узел.</span><span class="sxs-lookup"><span data-stu-id="c2083-112">As described earlier, a *stopped* Service Fabric node is a node intentionally targeted using hello Stop Node API.</span></span>  <span data-ttu-id="c2083-113">Объект *работу* узел является узлом, не работает для какой-либо причине (например hello виртуальная машина или машины — off).</span><span class="sxs-lookup"><span data-stu-id="c2083-113">A *down* node is a node that is down for any other reason (e.g. hello VM or machine is off).</span></span>  <span data-ttu-id="c2083-114">С hello остановить узел API системы hello не предоставляет сведения toodifferentiate между *остановлена* узлов и *работу* узлов.</span><span class="sxs-lookup"><span data-stu-id="c2083-114">With hello Stop Node API, hello system does not expose information toodifferentiate between *stopped* nodes and *down* nodes.</span></span>

<span data-ttu-id="c2083-115">Кроме того, некоторые сообщения об ошибках, возвращаемые этими API-интерфейсами, недостаточно содержательны.</span><span class="sxs-lookup"><span data-stu-id="c2083-115">In addition, some errors returned by these APIs are not as descriptive as they could be.</span></span>  <span data-ttu-id="c2083-116">Например, вызов hello остановить узел API на объект уже *остановлена* узел вернет ошибку hello *InvalidAddress*.</span><span class="sxs-lookup"><span data-stu-id="c2083-116">For example, invoking hello Stop Node API on an already *stopped* node will return hello error *InvalidAddress*.</span></span>  <span data-ttu-id="c2083-117">Это поведение можно оптимизировать.</span><span class="sxs-lookup"><span data-stu-id="c2083-117">This experience could be improved.</span></span>

<span data-ttu-id="c2083-118">Кроме того пока hello, запустить узел API вызывается hello время, в течение которого узел остановлен на «бесконечность».</span><span class="sxs-lookup"><span data-stu-id="c2083-118">Also, hello duration a node is stopped for is “infinite” until hello Start Node API is invoked.</span></span>  <span data-ttu-id="c2083-119">Выяснилось, что это может привести к проблемам и возникновению ошибок.</span><span class="sxs-lookup"><span data-stu-id="c2083-119">We’ve found this can cause problems and may be error-prone.</span></span>  <span data-ttu-id="c2083-120">Например описанных выше проблем, где пользователь вызывается hello остановить узел API на узле и затем забыли о нем.</span><span class="sxs-lookup"><span data-stu-id="c2083-120">For example, we’ve seen problems where a user invoked hello Stop Node API on a node and then forgot about it.</span></span>  <span data-ttu-id="c2083-121">Позже, было ясно, если узел hello был *работу* или *остановлена*.</span><span class="sxs-lookup"><span data-stu-id="c2083-121">Later, it was unclear if hello node was *down* or *stopped*.</span></span>


## <a name="introducing-hello-node-transition-apis"></a><span data-ttu-id="c2083-122">Знакомство с приложением hello API-интерфейсы узла перехода</span><span class="sxs-lookup"><span data-stu-id="c2083-122">Introducing hello Node Transition APIs</span></span>

<span data-ttu-id="c2083-123">Описанные выше проблемы можно решить с помощью нашего нового набора API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="c2083-123">We’ve addressed these issues above in a new set of APIs.</span></span>  <span data-ttu-id="c2083-124">новый узел перехода API Hello (управляемые: [StartNodeTransitionAsync()][snt]) может быть используется tootransition tooa узел Service Fabric *остановлена* состояния или tootransition его из *остановлена* состояние tooa обычного состояния.</span><span class="sxs-lookup"><span data-stu-id="c2083-124">hello new Node Transition API (managed: [StartNodeTransitionAsync()][snt]) may be used tootransition a Service Fabric node tooa *stopped* state, or tootransition it from a *stopped* state tooa normal up state.</span></span>  <span data-ttu-id="c2083-125">Обратите внимание, что hello «Start» в качестве имени hello hello API не ссылается toostarting узла.</span><span class="sxs-lookup"><span data-stu-id="c2083-125">Please note that hello “Start” in hello name of hello API does not refer toostarting a node.</span></span>  <span data-ttu-id="c2083-126">Он ссылается toobeginning асинхронной операции, система hello будет выполняться tootransition hello узел tooeither *остановлена* или рабочем состоянии.</span><span class="sxs-lookup"><span data-stu-id="c2083-126">It refers toobeginning an asynchronous operation that hello system will execute tootransition hello node tooeither *stopped* or started state.</span></span>

<span data-ttu-id="c2083-127">**Использование**</span><span class="sxs-lookup"><span data-stu-id="c2083-127">**Usage**</span></span>

<span data-ttu-id="c2083-128">Если hello узла перехода API не вызывает исключение при вызове, система hello принял hello асинхронной операции и выполнит его.</span><span class="sxs-lookup"><span data-stu-id="c2083-128">If hello Node Transition API does not throw an exception when invoked, then hello system has accepted hello asynchronous operation, and will execute it.</span></span>  <span data-ttu-id="c2083-129">Успешного вызова не означает, что еще завершена операция hello.</span><span class="sxs-lookup"><span data-stu-id="c2083-129">A successful call does not imply hello operation is finished yet.</span></span>  <span data-ttu-id="c2083-130">tooget сведения о текущем состоянии hello операции hello, hello вызов API выполняется переход узел (управляемые: [GetNodeTransitionProgressAsync()][gntp]) с идентификатором guid hello, используемых при вызове узла API переход для этой операции.</span><span class="sxs-lookup"><span data-stu-id="c2083-130">tooget information about hello current state of hello operation, call hello Node Transition Progress API (managed: [GetNodeTransitionProgressAsync()][gntp]) with hello guid used when invoking Node Transition API for this operation.</span></span>  <span data-ttu-id="c2083-131">Hello узла перехода выполняется API возвращает объект NodeTransitionProgress.</span><span class="sxs-lookup"><span data-stu-id="c2083-131">hello Node Transition Progress API returns an NodeTransitionProgress object.</span></span>  <span data-ttu-id="c2083-132">Состояние объекта указывает текущее состояние операции hello hello.</span><span class="sxs-lookup"><span data-stu-id="c2083-132">This object’s State property specifies hello current state of hello operation.</span></span>  <span data-ttu-id="c2083-133">Если hello состояние «выполняется», выполняется операция hello.</span><span class="sxs-lookup"><span data-stu-id="c2083-133">If hello state is “Running” then hello operation is executing.</span></span>  <span data-ttu-id="c2083-134">Если она будет завершена, операция hello завершена без ошибок.</span><span class="sxs-lookup"><span data-stu-id="c2083-134">If it is Completed, hello operation finished without error.</span></span>  <span data-ttu-id="c2083-135">Если он находится в состоянии сбоя, произошла ошибка при выполнении операции hello.</span><span class="sxs-lookup"><span data-stu-id="c2083-135">If it is Faulted, there was a problem executing hello operation.</span></span>  <span data-ttu-id="c2083-136">свойства Result Hello свойство будет указывать, какие hello выдавать исключение.</span><span class="sxs-lookup"><span data-stu-id="c2083-136">hello Result property’s Exception property will indicate what hello issue was.</span></span>  <span data-ttu-id="c2083-137">В разделе https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate Дополнительные сведения о свойство State hello и hello «Использование образца» приведены ниже в разделе примеров кода.</span><span class="sxs-lookup"><span data-stu-id="c2083-137">See https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate for more information about hello State property, and hello “Sample Usage” section below for code examples.</span></span>


<span data-ttu-id="c2083-138">**Разграничения остановлена узел и узел вниз** Если узел является *остановлена* с помощью hello API узел перехода, выходные данные запроса узел hello (управляемые: [GetNodeListAsync()] [ nodequery], PowerShell: [Get ServiceFabricNode][nodequeryps]) будет показывать, что этот узел есть *IsStopped* свойство значение true.</span><span class="sxs-lookup"><span data-stu-id="c2083-138">**Differentiating between a stopped node and a down node** If a node is *stopped* using hello Node Transition API, hello output of a node query (managed: [GetNodeListAsync()][nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) will show that this node has an *IsStopped* property value of true.</span></span>  <span data-ttu-id="c2083-139">Обратите внимание на это поведение отличается от значение hello hello *NodeStatus* свойство, которое укажет *работу*.</span><span class="sxs-lookup"><span data-stu-id="c2083-139">Note this is different from hello value of hello *NodeStatus* property, which will say *Down*.</span></span>  <span data-ttu-id="c2083-140">Если hello *NodeStatus* свойство имеет значение *работу*, но *IsStopped* имеет значение false, то hello узел не был остановлен, с помощью API перехода узла hello и является  *Вниз* из-за какой-либо другой причине.</span><span class="sxs-lookup"><span data-stu-id="c2083-140">If hello *NodeStatus* property has a value of *Down*, but *IsStopped* is false, then hello node was not stopped using hello Node Transition API, and is *Down* due some other reason.</span></span>  <span data-ttu-id="c2083-141">Если hello *IsStopped* свойство имеет значение true, а hello *NodeStatus* свойство *работу*, то остановлена с помощью hello API узла перехода.</span><span class="sxs-lookup"><span data-stu-id="c2083-141">If hello *IsStopped* property is true, and hello *NodeStatus* property is *Down*, then it was stopped using hello Node Transition API.</span></span>

<span data-ttu-id="c2083-142">Запуск *остановлена* узла, используя hello узла перехода API вернет его toofunction как обычный членом кластера hello еще раз.</span><span class="sxs-lookup"><span data-stu-id="c2083-142">Starting a *stopped* node using hello Node Transition API will return it toofunction as a normal member of hello cluster again.</span></span>  <span data-ttu-id="c2083-143">Hello выходные данные запроса узла hello API будет показывать *IsStopped* false, и *NodeStatus* как элемент, не являющийся вниз (например вверх).</span><span class="sxs-lookup"><span data-stu-id="c2083-143">hello output of hello node query API will show *IsStopped* as false, and *NodeStatus* as something that is not Down (e.g. Up).</span></span>


<span data-ttu-id="c2083-144">**Ограниченные длительность** при использовании узла перехода API hello toostop узла, один из hello необходимые параметры *stopNodeDurationInSeconds*, представляет hello количество времени в секундах tookeep hello узел  *Остановить*.</span><span class="sxs-lookup"><span data-stu-id="c2083-144">**Limited Duration** When using hello Node Transition API toostop a node, one of hello required parameters, *stopNodeDurationInSeconds*, represents hello amount of time in seconds tookeep hello node *stopped*.</span></span>  <span data-ttu-id="c2083-145">Это значение должно быть в допустимый диапазон, имеющий 600 минимум и максимум 14400 hello.</span><span class="sxs-lookup"><span data-stu-id="c2083-145">This value must be in hello allowed range, which has a minimum of 600, and a maximum of 14400.</span></span>  <span data-ttu-id="c2083-146">После истечения этого времени, узел hello сам в показатель состояния автоматически перезагрузится.</span><span class="sxs-lookup"><span data-stu-id="c2083-146">After this time expires, hello node will restart itself into Up state automatically.</span></span>  <span data-ttu-id="c2083-147">См. пример использования tooSample 1 ниже.</span><span class="sxs-lookup"><span data-stu-id="c2083-147">Refer tooSample 1 below for an example of usage.</span></span>

> [!WARNING]
> <span data-ttu-id="c2083-148">Использовать API-интерфейсы узла перехода и hello узла остановить и запустить узел API.</span><span class="sxs-lookup"><span data-stu-id="c2083-148">Avoid mixing Node Transition APIs and hello Stop Node and Start Node APIs.</span></span>  <span data-ttu-id="c2083-149">Hello рекомендуется слишком использовать только hello API узла перехода.</span><span class="sxs-lookup"><span data-stu-id="c2083-149">hello recommendation is too use hello Node Transition API only.</span></span>  <span data-ttu-id="c2083-150">> Если узел уже была остановлена при помощи hello остановить узел API, она должна быть запущена посредством hello API запустить узел сначала перед использованием hello > API-интерфейсы узла перехода.</span><span class="sxs-lookup"><span data-stu-id="c2083-150">> If a node has been already been stopped using hello Stop Node API, it should be started using hello Start Node API first before using hello > Node Transition APIs.</span></span>

> [!WARNING]
> <span data-ttu-id="c2083-151">Несколько интерфейсов API перехода узла вызовы нельзя сделать на hello одним узлом в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="c2083-151">Multiple Node Transition APIs calls cannot be made on hello same node in parallel.</span></span>  <span data-ttu-id="c2083-152">В таком случае будет hello API перехода узла > throw FabricException со значением свойства ErrorCode NodeTransitionInProgress.</span><span class="sxs-lookup"><span data-stu-id="c2083-152">In such a situation, hello Node Transition API will    > throw a FabricException with an ErrorCode property value of NodeTransitionInProgress.</span></span>  <span data-ttu-id="c2083-153">После перехода узла на определенном узле имеет > была запущена, нужно подождать, пока операция hello достигнет конечного состояния (завершено, Faulted или ForceCancelled) перед запуском > new переход на hello же узла.</span><span class="sxs-lookup"><span data-stu-id="c2083-153">Once a node transition on a specific node has  > been started, you should wait until hello operation reaches a terminal state (Completed, Faulted, or ForceCancelled) before starting a  > new transition on hello same node.</span></span>  <span data-ttu-id="c2083-154">Параллельные вызовы перехода на разных узлах разрешены.</span><span class="sxs-lookup"><span data-stu-id="c2083-154">Parallel node transition calls on different nodes are allowed.</span></span>


#### <a name="sample-usage"></a><span data-ttu-id="c2083-155">Пример использования</span><span class="sxs-lookup"><span data-stu-id="c2083-155">Sample Usage</span></span>


<span data-ttu-id="c2083-156">**Пример 1** -hello следующие образцы использования hello toostop API узла перехода узла.</span><span class="sxs-lookup"><span data-stu-id="c2083-156">**Sample 1** - hello following sample uses hello Node Transition API toostop a node.</span></span>

```csharp
        // Helper function tooget information about a node
        static Node GetNodeInfo(FabricClient fc, string node)
        {
            NodeList n = null;
            while (n == null)
            {
                n = fc.QueryManager.GetNodeListAsync(node).GetAwaiter().GetResult();
                Task.Delay(TimeSpan.FromSeconds(1)).GetAwaiter();
            };

            return n.FirstOrDefault();
        }

        static async Task WaitForStateAsync(FabricClient fc, Guid operationId, TestCommandProgressState targetState)
        {
            NodeTransitionProgress progress = null;

            do
            {
                bool exceptionObserved = false;
                try
                {
                    progress = await fc.TestManager.GetNodeTransitionProgressAsync(operationId, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                    exceptionObserved = true;
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                    exceptionObserved = true;
                }

                if (!exceptionObserved)
                {
                    Console.WriteLine("Current state of operation '{0}': {1}", operationId, progress.State);

                    if (progress.State == TestCommandProgressState.Faulted)
                    {
                        // Inspect hello progress object's Result.Exception.HResult tooget hello error code.
                        Console.WriteLine("'{0}' failed with: {1}, HResult: {2}", operationId, progress.Result.Exception, progress.Result.Exception.HResult);

                        // ...additional logic as required
                    }

                    if (progress.State == targetState)
                    {
                        Console.WriteLine("Target state '{0}' has been reached", targetState);
                        break;
                    }
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (true);
        }

        static async Task StopNodeAsync(FabricClient fc, string nodeName, int durationInSeconds)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            // Create a Guid
            Guid guid = Guid.NewGuid();

            // Create a NodeStopDescription object, which will be used as a parameter into StartNodeTransition
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, durationInSeconds);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStopDescription from above, which will stop hello target node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    // This is retryable
                }
                catch (FabricTransientException fte)
                {
                    // This is retryable
                }

                // Backoff
                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

<span data-ttu-id="c2083-157">**Пример 2** - hello после запуска образца *остановлена* узла.</span><span class="sxs-lookup"><span data-stu-id="c2083-157">**Sample 2** - hello following sample starts a *stopped* node.</span></span>  <span data-ttu-id="c2083-158">Она использует некоторые вспомогательные методы из первого примера hello.</span><span class="sxs-lookup"><span data-stu-id="c2083-158">It uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StartNodeAsync(FabricClient fc, string nodeName)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = n.NodeInstanceId;

            // Create a NodeStartDescription object, which will be used as a parameter into StartNodeTransition
            NodeStartDescription description = new NodeStartDescription(guid, n.NodeName, nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

<span data-ttu-id="c2083-159">**Пример 3** - hello ниже приведен пример неправильное использование.</span><span class="sxs-lookup"><span data-stu-id="c2083-159">**Sample 3** - hello following sample shows incorrect usage.</span></span>  <span data-ttu-id="c2083-160">Неверное использование этой поскольку hello *stopDurationInSeconds* он предоставляет больше, чем hello, допустимый диапазон.</span><span class="sxs-lookup"><span data-stu-id="c2083-160">This usage is incorrect because hello *stopDurationInSeconds* it provides is greater than hello allowed range.</span></span>  <span data-ttu-id="c2083-161">Поскольку StartNodeTransitionAsync() завершится ошибкой при возникновении неустранимой ошибки, hello операции не был принят, и не следует вызывать API hello хода выполнения.</span><span class="sxs-lookup"><span data-stu-id="c2083-161">Since StartNodeTransitionAsync() will fail with a fatal error, hello operation was not accepted, and hello progress API should not be called.</span></span>  <span data-ttu-id="c2083-162">Этот пример использует некоторые вспомогательные методы из первого примера hello.</span><span class="sxs-lookup"><span data-stu-id="c2083-162">This sample uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StopNodeWithOutOfRangeDurationAsync(FabricClient fc, string nodeName)
        {
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();

            // Use an out of range value for stopDurationInSeconds toodemonstrate error
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, 99999);

            try
            {
                await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
            }

            catch (FabricException e)
            {
                Console.WriteLine("Caught {0}", e);
                Console.WriteLine("ErrorCode {0}", e.ErrorCode);
                // Output:
                // Caught System.Fabric.FabricException: System.Runtime.InteropServices.COMException (-2147017629)
                // StopDurationInSeconds is out of range ---> System.Runtime.InteropServices.COMException: Exception from HRESULT: 0x80071C63
                // << Parts of exception omitted>>
                //
                // ErrorCode InvalidDuration
            }
        }
```

<span data-ttu-id="c2083-163">**Пример 4** - hello ниже приведен пример hello сведения об ошибке, возвращаемое из hello узла перехода выполняется API hello операцию, запущенную методом hello узла перехода API принимается, когда происходит сбой позже, во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="c2083-163">**Sample 4** - hello following sample shows hello error information that will be returned from hello Node Transition Progress API when hello operation initiated by hello Node Transition API is accepted, but fails later while executing.</span></span>  <span data-ttu-id="c2083-164">В случае hello происходит сбой, поскольку hello API перехода узел пытается toostart узел, который не существует.</span><span class="sxs-lookup"><span data-stu-id="c2083-164">In hello case, it fails because hello Node Transition API attempts toostart a node that does not exist.</span></span>  <span data-ttu-id="c2083-165">Этот пример использует некоторые вспомогательные методы из первого примера hello.</span><span class="sxs-lookup"><span data-stu-id="c2083-165">This sample uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StartNodeWithNonexistentNodeAsync(FabricClient fc)
        {
            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = 12345;

            // Intentionally use a nonexistent node
            NodeStartDescription description = new NodeStartDescription(guid, "NonexistentNode", nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hello desired state is reached.  In this case, it will end up in hello Faulted state since hello node does not exist.
            // When StartNodeTransitionProgressAsync()'s returned progress object has a State if Faulted, inspect hello progress object's Result.Exception.HResult tooget hello error code.
            // In this case, it will be NodeNotFound.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Faulted).ConfigureAwait(false);
        }
```

[stopnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StopNodeAsync_System_String_System_Numerics_BigInteger_System_Fabric_CompletionMode_
[stopnodeps]: https://msdn.microsoft.com/library/mt125982.aspx
[startnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StartNodeAsync_System_String_System_Numerics_BigInteger_System_String_System_Int32_System_Fabric_CompletionMode_System_Threading_CancellationToken_
[startnodeps]: https://msdn.microsoft.com/library/mt163520.aspx
[nodequery]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient#System_Fabric_FabricClient_QueryClient_GetNodeListAsync_System_String_
[nodequeryps]: https://docs.microsoft.com/powershell/servicefabric/vlatest/Get-ServiceFabricNode?redirectedfrom=msdn
[snt]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_StartNodeTransitionAsync_System_Fabric_Description_NodeTransitionDescription_System_TimeSpan_System_Threading_CancellationToken_
[gntp]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_GetNodeTransitionProgressAsync_System_Guid_System_TimeSpan_System_Threading_CancellationToken_
