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
ms.openlocfilehash: aecce83b4d4444f2651f48475b596fa76cb5f44a
ms.sourcegitcommit: 3fca41d1c978d4b9165666bb2a9a1fe2a13aabb6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/15/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a>Выполнение задач подготовки и задач завершения заданий на вычислительных узлах пакетной службы

 Для заданий пакетной службы Azure часто требуется определенная настройка перед выполнением задач и определенные действия по обслуживанию после завершения задач задания. Вам может понадобиться скачать входные данные общих задач на вычислительные узлы или отправить выходные данные задачи в службу хранилища Azure после завершения задания. Для выполнения этих операций можно использовать задачи **подготовки задания** и **прекращения задания**.

## <a name="what-are-job-preparation-and-release-tasks"></a>Сведения о задачах подготовки и снятия заданий
Задача подготовки задания выполняется на всех вычислительных узлах, на которых запланирован запуск минимум одного задания, до выполнения задач задания. Когда задание завершается, на каждом узле в пуле, на котором была выполнена хотя бы одна задача, выполняется задача снятия задания. Как и для обычных задач пакетной службы, для задач подготовки и снятия задания можно указать командную строку, вызываемую при выполнении задачи.

Задачи подготовки и завершения заданий предоставляют уже привычные возможности задач пакетной службы, такие как скачивание файла ([файлов ресурсов][net_job_prep_resourcefiles]), выполнение с повышенными правами, пользовательские переменные среды, максимальная продолжительность выполнения, число повторных попыток и период удержания файла.

В следующих разделах вы узнаете, как использовать классы [JobPreparationTask][net_job_prep] и [JobReleaseTask][net_job_release], которые находятся в библиотеке [.NET пакетной службы][api_net].

> [!TIP]
> Задачи подготовки и снятия заданий особенно полезны в средах с общим пулом, в которых пул вычислительных узлов сохраняется между запусками заданий и может совместно использоваться различными заданиями.
> 
> 

## <a name="when-to-use-job-preparation-and-release-tasks"></a>Когда используются задачи подготовки и снятия заданий
Задачи подготовки и снятия заданий отлично подходят для приведенных ниже сценариев.

**Скачивание данных общих задач**

Для задач пакетных заданий часто требуется общий набор входных данных. Например, в ежедневных расчетах по анализу рисков рыночные данные относятся к конкретному заданию, но являются общими для всех задач внутри этого задания. Эти рыночные данные, зачастую объемом в несколько гигабайт, нужно скачать на каждый вычислительный узел только один раз, после чего их сможет использовать любая задача, которая выполняется на этом узле. **Задача подготовки задания** позволяет скачать данные на все узлы перед выполнением других задач в задании.

**Удаление выходных данных заданий и задач**

В среде общего пула, где вычислительные узлы пула не удаляются из пула между заданиями, может потребоваться удалять данные заданий между запусками для экономии дискового пространства на узлах или в соответствии с политиками безопасности организации. С помощью **задачи прекращения задания** можно удалить данные, скачанные задачей подготовки задания или созданные во время выполнения задачи.

**Хранение журнала**

Может возникнуть необходимость хранить копию файлов журнала, создаваемых задачами, или, например, файлы аварийных дампов, создаваемые приложениями, в которых возникает сбой. В таких случаях с помощью **задачи снятия задания** можно сжать и передать эти данные в учетную запись [хранения Azure][azure_storage].

> [!TIP]
> Для хранения журналов и других выходных данных заданий и задач также можно использовать библиотеку [Azure Batch File Conventions](batch-task-output.md) .
> 
> 

## <a name="job-preparation-task"></a>Задача подготовки задания
Перед выполнением задач задания пакетная служба выполняет задачу подготовки задания на каждом вычислительном узле, где запланировано выполнение задач. По умолчанию пакетная служба ожидает завершения задачи подготовки задания и только после этого запускает задачи, запланированные для выполнения на узле. Это ожидание можно отключить в настройках службы. Задача подготовки задания запускается на вычислительном узле снова при перезапуске узла, но это поведение также можно отключить.

Задача подготовки задания выполняется только на узлах, на которых запланировано выполнение задач. Благодаря этому на узлах, которым не назначены задачи, ненужная задача подготовки выполняться не будет. Это может произойти, если число задач в задании меньше количества узлов в пуле. То же самое происходит, когда включено [параллельное выполнение](batch-parallel-node-tasks.md) , в результате чего некоторые узлы бездействуют, если число задач оказывается меньше, чем общее число возможных параллельных задач. Не выполняя задачи по подготовке заданий на неактивных узлах, вы сократите свои расходы на передачу данных.

> [!NOTE]
> Задача [net_job_prep_cloudjob][net_job_prep_cloudjob] отличается от [CloudPool.StartTask][pool_starttask] тем, что задача JobPreparationTask выполняется в начале каждого задания, тогда как StartTask выполняется только при первом присоединении вычислительного узла к пулу или при его перезапуске.
> 
> 

