---
title: "Создание задач подготовки и завершения заданий на вычислительных узлах пакетной службы Azure | Документация Майкрософт"
description: "Используйте задачи подготовки на уровне задания для минимизации передачи данных на вычислительные узлы пакетной службы Azure и задачи снятия для очистки узла после завершения задания."
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
ms.openlocfilehash: 6a2525c02ce7bd3969469d2e28a5fccc948f89b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a><span data-ttu-id="8fd46-103">Выполнение задач подготовки и задач завершения заданий на вычислительных узлах пакетной службы</span><span class="sxs-lookup"><span data-stu-id="8fd46-103">Run job preparation and job release tasks on Batch compute nodes</span></span>

 <span data-ttu-id="8fd46-104">Для заданий пакетной службы Azure часто требуется определенная настройка перед выполнением задач и определенные действия по обслуживанию после завершения задач задания.</span><span class="sxs-lookup"><span data-stu-id="8fd46-104">An Azure Batch job often requires some form of setup before its tasks are executed, and post-job maintenance when its tasks are completed.</span></span> <span data-ttu-id="8fd46-105">Вам может понадобиться скачать входные данные общих задач на вычислительные узлы или отправить выходные данные задачи в службу хранилища Azure после завершения задания.</span><span class="sxs-lookup"><span data-stu-id="8fd46-105">You might need to download common task input data to your compute nodes, or upload task output data to Azure Storage after the job completes.</span></span> <span data-ttu-id="8fd46-106">Для выполнения этих операций можно использовать задачи **подготовки задания** и **прекращения задания**.</span><span class="sxs-lookup"><span data-stu-id="8fd46-106">You can use **job preparation** and **job release** tasks to perform these operations.</span></span>

## <a name="what-are-job-preparation-and-release-tasks"></a><span data-ttu-id="8fd46-107">Сведения о задачах подготовки и снятия заданий</span><span class="sxs-lookup"><span data-stu-id="8fd46-107">What are job preparation and release tasks?</span></span>
<span data-ttu-id="8fd46-108">Задача подготовки задания выполняется на всех вычислительных узлах, на которых запланирован запуск минимум одного задания, до выполнения задач задания.</span><span class="sxs-lookup"><span data-stu-id="8fd46-108">Before a job's tasks run, the job preparation task runs on all compute nodes scheduled to run at least one task.</span></span> <span data-ttu-id="8fd46-109">Когда задание завершается, на каждом узле в пуле, на котором была выполнена хотя бы одна задача, выполняется задача снятия задания.</span><span class="sxs-lookup"><span data-stu-id="8fd46-109">Once the job is completed, the job release task runs on each node in the pool that executed at least one task.</span></span> <span data-ttu-id="8fd46-110">Как и для обычных задач пакетной службы, для задач подготовки и снятия задания можно указать командную строку, вызываемую при выполнении задачи.</span><span class="sxs-lookup"><span data-stu-id="8fd46-110">As with normal Batch tasks, you can specify a command line to be invoked when a job preparation or release task is run.</span></span>

<span data-ttu-id="8fd46-111">Задачи подготовки и завершения заданий предоставляют уже привычные возможности задач пакетной службы, такие как скачивание файла ([файлов ресурсов][net_job_prep_resourcefiles]), выполнение с повышенными правами, пользовательские переменные среды, максимальная продолжительность выполнения, число повторных попыток и период удержания файла.</span><span class="sxs-lookup"><span data-stu-id="8fd46-111">Job preparation and release tasks offer familiar Batch task features such as file download ([resource files][net_job_prep_resourcefiles]), elevated execution, custom environment variables, maximum execution duration, retry count, and file retention time.</span></span>

<span data-ttu-id="8fd46-112">В следующих разделах вы узнаете, как использовать классы [JobPreparationTask][net_job_prep] и [JobReleaseTask][net_job_release], которые находятся в библиотеке [.NET пакетной службы][api_net].</span><span class="sxs-lookup"><span data-stu-id="8fd46-112">In the following sections, you'll learn how to use the [JobPreparationTask][net_job_prep] and [JobReleaseTask][net_job_release] classes found in the [Batch .NET][api_net] library.</span></span>

> [!TIP]
> <span data-ttu-id="8fd46-113">Задачи подготовки и снятия заданий особенно полезны в средах с общим пулом, в которых пул вычислительных узлов сохраняется между запусками заданий и может совместно использоваться различными заданиями.</span><span class="sxs-lookup"><span data-stu-id="8fd46-113">Job preparation and release tasks are especially helpful in "shared pool" environments, in which a pool of compute nodes persists between job runs and is used by many jobs.</span></span>
> 
> 

