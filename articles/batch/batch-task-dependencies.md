---
title: "зависимости toorun aaaUse задач задачи на основании hello выполнения других задач - пакетной службы Azure | Документы Microsoft"
description: "Создайте задачи, которые зависят от hello выполнения других задач обработки MapReduce стиль и схожие данные больших рабочих нагрузок в пакете Azure."
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
ms.openlocfilehash: faf08ec38cb30b1f66acd51e256c31aea6215c62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-task-dependencies-toorun-tasks-that-depend-on-other-tasks"></a><span data-ttu-id="84150-103">Создание зависимостей задач toorun задач, которые зависят от других задач</span><span class="sxs-lookup"><span data-stu-id="84150-103">Create task dependencies toorun tasks that depend on other tasks</span></span>

<span data-ttu-id="84150-104">Toorun зависимости задач можно определить задачи или набора задач только после завершения родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="84150-104">You can define task dependencies toorun a task or set of tasks only after a parent task has completed.</span></span> <span data-ttu-id="84150-105">Ниже описано несколько ситуаций, в которых удобно использовать зависимости задач. Их можно использовать для:</span><span class="sxs-lookup"><span data-stu-id="84150-105">Some scenarios where task dependencies are useful include:</span></span>

* <span data-ttu-id="84150-106">Стиль MapReduce рабочих нагрузок в облако hello.</span><span class="sxs-lookup"><span data-stu-id="84150-106">MapReduce-style workloads in hello cloud.</span></span>
* <span data-ttu-id="84150-107">заданий, задачи обработки данных которых можно представить в виде направленного ациклического графа (DAG);</span><span class="sxs-lookup"><span data-stu-id="84150-107">Jobs whose data processing tasks can be expressed as a directed acyclic graph (DAG).</span></span>
* <span data-ttu-id="84150-108">Процессы предварительной подготовки к просмотру и после подготовки к просмотру, где каждая задача должна быть выполнена перед началом следующей задаче hello.</span><span class="sxs-lookup"><span data-stu-id="84150-108">Pre-rendering and post-rendering processes, where each task must complete before hello next task can begin.</span></span>
* <span data-ttu-id="84150-109">Любое другое задание, в котором подчиненные задачи зависят от hello выходные данные вышестоящего задачи.</span><span class="sxs-lookup"><span data-stu-id="84150-109">Any other job in which downstream tasks depend on hello output of upstream tasks.</span></span>

<span data-ttu-id="84150-110">С зависимостями задач пакета можно создать задачи, запланированные для выполнения на вычислительных узлах после завершения одного или нескольких родительских задачах hello.</span><span class="sxs-lookup"><span data-stu-id="84150-110">With Batch task dependencies, you can create tasks that are scheduled for execution on compute nodes after hello completion of one or more parent tasks.</span></span> <span data-ttu-id="84150-111">Например, можно создать задание, которое отрисовывает каждый кадр трехмерного фильма с помощью отдельных параллельных задач.</span><span class="sxs-lookup"><span data-stu-id="84150-111">For example, you can create a job that renders each frame of a 3D movie with separate, parallel tasks.</span></span> <span data-ttu-id="84150-112">Последняя задача Hello--hello «задача слияния»--слияний hello преобразуется кадры hello полный фильм только после того как все кадры отрисовываются успешно.</span><span class="sxs-lookup"><span data-stu-id="84150-112">hello final task--hello "merge task"--merges hello rendered frames into hello complete movie only after all frames have been successfully rendered.</span></span>

