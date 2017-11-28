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
# <a name="testability-scenarios"></a><span data-ttu-id="1d4b2-103">Сценарии Testability</span><span class="sxs-lookup"><span data-stu-id="1d4b2-103">Testability scenarios</span></span>
<span data-ttu-id="1d4b2-104">Крупные распределенные системы, такие как облачные инфраструктуры, ненадежные по своей сути.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-104">Large distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="1d4b2-105">Azure Service Fabric дает разработчикам hello возможность toowrite служб toorun поверх ненадежной инфраструктур.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-105">Azure Service Fabric gives developers hello ability toowrite services toorun on top of unreliable infrastructures.</span></span> <span data-ttu-id="1d4b2-106">В порядке toowrite высокого качества служб разработчики должны toobe может tooinduce таких ненадежных инфраструктуры tootest hello стабильность их службы.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-106">In order toowrite high-quality services, developers need toobe able tooinduce such unreliable infrastructure tootest hello stability of their services.</span></span>

<span data-ttu-id="1d4b2-107">Hello ошибки Analysis Service предоставляет разработчикам tootest hello возможность tooinduce сбоя действия службы в присутствии hello сбоев.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-107">hello Fault Analysis Service gives developers hello ability tooinduce fault actions tootest services in hello presence of failures.</span></span> <span data-ttu-id="1d4b2-108">Однако на этом преимущества целевого моделирования ошибок заканчиваются.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-108">However, targeted simulated faults will get you only so far.</span></span> <span data-ttu-id="1d4b2-109">tootake hello, кроме того, тестирование сценариев hello тестирования можно использовать в Service Fabric: хаоса и теста отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-109">tootake hello testing further, you can use hello test scenarios in Service Fabric: a chaos test and a failover test.</span></span> <span data-ttu-id="1d4b2-110">Эти сценарии моделирования непрерывного с чередованием ошибок корректное и нестандартного во всей кластера hello долгое время.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-110">These scenarios simulate continuous interleaved faults, both graceful and ungraceful, throughout hello cluster over extended periods of time.</span></span> <span data-ttu-id="1d4b2-111">После настройки тестового с коэффициентом hello и тип ошибок запускается через API-интерфейсы C# или PowerShell, toogenerate ошибки в кластере hello и службы.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-111">Once a test is configured with hello rate and kind of faults, it can be started through either C# APIs or PowerShell, toogenerate faults in hello cluster and your service.</span></span>

> [!WARNING]
> <span data-ttu-id="1d4b2-112">ChaosTestScenario заменен более устойчивым Chaos на основе службы.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-112">ChaosTestScenario is being replaced by a more resilient, service-based Chaos.</span></span> <span data-ttu-id="1d4b2-113">См. статью toohello [управляет хаоса](service-fabric-controlled-chaos.md) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-113">Please refer toohello new article [Controlled Chaos](service-fabric-controlled-chaos.md) for more details.</span></span>
> 
> 

## <a name="chaos-test"></a><span data-ttu-id="1d4b2-114">Хаотический тест</span><span class="sxs-lookup"><span data-stu-id="1d4b2-114">Chaos test</span></span>
<span data-ttu-id="1d4b2-115">сценарий хаоса Hello приводит к возникновению ошибки через весь кластер Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-115">hello chaos scenario generates faults across hello entire Service Fabric cluster.</span></span> <span data-ttu-id="1d4b2-116">сценарий Hello сжимает сбои обычно в месяцах или годах tooa несколько часов.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-116">hello scenario compresses faults generally seen in months or years tooa few hours.</span></span> <span data-ttu-id="1d4b2-117">сочетание Hello с чередованием ошибок с интенсивность высокий уровень сбоев hello находит случаи, в противном случае попасть в результаты.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-117">hello combination of interleaved faults with hello high fault rate finds corner cases that are otherwise missed.</span></span> <span data-ttu-id="1d4b2-118">Это порождает tooa значительное улучшение качества кода hello hello службы.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-118">This leads tooa significant improvement in hello code quality of hello service.</span></span>

