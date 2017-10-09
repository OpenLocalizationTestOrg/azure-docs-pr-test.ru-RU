---
title: "истечение срока действия aaaManage больших двоичных объектов хранилища Azure в Azure CDN | Документы Microsoft"
description: "Дополнительные сведения о hello параметры для управления срок жизни для больших двоичных объектов в кэше Azure CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ad4801e9-d09a-49bf-b35c-efdc4e6034e8
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9fecae9639deb28977da7f851e1da4a823ddc4e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a>Управление сроком действия больших двоичных объектов службы хранилища Azure в Azure CDN
> [!div class="op_single_selector"]
> * [Веб-приложения и облачные службы Azure, ASP.NET или IIS](cdn-manage-expiration-of-cloud-service-content.md)
> * [Служба BLOB-объектов в службе хранилища Azure](cdn-manage-expiration-of-blob-content.md)
> 
> 

Hello [службе BLOB-объектов](../storage/common/storage-introduction.md#blob-storage) в [хранилища Azure](../storage/common/storage-introduction.md) один из нескольких источников на основе Azure интегрируется с Azure CDN.  Любое общедоступное содержимое BLOB-объекта может кэшироваться в Azure CDN до истечения его срока жизни (TTL).  Hello TTL определяется hello [ *Cache-Control* заголовок](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) в hello HTTP-ответа из хранилища Azure.

> [!TIP]
> Вы можете tooset не TTL для большого двоичного объекта.  Тогда Azure CDN по умолчанию применит срок жизни длительностью семь дней.
> 
> Дополнительные сведения о работе toospeed tooblobs доступ и другие файлы в Azure CDN см. в разделе hello [Общие сведения о Azure CDN](cdn-overview.md).
> 
> Дополнительные сведения о hello BLOB-объектов хранилища Azure в разделе [основные понятия службы BLOB-объекта](https://msdn.microsoft.com/library/dd179376.aspx). 
> 
> 

В этом учебнике показано несколько способов, можно задать hello TTL для большого двоичного объекта в хранилище Azure.  

## <a name="azure-powershell"></a>Azure PowerShell
[Azure PowerShell](/powershell/azure/overview) является одним из tooadminister быстрый, самый эффективный способ hello служб Azure.  Используйте hello `Get-AzureStorageBlob` командлет tooget ссылки toohello (blob), затем установите hello `.ICloudBlob.Properties.CacheControl` свойство. 

```powershell
# Create a storage context
$context = New-AzureStorageContext -StorageAccountName "<storage account name>" -StorageAccountKey "<storage account key>"

# Get a reference toohello blob
$blob = Get-AzureStorageBlob -Context $context -Container "<container name>" -Blob "<blob name>"

# Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
$blob.ICloudBlob.Properties.CacheControl = "public, max-age=3600"

# Send hello update toohello cloud
$blob.ICloudBlob.SetProperties()
```

> [!TIP]
> Можно также использовать PowerShell слишком[управление CDN профилей и конечные точки](cdn-manage-powershell.md).
> 
> 

## <a name="azure-storage-client-library-for-net"></a>Клиентская библиотека хранилища Azure для .NET
tooset большой двоичный объект, с помощью .NET, используйте hello TTL [клиентская библиотека хранилища Azure для .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) свойство.

```csharp
class Program
{
    const string connectionString = "<storage connection string>";
    static void Main()
    {
        // Retrieve storage account information from connection string
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

        // Create a blob client for interacting with hello blob service.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Create a reference toohello container
        CloudBlobContainer container = blobClient.GetContainerReference("<container name>");

        // Create a reference toohello blob
        CloudBlob blob = container.GetBlobReference("<blob name>");

        // Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
        blob.Properties.CacheControl = "public, max-age=3600";

        // Update hello blob's properties in hello cloud
        blob.SetProperties();
    }
}
```

> [!TIP]
> Существует много Дополнительные примеры кода .NET в hello [примеры для хранилища BLOB-объектов Azure для .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).
> 
> 

## <a name="other-methods"></a>Другие методы
* [Интерфейс командной строки Azure](../cli-install-nodejs.md)
  
    При передаче большого двоичного объекта hello, задайте hello *cacheControl* свойства с помощью hello `-p` переключения.  Этот пример устанавливает hello TTL tooone часа (3600 секунд).
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [API-интерфейс REST служб хранилища Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    Явно hello набор *x-ms-blob-cache-control* свойство [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [поместить список блокировок](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), или [задание свойств больших двоичных объектов](https://msdn.microsoft.com/library/azure/ee691966.aspx) запроса.
* Сторонние средства управления хранилищем
  
    Некоторые средства управления сторонних разработчиков хранилища Azure позволяют tooset hello *CacheControl* свойство с большими двоичными объектами. 

## <a name="testing-hello-cache-control-header"></a>Тестирование hello *Cache-Control* заголовок
Можно легко проверить hello TTL BLOB-объектов.  С помощью обозревателя [средств разработчика](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), проверить, что вашим большим двоичным объектом — включая hello *Cache-Control* заголовок ответа.  Можно также использовать средства, подобного **wget**, [почтальон](https://www.getpostman.com/), или [Fiddler](http://www.telerik.com/fiddler) заголовки ответа tooexamine hello.

## <a name="next-steps"></a>Дальнейшие действия
* [Узнайте, как hello *Cache-Control* заголовок](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [Узнайте, как toomanage истечения срока действия содержимого облачных служб в Azure CDN](cdn-manage-expiration-of-cloud-service-content.md)

