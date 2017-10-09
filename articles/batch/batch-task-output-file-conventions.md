---
title: "aaaPersist заданий и задач вывода tooAzure хранилища с библиотекой hello файлов, принятых для .NET — пакетной службы Azure | Документы Microsoft"
description: "Узнайте, как библиотека toouse соглашения файлов пакета Azure для .NET toopersist задачи пакета и tooAzure выходные данные задания хранилища и представление hello сохраняются выходные данные в hello портал Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf2ac8632a13d32438c1bdcf11b4b9649de1e2b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a>Сохранение заданий и задач tooAzure данные хранилища с библиотекой hello пакетных файлов, принятых для .NET toopersist 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Одним из способов toopersist данных задачи — toouse hello [Azure пакетных файлов, принятых библиотека для .NET][nuget_package]. Hello библиотеки соглашения файлов упрощает процесс сохранения выходных данных задачи hello tooAzure данных хранения и извлечения. Можно использовать библиотеку hello файлов, принятых в коде задачи и клиента &mdash; в коде задачи для сохранения файлов и в клиенте кода toolist и извлекать их. Код задачи можно также использовать hello библиотеки tooretrieve hello выходные данные вышестоящего задачи, такие как в [зависимости задач](batch-task-dependencies.md) сценария. 

tooretrieve выходные файлы с библиотекой hello соглашения файлов, можно найти файлы hello данное задание или задачу, указав их по Идентификатору и цели. Не нужно tooknow hello имена и местоположения файлов hello. Например можно использовать все промежуточные файлы библиотеки toolist hello соглашения файлов для данной задачи или получить файл предварительного просмотра для данного задания.

> [!TIP]
> Начиная с версии 2017 г-05-01, hello API пакетной службы поддерживает сохранение вывода данных tooAzure хранилища для задач и задание диспетчера задач, выполняемых на пулы, созданных с помощью hello конфигурации виртуальной машины. Hello API пакетной службы предоставляет простой способ toopersist выходные данные в коде hello, которое создает задачу и служит в качестве библиотеку альтернативных toohello соглашения файлов. Можно изменить выходные данные toopersist пакета клиентских приложений без необходимости приложения hello tooupdate, на котором работает ваша задача. Дополнительные сведения см. в разделе [сохранения данных задач tooAzure хранилища с hello API пакетной службы](batch-task-output-files.md).
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a>Когда использовать выходные данные задачи toopersist hello соглашения файл библиотеки?

Пакет Azure предоставляет несколько способов toopersist выходные данные задачи. Hello соглашения файлов является наиболее подходит toothese сценариев:

- Можно легко изменить hello код приложения hello, что ваша задача запущена toopersist файлы с помощью библиотеки файлов, принятых hello.
- Во время выполнения hello задачи по-прежнему требуется tooAzure toostream данных хранилища.
- Вы хотите toopersist данные из пулов, созданных с помощью hello конфигурацию облачной службы или конфигурации виртуальной машины hello.
- Клиентское приложение или другие задачи в hello заданий toolocate потребностей и загрузки выходных файлов задач по Идентификатору или по назначению. 
- Вы хотите tooview выходные данные задачи в hello портал Azure.

Если ваш сценарий отличается от перечисленных выше, может потребоваться tooconsider другой подход. Дополнительные сведения о других способах сохранения выходных данных задачи. в разделе [Persist заданий и задач вывода tooAzure хранения](batch-task-output.md). 

## <a name="what-is-hello-batch-file-conventions-standard"></a>Что такое hello пакетных файлов, принятых standard?

Hello [пакетных файлов, принятых standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) предоставляет схему именования контейнеров назначения hello и выходные файлы записываются toowhich пути большого двоичного объекта. TooAzure сохраненные файлы хранилища, которые соответствуют toohello стандартные соглашения файлов автоматически доступны для просмотра в hello портал Azure. портал Hello учитывает соглашения об именовании hello и поэтому может отображать файлы, удовлетворяющие tooit.

Hello соглашения файлов библиотеки для .NET автоматически имен вашей контейнеров хранилища и выходных файлов задач toohello стандартные соглашения файлов в соответствии с. Hello файлов, принятых библиотека также предоставляет методы tooquery выходные файлы в хранилище Azure toojob идентификатор, идентификатор задачи или назначения в соответствии с.   

