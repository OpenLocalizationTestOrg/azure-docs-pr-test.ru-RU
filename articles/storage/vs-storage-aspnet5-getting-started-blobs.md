---
title: "aaaGet работы с Visual Studio и хранилище больших двоичных объектов подключенных служб (ASP.NET Core) | Документы Microsoft"
description: "Запуск с помощью хранилища больших двоичных объектов Azure в проекте Visual Studio ASP.NET Core после создания учетной записи хранилища с помощью Visual Studio tooget подключенные службы"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: a4c31c08c38d99eb9c66fe2af72ca42fa3804688
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="4235f-103">Приступая к работе с хранилищем BLOB-объектов Azure и подключенными службами Visual Studio (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="4235f-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="4235f-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="4235f-104">Overview</span></span>
<span data-ttu-id="4235f-105">В этой статье описывается, как tooget запущена с помощью хранилища больших двоичных объектов Azure в Visual Studio, после создания или ссылка на учетную запись хранилища Azure в проекте ASP.NET Core с помощью диалогового окна Visual Studio Добавление подключенных служб hello.</span><span class="sxs-lookup"><span data-stu-id="4235f-105">This article describes how tooget started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio Add Connected Services dialog.</span></span>

<span data-ttu-id="4235f-106">Хранилище Azure BLOB-объекта — это служба для хранения больших объемов неструктурированных данных, который может осуществляться из любого места в Здравствуй, мир! через HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4235f-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="4235f-107">Один большой двоичный объект может быть любого размера.</span><span class="sxs-lookup"><span data-stu-id="4235f-107">A single blob can be any size.</span></span> <span data-ttu-id="4235f-108">Большими двоичными объектами могут быть изображения, аудио- и видеофайлы, необработанные данные и файлы документов.</span><span class="sxs-lookup"><span data-stu-id="4235f-108">Blobs can be things like images, audio and video files, raw data, and document files.</span></span> <span data-ttu-id="4235f-109">В этой статье описывается, как tooget работы с хранилищем больших двоичных объектов, после создания учетной записи хранилища Azure с помощью Visual Studio hello **Добавление подключенных служб** диалогового окна в проектах ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="4235f-109">This article describes how tooget started with blob storage after you create an Azure storage account by using hello Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span></span>

<span data-ttu-id="4235f-110">Так же как файлы располагаются в папках, большие двоичные объекты хранилища располагаются в контейнерах.</span><span class="sxs-lookup"><span data-stu-id="4235f-110">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="4235f-111">После создания хранилища, можно создать один или несколько контейнеров в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="4235f-111">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="4235f-112">Например в хранилище, вызывается буферный «файл», контейнеров можно создать в хранилище hello, называется «images» toostore изображения и вызывается другой toostore «звук» звуковые файлы.</span><span class="sxs-lookup"><span data-stu-id="4235f-112">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="4235f-113">После создания hello контейнеры, можно передать файлы toothem отдельных больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="4235f-113">After you create hello containers, you can upload individual blob files toothem.</span></span> <span data-ttu-id="4235f-114">Дополнительные сведения о выполнении программных операций с большими двоичными объектами см. в статье [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="4235f-114">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="4235f-115">Доступ к контейнерам больших двоичных объектов в коде</span><span class="sxs-lookup"><span data-stu-id="4235f-115">Access blob containers in code</span></span>
<span data-ttu-id="4235f-116">tooprogrammatically доступа к большим двоичным объектам в проектах ASP.NET Core, требуется hello tooadd следующих элементов, если они еще не существует.</span><span class="sxs-lookup"><span data-stu-id="4235f-116">tooprogrammatically access blobs in ASP.NET Core projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="4235f-117">Добавьте следующий код объявления пространства имен toohello начало любого файла C#, которой требуется доступ tooprogrammatically хранилища Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4235f-117">Add hello following code namespace declarations toohello top of any C# file in which you want tooprogrammatically access Azure storage.</span></span>
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. <span data-ttu-id="4235f-118">Получите объект **CloudStorageAccount** , представляющий данные учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="4235f-118">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="4235f-119">Используйте следующий код tooget hello хранения строки соединения и сведения об учетной записи хранилища из конфигурации службы Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4235f-119">Use hello following code tooget your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    <span data-ttu-id="4235f-120">**Примечание:** использовать все hello над кодом перед кода hello в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="4235f-120">**NOTE:** Use all of hello above code in front of hello code in hello following sections.</span></span>
3. <span data-ttu-id="4235f-121">Используйте **CloudBlobClient** объекта tooget **CloudBlobContainer** ссылки tooan существующий контейнер в вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="4235f-121">Use a **CloudBlobClient** object tooget a **CloudBlobContainer** reference tooan existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a><span data-ttu-id="4235f-122">Создание контейнера в коде</span><span class="sxs-lookup"><span data-stu-id="4235f-122">Create a container in code</span></span>
<span data-ttu-id="4235f-123">Можно также использовать hello **CloudBlobClient** toocreate контейнера в учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="4235f-123">You can also use hello **CloudBlobClient** toocreate a container in your storage account.</span></span> <span data-ttu-id="4235f-124">Все что нужно toodo — tooadd вызов слишком**CreateIfNotExistsAsync** как hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="4235f-124">All you need toodo is tooadd a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="4235f-125">**Примечание:** hello API, которые выполняют вызовы tooAzure хранилища в ASP.NET Core являются асинхронными.</span><span class="sxs-lookup"><span data-stu-id="4235f-125">**NOTE:** hello APIs that perform calls tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="4235f-126">Дополнительные сведения см. в статье [Asynchronous Programming with async and await (C#)](http://msdn.microsoft.com/library/hh191443.aspx) (Асинхронное программирование с использованием ключевых слов Async и Await (C#)).</span><span class="sxs-lookup"><span data-stu-id="4235f-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="4235f-127">Приведенный ниже код Hello предполагается, что используются асинхронные методы программирования.</span><span class="sxs-lookup"><span data-stu-id="4235f-127">hello code below assumes async programming methods are being used.</span></span>

<span data-ttu-id="4235f-128">toomake файлов hello в доступных tooeveryone hello контейнера, можно задать toobe контейнера hello открытый с помощью hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="4235f-128">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="4235f-129">Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="4235f-129">Upload a blob into a container</span></span>
<span data-ttu-id="4235f-130">tooupload файла большого двоичного объекта в контейнер, получить ссылку на контейнер и использовать его tooget ссылку на большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="4235f-130">tooupload a blob file into a container, get a container reference and use it tooget a blob reference.</span></span> <span data-ttu-id="4235f-131">После того как вы ссылку на большой двоичный объект, можно передать любой поток данных tooit с вызывающему Привет **UploadFromStreamAsync** метод.</span><span class="sxs-lookup"><span data-stu-id="4235f-131">After you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStreamAsync** method.</span></span> <span data-ttu-id="4235f-132">Эта операция создает hello большого двоичного объекта, если он еще не существует, или перезаписывает его, если он существует.</span><span class="sxs-lookup"><span data-stu-id="4235f-132">This operation creates hello blob if it's not already there, or overwrites it if it does exist.</span></span> <span data-ttu-id="4235f-133">Следующий пример показывает как Hello tooupload большого двоичного объекта в контейнер и предполагается hello контейнера уже был создан.</span><span class="sxs-lookup"><span data-stu-id="4235f-133">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="4235f-134">Перечисление hello больших двоичных объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="4235f-134">List hello blobs in a container</span></span>
<span data-ttu-id="4235f-135">toolist hello BLOB-объектов в контейнере, сначала нужно получить ссылку на контейнер.</span><span class="sxs-lookup"><span data-stu-id="4235f-135">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="4235f-136">Затем можно вызвать hello контейнера **ListBlobsSegmentedAsync** метод tooretrieve hello BLOB-объектов и/или каталогов в ней.</span><span class="sxs-lookup"><span data-stu-id="4235f-136">You can then call hello container's **ListBlobsSegmentedAsync** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="4235f-137">широкий набор свойств и методов для возвращенной hello tooaccess **IListBlobItem**, необходимо привести tooa **CloudBlockBlob**, **CloudPageBlob**, или  **CloudBlobDirectory** объекта.</span><span class="sxs-lookup"><span data-stu-id="4235f-137">tooaccess hello rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="4235f-138">Если вы не знаете тип blob hello, можно использовать тип возврата toodetermine какие toocast его.</span><span class="sxs-lookup"><span data-stu-id="4235f-138">If you don't know hello blob type, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="4235f-139">Здравствуй, следующий код демонстрирует, как tooretrieve и вывод hello URI каждого элемента в контейнере.</span><span class="sxs-lookup"><span data-stu-id="4235f-139">hello following code demonstrates how tooretrieve and output hello URI of each item in a container.</span></span>

    BlobContinuationToken token = null;
    do
    {
        BlobResultSegment resultSegment = await container.ListBlobsSegmentedAsync(token);
        token = resultSegment.ContinuationToken;

        foreach (IListBlobItem item in resultSegment.Results)
        {
            if (item.GetType() == typeof(CloudBlockBlob))
            {
                CloudBlockBlob blob = (CloudBlockBlob)item;
                Console.WriteLine("Block blob of length {0}: {1}", blob.Properties.Length, blob.Uri);
            }

            else if (item.GetType() == typeof(CloudPageBlob))
            {
                CloudPageBlob pageBlob = (CloudPageBlob)item;

                Console.WriteLine("Page blob of length {0}: {1}", pageBlob.Properties.Length, pageBlob.Uri);
            }

            else if (item.GetType() == typeof(CloudBlobDirectory))
            {
                CloudBlobDirectory directory = (CloudBlobDirectory)item;

                Console.WriteLine("Directory: {0}", directory.Uri);
            }
        }
    } while (token != null);

<span data-ttu-id="4235f-140">Существуют и другие способы toolist hello содержимого контейнера BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="4235f-140">There are others ways toolist hello contents of a blob container.</span></span> <span data-ttu-id="4235f-141">Дополнительные сведения см. в разделе [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container).</span><span class="sxs-lookup"><span data-stu-id="4235f-141">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="4235f-142">Загрузка BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="4235f-142">Download a blob</span></span>
<span data-ttu-id="4235f-143">toodownload большого двоичного объекта, сначала нужно получить toohello эталонный BLOB-объект, а затем вызвать hello **DownloadToStreamAsync** метод.</span><span class="sxs-lookup"><span data-stu-id="4235f-143">toodownload a blob, first get a reference toohello blob, and then call hello **DownloadToStreamAsync** method.</span></span> <span data-ttu-id="4235f-144">Hello следующий пример использует hello **DownloadToStreamAsync** метод tootransfer hello blob содержимое tooa объект потока, который затем можно сохранить как локальный файл.</span><span class="sxs-lookup"><span data-stu-id="4235f-144">hello following example uses hello **DownloadToStreamAsync** method tootransfer hello blob contents tooa stream object that you can then save as a local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

<span data-ttu-id="4235f-145">Существуют другие способы toosave большие двоичные объекты как файлы.</span><span class="sxs-lookup"><span data-stu-id="4235f-145">There are other ways toosave blobs as files.</span></span> <span data-ttu-id="4235f-146">Дополнительные сведения см. в разделе [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](storage-dotnet-how-to-use-blobs.md#download-blobs).</span><span class="sxs-lookup"><span data-stu-id="4235f-146">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="4235f-147">Удаление большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="4235f-147">Delete a blob</span></span>
<span data-ttu-id="4235f-148">toodelete большого двоичного объекта, сначала нужно получить toohello эталонный BLOB-объект, а затем вызвать hello **DeleteAsync** метода.</span><span class="sxs-lookup"><span data-stu-id="4235f-148">toodelete a blob, first get a reference toohello blob, and then call hello **DeleteAsync** method on it.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a><span data-ttu-id="4235f-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4235f-149">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

