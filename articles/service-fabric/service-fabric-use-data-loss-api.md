---
title: "Как вызвать потерю данных в службах Service Fabric | Документация Майкрософт"
description: "Описывается, как использовать API потери данных."
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
ms.openlocfilehash: 0c4791e56f84d0df38783a13c8d8c564fd25f55f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-invoke-data-loss-on-services"></a><span data-ttu-id="a3fbc-103">Как вызвать потерю данных в службах</span><span class="sxs-lookup"><span data-stu-id="a3fbc-103">How to Invoke Data Loss on Services</span></span>
> [!WARNING]
> <span data-ttu-id="a3fbc-104">В этом документе описывается, как вызвать потерю данных в службах, поэтому он должен использоваться с осторожностью.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-104">This document describe how to cause data loss in your services, and should be used with care.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="a3fbc-105">Введение</span><span class="sxs-lookup"><span data-stu-id="a3fbc-105">Introduction</span></span>
<span data-ttu-id="a3fbc-106">Можно вызвать потерю данных в секции службы Service Fabric, вызвав StartPartitionDataLossAsync().</span><span class="sxs-lookup"><span data-stu-id="a3fbc-106">You can invoke data loss on a partition of your Service Fabric Service by calling StartPartitionDataLossAsync().</span></span>  <span data-ttu-id="a3fbc-107">Этот API использует службу внесения ошибок и анализа для выполнения работы, чтобы создать условия для потери данных.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-107">This api uses the Fault Injection and Analysis Service to perform the work to cause data loss conditions.</span></span>

## <a name="using-the-fault-injection-and-analysis-service"></a><span data-ttu-id="a3fbc-108">Использование службы внесения ошибок и анализа</span><span class="sxs-lookup"><span data-stu-id="a3fbc-108">Using the Fault Injection and Analysis Service</span></span>
<span data-ttu-id="a3fbc-109">В настоящее время служба внесения ошибок и анализа поддерживает следующие интерфейсы API, перечисленные в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-109">The Fault Injection and Analysis Service currently supports the following APIs in the chart below.</span></span>  <span data-ttu-id="a3fbc-110">В правой части диаграммы приведен соответствующий командлет PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-110">The right side of the chart shows the corresponding PowerShell cmdlet.</span></span>  <span data-ttu-id="a3fbc-111">Чтобы получить дополнительные сведения о каждом API, обратитесь к соответствующей документации на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-111">Please refer to the msdn documentation on each API for more information on each one.</span></span>

| <span data-ttu-id="a3fbc-112">API C#</span><span class="sxs-lookup"><span data-stu-id="a3fbc-112">C# API</span></span> | <span data-ttu-id="a3fbc-113">Командлет PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3fbc-113">PowerShell Cmdlet</span></span> |
| --- | ---:|
| <span data-ttu-id="a3fbc-114">[StartPartitionDataLossAsync][dl]</span><span class="sxs-lookup"><span data-stu-id="a3fbc-114">[StartPartitionDataLossAsync][dl]</span></span> |<span data-ttu-id="a3fbc-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span><span class="sxs-lookup"><span data-stu-id="a3fbc-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span></span> |
| <span data-ttu-id="a3fbc-116">[StartPartitionQuorumLossAsync][ql]</span><span class="sxs-lookup"><span data-stu-id="a3fbc-116">[StartPartitionQuorumLossAsync][ql]</span></span> |<span data-ttu-id="a3fbc-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span><span class="sxs-lookup"><span data-stu-id="a3fbc-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span></span> |
| <span data-ttu-id="a3fbc-118">[StartPartitionRestartAsync][rp]</span><span class="sxs-lookup"><span data-stu-id="a3fbc-118">[StartPartitionRestartAsync][rp]</span></span> |<span data-ttu-id="a3fbc-119">[Start-ServiceFabricPartitionRestart][psrp]</span><span class="sxs-lookup"><span data-stu-id="a3fbc-119">[Start-ServiceFabricPartitionRestart][psrp]</span></span> |

