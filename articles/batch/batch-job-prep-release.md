---
title: "aaaCreate задачи tooprepare и завершения задания на вычислительных узлах - пакетной службы Azure | Документы Microsoft"
description: "При использовании данных toominimize задачи подготовки задания уровня передачи tooAzure пакетных вычислительных узлов и отпустите задачи для очистки узла по завершении задания."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 63d9d4f1-8521-4bbb-b95a-c4cad73692d3
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fd5fb47ae6700281e63048c49a1241f4e935baba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a><span data-ttu-id="6ec35-103">Выполнение задач подготовки и задач завершения заданий на вычислительных узлах пакетной службы</span><span class="sxs-lookup"><span data-stu-id="6ec35-103">Run job preparation and job release tasks on Batch compute nodes</span></span>

 <span data-ttu-id="6ec35-104">Для заданий пакетной службы Azure часто требуется определенная настройка перед выполнением задач и определенные действия по обслуживанию после завершения задач задания.</span><span class="sxs-lookup"><span data-stu-id="6ec35-104">An Azure Batch job often requires some form of setup before its tasks are executed, and post-job maintenance when its tasks are completed.</span></span> <span data-ttu-id="6ec35-105">Вам может потребоваться toodownload распространенные задачи ввода данных tooyour вычислительных узлов, или отправить tooAzure данных выходные данные задачи хранилища после завершения задания hello.</span><span class="sxs-lookup"><span data-stu-id="6ec35-105">You might need toodownload common task input data tooyour compute nodes, or upload task output data tooAzure Storage after hello job completes.</span></span> <span data-ttu-id="6ec35-106">Можно использовать **задания подготовки** и **задания выпуска** задачи tooperform этих операций.</span><span class="sxs-lookup"><span data-stu-id="6ec35-106">You can use **job preparation** and **job release** tasks tooperform these operations.</span></span>

## <a name="what-are-job-preparation-and-release-tasks"></a><span data-ttu-id="6ec35-107">Сведения о задачах подготовки и снятия заданий</span><span class="sxs-lookup"><span data-stu-id="6ec35-107">What are job preparation and release tasks?</span></span>
<span data-ttu-id="6ec35-108">Перед выполнением задачи задания задачу подготовки задания hello выполняется на все вычислительные узлы запланированных toorun хотя бы одна задача.</span><span class="sxs-lookup"><span data-stu-id="6ec35-108">Before a job's tasks run, hello job preparation task runs on all compute nodes scheduled toorun at least one task.</span></span> <span data-ttu-id="6ec35-109">После завершения задания hello задачу прекращения задания hello запускается на каждом узле в пуле hello, выполняется хотя бы одна задача.</span><span class="sxs-lookup"><span data-stu-id="6ec35-109">Once hello job is completed, hello job release task runs on each node in hello pool that executed at least one task.</span></span> <span data-ttu-id="6ec35-110">Как и в обычном пакетные задачи можно указать toobe командной строки, вызывается, когда подготовки задания или запустить задачу прекращения.</span><span class="sxs-lookup"><span data-stu-id="6ec35-110">As with normal Batch tasks, you can specify a command line toobe invoked when a job preparation or release task is run.</span></span>

<span data-ttu-id="6ec35-111">Задачи подготовки и завершения заданий предоставляют уже привычные возможности задач пакетной службы, такие как скачивание файла ([файлов ресурсов][net_job_prep_resourcefiles]), выполнение с повышенными правами, пользовательские переменные среды, максимальная продолжительность выполнения, число повторных попыток и период удержания файла.</span><span class="sxs-lookup"><span data-stu-id="6ec35-111">Job preparation and release tasks offer familiar Batch task features such as file download ([resource files][net_job_prep_resourcefiles]), elevated execution, custom environment variables, maximum execution duration, retry count, and file retention time.</span></span>

