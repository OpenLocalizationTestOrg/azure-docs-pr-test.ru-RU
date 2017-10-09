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
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a><span data-ttu-id="8a75d-103">Управление сроком действия больших двоичных объектов службы хранилища Azure в Azure CDN</span><span class="sxs-lookup"><span data-stu-id="8a75d-103">Manage expiration of Azure Storage blobs in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8a75d-104">Веб-приложения и облачные службы Azure, ASP.NET или IIS</span><span class="sxs-lookup"><span data-stu-id="8a75d-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="8a75d-105">Служба BLOB-объектов в службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="8a75d-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="8a75d-106">Hello [службе BLOB-объектов](../storage/common/storage-introduction.md#blob-storage) в [хранилища Azure](../storage/common/storage-introduction.md) один из нескольких источников на основе Azure интегрируется с Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="8a75d-106">hello [blob service](../storage/common/storage-introduction.md#blob-storage) in [Azure Storage](../storage/common/storage-introduction.md) is one of several Azure-based origins integrated with Azure CDN.</span></span>  <span data-ttu-id="8a75d-107">Любое общедоступное содержимое BLOB-объекта может кэшироваться в Azure CDN до истечения его срока жизни (TTL).</span><span class="sxs-lookup"><span data-stu-id="8a75d-107">Any publicly accessible blob content can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="8a75d-108">Hello TTL определяется hello [ *Cache-Control* заголовок](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) в hello HTTP-ответа из хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="8a75d-108">hello TTL is determined by hello [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in hello HTTP response from Azure Storage.</span></span>

