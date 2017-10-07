---
title: "тесты aaaCreate хаоса и переход на другой ресурс для Azure микрослужбами | Документы Microsoft"
description: "Тест хаоса Service Fabric hello и обеспечивая отработку отказа тест ошибок tooinduce сценариев и проверьте надежность hello служб."
services: service-fabric
documentationcenter: .net
author: motanv
manager: rsinha
editor: toddabel
ms.assetid: 8eee7e89-404a-4605-8f00-7e4d4fb17553
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv
ms.openlocfilehash: 1cac4f9e0e4a6c8416d5220d1537b5110decd1f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="testability-scenarios"></a>Сценарии Testability
Крупные распределенные системы, такие как облачные инфраструктуры, ненадежные по своей сути. Azure Service Fabric дает разработчикам hello возможность toowrite служб toorun поверх ненадежной инфраструктур. В порядке toowrite высокого качества служб разработчики должны toobe может tooinduce таких ненадежных инфраструктуры tootest hello стабильность их службы.

Hello ошибки Analysis Service предоставляет разработчикам tootest hello возможность tooinduce сбоя действия службы в присутствии hello сбоев. Однако на этом преимущества целевого моделирования ошибок заканчиваются. tootake hello, кроме того, тестирование сценариев hello тестирования можно использовать в Service Fabric: хаоса и теста отработки отказа. Эти сценарии моделирования непрерывного с чередованием ошибок корректное и нестандартного во всей кластера hello долгое время. После настройки тестового с коэффициентом hello и тип ошибок запускается через API-интерфейсы C# или PowerShell, toogenerate ошибки в кластере hello и службы.

> [!WARNING]
> ChaosTestScenario заменен более устойчивым Chaos на основе службы. См. статью toohello [управляет хаоса](service-fabric-controlled-chaos.md) для получения дополнительных сведений.
> 
> 

## <a name="chaos-test"></a>Хаотический тест
сценарий хаоса Hello приводит к возникновению ошибки через весь кластер Service Fabric hello. сценарий Hello сжимает сбои обычно в месяцах или годах tooa несколько часов. сочетание Hello с чередованием ошибок с интенсивность высокий уровень сбоев hello находит случаи, в противном случае попасть в результаты. Это порождает tooa значительное улучшение качества кода hello hello службы.

### <a name="faults-simulated-in-hello-chaos-test"></a>Ошибки моделировать в хаос теста hello
* Перезапуск узла
* Перезапуск развернутого пакета кода
* Удаление реплики
* Перезапуск реплики
* Перемещение первичной реплики (необязательно)
* Перемещение вторичной реплики (необязательно)

Hello хаоса теста несколько итераций ошибок и проверки кластера для hello указанного периода времени. Hello время, затраченное для кластера toostabilize hello и toosucceed проверки может быть настроен. сценарий Hello не помеченным единичного отказа в проверке кластера.

Например рассмотрим тестового набора toorun одного часа с не более трех одновременных сбоев. Hello теста будет вызывать ошибки три и проверки работоспособности кластера hello. Hello теста будет итерацию hello предыдущего шага, пока hello кластер переходит в неработоспособное или передает один час. Если hello кластер переходит в неработоспособное в какой-либо итерации, т. е. он не стабилизировать в течение настроенного времени, hello тест завершится ошибкой с исключением. Это исключение указывает, что возникли проблемы, которые необходимо дополнительно изучить.

В своей текущей форме hello подсистему создания ошибки в тесте хаоса hello вызывает только безопасные ошибок. Это означает, что в отсутствие hello внешних ошибок, кворума или потери данных никогда не будет выполняться.

### <a name="important-configuration-options"></a>Важные параметры конфигурации
* **TimeToRun**: общее время, hello тест будет выполняться перед завершением работы с успешным выполнением. Hello теста можно завершить работу ранее вместо ошибки при проверке.
* **MaxClusterStabilizationTimeout**: максимальный объем времени toowait для hello кластера toobecome работоспособное до невыполнения теста hello. Hello проверок, является ли состояние кластера — нормальное, службы работоспособности в норме, hello целевой размер набора реплик достигается для раздела службы hello и не реплик InBuild существует.
* **MaxConcurrentFaults.** Максимальное количество одновременных ошибок, вызываемых при каждой итерации. Здравствуйте, большее число hello, hello более интенсивная hello теста, поэтому приводит к более сложные переход на другой ресурс и переход сочетания. Hello теста гарантирует, при отсутствии ошибок внешних существует не будет потери кворума или данных, независимо от того, насколько высоким является этой конфигурации.
* **EnableMoveReplicaFaults**: включает или отключает hello ошибок, вызывающих hello перемещения hello первичной или вторичной реплики. Эти ошибки отключены по умолчанию.
* **WaitTimeBetweenIterations**: объем toowait времени между итерациями, т. е. после цикла сбоев и соответствующей проверки.

