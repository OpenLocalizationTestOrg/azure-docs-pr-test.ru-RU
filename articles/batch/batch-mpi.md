---
title: "Использование задач с несколькими экземплярами для выполнения приложений MPI с помощью пакетной службы Azure | Документация Майкрософт"
description: "Узнайте, как выполнять приложения с интерфейсом передачи сообщений (MPI), используя тип задачи с несколькими экземплярами в пакетной службе Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 83e34bd7-a027-4b1b-8314-759384719327
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: 5/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 77d12d6d48b22dfb3e7f09f273dffc11401bb15f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-multi-instance-tasks-to-run-message-passing-interface-mpi-applications-in-batch"></a><span data-ttu-id="30dd5-103">Использование задач с несколькими экземплярами для запуска приложений с интерфейсом передачи сообщений в пакетной службе</span><span class="sxs-lookup"><span data-stu-id="30dd5-103">Use multi-instance tasks to run Message Passing Interface (MPI) applications in Batch</span></span>

<span data-ttu-id="30dd5-104">Многоэкземплярные задачи позволяют выполнять задачи пакетной службы Azure на нескольких вычислительных узлах одновременно.</span><span class="sxs-lookup"><span data-stu-id="30dd5-104">Multi-instance tasks allow you to run an Azure Batch task on multiple compute nodes simultaneously.</span></span> <span data-ttu-id="30dd5-105">Эти задачи реализуют в пакетной службе такие сценарии высокопроизводительных вычислений, как приложения интерфейса передачи сообщений (MPI).</span><span class="sxs-lookup"><span data-stu-id="30dd5-105">These tasks enable high performance computing scenarios like Message Passing Interface (MPI) applications in Batch.</span></span> <span data-ttu-id="30dd5-106">Из этой статьи вы узнаете, как выполнять задачи с несколькими экземплярами с помощью библиотеки [.NET пакетной службы][api_net].</span><span class="sxs-lookup"><span data-stu-id="30dd5-106">In this article, you learn how to execute multi-instance tasks using the [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> <span data-ttu-id="30dd5-107">Примеры в этой статье посвящены вычислительным узлам Batch .NET, MS-MPI и Windows. Рассматриваемые здесь принципы выполнения многоэкземплярных задач применимы для других платформ и технологий (Python и Intel MPI на узлах Linux, например).</span><span class="sxs-lookup"><span data-stu-id="30dd5-107">While the examples in this article focus on Batch .NET, MS-MPI, and Windows compute nodes, the multi-instance task concepts discussed here are applicable to other platforms and technologies (Python and Intel MPI on Linux nodes, for example).</span></span>
>
>

## <a name="multi-instance-task-overview"></a><span data-ttu-id="30dd5-108">Общие сведения о задачах с несколькими экземплярами</span><span class="sxs-lookup"><span data-stu-id="30dd5-108">Multi-instance task overview</span></span>
<span data-ttu-id="30dd5-109">В пакетной службе каждая задача обычно выполняется на одном вычислительном узле: вы отправляете несколько задач в задание, и пакетная служба планирует выполнение каждой задачи на узле.</span><span class="sxs-lookup"><span data-stu-id="30dd5-109">In Batch, each task is normally executed on a single compute node--you submit multiple tasks to a job, and the Batch service schedules each task for execution on a node.</span></span> <span data-ttu-id="30dd5-110">Тем не менее, если настроить **параметры использования нескольких экземпляров** задачи, вы сообщите пакетной службе вместо этого создать одну основную задачу и несколько подзадач, которые выполняются на нескольких узлах.</span><span class="sxs-lookup"><span data-stu-id="30dd5-110">However, by configuring a task's **multi-instance settings**, you tell Batch to instead create one primary task and several subtasks that are then executed on multiple nodes.</span></span>

<span data-ttu-id="30dd5-111">![Общие сведения о задачах с несколькими экземплярами][1]</span><span class="sxs-lookup"><span data-stu-id="30dd5-111">![Multi-instance task overview][1]</span></span>

<span data-ttu-id="30dd5-112">При отправке задачи с несколькими экземплярами в задание пакетная служба выполняет определенные действия.</span><span class="sxs-lookup"><span data-stu-id="30dd5-112">When you submit a task with multi-instance settings to a job, Batch performs several steps unique to multi-instance tasks:</span></span>

1. <span data-ttu-id="30dd5-113">Пакетная служба создает одну **основную** задачу и несколько **подзадач** на основе параметров использования нескольких экземпляров.</span><span class="sxs-lookup"><span data-stu-id="30dd5-113">The Batch service creates one **primary** and several **subtasks** based on the multi-instance settings.</span></span> <span data-ttu-id="30dd5-114">Общее число задач (основная плюс все подзадачи) соответствует количеству **экземпляров** (вычислительных узлов), указанному в параметрах использования нескольких экземпляров.</span><span class="sxs-lookup"><span data-stu-id="30dd5-114">The total number of tasks (primary plus all subtasks) matches the number of **instances** (compute nodes) you specify in the multi-instance settings.</span></span>
2. <span data-ttu-id="30dd5-115">Пакетная служба назначает один из вычислительных узлов **главным** и планирует выполнение основной задачи на нем.</span><span class="sxs-lookup"><span data-stu-id="30dd5-115">Batch designates one of the compute nodes as the **master**, and schedules the primary task to execute on the master.</span></span> <span data-ttu-id="30dd5-116">Выполнение подзадач она планирует на остальных вычислительных узлах, выделенных для многоэкземплярной задачи, размещая по одной подзадаче на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="30dd5-116">It schedules the subtasks to execute on the remainder of the compute nodes allocated to the multi-instance task, one subtask per node.</span></span>
3. <span data-ttu-id="30dd5-117">Основная задача и все подзадачи скачивают **общие файлы ресурсов**, указанные в параметрах использования нескольких экземпляров.</span><span class="sxs-lookup"><span data-stu-id="30dd5-117">The primary and all subtasks download any **common resource files** you specify in the multi-instance settings.</span></span>
4. <span data-ttu-id="30dd5-118">Потом они выполняют **команду координации** , указанную в параметрах для множественных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="30dd5-118">After the common resource files have been downloaded, the primary and subtasks execute the **coordination command** you specify in the multi-instance settings.</span></span> <span data-ttu-id="30dd5-119">Команда координации обычно используется для подготовки узлов к выполнению задачи.</span><span class="sxs-lookup"><span data-stu-id="30dd5-119">The coordination command is typically used to prepare nodes for executing the task.</span></span> <span data-ttu-id="30dd5-120">Подготовка может включать в себя запуск фоновых служб (таких как `smpd.exe` [Microsoft MPI][msmpi_msdn]) и проверку готовности узлов к обработке сообщений, передаваемых между узлами.</span><span class="sxs-lookup"><span data-stu-id="30dd5-120">This can include starting background services (such as [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) and verifying that the nodes are ready to process inter-node messages.</span></span>
5. <span data-ttu-id="30dd5-121">*После* того, как основная задача и все подзадачи успешно выполнят команду координации, основная задача выполнит **команду приложения** на главном узле.</span><span class="sxs-lookup"><span data-stu-id="30dd5-121">The primary task executes the **application command** on the master node *after* the coordination command has been completed successfully by the primary and all subtasks.</span></span> <span data-ttu-id="30dd5-122">Команда приложения — это командная строка, указанная для многоэкземплярной задачи. Ее выполняет только основная задача.</span><span class="sxs-lookup"><span data-stu-id="30dd5-122">The application command is the command line of the multi-instance task itself, and is executed only by the primary task.</span></span> <span data-ttu-id="30dd5-123">Например, вы можете запустить выполнение приложения с поддержкой MPI в решении на базе [MS-MPI][msmpi_msdn] с помощью команды `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="30dd5-123">In an [MS-MPI][msmpi_msdn]-based solution, this is where you execute your MPI-enabled application using `mpiexec.exe`.</span></span>

> [!NOTE]
> <span data-ttu-id="30dd5-124">Хотя задача с несколькими экземплярами по функциональности отличается от остальных задач, она не относится к типу таких уникальных задач, как [StartTask][net_starttask] или [JobPreparationTask][net_jobprep].</span><span class="sxs-lookup"><span data-stu-id="30dd5-124">Though it is functionally distinct, the "multi-instance task" is not a unique task type like the [StartTask][net_starttask] or [JobPreparationTask][net_jobprep].</span></span> <span data-ttu-id="30dd5-125">Задача с несколькими экземплярами — это всего лишь стандартная задача пакетной службы ([CloudTask][net_task] в .NET пакетной службы) с настроенными параметрами нескольких экземпляров.</span><span class="sxs-lookup"><span data-stu-id="30dd5-125">The multi-instance task is simply a standard Batch task ([CloudTask][net_task] in Batch .NET) whose multi-instance settings have been configured.</span></span> <span data-ttu-id="30dd5-126">В этой статье задача такого типа называется **задачей с несколькими экземплярами**.</span><span class="sxs-lookup"><span data-stu-id="30dd5-126">In this article, we refer to this as the **multi-instance task**.</span></span>
>
>

## <a name="requirements-for-multi-instance-tasks"></a><span data-ttu-id="30dd5-127">Требования к задачам с несколькими экземплярами</span><span class="sxs-lookup"><span data-stu-id="30dd5-127">Requirements for multi-instance tasks</span></span>
<span data-ttu-id="30dd5-128">При выполнении многоэкземплярной задачи требуется, чтобы в пуле был **включен обмен данными между узлами** и **отключено параллельное выполнение задач**.</span><span class="sxs-lookup"><span data-stu-id="30dd5-128">Multi-instance tasks require a pool with **inter-node communication enabled**, and with **concurrent task execution disabled**.</span></span> <span data-ttu-id="30dd5-129">Чтобы отключить параллельное выполнение задач, задайте для свойства [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) значение 1.</span><span class="sxs-lookup"><span data-stu-id="30dd5-129">To disable concurrent task execution, set the [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) property to 1.</span></span>

<span data-ttu-id="30dd5-130">В этом фрагменте кода показано, как создать пул для многоэкземплярных задач, используя библиотеку .NET для пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="30dd5-130">This code snippet shows how to create a pool for multi-instance tasks using the Batch .NET library.</span></span>

```csharp
CloudPool myCloudPool =
    myBatchClient.PoolOperations.CreatePool(
        poolId: "MultiInstanceSamplePool",
        targetDedicatedComputeNodes: 3
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Multi-instance tasks require inter-node communication, and those nodes
// must run only one task at a time.
myCloudPool.InterComputeNodeCommunicationEnabled = true;
myCloudPool.MaxTasksPerComputeNode = 1;
```

> [!NOTE]
> <span data-ttu-id="30dd5-131">Если запустить многоэкземплярную задачу в пуле с отключенным обменом данными между узлами или со значением параметра *maxTasksPerNode* больше 1, задача не будет запланирована. Вместо этого она будет постоянно находиться в состоянии "Активно".</span><span class="sxs-lookup"><span data-stu-id="30dd5-131">If you try to run a multi-instance task in a pool with internode communication disabled, or with a *maxTasksPerNode* value greater than 1, the task is never scheduled--it remains indefinitely in the "active" state.</span></span> 
>
> <span data-ttu-id="30dd5-132">Многоэкземплярные задачи могут выполняться только на узлах в пулах, созданных после 14 декабря 2015 года.</span><span class="sxs-lookup"><span data-stu-id="30dd5-132">Multi-instance tasks can execute only on nodes in pools created after 14 December 2015.</span></span>
>
>

### <a name="use-a-starttask-to-install-mpi"></a><span data-ttu-id="30dd5-133">Установка MPI с помощью StartTask</span><span class="sxs-lookup"><span data-stu-id="30dd5-133">Use a StartTask to install MPI</span></span>
<span data-ttu-id="30dd5-134">Для выполнения приложений MPI с помощью задачи с несколькими экземплярами на вычислительных узлах в пуле сначала необходимо установить реализацию MPI (например, MS-MPI или Intel MPI).</span><span class="sxs-lookup"><span data-stu-id="30dd5-134">To run MPI applications with a multi-instance task, you first need to install an MPI implementation (MS-MPI or Intel MPI, for example) on the compute nodes in the pool.</span></span> <span data-ttu-id="30dd5-135">Это хорошая возможность воспользоваться задачей [StartTask][net_starttask], которая выполняется каждый раз при присоединении узла к пулу или его перезапуске.</span><span class="sxs-lookup"><span data-stu-id="30dd5-135">This is a good time to use a [StartTask][net_starttask], which executes whenever a node joins a pool, or is restarted.</span></span> <span data-ttu-id="30dd5-136">В этом фрагменте кода создается StartTask, указывающий пакет установки MS-MPI в качестве [файла ресурсов][net_resourcefile].</span><span class="sxs-lookup"><span data-stu-id="30dd5-136">This code snippet creates a StartTask that specifies the MS-MPI setup package as a [resource file][net_resourcefile].</span></span> <span data-ttu-id="30dd5-137">Командная строка задачи запуска выполняется после скачивания файла ресурсов на узел.</span><span class="sxs-lookup"><span data-stu-id="30dd5-137">The start task's command line is executed after the resource file is downloaded to the node.</span></span> <span data-ttu-id="30dd5-138">В этом случае командная строка выполняет автоматическую установку MS-MPI.</span><span class="sxs-lookup"><span data-stu-id="30dd5-138">In this case, the command line performs an unattended install of MS-MPI.</span></span>

```csharp
// Create a StartTask for the pool which we use for installing MS-MPI on
// the nodes as they join the pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit the fully configured pool to the Batch service to actually create
// the pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a><span data-ttu-id="30dd5-139">Удаленный доступ к памяти (RDMA)</span><span class="sxs-lookup"><span data-stu-id="30dd5-139">Remote direct memory access (RDMA)</span></span>
<span data-ttu-id="30dd5-140">Если для пула пакетной службы выбран [размер с поддержкой RDMA](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), например А9, то приложение MPI может воспользоваться преимуществами сети RDMA Azure с удаленным доступом к памяти, обеспечивающей высокую производительность и низкие задержки.</span><span class="sxs-lookup"><span data-stu-id="30dd5-140">When you choose an [RDMA-capable size](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) such as A9 for the compute nodes in your Batch pool, your MPI application can take advantage of Azure's high-performance, low-latency remote direct memory access (RDMA) network.</span></span>

<span data-ttu-id="30dd5-141">Сведения о размерах, указанных в качестве "С поддержкой RDMA", см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="30dd5-141">Look for the sizes specified as "RDMA capable" in the following articles:</span></span>

* <span data-ttu-id="30dd5-142">Пулы **CloudServiceConfiguration**</span><span class="sxs-lookup"><span data-stu-id="30dd5-142">**CloudServiceConfiguration** pools</span></span>

  * <span data-ttu-id="30dd5-143">[Размеры для облачных служб](../cloud-services/cloud-services-sizes-specs.md) (только для Windows)</span><span class="sxs-lookup"><span data-stu-id="30dd5-143">[Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (Windows only)</span></span>
* <span data-ttu-id="30dd5-144">Пулы **VirtualMachineConfiguration**</span><span class="sxs-lookup"><span data-stu-id="30dd5-144">**VirtualMachineConfiguration** pools</span></span>

  * <span data-ttu-id="30dd5-145">[Размеры виртуальных машин в Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span><span class="sxs-lookup"><span data-stu-id="30dd5-145">[Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span></span>
  * <span data-ttu-id="30dd5-146">[Размеры виртуальных машин в Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span><span class="sxs-lookup"><span data-stu-id="30dd5-146">[Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span></span>

> [!NOTE]
> <span data-ttu-id="30dd5-147">Чтобы воспользоваться преимуществами RDMA на [вычислительных узлах Linux](batch-linux-nodes.md), на узлах необходимо использовать **Intel MPI**.</span><span class="sxs-lookup"><span data-stu-id="30dd5-147">To take advantage of RDMA on [Linux compute nodes](batch-linux-nodes.md), you must use **Intel MPI** on the nodes.</span></span> <span data-ttu-id="30dd5-148">Дополнительные сведения о пулах CloudServiceConfiguration и VirtualMachineConfiguration см. в разделе "Пул" статьи [Обзор функций пакетной службы для разработчиков](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="30dd5-148">For more information on CloudServiceConfiguration and VirtualMachineConfiguration pools, see the Pool section of the [Batch feature overview](batch-api-basics.md).</span></span>
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a><span data-ttu-id="30dd5-149">Создание задачи с несколькими экземплярами с помощью .NET для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="30dd5-149">Create a multi-instance task with Batch .NET</span></span>
<span data-ttu-id="30dd5-150">Теперь после рассмотрения требований к пулу и установки пакета MPI самое время перейти к созданию задачи с несколькими экземплярами.</span><span class="sxs-lookup"><span data-stu-id="30dd5-150">Now that we've covered the pool requirements and MPI package installation, let's create the multi-instance task.</span></span> <span data-ttu-id="30dd5-151">В этом фрагменте кода мы создадим стандартную задачу [CloudTask][net_task], а затем настроим ее свойство [MultiInstanceSettings][net_multiinstance_prop].</span><span class="sxs-lookup"><span data-stu-id="30dd5-151">In this snippet, we create a standard [CloudTask][net_task], then configure its [MultiInstanceSettings][net_multiinstance_prop] property.</span></span> <span data-ttu-id="30dd5-152">Как упоминалось выше, многоэкземплярная задача не относится к особому типу задач, а является стандартной задачей пакетной службы, настраиваемой с помощью параметров для множественных экземпляров.</span><span class="sxs-lookup"><span data-stu-id="30dd5-152">As mentioned earlier, the multi-instance task is not a distinct task type, but a standard Batch task configured with multi-instance settings.</span></span>

```csharp
// Create the multi-instance task. Its command line is the "application command"
// and will be executed *only* by the primary, and only after the primary and
// subtasks execute the CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure the task's MultiInstanceSettings. The CoordinationCommandLine will be executed by
// the primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit the task to the job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on the nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a><span data-ttu-id="30dd5-153">Основная задача и подзадачи</span><span class="sxs-lookup"><span data-stu-id="30dd5-153">Primary task and subtasks</span></span>
<span data-ttu-id="30dd5-154">При создании параметров для множественных экземпляров для задачи нужно указать число вычислительных узлов, которые должны выполнять задачу.</span><span class="sxs-lookup"><span data-stu-id="30dd5-154">When you create the multi-instance settings for a task, you specify the number of compute nodes that are to execute the task.</span></span> <span data-ttu-id="30dd5-155">При отправке задачи в задание пакетная служба создает одну **основную** задачу и такое количество **подзадач**, которое вместе с основной задачей совпадает с указанным количеством узлов.</span><span class="sxs-lookup"><span data-stu-id="30dd5-155">When you submit the task to a job, the Batch service creates one **primary** task and enough **subtasks** that together match the number of nodes you specified.</span></span>

<span data-ttu-id="30dd5-156">Этим задачам назначается целочисленный идентификатор в диапазоне от 0 до *numberOfInstances* – 1.</span><span class="sxs-lookup"><span data-stu-id="30dd5-156">These tasks are assigned an integer id in the range of 0 to *numberOfInstances* - 1.</span></span> <span data-ttu-id="30dd5-157">Задача с идентификатором 0 — это основная задача, а все остальные идентификаторы назначаются подзадачам.</span><span class="sxs-lookup"><span data-stu-id="30dd5-157">The task with id 0 is the primary task, and all other ids are subtasks.</span></span> <span data-ttu-id="30dd5-158">Например, при создании следующих параметров нескольких экземпляров для задачи основная задача будет иметь идентификатор 0, а подзадачи — в диапазоне от 1 до 9.</span><span class="sxs-lookup"><span data-stu-id="30dd5-158">For example, if you create the following multi-instance settings for a task, the primary task would have an id of 0, and the subtasks would have ids 1 through 9.</span></span>

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a><span data-ttu-id="30dd5-159">Главный узел</span><span class="sxs-lookup"><span data-stu-id="30dd5-159">Master node</span></span>
<span data-ttu-id="30dd5-160">Когда вы отправляете многоэкземплярную задачу, пакетная служба назначает один из вычислительных узлов главным и планирует выполнение основной задачи на нем.</span><span class="sxs-lookup"><span data-stu-id="30dd5-160">When you submit a multi-instance task, the Batch service designates one of the compute nodes as the "master" node, and schedules the primary task to execute on the master node.</span></span> <span data-ttu-id="30dd5-161">Выполнение подзадач она планирует на остальных вычислительных узлах, выделенных для многоэкземплярной задачи.</span><span class="sxs-lookup"><span data-stu-id="30dd5-161">The subtasks are scheduled to execute on the remainder of the nodes allocated to the multi-instance task.</span></span>

## <a name="coordination-command"></a><span data-ttu-id="30dd5-162">команду координации</span><span class="sxs-lookup"><span data-stu-id="30dd5-162">Coordination command</span></span>
<span data-ttu-id="30dd5-163">**Команду координации** выполняют основная задача и подзадачи.</span><span class="sxs-lookup"><span data-stu-id="30dd5-163">The **coordination command** is executed by both the primary and subtasks.</span></span>

<span data-ttu-id="30dd5-164">Вызов команды координации блокируется: пакетная служба не выполнит команду приложения, пока команда координации не будет успешно возвращена для всех подзадач.</span><span class="sxs-lookup"><span data-stu-id="30dd5-164">The invocation of the coordination command is blocking--Batch does not execute the application command until the coordination command has returned successfully for all subtasks.</span></span> <span data-ttu-id="30dd5-165">Таким образом, команда координации должна запустить все необходимые фоновые службы. Убедитесь, что они готовы к использованию, а затем выполните выход.</span><span class="sxs-lookup"><span data-stu-id="30dd5-165">The coordination command should therefore start any required background services, verify that they are ready for use, and then exit.</span></span> <span data-ttu-id="30dd5-166">К примеру, эта команда координации для решения с использованием MS-MPI версии 7 запускает службу SMPD на узле, а затем завершает работу:</span><span class="sxs-lookup"><span data-stu-id="30dd5-166">For example, this coordination command for a solution using MS-MPI version 7 starts the SMPD service on the node, then exits:</span></span>

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

<span data-ttu-id="30dd5-167">Обратите внимание, что в этой команде координации используется `start` .</span><span class="sxs-lookup"><span data-stu-id="30dd5-167">Note the use of `start` in this coordination command.</span></span> <span data-ttu-id="30dd5-168">Это необходимо, так как приложение `smpd.exe` не возвращается сразу после выполнения.</span><span class="sxs-lookup"><span data-stu-id="30dd5-168">This is required because the `smpd.exe` application does not return immediately after execution.</span></span> <span data-ttu-id="30dd5-169">Если не использовать команду [start][cmd_start], то команда координации не возвращается и поэтому выполнение команды приложения блокируется.</span><span class="sxs-lookup"><span data-stu-id="30dd5-169">Without the use of the [start][cmd_start] command, this coordination command would not return, and would therefore block the application command from running.</span></span>

## <a name="application-command"></a><span data-ttu-id="30dd5-170">Команда приложения</span><span class="sxs-lookup"><span data-stu-id="30dd5-170">Application command</span></span>
<span data-ttu-id="30dd5-171">Если основная задача и все подзадачи выполнили команду координации, командную строку многоэкземплярной задачи выполняет *только*основная задача.</span><span class="sxs-lookup"><span data-stu-id="30dd5-171">Once the primary task and all subtasks have finished executing the coordination command, the multi-instance task's command line is executed by the primary task *only*.</span></span> <span data-ttu-id="30dd5-172">Назовем эту командную строку **командой приложения** , чтобы отличать ее от команды координации.</span><span class="sxs-lookup"><span data-stu-id="30dd5-172">We call this the **application command** to distinguish it from the coordination command.</span></span>

<span data-ttu-id="30dd5-173">Для приложений MS-MPI используйте команду приложения, чтобы выполнить приложение с поддержкой MPI с использованием `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="30dd5-173">For MS-MPI applications, use the application command to execute your MPI-enabled application with `mpiexec.exe`.</span></span> <span data-ttu-id="30dd5-174">В качестве примера ниже приведена команда приложения для решения с использованием MS-MPI версии 7:</span><span class="sxs-lookup"><span data-stu-id="30dd5-174">For example, here is an application command for a solution using MS-MPI version 7:</span></span>

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> <span data-ttu-id="30dd5-175">Так как команда `mpiexec.exe` приложений MS-MPI использует переменную `CCP_NODES` по умолчанию (см. раздел [Переменные среды](#environment-variables)), в примере командной строки приложения выше она исключена.</span><span class="sxs-lookup"><span data-stu-id="30dd5-175">Because MS-MPI's `mpiexec.exe` uses the `CCP_NODES` variable by default (see [Environment variables](#environment-variables)) the example application command line above excludes it.</span></span>
>
>

## <a name="environment-variables"></a><span data-ttu-id="30dd5-176">Переменные среды</span><span class="sxs-lookup"><span data-stu-id="30dd5-176">Environment variables</span></span>
<span data-ttu-id="30dd5-177">Пакетная служба создает несколько [переменных среды][msdn_env_var] для конкретных задач с несколькими экземплярами на вычислительных узлах, выделенных для каждой задачи с несколькими экземплярами.</span><span class="sxs-lookup"><span data-stu-id="30dd5-177">Batch creates several [environment variables][msdn_env_var] specific to multi-instance tasks on the compute nodes allocated to a multi-instance task.</span></span> <span data-ttu-id="30dd5-178">Командные строки координации и приложения могут ссылаться на эти переменные среды, как и сценарии и программы, выполняемые с их помощью.</span><span class="sxs-lookup"><span data-stu-id="30dd5-178">Your coordination and application command lines can reference these environment variables, as can the scripts and programs they execute.</span></span>

<span data-ttu-id="30dd5-179">Приведенные ниже переменные среды создаются пакетной службой для использования многоэкземплярными задачами.</span><span class="sxs-lookup"><span data-stu-id="30dd5-179">The following environment variables are created by the Batch service for use by multi-instance tasks:</span></span>

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

<span data-ttu-id="30dd5-180">Полные сведения об этих и других переменных среды вычислительных узлов пакетной службы, включая их содержимое и видимость, доступны в разделе [Azure Batch compute node environment variables][msdn_env_var] (Переменные среды вычислительных узлов пакетной службы Azure).</span><span class="sxs-lookup"><span data-stu-id="30dd5-180">For full details on these and the other Batch compute node environment variables, including their contents and visibility, see [Compute node environment variables][msdn_env_var].</span></span>

> [!TIP]
> <span data-ttu-id="30dd5-181">Фрагмент кода Linux MPI для пакетной службы содержит пример использования некоторых из этих переменных среды.</span><span class="sxs-lookup"><span data-stu-id="30dd5-181">The Batch Linux MPI code sample contains an example of how several of these environment variables can be used.</span></span> <span data-ttu-id="30dd5-182">Сценарий Bash [coordination-cmd][coord_cmd_example] скачивает общее приложение и входные файлы из службы хранилища Azure, открывает доступ к общему ресурсу NFS на главном узле и настраивает другие узлы, выделенные для задачи с несколькими экземплярами, как NFS-клиенты.</span><span class="sxs-lookup"><span data-stu-id="30dd5-182">The [coordination-cmd][coord_cmd_example] Bash script downloads common application and input files from Azure Storage, enables a Network File System (NFS) share on the master node, and configures the other nodes allocated to the multi-instance task as NFS clients.</span></span>
>
>

## <a name="resource-files"></a><span data-ttu-id="30dd5-183">Файлы ресурсов</span><span class="sxs-lookup"><span data-stu-id="30dd5-183">Resource files</span></span>
<span data-ttu-id="30dd5-184">Для многоэкземплярных задач есть два набора файлов ресурсов: **общие файлы ресурсов**, которые скачивают *все* задачи (основная задача и подзадачи), и **файлы ресурсов**, указанные непосредственно для многоэкземплярной задачи, которые скачивает *только основная* задача.</span><span class="sxs-lookup"><span data-stu-id="30dd5-184">There are two sets of resource files to consider for multi-instance tasks: **common resource files** that *all* tasks download (both primary and subtasks), and the **resource files** specified for the multi-instance task itself, which *only the primary* task downloads.</span></span>

<span data-ttu-id="30dd5-185">В параметрах для задачи с множественными экземплярами можно указать один или несколько **общих файлов ресурсов** .</span><span class="sxs-lookup"><span data-stu-id="30dd5-185">You can specify one or more **common resource files** in the multi-instance settings for a task.</span></span> <span data-ttu-id="30dd5-186">Основная задача и все подзадачи скачивают эти общие файлы ресурсов из [службы хранилища Azure](../storage/common/storage-introduction.md) в **общий каталог задач** каждого узла.</span><span class="sxs-lookup"><span data-stu-id="30dd5-186">These common resource files are downloaded from [Azure Storage](../storage/common/storage-introduction.md) into each node's **task shared directory** by the primary and all subtasks.</span></span> <span data-ttu-id="30dd5-187">Доступ к общему каталогу задачи можно получить из приложения и командной строки координации с помощью переменной среды `AZ_BATCH_TASK_SHARED_DIR` .</span><span class="sxs-lookup"><span data-stu-id="30dd5-187">You can access the task shared directory from application and coordination command lines by using the `AZ_BATCH_TASK_SHARED_DIR` environment variable.</span></span> <span data-ttu-id="30dd5-188">Пути `AZ_BATCH_TASK_SHARED_DIR` идентичны для каждого узла, выделенного многоэкземплярной задаче, поэтому можно использовать общую команду координации для основной задачи и всех подзадач.</span><span class="sxs-lookup"><span data-stu-id="30dd5-188">The `AZ_BATCH_TASK_SHARED_DIR` path is identical on every node allocated to the multi-instance task, thus you can share a single coordination command between the primary and all subtasks.</span></span> <span data-ttu-id="30dd5-189">Пакетная служба не предоставляет общий доступ к каталогу, как при удаленном доступе, но его можно использовать в качестве подключаемого каталога или общего ресурса, как упоминалось ранее в подсказке к переменным среды.</span><span class="sxs-lookup"><span data-stu-id="30dd5-189">Batch does not "share" the directory in a remote access sense, but you can use it as a mount or share point as mentioned earlier in the tip on environment variables.</span></span>

<span data-ttu-id="30dd5-190">Файлы ресурсов, указываемые для самой многоэкземплярной задачи, по умолчанию скачиваются в ее рабочий каталог, `AZ_BATCH_TASK_WORKING_DIR`.</span><span class="sxs-lookup"><span data-stu-id="30dd5-190">Resource files that you specify for the multi-instance task itself are downloaded to the task's working directory, `AZ_BATCH_TASK_WORKING_DIR`, by default.</span></span> <span data-ttu-id="30dd5-191">Как уже упоминалось, в отличие от общих файлов ресурсов, только основная задача скачивает файлы ресурсов, указанные для многоэкземплярной задачи.</span><span class="sxs-lookup"><span data-stu-id="30dd5-191">As mentioned, in contrast to common resource files, only the primary task downloads resource files specified for the  multi-instance task itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="30dd5-192">Для создания ссылок на эти каталоги в командной строке всегда используйте переменные среды `AZ_BATCH_TASK_SHARED_DIR` и `AZ_BATCH_TASK_WORKING_DIR`.</span><span class="sxs-lookup"><span data-stu-id="30dd5-192">Always use the environment variables `AZ_BATCH_TASK_SHARED_DIR` and `AZ_BATCH_TASK_WORKING_DIR` to refer to these directories in your command lines.</span></span> <span data-ttu-id="30dd5-193">Не пытайтесь создать пути вручную.</span><span class="sxs-lookup"><span data-stu-id="30dd5-193">Do not attempt to construct the paths manually.</span></span>
>
>

## <a name="task-lifetime"></a><span data-ttu-id="30dd5-194">Срок действия задачи</span><span class="sxs-lookup"><span data-stu-id="30dd5-194">Task lifetime</span></span>
<span data-ttu-id="30dd5-195">Срок действия основной задачи определяет срок действия всей задачи с несколькими экземплярами.</span><span class="sxs-lookup"><span data-stu-id="30dd5-195">The lifetime of the primary task controls the lifetime of the entire multi-instance task.</span></span> <span data-ttu-id="30dd5-196">При выходе из основной задачи завершаются все подзадачи.</span><span class="sxs-lookup"><span data-stu-id="30dd5-196">When the primary exits, all of the subtasks are terminated.</span></span> <span data-ttu-id="30dd5-197">Код выхода основной задачи — это код выхода самой задачи с несколькими экземплярами. На его основе можно определить, как завершилась задача (успешно или со сбоем), т. е. нужно ли выполнять повторные попытки.</span><span class="sxs-lookup"><span data-stu-id="30dd5-197">The exit code of the primary is the exit code of the task, and is therefore used to determine the success or failure of the task for retry purposes.</span></span>

<span data-ttu-id="30dd5-198">Если любая из подзадач завершается неудачно, например, выполняется выход с ненулевым кодом возврата, происходит сбой всей задачи с несколькими экземплярами.</span><span class="sxs-lookup"><span data-stu-id="30dd5-198">If any of the subtasks fail, exiting with a non-zero return code, for example, the entire multi-instance task fails.</span></span> <span data-ttu-id="30dd5-199">Затем задача с несколькими экземплярами завершается и выполняется повторно, пока не будет достигнут предел повтора.</span><span class="sxs-lookup"><span data-stu-id="30dd5-199">The multi-instance task is then terminated and retried, up to its retry limit.</span></span>

<span data-ttu-id="30dd5-200">При удалении задачи с несколькими экземплярами пакетная служба удаляет основную задачу и все подзадачи.</span><span class="sxs-lookup"><span data-stu-id="30dd5-200">When you delete a multi-instance task, the primary and all subtasks are also deleted by the Batch service.</span></span> <span data-ttu-id="30dd5-201">Все каталоги и файлы подзадач удаляются из вычислительных узлов также, как и при стандартной задаче.</span><span class="sxs-lookup"><span data-stu-id="30dd5-201">All subtask directories and their files are deleted from the compute nodes, just as for a standard task.</span></span>

<span data-ttu-id="30dd5-202">Свойства [TaskConstraints][net_taskconstraints] для задачи с несколькими экземплярами (включая [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock] и [RetentionTime][net_taskconstraint_retention]), обрабатываются как свойства для стандартной задачи и применяются к основной задаче и всем подзадачам.</span><span class="sxs-lookup"><span data-stu-id="30dd5-202">[TaskConstraints][net_taskconstraints] for a multi-instance task, such as the [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock], and [RetentionTime][net_taskconstraint_retention] properties, are honored as they are for a standard task, and apply to the primary and all subtasks.</span></span> <span data-ttu-id="30dd5-203">Но если изменить свойство [RetentionTime][net_taskconstraint_retention] после добавления задачи с несколькими экземплярами в задание, это изменение будет применено только к основной задаче.</span><span class="sxs-lookup"><span data-stu-id="30dd5-203">However, if you change the [RetentionTime][net_taskconstraint_retention] property after adding the multi-instance task to the job, this change is applied only to the primary task.</span></span> <span data-ttu-id="30dd5-204">Для всех подзадач и дальше будет использоваться исходное значение свойства [RetentionTime][net_taskconstraint_retention].</span><span class="sxs-lookup"><span data-stu-id="30dd5-204">All of the subtasks continue to use the original [RetentionTime][net_taskconstraint_retention].</span></span>

<span data-ttu-id="30dd5-205">Если последняя задача является частью многоэкземплярной задачи, в списке последних задач вычислительного узла отображается идентификатор подзадачи.</span><span class="sxs-lookup"><span data-stu-id="30dd5-205">A compute node's recent task list reflects the id of a subtask if the recent task was part of a multi-instance task.</span></span>

## <a name="obtain-information-about-subtasks"></a><span data-ttu-id="30dd5-206">Получение сведений о подзадачах</span><span class="sxs-lookup"><span data-stu-id="30dd5-206">Obtain information about subtasks</span></span>
<span data-ttu-id="30dd5-207">Чтобы получить сведения о подзадачах с помощью библиотеки .NET пакетной службы, вызовите метод [CloudTask.ListSubtasks][net_task_listsubtasks].</span><span class="sxs-lookup"><span data-stu-id="30dd5-207">To obtain information on subtasks by using the Batch .NET library, call the [CloudTask.ListSubtasks][net_task_listsubtasks] method.</span></span> <span data-ttu-id="30dd5-208">Этот метод возвращает сведения о всех подзадачах и вычислительном узле, на котором выполняются задачи.</span><span class="sxs-lookup"><span data-stu-id="30dd5-208">This method returns information on all subtasks, and information about the compute node that executed the tasks.</span></span> <span data-ttu-id="30dd5-209">Руководствуясь полученной информацией, можно определить корневой каталог каждой подзадачи, идентификатор пула, его текущее состояние, код выхода и многое другое.</span><span class="sxs-lookup"><span data-stu-id="30dd5-209">From this information, you can determine each subtask's root directory, the pool id, its current state, exit code, and more.</span></span> <span data-ttu-id="30dd5-210">Эти сведения можно использовать в сочетании с методом [PoolOperations.GetNodeFile][poolops_getnodefile], чтобы получить файлы подзадачи.</span><span class="sxs-lookup"><span data-stu-id="30dd5-210">You can use this information in combination with the [PoolOperations.GetNodeFile][poolops_getnodefile] method to obtain the subtask's files.</span></span> <span data-ttu-id="30dd5-211">Обратите внимание, что этот метод не возвращает сведения для основной задачи (идентификатор — 0).</span><span class="sxs-lookup"><span data-stu-id="30dd5-211">Note that this method does not return information for the primary task (id 0).</span></span>

> [!NOTE]
> <span data-ttu-id="30dd5-212">Если не указано иное, методы .NET пакетной службы, которые используются для задачи с несколькими экземплярами [CloudTask][net_task], применяются *только* к основной задаче.</span><span class="sxs-lookup"><span data-stu-id="30dd5-212">Unless otherwise stated, Batch .NET methods that operate on the multi-instance [CloudTask][net_task] itself apply *only* to the primary task.</span></span> <span data-ttu-id="30dd5-213">Например, при вызове метода [CloudTask.ListNodeFiles][net_task_listnodefiles] для задачи с несколькими экземплярами возвращаются только файлы основной задачи.</span><span class="sxs-lookup"><span data-stu-id="30dd5-213">For example, when you call the [CloudTask.ListNodeFiles][net_task_listnodefiles] method on a multi-instance task, only the primary task's files are returned.</span></span>
>
>

<span data-ttu-id="30dd5-214">В следующем фрагменте кода показано, как получить сведения о подзадачах, а также запросить содержимое файла из узлов, на которых выполняются эти подзадачи.</span><span class="sxs-lookup"><span data-stu-id="30dd5-214">The following code snippet shows how to obtain subtask information, as well as request file contents from the nodes on which they executed.</span></span>

```csharp
// Obtain the job and the multi-instance task from the Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain the list of subtasks for the task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over the subtasks and print their stdout and stderr
// output if the subtask has completed
await subtasks.ForEachAsync(async (subtask) =>
{
    Console.WriteLine("subtask: {0}", subtask.Id);
    Console.WriteLine("exit code: {0}", subtask.ExitCode);

    if (subtask.State == SubtaskState.Completed)
    {
        ComputeNode node =
            await batchClient.PoolOperations.GetComputeNodeAsync(subtask.ComputeNodeInformation.PoolId,
                                                                 subtask.ComputeNodeInformation.ComputeNodeId);

        NodeFile stdOutFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardOutFileName);
        NodeFile stdErrFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardErrorFileName);
        stdOut = await stdOutFile.ReadAsStringAsync();
        stdErr = await stdErrFile.ReadAsStringAsync();

        Console.WriteLine("node: {0}:", node.Id);
        Console.WriteLine("stdout.txt: {0}", stdOut);
        Console.WriteLine("stderr.txt: {0}", stdErr);
    }
    else
    {
        Console.WriteLine("\tSubtask {0} is in state {1}", subtask.Id, subtask.State);
    }
});
```

## <a name="code-sample"></a><span data-ttu-id="30dd5-215">Пример кода</span><span class="sxs-lookup"><span data-stu-id="30dd5-215">Code sample</span></span>
<span data-ttu-id="30dd5-216">В примере кода [MultiInstanceTasks][github_mpi] в GitHub демонстрируется использование задачи с несколькими экземплярами для запуска приложения [MS-MPI][msmpi_msdn] на вычислительных узлах пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="30dd5-216">The [MultiInstanceTasks][github_mpi] code sample on GitHub demonstrates how to use a multi-instance task to run an [MS-MPI][msmpi_msdn] application on Batch compute nodes.</span></span> <span data-ttu-id="30dd5-217">Чтобы запустить пример, следуйте указаниям, приведенным в разделах [Подготовка](#preparation) и [Выполнение](#execution).</span><span class="sxs-lookup"><span data-stu-id="30dd5-217">Follow the steps in [Preparation](#preparation) and [Execution](#execution) to run the sample.</span></span>

### <a name="preparation"></a><span data-ttu-id="30dd5-218">Подготовка</span><span class="sxs-lookup"><span data-stu-id="30dd5-218">Preparation</span></span>
1. <span data-ttu-id="30dd5-219">Выполните первые два шага в статье [How to compile and run a simple MS-MPI program][msmpi_howto] (Как скомпилировать и выполнить простую программу MS-MPI).</span><span class="sxs-lookup"><span data-stu-id="30dd5-219">Follow the first two steps in [How to compile and run a simple MS-MPI program][msmpi_howto].</span></span> <span data-ttu-id="30dd5-220">Это поможет выполнить предварительные требования к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="30dd5-220">This satisfies the prerequesites for the following step.</span></span>
2. <span data-ttu-id="30dd5-221">Создайте версию *Выпуск* примера программы MPI [MPIHelloWorld][helloworld_proj].</span><span class="sxs-lookup"><span data-stu-id="30dd5-221">Build a *Release* version of the [MPIHelloWorld][helloworld_proj] sample MPI program.</span></span> <span data-ttu-id="30dd5-222">Это программа, которую будет выполнять на вычислительных узлах задача с несколькими экземплярами.</span><span class="sxs-lookup"><span data-stu-id="30dd5-222">This is the program that will be run on compute nodes by the multi-instance task.</span></span>
3. <span data-ttu-id="30dd5-223">Создайте ZIP-файл, содержащий файл `MPIHelloWorld.exe` (созданный на шаге 2) и `MSMpiSetup.exe` (скачанный на шаге 1).</span><span class="sxs-lookup"><span data-stu-id="30dd5-223">Create a zip file containing `MPIHelloWorld.exe` (which you built step 2) and `MSMpiSetup.exe` (which you downloaded step 1).</span></span> <span data-ttu-id="30dd5-224">Вы отправите этот ZIP-файл как пакет приложения на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="30dd5-224">You'll upload this zip file as an application package in the next step.</span></span>
4. <span data-ttu-id="30dd5-225">Используйте [портал Azure][portal] для создания [приложения](batch-application-packages.md) пакетной службы с именем MPIHelloWorld и укажите ZIP-файл, созданный на предыдущем шаге, в качестве версии 1.0 пакета приложения.</span><span class="sxs-lookup"><span data-stu-id="30dd5-225">Use the [Azure portal][portal] to create a Batch [application](batch-application-packages.md) called "MPIHelloWorld", and specify the zip file you created in the previous step as version "1.0" of the application package.</span></span> <span data-ttu-id="30dd5-226">Дополнительные сведения см. в разделе [Передача приложений и управление ими](batch-application-packages.md#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="30dd5-226">See [Upload and manage applications](batch-application-packages.md#upload-and-manage-applications) for more information.</span></span>

> [!TIP]
> <span data-ttu-id="30dd5-227">Создайте версию *Выпуск* файла `MPIHelloWorld.exe`, чтобы в пакет приложения не нужно было включать какие-либо дополнительные зависимости (например, `msvcp140d.dll` или `vcruntime140d.dll`).</span><span class="sxs-lookup"><span data-stu-id="30dd5-227">Build a *Release* version of `MPIHelloWorld.exe` so that you don't have to include any additional dependencies (for example, `msvcp140d.dll` or `vcruntime140d.dll`) in your application package.</span></span>
>
>

### <a name="execution"></a><span data-ttu-id="30dd5-228">Выполнение</span><span class="sxs-lookup"><span data-stu-id="30dd5-228">Execution</span></span>
1. <span data-ttu-id="30dd5-229">Скачайте файл [azure-batch-samples][github_samples_zip] из GitHub.</span><span class="sxs-lookup"><span data-stu-id="30dd5-229">Download the [azure-batch-samples][github_samples_zip] from GitHub.</span></span>
2. <span data-ttu-id="30dd5-230">Откройте **решение** MultiInstanceTasks в Visual Studio 2015 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="30dd5-230">Open the MultiInstanceTasks **solution** in Visual Studio 2015 or newer.</span></span> <span data-ttu-id="30dd5-231">Файл решения `MultiInstanceTasks.sln` находится в следующем расположении:</span><span class="sxs-lookup"><span data-stu-id="30dd5-231">The `MultiInstanceTasks.sln` solution file is located in:</span></span>

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. <span data-ttu-id="30dd5-232">Введите данные своей учетной записи пакетной службы и учетной записи хранения в `AccountSettings.settings` в проекте **Microsoft.Azure.Batch.Samples.Common**.</span><span class="sxs-lookup"><span data-stu-id="30dd5-232">Enter your Batch and Storage account credentials in `AccountSettings.settings` in the **Microsoft.Azure.Batch.Samples.Common** project.</span></span>
4. <span data-ttu-id="30dd5-233">**Создайте и запустите** решение MultiInstanceTasks, чтобы выполнить пример приложения MPI на вычислительных узлах в пуле пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="30dd5-233">**Build and run** the MultiInstanceTasks solution to execute the MPI sample application on compute nodes in a Batch pool.</span></span>
5. <span data-ttu-id="30dd5-234">*Необязательно.* Используйте [портал Azure][portal] портал или [обозреватель пакетной службы][batch_explorer], чтобы проверить пример пула, задания и задачи (MultiInstanceSamplePool, MultiInstanceSampleJob, MultiInstanceSampleTask), прежде чем удалить ресурсы.</span><span class="sxs-lookup"><span data-stu-id="30dd5-234">*Optional*: Use the [Azure portal][portal] or the [Batch Explorer][batch_explorer] to examine the sample pool, job, and task ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") before you delete the resources.</span></span>

> [!TIP]
> <span data-ttu-id="30dd5-235">Вы можете скачать [Visual Studio Community][visual_studio] бесплатно, если у вас нет Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="30dd5-235">You can download [Visual Studio Community][visual_studio] for free if you do not have Visual Studio.</span></span>
>
>

<span data-ttu-id="30dd5-236">Результат `MultiInstanceTasks.exe` аналогичен приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="30dd5-236">Output from `MultiInstanceTasks.exe` is similar to the following:</span></span>

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] to job [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks to complete...

---- Subtask information ----
subtask: 1
        exit code: 0
        node: tvm-1219235766_3-20161017t162002z
        stdout.txt:
        stderr.txt:
subtask: 2
        exit code: 0
        node: tvm-1219235766_2-20161017t162002z
        stdout.txt:
        stderr.txt:

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="30dd5-237">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="30dd5-237">Next steps</span></span>
* <span data-ttu-id="30dd5-238">В блоге команды разработчиков для Microsoft HPC и пакетной службы Azure обсуждается [поддержка MPI для Linux в пакетной службе Azure][blog_mpi_linux] и предоставляются сведения об использовании [OpenFOAM][openfoam] с пакетной службой.</span><span class="sxs-lookup"><span data-stu-id="30dd5-238">The Microsoft HPC & Azure Batch Team blog discusses [MPI support for Linux on Azure Batch][blog_mpi_linux], and includes information on using [OpenFOAM][openfoam] with Batch.</span></span> <span data-ttu-id="30dd5-239">Фрагменты кода Python для [примера OpenFOAM можно найти на сайте GitHub][github_mpi].</span><span class="sxs-lookup"><span data-stu-id="30dd5-239">You can find Python code samples for the [OpenFOAM example on GitHub][github_mpi].</span></span>
* <span data-ttu-id="30dd5-240">Узнайте, как [создавать пулы на вычислительных узлах Linux](batch-linux-nodes.md) для использования в решениях MPI пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="30dd5-240">Learn how to [create pools of Linux compute nodes](batch-linux-nodes.md) for use in your Azure Batch MPI solutions.</span></span>

[helloworld_proj]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks/MPIHelloWorld

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[blog_mpi_linux]: https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/
[cmd_start]: https://technet.microsoft.com/library/cc770297.aspx
[coord_cmd_example]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/mpi/data/linux/openfoam/coordination-cmd
[github_mpi]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[msdn_env_var]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[msmpi_msdn]: https://msdn.microsoft.com/library/bb524831.aspx
[msmpi_sdk]: http://go.microsoft.com/FWLink/p/?LinkID=389556
[msmpi_howto]: http://blogs.technet.com/b/windowshpc/archive/2015/02/02/how-to-compile-and-run-a-simple-ms-mpi-program.aspx
[openfoam]: http://www.openfoam.com/
[visual_studio]: https://www.visualstudio.com/vs/community/

[net_jobprep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_multiinstance_class]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_multiinstance_prop]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.multiinstancesettings.aspx
[net_multiinsance_commonresfiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.commonresourcefiles.aspx
[net_multiinstance_coordcmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.coordinationcommandline.aspx
[net_multiinstance_numinstances]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.numberofinstances.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_cmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.commandline.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_taskconstraints]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.aspx
[net_taskconstraint_maxretry]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxtaskretrycount.aspx
[net_taskconstraint_maxwallclock]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxwallclocktime.aspx
[net_taskconstraint_retention]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.retentiontime.aspx
[net_task_listsubtasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listsubtasks.aspx
[net_task_listnodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[poolops_getnodefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getnodefile.aspx

[portal]: https://portal.azure.com
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx

[1]: ./media/batch-mpi/batch_mpi_01.png "Общие сведения о нескольких экземплярах"