> [!TIP]
> <span data-ttu-id="8a75d-109">Вы можете tooset не TTL для большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="8a75d-109">You may choose tooset no TTL on a blob.</span></span>  <span data-ttu-id="8a75d-110">Тогда Azure CDN по умолчанию применит срок жизни длительностью семь дней.</span><span class="sxs-lookup"><span data-stu-id="8a75d-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="8a75d-111">Дополнительные сведения о работе toospeed tooblobs доступ и другие файлы в Azure CDN см. в разделе hello [Общие сведения о Azure CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8a75d-111">For more information about how Azure CDN works toospeed up access tooblobs and other files, see hello [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> <span data-ttu-id="8a75d-112">Дополнительные сведения о hello BLOB-объектов хранилища Azure в разделе [основные понятия службы BLOB-объекта](https://msdn.microsoft.com/library/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="8a75d-112">For more details on hello Azure Storage blob service, see [Blob Service Concepts](https://msdn.microsoft.com/library/dd179376.aspx).</span></span> 
> 
> 

<span data-ttu-id="8a75d-113">В этом учебнике показано несколько способов, можно задать hello TTL для большого двоичного объекта в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="8a75d-113">This tutorial demonstrates several ways that you can set hello TTL on a blob in Azure Storage.</span></span>  

## <a name="azure-powershell"></a><span data-ttu-id="8a75d-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a75d-114">Azure PowerShell</span></span>
<span data-ttu-id="8a75d-115">[Azure PowerShell](/powershell/azure/overview) является одним из tooadminister быстрый, самый эффективный способ hello служб Azure.</span><span class="sxs-lookup"><span data-stu-id="8a75d-115">[Azure PowerShell](/powershell/azure/overview) is one of hello quickest, most powerful ways tooadminister your Azure services.</span></span>  <span data-ttu-id="8a75d-116">Используйте hello `Get-AzureStorageBlob` командлет tooget ссылки toohello (blob), затем установите hello `.ICloudBlob.Properties.CacheControl` свойство.</span><span class="sxs-lookup"><span data-stu-id="8a75d-116">Use hello `Get-AzureStorageBlob` cmdlet tooget a reference toohello blob, then set hello `.ICloudBlob.Properties.CacheControl` property.</span></span> 

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
> <span data-ttu-id="8a75d-117">Можно также использовать PowerShell слишком[управление CDN профилей и конечные точки](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8a75d-117">You can also use PowerShell too[manage your CDN profiles and endpoints](cdn-manage-powershell.md).</span></span>
> 
> 

## <a name="azure-storage-client-library-for-net"></a><span data-ttu-id="8a75d-118">Клиентская библиотека хранилища Azure для .NET</span><span class="sxs-lookup"><span data-stu-id="8a75d-118">Azure Storage Client Library for .NET</span></span>
<span data-ttu-id="8a75d-119">tooset большой двоичный объект, с помощью .NET, используйте hello TTL [клиентская библиотека хранилища Azure для .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) свойство.</span><span class="sxs-lookup"><span data-stu-id="8a75d-119">tooset a blob's TTL using .NET, use hello [Azure Storage Client Library for .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) property.</span></span>

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
> <span data-ttu-id="8a75d-120">Существует много Дополнительные примеры кода .NET в hello [примеры для хранилища BLOB-объектов Azure для .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="8a75d-120">There are many more .NET code samples available in hello [Azure Blob Storage Samples for .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span>
> 
> 

## <a name="other-methods"></a><span data-ttu-id="8a75d-121">Другие методы</span><span class="sxs-lookup"><span data-stu-id="8a75d-121">Other methods</span></span>
* [<span data-ttu-id="8a75d-122">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="8a75d-122">Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)
  
    <span data-ttu-id="8a75d-123">При передаче большого двоичного объекта hello, задайте hello *cacheControl* свойства с помощью hello `-p` переключения.</span><span class="sxs-lookup"><span data-stu-id="8a75d-123">When uploading hello blob, set hello *cacheControl* property using hello `-p` switch.</span></span>  <span data-ttu-id="8a75d-124">Этот пример устанавливает hello TTL tooone часа (3600 секунд).</span><span class="sxs-lookup"><span data-stu-id="8a75d-124">This example sets hello TTL tooone hour (3600 seconds).</span></span>
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [<span data-ttu-id="8a75d-125">API-интерфейс REST служб хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="8a75d-125">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    <span data-ttu-id="8a75d-126">Явно hello набор *x-ms-blob-cache-control* свойство [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [поместить список блокировок](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), или [задание свойств больших двоичных объектов](https://msdn.microsoft.com/library/azure/ee691966.aspx) запроса.</span><span class="sxs-lookup"><span data-stu-id="8a75d-126">Explicitly set hello *x-ms-blob-cache-control* property on a [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put Block List](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), or [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) request.</span></span>
* <span data-ttu-id="8a75d-127">Сторонние средства управления хранилищем</span><span class="sxs-lookup"><span data-stu-id="8a75d-127">Third-party storage management tools</span></span>
  
    <span data-ttu-id="8a75d-128">Некоторые средства управления сторонних разработчиков хранилища Azure позволяют tooset hello *CacheControl* свойство с большими двоичными объектами.</span><span class="sxs-lookup"><span data-stu-id="8a75d-128">Some third-party Azure Storage management tools allow you tooset hello *CacheControl* property on blobs.</span></span> 

## <a name="testing-hello-cache-control-header"></a><span data-ttu-id="8a75d-129">Тестирование hello *Cache-Control* заголовок</span><span class="sxs-lookup"><span data-stu-id="8a75d-129">Testing hello *Cache-Control* header</span></span>
<span data-ttu-id="8a75d-130">Можно легко проверить hello TTL BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="8a75d-130">You can easily verify hello TTL of your blobs.</span></span>  <span data-ttu-id="8a75d-131">С помощью обозревателя [средств разработчика](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), проверить, что вашим большим двоичным объектом — включая hello *Cache-Control* заголовок ответа.</span><span class="sxs-lookup"><span data-stu-id="8a75d-131">Using your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test that your blob is including hello *Cache-Control* response header.</span></span>  <span data-ttu-id="8a75d-132">Можно также использовать средства, подобного **wget**, [почтальон](https://www.getpostman.com/), или [Fiddler](http://www.telerik.com/fiddler) заголовки ответа tooexamine hello.</span><span class="sxs-lookup"><span data-stu-id="8a75d-132">You can also use a tool like **wget**, [Postman](https://www.getpostman.com/), or [Fiddler](http://www.telerik.com/fiddler) tooexamine hello response headers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a75d-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8a75d-133">Next Steps</span></span>
* [<span data-ttu-id="8a75d-134">Узнайте, как hello *Cache-Control* заголовок</span><span class="sxs-lookup"><span data-stu-id="8a75d-134">Read about hello *Cache-Control* header</span></span>](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [<span data-ttu-id="8a75d-135">Узнайте, как toomanage истечения срока действия содержимого облачных служб в Azure CDN</span><span class="sxs-lookup"><span data-stu-id="8a75d-135">Learn how toomanage expiration of Cloud Service content in Azure CDN</span></span>](cdn-manage-expiration-of-cloud-service-content.md)

