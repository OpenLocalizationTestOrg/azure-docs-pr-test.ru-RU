---
title: "Создание тестов хаотичных сбоев и отработки отказа для микрослужб Azure | Документация Майкрософт"
description: "Использование сценариев тестов на хаос и отработку отказа Service Fabric для провоцирования ошибок и проверки надежности служб."
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
ms.openlocfilehash: d06026c750e01ad5825338a78d9af331265f434a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="testability-scenarios"></a><span data-ttu-id="3fcba-103">Сценарии Testability</span><span class="sxs-lookup"><span data-stu-id="3fcba-103">Testability scenarios</span></span>
<span data-ttu-id="3fcba-104">Крупные распределенные системы, такие как облачные инфраструктуры, ненадежные по своей сути.</span><span class="sxs-lookup"><span data-stu-id="3fcba-104">Large distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="3fcba-105">Azure Service Fabric предоставляет разработчикам возможность создавать службы, которые работают в ненадежных инфраструктурах.</span><span class="sxs-lookup"><span data-stu-id="3fcba-105">Azure Service Fabric gives developers the ability to write services to run on top of unreliable infrastructures.</span></span> <span data-ttu-id="3fcba-106">Чтобы создать высококачественные службы, разработчики должны иметь возможность проверить стабильность работы своих служб в таких ненадежных инфраструктурах.</span><span class="sxs-lookup"><span data-stu-id="3fcba-106">In order to write high-quality services, developers need to be able to induce such unreliable infrastructure to test the stability of their services.</span></span>

<span data-ttu-id="3fcba-107">Служба анализа сбоев позволяет разработчикам вызывать действия, порождающие сбой, для тестирования работы служб в условиях сбоя.</span><span class="sxs-lookup"><span data-stu-id="3fcba-107">The Fault Analysis Service gives developers the ability to induce fault actions to test services in the presence of failures.</span></span> <span data-ttu-id="3fcba-108">Однако на этом преимущества целевого моделирования ошибок заканчиваются.</span><span class="sxs-lookup"><span data-stu-id="3fcba-108">However, targeted simulated faults will get you only so far.</span></span> <span data-ttu-id="3fcba-109">Для дальнейшего развития тестирования вы можете использовать сценарии тестирования в Service Fabric: хаотический тест и тест отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="3fcba-109">To take the testing further, you can use the test scenarios in Service Fabric: a chaos test and a failover test.</span></span> <span data-ttu-id="3fcba-110">Они моделируют на кластере непрерывные ошибки с чередованием, как нормальные, так и ненормальные, на протяжении долгого периода времени.</span><span class="sxs-lookup"><span data-stu-id="3fcba-110">These scenarios simulate continuous interleaved faults, both graceful and ungraceful, throughout the cluster over extended periods of time.</span></span> <span data-ttu-id="3fcba-111">Настроив частоту и тип ошибок для теста, его можно запустить через интерфейсы API C# или PowerShell, создавая сбои в кластере и службе.</span><span class="sxs-lookup"><span data-stu-id="3fcba-111">Once a test is configured with the rate and kind of faults, it can be started through either C# APIs or PowerShell, to generate faults in the cluster and your service.</span></span>

> [!WARNING]
> <span data-ttu-id="3fcba-112">ChaosTestScenario заменен более устойчивым Chaos на основе службы.</span><span class="sxs-lookup"><span data-stu-id="3fcba-112">ChaosTestScenario is being replaced by a more resilient, service-based Chaos.</span></span> <span data-ttu-id="3fcba-113">Для получения дополнительных сведений ознакомьтесь с новой статьей [Вызов контролируемого хаоса в кластерах Service Fabric](service-fabric-controlled-chaos.md) .</span><span class="sxs-lookup"><span data-stu-id="3fcba-113">Please refer to the new article [Controlled Chaos](service-fabric-controlled-chaos.md) for more details.</span></span>
> 
> 

