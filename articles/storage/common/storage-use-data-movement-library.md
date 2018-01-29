---
title: "Передача данных с использованием библиотеки перемещения данных службы хранилища Microsoft Azure | Документация Майкрософт"
description: "Использование библиотеки перемещения данных для перемещения или копирования данных в большие двоичные объекты и файлы и из них. Копируйте данные в хранилище Azure из локальных файлов, а также внутри учетной записи хранения и из одной такой учетной записи в другую. Легко переносите данные в хранилище Azure."
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
ms.date: 09/27/2017
ms.author: seguler
ms.openlocfilehash: eb96f3697d5369ba96a1b0c491e3eacf09e7aac4
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/02/2018
---
# <a name="transfer-data-with-the-microsoft-azure-storage-data-movement-library"></a>Передача данных с использованием библиотеки перемещения данных службы хранилища Microsoft Azure

## <a name="overview"></a>Обзор
Библиотека перемещения данных службы хранилища Microsoft Azure — это кроссплатформенная библиотека открытого кода, предназначенная для ускорения передачи, скачивания и копирования больших двоичных объектов и файлов в службе хранилища Azure. Эта библиотека является базовой платформой перемещения данных, лежащей в основе [AzCopy](../storage-use-azcopy.md). Библиотека перемещения данных предоставляет удобные методы, которые недоступны в нашей традиционной [клиентской библиотеке службы хранилища Azure для .NET](../blobs/storage-dotnet-how-to-use-blobs.md). Сюда входит возможность задать количество параллельных операций, отслеживание выполнения передачи, удобное возобновление отмененной передачи и многое другое.  

