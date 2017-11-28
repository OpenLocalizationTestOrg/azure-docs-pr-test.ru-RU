---
title: "Использование зависимостей для выполнения задач на основе завершения других задач с помощью пакетной службы Azure | Документация Майкрософт"
description: "Создание задач, которые зависят от выполнения других задач, для обработки по модели MapReduce и аналогичных рабочих нагрузок больших данных в пакетной службе Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: b8d12db5-ca30-4c7d-993a-a05af9257210
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 465306d2de8d1dbe6ba1f0cd74be720b78a50de3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-task-dependencies-to-run-tasks-that-depend-on-other-tasks"></a><span data-ttu-id="b3861-103">Создание зависимостей для выполнения задач, которые зависят от других задач</span><span class="sxs-lookup"><span data-stu-id="b3861-103">Create task dependencies to run tasks that depend on other tasks</span></span>

<span data-ttu-id="b3861-104">Можно определить зависимости задач, чтобы запускать задачу или набор задач только после завершения родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="b3861-104">You can define task dependencies to run a task or set of tasks only after a parent task has completed.</span></span> <span data-ttu-id="b3861-105">Ниже описано несколько ситуаций, в которых удобно использовать зависимости задач. Их можно использовать для:</span><span class="sxs-lookup"><span data-stu-id="b3861-105">Some scenarios where task dependencies are useful include:</span></span>

* <span data-ttu-id="b3861-106">рабочих нагрузок MapReduce в облаке;</span><span class="sxs-lookup"><span data-stu-id="b3861-106">MapReduce-style workloads in the cloud.</span></span>
* <span data-ttu-id="b3861-107">заданий, задачи обработки данных которых можно представить в виде направленного ациклического графа (DAG);</span><span class="sxs-lookup"><span data-stu-id="b3861-107">Jobs whose data processing tasks can be expressed as a directed acyclic graph (DAG).</span></span>
* <span data-ttu-id="b3861-108">подготовительных и последующих процессов отрисовки, в которых каждая задача должна быть выполнена прежде, чем начнется выполнение следующей задачи;</span><span class="sxs-lookup"><span data-stu-id="b3861-108">Pre-rendering and post-rendering processes, where each task must complete before the next task can begin.</span></span>
* <span data-ttu-id="b3861-109">любых других заданий, в которых подчиненные задачи зависят от выходных данных вышестоящих задач.</span><span class="sxs-lookup"><span data-stu-id="b3861-109">Any other job in which downstream tasks depend on the output of upstream tasks.</span></span>

<span data-ttu-id="b3861-110">Зависимости задач пакетной службы позволяют создавать задачи, планируемые для выполнения на вычислительных узлах после завершения одной или нескольких родительских задач.</span><span class="sxs-lookup"><span data-stu-id="b3861-110">With Batch task dependencies, you can create tasks that are scheduled for execution on compute nodes after the completion of one or more parent tasks.</span></span> <span data-ttu-id="b3861-111">Например, можно создать задание, которое отрисовывает каждый кадр трехмерного фильма с помощью отдельных параллельных задач.</span><span class="sxs-lookup"><span data-stu-id="b3861-111">For example, you can create a job that renders each frame of a 3D movie with separate, parallel tasks.</span></span> <span data-ttu-id="b3861-112">Конечная задача, "задача слияния", объединяет отрисованные кадры в готовый фильм только после успешной отрисовки всех кадров.</span><span class="sxs-lookup"><span data-stu-id="b3861-112">The final task--the "merge task"--merges the rendered frames into the complete movie only after all frames have been successfully rendered.</span></span>

