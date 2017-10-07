---
title: "задачи aaaRun в toouse параллельные вычислительные ресурсы эффективно - пакетной службы Azure | Документы Microsoft"
description: "Вы можете увеличить эффективность и снизить стоимость, используя меньшее количество вычислительных узлов. Это возможно благодаря параллельному выполнению задач на каждом узле в пуле пакетной службы Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 538a067c-1f6e-44eb-a92b-8d51c33d3e1a
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05df4b7d8e0bc595168a97faa231b7c90fe81980
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-concurrently-toomaximize-usage-of-batch-compute-nodes"></a>Выполнение задач одновременно toomaximize использование пакетных вычислительных узлов 

При одновременной более одной задачи на каждом вычислительном узле в пуле пакетной службы Azure, можно увеличить использование ресурсов на меньшее число узлов в пул hello. Для некоторых рабочих нагрузок это позволит сократить время выполнения заданий и уменьшить затраты.

При некоторых сценариях преимущества выделять все узла в ресурсы tooa одну задачу, позволяя несколько задач tooshare эти ресурсы различных ситуаций с более эффективно:

* **Минимизация передачи данных** при задачи — это может tooshare данных. В этом сценарии можно значительно снизить расходы по передаче данных путем копирования общих данных tooa меньшее число узлов, а затем выполняя задачи параллельно на каждом узле. Это особенно относится узла копируются tooeach toobe данных hello должны передаваться между географических регионов.
* **повышается эффективность использования памяти** . Можно использовать меньше, но большего размера, вычислительные узлы с дополнительные tooefficiently памяти обработки таких пиков. Эти узлы будут иметь несколько задач, выполняющихся в параллельном режиме на каждом узле, но каждая задача будет использовать узлы hello много памяти в разное время.
* **уменьшается ограничение по количеству узлов** . В настоящее время пулы, настроенных для взаимодействия между узлами — ограниченный too50 вычислительных узлов. Если каждый узел в такой пул может tooexecute задачи параллельно, с увеличением количества задач могут выполняться одновременно.
* **Репликация на локальный вычислительный кластер**, например при переносе сначала tooAzure среды вычислений. Если текущее решение локальной выполняет несколько задач на вычислительном узле, можно увеличить максимальное количество hello узла задач toomore точно отражают этой конфигурации.

## <a name="example-scenario"></a>Пример сценария
Как tooillustrate пример hello преимущества выполнения параллельных задач, например, в приложении задачи есть требования к ЦП и памяти таким образом, что [Стандартная\_D1](../cloud-services/cloud-services-sizes-specs.md) узлы являются достаточно. Однако в toofinish hello задание времени требуется hello, необходимы 1000 этих узлов.

Вместо узлов размера Standard\_D1, каждый из которых содержит одно ядро ЦП, вы можете использовать 16-ядерные узлы [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md), включив на них параллельное выполнение задач. Таким образом, потребуется *в 16 раз меньше узлов* , то есть 63 узла вместо 1000. Кроме того Если требуются файлы большого приложения или ссылочные данные для каждого узла, длительность задания и эффективность снова улучшение поскольку hello данные копируются tooonly 16 узлов.

## <a name="enable-parallel-task-execution"></a>Включение параллельного выполнения задач
На уровне пула hello настроить вычислительные узлы для выполнения параллельных задач. Библиотека .NET пакета hello, установите hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] свойства при создании пула. При использовании API REST пакета hello задать hello [maxTasksPerNode] [ rest_addpool] элемент в тексте запроса hello во время создания пула.

Пакет Azure позволяет tooset максимальное число задач на каждом узле toofour раз (4 x) hello число ядер на узел. Например, если hello пула настраивается узлы размер «Большой» (4 ядра), затем `maxTasksPerNode` может задаваться too16. Дополнительные сведения о hello количество ядер для каждого из размеров hello узла см [размеров для облачных служб](../cloud-services/cloud-services-sizes-specs.md). Дополнительные сведения об ограничениях службы см. в разделе [квоты и лимиты для пакетной службы Azure hello](batch-quota-limit.md).

> [!TIP]
> Быть tootake убедиться, что в учетной записи hello `maxTasksPerNode` значение при создании [формула автоматического масштабирования] [ enable_autoscaling] для пула. Например, если в формуле учитывается параметр `$RunningTasks`, изменение количества задач существенно повлияет на результат ее применения. Дополнительные сведения см. в статье [Автоматическое масштабирование вычислительных узлов в пуле пакетной службы Azure](batch-automatic-scaling.md).
>
>

## <a name="distribution-of-tasks"></a>Распределение задач
При hello вычислительных узлов в пуле задачи могут выполняться параллельно, очень важно toospecify способ toobe задачи hello, распределенные по узлам hello в пуле hello.

С помощью hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] свойства, можно указать, что задачи следует назначать равномерно по всем узлам в пуле hello («распространение»). Или можно указать, что число задач должен выделяться tooeach узел перед задач, назначенных tooanother узла в пуле hello («упаковочный»).