<span data-ttu-id="6ec35-112">В следующих разделах hello, вы узнаете, как toouse hello [JobPreparationTask] [ net_job_prep] и [JobReleaseTask] [ net_job_release] классы найти в hello [Пакета .NET] [ api_net] библиотеки.</span><span class="sxs-lookup"><span data-stu-id="6ec35-112">In hello following sections, you'll learn how toouse hello [JobPreparationTask][net_job_prep] and [JobReleaseTask][net_job_release] classes found in hello [Batch .NET][api_net] library.</span></span>

> [!TIP]
> <span data-ttu-id="6ec35-113">Задачи подготовки и снятия заданий особенно полезны в средах с общим пулом, в которых пул вычислительных узлов сохраняется между запусками заданий и может совместно использоваться различными заданиями.</span><span class="sxs-lookup"><span data-stu-id="6ec35-113">Job preparation and release tasks are especially helpful in "shared pool" environments, in which a pool of compute nodes persists between job runs and is used by many jobs.</span></span>
> 
> 

## <a name="when-toouse-job-preparation-and-release-tasks"></a><span data-ttu-id="6ec35-114">Когда toouse подготовки задания и освободить задачи</span><span class="sxs-lookup"><span data-stu-id="6ec35-114">When toouse job preparation and release tasks</span></span>
<span data-ttu-id="6ec35-115">Подготовки задания и задания выпуска задачи хорошо подходят для hello в следующих ситуациях:</span><span class="sxs-lookup"><span data-stu-id="6ec35-115">Job preparation and job release tasks are a good fit for hello following situations:</span></span>

<span data-ttu-id="6ec35-116">**Скачивание данных общих задач**</span><span class="sxs-lookup"><span data-stu-id="6ec35-116">**Download common task data**</span></span>

<span data-ttu-id="6ec35-117">Выполнение пакетных заданий часто требуется общий набор данных в качестве входного для hello рабочих заданий.</span><span class="sxs-lookup"><span data-stu-id="6ec35-117">Batch jobs often require a common set of data as input for hello job's tasks.</span></span> <span data-ttu-id="6ec35-118">Например ежедневно вычислений анализа рисков, рыночные данные — конкретного задания, но распространенные задачи tooall в задании hello.</span><span class="sxs-lookup"><span data-stu-id="6ec35-118">For example, in daily risk analysis calculations, market data is job-specific, yet common tooall tasks in hello job.</span></span> <span data-ttu-id="6ec35-119">Эти данные рынка, часто несколько гигабайт, должно быть загруженного tooeach вычислительного узла только один раз, чтобы его можно было использовать любую задачу, которая работает на узле hello.</span><span class="sxs-lookup"><span data-stu-id="6ec35-119">This market data, often several gigabytes in size, should be downloaded tooeach compute node only once so that any task that runs on hello node can use it.</span></span> <span data-ttu-id="6ec35-120">Используйте **задача подготовки задания** toodownload этот узел tooeach данных до выполнения hello задания hello и другие задачи.</span><span class="sxs-lookup"><span data-stu-id="6ec35-120">Use a **job preparation task** toodownload this data tooeach node before hello execution of hello job's other tasks.</span></span>

<span data-ttu-id="6ec35-121">**Удаление выходных данных заданий и задач**</span><span class="sxs-lookup"><span data-stu-id="6ec35-121">**Delete job and task output**</span></span>

<span data-ttu-id="6ec35-122">В среде "общих ресурсов пул», где пул вычислительных узлов не выводится из эксплуатации между заданиями, может потребоваться toodelete задания данные между запусками.</span><span class="sxs-lookup"><span data-stu-id="6ec35-122">In a "shared pool" environment, where a pool's compute nodes are not decommissioned between jobs, you may need toodelete job data between runs.</span></span> <span data-ttu-id="6ec35-123">Может потребоваться tooconserve дисковое пространство на узлах hello или удовлетворять политикам безопасности организации.</span><span class="sxs-lookup"><span data-stu-id="6ec35-123">You might need tooconserve disk space on hello nodes, or satisfy your organization's security policies.</span></span> <span data-ttu-id="6ec35-124">Используйте **задачу прекращения задания** toodelete данных, был загружен задача подготовки задания, созданные во время выполнения задачи.</span><span class="sxs-lookup"><span data-stu-id="6ec35-124">Use a **job release task** toodelete data that was downloaded by a job preparation task, or generated during task execution.</span></span>

