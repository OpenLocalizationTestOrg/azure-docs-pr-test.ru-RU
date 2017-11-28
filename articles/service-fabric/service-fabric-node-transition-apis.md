---
title: "Запуск и остановка узлов кластера для проверки микрослужб Azure | Документация Майкрософт"
description: "Узнайте, как использовать внесение ошибок для тестирования приложения Service Fabric, запуская и останавливая узлы кластера."
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
ms.openlocfilehash: 850fbc0c74811ec942292da64064dec867cd1b9e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="replacing-the-start-node-and-stop-node-apis-with-the-node-transition-api"></a><span data-ttu-id="697c4-103">Замена API-интерфейсов запуска и остановки узла API-интерфейсом перехода узла</span><span class="sxs-lookup"><span data-stu-id="697c4-103">Replacing the Start Node and Stop node APIs with the Node Transition API</span></span>

## <a name="what-do-the-stop-node-and-start-node-apis-do"></a><span data-ttu-id="697c4-104">Для чего нужны API-интерфейсы запуска и остановки узла?</span><span class="sxs-lookup"><span data-stu-id="697c4-104">What do the Stop Node and Start Node APIs do?</span></span>

<span data-ttu-id="697c4-105">API остановки узла (управляемый: [StopNodeAsync()][stopnode], PowerShell: [Stop-ServiceFabricNode][stopnodeps]) останавливает узел Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="697c4-105">The Stop Node API (managed: [StopNodeAsync()][stopnode], PowerShell: [Stop-ServiceFabricNode][stopnodeps]) stops a Service Fabric node.</span></span>  <span data-ttu-id="697c4-106">Узел Service Fabric — это процесс, а не компьютер или виртуальная машина, поэтому компьютер или виртуальная машина будут продолжать работу.</span><span class="sxs-lookup"><span data-stu-id="697c4-106">A Service Fabric node is process, not a VM or machine – the VM or machine will still be running.</span></span>  <span data-ttu-id="697c4-107">В этом документе далее термин "узел" означает узел Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="697c4-107">For the rest of the document "node" will mean Service Fabric node.</span></span>  <span data-ttu-id="697c4-108">При остановке узел помещается в состояние *Остановлен*, при котором он не является элементом кластера и не может размещать службы, имитируя *отключенный* узел.</span><span class="sxs-lookup"><span data-stu-id="697c4-108">Stopping a node puts it into a *stopped* state where it is not a member of the cluster and cannot host services, thus simulating a *down* node.</span></span>  <span data-ttu-id="697c4-109">Это полезно для внесения ошибок в систему при тестировании приложения.</span><span class="sxs-lookup"><span data-stu-id="697c4-109">This is useful for injecting faults into the system to test your application.</span></span>  <span data-ttu-id="697c4-110">API запуска узла (управляемый: [StartNodeAsync()][startnode], PowerShell: [Start-ServiceFabricNode][startnodeps]]) обращает API остановки узла, возвращая узел в обычное состояние.</span><span class="sxs-lookup"><span data-stu-id="697c4-110">The Start Node API (managed: [StartNodeAsync()][startnode], PowerShell: [Start-ServiceFabricNode][startnodeps]]) reverses the Stop Node API,  which brings the node back to a normal state.</span></span>

## <a name="why-are-we-replacing-these"></a><span data-ttu-id="697c4-111">Зачем их заменять?</span><span class="sxs-lookup"><span data-stu-id="697c4-111">Why are we replacing these?</span></span>

<span data-ttu-id="697c4-112">Как было описано ранее, *остановленный* узел Service Fabric — это узел, к которому намеренно применен API остановки узла.</span><span class="sxs-lookup"><span data-stu-id="697c4-112">As described earlier, a *stopped* Service Fabric node is a node intentionally targeted using the Stop Node API.</span></span>  <span data-ttu-id="697c4-113">*Отключенный*  узел — это узел, который не работает по какой-либо другой причине (например, из-за отключения компьютера или виртуальной машины).</span><span class="sxs-lookup"><span data-stu-id="697c4-113">A *down* node is a node that is down for any other reason (e.g. the VM or machine is off).</span></span>  <span data-ttu-id="697c4-114">При использовании API остановки узла в системе не отображаются сведения, с помощью которых можно различить *остановленные* и *отключенные* узлы.</span><span class="sxs-lookup"><span data-stu-id="697c4-114">With the Stop Node API, the system does not expose information to differentiate between *stopped* nodes and *down* nodes.</span></span>

