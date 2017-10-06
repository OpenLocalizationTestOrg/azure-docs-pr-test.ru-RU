---
title: "aaaTutorial - используется клиентская библиотека hello пакетной службы Azure для .NET | Документы Microsoft"
description: "Изучите основные понятия hello пакетной службы Azure и создайте простое решение, с помощью .NET."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 76cb9807-cbc1-405a-8136-d1e53e66e82b
ms.service: batch
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 06062b3886a8081bd9a831824a981503ef55f9b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-building-solutions-with-hello-batch-client-library-for-net"></a>Приступить к созданию решения с hello пакета клиентской библиотеки для .NET

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Основы hello объекта [пакетной службы Azure] [ azure_batch] и hello [пакета .NET] [ net_api] библиотеки в этой статье в обсуждении C# образца приложения шаг по шаг. Мы рассмотрим как пример приложения hello использует hello пакетной службы tooprocess параллельной рабочей нагрузки в облаке hello, а также их взаимодействие с [хранилища Azure](../storage/common/storage-introduction.md) для файла промежуточного хранения и извлечения. Будет узнать общий рабочий процесс приложения пакета и получить представление о базовых hello основных компонентов пакета, например заданий, задач, пулы и вычислительных узлов.

![Рабочий процесс решения пакетной службы (основной)][11]<br/>

## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что вы уже работали с C# и Visual Studio. Также предполагается, что вы будете требования к создания может toosatisfy hello учетной записи, указанные ниже для Azure и пакета hello и служб хранилища.