## <a name="when-to-use-job-preparation-and-release-tasks"></a><span data-ttu-id="8fd46-114">Когда используются задачи подготовки и снятия заданий</span><span class="sxs-lookup"><span data-stu-id="8fd46-114">When to use job preparation and release tasks</span></span>
<span data-ttu-id="8fd46-115">Задачи подготовки и снятия заданий отлично подходят для приведенных ниже сценариев.</span><span class="sxs-lookup"><span data-stu-id="8fd46-115">Job preparation and job release tasks are a good fit for the following situations:</span></span>

<span data-ttu-id="8fd46-116">**Скачивание данных общих задач**</span><span class="sxs-lookup"><span data-stu-id="8fd46-116">**Download common task data**</span></span>

<span data-ttu-id="8fd46-117">Для задач пакетных заданий часто требуется общий набор входных данных.</span><span class="sxs-lookup"><span data-stu-id="8fd46-117">Batch jobs often require a common set of data as input for the job's tasks.</span></span> <span data-ttu-id="8fd46-118">Например, в ежедневных расчетах по анализу рисков рыночные данные относятся к конкретному заданию, но являются общими для всех задач внутри этого задания.</span><span class="sxs-lookup"><span data-stu-id="8fd46-118">For example, in daily risk analysis calculations, market data is job-specific, yet common to all tasks in the job.</span></span> <span data-ttu-id="8fd46-119">Эти рыночные данные, зачастую объемом в несколько гигабайт, нужно скачать на каждый вычислительный узел только один раз, после чего их сможет использовать любая задача, которая выполняется на этом узле.</span><span class="sxs-lookup"><span data-stu-id="8fd46-119">This market data, often several gigabytes in size, should be downloaded to each compute node only once so that any task that runs on the node can use it.</span></span> <span data-ttu-id="8fd46-120">**Задача подготовки задания** позволяет скачать данные на все узлы перед выполнением других задач в задании.</span><span class="sxs-lookup"><span data-stu-id="8fd46-120">Use a **job preparation task** to download this data to each node before the execution of the job's other tasks.</span></span>

<span data-ttu-id="8fd46-121">**Удаление выходных данных заданий и задач**</span><span class="sxs-lookup"><span data-stu-id="8fd46-121">**Delete job and task output**</span></span>

<span data-ttu-id="8fd46-122">В среде общего пула, где вычислительные узлы пула не удаляются из пула между заданиями, может потребоваться удалять данные заданий между запусками</span><span class="sxs-lookup"><span data-stu-id="8fd46-122">In a "shared pool" environment, where a pool's compute nodes are not decommissioned between jobs, you may need to delete job data between runs.</span></span> <span data-ttu-id="8fd46-123">для экономии дискового пространства на узлах или в соответствии с политиками безопасности организации.</span><span class="sxs-lookup"><span data-stu-id="8fd46-123">You might need to conserve disk space on the nodes, or satisfy your organization's security policies.</span></span> <span data-ttu-id="8fd46-124">С помощью **задачи прекращения задания** можно удалить данные, скачанные задачей подготовки задания или созданные во время выполнения задачи.</span><span class="sxs-lookup"><span data-stu-id="8fd46-124">Use a **job release task** to delete data that was downloaded by a job preparation task, or generated during task execution.</span></span>

<span data-ttu-id="8fd46-125">**Хранение журнала**</span><span class="sxs-lookup"><span data-stu-id="8fd46-125">**Log retention**</span></span>

<span data-ttu-id="8fd46-126">Может возникнуть необходимость хранить копию файлов журнала, создаваемых задачами, или, например, файлы аварийных дампов, создаваемые приложениями, в которых возникает сбой.</span><span class="sxs-lookup"><span data-stu-id="8fd46-126">You might want to keep a copy of log files that your tasks generate, or perhaps crash dump files that can be generated by failed applications.</span></span> <span data-ttu-id="8fd46-127">В таких случаях с помощью **задачи снятия задания** можно сжать и передать эти данные в учетную запись [хранения Azure][azure_storage].</span><span class="sxs-lookup"><span data-stu-id="8fd46-127">Use a **job release task** in such cases to compress and upload this data to an [Azure Storage][azure_storage] account.</span></span>

