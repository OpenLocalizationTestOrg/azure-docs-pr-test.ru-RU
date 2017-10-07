---
title: "aaaCreate и использование подписи общего доступа (SAS) с хранилищем больших двоичных объектов Azure | Документы Microsoft"
description: "В этом учебнике показано, как toocreate подписи коллективного доступа для использования с хранилищем больших двоичных объектов и как tooconsume их в клиентских приложениях."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 491e0b3c-76d4-4149-9a80-bbbd683b1f3e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 32004d7d29a190a7ed7234513428c3c156b833b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a><span data-ttu-id="3aaf1-103">Подписанные URL-адреса. Часть 2: создание и использование подписанного URL-адреса в службе BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="3aaf1-103">Shared Access Signatures, Part 2: Create and use a SAS with Blob storage</span></span>

<span data-ttu-id="3aaf1-104">[В части 1](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) этого учебника приведен обзор подписей общего доступа (SAS), а также даны советы и рекомендации по их использованию.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-104">[Part 1](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) of this tutorial explored shared access signatures (SAS) and explained best practices for using them.</span></span> <span data-ttu-id="3aaf1-105">Часть 2 показано, как toogenerate, а затем использовать общий доступ к подписи с помощью хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-105">Part 2 shows you how toogenerate and then use shared access signatures with Blob storage.</span></span> <span data-ttu-id="3aaf1-106">Hello примеры написаны на C# и используйте hello клиентская библиотека хранилища Azure для .NET.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-106">hello examples are written in C# and use hello Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="3aaf1-107">Примеры Hello в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-107">hello examples in this tutorial:</span></span>

* <span data-ttu-id="3aaf1-108">Создание подписанного URL-адреса для контейнера.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-108">Generate a shared access signature on a container</span></span>
* <span data-ttu-id="3aaf1-109">Создание подписанного URL-адреса для большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-109">Generate a shared access signature on a blob</span></span>
* <span data-ttu-id="3aaf1-110">Создание подписей toomanage политики доступа в ресурсы контейнера</span><span class="sxs-lookup"><span data-stu-id="3aaf1-110">Create a stored access policy toomanage signatures on a container's resources</span></span>
* <span data-ttu-id="3aaf1-111">Тестовые подписи hello общего доступа в клиентском приложении</span><span class="sxs-lookup"><span data-stu-id="3aaf1-111">Test hello shared access signatures in a client application</span></span>

## <a name="about-this-tutorial"></a><span data-ttu-id="3aaf1-112">О данном учебнике</span><span class="sxs-lookup"><span data-stu-id="3aaf1-112">About this tutorial</span></span>
<span data-ttu-id="3aaf1-113">В этом руководстве мы создадим два консольных приложения, демонстрирующих создание и использование подписанных URL-адресов для контейнеров и больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-113">In this tutorial, we create two console applications that demonstrate creating and using shared access signatures for containers and blobs:</span></span>

<span data-ttu-id="3aaf1-114">**Приложение 1**: hello приложение для управления.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-114">**Application 1**: hello management application.</span></span> <span data-ttu-id="3aaf1-115">Создает подписанный URL-адрес для контейнера и большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-115">Generates a shared access signature for a container and a blob.</span></span> <span data-ttu-id="3aaf1-116">Содержит ключ доступа учетной записи хранения hello в исходном коде.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-116">Includes hello storage account access key in source code.</span></span>

<span data-ttu-id="3aaf1-117">**Приложение 2**: hello клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-117">**Application 2**: hello client application.</span></span> <span data-ttu-id="3aaf1-118">Обращается к контейнера и большого двоичного объекта ресурсов с помощью URL-адреса hello совместно с первого приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-118">Accesses container and blob resources using hello shared access signatures created with hello first application.</span></span> <span data-ttu-id="3aaf1-119">Использует только hello общего доступа подписи tooaccess контейнера и больших двоичных объектов ресурсов — это происходит *не* включают hello ключ доступа учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-119">Uses only hello shared access signatures tooaccess container and blob resources--it does *not* include hello storage account access key.</span></span>