### <a name="faults-simulated-in-hello-chaos-test"></a><span data-ttu-id="1d4b2-119">Ошибки моделировать в хаос теста hello</span><span class="sxs-lookup"><span data-stu-id="1d4b2-119">Faults simulated in hello chaos test</span></span>
* <span data-ttu-id="1d4b2-120">Перезапуск узла</span><span class="sxs-lookup"><span data-stu-id="1d4b2-120">Restart a node</span></span>
* <span data-ttu-id="1d4b2-121">Перезапуск развернутого пакета кода</span><span class="sxs-lookup"><span data-stu-id="1d4b2-121">Restart a deployed code package</span></span>
* <span data-ttu-id="1d4b2-122">Удаление реплики</span><span class="sxs-lookup"><span data-stu-id="1d4b2-122">Remove a replica</span></span>
* <span data-ttu-id="1d4b2-123">Перезапуск реплики</span><span class="sxs-lookup"><span data-stu-id="1d4b2-123">Restart a replica</span></span>
* <span data-ttu-id="1d4b2-124">Перемещение первичной реплики (необязательно)</span><span class="sxs-lookup"><span data-stu-id="1d4b2-124">Move a primary replica (optional)</span></span>
* <span data-ttu-id="1d4b2-125">Перемещение вторичной реплики (необязательно)</span><span class="sxs-lookup"><span data-stu-id="1d4b2-125">Move a secondary replica (optional)</span></span>

<span data-ttu-id="1d4b2-126">Hello хаоса теста несколько итераций ошибок и проверки кластера для hello указанного периода времени.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-126">hello chaos test runs multiple iterations of faults and cluster validations for hello specified period of time.</span></span> <span data-ttu-id="1d4b2-127">Hello время, затраченное для кластера toostabilize hello и toosucceed проверки может быть настроен.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-127">hello time spent for hello cluster toostabilize and for validation toosucceed is also configurable.</span></span> <span data-ttu-id="1d4b2-128">сценарий Hello не помеченным единичного отказа в проверке кластера.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-128">hello scenario fails when you hit a single failure in cluster validation.</span></span>

<span data-ttu-id="1d4b2-129">Например рассмотрим тестового набора toorun одного часа с не более трех одновременных сбоев.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-129">For example, consider a test set toorun for one hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="1d4b2-130">Hello теста будет вызывать ошибки три и проверки работоспособности кластера hello.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-130">hello test will induce three faults, and then validate hello cluster health.</span></span> <span data-ttu-id="1d4b2-131">Hello теста будет итерацию hello предыдущего шага, пока hello кластер переходит в неработоспособное или передает один час.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-131">hello test will iterate through hello previous step till hello cluster becomes unhealthy or one hour passes.</span></span> <span data-ttu-id="1d4b2-132">Если hello кластер переходит в неработоспособное в какой-либо итерации, т. е. он не стабилизировать в течение настроенного времени, hello тест завершится ошибкой с исключением.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-132">If hello cluster becomes unhealthy in any iteration, i.e. it does not stabilize within a configured time, hello test will fail with an exception.</span></span> <span data-ttu-id="1d4b2-133">Это исключение указывает, что возникли проблемы, которые необходимо дополнительно изучить.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-133">This exception indicates that something has gone wrong and needs further investigation.</span></span>

