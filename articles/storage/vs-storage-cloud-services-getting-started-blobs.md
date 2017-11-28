---
title: "aaaGet работы с Visual Studio и хранилище больших двоичных объектов подключенных служб (облачных служб) | Документы Microsoft"
description: "Как tooget запущена с помощью хранилища больших двоичных объектов Azure в проект облачной службы в Visual Studio после подключения tooa учетной записи хранилища с помощью Visual Studio подключенные службы"
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
ms.openlocfilehash: 62fb7fcff0a90008859ebe23755f13ef0555e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="01e63-103">Начало работы с хранилищем больших двоичных объектов Azure и подключенными службами Visual Studio (проектами облачных служб)</span><span class="sxs-lookup"><span data-stu-id="01e63-103">Get started with Azure Blob Storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="01e63-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="01e63-104">Overview</span></span>
<span data-ttu-id="01e63-105">В этой статье описывается, как tooget работу с BLOB-хранилища Azure, после создания или ссылка на учетную запись хранилища Azure с помощью Visual Studio hello **Добавление подключенных служб** диалогового окна в облаке Visual Studio проект служб.</span><span class="sxs-lookup"><span data-stu-id="01e63-105">This article describes how tooget started with Azure Blob Storage after you created or referenced an Azure Storage account by using hello Visual Studio **Add Connected Services** dialog in a Visual Studio cloud services project.</span></span> <span data-ttu-id="01e63-106">Мы покажем, как tooaccess и создание контейнеров больших двоичных объектов и как tooperform общих задач и отправка, вывод и загрузка больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="01e63-106">We'll show you how tooaccess and create blob containers, and how tooperform common tasks like uploading, listing, and downloading blobs.</span></span> <span data-ttu-id="01e63-107">Hello примеры на языке C\# и использовать hello [клиентская библиотека хранилища Microsoft Azure для .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="01e63-107">hello samples are written in C\# and use hello [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="01e63-108">Хранилище Azure BLOB-объекта — это служба для хранения больших объемов неструктурированных данных, который может осуществляться из любого места в Здравствуй, мир! через HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="01e63-108">Azure Blob Storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="01e63-109">Один большой двоичный объект может быть любого размера.</span><span class="sxs-lookup"><span data-stu-id="01e63-109">A single blob can be any size.</span></span> <span data-ttu-id="01e63-110">Большими двоичными объектами могут быть изображения, аудио- и видеофайлы, необработанные данные и файлы документов.</span><span class="sxs-lookup"><span data-stu-id="01e63-110">Blobs can be things like images, audio and video files, raw data, and document files.</span></span>

<span data-ttu-id="01e63-111">Так же как файлы располагаются в папках, большие двоичные объекты хранилища располагаются в контейнерах.</span><span class="sxs-lookup"><span data-stu-id="01e63-111">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="01e63-112">После создания хранилища, можно создать один или несколько контейнеров в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="01e63-112">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="01e63-113">Например в хранилище, вызывается буферный «файл», контейнеров можно создать в хранилище hello, называется «images» toostore изображения и вызывается другой toostore «звук» звуковые файлы.</span><span class="sxs-lookup"><span data-stu-id="01e63-113">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="01e63-114">После создания hello контейнеры, можно передать файлы toothem отдельных больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="01e63-114">After you create hello containers, you can upload individual blob files toothem.</span></span>