<span data-ttu-id="697c4-115">Кроме того, некоторые сообщения об ошибках, возвращаемые этими API-интерфейсами, недостаточно содержательны.</span><span class="sxs-lookup"><span data-stu-id="697c4-115">In addition, some errors returned by these APIs are not as descriptive as they could be.</span></span>  <span data-ttu-id="697c4-116">Например, при вызове API остановки узла на уже *остановленном* узле возвращается ошибка *InvalidAddress*.</span><span class="sxs-lookup"><span data-stu-id="697c4-116">For example, invoking the Stop Node API on an already *stopped* node will return the error *InvalidAddress*.</span></span>  <span data-ttu-id="697c4-117">Это поведение можно оптимизировать.</span><span class="sxs-lookup"><span data-stu-id="697c4-117">This experience could be improved.</span></span>

<span data-ttu-id="697c4-118">Кроме того, работа узла останавливается на неограниченное время до вызова API запуска узла.</span><span class="sxs-lookup"><span data-stu-id="697c4-118">Also, the duration a node is stopped for is “infinite” until the Start Node API is invoked.</span></span>  <span data-ttu-id="697c4-119">Выяснилось, что это может привести к проблемам и возникновению ошибок.</span><span class="sxs-lookup"><span data-stu-id="697c4-119">We’ve found this can cause problems and may be error-prone.</span></span>  <span data-ttu-id="697c4-120">Например, мы сталкивались с проблемами, когда пользователь вызывал API остановки узла, а потом забывал об этом.</span><span class="sxs-lookup"><span data-stu-id="697c4-120">For example, we’ve seen problems where a user invoked the Stop Node API on a node and then forgot about it.</span></span>  <span data-ttu-id="697c4-121">Позже было невозможно установить, что произошло с узлом: был ли он *отключен* или *остановлен*.</span><span class="sxs-lookup"><span data-stu-id="697c4-121">Later, it was unclear if the node was *down* or *stopped*.</span></span>


## <a name="introducing-the-node-transition-apis"></a><span data-ttu-id="697c4-122">Знакомство с API-интерфейсами перехода узла</span><span class="sxs-lookup"><span data-stu-id="697c4-122">Introducing the Node Transition APIs</span></span>

<span data-ttu-id="697c4-123">Описанные выше проблемы можно решить с помощью нашего нового набора API-интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="697c4-123">We’ve addressed these issues above in a new set of APIs.</span></span>  <span data-ttu-id="697c4-124">Новый API перехода узла (управляемый: [StartNodeTransitionAsync()][snt]) может использоваться для перехода узла Service Fabric в *остановленное* состояние или для перехода из *остановленного* состояния в нормальное рабочее состояние.</span><span class="sxs-lookup"><span data-stu-id="697c4-124">The new Node Transition API (managed: [StartNodeTransitionAsync()][snt]) may be used to transition a Service Fabric node to a *stopped* state, or to transition it from a *stopped* state to a normal up state.</span></span>  <span data-ttu-id="697c4-125">Обратите внимание на то, что "запуск" в названии API не означает собственно запуск узла.</span><span class="sxs-lookup"><span data-stu-id="697c4-125">Please note that the “Start” in the name of the API does not refer to starting a node.</span></span>  <span data-ttu-id="697c4-126">Это означает начало асинхронной операции, которую выполняет система для перевода узла в *остановленное* или рабочее состояние.</span><span class="sxs-lookup"><span data-stu-id="697c4-126">It refers to beginning an asynchronous operation that the system will execute to transition the node to either *stopped* or started state.</span></span>

<span data-ttu-id="697c4-127">**Использование**</span><span class="sxs-lookup"><span data-stu-id="697c4-127">**Usage**</span></span>

