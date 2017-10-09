---
title: "aaaPersist заданий и задач вывода tooAzure хранилища с hello API службы пакетной службы Azure | Документы Microsoft"
description: "Узнайте, как задачи пакета toopersist toouse API пакетной службы и задания вывода tooAzure хранилища."
services: batch
author: tamram
manager: timlt
editor: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.openlocfilehash: 71b3f7c0dda2d2a9d8eb3eef83229873c70ca22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="persist-task-data-tooazure-storage-with-hello-batch-service-api"></a>Сохранение данных задач tooAzure хранилища с hello API пакетной службы

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Начиная с версии 2017 г-05-01, hello API пакетной службы поддерживает сохранение вывода данных tooAzure хранилища для задач и задание диспетчера задач, которые выполняются в пулах, hello конфигурации виртуальной машины. При добавлении задачи, можно указать контейнер в хранилище Azure как hello назначение для выходных данных задачи hello. Здравствуйте, пакетная служба, а затем записывает любого контейнера toothat вывода данных, при завершении задачи hello.

Выполняется hello toousing преимущества пакета, выходные данные задачи toopersist API службы является приложение hello toomodify, hello задач не требуется. Вместо этого с несколько простых изменения tooyour клиентского приложения можно сохранить задачу hello выходные данные в пределах hello код, создающий задачу hello.   

## <a name="when-do-i-use-hello-batch-service-api-toopersist-task-output"></a>Когда использовать выходные данные задачи toopersist hello API пакетной службы?

Пакет Azure предоставляет несколько способов toopersist выходные данные задачи. Использование hello API пакетной службы — удобный подход, который наиболее подходит toothese сценариев:

- Требуется toowrite кода toopersist задач выходные данные в клиентском приложении без изменения приложения hello, на котором работает ваша задача.
- Вы хотите toopersist выходных данных пакетных задач и задачи диспетчера заданий в пулах, созданных с помощью hello конфигурации виртуальной машины.
- Вы хотите toopersist выходной tooan контейнер хранилища Azure с произвольное имя.
- Требуется tooan хранилища Azure toopersist выходной контейнер с именем, соответствующим toohello [пакетных файлов, принятых standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). 

Если ваш сценарий отличается от перечисленных выше, может потребоваться tooconsider другой подход. Например, hello пакетной службы API не поддерживает в настоящее время потоковой передачи tooAzure выходные данные хранилища во время выполнения задачи hello. Выход toostream, рассмотрите возможность использования библиотеки пакетных файлов, принятых hello, доступных для .NET. Для других языков вам потребуется tooimplement собственное решение. Дополнительные сведения о других способах сохранения выходных данных задачи. в разделе [Persist заданий и задач вывода tooAzure хранения](batch-task-output.md). 

## <a name="create-a-container-in-azure-storage"></a>Создание контейнера в службе хранилища Azure