<span data-ttu-id="6ec35-125">**Хранение журнала**</span><span class="sxs-lookup"><span data-stu-id="6ec35-125">**Log retention**</span></span>

<span data-ttu-id="6ec35-126">Может потребоваться tookeep копию файлов журнала, которые создают задач или возможно файлы аварийного дампа, возникают в результате сбоя приложения.</span><span class="sxs-lookup"><span data-stu-id="6ec35-126">You might want tookeep a copy of log files that your tasks generate, or perhaps crash dump files that can be generated by failed applications.</span></span> <span data-ttu-id="6ec35-127">Используйте **задачу прекращения задания** в таких случаях toocompress и передать этот данных tooan [хранилища Azure] [ azure_storage] учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6ec35-127">Use a **job release task** in such cases toocompress and upload this data tooan [Azure Storage][azure_storage] account.</span></span>

> [!TIP]
> <span data-ttu-id="6ec35-128">Другой способ toopersist журналов и других заданий и задач выходных данных — toouse hello [Azure пакетных файлов, принятых](batch-task-output.md) библиотеки.</span><span class="sxs-lookup"><span data-stu-id="6ec35-128">Another way toopersist logs and other job and task output data is toouse hello [Azure Batch File Conventions](batch-task-output.md) library.</span></span>
> 
> 

## <a name="job-preparation-task"></a><span data-ttu-id="6ec35-129">Задача подготовки задания</span><span class="sxs-lookup"><span data-stu-id="6ec35-129">Job preparation task</span></span>
<span data-ttu-id="6ec35-130">Перед выполнением задач «задания» пакет выполняет задачу подготовки задания hello на каждом вычислительном узле, toorun запланированные задачи.</span><span class="sxs-lookup"><span data-stu-id="6ec35-130">Before execution of a job's tasks, Batch executes hello job preparation task on each compute node that is scheduled toorun a task.</span></span> <span data-ttu-id="6ec35-131">По умолчанию hello пакетная служба ожидает завершения перед запуском tooexecute запланированные задачи hello на узле hello задач toobe hello задания подготовки.</span><span class="sxs-lookup"><span data-stu-id="6ec35-131">By default, hello Batch service waits for hello job preparation task toobe completed before running hello tasks scheduled tooexecute on hello node.</span></span> <span data-ttu-id="6ec35-132">Тем не менее можно настроить службу hello не toowait.</span><span class="sxs-lookup"><span data-stu-id="6ec35-132">However, you can configure hello service not toowait.</span></span> <span data-ttu-id="6ec35-133">Если узел hello перезапускается, задачу подготовки задания hello запускается снова, но это поведение можно отключить.</span><span class="sxs-lookup"><span data-stu-id="6ec35-133">If hello node restarts, hello job preparation task runs again, but you can also disable this behavior.</span></span>

<span data-ttu-id="6ec35-134">Задача подготовки задания Hello выполняется только на узлах, которые являются toorun запланированные задачи.</span><span class="sxs-lookup"><span data-stu-id="6ec35-134">hello job preparation task is executed only on nodes that are scheduled toorun a task.</span></span> <span data-ttu-id="6ec35-135">Это предотвращает hello ненужные выполнения задачи подготовки в случае, если узел не назначена задача.</span><span class="sxs-lookup"><span data-stu-id="6ec35-135">This prevents hello unnecessary execution of a preparation task in case a node is not assigned a task.</span></span> <span data-ttu-id="6ec35-136">Это может произойти, если количество hello задачи для задания меньше hello количество узлов в пул.</span><span class="sxs-lookup"><span data-stu-id="6ec35-136">This can occur when hello number of tasks for a job is less than hello number of nodes in a pool.</span></span> <span data-ttu-id="6ec35-137">Оно также применяется, когда [выполнение параллельных задач](batch-parallel-node-tasks.md) включен, если число задач hello меньше всего hello возможных параллельных задач оставляет некоторые узлы простоя.</span><span class="sxs-lookup"><span data-stu-id="6ec35-137">It also applies when [concurrent task execution](batch-parallel-node-tasks.md) is enabled, which leaves some nodes idle if hello task count is lower than hello total possible concurrent tasks.</span></span> <span data-ttu-id="6ec35-138">Не выполнив задачу подготовки задания hello простоя узлах, могут тратить сокращения затрат на расходы по передаче данных.</span><span class="sxs-lookup"><span data-stu-id="6ec35-138">By not running hello job preparation task on idle nodes, you can spend less money on data transfer charges.</span></span>