### <a name="accounts"></a>Учетные записи
* **Учетная запись Azure.** Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure][azure_free_account].
* **Учетная запись пакетной службы**. Если у вас есть подписка Azure, [создайте учетную запись пакетной службы Azure](batch-account-create-portal.md).
* **Учетная запись хранения**. См. раздел [Создание учетной записи хранения](../storage/common/storage-create-storage-account.md#create-a-storage-account) в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).

> [!IMPORTANT]
> Пакетов в настоящее время поддерживает *только* hello **общего назначения** тип учетной записи хранения, как описано в шаге #5 [создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account) в [о Azure учетные записи хранения](../storage/common/storage-create-storage-account.md).
>
>

### <a name="visual-studio"></a>Visual Studio
Необходимо иметь **Visual Studio 2015 или более новой** toobuild hello образца проекта. Бесплатные и пробные версии Visual Studio можно найти в hello [Общие сведения о продуктах Visual Studio][visual_studio].

### <a name="dotnettutorial-code-sample"></a>*DotNetTutorial* 
Hello [DotNetTutorial] [ github_dotnettutorial] образца является одним из hello найти множество образцов кода пакета в hello [образцы azure пакета] [ github_samples] репозитория на GitHub. Можно загрузить все образцы hello, щелкнув **клон или загрузки > загрузить ZIP** на домашней странице hello репозитория или щелкнув hello [azure пакета образцы master.zip] [ github_samples_zip]прямой ссылкой скачивания. Как только вы извлекли содержимое hello hello ZIP-файл, hello решения можно найти в hello следующие папки:

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a>Обозреватель пакетной службы Azure (необязательно)
Hello [обозреватель пакета Azure] [ github_batchexplorer] является бесплатное средство, которое включено в hello [образцы azure пакета] [ github_samples] репозитория в GitHub. При toocomplete не требуется этого учебника, его можно использовать при разработке и отладке пакета решения.

## <a name="dotnettutorial-sample-project-overview"></a>Общие сведения о примере проекта DotNetTutorial
Hello *DotNetTutorial* образец кода представляет собой решение Visual Studio, которое состоит из двух проектов: **DotNetTutorial** и **TaskApplication**.

* **DotNetTutorial** представляет hello клиентское приложение, которое взаимодействует с tooexecute hello пакета и хранилище служб параллельной рабочей нагрузки на вычислительных узлов (виртуальных машин). DotNetTutorial работает на локальной рабочей станции.
* **TaskApplication** — hello программы, которая выполняется на вычислительных узлах в Azure tooperform hello фактическую работу. В образце hello `TaskApplication.exe` анализирует hello текст в файл, загруженный из хранилища Azure (hello входного файла). Затем он создает текстовый файл (hello выходной файл), содержащий список hello первых трех слов, которые содержатся во входном файле hello. После создания выходного файла hello, TaskApplication передает tooAzure hello файла хранилища. Это делает доступными toohello клиентского приложения для загрузки. TaskApplication выполняется параллельно на нескольких вычислительных узлах hello пакетной службы.

Hello следующей схеме показана hello основных операций, выполняемых клиентским приложением hello *DotNetTutorial*и приложение hello, выполняемое задачи hello *TaskApplication*. Этот основной рабочий процесс является типичным для многих вычислительных решений, созданных с помощью пакетной службы. Хотя здесь не показаны каждый компонент, доступный в hello пакетная служба, практически все пакета сценарий включает некоторые части этого рабочего процесса.

![Пример рабочего процесса пакетной службы][8]<br/>

[**Шаг 1.**](#step-1-create-storage-containers) Создайте **контейнеры** в хранилище BLOB-объектов Azure.<br/>
[**Шаг 2.**](#step-2-upload-task-application-and-data-files) Отправка файлов приложения задач и toocontainers входные файлы.<br/>
[**Шаг 3.**](#step-3-create-batch-pool) Создайте **пул** пакетной службы.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**3a.** Здравствуйте, пул **StartTask** загрузки hello toonodes двоичные файлы (TaskApplication) задачи, которые они присоединиться к пулу hello.<br/>
[**Шаг 4.**](#step-4-create-batch-job) Создайте **задание** пакетной службы.<br/>
[**Шаг 5.**](#step-5-add-tasks-to-job) Добавить **задачи** toohello задания.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**5a.** Hello задачи, запланированные tooexecute на узлах.<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;**5b.** Каждая задача скачивает свои входные данные из службы хранилища Azure, а затем начинает выполнение.<br/>
[**Шаг 6.**](#step-6-monitor-tasks) Мониторинг задач.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**6a.** Как выполнить действия, они отправляют их вывода данных tooAzure хранилища.<br/>
[**Шаг 7.**](#step-7-download-task-output) Скачайте выходные данные задачи из службы хранилища.

Как уже упоминалось, решение не каждый пакет выполняет эти конкретные шаги и может включать другие, но hello *DotNetTutorial* образце приложения показано общих процессов найден в решении пакета.

## <a name="build-hello-dotnettutorial-sample-project"></a>Построение hello *DotNetTutorial* образца проекта
Перед запуском образца hello, необходимо указать пакет и хранения учетных данных учетной записи в hello *DotNetTutorial* проекта `Program.cs` файла. Если вы еще не сделали этого, откройте hello решений в Visual Studio, дважды щелкнув hello `DotNetTutorial.sln` файл решения. Или откройте его из среды Visual Studio с помощью hello **файл > Открыть > проект или решение** меню.

Откройте `Program.cs` внутри hello *DotNetTutorial* проекта. Затем добавьте учетные данные в качестве указанной верхней hello hello файла:

```csharp
// Update hello Batch and Storage account credential strings below with hello values
// unique tooyour accounts. These are used when constructing connection strings
// for hello Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> Как упоминалось выше, в настоящее время необходимо указать учетные данные hello для **общего назначения** учетной записи хранения в хранилище Azure. Пакет приложения используют хранилище больших двоичных объектов в пределах hello **общего назначения** учетной записи хранилища. Не указан hello учетные данные для учетной записи хранилища, который был создан, выбрав hello *хранилище больших двоичных объектов* тип учетной записи.
>
>

Пакет и хранения учетные данные учетной записи в колонке hello учетной записи каждой службы можно найти в hello [портал Azure][azure_portal]:

![Пакетное учетные данные на портале hello][9]
![учетные данные хранилища на портале hello][10]<br/>

Теперь, когда вы обновили hello проекта с помощью учетных данных, щелкните правой кнопкой мыши решение hello в обозревателе решений и выберите **построить решение**. Подтверждение восстановления hello любых пакетов NuGet при появлении.

> [!TIP]
> Если пакеты NuGet hello не восстанавливаются автоматически или при обнаружении ошибок, о пакетах hello toorestore сбоя, обеспечьте hello [диспетчера пакетов NuGet] [ nuget_packagemgr] установлен. Затем включите hello загрузки отсутствующих пакетов. В разделе [Включение пакета восстановления во время построения] [ nuget_restore] tooenable загрузки пакета.
>
>

В следующих разделах hello мы подразделяется на несколько hello пример приложения hello шагов, что оно работает tooprocess рабочую нагрузку в hello пакетная служба и обсудить эти шаги подробно. Мы рекомендуем вам toorefer toohello откройте решение в Visual Studio во время работы по hello оставшейся части этой статьи, так как не все строки кода в образце hello рассматривается.

Перейдите toohello вверху hello `MainAsync` метод в hello *DotNetTutorial* проекта `Program.cs` файл toostart с шага 1. Каждый шаг ниже примерно следующим hello продвижения метода вызывает `MainAsync`.

## <a name="step-1-create-storage-containers"></a>Шаг 1. Создание контейнеров службы хранилища
![Создание контейнеров в службе хранилища Azure][1]
<br/>

Пакетная служба включает встроенную поддержку для взаимодействия со службой хранилища Azure. Контейнеры в учетной записи хранилища обеспечивают hello файлов, необходимых hello задач, которые выполняются в вашей учетной записи пакета. контейнеры Hello также обеспечивают месте toostore hello выходные данные задачи hello выдавать. Здравствуйте, первое, что hello *DotNetTutorial* клиентского приложения является создание трех контейнеров в [хранилища больших двоичных объектов](../storage/common/storage-introduction.md):

* **приложение**: этот контейнер будет хранить выполнения задачи hello, а также любой из его зависимостей, таких как библиотеки DLL приложения hello.
* **входной**: задачи будут загружены файлы tooprocess hello данных с hello *ввода* контейнера.
* **выходные данные**: после завершения выполнения задач обработки входных файлов они загрузит hello результаты toohello *вывода* контейнера.

В порядке toointeract с хранилищем учетной записи и создавать контейнеры, мы используем hello [клиентская библиотека хранилища Azure для .NET][net_api_storage]. Мы создадим ссылку toohello учетную запись с [CloudStorageAccount][net_cloudstorageaccount]и, создайте [CloudBlobClient][net_cloudblobclient]:

```csharp
// Construct hello Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve hello storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create hello blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

Мы используем hello `blobClient` ссылаться на протяжении приложения hello и передайте его в качестве параметра tooseveral методы. Примером этого является в блоке кода hello, стоящего выше hello, где мы называем `CreateContainerIfNotExistAsync` tooactually создавать контейнеры hello.

```csharp
// Use hello blob client toocreate hello containers in Azure Storage if they don't
// yet exist
const string appContainerName    = "application";
const string inputContainerName  = "input";
const string outputContainerName = "output";
await CreateContainerIfNotExistAsync(blobClient, appContainerName);
await CreateContainerIfNotExistAsync(blobClient, inputContainerName);
await CreateContainerIfNotExistAsync(blobClient, outputContainerName);
```

```csharp
private static async Task CreateContainerIfNotExistAsync(
    CloudBlobClient blobClient,
    string containerName)
{
        CloudBlobContainer container =
            blobClient.GetContainerReference(containerName);

        if (await container.CreateIfNotExistsAsync())
        {
                Console.WriteLine("Container [{0}] created.", containerName);
        }
        else
        {
                Console.WriteLine("Container [{0}] exists, skipping creation.",
                    containerName);
        }
}
```

После создания контейнеров hello приложения hello, теперь можно отправить hello файлы, которые будут использоваться задачами hello.

> [!TIP]
> [Как toouse хранилища BLOB-объектов из .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) хороший Обзор работы с контейнеров хранилища Azure и больших двоичных объектов. В начале работы с использованием пакета должно быть hello верхней части списка для чтения.
>
>

## <a name="step-2-upload-task-application-and-data-files"></a>Шаг 2. Отправка приложения задач и файлов данных
![Задача передачи приложения и ввода (данных) файлы toocontainers][2]
<br/>

В файле hello операции, передачи *DotNetTutorial* сначала определяет коллекции **приложения** и **ввода** пути к файлам, в котором они хранятся на локальном компьютере hello. Затем он передает эти контейнеры toohello файлы, созданные на предыдущем шаге hello.

```csharp
// Paths toohello executable and its dependencies that will be executed by hello tasks
List<string> applicationFilePaths = new List<string>
{
    // hello DotNetTutorial project includes a project reference tooTaskApplication,
    // allowing us toodetermine hello path of hello task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// hello collection of data files that are toobe processed by hello tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload hello application and its dependencies tooAzure Storage. This is the
// application that will process hello data files, and will be executed by each
// of hello tasks on hello compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload hello data files. This is hello data that will be processed by each of
// hello tasks that are executed on hello compute nodes within hello pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

Существует два метода в `Program.cs` , участвующие в процессе загрузки hello:

* `UploadFilesToContainerAsync`: Этот метод возвращает коллекцию [ResourceFile] [ net_resourcefile] объектов (как описано ниже) и внутренним образом вызывает метод `UploadFileToContainerAsync` tooupload каждый файл, который является переданный hello *filePaths* параметра.
* `UploadFileToContainerAsync`: Этот метод называется методом hello, который фактически выполняет загрузку файла hello и создает hello [ResourceFile] [ net_resourcefile] объектов. После отправки файла hello, он получает подпись общего доступа (SAS) для файла hello и возвращает объект ResourceFile, который ее представляет. Подписанные URL-адреса также рассматриваются ниже.

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} toocontainer [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set hello expiry time and permissions for hello blob shared access signature.
        // In this case, no start time is specified, so hello shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct hello SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a>ResourceFiles
Объект [ResourceFile] [ net_resourcefile] предоставляет задачи в пакете с файлом tooa hello URL-адрес в службе хранилища Azure, загруженные tooa вычислительный узел перед запуском этой задачи. Hello [ResourceFile.BlobSource] [ net_resourcefile_blobsource] свойство указывает hello полный URL-адрес файла hello, которое существовало в хранилище Azure. Hello URL-адрес может также включать подписанного URL-адреса (SAS), предоставляющий безопасный доступ toohello файла. Большинство типов задач в пакетной службе .NET, в том числе перечисленные ниже, содержат свойство *ResourceFiles* .

* [CloudTask][net_task]
* [StartTask][net_pool_starttask]
* [JobPreparationTask][net_jobpreptask]
* [JobReleaseTask][net_jobreltask]

DotNetTutorial пример приложения Hello не использует hello JobPreparationTask или JobReleaseTask типы задач, но вы можете прочитать больше о них в [выполнения задания Подготовка и выполнение задач в пакете Azure вычислительные узлы](batch-job-prep-release.md).

### <a name="shared-access-signature-sas"></a>Подписанный URL-адрес (SAS)
Общего доступа, подписи, строки которого — Если включается как часть URL-адреса — предоставить безопасный доступ toocontainers и больших двоичных объектов в хранилище Azure. Hello DotNetTutorial приложение использует оба большого двоичного объекта и контейнера общие URL-адреса подписи доступа и показано, как эти общие tooobtain доступ к строки подписи из hello службы хранилища.

* **BLOB-объектов подписи коллективного доступа**: hello пула StartTask в DotNetTutorial использует URL-адреса большого двоичного объекта совместно при загрузке hello двоичные файлы приложения и файлы входных данных из хранилища (см. шаг #3 ниже). Hello `UploadFileToContainerAsync` метода в его DotNetTutorial `Program.cs` содержит hello код, который получает подпись общего доступа для каждого большого двоичного объекта. Для этого выполняется вызов [CloudBlob.GetSharedAccessSignature][net_sas_blob].
* **Контейнер подписи коллективного доступа**: как каждая задача завершит свою работу на вычислительном узле hello, передает его выходной файл toohello *вывода* контейнера в хранилище Azure. toodo этого TaskApplication использует контейнер подписанный URL-адрес, предоставляющий доступ на запись toohello контейнера как часть пути hello, когда он передает файл hello. Получение подписи общего доступа контейнера hello выполняется таким же образом, как при больших двоичных объектов для получения hello подписанном URL-адресе. В DotNetTutorial, вы найдете, hello `GetContainerSasUrl` вызывает вспомогательный метод [CloudBlobContainer.GetSharedAccessSignature] [ net_sas_container] toodo так. Вам нужно прочитать больше об использовании контейнера hello TaskApplication подписанный URL-в «шаг 6: задачи монитора.»

> [!TIP]
> Извлечение серии из двух частей hello подписей общего доступа [часть 1: hello понимание общая модель адреса (SAS) доступ](../storage/common/storage-dotnet-shared-access-signature-part-1.md) и [часть 2: Создание и использование подписи общего доступа (SAS) с помощью хранилища больших двоичных объектов](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn дополнительные о предоставлении toodata безопасного доступа к вашей учетной записи хранилища.
>
>

## <a name="step-3-create-batch-pool"></a>Шаг 3. Создание пула пакетной службы
![Создание пула пакетной службы][3]
<br/>

**Пул** пакетной службы — это коллекция вычислительных узлов (виртуальных машин), на которых пакетная служба выполняет задачи задания.

После загрузки приложения hello и toohello файлы данных учетной записи хранилища с помощью API-интерфейсов хранилища Azure, *DotNetTutorial* начинает делать вызовы toohello пакетная служба с интерфейсами API, предоставляемые библиотекой .NET пакета hello. Hello код сначала создает [BatchClient][net_batchclient]:

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

Далее образец hello создает пул вычислительных узлов в hello пакетной учетной записи с помощью вызова слишком`CreatePoolIfNotExistsAsync`. `CreatePoolIfNotExistsAsync`использует hello [BatchClient.PoolOperations.CreatePool] [ net_pool_create] toocreate метод пула в hello пакетной службы:

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create hello unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign hello StartTask that will be executed when compute nodes join hello pool.
        // In this case, we copy hello StartTask's resource files (that will be automatically downloaded
        // toohello node by hello StartTask) into hello shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for hello StartTask that copies hello task application files toothe
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need toomanually exit with a 0 for Batch toorecognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow hello specific error code PoolExists since that is expected if hello pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("hello pool {0} already existed when we tried toocreate it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

При создании пула с [CreatePool][net_pool_create], можно указать несколько параметров, например hello количество вычислительных узлов hello [размер узлов hello](../cloud-services/cloud-services-sizes-specs.md), и hello операционной узлы система. В *DotNetTutorial*, мы используем [CloudServiceConfiguration] [ net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 из [облачные службы](../cloud-services/cloud-services-guestos-update-matrix.md). 

Также можно создать пулы вычислительных узлов, которые представляют собой виртуальные машины Azure (ВМ), указав hello [VirtualMachineConfiguration] [ net_virtualmachineconfiguration] для пула. Пул вычислительных узлов виртуальных машин можно создать из образов Windows или [Linux](batch-linux-nodes.md). Источник Hello для образов виртуальной Машины может быть либо:

- Hello [виртуальных машин Azure Marketplace][vm_marketplace], который предоставляет образы Windows и Linux, готовые к использованию. 
- Настраиваемый образ, подготавливаемый и предоставляемый пользователем. Дополнительные сведения о пользовательских образах см. в руководстве по [разработке решений для крупномасштабных параллельных вычислений с помощью пакетной службы](batch-api-basics.md#pool).

> [!IMPORTANT]
> В пакетной службе за использование вычислительных ресурсов взимается плата. toominimize затраты, можно понизить `targetDedicatedComputeNodes` too1 перед запуском образца hello.
>
>

Вместе с этим свойствам физического узла, можно также указать [StartTask] [ net_pool_starttask] hello в пуле. Hello StartTask выполняет на каждом узле, как этот узел соединяет hello пул, и каждый раз при перезапуске узла. Hello StartTask особенно полезен для установки приложений на вычислительных узлах предыдущих toohello выполнения задач. Например если задач обработки данных с помощью сценариев Python, можно использовать на вычислительных узлах hello StartTask tooinstall Python.

В этом образце приложения hello StartTask копирует hello файлы, загружаемые из хранилища (которые указываются с помощью hello [StartTask][net_starttask].[ ResourceFiles] [ net_starttask_resourcefiles] свойство) из общего каталога hello StartTask рабочий каталог toohello, *все* доступны задачи, выполняемые на узле hello. По сути, это копирует `TaskApplication.exe` и его toohello зависимости общих каталогов на каждом узле при присоединении узла hello пула hello доступа к ней все задачи, выполняемых в узле hello.

> [!TIP]
> Hello **пакетов приложений** компонент пакетной службы Azure предоставляет другим способом tooget приложения в hello вычислительных узлов в пуле. В разделе [развертывания приложений toocompute узлов с пакетами приложения пакета](batch-application-packages.md) подробные сведения.
>
>

Также значительным в приведенном выше фрагменте кода hello используется hello двух переменных среды в hello *CommandLine* свойство hello StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` и `%AZ_BATCH_NODE_SHARED_DIR%`. Несколько переменных среды, которые являются определенной tooBatch автоматически настраивается каждом вычислительном узле в пуле пакета. Любой процесс, выполняемый задачей имеет доступ к переменным среды toothese.

> [!TIP]
> toofind Дополнительные сведения о переменных среды hello, доступные на вычислительных узлах пула и сведения о задаче рабочие каталоги, в разделе hello [параметры среды для задачи](batch-api-basics.md#environment-settings-for-tasks) и [файлов и каталогов ](batch-api-basics.md#files-and-directories) подразделы hello [пакета Обзор возможностей для разработчиков](batch-api-basics.md).
>
>

## <a name="step-4-create-batch-job"></a>Шаг 4. Создание задания пакетной службы
![Создание задания пакетной службы][4]<br/>

**Задание** пакетной службы — это коллекция задач, связанных с пулом вычислительных узлов. Hello задачи в задании, выполняются в hello связанный пул вычислительных узлов.

Задания можно использовать не только для упорядочивания и отслеживания задач в связанных рабочих нагрузок, но также и для налагающий определенные ограничения, например hello максимального времени для задания hello (и по расширению, его задачи), а также приоритет задания в заданиях tooother отношений в пакете hello Учетная запись. В этом примере задание hello связаны только с пулом hello, который был создан на шаге #3. Дополнительные свойства не настроены.

Все задания пакетной службы связаны с конкретным пулом. Эта связь указывает, какие узлы будут выполняться задачи hello задания. Можно указать это, используя hello [CloudJob.PoolInformation] [ net_job_poolinfo] свойства, как показано в приведенном ниже фрагменте кода hello.

```csharp
private static async Task CreateJobAsync(
    BatchClient batchClient,
    string jobId,
    string poolId)
{
    Console.WriteLine("Creating job [{0}]...", jobId);

    CloudJob job = batchClient.JobOperations.CreateJob();
    job.Id = jobId;
    job.PoolInformation = new PoolInformation { PoolId = poolId };

    await job.CommitAsync();
}
```

После создания задания задачи добавляются рабочие tooperform hello.

## <a name="step-5-add-tasks-toojob"></a>Шаг 5: Добавление toojob задачи
![Добавление задачи toojob][5]<br/>
*(1) задачи добавляются toohello задания, (2) hello задачи, запланированные toorun на узлах и (3) hello задачи загрузки tooprocess файлы данных hello*

Пакет **задачи** являются hello отдельных рабочих элементов, выполните на hello вычислительных узлов. Задача имеет командную строку и выполняется hello сценарии или исполняемые файлы, укажите в этой командной строке.

tooactually выполнения работы, задачи должны быть добавлены tooa задания. Каждый [CloudTask] [ net_task] настраивается с помощью свойства командной строки и [ResourceFiles] [ net_task_resourcefiles] (как в случае с StartTask hello пула), Задача Hello загружает toohello узла перед его командной строки выполняется автоматически. В hello *DotNetTutorial* образец проекта, каждая задача обрабатывает только один файл. Поэтому его коллекция ResourceFiles содержит один элемент.

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks toojob [{1}]...", inputFiles.Count, jobId);

    // Create a collection toohold hello tasks that we'll be adding toohello job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of hello tasks. Because we copied hello task application toothe
    // node's shared directory with hello pool's StartTask, we can access it via
    // hello shared directory on hello node that hello task runs on.
    foreach (ResourceFile inputFile in inputFiles)
    {
        string taskId = "topNtask" + inputFiles.IndexOf(inputFile);
        string taskCommandLine = String.Format(
            "cmd /c %AZ_BATCH_NODE_SHARED_DIR%\\TaskApplication.exe {0} 3 \"{1}\"",
            inputFile.FilePath,
            outputContainerSasUrl);

        CloudTask task = new CloudTask(taskId, taskCommandLine);
        task.ResourceFiles = new List<ResourceFile> { inputFile };
        tasks.Add(task);
    }

    // Add hello tasks as a collection, as opposed tooissuing a separate AddTask call
    // for each. Bulk task submission helps tooensure efficient underlying API calls
    // toohello Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> При доступе переменные среды, такие как `%AZ_BATCH_NODE_SHARED_DIR%` или выполнить приложение не найдено в узле hello `PATH`, командные строки задача должна начинаться с префикса `cmd /c`. Будет явно выполнение интерпретатор команд hello и задать для него tooterminate после выполнения команду. Это требование не требуется, если задачи Выполнение приложения в узле hello `PATH` (такие как *robocopy.exe* или *powershell.exe*) и используются переменные среды.
>
>

В рамках hello `foreach` цикла в приведенном выше фрагменте кода hello, можно увидеть, что hello командной строки для задачи «hello» создается таким образом, что слишком передаются три аргумента командной строки*TaskApplication.exe*:

1. Hello **первый аргумент** hello путь файла tooprocess hello. Это файл toohello hello локальный путь, как она находится на узле hello. Когда hello объекта ResourceFile в `UploadFileToContainerAsync` была создана более поздней версии, имя файла hello использовался для этого свойства (как параметр конструктора ResourceFile toohello). Это означает, что этот файл hello можно найти в hello же каталоге, что и *TaskApplication.exe*.
2. Hello **второй аргумент** указывает, что верхней hello *N* слова должны быть написаны toohello выходного файла. В образце hello это будет жестко, чтобы верхний три слова hello записываются toohello выходного файла.
3. Hello **третий аргумент** — hello подписанного URL-адреса (SAS), предоставляющий доступ на запись toohello **вывода** контейнера в хранилище Azure. *TaskApplication.exe* использует этот общий доступ к URL-адрес подписи при его передаче hello выходной файл tooAzure хранилища. Для этого можно найти кода hello в hello `UploadFileToContainer` метода в проекте TaskApplication hello `Program.cs` файла:

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference toohello container using hello SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload hello file (as a new blob) toohello container
        try
        {
                CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
                blob.UploadFromFile(filePath);

                Console.WriteLine("Write operation succeeded for SAS URL " + containerSas);
                Console.WriteLine();
        }
        catch (StorageException e)
        {

                Console.WriteLine("Write operation failed for SAS URL " + containerSas);
                Console.WriteLine("Additional error information: " + e.Message);
                Console.WriteLine();

                // Indicate that a failure has occurred so that when hello Batch service
                // sets hello CloudTask.ExecutionInformation.ExitCode for hello task that
                // executed this application, it properly indicates that there was a
                // problem with hello task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a>Шаг 6. Мониторинг задач
![Мониторинг задач][6]<br/>
*Hello клиентского приложения (1) мониторы hello задачи для завершения и состояние успеха и (2) hello данных результата tooAzure хранилища для задачи передачи*

При добавлении задачи задания tooa они автоматически в очередь и запланировать выполнение на вычислительных узлах пула hello, связанный с заданием hello. В зависимости от настройки hello пакета обрабатывает все очереди задач, планирования, повтор и другие задачи администрирования обязанностей.

Существует множество подходов toomonitoring выполнения задачи. Приложение DotNetTutorial — это простой пример, который сообщает только о трех состояниях: завершение, сбой задачи и успешное завершение. В рамках hello `MonitorTasks` метода в его DotNetTutorial `Program.cs`, есть три пакета .NET понятия, которые служат основанием для обсуждения. Они перечислены ниже в порядке появления.

1. **ODATADetailLevel.** Чтобы обеспечить выполнение приложения пакетной службы, необходимо указать класс [ODATADetailLevel][net_odatadetaillevel] в операциях получения списков (таких как получение списка задач задания). Добавить [эффективно запрашивать hello пакетной службы Azure](batch-efficient-list-queries.md) tooyour при чтении списка, если вы планируете выполнять каких-либо мониторинга состояния пакета приложений.
2. **TaskStateMonitor.** Класс [TaskStateMonitor][net_taskstatemonitor] предоставляет приложениям .NET пакетной службы вспомогательные служебные программы для мониторинга состояния задач. В `MonitorTasks`, *DotNetTutorial* ожидает, пока все задачи tooreach [TaskState.Completed] [ net_taskstate] за отведенное время. Затем он завершает задание hello.
3. **TerminateJobAsync**: завершение задания с помощью [JobOperations.TerminateJobAsync] [ net_joboperations_terminatejob] (или hello блокировки JobOperations.TerminateJob) помечает задание как завершенное. Это основные toodo таким образом, если решение пакет использует [JobReleaseTask][net_jobreltask]. Это особый тип задачи, который описан в статье о [задачах подготовки и завершения заданий](batch-job-prep-release.md).

Hello `MonitorTasks` метод *DotNetTutorial* `Program.cs` показан ниже:

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed tooreach hello Completed state within hello timeout period.";

    // Obtain hello collection of tasks currently managed by hello job. Note that we use
    // a detail level too specify that only hello "id" property of each task should be
    // populated. Using a detail level for all list operations helps toolower
    // response time from hello Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor toomonitor hello state of our tasks. In this case, we
    // will wait for all tasks tooreach hello Completed state.
    TaskStateMonitor taskStateMonitor
        = batchClient.Utilities.CreateTaskStateMonitor();

    try
    {
        await taskStateMonitor.WhenAll(tasks, TaskState.Completed, timeout);
    }
    catch (TimeoutException)
    {
        await batchClient.JobOperations.TerminateJobAsync(jobId, failureMessage);
        Console.WriteLine(failureMessage);
        return false;
    }

    await batchClient.JobOperations.TerminateJobAsync(jobId, successMessage);

    // All tasks have reached hello "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property tooensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update hello detail level toopopulate only hello task id and executionInfo
    // properties. We refresh hello tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate hello task's properties with hello latest info from hello Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with hello task. It is important toonote that
            // hello task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that hello application executed by hello task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within hello specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a>Шаг 7. Загрузка выходных данных задачи
![Загрузка выходных данных задачи из службы хранилища][7]<br/>

Теперь, когда hello работа завершена, hello выходные данные задач hello можно загрузить из хранилища Azure. Это делается с помощью вызова слишком`DownloadBlobsFromContainerAsync` в *DotNetTutorial* `Program.cs`:

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference tooa previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all hello block blobs in hello specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference toohello current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents tooa file in hello specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded too{0}", directoryPath);
}
```

> [!NOTE]
> Здравствуйте вызов слишком`DownloadBlobsFromContainerAsync` в hello *DotNetTutorial* приложение указывает, hello файлы должны быть загруженного tooyour `%TEMP%` папки. Свободное toomodify считаете это расположение выходных данных.
>
>

## <a name="step-8-delete-containers"></a>Шаг 8. Удаление контейнеров
Поскольку плата взимается для данных, которые хранятся в хранилище Azure, всегда является хорошей идеей tooremove больших двоичных объектов, больше не нужны для пакетных заданий. В его DotNetTutorial `Program.cs`, это делается с помощью трех вызовов toohello вспомогательный метод `DeleteContainerAsync`:

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

сам метод Hello просто Получает контейнер toohello ссылку, а затем вызывает [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:

```csharp
private static async Task DeleteContainerAsync(
    CloudBlobClient blobClient,
    string containerName)
{
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);

    if (await container.DeleteIfExistsAsync())
    {
        Console.WriteLine("Container [{0}] deleted.", containerName);
    }
    else
    {
        Console.WriteLine("Container [{0}] does not exist, skipping deletion.",
            containerName);
    }
}
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a>Шаг 9: Удалить задание hello и hello пула
На заключительном этапе hello все запрашиваемые toodelete hello задания и hello пул, созданные приложением DotNetTutorial hello. Вы не оплачиваете задания и задачи, но *платите* за используемые вычислительные узлы. Поэтому рекомендуется выделять узлы только при необходимости. Удаление неиспользуемых пулов может быть частью процесса обслуживания.

Hello BatchClient [JobOperations] [ net_joboperations] и [PoolOperations] [ net_pooloperations] имеют соответствующие методы удаления, которые вызываются, если Удаление подтверждения пользователем Hello:

```csharp
// Clean up hello resources we've created in hello Batch account if hello user so chooses
Console.WriteLine();
Console.WriteLine("Delete job? [yes] no");
string response = Console.ReadLine().ToLower();
if (response != "n" && response != "no")
{
    await batchClient.JobOperations.DeleteJobAsync(JobId);
}

Console.WriteLine("Delete pool? [yes] no");
response = Console.ReadLine();
if (response != "n" && response != "no")
{
    await batchClient.PoolOperations.DeletePoolAsync(PoolId);
}
```

> [!IMPORTANT]
> Помните, что вы платите за использование вычислительных ресурсов, поэтому удаление неиспользуемых пулов позволит сократить затраты. Кроме того помните, что при удалении пула удаляются все вычислительные узлы этого пула, и все данные на узлах hello будет неустранимой после удаления пула hello.
>
>

## <a name="run-hello-dotnettutorial-sample"></a>Запустите hello *DotNetTutorial* образца
При запуске образца приложения hello, вывод на консоль hello будет примерно следующее toohello. Во время выполнения, могут возникнуть приостановит `Awaiting task completion, timeout in 00:30:00...` во время запуска hello пул вычислительных узлов. Используйте hello [портал Azure] [ azure_portal] toomonitor пула, вычислительные узлы, заданий и задач во время и после выполнения. Используйте hello [портал Azure] [ azure_portal] или hello [обозреватель хранилищ Azure] [ storage_explorers] tooview hello ресурсов хранилища (контейнеры и большие двоичные объекты), создается приложение hello.

Обычно время выполнения равно **около 5 минут** при запуске приложения hello в конфигурации по умолчанию.

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe toocontainer [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll toocontainer [application]...
Uploading file ..\..\taskdata1.txt toocontainer [input]...
Uploading file ..\..\taskdata2.txt toocontainer [input]...
Uploading file ..\..\taskdata3.txt toocontainer [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks toojob [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within hello specified timeout period.
Downloading all files from container [output]...
All files downloaded tooC:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a>Дальнейшие действия
Чувствовать себя свободного toomake изменения слишком*DotNetTutorial* и *TaskApplication* tooexperiment с различными вычислений сценариев. Например, попробуйте добавить задержки выполнения слишком*TaskApplication*, такие как в случае с [Thread.Sleep][net_thread_sleep], toosimulate длительные задачи, а также отслеживать их на портале hello. Попробуйте установить дополнительные задачи или изменить hello количество вычислительных узлов. Добавление toocheck логику для и разрешить использование hello существующих времени выполнения toospeed пула (*указание*: извлечение `ArticleHelpers.cs` в hello [Microsoft.Azure.Batch.Samples.Common] [ github_samples_common] проекта в [образцы azure пакета][github_samples]).

Теперь, когда вы знакомы с hello базовый рабочий процесс пакета решения, это время toodig в дополнительные возможности toohello hello пакетной службы.

* Просмотрите hello [возможности пакетной обработки Обзор Azure](batch-api-basics.md) статьи, которая рекомендуется, если вы новую службу toohello.
* Здравствуйте, запуска на другие статьи по разработке пакета в списке **разработки подробные** в hello [план обучения пакета][batch_learning_path].
* Извлечение другой реализации обработки рабочей нагрузки hello «N основных слова» с помощью пакета в hello [TopNWords] [ github_topnwords] образца.
* Просмотрите hello пакета .NET [заметки о выпуске](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) для hello последние изменения в библиотеке hello.

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[github_dotnettutorial]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/DotNetTutorial
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_common]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/Common
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[net_api]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[net_api_storage]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudblobclient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobclient.aspx
[net_cloudblobcontainer]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudserviceconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudserviceconfiguration.aspx
[net_container_delete]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.deleteifexistsasync.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_poolinfo]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.protocol.models.cloudjob.poolinformation.aspx
[net_joboperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.joboperations
[net_joboperations_terminatejob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_jobpreptask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_jobreltask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_odatadetaillevel]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_pooloperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.pooloperations
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_resourcefile_blobsource]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.blobsource.aspx
[net_sas_blob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblob.getsharedaccesssignature.aspx
[net_sas_container]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblobcontainer.getsharedaccesssignature.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.resourcefiles.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_task_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.resourcefiles.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_taskstatemonitor]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskstatemonitor.aspx
[net_thread_sleep]: https://msdn.microsoft.com/library/274eh01d(v=vs.110).aspx
[net_virtualmachineconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.virtualmachineconfiguration.aspx
[nuget_packagemgr]: https://docs.nuget.org/consume/installing-nuget
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build
[storage_explorers]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/vs/
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-dotnet-get-started/batch_workflow_01_sm.png "Создание контейнеров в службе хранилища Azure"
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "Задача передачи приложения и ввода (данных) файлы toocontainers"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Создание пула пакетной службы"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Создание задания пакетной службы"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "Добавление задачи toojob"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "Мониторинг задач"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Скачивание выходных данных задачи из службы хранилища"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Рабочий процесс решения пакетной службы (полная схема)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "Учетные данные пакетной службы на портале"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "Учетные данные службы хранилища на портале"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Рабочий процесс решения пакетной службы (сокращенная схема)"