<span data-ttu-id="1d4b2-134">В своей текущей форме hello подсистему создания ошибки в тесте хаоса hello вызывает только безопасные ошибок.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-134">In its current form, hello fault generation engine in hello chaos test induces only safe faults.</span></span> <span data-ttu-id="1d4b2-135">Это означает, что в отсутствие hello внешних ошибок, кворума или потери данных никогда не будет выполняться.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-135">This means that in hello absence of external faults, a quorum or data loss will never occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="1d4b2-136">Важные параметры конфигурации</span><span class="sxs-lookup"><span data-stu-id="1d4b2-136">Important configuration options</span></span>
* <span data-ttu-id="1d4b2-137">**TimeToRun**: общее время, hello тест будет выполняться перед завершением работы с успешным выполнением.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-137">**TimeToRun**: Total time that hello test will run before finishing with success.</span></span> <span data-ttu-id="1d4b2-138">Hello теста можно завершить работу ранее вместо ошибки при проверке.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-138">hello test can finish earlier in lieu of a validation failure.</span></span>
* <span data-ttu-id="1d4b2-139">**MaxClusterStabilizationTimeout**: максимальный объем времени toowait для hello кластера toobecome работоспособное до невыполнения теста hello.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-139">**MaxClusterStabilizationTimeout**: Maximum amount of time toowait for hello cluster toobecome healthy before failing hello test.</span></span> <span data-ttu-id="1d4b2-140">Hello проверок, является ли состояние кластера — нормальное, службы работоспособности в норме, hello целевой размер набора реплик достигается для раздела службы hello и не реплик InBuild существует.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-140">hello checks performed are whether cluster health is OK, service health is OK, hello target replica set size is achieved for hello service partition, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="1d4b2-141">**MaxConcurrentFaults.** Максимальное количество одновременных ошибок, вызываемых при каждой итерации.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-141">**MaxConcurrentFaults**: Maximum number of concurrent faults induced in each iteration.</span></span> <span data-ttu-id="1d4b2-142">Здравствуйте, большее число hello, hello более интенсивная hello теста, поэтому приводит к более сложные переход на другой ресурс и переход сочетания.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-142">hello higher hello number, hello more aggressive hello test, hence resulting in more complex failovers and transition combinations.</span></span> <span data-ttu-id="1d4b2-143">Hello теста гарантирует, при отсутствии ошибок внешних существует не будет потери кворума или данных, независимо от того, насколько высоким является этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-143">hello test guarantees that in absence of external faults there will not be a quorum or data loss, irrespective of how high this configuration is.</span></span>
* <span data-ttu-id="1d4b2-144">**EnableMoveReplicaFaults**: включает или отключает hello ошибок, вызывающих hello перемещения hello первичной или вторичной реплики.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-144">**EnableMoveReplicaFaults**: Enables or disables hello faults that are causing hello move of hello primary or secondary replicas.</span></span> <span data-ttu-id="1d4b2-145">Эти ошибки отключены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-145">These faults are disabled by default.</span></span>
* <span data-ttu-id="1d4b2-146">**WaitTimeBetweenIterations**: объем toowait времени между итерациями, т. е. после цикла сбоев и соответствующей проверки.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-146">**WaitTimeBetweenIterations**: Amount of time toowait between iterations, i.e. after a round of faults and corresponding validation.</span></span>

### <a name="how-toorun-hello-chaos-test"></a><span data-ttu-id="1d4b2-147">Как протестировать toorun хаоса hello</span><span class="sxs-lookup"><span data-stu-id="1d4b2-147">How toorun hello chaos test</span></span>
<span data-ttu-id="1d4b2-148">Пример на языке C#</span><span class="sxs-lookup"><span data-stu-id="1d4b2-148">C# sample</span></span>

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

<span data-ttu-id="1d4b2-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d4b2-149">PowerShell</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a><span data-ttu-id="1d4b2-150">Тест Failover Test</span><span class="sxs-lookup"><span data-stu-id="1d4b2-150">Failover test</span></span>
<span data-ttu-id="1d4b2-151">сценарии тестовой отработки отказа Hello — это версия сценария тестовой хаоса hello, предназначенный для конкретной службы секции.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-151">hello failover test scenario is a version of hello chaos test scenario that targets a specific service partition.</span></span> <span data-ttu-id="1d4b2-152">Она проверяет hello эффект перехода на другой ресурс в раздел конкретной службы и оставить hello другие службы не влияет.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-152">It tests hello effect of failover on a specific service partition while leaving hello other services unaffected.</span></span> <span data-ttu-id="1d4b2-153">Как только он использует сведения о hello целевой секции, а также другие параметры, он выполняется как клиентские средство, которое использует API-интерфейсы C# или PowerShell toogenerate ошибок для раздела службы.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-153">Once it's configured with hello target partition information and other parameters, it runs as a client-side tool that uses either C# APIs or PowerShell toogenerate faults for a service partition.</span></span> <span data-ttu-id="1d4b2-154">сценарий Hello итерацию последовательности имитацию сбоев и проверки службы во время бизнес-логики на стороне tooprovide hello рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-154">hello scenario iterates through a sequence of simulated faults and service validation while your business logic runs on hello side tooprovide a workload.</span></span> <span data-ttu-id="1d4b2-155">Ошибка при проверке службы указывает на проблему, которую необходимо дополнительно изучить.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-155">A failure in service validation indicates an issue that needs further investigation.</span></span>