> [!NOTE]
> <span data-ttu-id="6ec35-139">[JobPreparationTask] [ net_job_prep_cloudjob] отличается от [CloudPool.StartTask] [ pool_starttask] в том, что JobPreparationTask выполняется в начале каждого задания hello, тогда как StartTask выполняется, только если вычислительный узел сначала производит соединение пула или перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="6ec35-139">[JobPreparationTask][net_job_prep_cloudjob] differs from [CloudPool.StartTask][pool_starttask] in that JobPreparationTask executes at hello start of each job, whereas StartTask executes only when a compute node first joins a pool or restarts.</span></span>
> 
> 

## <a name="job-release-task"></a><span data-ttu-id="6ec35-140">задачи снятия задания</span><span class="sxs-lookup"><span data-stu-id="6ec35-140">Job release task</span></span>
<span data-ttu-id="6ec35-141">После задания помечается как завершенная, задачу прекращения задания hello выполняется на каждом узле в пуле hello, выполняется хотя бы одна задача.</span><span class="sxs-lookup"><span data-stu-id="6ec35-141">Once a job is marked as completed, hello job release task is executed on each node in hello pool that executed at least one task.</span></span> <span data-ttu-id="6ec35-142">Чтобы пометить задание как завершенное, нужно направить запрос прекращения.</span><span class="sxs-lookup"><span data-stu-id="6ec35-142">You mark a job as completed by issuing a terminate request.</span></span> <span data-ttu-id="6ec35-143">Hello пакетной службы, а затем задает hello состояние задания слишком*Завершение*, завершает active или не запущены задачи, связанной с заданием hello и запускает задачу прекращения задания hello.</span><span class="sxs-lookup"><span data-stu-id="6ec35-143">hello Batch service then sets hello job state too*terminating*, terminates any active or running tasks associated with hello job, and runs hello job release task.</span></span> <span data-ttu-id="6ec35-144">Задание Hello затем перемещает toohello *завершения* состояния.</span><span class="sxs-lookup"><span data-stu-id="6ec35-144">hello job then moves toohello *completed* state.</span></span>

> [!NOTE]
> <span data-ttu-id="6ec35-145">Удаление задания также выполняет задачу прекращения задания hello.</span><span class="sxs-lookup"><span data-stu-id="6ec35-145">Job deletion also executes hello job release task.</span></span> <span data-ttu-id="6ec35-146">Тем не менее если задание уже был завершен, задачу hello выпуска не запускается повторно, если задание hello позже удаляется.</span><span class="sxs-lookup"><span data-stu-id="6ec35-146">However, if a job has already been terminated, hello release task is not run a second time if hello job is later deleted.</span></span>
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a><span data-ttu-id="6ec35-147">Задачи подготовки и снятия заданий с использованием пакетной службы .NET</span><span class="sxs-lookup"><span data-stu-id="6ec35-147">Job prep and release tasks with Batch .NET</span></span>
<span data-ttu-id="6ec35-148">назначить задачу подготовки задания toouse [JobPreparationTask] [ net_job_prep] tooyour задания объекта [CloudJob.JobPreparationTask] [ net_job_prep_cloudjob] свойство .</span><span class="sxs-lookup"><span data-stu-id="6ec35-148">toouse a job preparation task, assign a [JobPreparationTask][net_job_prep] object tooyour job's [CloudJob.JobPreparationTask][net_job_prep_cloudjob] property.</span></span> <span data-ttu-id="6ec35-149">Аналогичным образом инициализировать [JobReleaseTask] [ net_job_release] и назначьте его задание tooyour [CloudJob.JobReleaseTask] [ net_job_prep_cloudjob] свойство tooset hello Задание выпуска.</span><span class="sxs-lookup"><span data-stu-id="6ec35-149">Similarly, initialize a [JobReleaseTask][net_job_release] and assign it tooyour job's [CloudJob.JobReleaseTask][net_job_prep_cloudjob] property tooset hello job's release task.</span></span>

