---
title: "aaaSet и получения объектов, свойств и метаданных в хранилище Azure | Документы Microsoft"
description: "Хранение пользовательских метаданных для объектов в службе хранилища Azure, а также задание и получение свойств системы."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 036f9006-273e-400b-844b-3329045e9e1f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 44f9243183014845964f337b476a6b0069dc0902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-and-retrieve-properties-and-metadata"></a><span data-ttu-id="2858d-103">Задание и получение свойств и метаданных</span><span class="sxs-lookup"><span data-stu-id="2858d-103">Set and retrieve properties and metadata</span></span>

<span data-ttu-id="2858d-104">Объектов в хранилище Azure поддержка системные свойства и определяемые пользователем метаданные, кроме toohello данных, содержащихся в них.</span><span class="sxs-lookup"><span data-stu-id="2858d-104">Objects in Azure Storage support system properties and user-defined metadata, in addition toohello data they contain.</span></span> <span data-ttu-id="2858d-105">В этой статье описывается управление системные свойства и определяемые пользователем метаданные с hello [клиентская библиотека хранилища Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="2858d-105">This article discusses managing system properties and user-defined metadata with hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span>

* <span data-ttu-id="2858d-106">**Свойства системы.** Свойства системы есть у каждого ресурса хранилища.</span><span class="sxs-lookup"><span data-stu-id="2858d-106">**System properties**: System properties exist on each storage resource.</span></span> <span data-ttu-id="2858d-107">Некоторые из них можно считать или задать, некоторые — только считать.</span><span class="sxs-lookup"><span data-stu-id="2858d-107">Some of them can be read or set, while others are read-only.</span></span> <span data-ttu-id="2858d-108">На деле hello некоторые системные свойства соответствуют toocertain стандартные заголовки HTTP.</span><span class="sxs-lookup"><span data-stu-id="2858d-108">Under hello covers, some system properties correspond toocertain standard HTTP headers.</span></span> <span data-ttu-id="2858d-109">Клиентская библиотека хранилища Azure Hello обслуживает их.</span><span class="sxs-lookup"><span data-stu-id="2858d-109">hello Azure storage client library maintains these for you.</span></span>

* <span data-ttu-id="2858d-110">**Определяемые пользователем метаданные**: определяемые пользователем метаданные — это метаданные, указанные для определенного ресурса в форме hello пары "имя значение".</span><span class="sxs-lookup"><span data-stu-id="2858d-110">**User-defined metadata**: User-defined metadata is metadata that you specify on a given resource in hello form of a name-value pair.</span></span> <span data-ttu-id="2858d-111">Можно использовать дополнительные значения метаданных toostore ресурсом хранилища.</span><span class="sxs-lookup"><span data-stu-id="2858d-111">You can use metadata toostore additional values with a storage resource.</span></span> <span data-ttu-id="2858d-112">Значения этих дополнительных метаданных только по своему усмотрению и не влияют на поведение hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2858d-112">These additional metadata values are for your own purposes only, and do not affect how hello resource behaves.</span></span>

<span data-ttu-id="2858d-113">Получение значений свойств и метаданных ресурса хранилища выполняется в два этапа.</span><span class="sxs-lookup"><span data-stu-id="2858d-113">Retrieving property and metadata values for a storage resource is a two-step process.</span></span> <span data-ttu-id="2858d-114">Прежде чем можно будет прочитать эти значения, необходимо явно запросить их по вызывающему Привет **FetchAttributes** метод.</span><span class="sxs-lookup"><span data-stu-id="2858d-114">Before you can read these values, you must explicitly fetch them by calling hello **FetchAttributes** method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2858d-115">Значения свойств и метаданных для ресурса хранилища не заполняются только при вызове одного из hello **FetchAttributes** методы.</span><span class="sxs-lookup"><span data-stu-id="2858d-115">Property and metadata values for a storage resource are not populated unless you call one of hello **FetchAttributes** methods.</span></span>
>
> <span data-ttu-id="2858d-116">Если любая из пар имен и значений содержит знаки не из набора ASCII, возвратится ошибка с кодом `400 Bad Request`.</span><span class="sxs-lookup"><span data-stu-id="2858d-116">You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters.</span></span> <span data-ttu-id="2858d-117">Пары имя/значение метаданных являются допустимыми заголовками HTTP и поэтому должен соответствовать tooall ограничений, относящихся к заголовкам HTTP.</span><span class="sxs-lookup"><span data-stu-id="2858d-117">Metadata name/value pairs are valid HTTP headers, and so must adhere tooall restrictions governing HTTP headers.</span></span> <span data-ttu-id="2858d-118">Для имен и значений, содержащих знаки не из набора ASCII, мы рекомендуем использовать кодировку URL или кодировку Base64.</span><span class="sxs-lookup"><span data-stu-id="2858d-118">It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.</span></span>
>

## <a name="setting-and-retrieving-properties"></a><span data-ttu-id="2858d-119">Установка и получение свойств</span><span class="sxs-lookup"><span data-stu-id="2858d-119">Setting and retrieving properties</span></span>
<span data-ttu-id="2858d-120">значения свойств tooretrieve, вызов hello **FetchAttributes** метод на большой двоичный объект или контейнер toopopulate hello свойств, затем считывать значения hello.</span><span class="sxs-lookup"><span data-stu-id="2858d-120">tooretrieve property values, call hello **FetchAttributes** method on your blob or container toopopulate hello properties, then read hello values.</span></span>

<span data-ttu-id="2858d-121">tooset свойств объекта, укажите значение свойства hello, а затем вызвать hello **SetProperties** метод.</span><span class="sxs-lookup"><span data-stu-id="2858d-121">tooset properties on an object, specify hello property value, then call hello **SetProperties** method.</span></span>

<span data-ttu-id="2858d-122">Hello следующий пример кода создает контейнер, а затем записывает некоторые из его окна консоли tooa значения свойства.</span><span class="sxs-lookup"><span data-stu-id="2858d-122">hello following code example creates a container, then writes some of its property values tooa console window.</span></span>

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create hello service client object for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
container.FetchAttributes();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a><span data-ttu-id="2858d-123">Установка и получение метаданных</span><span class="sxs-lookup"><span data-stu-id="2858d-123">Setting and retrieving metadata</span></span>
<span data-ttu-id="2858d-124">Метаданные можно указать как одну или несколько пар "имя-значение" для BLOB-ресурса или ресурса контейнера.</span><span class="sxs-lookup"><span data-stu-id="2858d-124">You can specify metadata as one or more name-value pairs on a blob or container resource.</span></span> <span data-ttu-id="2858d-125">метаданные tooset добавьте пары "имя значение" toohello **метаданные** коллекции hello ресурса, затем вызовите hello **SetMetadata** метод toosave hello значения toohello службы.</span><span class="sxs-lookup"><span data-stu-id="2858d-125">tooset metadata, add name-value pairs toohello **Metadata** collection on hello resource, then call hello **SetMetadata** method toosave hello values toohello service.</span></span>

> [!NOTE]
> <span data-ttu-id="2858d-126">Имя Hello метаданных должны соответствовать toohello соглашения об именовании идентификаторов C#.</span><span class="sxs-lookup"><span data-stu-id="2858d-126">hello name of your metadata must conform toohello naming conventions for C# identifiers.</span></span>
>
>

<span data-ttu-id="2858d-127">Hello следующий пример кода задает метаданные для контейнера.</span><span class="sxs-lookup"><span data-stu-id="2858d-127">hello following code example sets metadata on a container.</span></span> <span data-ttu-id="2858d-128">Одно значение задается с помощью коллекции hello **добавить** метод.</span><span class="sxs-lookup"><span data-stu-id="2858d-128">One value is set using hello collection's **Add** method.</span></span> <span data-ttu-id="2858d-129">Hello других значение задается с помощью синтаксиса неявный ключ значение.</span><span class="sxs-lookup"><span data-stu-id="2858d-129">hello other value is set using implicit key/value syntax.</span></span> <span data-ttu-id="2858d-130">Можно использовать любой из способов.</span><span class="sxs-lookup"><span data-stu-id="2858d-130">Both are valid.</span></span>

```csharp
public static void AddContainerMetadata(CloudBlobContainer container)
{
    //Add some metadata toohello container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    //Set hello container's metadata.
    container.SetMetadata();
}
```

<span data-ttu-id="2858d-131">метаданные tooretrieve, вызов hello **FetchAttributes** метод toopopulate вашей большого двоичного объекта или контейнера hello **метаданных** коллекции, затем считывать значения hello, как показано в приведенном ниже примере hello.</span><span class="sxs-lookup"><span data-stu-id="2858d-131">tooretrieve metadata, call hello **FetchAttributes** method on your blob or container toopopulate hello **Metadata** collection, then read hello values, as shown in hello example below.</span></span>

```csharp
public static void ListContainerMetadata(CloudBlobContainer container)
{
    //Fetch container attributes in order toopopulate hello container's properties and metadata.
    container.FetchAttributes();

    //Enumerate hello container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="2858d-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2858d-132">Next steps</span></span>
* [<span data-ttu-id="2858d-133">Справочные материалы клиентской библиотеки хранилища Azure для .NET</span><span class="sxs-lookup"><span data-stu-id="2858d-133">Azure Storage Client Library for .NET reference</span></span>](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [<span data-ttu-id="2858d-134">Клиентская библиотека хранилища Azure для пакетов NuGet .NET</span><span class="sxs-lookup"><span data-stu-id="2858d-134">Azure Storage Client Library for .NET NuGet package</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
