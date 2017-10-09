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
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a>Выполнение задач подготовки и задач завершения заданий на вычислительных узлах пакетной службы

 Для заданий пакетной службы Azure часто требуется определенная настройка перед выполнением задач и определенные действия по обслуживанию после завершения задач задания. Вам может потребоваться toodownload распространенные задачи ввода данных tooyour вычислительных узлов, или отправить tooAzure данных выходные данные задачи хранилища после завершения задания hello. Можно использовать **задания подготовки** и **задания выпуска** задачи tooperform этих операций.

## <a name="what-are-job-preparation-and-release-tasks"></a>Сведения о задачах подготовки и снятия заданий
Перед выполнением задачи задания задачу подготовки задания hello выполняется на все вычислительные узлы запланированных toorun хотя бы одна задача. После завершения задания hello задачу прекращения задания hello запускается на каждом узле в пуле hello, выполняется хотя бы одна задача. Как и в обычном пакетные задачи можно указать toobe командной строки, вызывается, когда подготовки задания или запустить задачу прекращения.

Задачи подготовки и завершения заданий предоставляют уже привычные возможности задач пакетной службы, такие как скачивание файла ([файлов ресурсов][net_job_prep_resourcefiles]), выполнение с повышенными правами, пользовательские переменные среды, максимальная продолжительность выполнения, число повторных попыток и период удержания файла.

В следующих разделах hello, вы узнаете, как toouse hello [JobPreparationTask] [ net_job_prep] и [JobReleaseTask] [ net_job_release] классы найти в hello [Пакета .NET] [ api_net] библиотеки.

> [!TIP]
> Задачи подготовки и снятия заданий особенно полезны в средах с общим пулом, в которых пул вычислительных узлов сохраняется между запусками заданий и может совместно использоваться различными заданиями.
> 
> 

## <a name="when-toouse-job-preparation-and-release-tasks"></a>Когда toouse подготовки задания и освободить задачи
Подготовки задания и задания выпуска задачи хорошо подходят для hello в следующих ситуациях:

**Скачивание данных общих задач**

Выполнение пакетных заданий часто требуется общий набор данных в качестве входного для hello рабочих заданий. Например ежедневно вычислений анализа рисков, рыночные данные — конкретного задания, но распространенные задачи tooall в задании hello. Эти данные рынка, часто несколько гигабайт, должно быть загруженного tooeach вычислительного узла только один раз, чтобы его можно было использовать любую задачу, которая работает на узле hello. Используйте **задача подготовки задания** toodownload этот узел tooeach данных до выполнения hello задания hello и другие задачи.

**Удаление выходных данных заданий и задач**

В среде "общих ресурсов пул», где пул вычислительных узлов не выводится из эксплуатации между заданиями, может потребоваться toodelete задания данные между запусками. Может потребоваться tooconserve дисковое пространство на узлах hello или удовлетворять политикам безопасности организации. Используйте **задачу прекращения задания** toodelete данных, был загружен задача подготовки задания, созданные во время выполнения задачи.

**Хранение журнала**

Может потребоваться tookeep копию файлов журнала, которые создают задач или возможно файлы аварийного дампа, возникают в результате сбоя приложения. Используйте **задачу прекращения задания** в таких случаях toocompress и передать этот данных tooan [хранилища Azure] [ azure_storage] учетной записи.

> [!TIP]
> Другой способ toopersist журналов и других заданий и задач выходных данных — toouse hello [Azure пакетных файлов, принятых](batch-task-output.md) библиотеки.
> 
> 

## <a name="job-preparation-task"></a>Задача подготовки задания
Перед выполнением задач «задания» пакет выполняет задачу подготовки задания hello на каждом вычислительном узле, toorun запланированные задачи. По умолчанию hello пакетная служба ожидает завершения перед запуском tooexecute запланированные задачи hello на узле hello задач toobe hello задания подготовки. Тем не менее можно настроить службу hello не toowait. Если узел hello перезапускается, задачу подготовки задания hello запускается снова, но это поведение можно отключить.

Задача подготовки задания Hello выполняется только на узлах, которые являются toorun запланированные задачи. Это предотвращает hello ненужные выполнения задачи подготовки в случае, если узел не назначена задача. Это может произойти, если количество hello задачи для задания меньше hello количество узлов в пул. Оно также применяется, когда [выполнение параллельных задач](batch-parallel-node-tasks.md) включен, если число задач hello меньше всего hello возможных параллельных задач оставляет некоторые узлы простоя. Не выполнив задачу подготовки задания hello простоя узлах, могут тратить сокращения затрат на расходы по передаче данных.

> [!NOTE]
> [JobPreparationTask] [ net_job_prep_cloudjob] отличается от [CloudPool.StartTask] [ pool_starttask] в том, что JobPreparationTask выполняется в начале каждого задания hello, тогда как StartTask выполняется, только если вычислительный узел сначала производит соединение пула или перезагрузки.
> 
> 