<span data-ttu-id="6ec35-150">В этом фрагменте кода `myBatchClient` является экземпляром класса [BatchClient][net_batch_client], и `myPool` является существующего пула внутри hello пакетной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6ec35-150">In this code snippet, `myBatchClient` is an instance of [BatchClient][net_batch_client], and `myPool` is an existing pool within hello Batch account.</span></span>

```csharp
// Create hello CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify hello command lines for hello job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign hello job preparation task toohello job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign hello job release task toohello job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

<span data-ttu-id="6ec35-151">Как упоминалось ранее, hello выпуска задач выполняется при удалении или завершение задания.</span><span class="sxs-lookup"><span data-stu-id="6ec35-151">As mentioned earlier, hello release task is executed when a job is terminated or deleted.</span></span> <span data-ttu-id="6ec35-152">Для завершения задания используется [JobOperations.TerminateJobAsync][net_job_terminate],</span><span class="sxs-lookup"><span data-stu-id="6ec35-152">Terminate a job with [JobOperations.TerminateJobAsync][net_job_terminate].</span></span> <span data-ttu-id="6ec35-153">а для удаления — [JobOperations.DeleteJobAsync][net_job_delete].</span><span class="sxs-lookup"><span data-stu-id="6ec35-153">Delete a job with [JobOperations.DeleteJobAsync][net_job_delete].</span></span> <span data-ttu-id="6ec35-154">Обычно оба эти действия выполняются после завершения задач задания или по истечении времени ожидания, которое было определено.</span><span class="sxs-lookup"><span data-stu-id="6ec35-154">You typically terminate or delete a job when its tasks are completed, or when a timeout that you've defined has been reached.</span></span>

```csharp
// Terminate hello job toomark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a><span data-ttu-id="6ec35-155">Пример кода на GitHub</span><span class="sxs-lookup"><span data-stu-id="6ec35-155">Code sample on GitHub</span></span>
<span data-ttu-id="6ec35-156">toosee Задание подготовки выпуска задачи и действия, извлечь hello [JobPrepRelease] [ job_prep_release_sample] примера проекта на GitHub.</span><span class="sxs-lookup"><span data-stu-id="6ec35-156">toosee job preparation and release tasks in action, check out hello [JobPrepRelease][job_prep_release_sample] sample project on GitHub.</span></span> <span data-ttu-id="6ec35-157">Это консольное приложение hello следующие:</span><span class="sxs-lookup"><span data-stu-id="6ec35-157">This console application does hello following:</span></span>