При разработке на языке, отличном от .NET, можно реализовать стандартного соглашения файлов hello самостоятельно в приложении. Дополнительные сведения см. в разделе [о стандартных пакетных файлов, принятых hello](batch-task-output.md#about-the-batch-file-conventions-standard).

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a>Связать tooyour учетной записи хранилища Azure пакетной учетной записи

данные вывода toopersist tooAzure хранилища с помощью hello соглашения файл библиотеки, необходимо сначала связать tooyour учетной записи хранилища Azure пакетной учетной записи. Если вы еще не сделали этого, связать tooyour учетной записи хранилища пакетной учетной записи с помощью hello [портал Azure](https://portal.azure.com):

1. Перейдите tooyour пакетной учетной записи в hello портал Azure. 
2. В разделе **Параметры** выберите **Учетная запись хранения**.
3. Если у вас еще нет учетной записи хранения, связанной с вашей учетной записью пакетной службы, нажмите кнопку **Учетная запись хранения (нет)**.
4. Выберите учетную запись хранения из списка hello для вашей подписки. Для повышения производительности рекомендуется использовать учетную запись хранилища Azure, hello же регионе, что учетной записи пакетной hello запущенным задачами.

## <a name="persist-output-data"></a>Сохранение выходных данных

toopersist заданий и задач выходных данных с библиотекой файлов, принятых hello, создать контейнер в хранилище Azure, а затем сохраните hello выходной toohello контейнер. Используйте hello [клиентской библиотеки хранилища Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage) в контейнере toohello выходные данные задачи кода tooupload hello задачи. 

Дополнительные сведения о работе с контейнерами и большими двоичными объектами в службе хранилища Azure см. в разделе [Приступая к работе со службой хранилища больших двоичных объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).

> [!WARNING]
> Сохраняются все выходные данные заданий и задач с файлов, принятых hello библиотеки хранятся в hello в одном контейнере. Если большого числа задач toopersist файлы hello же времени, [хранилища ограничивает](../storage/common/storage-performance-checklist.md#blobs) может применяться.
> 
> 

### <a name="create-storage-container"></a>Создание контейнера хранилища

tooAzure выходные данные задачи toopersist хранилища, сначала создайте контейнер, вызвав [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync]. Этот метод расширения принимает объект [CloudStorageAccount][net_cloudstorageaccount] в качестве параметра. Он создает контейнер, именованный соответствующим toohello файлов, принятых Standard Edition, таким образом, его содержимое, видимые hello Azure портал и hello методы получения, описанных далее в статье hello.

Обычно помещаются в клиентском приложении toocreate кода hello контейнер &mdash; hello приложение, которое создает ваш пулы, заданий и задач.

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference toohello linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create hello blob storage container for hello outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a>Хранение выходных данных задач

Теперь, когда подготовлен контейнера в хранилище Azure, задачи можно сохранить выходной toohello контейнер с помощью hello [TaskOutputStorage] [ net_taskoutputstorage] класса, найденный в библиотеке файлов, принятых hello.

В коде задач, сначала создайте [TaskOutputStorage] [ net_taskoutputstorage] объекта, а затем при задачу hello завершил свою работу, вызовите hello [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] toosave метод tooAzure его выходные данные хранилища.

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code tooprocess data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

Hello `kind` параметр hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) метод классифицирует hello сохраняются файлы. Существует четыре стандартных типа [TaskOutputKind] [net_taskoutputkind]: `TaskOutput`, `TaskPreview`, `TaskLog` и `TaskIntermediate.`. Также можно определить пользовательские категории выходных данных.

Эти типы выходных данных позволяют toospecify, какой тип toolist выходные данные при hello позже запросе пакета сохраняются выходные значения данной задачи. Другими словами при перечислении hello выходные данные задачи, можно отфильтровать список hello в одном из выходных данных типа hello. Например «приведите hello *предварительного просмотра* выходных данных для задачи *109*.» Дополнительные сведения о со списком и получение выходных данных отображается в [получить выходные данные](#retrieve-output) далее в статье hello.

> [!TIP]
> Hello тип выходных данных также определяет, где в hello Azure portal конкретного файла будет: *TaskOutput*-файлы по категориям, отображаются в списке **задач выходные файлы**, и *TaskLog*файлы отображаются в списке **задач журналы**.
> 
> 

### <a name="store-job-outputs"></a>Хранения выходных данных заданий

Кроме выводит toostoring задачи, можно хранить hello выходные данные, связанные с заданием целиком. Например в задаче слияния hello задания подготовки к просмотру фильма может сохраняться фильма hello полностью к просмотру как выходные данные задания. После завершения задания клиентского приложения можно перечислить и получить выходные данные hello для задания hello и не требуется tooquery hello отдельные задачи.

Сохранить выходные данные задания, вызывающему Привет [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] метода и укажите hello [JobOutputKind] [ net_joboutputkind] и имя файла:

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

Как и в hello **TaskOutputKind** типа для выходных данных задачи, используйте hello [JobOutputKind] [ net_joboutputkind] toocategorize тип задания сохранения файлов. Этот параметр позволяет toolater запроса (список) определенного типа выходных данных. Hello **JobOutputKind** типа включает категорий выходных данных и предварительного просмотра, а также поддерживает создание пользовательских категорий.

### <a name="store-task-logs"></a>Хранение журналов задач

В дополнение к этому toopersisting хранения toodurable файлов, когда задача или задание завершается, может потребоваться toopersist файлы, которые обновляются во время выполнения задачи hello &mdash; файлы журнала или `stdout.txt` и `stderr.txt`, например. Для этой цели hello Azure пакетных файлов, принятых библиотека предоставляет hello [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] метод. С [SaveTrackedAsync][net_savetrackedasync], можно отслеживать файл tooa обновлений на узле hello (с интервалом, можно указать) и сохранять эти обновления tooAzure хранилища.

В следующий фрагмент кода hello, мы используем [SaveTrackedAsync] [ net_savetrackedasync] tooupdate `stdout.txt` в хранилище Azure каждые 15 секунд во время выполнения hello задачи «hello»:

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// hello primary task logic is wrapped in a using statement that sends updates to
// hello stdout.txt blob in Storage every 15 seconds while hello task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code tooprocess data and produce output file(s) */

    // We are tracking hello disk file toosave our standard output, but the
    // node agent may take up too3 seconds tooflush hello stdout stream to
    // disk. So give hello file a moment toocatch up.
     await Task.Delay(stdoutFlushDelay);
}
```

раздел в комментарий Hello `Code tooprocess data and produce output file(s)` — это заполнитель для кода hello, как правило, выполняет свою задачу. Например, вам может понадобиться код, который скачивает данные из службы хранилища Azure и выполняет с ними операцию преобразования или вычисления. важной частью этот фрагмент кода Hello дает переноса такого кода в `using` tooperiodically блок обновления файла с [SaveTrackedAsync][net_savetrackedasync].

агент узла Hello — это программа, которая запускается на каждом узле в пуле hello и предоставляет интерфейс команды управления hello между узлом hello и hello пакетной службы. Hello `Task.Delay` вызов не требуется в конце hello это `using` tooensure блока, hello агента узла имеет содержимое hello tooflush времени стандарта toohello stdout.txt файл на узле hello. Эта задержка не имея ее возможные toomiss hello последние несколько секунд выходных данных. Задержка может не потребоваться для всех файлов.

> [!NOTE]
> При включении отслеживания с помощью файла **SaveTrackedAsync**только *добавляет* toohello отслеживаемого файла, сохраненного tooAzure хранилища. Используйте этот метод только для отслеживания не Смена файлов журнала или других файлов, которые записываются toowith добавить операции toohello конец файла hello.
> 
> 

## <a name="retrieve-output-data"></a>Извлечение выходных данных

При извлечении материализованный выходных данных с использованием библиотеки Azure пакетных файлов, принятых hello, осуществляется в виде задач и задание ориентированное. Можно запросить hello выходных данных для данной задачи или задания без необходимости tooknow пути в хранилище Azure или даже именем файла. Вместо этого выходные файлы можно запрашивать по идентификатору задачи или задания.

Hello следующий фрагмент кода перебор рабочих заданий, выводит некоторые сведения о hello выходные файлы для задачи «hello» и затем загружает его файлы из хранилища.

```csharp
foreach (CloudTask task in myJob.ListTasks())
{
    foreach (OutputFileReference output in
        task.OutputStorage(storageAccount).ListOutputs(
            TaskOutputKind.TaskOutput))
    {
        Console.WriteLine($"output file: {output.FilePath}");

        output.DownloadToFileAsync(
            $"{jobId}-{output.FilePath}",
            System.IO.FileMode.Create).Wait();
    }
}
```

## <a name="view-output-files-in-hello-azure-portal"></a>Просмотр выходных файлов hello портал Azure

Hello Azure портал отобразит выходных файлов задач и журналов, которые являются сохраненного tooa связанной учетной записи хранилища Azure с помощью hello [пакетных файлов, принятых standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). Можно реализовать эти соглашения о себе в hello язык или библиотеку hello соглашения файлов можно использовать в приложениях .NET.

Отображение hello tooenable выходные файлы в портале hello, должен удовлетворять hello следующие требования:

1. [Связать учетную запись хранилища Azure](#requirement-linked-storage-account) tooyour пакетной учетной записи.
2. Следовать toohello стандартные соглашения об именовании для файлов и контейнеров хранилища, при сохранении выходные данные. Определение hello из этих правил можно найти в hello соглашения файлов библиотеки [README][github_file_conventions_readme]. При использовании hello [Azure пакетных файлов, принятых] [ nuget_package] toopersist библиотеки на выход, файлы сохраняются toohello стандартные соглашения файлов в соответствии с.

выходные данные задачи tooview файлы и журналы в hello портал Azure, переходы toohello задаче, выходные данные которого вас интересуют, затем выберите пункт **сохраненный выходные файлы** или **сохраненные журналы**. На данном рисунке показан hello **сохраненный выходные файлы** для задачи «hello» с Идентификатором «007»:

![Выходные данные задач колонки в hello портал Azure][2]

## <a name="code-sample"></a>Пример кода

Hello [PersistOutputs] [ github_persistoutputs] образец проекта является одним из hello [образцы кода пакетной службы Azure] [ github_samples] на GitHub. Это решение Visual Studio показывает, как задачу toouse hello Azure пакетных файлов, принятых библиотеки toopersist вывода toodurable хранилища. toorun hello образец, выполните следующие действия:

1. Привет открыть проект в **Visual Studio 2015 или более новой версии**.
2. Добавить пакет и хранилища **учетные данные учетной записи** слишком**AccountSettings.settings** в проекте Microsoft.Azure.Batch.Samples.Common hello.
3. **Построение** (но не запускайте) hello решения. Восстановите необходимые пакеты NuGet в случае появления соответствующего запроса.
4. Используйте hello Azure портала tooupload [пакета приложения](batch-application-packages.md) для **PersistOutputsTask**. Включить hello `PersistOutputsTask.exe` и ее зависимые сборки в пакете .zip hello, идентификатор приложения hello набор слишком версии пакета «PersistOutputsTask» и приложение hello слишком «1.0».
5. **Запуск** (выполнения) hello **PersistOutputs** проекта.
6. При вводе toouse технологии запрашиваемые toochoose hello сохраняемости для выполнения образца hello, **1** toorun hello выборке, используя выходные данные задачи toopersist hello соглашения файл библиотеки. 

## <a name="next-steps"></a>Дальнейшие действия

### <a name="get-hello-batch-file-conventions-library-for-net"></a>Получить hello пакетных файлов, принятых библиотеки для .NET

Библиотека Hello пакетных файлов, принятых для .NET можно найти в [NuGet][nuget_package]. Библиотека Hello расширяет hello [CloudJob] [ net_cloudjob] и [CloudTask] [ net_cloudtask] классы за счет новых методов. См. также hello [справочная документация](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) для файлов, принятых библиотеки hello.

Hello [исходный код] [ github_file_conventions] для файлов, принятых hello библиотеки доступен на GitHub в hello Microsoft Azure SDK для .NET репозитория. 

### <a name="explore-other-approaches-for-persisting-output-data"></a>Другие методы сохранения выходных данных

- В разделе [Persist заданий и задач вывода tooAzure хранения](batch-task-output.md) Обзор сохранения данных задач и задание.
- В разделе [сохранения данных задач tooAzure хранилища с hello API пакетной службы](batch-task-output-files.md) toolearn как toopersist hello API пакетной службы toouse выходных данных.

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_file_conventions]: https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Batch/FileConventions
[github_file_conventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_fileconventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[net_joboutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputkind.aspx
[net_joboutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.aspx
[net_joboutputstorage_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.saveasync.aspx
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_prepareoutputasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.cloudjobextensions.prepareoutputstorageasync.aspx
[net_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx
[net_savetrackedasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.savetrackedasync.aspx
[net_taskoutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputkind.aspx
[net_taskoutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx
[nuget_manager]: https://docs.nuget.org/consume/installing-nuget
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/

[1]: ./media/batch-task-output/task-output-01.png "Селекторы сохраненных выходных файлов и журналов на портале"
[2]: ./media/batch-task-output/task-output-02.png "Выходные данные задач колонки в hello портал Azure"
