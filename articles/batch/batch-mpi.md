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
# <a name="use-multi-instance-tasks-toorun-message-passing-interface-mpi-applications-in-batch"></a>Использовать несколько экземпляров задач toorun интерфейса передачи сообщений (MPI) приложения в пакете

Многоэкземплярные задачи позволяют toorun задачу пакетной службы Azure на нескольких вычислительных узлах одновременно. Эти задачи реализуют в пакетной службе такие сценарии высокопроизводительных вычислений, как приложения интерфейса передачи сообщений (MPI). В этой статье вы узнаете, как hello tooexecute многоэкземплярные задач с помощью [пакета .NET] [ api_net] библиотеки.

> [!NOTE]
> Hello примеры в этой статье уделено пакета .NET, MS-MPI и Windows вычислительных узлов, hello нескольких экземпляров задач понятия, описанные здесь, применимо tooother платформ и технологий (Python и Intel MPI на узлах Linux, например).
>
>

## <a name="multi-instance-task-overview"></a>Общие сведения о задачах с несколькими экземплярами
В пакете, в каждой задачи — это обычно выполняются в одном вычислительном узле — Отправка задания tooa несколько задач и hello пакетная служба назначает каждой задачи для выполнения на узле. Тем не менее, настроив задачи **параметры с несколькими экземплярами**, сообщите пакета tooinstead создать один основной задачей и нескольких подзадач, которые выполняются на нескольких узлах.

![Общие сведения о задачах с несколькими экземплярами][1]

При отправке задачи с несколькими экземплярами параметры tooa задания, пакет выполняет несколько задач уникальный toomulti экземпляр действия:

1. Hello пакетная служба создает одно **основной** и несколько **подзадачи** на основе параметров hello несколькими экземплярами. Общее число задач (основной плюс все подзадачи) Hello соответствует номеру hello **экземпляров** (вычислительных узлов) укажите в параметрах hello несколькими экземплярами.
2. Определяет пакет, один hello вычислительные узлы как hello **master**, и расписания hello tooexecute основная задача образец hello. Оно планирует tooexecute подзадачи hello на остаток hello hello вычислительных узлов выделенный toohello несколькими экземплярами задачи один подзадачи на каждом узле.
3. Hello первичной и всех подзадачи загрузить все **обычные файлы ресурсов** укажите в параметрах hello несколькими экземплярами.
4. После загрузки hello обычные файлы ресурсов hello первичный и подзадачи выполнение hello **координации командной** укажите в параметрах hello несколькими экземплярами. Команда координации Hello — узлы tooprepare обычно используется для выполнения задачи hello. Это может включать запуск фоновых служб (таких как [Microsoft MPI][msmpi_msdn] `smpd.exe`) и проверка готовности tooprocess между узлами сообщения hello узлов.
5. Основная задача Hello выполняет hello **команды приложения** на главном узле hello *после* hello координации команды успешно завершен, hello первичной и всех подзадач. Команда приложения Hello Командная строка hello самой задачи многоэкземплярные hello и выполняется только основная задача hello. Например, вы можете запустить выполнение приложения с поддержкой MPI в решении на базе [MS-MPI][msmpi_msdn] с помощью команды `mpiexec.exe`.

> [!NOTE]
> Хотя функционально distinct, hello «многоэкземплярные task» не является типом уникальный задач как hello [StartTask] [ net_starttask] или [JobPreparationTask] [ net_jobprep]. Hello многоэкземплярные задача является просто стандартный пакет ([CloudTask] [ net_task] в пакете .NET) были настроены, параметры которого несколькими экземплярами. В этой статье мы называем toothis как hello **задач с несколькими экземплярами**.
>
>

## <a name="requirements-for-multi-instance-tasks"></a>Требования к задачам с несколькими экземплярами
При выполнении многоэкземплярной задачи требуется, чтобы в пуле был **включен обмен данными между узлами** и **отключено параллельное выполнение задач**. выполнение параллельных задач toodisable, набор hello [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) too1 свойство.

Этот фрагмент кода показывает, как toocreate пул для нескольких экземпляров задачи с помощью библиотеки .NET пакета hello.

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
> При попытке toorun отключена задача нескольких экземпляров в пуле с связи между узлами или с *maxTasksPerNode* значение больше 1, задача hello никогда не запланирована--бесконечно остается в состоянии «Активно» hello. 
>
> Многоэкземплярные задачи могут выполняться только на узлах в пулах, созданных после 14 декабря 2015 года.
>
>

