---
title: "aaaGet к работе с хранилищем больших двоичных объектов Azure (хранилище объектов), с помощью .NET | Документы Microsoft"
description: "Храните неструктурированные данные в облаке hello с хранилищем больших двоичных объектов Azure (хранилище объектов)."
services: storage
documentationcenter: .net
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: d18a8fc8-97cb-4d37-a408-a6f8107ea8b3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: marsma
ms.openlocfilehash: 9b675ac073e7e901fe1afe54f7bfea12eefbf3ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a><span data-ttu-id="032ce-103">Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="032ce-103">Get started with Azure Blob storage using .NET</span></span>

[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

<span data-ttu-id="032ce-104">Хранилище больших двоичных объектов Azure — это служба, неструктурированные данные хранятся в облаке hello как большие двоичные объекты и объекты.</span><span class="sxs-lookup"><span data-stu-id="032ce-104">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="032ce-105">В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений.</span><span class="sxs-lookup"><span data-stu-id="032ce-105">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="032ce-106">Хранилище больших двоичных объектов также является ссылка tooas объекта хранилища.</span><span class="sxs-lookup"><span data-stu-id="032ce-106">Blob storage is also referred tooas object storage.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="032ce-107">О данном учебнике</span><span class="sxs-lookup"><span data-stu-id="032ce-107">About this tutorial</span></span>
<span data-ttu-id="032ce-108">В этом учебнике показано, как toowrite .NET кода в некоторых распространенных сценариях, с помощью хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="032ce-108">This tutorial shows how toowrite .NET code for some common scenarios using Azure Blob storage.</span></span> <span data-ttu-id="032ce-109">Эти сценарии включают отправку, перечисление, загрузку и удаление больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="032ce-109">Scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

<span data-ttu-id="032ce-110">**Предварительные требования:**</span><span class="sxs-lookup"><span data-stu-id="032ce-110">**Prerequisites:**</span></span>

* [<span data-ttu-id="032ce-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="032ce-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/)
* [<span data-ttu-id="032ce-112">Клиентская библиотека хранилища Azure для .NET</span><span class="sxs-lookup"><span data-stu-id="032ce-112">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="032ce-113">Диспетчер конфигураций Azure для .NET</span><span class="sxs-lookup"><span data-stu-id="032ce-113">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="032ce-114">[учетная запись хранения Azure](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="032ce-114">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="032ce-115">Другие примеры</span><span class="sxs-lookup"><span data-stu-id="032ce-115">More samples</span></span>
<span data-ttu-id="032ce-116">Дополнительные примеры использования хранилища BLOB-объектов см. в статье [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) (Приступая к работе с хранилищем BLOB-объектов Azure в .NET).</span><span class="sxs-lookup"><span data-stu-id="032ce-116">For additional examples using Blob storage, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span> <span data-ttu-id="032ce-117">Можно загрузить пример приложения hello и запустите его или просмотр кода hello в GitHub.</span><span class="sxs-lookup"><span data-stu-id="032ce-117">You can download hello sample application and run it, or browse hello code on GitHub.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="032ce-118">Добавление директив using</span><span class="sxs-lookup"><span data-stu-id="032ce-118">Add using directives</span></span>
<span data-ttu-id="032ce-119">Добавьте следующее hello **с помощью** директивы toohello вверху hello `Program.cs` файла:</span><span class="sxs-lookup"><span data-stu-id="032ce-119">Add hello following **using** directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="032ce-120">Синтаксический анализ строки соединения hello</span><span class="sxs-lookup"><span data-stu-id="032ce-120">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-blob-service-client"></a><span data-ttu-id="032ce-121">Создание клиента службы BLOB-объектов hello</span><span class="sxs-lookup"><span data-stu-id="032ce-121">Create hello Blob service client</span></span>
<span data-ttu-id="032ce-122">Hello **CloudBlobClient** класс позволяет tooretrieve контейнеры и большие двоичные объекты, хранящиеся в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="032ce-122">hello **CloudBlobClient** class enables you tooretrieve containers and blobs stored in Blob storage.</span></span> <span data-ttu-id="032ce-123">Вот один из способов toocreate hello службы клиента.</span><span class="sxs-lookup"><span data-stu-id="032ce-123">Here's one way toocreate hello service client:</span></span>

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
<span data-ttu-id="032ce-124">Теперь все готово toowrite код, который считывает и записывает tooBlob хранения данных.</span><span class="sxs-lookup"><span data-stu-id="032ce-124">Now you are ready toowrite code that reads data from and writes data tooBlob storage.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="032ce-125">Создать контейнер</span><span class="sxs-lookup"><span data-stu-id="032ce-125">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="032ce-126">В этом примере показано, как toocreate контейнера, если он еще не существует:</span><span class="sxs-lookup"><span data-stu-id="032ce-126">This example shows how toocreate a container if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it doesn't already exist.
container.CreateIfNotExists();
```

<span data-ttu-id="032ce-127">По умолчанию hello новый контейнер является закрытым, это означает, что необходимо указать хранилища доступа ключа toodownload BLOB-объектов из этого контейнера.</span><span class="sxs-lookup"><span data-stu-id="032ce-127">By default, hello new container is private, meaning that you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="032ce-128">Если файлы toomake hello в пределах доступных tooeveryone hello контейнера, можно задать toobe контейнера hello общим с помощью hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="032ce-128">If you want toomake hello files within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

<span data-ttu-id="032ce-129">Всем пользователям в Интернете hello можно увидеть в открытый контейнер BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="032ce-129">Anyone on hello Internet can see blobs in a public container.</span></span> <span data-ttu-id="032ce-130">Тем не менее можно изменить или удалить их только в том случае, если у вас есть ключ доступа hello соответствующей учетной записи или подписанный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="032ce-130">However, you can modify or delete them only if you have hello appropriate account access key or a shared access signature.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="032ce-131">Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="032ce-131">Upload a blob into a container</span></span>
<span data-ttu-id="032ce-132">Хранилище BLOB-объектов Azure поддерживает блочные и страничные BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="032ce-132">Azure Blob Storage supports block blobs and page blobs.</span></span>  <span data-ttu-id="032ce-133">В большинстве случаев блочного BLOB-объекта — hello, рекомендуется toouse типа.</span><span class="sxs-lookup"><span data-stu-id="032ce-133">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="032ce-134">большой двоичный объект блока файла tooa tooupload получить ссылку на контейнер и использовать его tooget ссылку на большой двоичный объект блока.</span><span class="sxs-lookup"><span data-stu-id="032ce-134">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="032ce-135">Получив ссылку на большой двоичный объект можно передать любой поток данных tooit с вызывающему Привет **UploadFromStream** метод.</span><span class="sxs-lookup"><span data-stu-id="032ce-135">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="032ce-136">Эта операция создает hello большого двоичного объекта, если он не был найден ранее, или перезаписывает его, если он существует.</span><span class="sxs-lookup"><span data-stu-id="032ce-136">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span>

<span data-ttu-id="032ce-137">Следующий пример показывает как Hello tooupload большого двоичного объекта в контейнер и предполагается hello контейнера уже был создан.</span><span class="sxs-lookup"><span data-stu-id="032ce-137">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

// Create or overwrite hello "myblob" blob with contents from a local file.
using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
{
    blockBlob.UploadFromStream(fileStream);
}
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="032ce-138">Перечисление hello больших двоичных объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="032ce-138">List hello blobs in a container</span></span>
<span data-ttu-id="032ce-139">toolist hello BLOB-объектов в контейнере, сначала нужно получить ссылку на контейнер.</span><span class="sxs-lookup"><span data-stu-id="032ce-139">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="032ce-140">Затем можно использовать контейнер hello **ListBlobs** метод tooretrieve hello BLOB-объектов и/или каталогов в ней.</span><span class="sxs-lookup"><span data-stu-id="032ce-140">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="032ce-141">широкий набор свойств и методов для возвращенной hello tooaccess **IListBlobItem**, необходимо привести tooa **CloudBlockBlob**, **CloudPageBlob**, или  **CloudBlobDirectory** объекта.</span><span class="sxs-lookup"><span data-stu-id="032ce-141">tooaccess hello  rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="032ce-142">Если неизвестен тип hello, можно использовать проверку типа toodetermine какие toocast его.</span><span class="sxs-lookup"><span data-stu-id="032ce-142">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="032ce-143">Hello следующий код демонстрирует, как tooretrieve и вывод hello URI каждого элемента в hello _фотографии_ контейнера:</span><span class="sxs-lookup"><span data-stu-id="032ce-143">hello following code demonstrates how tooretrieve and output hello URI of each item in hello _photos_ container:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("photos");

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
```

<span data-ttu-id="032ce-144">Включив сведения о пути в имена BLOB-объектов, вы можете создать структуру виртуальных каталогов, которую можно организовывать и просматривать, как обычную файловую систему.</span><span class="sxs-lookup"><span data-stu-id="032ce-144">By including path information in blob names, you can create a virtual directory structure you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="032ce-145">Структура каталогов Hello является виртуальным только--hello только доступные ресурсы в хранилище больших двоичных объектов, контейнеры и большие двоичные объекты.</span><span class="sxs-lookup"><span data-stu-id="032ce-145">hello directory structure is virtual only--hello only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="032ce-146">Однако клиентская библиотека хранилища hello предлагает **CloudBlobDirectory** объекта виртуального каталога tooa toorefer и упростить процесс работы с большими двоичными объектами, которые упорядочены таким образом hello.</span><span class="sxs-lookup"><span data-stu-id="032ce-146">However, hello storage client library offers a **CloudBlobDirectory** object toorefer tooa virtual directory and simplify hello process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="032ce-147">Например, рассмотрим следующий набор блочных больших двоичных объектов в контейнере с именем hello *фотографии*:</span><span class="sxs-lookup"><span data-stu-id="032ce-147">For example, consider hello following set of block blobs in a container named *photos*:</span></span>

```
photo1.jpg
2010/architecture/description.txt
2010/architecture/photo3.jpg
2010/architecture/photo4.jpg
2011/architecture/photo5.jpg
2011/architecture/photo6.jpg
2011/architecture/description.txt
2011/photo7.jpg
```

<span data-ttu-id="032ce-148">При вызове **ListBlobs** на hello *фотографии* контейнера (как hello предшествующий фрагмент кода), возвращается иерархический список.</span><span class="sxs-lookup"><span data-stu-id="032ce-148">When you call **ListBlobs** on hello *photos* container (as in hello preceding code snippet), a hierarchical listing is returned.</span></span> <span data-ttu-id="032ce-149">Он содержит оба **CloudBlobDirectory** и **CloudBlockBlob** объекты, представляющие каталоги hello и большие двоичные объекты в контейнере hello соответственно.</span><span class="sxs-lookup"><span data-stu-id="032ce-149">It contains both **CloudBlobDirectory** and **CloudBlockBlob** objects, representing hello directories and blobs in hello container, respectively.</span></span> <span data-ttu-id="032ce-150">выходные данные, полученные Hello выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="032ce-150">hello resulting output looks like:</span></span>

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

<span data-ttu-id="032ce-151">При необходимости можно задать hello **UseFlatBlobListing** параметр hello **ListBlobs** метод **true**.</span><span class="sxs-lookup"><span data-stu-id="032ce-151">Optionally, you can set hello **UseFlatBlobListing** parameter of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="032ce-152">В этом случае каждый большой двоичный объект в контейнере hello возвращается в виде **CloudBlockBlob** объекта.</span><span class="sxs-lookup"><span data-stu-id="032ce-152">In this case, every blob in hello container is returned as a **CloudBlockBlob** object.</span></span> <span data-ttu-id="032ce-153">Здравствуйте вызов слишком**ListBlobs** tooreturn плоском листинге выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="032ce-153">hello call too**ListBlobs** tooreturn a flat listing looks like this:</span></span>

```csharp
// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

<span data-ttu-id="032ce-154">и hello результаты выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="032ce-154">and hello results look like this:</span></span>

```
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

## <a name="download-blobs"></a><span data-ttu-id="032ce-155">Скачивание больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="032ce-155">Download blobs</span></span>
<span data-ttu-id="032ce-156">toodownload больших двоичных объектов, сначала получить ссылку на большой двоичный объект, а затем вызвать hello **методов DownloadToStream** метод.</span><span class="sxs-lookup"><span data-stu-id="032ce-156">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="032ce-157">Hello следующий пример использует hello **методов DownloadToStream** метод tootransfer hello blob содержимое tooa объекта потока могут затем сохраняться tooa локального файла.</span><span class="sxs-lookup"><span data-stu-id="032ce-157">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "photo1.jpg".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

// Save blob contents tooa file.
using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
{
    blockBlob.DownloadToStream(fileStream);
}
```

<span data-ttu-id="032ce-158">Можно также использовать hello **методов DownloadToStream** метод toodownload hello содержимое большого двоичного объекта в виде строки текста.</span><span class="sxs-lookup"><span data-stu-id="032ce-158">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt"
CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

string text;
using (var memoryStream = new MemoryStream())
{
    blockBlob2.DownloadToStream(memoryStream);
    text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
}
```

## <a name="delete-blobs"></a><span data-ttu-id="032ce-159">Удаление blob-объектов</span><span class="sxs-lookup"><span data-stu-id="032ce-159">Delete blobs</span></span>
<span data-ttu-id="032ce-160">toodelete большого двоичного объекта сначала получить ссылку на большой двоичный объект, а затем вызвать **удалить** метода.</span><span class="sxs-lookup"><span data-stu-id="032ce-160">toodelete a blob, first get a blob reference and then call the **Delete** method on it.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

// Delete hello blob.
blockBlob.Delete();
```

## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="032ce-161">Асинхронное перечисление BLOB-объектов в страницах</span><span class="sxs-lookup"><span data-stu-id="032ce-161">List blobs in pages asynchronously</span></span>
<span data-ttu-id="032ce-162">Если следует toocontrol hello число результатов, возвращаемых в одной операцией получения листинга списка большое количество больших двоичных объектов, можно перечислить большие двоичные объекты в страницы результатов.</span><span class="sxs-lookup"><span data-stu-id="032ce-162">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="032ce-163">Этот пример отображением tooreturn результатов на страницах асинхронно, так что выполнение не блокируются во время ожидания tooreturn большого набора результатов.</span><span class="sxs-lookup"><span data-stu-id="032ce-163">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="032ce-164">В этом примере показано плоский перечисления больших двоичных объектов, но можно также выполнить иерархический список, установка hello _useFlatBlobListing_ параметр hello **ListBlobsSegmentedAsync** too_false_ метод.</span><span class="sxs-lookup"><span data-stu-id="032ce-164">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello _useFlatBlobListing_ parameter of hello **ListBlobsSegmentedAsync** method too_false_.</span></span>

<span data-ttu-id="032ce-165">Поскольку метод образец hello вызывает асинхронный метод, он должен предваряться символом hello _async_ ключевое слово и он должен возвращать **задачи** объекта.</span><span class="sxs-lookup"><span data-stu-id="032ce-165">Because hello sample method calls an asynchronous method, it must be prefaced with hello _async_ keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="032ce-166">Hello await-ключевое слово, указанный для hello **ListBlobsSegmentedAsync** метод приостанавливает выполнение метода образец hello до завершения выполнения задачи листинг hello.</span><span class="sxs-lookup"><span data-stu-id="032ce-166">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

```csharp
async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
{
    //List blobs toohello console window, with paging.
    Console.WriteLine("List blobs in pages:");

    int i = 0;
    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
    //When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
    do
    {
        //This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
        //or by calling a different overload.
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
```

## <a name="writing-tooan-append-blob"></a><span data-ttu-id="032ce-167">Написание tooan append больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="032ce-167">Writing tooan append blob</span></span>
<span data-ttu-id="032ce-168">Добавочный большой двоичный объект оптимизирован для операций добавления, например ведения журналов.</span><span class="sxs-lookup"><span data-stu-id="032ce-168">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="032ce-169">Как большой двоичный объект блока добавочный BLOB-объект состоит из блоков, но при добавлении нового большого двоичного объекта tooan append блок, это всегда присоединенных toohello конец hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="032ce-169">Like a block blob, an append blob is comprised of blocks, but when you add a new block tooan append blob, it is always appended toohello end of hello blob.</span></span> <span data-ttu-id="032ce-170">Вы не можете обновить или удалить существующий блок в добавочном большом двоичном объекте.</span><span class="sxs-lookup"><span data-stu-id="032ce-170">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="032ce-171">Идентификаторы блокировок Hello для добавочный большой двоичный объект не отображаются, как и для большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="032ce-171">hello block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="032ce-172">Каждый блок в добавочный большой двоичный объект может быть разный размер копии tooa более 4 Мбайт и добавочный большой двоичный объект может содержать не более 50 000 блоков.</span><span class="sxs-lookup"><span data-stu-id="032ce-172">Each block in an append blob can be a different size, up tooa maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="032ce-173">Максимальный размер Hello добавочный большой двоичный объект таким образом — немного более 195 ГБ (4 МБ X 50 000 блоков).</span><span class="sxs-lookup"><span data-stu-id="032ce-173">hello maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="032ce-174">Hello приведенном ниже примере создается новый добавочный большой двоичный объект и добавляет tooit некоторых данных, имитируя операция простого ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="032ce-174">hello example below creates a new append blob and appends some data tooit, simulating a simple logging operation.</span></span>

```csharp
//Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

//Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("my-append-blobs");

//Create hello container if it does not already exist.
container.CreateIfNotExists();

//Get a reference tooan append blob.
CloudAppendBlob appendBlob = container.GetAppendBlobReference("append-blob.log");

//Create hello append blob. Note that if hello blob already exists, hello CreateOrReplace() method will overwrite it.
//You can check whether hello blob exists tooavoid overwriting it by using CloudAppendBlob.Exists().
appendBlob.CreateOrReplace();

int numBlocks = 10;

//Generate an array of random bytes.
Random rnd = new Random();
byte[] bytes = new byte[numBlocks];
rnd.NextBytes(bytes);

//Simulate a logging operation by writing text data and byte data toohello end of hello append blob.
for (int i = 0; i < numBlocks; i++)
{
    appendBlob.AppendText(String.Format("Timestamp: {0:u} \tLog Entry: {1}{2}",
        DateTime.UtcNow, bytes[i], Environment.NewLine));
}

//Read hello append blob toohello console window.
Console.WriteLine(appendBlob.DownloadText());
```

<span data-ttu-id="032ce-175">В разделе [основные сведения о блочных, страничные большие двоичные объекты и добавьте большие двоичные объекты](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) Дополнительные сведения об отличиях hello hello три типа больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="032ce-175">See [Understanding Block Blobs, Page Blobs, and Append Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) for more information about hello differences between hello three types of blobs.</span></span>

## <a name="managing-security-for-blobs"></a><span data-ttu-id="032ce-176">Управление системой безопасности больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="032ce-176">Managing security for blobs</span></span>
<span data-ttu-id="032ce-177">По умолчанию хранилища Azure защищает ваши данные, ограничивая доступ toohello учетной записи владельца, являющегося владеющим hello ключей доступа учетных записей.</span><span class="sxs-lookup"><span data-stu-id="032ce-177">By default, Azure Storage keeps your data secure by limiting access toohello account owner, who is in possession of hello account access keys.</span></span> <span data-ttu-id="032ce-178">При необходимости данные большого двоичного объекта tooshare вашей учетной записи хранилища является важным toodo так без риска для безопасности hello ключей доступа к вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="032ce-178">When you need tooshare blob data in your storage account, it is important toodo so without compromising hello security of your account access keys.</span></span> <span data-ttu-id="032ce-179">Кроме того вы можете зашифровать tooensure данные большого двоичного объекта, безопасность, перейдя по сети hello и в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="032ce-179">Additionally, you can encrypt blob data tooensure that it is secure going over hello wire and in Azure Storage.</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-tooblob-data"></a><span data-ttu-id="032ce-180">Управление tooblob доступа к данным</span><span class="sxs-lookup"><span data-stu-id="032ce-180">Controlling access tooblob data</span></span>
<span data-ttu-id="032ce-181">По умолчанию hello данные большого двоичного объекта в учетной записи — доступны только владелец учетной записи toostorage.</span><span class="sxs-lookup"><span data-stu-id="032ce-181">By default, hello blob data in your storage account is accessible only toostorage account owner.</span></span> <span data-ttu-id="032ce-182">Проверка подлинности запросов в службу хранилища больших двоичных объектов требуется hello ключ доступа учетной записи по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="032ce-182">Authenticating requests against Blob storage requires hello account access key by default.</span></span> <span data-ttu-id="032ce-183">Тем не менее, вы можете toomake определенных пользователей доступны tooother данных больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="032ce-183">However, you may wish toomake certain blob data available tooother users.</span></span> <span data-ttu-id="032ce-184">Существует два варианта.</span><span class="sxs-lookup"><span data-stu-id="032ce-184">You have two options:</span></span>

* <span data-ttu-id="032ce-185">**Анонимный доступ**. Вы можете предоставить общий анонимный доступ к контейнеру или его большим двоичным объектам.</span><span class="sxs-lookup"><span data-stu-id="032ce-185">**Anonymous access:** You can make a container or its blobs publicly available for anonymous access.</span></span> <span data-ttu-id="032ce-186">В разделе [управления toocontainers анонимный доступ для чтения и большие двоичные объекты](storage-manage-access-to-resources.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="032ce-186">See [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="032ce-187">**Подписи коллективного доступа:** подписанного URL-адреса (SAS), предоставляющий ресурс tooa делегированный доступ в учетной записи с разрешениями, указываемые и за определенный интервал времени, указываемое могут предоставить клиентам.</span><span class="sxs-lookup"><span data-stu-id="032ce-187">**Shared access signatures:** You can provide clients with a shared access signature (SAS), which provides delegated access tooa resource in your storage account, with permissions that you specify and over an interval that you specify.</span></span> <span data-ttu-id="032ce-188">Дополнительные сведения см. в статье [Использование подписанных URL-адресов (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="032ce-188">See [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) for more information.</span></span>

### <a name="encrypting-blob-data"></a><span data-ttu-id="032ce-189">Шифрование данных больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="032ce-189">Encrypting blob data</span></span>
<span data-ttu-id="032ce-190">Хранилище Azure поддерживает шифрование данных больших двоичных объектов как на приветствия клиента, так и на сервере hello:</span><span class="sxs-lookup"><span data-stu-id="032ce-190">Azure Storage supports encrypting blob data both at hello client and on hello server:</span></span>

* <span data-ttu-id="032ce-191">**Шифрование на стороне клиента:** hello клиентской библиотеки хранилища для .NET поддерживает шифрование данных в клиентские приложения перед загрузкой tooAzure хранилища и расшифровки данных при загрузке toohello клиента.</span><span class="sxs-lookup"><span data-stu-id="032ce-191">**Client-side encryption:** hello Storage Client Library for .NET supports encrypting data within client applications before uploading tooAzure Storage, and decrypting data while downloading toohello client.</span></span> <span data-ttu-id="032ce-192">Библиотека Hello также поддерживает интеграцию с хранилищем ключей Azure для управления ключами учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="032ce-192">hello library also supports integration with Azure Key Vault for storage account key management.</span></span> <span data-ttu-id="032ce-193">Дополнительные сведения см. в статье [Шифрование на стороне клиента для службы хранилища Microsoft Azure](storage-client-side-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="032ce-193">See [Client-Side Encryption with .NET for Microsoft Azure Storage](storage-client-side-encryption.md) for more information.</span></span> <span data-ttu-id="032ce-194">Кроме того, см. сведения в статье [Шифрование и расшифровка BLOB-объектов в хранилище Microsoft Azure с помощью хранилища ключей Azure](storage-encrypt-decrypt-blobs-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="032ce-194">Also see [Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).</span></span>
* <span data-ttu-id="032ce-195">**Шифрование на стороне сервера**. Служба хранилища Azure теперь поддерживает шифрование на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="032ce-195">**Server-side encryption**: Azure Storage now supports server-side encryption.</span></span> <span data-ttu-id="032ce-196">См. статью [Шифрование службы хранилища Azure для неактивных данных (предварительная версия)](storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="032ce-196">See [Azure Storage Service Encryption for Data at Rest (Preview)](storage-service-encryption.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="032ce-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="032ce-197">Next steps</span></span>
<span data-ttu-id="032ce-198">Теперь, когда вы узнали основы hello хранилища больших двоичных объектов, выполните следующие дополнительные toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="032ce-198">Now that you've learned hello basics of Blob storage, follow these links toolearn more.</span></span>

### <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="032ce-199">Обозреватель службы хранилища Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="032ce-199">Microsoft Azure Storage Explorer</span></span>
* <span data-ttu-id="032ce-200">[Обозреватель хранилища Microsoft Azure (MASE)](../vs-azure-tools-storage-manage-with-storage-explorer.md) является бесплатной, отдельное приложение от Майкрософт, позволяющая toowork визуально с помощью данных из хранилища Azure в Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="032ce-200">[Microsoft Azure Storage Explorer (MASE)](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

### <a name="blob-storage-samples"></a><span data-ttu-id="032ce-201">Примеры для хранилища BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="032ce-201">Blob storage samples</span></span>
* [<span data-ttu-id="032ce-202">Getting Started with Azure Blob Storage in .NET (Приступая к работе с хранилищем BLOB-объектов Azure в .NET)</span><span class="sxs-lookup"><span data-stu-id="032ce-202">Getting Started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a><span data-ttu-id="032ce-203">Справочная документация по хранилищу BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="032ce-203">Blob storage reference</span></span>
* [<span data-ttu-id="032ce-204">Справочник по клиентской библиотеке хранилища для .NET</span><span class="sxs-lookup"><span data-stu-id="032ce-204">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [<span data-ttu-id="032ce-205">Справочник по REST API</span><span class="sxs-lookup"><span data-stu-id="032ce-205">REST API reference</span></span>](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a><span data-ttu-id="032ce-206">Основные рекомендации</span><span class="sxs-lookup"><span data-stu-id="032ce-206">Conceptual guides</span></span>
* [<span data-ttu-id="032ce-207">Перенесите данные с помощью командной строки программу AzCopy hello</span><span class="sxs-lookup"><span data-stu-id="032ce-207">Transfer data with hello AzCopy command-line utility</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="032ce-208">Приступая к работе с хранилищем файлов для .NET</span><span class="sxs-lookup"><span data-stu-id="032ce-208">Get started with File storage for .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="032ce-209">Как toouse Azure хранилище больших двоичных объектов с hello SDK веб-заданий</span><span class="sxs-lookup"><span data-stu-id="032ce-209">How toouse Azure blob storage with hello WebJobs SDK</span></span>](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