## <a name="part-1-create-a-console-application-toogenerate-shared-access-signatures"></a><span data-ttu-id="3aaf1-120">Часть 1: Создать toogenerate общего доступа приложения консоли подписи</span><span class="sxs-lookup"><span data-stu-id="3aaf1-120">Part 1: Create a console application toogenerate shared access signatures</span></span>
<span data-ttu-id="3aaf1-121">Во-первых Обеспечьте hello клиентская библиотека хранилища Azure для установки .NET.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-121">First, ensure that you have hello Azure Storage Client Library for .NET installed.</span></span> <span data-ttu-id="3aaf1-122">Вы можете установить hello [пакет NuGet](http://nuget.org/packages/WindowsAzure.Storage/ "пакет NuGet") содержащих hello самые последние сборки для hello клиентской библиотеки.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-122">You can install hello [NuGet package](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet package") containing hello most up-to-date assemblies for hello client library.</span></span> <span data-ttu-id="3aaf1-123">Это рекомендуется использовать метод, чтобы обеспечить наличие последних исправлений hello hello.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-123">This is hello recommended method for ensuring that you have hello most recent fixes.</span></span> <span data-ttu-id="3aaf1-124">Можно также загрузить клиентскую библиотеку hello как часть hello самую последнюю версию hello [Azure SDK для .NET](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="3aaf1-124">You can also download hello client library as part of hello most recent version of hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/).</span></span>

<span data-ttu-id="3aaf1-125">В Visual Studio создайте новое консольное приложение Windows и назовите его **GenerateSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-125">In Visual Studio, create a new Windows console application and name it **GenerateSharedAccessSignatures**.</span></span> <span data-ttu-id="3aaf1-126">Добавьте ссылки на слишком[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) и [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) с помощью одного из hello следующие подходы:</span><span class="sxs-lookup"><span data-stu-id="3aaf1-126">Add references too[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) by using one of hello following approaches:</span></span>

* <span data-ttu-id="3aaf1-127">Используйте hello [диспетчера пакетов NuGet](https://docs.nuget.org/consume/installing-nuget) в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-127">Use hello [NuGet package manager](https://docs.nuget.org/consume/installing-nuget) in Visual Studio.</span></span> <span data-ttu-id="3aaf1-128">Выберите **Проект** > **Управление пакетами NuGet**, выполните поиск в Интернете для каждого пакета (Microsoft.WindowsAzure.ConfigurationManager и WindowsAzure.Storage) и установите их.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-128">Select **Project** > **Manage NuGet Packages**, search online for each package (Microsoft.WindowsAzure.ConfigurationManager and WindowsAzure.Storage) and install them.</span></span>
* <span data-ttu-id="3aaf1-129">Можно также найти эти сборки в установке hello Azure SDK и добавьте ссылки на toothem:</span><span class="sxs-lookup"><span data-stu-id="3aaf1-129">Alternatively, locate these assemblies in your installation of hello Azure SDK and add references toothem:</span></span>
  * <span data-ttu-id="3aaf1-130">Microsoft.WindowsAzure.Configuration.dll.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-130">Microsoft.WindowsAzure.Configuration.dll</span></span>
  * <span data-ttu-id="3aaf1-131">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="3aaf1-131">Microsoft.WindowsAzure.Storage.dll</span></span>

<span data-ttu-id="3aaf1-132">Вверху hello hello файла Program.cs добавьте следующую hello **с помощью** директивы:</span><span class="sxs-lookup"><span data-stu-id="3aaf1-132">At hello top of hello Program.cs file, add hello following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="3aaf1-133">Измените файл app.config hello, чтобы он содержал параметр конфигурации со строкой соединения, указывающий tooyour учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-133">Edit hello app.config file so that it contains a configuration setting with a connection string that points tooyour storage account.</span></span> <span data-ttu-id="3aaf1-134">Файл app.config должен выглядеть примерно toothis один:</span><span class="sxs-lookup"><span data-stu-id="3aaf1-134">Your app.config file should look similar toothis one:</span></span>

```xml
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
  </startup>
  <appSettings>
    <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey"/>
  </appSettings>
</configuration>
```

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a><span data-ttu-id="3aaf1-135">Создание универсального кода ресурса (URI) подписанного URL-адреса для контейнера</span><span class="sxs-lookup"><span data-stu-id="3aaf1-135">Generate a shared access signature URI for a container</span></span>
<span data-ttu-id="3aaf1-136">toobegin с добавляется метод toogenerate подписанного URL-адреса на новый контейнер.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-136">toobegin with, we add a method toogenerate a shared access signature on a new container.</span></span> <span data-ttu-id="3aaf1-137">В этом случае hello подпись не связана с хранимой политикой доступа, предоставляет, он продолжает hello данные hello URI для его разрешения hello и время истечения срока действия.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-137">In this case, hello signature is not associated with a stored access policy, so it carries on hello URI hello information indicating its expiry time and hello permissions it grants.</span></span>

<span data-ttu-id="3aaf1-138">Сначала добавьте код toohello **Main()** tooauthenticate метод доступа к учетной записи хранилища tooyour и создать новый контейнер:</span><span class="sxs-lookup"><span data-stu-id="3aaf1-138">First, add code toohello **Main()** method tooauthenticate access tooyour storage account and create a new container:</span></span>

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Insert calls toohello methods created below here...

    //Require user input before closing hello console window.
    Console.ReadLine();
}
```

<span data-ttu-id="3aaf1-139">Добавьте метод, который приводит к возникновению ошибки hello подписанный URL-адрес для контейнера hello и возвращает подпись hello URI.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-139">Next, add a method that generates hello shared access signature for hello container and returns hello signature URI:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
    //Set hello expiry time and permissions for hello container.
    //In this case no start time is specified, so hello shared access signature becomes valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="3aaf1-140">Добавьте следующие строки внизу hello hello hello **Main()** метода, прежде чем hello вызвать слишком**Console.ReadLine()**, toocall **GetContainerSasUri()** и записи hello окно консоли toohello URI подписи:</span><span class="sxs-lookup"><span data-stu-id="3aaf1-140">Add hello following lines at hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, toocall **GetContainerSasUri()** and write hello signature URI toohello console window:</span></span>

```csharp
//Generate a SAS URI for hello container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="3aaf1-141">Скомпилируйте и запустите toooutput hello URI подписи коллективного доступа для нового контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-141">Compile and run toooutput hello shared access signature URI for hello new container.</span></span> <span data-ttu-id="3aaf1-142">Hello URI будет иметь примерно следующий toohello:</span><span class="sxs-lookup"><span data-stu-id="3aaf1-142">hello URI will be similar toohello following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

<span data-ttu-id="3aaf1-143">После выполнения кода hello hello подписанный URL-адрес, созданный для контейнера hello допустимы для hello каждые 24 часа.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-143">Once you have run hello code, hello shared access signature you created for hello container will be valid for hello next 24 hours.</span></span> <span data-ttu-id="3aaf1-144">подпись Hello предоставляет клиент разрешение toolist BLOB-объектов в контейнере hello и toowrite toohello контейнер больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-144">hello signature grants a client permission toolist blobs in hello container and toowrite new blobs toohello container.</span></span>

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a><span data-ttu-id="3aaf1-145">Создание URI подписанного URL-адреса для большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="3aaf1-145">Generate a shared access signature URI for a blob</span></span>
<span data-ttu-id="3aaf1-146">Затем мы записать новый большой двоичный объект в контейнере hello аналогичные toocreate код и создать подпись общего доступа для него.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-146">Next, we write similar code toocreate a new blob within hello container and generate a shared access signature for it.</span></span> <span data-ttu-id="3aaf1-147">Подписанный URL-адрес не связан с хранимой политикой доступа, включив в него hello время начала, срок действия и сведения о разрешениях в hello URI.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-147">This shared access signature is not associated with a stored access policy, so it includes hello start time, expiry time, and permission information in hello URI.</span></span>

<span data-ttu-id="3aaf1-148">Добавьте новый метод, который создает новый большой двоичный объект и записывает некоторые tooit текста, затем создает подпись общего доступа и возвращает URI подписи hello:</span><span class="sxs-lookup"><span data-stu-id="3aaf1-148">Add a new method that creates a new blob and writes some text tooit, then generates a shared access signature and returns hello signature URI:</span></span>

```csharp
static string GetBlobSasUri(CloudBlobContainer container)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblob.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature (SAS).";
    blob.UploadText(blobContent);

    //Set hello expiry time and permissions for hello blob.
    //In this case, hello start time is specified as a few minutes in hello past, toomitigate clock skew.
    //hello shared access signature will be valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessStartTime = DateTimeOffset.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="3aaf1-149">Внизу hello hello **Main()** метод, добавить следующие строки toocall hello **GetBlobSasUri()**, прежде чем hello вызвать слишком**Console.ReadLine()**и записи совместно hello окно консоли toohello URI подписи доступа:</span><span class="sxs-lookup"><span data-stu-id="3aaf1-149">At hello bottom of hello **Main()** method, add hello following lines toocall **GetBlobSasUri()**, before hello call too**Console.ReadLine()**, and write hello shared access signature URI toohello console window:</span></span>

```csharp
//Generate a SAS URI for a blob within hello container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="3aaf1-150">Скомпилируйте и запустите toooutput hello подписанного URL-адреса URI hello новый большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-150">Compile and run toooutput hello shared access signature URI for hello new blob.</span></span> <span data-ttu-id="3aaf1-151">Hello URI будет иметь примерно следующий toohello:</span><span class="sxs-lookup"><span data-stu-id="3aaf1-151">hello URI will be similar toohello following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-hello-container"></a><span data-ttu-id="3aaf1-152">Создание хранимой политики доступа на контейнер hello</span><span class="sxs-lookup"><span data-stu-id="3aaf1-152">Create a stored access policy on hello container</span></span>
<span data-ttu-id="3aaf1-153">Теперь давайте создадим хранимая политика доступа на контейнер hello, в котором будут определены ограничения hello для сигнатур общего доступа, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-153">Now let's create a stored access policy on hello container, which will define hello constraints for any shared access signatures that are associated with it.</span></span>

<span data-ttu-id="3aaf1-154">В предыдущих примерах hello можно указать время начала hello (явно или неявно), hello срок действия и разрешения hello на hello подписанном URL-адресе URI сам.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-154">In hello previous examples, we specified hello start time (implicitly or explicitly), hello expiry time, and hello permissions on hello shared access signature URI itself.</span></span> <span data-ttu-id="3aaf1-155">В следующих примерах hello мы задавать их hello хранимые политики доступа, отличный от hello подписанного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-155">In hello following examples, we specify these on hello stored access policy, not on hello shared access signature.</span></span> <span data-ttu-id="3aaf1-156">Это позволяет нам toochange эти ограничения без повторной выдачи hello общий доступ к подписи.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-156">Doing so enables us toochange these constraints without reissuing hello shared access signature.</span></span>

<span data-ttu-id="3aaf1-157">Это возможно toohave один или несколько ограничений hello на подписанный URL-адрес hello и остаток hello hello хранимой политике доступа.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-157">It's possible toohave one or more of hello constraints on hello shared access signature, and hello remainder on hello stored access policy.</span></span> <span data-ttu-id="3aaf1-158">Тем не менее можно только указать hello время начала, время окончания и разрешения в одном месте или других hello.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-158">However, you can only specify hello start time, expiry time, and permissions in one place or hello other.</span></span> <span data-ttu-id="3aaf1-159">Например нельзя задать разрешения на подписанный URL-адрес hello и также указать их на hello хранимые политики доступа.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-159">For example, you can't specify permissions on hello shared access signature and also specify them on hello stored access policy.</span></span>

<span data-ttu-id="3aaf1-160">При добавлении контейнер tooa политики доступа, необходимо получить hello контейнера существующие разрешения, добавить новую политику доступа hello и установить разрешения контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-160">When you add a stored access policy tooa container, you must get hello container's existing permissions, add hello new access policy, and then set hello container's permissions.</span></span>

<span data-ttu-id="3aaf1-161">Добавьте новый метод, который создает новую политику доступа на контейнер и возвращает имя hello hello политики:</span><span class="sxs-lookup"><span data-stu-id="3aaf1-161">Add a new method that creates a new stored access policy on a container and returns hello name of hello policy:</span></span>

```csharp
static void CreateSharedAccessPolicy(CloudBlobClient blobClient, CloudBlobContainer container,
    string policyName)
{
    //Get hello container's existing permissions.
    BlobContainerPermissions permissions = container.GetPermissions();

    //Create a new shared access policy and define its constraints.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Read
    };

    //Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    container.SetPermissions(permissions);
}
```

<span data-ttu-id="3aaf1-162">Внизу hello hello **Main()** метода, прежде чем hello вызвать слишком**Console.ReadLine()**, добавьте следующие hello строк toofirst снимите все существующие политики доступа, а затем вызвать hello  **CreateSharedAccessPolicy()** метод:</span><span class="sxs-lookup"><span data-stu-id="3aaf1-162">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toofirst clear any existing access policies, and then call hello **CreateSharedAccessPolicy()** method:</span></span>

```csharp
//Clear any existing access policies on container.
BlobContainerPermissions perms = container.GetPermissions();
perms.SharedAccessPolicies.Clear();
container.SetPermissions(perms);

//Create a new access policy on hello container, which may be optionally used tooprovide constraints for
//shared access signatures on hello container and hello blob.
string sharedAccessPolicyName = "tutorialpolicy";
CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);
```

<span data-ttu-id="3aaf1-163">При удалении hello политики доступа на контейнер, необходимо сначала получить hello контейнера существующие разрешения, а затем снимите hello разрешения, а затем снова установить разрешения hello.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-163">When you clear hello access policies on a container, you must first get hello container's existing permissions, then clear hello permissions, then set hello permissions again.</span></span>

### <a name="generate-a-shared-access-signature-uri-on-hello-container-that-uses-an-access-policy"></a><span data-ttu-id="3aaf1-164">Создание подписанного URL-адреса URI в контейнере hello, который использует политику доступа</span><span class="sxs-lookup"><span data-stu-id="3aaf1-164">Generate a shared access signature URI on hello container that uses an access policy</span></span>
<span data-ttu-id="3aaf1-165">Далее мы создадим другой подписанный URL-адрес для контейнера hello, которая была создана ранее, но сейчас мы связать hello подписи с hello хранимые политики доступа, созданной в предыдущем примере hello.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-165">Next, we create another shared access signature for hello container that we created earlier, but this time we associate hello signature with hello stored access policy we created in hello previous example.</span></span>

<span data-ttu-id="3aaf1-166">Добавьте новый toogenerate метод другой подписанный URL-адрес для контейнера hello:</span><span class="sxs-lookup"><span data-stu-id="3aaf1-166">Add a new method toogenerate another shared access signature for hello container:</span></span>

```csharp
static string GetContainerSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Generate hello shared access signature on hello container. In this case, all of hello constraints for the
    //shared access signature are specified on hello stored access policy.
    string sasContainerToken = container.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="3aaf1-167">Внизу hello hello **Main()** метода, прежде чем hello вызвать слишком**Console.ReadLine()**, добавить следующие строки toocall hello hello **GetContainerSasUriWithPolicy** метод :</span><span class="sxs-lookup"><span data-stu-id="3aaf1-167">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toocall hello **GetContainerSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-hello-blob-that-uses-an-access-policy"></a><span data-ttu-id="3aaf1-168">Создание URI подписи общего доступа на большой двоичный объект, использует hello политики доступа</span><span class="sxs-lookup"><span data-stu-id="3aaf1-168">Generate a Shared Access Signature URI on hello Blob That Uses an Access Policy</span></span>
<span data-ttu-id="3aaf1-169">Наконец мы добавьте аналогичные toocreate метод другой большой двоичный объект и создайте подписанный URL-адрес, связанный с хранимой политикой доступа.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-169">Finally, we add a similar method toocreate another blob and generate a shared access signature that's associated with a stored access policy.</span></span>

<span data-ttu-id="3aaf1-170">Добавьте новый toocreate метод большого двоичного объекта и создайте подписанный URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="3aaf1-170">Add a new method toocreate a blob and generate a shared access signature:</span></span>

```csharp
static string GetBlobSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblobpolicy.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature. " +
    "A stored access policy defines hello constraints for hello signature.";
    MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    ms.Position = 0;
    using (ms)
    {
        blob.UploadFromStream(ms);
    }

    //Generate hello shared access signature on hello blob.
    string sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="3aaf1-171">Внизу hello hello **Main()** метода, прежде чем hello вызвать слишком**Console.ReadLine()**, добавить следующие строки toocall hello hello **GetBlobSasUriWithPolicy** метод:</span><span class="sxs-lookup"><span data-stu-id="3aaf1-171">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toocall hello **GetBlobSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

<span data-ttu-id="3aaf1-172">Hello **Main()** метод должен выглядеть следующим образом в полном объеме.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-172">hello **Main()** method should now look like this in its entirety.</span></span> <span data-ttu-id="3aaf1-173">Запустите его toowrite hello подписанный URL-адрес окна консоли toohello идентификаторы URI, затем скопируйте и вставьте их в текстовый файл для использования в hello во второй части этого учебника.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-173">Run it toowrite hello shared access signature URIs toohello console window, then copy and paste them into a text file for use in hello second part of this tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Generate a SAS URI for hello container, without a stored access policy.
    Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, without a stored access policy.
    Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
    Console.WriteLine();

    //Clear any existing access policies on container.
    BlobContainerPermissions perms = container.GetPermissions();
    perms.SharedAccessPolicies.Clear();
    container.SetPermissions(perms);

    //Create a new access policy on hello container, which may be optionally used tooprovide constraints for
    //shared access signatures on hello container and hello blob.
    string sharedAccessPolicyName = "tutorialpolicy";
    CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);

    //Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    Console.ReadLine();
}
```

<span data-ttu-id="3aaf1-174">При запуске консольного приложения hello GenerateSharedAccessSignatures, вы увидите примерно toohello следующие выходные данные.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-174">When you run hello GenerateSharedAccessSignatures console application, you'll see output similar toohello following.</span></span> <span data-ttu-id="3aaf1-175">Это hello общий URL-адреса, используемого во второй части учебника hello.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-175">These are hello shared access signatures you use in Part 2 of hello tutorial.</span></span>

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-tootest-hello-shared-access-signatures"></a><span data-ttu-id="3aaf1-176">Часть 2: Создание подписей консоли приложению tootest hello общий доступ</span><span class="sxs-lookup"><span data-stu-id="3aaf1-176">Part 2: Create a console application tootest hello shared access signatures</span></span>
<span data-ttu-id="3aaf1-177">tootest hello подписи коллективного доступа созданные в предыдущих примерах hello, мы создаем второй консольное приложение, которое использует hello подписи tooperform операций на hello контейнера и большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-177">tootest hello shared access signatures created in hello previous examples, we create a second console application that uses hello signatures tooperform operations on hello container and on a blob.</span></span>

> [!NOTE]
> <span data-ttu-id="3aaf1-178">Если с завершена hello первой части учебника hello прошло более 24 часов, hello подписи, созданные больше не допустимы.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-178">If more than 24 hours have passed since you completed hello first part of hello tutorial, hello signatures you generated will no longer be valid.</span></span> <span data-ttu-id="3aaf1-179">В этом случае следует запустить кода hello hello первый консольного приложения toogenerate свежей подписанные URL-адреса для использования в hello во второй части учебника hello.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-179">In this case, you should run hello code in hello first console application toogenerate fresh shared access signatures for use in hello second part of hello tutorial.</span></span>
>

<span data-ttu-id="3aaf1-180">В Visual Studio создайте новое консольное приложение Windows и назовите его **ConsumeSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-180">In Visual Studio, create a new Windows console application and name it **ConsumeSharedAccessSignatures**.</span></span> <span data-ttu-id="3aaf1-181">Добавьте ссылки на слишком[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) и [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), как это делалось ранее.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-181">Add references too[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), as you did previously.</span></span>

<span data-ttu-id="3aaf1-182">Вверху hello hello файла Program.cs добавьте следующую hello **с помощью** директивы:</span><span class="sxs-lookup"><span data-stu-id="3aaf1-182">At hello top of hello Program.cs file, add hello following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="3aaf1-183">В тексте hello hello **Main()** метод, добавить hello следующие строковые константы, изменения их значения toohello общего доступа подписей, созданные в части 1 руководства hello.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-183">In hello body of hello **Main()** method, add hello following string constants, changing their values toohello shared access signatures you generated in part 1 of hello tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-tootry-container-operations-using-a-shared-access-signature"></a><span data-ttu-id="3aaf1-184">Добавьте контейнер операции tootry метод, с помощью подписанного URL-адреса</span><span class="sxs-lookup"><span data-stu-id="3aaf1-184">Add a method tootry container operations using a shared access signature</span></span>
<span data-ttu-id="3aaf1-185">Далее мы добавить метод, который проверяет некоторые операции контейнера, с помощью подписи общего доступа для контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-185">Next, we add a method that tests some container operations using a shared access signature for hello container.</span></span> <span data-ttu-id="3aaf1-186">подпись коллективного доступа Hello — используется tooreturn контейнер toohello ссылка проверки подлинности доступа toohello контейнера на основе сигнатуры hello сама по себе.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-186">hello shared access signature is used tooreturn a reference toohello container, authenticating access toohello container based on hello signature alone.</span></span>

<span data-ttu-id="3aaf1-187">Добавьте следующий метод tooProgram.cs hello:</span><span class="sxs-lookup"><span data-stu-id="3aaf1-187">Add hello following method tooProgram.cs:</span></span>

```csharp
static void UseContainerSAS(string sas)
{
    //Try performing container operations with hello SAS provided.

    //Return a reference toohello container using hello SAS URI.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(sas));

    //Create a list toostore blob URIs returned by a listing operation on hello container.
    List<ICloudBlob> blobList = new List<ICloudBlob>();

    //Write operation: write a new blob toohello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference("blobCreatedViaSAS.txt");
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello container. ";
        blob.UploadText(blobContent);

        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //List operation: List hello blobs in hello container.
    try
    {
        foreach (ICloudBlob blob in container.ListBlobs())
        {
            blobList.Add(blob);
        }
        Console.WriteLine("List operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("List operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Get a reference tooone of hello blobs in hello container and read it.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        MemoryStream msRead = new MemoryStream();
        msRead.Position = 0;
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            Console.WriteLine(msRead.Length);
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    Console.WriteLine();

    //Delete operation: Delete a blob in hello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

<span data-ttu-id="3aaf1-188">Обновление hello **Main()** toocall метод **UseContainerSAS()** с обоими hello подписи коллективного доступа на контейнер hello:</span><span class="sxs-lookup"><span data-stu-id="3aaf1-188">Update hello **Main()** method toocall **UseContainerSAS()** with both of hello shared access signatures you created on hello container:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    Console.ReadLine();
}
```

### <a name="add-a-method-tootry-blob-operations-using-a-shared-access-signature"></a><span data-ttu-id="3aaf1-189">Добавьте метод операции tootry BLOB-объекта, с помощью подписанного URL-адреса</span><span class="sxs-lookup"><span data-stu-id="3aaf1-189">Add a method tootry blob operations using a shared access signature</span></span>
<span data-ttu-id="3aaf1-190">Наконец добавим метод, который проверяет некоторые операции BLOB-объекта с помощью подписанного URL-адреса для большого двоичного объекта hello.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-190">Finally, we add a method that tests some blob operations using a shared access signature on hello blob.</span></span> <span data-ttu-id="3aaf1-191">В этом случае мы используем hello конструктор **CloudBlockBlob(String)**, передавая hello подписанный URL-адрес tooreturn toohello эталонный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-191">In this case, we use hello constructor **CloudBlockBlob(String)**, passing in hello shared access signature, tooreturn a reference toohello blob.</span></span> <span data-ttu-id="3aaf1-192">Без проверки подлинности не требуется; он основан на подпись hello сама по себе.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-192">No other authentication is required; it's based on hello signature alone.</span></span>

<span data-ttu-id="3aaf1-193">Добавьте следующий метод tooProgram.cs hello:</span><span class="sxs-lookup"><span data-stu-id="3aaf1-193">Add hello following method tooProgram.cs:</span></span>

```csharp
static void UseBlobSAS(string sas)
{
    //Try performing blob operations using hello SAS provided.

    //Return a reference toohello blob using hello SAS URI.
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(sas));

    //Write operation: Write a new blob toohello container.
    try
    {
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello blob. ";
        MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
        msWrite.Position = 0;
        using (msWrite)
        {
            blob.UploadFromStream(msWrite);
        }
        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Read hello contents of hello blob.
    try
    {
        MemoryStream msRead = new MemoryStream();
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            msRead.Position = 0;
            using (StreamReader reader = new StreamReader(msRead, true))
            {
                string line;
                while ((line = reader.ReadLine()) != null)
                {
                    Console.WriteLine(line);
                }
            }
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Delete operation: Delete hello blob.
    try
    {
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

<span data-ttu-id="3aaf1-194">Обновление hello **Main()** toocall метод **UseBlobSAS()** с обоими hello подписи коллективного доступа, созданные для hello большого двоичного объекта:</span><span class="sxs-lookup"><span data-stu-id="3aaf1-194">Update hello **Main()** method toocall **UseBlobSAS()** with both of hello shared access signatures that you created on hello blob:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    //Call hello test methods with hello shared access signatures created on hello blob, with and without hello access policy.
    UseBlobSAS(blobSAS);
    UseBlobSAS(blobSASWithAccessPolicy);

    Console.ReadLine();
}
```

<span data-ttu-id="3aaf1-195">Запустите консольное приложение hello и просмотрите hello toosee выходные данные, какие операции разрешены какие подписи.</span><span class="sxs-lookup"><span data-stu-id="3aaf1-195">Run hello console application and observe hello output toosee which operations are permitted for which signatures.</span></span> <span data-ttu-id="3aaf1-196">результат Hello в окне консоли hello будет выглядеть аналогично toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="3aaf1-196">hello output in hello console window will look similar toohello following:</span></span>

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a><span data-ttu-id="3aaf1-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3aaf1-197">Next Steps</span></span>

* [<span data-ttu-id="3aaf1-198">Подписи коллективного доступа, часть 1: Общие сведения о модели SAS hello</span><span class="sxs-lookup"><span data-stu-id="3aaf1-198">Shared Access Signatures, Part 1: Understanding hello SAS Model</span></span>](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="3aaf1-199">Управление toocontainers анонимный доступ для чтения и больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="3aaf1-199">Manage anonymous read access toocontainers and blobs</span></span>](storage-manage-access-to-resources.md)
* <span data-ttu-id="3aaf1-200">[Delegating Access with a Shared Access Signature](http://msdn.microsoft.com/library/azure/ee395415.aspx) (Делегирование доступа с помощью подписанного URL-адреса)</span><span class="sxs-lookup"><span data-stu-id="3aaf1-200">[Delegating access with a shared access signature (REST API)](http://msdn.microsoft.com/library/azure/ee395415.aspx)</span></span>
* [<span data-ttu-id="3aaf1-201">Введение в использование SAS таблиц и очередей</span><span class="sxs-lookup"><span data-stu-id="3aaf1-201">Introducing Table and Queue SAS</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
