---
title: "aaaTransfer данных с hello библиотека перемещения данных для хранилища Microsoft Azure | Документы Microsoft"
description: "Используйте hello библиотеки перемещения данных toomove или копирования данных tooor из больших двоичных объектов и содержимого файла. Копирование данных tooAzure хранилища из локальных файлов или копирования данных в пределах или между учетными записями хранения. Легко перенесите на tooAzure данных хранилища."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/22/2017
ms.author: seguler
ms.openlocfilehash: 9aec6cb171f794cc6ca432938ce499079e7dfdec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a>Передача данных с помощью hello библиотека перемещения данных для хранилища Microsoft Azure

## <a name="overview"></a>Обзор
Hello библиотека перемещения данных для хранилища Microsoft Azure — это библиотека кросс платформенных открытым исходным кодом, предназначенный для высокопроизводительных передача, загрузка и копирование файлов и больших двоичных объектах хранилища Azure. Эта библиотека является перемещение hello core data framework, лежащих в основе [AzCopy](../storage-use-azcopy.md). Hello библиотеки перемещения данных предоставляет удобные методы, недоступные в нашей традиционной [клиентской библиотеки хранилища Azure .NET](../blobs/storage-dotnet-how-to-use-blobs.md). Сюда входят hello возможность tooset hello число параллельных операций, отслеживание хода выполнения передачи, легко Возобновить отмененные передачи и многое другое.  

