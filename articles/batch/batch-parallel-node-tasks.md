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
# <a name="run-tasks-concurrently-toomaximize-usage-of-batch-compute-nodes"></a><span data-ttu-id="8d7e0-103">Выполнение задач одновременно toomaximize использование пакетных вычислительных узлов</span><span class="sxs-lookup"><span data-stu-id="8d7e0-103">Run tasks concurrently toomaximize usage of Batch compute nodes</span></span> 

<span data-ttu-id="8d7e0-104">При одновременной более одной задачи на каждом вычислительном узле в пуле пакетной службы Azure, можно увеличить использование ресурсов на меньшее число узлов в пул hello.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-104">By running more than one task simultaneously on each compute node in your Azure Batch pool, you can maximize resource usage on a smaller number of nodes in hello pool.</span></span> <span data-ttu-id="8d7e0-105">Для некоторых рабочих нагрузок это позволит сократить время выполнения заданий и уменьшить затраты.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-105">For some workloads, this can result in shorter job times and lower cost.</span></span>

<span data-ttu-id="8d7e0-106">При некоторых сценариях преимущества выделять все узла в ресурсы tooa одну задачу, позволяя несколько задач tooshare эти ресурсы различных ситуаций с более эффективно:</span><span class="sxs-lookup"><span data-stu-id="8d7e0-106">While some scenarios benefit from dedicating all of a node's resources tooa single task, several situations benefit from allowing multiple tasks tooshare those resources:</span></span>

* <span data-ttu-id="8d7e0-107">**Минимизация передачи данных** при задачи — это может tooshare данных.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-107">**Minimizing data transfer** when tasks are able tooshare data.</span></span> <span data-ttu-id="8d7e0-108">В этом сценарии можно значительно снизить расходы по передаче данных путем копирования общих данных tooa меньшее число узлов, а затем выполняя задачи параллельно на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-108">In this scenario, you can dramatically reduce data transfer charges by copying shared data tooa smaller number of nodes and executing tasks in parallel on each node.</span></span> <span data-ttu-id="8d7e0-109">Это особенно относится узла копируются tooeach toobe данных hello должны передаваться между географических регионов.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-109">This especially applies if hello data toobe copied tooeach node must be transferred between geographic regions.</span></span>
* <span data-ttu-id="8d7e0-110">**повышается эффективность использования памяти** .</span><span class="sxs-lookup"><span data-stu-id="8d7e0-110">**Maximizing memory usage** when tasks require a large amount of memory, but only during short periods of time, and at variable times during execution.</span></span> <span data-ttu-id="8d7e0-111">Можно использовать меньше, но большего размера, вычислительные узлы с дополнительные tooefficiently памяти обработки таких пиков.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-111">You can employ fewer, but larger, compute nodes with more memory tooefficiently handle such spikes.</span></span> <span data-ttu-id="8d7e0-112">Эти узлы будут иметь несколько задач, выполняющихся в параллельном режиме на каждом узле, но каждая задача будет использовать узлы hello много памяти в разное время.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-112">These nodes would have multiple tasks running in parallel on each node, but each task would take advantage of hello nodes' plentiful memory at different times.</span></span>
* <span data-ttu-id="8d7e0-113">**уменьшается ограничение по количеству узлов** .</span><span class="sxs-lookup"><span data-stu-id="8d7e0-113">**Mitigating node number limits** when inter-node communication is required within a pool.</span></span> <span data-ttu-id="8d7e0-114">В настоящее время пулы, настроенных для взаимодействия между узлами — ограниченный too50 вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-114">Currently, pools configured for inter-node communication are limited too50 compute nodes.</span></span> <span data-ttu-id="8d7e0-115">Если каждый узел в такой пул может tooexecute задачи параллельно, с увеличением количества задач могут выполняться одновременно.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-115">If each node in such a pool is able tooexecute tasks in parallel, a greater number of tasks can be executed simultaneously.</span></span>
* <span data-ttu-id="8d7e0-116">**Репликация на локальный вычислительный кластер**, например при переносе сначала tooAzure среды вычислений.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-116">**Replicating an on-premises compute cluster**, such as when you first move a compute environment tooAzure.</span></span> <span data-ttu-id="8d7e0-117">Если текущее решение локальной выполняет несколько задач на вычислительном узле, можно увеличить максимальное количество hello узла задач toomore точно отражают этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-117">If your current on-premises solution executes multiple tasks per compute node, you can increase hello maximum number of node tasks toomore closely mirror that configuration.</span></span>