В качестве примера как полезно использовать эту функцию, рассмотрим hello пула [Стандартная\_D14](../cloud-services/cloud-services-sizes-specs.md) узлов (в приведенном выше примере hello), которые настроены с [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] значение 16. Если hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] оснащен [ComputeNodeFillType] [ fill_type] из *пакет*, будет максимизации использования всех 16 ядер каждого узла и разрешить [автоматическое масштабирование пула](batch-automatic-scaling.md) tooprune неиспользуемые узлы из пула hello (узлы без назначенных задач). Это снизит использование ресурсов и расходы на них.

## <a name="batch-net-example"></a>Пример использования компонента .NET пакетной службы
Это [пакета .NET] [ api_net] API фрагмент кода показывает toocreate запрос пула, который содержит четыре больших узлы с не более четырех задач на каждом узле. Он указывает задачи планирования политики, который будет заполнять каждый узел с узлом tooanother задачи tooassigning предыдущие задачи в пуле hello. Дополнительные сведения о добавлении пулы с помощью пакета .NET API hello. в разделе [BatchClient.PoolOperations.CreatePool][poolcreate_net].

```csharp
CloudPool pool =
    batchClient.PoolOperations.CreatePool(
        poolId: "mypool",
        targetDedicatedComputeNodes: 4
        virtualMachineSize: "large",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

pool.MaxTasksPerComputeNode = 4;
pool.TaskSchedulingPolicy = new TaskSchedulingPolicy(ComputeNodeFillType.Pack);
pool.Commit();
```

## <a name="batch-rest-example"></a>Пример интерфейса REST API пакетной службы
Это [REST пакетной] [ api_rest] API фрагменте показано toocreate запрос пула, содержащего два больших узла с не более четырех задач на каждом узле. Дополнительные сведения о добавлении пулы с помощью API-интерфейса REST hello. в разделе [добавить учетную запись пула tooan][rest_addpool].

```json
{
  "odata.metadata":"https://myaccount.myregion.batch.azure.com/$metadata#pools/@Element",
  "id":"mypool",
  "vmSize":"large",
  "cloudServiceConfiguration": {
    "osFamily":"4",
    "targetOSVersion":"*",
  }
  "targetDedicatedComputeNodes":2,
  "maxTasksPerNode":4,
  "enableInterNodeCommunication":true,
}
```

> [!NOTE]
> Можно задать hello `maxTasksPerNode` элемент и [MaxTasksPerComputeNode] [ maxtasks_net] свойства только во время создания пула. Их невозможно изменить после создания пула.
>
>

## <a name="code-sample"></a>Пример кода
Hello [ParallelNodeTasks] [ parallel_tasks_sample] проекта на GitHub иллюстрирует использование hello hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] свойство.

Это консольное приложение C# использует hello [пакета .NET] [ api_net] toocreate библиотеки пула с одним или несколькими вычислительных узлов. Он выполняет ряд задач, можно настроить на эти узлы toosimulate переменная нагрузка. Выход из приложения hello определяет, какие узлы выполнения каждой задачи. приложение Hello также описаны основные параметры задания hello и длительность. Сводка часть Hello hello выходные данные двух разных запусках пример приложения hello появляется внизу.

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

Hello первого выполнения образца приложения hello показывает, что с одним узлом в пуле hello и по умолчанию hello одной задачи на каждом узле, продолжительность задания hello составляет более 30 минут.

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

Второй запуск отображается образец hello к значительному снижению длительности задания Hello. Это происходит потому hello пула была настроена с помощью четырех задач на узел, который позволяет почти квартала hello времени toocomplete hello параллельной задачи выполнения задания.

> [!NOTE]
> Длительность задания Hello в сводках hello выше, не включайте время создания пула. Каждое из заданий hello выше был отправленной toopreviously создания пулов, вычислительные узлы были в hello *Idle* состояния во время передачи.
>
>

## <a name="next-steps"></a>Дальнейшие действия
### <a name="batch-explorer-heat-map"></a>Тепловая карта обозревателя пакетной службы
Hello [обозреватель пакета Azure][batch_explorer], один из hello пакетной службы Azure [образцы приложений][github_samples], содержит *тепловой карты* компонент, который предоставляет визуализации выполнения задачи. При выполнении hello [ParallelTasks] [ parallel_tasks_sample] образец приложения, можно использовать функции tooeasily hello тепловой карты визуализировать hello исполнение параллельных задач на каждом узле.

![Тепловая карта обозревателя пакетной службы][1]

*Тепловая карта обозревателя пакетной службы, отображающая пул из четырех узлов, на каждом из которых выполняется четыре задачи.*

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[enable_autoscaling]: https://msdn.microsoft.com/library/azure/dn820173.aspx
[fill_type]: https://msdn.microsoft.com/library/microsoft.azure.batch.common.computenodefilltype.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[maxtasks_net]: http://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.maxtaskspercomputenode.aspx
[rest_addpool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[parallel_tasks_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/ParallelTasks
[poolcreate_net]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[task_schedule]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudpool.taskschedulingpolicy.aspx

[1]: ./media/batch-parallel-node-tasks\heat_map.png
