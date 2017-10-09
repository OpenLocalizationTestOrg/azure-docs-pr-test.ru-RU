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
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a><span data-ttu-id="b89e4-105">Передача данных с помощью hello библиотека перемещения данных для хранилища Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b89e4-105">Transfer Data with hello Microsoft Azure Storage Data Movement Library</span></span>

## <a name="overview"></a><span data-ttu-id="b89e4-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="b89e4-106">Overview</span></span>
<span data-ttu-id="b89e4-107">Hello библиотека перемещения данных для хранилища Microsoft Azure — это библиотека кросс платформенных открытым исходным кодом, предназначенный для высокопроизводительных передача, загрузка и копирование файлов и больших двоичных объектах хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b89e4-107">hello Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span></span> <span data-ttu-id="b89e4-108">Эта библиотека является перемещение hello core data framework, лежащих в основе [AzCopy](../storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="b89e4-108">This library is hello core data movement framework that powers [AzCopy](../storage-use-azcopy.md).</span></span> <span data-ttu-id="b89e4-109">Hello библиотеки перемещения данных предоставляет удобные методы, недоступные в нашей традиционной [клиентской библиотеки хранилища Azure .NET](../blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="b89e4-109">hello Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](../blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="b89e4-110">Сюда входят hello возможность tooset hello число параллельных операций, отслеживание хода выполнения передачи, легко Возобновить отмененные передачи и многое другое.</span><span class="sxs-lookup"><span data-stu-id="b89e4-110">This includes hello ability tooset hello number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span></span>  

<span data-ttu-id="b89e4-111">Эта библиотека также использует .NET Core, а это означает, что ее можно применять при создании приложений .NET для Windows, Linux и MacOS.</span><span class="sxs-lookup"><span data-stu-id="b89e4-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span></span> <span data-ttu-id="b89e4-112">toolearn Дополнительные сведения о .NET Core ссылаться toohello [документации .NET Core](https://dotnet.github.io/).</span><span class="sxs-lookup"><span data-stu-id="b89e4-112">toolearn more about .NET Core, refer toohello [.NET Core documentation](https://dotnet.github.io/).</span></span> <span data-ttu-id="b89e4-113">Эта библиотека также подходит для традиционных приложений .NET Framework для Windows.</span><span class="sxs-lookup"><span data-stu-id="b89e4-113">This library also works for traditional .NET Framework apps for Windows.</span></span> 

<span data-ttu-id="b89e4-114">В этом документе показано, как .NET Core toocreate консольное приложение, выполняется в Windows, Linux и macOS и выполняет hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="b89e4-114">This document demonstrates how toocreate a .NET Core console application that that runs on Windows, Linux, and macOS and performs hello following scenarios:</span></span>

- <span data-ttu-id="b89e4-115">Передача файлов и каталогов tooBlob хранилища.</span><span class="sxs-lookup"><span data-stu-id="b89e4-115">Upload files and directories tooBlob Storage.</span></span>
- <span data-ttu-id="b89e4-116">Определите hello число параллельных операций, при передаче данных.</span><span class="sxs-lookup"><span data-stu-id="b89e4-116">Define hello number of parallel operations when transferring data.</span></span>
- <span data-ttu-id="b89e4-117">Отслеживание выполнения передачи данных.</span><span class="sxs-lookup"><span data-stu-id="b89e4-117">Track data transfer progress.</span></span>
- <span data-ttu-id="b89e4-118">Возобновление отмененной передачи данных.</span><span class="sxs-lookup"><span data-stu-id="b89e4-118">Resume canceled data transfer.</span></span> 
- <span data-ttu-id="b89e4-119">Скопируйте файл из tooBlob URL-адрес хранилища.</span><span class="sxs-lookup"><span data-stu-id="b89e4-119">Copy file from URL tooBlob Storage.</span></span> 
- <span data-ttu-id="b89e4-120">Скопируйте из tooBlob хранилища больших двоичных объектов хранилища.</span><span class="sxs-lookup"><span data-stu-id="b89e4-120">Copy from Blob Storage tooBlob Storage.</span></span>