### <a name="how-toorun-hello-chaos-test"></a>Как протестировать toorun хаоса hello
Пример на языке C#

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunChaosTestScenarioAsync(clusterConnection).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunChaosTestScenarioAsync(string clusterConnection)
    {
        TimeSpan maxClusterStabilizationTimeout = TimeSpan.FromSeconds(180);
        uint maxConcurrentFaults = 3;
        bool enableMoveReplicaFaults = true;

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // hello chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        ChaosTestScenarioParameters scenarioParameters = new ChaosTestScenarioParameters(
          maxClusterStabilizationTimeout,
          maxConcurrentFaults,
          enableMoveReplicaFaults,
          timeToRun);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create hello scenario class and execute it asynchronously.
        ChaosTestScenario chaosScenario = new ChaosTestScenario(fabricClient, scenarioParameters);

        try
        {
            await chaosScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```

PowerShell

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a>Тест Failover Test
сценарии тестовой отработки отказа Hello — это версия сценария тестовой хаоса hello, предназначенный для конкретной службы секции. Она проверяет hello эффект перехода на другой ресурс в раздел конкретной службы и оставить hello другие службы не влияет. Как только он использует сведения о hello целевой секции, а также другие параметры, он выполняется как клиентские средство, которое использует API-интерфейсы C# или PowerShell toogenerate ошибок для раздела службы. сценарий Hello итерацию последовательности имитацию сбоев и проверки службы во время бизнес-логики на стороне tooprovide hello рабочей нагрузки. Ошибка при проверке службы указывает на проблему, которую необходимо дополнительно изучить.

### <a name="faults-simulated-in-hello-failover-test"></a>Ошибки, смоделированные в тесте отработки отказа hello
* Перезапустите развернутый пакет кода размещения hello секции
* Удаление первичной или вторичной реплики либо экземпляра без отслеживания состояния
* Перезапуск первичной или вторичной реплики (в материализованной службе)
* Перемещение первичной реплики
* Перемещение вторичной реплики
* Перезапустите hello секции

тест отработки отказа Hello вызывает ошибку выбранной и затем выполняет проверку службы tooensure hello его стабильности. тест отработки отказа Hello вызывает только одно ошибок во время, в отличие от toopossible несколько ошибок в тесте хаоса hello. Если раздела службы hello не стабилизировать в течение периода ожидания hello настроен после каждой ошибки, hello тест не пройден. тест Hello вызывает только безопасные ошибок. Это означает, что при отсутствии внешних ошибок исключена вероятность потери кворума или данных.

### <a name="important-configuration-options"></a>Важные параметры конфигурации
* **PartitionSelector**: объект выбора, указывающее hello раздел, который требуется toobe целевые.
* **TimeToRun**: общее время, hello тест будет выполняться до завершения.
* **MaxServiceStabilizationTimeout**: максимальный объем времени toowait для hello кластера toobecome работоспособное до невыполнения теста hello. Hello проверок, ли служба работоспособности — ОК, hello целевой размер набора реплик обеспечивается для всех секций и не реплик InBuild существует.
* **WaitTimeBetweenFaults**: объем toowait времени между цикл каждого сбоя и проверки.

### <a name="how-toorun-hello-failover-test"></a>Как протестировать hello toorun перехода на другой ресурс
**C#**

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunFailoverTestScenarioAsync(clusterConnection, serviceName).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunFailoverTestScenarioAsync(string clusterConnection, Uri serviceName)
    {
        TimeSpan maxServiceStabilizationTimeout = TimeSpan.FromSeconds(180);
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // hello chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        FailoverTestScenarioParameters scenarioParameters = new FailoverTestScenarioParameters(
          randomPartitionSelector,
          timeToRun,
          maxServiceStabilizationTimeout);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create hello scenario class and execute it asynchronously.
        FailoverTestScenario failoverScenario = new FailoverTestScenario(fabricClient, scenarioParameters);

        try
        {
            await failoverScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```


**PowerShell**

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
