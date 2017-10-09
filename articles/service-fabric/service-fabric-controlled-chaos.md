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
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a>Вызов контролируемого хаоса в кластерах Service Fabric
Крупномасштабные распределенные системы, такие как облачные инфраструктуры, ненадежны по своей сути. Azure Service Fabric позволяет разработчикам toowrite надежных распределенных служб поверх ненадежной инфраструктуры. toowrite надежных распределенных служб поверх ненадежной инфраструктуру, разработчики должны toobe может tootest hello стабильности служб, пока hello базовый ненадежной инфраструктуры проходит через сложных переходы между состояниями toofaults заказа.

Hello [внесения ошибок и служба кластеров анализа](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (также известный как hello ошибки Analysis Service) дает разработчикам возможность hello tooinduce ошибках tootest их службы. Эти целевые имитируемые ошибок, таких как [перезапуска секции](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), может помочь Упражнение hello наиболее общие переходы между состояниями. При этом целевым имитируемым ошибкам по определению свойственна погрешность, поэтому могут происходить ошибки, которые появляются только в трудной для прогнозирования, длинной и сложной последовательности переходов между состояниями. Для неискаженного тестирования без можно использовать Chaos.

Хаоса имитирует периодически, с чередованием ошибок (корректное и нестандартного) в кластере hello долгое время. После настройки хаоса с коэффициентом hello и вид hello ошибок, можно запустить хаоса через C# или Powershell API toostart Создание ошибок в кластере hello и в службах. Вы можете настроить toorun хаоса для указанного периода времени (например, в течение одного часа), после чего хаоса останавливается автоматически, или можно вызвать API StopChaos (C# или Powershell) toostop его в любое время.

> [!NOTE]
> В своей текущей форме хаоса вызывает только безопасные ошибки, который предполагает, что при отсутствии hello внешних ошибок потери кворума, или потери данных никогда не выполняется.
>

Пока выполняется хаоса, он создает различные события, включающие hello состоянии выполнения в момент hello hello. Например ExecutingFaultsEvent содержит всех ошибок hello, что хаоса приняла решение tooexecute в этой итерации. ValidationFailedEvent содержит сведения об hello сбоя проверки (проблемы работоспособности или стабильность), обнаруженной во время проверки hello hello кластера. Можно вызвать отчетов hello hello GetChaosReport API (C# или Powershell) tooget хаос запусков. Эти события сохраняются в [надежном словаре](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), для которого настроена политика усечения, диктуемая двумя конфигурациями: **MaxStoredChaosEventCount** (значение по умолчанию — 25 000) и **StoredActionCleanupIntervalInSeconds** (значение по умолчанию — 3600). Каждый *StoredActionCleanupIntervalInSeconds* хаоса проверок и всех но hello последней *MaxStoredChaosEventCount* события, удаляются из словаря надежного hello.

## <a name="faults-induced-in-chaos"></a>Ошибки, вызываемые Chaos
Хаоса приводит к возникновению ошибки через весь кластер Service Fabric hello и сжимает ошибок, которые видны в месяцах или годах, в течение нескольких часов. сочетание Hello с чередованием ошибок с интенсивность высокий уровень сбоев hello находит случаи, в противном случае могут быть пропущены. Это упражнение хаоса приводит tooa значительные улучшения в качества кода hello hello службы.

Хаоса вызывает ошибки из hello следующие категории:

* Перезапуск узла
* Перезапуск развернутого пакета кода
* Удаление реплики
* Перезапуск реплики
* перемещение первичной реплики (настраивается);
* перемещение вторичной реплики (настраивается).

Chaos выполняет несколько итераций. Каждая итерация состоит из ошибки и проверки кластеров для hello указанный период. Вы можете настроить hello время, затраченное для кластера toostabilize hello и toosucceed проверки. При обнаружении сбоя при проверке кластера хаоса создает и сохраняет ValidationFailedEvent с меткой времени UTC hello и подробные сведения об ошибках hello. Например рассмотрим экземпляр хаоса, задаваемое toorun часа с не более трех одновременных сбоев. Хаоса вызывает три ошибок, а затем проводится проверка работоспособности кластера hello. Он проходит по предыдущей hello передает шаг, пока он не будет явно остановлена через StopChaosAsync API hello или один час. Если hello кластер переходит в неработоспособное в какой-либо итерации (то есть он не стабилизация внутри hello переданное MaxClusterStabilizationTimeout), хаоса приводит к возникновению ошибки ValidationFailedEvent. Это событие указывает на наличие ошибки, которую необходимо дополнительно изучить.

tooget которого ошибках вызываемые хаоса, можно использовать API GetChaosReport (powershell или C#). Hello API возвращает hello следующего сегмента hello хаоса отчет, основанный на токен продолжения переданное hello или hello переданное временных интервалов. Можно указать hello ContinuationToken tooget hello следующего сегмента hello хаоса отчета или временных интервалов hello через StartTimeUtc и EndTimeUtc можно указать, но нельзя указать hello ContinuationToken и диапазон времени hello в hello одного вызова. При наличии более чем 100 событий хаоса, hello хаоса отчет возвращается в сегментов, где сегмент содержит не более 100 событий хаоса.

## <a name="important-configuration-options"></a>Важные параметры конфигурации
* **TimeToRun**. Общее время выполнения Chaos до успешного завершения. Вы можете остановить хаоса до его использования для периода TimeToRun hello через StopChaos API hello.

* **MaxClusterStabilizationTimeout**: hello максимальный объем времени toowait для работоспособности, прежде чем выдать ValidationFailedEvent toobecome кластера hello. Это время ожидания составляет tooreduce hello нагрузки в кластере hello, пока он восстанавливается. выполняются проверки Hello являются:
  * Если состояние кластера hello — нормальное
  * Если служба работоспособности hello нормальное
  * Если hello целевой размер набора реплик осуществляется только hello служебного раздела
  * отсутствуют ли реплики InBuild.
* **MaxConcurrentFaults**: hello максимальное количество одновременных ошибок, вносимое в каждой итерации. большее число hello Hello, hello более интенсивная является хаоса и проходит через hello переход на другой ресурс и hello состояния перехода комбинации, которые hello кластера также являются более сложными. 

> [!NOTE]
> Независимо от того как большое значение *MaxConcurrentFaults* имеет хаоса гарантирует - в отсутствие hello внешних ошибки — нет потери кворума или потери данных.
>

* **EnableMoveReplicaFaults**: включает или отключает hello ошибки, вызывающие toomove hello первичной или вторичной реплики. Эти ошибки отключены по умолчанию.
* **WaitTimeBetweenIterations**: hello объем toowait времени между итерациями. То есть hello время хаоса приостановит работу после выполнения цикла сбоев и завершения hello соответствующие проверки работоспособности hello hello кластера. Здравствуйте, чем выше значение hello, hello нижней — скорость внедрения среднее ошибки hello.
* **WaitTimeBetweenFaults**: hello объем toowait времени между двух последовательных сбоев в один проход. Здравствуйте, чем выше значение hello, hello нижней параллелизм hello (или hello перекрывают друг друга) ошибок.
* **ClusterHealthPolicy**: политика работоспособности кластера — используется toovalidate hello работоспособности кластера hello между итерациями хаос. Если hello работоспособности кластера является недопустимым или происходит непредвиденное исключение во время выполнения ошибки, хаоса ожидает 30 минут, прежде чем hello Далее проверки работоспособности - tooprovide hello кластер с toorecuperate некоторое время.
* **Context**. Коллекция (string, string) пар "ключ —значение". Hello карты может быть toorecord используется информация о hello хаоса запуска. Максимальное число таких пар — 100. Каждая строка (ключ или значение) может содержать не более 4095 символов. На этой карте задается начальный hello hello хаоса запуска toooptionally хранилище hello контекста о hello конкретного выполнения.

## <a name="how-toorun-chaos"></a>Как toorun хаоса

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
