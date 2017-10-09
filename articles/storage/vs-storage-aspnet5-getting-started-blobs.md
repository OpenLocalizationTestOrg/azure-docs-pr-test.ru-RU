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
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a>Приступая к работе с хранилищем BLOB-объектов Azure и подключенными службами Visual Studio (ASP.NET Core)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Обзор
В этой статье описывается, как tooget запущена с помощью хранилища больших двоичных объектов Azure в Visual Studio, после создания или ссылка на учетную запись хранилища Azure в проекте ASP.NET Core с помощью диалогового окна Visual Studio Добавление подключенных служб hello.

Хранилище Azure BLOB-объекта — это служба для хранения больших объемов неструктурированных данных, который может осуществляться из любого места в Здравствуй, мир! через HTTP или HTTPS. Один большой двоичный объект может быть любого размера. Большими двоичными объектами могут быть изображения, аудио- и видеофайлы, необработанные данные и файлы документов. В этой статье описывается, как tooget работы с хранилищем больших двоичных объектов, после создания учетной записи хранилища Azure с помощью Visual Studio hello **Добавление подключенных служб** диалогового окна в проектах ASP.NET Core.

Так же как файлы располагаются в папках, большие двоичные объекты хранилища располагаются в контейнерах. После создания хранилища, можно создать один или несколько контейнеров в хранилище hello. Например в хранилище, вызывается буферный «файл», контейнеров можно создать в хранилище hello, называется «images» toostore изображения и вызывается другой toostore «звук» звуковые файлы. После создания hello контейнеры, можно передать файлы toothem отдельных больших двоичных объектов. Дополнительные сведения о выполнении программных операций с большими двоичными объектами см. в статье [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](storage-dotnet-how-to-use-blobs.md).

## <a name="access-blob-containers-in-code"></a>Доступ к контейнерам больших двоичных объектов в коде
tooprogrammatically доступа к большим двоичным объектам в проектах ASP.NET Core, требуется hello tooadd следующих элементов, если они еще не существует.

1. Добавьте следующий код объявления пространства имен toohello начало любого файла C#, которой требуется доступ tooprogrammatically хранилища Azure hello.
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. Получите объект **CloudStorageAccount** , представляющий данные учетной записи хранения. Используйте следующий код tooget hello хранения строки соединения и сведения об учетной записи хранилища из конфигурации службы Azure hello.
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    **Примечание:** использовать все hello над кодом перед кода hello в следующих разделах hello.
3. Используйте **CloudBlobClient** объекта tooget **CloudBlobContainer** ссылки tooan существующий контейнер в вашей учетной записи хранилища.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a>Создание контейнера в коде
Можно также использовать hello **CloudBlobClient** toocreate контейнера в учетной записи хранилища. Все что нужно toodo — tooadd вызов слишком**CreateIfNotExistsAsync** как hello, следующий код:

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


**Примечание:** hello API, которые выполняют вызовы tooAzure хранилища в ASP.NET Core являются асинхронными. Дополнительные сведения см. в статье [Asynchronous Programming with async and await (C#)](http://msdn.microsoft.com/library/hh191443.aspx) (Асинхронное программирование с использованием ключевых слов Async и Await (C#)). Приведенный ниже код Hello предполагается, что используются асинхронные методы программирования.

toomake файлов hello в доступных tooeveryone hello контейнера, можно задать toobe контейнера hello открытый с помощью hello, следующий код.

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a>Отправка BLOB-объекта в контейнер
tooupload файла большого двоичного объекта в контейнер, получить ссылку на контейнер и использовать его tooget ссылку на большой двоичный объект. После того как вы ссылку на большой двоичный объект, можно передать любой поток данных tooit с вызывающему Привет **UploadFromStreamAsync** метод. Эта операция создает hello большого двоичного объекта, если он еще не существует, или перезаписывает его, если он существует. Следующий пример показывает как Hello tooupload большого двоичного объекта в контейнер и предполагается hello контейнера уже был создан.

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>Перечисление hello больших двоичных объектов в контейнере
toolist hello BLOB-объектов в контейнере, сначала нужно получить ссылку на контейнер. Затем можно вызвать hello контейнера **ListBlobsSegmentedAsync** метод tooretrieve hello BLOB-объектов и/или каталогов в ней. широкий набор свойств и методов для возвращенной hello tooaccess **IListBlobItem**, необходимо привести tooa **CloudBlockBlob**, **CloudPageBlob**, или  **CloudBlobDirectory** объекта. Если вы не знаете тип blob hello, можно использовать тип возврата toodetermine какие toocast его. Здравствуй, следующий код демонстрирует, как tooretrieve и вывод hello URI каждого элемента в контейнере.

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

Существуют и другие способы toolist hello содержимого контейнера BLOB-объектов. Дополнительные сведения см. в разделе [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container).

## <a name="download-a-blob"></a>Загрузка BLOB-объектов
toodownload большого двоичного объекта, сначала нужно получить toohello эталонный BLOB-объект, а затем вызвать hello **DownloadToStreamAsync** метод. Hello следующий пример использует hello **DownloadToStreamAsync** метод tootransfer hello blob содержимое tooa объект потока, который затем можно сохранить как локальный файл.

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

Существуют другие способы toosave большие двоичные объекты как файлы. Дополнительные сведения см. в разделе [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](storage-dotnet-how-to-use-blobs.md#download-blobs).

## <a name="delete-a-blob"></a>Удаление большого двоичного объекта
toodelete большого двоичного объекта, сначала нужно получить toohello эталонный BLOB-объект, а затем вызвать hello **DeleteAsync** метода.

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

