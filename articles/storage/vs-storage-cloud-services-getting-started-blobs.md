---
title: "Приступая к работе с хранилищем BLOB-объектов и подключенными службами Visual Studio (облачные службы) | Документация Майкрософт"
description: "Как приступить к работе, используя хранилище больших двоичных объектов Azure в проекте облачной службы в Visual Studio после подключения к учетной записи хранения с помощью подключенных служб Visual Studio"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: e154c81ef3765a3c006b3c27a979be881f14d0ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="bb6fa-103">Начало работы с хранилищем больших двоичных объектов Azure и подключенными службами Visual Studio (проектами облачных служб)</span><span class="sxs-lookup"><span data-stu-id="bb6fa-103">Get started with Azure Blob Storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="bb6fa-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="bb6fa-104">Overview</span></span>
<span data-ttu-id="bb6fa-105">В этой статье описывается, как приступить к использованию хранилища больших двоичных объектов Azure после создания учетной записи хранения Azure с помощью диалогового окна **Добавление подключенных служб** в проекте облачных служб Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-105">This article describes how to get started with Azure Blob Storage after you created or referenced an Azure Storage account by using the Visual Studio **Add Connected Services** dialog in a Visual Studio cloud services project.</span></span> <span data-ttu-id="bb6fa-106">Мы покажем, как получить доступ к контейнерам больших двоичных объектов и как создавать их, а также как выполнять общие задачи, такие как отправка, перечисление и скачивание больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-106">We'll show you how to access and create blob containers, and how to perform common tasks like uploading, listing, and downloading blobs.</span></span> <span data-ttu-id="bb6fa-107">Примеры написаны на C\# и используют [клиентскую библиотеку службы хранилища Microsoft Azure для .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="bb6fa-107">The samples are written in C\# and use the [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="bb6fa-108">Хранилище больших двоичных объектов Azure — это служба хранения большого количества неструктурированных данных, к которым можно получить доступ практически из любой точки мира по протоколам HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-108">Azure Blob Storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="bb6fa-109">Один большой двоичный объект может быть любого размера.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-109">A single blob can be any size.</span></span> <span data-ttu-id="bb6fa-110">Большими двоичными объектами могут быть изображения, аудио- и видеофайлы, необработанные данные и файлы документов.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-110">Blobs can be things like images, audio and video files, raw data, and document files.</span></span>

<span data-ttu-id="bb6fa-111">Так же как файлы располагаются в папках, большие двоичные объекты хранилища располагаются в контейнерах.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-111">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="bb6fa-112">После создания хранилища вы можете создать один или несколько контейнеров в нем.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-112">After you have created a storage, you create one or more containers in the storage.</span></span> <span data-ttu-id="bb6fa-113">Например, можно создать хранилище с именем "Альбом", в нем создать контейнеры "изображения" для хранения файлов изображений и "аудио" для хранения аудиофайлов.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-113">For example, in a storage called "Scrapbook," you can create containers in the storage called "images" to store pictures and another called "audio" to store audio files.</span></span> <span data-ttu-id="bb6fa-114">После создания контейнеров в них можно отправлять индивидуальные большие двоичные объекты.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-114">After you create the containers, you can upload individual blob files to them.</span></span>