> [!TIP]
> <span data-ttu-id="8fd46-128">Для хранения журналов и других выходных данных заданий и задач также можно использовать библиотеку [Azure Batch File Conventions](batch-task-output.md) .</span><span class="sxs-lookup"><span data-stu-id="8fd46-128">Another way to persist logs and other job and task output data is to use the [Azure Batch File Conventions](batch-task-output.md) library.</span></span>
> 
> 

## <a name="job-preparation-task"></a><span data-ttu-id="8fd46-129">Задача подготовки задания</span><span class="sxs-lookup"><span data-stu-id="8fd46-129">Job preparation task</span></span>
<span data-ttu-id="8fd46-130">Перед выполнением задач задания пакетная служба выполняет задачу подготовки задания на каждом вычислительном узле, где запланировано выполнение задач.</span><span class="sxs-lookup"><span data-stu-id="8fd46-130">Before execution of a job's tasks, Batch executes the job preparation task on each compute node that is scheduled to run a task.</span></span> <span data-ttu-id="8fd46-131">По умолчанию пакетная служба ожидает завершения задачи подготовки задания и только после этого запускает задачи, запланированные для выполнения на узле.</span><span class="sxs-lookup"><span data-stu-id="8fd46-131">By default, the Batch service waits for the job preparation task to be completed before running the tasks scheduled to execute on the node.</span></span> <span data-ttu-id="8fd46-132">Это ожидание можно отключить в настройках службы.</span><span class="sxs-lookup"><span data-stu-id="8fd46-132">However, you can configure the service not to wait.</span></span> <span data-ttu-id="8fd46-133">Задача подготовки задания запускается на вычислительном узле снова при перезапуске узла, но это поведение также можно отключить.</span><span class="sxs-lookup"><span data-stu-id="8fd46-133">If the node restarts, the job preparation task runs again, but you can also disable this behavior.</span></span>

<span data-ttu-id="8fd46-134">Задача подготовки задания выполняется только на узлах, на которых запланировано выполнение задач.</span><span class="sxs-lookup"><span data-stu-id="8fd46-134">The job preparation task is executed only on nodes that are scheduled to run a task.</span></span> <span data-ttu-id="8fd46-135">Благодаря этому на узлах, которым не назначены задачи, ненужная задача подготовки выполняться не будет.</span><span class="sxs-lookup"><span data-stu-id="8fd46-135">This prevents the unnecessary execution of a preparation task in case a node is not assigned a task.</span></span> <span data-ttu-id="8fd46-136">Это может произойти, если число задач в задании меньше количества узлов в пуле.</span><span class="sxs-lookup"><span data-stu-id="8fd46-136">This can occur when the number of tasks for a job is less than the number of nodes in a pool.</span></span> <span data-ttu-id="8fd46-137">То же самое происходит, когда включено [параллельное выполнение](batch-parallel-node-tasks.md) , в результате чего некоторые узлы бездействуют, если число задач оказывается меньше, чем общее число возможных параллельных задач.</span><span class="sxs-lookup"><span data-stu-id="8fd46-137">It also applies when [concurrent task execution](batch-parallel-node-tasks.md) is enabled, which leaves some nodes idle if the task count is lower than the total possible concurrent tasks.</span></span> <span data-ttu-id="8fd46-138">Не выполняя задачи по подготовке заданий на неактивных узлах, вы сократите свои расходы на передачу данных.</span><span class="sxs-lookup"><span data-stu-id="8fd46-138">By not running the job preparation task on idle nodes, you can spend less money on data transfer charges.</span></span>

> [!NOTE]
> <span data-ttu-id="8fd46-139">Задача [net_job_prep_cloudjob][net_job_prep_cloudjob] отличается от [CloudPool.StartTask][pool_starttask] тем, что задача JobPreparationTask выполняется в начале каждого задания, тогда как StartTask выполняется только при первом присоединении вычислительного узла к пулу или при его перезапуске.</span><span class="sxs-lookup"><span data-stu-id="8fd46-139">[JobPreparationTask][net_job_prep_cloudjob] differs from [CloudPool.StartTask][pool_starttask] in that JobPreparationTask executes at the start of each job, whereas StartTask executes only when a compute node first joins a pool or restarts.</span></span>
> 
> 

