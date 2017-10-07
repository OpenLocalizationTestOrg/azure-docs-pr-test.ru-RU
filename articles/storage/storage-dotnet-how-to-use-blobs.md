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
# <a name="get-started-with-azure-blob-storage-using-net"></a>Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET

[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

Хранилище больших двоичных объектов Azure — это служба, неструктурированные данные хранятся в облаке hello как большие двоичные объекты и объекты. В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений. Хранилище больших двоичных объектов также является ссылка tooas объекта хранилища.

### <a name="about-this-tutorial"></a>О данном учебнике
В этом учебнике показано, как toowrite .NET кода в некоторых распространенных сценариях, с помощью хранилища больших двоичных объектов Azure. Эти сценарии включают отправку, перечисление, загрузку и удаление больших двоичных объектов.

**Предварительные требования:**

* [Microsoft Visual Studio](https://www.visualstudio.com/)
* [Клиентская библиотека хранилища Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Диспетчер конфигураций Azure для .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [учетная запись хранения Azure](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a>Другие примеры
Дополнительные примеры использования хранилища BLOB-объектов см. в статье [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/) (Приступая к работе с хранилищем BLOB-объектов Azure в .NET). Можно загрузить пример приложения hello и запустите его или просмотр кода hello в GitHub.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Добавление директив using
Добавьте следующее hello **с помощью** директивы toohello вверху hello `Program.cs` файла:

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-hello-connection-string"></a>Синтаксический анализ строки соединения hello
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-blob-service-client"></a>Создание клиента службы BLOB-объектов hello
Hello **CloudBlobClient** класс позволяет tooretrieve контейнеры и большие двоичные объекты, хранящиеся в хранилище больших двоичных объектов. Вот один из способов toocreate hello службы клиента.

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
Теперь все готово toowrite код, который считывает и записывает tooBlob хранения данных.

## <a name="create-a-container"></a>Создать контейнер
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

В этом примере показано, как toocreate контейнера, если он еще не существует:

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

По умолчанию hello новый контейнер является закрытым, это означает, что необходимо указать хранилища доступа ключа toodownload BLOB-объектов из этого контейнера. Если файлы toomake hello в пределах доступных tooeveryone hello контейнера, можно задать toobe контейнера hello общим с помощью hello, следующий код:

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

Всем пользователям в Интернете hello можно увидеть в открытый контейнер BLOB-объектов. Тем не менее можно изменить или удалить их только в том случае, если у вас есть ключ доступа hello соответствующей учетной записи или подписанный URL-адрес.

## <a name="upload-a-blob-into-a-container"></a>Отправка BLOB-объекта в контейнер
Хранилище BLOB-объектов Azure поддерживает блочные и страничные BLOB-объекты.  В большинстве случаев блочного BLOB-объекта — hello, рекомендуется toouse типа.

большой двоичный объект блока файла tooa tooupload получить ссылку на контейнер и использовать его tooget ссылку на большой двоичный объект блока. Получив ссылку на большой двоичный объект можно передать любой поток данных tooit с вызывающему Привет **UploadFromStream** метод. Эта операция создает hello большого двоичного объекта, если он не был найден ранее, или перезаписывает его, если он существует.

Следующий пример показывает как Hello tooupload большого двоичного объекта в контейнер и предполагается hello контейнера уже был создан.

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

## <a name="list-hello-blobs-in-a-container"></a>Перечисление hello больших двоичных объектов в контейнере
toolist hello BLOB-объектов в контейнере, сначала нужно получить ссылку на контейнер. Затем можно использовать контейнер hello **ListBlobs** метод tooretrieve hello BLOB-объектов и/или каталогов в ней. широкий набор свойств и методов для возвращенной hello tooaccess **IListBlobItem**, необходимо привести tooa **CloudBlockBlob**, **CloudPageBlob**, или  **CloudBlobDirectory** объекта. Если неизвестен тип hello, можно использовать проверку типа toodetermine какие toocast его. Hello следующий код демонстрирует, как tooretrieve и вывод hello URI каждого элемента в hello _фотографии_ контейнера:

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

Включив сведения о пути в имена BLOB-объектов, вы можете создать структуру виртуальных каталогов, которую можно организовывать и просматривать, как обычную файловую систему. Структура каталогов Hello является виртуальным только--hello только доступные ресурсы в хранилище больших двоичных объектов, контейнеры и большие двоичные объекты. Однако клиентская библиотека хранилища hello предлагает **CloudBlobDirectory** объекта виртуального каталога tooa toorefer и упростить процесс работы с большими двоичными объектами, которые упорядочены таким образом hello.

Например, рассмотрим следующий набор блочных больших двоичных объектов в контейнере с именем hello *фотографии*:

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

При вызове **ListBlobs** на hello *фотографии* контейнера (как hello предшествующий фрагмент кода), возвращается иерархический список. Он содержит оба **CloudBlobDirectory** и **CloudBlockBlob** объекты, представляющие каталоги hello и большие двоичные объекты в контейнере hello соответственно. выходные данные, полученные Hello выглядит следующим образом.

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

При необходимости можно задать hello **UseFlatBlobListing** параметр hello **ListBlobs** метод **true**. В этом случае каждый большой двоичный объект в контейнере hello возвращается в виде **CloudBlockBlob** объекта. Здравствуйте вызов слишком**ListBlobs** tooreturn плоском листинге выглядит следующим образом:

```csharp
// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

и hello результаты выглядят следующим образом:

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
toodownload больших двоичных объектов, сначала получить ссылку на большой двоичный объект, а затем вызвать hello **методов DownloadToStream** метод. Hello следующий пример использует hello **методов DownloadToStream** метод tootransfer hello blob содержимое tooa объекта потока могут затем сохраняться tooa локального файла.

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

Можно также использовать hello **методов DownloadToStream** метод toodownload hello содержимое большого двоичного объекта в виде строки текста.

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

## <a name="delete-blobs"></a>Удаление blob-объектов
toodelete большого двоичного объекта сначала получить ссылку на большой двоичный объект, а затем вызвать **удалить** метода.

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

## <a name="list-blobs-in-pages-asynchronously"></a>Асинхронное перечисление BLOB-объектов в страницах
Если следует toocontrol hello число результатов, возвращаемых в одной операцией получения листинга списка большое количество больших двоичных объектов, можно перечислить большие двоичные объекты в страницы результатов. Этот пример отображением tooreturn результатов на страницах асинхронно, так что выполнение не блокируются во время ожидания tooreturn большого набора результатов.

В этом примере показано плоский перечисления больших двоичных объектов, но можно также выполнить иерархический список, установка hello _useFlatBlobListing_ параметр hello **ListBlobsSegmentedAsync** too_false_ метод.

Поскольку метод образец hello вызывает асинхронный метод, он должен предваряться символом hello _async_ ключевое слово и он должен возвращать **задачи** объекта. Hello await-ключевое слово, указанный для hello **ListBlobsSegmentedAsync** метод приостанавливает выполнение метода образец hello до завершения выполнения задачи листинг hello.

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

## <a name="writing-tooan-append-blob"></a>Написание tooan append больших двоичных объектов
Добавочный большой двоичный объект оптимизирован для операций добавления, например ведения журналов. Как большой двоичный объект блока добавочный BLOB-объект состоит из блоков, но при добавлении нового большого двоичного объекта tooan append блок, это всегда присоединенных toohello конец hello большого двоичного объекта. Вы не можете обновить или удалить существующий блок в добавочном большом двоичном объекте. Идентификаторы блокировок Hello для добавочный большой двоичный объект не отображаются, как и для большого двоичного объекта.

Каждый блок в добавочный большой двоичный объект может быть разный размер копии tooa более 4 Мбайт и добавочный большой двоичный объект может содержать не более 50 000 блоков. Максимальный размер Hello добавочный большой двоичный объект таким образом — немного более 195 ГБ (4 МБ X 50 000 блоков).

Hello приведенном ниже примере создается новый добавочный большой двоичный объект и добавляет tooit некоторых данных, имитируя операция простого ведения журнала.

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

В разделе [основные сведения о блочных, страничные большие двоичные объекты и добавьте большие двоичные объекты](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) Дополнительные сведения об отличиях hello hello три типа больших двоичных объектов.

## <a name="managing-security-for-blobs"></a>Управление системой безопасности больших двоичных объектов
По умолчанию хранилища Azure защищает ваши данные, ограничивая доступ toohello учетной записи владельца, являющегося владеющим hello ключей доступа учетных записей. При необходимости данные большого двоичного объекта tooshare вашей учетной записи хранилища является важным toodo так без риска для безопасности hello ключей доступа к вашей учетной записи. Кроме того вы можете зашифровать tooensure данные большого двоичного объекта, безопасность, перейдя по сети hello и в хранилище Azure.

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-tooblob-data"></a>Управление tooblob доступа к данным
По умолчанию hello данные большого двоичного объекта в учетной записи — доступны только владелец учетной записи toostorage. Проверка подлинности запросов в службу хранилища больших двоичных объектов требуется hello ключ доступа учетной записи по умолчанию. Тем не менее, вы можете toomake определенных пользователей доступны tooother данных больших двоичных объектов. Существует два варианта.

* **Анонимный доступ**. Вы можете предоставить общий анонимный доступ к контейнеру или его большим двоичным объектам. В разделе [управления toocontainers анонимный доступ для чтения и большие двоичные объекты](storage-manage-access-to-resources.md) для получения дополнительной информации.
* **Подписи коллективного доступа:** подписанного URL-адреса (SAS), предоставляющий ресурс tooa делегированный доступ в учетной записи с разрешениями, указываемые и за определенный интервал времени, указываемое могут предоставить клиентам. Дополнительные сведения см. в статье [Использование подписанных URL-адресов (SAS)](storage-dotnet-shared-access-signature-part-1.md).

### <a name="encrypting-blob-data"></a>Шифрование данных больших двоичных объектов
Хранилище Azure поддерживает шифрование данных больших двоичных объектов как на приветствия клиента, так и на сервере hello:

* **Шифрование на стороне клиента:** hello клиентской библиотеки хранилища для .NET поддерживает шифрование данных в клиентские приложения перед загрузкой tooAzure хранилища и расшифровки данных при загрузке toohello клиента. Библиотека Hello также поддерживает интеграцию с хранилищем ключей Azure для управления ключами учетной записи хранилища. Дополнительные сведения см. в статье [Шифрование на стороне клиента для службы хранилища Microsoft Azure](storage-client-side-encryption.md). Кроме того, см. сведения в статье [Шифрование и расшифровка BLOB-объектов в хранилище Microsoft Azure с помощью хранилища ключей Azure](storage-encrypt-decrypt-blobs-key-vault.md).
* **Шифрование на стороне сервера**. Служба хранилища Azure теперь поддерживает шифрование на стороне сервера. См. статью [Шифрование службы хранилища Azure для неактивных данных (предварительная версия)](storage-service-encryption.md).

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello хранилища больших двоичных объектов, выполните следующие дополнительные toolearn ссылки.

### <a name="microsoft-azure-storage-explorer"></a>Обозреватель службы хранилища Microsoft Azure
* [Обозреватель хранилища Microsoft Azure (MASE)](../vs-azure-tools-storage-manage-with-storage-explorer.md) является бесплатной, отдельное приложение от Майкрософт, позволяющая toowork визуально с помощью данных из хранилища Azure в Windows, macOS и Linux.

### <a name="blob-storage-samples"></a>Примеры для хранилища BLOB-объектов
* [Getting Started with Azure Blob Storage in .NET (Приступая к работе с хранилищем BLOB-объектов Azure в .NET)](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a>Справочная документация по хранилищу BLOB-объектов
* [Справочник по клиентской библиотеке хранилища для .NET](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [Справочник по REST API](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a>Основные рекомендации
* [Перенесите данные с помощью командной строки программу AzCopy hello](storage-use-azcopy.md)
* [Приступая к работе с хранилищем файлов для .NET](storage-dotnet-how-to-use-files.md)
* [Как toouse Azure хранилище больших двоичных объектов с hello SDK веб-заданий](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
