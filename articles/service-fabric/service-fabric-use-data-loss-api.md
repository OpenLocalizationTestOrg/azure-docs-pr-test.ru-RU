---
title: "aaaHow tooInvoke потери данных в службы структуры службы | Документы Microsoft"
description: "Описывает, каким образом toouse hello потери данных api"
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
ms.date: 09/19/2016
ms.author: lemai
redirect_url: /azure/service-fabric/service-fabric-testability-overview
ms.openlocfilehash: 014c7ebfd2c42d79a5fe1802ecc3fa0c1f26f9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinvoke-data-loss-on-services"></a><span data-ttu-id="a9358-103">Как tooInvoke потери данных в службах</span><span class="sxs-lookup"><span data-stu-id="a9358-103">How tooInvoke Data Loss on Services</span></span>
> [!WARNING]
> <span data-ttu-id="a9358-104">В этом документе описаны как toocause потери данных в службах и должны использоваться с осторожностью.</span><span class="sxs-lookup"><span data-stu-id="a9358-104">This document describe how toocause data loss in your services, and should be used with care.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="a9358-105">Введение</span><span class="sxs-lookup"><span data-stu-id="a9358-105">Introduction</span></span>
<span data-ttu-id="a9358-106">Можно вызвать потерю данных в секции службы Service Fabric, вызвав StartPartitionDataLossAsync().</span><span class="sxs-lookup"><span data-stu-id="a9358-106">You can invoke data loss on a partition of your Service Fabric Service by calling StartPartitionDataLossAsync().</span></span>  <span data-ttu-id="a9358-107">Этот api использует hello внесения ошибок и служб Analysis Service tooperform hello рабочих toocause данных потери условия.</span><span class="sxs-lookup"><span data-stu-id="a9358-107">This api uses hello Fault Injection and Analysis Service tooperform hello work toocause data loss conditions.</span></span>

## <a name="using-hello-fault-injection-and-analysis-service"></a><span data-ttu-id="a9358-108">С помощью hello внесения ошибок и служб Analysis Services</span><span class="sxs-lookup"><span data-stu-id="a9358-108">Using hello Fault Injection and Analysis Service</span></span>
<span data-ttu-id="a9358-109">Hello внесения ошибок и служб Analysis Services в настоящее время поддерживает следующие интерфейсы API в представленной ниже диаграмме hello hello.</span><span class="sxs-lookup"><span data-stu-id="a9358-109">hello Fault Injection and Analysis Service currently supports hello following APIs in hello chart below.</span></span>  <span data-ttu-id="a9358-110">Hello правой части диаграммы hello показаны hello соответствующий командлет PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9358-110">hello right side of hello chart shows hello corresponding PowerShell cmdlet.</span></span>  <span data-ttu-id="a9358-111">Дополнительные сведения для каждого из них см. в документации msdn toohello на каждый API.</span><span class="sxs-lookup"><span data-stu-id="a9358-111">Please refer toohello msdn documentation on each API for more information on each one.</span></span>

| <span data-ttu-id="a9358-112">API C#</span><span class="sxs-lookup"><span data-stu-id="a9358-112">C# API</span></span> | <span data-ttu-id="a9358-113">Командлет PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9358-113">PowerShell Cmdlet</span></span> |
| --- | ---:|
| <span data-ttu-id="a9358-114">[StartPartitionDataLossAsync][dl]</span><span class="sxs-lookup"><span data-stu-id="a9358-114">[StartPartitionDataLossAsync][dl]</span></span> |<span data-ttu-id="a9358-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span><span class="sxs-lookup"><span data-stu-id="a9358-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span></span> |
| <span data-ttu-id="a9358-116">[StartPartitionQuorumLossAsync][ql]</span><span class="sxs-lookup"><span data-stu-id="a9358-116">[StartPartitionQuorumLossAsync][ql]</span></span> |<span data-ttu-id="a9358-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span><span class="sxs-lookup"><span data-stu-id="a9358-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span></span> |
| <span data-ttu-id="a9358-118">[StartPartitionRestartAsync][rp]</span><span class="sxs-lookup"><span data-stu-id="a9358-118">[StartPartitionRestartAsync][rp]</span></span> |<span data-ttu-id="a9358-119">[Start-ServiceFabricPartitionRestart][psrp]</span><span class="sxs-lookup"><span data-stu-id="a9358-119">[Start-ServiceFabricPartitionRestart][psrp]</span></span> |