Эта библиотека также использует .NET Core, а это означает, что ее можно применять при создании приложений .NET для Windows, Linux и MacOS. Дополнительные сведения о .NET Core см. [документации по .NET Core](https://dotnet.github.io/). Эта библиотека также подходит для традиционных приложений .NET Framework для Windows. 

В этом документе показано, как создать консольное приложение .NET Core, который выполняется в Windows, Linux и macOS и выполняет следующие сценарии:

- Передача файлов и каталогов в хранилище BLOB-объектов.
- Определение количества параллельных операций при передаче данных.
- Отслеживание выполнения передачи данных.
- Возобновление отмененной передачи данных. 
- Копирование файла по URL-адресу в хранилище BLOB-объектов. 
- Копирование из хранилища BLOB-объектов в хранилище BLOB-объектов.

**Необходимые компоненты:**

* [Visual Studio Code](https://code.visualstudio.com/)
* [учетная запись хранения Azure](storage-create-storage-account.md#create-a-storage-account)

> [!NOTE]
> Для работы с этим руководством предполагается, что у вас есть общее представление о [службе хранилища Azure](https://azure.microsoft.com/services/storage/). Если вы еще не работали со службой хранилища Azure, ознакомьтесь со статьей [Введение в хранилище Microsoft Azure](storage-introduction.md). Что еще более важно, для использования библиотеки перемещения данных потребуется [создать учетную запись хранения](storage-create-storage-account.md#create-a-storage-account).
> 
> 

## <a name="setup"></a>Настройка  

1. Ознакомьтесь с [руководством по установке .NET Core](https://www.microsoft.com/net/core), чтобы установить .NET Core. При выборе среды щелкните параметр командной строки. 
2. В командной строке создайте каталог для проекта. Перейдите в этот каталог и введите `dotnet new console -o <sample-project-name>` для создания проекта консольного приложения C#.
3. Откройте этот каталог в Visual Studio Code. Этот шаг можно быстро выполнить, введя в командной строке `code .` в Windows.  
4. Установите [расширение C# ](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) из Marketplace для Visual Studio Code. Перезапустите Visual Studio Code. 
5. На этом этапе должны отобразиться два запроса. Первый — для добавления необходимых ресурсов для сборки. Щелкните "Да". Второй запрос — для восстановления неразрешенных зависимостей. Щелкните "Восстановить".
6. Измените `launch.json` в `.vscode`, чтобы использовать внешний терминал в качестве консоли. Этот параметр следует читать как ` "console": "externalTerminal"`.
7. Visual Studio Code позволяет отлаживать приложения .NET Core. Нажмите клавишу `F5`, чтобы запустить приложение и проверить настройки. Вы должны увидеть текст "Hello World!" в консоли. 

## <a name="add-data-movement-library-to-your-project"></a>Добавление в проект библиотеки перемещения данных

1. Добавьте последнюю версию библиотеки перемещения данных в раздел `dependencies` файла `<project-name>.csproj`. На момент написания статьи это версия `"Microsoft.Azure.Storage.DataMovement": "0.6.2"`. 
2. Должен появиться запрос на восстановление проекта. Нажмите кнопку "Восстановить". Можно также восстановить проект из командной строки, введя команду `dotnet restore` в корневом каталоге проекта.

Измените `<project-name>.csproj`.

    <Project Sdk="Microsoft.NET.Sdk">

        <PropertyGroup>
            <OutputType>Exe</OutputType>
            <TargetFramework>netcoreapp2.0</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
            <PackageReference Include="Microsoft.Azure.Storage.DataMovement" Version="0.6.2" />
            </ItemGroup>
        </Project>

## <a name="set-up-the-skeleton-of-your-application"></a>Настройка схемы приложения
Первое, что мы сделаем — настроим схему кода приложения. Этот код запрашивает имя и ключ учетной записи хранения и использует эти учетные данные для создания объекта `CloudStorageAccount`. Этот объект используется для взаимодействия с нашей учетной записи хранения во всех сценариях передачи данных. Код также предлагает выбрать тип операции передачи, которую нужно выполнить. 

Измените `Program.cs`.

```csharp
using System;
using System.Threading;
using System.Threading.Tasks;
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
            Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
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

## <a name="transfer-local-file-to-azure-blob"></a>Передача локального файла в большой двоичный объект Azure
Добавьте методы `GetSourcePath` и `GetBlob` в `Program.cs`.

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

Измените метод `TransferLocalFileToAzureBlob`.

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

Этот код запрашивает путь к локальному файлу, имя нового или существующего контейнера и имя нового большого двоичного объекта. На основе этой информации метод `TransferManager.UploadAsync` выполняет передачу. 

Нажмите клавишу `F5`, чтобы запустить приложение. Чтобы проверить, выполнена ли передача, можно просмотреть свою учетную запись хранения в [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

## <a name="set-number-of-parallel-operations"></a>Настройка количества параллельных операций
Отличной функцией, предоставляемой библиотекой перемещения данных, является возможность задать количество параллельных операций, чтобы увеличить пропускную способность передачи данных. По умолчанию библиотека перемещения данных задает количество параллельных операций, равное восьмикратному числу ядер в компьютере. 

Следует помнить, что большое количество одновременных операций в среде с низкой пропускной способностью может перегрузить сетевое подключение и фактически помешать полному завершению операций. Вам потребуется поэкспериментировать с этим параметром, чтобы определить, что лучше всего подходит для имеющейся пропускной способности сети. 

Давайте добавим код, который позволяет задать число параллельных операций. Также добавим код, определяющий допустимую длительность передачи.

Добавьте `SetNumberOfParallelOperations` в метод `Program.cs`.

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like to use?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

Измените метод `ExecuteChoice`, чтобы использовать `SetNumberOfParallelOperations`.

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
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

Измените метод `TransferLocalFileToAzureBlob`, чтобы использовать таймер.

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
Хорошо знать, сколько времени займет передача данных. Но еще лучше — следить за ходом передачи *во время* ее выполнения. Чтобы получить такую возможность, необходимо создать объект `TransferContext`. Объект `TransferContext` бывает двух типов: `SingleTransferContext` и `DirectoryTransferContext`. Первый — для передачи отдельного файла (как раз то, что мы делаем), а второй — для передачи каталога с файлами (которые мы добавим позже).

Добавьте методы `GetSingleTransferContext` и `GetDirectoryTransferContext` в `Program.cs`. 

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

Измените метод `TransferLocalFileToAzureBlob`, чтобы использовать `GetSingleTransferContext`.

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
Еще одной удобной функцией, предоставляемой библиотекой перемещения данных, является возможность возобновить отмененные передачи. Давайте добавим код, позволяющий временно отменить передачу, введя `c`, а через 3 секунды возобновить ее.

Измените `TransferLocalFileToAzureBlob`.

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

До сих пор параметр `checkpoint` всегда имел значение `null`. Теперь, если мы отменим передачу, то получим ее последнюю контрольную точку, а затем используем эту новую контрольную точку в контексте передачи. 

## <a name="transfer-local-directory-to-azure-blob-directory"></a>Передача локального каталога в каталог больших двоичных объектов Azure
Было бы печально, если бы библиотека перемещения данных могла передавать только отдельные файлы. К счастью, это не так. Библиотека перемещения данных дает возможность передать каталог с файлами и все его подкаталоги. Давайте добавим код, позволяющий сделать это.

Сначала добавьте метод `GetBlobDirectory` в `Program.cs`.

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
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

Существует ряд различий между этим методом и методом для передачи отдельного файла. Сейчас мы используем методы `TransferManager.UploadDirectoryAsync` и `getDirectoryTransferContext`, созданные ранее. Кроме того, мы задаем значение `options` для нашей операции передачи. Это позволяет указать, что в нее нужно включить подкаталоги. 

## <a name="copy-file-from-url-to-azure-blob"></a>Копирование файла по URL-адресу в большой двоичный объект Azure
Теперь давайте добавим код, который позволяет скопировать файл по URL-адресу в большой двоичный объект Azure. 

Измените `TransferUrlToAzureBlob`.

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

Одним из важных применений этой функции является перемещение данных из другой облачной службы (например, AWS) в Azure. Если у вас есть URL-адрес, который предоставляет доступ к ресурсу, то этот ресурс можно легко переместить в большие двоичные объекты Azure, воспользовавшись методом `TransferManager.CopyAsync`. В этом методе также представлен новый логический параметр. Если присвоить ему значение `true`, то будет выполнено асинхронное копирование на стороне сервера. Если присвоить ему значение `false`, то будет выполнено синхронное копирование, то есть ресурс сначала скачивается на локальный компьютер, а затем передается в большой двоичный объект Azure. В данный момент синхронное копирование доступно только для копирования между ресурсами службы хранилища Azure. 

## <a name="transfer-azure-blob-to-azure-blob"></a>Передача большого двоичного объекта Azure в большой двоичный объект Azure
Еще одна функция, предоставляемая исключительно библиотекой перемещения данных, — возможность копирования данных между ресурсами службы хранилища Azure. 

Измените `TransferAzureBlobToAzureBlob`.

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

В этом примере мы присваиваем логическому параметру в `TransferManager.CopyAsync` значение `false`, чтобы указать, что нам нужно выполнить синхронное копирование. Это означает, что ресурс сначала скачивается на локальный компьютер, а затем передается в большой двоичный объект Azure. Синхронное копирование — отличный способ обеспечить постоянную скорость копирования. Напротив, скорость асинхронного копирования на стороне сервера зависит от доступной пропускной способности на сервере, которая может меняться. Однако синхронное копирование может повлечь дополнительные затраты на исходящий трафик по сравнению с асинхронным копированием. Во избежание таких затрат мы советуем использовать синхронное копирование в виртуальных машинах Azure, которые находятся в одном регионе с вашей учетной записью хранения.

## <a name="conclusion"></a>Заключение
Приложение для перемещения данных готово. [Полный пример кода можно найти на сайте GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app). 

## <a name="next-steps"></a>Дальнейшие действия
В данном руководстве по началу работы мы создали приложение, которое взаимодействует со службой хранилища Azure и работает в Windows, Linux и MacOS. Данное руководство ориентировано на хранилище BLOB-объектов. Тем не менее полученные знания можно применить и к хранилищу файлов. Чтобы узнать больше, ознакомьтесь со [справочной документацией по библиотеке перемещения данных службы хранилища Azure](https://azure.github.io/azure-storage-net-data-movement).

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]




