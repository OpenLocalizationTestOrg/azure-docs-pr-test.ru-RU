---
title: "кластеры хаос в Service Fabric aaaInduce | Документы Microsoft"
description: "С помощью внесения ошибок и API-интерфейсы службы анализа кластера toomanage хаос в кластере hello."
services: service-fabric
documentationcenter: .net
author: motanv
manager: anmola
editor: motanv
ms.assetid: 2bd13443-3478-4382-9a5a-1f6c6b32bfc9
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: motanv
ms.openlocfilehash: 7e87cae22645fc4ba52e258471d8f3a4ffdb1cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a><span data-ttu-id="acc11-103">Вызов контролируемого хаоса в кластерах Service Fabric</span><span class="sxs-lookup"><span data-stu-id="acc11-103">Induce controlled Chaos in Service Fabric clusters</span></span>
<span data-ttu-id="acc11-104">Крупномасштабные распределенные системы, такие как облачные инфраструктуры, ненадежны по своей сути.</span><span class="sxs-lookup"><span data-stu-id="acc11-104">Large-scale distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="acc11-105">Azure Service Fabric позволяет разработчикам toowrite надежных распределенных служб поверх ненадежной инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="acc11-105">Azure Service Fabric enables developers toowrite reliable distributed services on top of an unreliable infrastructure.</span></span> <span data-ttu-id="acc11-106">toowrite надежных распределенных служб поверх ненадежной инфраструктуру, разработчики должны toobe может tootest hello стабильности служб, пока hello базовый ненадежной инфраструктуры проходит через сложных переходы между состояниями toofaults заказа.</span><span class="sxs-lookup"><span data-stu-id="acc11-106">toowrite robust distributed services on top of an unreliable infrastructure, developers need toobe able tootest hello stability of their services while hello underlying unreliable infrastructure is going through complicated state transitions due toofaults.</span></span>