### <a name="use-a-starttask-tooinstall-mpi"></a>Используйте StartTask tooinstall MPI
toorun приложений MPI с несколькими экземплярами задачей, необходимо сначала tooinstall реализации MPI (MS-MPI или MPI Intel, например) на вычислительных узлах hello в пуле hello. Это подходящий момент toouse [StartTask][net_starttask], которое выполняется каждый раз, когда узел присоединяется пул, или перезапуска. Этот фрагмент кода создает StartTask, задающий hello MS-MPI пакет установки в виде [файла ресурсов][net_resourcefile]. задачи запуска Hello командной строки выполняется после файла ресурсов hello загруженный toohello узла. В этом случае hello Командная строка выполняет автоматическую установку MS-MPI.

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

### <a name="remote-direct-memory-access-rdma"></a>Удаленный доступ к памяти (RDMA)
При выборе [функцией RDMA размер](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) например A9 для hello вычислительных узлов в пуле пакета, приложения MPI могут воспользоваться преимуществами Azure высокой производительности и малой задержкой сети удаленного памяти (RDMA) доступ.

Найдите размеры hello, указанные как «Поддержкой RDMA» в hello в следующих статьях:

* Пулы **CloudServiceConfiguration**

  * [Размеры для облачных служб](../cloud-services/cloud-services-sizes-specs.md) (только для Windows)
* Пулы **VirtualMachineConfiguration**

  * [Размеры виртуальных машин в Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)
  * [Размеры виртуальных машин в Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)

> [!NOTE]
> преимущества tootake RDMA на [Linux вычислительных узлов](batch-linux-nodes.md), необходимо использовать **Intel MPI** на узлах hello. Дополнительные сведения о CloudServiceConfiguration и VirtualMachineConfiguration пулов см. в разделе hello пула раздел hello [Обзор функций пакета](batch-api-basics.md).
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a>Создание задачи с несколькими экземплярами с помощью .NET для пакетной службы
Теперь, когда мы рассмотрели hello пула требований и установка пакета MPI, давайте создадим задачу hello несколькими экземплярами. В этом фрагменте кода мы создадим стандартную задачу [CloudTask][net_task], а затем настроим ее свойство [MultiInstanceSettings][net_multiinstance_prop]. Как упоминалось ранее, задачу hello нескольких экземпляров не типом различных задач, а также стандартные задачи пакета настроены параметры с несколькими экземплярами.

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

## <a name="primary-task-and-subtasks"></a>Основная задача и подзадачи
При создании нескольких экземпляров параметров задачи hello указываются hello количество вычислительных узлов, которые являются tooexecute задачу hello. При отправке задания tooa задача hello hello пакетная служба создает одно **основной** задач и достаточно **подзадачи** друг с другом, которые соответствуют hello количество узлов, указанной.

Эти задачи назначаются целочисленный идентификатор hello диапазона от 0 слишком*numberOfInstances* - 1. Задача Hello с идентификатором 0 основная задача hello и другие идентификаторы, подзадачи. Например при создании hello после настройки нескольких экземпляров для задачи, основная задача hello будет иметь идентификатор 0, и hello подзадачи будет иметь идентификаторы от 1 до 9.

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a>Главный узел
При отправке задачи нескольких экземпляров, hello пакетная служба назначает один hello вычислительные узлы «главный» узла hello и расписания hello tooexecute основная задача hello главного узла. Hello подзадачи, запланированных tooexecute на остаток hello hello узлов, выделенных задач toohello несколькими экземплярами.

## <a name="coordination-command"></a>команду координации
Hello **координации командной** выполняется путем hello первичный и подзадачи.

блокирует Hello вызова команды координации hello--пакета не выполняет команды приложения hello, пока hello координации команда вернула успешно для всех подзадач. Hello координации командной таким образом следует запустить службы любой необходимый цвет фона, убедитесь, что они готовы для использования и завершает работу. Например эта команда координации для решения с использованием версии 7 MS-MPI запускает службу hello SMPD на узле hello, а затем завершает работу:

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

Обратите внимание на использование hello `start` в этой команде координации. Это необходимо, поскольку hello `smpd.exe` приложения не возвращается немедленно после выполнения. Без использования hello hello [запустить] [ cmd_start] команд, эта команда координации не вернет и поэтому заблокирует команды приложения hello.

## <a name="application-command"></a>Команда приложения
Когда основная задача hello и все подзадачи завершения выполнения команды координации hello, многоэкземплярных задачу hello командной строки выполняется путем основная задача hello *только*. Мы называем это hello **команды приложения** toodistinguish его из команды координации hello.

