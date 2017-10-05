---
title: "Приступая к работе с хранилищем BLOB-объектов Azure (хранилищем объектов) с помощью .NET | Документация Майкрософт"
description: "Хранение неструктурированных данных в облаке в хранилище BLOB-объектов Azure."
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
ms.openlocfilehash: 70c7d6a5e1b9aa9a13481893e0baa56538be097c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a><span data-ttu-id="91f84-103">Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="91f84-103">Get started with Azure Blob storage using .NET</span></span>

[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

<span data-ttu-id="91f84-104">Хранилище BLOB-объектов Azure — это служба, которая хранит неструктурированные данные в облаке в качестве объектов или больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="91f84-104">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="91f84-105">В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений.</span><span class="sxs-lookup"><span data-stu-id="91f84-105">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="91f84-106">Хранилище BLOB-объектов иногда также называют хранилищем объектов.</span><span class="sxs-lookup"><span data-stu-id="91f84-106">Blob storage is also referred to as object storage.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="91f84-107">О данном учебнике</span><span class="sxs-lookup"><span data-stu-id="91f84-107">About this tutorial</span></span>
<span data-ttu-id="91f84-108">В этом руководстве показано, как написать код .NET для некоторых распространенных сценариев использования хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="91f84-108">This tutorial shows how to write .NET code for some common scenarios using Azure Blob storage.</span></span> <span data-ttu-id="91f84-109">Эти сценарии включают отправку, перечисление, загрузку и удаление больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="91f84-109">Scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

<span data-ttu-id="91f84-110">**Предварительные требования:**</span><span class="sxs-lookup"><span data-stu-id="91f84-110">**Prerequisites:**</span></span>

* [<span data-ttu-id="91f84-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="91f84-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/)
* [<span data-ttu-id="91f84-112">Клиентская библиотека хранилища Azure для .NET</span><span class="sxs-lookup"><span data-stu-id="91f84-112">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="91f84-113">Диспетчер конфигураций Azure для .NET</span><span class="sxs-lookup"><span data-stu-id="91f84-113">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="91f84-114">[учетная запись хранения Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="91f84-114">An [Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="91f84-115">Другие примеры</span><span class="sxs-lookup"><span data-stu-id="91f84-115">More samples</span></span>
<span data-ttu-id="91f84-116">Дополнительные примеры использования хранилища BLOB-объектов см. в статье [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) (Приступая к работе с хранилищем BLOB-объектов Azure в .NET).</span><span class="sxs-lookup"><span data-stu-id="91f84-116">For additional examples using Blob storage, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span> <span data-ttu-id="91f84-117">Вы можете скачать пример приложения и запустить его или просмотреть код на GitHub.</span><span class="sxs-lookup"><span data-stu-id="91f84-117">You can download the sample application and run it, or browse the code on GitHub.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="91f84-118">Добавление директив using</span><span class="sxs-lookup"><span data-stu-id="91f84-118">Add using directives</span></span>
<span data-ttu-id="91f84-119">Добавьте в верхнюю часть файла `Program.cs` следующие директивы **using**:</span><span class="sxs-lookup"><span data-stu-id="91f84-119">Add the following **using** directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="91f84-120">Анализ строки подключения</span><span class="sxs-lookup"><span data-stu-id="91f84-120">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-blob-service-client"></a><span data-ttu-id="91f84-121">Создание клиента службы BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="91f84-121">Create the Blob service client</span></span>
<span data-ttu-id="91f84-122">Класс **CloudBlobClient** позволяет извлекать контейнеры и большие двоичные объекты, которые хранятся в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="91f84-122">The **CloudBlobClient** class enables you to retrieve containers and blobs stored in Blob storage.</span></span> <span data-ttu-id="91f84-123">Вот один из способов создать клиента службы.</span><span class="sxs-lookup"><span data-stu-id="91f84-123">Here's one way to create the service client:</span></span>

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
<span data-ttu-id="91f84-124">Теперь вы можете написать код, который считывает и записывает данные в хранилище BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="91f84-124">Now you are ready to write code that reads data from and writes data to Blob storage.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="91f84-125">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="91f84-125">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="91f84-126">В этом примере показано, как создать контейнер:</span><span class="sxs-lookup"><span data-stu-id="91f84-126">This example shows how to create a container if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create the container if it doesn't already exist.
container.CreateIfNotExists();
```

<span data-ttu-id="91f84-127">По умолчанию новый контейнер является закрытым. Это значит, что вам нужно указать ключ доступа к хранилищу, чтобы загрузить большие двоичные объекты из этого контейнера.</span><span class="sxs-lookup"><span data-stu-id="91f84-127">By default, the new container is private, meaning that you must specify your storage access key to download blobs from this container.</span></span> <span data-ttu-id="91f84-128">Чтобы сделать файлы в этом контейнере доступными для всех пользователей, сделайте контейнер открытым, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="91f84-128">If you want to make the files within the container available to everyone, you can set the container to be public using the following code:</span></span>

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

<span data-ttu-id="91f84-129">Любой пользователь в Интернете может видеть BLOB-объекты в открытом контейнере,</span><span class="sxs-lookup"><span data-stu-id="91f84-129">Anyone on the Internet can see blobs in a public container.</span></span> <span data-ttu-id="91f84-130">но изменить или удалить их можно только при наличии ключа доступа или подписанного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="91f84-130">However, you can modify or delete them only if you have the appropriate account access key or a shared access signature.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="91f84-131">Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="91f84-131">Upload a blob into a container</span></span>
<span data-ttu-id="91f84-132">Хранилище BLOB-объектов Azure поддерживает блочные и страничные BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="91f84-132">Azure Blob Storage supports block blobs and page blobs.</span></span>  <span data-ttu-id="91f84-133">В большинстве случаев рекомендуется использовать блочные BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="91f84-133">In most cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="91f84-134">Для передачи файла в блочный BLOB-объект получите ссылку на контейнер и используйте ее для получения ссылки на блочный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="91f84-134">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="91f84-135">Получив ссылку на большой двоичный объект, вы можете отправить в него любой поток данных с помощью метода **UploadFromStream** .</span><span class="sxs-lookup"><span data-stu-id="91f84-135">Once you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStream** method.</span></span> <span data-ttu-id="91f84-136">Эта операция создает большой двоичный объект, если он не существует, или заменяет его, если он существует.</span><span class="sxs-lookup"><span data-stu-id="91f84-136">This operation creates the blob if it didn't previously exist, or overwrites it if it does exist.</span></span>

<span data-ttu-id="91f84-137">В следующем примере показано, как отправить BLOB-объект в контейнер. Предполагается, что контейнер уже был создан.</span><span class="sxs-lookup"><span data-stu-id="91f84-137">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "myblob".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

// Create or overwrite the "myblob" blob with contents from a local file.
using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
{
    blockBlob.UploadFromStream(fileStream);
}
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="91f84-138">Перечисление BLOB-объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="91f84-138">List the blobs in a container</span></span>
<span data-ttu-id="91f84-139">Для перечисления BLOB-объектов в контейнере сначала необходимо получить ссылку на контейнер.</span><span class="sxs-lookup"><span data-stu-id="91f84-139">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="91f84-140">Затем можно использовать метод **ListBlobs** контейнера, чтобы извлечь большие двоичные объекты и/или каталоги в нем.</span><span class="sxs-lookup"><span data-stu-id="91f84-140">You can then use the container's **ListBlobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="91f84-141">Для доступа к широкому набору свойств и методов возвращаемого объекта **IListBlobItem** необходимо преобразовать его в объект **CloudBlockBlob**, **CloudPageBlob** или **CloudBlobDirectory**.</span><span class="sxs-lookup"><span data-stu-id="91f84-141">To access the  rich set of properties and methods for a returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="91f84-142">Если тип неизвестен, можно использовать проверку типов, чтобы определить нужный тип.</span><span class="sxs-lookup"><span data-stu-id="91f84-142">If the type is unknown, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="91f84-143">Следующий код демонстрирует, как получить и вывести универсальный код ресурса (URI) каждого элемента в контейнере _photos_.</span><span class="sxs-lookup"><span data-stu-id="91f84-143">The following code demonstrates how to retrieve and output the URI of each item in the _photos_ container:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("photos");

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
```

<span data-ttu-id="91f84-144">Включив сведения о пути в имена BLOB-объектов, вы можете создать структуру виртуальных каталогов, которую можно организовывать и просматривать, как обычную файловую систему.</span><span class="sxs-lookup"><span data-stu-id="91f84-144">By including path information in blob names, you can create a virtual directory structure you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="91f84-145">Используется только структура виртуальных каталогов, так как единственные ресурсы, доступные в хранилище BLOB-объектов, — контейнеры и BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="91f84-145">The directory structure is virtual only--the only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="91f84-146">Тем не менее, в клиентской библиотеке хранилища содержится объект **CloudBlobDirectory** , который позволяет обратится к виртуальному каталогу и упростить процесс работы с большими двоичными объектами, упорядоченными таким образом.</span><span class="sxs-lookup"><span data-stu-id="91f84-146">However, the storage client library offers a **CloudBlobDirectory** object to refer to a virtual directory and simplify the process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="91f84-147">Для примера рассмотрим набор блочных BLOB-объектов в контейнере *photos*.</span><span class="sxs-lookup"><span data-stu-id="91f84-147">For example, consider the following set of block blobs in a container named *photos*:</span></span>

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

<span data-ttu-id="91f84-148">При вызове метода **ListBlobs** для контейнера *photos* (как в примере кода выше) возвращается иерархический список.</span><span class="sxs-lookup"><span data-stu-id="91f84-148">When you call **ListBlobs** on the *photos* container (as in the preceding code snippet), a hierarchical listing is returned.</span></span> <span data-ttu-id="91f84-149">Он содержит объекты **CloudBlobDirectory** и **CloudBlockBlob**, которые представляют собой каталоги и большие двоичные объекты в контейнере соответственно.</span><span class="sxs-lookup"><span data-stu-id="91f84-149">It contains both **CloudBlobDirectory** and **CloudBlockBlob** objects, representing the directories and blobs in the container, respectively.</span></span> <span data-ttu-id="91f84-150">Результат выглядит так:</span><span class="sxs-lookup"><span data-stu-id="91f84-150">The resulting output looks like:</span></span>

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

<span data-ttu-id="91f84-151">При необходимости можно установить для параметра **UseFlatBlobListing** метода **ListBlobs** значение **true**.</span><span class="sxs-lookup"><span data-stu-id="91f84-151">Optionally, you can set the **UseFlatBlobListing** parameter of the **ListBlobs** method to **true**.</span></span> <span data-ttu-id="91f84-152">В этом случае каждый большой двоичный объект в контейнере возвращается в виде объекта **CloudBlockBlob** .</span><span class="sxs-lookup"><span data-stu-id="91f84-152">In this case, every blob in the container is returned as a **CloudBlockBlob** object.</span></span> <span data-ttu-id="91f84-153">Вызов метода **ListBlobs** для возврата неструктурированного списка выглядит так:</span><span class="sxs-lookup"><span data-stu-id="91f84-153">The call to **ListBlobs** to return a flat listing looks like this:</span></span>

```csharp
// Loop over items within the container and output the length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

<span data-ttu-id="91f84-154">А результаты выглядят так:</span><span class="sxs-lookup"><span data-stu-id="91f84-154">and the results look like this:</span></span>

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

## <a name="download-blobs"></a><span data-ttu-id="91f84-155">Скачивание больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="91f84-155">Download blobs</span></span>
<span data-ttu-id="91f84-156">Для загрузки BLOB-объектов сначала нужно получить ссылку на BLOB-объект, а затем вызвать метод **DownloadToStream** .</span><span class="sxs-lookup"><span data-stu-id="91f84-156">To download blobs, first retrieve a blob reference and then call the **DownloadToStream** method.</span></span> <span data-ttu-id="91f84-157">В следующем примере метод **DownloadToStream** используется для переноса содержимого большого двоичного объекта в объект потока, который затем можно сохранить в локальном файле.</span><span class="sxs-lookup"><span data-stu-id="91f84-157">The following example uses the **DownloadToStream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "photo1.jpg".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

// Save blob contents to a file.
using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
{
    blockBlob.DownloadToStream(fileStream);
}
```

<span data-ttu-id="91f84-158">Можно также использовать метод **DownloadToStream** , чтобы загрузить содержимое BLOB-объекта как текстовую строку.</span><span class="sxs-lookup"><span data-stu-id="91f84-158">You can also use the **DownloadToStream** method to download the contents of a blob as a text string.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "myblob.txt"
CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

string text;
using (var memoryStream = new MemoryStream())
{
    blockBlob2.DownloadToStream(memoryStream);
    text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
}
```

## <a name="delete-blobs"></a><span data-ttu-id="91f84-159">Удаление blob-объектов</span><span class="sxs-lookup"><span data-stu-id="91f84-159">Delete blobs</span></span>
<span data-ttu-id="91f84-160">Чтобы удалить большой двоичный объект, сначала нужно получить ссылку на него, а затем вызвать метод **Delete** .</span><span class="sxs-lookup"><span data-stu-id="91f84-160">To delete a blob, first get a blob reference and then call the **Delete** method on it.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference to a previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference to a blob named "myblob.txt".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

// Delete the blob.
blockBlob.Delete();
```

## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="91f84-161">Асинхронное перечисление BLOB-объектов в страницах</span><span class="sxs-lookup"><span data-stu-id="91f84-161">List blobs in pages asynchronously</span></span>
<span data-ttu-id="91f84-162">Если вам нужно расположить большое количество BLOB-объектов или вы хотите управлять отображением количества объектов в результате запроса, вы можете задать расположение BLOB-объектов на странице.</span><span class="sxs-lookup"><span data-stu-id="91f84-162">If you are listing a large number of blobs, or you want to control the number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="91f84-163">В этом примере вы узнаете, как расположить запрошенные результаты на странице асинхронно для того, чтобы не блокировать выполнение задачи ожиданием большого объема возвращаемых данных.</span><span class="sxs-lookup"><span data-stu-id="91f84-163">This example shows how to return results in pages asynchronously, so that execution is not blocked while waiting to return a large set of results.</span></span>

<span data-ttu-id="91f84-164">В этом примере показано создание плоского списка больших двоичных объектов. Но вы также можете создать иерархический список, установив для параметра _useFlatBlobListing_ в методе **ListBlobsSegmentedAsync** значение _false_.</span><span class="sxs-lookup"><span data-stu-id="91f84-164">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting the _useFlatBlobListing_ parameter of the **ListBlobsSegmentedAsync** method to _false_.</span></span>

<span data-ttu-id="91f84-165">Так как метод из примера вызывает асинхронный метод, перед ним необходимо задать ключевое слово _async_. Это позволит вернуть объект **Task**.</span><span class="sxs-lookup"><span data-stu-id="91f84-165">Because the sample method calls an asynchronous method, it must be prefaced with the _async_ keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="91f84-166">При ожидании ключевого слова для **ListBlobsSegmentedAsync** метод приостанавливает выполнение примера до тех пор, пока задача размещения результатов не завершена.</span><span class="sxs-lookup"><span data-stu-id="91f84-166">The await keyword specified for the **ListBlobsSegmentedAsync** method suspends execution of the sample method until the listing task completes.</span></span>

```csharp
async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
{
    //List blobs to the console window, with paging.
    Console.WriteLine("List blobs in pages:");

    int i = 0;
    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate the result segment returned, while the continuation token is non-null.
    //When the continuation token is null, the last page has been returned and execution can exit the loop.
    do
    {
        //This overload allows control of the page size. You can return all remaining results by passing null for the maxResults parameter,
        //or by calling a different overload.
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
```

## <a name="writing-to-an-append-blob"></a><span data-ttu-id="91f84-167">Запись в расширенный большой двоичный объект</span><span class="sxs-lookup"><span data-stu-id="91f84-167">Writing to an append blob</span></span>
<span data-ttu-id="91f84-168">Добавочный большой двоичный объект оптимизирован для операций добавления, например ведения журналов.</span><span class="sxs-lookup"><span data-stu-id="91f84-168">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="91f84-169">Как и блочный BLOB-объект, добавочный большой двоичный объект состоит из блоков, но при добавлении нового блока в добавочный большой двоичный объект он всегда добавляется в конец этого объекта.</span><span class="sxs-lookup"><span data-stu-id="91f84-169">Like a block blob, an append blob is comprised of blocks, but when you add a new block to an append blob, it is always appended to the end of the blob.</span></span> <span data-ttu-id="91f84-170">Вы не можете обновить или удалить существующий блок в добавочном большом двоичном объекте.</span><span class="sxs-lookup"><span data-stu-id="91f84-170">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="91f84-171">Идентификаторы блоков в добавочном большом двоичном объекте не отображаются, как в блочном BLOB-объекте.</span><span class="sxs-lookup"><span data-stu-id="91f84-171">The block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="91f84-172">Каждый блок в добавочном большом двоичном объекте может иметь разный размер (не более 4 МБ), кроме того, добавочный большой двоичный объект может содержать не более 50 000 блоков.</span><span class="sxs-lookup"><span data-stu-id="91f84-172">Each block in an append blob can be a different size, up to a maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="91f84-173">Таким образом, максимальный размер добавочного большого двоичного объекта немного превышает 195 ГБ (4 МБ X 50 000 блоков).</span><span class="sxs-lookup"><span data-stu-id="91f84-173">The maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="91f84-174">Приведенный ниже пример создает новый добавочный большой двоичный объект и добавляет в него некоторые данные, имитируя простые операции ведение журнала.</span><span class="sxs-lookup"><span data-stu-id="91f84-174">The example below creates a new append blob and appends some data to it, simulating a simple logging operation.</span></span>

```csharp
//Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

//Create service client for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("my-append-blobs");

//Create the container if it does not already exist.
container.CreateIfNotExists();

//Get a reference to an append blob.
CloudAppendBlob appendBlob = container.GetAppendBlobReference("append-blob.log");

//Create the append blob. Note that if the blob already exists, the CreateOrReplace() method will overwrite it.
//You can check whether the blob exists to avoid overwriting it by using CloudAppendBlob.Exists().
appendBlob.CreateOrReplace();

int numBlocks = 10;

//Generate an array of random bytes.
Random rnd = new Random();
byte[] bytes = new byte[numBlocks];
rnd.NextBytes(bytes);

//Simulate a logging operation by writing text data and byte data to the end of the append blob.
for (int i = 0; i < numBlocks; i++)
{
    appendBlob.AppendText(String.Format("Timestamp: {0:u} \tLog Entry: {1}{2}",
        DateTime.UtcNow, bytes[i], Environment.NewLine));
}

//Read the append blob to the console window.
Console.WriteLine(appendBlob.DownloadText());
```

<span data-ttu-id="91f84-175">Дополнительные сведения о различиях между тремя типами больших двоичных объектов см. в статье [Основные сведения о блочных, страничных и добавочных BLOB-объектах](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span><span class="sxs-lookup"><span data-stu-id="91f84-175">See [Understanding Block Blobs, Page Blobs, and Append Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) for more information about the differences between the three types of blobs.</span></span>

## <a name="managing-security-for-blobs"></a><span data-ttu-id="91f84-176">Управление системой безопасности больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="91f84-176">Managing security for blobs</span></span>
<span data-ttu-id="91f84-177">По умолчанию служба хранилища Azure защищает данные, ограничивая доступ к учетной записи пользователя, который владеет ключами доступа к учетной записи.</span><span class="sxs-lookup"><span data-stu-id="91f84-177">By default, Azure Storage keeps your data secure by limiting access to the account owner, who is in possession of the account access keys.</span></span> <span data-ttu-id="91f84-178">Если вы хотите предоставить доступ к данным больших двоичных объектов в своей учетной записи хранения, важно сделать это без ущерба для безопасности ключей доступа к учетной записи.</span><span class="sxs-lookup"><span data-stu-id="91f84-178">When you need to share blob data in your storage account, it is important to do so without compromising the security of your account access keys.</span></span> <span data-ttu-id="91f84-179">Кроме того, вы можете зашифровать данные больших двоичных объектов, чтобы обеспечить их безопасную отправку по сети в службу хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="91f84-179">Additionally, you can encrypt blob data to ensure that it is secure going over the wire and in Azure Storage.</span></span>

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-to-blob-data"></a><span data-ttu-id="91f84-180">Управление доступом к данным больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="91f84-180">Controlling access to blob data</span></span>
<span data-ttu-id="91f84-181">По умолчанию данные больших двоичных объектов в учетной записи хранения доступны только владельцу учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="91f84-181">By default, the blob data in your storage account is accessible only to storage account owner.</span></span> <span data-ttu-id="91f84-182">По умолчанию для проверки подлинности запросов к хранилищу BLOB-объектов требуется ключ доступа к учетной записи.</span><span class="sxs-lookup"><span data-stu-id="91f84-182">Authenticating requests against Blob storage requires the account access key by default.</span></span> <span data-ttu-id="91f84-183">Но вы можете предоставить другим пользователям доступ к некоторым данным больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="91f84-183">However, you may wish to make certain blob data available to other users.</span></span> <span data-ttu-id="91f84-184">Существует два варианта.</span><span class="sxs-lookup"><span data-stu-id="91f84-184">You have two options:</span></span>

* <span data-ttu-id="91f84-185">**Анонимный доступ**. Вы можете предоставить общий анонимный доступ к контейнеру или его большим двоичным объектам.</span><span class="sxs-lookup"><span data-stu-id="91f84-185">**Anonymous access:** You can make a container or its blobs publicly available for anonymous access.</span></span> <span data-ttu-id="91f84-186">Дополнительные сведения см. в статье [Управление анонимным доступом на чтение к контейнерам и большим двоичным объектам](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="91f84-186">See [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="91f84-187">**Подписанные URL-адреса**. Вы можете предоставить клиентам подписанный URL-адрес (SAS), который обеспечивает делегированный доступ к ресурсу в вашей учетной записи хранения. Для этого доступа вы можете указать разрешения и интервал времени доступа.</span><span class="sxs-lookup"><span data-stu-id="91f84-187">**Shared access signatures:** You can provide clients with a shared access signature (SAS), which provides delegated access to a resource in your storage account, with permissions that you specify and over an interval that you specify.</span></span> <span data-ttu-id="91f84-188">Дополнительные сведения см. в статье [Использование подписанных URL-адресов (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="91f84-188">See [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

### <a name="encrypting-blob-data"></a><span data-ttu-id="91f84-189">Шифрование данных больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="91f84-189">Encrypting blob data</span></span>
<span data-ttu-id="91f84-190">Служба хранилища Azure поддерживает шифрование больших двоичных объектов данных на стороне клиента и сервера:</span><span class="sxs-lookup"><span data-stu-id="91f84-190">Azure Storage supports encrypting blob data both at the client and on the server:</span></span>

* <span data-ttu-id="91f84-191">**Шифрование на стороне клиента**. Клиентская библиотека службы хранилища для .NET поддерживает шифрование данных в клиентских приложениях перед их отправкой в службу хранилища Azure и расшифровку данных во время скачивания на клиент.</span><span class="sxs-lookup"><span data-stu-id="91f84-191">**Client-side encryption:** The Storage Client Library for .NET supports encrypting data within client applications before uploading to Azure Storage, and decrypting data while downloading to the client.</span></span> <span data-ttu-id="91f84-192">Библиотека также поддерживает интеграцию с хранилищем ключей Azure для управления ключами учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="91f84-192">The library also supports integration with Azure Key Vault for storage account key management.</span></span> <span data-ttu-id="91f84-193">Дополнительные сведения см. в статье [Шифрование на стороне клиента для службы хранилища Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="91f84-193">See [Client-Side Encryption with .NET for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span> <span data-ttu-id="91f84-194">Кроме того, см. сведения в статье [Шифрование и расшифровка BLOB-объектов в хранилище Microsoft Azure с помощью хранилища ключей Azure](storage-encrypt-decrypt-blobs-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="91f84-194">Also see [Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).</span></span>
* <span data-ttu-id="91f84-195">**Шифрование на стороне сервера**. Служба хранилища Azure теперь поддерживает шифрование на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="91f84-195">**Server-side encryption**: Azure Storage now supports server-side encryption.</span></span> <span data-ttu-id="91f84-196">См. статью [Шифрование службы хранилища Azure для неактивных данных (предварительная версия)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="91f84-196">See [Azure Storage Service Encryption for Data at Rest (Preview)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="91f84-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="91f84-197">Next steps</span></span>
<span data-ttu-id="91f84-198">Вы ознакомились с базовыми понятиями о хранилище BLOB-объектов. Дополнительные сведения см. по следующим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="91f84-198">Now that you've learned the basics of Blob storage, follow these links to learn more.</span></span>

### <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="91f84-199">Обозреватель службы хранилища Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="91f84-199">Microsoft Azure Storage Explorer</span></span>
* <span data-ttu-id="91f84-200">[Обозреватель хранилищ Microsoft Azure (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md) — это бесплатное автономное приложение от корпорации Майкрософт, позволяющее визуализировать данные из службы хранилища Azure на платформе Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="91f84-200">[Microsoft Azure Storage Explorer (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

### <a name="blob-storage-samples"></a><span data-ttu-id="91f84-201">Примеры для хранилища BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="91f84-201">Blob storage samples</span></span>
* [<span data-ttu-id="91f84-202">Getting Started with Azure Blob Storage in .NET (Приступая к работе с хранилищем BLOB-объектов Azure в .NET)</span><span class="sxs-lookup"><span data-stu-id="91f84-202">Getting Started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a><span data-ttu-id="91f84-203">Справочная документация по хранилищу BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="91f84-203">Blob storage reference</span></span>
* [<span data-ttu-id="91f84-204">Справочник по клиентской библиотеке хранилища для .NET</span><span class="sxs-lookup"><span data-stu-id="91f84-204">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [<span data-ttu-id="91f84-205">Справочник по REST API</span><span class="sxs-lookup"><span data-stu-id="91f84-205">REST API reference</span></span>](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a><span data-ttu-id="91f84-206">Основные рекомендации</span><span class="sxs-lookup"><span data-stu-id="91f84-206">Conceptual guides</span></span>
* [<span data-ttu-id="91f84-207">Приступая к работе со служебной программой командной строки AzCopy</span><span class="sxs-lookup"><span data-stu-id="91f84-207">Transfer data with the AzCopy command-line utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="91f84-208">Приступая к работе с хранилищем файлов для .NET</span><span class="sxs-lookup"><span data-stu-id="91f84-208">Get started with File storage for .NET</span></span>](../files/storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="91f84-209">Использование хранилища больших двоичных объектов Azure с пакетом SDK веб-заданий</span><span class="sxs-lookup"><span data-stu-id="91f84-209">How to use Azure blob storage with the WebJobs SDK</span></span>](../../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