<span data-ttu-id="84150-113">По умолчанию зависимые задачи, планируются для выполнения только в том случае, после успешного завершения родительской задачи hello.</span><span class="sxs-lookup"><span data-stu-id="84150-113">By default, dependent tasks are scheduled for execution only after hello parent task has completed successfully.</span></span> <span data-ttu-id="84150-114">Можно указать поведение по умолчанию действие toooverride зависимостей hello и запускать задачи при сбое hello родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="84150-114">You can specify a dependency action toooverride hello default behavior and run tasks when hello parent task fails.</span></span> <span data-ttu-id="84150-115">В разделе hello [действия зависимостей](#dependency-actions) подробные сведения см.</span><span class="sxs-lookup"><span data-stu-id="84150-115">See hello [Dependency actions](#dependency-actions) section for details.</span></span>  

<span data-ttu-id="84150-116">Можно создавать задачи, которые зависят от других задач по схеме "один к одному" или "один ко многим".</span><span class="sxs-lookup"><span data-stu-id="84150-116">You can create tasks that depend on other tasks in a one-to-one or one-to-many relationship.</span></span> <span data-ttu-id="84150-117">Можно также создать диапазона зависимостей, где задачи зависит от выполнения hello группы задач в пределах указанного диапазона идентификаторов задач.</span><span class="sxs-lookup"><span data-stu-id="84150-117">You can also create a range dependency where a task depends on hello completion of a group of tasks within a specified range of task IDs.</span></span> <span data-ttu-id="84150-118">Можно объединять эти три основных сценария toocreate многие ко многим связи.</span><span class="sxs-lookup"><span data-stu-id="84150-118">You can combine these three basic scenarios toocreate many-to-many relationships.</span></span>

## <a name="task-dependencies-with-batch-net"></a><span data-ttu-id="84150-119">Зависимости задач .NET пакетной службы</span><span class="sxs-lookup"><span data-stu-id="84150-119">Task dependencies with Batch .NET</span></span>
<span data-ttu-id="84150-120">В этой статье мы рассмотрим, как hello tooconfigure зависимостей задач с помощью [пакета .NET] [ net_msdn] библиотеки.</span><span class="sxs-lookup"><span data-stu-id="84150-120">In this article, we discuss how tooconfigure task dependencies by using hello [Batch .NET][net_msdn] library.</span></span> <span data-ttu-id="84150-121">Мы сначала показано, каким образом слишком[включить зависимость](#enable-task-dependencies) в заданиях, а затем показывается, как слишком[настройте задачу с зависимостями](#create-dependent-tasks).</span><span class="sxs-lookup"><span data-stu-id="84150-121">We first show you how too[enable task dependency](#enable-task-dependencies) on your jobs, and then demonstrate how too[configure a task with dependencies](#create-dependent-tasks).</span></span> <span data-ttu-id="84150-122">Также описывается, как toospecify toorun зависимого действия зависимостей задач при сбое родительской hello.</span><span class="sxs-lookup"><span data-stu-id="84150-122">We also describe how toospecify a dependency action toorun dependent tasks if hello parent fails.</span></span> <span data-ttu-id="84150-123">Наконец, мы обсудим hello [сценарии зависимостей](#dependency-scenarios) , поддерживающий пакета.</span><span class="sxs-lookup"><span data-stu-id="84150-123">Finally, we discuss hello [dependency scenarios](#dependency-scenarios) that Batch supports.</span></span>

## <a name="enable-task-dependencies"></a><span data-ttu-id="84150-124">Включение зависимостей задач</span><span class="sxs-lookup"><span data-stu-id="84150-124">Enable task dependencies</span></span>
<span data-ttu-id="84150-125">toouse зависимостей задач в пакет приложения, необходимо сначала настроить зависимостей задач toouse задания hello.</span><span class="sxs-lookup"><span data-stu-id="84150-125">toouse task dependencies in your Batch application, you must first configure hello job toouse task dependencies.</span></span> <span data-ttu-id="84150-126">В пакете .NET, включить его на ваш [CloudJob] [ net_cloudjob] , установив его [UsesTaskDependencies] [ net_usestaskdependencies] свойство слишком`true`:</span><span class="sxs-lookup"><span data-stu-id="84150-126">In Batch .NET, enable it on your [CloudJob][net_cloudjob] by setting its [UsesTaskDependencies][net_usestaskdependencies] property too`true`:</span></span>

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

<span data-ttu-id="84150-127">В предыдущих фрагмент кода hello, «batchClient» является экземпляром типа hello [BatchClient] [ net_batchclient] класса.</span><span class="sxs-lookup"><span data-stu-id="84150-127">In hello preceding code snippet, "batchClient" is an instance of hello [BatchClient][net_batchclient] class.</span></span>

## <a name="create-dependent-tasks"></a><span data-ttu-id="84150-128">Создание зависимости задач</span><span class="sxs-lookup"><span data-stu-id="84150-128">Create dependent tasks</span></span>
<span data-ttu-id="84150-129">toocreate задачу, которая зависит от выполнения hello одного или нескольких родительских задач можно указать задачу «зависит от» hello, hello другие задачи.</span><span class="sxs-lookup"><span data-stu-id="84150-129">toocreate a task that depends on hello completion of one or more parent tasks, you can specify that hello task "depends on" hello other tasks.</span></span> <span data-ttu-id="84150-130">В пакете .NET, настройте hello [CloudTask][net_cloudtask].[ DependsOn] [ net_dependson] свойство с помощью экземпляра hello [TaskDependencies] [ net_taskdependencies] класса:</span><span class="sxs-lookup"><span data-stu-id="84150-130">In Batch .NET, configure hello [CloudTask][net_cloudtask].[DependsOn][net_dependson] property with an instance of hello [TaskDependencies][net_taskdependencies] class:</span></span>

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

<span data-ttu-id="84150-131">Этот фрагмент кода создает зависимую задачу с идентификатором задачи Flowers.</span><span class="sxs-lookup"><span data-stu-id="84150-131">This code snippet creates a dependent task with task ID "Flowers".</span></span> <span data-ttu-id="84150-132">Hello «Цветов» задача зависит от задачи «Дождь» и «Sun».</span><span class="sxs-lookup"><span data-stu-id="84150-132">hello "Flowers" task depends on tasks "Rain" and "Sun".</span></span> <span data-ttu-id="84150-133">Задача «Цветов» будет запланированных toorun на вычислительном узле только после задачи «Дождь» и «Sun» завершена успешно.</span><span class="sxs-lookup"><span data-stu-id="84150-133">Task "Flowers" will be scheduled toorun on a compute node only after tasks "Rain" and "Sun" have completed successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="84150-134">Задача считается toobe выполнена успешно, если он находится в hello **завершения** состояние и его **код выхода** — `0`.</span><span class="sxs-lookup"><span data-stu-id="84150-134">A task is considered toobe completed successfully when it is in hello **completed** state and its **exit code** is `0`.</span></span> <span data-ttu-id="84150-135">В пакете .NET, это означает [CloudTask][net_cloudtask].[ Состояние] [ net_taskstate] значение свойства `Completed` и hello CloudTask [TaskExecutionInformation][net_taskexecutioninformation].[ ExitCode] [ net_exitcode] значение свойства `0`.</span><span class="sxs-lookup"><span data-stu-id="84150-135">In Batch .NET, this means a [CloudTask][net_cloudtask].[State][net_taskstate] property value of `Completed` and hello CloudTask's [TaskExecutionInformation][net_taskexecutioninformation].[ExitCode][net_exitcode] property value is `0`.</span></span>
> 
> 

## <a name="dependency-scenarios"></a><span data-ttu-id="84150-136">сценарии использования зависимостей</span><span class="sxs-lookup"><span data-stu-id="84150-136">Dependency scenarios</span></span>
<span data-ttu-id="84150-137">Есть три основных сценария зависимостей задач, которые можно использовать в пакетной службе Azure: "один к одному", "один ко многим" и зависимость диапазона идентификаторов задач.</span><span class="sxs-lookup"><span data-stu-id="84150-137">There are three basic task dependency scenarios that you can use in Azure Batch: one-to-one, one-to-many, and task ID range dependency.</span></span> <span data-ttu-id="84150-138">Это могут быть объединенный tooprovide четвертый сценарии многие ко многим.</span><span class="sxs-lookup"><span data-stu-id="84150-138">These can be combined tooprovide a fourth scenario, many-to-many.</span></span>

| <span data-ttu-id="84150-139">Сценарий&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span class="sxs-lookup"><span data-stu-id="84150-139">Scenario&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></span> | <span data-ttu-id="84150-140">Пример</span><span class="sxs-lookup"><span data-stu-id="84150-140">Example</span></span> |  |
|:---:| --- | --- |
|  [<span data-ttu-id="84150-141">Один к одному</span><span class="sxs-lookup"><span data-stu-id="84150-141">One-to-one</span></span>](#one-to-one) |<span data-ttu-id="84150-142">Задача *taskB* зависит от задачи *taskA*.</span><span class="sxs-lookup"><span data-stu-id="84150-142">*taskB* depends on *taskA*</span></span> <p/> <span data-ttu-id="84150-143">Выполнение задачи *taskB* не начнется, пока задача *taskA* не будет успешно выполнена.</span><span class="sxs-lookup"><span data-stu-id="84150-143">*taskB* will not be scheduled for execution until *taskA* has completed successfully</span></span> |<span data-ttu-id="84150-144">![Схема: зависимость задач "один к одному"][1]</span><span class="sxs-lookup"><span data-stu-id="84150-144">![Diagram: one-to-one task dependency][1]</span></span> |
|  [<span data-ttu-id="84150-145">Один ко многим</span><span class="sxs-lookup"><span data-stu-id="84150-145">One-to-many</span></span>](#one-to-many) |<span data-ttu-id="84150-146">Задача *taskC* зависит от задач *taskA* и *taskB*.</span><span class="sxs-lookup"><span data-stu-id="84150-146">*taskC* depends on both *taskA* and *taskB*</span></span> <p/> <span data-ttu-id="84150-147">Выполнение задачи *taskC* не начнется, пока задачи *taskA* и *taskB* не будут успешно выполнены).</span><span class="sxs-lookup"><span data-stu-id="84150-147">*taskC* will not be scheduled for execution until both *taskA* and *taskB* have completed successfully</span></span> |<span data-ttu-id="84150-148">![Схема: зависимость задач "один ко многим"][2]</span><span class="sxs-lookup"><span data-stu-id="84150-148">![Diagram: one-to-many task dependency][2]</span></span> |
|  [<span data-ttu-id="84150-149">Диапазон идентификаторов задач</span><span class="sxs-lookup"><span data-stu-id="84150-149">Task ID range</span></span>](#task-id-range) |<span data-ttu-id="84150-150">Задача *taskD* зависит от ряда задач.</span><span class="sxs-lookup"><span data-stu-id="84150-150">*taskD* depends on a range of tasks</span></span> <p/> <span data-ttu-id="84150-151">*taskD* не будут запланированы для выполнения до hello задачи с идентификаторами *1* через *10* завершена успешно</span><span class="sxs-lookup"><span data-stu-id="84150-151">*taskD* will not be scheduled for execution until hello tasks with IDs *1* through *10* have completed successfully</span></span> |<span data-ttu-id="84150-152">![Схема: зависимость диапазона идентификаторов задач][3]</span><span class="sxs-lookup"><span data-stu-id="84150-152">![Diagram: Task id range dependency][3]</span></span> |

> [!TIP]
> <span data-ttu-id="84150-153">Можно создать **многие ко многим** связи, например когда задачи C, D, E и F каждого зависят от задач A и B. Это полезно, например, в которых подчиненных задач зависит от hello вывод нескольких задач вышестоящего Параллелизованный предварительной обработки сценариев.</span><span class="sxs-lookup"><span data-stu-id="84150-153">You can create **many-to-many** relationships, such as where tasks C, D, E, and F each depend on tasks A and B. This is useful, for example, in parallelized preprocessing scenarios where your downstream tasks depend on hello output of multiple upstream tasks.</span></span>
> 
> <span data-ttu-id="84150-154">В примерах этого раздела hello зависимая задача выполняется только после успешного завершения задач родительского hello.</span><span class="sxs-lookup"><span data-stu-id="84150-154">In hello examples in this section, a dependent task runs only after hello parent tasks complete successfully.</span></span> <span data-ttu-id="84150-155">Данное поведение является поведением по умолчанию hello для зависимой задачи.</span><span class="sxs-lookup"><span data-stu-id="84150-155">This behavior is hello default behavior for a dependent task.</span></span> <span data-ttu-id="84150-156">Можно запустить выполнение зависимой задачи родительская задача завершается посредством определения поведения по умолчанию hello toooverride действие зависимостей.</span><span class="sxs-lookup"><span data-stu-id="84150-156">You can run a dependent task after a parent task fails by specifying a dependency action toooverride hello default behavior.</span></span> <span data-ttu-id="84150-157">В разделе hello [действия зависимостей](#dependency-actions) подробные сведения см.</span><span class="sxs-lookup"><span data-stu-id="84150-157">See hello [Dependency actions](#dependency-actions) section for details.</span></span>

### <a name="one-to-one"></a><span data-ttu-id="84150-158">Один к одному</span><span class="sxs-lookup"><span data-stu-id="84150-158">One-to-one</span></span>
<span data-ttu-id="84150-159">Связи «один к одному» задача зависит от hello успешное завершение задачи одного родительского элемента.</span><span class="sxs-lookup"><span data-stu-id="84150-159">In a one-to-one relationship, a task depends on hello successful completion of one parent task.</span></span> <span data-ttu-id="84150-160">toocreate hello зависимостей, укажите идентификатор одну задачу toohello [TaskDependencies][net_taskdependencies].[ OnId] [ net_onid] статический метод, при заполнении hello [DependsOn] [ net_dependson] свойство [CloudTask] [ net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="84150-160">toocreate hello dependency, provide a single task ID toohello [TaskDependencies][net_taskdependencies].[OnId][net_onid] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a><span data-ttu-id="84150-161">Один ко многим</span><span class="sxs-lookup"><span data-stu-id="84150-161">One-to-many</span></span>
<span data-ttu-id="84150-162">В отношении "один ко многим" задача зависит от выполнения hello несколько родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="84150-162">In a one-to-many relationship, a task depends on hello completion of multiple parent tasks.</span></span> <span data-ttu-id="84150-163">toocreate Здравствуйте зависимостей, образуют набор задач идентификаторы toohello [TaskDependencies][net_taskdependencies].[ OnIds] [ net_onids] статический метод, при заполнении hello [DependsOn] [ net_dependson] свойство [CloudTask] [ net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="84150-163">toocreate hello dependency, provide a collection of task IDs toohello [TaskDependencies][net_taskdependencies].[OnIds][net_onids] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

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

### <a name="task-id-range"></a><span data-ttu-id="84150-164">Диапазон идентификаторов задач</span><span class="sxs-lookup"><span data-stu-id="84150-164">Task ID range</span></span>
<span data-ttu-id="84150-165">В зависимость от родительской задачи задача зависит hello hello выполнения задач, идентификаторы которых находятся в пределах диапазона.</span><span class="sxs-lookup"><span data-stu-id="84150-165">In a dependency on a range of parent tasks, a task depends on hello hello completion of tasks whose IDs lie within a range.</span></span>
<span data-ttu-id="84150-166">зависимость toocreate hello, сначала укажите hello и последнего ИД задач в диапазоне toohello hello [TaskDependencies][net_taskdependencies].[ OnIdRange] [ net_onidrange] статический метод, при заполнении hello [DependsOn] [ net_dependson] свойство [CloudTask] [net_cloudtask].</span><span class="sxs-lookup"><span data-stu-id="84150-166">toocreate hello dependency, provide hello first and last task IDs in hello range toohello [TaskDependencies][net_taskdependencies].[OnIdRange][net_onidrange] static method when you populate hello [DependsOn][net_dependson] property of [CloudTask][net_cloudtask].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84150-167">При использовании задач диапазоны Идентификаторов для зависимостей hello идентификаторы задач в диапазоне hello *должен* быть строковые представления значений целое число со знаком.</span><span class="sxs-lookup"><span data-stu-id="84150-167">When you use task ID ranges for your dependencies, hello task IDs in hello range *must* be string representations of integer values.</span></span>
> 
> <span data-ttu-id="84150-168">Каждая задача в диапазоне hello должны удовлетворять зависимостей hello успешному завершению работы или завершение со сбоем, задано слишком действие зависимостей сопоставленных tooa**Satisfy**.</span><span class="sxs-lookup"><span data-stu-id="84150-168">Every task in hello range must satisfy hello dependency, either by completing successfully or by completing with a failure that’s mapped tooa dependency action set too**Satisfy**.</span></span> <span data-ttu-id="84150-169">В разделе hello [действия зависимостей](#dependency-actions) подробные сведения см.</span><span class="sxs-lookup"><span data-stu-id="84150-169">See hello [Dependency actions](#dependency-actions) section for details.</span></span>
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
    // toouse a range of tasks, their ids must be integer values.
    // Note that we pass integers as parameters tooTaskIdRange,
    // but their ids (above) are string representations of hello ids.
    DependsOn = TaskDependencies.OnIdRange(1, 3)
},
```

## <a name="dependency-actions"></a><span data-ttu-id="84150-170">Действия зависимостей</span><span class="sxs-lookup"><span data-stu-id="84150-170">Dependency actions</span></span>

<span data-ttu-id="84150-171">По умолчанию зависимая задача или набор задач выполняется только после успешного завершения родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="84150-171">By default, a dependent task or set of tasks runs only after a parent task has completed successfully.</span></span> <span data-ttu-id="84150-172">В некоторых сценариях может потребоваться зависимые задачи toorun даже в случае сбоя hello родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="84150-172">In some scenarios, you may want toorun dependent tasks even if hello parent task fails.</span></span> <span data-ttu-id="84150-173">Можно переопределить поведение по умолчанию hello, указав действие зависимостей.</span><span class="sxs-lookup"><span data-stu-id="84150-173">You can override hello default behavior by specifying a dependency action.</span></span> <span data-ttu-id="84150-174">Действие зависимостей указывает, является ли выполнение зависимой задачи подходящих toorun, основании hello успешности hello родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="84150-174">A dependency action specifies whether a dependent task is eligible toorun, based on hello success or failure of hello parent task.</span></span> 

<span data-ttu-id="84150-175">Например предположим, что зависимая задача ожидает данные из hello завершения задачи вышестоящего hello.</span><span class="sxs-lookup"><span data-stu-id="84150-175">For example, suppose that a dependent task is awaiting data from hello completion of hello upstream task.</span></span> <span data-ttu-id="84150-176">В случае сбоя задачи вышестоящего hello hello зависимая задача по-прежнему возможно может toorun, с помощью старых данных.</span><span class="sxs-lookup"><span data-stu-id="84150-176">If hello upstream task fails, hello dependent task may still be able toorun using older data.</span></span> <span data-ttu-id="84150-177">В этом случае действия зависимостей можно указать hello зависимых она подходящих toorun несмотря на сбой hello hello родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="84150-177">In this case, a dependency action can specify that hello dependent task is eligible toorun despite hello failure of hello parent task.</span></span>

<span data-ttu-id="84150-178">Действие зависимостей зависит от условия выхода для hello родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="84150-178">A dependency action is based on an exit condition for hello parent task.</span></span> <span data-ttu-id="84150-179">Можно указать действие зависимостей для любого hello следующие условия выхода; для .NET, в разделе hello [ExitConditions] [ net_exitconditions] класс подробные сведения:</span><span class="sxs-lookup"><span data-stu-id="84150-179">You can specify a dependency action for any of hello following exit conditions; for .NET, see hello [ExitConditions][net_exitconditions] class for details:</span></span>

- <span data-ttu-id="84150-180">Если возникла ошибка предварительной обработки.</span><span class="sxs-lookup"><span data-stu-id="84150-180">When a pre-processing error occurs.</span></span>
- <span data-ttu-id="84150-181">Если возникла ошибка отправки файла.</span><span class="sxs-lookup"><span data-stu-id="84150-181">When a file upload error occurs.</span></span> <span data-ttu-id="84150-182">Если задачу hello завершает работу с кодом выхода, который указан через **exitCodes** или **exitCodeRanges**, а затем возникает ошибка передачи файла, указанное, приоритет имеет код выхода hello действие hello.</span><span class="sxs-lookup"><span data-stu-id="84150-182">If hello task exits with an exit code that was specified via **exitCodes** or **exitCodeRanges**, and then encounters a file upload error, hello action specified by hello exit code takes precedence.</span></span>
- <span data-ttu-id="84150-183">При выходе из задачу hello с кодом выхода, определяемый hello **ExitCodes** свойство.</span><span class="sxs-lookup"><span data-stu-id="84150-183">When hello task exits with an exit code defined by hello **ExitCodes** property.</span></span>
- <span data-ttu-id="84150-184">При выходе из задачу hello с кодом выхода, который попадает в диапазон, заданный hello **ExitCodeRanges** свойство.</span><span class="sxs-lookup"><span data-stu-id="84150-184">When hello task exits with an exit code that falls within a range specified by hello **ExitCodeRanges** property.</span></span>
- <span data-ttu-id="84150-185">Здравствуйте вариант по умолчанию, если задача hello завершается с кодом выхода, не заданные **ExitCodes** или **ExitCodeRanges**, или если hello задача завершается с предварительной обработки ошибок и hello **PreProcessingError**  свойство не задано, или если hello задачи завершается неудачей с файлом Загрузите ошибки и hello **FileUploadError** свойство не задано.</span><span class="sxs-lookup"><span data-stu-id="84150-185">hello default case, if hello task exits with an exit code not defined by **ExitCodes** or **ExitCodeRanges**, or if hello task exits with a pre-processing error and hello **PreProcessingError** property is not set, or if hello task fails with a file upload error and hello **FileUploadError** property is not set.</span></span> 

<span data-ttu-id="84150-186">toospecify действие зависимостей в .NET, набор hello [ExitOptions][net_exitoptions].[ DependencyAction] [ net_dependencyaction] свойство hello выходного условия.</span><span class="sxs-lookup"><span data-stu-id="84150-186">toospecify a dependency action in .NET, set hello [ExitOptions][net_exitoptions].[DependencyAction][net_dependencyaction] property for hello exit condition.</span></span> <span data-ttu-id="84150-187">Hello **DependencyAction** свойство принимает одно из двух значений:</span><span class="sxs-lookup"><span data-stu-id="84150-187">hello **DependencyAction** property takes one of two values:</span></span>

- <span data-ttu-id="84150-188">Параметр hello **DependencyAction** свойство слишком**Satisfy** означает, что зависимые задачи подходящих toorun Если hello родительская задача завершается с указанной ошибкой.</span><span class="sxs-lookup"><span data-stu-id="84150-188">Setting hello **DependencyAction** property too**Satisfy** indicates that dependent tasks are eligible toorun if hello parent task exits with a specified error.</span></span>
- <span data-ttu-id="84150-189">Параметр hello **DependencyAction** свойство слишком**блок** указывает, что зависимые задачи, подходящие toorun.</span><span class="sxs-lookup"><span data-stu-id="84150-189">Setting hello **DependencyAction** property too**Block** indicates that dependent tasks are not eligible toorun.</span></span>

<span data-ttu-id="84150-190">Здравствуйте, по умолчанию hello **DependencyAction** свойство **Satisfy** для код выхода 0, и **блок** для всех остальных условий выхода.</span><span class="sxs-lookup"><span data-stu-id="84150-190">hello default setting for hello **DependencyAction** property is **Satisfy** for exit code 0, and **Block** for all other exit conditions.</span></span>

<span data-ttu-id="84150-191">Hello следующий фрагмент кода задает hello **DependencyAction** свойство для родительской задачи.</span><span class="sxs-lookup"><span data-stu-id="84150-191">hello following code snippet sets hello **DependencyAction** property for a parent task.</span></span> <span data-ttu-id="84150-192">Если hello родительская задача завершается с предварительной обработки ошибок или с hello ошибки с заданными кодами hello зависимых задач заблокирована.</span><span class="sxs-lookup"><span data-stu-id="84150-192">If hello parent task exits with a pre-processing error, or with hello specified error codes, hello dependent task is blocked.</span></span> <span data-ttu-id="84150-193">Если родительская задача hello создано любая другая ошибка ненулевое значение, зависимую задачу hello — право toorun.</span><span class="sxs-lookup"><span data-stu-id="84150-193">If hello parent task exits with any other non-zero error, hello dependent task is eligible toorun.</span></span>

```csharp
// Task A is hello parent task.
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
        // If task A exits with hello specified error codes, block any downstream tasks (in this example, task B).
        ExitCodes = new List<ExitCodeMapping>
        {
            new ExitCodeMapping(10, new ExitOptions() { DependencyAction = DependencyAction.Block }),
            new ExitCodeMapping(20, new ExitOptions() { DependencyAction = DependencyAction.Block })
        },
        // If task A succeeds or fails with any other error, any downstream tasks become eligible toorun 
        // (in this example, task B).
        Default = new ExitOptions
        {
            DependencyAction = DependencyAction.Satisfy
        }
    }
},
// Task B depends on task A. Whether it becomes eligible toorun depends on how task A exits.
new CloudTask("B", "cmd.exe /c echo B")
{
    DependsOn = TaskDependencies.OnId("A")
},
```

## <a name="code-sample"></a><span data-ttu-id="84150-194">Пример кода</span><span class="sxs-lookup"><span data-stu-id="84150-194">Code sample</span></span>
<span data-ttu-id="84150-195">Hello [TaskDependencies] [ github_taskdependencies] образец проекта является одним из hello [образцы кода пакетной службы Azure] [ github_samples] на GitHub.</span><span class="sxs-lookup"><span data-stu-id="84150-195">hello [TaskDependencies][github_taskdependencies] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="84150-196">Это решение Visual Studio демонстрирует следующее:</span><span class="sxs-lookup"><span data-stu-id="84150-196">This Visual Studio solution demonstrates:</span></span>

- <span data-ttu-id="84150-197">Как tooenable задач зависимость от задания</span><span class="sxs-lookup"><span data-stu-id="84150-197">How tooenable task dependency on a job</span></span>
- <span data-ttu-id="84150-198">Как toocreate задачи зависят от других задач</span><span class="sxs-lookup"><span data-stu-id="84150-198">How toocreate tasks that depend on other tasks</span></span>
- <span data-ttu-id="84150-199">Выполнение tooexecute тех задач в пуле вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="84150-199">How tooexecute those tasks on a pool of compute nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84150-200">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="84150-200">Next steps</span></span>
### <a name="application-deployment"></a><span data-ttu-id="84150-201">Развертывание приложения</span><span class="sxs-lookup"><span data-stu-id="84150-201">Application deployment</span></span>
<span data-ttu-id="84150-202">Hello [пакетов приложений](batch-application-packages.md) пакета предоставляет простой способ развертывания tooboth и версия приложения hello, выполняемых задач на вычислительных узлах.</span><span class="sxs-lookup"><span data-stu-id="84150-202">hello [application packages](batch-application-packages.md) feature of Batch provides an easy way tooboth deploy and version hello applications that your tasks execute on compute nodes.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="84150-203">Установка приложений и промежуточных данных</span><span class="sxs-lookup"><span data-stu-id="84150-203">Installing applications and staging data</span></span>
<span data-ttu-id="84150-204">В разделе [установка приложений и данных в пакете размещения вычислительных узлов] [ forum_post] форуме пакетной службы Azure hello Обзор для подготовки узлов toorun задачи.</span><span class="sxs-lookup"><span data-stu-id="84150-204">See [Installing applications and staging data on Batch compute nodes][forum_post] in hello Azure Batch forum for an overview of methods for preparing your nodes toorun tasks.</span></span> <span data-ttu-id="84150-205">Записываются одним из членов команды hello пакетной службы Azure, эта статья — хороший учебник на toocopy приложения hello различными способами, входные данные задачи и другие файлы tooyour вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="84150-205">Written by one of hello Azure Batch team members, this post is a good primer on hello different ways toocopy applications, task input data, and other files tooyour compute nodes.</span></span>

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

[1]: ./media/batch-task-dependency/01_one_to_one.png "Схема: зависимость "один к одному""
[2]: ./media/batch-task-dependency/02_one_to_many.png "Схема: зависимость "один ко многим""
[3]: ./media/batch-task-dependency/03_task_id_range.png "Схема: зависимость диапазона идентификаторов задач"