## <a name="job-release-task"></a><span data-ttu-id="8fd46-140">задачи снятия задания</span><span class="sxs-lookup"><span data-stu-id="8fd46-140">Job release task</span></span>
<span data-ttu-id="8fd46-141">Когда задание будет отмечено как завершенное, на каждом узле в пуле, на котором была выполнена хотя бы одна задача, выполняется задача снятия задания.</span><span class="sxs-lookup"><span data-stu-id="8fd46-141">Once a job is marked as completed, the job release task is executed on each node in the pool that executed at least one task.</span></span> <span data-ttu-id="8fd46-142">Чтобы пометить задание как завершенное, нужно направить запрос прекращения.</span><span class="sxs-lookup"><span data-stu-id="8fd46-142">You mark a job as completed by issuing a terminate request.</span></span> <span data-ttu-id="8fd46-143">После этого пакетная служба устанавливает состояние задания *Прекращение*, прекращает все активные или запущенные задачи, связанные с заданием, и запускает задачу снятия задания.</span><span class="sxs-lookup"><span data-stu-id="8fd46-143">The Batch service then sets the job state to *terminating*, terminates any active or running tasks associated with the job, and runs the job release task.</span></span> <span data-ttu-id="8fd46-144">Затем состояние задания меняется на *Завершено* .</span><span class="sxs-lookup"><span data-stu-id="8fd46-144">The job then moves to the *completed* state.</span></span>

> [!NOTE]
> <span data-ttu-id="8fd46-145">Задача снятия задания также выполняется при удалении задания.</span><span class="sxs-lookup"><span data-stu-id="8fd46-145">Job deletion also executes the job release task.</span></span> <span data-ttu-id="8fd46-146">Однако если задание уже было прекращено, задача снятия задания при последующем удалении задания вторично не выполняется.</span><span class="sxs-lookup"><span data-stu-id="8fd46-146">However, if a job has already been terminated, the release task is not run a second time if the job is later deleted.</span></span>
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a><span data-ttu-id="8fd46-147">Задачи подготовки и снятия заданий с использованием пакетной службы .NET</span><span class="sxs-lookup"><span data-stu-id="8fd46-147">Job prep and release tasks with Batch .NET</span></span>
<span data-ttu-id="8fd46-148">Чтобы использовать задачу подготовки задания, назначьте объект [JobPreparationTask][net_job_prep] свойству [CloudJob.JobPreparationTask][net_job_prep_cloudjob].</span><span class="sxs-lookup"><span data-stu-id="8fd46-148">To use a job preparation task, assign a [JobPreparationTask][net_job_prep] object to your job's [CloudJob.JobPreparationTask][net_job_prep_cloudjob] property.</span></span> <span data-ttu-id="8fd46-149">Аналогичным образом инициализируйте задачу [JobReleaseTask][net_job_release] и назначьте ее свойству [CloudJob.JobReleaseTask][net_job_prep_cloudjob] задания, чтобы настроить задачу снятия задания.</span><span class="sxs-lookup"><span data-stu-id="8fd46-149">Similarly, initialize a [JobReleaseTask][net_job_release] and assign it to your job's [CloudJob.JobReleaseTask][net_job_prep_cloudjob] property to set the job's release task.</span></span>

<span data-ttu-id="8fd46-150">В этом фрагменте кода `myBatchClient` представляет собой экземпляр [BatchClient][net_batch_client], а `myPool` — существующий пул в учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="8fd46-150">In this code snippet, `myBatchClient` is an instance of [BatchClient][net_batch_client], and `myPool` is an existing pool within the Batch account.</span></span>

