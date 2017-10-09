---
title: "Многоэкземплярные aaaUse задач приложений MPI toorun - пакетной службы Azure | Документы Microsoft"
description: "Узнайте, как тип tooexecute приложений интерфейса передачи сообщений (MPI), с помощью нескольких экземпляров задачу hello в пакете Azure."
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
ms.openlocfilehash: b0e3295a6aeb76267c26d5504bcff59de3dc5e22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-multi-instance-tasks-toorun-message-passing-interface-mpi-applications-in-batch"></a><span data-ttu-id="aa7eb-103">Использовать несколько экземпляров задач toorun интерфейса передачи сообщений (MPI) приложения в пакете</span><span class="sxs-lookup"><span data-stu-id="aa7eb-103">Use multi-instance tasks toorun Message Passing Interface (MPI) applications in Batch</span></span>

<span data-ttu-id="aa7eb-104">Многоэкземплярные задачи позволяют toorun задачу пакетной службы Azure на нескольких вычислительных узлах одновременно.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-104">Multi-instance tasks allow you toorun an Azure Batch task on multiple compute nodes simultaneously.</span></span> <span data-ttu-id="aa7eb-105">Эти задачи реализуют в пакетной службе такие сценарии высокопроизводительных вычислений, как приложения интерфейса передачи сообщений (MPI).</span><span class="sxs-lookup"><span data-stu-id="aa7eb-105">These tasks enable high performance computing scenarios like Message Passing Interface (MPI) applications in Batch.</span></span> <span data-ttu-id="aa7eb-106">В этой статье вы узнаете, как hello tooexecute многоэкземплярные задач с помощью [пакета .NET] [ api_net] библиотеки.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-106">In this article, you learn how tooexecute multi-instance tasks using hello [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> <span data-ttu-id="aa7eb-107">Hello примеры в этой статье уделено пакета .NET, MS-MPI и Windows вычислительных узлов, hello нескольких экземпляров задач понятия, описанные здесь, применимо tooother платформ и технологий (Python и Intel MPI на узлах Linux, например).</span><span class="sxs-lookup"><span data-stu-id="aa7eb-107">While hello examples in this article focus on Batch .NET, MS-MPI, and Windows compute nodes, hello multi-instance task concepts discussed here are applicable tooother platforms and technologies (Python and Intel MPI on Linux nodes, for example).</span></span>
>
>

## <a name="multi-instance-task-overview"></a><span data-ttu-id="aa7eb-108">Общие сведения о задачах с несколькими экземплярами</span><span class="sxs-lookup"><span data-stu-id="aa7eb-108">Multi-instance task overview</span></span>
<span data-ttu-id="aa7eb-109">В пакете, в каждой задачи — это обычно выполняются в одном вычислительном узле — Отправка задания tooa несколько задач и hello пакетная служба назначает каждой задачи для выполнения на узле.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-109">In Batch, each task is normally executed on a single compute node--you submit multiple tasks tooa job, and hello Batch service schedules each task for execution on a node.</span></span> <span data-ttu-id="aa7eb-110">Тем не менее, настроив задачи **параметры с несколькими экземплярами**, сообщите пакета tooinstead создать один основной задачей и нескольких подзадач, которые выполняются на нескольких узлах.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-110">However, by configuring a task's **multi-instance settings**, you tell Batch tooinstead create one primary task and several subtasks that are then executed on multiple nodes.</span></span>

<span data-ttu-id="aa7eb-111">![Общие сведения о задачах с несколькими экземплярами][1]</span><span class="sxs-lookup"><span data-stu-id="aa7eb-111">![Multi-instance task overview][1]</span></span>

<span data-ttu-id="aa7eb-112">При отправке задачи с несколькими экземплярами параметры tooa задания, пакет выполняет несколько задач уникальный toomulti экземпляр действия:</span><span class="sxs-lookup"><span data-stu-id="aa7eb-112">When you submit a task with multi-instance settings tooa job, Batch performs several steps unique toomulti-instance tasks:</span></span>

1. <span data-ttu-id="aa7eb-113">Hello пакетная служба создает одно **основной** и несколько **подзадачи** на основе параметров hello несколькими экземплярами.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-113">hello Batch service creates one **primary** and several **subtasks** based on hello multi-instance settings.</span></span> <span data-ttu-id="aa7eb-114">Общее число задач (основной плюс все подзадачи) Hello соответствует номеру hello **экземпляров** (вычислительных узлов) укажите в параметрах hello несколькими экземплярами.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-114">hello total number of tasks (primary plus all subtasks) matches hello number of **instances** (compute nodes) you specify in hello multi-instance settings.</span></span>
2. <span data-ttu-id="aa7eb-115">Определяет пакет, один hello вычислительные узлы как hello **master**, и расписания hello tooexecute основная задача образец hello.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-115">Batch designates one of hello compute nodes as hello **master**, and schedules hello primary task tooexecute on hello master.</span></span> <span data-ttu-id="aa7eb-116">Оно планирует tooexecute подзадачи hello на остаток hello hello вычислительных узлов выделенный toohello несколькими экземплярами задачи один подзадачи на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-116">It schedules hello subtasks tooexecute on hello remainder of hello compute nodes allocated toohello multi-instance task, one subtask per node.</span></span>
3. <span data-ttu-id="aa7eb-117">Hello первичной и всех подзадачи загрузить все **обычные файлы ресурсов** укажите в параметрах hello несколькими экземплярами.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-117">hello primary and all subtasks download any **common resource files** you specify in hello multi-instance settings.</span></span>
4. <span data-ttu-id="aa7eb-118">После загрузки hello обычные файлы ресурсов hello первичный и подзадачи выполнение hello **координации командной** укажите в параметрах hello несколькими экземплярами.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-118">After hello common resource files have been downloaded, hello primary and subtasks execute hello **coordination command** you specify in hello multi-instance settings.</span></span> <span data-ttu-id="aa7eb-119">Команда координации Hello — узлы tooprepare обычно используется для выполнения задачи hello.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-119">hello coordination command is typically used tooprepare nodes for executing hello task.</span></span> <span data-ttu-id="aa7eb-120">Это может включать запуск фоновых служб (таких как [Microsoft MPI][msmpi_msdn] `smpd.exe`) и проверка готовности tooprocess между узлами сообщения hello узлов.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-120">This can include starting background services (such as [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) and verifying that hello nodes are ready tooprocess inter-node messages.</span></span>
5. <span data-ttu-id="aa7eb-121">Основная задача Hello выполняет hello **команды приложения** на главном узле hello *после* hello координации команды успешно завершен, hello первичной и всех подзадач.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-121">hello primary task executes hello **application command** on hello master node *after* hello coordination command has been completed successfully by hello primary and all subtasks.</span></span> <span data-ttu-id="aa7eb-122">Команда приложения Hello Командная строка hello самой задачи многоэкземплярные hello и выполняется только основная задача hello.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-122">hello application command is hello command line of hello multi-instance task itself, and is executed only by hello primary task.</span></span> <span data-ttu-id="aa7eb-123">Например, вы можете запустить выполнение приложения с поддержкой MPI в решении на базе [MS-MPI][msmpi_msdn] с помощью команды `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-123">In an [MS-MPI][msmpi_msdn]-based solution, this is where you execute your MPI-enabled application using `mpiexec.exe`.</span></span>

> [!NOTE]
> <span data-ttu-id="aa7eb-124">Хотя функционально distinct, hello «многоэкземплярные task» не является типом уникальный задач как hello [StartTask] [ net_starttask] или [JobPreparationTask] [ net_jobprep].</span><span class="sxs-lookup"><span data-stu-id="aa7eb-124">Though it is functionally distinct, hello "multi-instance task" is not a unique task type like hello [StartTask][net_starttask] or [JobPreparationTask][net_jobprep].</span></span> <span data-ttu-id="aa7eb-125">Hello многоэкземплярные задача является просто стандартный пакет ([CloudTask] [ net_task] в пакете .NET) были настроены, параметры которого несколькими экземплярами.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-125">hello multi-instance task is simply a standard Batch task ([CloudTask][net_task] in Batch .NET) whose multi-instance settings have been configured.</span></span> <span data-ttu-id="aa7eb-126">В этой статье мы называем toothis как hello **задач с несколькими экземплярами**.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-126">In this article, we refer toothis as hello **multi-instance task**.</span></span>
>
>

## <a name="requirements-for-multi-instance-tasks"></a><span data-ttu-id="aa7eb-127">Требования к задачам с несколькими экземплярами</span><span class="sxs-lookup"><span data-stu-id="aa7eb-127">Requirements for multi-instance tasks</span></span>
<span data-ttu-id="aa7eb-128">При выполнении многоэкземплярной задачи требуется, чтобы в пуле был **включен обмен данными между узлами** и **отключено параллельное выполнение задач**.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-128">Multi-instance tasks require a pool with **inter-node communication enabled**, and with **concurrent task execution disabled**.</span></span> <span data-ttu-id="aa7eb-129">выполнение параллельных задач toodisable, набор hello [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) too1 свойство.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-129">toodisable concurrent task execution, set hello [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) property too1.</span></span>

<span data-ttu-id="aa7eb-130">Этот фрагмент кода показывает, как toocreate пул для нескольких экземпляров задачи с помощью библиотеки .NET пакета hello.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-130">This code snippet shows how toocreate a pool for multi-instance tasks using hello Batch .NET library.</span></span>

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
> <span data-ttu-id="aa7eb-131">При попытке toorun отключена задача нескольких экземпляров в пуле с связи между узлами или с *maxTasksPerNode* значение больше 1, задача hello никогда не запланирована--бесконечно остается в состоянии «Активно» hello.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-131">If you try toorun a multi-instance task in a pool with internode communication disabled, or with a *maxTasksPerNode* value greater than 1, hello task is never scheduled--it remains indefinitely in hello "active" state.</span></span> 
>
> <span data-ttu-id="aa7eb-132">Многоэкземплярные задачи могут выполняться только на узлах в пулах, созданных после 14 декабря 2015 года.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-132">Multi-instance tasks can execute only on nodes in pools created after 14 December 2015.</span></span>
>
>

### <a name="use-a-starttask-tooinstall-mpi"></a><span data-ttu-id="aa7eb-133">Используйте StartTask tooinstall MPI</span><span class="sxs-lookup"><span data-stu-id="aa7eb-133">Use a StartTask tooinstall MPI</span></span>
<span data-ttu-id="aa7eb-134">toorun приложений MPI с несколькими экземплярами задачей, необходимо сначала tooinstall реализации MPI (MS-MPI или MPI Intel, например) на вычислительных узлах hello в пуле hello.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-134">toorun MPI applications with a multi-instance task, you first need tooinstall an MPI implementation (MS-MPI or Intel MPI, for example) on hello compute nodes in hello pool.</span></span> <span data-ttu-id="aa7eb-135">Это подходящий момент toouse [StartTask][net_starttask], которое выполняется каждый раз, когда узел присоединяется пул, или перезапуска.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-135">This is a good time toouse a [StartTask][net_starttask], which executes whenever a node joins a pool, or is restarted.</span></span> <span data-ttu-id="aa7eb-136">Этот фрагмент кода создает StartTask, задающий hello MS-MPI пакет установки в виде [файла ресурсов][net_resourcefile].</span><span class="sxs-lookup"><span data-stu-id="aa7eb-136">This code snippet creates a StartTask that specifies hello MS-MPI setup package as a [resource file][net_resourcefile].</span></span> <span data-ttu-id="aa7eb-137">задачи запуска Hello командной строки выполняется после файла ресурсов hello загруженный toohello узла.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-137">hello start task's command line is executed after hello resource file is downloaded toohello node.</span></span> <span data-ttu-id="aa7eb-138">В этом случае hello Командная строка выполняет автоматическую установку MS-MPI.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-138">In this case, hello command line performs an unattended install of MS-MPI.</span></span>

```csharp
// Create a StartTask for hello pool which we use for installing MS-MPI on
// hello nodes as they join hello pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit hello fully configured pool toohello Batch service tooactually create
// hello pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a><span data-ttu-id="aa7eb-139">Удаленный доступ к памяти (RDMA)</span><span class="sxs-lookup"><span data-stu-id="aa7eb-139">Remote direct memory access (RDMA)</span></span>
<span data-ttu-id="aa7eb-140">При выборе [функцией RDMA размер](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) например A9 для hello вычислительных узлов в пуле пакета, приложения MPI могут воспользоваться преимуществами Azure высокой производительности и малой задержкой сети удаленного памяти (RDMA) доступ.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-140">When you choose an [RDMA-capable size](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) such as A9 for hello compute nodes in your Batch pool, your MPI application can take advantage of Azure's high-performance, low-latency remote direct memory access (RDMA) network.</span></span>

<span data-ttu-id="aa7eb-141">Найдите размеры hello, указанные как «Поддержкой RDMA» в hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="aa7eb-141">Look for hello sizes specified as "RDMA capable" in hello following articles:</span></span>

* <span data-ttu-id="aa7eb-142">Пулы **CloudServiceConfiguration**</span><span class="sxs-lookup"><span data-stu-id="aa7eb-142">**CloudServiceConfiguration** pools</span></span>

  * <span data-ttu-id="aa7eb-143">[Размеры для облачных служб](../cloud-services/cloud-services-sizes-specs.md) (только для Windows)</span><span class="sxs-lookup"><span data-stu-id="aa7eb-143">[Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (Windows only)</span></span>
* <span data-ttu-id="aa7eb-144">Пулы **VirtualMachineConfiguration**</span><span class="sxs-lookup"><span data-stu-id="aa7eb-144">**VirtualMachineConfiguration** pools</span></span>

  * <span data-ttu-id="aa7eb-145">[Размеры виртуальных машин в Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span><span class="sxs-lookup"><span data-stu-id="aa7eb-145">[Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span></span>
  * <span data-ttu-id="aa7eb-146">[Размеры виртуальных машин в Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span><span class="sxs-lookup"><span data-stu-id="aa7eb-146">[Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span></span>

> [!NOTE]
> <span data-ttu-id="aa7eb-147">преимущества tootake RDMA на [Linux вычислительных узлов](batch-linux-nodes.md), необходимо использовать **Intel MPI** на узлах hello.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-147">tootake advantage of RDMA on [Linux compute nodes](batch-linux-nodes.md), you must use **Intel MPI** on hello nodes.</span></span> <span data-ttu-id="aa7eb-148">Дополнительные сведения о CloudServiceConfiguration и VirtualMachineConfiguration пулов см. в разделе hello пула раздел hello [Обзор функций пакета](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="aa7eb-148">For more information on CloudServiceConfiguration and VirtualMachineConfiguration pools, see hello Pool section of hello [Batch feature overview](batch-api-basics.md).</span></span>
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a><span data-ttu-id="aa7eb-149">Создание задачи с несколькими экземплярами с помощью .NET для пакетной службы</span><span class="sxs-lookup"><span data-stu-id="aa7eb-149">Create a multi-instance task with Batch .NET</span></span>
<span data-ttu-id="aa7eb-150">Теперь, когда мы рассмотрели hello пула требований и установка пакета MPI, давайте создадим задачу hello несколькими экземплярами.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-150">Now that we've covered hello pool requirements and MPI package installation, let's create hello multi-instance task.</span></span> <span data-ttu-id="aa7eb-151">В этом фрагменте кода мы создадим стандартную задачу [CloudTask][net_task], а затем настроим ее свойство [MultiInstanceSettings][net_multiinstance_prop].</span><span class="sxs-lookup"><span data-stu-id="aa7eb-151">In this snippet, we create a standard [CloudTask][net_task], then configure its [MultiInstanceSettings][net_multiinstance_prop] property.</span></span> <span data-ttu-id="aa7eb-152">Как упоминалось ранее, задачу hello нескольких экземпляров не типом различных задач, а также стандартные задачи пакета настроены параметры с несколькими экземплярами.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-152">As mentioned earlier, hello multi-instance task is not a distinct task type, but a standard Batch task configured with multi-instance settings.</span></span>

```csharp
// Create hello multi-instance task. Its command line is hello "application command"
// and will be executed *only* by hello primary, and only after hello primary and
// subtasks execute hello CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure hello task's MultiInstanceSettings. hello CoordinationCommandLine will be executed by
// hello primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit hello task toohello job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on hello nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a><span data-ttu-id="aa7eb-153">Основная задача и подзадачи</span><span class="sxs-lookup"><span data-stu-id="aa7eb-153">Primary task and subtasks</span></span>
<span data-ttu-id="aa7eb-154">При создании нескольких экземпляров параметров задачи hello указываются hello количество вычислительных узлов, которые являются tooexecute задачу hello.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-154">When you create hello multi-instance settings for a task, you specify hello number of compute nodes that are tooexecute hello task.</span></span> <span data-ttu-id="aa7eb-155">При отправке задания tooa задача hello hello пакетная служба создает одно **основной** задач и достаточно **подзадачи** друг с другом, которые соответствуют hello количество узлов, указанной.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-155">When you submit hello task tooa job, hello Batch service creates one **primary** task and enough **subtasks** that together match hello number of nodes you specified.</span></span>

<span data-ttu-id="aa7eb-156">Эти задачи назначаются целочисленный идентификатор hello диапазона от 0 слишком*numberOfInstances* - 1.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-156">These tasks are assigned an integer id in hello range of 0 too*numberOfInstances* - 1.</span></span> <span data-ttu-id="aa7eb-157">Задача Hello с идентификатором 0 основная задача hello и другие идентификаторы, подзадачи.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-157">hello task with id 0 is hello primary task, and all other ids are subtasks.</span></span> <span data-ttu-id="aa7eb-158">Например при создании hello после настройки нескольких экземпляров для задачи, основная задача hello будет иметь идентификатор 0, и hello подзадачи будет иметь идентификаторы от 1 до 9.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-158">For example, if you create hello following multi-instance settings for a task, hello primary task would have an id of 0, and hello subtasks would have ids 1 through 9.</span></span>

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a><span data-ttu-id="aa7eb-159">Главный узел</span><span class="sxs-lookup"><span data-stu-id="aa7eb-159">Master node</span></span>
<span data-ttu-id="aa7eb-160">При отправке задачи нескольких экземпляров, hello пакетная служба назначает один hello вычислительные узлы «главный» узла hello и расписания hello tooexecute основная задача hello главного узла.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-160">When you submit a multi-instance task, hello Batch service designates one of hello compute nodes as hello "master" node, and schedules hello primary task tooexecute on hello master node.</span></span> <span data-ttu-id="aa7eb-161">Hello подзадачи, запланированных tooexecute на остаток hello hello узлов, выделенных задач toohello несколькими экземплярами.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-161">hello subtasks are scheduled tooexecute on hello remainder of hello nodes allocated toohello multi-instance task.</span></span>

## <a name="coordination-command"></a><span data-ttu-id="aa7eb-162">команду координации</span><span class="sxs-lookup"><span data-stu-id="aa7eb-162">Coordination command</span></span>
<span data-ttu-id="aa7eb-163">Hello **координации командной** выполняется путем hello первичный и подзадачи.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-163">hello **coordination command** is executed by both hello primary and subtasks.</span></span>

<span data-ttu-id="aa7eb-164">блокирует Hello вызова команды координации hello--пакета не выполняет команды приложения hello, пока hello координации команда вернула успешно для всех подзадач.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-164">hello invocation of hello coordination command is blocking--Batch does not execute hello application command until hello coordination command has returned successfully for all subtasks.</span></span> <span data-ttu-id="aa7eb-165">Hello координации командной таким образом следует запустить службы любой необходимый цвет фона, убедитесь, что они готовы для использования и завершает работу.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-165">hello coordination command should therefore start any required background services, verify that they are ready for use, and then exit.</span></span> <span data-ttu-id="aa7eb-166">Например эта команда координации для решения с использованием версии 7 MS-MPI запускает службу hello SMPD на узле hello, а затем завершает работу:</span><span class="sxs-lookup"><span data-stu-id="aa7eb-166">For example, this coordination command for a solution using MS-MPI version 7 starts hello SMPD service on hello node, then exits:</span></span>

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

<span data-ttu-id="aa7eb-167">Обратите внимание на использование hello `start` в этой команде координации.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-167">Note hello use of `start` in this coordination command.</span></span> <span data-ttu-id="aa7eb-168">Это необходимо, поскольку hello `smpd.exe` приложения не возвращается немедленно после выполнения.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-168">This is required because hello `smpd.exe` application does not return immediately after execution.</span></span> <span data-ttu-id="aa7eb-169">Без использования hello hello [запустить] [ cmd_start] команд, эта команда координации не вернет и поэтому заблокирует команды приложения hello.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-169">Without hello use of hello [start][cmd_start] command, this coordination command would not return, and would therefore block hello application command from running.</span></span>

## <a name="application-command"></a><span data-ttu-id="aa7eb-170">Команда приложения</span><span class="sxs-lookup"><span data-stu-id="aa7eb-170">Application command</span></span>
<span data-ttu-id="aa7eb-171">Когда основная задача hello и все подзадачи завершения выполнения команды координации hello, многоэкземплярных задачу hello командной строки выполняется путем основная задача hello *только*.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-171">Once hello primary task and all subtasks have finished executing hello coordination command, hello multi-instance task's command line is executed by hello primary task *only*.</span></span> <span data-ttu-id="aa7eb-172">Мы называем это hello **команды приложения** toodistinguish его из команды координации hello.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-172">We call this hello **application command** toodistinguish it from hello coordination command.</span></span>

<span data-ttu-id="aa7eb-173">Для приложений, MS-MPI, используйте hello приложения команды tooexecute приложения с поддержкой MPI `mpiexec.exe`.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-173">For MS-MPI applications, use hello application command tooexecute your MPI-enabled application with `mpiexec.exe`.</span></span> <span data-ttu-id="aa7eb-174">В качестве примера ниже приведена команда приложения для решения с использованием MS-MPI версии 7:</span><span class="sxs-lookup"><span data-stu-id="aa7eb-174">For example, here is an application command for a solution using MS-MPI version 7:</span></span>

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> <span data-ttu-id="aa7eb-175">Так как MS-MPI `mpiexec.exe` hello использует `CCP_NODES` переменной по умолчанию (в разделе [переменных среды](#environment-variables)) hello пример приложения командной строки выше исключает его.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-175">Because MS-MPI's `mpiexec.exe` uses hello `CCP_NODES` variable by default (see [Environment variables](#environment-variables)) hello example application command line above excludes it.</span></span>
>
>

## <a name="environment-variables"></a><span data-ttu-id="aa7eb-176">Переменные среды</span><span class="sxs-lookup"><span data-stu-id="aa7eb-176">Environment variables</span></span>
<span data-ttu-id="aa7eb-177">Пакет создается несколько [переменных среды] [ msdn_env_var] экземпляра toomulti задачи на hello вычислений tooa многоэкземплярные задач выделенных узлов.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-177">Batch creates several [environment variables][msdn_env_var] specific toomulti-instance tasks on hello compute nodes allocated tooa multi-instance task.</span></span> <span data-ttu-id="aa7eb-178">Командные строки координации и приложение может ссылаться эти переменные среды можно hello сценариев и программ, которые они выполняются.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-178">Your coordination and application command lines can reference these environment variables, as can hello scripts and programs they execute.</span></span>

<span data-ttu-id="aa7eb-179">Hello следующие переменные среды создаются службой hello пакета для использования с несколькими экземплярами задачи:</span><span class="sxs-lookup"><span data-stu-id="aa7eb-179">hello following environment variables are created by hello Batch service for use by multi-instance tasks:</span></span>

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

<span data-ttu-id="aa7eb-180">Полные сведения об этих и hello других пакета вычислительного узла переменные среды, включая их содержимое и видимость, в разделе [вычислений переменные среды узла][msdn_env_var].</span><span class="sxs-lookup"><span data-stu-id="aa7eb-180">For full details on these and hello other Batch compute node environment variables, including their contents and visibility, see [Compute node environment variables][msdn_env_var].</span></span>

> [!TIP]
> <span data-ttu-id="aa7eb-181">Образец кода Hello MPI Linux пакета содержит пример использования некоторые из этих переменных среды.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-181">hello Batch Linux MPI code sample contains an example of how several of these environment variables can be used.</span></span> <span data-ttu-id="aa7eb-182">Hello [cmd координации] [ coord_cmd_example] Bash скрипт загружает Общие приложения и входные файлы из хранилища Azure, обеспечивает общую папку сетевой файловой системы (NFS) на главном узле hello и настраивает hello другие узлы выделить toohello многоэкземплярные задач как клиенты NFS.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-182">hello [coordination-cmd][coord_cmd_example] Bash script downloads common application and input files from Azure Storage, enables a Network File System (NFS) share on hello master node, and configures hello other nodes allocated toohello multi-instance task as NFS clients.</span></span>
>
>

## <a name="resource-files"></a><span data-ttu-id="aa7eb-183">Файлы ресурсов</span><span class="sxs-lookup"><span data-stu-id="aa7eb-183">Resource files</span></span>
<span data-ttu-id="aa7eb-184">Существует два набора tooconsider файлы ресурсов для нескольких экземпляров задач: **обычные файлы ресурсов** , *все* задачи загрузки (основного и подзадачи) и hello **файлы ресурсов** для hello многоэкземплярные задач, который *основной hello* задач загрузки.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-184">There are two sets of resource files tooconsider for multi-instance tasks: **common resource files** that *all* tasks download (both primary and subtasks), and hello **resource files** specified for hello multi-instance task itself, which *only hello primary* task downloads.</span></span>

<span data-ttu-id="aa7eb-185">Можно указать один или несколько **обычные файлы ресурсов** в параметрах многоэкземплярные hello для задачи.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-185">You can specify one or more **common resource files** in hello multi-instance settings for a task.</span></span> <span data-ttu-id="aa7eb-186">Эти общие файлы ресурсов, загружаются из [хранилища Azure](../storage/common/storage-introduction.md) в каждом узле **каталог общих задач** hello первичной и всех подзадач.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-186">These common resource files are downloaded from [Azure Storage](../storage/common/storage-introduction.md) into each node's **task shared directory** by hello primary and all subtasks.</span></span> <span data-ttu-id="aa7eb-187">Каталог общих задач hello доступны из приложения и координации командной строки с помощью hello `AZ_BATCH_TASK_SHARED_DIR` переменной среды.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-187">You can access hello task shared directory from application and coordination command lines by using hello `AZ_BATCH_TASK_SHARED_DIR` environment variable.</span></span> <span data-ttu-id="aa7eb-188">Hello `AZ_BATCH_TASK_SHARED_DIR` пути идентичны для каждой задачи многоэкземплярные toohello выделенный узел, таким образом вы можете совместно использовать команду один координации между основной hello и все подзадачи.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-188">hello `AZ_BATCH_TASK_SHARED_DIR` path is identical on every node allocated toohello multi-instance task, thus you can share a single coordination command between hello primary and all subtasks.</span></span> <span data-ttu-id="aa7eb-189">Пакет не» тот» hello каталог в смысле удаленного доступа, но можно использовать в качестве монтирования или совместного использования точки, как упоминалось ранее в подсказке hello на переменных среды.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-189">Batch does not "share" hello directory in a remote access sense, but you can use it as a mount or share point as mentioned earlier in hello tip on environment variables.</span></span>

<span data-ttu-id="aa7eb-190">Файлы ресурсов, указанных для hello саму задачу многоэкземплярные: рабочий каталог загруженный toohello задач, `AZ_BATCH_TASK_WORKING_DIR`, по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-190">Resource files that you specify for hello multi-instance task itself are downloaded toohello task's working directory, `AZ_BATCH_TASK_WORKING_DIR`, by default.</span></span> <span data-ttu-id="aa7eb-191">В отличие от как уже упоминалось, toocommon файлы ресурсов, только hello основная задача загружает файлы ресурсов, указанный для саму задачу hello несколькими экземплярами.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-191">As mentioned, in contrast toocommon resource files, only hello primary task downloads resource files specified for hello  multi-instance task itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aa7eb-192">Всегда используйте переменные среды hello `AZ_BATCH_TASK_SHARED_DIR` и `AZ_BATCH_TASK_WORKING_DIR` toorefer toothese каталогов в вашей команды.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-192">Always use hello environment variables `AZ_BATCH_TASK_SHARED_DIR` and `AZ_BATCH_TASK_WORKING_DIR` toorefer toothese directories in your command lines.</span></span> <span data-ttu-id="aa7eb-193">Не пытайтесь пути hello tooconstruct вручную.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-193">Do not attempt tooconstruct hello paths manually.</span></span>
>
>

## <a name="task-lifetime"></a><span data-ttu-id="aa7eb-194">Срок действия задачи</span><span class="sxs-lookup"><span data-stu-id="aa7eb-194">Task lifetime</span></span>
<span data-ttu-id="aa7eb-195">время существования Hello hello основная задача элементы управления hello времени существования hello всего несколькими экземпляра задачи.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-195">hello lifetime of hello primary task controls hello lifetime of hello entire multi-instance task.</span></span> <span data-ttu-id="aa7eb-196">При выходе из первичного hello, завершаются все подзадачи hello.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-196">When hello primary exits, all of hello subtasks are terminated.</span></span> <span data-ttu-id="aa7eb-197">код выхода Hello hello основной — hello код выхода задачи «hello» и поэтому используется toodetermine hello успешности задачу hello целях повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-197">hello exit code of hello primary is hello exit code of hello task, and is therefore used toodetermine hello success or failure of hello task for retry purposes.</span></span>

<span data-ttu-id="aa7eb-198">В случае сбоя любой подзадачи hello выход с ненулевым кодом возврата, например, hello всего несколькими экземплярами задача завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-198">If any of hello subtasks fail, exiting with a non-zero return code, for example, hello entire multi-instance task fails.</span></span> <span data-ttu-id="aa7eb-199">затем многоэкземплярные задачу Hello завершается и повторить копирование tooits предел повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-199">hello multi-instance task is then terminated and retried, up tooits retry limit.</span></span>

<span data-ttu-id="aa7eb-200">При удалении задачи многоэкземплярные hello первичной и всех подзадачи удаляются hello пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-200">When you delete a multi-instance task, hello primary and all subtasks are also deleted by hello Batch service.</span></span> <span data-ttu-id="aa7eb-201">Все подзадачи каталоги и их файлы удаляются из hello вычислительных узлов, как и в случае стандартных задач.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-201">All subtask directories and their files are deleted from hello compute nodes, just as for a standard task.</span></span>

<span data-ttu-id="aa7eb-202">[TaskConstraints] [ net_taskconstraints] многоэкземплярные задачи, например hello [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime] [ net_taskconstraint_maxwallclock], и [RetentionTime] [ net_taskconstraint_retention] свойства, обрабатываются как они предназначены для стандартных задач, а также применить toohello первичная файловая группа и все подзадачи.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-202">[TaskConstraints][net_taskconstraints] for a multi-instance task, such as hello [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock], and [RetentionTime][net_taskconstraint_retention] properties, are honored as they are for a standard task, and apply toohello primary and all subtasks.</span></span> <span data-ttu-id="aa7eb-203">Однако если изменить hello [RetentionTime] [ net_taskconstraint_retention] задано после добавления задачи toohello hello нескольких экземпляров задания, это изменение применяется только toohello основная задача.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-203">However, if you change hello [RetentionTime][net_taskconstraint_retention] property after adding hello multi-instance task toohello job, this change is applied only toohello primary task.</span></span> <span data-ttu-id="aa7eb-204">Все подзадачи hello продолжить оригинал hello toouse [RetentionTime][net_taskconstraint_retention].</span><span class="sxs-lookup"><span data-stu-id="aa7eb-204">All of hello subtasks continue toouse hello original [RetentionTime][net_taskconstraint_retention].</span></span>

<span data-ttu-id="aa7eb-205">Вычислительный узел списка недавних задач отражает идентификатор hello подзадачей, если последние задачу hello входил в состав задачи нескольких экземпляров.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-205">A compute node's recent task list reflects hello id of a subtask if hello recent task was part of a multi-instance task.</span></span>

## <a name="obtain-information-about-subtasks"></a><span data-ttu-id="aa7eb-206">Получение сведений о подзадачах</span><span class="sxs-lookup"><span data-stu-id="aa7eb-206">Obtain information about subtasks</span></span>
<span data-ttu-id="aa7eb-207">tooobtain сведения на подзадачи, с помощью библиотеки .NET пакета hello, вызов hello [CloudTask.ListSubtasks] [ net_task_listsubtasks] метод.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-207">tooobtain information on subtasks by using hello Batch .NET library, call hello [CloudTask.ListSubtasks][net_task_listsubtasks] method.</span></span> <span data-ttu-id="aa7eb-208">Этот метод возвращает сведения о всех подзадачи и сведения о hello вычислительного узла, который выполнен hello задачи.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-208">This method returns information on all subtasks, and information about hello compute node that executed hello tasks.</span></span> <span data-ttu-id="aa7eb-209">По этим данным можно определить корневой каталог для каждой из них, идентификатор пула hello, текущего состояния, код выхода и многое другое.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-209">From this information, you can determine each subtask's root directory, hello pool id, its current state, exit code, and more.</span></span> <span data-ttu-id="aa7eb-210">Эти сведения можно использовать в сочетании с hello [PoolOperations.GetNodeFile] [ poolops_getnodefile] файлы метод tooobtain hello подзадач.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-210">You can use this information in combination with hello [PoolOperations.GetNodeFile][poolops_getnodefile] method tooobtain hello subtask's files.</span></span> <span data-ttu-id="aa7eb-211">Обратите внимание, что этот метод не возвращает сведения о основная задача hello (идентификатор 0).</span><span class="sxs-lookup"><span data-stu-id="aa7eb-211">Note that this method does not return information for hello primary task (id 0).</span></span>

> [!NOTE]
> <span data-ttu-id="aa7eb-212">Если не указано иное, пакет .NET методов, которые работают на hello нескольких экземпляров [CloudTask] [ net_task] сам применить *только* toohello основная задача.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-212">Unless otherwise stated, Batch .NET methods that operate on hello multi-instance [CloudTask][net_task] itself apply *only* toohello primary task.</span></span> <span data-ttu-id="aa7eb-213">Например, при вызове hello [CloudTask.ListNodeFiles] [ net_task_listnodefiles] метода задаче нескольких экземпляров, возвращаются только файлы, основная задача hello.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-213">For example, when you call hello [CloudTask.ListNodeFiles][net_task_listnodefiles] method on a multi-instance task, only hello primary task's files are returned.</span></span>
>
>

<span data-ttu-id="aa7eb-214">Hello следующий фрагмент кода показывает, как tooobtain подзадачи сведения, а также запрашивать содержимое файла hello узлы, на которых выполняется.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-214">hello following code snippet shows how tooobtain subtask information, as well as request file contents from hello nodes on which they executed.</span></span>

```csharp
// Obtain hello job and hello multi-instance task from hello Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain hello list of subtasks for hello task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over hello subtasks and print their stdout and stderr
// output if hello subtask has completed
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

## <a name="code-sample"></a><span data-ttu-id="aa7eb-215">Пример кода</span><span class="sxs-lookup"><span data-stu-id="aa7eb-215">Code sample</span></span>
<span data-ttu-id="aa7eb-216">Hello [MultiInstanceTasks] [ github_mpi] демонстрируется образец кода на GitHub как toouse нескольких экземпляров задач toorun [MS-MPI] [ msmpi_msdn] приложение в пакете вычислительных узлах.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-216">hello [MultiInstanceTasks][github_mpi] code sample on GitHub demonstrates how toouse a multi-instance task toorun an [MS-MPI][msmpi_msdn] application on Batch compute nodes.</span></span> <span data-ttu-id="aa7eb-217">Следуйте указаниям hello [подготовки](#preparation) и [выполнения](#execution) toorun образец hello.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-217">Follow hello steps in [Preparation](#preparation) and [Execution](#execution) toorun hello sample.</span></span>

### <a name="preparation"></a><span data-ttu-id="aa7eb-218">Подготовка</span><span class="sxs-lookup"><span data-stu-id="aa7eb-218">Preparation</span></span>
1. <span data-ttu-id="aa7eb-219">Выполните первые два действия hello в [как toocompile и выполните простой программы MS-MPI][msmpi_howto].</span><span class="sxs-lookup"><span data-stu-id="aa7eb-219">Follow hello first two steps in [How toocompile and run a simple MS-MPI program][msmpi_howto].</span></span> <span data-ttu-id="aa7eb-220">Это убеждает prerequesites hello для hello следующий шаг.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-220">This satisfies hello prerequesites for hello following step.</span></span>
2. <span data-ttu-id="aa7eb-221">Построение *выпуска* версии hello [MPIHelloWorld] [ helloworld_proj] MPI образец программы.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-221">Build a *Release* version of hello [MPIHelloWorld][helloworld_proj] sample MPI program.</span></span> <span data-ttu-id="aa7eb-222">Это hello программы, которая будет выполняться на вычислительных узлах задачу hello несколькими экземплярами.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-222">This is hello program that will be run on compute nodes by hello multi-instance task.</span></span>
3. <span data-ttu-id="aa7eb-223">Создайте ZIP-файл, содержащий файл `MPIHelloWorld.exe` (созданный на шаге 2) и `MSMpiSetup.exe` (скачанный на шаге 1).</span><span class="sxs-lookup"><span data-stu-id="aa7eb-223">Create a zip file containing `MPIHelloWorld.exe` (which you built step 2) and `MSMpiSetup.exe` (which you downloaded step 1).</span></span> <span data-ttu-id="aa7eb-224">Как пакет приложения hello следующем шаге вы отправите этот ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-224">You'll upload this zip file as an application package in hello next step.</span></span>
4. <span data-ttu-id="aa7eb-225">Используйте hello [портал Azure] [ portal] toocreate пакета [приложения](batch-application-packages.md) называется «MPIHelloWorld» и укажите hello ZIP-файл, созданный на предыдущем шаге hello в качестве версии «1.0» пакет приложения Hello.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-225">Use hello [Azure portal][portal] toocreate a Batch [application](batch-application-packages.md) called "MPIHelloWorld", and specify hello zip file you created in hello previous step as version "1.0" of hello application package.</span></span> <span data-ttu-id="aa7eb-226">Дополнительные сведения см. в разделе [Передача приложений и управление ими](batch-application-packages.md#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="aa7eb-226">See [Upload and manage applications](batch-application-packages.md#upload-and-manage-applications) for more information.</span></span>

> [!TIP]
> <span data-ttu-id="aa7eb-227">Построение *выпуска* версии `MPIHelloWorld.exe` , чтобы не нужно tooinclude никакие дополнительные зависимости (например, `msvcp140d.dll` или `vcruntime140d.dll`) в пакет приложения.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-227">Build a *Release* version of `MPIHelloWorld.exe` so that you don't have tooinclude any additional dependencies (for example, `msvcp140d.dll` or `vcruntime140d.dll`) in your application package.</span></span>
>
>

### <a name="execution"></a><span data-ttu-id="aa7eb-228">Выполнение</span><span class="sxs-lookup"><span data-stu-id="aa7eb-228">Execution</span></span>
1. <span data-ttu-id="aa7eb-229">Загрузите hello [образцы azure пакета] [ github_samples_zip] из GitHub.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-229">Download hello [azure-batch-samples][github_samples_zip] from GitHub.</span></span>
2. <span data-ttu-id="aa7eb-230">Откройте hello MultiInstanceTasks **решения** в Visual Studio 2015 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-230">Open hello MultiInstanceTasks **solution** in Visual Studio 2015 or newer.</span></span> <span data-ttu-id="aa7eb-231">Hello `MultiInstanceTasks.sln` решения файл находится в:</span><span class="sxs-lookup"><span data-stu-id="aa7eb-231">hello `MultiInstanceTasks.sln` solution file is located in:</span></span>

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. <span data-ttu-id="aa7eb-232">Ввести учетные данные учетной записи пакета и хранилища в `AccountSettings.settings` в hello **Microsoft.Azure.Batch.Samples.Common** проекта.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-232">Enter your Batch and Storage account credentials in `AccountSettings.settings` in hello **Microsoft.Azure.Batch.Samples.Common** project.</span></span>
4. <span data-ttu-id="aa7eb-233">**Построение и запуск** hello MultiInstanceTasks решения tooexecute hello MPI пример приложения на вычислительных узлов в пуле пакета.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-233">**Build and run** hello MultiInstanceTasks solution tooexecute hello MPI sample application on compute nodes in a Batch pool.</span></span>
5. <span data-ttu-id="aa7eb-234">*Необязательный*: hello используйте [портал Azure] [ portal] или hello [обозреватель пакета] [ batch_explorer] tooexamine пула образец hello, задания, и задачи («MultiInstanceSamplePool», «MultiInstanceSampleJob», «MultiInstanceSampleTask»), прежде чем удалить ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-234">*Optional*: Use hello [Azure portal][portal] or hello [Batch Explorer][batch_explorer] tooexamine hello sample pool, job, and task ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") before you delete hello resources.</span></span>

> [!TIP]
> <span data-ttu-id="aa7eb-235">Вы можете скачать [Visual Studio Community][visual_studio] бесплатно, если у вас нет Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-235">You can download [Visual Studio Community][visual_studio] for free if you do not have Visual Studio.</span></span>
>
>

<span data-ttu-id="aa7eb-236">Выходные данные `MultiInstanceTasks.exe` — примерно toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="aa7eb-236">Output from `MultiInstanceTasks.exe` is similar toohello following:</span></span>

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] toojob [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks toocomplete...

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

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="aa7eb-237">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aa7eb-237">Next steps</span></span>
* <span data-ttu-id="aa7eb-238">Hello Microsoft HPC и пакетной команды Azure блоге обсуждается [MPI поддержка Linux в Azure пакет][blog_mpi_linux]и включает сведения об использовании [OpenFOAM] [ openfoam] с использованием пакета.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-238">hello Microsoft HPC & Azure Batch Team blog discusses [MPI support for Linux on Azure Batch][blog_mpi_linux], and includes information on using [OpenFOAM][openfoam] with Batch.</span></span> <span data-ttu-id="aa7eb-239">Можно найти примеры кода Python для hello [пример OpenFOAM на GitHub][github_mpi].</span><span class="sxs-lookup"><span data-stu-id="aa7eb-239">You can find Python code samples for hello [OpenFOAM example on GitHub][github_mpi].</span></span>
* <span data-ttu-id="aa7eb-240">Узнайте, каким образом слишком[создание кластеров Linux вычислительные узлы](batch-linux-nodes.md) для использования в решениях Azure пакета MPI.</span><span class="sxs-lookup"><span data-stu-id="aa7eb-240">Learn how too[create pools of Linux compute nodes](batch-linux-nodes.md) for use in your Azure Batch MPI solutions.</span></span>

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