## <a name="example-scenario"></a><span data-ttu-id="8d7e0-118">Пример сценария</span><span class="sxs-lookup"><span data-stu-id="8d7e0-118">Example scenario</span></span>
<span data-ttu-id="8d7e0-119">Как tooillustrate пример hello преимущества выполнения параллельных задач, например, в приложении задачи есть требования к ЦП и памяти таким образом, что [Стандартная\_D1](../cloud-services/cloud-services-sizes-specs.md) узлы являются достаточно.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-119">As an example tooillustrate hello benefits of parallel task execution, let's say that your task application has CPU and memory requirements such that [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodes are sufficient.</span></span> <span data-ttu-id="8d7e0-120">Однако в toofinish hello задание времени требуется hello, необходимы 1000 этих узлов.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-120">But, in order toofinish hello job in hello required time, 1,000 of these nodes are needed.</span></span>

<span data-ttu-id="8d7e0-121">Вместо узлов размера Standard\_D1, каждый из которых содержит одно ядро ЦП, вы можете использовать 16-ядерные узлы [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md), включив на них параллельное выполнение задач.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-121">Instead of using Standard\_D1 nodes that have 1 CPU core, you could use [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes that have 16 cores each, and enable parallel task execution.</span></span> <span data-ttu-id="8d7e0-122">Таким образом, потребуется *в 16 раз меньше узлов* , то есть 63 узла вместо 1000.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-122">Therefore, *16 times fewer nodes* could be used--instead of 1,000 nodes, only 63 would be required.</span></span> <span data-ttu-id="8d7e0-123">Кроме того Если требуются файлы большого приложения или ссылочные данные для каждого узла, длительность задания и эффективность снова улучшение поскольку hello данные копируются tooonly 16 узлов.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-123">Additionally, if large application files or reference data are required for each node, job duration and efficiency are again improved since hello data is copied tooonly 16 nodes.</span></span>