```csharp
// Create the CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify the command lines for the job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign the job preparation task to the job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign the job release task to the job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

<span data-ttu-id="8fd46-151">Как упоминалось выше, задача снятия выполняется, когда задание прекращается или удаляется.</span><span class="sxs-lookup"><span data-stu-id="8fd46-151">As mentioned earlier, the release task is executed when a job is terminated or deleted.</span></span> <span data-ttu-id="8fd46-152">Для завершения задания используется [JobOperations.TerminateJobAsync][net_job_terminate],</span><span class="sxs-lookup"><span data-stu-id="8fd46-152">Terminate a job with [JobOperations.TerminateJobAsync][net_job_terminate].</span></span> <span data-ttu-id="8fd46-153">а для удаления — [JobOperations.DeleteJobAsync][net_job_delete].</span><span class="sxs-lookup"><span data-stu-id="8fd46-153">Delete a job with [JobOperations.DeleteJobAsync][net_job_delete].</span></span> <span data-ttu-id="8fd46-154">Обычно оба эти действия выполняются после завершения задач задания или по истечении времени ожидания, которое было определено.</span><span class="sxs-lookup"><span data-stu-id="8fd46-154">You typically terminate or delete a job when its tasks are completed, or when a timeout that you've defined has been reached.</span></span>

```csharp
// Terminate the job to mark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a><span data-ttu-id="8fd46-155">Пример кода на GitHub</span><span class="sxs-lookup"><span data-stu-id="8fd46-155">Code sample on GitHub</span></span>
<span data-ttu-id="8fd46-156">В примере проекта [JobPrepRelease][job_prep_release_sample] с сайта GitHub можно ознакомиться с действием задач подготовки и снятия задания.</span><span class="sxs-lookup"><span data-stu-id="8fd46-156">To see job preparation and release tasks in action, check out the [JobPrepRelease][job_prep_release_sample] sample project on GitHub.</span></span> <span data-ttu-id="8fd46-157">Это консольное приложение выполняет следующее.</span><span class="sxs-lookup"><span data-stu-id="8fd46-157">This console application does the following:</span></span>

1. <span data-ttu-id="8fd46-158">Создает пул с двумя "небольшими" узлами.</span><span class="sxs-lookup"><span data-stu-id="8fd46-158">Creates a pool with two "small" nodes.</span></span>
2. <span data-ttu-id="8fd46-159">Создает задание с задачами подготовки задания, снятия задания и стандартными задачами.</span><span class="sxs-lookup"><span data-stu-id="8fd46-159">Creates a job with job preparation, release, and standard tasks.</span></span>
3. <span data-ttu-id="8fd46-160">Запускает задачу подготовки задания, которая сначала записывает идентификатор узла в текстовый файл в общем каталоге узла.</span><span class="sxs-lookup"><span data-stu-id="8fd46-160">Runs the job preparation task, which first writes the node ID to a text file in a node's "shared" directory.</span></span>
4. <span data-ttu-id="8fd46-161">Запускает на каждом узле задачу, которая записывает свой идентификатор в тот же текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="8fd46-161">Runs a task on each node that writes its task ID to the same text file.</span></span>
5. <span data-ttu-id="8fd46-162">После завершения всех задач (или по истечении времени ожидания) выводит содержимое текстового файла каждого узла на консоль.</span><span class="sxs-lookup"><span data-stu-id="8fd46-162">Once all tasks are completed (or the timeout is reached), prints the contents of each node's text file to the console.</span></span>
6. <span data-ttu-id="8fd46-163">После завершения задания запускает задачу снятия задания для удаления файла с узла.</span><span class="sxs-lookup"><span data-stu-id="8fd46-163">When the job is completed, runs the job release task to delete the file from the node.</span></span>
7. <span data-ttu-id="8fd46-164">Выводит коды завершения задач подготовки и снятия задания для каждого узла, на котором они выполнялись.</span><span class="sxs-lookup"><span data-stu-id="8fd46-164">Prints the exit codes of the job preparation and release tasks for each node on which they executed.</span></span>
8. <span data-ttu-id="8fd46-165">Приостанавливает выполнение, чтобы подтвердить удаление задания или пула.</span><span class="sxs-lookup"><span data-stu-id="8fd46-165">Pauses execution to allow confirmation of job and/or pool deletion.</span></span>

<span data-ttu-id="8fd46-166">Выходные данные в этом примере приложения будут аналогичны следующему примеру:</span><span class="sxs-lookup"><span data-stu-id="8fd46-166">Output from the sample application is similar to the following:</span></span>

```
Attempting to create pool: JobPrepReleaseSamplePool
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

Waiting for job JobPrepReleaseSampleJob to reach state Completed
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

Sample complete, hit ENTER to exit...
```