Для приложений, MS-MPI, используйте hello приложения команды tooexecute приложения с поддержкой MPI `mpiexec.exe`. В качестве примера ниже приведена команда приложения для решения с использованием MS-MPI версии 7:

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> Так как MS-MPI `mpiexec.exe` hello использует `CCP_NODES` переменной по умолчанию (в разделе [переменных среды](#environment-variables)) hello пример приложения командной строки выше исключает его.
>
>

## <a name="environment-variables"></a>Переменные среды
Пакет создается несколько [переменных среды] [ msdn_env_var] экземпляра toomulti задачи на hello вычислений tooa многоэкземплярные задач выделенных узлов. Командные строки координации и приложение может ссылаться эти переменные среды можно hello сценариев и программ, которые они выполняются.

Hello следующие переменные среды создаются службой hello пакета для использования с несколькими экземплярами задачи:

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

Полные сведения об этих и hello других пакета вычислительного узла переменные среды, включая их содержимое и видимость, в разделе [вычислений переменные среды узла][msdn_env_var].

> [!TIP]
> Образец кода Hello MPI Linux пакета содержит пример использования некоторые из этих переменных среды. Hello [cmd координации] [ coord_cmd_example] Bash скрипт загружает Общие приложения и входные файлы из хранилища Azure, обеспечивает общую папку сетевой файловой системы (NFS) на главном узле hello и настраивает hello другие узлы выделить toohello многоэкземплярные задач как клиенты NFS.
>
>

## <a name="resource-files"></a>Файлы ресурсов
Существует два набора tooconsider файлы ресурсов для нескольких экземпляров задач: **обычные файлы ресурсов** , *все* задачи загрузки (основного и подзадачи) и hello **файлы ресурсов** для hello многоэкземплярные задач, который *основной hello* задач загрузки.

Можно указать один или несколько **обычные файлы ресурсов** в параметрах многоэкземплярные hello для задачи. Эти общие файлы ресурсов, загружаются из [хранилища Azure](../storage/common/storage-introduction.md) в каждом узле **каталог общих задач** hello первичной и всех подзадач. Каталог общих задач hello доступны из приложения и координации командной строки с помощью hello `AZ_BATCH_TASK_SHARED_DIR` переменной среды. Hello `AZ_BATCH_TASK_SHARED_DIR` пути идентичны для каждой задачи многоэкземплярные toohello выделенный узел, таким образом вы можете совместно использовать команду один координации между основной hello и все подзадачи. Пакет не» тот» hello каталог в смысле удаленного доступа, но можно использовать в качестве монтирования или совместного использования точки, как упоминалось ранее в подсказке hello на переменных среды.

Файлы ресурсов, указанных для hello саму задачу многоэкземплярные: рабочий каталог загруженный toohello задач, `AZ_BATCH_TASK_WORKING_DIR`, по умолчанию. В отличие от как уже упоминалось, toocommon файлы ресурсов, только hello основная задача загружает файлы ресурсов, указанный для саму задачу hello несколькими экземплярами.

> [!IMPORTANT]
> Всегда используйте переменные среды hello `AZ_BATCH_TASK_SHARED_DIR` и `AZ_BATCH_TASK_WORKING_DIR` toorefer toothese каталогов в вашей команды. Не пытайтесь пути hello tooconstruct вручную.
>
>

## <a name="task-lifetime"></a>Срок действия задачи
время существования Hello hello основная задача элементы управления hello времени существования hello всего несколькими экземпляра задачи. При выходе из первичного hello, завершаются все подзадачи hello. код выхода Hello hello основной — hello код выхода задачи «hello» и поэтому используется toodetermine hello успешности задачу hello целях повторных попыток.

В случае сбоя любой подзадачи hello выход с ненулевым кодом возврата, например, hello всего несколькими экземплярами задача завершается ошибкой. затем многоэкземплярные задачу Hello завершается и повторить копирование tooits предел повторных попыток.

При удалении задачи многоэкземплярные hello первичной и всех подзадачи удаляются hello пакетной службы. Все подзадачи каталоги и их файлы удаляются из hello вычислительных узлов, как и в случае стандартных задач.

[TaskConstraints] [ net_taskconstraints] многоэкземплярные задачи, например hello [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime] [ net_taskconstraint_maxwallclock], и [RetentionTime] [ net_taskconstraint_retention] свойства, обрабатываются как они предназначены для стандартных задач, а также применить toohello первичная файловая группа и все подзадачи. Однако если изменить hello [RetentionTime] [ net_taskconstraint_retention] задано после добавления задачи toohello hello нескольких экземпляров задания, это изменение применяется только toohello основная задача. Все подзадачи hello продолжить оригинал hello toouse [RetentionTime][net_taskconstraint_retention].

Вычислительный узел списка недавних задач отражает идентификатор hello подзадачей, если последние задачу hello входил в состав задачи нескольких экземпляров.

## <a name="obtain-information-about-subtasks"></a>Получение сведений о подзадачах
tooobtain сведения на подзадачи, с помощью библиотеки .NET пакета hello, вызов hello [CloudTask.ListSubtasks] [ net_task_listsubtasks] метод. Этот метод возвращает сведения о всех подзадачи и сведения о hello вычислительного узла, который выполнен hello задачи. По этим данным можно определить корневой каталог для каждой из них, идентификатор пула hello, текущего состояния, код выхода и многое другое. Эти сведения можно использовать в сочетании с hello [PoolOperations.GetNodeFile] [ poolops_getnodefile] файлы метод tooobtain hello подзадач. Обратите внимание, что этот метод не возвращает сведения о основная задача hello (идентификатор 0).

> [!NOTE]
> Если не указано иное, пакет .NET методов, которые работают на hello нескольких экземпляров [CloudTask] [ net_task] сам применить *только* toohello основная задача. Например, при вызове hello [CloudTask.ListNodeFiles] [ net_task_listnodefiles] метода задаче нескольких экземпляров, возвращаются только файлы, основная задача hello.
>
>

Hello следующий фрагмент кода показывает, как tooobtain подзадачи сведения, а также запрашивать содержимое файла hello узлы, на которых выполняется.

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

## <a name="code-sample"></a>Пример кода
Hello [MultiInstanceTasks] [ github_mpi] демонстрируется образец кода на GitHub как toouse нескольких экземпляров задач toorun [MS-MPI] [ msmpi_msdn] приложение в пакете вычислительных узлах. Следуйте указаниям hello [подготовки](#preparation) и [выполнения](#execution) toorun образец hello.

### <a name="preparation"></a>Подготовка
1. Выполните первые два действия hello в [как toocompile и выполните простой программы MS-MPI][msmpi_howto]. Это убеждает prerequesites hello для hello следующий шаг.
2. Построение *выпуска* версии hello [MPIHelloWorld] [ helloworld_proj] MPI образец программы. Это hello программы, которая будет выполняться на вычислительных узлах задачу hello несколькими экземплярами.
3. Создайте ZIP-файл, содержащий файл `MPIHelloWorld.exe` (созданный на шаге 2) и `MSMpiSetup.exe` (скачанный на шаге 1). Как пакет приложения hello следующем шаге вы отправите этот ZIP-файл.
4. Используйте hello [портал Azure] [ portal] toocreate пакета [приложения](batch-application-packages.md) называется «MPIHelloWorld» и укажите hello ZIP-файл, созданный на предыдущем шаге hello в качестве версии «1.0» пакет приложения Hello. Дополнительные сведения см. в разделе [Передача приложений и управление ими](batch-application-packages.md#upload-and-manage-applications).

> [!TIP]
> Построение *выпуска* версии `MPIHelloWorld.exe` , чтобы не нужно tooinclude никакие дополнительные зависимости (например, `msvcp140d.dll` или `vcruntime140d.dll`) в пакет приложения.
>
>

### <a name="execution"></a>Выполнение
1. Загрузите hello [образцы azure пакета] [ github_samples_zip] из GitHub.
2. Откройте hello MultiInstanceTasks **решения** в Visual Studio 2015 или более поздней версии. Hello `MultiInstanceTasks.sln` решения файл находится в:

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. Ввести учетные данные учетной записи пакета и хранилища в `AccountSettings.settings` в hello **Microsoft.Azure.Batch.Samples.Common** проекта.
4. **Построение и запуск** hello MultiInstanceTasks решения tooexecute hello MPI пример приложения на вычислительных узлов в пуле пакета.
5. *Необязательный*: hello используйте [портал Azure] [ portal] или hello [обозреватель пакета] [ batch_explorer] tooexamine пула образец hello, задания, и задачи («MultiInstanceSamplePool», «MultiInstanceSampleJob», «MultiInstanceSampleTask»), прежде чем удалить ресурсы hello.

> [!TIP]
> Вы можете скачать [Visual Studio Community][visual_studio] бесплатно, если у вас нет Visual Studio.
>
>

Выходные данные `MultiInstanceTasks.exe` — примерно toohello следующее:

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

## <a name="next-steps"></a>Дальнейшие действия
* Hello Microsoft HPC и пакетной команды Azure блоге обсуждается [MPI поддержка Linux в Azure пакет][blog_mpi_linux]и включает сведения об использовании [OpenFOAM] [ openfoam] с использованием пакета. Можно найти примеры кода Python для hello [пример OpenFOAM на GitHub][github_mpi].
* Узнайте, каким образом слишком[создание кластеров Linux вычислительные узлы](batch-linux-nodes.md) для использования в решениях Azure пакета MPI.

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