## <a name="enable-parallel-task-execution"></a><span data-ttu-id="8d7e0-124">Включение параллельного выполнения задач</span><span class="sxs-lookup"><span data-stu-id="8d7e0-124">Enable parallel task execution</span></span>
<span data-ttu-id="8d7e0-125">На уровне пула hello настроить вычислительные узлы для выполнения параллельных задач.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-125">You configure compute nodes for parallel task execution at hello pool level.</span></span> <span data-ttu-id="8d7e0-126">Библиотека .NET пакета hello, установите hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] свойства при создании пула.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-126">With hello Batch .NET library, set hello [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property when you create a pool.</span></span> <span data-ttu-id="8d7e0-127">При использовании API REST пакета hello задать hello [maxTasksPerNode] [ rest_addpool] элемент в тексте запроса hello во время создания пула.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-127">If you are using hello Batch REST API, set hello [maxTasksPerNode][rest_addpool] element in hello request body during pool creation.</span></span>

<span data-ttu-id="8d7e0-128">Пакет Azure позволяет tooset максимальное число задач на каждом узле toofour раз (4 x) hello число ядер на узел.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-128">Azure Batch allows you tooset maximum tasks per node up toofour times (4x) hello number of node cores.</span></span> <span data-ttu-id="8d7e0-129">Например, если hello пула настраивается узлы размер «Большой» (4 ядра), затем `maxTasksPerNode` может задаваться too16.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-129">For example, if hello pool is configured with nodes of size "Large" (four cores), then `maxTasksPerNode` may be set too16.</span></span> <span data-ttu-id="8d7e0-130">Дополнительные сведения о hello количество ядер для каждого из размеров hello узла см [размеров для облачных служб](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="8d7e0-130">For details on hello number of cores for each of hello node sizes, see [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span> <span data-ttu-id="8d7e0-131">Дополнительные сведения об ограничениях службы см. в разделе [квоты и лимиты для пакетной службы Azure hello](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="8d7e0-131">For more information on service limits, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span>

> [!TIP]
> <span data-ttu-id="8d7e0-132">Быть tootake убедиться, что в учетной записи hello `maxTasksPerNode` значение при создании [формула автоматического масштабирования] [ enable_autoscaling] для пула.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-132">Be sure tootake into account hello `maxTasksPerNode` value when you construct an [autoscale formula][enable_autoscaling] for your pool.</span></span> <span data-ttu-id="8d7e0-133">Например, если в формуле учитывается параметр `$RunningTasks`, изменение количества задач существенно повлияет на результат ее применения.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-133">For example, a formula that evaluates `$RunningTasks` could be dramatically affected by an increase in tasks per node.</span></span> <span data-ttu-id="8d7e0-134">Дополнительные сведения см. в статье [Автоматическое масштабирование вычислительных узлов в пуле пакетной службы Azure](batch-automatic-scaling.md).</span><span class="sxs-lookup"><span data-stu-id="8d7e0-134">See [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) for more information.</span></span>
>
>

## <a name="distribution-of-tasks"></a><span data-ttu-id="8d7e0-135">Распределение задач</span><span class="sxs-lookup"><span data-stu-id="8d7e0-135">Distribution of tasks</span></span>
<span data-ttu-id="8d7e0-136">При hello вычислительных узлов в пуле задачи могут выполняться параллельно, очень важно toospecify способ toobe задачи hello, распределенные по узлам hello в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-136">When hello compute nodes in a pool can execute tasks concurrently, it's important toospecify how you want hello tasks toobe distributed across hello nodes in hello pool.</span></span>

<span data-ttu-id="8d7e0-137">С помощью hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] свойства, можно указать, что задачи следует назначать равномерно по всем узлам в пуле hello («распространение»).</span><span class="sxs-lookup"><span data-stu-id="8d7e0-137">By using hello [CloudPool.TaskSchedulingPolicy][task_schedule] property, you can specify that tasks should be assigned evenly across all nodes in hello pool ("spreading").</span></span> <span data-ttu-id="8d7e0-138">Или можно указать, что число задач должен выделяться tooeach узел перед задач, назначенных tooanother узла в пуле hello («упаковочный»).</span><span class="sxs-lookup"><span data-stu-id="8d7e0-138">Or you can specify that as many tasks as possible should be assigned tooeach node before tasks are assigned tooanother node in hello pool ("packing").</span></span>

<span data-ttu-id="8d7e0-139">В качестве примера как полезно использовать эту функцию, рассмотрим hello пула [Стандартная\_D14](../cloud-services/cloud-services-sizes-specs.md) узлов (в приведенном выше примере hello), которые настроены с [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] значение 16.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-139">As an example of how this feature is valuable, consider hello pool of [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes (in hello example above) that is configured with a [CloudPool.MaxTasksPerComputeNode][maxtasks_net] value of 16.</span></span> <span data-ttu-id="8d7e0-140">Если hello [CloudPool.TaskSchedulingPolicy] [ task_schedule] оснащен [ComputeNodeFillType] [ fill_type] из *пакет*, будет максимизации использования всех 16 ядер каждого узла и разрешить [автоматическое масштабирование пула](batch-automatic-scaling.md) tooprune неиспользуемые узлы из пула hello (узлы без назначенных задач).</span><span class="sxs-lookup"><span data-stu-id="8d7e0-140">If hello [CloudPool.TaskSchedulingPolicy][task_schedule] is configured with a [ComputeNodeFillType][fill_type] of *Pack*, it would maximize usage of all 16 cores of each node and allow an [autoscaling pool](batch-automatic-scaling.md) tooprune unused nodes from hello pool (nodes without any tasks assigned).</span></span> <span data-ttu-id="8d7e0-141">Это снизит использование ресурсов и расходы на них.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-141">This minimizes resource usage and saves money.</span></span>

## <a name="batch-net-example"></a><span data-ttu-id="8d7e0-142">Пример использования компонента .NET пакетной службы</span><span class="sxs-lookup"><span data-stu-id="8d7e0-142">Batch .NET example</span></span>
<span data-ttu-id="8d7e0-143">Это [пакета .NET] [ api_net] API фрагмент кода показывает toocreate запрос пула, который содержит четыре больших узлы с не более четырех задач на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-143">This [Batch .NET][api_net] API code snippet shows a request toocreate a pool that contains four large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="8d7e0-144">Он указывает задачи планирования политики, который будет заполнять каждый узел с узлом tooanother задачи tooassigning предыдущие задачи в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-144">It specifies a task scheduling policy that will fill each node with tasks prior tooassigning tasks tooanother node in hello pool.</span></span> <span data-ttu-id="8d7e0-145">Дополнительные сведения о добавлении пулы с помощью пакета .NET API hello. в разделе [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span><span class="sxs-lookup"><span data-stu-id="8d7e0-145">For more information on adding pools by using hello Batch .NET API, see [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span></span>

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

## <a name="batch-rest-example"></a><span data-ttu-id="8d7e0-146">Пример интерфейса REST API пакетной службы</span><span class="sxs-lookup"><span data-stu-id="8d7e0-146">Batch REST example</span></span>
<span data-ttu-id="8d7e0-147">Это [REST пакетной] [ api_rest] API фрагменте показано toocreate запрос пула, содержащего два больших узла с не более четырех задач на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-147">This [Batch REST][api_rest] API snippet shows a request toocreate a pool that contains two large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="8d7e0-148">Дополнительные сведения о добавлении пулы с помощью API-интерфейса REST hello. в разделе [добавить учетную запись пула tooan][rest_addpool].</span><span class="sxs-lookup"><span data-stu-id="8d7e0-148">For more information on adding pools by using hello REST API, see [Add a pool tooan account][rest_addpool].</span></span>

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
> <span data-ttu-id="8d7e0-149">Можно задать hello `maxTasksPerNode` элемент и [MaxTasksPerComputeNode] [ maxtasks_net] свойства только во время создания пула.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-149">You can set hello `maxTasksPerNode` element and [MaxTasksPerComputeNode][maxtasks_net] property only at pool creation time.</span></span> <span data-ttu-id="8d7e0-150">Их невозможно изменить после создания пула.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-150">They cannot be modified after a pool has already been created.</span></span>
>
>

## <a name="code-sample"></a><span data-ttu-id="8d7e0-151">Пример кода</span><span class="sxs-lookup"><span data-stu-id="8d7e0-151">Code sample</span></span>
<span data-ttu-id="8d7e0-152">Hello [ParallelNodeTasks] [ parallel_tasks_sample] проекта на GitHub иллюстрирует использование hello hello [CloudPool.MaxTasksPerComputeNode] [ maxtasks_net] свойство.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-152">hello [ParallelNodeTasks][parallel_tasks_sample] project on GitHub illustrates hello use of hello [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property.</span></span>

<span data-ttu-id="8d7e0-153">Это консольное приложение C# использует hello [пакета .NET] [ api_net] toocreate библиотеки пула с одним или несколькими вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-153">This C# console application uses hello [Batch .NET][api_net] library toocreate a pool with one or more compute nodes.</span></span> <span data-ttu-id="8d7e0-154">Он выполняет ряд задач, можно настроить на эти узлы toosimulate переменная нагрузка.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-154">It executes a configurable number of tasks on those nodes toosimulate variable load.</span></span> <span data-ttu-id="8d7e0-155">Выход из приложения hello определяет, какие узлы выполнения каждой задачи.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-155">Output from hello application specifies which nodes executed each task.</span></span> <span data-ttu-id="8d7e0-156">приложение Hello также описаны основные параметры задания hello и длительность.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-156">hello application also provides a summary of hello job parameters and duration.</span></span> <span data-ttu-id="8d7e0-157">Сводка часть Hello hello выходные данные двух разных запусках пример приложения hello появляется внизу.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-157">hello summary portion of hello output from two different runs of hello sample application appears below.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

<span data-ttu-id="8d7e0-158">Hello первого выполнения образца приложения hello показывает, что с одним узлом в пуле hello и по умолчанию hello одной задачи на каждом узле, продолжительность задания hello составляет более 30 минут.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-158">hello first execution of hello sample application shows that with a single node in hello pool and hello default setting of one task per node, hello job duration is over 30 minutes.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

<span data-ttu-id="8d7e0-159">Второй запуск отображается образец hello к значительному снижению длительности задания Hello.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-159">hello second run of hello sample shows a significant decrease in job duration.</span></span> <span data-ttu-id="8d7e0-160">Это происходит потому hello пула была настроена с помощью четырех задач на узел, который позволяет почти квартала hello времени toocomplete hello параллельной задачи выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-160">This is because hello pool was configured with four tasks per node, which allows for parallel task execution toocomplete hello job in nearly a quarter of hello time.</span></span>

> [!NOTE]
> <span data-ttu-id="8d7e0-161">Длительность задания Hello в сводках hello выше, не включайте время создания пула.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-161">hello job durations in hello summaries above do not include pool creation time.</span></span> <span data-ttu-id="8d7e0-162">Каждое из заданий hello выше был отправленной toopreviously создания пулов, вычислительные узлы были в hello *Idle* состояния во время передачи.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-162">Each of hello jobs above was submitted toopreviously created pools whose compute nodes were in hello *Idle* state at submission time.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="8d7e0-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8d7e0-163">Next steps</span></span>
### <a name="batch-explorer-heat-map"></a><span data-ttu-id="8d7e0-164">Тепловая карта обозревателя пакетной службы</span><span class="sxs-lookup"><span data-stu-id="8d7e0-164">Batch Explorer Heat Map</span></span>
<span data-ttu-id="8d7e0-165">Hello [обозреватель пакета Azure][batch_explorer], один из hello пакетной службы Azure [образцы приложений][github_samples], содержит *тепловой карты* компонент, который предоставляет визуализации выполнения задачи.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-165">hello [Azure Batch Explorer][batch_explorer], one of hello Azure Batch [sample applications][github_samples], contains a *Heat Map* feature that provides visualization of task execution.</span></span> <span data-ttu-id="8d7e0-166">При выполнении hello [ParallelTasks] [ parallel_tasks_sample] образец приложения, можно использовать функции tooeasily hello тепловой карты визуализировать hello исполнение параллельных задач на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="8d7e0-166">When you're executing hello [ParallelTasks][parallel_tasks_sample] sample application, you can use hello Heat Map feature tooeasily visualize hello execution of parallel tasks on each node.</span></span>

![Тепловая карта обозревателя пакетной службы][1]

<span data-ttu-id="8d7e0-168">*Тепловая карта обозревателя пакетной службы, отображающая пул из четырех узлов, на каждом из которых выполняется четыре задачи.*</span><span class="sxs-lookup"><span data-stu-id="8d7e0-168">*Batch Explorer Heat Map showing a pool of four nodes, with each node currently executing four tasks*</span></span>

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