## <a name="conceptual-overview-of-running-a-command"></a><span data-ttu-id="a9358-120">Принцип выполнения команды</span><span class="sxs-lookup"><span data-stu-id="a9358-120">Conceptual Overview of Running a Command</span></span>
<span data-ttu-id="a9358-121">Здравствуйте, внесения ошибок и служб Analysis Services использует асинхронную модель, где начинается hello команды с одного API называется tooas hello «Start» API-интерфейса в этом документе, а затем проверяет hello ход выполнения этой команды с помощью API «GetProgress» до достижения терминала состояние, или пока вы отмените его.</span><span class="sxs-lookup"><span data-stu-id="a9358-121">hello Fault Injection and Analysis Service uses an asynchronous model where you start hello command with one API, referred tooas hello “Start” API in this document, then checks hello progress of this command using a “GetProgress” API until it has reached a terminal state, or until you cancel it.</span></span>
<span data-ttu-id="a9358-122">toostart команду, при вызове API «Start» hello hello соответствующий API.</span><span class="sxs-lookup"><span data-stu-id="a9358-122">toostart a command, call hello “Start” API for hello corresponding API.</span></span>  <span data-ttu-id="a9358-123">Этот API возвращает при hello внесения ошибок и служб Analysis Services принял запрос hello.</span><span class="sxs-lookup"><span data-stu-id="a9358-123">This API returns when hello Fault Injection and Analysis Service has accepted hello request.</span></span>  <span data-ttu-id="a9358-124">Однако это не указывает, насколько выполнена команда или было ли вообще начато ее выполнение.</span><span class="sxs-lookup"><span data-stu-id="a9358-124">However, it does not indicate how far a command has run, or even if it has started yet.</span></span>  <span data-ttu-id="a9358-125">В порядке toocheck ход выполнения команды вызовите hello «GetProgress» API, который соответствует вызван ранее API toohello «Start».</span><span class="sxs-lookup"><span data-stu-id="a9358-125">In order toocheck progress of a command, call hello “GetProgress” API that corresponds toohello “Start” API previously called.</span></span>  <span data-ttu-id="a9358-126">Hello «GetProgress» API-Интерфейс вернет объект, указывая hello текущее состояние команды hello внутри свойства его состояние.</span><span class="sxs-lookup"><span data-stu-id="a9358-126">hello “GetProgress” API will return an object indicating hello current status of hello command inside its State property.</span></span>  <span data-ttu-id="a9358-127">Команда выполняется неограниченное время, пока не будет выполнено одно из следующих условий.</span><span class="sxs-lookup"><span data-stu-id="a9358-127">A command runs indefinitely until:</span></span>

1. <span data-ttu-id="a9358-128">Она полностью выполнена.</span><span class="sxs-lookup"><span data-stu-id="a9358-128">It completes successfully.</span></span>  <span data-ttu-id="a9358-129">При вызове метода «GetProgress» на его таким образом, состояние объекта выполняется hello будет завершено.</span><span class="sxs-lookup"><span data-stu-id="a9358-129">If you call “GetProgress” on it in this case, hello progress object’s State will be Completed.</span></span>
2. <span data-ttu-id="a9358-130">При выполнении возникла неустранимая ошибка.</span><span class="sxs-lookup"><span data-stu-id="a9358-130">It encounters a fatal error.</span></span>  <span data-ttu-id="a9358-131">При вызове метода «GetProgress» на его таким образом, произошел сбой состояния объекта выполняется hello</span><span class="sxs-lookup"><span data-stu-id="a9358-131">If you call “GetProgress” on it in this case, hello progress object’s State will be Faulted</span></span>
3. <span data-ttu-id="a9358-132">Отменить его через hello [CancelTestCommandAsync] [ cancel] API, или [Stop ServiceFabricTestCommand] [ cancelps] командлета PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9358-132">You cancel it through hello [CancelTestCommandAsync][cancel] API, or [Stop-ServiceFabricTestCommand][cancelps] PowerShell cmdlet.</span></span>  <span data-ttu-id="a9358-133">При вызове метода «GetProgress» на его таким образом, hello объекта выполняется состояние будет отменено или ForceCancelled, в зависимости от аргумента toothat API.</span><span class="sxs-lookup"><span data-stu-id="a9358-133">If you call “GetProgress” on it in this case, hello progress object’s State will be either Cancelled or ForceCancelled, depending on an argument toothat API.</span></span>  <span data-ttu-id="a9358-134">В документации hello [CancelTestCommandAsync] [ cancel] для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="a9358-134">See hello documentation for [CancelTestCommandAsync][cancel] for more details.</span></span>