## <a name="job-release-task"></a>задачи снятия задания
После задания помечается как завершенная, задачу прекращения задания hello выполняется на каждом узле в пуле hello, выполняется хотя бы одна задача. Чтобы пометить задание как завершенное, нужно направить запрос прекращения. Hello пакетной службы, а затем задает hello состояние задания слишком*Завершение*, завершает active или не запущены задачи, связанной с заданием hello и запускает задачу прекращения задания hello. Задание Hello затем перемещает toohello *завершения* состояния.

> [!NOTE]
> Удаление задания также выполняет задачу прекращения задания hello. Тем не менее если задание уже был завершен, задачу hello выпуска не запускается повторно, если задание hello позже удаляется.
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a>Задачи подготовки и снятия заданий с использованием пакетной службы .NET
назначить задачу подготовки задания toouse [JobPreparationTask] [ net_job_prep] tooyour задания объекта [CloudJob.JobPreparationTask] [ net_job_prep_cloudjob] свойство . Аналогичным образом инициализировать [JobReleaseTask] [ net_job_release] и назначьте его задание tooyour [CloudJob.JobReleaseTask] [ net_job_prep_cloudjob] свойство tooset hello Задание выпуска.

В этом фрагменте кода `myBatchClient` является экземпляром класса [BatchClient][net_batch_client], и `myPool` является существующего пула внутри hello пакетной учетной записи.

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

Как упоминалось ранее, hello выпуска задач выполняется при удалении или завершение задания. Для завершения задания используется [JobOperations.TerminateJobAsync][net_job_terminate], а для удаления — [JobOperations.DeleteJobAsync][net_job_delete]. Обычно оба эти действия выполняются после завершения задач задания или по истечении времени ожидания, которое было определено.

```csharp
// Terminate hello job toomark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a>Пример кода на GitHub
toosee Задание подготовки выпуска задачи и действия, извлечь hello [JobPrepRelease] [ job_prep_release_sample] примера проекта на GitHub. Это консольное приложение hello следующие:

1. Создает пул с двумя "небольшими" узлами.
2. Создает задание с задачами подготовки задания, снятия задания и стандартными задачами.
3. Запускает hello задачи подготовки задания, который сначала записывает hello узел идентификатор tooa текстового файла в каталоге «общий» узла.
4. Выполняет задачу на каждом узле, который записывает его toohello идентификатор задачи текстовый файл.
5. После завершения всех задач (или истечет время ожидания hello) печатает содержимое hello toohello файл консоли для каждого узла текста.
6. По завершении задания hello запускает файл hello toodelete задач версии hello задания из узла "hello".
7. Печатает hello коды подготовки задания hello завершения и выпуска задач для каждого узла, на котором выполняется.
8. Приостанавливает выполнение tooallow подтверждение удаления задания и/или пула.

Выходные данные из образца приложения hello выглядят примерно следующие toohello:

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
> Из-за toohello переменной создания и время запуска узлов в новый пул (некоторые узлы готовы для задачи, прежде чем другие) может увидеть различные результаты. В частности из-за быстрого выполнения задач hello, один из узлов hello пула могут выполнять все задачи hello задания. В этом случае можно заметить, что hello подготовки задания и освободить задачи не существуют для узла hello, выполняемые задачи отсутствуют.
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-hello-azure-portal"></a>Проверять подготовки задания и задач выпуска в hello портал Azure
При запуске образца приложения hello, можно использовать hello [портал Azure] [ portal] tooview hello свойства hello задания и его задачи, или даже Загрузите hello общего текстового файла, изменяемом hello рабочих заданий.

Hello снимке экрана показано hello **колонке задачи подготовки** в hello портал Azure после запуска образца приложения hello. Перейдите toohello *JobPrepReleaseSampleJob* свойства после завершения задачи (но до удаления задания и пула) и нажмите кнопку **задачи подготовки** или **выпусказадачи** tooview их свойства.

![Свойства подготовки задания на портале Azure][1]

## <a name="next-steps"></a>Дальнейшие действия
### <a name="application-packages"></a>Пакеты приложений
В задачи подготовки задания toohello сложения, можно также использовать hello [пакетов приложений](batch-application-packages.md) функция tooprepare пакетных вычислительных узлов для выполнения задач. Эта функция особенно полезна для развертывания приложений, которые не требуют выполнения установщика, приложений с большим числом файлов (более 100) и приложений, требующих строгого управления версиями.

### <a name="installing-applications-and-staging-data"></a>Установка приложений и промежуточных данных
В этой публикации на форуме MSDN рассматриваются несколько методов подготовки узлов для выполнения задач:

[Installing applications and staging data on Batch compute nodes][forum_post] (Установка приложений и промежуточное размещение данных на вычислительных узлах пакетной службы)

Записываются одним из членов команды hello пакетной службы Azure, в нем описывается несколько методов, которые можно использовать узлы toocompute toodeploy приложениям и данным.

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