1. <span data-ttu-id="6ec35-158">Создает пул с двумя "небольшими" узлами.</span><span class="sxs-lookup"><span data-stu-id="6ec35-158">Creates a pool with two "small" nodes.</span></span>
2. <span data-ttu-id="6ec35-159">Создает задание с задачами подготовки задания, снятия задания и стандартными задачами.</span><span class="sxs-lookup"><span data-stu-id="6ec35-159">Creates a job with job preparation, release, and standard tasks.</span></span>
3. <span data-ttu-id="6ec35-160">Запускает hello задачи подготовки задания, который сначала записывает hello узел идентификатор tooa текстового файла в каталоге «общий» узла.</span><span class="sxs-lookup"><span data-stu-id="6ec35-160">Runs hello job preparation task, which first writes hello node ID tooa text file in a node's "shared" directory.</span></span>
4. <span data-ttu-id="6ec35-161">Выполняет задачу на каждом узле, который записывает его toohello идентификатор задачи текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="6ec35-161">Runs a task on each node that writes its task ID toohello same text file.</span></span>
5. <span data-ttu-id="6ec35-162">После завершения всех задач (или истечет время ожидания hello) печатает содержимое hello toohello файл консоли для каждого узла текста.</span><span class="sxs-lookup"><span data-stu-id="6ec35-162">Once all tasks are completed (or hello timeout is reached), prints hello contents of each node's text file toohello console.</span></span>
6. <span data-ttu-id="6ec35-163">По завершении задания hello запускает файл hello toodelete задач версии hello задания из узла "hello".</span><span class="sxs-lookup"><span data-stu-id="6ec35-163">When hello job is completed, runs hello job release task toodelete hello file from hello node.</span></span>
7. <span data-ttu-id="6ec35-164">Печатает hello коды подготовки задания hello завершения и выпуска задач для каждого узла, на котором выполняется.</span><span class="sxs-lookup"><span data-stu-id="6ec35-164">Prints hello exit codes of hello job preparation and release tasks for each node on which they executed.</span></span>
8. <span data-ttu-id="6ec35-165">Приостанавливает выполнение tooallow подтверждение удаления задания и/или пула.</span><span class="sxs-lookup"><span data-stu-id="6ec35-165">Pauses execution tooallow confirmation of job and/or pool deletion.</span></span>

<span data-ttu-id="6ec35-166">Выходные данные из образца приложения hello выглядят примерно следующие toohello:</span><span class="sxs-lookup"><span data-stu-id="6ec35-166">Output from hello sample application is similar toohello following:</span></span>

```
Attempting toocreate pool: JobPrepReleaseSamplePool
Created pool JobPrepReleaseSamplePool with 2 small nodes
Checking for existing job JobPrepReleaseSampleJob...
Job JobPrepReleaseSampleJob not found, creating...
Submitting tasks and awaiting completion...
All tasks completed.

Contents of shared\job_prep_and_release.txt on tvm-2434664350_1-20160623t173951z:
-------------------------------------------
tvm-2434664350_1-20160623t173951z tasks:
  task001
  task004
  task005
  task006

Contents of shared\job_prep_and_release.txt on tvm-2434664350_2-20160623t173951z:
-------------------------------------------
tvm-2434664350_2-20160623t173951z tasks:
  task008
  task002
  task003
  task007

Waiting for job JobPrepReleaseSampleJob tooreach state Completed
...

tvm-2434664350_1-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

tvm-2434664350_2-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

Delete job? [yes] no
yes
Delete pool? [yes] no
yes

Sample complete, hit ENTER tooexit...
```

> [!NOTE]
> <span data-ttu-id="6ec35-167">Из-за toohello переменной создания и время запуска узлов в новый пул (некоторые узлы готовы для задачи, прежде чем другие) может увидеть различные результаты.</span><span class="sxs-lookup"><span data-stu-id="6ec35-167">Due toohello variable creation and start time of nodes in a new pool (some nodes are ready for tasks before others), you may see different output.</span></span> <span data-ttu-id="6ec35-168">В частности из-за быстрого выполнения задач hello, один из узлов hello пула могут выполнять все задачи hello задания.</span><span class="sxs-lookup"><span data-stu-id="6ec35-168">Specifically, because hello tasks complete quickly, one of hello pool's nodes may execute all of hello job's tasks.</span></span> <span data-ttu-id="6ec35-169">В этом случае можно заметить, что hello подготовки задания и освободить задачи не существуют для узла hello, выполняемые задачи отсутствуют.</span><span class="sxs-lookup"><span data-stu-id="6ec35-169">If this occurs, you will notice that hello job prep and release tasks do not exist for hello node that executed no tasks.</span></span>
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-hello-azure-portal"></a><span data-ttu-id="6ec35-170">Проверять подготовки задания и задач выпуска в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="6ec35-170">Inspect job preparation and release tasks in hello Azure portal</span></span>
<span data-ttu-id="6ec35-171">При запуске образца приложения hello, можно использовать hello [портал Azure] [ portal] tooview hello свойства hello задания и его задачи, или даже Загрузите hello общего текстового файла, изменяемом hello рабочих заданий.</span><span class="sxs-lookup"><span data-stu-id="6ec35-171">When you run hello sample application, you can use hello [Azure portal][portal] tooview hello properties of hello job and its tasks, or even download hello shared text file that is modified by hello job's tasks.</span></span>