## <a name="chaos-test"></a><span data-ttu-id="3fcba-114">Хаотический тест</span><span class="sxs-lookup"><span data-stu-id="3fcba-114">Chaos test</span></span>
<span data-ttu-id="3fcba-115">Сценарий хаотического тестирования создает ошибки в масштабах всего кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3fcba-115">The chaos scenario generates faults across the entire Service Fabric cluster.</span></span> <span data-ttu-id="3fcba-116">Этот сценарий позволяет всего за несколько часов проработать ошибки, которые обычно наблюдаются в течение многих месяцев или лет.</span><span class="sxs-lookup"><span data-stu-id="3fcba-116">The scenario compresses faults generally seen in months or years to a few hours.</span></span> <span data-ttu-id="3fcba-117">Сочетание ошибок с чередованием с высокой частотой возникновения сбоев позволяет находить проблемы, которые в противном случае были бы упущены.</span><span class="sxs-lookup"><span data-stu-id="3fcba-117">The combination of interleaved faults with the high fault rate finds corner cases that are otherwise missed.</span></span> <span data-ttu-id="3fcba-118">Это обеспечивает значительное улучшение качества кода службы.</span><span class="sxs-lookup"><span data-stu-id="3fcba-118">This leads to a significant improvement in the code quality of the service.</span></span>

### <a name="faults-simulated-in-the-chaos-test"></a><span data-ttu-id="3fcba-119">Ошибки, моделируемые в хаотическом тесте</span><span class="sxs-lookup"><span data-stu-id="3fcba-119">Faults simulated in the chaos test</span></span>
* <span data-ttu-id="3fcba-120">Перезапуск узла</span><span class="sxs-lookup"><span data-stu-id="3fcba-120">Restart a node</span></span>
* <span data-ttu-id="3fcba-121">Перезапуск развернутого пакета кода</span><span class="sxs-lookup"><span data-stu-id="3fcba-121">Restart a deployed code package</span></span>
* <span data-ttu-id="3fcba-122">Удаление реплики</span><span class="sxs-lookup"><span data-stu-id="3fcba-122">Remove a replica</span></span>
* <span data-ttu-id="3fcba-123">Перезапуск реплики</span><span class="sxs-lookup"><span data-stu-id="3fcba-123">Restart a replica</span></span>
* <span data-ttu-id="3fcba-124">Перемещение первичной реплики (необязательно)</span><span class="sxs-lookup"><span data-stu-id="3fcba-124">Move a primary replica (optional)</span></span>
* <span data-ttu-id="3fcba-125">Перемещение вторичной реплики (необязательно)</span><span class="sxs-lookup"><span data-stu-id="3fcba-125">Move a secondary replica (optional)</span></span>

<span data-ttu-id="3fcba-126">Хаотический тест выполняет несколько итераций сбоев и проверок кластера в течение указанного периода времени.</span><span class="sxs-lookup"><span data-stu-id="3fcba-126">The chaos test runs multiple iterations of faults and cluster validations for the specified period of time.</span></span> <span data-ttu-id="3fcba-127">Кроме того, вы можете настроить время, затрачиваемое на стабилизацию работы и проверку кластера для успешной его работы.</span><span class="sxs-lookup"><span data-stu-id="3fcba-127">The time spent for the cluster to stabilize and for validation to succeed is also configurable.</span></span> <span data-ttu-id="3fcba-128">Сценарий завершается ошибкой, если при проверке кластера обнаруживается сбой.</span><span class="sxs-lookup"><span data-stu-id="3fcba-128">The scenario fails when you hit a single failure in cluster validation.</span></span>