* <span data-ttu-id="01e63-115">Дополнительные сведения о программных операциях с большими двоичными объектами см. в статье [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="01e63-115">For more information on programmatically manipulating blobs, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md).</span></span>
* <span data-ttu-id="01e63-116">Общие сведения о службе хранилища Azure см. в [документации по службе хранилища](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="01e63-116">For general information about Azure Storage, see [Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>
* <span data-ttu-id="01e63-117">Общие сведения об облачных службах Azure см. в [документации по облачным службам](https://azure.microsoft.com/documentation/services/cloud-services/).</span><span class="sxs-lookup"><span data-stu-id="01e63-117">For general information about Azure Cloud Services, see [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/).</span></span>
* <span data-ttu-id="01e63-118">Дополнительные сведения о программировании для приложений ASP.NET см. в разделе [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="01e63-118">For more information about programming ASP.NET applications, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="01e63-119">Доступ к контейнерам больших двоичных объектов в коде</span><span class="sxs-lookup"><span data-stu-id="01e63-119">Access blob containers in code</span></span>
<span data-ttu-id="01e63-120">tooprogrammatically доступа к большим двоичным объектам в проектах облачных служб, необходимо tooadd hello следующих элементов, в том случае, если они еще не существует.</span><span class="sxs-lookup"><span data-stu-id="01e63-120">tooprogrammatically access blobs in cloud service projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="01e63-121">Добавьте следующий код объявления пространства имен toohello начало любой файл C#, в котором вы хотите tooprogrammatically доступа хранилища Azure hello.</span><span class="sxs-lookup"><span data-stu-id="01e63-121">Add hello following code namespace declarations toohello top of any C# file in which you wish tooprogrammatically access Azure Storage.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="01e63-122">Получите объект **CloudStorageAccount** , представляющий данные учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="01e63-122">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="01e63-123">Hello используйте следующий код tooget hello хранения строки соединения и сведения об учетной записи хранилища из конфигурации службы Azure hello.</span><span class="sxs-lookup"><span data-stu-id="01e63-123">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. <span data-ttu-id="01e63-124">Получить **CloudBlobClient** объекта tooreference существующий контейнер в вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="01e63-124">Get a **CloudBlobClient** object tooreference an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. <span data-ttu-id="01e63-125">Получить **CloudBlobContainer** объекта tooreference конкретного BLOB-контейнере.</span><span class="sxs-lookup"><span data-stu-id="01e63-125">Get a **CloudBlobContainer** object tooreference a specific blob container.</span></span>
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> <span data-ttu-id="01e63-126">Используйте все hello код, показанный в предыдущей процедуре hello перед hello код, показываемый в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="01e63-126">Use all of hello code shown in hello previous procedure in front of hello code shown in hello following sections.</span></span>
> 
> 

## <a name="create-a-container-in-code"></a><span data-ttu-id="01e63-127">Создание контейнера в коде</span><span class="sxs-lookup"><span data-stu-id="01e63-127">Create a container in code</span></span>
> [!NOTE]
> <span data-ttu-id="01e63-128">Некоторые интерфейсы API, выполняющие вызовы out tooAzure хранилища в ASP.NET является асинхронным.</span><span class="sxs-lookup"><span data-stu-id="01e63-128">Some APIs that perform calls out tooAzure Storage in ASP.NET are asynchronous.</span></span> <span data-ttu-id="01e63-129">Дополнительные сведения см. в статье [Asynchronous Programming with async and await (C#)](http://msdn.microsoft.com/library/hh191443.aspx) (Асинхронное программирование с использованием ключевых слов Async и Await (C#)).</span><span class="sxs-lookup"><span data-stu-id="01e63-129">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="01e63-130">Hello кода hello следующий пример предполагает, что вы используете асинхронные методы программирования.</span><span class="sxs-lookup"><span data-stu-id="01e63-130">hello code in hello following example assumes that you are using async programming methods.</span></span>
> 
> 

<span data-ttu-id="01e63-131">toocreate контейнера в учетной записи хранения, все, что нужно toodo добавить вызов слишком**CreateIfNotExistsAsync** как hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="01e63-131">toocreate a container in your storage account, all you need toodo is add a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="01e63-132">toomake файлов hello в доступных tooeveryone hello контейнера, можно задать toobe контейнера hello открытый с помощью hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="01e63-132">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


<span data-ttu-id="01e63-133">Всем пользователям в Интернете hello можно увидеть в открытый контейнер BLOB-объектов, но можно изменить или удалить их только в том случае, если у вас есть ключ hello соответствующие права доступа.</span><span class="sxs-lookup"><span data-stu-id="01e63-133">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="01e63-134">Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="01e63-134">Upload a blob into a container</span></span>
<span data-ttu-id="01e63-135">Хранилище BLOB-объектов Azure поддерживает блочные и страничные BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="01e63-135">Azure Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="01e63-136">В большинстве случаев hello блочного BLOB-объекта — hello, рекомендуется toouse типа.</span><span class="sxs-lookup"><span data-stu-id="01e63-136">In hello majority of cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="01e63-137">большой двоичный объект блока файла tooa tooupload получить ссылку на контейнер и использовать его tooget ссылку на большой двоичный объект блока.</span><span class="sxs-lookup"><span data-stu-id="01e63-137">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="01e63-138">Получив ссылку на большой двоичный объект можно передать любой поток данных tooit с вызывающему Привет **UploadFromStream** метод.</span><span class="sxs-lookup"><span data-stu-id="01e63-138">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="01e63-139">Эта операция создает hello большого двоичного объекта, если он не был найден ранее, или перезаписывает его, если он существует.</span><span class="sxs-lookup"><span data-stu-id="01e63-139">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="01e63-140">Следующий пример показывает как Hello tooupload большого двоичного объекта в контейнер и предполагается hello контейнера уже был создан.</span><span class="sxs-lookup"><span data-stu-id="01e63-140">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="01e63-141">Перечисление hello больших двоичных объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="01e63-141">List hello blobs in a container</span></span>
<span data-ttu-id="01e63-142">toolist hello BLOB-объектов в контейнере, сначала нужно получить ссылку на контейнер.</span><span class="sxs-lookup"><span data-stu-id="01e63-142">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="01e63-143">Затем можно использовать контейнер hello **ListBlobs** метод tooretrieve hello BLOB-объектов и/или каталогов в ней.</span><span class="sxs-lookup"><span data-stu-id="01e63-143">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="01e63-144">широкий набор свойств и методов для возвращенной hello tooaccess **IListBlobItem**, необходимо привести tooa **CloudBlockBlob**, **CloudPageBlob**, или  **CloudBlobDirectory** объекта.</span><span class="sxs-lookup"><span data-stu-id="01e63-144">tooaccess hello rich set of properties and methods for a  returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="01e63-145">Если неизвестен тип hello, можно использовать проверку типа toodetermine какие toocast его.</span><span class="sxs-lookup"><span data-stu-id="01e63-145">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="01e63-146">Hello следующий код демонстрирует, как tooretrieve и вывод hello URI каждого элемента в hello **фотографии** контейнера:</span><span class="sxs-lookup"><span data-stu-id="01e63-146">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **photos** container:</span></span>

    // Loop over items within hello container and output hello length and URI.
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

<span data-ttu-id="01e63-147">Как показано в предыдущем образце кода hello hello BLOB-объектов имеет концепции hello каталогов в контейнерах, а также.</span><span class="sxs-lookup"><span data-stu-id="01e63-147">As shown in hello previous code sample, hello blob service has hello concept of directories within containers, as well.</span></span> <span data-ttu-id="01e63-148">Таким образом, можно организовать BLOB-объекты в структуре, похожей на папки.</span><span class="sxs-lookup"><span data-stu-id="01e63-148">This is so that you can organize your blobs in a more folder-like structure.</span></span> <span data-ttu-id="01e63-149">Например, рассмотрим следующий набор блочных больших двоичных объектов в контейнере с именем hello **фотографии**:</span><span class="sxs-lookup"><span data-stu-id="01e63-149">For example, consider hello following set of block blobs in a container named **photos**:</span></span>

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

<span data-ttu-id="01e63-150">При вызове **ListBlobs** в контейнере hello (как в предыдущем примере hello), содержит hello коллекция, возвращенная **CloudBlobDirectory** и **CloudBlockBlob** объектов представляющий hello каталоги и большие двоичные объекты, содержащиеся на верхнем уровне hello.</span><span class="sxs-lookup"><span data-stu-id="01e63-150">When you call **ListBlobs** on hello container (as in hello previous sample), hello collection returned contains **CloudBlobDirectory** and **CloudBlockBlob** objects representing hello directories and blobs contained at hello top level.</span></span> <span data-ttu-id="01e63-151">Ниже приведен результат hello:</span><span class="sxs-lookup"><span data-stu-id="01e63-151">Here is hello resulting output:</span></span>

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


<span data-ttu-id="01e63-152">При необходимости можно задать hello **UseFlatBlobListing** параметра hello **ListBlobs** метод **true**.</span><span class="sxs-lookup"><span data-stu-id="01e63-152">Optionally, you can set hello **UseFlatBlobListing** parameter of of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="01e63-153">Это приведет к возвращению каждого большого двоичного объекта в виде **CloudBlockBlob**независимо от того, какой каталог используется.</span><span class="sxs-lookup"><span data-stu-id="01e63-153">This results in every blob being returned as a **CloudBlockBlob**, regardless of directory.</span></span> <span data-ttu-id="01e63-154">Вот вызов hello слишком**ListBlobs**:</span><span class="sxs-lookup"><span data-stu-id="01e63-154">Here is hello call too**ListBlobs**:</span></span>

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

<span data-ttu-id="01e63-155">а вот hello результаты:</span><span class="sxs-lookup"><span data-stu-id="01e63-155">and here are hello results:</span></span>

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

<span data-ttu-id="01e63-156">Дополнительные сведения см. в описании метода [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span><span class="sxs-lookup"><span data-stu-id="01e63-156">For more information, see [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span></span>

## <a name="download-blobs"></a><span data-ttu-id="01e63-157">Скачивание больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="01e63-157">Download blobs</span></span>
<span data-ttu-id="01e63-158">toodownload больших двоичных объектов, сначала получить ссылку на большой двоичный объект, а затем вызвать hello **методов DownloadToStream** метод.</span><span class="sxs-lookup"><span data-stu-id="01e63-158">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="01e63-159">Hello следующий пример использует hello **методов DownloadToStream** метод tootransfer hello blob содержимое tooa объекта потока могут затем сохраняться tooa локального файла.</span><span class="sxs-lookup"><span data-stu-id="01e63-159">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

<span data-ttu-id="01e63-160">Можно также использовать hello **методов DownloadToStream** метод toodownload hello содержимое большого двоичного объекта в виде строки текста.</span><span class="sxs-lookup"><span data-stu-id="01e63-160">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a><span data-ttu-id="01e63-161">Удаление blob-объектов</span><span class="sxs-lookup"><span data-stu-id="01e63-161">Delete blobs</span></span>
<span data-ttu-id="01e63-162">toodelete большого двоичного объекта сначала получить ссылку на большой двоичный объект, а затем вызвать **удалить** метод.</span><span class="sxs-lookup"><span data-stu-id="01e63-162">toodelete a blob, first get a blob reference and then call the **Delete** method.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="01e63-163">Асинхронное перечисление BLOB-объектов в страницах</span><span class="sxs-lookup"><span data-stu-id="01e63-163">List blobs in pages asynchronously</span></span>
<span data-ttu-id="01e63-164">Если следует toocontrol hello число результатов, возвращаемых в одной операцией получения листинга списка большое количество больших двоичных объектов, можно перечислить большие двоичные объекты в страницы результатов.</span><span class="sxs-lookup"><span data-stu-id="01e63-164">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="01e63-165">Этот пример отображением tooreturn результатов на страницах асинхронно, так что выполнение не блокируются во время ожидания tooreturn большого набора результатов.</span><span class="sxs-lookup"><span data-stu-id="01e63-165">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="01e63-166">В этом примере показано плоский перечисления больших двоичных объектов, но можно также выполнить иерархический список, установка hello **useFlatBlobListing** параметр hello **ListBlobsSegmentedAsync** метод слишком **false**.</span><span class="sxs-lookup"><span data-stu-id="01e63-166">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello **useFlatBlobListing** parameter of hello **ListBlobsSegmentedAsync** method too**false**.</span></span>

<span data-ttu-id="01e63-167">Поскольку метод образец hello вызывает асинхронный метод, он должен предваряться символом hello **async** ключевое слово и он должен возвращать **задачи** объекта.</span><span class="sxs-lookup"><span data-stu-id="01e63-167">Because hello sample method calls an asynchronous method, it must be prefaced with hello **async** keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="01e63-168">Hello await-ключевое слово, указанный для hello **ListBlobsSegmentedAsync** метод приостанавливает выполнение метода образец hello до завершения выполнения задачи листинг hello.</span><span class="sxs-lookup"><span data-stu-id="01e63-168">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs toohello console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
        // When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
        do
        {
            // This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
            // or by calling a different overload.
            resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
            if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
            foreach (var blobItem in resultSegment.Results)
            {
                Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
            }
            Console.WriteLine();

            //Get hello continuation token.
            continuationToken = resultSegment.ContinuationToken;
        }
        while (continuationToken != null);
    }

## <a name="next-steps"></a><span data-ttu-id="01e63-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="01e63-169">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