<span data-ttu-id="697c4-128">Если при вызове API перехода узла не возвращается исключение, это означает, что система приняла асинхронную операцию и собирается ее выполнить.</span><span class="sxs-lookup"><span data-stu-id="697c4-128">If the Node Transition API does not throw an exception when invoked, then the system has accepted the asynchronous operation, and will execute it.</span></span>  <span data-ttu-id="697c4-129">Успешный вызов еще не означает, что операция завершена.</span><span class="sxs-lookup"><span data-stu-id="697c4-129">A successful call does not imply the operation is finished yet.</span></span>  <span data-ttu-id="697c4-130">Для получения сведений о текущем состоянии операции вызовите API хода выполнения перехода узла (управляемый: [GetNodeTransitionProgressAsync()][gntp]) с помощью идентификатора GUID, используемого при вызове API перехода узла для этой операции.</span><span class="sxs-lookup"><span data-stu-id="697c4-130">To get information about the current state of the operation, call the Node Transition Progress API (managed: [GetNodeTransitionProgressAsync()][gntp]) with the guid used when invoking Node Transition API for this operation.</span></span>  <span data-ttu-id="697c4-131">API хода выполнения перехода узла возвращает объект NodeTransitionProgress.</span><span class="sxs-lookup"><span data-stu-id="697c4-131">The Node Transition Progress API returns an NodeTransitionProgress object.</span></span>  <span data-ttu-id="697c4-132">Это свойство State объекта указывает текущее состояние операции.</span><span class="sxs-lookup"><span data-stu-id="697c4-132">This object’s State property specifies the current state of the operation.</span></span>  <span data-ttu-id="697c4-133">Если свойство имеет значение Running, операция выполняется.</span><span class="sxs-lookup"><span data-stu-id="697c4-133">If the state is “Running” then the operation is executing.</span></span>  <span data-ttu-id="697c4-134">Значение Completed указывает на то, что операция завершена без ошибок.</span><span class="sxs-lookup"><span data-stu-id="697c4-134">If it is Completed, the operation finished without error.</span></span>  <span data-ttu-id="697c4-135">А значение Faulted — на ошибку, возникшую при выполнении операции.</span><span class="sxs-lookup"><span data-stu-id="697c4-135">If it is Faulted, there was a problem executing the operation.</span></span>  <span data-ttu-id="697c4-136">Свойство Exception в свойстве Result указывает на наличие проблемы.</span><span class="sxs-lookup"><span data-stu-id="697c4-136">The Result property’s Exception property will indicate what the issue was.</span></span>  <span data-ttu-id="697c4-137">Дополнительные сведения о свойстве State см. на странице https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate. Примеры кода приведены в разделе "Пример использования" далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="697c4-137">See https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate for more information about the State property, and the “Sample Usage” section below for code examples.</span></span>