<span data-ttu-id="6ec35-172">Hello снимке экрана показано hello **колонке задачи подготовки** в hello портал Azure после запуска образца приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6ec35-172">hello screenshot below shows hello **Preparation tasks blade** in hello Azure portal after a run of hello sample application.</span></span> <span data-ttu-id="6ec35-173">Перейдите toohello *JobPrepReleaseSampleJob* свойства после завершения задачи (но до удаления задания и пула) и нажмите кнопку **задачи подготовки** или **выпусказадачи** tooview их свойства.</span><span class="sxs-lookup"><span data-stu-id="6ec35-173">Navigate toohello *JobPrepReleaseSampleJob* properties after your tasks have completed (but before deleting your job and pool) and click **Preparation tasks** or **Release tasks** tooview their properties.</span></span>

![Свойства подготовки задания на портале Azure][1]

## <a name="next-steps"></a><span data-ttu-id="6ec35-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6ec35-175">Next steps</span></span>
### <a name="application-packages"></a><span data-ttu-id="6ec35-176">Пакеты приложений</span><span class="sxs-lookup"><span data-stu-id="6ec35-176">Application packages</span></span>
<span data-ttu-id="6ec35-177">В задачи подготовки задания toohello сложения, можно также использовать hello [пакетов приложений](batch-application-packages.md) функция tooprepare пакетных вычислительных узлов для выполнения задач.</span><span class="sxs-lookup"><span data-stu-id="6ec35-177">In addition toohello job preparation task, you can also use hello [application packages](batch-application-packages.md) feature of Batch tooprepare compute nodes for task execution.</span></span> <span data-ttu-id="6ec35-178">Эта функция особенно полезна для развертывания приложений, которые не требуют выполнения установщика, приложений с большим числом файлов (более 100) и приложений, требующих строгого управления версиями.</span><span class="sxs-lookup"><span data-stu-id="6ec35-178">This feature is especially useful for deploying applications that do not require running an installer, applications that contain many (100+) files, or applications that require strict version control.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="6ec35-179">Установка приложений и промежуточных данных</span><span class="sxs-lookup"><span data-stu-id="6ec35-179">Installing applications and staging data</span></span>
<span data-ttu-id="6ec35-180">В этой публикации на форуме MSDN рассматриваются несколько методов подготовки узлов для выполнения задач:</span><span class="sxs-lookup"><span data-stu-id="6ec35-180">This MSDN forum post provides an overview of several methods of preparing your nodes for running tasks:</span></span>

<span data-ttu-id="6ec35-181">[Installing applications and staging data on Batch compute nodes][forum_post] (Установка приложений и промежуточное размещение данных на вычислительных узлах пакетной службы)</span><span class="sxs-lookup"><span data-stu-id="6ec35-181">[Installing applications and staging data on Batch compute nodes][forum_post]</span></span>

<span data-ttu-id="6ec35-182">Записываются одним из членов команды hello пакетной службы Azure, в нем описывается несколько методов, которые можно использовать узлы toocompute toodeploy приложениям и данным.</span><span class="sxs-lookup"><span data-stu-id="6ec35-182">Written by one of hello Azure Batch team members, it discusses several techniques that you can use toodeploy applications and data toocompute nodes.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[azure_storage]: https://azure.microsoft.com/services/storage/
[portal]: https://portal.azure.com
[job_prep_release_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/JobPrepRelease
[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]:https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_prep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_job_prep_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_job_prep_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.resourcefiles.aspx
[net_job_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.deletejobasync.aspx
[net_job_terminate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_job_release]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobreleasetask.aspx
[net_job_release_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[1]: ./media/batch-job-prep-release/portal-jobprep-01.png