* <span data-ttu-id="bb6fa-115">Дополнительные сведения о программных операциях с большими двоичными объектами см. в статье [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="bb6fa-115">For more information on programmatically manipulating blobs, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md).</span></span>
* <span data-ttu-id="bb6fa-116">Общие сведения о службе хранилища Azure см. в [документации по службе хранилища](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="bb6fa-116">For general information about Azure Storage, see [Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>
* <span data-ttu-id="bb6fa-117">Общие сведения об облачных службах Azure см. в [документации по облачным службам](https://azure.microsoft.com/documentation/services/cloud-services/).</span><span class="sxs-lookup"><span data-stu-id="bb6fa-117">For general information about Azure Cloud Services, see [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/).</span></span>
* <span data-ttu-id="bb6fa-118">Дополнительные сведения о программировании для приложений ASP.NET см. в разделе [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="bb6fa-118">For more information about programming ASP.NET applications, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="bb6fa-119">Доступ к контейнерам больших двоичных объектов в коде</span><span class="sxs-lookup"><span data-stu-id="bb6fa-119">Access blob containers in code</span></span>
<span data-ttu-id="bb6fa-120">Для программного доступа к большим двоичным объектам в проектах облачных служб необходимо добавить следующие элементы, если они еще не существуют.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-120">To programmatically access blobs in cloud service projects, you need to add the following items, if they're not already present.</span></span>

1. <span data-ttu-id="bb6fa-121">Добавьте следующие объявления пространств имен кода в начало любого файла C#,в котором вы собираетесь получать доступ к хранилищу Azure программным способом.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-121">Add the following code namespace declarations to the top of any C# file in which you wish to programmatically access Azure Storage.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="bb6fa-122">Получите объект **CloudStorageAccount** , представляющий данные учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-122">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="bb6fa-123">Используйте следующий код, чтобы получить строку подключения и сведения об учетной записи хранения из конфигурации службы Azure.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-123">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. <span data-ttu-id="bb6fa-124">Получите объект **CloudBlobClient** , чтобы указать ссылку на существующий контейнер в вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-124">Get a **CloudBlobClient** object to reference an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. <span data-ttu-id="bb6fa-125">Получите объект **CloudBlobContainer** , чтобы указать ссылку на определенный контейнер больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-125">Get a **CloudBlobContainer** object to reference a specific blob container.</span></span>
   
        // Get a reference to a container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> <span data-ttu-id="bb6fa-126">Вставьте весь код, показанный в предыдущей процедуре, перед кодом, показанным в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-126">Use all of the code shown in the previous procedure in front of the code shown in the following sections.</span></span>
> 
> 

## <a name="create-a-container-in-code"></a><span data-ttu-id="bb6fa-127">Создание контейнера в коде</span><span class="sxs-lookup"><span data-stu-id="bb6fa-127">Create a container in code</span></span>
> [!NOTE]
> <span data-ttu-id="bb6fa-128">Некоторые интерфейсы API, которые выполняют вызовы в хранилище Azure в ASP.NET, являются асинхронными.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-128">Some APIs that perform calls out to Azure Storage in ASP.NET are asynchronous.</span></span> <span data-ttu-id="bb6fa-129">Дополнительные сведения см. в статье [Asynchronous Programming with async and await (C#)](http://msdn.microsoft.com/library/hh191443.aspx) (Асинхронное программирование с использованием ключевых слов Async и Await (C#)).</span><span class="sxs-lookup"><span data-stu-id="bb6fa-129">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="bb6fa-130">Код в приведенном ниже примере предполагает, что вы используете асинхронные методы программирования.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-130">The code in the following example assumes that you are using async programming methods.</span></span>
> 
> 

<span data-ttu-id="bb6fa-131">Чтобы создать контейнер в учетной записи хранения, необходимо всего лишь добавить вызов **CreateIfNotExistsAsync** , как это сделано в следующем коде.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-131">To create a container in your storage account, all you need to do is add a call to **CreateIfNotExistsAsync** as in the following code:</span></span>

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="bb6fa-132">Чтобы сделать файлы в контейнере доступными для всех пользователей, сделайте контейнер общедоступным с помощью следующего примера кода.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-132">To make the files within the container available to everyone, you can set the container to be public by using the following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


<span data-ttu-id="bb6fa-133">Любой пользователь в Интернете может видеть большие двоичные объекты в открытом контейнере, но изменить или удалить их можно только при наличии ключа доступа.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-133">Anyone on the Internet can see blobs in a public container, but you can modify or delete them only if you have the appropriate access key.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="bb6fa-134">Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="bb6fa-134">Upload a blob into a container</span></span>
<span data-ttu-id="bb6fa-135">Хранилище BLOB-объектов Azure поддерживает блочные и страничные BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-135">Azure Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="bb6fa-136">В большинстве случаев рекомендуется использовать блочные BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-136">In the majority of cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="bb6fa-137">Для передачи файла в блочный BLOB-объект получите ссылку на контейнер и используйте ее для получения ссылки на блочный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-137">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="bb6fa-138">Получив ссылку на большой двоичный объект, вы можете отправить в него любой поток данных с помощью метода **UploadFromStream** .</span><span class="sxs-lookup"><span data-stu-id="bb6fa-138">Once you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStream** method.</span></span> <span data-ttu-id="bb6fa-139">Эта операция создает большой двоичный объект, если он не существует, или заменяет его, если он существует.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-139">This operation creates the blob if it didn't previously exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="bb6fa-140">В следующем примере показано, как отправить BLOB-объект в контейнер. Предполагается, что контейнер уже был создан.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-140">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

    // Retrieve a reference to a blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite the "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="bb6fa-141">Перечисление BLOB-объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="bb6fa-141">List the blobs in a container</span></span>
<span data-ttu-id="bb6fa-142">Для перечисления BLOB-объектов в контейнере сначала необходимо получить ссылку на контейнер.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-142">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="bb6fa-143">Затем можно использовать метод **ListBlobs** контейнера, чтобы извлечь большие двоичные объекты и/или каталоги в нем.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-143">You can then use the container's **ListBlobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="bb6fa-144">Для доступа к широкому набору свойств и методов возвращаемого объекта **IListBlobItem** необходимо преобразовать его в объект **CloudBlockBlob**, **CloudPageBlob** или **CloudBlobDirectory**.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-144">To access the rich set of properties and methods for a  returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="bb6fa-145">Если тип неизвестен, можно использовать проверку типов, чтобы определить нужный тип.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-145">If the type is unknown, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="bb6fa-146">Следующий код демонстрирует, как получить и вывести универсальный код ресурса (URI) каждого элемента в контейнере **photos** .</span><span class="sxs-lookup"><span data-stu-id="bb6fa-146">The following code demonstrates how to retrieve and output the URI of each item in the **photos** container:</span></span>

    // Loop over items within the container and output the length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, false))
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

<span data-ttu-id="bb6fa-147">Как показано в предыдущем примере кода, служба BLOB-объектов также использует концепцию каталогов внутри контейнеров.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-147">As shown in the previous code sample, the blob service has the concept of directories within containers, as well.</span></span> <span data-ttu-id="bb6fa-148">Таким образом, можно организовать BLOB-объекты в структуре, похожей на папки.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-148">This is so that you can organize your blobs in a more folder-like structure.</span></span> <span data-ttu-id="bb6fa-149">Для примера рассмотрим следующий набор блочных BLOB-объектов в контейнере **photos**.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-149">For example, consider the following set of block blobs in a container named **photos**:</span></span>

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

<span data-ttu-id="bb6fa-150">При вызове метода **ListBlobs** контейнера (как в примере выше) возвращаемая коллекция будет содержать объекты **CloudBlobDirectory** и **CloudBlockBlob**, представляющие каталоги и большие двоичные объекты верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-150">When you call **ListBlobs** on the container (as in the previous sample), the collection returned contains **CloudBlobDirectory** and **CloudBlockBlob** objects representing the directories and blobs contained at the top level.</span></span> <span data-ttu-id="bb6fa-151">В результате получается следующее:</span><span class="sxs-lookup"><span data-stu-id="bb6fa-151">Here is the resulting output:</span></span>

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


<span data-ttu-id="bb6fa-152">При необходимости можно установить для параметра **UseFlatBlobListing** метода **ListBlobs** значение **true**.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-152">Optionally, you can set the **UseFlatBlobListing** parameter of of the **ListBlobs** method to **true**.</span></span> <span data-ttu-id="bb6fa-153">Это приведет к возвращению каждого большого двоичного объекта в виде **CloudBlockBlob**независимо от того, какой каталог используется.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-153">This results in every blob being returned as a **CloudBlockBlob**, regardless of directory.</span></span> <span data-ttu-id="bb6fa-154">Вот как выглядит вызов метода **ListBlobs**.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-154">Here is the call to **ListBlobs**:</span></span>

    // Loop over items within the container and output the length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

<span data-ttu-id="bb6fa-155">А это — результат:</span><span class="sxs-lookup"><span data-stu-id="bb6fa-155">and here are the results:</span></span>

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

<span data-ttu-id="bb6fa-156">Дополнительные сведения см. в описании метода [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span><span class="sxs-lookup"><span data-stu-id="bb6fa-156">For more information, see [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span></span>

## <a name="download-blobs"></a><span data-ttu-id="bb6fa-157">Скачивание больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="bb6fa-157">Download blobs</span></span>
<span data-ttu-id="bb6fa-158">Для загрузки BLOB-объектов сначала нужно получить ссылку на BLOB-объект, а затем вызвать метод **DownloadToStream** .</span><span class="sxs-lookup"><span data-stu-id="bb6fa-158">To download blobs, first retrieve a blob reference and then call the **DownloadToStream** method.</span></span> <span data-ttu-id="bb6fa-159">В следующем примере метод **DownloadToStream** используется для переноса содержимого большого двоичного объекта в объект потока, который затем можно сохранить в локальном файле.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-159">The following example uses the **DownloadToStream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>

    // Get a reference to a blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents to a file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

<span data-ttu-id="bb6fa-160">Можно также использовать метод **DownloadToStream** , чтобы загрузить содержимое BLOB-объекта как текстовую строку.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-160">You can also use the **DownloadToStream** method to download the contents of a blob as a text string.</span></span>

    // Get a reference to a blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a><span data-ttu-id="bb6fa-161">Удаление blob-объектов</span><span class="sxs-lookup"><span data-stu-id="bb6fa-161">Delete blobs</span></span>
<span data-ttu-id="bb6fa-162">Чтобы удалить большой двоичный объект, сначала нужно получить ссылку на него, а затем вызвать метод **Delete** .</span><span class="sxs-lookup"><span data-stu-id="bb6fa-162">To delete a blob, first get a blob reference and then call the **Delete** method.</span></span>

    // Get a reference to a blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete the blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="bb6fa-163">Асинхронное перечисление BLOB-объектов в страницах</span><span class="sxs-lookup"><span data-stu-id="bb6fa-163">List blobs in pages asynchronously</span></span>
<span data-ttu-id="bb6fa-164">Если вам нужно расположить большое количество BLOB-объектов или вы хотите управлять отображением количества объектов в результате запроса, вы можете задать расположение BLOB-объектов на странице.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-164">If you are listing a large number of blobs, or you want to control the number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="bb6fa-165">В этом примере вы узнаете, как расположить запрошенные результаты на странице асинхронно для того, чтобы не блокировать выполнение задачи ожиданием большого объема возвращаемых данных.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-165">This example shows how to return results in pages asynchronously, so that execution is not blocked while waiting to return a large set of results.</span></span>

<span data-ttu-id="bb6fa-166">В этом примере показано создание плоского списка больших двоичных объектов. Но вы также можете создать иерархический список, установив для параметра **useFlatBlobListing** в методе **ListBlobsSegmentedAsync** значение **false**.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-166">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting the **useFlatBlobListing** parameter of the **ListBlobsSegmentedAsync** method to **false**.</span></span>

<span data-ttu-id="bb6fa-167">Так как метод из примера вызывает асинхронный метод, перед ним необходимо задать ключевое слово **async**. Это позволит вернуть объект **Task**.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-167">Because the sample method calls an asynchronous method, it must be prefaced with the **async** keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="bb6fa-168">При ожидании ключевого слова для **ListBlobsSegmentedAsync** метод приостанавливает выполнение примера до тех пор, пока задача размещения результатов не завершена.</span><span class="sxs-lookup"><span data-stu-id="bb6fa-168">The await keyword specified for the **ListBlobsSegmentedAsync** method suspends execution of the sample method until the listing task completes.</span></span>

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs to the console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate the result segment returned, while the continuation token is non-null.
        // When the continuation token is null, the last page has been returned and execution can exit the loop.
        do
        {
            // This overload allows control of the page size. You can return all remaining results by passing null for the maxResults parameter,
            // or by calling a different overload.
            resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
            if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
            foreach (var blobItem in resultSegment.Results)
            {
                Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
            }
            Console.WriteLine();

            //Get the continuation token.
            continuationToken = resultSegment.ContinuationToken;
        }
        while (continuationToken != null);
    }

## <a name="next-steps"></a><span data-ttu-id="bb6fa-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bb6fa-169">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

