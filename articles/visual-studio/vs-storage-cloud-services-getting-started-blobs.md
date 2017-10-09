---
title: "aaaGet работы с Visual Studio и хранилище больших двоичных объектов подключенных служб (облачных служб) | Документы Microsoft"
description: "Как tooget запущена с помощью хранилища больших двоичных объектов Azure в проект облачной службы в Visual Studio после подключения tooa учетной записи хранилища с помощью Visual Studio подключенные службы"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 158197a9d49bc4f26841d689405529192c52f529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Начало работы с хранилищем больших двоичных объектов Azure и подключенными службами Visual Studio (проектами облачных служб)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Обзор
В этой статье описывается, как tooget работу с BLOB-хранилища Azure, после создания или ссылка на учетную запись хранилища Azure с помощью Visual Studio hello **Добавление подключенных служб** диалогового окна в облаке Visual Studio проект служб. Мы покажем, как tooaccess и создание контейнеров больших двоичных объектов и как tooperform общих задач и отправка, вывод и загрузка больших двоичных объектов. Hello примеры на языке C\# и использовать hello [клиентская библиотека хранилища Microsoft Azure для .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Хранилище Azure BLOB-объекта — это служба для хранения больших объемов неструктурированных данных, который может осуществляться из любого места в Здравствуй, мир! через HTTP или HTTPS. Один большой двоичный объект может быть любого размера. Большими двоичными объектами могут быть изображения, аудио- и видеофайлы, необработанные данные и файлы документов.

Так же как файлы располагаются в папках, большие двоичные объекты хранилища располагаются в контейнерах. После создания хранилища, можно создать один или несколько контейнеров в хранилище hello. Например в хранилище, вызывается буферный «файл», контейнеров можно создать в хранилище hello, называется «images» toostore изображения и вызывается другой toostore «звук» звуковые файлы. После создания hello контейнеры, можно передать файлы toothem отдельных больших двоичных объектов.