## <a name="job-release-task"></a>задачи снятия задания
Когда задание будет отмечено как завершенное, на каждом узле в пуле, на котором была выполнена хотя бы одна задача, выполняется задача снятия задания. Чтобы пометить задание как завершенное, нужно направить запрос прекращения. После этого пакетная служба устанавливает состояние задания *Прекращение*, прекращает все активные или запущенные задачи, связанные с заданием, и запускает задачу снятия задания. Затем состояние задания меняется на *Завершено* .

> [!NOTE]
> Задача снятия задания также выполняется при удалении задания. Однако если задание уже было прекращено, задача снятия задания при последующем удалении задания вторично не выполняется.
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a>Задачи подготовки и снятия заданий с использованием пакетной службы .NET
Чтобы использовать задачу подготовки задания, назначьте объект [JobPreparationTask][net_job_prep] свойству [CloudJob.JobPreparationTask][net_job_prep_cloudjob]. Аналогичным образом инициализируйте задачу [JobReleaseTask][net_job_release] и назначьте ее свойству [CloudJob.JobReleaseTask][net_job_prep_cloudjob] задания, чтобы настроить задачу снятия задания.

В этом фрагменте кода `myBatchClient` представляет собой экземпляр [BatchClient][net_batch_client], а `myPool` — существующий пул в учетной записи пакетной службы.

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
    new JobReleaseTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

Как упоминалось выше, задача снятия выполняется, когда задание прекращается или удаляется. Для завершения задания используется [JobOperations.TerminateJobAsync][net_job_terminate], а для удаления — [JobOperations.DeleteJobAsync][net_job_delete]. Обычно оба эти действия выполняются после завершения задач задания или по истечении времени ожидания, которое было определено.

```csharp
// Terminate the job to mark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsync("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a>Пример кода на GitHub
В примере проекта [JobPrepRelease][job_prep_release_sample] с сайта GitHub можно ознакомиться с действием задач подготовки и снятия задания. Это консольное приложение выполняет следующее.

1. Создает пул с двумя "небольшими" узлами.
2. Создает задание с задачами подготовки задания, снятия задания и стандартными задачами.
3. Запускает задачу подготовки задания, которая сначала записывает идентификатор узла в текстовый файл в общем каталоге узла.
4. Запускает на каждом узле задачу, которая записывает свой идентификатор в тот же текстовый файл.
5. После завершения всех задач (или по истечении времени ожидания) выводит содержимое текстового файла каждого узла на консоль.
6. После завершения задания запускает задачу снятия задания для удаления файла с узла.
7. Выводит коды завершения задач подготовки и снятия задания для каждого узла, на котором они выполнялись.
8. Приостанавливает выполнение, чтобы подтвердить удаление задания или пула.

Выходные данные в этом примере приложения будут аналогичны следующему примеру:

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
> Так как время создания и запуска узлов в новом пуле может различаться (некоторые узлы раньше других будут готовы выполнять задачи), отображаемые результаты будут разными. Например, один из узлов пула может выполнить все задачи задания, так как эти задачи очень короткие. В таком случае вы увидите, что задачи подготовки и снятия заданий не существуют для тех узлов, которые не выполнили ни одной задачи.
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-the-azure-portal"></a>Проверка задачи подготовки и снятия заданий на портале Azure
Выполняя пример приложения, на [портале Azure][portal] можно просмотреть свойства задания и входящие в него задачи и даже скачать общий текстовый файл, который редактируется задачами задания.

На снимке экрана ниже показана **колонка задач подготовки** на портале Azure после запуска примера приложения. После выполнения всех задач (но до удаления задания и пула) откройте свойства *JobPrepReleaseSampleJob* и щелкните **Задачи подготовки** или **Задачи прекращения**, чтобы просмотреть их свойства.

![Свойства подготовки задания на портале Azure][1]

## <a name="next-steps"></a>Дальнейшие действия
### <a name="application-packages"></a>Пакеты приложений
Для подготовки вычислительных узлов к выполнению задач вы можете использовать не только задачи подготовки заданий, но и функцию пакетной службы [Пакет приложения](batch-application-packages.md) . Эта функция особенно полезна для развертывания приложений, которые не требуют выполнения установщика, приложений с большим числом файлов (более 100) и приложений, требующих строгого управления версиями.

### <a name="installing-applications-and-staging-data"></a>Установка приложений и промежуточных данных
В этой публикации на форуме MSDN рассматриваются несколько методов подготовки узлов для выполнения задач:

[Installing applications and staging data on Batch compute nodes][forum_post] (Установка приложений и промежуточное размещение данных на вычислительных узлах пакетной службы)

Эта публикация написана одним из участников команды разработчиков пакетной службы Azure. В ней приведены несколько методов, которые можно использовать при развертывании приложений и данных на вычислительных узлах.

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
