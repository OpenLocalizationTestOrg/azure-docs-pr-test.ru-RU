---
title: "Приступая к работе с хранилищем BLOB-объектов и подключенными службами Visual Studio (ASP.NET Core) | Документация Майкрософт"
description: "Начало работы с хранилищем BLOB-объектов Azure в проекте Visual Studio ASP.NET Core после создания учетной записи хранения с использованием подключенных служб Visual Studio."
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
ms.openlocfilehash: e725015c8be7ecfa908f0ae75986b73f218fa3ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="06a1c-103">Приступая к работе с хранилищем BLOB-объектов Azure и подключенными службами Visual Studio (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="06a1c-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="06a1c-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="06a1c-104">Overview</span></span>
<span data-ttu-id="06a1c-105">В этой статье описывается, как приступить к использованию хранилища BLOB-объектов Azure в Visual Studio после создания учетной записи хранения Azure или указания ссылки на нее в проекте ASP.NET Core с помощью диалогового окна "Добавление подключенных служб" в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="06a1c-105">This article describes how to get started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio Add Connected Services dialog.</span></span>

<span data-ttu-id="06a1c-106">Хранилище больших двоичных объектов Azure — это служба хранения большого количества неструктурированных данных, к которым можно получить доступ практически из любой точки мира по протоколам HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="06a1c-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="06a1c-107">Один большой двоичный объект может быть любого размера.</span><span class="sxs-lookup"><span data-stu-id="06a1c-107">A single blob can be any size.</span></span> <span data-ttu-id="06a1c-108">Большими двоичными объектами могут быть изображения, аудио- и видеофайлы, необработанные данные и файлы документов.</span><span class="sxs-lookup"><span data-stu-id="06a1c-108">Blobs can be things like images, audio and video files, raw data, and document files.</span></span> <span data-ttu-id="06a1c-109">В этой статье описывается, как приступить к работе с хранилищем BLOB-объектов после создания учетной записи хранения Azure с помощью диалогового окна **Добавление подключенных служб** в проекте ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="06a1c-109">This article describes how to get started with blob storage after you create an Azure storage account by using the Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span></span>

<span data-ttu-id="06a1c-110">Так же как файлы располагаются в папках, большие двоичные объекты хранилища располагаются в контейнерах.</span><span class="sxs-lookup"><span data-stu-id="06a1c-110">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="06a1c-111">После создания хранилища вы можете создать один или несколько контейнеров в нем.</span><span class="sxs-lookup"><span data-stu-id="06a1c-111">After you have created a storage, you create one or more containers in the storage.</span></span> <span data-ttu-id="06a1c-112">Например, можно создать хранилище с именем "Альбом", в нем создать контейнеры "изображения" для хранения файлов изображений и "аудио" для хранения аудиофайлов.</span><span class="sxs-lookup"><span data-stu-id="06a1c-112">For example, in a storage called "Scrapbook," you can create containers in the storage called "images" to store pictures and another called "audio" to store audio files.</span></span> <span data-ttu-id="06a1c-113">После создания контейнеров в них можно отправлять индивидуальные большие двоичные объекты.</span><span class="sxs-lookup"><span data-stu-id="06a1c-113">After you create the containers, you can upload individual blob files to them.</span></span> <span data-ttu-id="06a1c-114">Дополнительные сведения о выполнении программных операций с большими двоичными объектами см. в статье [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="06a1c-114">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="06a1c-115">Доступ к контейнерам больших двоичных объектов в коде</span><span class="sxs-lookup"><span data-stu-id="06a1c-115">Access blob containers in code</span></span>
<span data-ttu-id="06a1c-116">Для программного доступа к большим двоичным объектам в проектах ASP.NET Core необходимо добавить следующие элементы, если они еще не существуют.</span><span class="sxs-lookup"><span data-stu-id="06a1c-116">To programmatically access blobs in ASP.NET Core projects, you need to add the following items, if they're not already present.</span></span>

1. <span data-ttu-id="06a1c-117">Добавьте следующие объявления пространств имен кода в начало каждого файла C#, в котором вы собираетесь обращаться к службе хранилища Azure программным способом.</span><span class="sxs-lookup"><span data-stu-id="06a1c-117">Add the following code namespace declarations to the top of any C# file in which you want to programmatically access Azure storage.</span></span>
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. <span data-ttu-id="06a1c-118">Получите объект **CloudStorageAccount** , представляющий данные учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="06a1c-118">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="06a1c-119">Используйте следующий код, чтобы получить строку подключения и сведения об учетной записи хранения из конфигурации службы Azure.</span><span class="sxs-lookup"><span data-stu-id="06a1c-119">Use the following code to get your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    <span data-ttu-id="06a1c-120">**ПРИМЕЧАНИЕ.** Вставьте весь код, представленный выше, перед кодом из следующих разделов.</span><span class="sxs-lookup"><span data-stu-id="06a1c-120">**NOTE:** Use all of the above code in front of the code in the following sections.</span></span>
3. <span data-ttu-id="06a1c-121">Используйте объект **CloudBlobClient**, чтобы получить ссылку **CloudBlobContainer** на существующий контейнер в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="06a1c-121">Use a **CloudBlobClient** object to get a **CloudBlobContainer** reference to an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference to a container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a><span data-ttu-id="06a1c-122">Создание контейнера в коде</span><span class="sxs-lookup"><span data-stu-id="06a1c-122">Create a container in code</span></span>
<span data-ttu-id="06a1c-123">Вы также можете использовать объект **CloudBlobClient** для создания контейнера в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="06a1c-123">You can also use the **CloudBlobClient** to create a container in your storage account.</span></span> <span data-ttu-id="06a1c-124">Вам нужно всего лишь добавить вызов **CreateIfNotExistsAsync** , как это сделано в следующем коде:</span><span class="sxs-lookup"><span data-stu-id="06a1c-124">All you need to do is to add a call to **CreateIfNotExistsAsync** as in the following code:</span></span>

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference to a container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="06a1c-125">**Примечание**. Интерфейсы API, которые выполняют вызовы к службе хранилища Azure в ASP.NET Core, являются асинхронными.</span><span class="sxs-lookup"><span data-stu-id="06a1c-125">**NOTE:** The APIs that perform calls to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="06a1c-126">Дополнительные сведения см. в статье [Asynchronous Programming with async and await (C#)](http://msdn.microsoft.com/library/hh191443.aspx) (Асинхронное программирование с использованием ключевых слов Async и Await (C#)).</span><span class="sxs-lookup"><span data-stu-id="06a1c-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="06a1c-127">В следующем примере кода предполагается, что используются асинхронные методы программирования.</span><span class="sxs-lookup"><span data-stu-id="06a1c-127">The code below assumes async programming methods are being used.</span></span>

<span data-ttu-id="06a1c-128">Чтобы сделать файлы в контейнере доступными для всех пользователей, сделайте контейнер общедоступным с помощью следующего примера кода.</span><span class="sxs-lookup"><span data-stu-id="06a1c-128">To make the files within the container available to everyone, you can set the container to be public by using the following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="06a1c-129">Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="06a1c-129">Upload a blob into a container</span></span>
<span data-ttu-id="06a1c-130">Для отправки файла большого двоичного объекта в контейнер получите ссылку на контейнер и используйте ее для получения ссылки на большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="06a1c-130">To upload a blob file into a container, get a container reference and use it to get a blob reference.</span></span> <span data-ttu-id="06a1c-131">Получив ссылку на большой двоичный объект, вы можете передать в него любой поток данных с помощью метода **UploadFromStreamAsync**.</span><span class="sxs-lookup"><span data-stu-id="06a1c-131">After you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStreamAsync** method.</span></span> <span data-ttu-id="06a1c-132">Эта операция создает большой двоичный объект, если он не существует, или заменяет его, если он существует.</span><span class="sxs-lookup"><span data-stu-id="06a1c-132">This operation creates the blob if it's not already there, or overwrites it if it does exist.</span></span> <span data-ttu-id="06a1c-133">В следующем примере показано, как отправить BLOB-объект в контейнер. Предполагается, что контейнер уже был создан.</span><span class="sxs-lookup"><span data-stu-id="06a1c-133">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

    // Get a reference to a blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite the "myblob" blob with the contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="06a1c-134">Перечисление BLOB-объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="06a1c-134">List the blobs in a container</span></span>
<span data-ttu-id="06a1c-135">Для перечисления BLOB-объектов в контейнере сначала необходимо получить ссылку на контейнер.</span><span class="sxs-lookup"><span data-stu-id="06a1c-135">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="06a1c-136">После этого вы сможете извлекать из контейнера большие двоичные объекты и каталоги с помощью метода **ListBlobsSegmentedAsync** .</span><span class="sxs-lookup"><span data-stu-id="06a1c-136">You can then call the container's **ListBlobsSegmentedAsync** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="06a1c-137">Для доступа к широкому набору свойств и методов возвращаемого объекта **IListBlobItem** необходимо преобразовать его в объект **CloudBlockBlob**, **CloudPageBlob** или **CloudBlobDirectory**.</span><span class="sxs-lookup"><span data-stu-id="06a1c-137">To access the rich set of properties and methods for a returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="06a1c-138">Если тип большого двоичного объекта неизвестен, можно использовать проверку типов, чтобы определить нужный.</span><span class="sxs-lookup"><span data-stu-id="06a1c-138">If you don't know the blob type, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="06a1c-139">Следующий код показывает, как получить и вывести URI каждого элемента в контейнере.</span><span class="sxs-lookup"><span data-stu-id="06a1c-139">The following code demonstrates how to retrieve and output the URI of each item in a container.</span></span>

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

<span data-ttu-id="06a1c-140">Можно вывести список содержимого контейнера BLOB-объектов и другими способами.</span><span class="sxs-lookup"><span data-stu-id="06a1c-140">There are others ways to list the contents of a blob container.</span></span> <span data-ttu-id="06a1c-141">Дополнительные сведения см. в разделе [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container).</span><span class="sxs-lookup"><span data-stu-id="06a1c-141">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="06a1c-142">Загрузка BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="06a1c-142">Download a blob</span></span>
<span data-ttu-id="06a1c-143">Чтобы скачать большой двоичный объект, сначала получите ссылку на него, а затем вызовите метод **DownloadToStreamAsync** .</span><span class="sxs-lookup"><span data-stu-id="06a1c-143">To download a blob, first get a reference to the blob, and then call the **DownloadToStreamAsync** method.</span></span> <span data-ttu-id="06a1c-144">В следующем примере метод **DownloadToStreamAsync** используется для переноса содержимого большого двоичного объекта в объект потока, который затем можно сохранить в локальном файле.</span><span class="sxs-lookup"><span data-stu-id="06a1c-144">The following example uses the **DownloadToStreamAsync** method to transfer the blob contents to a stream object that you can then save as a local file.</span></span>

    // Get a reference to a blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save the blob contents to a file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

<span data-ttu-id="06a1c-145">Есть другие способы сохранения больших двоичных объектов в виде файлов.</span><span class="sxs-lookup"><span data-stu-id="06a1c-145">There are other ways to save blobs as files.</span></span> <span data-ttu-id="06a1c-146">Дополнительные сведения см. в разделе [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](storage-dotnet-how-to-use-blobs.md#download-blobs).</span><span class="sxs-lookup"><span data-stu-id="06a1c-146">See [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="06a1c-147">Удаление большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="06a1c-147">Delete a blob</span></span>
<span data-ttu-id="06a1c-148">Чтобы удалить большой двоичный объект, сначала получите ссылку на него, а затем вызовите метод **DeleteAsync** .</span><span class="sxs-lookup"><span data-stu-id="06a1c-148">To delete a blob, first get a reference to the blob, and then call the **DeleteAsync** method on it.</span></span>

    // Get a reference to a blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete the blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a><span data-ttu-id="06a1c-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="06a1c-149">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