<span data-ttu-id="697c4-138">**Определение остановленного и отключенного узла.** Если узел *остановлен* с помощью API перехода узла, в выходных данных запроса узла (управляемый: [GetNodeListAsync()][nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) свойство *IsStopped* этого узла будет иметь значение true.</span><span class="sxs-lookup"><span data-stu-id="697c4-138">**Differentiating between a stopped node and a down node** If a node is *stopped* using the Node Transition API, the output of a node query (managed: [GetNodeListAsync()][nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) will show that this node has an *IsStopped* property value of true.</span></span>  <span data-ttu-id="697c4-139">Обратите внимание, что оно отличается от значения свойства *NodeStatus*, которое равно *Down*.</span><span class="sxs-lookup"><span data-stu-id="697c4-139">Note this is different from the value of the *NodeStatus* property, which will say *Down*.</span></span>  <span data-ttu-id="697c4-140">Если свойство *NodeStatus* имеет значение *Down*, но свойство *IsStopped* имеет значение false, это значит, что узел не остановлен с помощью API перехода узла, а *отключен* по какой-то другой причине.</span><span class="sxs-lookup"><span data-stu-id="697c4-140">If the *NodeStatus* property has a value of *Down*, but *IsStopped* is false, then the node was not stopped using the Node Transition API, and is *Down* due some other reason.</span></span>  <span data-ttu-id="697c4-141">Если свойство *IsStopped* имеет значение true, а свойство *NodeStatus* — значение *Down*, это значит, что узел остановлен с помощью API перехода узла.</span><span class="sxs-lookup"><span data-stu-id="697c4-141">If the *IsStopped* property is true, and the *NodeStatus* property is *Down*, then it was stopped using the Node Transition API.</span></span>

<span data-ttu-id="697c4-142">Запуск *остановленного* узла с помощью API перехода узла вернет его к работе в качестве обычного элемента кластера.</span><span class="sxs-lookup"><span data-stu-id="697c4-142">Starting a *stopped* node using the Node Transition API will return it to function as a normal member of the cluster again.</span></span>  <span data-ttu-id="697c4-143">В выходных данных API запроса узла для свойства *IsStopped* будет отображаться значение false, а для свойства *NodeStatus* — значение, отличное от Down (например, Up).</span><span class="sxs-lookup"><span data-stu-id="697c4-143">The output of the node query API will show *IsStopped* as false, and *NodeStatus* as something that is not Down (e.g. Up).</span></span>


<span data-ttu-id="697c4-144">**Ограниченное время.** При использовании API перехода узла для остановки узла один из обязательных параметров, *stopNodeDurationInSeconds*, отображает время в секундах, в течение которого узел будет оставаться *остановленным*.</span><span class="sxs-lookup"><span data-stu-id="697c4-144">**Limited Duration** When using the Node Transition API to stop a node, one of the required parameters, *stopNodeDurationInSeconds*, represents the amount of time in seconds to keep the node *stopped*.</span></span>  <span data-ttu-id="697c4-145">Это должно быть значение в разрешенном диапазоне — не менее 600 и не более 14 400.</span><span class="sxs-lookup"><span data-stu-id="697c4-145">This value must be in the allowed range, which has a minimum of 600, and a maximum of 14400.</span></span>  <span data-ttu-id="697c4-146">По истечении этого времени узел автоматически перезапустится и перейдет в рабочее состояние (Up).</span><span class="sxs-lookup"><span data-stu-id="697c4-146">After this time expires, the node will restart itself into Up state automatically.</span></span>  <span data-ttu-id="697c4-147">Использование этого API показано в примере 1 ниже.</span><span class="sxs-lookup"><span data-stu-id="697c4-147">Refer to Sample 1 below for an example of usage.</span></span>

> [!WARNING]
> <span data-ttu-id="697c4-148">Не используйте одновременно API-интерфейсы перехода узла и API-интерфейсы запуска и остановки узла.</span><span class="sxs-lookup"><span data-stu-id="697c4-148">Avoid mixing Node Transition APIs and the Stop Node and Start Node APIs.</span></span>  <span data-ttu-id="697c4-149">Рекомендуем использовать только API перехода узла.</span><span class="sxs-lookup"><span data-stu-id="697c4-149">The recommendation is to  use the Node Transition API only.</span></span>  <span data-ttu-id="697c4-150">Если узел уже остановлен с помощью API остановки узла, его следует запустить с помощью API запуска узла и только потом использовать API перехода узла.</span><span class="sxs-lookup"><span data-stu-id="697c4-150">> If a node has been already been stopped using the Stop Node API, it should be started using the Start Node API first before using the > Node Transition APIs.</span></span>

> [!WARNING]
> <span data-ttu-id="697c4-151">На одном узле нельзя параллельно выполнить несколько вызовов API перехода узла.</span><span class="sxs-lookup"><span data-stu-id="697c4-151">Multiple Node Transition APIs calls cannot be made on the same node in parallel.</span></span>  <span data-ttu-id="697c4-152">В таком случае API перехода узла выдаст исключение FabricException со значением свойства ErrorCode, равным NodeTransitionInProgress.</span><span class="sxs-lookup"><span data-stu-id="697c4-152">In such a situation, the Node Transition API will    > throw a FabricException with an ErrorCode property value of NodeTransitionInProgress.</span></span>  <span data-ttu-id="697c4-153">После начала перехода на определенном узле следует подождать, пока операция достигнет конечного состояния (Completed, Faulted или ForceCancelled), прежде чем начинать новый переход на том же узле.</span><span class="sxs-lookup"><span data-stu-id="697c4-153">Once a node transition on a specific node has  > been started, you should wait until the operation reaches a terminal state (Completed, Faulted, or ForceCancelled) before starting a  > new transition on the same node.</span></span>  <span data-ttu-id="697c4-154">Параллельные вызовы перехода на разных узлах разрешены.</span><span class="sxs-lookup"><span data-stu-id="697c4-154">Parallel node transition calls on different nodes are allowed.</span></span>


#### <a name="sample-usage"></a><span data-ttu-id="697c4-155">Пример использования</span><span class="sxs-lookup"><span data-stu-id="697c4-155">Sample Usage</span></span>


<span data-ttu-id="697c4-156">**Пример 1.** В этом примере API перехода узла используется для остановки узла.</span><span class="sxs-lookup"><span data-stu-id="697c4-156">**Sample 1** - The following sample uses the Node Transition API to stop a node.</span></span>

```csharp
        // Helper function to get information about a node
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
                        // Inspect the progress object's Result.Exception.HResult to get the error code.
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
            // Uses the GetNodeListAsync() API to get information about the target node
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
                    // Invoke StartNodeTransitionAsync with the NodeStopDescription from above, which will stop the target node.  Retry transient errors.
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

<span data-ttu-id="697c4-157">**Пример 2.** В этом примере запускается *остановленный* узел.</span><span class="sxs-lookup"><span data-stu-id="697c4-157">**Sample 2** - The following sample starts a *stopped* node.</span></span>  <span data-ttu-id="697c4-158">Здесь используются некоторые вспомогательные методы из первого примера.</span><span class="sxs-lookup"><span data-stu-id="697c4-158">It uses some helper methods from the first sample.</span></span>

```csharp
        static async Task StartNodeAsync(FabricClient fc, string nodeName)
        {
            // Uses the GetNodeListAsync() API to get information about the target node
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
                    // Invoke StartNodeTransitionAsync with the NodeStartDescription from above, which will start the target stopped node.  Retry transient errors.
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

<span data-ttu-id="697c4-159">**Пример 3.** В этом примере показано неправильное использование.</span><span class="sxs-lookup"><span data-stu-id="697c4-159">**Sample 3** - The following sample shows incorrect usage.</span></span>  <span data-ttu-id="697c4-160">Ошибка заключается в том, что для свойства *stopDurationInSeconds* указано значение за пределами допустимого диапазона.</span><span class="sxs-lookup"><span data-stu-id="697c4-160">This usage is incorrect because the *stopDurationInSeconds* it provides is greater than the allowed range.</span></span>  <span data-ttu-id="697c4-161">Так как API StartNodeTransitionAsync() прекращает работу с неустранимой ошибкой, операция отклоняется, и API хода выполнения невозможно вызвать.</span><span class="sxs-lookup"><span data-stu-id="697c4-161">Since StartNodeTransitionAsync() will fail with a fatal error, the operation was not accepted, and the progress API should not be called.</span></span>  <span data-ttu-id="697c4-162">В этом примере используются некоторые вспомогательные методы из первого примера.</span><span class="sxs-lookup"><span data-stu-id="697c4-162">This sample uses some helper methods from the first sample.</span></span>

```csharp
        static async Task StopNodeWithOutOfRangeDurationAsync(FabricClient fc, string nodeName)
        {
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();

            // Use an out of range value for stopDurationInSeconds to demonstrate error
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

<span data-ttu-id="697c4-163">**Пример 4.** В этом примере показаны сведения об ошибке, возвращаемые из API хода выполнения перехода узла, когда операция, запущенная с помощью API перехода узла, принимается, но затем при ее выполнении происходит сбой.</span><span class="sxs-lookup"><span data-stu-id="697c4-163">**Sample 4** - The following sample shows the error information that will be returned from the Node Transition Progress API when the operation initiated by the Node Transition API is accepted, but fails later while executing.</span></span>  <span data-ttu-id="697c4-164">В этом случае сбой происходит из-за того, что API перехода узла пытается запустить несуществующий узел.</span><span class="sxs-lookup"><span data-stu-id="697c4-164">In the case, it fails because the Node Transition API attempts to start a node that does not exist.</span></span>  <span data-ttu-id="697c4-165">В этом примере используются некоторые вспомогательные методы из первого примера.</span><span class="sxs-lookup"><span data-stu-id="697c4-165">This sample uses some helper methods from the first sample.</span></span>

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
                    // Invoke StartNodeTransitionAsync with the NodeStartDescription from above, which will start the target stopped node.  Retry transient errors.
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

            // Now call StartNodeTransitionProgressAsync() until the desired state is reached.  In this case, it will end up in the Faulted state since the node does not exist.
            // When StartNodeTransitionProgressAsync()'s returned progress object has a State if Faulted, inspect the progress object's Result.Exception.HResult to get the error code.
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