<span data-ttu-id="3fcba-129">Рассмотрим тест, запланированный на выполнение в течение одного часа и включающий не более трех одновременных сбоев.</span><span class="sxs-lookup"><span data-stu-id="3fcba-129">For example, consider a test set to run for one hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="3fcba-130">В ходе теста будут вызваны три ошибки, а затем проверена работоспособность кластера.</span><span class="sxs-lookup"><span data-stu-id="3fcba-130">The test will induce three faults, and then validate the cluster health.</span></span> <span data-ttu-id="3fcba-131">Во время теста предыдущий шаг будет повторяться, пока кластер не станет неработоспособным или не пройдет один час.</span><span class="sxs-lookup"><span data-stu-id="3fcba-131">The test will iterate through the previous step till the cluster becomes unhealthy or one hour passes.</span></span> <span data-ttu-id="3fcba-132">Если при любой итерации кластер становится неработоспособным, т. е. его работа не стабилизируется в течение заданного времени, тест завершится ошибкой с исключением.</span><span class="sxs-lookup"><span data-stu-id="3fcba-132">If the cluster becomes unhealthy in any iteration, i.e. it does not stabilize within a configured time, the test will fail with an exception.</span></span> <span data-ttu-id="3fcba-133">Это исключение указывает, что возникли проблемы, которые необходимо дополнительно изучить.</span><span class="sxs-lookup"><span data-stu-id="3fcba-133">This exception indicates that something has gone wrong and needs further investigation.</span></span>

<span data-ttu-id="3fcba-134">В своей текущей форме механизм создания ошибок при хаотическом тесте вызывает только безопасные сбои.</span><span class="sxs-lookup"><span data-stu-id="3fcba-134">In its current form, the fault generation engine in the chaos test induces only safe faults.</span></span> <span data-ttu-id="3fcba-135">Это означает, что при отсутствии внешних ошибок исключена вероятность потери кворума или данных.</span><span class="sxs-lookup"><span data-stu-id="3fcba-135">This means that in the absence of external faults, a quorum or data loss will never occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="3fcba-136">Важные параметры конфигурации</span><span class="sxs-lookup"><span data-stu-id="3fcba-136">Important configuration options</span></span>
* <span data-ttu-id="3fcba-137">**TimeToRun.** Общее время выполнения теста до успешного завершения.</span><span class="sxs-lookup"><span data-stu-id="3fcba-137">**TimeToRun**: Total time that the test will run before finishing with success.</span></span> <span data-ttu-id="3fcba-138">Тест может завершиться ранее вместо ошибки проверки.</span><span class="sxs-lookup"><span data-stu-id="3fcba-138">The test can finish earlier in lieu of a validation failure.</span></span>
* <span data-ttu-id="3fcba-139">**MaxClusterStabilizationTimeout.** Максимальный период ожидания возврата кластера в работоспособное состояние до завершения теста с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="3fcba-139">**MaxClusterStabilizationTimeout**: Maximum amount of time to wait for the cluster to become healthy before failing the test.</span></span> <span data-ttu-id="3fcba-140">Проверяется, работоспособны ли кластер и службы, соответствует ли размер набора целевых реплик разделу службы, а также отсутствуют ли реплики InBuild.</span><span class="sxs-lookup"><span data-stu-id="3fcba-140">The checks performed are whether cluster health is OK, service health is OK, the target replica set size is achieved for the service partition, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="3fcba-141">**MaxConcurrentFaults.** Максимальное количество одновременных ошибок, вызываемых при каждой итерации.</span><span class="sxs-lookup"><span data-stu-id="3fcba-141">**MaxConcurrentFaults**: Maximum number of concurrent faults induced in each iteration.</span></span> <span data-ttu-id="3fcba-142">Чем больше это число, тем более интенсивно проводится тест, что приведет к более сложным отработкам отказа и переходам.</span><span class="sxs-lookup"><span data-stu-id="3fcba-142">The higher the number, the more aggressive the test, hence resulting in more complex failovers and transition combinations.</span></span> <span data-ttu-id="3fcba-143">Во время этого теста при отсутствии внешних ошибок исключена вероятность потери кворума или данных, независимо от значения этого параметра.</span><span class="sxs-lookup"><span data-stu-id="3fcba-143">The test guarantees that in absence of external faults there will not be a quorum or data loss, irrespective of how high this configuration is.</span></span>
* <span data-ttu-id="3fcba-144">**EnableMoveReplicaFaults**: включает или отключает ошибки, что приводит к перемещению первичных или вторичных реплик.</span><span class="sxs-lookup"><span data-stu-id="3fcba-144">**EnableMoveReplicaFaults**: Enables or disables the faults that are causing the move of the primary or secondary replicas.</span></span> <span data-ttu-id="3fcba-145">Эти ошибки отключены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3fcba-145">These faults are disabled by default.</span></span>
* <span data-ttu-id="3fcba-146">**WaitTimeBetweenIterations**: время ожидания между итерациями, то есть после цикла ошибок и соответствующей проверки.</span><span class="sxs-lookup"><span data-stu-id="3fcba-146">**WaitTimeBetweenIterations**: Amount of time to wait between iterations, i.e. after a round of faults and corresponding validation.</span></span>

