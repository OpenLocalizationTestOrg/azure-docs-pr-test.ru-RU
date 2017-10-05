---
title: "Параллельное выполнение задач для эффективного использования вычислительных ресурсов пакетной службы Azure | Документация Майкрософт"
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
ms.openlocfilehash: 6903552d907a1ddb21d3b678e2d224b4b5e35b77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="run-tasks-concurrently-to-maximize-usage-of-batch-compute-nodes"></a><span data-ttu-id="0b014-103">Параллельное выполнение задач для эффективного использования вычислительных узлов пакетной службы</span><span class="sxs-lookup"><span data-stu-id="0b014-103">Run tasks concurrently to maximize usage of Batch compute nodes</span></span> 

<span data-ttu-id="0b014-104">Выполняя несколько задач одновременно на каждом вычислительном узле в пуле пакетной службы Azure, можно увеличить использование ресурсов при меньшем количестве узлов в пуле.</span><span class="sxs-lookup"><span data-stu-id="0b014-104">By running more than one task simultaneously on each compute node in your Azure Batch pool, you can maximize resource usage on a smaller number of nodes in the pool.</span></span> <span data-ttu-id="0b014-105">Для некоторых рабочих нагрузок это позволит сократить время выполнения заданий и уменьшить затраты.</span><span class="sxs-lookup"><span data-stu-id="0b014-105">For some workloads, this can result in shorter job times and lower cost.</span></span>

<span data-ttu-id="0b014-106">Во многих случаях выгоднее использовать все ресурсы узла для выполнения одной задачи. Но для нескольких ситуаций совместное использование ресурсов несколькими задачами дает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="0b014-106">While some scenarios benefit from dedicating all of a node's resources to a single task, several situations benefit from allowing multiple tasks to share those resources:</span></span>

* <span data-ttu-id="0b014-107">**уменьшается объем передачи данных** .</span><span class="sxs-lookup"><span data-stu-id="0b014-107">**Minimizing data transfer** when tasks are able to share data.</span></span> <span data-ttu-id="0b014-108">В этом сценарии можно существенно сократить стоимость передачи данных, копируя общие данные на меньшее количество узлов и выполняя задачи в параллельном режиме на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="0b014-108">In this scenario, you can dramatically reduce data transfer charges by copying shared data to a smaller number of nodes and executing tasks in parallel on each node.</span></span> <span data-ttu-id="0b014-109">Это особенно актуально, если данные, которые копируются на каждый узел, необходимо передавать между географическими регионами.</span><span class="sxs-lookup"><span data-stu-id="0b014-109">This especially applies if the data to be copied to each node must be transferred between geographic regions.</span></span>
* <span data-ttu-id="0b014-110">**повышается эффективность использования памяти** .</span><span class="sxs-lookup"><span data-stu-id="0b014-110">**Maximizing memory usage** when tasks require a large amount of memory, but only during short periods of time, and at variable times during execution.</span></span> <span data-ttu-id="0b014-111">Для эффективной обработки таких нагрузок можно использовать меньшее число более крупных вычислительных узлов с большим объемом памяти.</span><span class="sxs-lookup"><span data-stu-id="0b014-111">You can employ fewer, but larger, compute nodes with more memory to efficiently handle such spikes.</span></span> <span data-ttu-id="0b014-112">Эти узлы могли бы иметь параллельные задачи, которые выполняются на каждом узле, но каждая задача использовала бы большой объем памяти узлов в разное время.</span><span class="sxs-lookup"><span data-stu-id="0b014-112">These nodes would have multiple tasks running in parallel on each node, but each task would take advantage of the nodes' plentiful memory at different times.</span></span>
* <span data-ttu-id="0b014-113">**уменьшается ограничение по количеству узлов** .</span><span class="sxs-lookup"><span data-stu-id="0b014-113">**Mitigating node number limits** when inter-node communication is required within a pool.</span></span> <span data-ttu-id="0b014-114">Сейчас существует ограничение в 50 вычислительных узлов для пулов, в которых настроен обмен данными между узлами.</span><span class="sxs-lookup"><span data-stu-id="0b014-114">Currently, pools configured for inter-node communication are limited to 50 compute nodes.</span></span> <span data-ttu-id="0b014-115">Поэтому если каждый узел в таком пуле будет выполнять задачи параллельно, можно будет выполнять больше задач одновременно.</span><span class="sxs-lookup"><span data-stu-id="0b014-115">If each node in such a pool is able to execute tasks in parallel, a greater number of tasks can be executed simultaneously.</span></span>
* <span data-ttu-id="0b014-116">**Выполняется репликация локального вычислительного кластера**, например, как при первичном переходе в вычислительную среду Azure.</span><span class="sxs-lookup"><span data-stu-id="0b014-116">**Replicating an on-premises compute cluster**, such as when you first move a compute environment to Azure.</span></span> <span data-ttu-id="0b014-117">Увеличение максимального числа задач на узле позволит точнее скопировать существующую физическую конфигурацию, если текущее локальное решение позволяет выполнять несколько задач на каждом вычислительном узле.</span><span class="sxs-lookup"><span data-stu-id="0b014-117">If your current on-premises solution executes multiple tasks per compute node, you can increase the maximum number of node tasks to more closely mirror that configuration.</span></span>