<span data-ttu-id="acc11-107">Hello [внесения ошибок и служба кластеров анализа](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (также известный как hello ошибки Analysis Service) дает разработчикам возможность hello tooinduce ошибках tootest их службы.</span><span class="sxs-lookup"><span data-stu-id="acc11-107">hello [Fault Injection and Cluster Analysis Service](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (also known as hello Fault Analysis Service) gives developers hello ability tooinduce faults tootest their services.</span></span> <span data-ttu-id="acc11-108">Эти целевые имитируемые ошибок, таких как [перезапуска секции](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), может помочь Упражнение hello наиболее общие переходы между состояниями.</span><span class="sxs-lookup"><span data-stu-id="acc11-108">These targeted simulated faults, like [restarting a partition](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), can help exercise hello most common state transitions.</span></span> <span data-ttu-id="acc11-109">При этом целевым имитируемым ошибкам по определению свойственна погрешность, поэтому могут происходить ошибки, которые появляются только в трудной для прогнозирования, длинной и сложной последовательности переходов между состояниями.</span><span class="sxs-lookup"><span data-stu-id="acc11-109">However targeted simulated faults are biased by definition and thus may miss bugs that show up only in hard-to-predict, long and complicated sequence of state transitions.</span></span> <span data-ttu-id="acc11-110">Для неискаженного тестирования без можно использовать Chaos.</span><span class="sxs-lookup"><span data-stu-id="acc11-110">For an unbiased testing, you can use Chaos.</span></span>

<span data-ttu-id="acc11-111">Хаоса имитирует периодически, с чередованием ошибок (корректное и нестандартного) в кластере hello долгое время.</span><span class="sxs-lookup"><span data-stu-id="acc11-111">Chaos simulates periodic, interleaved faults (both graceful and ungraceful) throughout hello cluster over extended periods of time.</span></span> <span data-ttu-id="acc11-112">После настройки хаоса с коэффициентом hello и вид hello ошибок, можно запустить хаоса через C# или Powershell API toostart Создание ошибок в кластере hello и в службах.</span><span class="sxs-lookup"><span data-stu-id="acc11-112">Once you have configured Chaos with hello rate and hello kind of faults, you can start Chaos through C# or Powershell API toostart generating faults in hello cluster and in your services.</span></span> <span data-ttu-id="acc11-113">Вы можете настроить toorun хаоса для указанного периода времени (например, в течение одного часа), после чего хаоса останавливается автоматически, или можно вызвать API StopChaos (C# или Powershell) toostop его в любое время.</span><span class="sxs-lookup"><span data-stu-id="acc11-113">You can configure Chaos toorun for a specified time period (for example, for one hour), after which Chaos stops automatically, or you can call StopChaos API (C# or Powershell) toostop it at any time.</span></span>

> [!NOTE]
> <span data-ttu-id="acc11-114">В своей текущей форме хаоса вызывает только безопасные ошибки, который предполагает, что при отсутствии hello внешних ошибок потери кворума, или потери данных никогда не выполняется.</span><span class="sxs-lookup"><span data-stu-id="acc11-114">In its current form, Chaos induces only safe faults, which implies that in hello absence of external faults a quorum loss, or data loss never occurs.</span></span>
>

<span data-ttu-id="acc11-115">Пока выполняется хаоса, он создает различные события, включающие hello состоянии выполнения в момент hello hello.</span><span class="sxs-lookup"><span data-stu-id="acc11-115">While Chaos is running, it produces different events that capture hello state of hello run at hello moment.</span></span> <span data-ttu-id="acc11-116">Например ExecutingFaultsEvent содержит всех ошибок hello, что хаоса приняла решение tooexecute в этой итерации.</span><span class="sxs-lookup"><span data-stu-id="acc11-116">For example, an ExecutingFaultsEvent contains all hello faults that Chaos has decided tooexecute in that iteration.</span></span> <span data-ttu-id="acc11-117">ValidationFailedEvent содержит сведения об hello сбоя проверки (проблемы работоспособности или стабильность), обнаруженной во время проверки hello hello кластера.</span><span class="sxs-lookup"><span data-stu-id="acc11-117">A ValidationFailedEvent contains hello details of a validation failure (health or stability issues) that was found during hello validation of hello cluster.</span></span> <span data-ttu-id="acc11-118">Можно вызвать отчетов hello hello GetChaosReport API (C# или Powershell) tooget хаос запусков.</span><span class="sxs-lookup"><span data-stu-id="acc11-118">You can invoke hello GetChaosReport API (C# or Powershell) tooget hello report of Chaos runs.</span></span> <span data-ttu-id="acc11-119">Эти события сохраняются в [надежном словаре](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), для которого настроена политика усечения, диктуемая двумя конфигурациями: **MaxStoredChaosEventCount** (значение по умолчанию — 25 000) и **StoredActionCleanupIntervalInSeconds** (значение по умолчанию — 3600).</span><span class="sxs-lookup"><span data-stu-id="acc11-119">These events get persisted in a [reliable dictionary](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), which has a truncation policy dictated by two configurations: **MaxStoredChaosEventCount** (default value is 25000) and **StoredActionCleanupIntervalInSeconds** (default value is 3600).</span></span> <span data-ttu-id="acc11-120">Каждый *StoredActionCleanupIntervalInSeconds* хаоса проверок и всех но hello последней *MaxStoredChaosEventCount* события, удаляются из словаря надежного hello.</span><span class="sxs-lookup"><span data-stu-id="acc11-120">Every *StoredActionCleanupIntervalInSeconds* Chaos checks and all but hello most recent *MaxStoredChaosEventCount* events, are purged from hello reliable dictionary.</span></span>

## <a name="faults-induced-in-chaos"></a><span data-ttu-id="acc11-121">Ошибки, вызываемые Chaos</span><span class="sxs-lookup"><span data-stu-id="acc11-121">Faults induced in Chaos</span></span>
<span data-ttu-id="acc11-122">Хаоса приводит к возникновению ошибки через весь кластер Service Fabric hello и сжимает ошибок, которые видны в месяцах или годах, в течение нескольких часов.</span><span class="sxs-lookup"><span data-stu-id="acc11-122">Chaos generates faults across hello entire Service Fabric cluster and compresses faults that are seen in months or years into a few hours.</span></span> <span data-ttu-id="acc11-123">сочетание Hello с чередованием ошибок с интенсивность высокий уровень сбоев hello находит случаи, в противном случае могут быть пропущены.</span><span class="sxs-lookup"><span data-stu-id="acc11-123">hello combination of interleaved faults with hello high fault rate finds corner cases that may otherwise be missed.</span></span> <span data-ttu-id="acc11-124">Это упражнение хаоса приводит tooa значительные улучшения в качества кода hello hello службы.</span><span class="sxs-lookup"><span data-stu-id="acc11-124">This exercise of Chaos leads tooa significant improvement in hello code quality of hello service.</span></span>

<span data-ttu-id="acc11-125">Хаоса вызывает ошибки из hello следующие категории:</span><span class="sxs-lookup"><span data-stu-id="acc11-125">Chaos induces faults from hello following categories:</span></span>

* <span data-ttu-id="acc11-126">Перезапуск узла</span><span class="sxs-lookup"><span data-stu-id="acc11-126">Restart a node</span></span>
* <span data-ttu-id="acc11-127">Перезапуск развернутого пакета кода</span><span class="sxs-lookup"><span data-stu-id="acc11-127">Restart a deployed code package</span></span>
* <span data-ttu-id="acc11-128">Удаление реплики</span><span class="sxs-lookup"><span data-stu-id="acc11-128">Remove a replica</span></span>
* <span data-ttu-id="acc11-129">Перезапуск реплики</span><span class="sxs-lookup"><span data-stu-id="acc11-129">Restart a replica</span></span>
* <span data-ttu-id="acc11-130">перемещение первичной реплики (настраивается);</span><span class="sxs-lookup"><span data-stu-id="acc11-130">Move a primary replica (configurable)</span></span>
* <span data-ttu-id="acc11-131">перемещение вторичной реплики (настраивается).</span><span class="sxs-lookup"><span data-stu-id="acc11-131">Move a secondary replica (configurable)</span></span>

<span data-ttu-id="acc11-132">Chaos выполняет несколько итераций.</span><span class="sxs-lookup"><span data-stu-id="acc11-132">Chaos runs in multiple iterations.</span></span> <span data-ttu-id="acc11-133">Каждая итерация состоит из ошибки и проверки кластеров для hello указанный период.</span><span class="sxs-lookup"><span data-stu-id="acc11-133">Each iteration consists of faults and cluster validation for hello specified period.</span></span> <span data-ttu-id="acc11-134">Вы можете настроить hello время, затраченное для кластера toostabilize hello и toosucceed проверки.</span><span class="sxs-lookup"><span data-stu-id="acc11-134">You can configure hello time spent for hello cluster toostabilize and for validation toosucceed.</span></span> <span data-ttu-id="acc11-135">При обнаружении сбоя при проверке кластера хаоса создает и сохраняет ValidationFailedEvent с меткой времени UTC hello и подробные сведения об ошибках hello.</span><span class="sxs-lookup"><span data-stu-id="acc11-135">If a failure is found in cluster validation, Chaos generates and persists a ValidationFailedEvent with hello UTC timestamp and hello failure details.</span></span> <span data-ttu-id="acc11-136">Например рассмотрим экземпляр хаоса, задаваемое toorun часа с не более трех одновременных сбоев.</span><span class="sxs-lookup"><span data-stu-id="acc11-136">For example, consider an instance of Chaos that is set toorun for an hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="acc11-137">Хаоса вызывает три ошибок, а затем проводится проверка работоспособности кластера hello.</span><span class="sxs-lookup"><span data-stu-id="acc11-137">Chaos induces three faults, and then validates hello cluster health.</span></span> <span data-ttu-id="acc11-138">Он проходит по предыдущей hello передает шаг, пока он не будет явно остановлена через StopChaosAsync API hello или один час.</span><span class="sxs-lookup"><span data-stu-id="acc11-138">It iterates through hello previous step until it is explicitly stopped through hello StopChaosAsync API or one-hour passes.</span></span> <span data-ttu-id="acc11-139">Если hello кластер переходит в неработоспособное в какой-либо итерации (то есть он не стабилизация внутри hello переданное MaxClusterStabilizationTimeout), хаоса приводит к возникновению ошибки ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="acc11-139">If hello cluster becomes unhealthy in any iteration (that is, it does not stabilize within hello passed-in MaxClusterStabilizationTimeout), Chaos generates a ValidationFailedEvent.</span></span> <span data-ttu-id="acc11-140">Это событие указывает на наличие ошибки, которую необходимо дополнительно изучить.</span><span class="sxs-lookup"><span data-stu-id="acc11-140">This event indicates that something has gone wrong and might need further investigation.</span></span>

<span data-ttu-id="acc11-141">tooget которого ошибках вызываемые хаоса, можно использовать API GetChaosReport (powershell или C#).</span><span class="sxs-lookup"><span data-stu-id="acc11-141">tooget which faults Chaos induced, you can use GetChaosReport API (powershell or C#).</span></span> <span data-ttu-id="acc11-142">Hello API возвращает hello следующего сегмента hello хаоса отчет, основанный на токен продолжения переданное hello или hello переданное временных интервалов.</span><span class="sxs-lookup"><span data-stu-id="acc11-142">hello API gets hello next segment of hello Chaos report based on hello passed-in continuation token or hello passed-in time-range.</span></span> <span data-ttu-id="acc11-143">Можно указать hello ContinuationToken tooget hello следующего сегмента hello хаоса отчета или временных интервалов hello через StartTimeUtc и EndTimeUtc можно указать, но нельзя указать hello ContinuationToken и диапазон времени hello в hello одного вызова.</span><span class="sxs-lookup"><span data-stu-id="acc11-143">You can either specify hello ContinuationToken tooget hello next segment of hello Chaos report or you can specify hello time-range through StartTimeUtc and EndTimeUtc, but you cannot specify both hello ContinuationToken and hello time-range in hello same call.</span></span> <span data-ttu-id="acc11-144">При наличии более чем 100 событий хаоса, hello хаоса отчет возвращается в сегментов, где сегмент содержит не более 100 событий хаоса.</span><span class="sxs-lookup"><span data-stu-id="acc11-144">When there are more than 100 Chaos events, hello Chaos report is returned in segments where a segment contains no more than 100 Chaos events.</span></span>

## <a name="important-configuration-options"></a><span data-ttu-id="acc11-145">Важные параметры конфигурации</span><span class="sxs-lookup"><span data-stu-id="acc11-145">Important configuration options</span></span>
* <span data-ttu-id="acc11-146">**TimeToRun**. Общее время выполнения Chaos до успешного завершения.</span><span class="sxs-lookup"><span data-stu-id="acc11-146">**TimeToRun**: Total time that Chaos runs before it finishes with success.</span></span> <span data-ttu-id="acc11-147">Вы можете остановить хаоса до его использования для периода TimeToRun hello через StopChaos API hello.</span><span class="sxs-lookup"><span data-stu-id="acc11-147">You can stop Chaos before it has run for hello TimeToRun period through hello StopChaos API.</span></span>

* <span data-ttu-id="acc11-148">**MaxClusterStabilizationTimeout**: hello максимальный объем времени toowait для работоспособности, прежде чем выдать ValidationFailedEvent toobecome кластера hello.</span><span class="sxs-lookup"><span data-stu-id="acc11-148">**MaxClusterStabilizationTimeout**: hello maximum amount of time toowait for hello cluster toobecome healthy before producing a ValidationFailedEvent.</span></span> <span data-ttu-id="acc11-149">Это время ожидания составляет tooreduce hello нагрузки в кластере hello, пока он восстанавливается.</span><span class="sxs-lookup"><span data-stu-id="acc11-149">This wait is tooreduce hello load on hello cluster while it is recovering.</span></span> <span data-ttu-id="acc11-150">выполняются проверки Hello являются:</span><span class="sxs-lookup"><span data-stu-id="acc11-150">hello checks performed are:</span></span>
  * <span data-ttu-id="acc11-151">Если состояние кластера hello — нормальное</span><span class="sxs-lookup"><span data-stu-id="acc11-151">If hello cluster health is OK</span></span>
  * <span data-ttu-id="acc11-152">Если служба работоспособности hello нормальное</span><span class="sxs-lookup"><span data-stu-id="acc11-152">If hello service health is OK</span></span>
  * <span data-ttu-id="acc11-153">Если hello целевой размер набора реплик осуществляется только hello служебного раздела</span><span class="sxs-lookup"><span data-stu-id="acc11-153">If hello target replica set size is achieved for hello service partition</span></span>
  * <span data-ttu-id="acc11-154">отсутствуют ли реплики InBuild.</span><span class="sxs-lookup"><span data-stu-id="acc11-154">That no InBuild replicas exist</span></span>
* <span data-ttu-id="acc11-155">**MaxConcurrentFaults**: hello максимальное количество одновременных ошибок, вносимое в каждой итерации.</span><span class="sxs-lookup"><span data-stu-id="acc11-155">**MaxConcurrentFaults**: hello maximum number of concurrent faults that are induced in each iteration.</span></span> <span data-ttu-id="acc11-156">большее число hello Hello, hello более интенсивная является хаоса и проходит через hello переход на другой ресурс и hello состояния перехода комбинации, которые hello кластера также являются более сложными.</span><span class="sxs-lookup"><span data-stu-id="acc11-156">hello higher hello number, hello more aggressive Chaos is and hello failovers and hello state transition combinations that hello cluster goes through are also more complex.</span></span> 

> [!NOTE]
> <span data-ttu-id="acc11-157">Независимо от того как большое значение *MaxConcurrentFaults* имеет хаоса гарантирует - в отсутствие hello внешних ошибки — нет потери кворума или потери данных.</span><span class="sxs-lookup"><span data-stu-id="acc11-157">Regardless how high a value *MaxConcurrentFaults* has, Chaos guarantees - in hello absence of external faults - there is no quorum loss or data loss.</span></span>
>

* <span data-ttu-id="acc11-158">**EnableMoveReplicaFaults**: включает или отключает hello ошибки, вызывающие toomove hello первичной или вторичной реплики.</span><span class="sxs-lookup"><span data-stu-id="acc11-158">**EnableMoveReplicaFaults**: Enables or disables hello faults that cause hello primary or secondary replicas toomove.</span></span> <span data-ttu-id="acc11-159">Эти ошибки отключены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="acc11-159">These faults are disabled by default.</span></span>
* <span data-ttu-id="acc11-160">**WaitTimeBetweenIterations**: hello объем toowait времени между итерациями.</span><span class="sxs-lookup"><span data-stu-id="acc11-160">**WaitTimeBetweenIterations**: hello amount of time toowait between iterations.</span></span> <span data-ttu-id="acc11-161">То есть hello время хаоса приостановит работу после выполнения цикла сбоев и завершения hello соответствующие проверки работоспособности hello hello кластера.</span><span class="sxs-lookup"><span data-stu-id="acc11-161">That is, hello amount of time Chaos will pause after having executed a round of faults and having finished hello corresponding validation of hello health of hello cluster.</span></span> <span data-ttu-id="acc11-162">Здравствуйте, чем выше значение hello, hello нижней — скорость внедрения среднее ошибки hello.</span><span class="sxs-lookup"><span data-stu-id="acc11-162">hello higher hello value, hello lower is hello average fault injection rate.</span></span>
* <span data-ttu-id="acc11-163">**WaitTimeBetweenFaults**: hello объем toowait времени между двух последовательных сбоев в один проход.</span><span class="sxs-lookup"><span data-stu-id="acc11-163">**WaitTimeBetweenFaults**: hello amount of time toowait between two consecutive faults in a single iteration.</span></span> <span data-ttu-id="acc11-164">Здравствуйте, чем выше значение hello, hello нижней параллелизм hello (или hello перекрывают друг друга) ошибок.</span><span class="sxs-lookup"><span data-stu-id="acc11-164">hello higher hello value, hello lower hello concurrency of (or hello overlap between) faults.</span></span>
* <span data-ttu-id="acc11-165">**ClusterHealthPolicy**: политика работоспособности кластера — используется toovalidate hello работоспособности кластера hello между итерациями хаос.</span><span class="sxs-lookup"><span data-stu-id="acc11-165">**ClusterHealthPolicy**: Cluster health policy is used toovalidate hello health of hello cluster in between Chaos iterations.</span></span> <span data-ttu-id="acc11-166">Если hello работоспособности кластера является недопустимым или происходит непредвиденное исключение во время выполнения ошибки, хаоса ожидает 30 минут, прежде чем hello Далее проверки работоспособности - tooprovide hello кластер с toorecuperate некоторое время.</span><span class="sxs-lookup"><span data-stu-id="acc11-166">If hello cluster health is in error or if an unexpected exception happens during fault execution, Chaos will wait for 30 minutes before hello next health-check - tooprovide hello cluster with some time toorecuperate.</span></span>
* <span data-ttu-id="acc11-167">**Context**. Коллекция (string, string) пар "ключ —значение".</span><span class="sxs-lookup"><span data-stu-id="acc11-167">**Context**: A collection of (string, string) type key-value pairs.</span></span> <span data-ttu-id="acc11-168">Hello карты может быть toorecord используется информация о hello хаоса запуска.</span><span class="sxs-lookup"><span data-stu-id="acc11-168">hello map can be used toorecord information about hello Chaos run.</span></span> <span data-ttu-id="acc11-169">Максимальное число таких пар — 100. Каждая строка (ключ или значение) может содержать не более 4095 символов.</span><span class="sxs-lookup"><span data-stu-id="acc11-169">There cannot be more than 100 such pairs and each string (key or value) can be at most 4095 characters long.</span></span> <span data-ttu-id="acc11-170">На этой карте задается начальный hello hello хаоса запуска toooptionally хранилище hello контекста о hello конкретного выполнения.</span><span class="sxs-lookup"><span data-stu-id="acc11-170">This map is set by hello starter of hello Chaos run toooptionally store hello context about hello specific run.</span></span>

## <a name="how-toorun-chaos"></a><span data-ttu-id="acc11-171">Как toorun хаоса</span><span class="sxs-lookup"><span data-stu-id="acc11-171">How toorun Chaos</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using System.Fabric;

using System.Diagnostics;
using System.Fabric.Chaos.DataStructures;

class Program
{
    private class ChaosEventComparer : IEqualityComparer<ChaosEvent>
    {
        public bool Equals(ChaosEvent x, ChaosEvent y)
        {
            return x.TimeStampUtc.Equals(y.TimeStampUtc);
        }

        public int GetHashCode(ChaosEvent obj)
        {
            return obj.TimeStampUtc.GetHashCode();
        }
    }

    static void Main(string[] args)
    {
        var clusterConnectionString = "localhost:19000";
        using (var client = new FabricClient(clusterConnectionString))
        {
            var startTimeUtc = DateTime.UtcNow;
            var stabilizationTimeout = TimeSpan.FromSeconds(30.0);
            var timeToRun = TimeSpan.FromMinutes(60.0);
            var maxConcurrentFaults = 3;

            var parameters = new ChaosParameters(
                stabilizationTimeout,
                maxConcurrentFaults,
                true, /* EnableMoveReplicaFault */
                timeToRun);

            try
            {
                client.TestManager.StartChaosAsync(parameters).GetAwaiter().GetResult();
            }
            catch (FabricChaosAlreadyRunningException)
            {
                Console.WriteLine("An instance of Chaos is already running in hello cluster.");
            }

            var filter = new ChaosReportFilter(startTimeUtc, DateTime.MaxValue);

            var eventSet = new HashSet<ChaosEvent>(new ChaosEventComparer());

            while (true)
            {
                var report = client.TestManager.GetChaosReportAsync(filter).GetAwaiter().GetResult();

                foreach (var chaosEvent in report.History)
                {
                    if (eventSet.Add(chaosEvent))
                    {
                        Console.WriteLine(chaosEvent);
                    }
                }

                // When Chaos stops, a StoppedEvent is created.
                // If a StoppedEvent is found, exit hello loop.
                var lastEvent = report.History.LastOrDefault();

                if (lastEvent is StoppedEvent)
                {
                    break;
                }

                Task.Delay(TimeSpan.FromSeconds(1.0)).GetAwaiter().GetResult();
            }
        }
    }
}
```

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

$events = @{}
$now = [System.DateTime]::UtcNow

Start-ServiceFabricChaos -TimeToRunMinute $timeToRun -MaxConcurrentFaults $concurrentFaults -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec

while($true)
{
    $stopped = $false
    $report = Get-ServiceFabricChaosReport -StartTimeUtc $now -EndTimeUtc ([System.DateTime]::MaxValue)

    foreach ($e in $report.History) {

        if(-Not ($events.Contains($e.TimeStampUtc.Ticks)))
        {
            $events.Add($e.TimeStampUtc.Ticks, $e)
            if($e -is [System.Fabric.Chaos.DataStructures.ValidationFailedEvent])
            {
                Write-Host -BackgroundColor White -ForegroundColor Red $e
            }
            else
            {
                if($e -is [System.Fabric.Chaos.DataStructures.StoppedEvent])
                {
                    $stopped = $true
                }

                Write-Host $e
            }
        }
    }

    if($stopped -eq $true)
    {
        break
    }

    Start-Sleep -Seconds 1
}

Stop-ServiceFabricChaos
```
