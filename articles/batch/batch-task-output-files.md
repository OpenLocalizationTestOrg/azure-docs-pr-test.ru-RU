---
title: "Сохранение выходных данных заданий и задач в службе хранилища Azure с помощью API пакетной службы Azure | Документы Майкрософт"
description: "Подробнее об использовании API пакетной службы для сохранения выходных данных заданий и задач в службе хранилища Azure."
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
ms.openlocfilehash: 2530b7c20347b9fb58aee4dfe693847cf3911741
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="persist-task-data-to-azure-storage-with-the-batch-service-api"></a>Сохранение данных для задач в службе хранилища Azure с помощью API пакетной службы

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Начиная с версии 2017-05-01, API пакетной службы поддерживает сохранение выходных данных в службе хранилища Azure для обычных задач и задач диспетчера заданий, которые выполняются в пулах с конфигурацией виртуальной машины. При добавлении задачи в службе хранилища Azure можно указать контейнер в качестве назначения для выходных данных задачи. Затем после выполнения задачи пакетная служба будет записывать выходные данные в этот контейнер.

Преимуществом использования API пакетной службы для сохранения выходных данных для задачи является отсутствие необходимости изменять приложение, в котором выполняется задача. Вместо этого при незначительном изменении клиентского приложения выходные данные задачи можно сохранять в коде, который создает эта задача.   

## <a name="when-do-i-use-the-batch-service-api-to-persist-task-output"></a>Примеры использования API пакетной службы для сохранения выходных данных задачи

Пакетная служба Azure поддерживает несколько способов сохранения выходных данных задачи. API пакетной службы представляет собой удобный способ, который лучше всего подходит для следующих сценариев.

- Необходимо написать код для сохранения выходных данных задачи из клиентского приложения, не изменяя приложение, в котором выполняется ваша задача.
- Необходимо сохранять выходные данные задач пакетной службы и задач диспетчера заданий в пулах, созданных с конфигурацией виртуальной машины.
- Необходимо сохранять выходные данные в контейнер службы хранилища Azure с произвольным именем.
- Необходимо сохранять выходные данные в контейнер службы хранилища Azure в соответствии со [стандартом соглашений об именовании файлов пакетной службы](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). 

Если ваш случай отличается от перечисленных выше, возможно, придется использовать другой метод. Например, API пакетной службы в настоящее время не поддерживает потоковый вывод в службу хранилища Azure во время выполнения задачи. Для потокового вывода попробуйте использовать библиотеку соглашений о пакетных файлах, доступную для .NET. Для других языков придется придумать свое собственное решение. Дополнительные сведения о других способах сохранения выходных данных задачи см. в разделе [Сохранение выходных данных заданий и задач в службе хранилища Azure](batch-task-output.md). 

## <a name="create-a-container-in-azure-storage"></a>Создание контейнера в службе хранилища Azure