### <a name="how-to-run-the-chaos-test"></a><span data-ttu-id="3fcba-147">Выполнение хаотического теста</span><span class="sxs-lookup"><span data-stu-id="3fcba-147">How to run the chaos test</span></span>
<span data-ttu-id="3fcba-148">Пример на языке C#</span><span class="sxs-lookup"><span data-stu-id="3fcba-148">C# sample</span></span>

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

        // The chaos test scenario should run at least 60 minutes or until it fails.
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

        // Create the scenario class and execute it asynchronously.
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

<span data-ttu-id="3fcba-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3fcba-149">PowerShell</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a><span data-ttu-id="3fcba-150">Тест Failover Test</span><span class="sxs-lookup"><span data-stu-id="3fcba-150">Failover test</span></span>
<span data-ttu-id="3fcba-151">Сценарий тестирования отработки отказа — это версия сценария хаотического тестирования, предназначенная для конкретного раздела службы.</span><span class="sxs-lookup"><span data-stu-id="3fcba-151">The failover test scenario is a version of the chaos test scenario that targets a specific service partition.</span></span> <span data-ttu-id="3fcba-152">В ходе этого теста проверяется влияние отработки отказа на определенный раздел службы (другие службы не затрагиваются).</span><span class="sxs-lookup"><span data-stu-id="3fcba-152">It tests the effect of failover on a specific service partition while leaving the other services unaffected.</span></span> <span data-ttu-id="3fcba-153">Если ввести сведения о целевом разделе и других параметрах, тест выполняется как клиентское средство, которое использует API C# или PowerShell, чтобы создавать ошибки для раздела службы.</span><span class="sxs-lookup"><span data-stu-id="3fcba-153">Once it's configured with the target partition information and other parameters, it runs as a client-side tool that uses either C# APIs or PowerShell to generate faults for a service partition.</span></span> <span data-ttu-id="3fcba-154">В ходе сценария повторяется последовательность моделируемых сбоев и проверка службы, в то время как бизнес-логика обеспечивает рабочую нагрузку.</span><span class="sxs-lookup"><span data-stu-id="3fcba-154">The scenario iterates through a sequence of simulated faults and service validation while your business logic runs on the side to provide a workload.</span></span> <span data-ttu-id="3fcba-155">Ошибка при проверке службы указывает на проблему, которую необходимо дополнительно изучить.</span><span class="sxs-lookup"><span data-stu-id="3fcba-155">A failure in service validation indicates an issue that needs further investigation.</span></span>

### <a name="faults-simulated-in-the-failover-test"></a><span data-ttu-id="3fcba-156">Ошибки, моделируемые во время теста отработки отказа</span><span class="sxs-lookup"><span data-stu-id="3fcba-156">Faults simulated in the failover test</span></span>
* <span data-ttu-id="3fcba-157">Перезапуск развернутого пакета кода в расположении раздела</span><span class="sxs-lookup"><span data-stu-id="3fcba-157">Restart a deployed code package where the partition is hosted</span></span>
* <span data-ttu-id="3fcba-158">Удаление первичной или вторичной реплики либо экземпляра без отслеживания состояния</span><span class="sxs-lookup"><span data-stu-id="3fcba-158">Remove a primary/secondary replica or stateless instance</span></span>
* <span data-ttu-id="3fcba-159">Перезапуск первичной или вторичной реплики (в материализованной службе)</span><span class="sxs-lookup"><span data-stu-id="3fcba-159">Restart a primary secondary replica (if a persisted service)</span></span>
* <span data-ttu-id="3fcba-160">Перемещение первичной реплики</span><span class="sxs-lookup"><span data-stu-id="3fcba-160">Move a primary replica</span></span>
* <span data-ttu-id="3fcba-161">Перемещение вторичной реплики</span><span class="sxs-lookup"><span data-stu-id="3fcba-161">Move a secondary replica</span></span>
* <span data-ttu-id="3fcba-162">Перезапуск раздела</span><span class="sxs-lookup"><span data-stu-id="3fcba-162">Restart the partition</span></span>