## <a name="details-of-running-a-command"></a><span data-ttu-id="a9358-135">Подробное описание выполнения команды</span><span class="sxs-lookup"><span data-stu-id="a9358-135">Details of Running a Command</span></span>
<span data-ttu-id="a9358-136">В порядке toostart команду вызовите hello запустить API с аргументами hello ожидается.</span><span class="sxs-lookup"><span data-stu-id="a9358-136">In order toostart a command, call hello Start API with hello expected arguments.</span></span>  <span data-ttu-id="a9358-137">У всех API Start есть аргумент Guid, называемый operationId.</span><span class="sxs-lookup"><span data-stu-id="a9358-137">All Start APIs have a Guid argument named operationId.</span></span>  <span data-ttu-id="a9358-138">Вы должны хранить список аргументов hello идентификатором операции, так как он используется tootrack ход выполнения этой команды.</span><span class="sxs-lookup"><span data-stu-id="a9358-138">You should keep track of hello operationId argument, since it is used tootrack progress of this command.</span></span>  <span data-ttu-id="a9358-139">Это должен быть передан в hello «GetProgress» API выполняется tootrack порядок hello команды.</span><span class="sxs-lookup"><span data-stu-id="a9358-139">This must be passed into hello “GetProgress” API in order tootrack progress of hello command.</span></span>  <span data-ttu-id="a9358-140">идентификатором Hello операции должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="a9358-140">hello operationId must be unique.</span></span>

<span data-ttu-id="a9358-141">После успешного вызова метода hello запустить API, hello, который должен вызываться в цикле GetProgress API до выполнения возврата hello объекта состояния завершения.</span><span class="sxs-lookup"><span data-stu-id="a9358-141">After successfully calling hello Start API, hello GetProgress API should be called in a loop until hello returned progress object’s State property is Completed.</span></span>  <span data-ttu-id="a9358-142">Все исключения [FabricTransientException][fte] и OperationCanceledException должны быть обработаны путем повтора операции.</span><span class="sxs-lookup"><span data-stu-id="a9358-142">All [FabricTransientException’s][fte] and OperationCanceledException’s should be retried.</span></span>
<span data-ttu-id="a9358-143">При достижении конечного состояния (завершено, Faulted или отменено) команда hello hello вернул свойство объекта выполняется результат будет иметь дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="a9358-143">When hello command has reached a terminal state (Completed, Faulted, or Cancelled), hello returned progress object’s Result property will have additional information.</span></span>  <span data-ttu-id="a9358-144">Если hello состояние завершения, Result.SelectedPartition.PartitionId будет содержать идентификатор секции hello, которая была выбрана.</span><span class="sxs-lookup"><span data-stu-id="a9358-144">If hello state is Completed, Result.SelectedPartition.PartitionId will contain hello partition id that was selected.</span></span>  <span data-ttu-id="a9358-145">Result.Exception будет иметь значение NULL.</span><span class="sxs-lookup"><span data-stu-id="a9358-145">Result.Exception will be null.</span></span>  <span data-ttu-id="a9358-146">Если hello состоянием является Faulted, Result.Exception будет иметь hello причина hello внесения ошибок и команда hello сбой службы Analysis.</span><span class="sxs-lookup"><span data-stu-id="a9358-146">If hello state is Faulted, Result.Exception will have hello reason hello Fault Injection and Analysis Service faulted hello command.</span></span>  <span data-ttu-id="a9358-147">Result.SelectedPartition.PartitionId будет иметь идентификатор секции hello, которая была выбрана.</span><span class="sxs-lookup"><span data-stu-id="a9358-147">Result.SelectedPartition.PartitionId will have hello partition id that was selected.</span></span>  <span data-ttu-id="a9358-148">В некоторых ситуациях hello команды может не продолжилось так toochoose секции.</span><span class="sxs-lookup"><span data-stu-id="a9358-148">In some situations, hello command may not have proceeded far enough toochoose a partition.</span></span>  <span data-ttu-id="a9358-149">В этом случае hello PartitionId будет 0.</span><span class="sxs-lookup"><span data-stu-id="a9358-149">In that case, hello PartitionId will be 0.</span></span>  <span data-ttu-id="a9358-150">При отмене состояния hello Result.Exception будет иметь значение null.</span><span class="sxs-lookup"><span data-stu-id="a9358-150">If hello state is Cancelled, Result.Exception will be null.</span></span>  <span data-ttu-id="a9358-151">Как hello случай Faulted Result.SelectedPartition.PartitionId будет иметь идентификатор hello секции, которая была выбрана, но если команда hello не была выполнена так, toodo таким образом, оно будет равно 0.</span><span class="sxs-lookup"><span data-stu-id="a9358-151">Like hello Faulted case, Result.SelectedPartition.PartitionId will have hello partition id that was chosen, but if hello command has not proceeded far enough toodo so, it will be 0.</span></span>  <span data-ttu-id="a9358-152">Также см. Образец toohello ниже.</span><span class="sxs-lookup"><span data-stu-id="a9358-152">Please also refer toohello sample below.</span></span>