### <a name="faults-simulated-in-hello-failover-test"></a><span data-ttu-id="1d4b2-156">Ошибки, смоделированные в тесте отработки отказа hello</span><span class="sxs-lookup"><span data-stu-id="1d4b2-156">Faults simulated in hello failover test</span></span>
* <span data-ttu-id="1d4b2-157">Перезапустите развернутый пакет кода размещения hello секции</span><span class="sxs-lookup"><span data-stu-id="1d4b2-157">Restart a deployed code package where hello partition is hosted</span></span>
* <span data-ttu-id="1d4b2-158">Удаление первичной или вторичной реплики либо экземпляра без отслеживания состояния</span><span class="sxs-lookup"><span data-stu-id="1d4b2-158">Remove a primary/secondary replica or stateless instance</span></span>
* <span data-ttu-id="1d4b2-159">Перезапуск первичной или вторичной реплики (в материализованной службе)</span><span class="sxs-lookup"><span data-stu-id="1d4b2-159">Restart a primary secondary replica (if a persisted service)</span></span>
* <span data-ttu-id="1d4b2-160">Перемещение первичной реплики</span><span class="sxs-lookup"><span data-stu-id="1d4b2-160">Move a primary replica</span></span>
* <span data-ttu-id="1d4b2-161">Перемещение вторичной реплики</span><span class="sxs-lookup"><span data-stu-id="1d4b2-161">Move a secondary replica</span></span>
* <span data-ttu-id="1d4b2-162">Перезапустите hello секции</span><span class="sxs-lookup"><span data-stu-id="1d4b2-162">Restart hello partition</span></span>

<span data-ttu-id="1d4b2-163">тест отработки отказа Hello вызывает ошибку выбранной и затем выполняет проверку службы tooensure hello его стабильности.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-163">hello failover test induces a chosen fault and then runs validation on hello service tooensure its stability.</span></span> <span data-ttu-id="1d4b2-164">тест отработки отказа Hello вызывает только одно ошибок во время, в отличие от toopossible несколько ошибок в тесте хаоса hello.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-164">hello failover test induces only one fault at a time, as opposed toopossible multiple faults in hello chaos test.</span></span> <span data-ttu-id="1d4b2-165">Если раздела службы hello не стабилизировать в течение периода ожидания hello настроен после каждой ошибки, hello тест не пройден.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-165">If hello service partition does not stabilize within hello configured timeout after each fault, hello test fails.</span></span> <span data-ttu-id="1d4b2-166">тест Hello вызывает только безопасные ошибок.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-166">hello test induces only safe faults.</span></span> <span data-ttu-id="1d4b2-167">Это означает, что при отсутствии внешних ошибок исключена вероятность потери кворума или данных.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-167">This means that in absence of external failures, a quorum or data loss will not occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="1d4b2-168">Важные параметры конфигурации</span><span class="sxs-lookup"><span data-stu-id="1d4b2-168">Important configuration options</span></span>
* <span data-ttu-id="1d4b2-169">**PartitionSelector**: объект выбора, указывающее hello раздел, который требуется toobe целевые.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-169">**PartitionSelector**: Selector object that specifies hello partition that needs toobe targeted.</span></span>
* <span data-ttu-id="1d4b2-170">**TimeToRun**: общее время, hello тест будет выполняться до завершения.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-170">**TimeToRun**: Total time that hello test will run before finishing.</span></span>
* <span data-ttu-id="1d4b2-171">**MaxServiceStabilizationTimeout**: максимальный объем времени toowait для hello кластера toobecome работоспособное до невыполнения теста hello.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-171">**MaxServiceStabilizationTimeout**: Maximum amount of time toowait for hello cluster toobecome healthy before failing hello test.</span></span> <span data-ttu-id="1d4b2-172">Hello проверок, ли служба работоспособности — ОК, hello целевой размер набора реплик обеспечивается для всех секций и не реплик InBuild существует.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-172">hello checks performed are whether service health is OK, hello target replica set size is achieved for all partitions, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="1d4b2-173">**WaitTimeBetweenFaults**: объем toowait времени между цикл каждого сбоя и проверки.</span><span class="sxs-lookup"><span data-stu-id="1d4b2-173">**WaitTimeBetweenFaults**: Amount of time toowait between every fault and validation cycle.</span></span>

### <a name="how-toorun-hello-failover-test"></a><span data-ttu-id="1d4b2-174">Как протестировать hello toorun перехода на другой ресурс</span><span class="sxs-lookup"><span data-stu-id="1d4b2-174">How toorun hello failover test</span></span>
<span data-ttu-id="1d4b2-175">**C#**</span><span class="sxs-lookup"><span data-stu-id="1d4b2-175">**C#**</span></span>

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


<span data-ttu-id="1d4b2-176">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="1d4b2-176">**PowerShell**</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