## <a name="example-scenario"></a><span data-ttu-id="0b014-118">Пример сценария</span><span class="sxs-lookup"><span data-stu-id="0b014-118">Example scenario</span></span>
<span data-ttu-id="0b014-119">Чтобы продемонстрировать преимущества параллельного выполнения задач, рассмотрим такой пример. Допустим, ваше приложение имеет такие требования к ЦП и памяти, что для его работы достаточно узла размера [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="0b014-119">As an example to illustrate the benefits of parallel task execution, let's say that your task application has CPU and memory requirements such that [Standard\_D1](../cloud-services/cloud-services-sizes-specs.md) nodes are sufficient.</span></span> <span data-ttu-id="0b014-120">Однако для выполнения задачи в заданное время потребуется 1000 таких узлов.</span><span class="sxs-lookup"><span data-stu-id="0b014-120">But, in order to finish the job in the required time, 1,000 of these nodes are needed.</span></span>

<span data-ttu-id="0b014-121">Вместо узлов размера Standard\_D1, каждый из которых содержит одно ядро ЦП, вы можете использовать 16-ядерные узлы [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md), включив на них параллельное выполнение задач.</span><span class="sxs-lookup"><span data-stu-id="0b014-121">Instead of using Standard\_D1 nodes that have 1 CPU core, you could use [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes that have 16 cores each, and enable parallel task execution.</span></span> <span data-ttu-id="0b014-122">Таким образом, потребуется *в 16 раз меньше узлов* , то есть 63 узла вместо 1000.</span><span class="sxs-lookup"><span data-stu-id="0b014-122">Therefore, *16 times fewer nodes* could be used--instead of 1,000 nodes, only 63 would be required.</span></span> <span data-ttu-id="0b014-123">Кроме того, если каждому узлу требуются большие файлы приложений либо эталонные данные, время выполнения и эффективность будут улучшены, так как данные будут копироваться только на 16 узлов.</span><span class="sxs-lookup"><span data-stu-id="0b014-123">Additionally, if large application files or reference data are required for each node, job duration and efficiency are again improved since the data is copied to only 16 nodes.</span></span>

## <a name="enable-parallel-task-execution"></a><span data-ttu-id="0b014-124">Включение параллельного выполнения задач</span><span class="sxs-lookup"><span data-stu-id="0b014-124">Enable parallel task execution</span></span>
<span data-ttu-id="0b014-125">Настройка параллельного выполнения задач для вычислительных узлов выполняется на уровне пула.</span><span class="sxs-lookup"><span data-stu-id="0b014-125">You configure compute nodes for parallel task execution at the pool level.</span></span> <span data-ttu-id="0b014-126">С помощью библиотеки .NET пакетной службы задайте свойство [CloudPool.MaxTasksPerComputeNode][maxtasks_net] при создании пула.</span><span class="sxs-lookup"><span data-stu-id="0b014-126">With the Batch .NET library, set the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property when you create a pool.</span></span> <span data-ttu-id="0b014-127">Если вы используете REST API пакетной службы, включите элемент [maxTasksPerNode][rest_addpool] в текст запроса при создании пула.</span><span class="sxs-lookup"><span data-stu-id="0b014-127">If you are using the Batch REST API, set the [maxTasksPerNode][rest_addpool] element in the request body during pool creation.</span></span>

<span data-ttu-id="0b014-128">Пакетная служба Azure позволяет задать для каждого узла максимальное количество задач, в 4 раза превышающее количество ядер узла.</span><span class="sxs-lookup"><span data-stu-id="0b014-128">Azure Batch allows you to set maximum tasks per node up to four times (4x) the number of node cores.</span></span> <span data-ttu-id="0b014-129">Например, если для пула настроены узлы размера "Большой" (четыре ядра), для параметра `maxTasksPerNode` можно задать значение 16.</span><span class="sxs-lookup"><span data-stu-id="0b014-129">For example, if the pool is configured with nodes of size "Large" (four cores), then `maxTasksPerNode` may be set to 16.</span></span> <span data-ttu-id="0b014-130">Сведения о количестве ядер для каждого узла см. в статье [Размеры для облачных служб](../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="0b014-130">For details on the number of cores for each of the node sizes, see [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md).</span></span> <span data-ttu-id="0b014-131">Дополнительные сведения об ограничениях службы см. в статье [Квоты и ограничения пакетной службы Azure](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="0b014-131">For more information on service limits, see [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span>

> [!TIP]
> <span data-ttu-id="0b014-132">Обязательно учитывайте значение параметра `maxTasksPerNode` при создании [формулы автомасштабирования][enable_autoscaling] для пула.</span><span class="sxs-lookup"><span data-stu-id="0b014-132">Be sure to take into account the `maxTasksPerNode` value when you construct an [autoscale formula][enable_autoscaling] for your pool.</span></span> <span data-ttu-id="0b014-133">Например, если в формуле учитывается параметр `$RunningTasks`, изменение количества задач существенно повлияет на результат ее применения.</span><span class="sxs-lookup"><span data-stu-id="0b014-133">For example, a formula that evaluates `$RunningTasks` could be dramatically affected by an increase in tasks per node.</span></span> <span data-ttu-id="0b014-134">Дополнительные сведения см. в статье [Автоматическое масштабирование вычислительных узлов в пуле пакетной службы Azure](batch-automatic-scaling.md).</span><span class="sxs-lookup"><span data-stu-id="0b014-134">See [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) for more information.</span></span>
>
>

## <a name="distribution-of-tasks"></a><span data-ttu-id="0b014-135">Распределение задач</span><span class="sxs-lookup"><span data-stu-id="0b014-135">Distribution of tasks</span></span>
<span data-ttu-id="0b014-136">Если вычислительные узлы в пуле могут выполнять задачи параллельно, важно указать правила распределения задач между узлами пула.</span><span class="sxs-lookup"><span data-stu-id="0b014-136">When the compute nodes in a pool can execute tasks concurrently, it's important to specify how you want the tasks to be distributed across the nodes in the pool.</span></span>

<span data-ttu-id="0b014-137">С помощью свойства [CloudPool.TaskSchedulingPolicy][task_schedule] можно указать, что задачи должны назначаться ("распространяться") равномерно по всем узлам в кластере.</span><span class="sxs-lookup"><span data-stu-id="0b014-137">By using the [CloudPool.TaskSchedulingPolicy][task_schedule] property, you can specify that tasks should be assigned evenly across all nodes in the pool ("spreading").</span></span> <span data-ttu-id="0b014-138">Или можно указать, что перед переходом к следующему узлу необходимо назначить максимальное количество задач текущему узлу ("упаковка").</span><span class="sxs-lookup"><span data-stu-id="0b014-138">Or you can specify that as many tasks as possible should be assigned to each node before tasks are assigned to another node in the pool ("packing").</span></span>

<span data-ttu-id="0b014-139">Чтобы понять важность этой функции, давайте рассмотрим пул из предыдущего примера. Он состоит из узлов размера [Standard_Standard\_D14](../cloud-services/cloud-services-sizes-specs.md), для которых параметр [CloudPool.MaxTasksPerComputeNode][maxtasks_net] имеет значение 16.</span><span class="sxs-lookup"><span data-stu-id="0b014-139">As an example of how this feature is valuable, consider the pool of [Standard\_D14](../cloud-services/cloud-services-sizes-specs.md) nodes (in the example above) that is configured with a [CloudPool.MaxTasksPerComputeNode][maxtasks_net] value of 16.</span></span> <span data-ttu-id="0b014-140">Если в свойстве [CloudPool.TaskSchedulingPolicy][task_schedule] для параметра [ComputeNodeFillType][fill_type] будет указано значение *Pack*, то на каждом узле все 16 ядер будут задействованы по максимуму. При этом [автомасштабируемый пул](batch-automatic-scaling.md) будет исключать неиспользуемые узлы (для которых не назначены задачи).</span><span class="sxs-lookup"><span data-stu-id="0b014-140">If the [CloudPool.TaskSchedulingPolicy][task_schedule] is configured with a [ComputeNodeFillType][fill_type] of *Pack*, it would maximize usage of all 16 cores of each node and allow an [autoscaling pool](batch-automatic-scaling.md) to prune unused nodes from the pool (nodes without any tasks assigned).</span></span> <span data-ttu-id="0b014-141">Это снизит использование ресурсов и расходы на них.</span><span class="sxs-lookup"><span data-stu-id="0b014-141">This minimizes resource usage and saves money.</span></span>

## <a name="batch-net-example"></a><span data-ttu-id="0b014-142">Пример использования компонента .NET пакетной службы</span><span class="sxs-lookup"><span data-stu-id="0b014-142">Batch .NET example</span></span>
<span data-ttu-id="0b014-143">Этот фрагмент кода API [.NET пакетной службы][api_net] содержит запрос на создание пула с четырьмя большими узлами и максимальным количеством задач на каждый узел, равным четырем.</span><span class="sxs-lookup"><span data-stu-id="0b014-143">This [Batch .NET][api_net] API code snippet shows a request to create a pool that contains four large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="0b014-144">Он задает политику планирования задач, при которой каждому узлу назначается максимальное количество задач перед переходом к следующему узлу пула.</span><span class="sxs-lookup"><span data-stu-id="0b014-144">It specifies a task scheduling policy that will fill each node with tasks prior to assigning tasks to another node in the pool.</span></span> <span data-ttu-id="0b014-145">Дополнительные сведения о добавлении пулов с использованием API .NET пакетной службы см. в описании метода [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span><span class="sxs-lookup"><span data-stu-id="0b014-145">For more information on adding pools by using the Batch .NET API, see [BatchClient.PoolOperations.CreatePool][poolcreate_net].</span></span>

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

## <a name="batch-rest-example"></a><span data-ttu-id="0b014-146">Пример интерфейса REST API пакетной службы</span><span class="sxs-lookup"><span data-stu-id="0b014-146">Batch REST example</span></span>
<span data-ttu-id="0b014-147">Этот фрагмент кода для [REST API пакетной службы][api_rest] содержит запрос на создание пула с двумя большими узлами и максимальным количеством задач на каждый узел, равным четырем.</span><span class="sxs-lookup"><span data-stu-id="0b014-147">This [Batch REST][api_rest] API snippet shows a request to create a pool that contains two large nodes with a maximum of four tasks per node.</span></span> <span data-ttu-id="0b014-148">Дополнительные сведения о добавлении пулов с помощью REST API см. в статье [Добавление пула к учетной записи][rest_addpool].</span><span class="sxs-lookup"><span data-stu-id="0b014-148">For more information on adding pools by using the REST API, see [Add a pool to an account][rest_addpool].</span></span>

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
> <span data-ttu-id="0b014-149">Элемент `maxTasksPerNode` и свойство [MaxTasksPerComputeNode][maxtasks_net] можно задать только во время создания пула.</span><span class="sxs-lookup"><span data-stu-id="0b014-149">You can set the `maxTasksPerNode` element and [MaxTasksPerComputeNode][maxtasks_net] property only at pool creation time.</span></span> <span data-ttu-id="0b014-150">Их невозможно изменить после создания пула.</span><span class="sxs-lookup"><span data-stu-id="0b014-150">They cannot be modified after a pool has already been created.</span></span>
>
>

## <a name="code-sample"></a><span data-ttu-id="0b014-151">Пример кода</span><span class="sxs-lookup"><span data-stu-id="0b014-151">Code sample</span></span>
<span data-ttu-id="0b014-152">Проект [ParallelNodeTasks][parallel_tasks_sample] в репозитории GitHub является примером использования свойства [CloudPool.MaxTasksPerComputeNode][maxtasks_net].</span><span class="sxs-lookup"><span data-stu-id="0b014-152">The [ParallelNodeTasks][parallel_tasks_sample] project on GitHub illustrates the use of the [CloudPool.MaxTasksPerComputeNode][maxtasks_net] property.</span></span>

<span data-ttu-id="0b014-153">Это консольное приложение C# использует библиотеку [.NET пакетной службы][api_net] для создания пула с одним или несколькими вычислительными узлами.</span><span class="sxs-lookup"><span data-stu-id="0b014-153">This C# console application uses the [Batch .NET][api_net] library to create a pool with one or more compute nodes.</span></span> <span data-ttu-id="0b014-154">Для имитации переменной нагрузки оно выполняет заданное количество задач на этих узлах.</span><span class="sxs-lookup"><span data-stu-id="0b014-154">It executes a configurable number of tasks on those nodes to simulate variable load.</span></span> <span data-ttu-id="0b014-155">Вывод приложения указывает, на каких узлах выполнялась каждая задача.</span><span class="sxs-lookup"><span data-stu-id="0b014-155">Output from the application specifies which nodes executed each task.</span></span> <span data-ttu-id="0b014-156">Приложение также предоставляет сводку параметров задания и времени его выполнения.</span><span class="sxs-lookup"><span data-stu-id="0b014-156">The application also provides a summary of the job parameters and duration.</span></span> <span data-ttu-id="0b014-157">Ниже приводится часть сводки выходных данных примера приложения по двум различным запускам.</span><span class="sxs-lookup"><span data-stu-id="0b014-157">The summary portion of the output from two different runs of the sample application appears below.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 1
Tasks: 32
Duration: 00:30:01.4638023
```

<span data-ttu-id="0b014-158">Первый запуск примера приложения показывает, что с одним узлом в пуле и с одной задачей на узел (настройка по умолчанию) на выполнение задания потребовалось более 30 минут.</span><span class="sxs-lookup"><span data-stu-id="0b014-158">The first execution of the sample application shows that with a single node in the pool and the default setting of one task per node, the job duration is over 30 minutes.</span></span>

```
Nodes: 1
Node size: large
Max tasks per node: 4
Tasks: 32
Duration: 00:08:48.2423500
```

<span data-ttu-id="0b014-159">Второй запуск примера показывает значительное уменьшение времени выполнения задания.</span><span class="sxs-lookup"><span data-stu-id="0b014-159">The second run of the sample shows a significant decrease in job duration.</span></span> <span data-ttu-id="0b014-160">Это вызвано тем, что пул был настроен с четырьмя задачами на узел, что позволяет параллельно выполнять задачи для выполнения задания примерно за четверть исходного времени.</span><span class="sxs-lookup"><span data-stu-id="0b014-160">This is because the pool was configured with four tasks per node, which allows for parallel task execution to complete the job in nearly a quarter of the time.</span></span>

> [!NOTE]
> <span data-ttu-id="0b014-161">В приведенных выше сводках длительность выполнения задания не включает время создания пула.</span><span class="sxs-lookup"><span data-stu-id="0b014-161">The job durations in the summaries above do not include pool creation time.</span></span> <span data-ttu-id="0b014-162">Каждое из заданий в примерах выше отправлялось в уже созданные пулы, вычислительные узлы которых на момент отправки находились в состоянии *простоя* .</span><span class="sxs-lookup"><span data-stu-id="0b014-162">Each of the jobs above was submitted to previously created pools whose compute nodes were in the *Idle* state at submission time.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="0b014-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0b014-163">Next steps</span></span>
### <a name="batch-explorer-heat-map"></a><span data-ttu-id="0b014-164">Тепловая карта обозревателя пакетной службы</span><span class="sxs-lookup"><span data-stu-id="0b014-164">Batch Explorer Heat Map</span></span>
<span data-ttu-id="0b014-165">В списке [примеров приложений][github_samples] пакетной службы Azure есть [Azure Batch Explorer][batch_explorer]. Он содержит компонент *Heat Map*, который визуализирует выполнение задач.</span><span class="sxs-lookup"><span data-stu-id="0b014-165">The [Azure Batch Explorer][batch_explorer], one of the Azure Batch [sample applications][github_samples], contains a *Heat Map* feature that provides visualization of task execution.</span></span> <span data-ttu-id="0b014-166">Используйте этот компонент при выполнении примера приложения [ParallelTasks][parallel_tasks_sample], чтобы наглядно представить параллельное выполнение задач на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="0b014-166">When you're executing the [ParallelTasks][parallel_tasks_sample] sample application, you can use the Heat Map feature to easily visualize the execution of parallel tasks on each node.</span></span>

![Тепловая карта обозревателя пакетной службы][1]

<span data-ttu-id="0b014-168">*Тепловая карта обозревателя пакетной службы, отображающая пул из четырех узлов, на каждом из которых выполняется четыре задачи.*</span><span class="sxs-lookup"><span data-stu-id="0b014-168">*Batch Explorer Heat Map showing a pool of four nodes, with each node currently executing four tasks*</span></span>

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
