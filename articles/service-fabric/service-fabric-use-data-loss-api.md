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
# <a name="how-tooinvoke-data-loss-on-services"></a>Как tooInvoke потери данных в службах
> [!WARNING]
> В этом документе описаны как toocause потери данных в службах и должны использоваться с осторожностью.
> 
> 

## <a name="introduction"></a>Введение
Можно вызвать потерю данных в секции службы Service Fabric, вызвав StartPartitionDataLossAsync().  Этот api использует hello внесения ошибок и служб Analysis Service tooperform hello рабочих toocause данных потери условия.

## <a name="using-hello-fault-injection-and-analysis-service"></a>С помощью hello внесения ошибок и служб Analysis Services
Hello внесения ошибок и служб Analysis Services в настоящее время поддерживает следующие интерфейсы API в представленной ниже диаграмме hello hello.  Hello правой части диаграммы hello показаны hello соответствующий командлет PowerShell.  Дополнительные сведения для каждого из них см. в документации msdn toohello на каждый API.

| API C# | Командлет PowerShell |
| --- | ---:|
| [StartPartitionDataLossAsync][dl] |[Start-ServiceFabricPartitionDataLoss][psdl] |
| [StartPartitionQuorumLossAsync][ql] |[Start-ServiceFabricPartitionQuorumLoss][psql] |
| [StartPartitionRestartAsync][rp] |[Start-ServiceFabricPartitionRestart][psrp] |

## <a name="conceptual-overview-of-running-a-command"></a>Принцип выполнения команды
Здравствуйте, внесения ошибок и служб Analysis Services использует асинхронную модель, где начинается hello команды с одного API называется tooas hello «Start» API-интерфейса в этом документе, а затем проверяет hello ход выполнения этой команды с помощью API «GetProgress» до достижения терминала состояние, или пока вы отмените его.
toostart команду, при вызове API «Start» hello hello соответствующий API.  Этот API возвращает при hello внесения ошибок и служб Analysis Services принял запрос hello.  Однако это не указывает, насколько выполнена команда или было ли вообще начато ее выполнение.  В порядке toocheck ход выполнения команды вызовите hello «GetProgress» API, который соответствует вызван ранее API toohello «Start».  Hello «GetProgress» API-Интерфейс вернет объект, указывая hello текущее состояние команды hello внутри свойства его состояние.  Команда выполняется неограниченное время, пока не будет выполнено одно из следующих условий.

1. Она полностью выполнена.  При вызове метода «GetProgress» на его таким образом, состояние объекта выполняется hello будет завершено.
2. При выполнении возникла неустранимая ошибка.  При вызове метода «GetProgress» на его таким образом, произошел сбой состояния объекта выполняется hello
3. Отменить его через hello [CancelTestCommandAsync] [ cancel] API, или [Stop ServiceFabricTestCommand] [ cancelps] командлета PowerShell.  При вызове метода «GetProgress» на его таким образом, hello объекта выполняется состояние будет отменено или ForceCancelled, в зависимости от аргумента toothat API.  В документации hello [CancelTestCommandAsync] [ cancel] для получения дополнительных сведений.

## <a name="details-of-running-a-command"></a>Подробное описание выполнения команды
В порядке toostart команду вызовите hello запустить API с аргументами hello ожидается.  У всех API Start есть аргумент Guid, называемый operationId.  Вы должны хранить список аргументов hello идентификатором операции, так как он используется tootrack ход выполнения этой команды.  Это должен быть передан в hello «GetProgress» API выполняется tootrack порядок hello команды.  идентификатором Hello операции должно быть уникальным.

После успешного вызова метода hello запустить API, hello, который должен вызываться в цикле GetProgress API до выполнения возврата hello объекта состояния завершения.  Все исключения [FabricTransientException][fte] и OperationCanceledException должны быть обработаны путем повтора операции.
При достижении конечного состояния (завершено, Faulted или отменено) команда hello hello вернул свойство объекта выполняется результат будет иметь дополнительные сведения.  Если hello состояние завершения, Result.SelectedPartition.PartitionId будет содержать идентификатор секции hello, которая была выбрана.  Result.Exception будет иметь значение NULL.  Если hello состоянием является Faulted, Result.Exception будет иметь hello причина hello внесения ошибок и команда hello сбой службы Analysis.  Result.SelectedPartition.PartitionId будет иметь идентификатор секции hello, которая была выбрана.  В некоторых ситуациях hello команды может не продолжилось так toochoose секции.  В этом случае hello PartitionId будет 0.  При отмене состояния hello Result.Exception будет иметь значение null.  Как hello случай Faulted Result.SelectedPartition.PartitionId будет иметь идентификатор hello секции, которая была выбрана, но если команда hello не была выполнена так, toodo таким образом, оно будет равно 0.  Также см. Образец toohello ниже.

Hello в образце кода ниже показано, как toostart затем проверить выполнение команды toocause потеря данных в определенный раздел.

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

Образец Hello ниже показано, как toouse hello PartitionSelector toochoose случайных секционирования из заданной службы.

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

## <a name="history-and-truncation"></a>Журнал и усечение
После достижения конечного состояния команды свои метаданные сохранятся в hello внесения ошибок и служб Analysis Services для определенного времени, прежде чем он будет удален toosave пространства.  Если «GetProgress» вызывается с идентификатором hello операции команды, после он был удален, возвращается FabricException с ErrorCode KeyNotFound.

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