<span data-ttu-id="3fcba-163">В ходе теста отработки отказа вызывается выбранная ошибка, а затем выполняется проверка службы для обеспечения ее стабильной работы.</span><span class="sxs-lookup"><span data-stu-id="3fcba-163">The failover test induces a chosen fault and then runs validation on the service to ensure its stability.</span></span> <span data-ttu-id="3fcba-164">Во время теста отработки отказа одновременно вызывается только одна ошибка в отличие от хаотического теста, в ходе которого может инициироваться несколько сбоев.</span><span class="sxs-lookup"><span data-stu-id="3fcba-164">The failover test induces only one fault at a time, as opposed to possible multiple faults in the chaos test.</span></span> <span data-ttu-id="3fcba-165">Если после каждого сбоя раздел службы не стабилизируется в течение заданного времени ожидания, тест не пройден.</span><span class="sxs-lookup"><span data-stu-id="3fcba-165">If the service partition does not stabilize within the configured timeout after each fault, the test fails.</span></span> <span data-ttu-id="3fcba-166">Этот тест вызывает только безопасные ошибки.</span><span class="sxs-lookup"><span data-stu-id="3fcba-166">The test induces only safe faults.</span></span> <span data-ttu-id="3fcba-167">Это означает, что при отсутствии внешних ошибок исключена вероятность потери кворума или данных.</span><span class="sxs-lookup"><span data-stu-id="3fcba-167">This means that in absence of external failures, a quorum or data loss will not occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="3fcba-168">Важные параметры конфигурации</span><span class="sxs-lookup"><span data-stu-id="3fcba-168">Important configuration options</span></span>
* <span data-ttu-id="3fcba-169">**PartitionSelector**— объект выбора, указывающий целевой раздел.</span><span class="sxs-lookup"><span data-stu-id="3fcba-169">**PartitionSelector**: Selector object that specifies the partition that needs to be targeted.</span></span>
* <span data-ttu-id="3fcba-170">**TimeToRun**— общее время выполнения теста до завершения.</span><span class="sxs-lookup"><span data-stu-id="3fcba-170">**TimeToRun**: Total time that the test will run before finishing.</span></span>
* <span data-ttu-id="3fcba-171">**MaxServiceStabilizationTimeout**— максимальный период ожидания возврата кластера в работоспособное состояние до завершения теста с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="3fcba-171">**MaxServiceStabilizationTimeout**: Maximum amount of time to wait for the cluster to become healthy before failing the test.</span></span> <span data-ttu-id="3fcba-172">Проверяется, работоспособна ли служба, соответствует ли размер набора целевых реплик всем разделам, а также отсутствуют ли реплики InBuild.</span><span class="sxs-lookup"><span data-stu-id="3fcba-172">The checks performed are whether service health is OK, the target replica set size is achieved for all partitions, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="3fcba-173">**WaitTimeBetweenFaults**— время ожидания между каждым циклом сбоя и проверки.</span><span class="sxs-lookup"><span data-stu-id="3fcba-173">**WaitTimeBetweenFaults**: Amount of time to wait between every fault and validation cycle.</span></span>

### <a name="how-to-run-the-failover-test"></a><span data-ttu-id="3fcba-174">Выполнение теста отработки отказа</span><span class="sxs-lookup"><span data-stu-id="3fcba-174">How to run the failover test</span></span>
<span data-ttu-id="3fcba-175">**C#**</span><span class="sxs-lookup"><span data-stu-id="3fcba-175">**C#**</span></span>

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

        // The chaos test scenario should run at least 60 minutes or until it fails.
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

        // Create the scenario class and execute it asynchronously.
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


<span data-ttu-id="3fcba-176">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="3fcba-176">**PowerShell**</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