Эта библиотека также использует .NET Core, а это означает, что ее можно применять при создании приложений .NET для Windows, Linux и MacOS. toolearn Дополнительные сведения о .NET Core ссылаться toohello [документации .NET Core](https://dotnet.github.io/). Эта библиотека также подходит для традиционных приложений .NET Framework для Windows. 

В этом документе показано, как .NET Core toocreate консольное приложение, выполняется в Windows, Linux и macOS и выполняет hello следующие сценарии:

- Передача файлов и каталогов tooBlob хранилища.
- Определите hello число параллельных операций, при передаче данных.
- Отслеживание выполнения передачи данных.
- Возобновление отмененной передачи данных. 
- Скопируйте файл из tooBlob URL-адрес хранилища. 
- Скопируйте из tooBlob хранилища больших двоичных объектов хранилища.

**Необходимые компоненты:**

* [Visual Studio Code](https://code.visualstudio.com/)
* [учетная запись хранения Azure](storage-create-storage-account.md#create-a-storage-account)

> [!NOTE]
> Для работы с этим руководством предполагается, что у вас есть общее представление о [службе хранилища Azure](https://azure.microsoft.com/services/storage/). Если нет, чтение hello [tooAzure введение хранилища](storage-introduction.md) полезно документации. Самое главное, требуется слишком[создать учетную запись хранилища](storage-create-storage-account.md#create-a-storage-account) toostart с помощью hello библиотеки перемещения данных.
> 
> 

## <a name="setup"></a>Настройка  

1. Посетите hello [руководство по установке .NET Core](https://www.microsoft.com/net/core) tooinstall .NET Core. При выборе среды, выберите параметр командной строки hello. 
2. Из командной строки hello создайте каталог для проекта. Перейдите в этот каталог, затем введите `dotnet new` проект консольного toocreate на языке C#.
3. Откройте этот каталог в Visual Studio Code. Этот шаг можно быстро сделать с помощью hello командной строки, введя `code .`.  
4. Установка hello [C# расширения](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) из Visual Studio Marketplace кода hello. Перезапустите Visual Studio Code. 
5. На этом этапе должны отобразиться два запроса. Один позволяет добавлять «toobuild необходимых средств и отладки». Щелкните "Да". Второй запрос — для восстановления неразрешенных зависимостей. Щелкните "Восстановить".
6. Приложение теперь должен содержать `launch.json` файл в папке hello `.vscode` каталога. В этот файл, измените hello `externalConsole` значение слишком`true`.
7. Код Visual Studio позволяет toodebug приложений .NET Core. Попаданий `F5` toorun приложение и проверьте работоспособность настройки программы установки. Вы должны увидеть текст "Hello World!" Печать toohello консоли. 

## <a name="add-data-movement-library-tooyour-project"></a>Добавьте проект библиотеки перемещения данных tooyour

1. Добавить hello последнюю версию библиотеки перемещения данных toohello hello `dependencies` части вашего `project.json` файла. На момент написания статьи hello будет этой версии`"Microsoft.Azure.Storage.DataMovement": "0.5.0"` 
2. Добавить `"portable-net45+win8"` toohello `imports` раздела. 
3. Запрос должен отображать toorestore проекта. Нажмите кнопку «Восстановить» hello. Можно также восстановить проект из hello командной строки, введя команду hello `dotnet restore` hello корневом каталоге проекта.

Измените `project.json`.

    {
      "version": "1.0.0-*",
      "buildOptions": {
        "debugType": "portable",
        "emitEntryPoint": true
      },
      "dependencies": {
        "Microsoft.Azure.Storage.DataMovement": "0.5.0"
      },
      "frameworks": {
        "netcoreapp1.1": {
          "dependencies": {
            "Microsoft.NETCore.App": {
              "type": "platform",
              "version": "1.1.0"
            }
          },
          "imports": [
            "dnxcore50",
            "portable-net45+win8"
          ]
        }
      }
    }

## <a name="set-up-hello-skeleton-of-your-application"></a>Настроить основу hello объекта приложения
Hello первое, что мы делаем имеет значение «каркасного» hello, код приложения. Этот код запрашивает ключ учетной записи и имени учетной записи хранения и использует эти учетные данные toocreate `CloudStorageAccount` объекта. Этот объект является используется toointeract с нашей учетной записи хранения во всех сценариях передачи. Hello код также отображает запрос нам toochoose hello тип операции передачи, мы хотели бы tooexecute. 

Измените `Program.cs`.

```csharp
using System;
using System.Threading;
using System.Diagnostics;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.WindowsAzure.Storage.DataMovement;

namespace DMLibSample
{
    public class Program
    {
        public static void Main()
        {
            Console.WriteLine("Enter Storage account name:");           
            string accountName = Console.ReadLine();

            Console.WriteLine("\nEnter Storage account key:");           
            string accountKey = Console.ReadLine();

            string storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + accountName + ";AccountKey=" + accountKey;
            CloudStorageAccount account = CloudStorageAccount.Parse(storageConnectionString);

            ExecuteChoice(account);
        }

        public static void ExecuteChoice(CloudStorageAccount account)
        {
            Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
            int choice = int.Parse(Console.ReadLine());

            if(choice == 1)
            {
                TransferLocalFileToAzureBlob(account).Wait();
            }
            else if(choice == 2)
            {
                TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
            }
            else if(choice == 3)
            {
                TransferUrlToAzureBlob(account).Wait();
            }
            else if(choice == 4)
            {
                TransferAzureBlobToAzureBlob(account).Wait();
            }
        }

        public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
        {

        }

        public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
        {

        }
    }
}
```

## <a name="transfer-local-file-tooazure-blob"></a>Передача локального файла tooAzure больших двоичных объектов
Добавьте методы hello `GetSourcePath` и `GetBlob` слишком`Program.cs`:

```csharp
public static string GetSourcePath()
{
    Console.WriteLine("\nProvide path for source:");
    string sourcePath = Console.ReadLine();

    return sourcePath;
}

public static CloudBlockBlob GetBlob(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    Console.WriteLine("\nProvide name of new Blob:");
    string blobName = Console.ReadLine();
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    return blob;
}
```

Изменение hello `TransferLocalFileToAzureBlob` метод:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    await TransferManager.UploadAsync(localFilePath, blob);
    Console.WriteLine("\nTransfer operation complete.");
    ExecuteChoice(account);
}
```

Этот код запрашивает hello путь tooa локальный файл, имя hello нового или существующего контейнера и имя hello новый большой двоичный объект. Hello `TransferManager.UploadAsync` метод выполняет передачи hello, используя эту информацию. 

Попаданий `F5` toorun приложения. Можно проверить, произошло этой отправки hello, просмотрев вашей учетной записи хранилища с hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

## <a name="set-number-of-parallel-operations"></a>Настройка количества параллельных операций
Прекрасная возможность предлагаемых hello библиотеки перемещения данных является возможность hello tooset номер hello передачи пропускная способность hello tooincrease параллельных операций. По умолчанию hello библиотеки перемещения данных задает hello число параллельных операций too8 * hello число ядер в компьютере. 

Имейте в виду, что много параллельных операций в среде с низкой пропускной способностью может переполнить hello сетевое подключение и фактически предотвратить операций полностью завершить. Вам потребуется tooexperiment с помощью этого параметра toodetermine что работает лучше всего на основе на пропускной способности сети. 

Давайте добавим код, который позволяет нам tooset hello число параллельных операций. Также добавим код, время, время, необходимое для передачи toocomplete hello.

Добавить `SetNumberOfParallelOperations` метод слишком`Program.cs`:

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

Изменение hello `ExecuteChoice` toouse метод `SetNumberOfParallelOperations`:

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
    int choice = int.Parse(Console.ReadLine());

    SetNumberOfParallelOperations();

    if(choice == 1)
    {
        TransferLocalFileToAzureBlob(account).Wait();
    }
    else if(choice == 2)
    {
        TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
    }
    else if(choice == 3)
    {
        TransferUrlToAzureBlob(account).Wait();
    }
    else if(choice == 4)
    {
        TransferAzureBlobToAzureBlob(account).Wait();
    }
}
```

Изменение hello `TransferLocalFileToAzureBlob` toouse метода таймера:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="track-transfer-progress"></a>Отслеживание выполнения передачи
Отлично подходит знать, сколько времени прошло tootransfer наших данных. Тем не менее, могут toosee о ходе hello нашей передачи *во время* даже лучше было бы использовать hello операции передачи. tooachieve этого сценария необходимо toocreate `TransferContext` объекта. Hello `TransferContext` объекта бывают двух видов: `SingleTransferContext` и `DirectoryTransferContext`. Бывшая Hello применяется для передачи один файл (который является, что мы делаем сейчас) и последний hello применяется для передачи каталог файлов (которые мы добавляем более поздней версии).

Добавьте методы hello `GetSingleTransferContext` и `GetDirectoryTransferContext` слишком`Program.cs`: 

```csharp
public static SingleTransferContext GetSingleTransferContext(TransferCheckpoint checkpoint)
{
    SingleTransferContext context = new SingleTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}

public static DirectoryTransferContext GetDirectoryTransferContext(TransferCheckpoint checkpoint)
{
    DirectoryTransferContext context = new DirectoryTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}
```

Изменение hello `TransferLocalFileToAzureBlob` toouse метод `GetSingleTransferContext`:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint);
    Console.WriteLine("\nTransfer started...\n");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob, null, context);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="resume-a-canceled-transfer"></a>Возобновление отмененной передачи
Другой удобный функцию, предоставляемую hello библиотеки перемещения данных — возможность hello tooresume отменена передача. Давайте добавим код, который позволяет нам передачи hello tootemporarily "Отмена", введя `c`, а затем продолжить передачу hello 3 секунды.

Измените `TransferLocalFileToAzureBlob`.

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.UploadAsync(localFilePath, blob, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadAsync(localFilePath, blob, null, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

До сих пор наши `checkpoint` всегда задано слишком`null`. Теперь если производится Отмена передачи hello, мы получения последней контрольной точки hello нашей передачи, а затем использования этой новой контрольной точки в наш контекст передачи. 

## <a name="transfer-local-directory-tooazure-blob-directory"></a>Передача каталог больших двоичных объектов tooAzure локальный каталог
Было бы неудовлетворительным, если hello библиотеки перемещения данных можно передать только один файл одновременно. К счастью это не так hello. Hello библиотеки перемещения данных предоставляет возможность tootransfer hello каталог файлов и всех его подкаталогах. Давайте добавим код, который позволяет нам toodo именно это.

Во-первых, добавьте метод hello `GetBlobDirectory` слишком`Program.cs`:

```csharp
public static CloudBlobDirectory GetBlobDirectory(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container. This can be a new or existing Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    CloudBlobDirectory blobDirectory = container.GetDirectoryReference("");

    return blobDirectory;
}
```

Затем измените `TransferLocalDirectoryToAzureBlobDirectory`.

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    UploadDirectoryOptions options = new UploadDirectoryOptions()
    {
        Recursive = true
    };

    try
    {
        task = TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetDirectoryTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Существует ряд различий между этот метод и метод hello для передачи одного файла. Теперь мы используем `TransferManager.UploadDirectoryAsync` и hello `getDirectoryTransferContext` метода, созданную ранее. Кроме того, теперь мы предоставляем `options` значение tooour передачи операция, которая позволяет нам tooindicate, мы хотим tooinclude подкаталогов, в нашем передачи. 

## <a name="copy-file-from-url-tooazure-blob"></a>Скопируйте файл из tooAzure URL-адрес большого двоичного объекта
Теперь добавим код, который позволяет нам toocopy файл из tooan URL-адрес BLOB-объектов Azure. 

Измените `TransferUrlToAzureBlob`.

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Один вариант важные использования для этой функции — при необходимости toomove данные из другой облачной службы (например, AWS) tooAzure. Пока у вас есть URL-адрес, который предоставляет вам доступ к ресурсу toohello, можно легко переместить этот ресурс в BLOB-объектов Azure с помощью hello `TransferManager.CopyAsync` метод. В этом методе также представлен новый логический параметр. Этот параметр слишком`true` указывает, что мы хотим toodo асинхронной серверную копирования. Этот параметр слишком`false` указывает синхронной копии - т hello ресурсов локального компьютера загруженный tooour во-первых, затем отправлены tooAzure больших двоичных объектов. Однако синхронного копирования в данный момент доступна только для копирования из одного tooanother ресурсов хранилища Azure. 

## <a name="transfer-azure-blob-tooazure-blob"></a>Передача больших двоичных объектов Azure tooAzure больших двоичных объектов
Другая функция, предоставляемая однозначно hello библиотеки перемещения данных — toocopy возможность hello из одного tooanother ресурсов хранилища Azure. 

Измените `TransferAzureBlobToAzureBlob`.

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(sourceBlob, destinationBlob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(sourceBlob, destinationBlob, false, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

В этом примере задается hello логического параметра `TransferManager.CopyAsync` слишком`false` tooindicate, что мы хотим toodo синхронного копирования. Это значит, которая hello ресурсов локального компьютера загруженный tooour сначала, то отправлен tooAzure больших двоичных объектов. параметр синхронного копирования Hello — отличный способ tooensure, что операции копирования обеспечивает согласованное скорость. Напротив скорость hello асинхронную копию серверных зависит hello доступную пропускную способность сети на сервере hello, который может меняться. Однако синхронного копирования может создавать копии tooasynchronous исходящих дополнительных затрат по сравнению. Hello рекомендуется toouse синхронного копирования на виртуальной Машине Azure, hello же регионе, что ваш источник учетной записи tooavoid исходящих затраты на хранение.

## <a name="conclusion"></a>Заключение
Приложение для перемещения данных готово. [Hello полный образец кода можно найти в GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app). 

## <a name="next-steps"></a>Дальнейшие действия
В данном руководстве по началу работы мы создали приложение, которое взаимодействует со службой хранилища Azure и работает в Windows, Linux и MacOS. Данное руководство ориентировано на хранилище BLOB-объектов. Тем не менее этот же набор знаний может быть применен tooFile хранилища. toolearn более, извлечь [справочная документация по библиотеке перемещения данных хранилища Azure](https://azure.github.io/azure-storage-net-data-movement).

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]