<span data-ttu-id="b89e4-121">**Необходимые компоненты:**</span><span class="sxs-lookup"><span data-stu-id="b89e4-121">**What you need:**</span></span>

* [<span data-ttu-id="b89e4-122">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="b89e4-122">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="b89e4-123">[учетная запись хранения Azure](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="b89e4-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

> [!NOTE]
> <span data-ttu-id="b89e4-124">Для работы с этим руководством предполагается, что у вас есть общее представление о [службе хранилища Azure](https://azure.microsoft.com/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="b89e4-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="b89e4-125">Если нет, чтение hello [tooAzure введение хранилища](storage-introduction.md) полезно документации.</span><span class="sxs-lookup"><span data-stu-id="b89e4-125">If not, reading hello [Introduction tooAzure Storage](storage-introduction.md) documentation is helpful.</span></span> <span data-ttu-id="b89e4-126">Самое главное, требуется слишком[создать учетную запись хранилища](storage-create-storage-account.md#create-a-storage-account) toostart с помощью hello библиотеки перемещения данных.</span><span class="sxs-lookup"><span data-stu-id="b89e4-126">Most importantly, you need too[create a Storage account](storage-create-storage-account.md#create-a-storage-account) toostart using hello Data Movement Library.</span></span>
> 
> 

## <a name="setup"></a><span data-ttu-id="b89e4-127">Настройка</span><span class="sxs-lookup"><span data-stu-id="b89e4-127">Setup</span></span>  

1. <span data-ttu-id="b89e4-128">Посетите hello [руководство по установке .NET Core](https://www.microsoft.com/net/core) tooinstall .NET Core.</span><span class="sxs-lookup"><span data-stu-id="b89e4-128">Visit hello [.NET Core Installation Guide](https://www.microsoft.com/net/core) tooinstall .NET Core.</span></span> <span data-ttu-id="b89e4-129">При выборе среды, выберите параметр командной строки hello.</span><span class="sxs-lookup"><span data-stu-id="b89e4-129">When selecting your environment, choose hello command-line option.</span></span> 
2. <span data-ttu-id="b89e4-130">Из командной строки hello создайте каталог для проекта.</span><span class="sxs-lookup"><span data-stu-id="b89e4-130">From hello command line, create a directory for your project.</span></span> <span data-ttu-id="b89e4-131">Перейдите в этот каталог, затем введите `dotnet new` проект консольного toocreate на языке C#.</span><span class="sxs-lookup"><span data-stu-id="b89e4-131">Navigate into this directory, then type `dotnet new` toocreate a C# console project.</span></span>
3. <span data-ttu-id="b89e4-132">Откройте этот каталог в Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="b89e4-132">Open this directory in Visual Studio Code.</span></span> <span data-ttu-id="b89e4-133">Этот шаг можно быстро сделать с помощью hello командной строки, введя `code .`.</span><span class="sxs-lookup"><span data-stu-id="b89e4-133">This step can be quickly done via hello command line by typing `code .`.</span></span>  
4. <span data-ttu-id="b89e4-134">Установка hello [C# расширения](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) из Visual Studio Marketplace кода hello.</span><span class="sxs-lookup"><span data-stu-id="b89e4-134">Install hello [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from hello Visual Studio Code Marketplace.</span></span> <span data-ttu-id="b89e4-135">Перезапустите Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="b89e4-135">Restart Visual Studio Code.</span></span> 
5. <span data-ttu-id="b89e4-136">На этом этапе должны отобразиться два запроса.</span><span class="sxs-lookup"><span data-stu-id="b89e4-136">At this point, you should see two prompts.</span></span> <span data-ttu-id="b89e4-137">Один позволяет добавлять «toobuild необходимых средств и отладки».</span><span class="sxs-lookup"><span data-stu-id="b89e4-137">One is for adding "required assets toobuild and debug."</span></span> <span data-ttu-id="b89e4-138">Щелкните "Да".</span><span class="sxs-lookup"><span data-stu-id="b89e4-138">Click "yes."</span></span> <span data-ttu-id="b89e4-139">Второй запрос — для восстановления неразрешенных зависимостей.</span><span class="sxs-lookup"><span data-stu-id="b89e4-139">Another prompt is for restoring unresolved dependencies.</span></span> <span data-ttu-id="b89e4-140">Щелкните "Восстановить".</span><span class="sxs-lookup"><span data-stu-id="b89e4-140">Click "restore."</span></span>
6. <span data-ttu-id="b89e4-141">Приложение теперь должен содержать `launch.json` файл в папке hello `.vscode` каталога.</span><span class="sxs-lookup"><span data-stu-id="b89e4-141">Your application should now contain a `launch.json` file under hello `.vscode` directory.</span></span> <span data-ttu-id="b89e4-142">В этот файл, измените hello `externalConsole` значение слишком`true`.</span><span class="sxs-lookup"><span data-stu-id="b89e4-142">In this file, change hello `externalConsole` value too`true`.</span></span>
7. <span data-ttu-id="b89e4-143">Код Visual Studio позволяет toodebug приложений .NET Core.</span><span class="sxs-lookup"><span data-stu-id="b89e4-143">Visual Studio Code allows you toodebug .NET Core applications.</span></span> <span data-ttu-id="b89e4-144">Попаданий `F5` toorun приложение и проверьте работоспособность настройки программы установки.</span><span class="sxs-lookup"><span data-stu-id="b89e4-144">Hit `F5` toorun your application and verify that your setup is working.</span></span> <span data-ttu-id="b89e4-145">Вы должны увидеть текст "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="b89e4-145">You should see "Hello World!"</span></span> <span data-ttu-id="b89e4-146">Печать toohello консоли.</span><span class="sxs-lookup"><span data-stu-id="b89e4-146">printed toohello console.</span></span> 

## <a name="add-data-movement-library-tooyour-project"></a><span data-ttu-id="b89e4-147">Добавьте проект библиотеки перемещения данных tooyour</span><span class="sxs-lookup"><span data-stu-id="b89e4-147">Add Data Movement Library tooyour project</span></span>

1. <span data-ttu-id="b89e4-148">Добавить hello последнюю версию библиотеки перемещения данных toohello hello `dependencies` части вашего `project.json` файла.</span><span class="sxs-lookup"><span data-stu-id="b89e4-148">Add hello latest version of hello Data Movement Library toohello `dependencies` section of your `project.json` file.</span></span> <span data-ttu-id="b89e4-149">На момент написания статьи hello будет этой версии`"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span><span class="sxs-lookup"><span data-stu-id="b89e4-149">At hello time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span></span> 
2. <span data-ttu-id="b89e4-150">Добавить `"portable-net45+win8"` toohello `imports` раздела.</span><span class="sxs-lookup"><span data-stu-id="b89e4-150">Add `"portable-net45+win8"` toohello `imports` section.</span></span> 
3. <span data-ttu-id="b89e4-151">Запрос должен отображать toorestore проекта.</span><span class="sxs-lookup"><span data-stu-id="b89e4-151">A prompt should display toorestore your project.</span></span> <span data-ttu-id="b89e4-152">Нажмите кнопку «Восстановить» hello.</span><span class="sxs-lookup"><span data-stu-id="b89e4-152">Click hello "restore" button.</span></span> <span data-ttu-id="b89e4-153">Можно также восстановить проект из hello командной строки, введя команду hello `dotnet restore` hello корневом каталоге проекта.</span><span class="sxs-lookup"><span data-stu-id="b89e4-153">You can also restore your project from hello command line by typing hello command `dotnet restore` in hello root of your project directory.</span></span>

<span data-ttu-id="b89e4-154">Измените `project.json`.</span><span class="sxs-lookup"><span data-stu-id="b89e4-154">Modify `project.json`:</span></span>

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

## <a name="set-up-hello-skeleton-of-your-application"></a><span data-ttu-id="b89e4-155">Настроить основу hello объекта приложения</span><span class="sxs-lookup"><span data-stu-id="b89e4-155">Set up hello skeleton of your application</span></span>
<span data-ttu-id="b89e4-156">Hello первое, что мы делаем имеет значение «каркасного» hello, код приложения.</span><span class="sxs-lookup"><span data-stu-id="b89e4-156">hello first thing we do is set up hello "skeleton" code of our application.</span></span> <span data-ttu-id="b89e4-157">Этот код запрашивает ключ учетной записи и имени учетной записи хранения и использует эти учетные данные toocreate `CloudStorageAccount` объекта.</span><span class="sxs-lookup"><span data-stu-id="b89e4-157">This code prompts us for a Storage account name and account key and uses those credentials toocreate a `CloudStorageAccount` object.</span></span> <span data-ttu-id="b89e4-158">Этот объект является используется toointeract с нашей учетной записи хранения во всех сценариях передачи.</span><span class="sxs-lookup"><span data-stu-id="b89e4-158">This object is used toointeract with our Storage account in all transfer scenarios.</span></span> <span data-ttu-id="b89e4-159">Hello код также отображает запрос нам toochoose hello тип операции передачи, мы хотели бы tooexecute.</span><span class="sxs-lookup"><span data-stu-id="b89e4-159">hello code also prompts us toochoose hello type of transfer operation we would like tooexecute.</span></span> 

<span data-ttu-id="b89e4-160">Измените `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="b89e4-160">Modify `Program.cs`:</span></span>

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

## <a name="transfer-local-file-tooazure-blob"></a><span data-ttu-id="b89e4-161">Передача локального файла tooAzure больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="b89e4-161">Transfer local file tooAzure Blob</span></span>
<span data-ttu-id="b89e4-162">Добавьте методы hello `GetSourcePath` и `GetBlob` слишком`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="b89e4-162">Add hello methods `GetSourcePath` and `GetBlob` too`Program.cs`:</span></span>

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

<span data-ttu-id="b89e4-163">Изменение hello `TransferLocalFileToAzureBlob` метод:</span><span class="sxs-lookup"><span data-stu-id="b89e4-163">Modify hello `TransferLocalFileToAzureBlob` method:</span></span>

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

<span data-ttu-id="b89e4-164">Этот код запрашивает hello путь tooa локальный файл, имя hello нового или существующего контейнера и имя hello новый большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="b89e4-164">This code prompts us for hello path tooa local file, hello name of a new or existing container, and hello name of a new blob.</span></span> <span data-ttu-id="b89e4-165">Hello `TransferManager.UploadAsync` метод выполняет передачи hello, используя эту информацию.</span><span class="sxs-lookup"><span data-stu-id="b89e4-165">hello `TransferManager.UploadAsync` method performs hello upload using this information.</span></span> 

<span data-ttu-id="b89e4-166">Попаданий `F5` toorun приложения.</span><span class="sxs-lookup"><span data-stu-id="b89e4-166">Hit `F5` toorun your application.</span></span> <span data-ttu-id="b89e4-167">Можно проверить, произошло этой отправки hello, просмотрев вашей учетной записи хранилища с hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="b89e4-167">You can verify that hello upload occurred by viewing your Storage account with hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="set-number-of-parallel-operations"></a><span data-ttu-id="b89e4-168">Настройка количества параллельных операций</span><span class="sxs-lookup"><span data-stu-id="b89e4-168">Set number of parallel operations</span></span>
<span data-ttu-id="b89e4-169">Прекрасная возможность предлагаемых hello библиотеки перемещения данных является возможность hello tooset номер hello передачи пропускная способность hello tooincrease параллельных операций.</span><span class="sxs-lookup"><span data-stu-id="b89e4-169">A great feature offered by hello Data Movement Library is hello ability tooset hello number of parallel operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="b89e4-170">По умолчанию hello библиотеки перемещения данных задает hello число параллельных операций too8 * hello число ядер в компьютере.</span><span class="sxs-lookup"><span data-stu-id="b89e4-170">By default, hello Data Movement Library sets hello number of parallel operations too8 * hello number of cores on your machine.</span></span> 

<span data-ttu-id="b89e4-171">Имейте в виду, что много параллельных операций в среде с низкой пропускной способностью может переполнить hello сетевое подключение и фактически предотвратить операций полностью завершить.</span><span class="sxs-lookup"><span data-stu-id="b89e4-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm hello network connection and actually prevent operations from fully completing.</span></span> <span data-ttu-id="b89e4-172">Вам потребуется tooexperiment с помощью этого параметра toodetermine что работает лучше всего на основе на пропускной способности сети.</span><span class="sxs-lookup"><span data-stu-id="b89e4-172">You'll need tooexperiment with this setting toodetermine what works best based on your available network bandwidth.</span></span> 

<span data-ttu-id="b89e4-173">Давайте добавим код, который позволяет нам tooset hello число параллельных операций.</span><span class="sxs-lookup"><span data-stu-id="b89e4-173">Let's add some code that allows us tooset hello number of parallel operations.</span></span> <span data-ttu-id="b89e4-174">Также добавим код, время, время, необходимое для передачи toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="b89e4-174">Let's also add code that times how long it takes for hello transfer toocomplete.</span></span>

<span data-ttu-id="b89e4-175">Добавить `SetNumberOfParallelOperations` метод слишком`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="b89e4-175">Add a `SetNumberOfParallelOperations` method too`Program.cs`:</span></span>

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

<span data-ttu-id="b89e4-176">Изменение hello `ExecuteChoice` toouse метод `SetNumberOfParallelOperations`:</span><span class="sxs-lookup"><span data-stu-id="b89e4-176">Modify hello `ExecuteChoice` method toouse `SetNumberOfParallelOperations`:</span></span>

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

<span data-ttu-id="b89e4-177">Изменение hello `TransferLocalFileToAzureBlob` toouse метода таймера:</span><span class="sxs-lookup"><span data-stu-id="b89e4-177">Modify hello `TransferLocalFileToAzureBlob` method toouse a timer:</span></span>

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

## <a name="track-transfer-progress"></a><span data-ttu-id="b89e4-178">Отслеживание выполнения передачи</span><span class="sxs-lookup"><span data-stu-id="b89e4-178">Track transfer progress</span></span>
<span data-ttu-id="b89e4-179">Отлично подходит знать, сколько времени прошло tootransfer наших данных.</span><span class="sxs-lookup"><span data-stu-id="b89e4-179">Knowing how long it took for our data tootransfer is great.</span></span> <span data-ttu-id="b89e4-180">Тем не менее, могут toosee о ходе hello нашей передачи *во время* даже лучше было бы использовать hello операции передачи.</span><span class="sxs-lookup"><span data-stu-id="b89e4-180">However, being able toosee hello progress of our transfer *during* hello transfer operation would be even better.</span></span> <span data-ttu-id="b89e4-181">tooachieve этого сценария необходимо toocreate `TransferContext` объекта.</span><span class="sxs-lookup"><span data-stu-id="b89e4-181">tooachieve this scenario, we need toocreate a `TransferContext` object.</span></span> <span data-ttu-id="b89e4-182">Hello `TransferContext` объекта бывают двух видов: `SingleTransferContext` и `DirectoryTransferContext`.</span><span class="sxs-lookup"><span data-stu-id="b89e4-182">hello `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span></span> <span data-ttu-id="b89e4-183">Бывшая Hello применяется для передачи один файл (который является, что мы делаем сейчас) и последний hello применяется для передачи каталог файлов (которые мы добавляем более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="b89e4-183">hello former is for transferring a single file (which is what we're doing now) and hello latter is for transferring a directory of files (which we are adding later).</span></span>

<span data-ttu-id="b89e4-184">Добавьте методы hello `GetSingleTransferContext` и `GetDirectoryTransferContext` слишком`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="b89e4-184">Add hello methods `GetSingleTransferContext` and `GetDirectoryTransferContext` too`Program.cs`:</span></span> 

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

<span data-ttu-id="b89e4-185">Изменение hello `TransferLocalFileToAzureBlob` toouse метод `GetSingleTransferContext`:</span><span class="sxs-lookup"><span data-stu-id="b89e4-185">Modify hello `TransferLocalFileToAzureBlob` method toouse `GetSingleTransferContext`:</span></span>

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

## <a name="resume-a-canceled-transfer"></a><span data-ttu-id="b89e4-186">Возобновление отмененной передачи</span><span class="sxs-lookup"><span data-stu-id="b89e4-186">Resume a canceled transfer</span></span>
<span data-ttu-id="b89e4-187">Другой удобный функцию, предоставляемую hello библиотеки перемещения данных — возможность hello tooresume отменена передача.</span><span class="sxs-lookup"><span data-stu-id="b89e4-187">Another convenient feature offered by hello Data Movement Library is hello ability tooresume a canceled transfer.</span></span> <span data-ttu-id="b89e4-188">Давайте добавим код, который позволяет нам передачи hello tootemporarily "Отмена", введя `c`, а затем продолжить передачу hello 3 секунды.</span><span class="sxs-lookup"><span data-stu-id="b89e4-188">Let's add some code that allows us tootemporarily cancel hello transfer by typing `c`, and then resume hello transfer 3 seconds later.</span></span>

<span data-ttu-id="b89e4-189">Измените `TransferLocalFileToAzureBlob`.</span><span class="sxs-lookup"><span data-stu-id="b89e4-189">Modify `TransferLocalFileToAzureBlob`:</span></span>

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

<span data-ttu-id="b89e4-190">До сих пор наши `checkpoint` всегда задано слишком`null`.</span><span class="sxs-lookup"><span data-stu-id="b89e4-190">Up until now, our `checkpoint` value has always been set too`null`.</span></span> <span data-ttu-id="b89e4-191">Теперь если производится Отмена передачи hello, мы получения последней контрольной точки hello нашей передачи, а затем использования этой новой контрольной точки в наш контекст передачи.</span><span class="sxs-lookup"><span data-stu-id="b89e4-191">Now, if we cancel hello transfer, we retrieve hello last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span></span> 

## <a name="transfer-local-directory-tooazure-blob-directory"></a><span data-ttu-id="b89e4-192">Передача каталог больших двоичных объектов tooAzure локальный каталог</span><span class="sxs-lookup"><span data-stu-id="b89e4-192">Transfer local directory tooAzure Blob directory</span></span>
<span data-ttu-id="b89e4-193">Было бы неудовлетворительным, если hello библиотеки перемещения данных можно передать только один файл одновременно.</span><span class="sxs-lookup"><span data-stu-id="b89e4-193">It would be disappointing if hello Data Movement Library could only transfer one file at a time.</span></span> <span data-ttu-id="b89e4-194">К счастью это не так hello.</span><span class="sxs-lookup"><span data-stu-id="b89e4-194">Luckily, this is not hello case.</span></span> <span data-ttu-id="b89e4-195">Hello библиотеки перемещения данных предоставляет возможность tootransfer hello каталог файлов и всех его подкаталогах.</span><span class="sxs-lookup"><span data-stu-id="b89e4-195">hello Data Movement Library provides hello ability tootransfer a directory of files and all of its subdirectories.</span></span> <span data-ttu-id="b89e4-196">Давайте добавим код, который позволяет нам toodo именно это.</span><span class="sxs-lookup"><span data-stu-id="b89e4-196">Let's add some code that allows us toodo just that.</span></span>

<span data-ttu-id="b89e4-197">Во-первых, добавьте метод hello `GetBlobDirectory` слишком`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="b89e4-197">First, add hello method `GetBlobDirectory` too`Program.cs`:</span></span>

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

<span data-ttu-id="b89e4-198">Затем измените `TransferLocalDirectoryToAzureBlobDirectory`.</span><span class="sxs-lookup"><span data-stu-id="b89e4-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span></span>

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

<span data-ttu-id="b89e4-199">Существует ряд различий между этот метод и метод hello для передачи одного файла.</span><span class="sxs-lookup"><span data-stu-id="b89e4-199">There are a few differences between this method and hello method for uploading a single file.</span></span> <span data-ttu-id="b89e4-200">Теперь мы используем `TransferManager.UploadDirectoryAsync` и hello `getDirectoryTransferContext` метода, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="b89e4-200">We're now using `TransferManager.UploadDirectoryAsync` and hello `getDirectoryTransferContext` method we created earlier.</span></span> <span data-ttu-id="b89e4-201">Кроме того, теперь мы предоставляем `options` значение tooour передачи операция, которая позволяет нам tooindicate, мы хотим tooinclude подкаталогов, в нашем передачи.</span><span class="sxs-lookup"><span data-stu-id="b89e4-201">In addition, we now provide an `options` value tooour upload operation, which allows us tooindicate that we want tooinclude subdirectories in our upload.</span></span> 

## <a name="copy-file-from-url-tooazure-blob"></a><span data-ttu-id="b89e4-202">Скопируйте файл из tooAzure URL-адрес большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="b89e4-202">Copy file from URL tooAzure Blob</span></span>
<span data-ttu-id="b89e4-203">Теперь добавим код, который позволяет нам toocopy файл из tooan URL-адрес BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="b89e4-203">Now, let's add code that allows us toocopy a file from a URL tooan Azure Blob.</span></span> 

<span data-ttu-id="b89e4-204">Измените `TransferUrlToAzureBlob`.</span><span class="sxs-lookup"><span data-stu-id="b89e4-204">Modify `TransferUrlToAzureBlob`:</span></span>

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

<span data-ttu-id="b89e4-205">Один вариант важные использования для этой функции — при необходимости toomove данные из другой облачной службы (например, AWS) tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b89e4-205">One important use case for this feature is when you need toomove data from another cloud service (e.g. AWS) tooAzure.</span></span> <span data-ttu-id="b89e4-206">Пока у вас есть URL-адрес, который предоставляет вам доступ к ресурсу toohello, можно легко переместить этот ресурс в BLOB-объектов Azure с помощью hello `TransferManager.CopyAsync` метод.</span><span class="sxs-lookup"><span data-stu-id="b89e4-206">As long as you have a URL that gives you access toohello resource, you can easily move that resource into Azure Blobs by using hello `TransferManager.CopyAsync` method.</span></span> <span data-ttu-id="b89e4-207">В этом методе также представлен новый логический параметр.</span><span class="sxs-lookup"><span data-stu-id="b89e4-207">This method also introduces a new boolean parameter.</span></span> <span data-ttu-id="b89e4-208">Этот параметр слишком`true` указывает, что мы хотим toodo асинхронной серверную копирования.</span><span class="sxs-lookup"><span data-stu-id="b89e4-208">Setting this parameter too`true` indicates that we want toodo an asynchronous server-side copy.</span></span> <span data-ttu-id="b89e4-209">Этот параметр слишком`false` указывает синхронной копии - т hello ресурсов локального компьютера загруженный tooour во-первых, затем отправлены tooAzure больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="b89e4-209">Setting this parameter too`false` indicates a synchronous copy - meaning hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="b89e4-210">Однако синхронного копирования в данный момент доступна только для копирования из одного tooanother ресурсов хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b89e4-210">However, synchronous copy is currently only available for copying from one Azure Storage resource tooanother.</span></span> 

## <a name="transfer-azure-blob-tooazure-blob"></a><span data-ttu-id="b89e4-211">Передача больших двоичных объектов Azure tooAzure больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="b89e4-211">Transfer Azure Blob tooAzure Blob</span></span>
<span data-ttu-id="b89e4-212">Другая функция, предоставляемая однозначно hello библиотеки перемещения данных — toocopy возможность hello из одного tooanother ресурсов хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b89e4-212">Another feature that's uniquely provided by hello Data Movement Library is hello ability toocopy from one Azure Storage resource tooanother.</span></span> 

<span data-ttu-id="b89e4-213">Измените `TransferAzureBlobToAzureBlob`.</span><span class="sxs-lookup"><span data-stu-id="b89e4-213">Modify `TransferAzureBlobToAzureBlob`:</span></span>

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

<span data-ttu-id="b89e4-214">В этом примере задается hello логического параметра `TransferManager.CopyAsync` слишком`false` tooindicate, что мы хотим toodo синхронного копирования.</span><span class="sxs-lookup"><span data-stu-id="b89e4-214">In this example, we set hello boolean parameter in `TransferManager.CopyAsync` too`false` tooindicate that we want toodo a synchronous copy.</span></span> <span data-ttu-id="b89e4-215">Это значит, которая hello ресурсов локального компьютера загруженный tooour сначала, то отправлен tooAzure больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="b89e4-215">This means that hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="b89e4-216">параметр синхронного копирования Hello — отличный способ tooensure, что операции копирования обеспечивает согласованное скорость.</span><span class="sxs-lookup"><span data-stu-id="b89e4-216">hello synchronous copy option is a great way tooensure that your copy operation has a consistent speed.</span></span> <span data-ttu-id="b89e4-217">Напротив скорость hello асинхронную копию серверных зависит hello доступную пропускную способность сети на сервере hello, который может меняться.</span><span class="sxs-lookup"><span data-stu-id="b89e4-217">In contrast, hello speed of an asynchronous server-side copy is dependent on hello available network bandwidth on hello server, which can fluctuate.</span></span> <span data-ttu-id="b89e4-218">Однако синхронного копирования может создавать копии tooasynchronous исходящих дополнительных затрат по сравнению.</span><span class="sxs-lookup"><span data-stu-id="b89e4-218">However, synchronous copy may generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="b89e4-219">Hello рекомендуется toouse синхронного копирования на виртуальной Машине Azure, hello же регионе, что ваш источник учетной записи tooavoid исходящих затраты на хранение.</span><span class="sxs-lookup"><span data-stu-id="b89e4-219">hello recommended approach is toouse synchronous copy in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="conclusion"></a><span data-ttu-id="b89e4-220">Заключение</span><span class="sxs-lookup"><span data-stu-id="b89e4-220">Conclusion</span></span>
<span data-ttu-id="b89e4-221">Приложение для перемещения данных готово.</span><span class="sxs-lookup"><span data-stu-id="b89e4-221">Our data movement application is now complete.</span></span> <span data-ttu-id="b89e4-222">[Hello полный образец кода можно найти в GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span><span class="sxs-lookup"><span data-stu-id="b89e4-222">[hello full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b89e4-223">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b89e4-223">Next steps</span></span>
<span data-ttu-id="b89e4-224">В данном руководстве по началу работы мы создали приложение, которое взаимодействует со службой хранилища Azure и работает в Windows, Linux и MacOS.</span><span class="sxs-lookup"><span data-stu-id="b89e4-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span></span> <span data-ttu-id="b89e4-225">Данное руководство ориентировано на хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="b89e4-225">This getting started focused on Blob Storage.</span></span> <span data-ttu-id="b89e4-226">Тем не менее этот же набор знаний может быть применен tooFile хранилища.</span><span class="sxs-lookup"><span data-stu-id="b89e4-226">However, this same knowledge can be applied tooFile Storage.</span></span> <span data-ttu-id="b89e4-227">toolearn более, извлечь [справочная документация по библиотеке перемещения данных хранилища Azure](https://azure.github.io/azure-storage-net-data-movement).</span><span class="sxs-lookup"><span data-stu-id="b89e4-227">toolearn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span></span>

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]