## <a name="conceptual-overview-of-running-a-command"></a><span data-ttu-id="a3fbc-120">Принцип выполнения команды</span><span class="sxs-lookup"><span data-stu-id="a3fbc-120">Conceptual Overview of Running a Command</span></span>
<span data-ttu-id="a3fbc-121">Служба внесения ошибок и анализа использует асинхронную модель, в которой вы начинаете с выполнения команды в одном API (т. н. API Start в этом документе), а затем проверяете ход выполнения этой команды с помощью API GetProgress, пока она не достигнет конечного состояния или не будет отменена вами.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-121">The Fault Injection and Analysis Service uses an asynchronous model where you start the command with one API, referred to as the “Start” API in this document, then checks the progress of this command using a “GetProgress” API until it has reached a terminal state, or until you cancel it.</span></span>
<span data-ttu-id="a3fbc-122">Чтобы выполнить команду, вызовите API Start для соответствующего API.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-122">To start a command, call the “Start” API for the corresponding API.</span></span>  <span data-ttu-id="a3fbc-123">Этот API возвращается, если служба внесения ошибок и анализа приняла запрос.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-123">This API returns when the Fault Injection and Analysis Service has accepted the request.</span></span>  <span data-ttu-id="a3fbc-124">Однако это не указывает, насколько выполнена команда или было ли вообще начато ее выполнение.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-124">However, it does not indicate how far a command has run, or even if it has started yet.</span></span>  <span data-ttu-id="a3fbc-125">Чтобы проверить ход выполнения команды, вызовите API GetProgress, который соответствует ранее вызванному API Start.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-125">In order to check progress of a command, call the “GetProgress” API that corresponds to the “Start” API previously called.</span></span>  <span data-ttu-id="a3fbc-126">API GetProgress вернет объект, указывающий в своем свойстве State текущее состояние команды.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-126">The “GetProgress” API will return an object indicating the current status of the command inside its State property.</span></span>  <span data-ttu-id="a3fbc-127">Команда выполняется неограниченное время, пока не будет выполнено одно из следующих условий.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-127">A command runs indefinitely until:</span></span>

1. <span data-ttu-id="a3fbc-128">Она полностью выполнена.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-128">It completes successfully.</span></span>  <span data-ttu-id="a3fbc-129">При вызове GetProgress в этом случае свойство State объекта хода выполнения будет иметь значение Completed.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-129">If you call “GetProgress” on it in this case, the progress object’s State will be Completed.</span></span>
2. <span data-ttu-id="a3fbc-130">При выполнении возникла неустранимая ошибка.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-130">It encounters a fatal error.</span></span>  <span data-ttu-id="a3fbc-131">При вызове GetProgress в этом случае свойство State объекта хода выполнения будет иметь значение Faulted.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-131">If you call “GetProgress” on it in this case, the progress object’s State will be Faulted</span></span>
3. <span data-ttu-id="a3fbc-132">Вы отменили команду с помощью API [CancelTestCommandAsync][cancel] или командлета PowerShell [Stop-ServiceFabricTestCommand][cancelps].</span><span class="sxs-lookup"><span data-stu-id="a3fbc-132">You cancel it through the [CancelTestCommandAsync][cancel] API, or [Stop-ServiceFabricTestCommand][cancelps] PowerShell cmdlet.</span></span>  <span data-ttu-id="a3fbc-133">При вызове GetProgress в этом случае свойство State объекта хода выполнения будет иметь значение Cancelled или ForceCancelled, в зависимости от аргумента данного API.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-133">If you call “GetProgress” on it in this case, the progress object’s State will be either Cancelled or ForceCancelled, depending on an argument to that API.</span></span>  <span data-ttu-id="a3fbc-134">Обратитесь к документации по [CancelTestCommandAsync][cancel] для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-134">See the documentation for [CancelTestCommandAsync][cancel] for more details.</span></span>

## <a name="details-of-running-a-command"></a><span data-ttu-id="a3fbc-135">Подробное описание выполнения команды</span><span class="sxs-lookup"><span data-stu-id="a3fbc-135">Details of Running a Command</span></span>
<span data-ttu-id="a3fbc-136">Чтобы начать выполнение команды, вызовите API Start с ожидаемыми аргументами.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-136">In order to start a command, call the Start API with the expected arguments.</span></span>  <span data-ttu-id="a3fbc-137">У всех API Start есть аргумент Guid, называемый operationId.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-137">All Start APIs have a Guid argument named operationId.</span></span>  <span data-ttu-id="a3fbc-138">Данный аргумент нужно отслеживать, так как он используется для отслеживания хода выполнения этой команды.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-138">You should keep track of the operationId argument, since it is used to track progress of this command.</span></span>  <span data-ttu-id="a3fbc-139">Его нужно передать в API GetProgress, чтобы отслеживать ход выполнения команды.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-139">This must be passed into the “GetProgress” API in order to track progress of the command.</span></span>  <span data-ttu-id="a3fbc-140">Значение operationId должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-140">The operationId must be unique.</span></span>

