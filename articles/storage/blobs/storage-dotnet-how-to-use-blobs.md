---
title: "Приступая к работе с хранилищем BLOB-объектов Azure (хранилищем объектов) с помощью .NET | Документация Майкрософт"
description: "Хранение неструктурированных данных в облаке в хранилище BLOB-объектов Azure."
services: storage
documentationcenter: .net
author: tamram
manager: timlt
editor: tysonn
ms.assetid: d18a8fc8-97cb-4d37-a408-a6f8107ea8b3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: tamram
ms.openlocfilehash: 87594d2688e3cd01f5e7db8f5be8ca513969e774
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a>Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET

[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

Хранилище BLOB-объектов Azure — это служба, которая хранит неструктурированные данные в облаке в качестве объектов или больших двоичных объектов. В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений. Хранилище BLOB-объектов иногда также называют хранилищем объектов.

### <a name="about-this-tutorial"></a>О данном учебнике
В этом руководстве показано, как написать код .NET для некоторых распространенных сценариев использования хранилища BLOB-объектов Azure. Эти сценарии включают отправку, перечисление, загрузку и удаление больших двоичных объектов.

**Предварительные требования:**

* [Microsoft Visual Studio](https://www.visualstudio.com/)
* [Клиентская библиотека хранилища Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Диспетчер конфигураций Azure для .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [учетная запись хранения Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a>Другие примеры
Дополнительные примеры использования хранилища BLOB-объектов см. в статье [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) (Приступая к работе с хранилищем BLOB-объектов Azure в .NET). Вы можете скачать пример приложения и запустить его или просмотреть код на GitHub.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Добавление директив using
Добавьте в верхнюю часть файла `Program.cs` следующие директивы **using**:

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-the-connection-string"></a>Анализ строки подключения
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-blob-service-client"></a>Создание клиента службы BLOB-объектов
Класс **CloudBlobClient** позволяет извлекать контейнеры и большие двоичные объекты, которые хранятся в хранилище BLOB-объектов. Вот один из способов создать клиента службы.

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
Теперь вы можете написать код, который считывает и записывает данные в хранилище BLOB-объектов.

## <a name="create-a-container"></a>Создание контейнера
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

В этом примере показано, как создать контейнер:

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

По умолчанию новый контейнер является закрытым. Это значит, что вам нужно указать ключ доступа к хранилищу, чтобы загрузить большие двоичные объекты из этого контейнера. Чтобы сделать файлы в этом контейнере доступными для всех пользователей, сделайте контейнер открытым, используя следующий код:

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

Любой пользователь в Интернете может видеть BLOB-объекты в открытом контейнере, но изменить или удалить их можно только при наличии ключа доступа или подписанного URL-адреса.

## <a name="upload-a-blob-into-a-container"></a>Отправка BLOB-объекта в контейнер
Хранилище BLOB-объектов Azure поддерживает блочные и страничные BLOB-объекты.  В большинстве случаев рекомендуется использовать блочные BLOB-объекты.

Для передачи файла в блочный BLOB-объект получите ссылку на контейнер и используйте ее для получения ссылки на блочный BLOB-объект. Получив ссылку на большой двоичный объект, вы можете отправить в него любой поток данных с помощью метода **UploadFromStream** . Эта операция создает большой двоичный объект, если он не существует, или заменяет его, если он существует.

В следующем примере показано, как отправить BLOB-объект в контейнер. Предполагается, что контейнер уже был создан.

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

## <a name="list-the-blobs-in-a-container"></a>Перечисление BLOB-объектов в контейнере
Для перечисления BLOB-объектов в контейнере сначала необходимо получить ссылку на контейнер. Затем можно использовать метод **ListBlobs** контейнера, чтобы извлечь большие двоичные объекты и/или каталоги в нем. Для доступа к широкому набору свойств и методов возвращаемого объекта **IListBlobItem** необходимо преобразовать его в объект **CloudBlockBlob**, **CloudPageBlob** или **CloudBlobDirectory**. Если тип неизвестен, можно использовать проверку типов, чтобы определить нужный тип. Следующий код демонстрирует, как получить и вывести универсальный код ресурса (URI) каждого элемента в контейнере _photos_.

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

Включив сведения о пути в имена BLOB-объектов, вы можете создать структуру виртуальных каталогов, которую можно организовывать и просматривать, как обычную файловую систему. Используется только структура виртуальных каталогов, так как единственные ресурсы, доступные в хранилище BLOB-объектов, — контейнеры и BLOB-объекты. Тем не менее, в клиентской библиотеке хранилища содержится объект **CloudBlobDirectory** , который позволяет обратится к виртуальному каталогу и упростить процесс работы с большими двоичными объектами, упорядоченными таким образом.

Для примера рассмотрим набор блочных BLOB-объектов в контейнере *photos*.

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

При вызове метода **ListBlobs** для контейнера *photos* (как в примере кода выше) возвращается иерархический список. Он содержит объекты **CloudBlobDirectory** и **CloudBlockBlob**, которые представляют собой каталоги и большие двоичные объекты в контейнере соответственно. Результат выглядит так:

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

При необходимости можно установить для параметра **UseFlatBlobListing** метода **ListBlobs** значение **true**. В этом случае каждый большой двоичный объект в контейнере возвращается в виде объекта **CloudBlockBlob** . Вызов метода **ListBlobs** для возврата неструктурированного списка выглядит так:

```csharp
// Loop over items within the container and output the length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

А результаты выглядят так:

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

## <a name="download-blobs"></a>Скачивание больших двоичных объектов
Для загрузки BLOB-объектов сначала нужно получить ссылку на BLOB-объект, а затем вызвать метод **DownloadToStream** . В следующем примере метод **DownloadToStream** используется для переноса содержимого большого двоичного объекта в объект потока, который затем можно сохранить в локальном файле.

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

Можно также использовать метод **DownloadToStream** , чтобы загрузить содержимое BLOB-объекта как текстовую строку.

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

## <a name="delete-blobs"></a>Удаление blob-объектов
Чтобы удалить большой двоичный объект, сначала нужно получить ссылку на него, а затем вызвать метод **Delete** .

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

## <a name="list-blobs-in-pages-asynchronously"></a>Асинхронное перечисление BLOB-объектов в страницах
Если вам нужно расположить большое количество BLOB-объектов или вы хотите управлять отображением количества объектов в результате запроса, вы можете задать расположение BLOB-объектов на странице. В этом примере вы узнаете, как расположить запрошенные результаты на странице асинхронно для того, чтобы не блокировать выполнение задачи ожиданием большого объема возвращаемых данных.

В этом примере показано создание плоского списка больших двоичных объектов. Но вы также можете создать иерархический список, установив для параметра _useFlatBlobListing_ в методе **ListBlobsSegmentedAsync** значение _false_.

Так как метод из примера вызывает асинхронный метод, перед ним необходимо задать ключевое слово _async_. Это позволит вернуть объект **Task**. При ожидании ключевого слова для **ListBlobsSegmentedAsync** метод приостанавливает выполнение примера до тех пор, пока задача размещения результатов не завершена.

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

## <a name="writing-to-an-append-blob"></a>Запись в расширенный большой двоичный объект
Добавочный большой двоичный объект оптимизирован для операций добавления, например ведения журналов. Как и блочный BLOB-объект, добавочный большой двоичный объект состоит из блоков, но при добавлении нового блока в добавочный большой двоичный объект он всегда добавляется в конец этого объекта. Вы не можете обновить или удалить существующий блок в добавочном большом двоичном объекте. Идентификаторы блоков в добавочном большом двоичном объекте не отображаются, как в блочном BLOB-объекте.

Каждый блок в добавочном большом двоичном объекте может иметь разный размер (не более 4 МБ), кроме того, добавочный большой двоичный объект может содержать не более 50 000 блоков. Таким образом, максимальный размер добавочного большого двоичного объекта немного превышает 195 ГБ (4 МБ X 50 000 блоков).

Приведенный ниже пример создает новый добавочный большой двоичный объект и добавляет в него некоторые данные, имитируя простые операции ведение журнала.

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

Дополнительные сведения о различиях между тремя типами больших двоичных объектов см. в статье [Основные сведения о блочных, страничных и добавочных BLOB-объектах](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).

## <a name="managing-security-for-blobs"></a>Управление системой безопасности больших двоичных объектов
По умолчанию служба хранилища Azure защищает данные, ограничивая доступ к учетной записи пользователя, который владеет ключами доступа к учетной записи. Если вы хотите предоставить доступ к данным больших двоичных объектов в своей учетной записи хранения, важно сделать это без ущерба для безопасности ключей доступа к учетной записи. Кроме того, вы можете зашифровать данные больших двоичных объектов, чтобы обеспечить их безопасную отправку по сети в службу хранилища Azure.

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-to-blob-data"></a>Управление доступом к данным больших двоичных объектов
По умолчанию данные больших двоичных объектов в учетной записи хранения доступны только владельцу учетной записи хранения. По умолчанию для проверки подлинности запросов к хранилищу BLOB-объектов требуется ключ доступа к учетной записи. Но вы можете предоставить другим пользователям доступ к некоторым данным больших двоичных объектов. Существует два варианта.

* **Анонимный доступ**. Вы можете предоставить общий анонимный доступ к контейнеру или его большим двоичным объектам. Дополнительные сведения см. в статье [Управление анонимным доступом на чтение к контейнерам и большим двоичным объектам](storage-manage-access-to-resources.md).
* **Подписанные URL-адреса**. Вы можете предоставить клиентам подписанный URL-адрес (SAS), который обеспечивает делегированный доступ к ресурсу в вашей учетной записи хранения. Для этого доступа вы можете указать разрешения и интервал времени доступа. Дополнительные сведения см. в статье [Использование подписанных URL-адресов (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

### <a name="encrypting-blob-data"></a>Шифрование данных больших двоичных объектов
Служба хранилища Azure поддерживает шифрование больших двоичных объектов данных на стороне клиента и сервера:

* **Шифрование на стороне клиента**. Клиентская библиотека службы хранилища для .NET поддерживает шифрование данных в клиентских приложениях перед их отправкой в службу хранилища Azure и расшифровку данных во время скачивания на клиент. Библиотека также поддерживает интеграцию с хранилищем ключей Azure для управления ключами учетной записи хранения. Дополнительные сведения см. в статье [Шифрование на стороне клиента для службы хранилища Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json). Кроме того, см. сведения в статье [Шифрование и расшифровка BLOB-объектов в хранилище Microsoft Azure с помощью хранилища ключей Azure](storage-encrypt-decrypt-blobs-key-vault.md).
* **Шифрование на стороне сервера**. Служба хранилища Azure теперь поддерживает шифрование на стороне сервера. См. статью [Шифрование службы хранилища Azure для неактивных данных (предварительная версия)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

## <a name="next-steps"></a>Дальнейшие действия
Вы ознакомились с базовыми понятиями о хранилище BLOB-объектов. Дополнительные сведения см. по следующим ссылкам.

### <a name="microsoft-azure-storage-explorer"></a>Обозреватель службы хранилища Microsoft Azure
* [Обозреватель хранилищ Microsoft Azure (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md) — это бесплатное автономное приложение от корпорации Майкрософт, позволяющее визуализировать данные из службы хранилища Azure на платформе Windows, macOS и Linux.

### <a name="blob-storage-samples"></a>Примеры для хранилища BLOB-объектов
* [Getting Started with Azure Blob Storage in .NET (Приступая к работе с хранилищем BLOB-объектов Azure в .NET)](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a>Справочная документация по хранилищу BLOB-объектов
* [Справочник по клиентской библиотеке хранилища для .NET](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [Справочник по REST API](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a>Основные рекомендации
* [Приступая к работе со служебной программой командной строки AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [Приступая к работе с хранилищем файлов для .NET](../files/storage-dotnet-how-to-use-files.md)
* [Использование хранилища больших двоичных объектов Azure с пакетом SDK веб-заданий](https://github.com/Azure/azure-webjobs-sdk/wiki)