> [!NOTE]
> <span data-ttu-id="8fd46-167">Так как время создания и запуска узлов в новом пуле может различаться (некоторые узлы раньше других будут готовы выполнять задачи), отображаемые результаты будут разными.</span><span class="sxs-lookup"><span data-stu-id="8fd46-167">Due to the variable creation and start time of nodes in a new pool (some nodes are ready for tasks before others), you may see different output.</span></span> <span data-ttu-id="8fd46-168">Например, один из узлов пула может выполнить все задачи задания, так как эти задачи очень короткие.</span><span class="sxs-lookup"><span data-stu-id="8fd46-168">Specifically, because the tasks complete quickly, one of the pool's nodes may execute all of the job's tasks.</span></span> <span data-ttu-id="8fd46-169">В таком случае вы увидите, что задачи подготовки и снятия заданий не существуют для тех узлов, которые не выполнили ни одной задачи.</span><span class="sxs-lookup"><span data-stu-id="8fd46-169">If this occurs, you will notice that the job prep and release tasks do not exist for the node that executed no tasks.</span></span>
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-the-azure-portal"></a><span data-ttu-id="8fd46-170">Проверка задачи подготовки и снятия заданий на портале Azure</span><span class="sxs-lookup"><span data-stu-id="8fd46-170">Inspect job preparation and release tasks in the Azure portal</span></span>
<span data-ttu-id="8fd46-171">Выполняя пример приложения, на [портале Azure][portal] можно просмотреть свойства задания и входящие в него задачи и даже скачать общий текстовый файл, который редактируется задачами задания.</span><span class="sxs-lookup"><span data-stu-id="8fd46-171">When you run the sample application, you can use the [Azure portal][portal] to view the properties of the job and its tasks, or even download the shared text file that is modified by the job's tasks.</span></span>

<span data-ttu-id="8fd46-172">На снимке экрана ниже показана **колонка задач подготовки** на портале Azure после запуска примера приложения.</span><span class="sxs-lookup"><span data-stu-id="8fd46-172">The screenshot below shows the **Preparation tasks blade** in the Azure portal after a run of the sample application.</span></span> <span data-ttu-id="8fd46-173">После выполнения всех задач (но до удаления задания и пула) откройте свойства *JobPrepReleaseSampleJob* и щелкните **Задачи подготовки** или **Задачи прекращения**, чтобы просмотреть их свойства.</span><span class="sxs-lookup"><span data-stu-id="8fd46-173">Navigate to the *JobPrepReleaseSampleJob* properties after your tasks have completed (but before deleting your job and pool) and click **Preparation tasks** or **Release tasks** to view their properties.</span></span>

![Свойства подготовки задания на портале Azure][1]

## <a name="next-steps"></a><span data-ttu-id="8fd46-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8fd46-175">Next steps</span></span>
### <a name="application-packages"></a><span data-ttu-id="8fd46-176">Пакеты приложений</span><span class="sxs-lookup"><span data-stu-id="8fd46-176">Application packages</span></span>
<span data-ttu-id="8fd46-177">Для подготовки вычислительных узлов к выполнению задач вы можете использовать не только задачи подготовки заданий, но и функцию пакетной службы [Пакет приложения](batch-application-packages.md) .</span><span class="sxs-lookup"><span data-stu-id="8fd46-177">In addition to the job preparation task, you can also use the [application packages](batch-application-packages.md) feature of Batch to prepare compute nodes for task execution.</span></span> <span data-ttu-id="8fd46-178">Эта функция особенно полезна для развертывания приложений, которые не требуют выполнения установщика, приложений с большим числом файлов (более 100) и приложений, требующих строгого управления версиями.</span><span class="sxs-lookup"><span data-stu-id="8fd46-178">This feature is especially useful for deploying applications that do not require running an installer, applications that contain many (100+) files, or applications that require strict version control.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="8fd46-179">Установка приложений и промежуточных данных</span><span class="sxs-lookup"><span data-stu-id="8fd46-179">Installing applications and staging data</span></span>
<span data-ttu-id="8fd46-180">В этой публикации на форуме MSDN рассматриваются несколько методов подготовки узлов для выполнения задач:</span><span class="sxs-lookup"><span data-stu-id="8fd46-180">This MSDN forum post provides an overview of several methods of preparing your nodes for running tasks:</span></span>

<span data-ttu-id="8fd46-181">[Installing applications and staging data on Batch compute nodes][forum_post] (Установка приложений и промежуточное размещение данных на вычислительных узлах пакетной службы)</span><span class="sxs-lookup"><span data-stu-id="8fd46-181">[Installing applications and staging data on Batch compute nodes][forum_post]</span></span>

<span data-ttu-id="8fd46-182">Эта публикация написана одним из участников команды разработчиков пакетной службы Azure. В ней приведены несколько методов, которые можно использовать при развертывании приложений и данных на вычислительных узлах.</span><span class="sxs-lookup"><span data-stu-id="8fd46-182">Written by one of the Azure Batch team members, it discusses several techniques that you can use to deploy applications and data to compute nodes.</span></span>

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