Задача toopersist вывод tooAzure хранилища, вам потребуется toocreate контейнер, который служит в качестве назначения hello для выходные файлы. Создание контейнера hello, прежде чем запускать задачу, предпочтительно перед отправкой задания. toocreate hello контейнера, используйте hello соответствующую хранилища Azure клиентскую библиотеку или SDK. Дополнительные сведения об API-интерфейсов хранилища Azure см. в разделе hello [документации по хранилищу Azure](https://docs.microsoft.com/azure/storage/).

Например, при создании приложения на языке C# используйте hello [клиентской библиотеки хранилища Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage/). Следующий пример показывает как Hello toocreate контейнер:

```csharp
CloudBlobContainer container = storageAccount.CreateCloudBlobClient().GetContainerReference(containerName);
await conainer.CreateIfNotExists();
```

## <a name="get-a-shared-access-signature-for-hello-container"></a>Получить подписанный URL-адрес для контейнера hello

После создания контейнера hello получите подпись общего доступа (SAS) с контейнером toohello доступ для записи. Подписанный URL-адрес содержит контейнер toohello делегированный доступ. Hello SAS предоставляет доступ с указанным набором разрешений и через указанный интервал времени. Hello пакетная служба должна SAS с контейнера toohello выходные данные задачи toowrite записи разрешений. Дополнительные сведения о подписанных URL-адресах см. в разделе [Использование подписанных URL-адресов \(SAS\) в службе хранилища Azure](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

При получении SAS, с помощью API-интерфейсов хранилища Azure hello hello API возвращает строку токена SAS. Эта строка токена, включает все параметры hello SAS, включая разрешения hello и интервал приветствия, над какой hello SAS является допустимым. toouse hello tooaccess SAS контейнера в хранилище Azure, необходимо tooappend hello SAS строку лексемы toohello ресурса (URI). Hello URI ресурса, а также hello добавляется маркер SAS, предоставляет доступ с проверкой подлинности tooAzure хранилища.

Hello следующем примере показано, как строку hello контейнера токена tooget SAS только для записи, а затем добавляет URI контейнера toohello hello SAS:

```csharp
string containerSasToken = container.GetSharedAccessSignature(new SharedAccessBlobPolicy()
{
    SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddDays(1),
    Permissions = SharedAccessBlobPermissions.Write
});

string containerSasUrl = container.Uri.AbsoluteUri + containerSasToken; 
```

## <a name="specify-output-files-for-task-output"></a>Указание файлов для выходных данных задачи

toospecify выходные файлы для задачи, создать коллекцию [OutputFile](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile) объектов и назначьте его toohello [CloudTask.OutputFiles](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudtask.outputfiles#Microsoft_Azure_Batch_CloudTask_OutputFiles) свойства при создании задачи hello. 

Hello пример кода .NET создает задачу, которая создает случайные числа tooa файл с именем `output.txt`. пример Hello создает выходной файл для `output.txt` toobe записи toohello контейнера. пример Hello также создает выходные файлы для всех файлов журнала, соответствующие шаблону файла hello `std*.txt` (_например_, `stdout.txt` и `stderr.txt`). URL-адрес контейнера Hello требует hello SAS, который был создан ранее для контейнера hello. Hello пакетная служба использует hello SAS tooauthenticate доступа toohello контейнера: 

```csharp
new CloudTask(taskId, "cmd /v:ON /c \"echo off && set && (FOR /L %i IN (1,1,100000) DO (ECHO !RANDOM!)) > output.txt\"")
{
    OutputFiles = new List<OutputFile>
    {
        new OutputFile(
            filePattern: @"..\std*.txt",
            destination: new OutputFileDestination(
         new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId)),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
        new OutputFile(
            filePattern: @"output.txt",
            destination: 
         new OutputFileDestination(new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId + @"\output.txt")),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
}
```

### <a name="specify-a-file-pattern-for-matching"></a>Указание шаблона файла для поиска соответствий

При указании выходной файл, можно использовать hello [OutputFile.FilePattern](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile.filepattern#Microsoft_Azure_Batch_OutputFile_FilePattern) toospecify свойство шаблон файла для сопоставления. шаблон файла Hello может соответствовать файлов ноль, один файл или набор файлов, созданных задачей «hello».

Hello **FilePattern** свойство поддерживает подстановочные знаки стандартной файловой системы, такие как `*` (для нерекурсивных соответствует) и `**` (для рекурсивного соответствует). Hello приведенном выше примере указывается hello файл шаблона toomatch `std*.txt` нерекурсивно: 

`filePattern: @"..\std*.txt"`

tooupload один файл, укажите шаблон файла без подстановочных знаков. Hello приведенном выше примере указывается hello файл шаблона toomatch `output.txt`:

`filePattern: @"output.txt"`

### <a name="specify-an-upload-condition"></a>Указание условия отправки

Hello [OutputFileUploadOptions.UploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileuploadoptions.uploadcondition#Microsoft_Azure_Batch_OutputFileUploadOptions_UploadCondition) свойство разрешает условного Отправка выходных файлов. Распространенным сценарием является tooupload один набор файлов, если hello задача выполнена успешно, а другой набор файлов в случае неудачи. Например вы можете tooupload подробных файлов журнала только в том случае, когда задача hello завершается ошибкой и завершает работу с ненулевой код выхода. Аналогичным образом вы можете tooupload результирующие файлы только в том случае, если задача hello завершается успешно, как возможно, эти файлы отсутствуют или являются неполными, если происходит сбой задачи hello.

Hello кода выше образце hello **UploadCondition** свойство слишком**TaskCompletion**. Этот параметр указывает, что это файл hello toobe отправлен после завершения задачи hello, независимо от того, hello значение кода выхода hello. 

`uploadCondition: OutputFileUploadCondition.TaskCompletion`

Другие параметры в разделе hello [OutputFileUploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.common.outputfileuploadcondition) перечисления.

### <a name="disambiguate-files-with-hello-same-name"></a>Файлы с hello устранения неоднозначности таким же именем

Hello задачи в задании может создают файлы, содержащие hello таким же именем. Например, для каждой задачи, выполняемой в задании, создаются файлы `stdout.txt` и `stderr.txt`. Поскольку каждая задача выполняется в его собственном контексте, эти файлы не конфликтует hello узла в файловой системе. Однако при передаче файлов из общего контейнера tooa несколько задач, вам потребуется toodisambiguate файлы с hello таким же именем.

Hello [OutputFileBlobContainerDestination.Path](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination.path#Microsoft_Azure_Batch_OutputFileBlobContainerDestination_Path) свойство задает BLOB-объект назначения hello или виртуальный каталог для выходных файлов. Можно использовать hello **путь** свойство tooname hello blob или виртуального каталога, таким образом, что выходные данные файлы с таким же именем должны иметь уникальные имена в хранилище Azure hello. Использование ИД задачи: hello hello пути является хорошим способом tooensure уникальные имена и легко идентифицировать файлы.

Если hello **FilePattern** свойству tooa выражение с подстановочными знаками, то все файлы, которые соответствуют шаблону hello не переданные toohello виртуальный каталог, заданный параметром hello **путь** свойство. Например, если hello контейнером является `mycontainer`, hello задачи с Идентификатором `mytask`, и является шаблон файла hello `..\std*.txt`, затем hello абсолютные идентификаторы URI toohello выходные файлы в хранилище Azure будет выглядеть следующим образом:

```
https://myaccount.blob.core.windows.net/mycontainer/mytask/stderr.txt
https://myaccount.blob.core.windows.net/mycontainer/mytask/stdout.txt
```

Если hello **FilePattern** свойство является набор toomatch одно имя файла, то есть не содержит подстановочные знаки, затем hello значение hello **путь** указывает имя hello полное больших двоичных объектов . Если предполагается конфликты имен с один файл из нескольких задач, включите hello имя виртуального каталога hello как часть toodisambiguate имя файла hello этих файлов. Например, набор hello **путь** идентификатор задачи hello tooinclude свойства, символ-разделитель hello (обычно косой черты) и имя файла hello:

`path: taskId + @"/output.txt"`

Hello абсолютные идентификаторы URI toohello выходных файлов для списка задач будет аналогичен:

```
https://myaccount.blob.core.windows.net/mycontainer/task1/output.txt
https://myaccount.blob.core.windows.net/mycontainer/task2/output.txt
```

Дополнительные сведения о виртуальных каталогах в хранилище Azure см. в разделе [hello двоичные объекты перечислены в контейнер](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container).


## <a name="diagnose-file-upload-errors"></a>Диагностика ошибок при передаче файлов

Если отправка выходных данных файлов tooAzure хранилища, а затем задачу hello переходит toohello **завершено** состояния и hello [TaskExecutionInformation.FailureInformation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.taskexecutioninformation.failureinformation#Microsoft_Azure_Batch_TaskExecutionInformation_FailureInformation) свойству. Изучите hello **FailureInformation** toodetermine свойство причину возникновения ошибки. Например это ошибка, возникающая на передачу файла, если не удается найти контейнер hello: 

```
Category: UserError
Code: FileUploadContainerNotFound
Message: One of hello specified Azure container(s) was not found while attempting tooupload an output file
```

На каждой отправки файла пакета записывает два журнала файлов toohello вычислительных узлов, `fileuploadout.txt` и `fileuploaderr.txt`. Можно проверить эти toolearn файлы журналов, дополнительные о конкретной ошибке. В случаях, где hello попыталась загрузить файл никогда не, например, так как не удалось выполнить саму задачу hello затем эти файлы журналов не существует.

## <a name="diagnose-file-upload-performance"></a>Диагностика производительности передачи файлов

Hello `fileuploadout.txt` прогресса отправки журналов файла. Можно проверить этот файл toolearn, которые делаются узнать, как долго загружает файл. Следует помнить, существует множество ключевых факторов производительности tooupload, включая размер hello узла hello, другие действия на узле hello во время hello передачи hello, является ли целевой контейнер hello hello, сколько узлов же регионе в качестве пула пакета hello Отправка toohello учетной записи хранилища в hello же время и т. д.

## <a name="use-hello-batch-service-api-with-hello-batch-file-conventions-standard"></a>Использовать API-Интерфейс службы hello пакета с hello пакетных файлов, принятых standard

При сохранении выходные данные задачи с hello API пакетной службы вы можно присвоить имя конечного контейнера и больших двоичных объектов, однако вам нравится. Вы также можете tooname их в соответствии с toohello [пакетных файлов, принятых standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). стандартный файл соглашения Hello определяет имена hello hello конечный контейнер и BLOB-объектов в хранилище Azure для данной выходной файл, на основе имен hello hello заданий и задач. Если вы используете hello стандартные соглашения файлов для именования выходных файлов, то выходные файлы были доступны для просмотра в hello [портал Azure](https://portal.azure.com).

При разработке на языке C# можно использовать методы hello, встроенные в hello [пакетных файлов, принятых библиотека для .NET](https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files). Эта библиотека создает hello правильно указаны контейнеры и путей больших двоичных объектов для вас. Например можно вызвать hello API tooget hello верное имя для контейнера hello, на основе имени задания hello:

```csharp
string containerName = job.OutputStorageContainerName();
```

Можно использовать hello [CloudJobExtensions.GetOutputStorageContainerUrl](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files.cloudjobextensions.getoutputstoragecontainerurl) tooreturn метод адреса (SAS) URL-адрес используется toowrite toohello контейнера. Затем можно передать этот SAS toohello [OutputFileBlobContainerDestination](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination) конструктор.

При разработке на языке, отличном от C#, необходимо будет стандартного соглашения файлов hello tooimplement самостоятельно.

## <a name="code-sample"></a>Пример кода

Hello [PersistOutputs] [ github_persistoutputs] образец проекта является одним из hello [образцы кода пакетной службы Azure] [ github_samples] на GitHub. Это решение Visual Studio показывает, как toouse hello пакета клиентская библиотека .NET toopersist задачи вывода toodurable хранилища. toorun hello образец, выполните следующие действия:

1. Привет открыть проект в **Visual Studio 2015 или более новой версии**.
2. Добавить пакет и хранилища **учетные данные учетной записи** слишком**AccountSettings.settings** в проекте Microsoft.Azure.Batch.Samples.Common hello.
3. **Построение** (но не запускайте) hello решения. Восстановите необходимые пакеты NuGet в случае появления соответствующего запроса.
4. Используйте hello Azure портала tooupload [пакета приложения](batch-application-packages.md) для **PersistOutputsTask**. Включить hello `PersistOutputsTask.exe` и ее зависимые сборки в пакете .zip hello, идентификатор приложения hello набор слишком версии пакета «PersistOutputsTask» и приложение hello слишком «1.0».
5. **Запуск** (выполнения) hello **PersistOutputs** проекта.
6. При вводе toouse технологии запрашиваемые toochoose hello сохраняемости для выполнения образца hello, **2** toorun hello выборке, используя выходные данные задачи toopersist hello API пакетной службы.
7. При желании образец hello снова запустить, введя **3** toopersist выходные данные с API-Интерфейс службы пакета hello и tooname hello контейнера и больших двоичных объектов путь назначения toohello стандартные соглашения файлов в соответствии с.

## <a name="next-steps"></a>Дальнейшие действия

- Дополнительные сведения о сохранения выходных данных задачи с библиотекой hello файлов, принятых для .NET. в разделе [сохранения заданий и задач tooAzure данные хранилища с библиотекой hello пакетных файлов, принятых для .NET toopersist ](batch-task-output-file-conventions.md).
- Сведения о других подходов для сохранения выходных данных в пакете Azure см. в разделе [Persist заданий и задач вывода tooAzure хранения](batch-task-output.md).

[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