Для сохранения выходных данных задач в службе хранилища Azure необходимо создать контейнер, который служит в качестве назначения для файлов выходных данных. Создайте контейнер до выполнения задачи, предпочтительно перед отправкой задания. Для создания контейнера используйте соответствующую клиентскую библиотеку службы хранилища Azure или пакет SDK. Дополнительные сведения об интерфейсах API службы хранилища Azure см. в [документации по службе хранилища Azure](https://docs.microsoft.com/azure/storage/).

Например, при создании приложения на языке C# используйте [клиентскую библиотеку службы хранилища Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage/). В следующем примере показано, как создать контейнер.

```csharp
CloudBlobContainer container = storageAccount.CreateCloudBlobClient().GetContainerReference(containerName);
await conainer.CreateIfNotExists();
```

## <a name="get-a-shared-access-signature-for-the-container"></a>Получение подписанного URL-адреса для контейнера

После создания контейнера получите подписанный URL-адрес (SAS) с доступом к контейнеру с правом записи. SAS предоставляет делегированный доступ к контейнеру. SAS предоставляет доступ с заданным набором разрешений и в течение определенного интервала времени. Для записи выходных данных задачи в контейнер пакетной службе требуется SAS с разрешениями на запись. Дополнительные сведения о подписанных URL-адресах см. в разделе [Использование подписанных URL-адресов \(SAS\) в службе хранилища Azure](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

При получении SAS с помощью интерфейсов API службы хранилища Azure интерфейс API возвращает строку токена SAS. Эта строка содержит все параметры SAS, включая разрешения и интервал времени, в течение которого SAS является действительным. Чтобы использовать SAS для доступа к контейнеру в службе хранилища Azure, строку токена SAS необходимо добавить к коду URI ресурса. Код URI ресурса, вместе с добавленным маркером SAS, предоставляет доступ к службе хранилища Azure.

В следующем примере показано, как получить строку токена SAS, доступного только на запись, для контейнера, а затем добавить SAS в код URI контейнера:

```csharp
string containerSasToken = container.GetSharedAccessSignature(new SharedAccessBlobPolicy()
{
    SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddDays(1),
    Permissions = SharedAccessBlobPermissions.Write
});

string containerSasUrl = container.Uri.AbsoluteUri + containerSasToken; 
```

## <a name="specify-output-files-for-task-output"></a>Указание файлов для выходных данных задачи

Чтобы указать выходные файлы для задачи, создайте коллекцию объектов [OutputFile](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile) и назначьте ему свойство [CloudTask.OutputFiles](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudtask.outputfiles#Microsoft_Azure_Batch_CloudTask_OutputFiles) при создании задачи. 

В следующем примере кода .NET создается задача, которая записывает случайные числа в файл с именем `output.txt`. В примере создается выходной файл, чтобы записывать `output.txt` в контейнер. В примере также создаются выходные файлы для всех файлов журнала, соответствующих шаблону файла `std*.txt` (_например_, `stdout.txt` и `stderr.txt`). Для URL-адреса контейнера требуется SAS, который был создан ранее для контейнера. Пакетная служба использует SAS для проверки подлинности при доступе к контейнеру: 

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

При указании выходного файла можно использовать свойство [OutputFile.FilePattern](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile.filepattern#Microsoft_Azure_Batch_OutputFile_FilePattern), чтобы задать шаблон файла для поиска соответствий. Файл шаблона может соответствовать одному файлу, набору файлов, создаваемых задачей, или ни одному файлу.

Свойство **FilePattern** поддерживает стандартные подстановочные знаки файловой системы, такие как `*` (для нерекурсивных совпадений) и `**` (для рекурсивных совпадений). Например, в приведенном выше примере кода указан шаблон файла для нерекурсивного сопоставления с `std*.txt`: 

`filePattern: @"..\std*.txt"`

Чтобы отправить один файл, укажите шаблон файла без подстановочных знаков. Например, в приведенном выше примере кода указан шаблон файла для сопоставления с `output.txt`:

`filePattern: @"output.txt"`

### <a name="specify-an-upload-condition"></a>Указание условия отправки

Свойство [OutputFileUploadOptions.UploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileuploadoptions.uploadcondition#Microsoft_Azure_Batch_OutputFileUploadOptions_UploadCondition) разрешает условную отправку выходных файлов. Распространенным сценарием является отправка одного набора файлов, если задача выполнена успешно, и другого набора файлов в случае неудачи. Например, файлы подробного журнала можно отправлять только в том случае, когда задача завершается ошибкой и завершает работу с ненулевым кодом выхода. Аналогичным образом файлы результатов можно отправлять только в том случае, если задача выполнена успешно, поскольку эти файлы могут отсутствовать или быть неполными, если задача завершается с ошибкой.

В примере кода выше для свойства **UploadCondition** задано значение **TaskCompletion**. Это значение указывает, что файл должен быть отправлен по окончании задачи, независимо от значения кода выхода. 

`uploadCondition: OutputFileUploadCondition.TaskCompletion`

Другие параметры см. в перечислении [OutputFileUploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.common.outputfileuploadcondition).

### <a name="disambiguate-files-with-the-same-name"></a>Устранение неоднозначности файлов с одинаковым именем

Задачи в задании могут создавать файлы с одинаковым именем. Например, для каждой задачи, выполняемой в задании, создаются файлы `stdout.txt` и `stderr.txt`. Поскольку каждая задача выполняется в своем собственном контексте, эти файлы не конфликтуют в файловой системе узла. Однако при отправке файлов из нескольких задач в общий контейнер необходимо устранять неоднозначность файлов с одинаковым именем.

Свойство [OutputFileBlobContainerDestination.Path](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination.path#Microsoft_Azure_Batch_OutputFileBlobContainerDestination_Path) задает целевой большой двоичный объект или виртуальный каталог для выходных файлов. Свойство **Path** можно использовать для именования больших двоичных объектов или виртуального каталога таким образом, чтобы выходные файлы с одинаковым именем получали уникальные имена в хранилище Azure. Использование идентификатора задачи в пути позволяет обеспечивать уникальность имен и быстро определять файлы.

Если для свойства **FilePattern** установлено выражение с подстановочными знаками, то все файлы, соответствующие шаблону, будут отправляться в виртуальный каталог, заданный свойством **Path**. Например, если имеются контейнер `mycontainer`, идентификатор задачи `mytask` и шаблон файла `..\std*.txt`, то абсолютные URI для выходных файлов в службе хранилища Azure будут выглядеть следующим образом:

```
https://myaccount.blob.core.windows.net/mycontainer/mytask/stderr.txt
https://myaccount.blob.core.windows.net/mycontainer/mytask/stdout.txt
```

Если свойство **FilePattern** должно совпадать с именем одного файла, то есть оно не содержит подстановочные знаки, то значение свойства **Path** задает полное имя большого двоичного объекта. Если могут происходить конфликты имен с одним файлом из нескольких задач, то для устранения неоднозначности таких файлов включите имя виртуального каталога в имя файла. Например, в качестве значения свойства **Path** укажите идентификатор задачи, знак-разделитель (обычно косую черту) и имя файла:

`path: taskId + @"/output.txt"`

Абсолютные URI для выходных файлов для списка задач будут выглядеть следующим образом:

```
https://myaccount.blob.core.windows.net/mycontainer/task1/output.txt
https://myaccount.blob.core.windows.net/mycontainer/task2/output.txt
```

Дополнительные сведения о виртуальных каталогах в службе хранилища Azure см. в разделе [Перечисление больших двоичных объектов в контейнере](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container).


## <a name="diagnose-file-upload-errors"></a>Диагностика ошибок при передаче файлов

Если отправка выходных файлов в службу хранилища Azure завершается ошибкой, то задача переходит в состояние **Завершено** и устанавливается свойство [TaskExecutionInformation.FailureInformation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.taskexecutioninformation.failureinformation#Microsoft_Azure_Batch_TaskExecutionInformation_FailureInformation). Чтобы определить причину возникновения ошибки, проанализируйте свойство **FailureInformation**. Например, имеется ошибка, возникающая при передаче файла, если не удается найти контейнер: 

```
Category: UserError
Code: FileUploadContainerNotFound
Message: One of the specified Azure container(s) was not found while attempting to upload an output file
```

В каждом сеансе передачи файла пакетная служба записывает в вычислительный узел два файла журнала: `fileuploadout.txt` и `fileuploaderr.txt`. Для получения дополнительных сведений о конкретной ошибке можно проанализировать файлы журнала. В тех случаях, когда передача файлов никогда не выполнялась, например, так как не удалось выполнить саму задачу, этих файлов журналов вообще не будет.

## <a name="diagnose-file-upload-performance"></a>Диагностика производительности передачи файлов

В файле `fileuploadout.txt` регистрируется ход выполнения передачи. С помощью этого файла можно получить дополнительные сведения о продолжительности сеансов передачи файлов. Обратите внимание, что на производительность передачи влияют различные факторы, в том числе размер узла, другие операции, выполняемые на узле во время передачи, находится ли целевой контейнер в том же регионе, что и пул пакетной службы, сколько узлов одновременно выполняют передачу данных в учетную запись хранения и т. д.

## <a name="use-the-batch-service-api-with-the-batch-file-conventions-standard"></a>Использование API пакетной службы со стандартом соглашений о пакетных файлах

При сохранении выходных данных задачи с помощью API пакетной службы имена целевому контейнеру и большим двоичным объектам можно присваивать произвольным образом. Имена для них также можно выбирать в соответствии со [стандартом соглашений о пакетных файлах](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). Стандарт соглашений об именовании файлов определяет имена целевого контейнера и большого двоичного объекта в службе хранилища Azure для заданного выходного файла на основе имен задания и задачи. Если для именования выходных файлов используется стандарт соглашений об именовании файлов, то выходные файлы доступны для просмотра на [портале Azure](https://portal.azure.com).

При работе на языке C# можно использовать методы, встроенные в [библиотеку соглашений о пакетных файлах для .NET](https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files). Эта библиотека создает корректно именованные пути к контейнерам и большим двоичным объектам. Например, можно вызвать API для получения корректного имени для контейнера на основе имени задания:

```csharp
string containerName = job.OutputStorageContainerName();
```

Для возврата подписанного URL-адреса (SAS), используемого для записи в контейнер, можно применить метод [CloudJobExtensions.GetOutputStorageContainerUrl](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files.cloudjobextensions.getoutputstoragecontainerurl). Затем этот SAS можно передать в конструктор [OutputFileBlobContainerDestination](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination).

При работе на языке, отличном от C#, необходимо самостоятельно реализовать стандарт соглашений об именовании файлов.

## <a name="code-sample"></a>Пример кода

Пример проекта [PersistOutputs][github_persistoutputs] — это один из [примеров кода пакетной службы Azure][github_samples] на портале GitHub. Это решение Visual Studio демонстрирует использование клиентской библиотеки пакетной службы для сохранения выходных данных задачи в долговременном хранилище. Чтобы запустить пример приложения, выполните следующее.

1. Откройте проект в **Visual Studio 2015 или более поздней версии**.
2. Добавьте свои **данные** учетной записи пакетной службы и учетной записи хранения в **AccountSettings.settings** в проекте Microsoft.Azure.Batch.Samples.Common.
3. **сборку** решения (но не запускайте его). Восстановите необходимые пакеты NuGet в случае появления соответствующего запроса.
4. С помощью портала Azure передайте [пакет приложения](batch-application-packages.md) для **PersistOutputsTask**. Добавьте в ZIP-файл пакета `PersistOutputsTask.exe` и его зависимые сборки , задайте для приложения идентификатор PersistOutputsTask, а для версии пакета приложения — значение "1.0".
5. **Запустите** (выполните) проект **PersistOutputs**.
6. Когда появится запрос на выбор технологии постоянного хранения для выполнения образца, введите **2** для запуска образца с помощью API пакетной службы для сохранения выходных данных задачи.
7. При необходимости запустите пример снова путем ввода **3** для сохранения выходных данных с помощью API пакетной службы, а также именования пути к целевому контейнеру и большому двоичному объекту в соответствии со стандартом соглашений об именовании файлов.

## <a name="next-steps"></a>Дальнейшие действия

- Дополнительные сведения о сохранении выходных данных задачи с помощью библиотеки соглашений по файлам для .NET см. в разделе [Сохранение данных заданий и задач в службе хранилища Azure с помощью библиотеки соглашений о пакетных файлах для .NET](batch-task-output-file-conventions.md).
- Дополнительные сведения о других способах сохранения выходных данных задачи в пакетной службе Azure см. в разделе [Сохранение выходных данных заданий и задач в службе хранилища Azure](batch-task-output.md).

[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