* Дополнительные сведения о программных операциях с большими двоичными объектами см. в статье [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).
* Общие сведения о службе хранилища Azure см. в [документации по службе хранилища](https://azure.microsoft.com/documentation/services/storage/).
* Общие сведения об облачных службах Azure см. в [документации по облачным службам](https://azure.microsoft.com/documentation/services/cloud-services/).
* Дополнительные сведения о программировании для приложений ASP.NET см. в разделе [ASP.NET](http://www.asp.net).

## <a name="access-blob-containers-in-code"></a>Доступ к контейнерам больших двоичных объектов в коде
tooprogrammatically доступа к большим двоичным объектам в проектах облачных служб, необходимо tooadd hello следующих элементов, в том случае, если они еще не существует.

1. Добавьте следующий код объявления пространства имен toohello начало любой файл C#, в котором вы хотите tooprogrammatically доступа хранилища Azure hello.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Получите объект **CloudStorageAccount** , представляющий данные учетной записи хранения. Hello используйте следующий код tooget hello хранения строки соединения и сведения об учетной записи хранилища из конфигурации службы Azure hello.
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. Получить **CloudBlobClient** объекта tooreference существующий контейнер в вашей учетной записи хранилища.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. Получить **CloudBlobContainer** объекта tooreference конкретного BLOB-контейнере.
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> Используйте все hello код, показанный в предыдущей процедуре hello перед hello код, показываемый в следующих разделах hello.
> 
> 

## <a name="create-a-container-in-code"></a>Создание контейнера в коде
> [!NOTE]
> Некоторые интерфейсы API, выполняющие вызовы out tooAzure хранилища в ASP.NET является асинхронным. Дополнительные сведения см. в статье [Asynchronous Programming with async and await (C#)](http://msdn.microsoft.com/library/hh191443.aspx) (Асинхронное программирование с использованием ключевых слов Async и Await (C#)). Hello кода hello следующий пример предполагает, что вы используете асинхронные методы программирования.
> 
> 

toocreate контейнера в учетной записи хранения, все, что нужно toodo добавить вызов слишком**CreateIfNotExistsAsync** как hello, следующий код:

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


toomake файлов hello в доступных tooeveryone hello контейнера, можно задать toobe контейнера hello открытый с помощью hello, следующий код.

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


Всем пользователям в Интернете hello можно увидеть в открытый контейнер BLOB-объектов, но можно изменить или удалить их только в том случае, если у вас есть ключ hello соответствующие права доступа.

## <a name="upload-a-blob-into-a-container"></a>Отправка BLOB-объекта в контейнер
Хранилище BLOB-объектов Azure поддерживает блочные и страничные BLOB-объекты. В большинстве случаев hello блочного BLOB-объекта — hello, рекомендуется toouse типа.

большой двоичный объект блока файла tooa tooupload получить ссылку на контейнер и использовать его tooget ссылку на большой двоичный объект блока. Получив ссылку на большой двоичный объект можно передать любой поток данных tooit с вызывающему Привет **UploadFromStream** метод. Эта операция создает hello большого двоичного объекта, если он не был найден ранее, или перезаписывает его, если он существует. Следующий пример показывает как Hello tooupload большого двоичного объекта в контейнер и предполагается hello контейнера уже был создан.

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>Перечисление hello больших двоичных объектов в контейнере
toolist hello BLOB-объектов в контейнере, сначала нужно получить ссылку на контейнер. Затем можно использовать контейнер hello **ListBlobs** метод tooretrieve hello BLOB-объектов и/или каталогов в ней. широкий набор свойств и методов для возвращенной hello tooaccess **IListBlobItem**, необходимо привести tooa **CloudBlockBlob**, **CloudPageBlob**, или  **CloudBlobDirectory** объекта. Если неизвестен тип hello, можно использовать проверку типа toodetermine какие toocast его. Hello следующий код демонстрирует, как tooretrieve и вывод hello URI каждого элемента в hello **фотографии** контейнера:

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

Как показано в предыдущем образце кода hello hello BLOB-объектов имеет концепции hello каталогов в контейнерах, а также. Таким образом, можно организовать BLOB-объекты в структуре, похожей на папки. Например, рассмотрим следующий набор блочных больших двоичных объектов в контейнере с именем hello **фотографии**:

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

При вызове **ListBlobs** в контейнере hello (как в предыдущем примере hello), содержит hello коллекция, возвращенная **CloudBlobDirectory** и **CloudBlockBlob** объектов представляющий hello каталоги и большие двоичные объекты, содержащиеся на верхнем уровне hello. Ниже приведен результат hello:

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


При необходимости можно задать hello **UseFlatBlobListing** параметра hello **ListBlobs** метод **true**. Это приведет к возвращению каждого большого двоичного объекта в виде **CloudBlockBlob**независимо от того, какой каталог используется. Вот вызов hello слишком**ListBlobs**:

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

а вот hello результаты:

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

Дополнительные сведения см. в описании метода [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).

## <a name="download-blobs"></a>Скачивание больших двоичных объектов
toodownload больших двоичных объектов, сначала получить ссылку на большой двоичный объект, а затем вызвать hello **методов DownloadToStream** метод. Hello следующий пример использует hello **методов DownloadToStream** метод tootransfer hello blob содержимое tooa объекта потока могут затем сохраняться tooa локального файла.

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

Можно также использовать hello **методов DownloadToStream** метод toodownload hello содержимое большого двоичного объекта в виде строки текста.

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a>Удаление blob-объектов
toodelete большого двоичного объекта сначала получить ссылку на большой двоичный объект, а затем вызвать **удалить** метод.

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a>Асинхронное перечисление BLOB-объектов в страницах
Если следует toocontrol hello число результатов, возвращаемых в одной операцией получения листинга списка большое количество больших двоичных объектов, можно перечислить большие двоичные объекты в страницы результатов. Этот пример отображением tooreturn результатов на страницах асинхронно, так что выполнение не блокируются во время ожидания tooreturn большого набора результатов.

В этом примере показано плоский перечисления больших двоичных объектов, но можно также выполнить иерархический список, установка hello **useFlatBlobListing** параметр hello **ListBlobsSegmentedAsync** метод слишком **false**.

Поскольку метод образец hello вызывает асинхронный метод, он должен предваряться символом hello **async** ключевое слово и он должен возвращать **задачи** объекта. Hello await-ключевое слово, указанный для hello **ListBlobsSegmentedAsync** метод приостанавливает выполнение метода образец hello до завершения выполнения задачи листинг hello.

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

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