<span data-ttu-id="a3fbc-141">После успешного вызова API Start вызов API GetProgress должен осуществляться циклически, пока свойство State возвращаемого объекта хода выполнения не примет значение Completed.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-141">After successfully calling the Start API, the GetProgress API should be called in a loop until the returned progress object’s State property is Completed.</span></span>  <span data-ttu-id="a3fbc-142">Все исключения [FabricTransientException][fte] и OperationCanceledException должны быть обработаны путем повтора операции.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-142">All [FabricTransientException’s][fte] and OperationCanceledException’s should be retried.</span></span>
<span data-ttu-id="a3fbc-143">Когда команда достигнет конечного состояния (Completed, Faulted или Cancelled), свойство Result возвращаемого объекта хода выполнения будет содержать дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-143">When the command has reached a terminal state (Completed, Faulted, or Cancelled), the returned progress object’s Result property will have additional information.</span></span>  <span data-ttu-id="a3fbc-144">Если состояние — Completed, то Result.SelectedPartition.PartitionId будет содержать идентификатор секции, которая была выбрана.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-144">If the state is Completed, Result.SelectedPartition.PartitionId will contain the partition id that was selected.</span></span>  <span data-ttu-id="a3fbc-145">Result.Exception будет иметь значение NULL.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-145">Result.Exception will be null.</span></span>  <span data-ttu-id="a3fbc-146">Если состояние — Faulted, то Result.Exception будет содержать причину, по которой служба внесения ошибок и анализа присвоила это состояние выполнения команды.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-146">If the state is Faulted, Result.Exception will have the reason the Fault Injection and Analysis Service faulted the command.</span></span>  <span data-ttu-id="a3fbc-147">Result.SelectedPartition.PartitionId будет содержать идентификатор секции, которая была выбрана.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-147">Result.SelectedPartition.PartitionId will have the partition id that was selected.</span></span>  <span data-ttu-id="a3fbc-148">В некоторых ситуациях команда может быть выполнена недостаточно, чтобы можно было выбрать секцию.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-148">In some situations, the command may not have proceeded far enough to choose a partition.</span></span>  <span data-ttu-id="a3fbc-149">В этом случае значение PartitionId будет равно 0.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-149">In that case, the PartitionId will be 0.</span></span>  <span data-ttu-id="a3fbc-150">Если состояние — Cancelled, то Result.Exception будет иметь значение NULL.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-150">If the state is Cancelled, Result.Exception will be null.</span></span>  <span data-ttu-id="a3fbc-151">Как и в случае состояния Faulted, Result.SelectedPartition.PartitionId будет содержать идентификатор секции, которая была выбрана, но если команда была выполнена недостаточно для этого, этот идентификатор будет равен 0.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-151">Like the Faulted case, Result.SelectedPartition.PartitionId will have the partition id that was chosen, but if the command has not proceeded far enough to do so, it will be 0.</span></span>  <span data-ttu-id="a3fbc-152">Ознакомьтесь также с примером ниже.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-152">Please also refer to the sample below.</span></span>

<span data-ttu-id="a3fbc-153">В этом примере кода показано, как начать, а затем проверять выполнение команды, которая приводит к потере данных в определенном разделе.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-153">The sample code below shows how to start then check progress on a command to cause data loss on a specific partition.</span></span>

```csharp
    static async Task PerformDataLossSample()
    {
        // Create a unique operation id for the command below
        Guid operationId = Guid.NewGuid();

        // Note: Use the appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // The name of the target service
        Uri targetServiceName = new Uri("fabric:/MyService");

        // The id of the target partition inside the target service
        Guid targetPartitionId = new Guid("00000000-0000-0000-0000-000002233445");

        PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(targetServiceName, targetPartitionId);

        // Start the command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means the Fault Injection and Analysis Service has saved the intent to perform this work.  It does not say anything about the progress
        // of the command.
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

        // Poll the progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // the command won't be cancelled.        

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

                // In a terminal state .Result.SelectedPartition.PartitionId will have the chosen partition
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);
                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, the progress object's Result property's Exception property will have the reason why.
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

<span data-ttu-id="a3fbc-154">В примере ниже показано, как использовать PartitionSelector для выбора случайной секции заданной службы.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-154">The sample below shows how to use the PartitionSelector to choose a random partition of a specified service:</span></span>

```csharp
    static async Task PerformDataLossUseSelectorSample()
    {
        // Create a unique operation id for the command below
        Guid operationId = Guid.NewGuid();

        // Note: Use the appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // The name of the target service
        Uri targetServiceName = new Uri("fabric:/SampleService ");

        // Use a PartitionSelector that will have the Fault Injection and Analysis Service choose a random partition of “targetServiceName”
        PartitionSelector partitionSelector = PartitionSelector.RandomOf(targetServiceName);

        // Start the command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means the Fault Injection and Analysis Service has saved the intent to perform this work.  It does not say anything about the progress
        // of the command.
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

        // Poll the progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // the command won't be cancelled.

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
                // If State is Faulted, the progress object's Result property's Exception property will have the reason why.
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

## <a name="history-and-truncation"></a><span data-ttu-id="a3fbc-155">Журнал и усечение</span><span class="sxs-lookup"><span data-stu-id="a3fbc-155">History and Truncation</span></span>
<span data-ttu-id="a3fbc-156">После достижения командой конечного состояния ее метаданные на какое-то время остаются в службе внесения ошибок и анализа, прежде чем будут удалены для экономии места.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-156">After a command has reached a terminal state, its metadata will remain in the Fault Injection and Analysis Service for a certain time, before it will be removed to save space.</span></span>  <span data-ttu-id="a3fbc-157">Если после их удаления вызвать GetProgress с operationId этой команды, то будет возвращено исключение FabricException с кодом ErrorCode, равным KeyNotFound.</span><span class="sxs-lookup"><span data-stu-id="a3fbc-157">If “GetProgress” is called using the operationId of a command after it has been removed, it will return a FabricException with an ErrorCode of KeyNotFound.</span></span>

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
