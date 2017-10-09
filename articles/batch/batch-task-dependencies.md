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
# <a name="create-task-dependencies-toorun-tasks-that-depend-on-other-tasks"></a>Создание зависимостей задач toorun задач, которые зависят от других задач

Toorun зависимости задач можно определить задачи или набора задач только после завершения родительской задачи. Ниже описано несколько ситуаций, в которых удобно использовать зависимости задач. Их можно использовать для:

* Стиль MapReduce рабочих нагрузок в облако hello.
* заданий, задачи обработки данных которых можно представить в виде направленного ациклического графа (DAG);
* Процессы предварительной подготовки к просмотру и после подготовки к просмотру, где каждая задача должна быть выполнена перед началом следующей задаче hello.
* Любое другое задание, в котором подчиненные задачи зависят от hello выходные данные вышестоящего задачи.

С зависимостями задач пакета можно создать задачи, запланированные для выполнения на вычислительных узлах после завершения одного или нескольких родительских задачах hello. Например, можно создать задание, которое отрисовывает каждый кадр трехмерного фильма с помощью отдельных параллельных задач. Последняя задача Hello--hello «задача слияния»--слияний hello преобразуется кадры hello полный фильм только после того как все кадры отрисовываются успешно.

По умолчанию зависимые задачи, планируются для выполнения только в том случае, после успешного завершения родительской задачи hello. Можно указать поведение по умолчанию действие toooverride зависимостей hello и запускать задачи при сбое hello родительской задачи. В разделе hello [действия зависимостей](#dependency-actions) подробные сведения см.  

Можно создавать задачи, которые зависят от других задач по схеме "один к одному" или "один ко многим". Можно также создать диапазона зависимостей, где задачи зависит от выполнения hello группы задач в пределах указанного диапазона идентификаторов задач. Можно объединять эти три основных сценария toocreate многие ко многим связи.

## <a name="task-dependencies-with-batch-net"></a>Зависимости задач .NET пакетной службы
В этой статье мы рассмотрим, как hello tooconfigure зависимостей задач с помощью [пакета .NET] [ net_msdn] библиотеки. Мы сначала показано, каким образом слишком[включить зависимость](#enable-task-dependencies) в заданиях, а затем показывается, как слишком[настройте задачу с зависимостями](#create-dependent-tasks). Также описывается, как toospecify toorun зависимого действия зависимостей задач при сбое родительской hello. Наконец, мы обсудим hello [сценарии зависимостей](#dependency-scenarios) , поддерживающий пакета.

## <a name="enable-task-dependencies"></a>Включение зависимостей задач
toouse зависимостей задач в пакет приложения, необходимо сначала настроить зависимостей задач toouse задания hello. В пакете .NET, включить его на ваш [CloudJob] [ net_cloudjob] , установив его [UsesTaskDependencies] [ net_usestaskdependencies] свойство слишком`true`:

```csharp
CloudJob unboundJob = batchClient.JobOperations.CreateJob( "job001",
    new PoolInformation { PoolId = "pool001" });

// IMPORTANT: This is REQUIRED for using task dependencies.
unboundJob.UsesTaskDependencies = true;
```

В предыдущих фрагмент кода hello, «batchClient» является экземпляром типа hello [BatchClient] [ net_batchclient] класса.

## <a name="create-dependent-tasks"></a>Создание зависимости задач
toocreate задачу, которая зависит от выполнения hello одного или нескольких родительских задач можно указать задачу «зависит от» hello, hello другие задачи. В пакете .NET, настройте hello [CloudTask][net_cloudtask].[ DependsOn] [ net_dependson] свойство с помощью экземпляра hello [TaskDependencies] [ net_taskdependencies] класса:

```csharp
// Task 'Flowers' depends on completion of both 'Rain' and 'Sun'
// before it is run.
new CloudTask("Flowers", "cmd.exe /c echo Flowers")
{
    DependsOn = TaskDependencies.OnIds("Rain", "Sun")
},
```

Этот фрагмент кода создает зависимую задачу с идентификатором задачи Flowers. Hello «Цветов» задача зависит от задачи «Дождь» и «Sun». Задача «Цветов» будет запланированных toorun на вычислительном узле только после задачи «Дождь» и «Sun» завершена успешно.

> [!NOTE]
> Задача считается toobe выполнена успешно, если он находится в hello **завершения** состояние и его **код выхода** — `0`. В пакете .NET, это означает [CloudTask][net_cloudtask].[ Состояние] [ net_taskstate] значение свойства `Completed` и hello CloudTask [TaskExecutionInformation][net_taskexecutioninformation].[ ExitCode] [ net_exitcode] значение свойства `0`.
> 
> 

## <a name="dependency-scenarios"></a>сценарии использования зависимостей
Есть три основных сценария зависимостей задач, которые можно использовать в пакетной службе Azure: "один к одному", "один ко многим" и зависимость диапазона идентификаторов задач. Это могут быть объединенный tooprovide четвертый сценарии многие ко многим.

| Сценарий&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Пример |  |
|:---:| --- | --- |
|  [Один к одному](#one-to-one) |Задача *taskB* зависит от задачи *taskA*. <p/> Выполнение задачи *taskB* не начнется, пока задача *taskA* не будет успешно выполнена. |![Схема: зависимость задач "один к одному"][1] |
|  [Один ко многим](#one-to-many) |Задача *taskC* зависит от задач *taskA* и *taskB*. <p/> Выполнение задачи *taskC* не начнется, пока задачи *taskA* и *taskB* не будут успешно выполнены). |![Схема: зависимость задач "один ко многим"][2] |
|  [Диапазон идентификаторов задач](#task-id-range) |Задача *taskD* зависит от ряда задач. <p/> *taskD* не будут запланированы для выполнения до hello задачи с идентификаторами *1* через *10* завершена успешно |![Схема: зависимость диапазона идентификаторов задач][3] |

> [!TIP]
> Можно создать **многие ко многим** связи, например когда задачи C, D, E и F каждого зависят от задач A и B. Это полезно, например, в которых подчиненных задач зависит от hello вывод нескольких задач вышестоящего Параллелизованный предварительной обработки сценариев.
> 
> В примерах этого раздела hello зависимая задача выполняется только после успешного завершения задач родительского hello. Данное поведение является поведением по умолчанию hello для зависимой задачи. Можно запустить выполнение зависимой задачи родительская задача завершается посредством определения поведения по умолчанию hello toooverride действие зависимостей. В разделе hello [действия зависимостей](#dependency-actions) подробные сведения см.

### <a name="one-to-one"></a>Один к одному
Связи «один к одному» задача зависит от hello успешное завершение задачи одного родительского элемента. toocreate hello зависимостей, укажите идентификатор одну задачу toohello [TaskDependencies][net_taskdependencies].[ OnId] [ net_onid] статический метод, при заполнении hello [DependsOn] [ net_dependson] свойство [CloudTask] [ net_cloudtask].

```csharp
// Task 'taskA' doesn't depend on any other tasks
new CloudTask("taskA", "cmd.exe /c echo taskA"),

// Task 'taskB' depends on completion of task 'taskA'
new CloudTask("taskB", "cmd.exe /c echo taskB")
{
    DependsOn = TaskDependencies.OnId("taskA")
},
```

### <a name="one-to-many"></a>Один ко многим
В отношении "один ко многим" задача зависит от выполнения hello несколько родительской задачи. toocreate Здравствуйте зависимостей, образуют набор задач идентификаторы toohello [TaskDependencies][net_taskdependencies].[ OnIds] [ net_onids] статический метод, при заполнении hello [DependsOn] [ net_dependson] свойство [CloudTask] [ net_cloudtask].

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

### <a name="task-id-range"></a>Диапазон идентификаторов задач
В зависимость от родительской задачи задача зависит hello hello выполнения задач, идентификаторы которых находятся в пределах диапазона.
зависимость toocreate hello, сначала укажите hello и последнего ИД задач в диапазоне toohello hello [TaskDependencies][net_taskdependencies].[ OnIdRange] [ net_onidrange] статический метод, при заполнении hello [DependsOn] [ net_dependson] свойство [CloudTask] [net_cloudtask].

> [!IMPORTANT]
> При использовании задач диапазоны Идентификаторов для зависимостей hello идентификаторы задач в диапазоне hello *должен* быть строковые представления значений целое число со знаком.
> 
> Каждая задача в диапазоне hello должны удовлетворять зависимостей hello успешному завершению работы или завершение со сбоем, задано слишком действие зависимостей сопоставленных tooa**Satisfy**. В разделе hello [действия зависимостей](#dependency-actions) подробные сведения см.
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

## <a name="dependency-actions"></a>Действия зависимостей

По умолчанию зависимая задача или набор задач выполняется только после успешного завершения родительской задачи. В некоторых сценариях может потребоваться зависимые задачи toorun даже в случае сбоя hello родительской задачи. Можно переопределить поведение по умолчанию hello, указав действие зависимостей. Действие зависимостей указывает, является ли выполнение зависимой задачи подходящих toorun, основании hello успешности hello родительской задачи. 

Например предположим, что зависимая задача ожидает данные из hello завершения задачи вышестоящего hello. В случае сбоя задачи вышестоящего hello hello зависимая задача по-прежнему возможно может toorun, с помощью старых данных. В этом случае действия зависимостей можно указать hello зависимых она подходящих toorun несмотря на сбой hello hello родительской задачи.

Действие зависимостей зависит от условия выхода для hello родительской задачи. Можно указать действие зависимостей для любого hello следующие условия выхода; для .NET, в разделе hello [ExitConditions] [ net_exitconditions] класс подробные сведения:

- Если возникла ошибка предварительной обработки.
- Если возникла ошибка отправки файла. Если задачу hello завершает работу с кодом выхода, который указан через **exitCodes** или **exitCodeRanges**, а затем возникает ошибка передачи файла, указанное, приоритет имеет код выхода hello действие hello.
- При выходе из задачу hello с кодом выхода, определяемый hello **ExitCodes** свойство.
- При выходе из задачу hello с кодом выхода, который попадает в диапазон, заданный hello **ExitCodeRanges** свойство.
- Здравствуйте вариант по умолчанию, если задача hello завершается с кодом выхода, не заданные **ExitCodes** или **ExitCodeRanges**, или если hello задача завершается с предварительной обработки ошибок и hello **PreProcessingError**  свойство не задано, или если hello задачи завершается неудачей с файлом Загрузите ошибки и hello **FileUploadError** свойство не задано. 

toospecify действие зависимостей в .NET, набор hello [ExitOptions][net_exitoptions].[ DependencyAction] [ net_dependencyaction] свойство hello выходного условия. Hello **DependencyAction** свойство принимает одно из двух значений:

- Параметр hello **DependencyAction** свойство слишком**Satisfy** означает, что зависимые задачи подходящих toorun Если hello родительская задача завершается с указанной ошибкой.
- Параметр hello **DependencyAction** свойство слишком**блок** указывает, что зависимые задачи, подходящие toorun.

Здравствуйте, по умолчанию hello **DependencyAction** свойство **Satisfy** для код выхода 0, и **блок** для всех остальных условий выхода.

Hello следующий фрагмент кода задает hello **DependencyAction** свойство для родительской задачи. Если hello родительская задача завершается с предварительной обработки ошибок или с hello ошибки с заданными кодами hello зависимых задач заблокирована. Если родительская задача hello создано любая другая ошибка ненулевое значение, зависимую задачу hello — право toorun.

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

## <a name="code-sample"></a>Пример кода
Hello [TaskDependencies] [ github_taskdependencies] образец проекта является одним из hello [образцы кода пакетной службы Azure] [ github_samples] на GitHub. Это решение Visual Studio демонстрирует следующее:

- Как tooenable задач зависимость от задания
- Как toocreate задачи зависят от других задач
- Выполнение tooexecute тех задач в пуле вычислительных узлов.

## <a name="next-steps"></a>Дальнейшие действия
### <a name="application-deployment"></a>Развертывание приложения
Hello [пакетов приложений](batch-application-packages.md) пакета предоставляет простой способ развертывания tooboth и версия приложения hello, выполняемых задач на вычислительных узлах.

### <a name="installing-applications-and-staging-data"></a>Установка приложений и промежуточных данных
В разделе [установка приложений и данных в пакете размещения вычислительных узлов] [ forum_post] форуме пакетной службы Azure hello Обзор для подготовки узлов toorun задачи. Записываются одним из членов команды hello пакетной службы Azure, эта статья — хороший учебник на toocopy приложения hello различными способами, входные данные задачи и другие файлы tooyour вычислительных узлов.

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