<span data-ttu-id="a9358-153">Hello в образце кода ниже показано, как toostart затем проверить выполнение команды toocause потеря данных в определенный раздел.</span><span class="sxs-lookup"><span data-stu-id="a9358-153">hello sample code below shows how toostart then check progress on a command toocause data loss on a specific partition.</span></span>

```csharp
    static async Task PerformDataLossSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/MyService");

        // hello id of hello target partition inside hello target service
        Guid targetPartitionId = new Guid("00000000-0000-0000-0000-000002233445");

        PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(targetServiceName, targetPartitionId);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.        

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                // In a terminal state .Result.SelectedPartition.PartitionId will have hello chosen partition
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);
                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
                Console.WriteLine("Command '{0}' failed with '{1}'", operationId, progress.Result.Exception);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(5.0d)).ConfigureAwait(false);
        }
    }
```

<span data-ttu-id="a9358-154">Образец Hello ниже показано, как toouse hello PartitionSelector toochoose случайных секционирования из заданной службы.</span><span class="sxs-lookup"><span data-stu-id="a9358-154">hello sample below shows how toouse hello PartitionSelector toochoose a random partition of a specified service:</span></span>

```csharp
    static async Task PerformDataLossUseSelectorSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/SampleService ");

        // Use a PartitionSelector that will have hello Fault Injection and Analysis Service choose a random partition of “targetServiceName”
        PartitionSelector partitionSelector = PartitionSelector.RandomOf(targetServiceName);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }
            catch (Exception e)
            {
                Console.WriteLine("Unexpected exception '{0}'", e);
                throw;
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                Console.WriteLine("Printing progress.Result:");
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);

                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
                Console.WriteLine("Command '{0}' failed with '{1}', SelectedPartition {2}", operationId, progress.Result.Exception, progress.Result.SelectedPartition);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }
    }
```

## <a name="history-and-truncation"></a><span data-ttu-id="a9358-155">Журнал и усечение</span><span class="sxs-lookup"><span data-stu-id="a9358-155">History and Truncation</span></span>
<span data-ttu-id="a9358-156">После достижения конечного состояния команды свои метаданные сохранятся в hello внесения ошибок и служб Analysis Services для определенного времени, прежде чем он будет удален toosave пространства.</span><span class="sxs-lookup"><span data-stu-id="a9358-156">After a command has reached a terminal state, its metadata will remain in hello Fault Injection and Analysis Service for a certain time, before it will be removed toosave space.</span></span>  <span data-ttu-id="a9358-157">Если «GetProgress» вызывается с идентификатором hello операции команды, после он был удален, возвращается FabricException с ErrorCode KeyNotFound.</span><span class="sxs-lookup"><span data-stu-id="a9358-157">If “GetProgress” is called using hello operationId of a command after it has been removed, it will return a FabricException with an ErrorCode of KeyNotFound.</span></span>

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
