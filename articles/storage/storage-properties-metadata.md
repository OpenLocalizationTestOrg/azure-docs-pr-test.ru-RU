---
title: "Задание и получение свойств и метаданных объектов в службе хранилища Azure | Документация Майкрософт"
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
ms.openlocfilehash: 6af66607478c58874f00bcf017a35abfc37888df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="set-and-retrieve-properties-and-metadata"></a><span data-ttu-id="65dd2-103">Задание и получение свойств и метаданных</span><span class="sxs-lookup"><span data-stu-id="65dd2-103">Set and retrieve properties and metadata</span></span>

<span data-ttu-id="65dd2-104">Кроме данных, которые они содержат, объекты в службе хранилища Azure поддерживают свойства системы и пользовательские метаданные.</span><span class="sxs-lookup"><span data-stu-id="65dd2-104">Objects in Azure Storage support system properties and user-defined metadata, in addition to the data they contain.</span></span> <span data-ttu-id="65dd2-105">В этой статье описывается управление свойствами системы и определяемыми пользователем метаданными с помощью [клиентской библиотеки хранилища Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="65dd2-105">This article discusses managing system properties and user-defined metadata with the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span>

* <span data-ttu-id="65dd2-106">**Свойства системы.** Свойства системы есть у каждого ресурса хранилища.</span><span class="sxs-lookup"><span data-stu-id="65dd2-106">**System properties**: System properties exist on each storage resource.</span></span> <span data-ttu-id="65dd2-107">Некоторые из них можно считать или задать, некоторые — только считать.</span><span class="sxs-lookup"><span data-stu-id="65dd2-107">Some of them can be read or set, while others are read-only.</span></span> <span data-ttu-id="65dd2-108">На самом деле, некоторые свойства системы соответствуют определенным стандартным заголовкам HTTP.</span><span class="sxs-lookup"><span data-stu-id="65dd2-108">Under the covers, some system properties correspond to certain standard HTTP headers.</span></span> <span data-ttu-id="65dd2-109">Они хранятся в клиентской библиотеке службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="65dd2-109">The Azure storage client library maintains these for you.</span></span>

* <span data-ttu-id="65dd2-110">**Определяемые пользователем метаданные.** Метаданные, которые можно указать для определенного ресурса в виде пары "имя — значение".</span><span class="sxs-lookup"><span data-stu-id="65dd2-110">**User-defined metadata**: User-defined metadata is metadata that you specify on a given resource in the form of a name-value pair.</span></span> <span data-ttu-id="65dd2-111">Вы можете использовать метаданные для хранения дополнительных значений с использованием ресурса хранилища.</span><span class="sxs-lookup"><span data-stu-id="65dd2-111">You can use metadata to store additional values with a storage resource.</span></span> <span data-ttu-id="65dd2-112">Эти значения являются пользовательскими и не влияют на поведение ресурса.</span><span class="sxs-lookup"><span data-stu-id="65dd2-112">These additional metadata values are for your own purposes only, and do not affect how the resource behaves.</span></span>

<span data-ttu-id="65dd2-113">Получение значений свойств и метаданных ресурса хранилища выполняется в два этапа.</span><span class="sxs-lookup"><span data-stu-id="65dd2-113">Retrieving property and metadata values for a storage resource is a two-step process.</span></span> <span data-ttu-id="65dd2-114">Прежде чем считывать эти значения, необходимо получить их, вызвав метод **FetchAttributes** .</span><span class="sxs-lookup"><span data-stu-id="65dd2-114">Before you can read these values, you must explicitly fetch them by calling the **FetchAttributes** method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65dd2-115">Значения свойств и метаданных для ресурса хранилища заполняются только при вызове одного из методов **FetchAttributes** .</span><span class="sxs-lookup"><span data-stu-id="65dd2-115">Property and metadata values for a storage resource are not populated unless you call one of the **FetchAttributes** methods.</span></span>
>
> <span data-ttu-id="65dd2-116">Если любая из пар имен и значений содержит знаки не из набора ASCII, возвратится ошибка с кодом `400 Bad Request`.</span><span class="sxs-lookup"><span data-stu-id="65dd2-116">You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters.</span></span> <span data-ttu-id="65dd2-117">Пары имен и значений метаданных являются действительными HTTP-заголовками, поэтому они должны соответствовать всем ограничениям для HTTP-заголовков.</span><span class="sxs-lookup"><span data-stu-id="65dd2-117">Metadata name/value pairs are valid HTTP headers, and so must adhere to all restrictions governing HTTP headers.</span></span> <span data-ttu-id="65dd2-118">Для имен и значений, содержащих знаки не из набора ASCII, мы рекомендуем использовать кодировку URL или кодировку Base64.</span><span class="sxs-lookup"><span data-stu-id="65dd2-118">It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.</span></span>
>

## <a name="setting-and-retrieving-properties"></a><span data-ttu-id="65dd2-119">Установка и получение свойств</span><span class="sxs-lookup"><span data-stu-id="65dd2-119">Setting and retrieving properties</span></span>
<span data-ttu-id="65dd2-120">Чтобы получить значения свойств, вызовите метод **FetchAttributes** для BLOB-объекта или контейнера, а затем считайте значения.</span><span class="sxs-lookup"><span data-stu-id="65dd2-120">To retrieve property values, call the **FetchAttributes** method on your blob or container to populate the properties, then read the values.</span></span>

<span data-ttu-id="65dd2-121">Чтобы задать свойства объекта, укажите значение свойства, а затем вызовите метод **SetProperties** .</span><span class="sxs-lookup"><span data-stu-id="65dd2-121">To set properties on an object, specify the property value, then call the **SetProperties** method.</span></span>

<span data-ttu-id="65dd2-122">В следующем примере кода будет создан контейнер, а значения некоторых свойств будут выведены в окно консоли.</span><span class="sxs-lookup"><span data-stu-id="65dd2-122">The following code example creates a container, then writes some of its property values to a console window.</span></span>

```csharp
//Parse the connection string for the storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create the service client object for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference to a container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create the container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
container.FetchAttributes();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a><span data-ttu-id="65dd2-123">Установка и получение метаданных</span><span class="sxs-lookup"><span data-stu-id="65dd2-123">Setting and retrieving metadata</span></span>
<span data-ttu-id="65dd2-124">Метаданные можно указать как одну или несколько пар "имя-значение" для BLOB-ресурса или ресурса контейнера.</span><span class="sxs-lookup"><span data-stu-id="65dd2-124">You can specify metadata as one or more name-value pairs on a blob or container resource.</span></span> <span data-ttu-id="65dd2-125">Чтобы задать метаданные, добавьте пары "имя — значение" в коллекцию **Metadata** ресурса, а затем вызовите метод **SetMetadata**, чтобы сохранить значения в службе.</span><span class="sxs-lookup"><span data-stu-id="65dd2-125">To set metadata, add name-value pairs to the **Metadata** collection on the resource, then call the **SetMetadata** method to save the values to the service.</span></span>

> [!NOTE]
> <span data-ttu-id="65dd2-126">Имя метаданных должно соответствовать соглашениям об именовании идентификаторов C#.</span><span class="sxs-lookup"><span data-stu-id="65dd2-126">The name of your metadata must conform to the naming conventions for C# identifiers.</span></span>
>
>

<span data-ttu-id="65dd2-127">В следующем примере кода задаются метаданные для контейнера.</span><span class="sxs-lookup"><span data-stu-id="65dd2-127">The following code example sets metadata on a container.</span></span> <span data-ttu-id="65dd2-128">Одно значение задается с помощью метода коллекции **Add** .</span><span class="sxs-lookup"><span data-stu-id="65dd2-128">One value is set using the collection's **Add** method.</span></span> <span data-ttu-id="65dd2-129">Другое значение задается с помощью неявного синтаксиса «ключ/значение».</span><span class="sxs-lookup"><span data-stu-id="65dd2-129">The other value is set using implicit key/value syntax.</span></span> <span data-ttu-id="65dd2-130">Можно использовать любой из способов.</span><span class="sxs-lookup"><span data-stu-id="65dd2-130">Both are valid.</span></span>

```csharp
public static void AddContainerMetadata(CloudBlobContainer container)
{
    //Add some metadata to the container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    //Set the container's metadata.
    container.SetMetadata();
}
```

<span data-ttu-id="65dd2-131">Чтобы получить метаданные, вызовите метод **FetchAttributes** для BLOB-объекта или контейнера (для заполнения коллекции **Metadata**), а затем считайте значения, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="65dd2-131">To retrieve metadata, call the **FetchAttributes** method on your blob or container to populate the **Metadata** collection, then read the values, as shown in the example below.</span></span>

```csharp
public static void ListContainerMetadata(CloudBlobContainer container)
{
    //Fetch container attributes in order to populate the container's properties and metadata.
    container.FetchAttributes();

    //Enumerate the container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="65dd2-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="65dd2-132">Next steps</span></span>
* [<span data-ttu-id="65dd2-133">Справочные материалы клиентской библиотеки хранилища Azure для .NET</span><span class="sxs-lookup"><span data-stu-id="65dd2-133">Azure Storage Client Library for .NET reference</span></span>](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [<span data-ttu-id="65dd2-134">Клиентская библиотека хранилища Azure для пакетов NuGet .NET</span><span class="sxs-lookup"><span data-stu-id="65dd2-134">Azure Storage Client Library for .NET NuGet package</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
