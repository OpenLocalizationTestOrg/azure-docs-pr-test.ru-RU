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
# <a name="replacing-hello-start-node-and-stop-node-apis-with-hello-node-transition-api"></a>Заменив hello узла перехода API hello начального узла и остановка узла API-интерфейсы

## <a name="what-do-hello-stop-node-and-start-node-apis-do"></a>Что hello остановить узел и запуск узла интерфейсы API?

Остановить узел API Hello (управляемые: [StopNodeAsync()][stopnode], PowerShell: [Stop ServiceFabricNode][stopnodeps]) останавливает узел Service Fabric.  Узел Service Fabric — процесс, виртуальная машина или машины — hello виртуальная машина или машины по-прежнему будут выполняться.  Hello оставшейся части документа hello «узла» будет означать узел Service Fabric.  Остановка узла помещает его в *остановлена* состоянии, которое он не является членом кластера hello невозможно разместить службы, что позволяет имитировать *работу* узла.  Это полезно для добавления ошибок в системе tootest hello приложения.  Hello запустить узел API (управляемые: [StartNodeAsync()][startnode], PowerShell: [начала ServiceFabricNode][startnodeps]]) отменяет hello API остановить узел  вызывает hello узел задней tooa нормальное состояние.

## <a name="why-are-we-replacing-these"></a>Зачем их заменять?

Как было сказано выше, *остановлена* Service Fabric узел является узлом намеренно целевые с помощью hello API остановить узел.  Объект *работу* узел является узлом, не работает для какой-либо причине (например hello виртуальная машина или машины — off).  С hello остановить узел API системы hello не предоставляет сведения toodifferentiate между *остановлена* узлов и *работу* узлов.

Кроме того, некоторые сообщения об ошибках, возвращаемые этими API-интерфейсами, недостаточно содержательны.  Например, вызов hello остановить узел API на объект уже *остановлена* узел вернет ошибку hello *InvalidAddress*.  Это поведение можно оптимизировать.

Кроме того пока hello, запустить узел API вызывается hello время, в течение которого узел остановлен на «бесконечность».  Выяснилось, что это может привести к проблемам и возникновению ошибок.  Например описанных выше проблем, где пользователь вызывается hello остановить узел API на узле и затем забыли о нем.  Позже, было ясно, если узел hello был *работу* или *остановлена*.


## <a name="introducing-hello-node-transition-apis"></a>Знакомство с приложением hello API-интерфейсы узла перехода

Описанные выше проблемы можно решить с помощью нашего нового набора API-интерфейсов.  новый узел перехода API Hello (управляемые: [StartNodeTransitionAsync()][snt]) может быть используется tootransition tooa узел Service Fabric *остановлена* состояния или tootransition его из *остановлена* состояние tooa обычного состояния.  Обратите внимание, что hello «Start» в качестве имени hello hello API не ссылается toostarting узла.  Он ссылается toobeginning асинхронной операции, система hello будет выполняться tootransition hello узел tooeither *остановлена* или рабочем состоянии.

**Использование**

Если hello узла перехода API не вызывает исключение при вызове, система hello принял hello асинхронной операции и выполнит его.  Успешного вызова не означает, что еще завершена операция hello.  tooget сведения о текущем состоянии hello операции hello, hello вызов API выполняется переход узел (управляемые: [GetNodeTransitionProgressAsync()][gntp]) с идентификатором guid hello, используемых при вызове узла API переход для этой операции.  Hello узла перехода выполняется API возвращает объект NodeTransitionProgress.  Состояние объекта указывает текущее состояние операции hello hello.  Если hello состояние «выполняется», выполняется операция hello.  Если она будет завершена, операция hello завершена без ошибок.  Если он находится в состоянии сбоя, произошла ошибка при выполнении операции hello.  свойства Result Hello свойство будет указывать, какие hello выдавать исключение.  В разделе https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate Дополнительные сведения о свойство State hello и hello «Использование образца» приведены ниже в разделе примеров кода.


**Разграничения остановлена узел и узел вниз** Если узел является *остановлена* с помощью hello API узел перехода, выходные данные запроса узел hello (управляемые: [GetNodeListAsync()] [ nodequery], PowerShell: [Get ServiceFabricNode][nodequeryps]) будет показывать, что этот узел есть *IsStopped* свойство значение true.  Обратите внимание на это поведение отличается от значение hello hello *NodeStatus* свойство, которое укажет *работу*.  Если hello *NodeStatus* свойство имеет значение *работу*, но *IsStopped* имеет значение false, то hello узел не был остановлен, с помощью API перехода узла hello и является  *Вниз* из-за какой-либо другой причине.  Если hello *IsStopped* свойство имеет значение true, а hello *NodeStatus* свойство *работу*, то остановлена с помощью hello API узла перехода.

Запуск *остановлена* узла, используя hello узла перехода API вернет его toofunction как обычный членом кластера hello еще раз.  Hello выходные данные запроса узла hello API будет показывать *IsStopped* false, и *NodeStatus* как элемент, не являющийся вниз (например вверх).


**Ограниченные длительность** при использовании узла перехода API hello toostop узла, один из hello необходимые параметры *stopNodeDurationInSeconds*, представляет hello количество времени в секундах tookeep hello узел  *Остановить*.  Это значение должно быть в допустимый диапазон, имеющий 600 минимум и максимум 14400 hello.  После истечения этого времени, узел hello сам в показатель состояния автоматически перезагрузится.  См. пример использования tooSample 1 ниже.

> [!WARNING]
> Использовать API-интерфейсы узла перехода и hello узла остановить и запустить узел API.  Hello рекомендуется слишком использовать только hello API узла перехода.  > Если узел уже была остановлена при помощи hello остановить узел API, она должна быть запущена посредством hello API запустить узел сначала перед использованием hello > API-интерфейсы узла перехода.

> [!WARNING]
> Несколько интерфейсов API перехода узла вызовы нельзя сделать на hello одним узлом в параллельном режиме.  В таком случае будет hello API перехода узла > throw FabricException со значением свойства ErrorCode NodeTransitionInProgress.  После перехода узла на определенном узле имеет > была запущена, нужно подождать, пока операция hello достигнет конечного состояния (завершено, Faulted или ForceCancelled) перед запуском > new переход на hello же узла.  Параллельные вызовы перехода на разных узлах разрешены.


#### <a name="sample-usage"></a>Пример использования


**Пример 1** -hello следующие образцы использования hello toostop API узла перехода узла.

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

**Пример 2** - hello после запуска образца *остановлена* узла.  Она использует некоторые вспомогательные методы из первого примера hello.

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

**Пример 3** - hello ниже приведен пример неправильное использование.  Неверное использование этой поскольку hello *stopDurationInSeconds* он предоставляет больше, чем hello, допустимый диапазон.  Поскольку StartNodeTransitionAsync() завершится ошибкой при возникновении неустранимой ошибки, hello операции не был принят, и не следует вызывать API hello хода выполнения.  Этот пример использует некоторые вспомогательные методы из первого примера hello.

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

**Пример 4** - hello ниже приведен пример hello сведения об ошибке, возвращаемое из hello узла перехода выполняется API hello операцию, запущенную методом hello узла перехода API принимается, когда происходит сбой позже, во время выполнения.  В случае hello происходит сбой, поскольку hello API перехода узел пытается toostart узел, который не существует.  Этот пример использует некоторые вспомогательные методы из первого примера hello.

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