<span data-ttu-id="b3861-113">По умолчанию выполнение зависимых задач планируются только после успешного завершения родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="b3861-113">By default, dependent tasks are scheduled for execution only after the parent task has completed successfully.</span></span> <span data-ttu-id="b3861-114">Можно указать действие зависимости, чтобы переопределить поведение по умолчанию и выполнить задачи при сбое родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="b3861-114">You can specify a dependency action to override the default behavior and run tasks when the parent task fails.</span></span> <span data-ttu-id="b3861-115">Дополнительные сведения см. в разделе [Действия зависимостей](#dependency-actions).</span><span class="sxs-lookup"><span data-stu-id="b3861-115">See the [Dependency actions](#dependency-actions) section for details.</span></span>  

<span data-ttu-id="b3861-116">Можно создавать задачи, которые зависят от других задач по схеме "один к одному" или "один ко многим".</span><span class="sxs-lookup"><span data-stu-id="b3861-116">You can create tasks that depend on other tasks in a one-to-one or one-to-many relationship.</span></span> <span data-ttu-id="b3861-117">Можно также создать зависимость от диапазона, при которой задача зависит от завершения группы задач, идентификаторы которых находятся в пределах определенного диапазона.</span><span class="sxs-lookup"><span data-stu-id="b3861-117">You can also create a range dependency where a task depends on the completion of a group of tasks within a specified range of task IDs.</span></span> <span data-ttu-id="b3861-118">Вы можете объединить эти три основные сценария, чтобы создать связь "многие ко многим".</span><span class="sxs-lookup"><span data-stu-id="b3861-118">You can combine these three basic scenarios to create many-to-many relationships.</span></span>

## <a name="task-dependencies-with-batch-net"></a><span data-ttu-id="b3861-119">Зависимости задач .NET пакетной службы</span><span class="sxs-lookup"><span data-stu-id="b3861-119">Task dependencies with Batch .NET</span></span>
<span data-ttu-id="b3861-120">В этой статье рассматривается настройка зависимостей задач с помощью библиотеки [.NET пакетной службы][net_msdn].</span><span class="sxs-lookup"><span data-stu-id="b3861-120">In this article, we discuss how to configure task dependencies by using the [Batch .NET][net_msdn] library.</span></span> <span data-ttu-id="b3861-121">Сначала в этой статье описывается, как [включить зависимость задачи](#enable-task-dependencies) в заданиях, а потом рассматривается, как [настроить задачу с зависимостями](#create-dependent-tasks).</span><span class="sxs-lookup"><span data-stu-id="b3861-121">We first show you how to [enable task dependency](#enable-task-dependencies) on your jobs, and then demonstrate how to [configure a task with dependencies](#create-dependent-tasks).</span></span> <span data-ttu-id="b3861-122">Мы также опишем, как указать действие зависимости, запускающее зависимые задачи при сбое родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="b3861-122">We also describe how to specify a dependency action to run dependent tasks if the parent fails.</span></span> <span data-ttu-id="b3861-123">Напоследок рассматриваются поддерживаемые пакетной службой [сценарии использования зависимостей](#dependency-scenarios) .</span><span class="sxs-lookup"><span data-stu-id="b3861-123">Finally, we discuss the [dependency scenarios](#dependency-scenarios) that Batch supports.</span></span>

## <a name="enable-task-dependencies"></a><span data-ttu-id="b3861-124">Включение зависимостей задач</span><span class="sxs-lookup"><span data-stu-id="b3861-124">Enable task dependencies</span></span>
<span data-ttu-id="b3861-125">Чтобы использовать зависимости задач в приложении пакетной службы, сначала необходимо настроить задание для использования зависимостей задач.</span><span class="sxs-lookup"><span data-stu-id="b3861-125">To use task dependencies in your Batch application, you must first configure the job to use task dependencies.</span></span> <span data-ttu-id="b3861-126">В .NET пакетной службы включите зависимости задач в классе [CloudJob][net_cloudjob], задав для свойства [UsesTaskDependencies][net_usestaskdependencies] значение `true`.</span><span class="sxs-lookup"><span data-stu-id="b3861-126">In Batch .NET, enable it on your [CloudJob][net_cloudjob] by setting its [UsesTaskDependencies][net_usestaskdependencies] property to `true`:</span></span>

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

<span data-ttu-id="b3861-127">Приведенный выше фрагмент кода batchClient представляет собой экземпляр класса [BatchClient][net_batchclient].</span><span class="sxs-lookup"><span data-stu-id="b3861-127">In the preceding code snippet, "batchClient" is an instance of the [BatchClient][net_batchclient] class.</span></span>

## <a name="create-dependent-tasks"></a><span data-ttu-id="b3861-128">Создание зависимости задач</span><span class="sxs-lookup"><span data-stu-id="b3861-128">Create dependent tasks</span></span>
<span data-ttu-id="b3861-129">Чтобы создать задачу, зависящую от выполнения одной или нескольких родительских задач, можно указать, что эта задача "зависит" от других задач.</span><span class="sxs-lookup"><span data-stu-id="b3861-129">To create a task that depends on the completion of one or more parent tasks, you can specify that the task "depends on" the other tasks.</span></span> <span data-ttu-id="b3861-130">В .NET пакетной службы укажите свойство [CloudTask][net_cloudtask].[DependsOn][net_dependson] с помощью экземпляра класса [TaskDependencies][net_taskdependencies].</span><span class="sxs-lookup"><span data-stu-id="b3861-130">In Batch .NET, configure the [CloudTask][net_cloudtask].[DependsOn][net_dependson] property with an instance of the [TaskDependencies][net_taskdependencies] class:</span></span>

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

<span data-ttu-id="b3861-131">Этот фрагмент кода создает зависимую задачу с идентификатором задачи Flowers.</span><span class="sxs-lookup"><span data-stu-id="b3861-131">This code snippet creates a dependent task with task ID "Flowers".</span></span> <span data-ttu-id="b3861-132">Задача Flowers зависит от задач Rain и Sun.</span><span class="sxs-lookup"><span data-stu-id="b3861-132">The "Flowers" task depends on tasks "Rain" and "Sun".</span></span> <span data-ttu-id="b3861-133">Выполнение задачи Flowers будет запланировано на вычислительном узле только после успешного завершения задач Rain и Sun.</span><span class="sxs-lookup"><span data-stu-id="b3861-133">Task "Flowers" will be scheduled to run on a compute node only after tasks "Rain" and "Sun" have completed successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="b3861-134">Задача считается успешно выполненной, когда она находится в состоянии **Выполнено** и ее **код выхода** равен `0`.</span><span class="sxs-lookup"><span data-stu-id="b3861-134">A task is considered to be completed successfully when it is in the **completed** state and its **exit code** is `0`.</span></span> <span data-ttu-id="b3861-135">В .NET пакетной службы это означает, что значение свойства [CloudTask][net_cloudtask].[State][net_taskstate] — `Completed`, а значение свойства [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] класса CloudTask — `0`.</span><span class="sxs-lookup"><span data-stu-id="b3861-135">In Batch .NET, this means a [CloudTask][net_cloudtask].[State][net_taskstate] property value of `Completed` and the CloudTask's [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] property value is `0`.</span></span>
> 
> 

## <a name="dependency-scenarios"></a><span data-ttu-id="b3861-136">сценарии использования зависимостей</span><span class="sxs-lookup"><span data-stu-id="b3861-136">Dependency scenarios</span></span>
<span data-ttu-id="b3861-137">Есть три основных сценария зависимостей задач, которые можно использовать в пакетной службе Azure: "один к одному", "один ко многим" и зависимость диапазона идентификаторов задач.</span><span class="sxs-lookup"><span data-stu-id="b3861-137">There are three basic task dependency scenarios that you can use in Azure Batch: one-to-one, one-to-many, and task ID range dependency.</span></span> <span data-ttu-id="b3861-138">Их можно объединить, чтобы получить четвертый сценарий — "многие ко многим".</span><span class="sxs-lookup"><span data-stu-id="b3861-138">These can be combined to provide a fourth scenario, many-to-many.</span></span>

| <span data-ttu-id="b3861-139">Сценарий&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="b3861-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="b3861-140">Пример</span><span class="sxs-lookup"><span data-stu-id="b3861-140">Example</span></span> |  |
|:---:| --- | --- |
|  [<span data-ttu-id="b3861-141">Один к одному</span><span class="sxs-lookup"><span data-stu-id="b3861-141">One-to-one</span></span>](#one-to-one) |<span data-ttu-id="b3861-142">Задача *taskB* зависит от задачи *taskA*.</span><span class="sxs-lookup"><span data-stu-id="b3861-142">*taskB* depends on *taskA*</span></span> <p/> <span data-ttu-id="b3861-143">Выполнение задачи *taskB* не начнется, пока задача *taskA* не будет успешно выполнена.</span><span class="sxs-lookup"><span data-stu-id="b3861-143">*taskB* will not be scheduled for execution until *taskA* has completed successfully</span></span> |<span data-ttu-id="b3861-144">![Схема: зависимость задач "один к одному"][1]</span><span class="sxs-lookup"><span data-stu-id="b3861-144">![Diagram: one-to-one task dependency][1]</span></span> |
|  [<span data-ttu-id="b3861-145">Один ко многим</span><span class="sxs-lookup"><span data-stu-id="b3861-145">One-to-many</span></span>](#one-to-many) |<span data-ttu-id="b3861-146">Задача *taskC* зависит от задач *taskA* и *taskB*.</span><span class="sxs-lookup"><span data-stu-id="b3861-146">*taskC* depends on both *taskA* and *taskB*</span></span> <p/> <span data-ttu-id="b3861-147">Выполнение задачи *taskC* не начнется, пока задачи *taskA* и *taskB* не будут успешно выполнены).</span><span class="sxs-lookup"><span data-stu-id="b3861-147">*taskC* will not be scheduled for execution until both *taskA* and *taskB* have completed successfully</span></span> |<span data-ttu-id="b3861-148">![Схема: зависимость задач "один ко многим"][2]</span><span class="sxs-lookup"><span data-stu-id="b3861-148">![Diagram: one-to-many task dependency][2]</span></span> |
|  [<span data-ttu-id="b3861-149">Диапазон идентификаторов задач</span><span class="sxs-lookup"><span data-stu-id="b3861-149">Task ID range</span></span>](#task-id-range) |<span data-ttu-id="b3861-150">Задача *taskD* зависит от ряда задач.</span><span class="sxs-lookup"><span data-stu-id="b3861-150">*taskD* depends on a range of tasks</span></span> <p/> <span data-ttu-id="b3861-151">Выполнение задачи *taskD* не начнется, пока не будут успешно выполнены задачи с идентификаторами от *1* до *10*.</span><span class="sxs-lookup"><span data-stu-id="b3861-151">*taskD* will not be scheduled for execution until the tasks with IDs *1* through *10* have completed successfully</span></span> |<span data-ttu-id="b3861-152">![Схема: зависимость диапазона идентификаторов задач][3]</span><span class="sxs-lookup"><span data-stu-id="b3861-152">![Diagram: Task id range dependency][3]</span></span> |

> [!TIP]
> <span data-ttu-id="b3861-153">Вы можете создать связь **многие ко многим**, например, когда каждая задача C, D, E и F зависит от задач A и B. Это удобно, например, в сценариях распараллеленной предварительной обработки, где подчиненные задачи зависят от выходных данных нескольких вышестоящих задач.</span><span class="sxs-lookup"><span data-stu-id="b3861-153">You can create **many-to-many** relationships, such as where tasks C, D, E, and F each depend on tasks A and B. This is useful, for example, in parallelized preprocessing scenarios where your downstream tasks depend on the output of multiple upstream tasks.</span></span>
> 
> <span data-ttu-id="b3861-154">В примерах в этом разделе зависимая задача выполняется только после успешного завершения родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="b3861-154">In the examples in this section, a dependent task runs only after the parent tasks complete successfully.</span></span> <span data-ttu-id="b3861-155">Это поведение по умолчанию для зависимой задачи.</span><span class="sxs-lookup"><span data-stu-id="b3861-155">This behavior is the default behavior for a dependent task.</span></span> <span data-ttu-id="b3861-156">Можно запустить зависимую задачу после сбоя родительской задачи, указав действие зависимости, чтобы переопределить поведение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b3861-156">You can run a dependent task after a parent task fails by specifying a dependency action to override the default behavior.</span></span> <span data-ttu-id="b3861-157">Дополнительные сведения см. в разделе [Действия зависимостей](#dependency-actions).</span><span class="sxs-lookup"><span data-stu-id="b3861-157">See the [Dependency actions](#dependency-actions) section for details.</span></span>

### <a name="one-to-one"></a><span data-ttu-id="b3861-158">Один к одному</span><span class="sxs-lookup"><span data-stu-id="b3861-158">One-to-one</span></span>
<span data-ttu-id="b3861-159">При взаимосвязи "один к одному" задача зависит от успешного выполнения одной родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="b3861-159">In a one-to-one relationship, a task depends on the successful completion of one parent task.</span></span> <span data-ttu-id="b3861-160">Чтобы создать зависимость, укажите один идентификатор задачи в статическом методе [TaskDependencies][net_taskdependencies].[OnId][net_onid] при заполнении свойства [DependsOn][net_dependson] элемента [CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="b3861-160">To create the dependency, provide a single task ID to the [TaskDependencies][net_taskdependencies].[OnId][net_onid] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a><span data-ttu-id="b3861-161">Один ко многим</span><span class="sxs-lookup"><span data-stu-id="b3861-161">One-to-many</span></span>
<span data-ttu-id="b3861-162">При взаимосвязи "один ко многим" задача зависит от успешного выполнения нескольких родительских задач.</span><span class="sxs-lookup"><span data-stu-id="b3861-162">In a one-to-many relationship, a task depends on the completion of multiple parent tasks.</span></span> <span data-ttu-id="b3861-163">Чтобы создать зависимость, укажите набор идентификаторов задач в статическом методе [TaskDependencies][net_taskdependencies].[OnIds][net_onids] при заполнении свойства [DependsOn][net_dependson] элемента [CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="b3861-163">To create the dependency, provide a collection of task IDs to the [TaskDependencies][net_taskdependencies].[OnIds][net_onids] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// 'Rain' and 'Sun' don't depend on any other tasks
new CloudTask("Rain", "cmd.exe /c echo Rain"),
new CloudTask("Sun", "cmd.exe /c echo Sun"),

// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
``` 

### <a name="task-id-range"></a><span data-ttu-id="b3861-164">Диапазон идентификаторов задач</span><span class="sxs-lookup"><span data-stu-id="b3861-164">Task ID range</span></span>
<span data-ttu-id="b3861-165">При зависимости от диапазона родительских задач задача зависит от выполнения задач, идентификаторы которых находятся в указанном диапазоне.</span><span class="sxs-lookup"><span data-stu-id="b3861-165">In a dependency on a range of parent tasks, a task depends on the the completion of tasks whose IDs lie within a range.</span></span>
<span data-ttu-id="b3861-166">Чтобы создать зависимость, укажите первый и последний идентификаторы задач в статическом методе [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] при заполнении свойства [DependsOn][net_dependson] элемента [CloudTask][net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="b3861-166">To create the dependency, provide the first and last task IDs in the range to the [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] static method when you populate the [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3861-167">Если вы используете диапазоны идентификаторов задач для зависимостей, то идентификаторы задач в диапазоне *должны* быть строковыми представлениями целых чисел.</span><span class="sxs-lookup"><span data-stu-id="b3861-167">When you use task ID ranges for your dependencies, the task IDs in the range *must* be string representations of integer values.</span></span>
> 
> <span data-ttu-id="b3861-168">Каждая задача в диапазоне должна выполнить условие зависимости, завершившись успешно или сбоем, который сопоставлен с действием зависимости со значением **Satisfy**.</span><span class="sxs-lookup"><span data-stu-id="b3861-168">Every task in the range must satisfy the dependency, either by completing successfully or by completing with a failure that’s mapped to a dependency action set to **Satisfy**.</span></span> <span data-ttu-id="b3861-169">Дополнительные сведения см. в разделе [Действия зависимостей](#dependency-actions).</span><span class="sxs-lookup"><span data-stu-id="b3861-169">See the [Dependency actions](#dependency-actions) section for details.</span></span>
>
>

```csharp
// Tasks 1, 2, and 3 don't depend on any other tasks. Because
// we will be using them for a task range dependency, we must
// specify string representations of integers as their ids.
new CloudTask("1", "cmd.exe /c echo 1"),
new CloudTask("2", "cmd.exe /c echo 2"),
new CloudTask("3", "cmd.exe /c echo 3"),

// Task 4 depends on a range of tasks, 1 through 3
new CloudTask("4", "cmd.exe /c echo 4")
{
    // To use a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters to TaskIdRange,
    // but their ids (above) are string representations of the ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a><span data-ttu-id="b3861-170">Действия зависимостей</span><span class="sxs-lookup"><span data-stu-id="b3861-170">Dependency actions</span></span>

<span data-ttu-id="b3861-171">По умолчанию зависимая задача или набор задач выполняется только после успешного завершения родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="b3861-171">By default, a dependent task or set of tasks runs only after a parent task has completed successfully.</span></span> <span data-ttu-id="b3861-172">В некоторых случаях может потребоваться запустить зависимые задачи даже в случае сбоя родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="b3861-172">In some scenarios, you may want to run dependent tasks even if the parent task fails.</span></span> <span data-ttu-id="b3861-173">Поведение по умолчанию можно переопределить, указав действие зависимости.</span><span class="sxs-lookup"><span data-stu-id="b3861-173">You can override the default behavior by specifying a dependency action.</span></span> <span data-ttu-id="b3861-174">Действие зависимости указывает, следует ли запускать зависимую задачу в случае успешного завершения или сбоя родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="b3861-174">A dependency action specifies whether a dependent task is eligible to run, based on the success or failure of the parent task.</span></span> 

<span data-ttu-id="b3861-175">Например предположим, что зависимая задача ожидает данные из восходящей задачи.</span><span class="sxs-lookup"><span data-stu-id="b3861-175">For example, suppose that a dependent task is awaiting data from the completion of the upstream task.</span></span> <span data-ttu-id="b3861-176">При сбое восходящей задачи зависимая задача все равно может быть выполнена с использованием старых данных.</span><span class="sxs-lookup"><span data-stu-id="b3861-176">If the upstream task fails, the dependent task may still be able to run using older data.</span></span> <span data-ttu-id="b3861-177">В этом случае с помощью действия зависимости можно указать, что зависимая задача может быть выполнена в случае сбоя родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="b3861-177">In this case, a dependency action can specify that the dependent task is eligible to run despite the failure of the parent task.</span></span>

<span data-ttu-id="b3861-178">Действие зависимости основано на условии выхода родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="b3861-178">A dependency action is based on an exit condition for the parent task.</span></span> <span data-ttu-id="b3861-179">Можно указать действие зависимости для любого из приведенных ниже условий выхода. Чтобы получить сведения для .NET, ознакомьтесь с классом [ExitConditions][net_exitconditions].</span><span class="sxs-lookup"><span data-stu-id="b3861-179">You can specify a dependency action for any of the following exit conditions; for .NET, see the [ExitConditions][net_exitconditions] class for details:</span></span>

- <span data-ttu-id="b3861-180">Если возникла ошибка предварительной обработки.</span><span class="sxs-lookup"><span data-stu-id="b3861-180">When a pre-processing error occurs.</span></span>
- <span data-ttu-id="b3861-181">Если возникла ошибка отправки файла.</span><span class="sxs-lookup"><span data-stu-id="b3861-181">When a file upload error occurs.</span></span> <span data-ttu-id="b3861-182">Если задача завершается с кодом выхода, который был задан с помощью свойства **exitCodes** или **exitCodeRanges**, а затем возникает ошибка отправки файла, действие, указанное в коде выхода, имеет более высокий приоритет.</span><span class="sxs-lookup"><span data-stu-id="b3861-182">If the task exits with an exit code that was specified via **exitCodes** or **exitCodeRanges**, and then encounters a file upload error, the action specified by the exit code takes precedence.</span></span>
- <span data-ttu-id="b3861-183">Когда задача завершается с кодом выхода, определенным в свойстве **ExitCodes**.</span><span class="sxs-lookup"><span data-stu-id="b3861-183">When the task exits with an exit code defined by the **ExitCodes** property.</span></span>
- <span data-ttu-id="b3861-184">Когда задача завершается с кодом выхода, который попадает в диапазон, заданный свойством **ExitCodeRanges**.</span><span class="sxs-lookup"><span data-stu-id="b3861-184">When the task exits with an exit code that falls within a range specified by the **ExitCodeRanges** property.</span></span>
- <span data-ttu-id="b3861-185">По умолчанию, если задача завершается с кодом выхода, не указанным в свойстве **ExitCodes** или **ExitCodeRanges**, или если задача завершается с ошибкой предварительной обработки и свойство **PreProcessingError** не задано, или если происходит сбой выполнения задачи с ошибкой отправки файла и свойство **FileUploadError** не задано.</span><span class="sxs-lookup"><span data-stu-id="b3861-185">The default case, if the task exits with an exit code not defined by **ExitCodes** or **ExitCodeRanges**, or if the task exits with a pre-processing error and the **PreProcessingError** property is not set, or if the task fails with a file upload error and the **FileUploadError** property is not set.</span></span> 

<span data-ttu-id="b3861-186">Чтобы указать действие зависимости в .NET, задайте свойство [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] для условия выхода.</span><span class="sxs-lookup"><span data-stu-id="b3861-186">To specify a dependency action in .NET, set the [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] property for the exit condition.</span></span> <span data-ttu-id="b3861-187">Свойство **DependencyAction** принимает одно из двух значений:</span><span class="sxs-lookup"><span data-stu-id="b3861-187">The **DependencyAction** property takes one of two values:</span></span>

- <span data-ttu-id="b3861-188">Если свойству **DependencyAction** присвоить значение **Satisfy**, то зависимые задачи смогут быть выполнены, если родительская задача завершается с указанной ошибкой.</span><span class="sxs-lookup"><span data-stu-id="b3861-188">Setting the **DependencyAction** property to **Satisfy** indicates that dependent tasks are eligible to run if the parent task exits with a specified error.</span></span>
- <span data-ttu-id="b3861-189">Если свойству **DependencyAction** присвоить значение **Block** то, зависимые задачи не будут выполнены.</span><span class="sxs-lookup"><span data-stu-id="b3861-189">Setting the **DependencyAction** property to **Block** indicates that dependent tasks are not eligible to run.</span></span>

<span data-ttu-id="b3861-190">По умолчанию для свойства **DependencyAction** заданы значение **Satisfy** для кода выхода 0 и значение **Block** для всех остальных условий выхода.</span><span class="sxs-lookup"><span data-stu-id="b3861-190">The default setting for the **DependencyAction** property is **Satisfy** for exit code 0, and **Block** for all other exit conditions.</span></span>

<span data-ttu-id="b3861-191">В следующем фрагменте кода настраивается свойство **DependencyAction** родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="b3861-191">The following code snippet sets the **DependencyAction** property for a parent task.</span></span> <span data-ttu-id="b3861-192">Если родительская задача завершается ошибкой предварительной обработки или ошибкой с заданным кодом, то зависимая задача блокируется.</span><span class="sxs-lookup"><span data-stu-id="b3861-192">If the parent task exits with a pre-processing error, or with the specified error codes, the dependent task is blocked.</span></span> <span data-ttu-id="b3861-193">Если родительская задача завершается с любой другой ошибкой, код которой не равен 0, то зависимая задача выполняется.</span><span class="sxs-lookup"><span data-stu-id="b3861-193">If the parent task exits with any other non-zero error, the dependent task is eligible to run.</span></span>

```csharp
// Task A is the parent task.
new CloudTask("A", "cmd.exe /c echo A")
{
    // Specify exit conditions for task A and their dependency actions.
    ExitConditions = new ExitConditions
    {
        // If task A exits with a pre-processing error, block any downstream tasks (in this example, task B).
        PreProcessingError = new ExitOptions
        {
            DependencyAction = DependencyAction.Block
        },
        // If task A exits with the specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible to run 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible to run depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a><span data-ttu-id="b3861-194">Пример кода</span><span class="sxs-lookup"><span data-stu-id="b3861-194">Code sample</span></span>
<span data-ttu-id="b3861-195">[TaskDependencies][github_taskdependencies] — это один из [примеров кода пакетной службы Azure][github_samples] на портале GitHub.</span><span class="sxs-lookup"><span data-stu-id="b3861-195">The [TaskDependencies][github_taskdependencies] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="b3861-196">Это решение Visual Studio демонстрирует следующее:</span><span class="sxs-lookup"><span data-stu-id="b3861-196">This Visual Studio solution demonstrates:</span></span>

- <span data-ttu-id="b3861-197">как включить зависимость задачи для задания;</span><span class="sxs-lookup"><span data-stu-id="b3861-197">How to enable task dependency on a job</span></span>
- <span data-ttu-id="b3861-198">как создать задачи, которые зависят от других задач;</span><span class="sxs-lookup"><span data-stu-id="b3861-198">How to create tasks that depend on other tasks</span></span>
- <span data-ttu-id="b3861-199">как выполнить эти задачи в пуле вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="b3861-199">How to execute those tasks on a pool of compute nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3861-200">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b3861-200">Next steps</span></span>
### <a name="application-deployment"></a><span data-ttu-id="b3861-201">Развертывание приложения</span><span class="sxs-lookup"><span data-stu-id="b3861-201">Application deployment</span></span>
<span data-ttu-id="b3861-202">Функция [пакетов приложения](batch-application-packages.md) в пакетной службе дает возможность очень легко развернуть приложения, которые задачи выполняют на вычислительных узлах, и управлять их версиями.</span><span class="sxs-lookup"><span data-stu-id="b3861-202">The [application packages](batch-application-packages.md) feature of Batch provides an easy way to both deploy and version the applications that your tasks execute on compute nodes.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="b3861-203">Установка приложений и промежуточных данных</span><span class="sxs-lookup"><span data-stu-id="b3861-203">Installing applications and staging data</span></span>
<span data-ttu-id="b3861-204">Ознакомьтесь с публикацией [Installing applications and staging data on Batch compute nodes][forum_post] (Установка приложений и промежуточное размещение данных на вычислительных узлах пакетной службы) на форуме по пакетной службе Azure. Из нее вы узнаете о различных способах подготовки узлов для выполнения задач.</span><span class="sxs-lookup"><span data-stu-id="b3861-204">See [Installing applications and staging data on Batch compute nodes][forum_post] in the Azure Batch forum for an overview of methods for preparing your nodes to run tasks.</span></span> <span data-ttu-id="b3861-205">Эта публикация написана одним из участников команды разработчиков пакетной службы Azure, и она дает хорошее базовое понимание разных способов копирования приложений, входных данных для задач и других файлов на вычислительные узлы.</span><span class="sxs-lookup"><span data-stu-id="b3861-205">Written by one of the Azure Batch team members, this post is a good primer on the different ways to copy applications, task input data, and other files to your compute nodes.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_taskdependencies]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_dependson]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.dependson.aspx
[net_exitcode]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.exitcode.aspx
[net_exitconditions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitconditions
[net_exitoptions]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions
[net_dependencyaction]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.exitoptions#Microsoft_Azure_Batch_ExitOptions_DependencyAction
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_onid]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onid.aspx
[net_onids]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onids.aspx
[net_onidrange]: https://msdn.microsoft.com/library/microsoft.azure.batch.taskdependencies.onidrange.aspx
[net_taskexecutioninformation]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskexecutioninformation.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_usestaskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.usestaskdependencies.aspx
[net_taskdependencies]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskdependencies.aspx

<span data-ttu-id="b3861-206">[1]: ./media/batch-task-dependency/01_one_to_one.png "Схема: зависимость "один к одному""</span><span class="sxs-lookup"><span data-stu-id="b3861-206">[1]: ./media/batch-task-dependency/01_one_to_one.png "Diagram: one-to-one dependency"</span></span>
<span data-ttu-id="b3861-207">[2]: ./media/batch-task-dependency/02_one_to_many.png "Схема: зависимость "один ко многим""</span><span class="sxs-lookup"><span data-stu-id="b3861-207">[2]: ./media/batch-task-dependency/02_one_to_many.png "Diagram: one-to-many dependency"</span></span>
<span data-ttu-id="b3861-208">[3]: ./media/batch-task-dependency/03_task_id_range.png "Схема: зависимость диапазона идентификаторов задач"</span><span class="sxs-lookup"><span data-stu-id="b3861-208">[3]: ./media/batch-task-dependency/03_task_id_range.png "Diagram: task id range dependency"</span></span>
