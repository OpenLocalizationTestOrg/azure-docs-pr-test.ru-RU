---
title: "Создание и использование подписанного URL-адреса (SAS) с хранилищем BLOB-объектов Azure | Документация Майкрософт"
description: "В этом руководстве показано, как создать подписанные URL-адреса для использования с хранилищем больших двоичных объектов и как использовать их в клиентских приложениях."
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
ms.openlocfilehash: 0d7bede352667931527c8583cb172a46a37b5aa8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a><span data-ttu-id="03d91-103">Подписанные URL-адреса. Часть 2: создание и использование подписанного URL-адреса в службе BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="03d91-103">Shared Access Signatures, Part 2: Create and use a SAS with Blob storage</span></span>

<span data-ttu-id="03d91-104">[В части 1](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) этого учебника приведен обзор подписей общего доступа (SAS), а также даны советы и рекомендации по их использованию.</span><span class="sxs-lookup"><span data-stu-id="03d91-104">[Part 1](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) of this tutorial explored shared access signatures (SAS) and explained best practices for using them.</span></span> <span data-ttu-id="03d91-105">В части 2 показано, как создать и затем использовать подписи общего доступа с помощью хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="03d91-105">Part 2 shows you how to generate and then use shared access signatures with Blob storage.</span></span> <span data-ttu-id="03d91-106">Примеры написаны на C# и используют библиотеку клиента хранения Azure для .NET.</span><span class="sxs-lookup"><span data-stu-id="03d91-106">The examples are written in C# and use the Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="03d91-107">В примерах этого руководства выполняются следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="03d91-107">The examples in this tutorial:</span></span>

* <span data-ttu-id="03d91-108">Создание подписанного URL-адреса для контейнера.</span><span class="sxs-lookup"><span data-stu-id="03d91-108">Generate a shared access signature on a container</span></span>
* <span data-ttu-id="03d91-109">Создание подписанного URL-адреса для большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="03d91-109">Generate a shared access signature on a blob</span></span>
* <span data-ttu-id="03d91-110">Создание хранимой политики доступа для управления подписями в ресурсах контейнера.</span><span class="sxs-lookup"><span data-stu-id="03d91-110">Create a stored access policy to manage signatures on a container's resources</span></span>
* <span data-ttu-id="03d91-111">Проверка подписанных URL-адресов в клиентском приложении.</span><span class="sxs-lookup"><span data-stu-id="03d91-111">Test the shared access signatures in a client application</span></span>

## <a name="about-this-tutorial"></a><span data-ttu-id="03d91-112">О данном учебнике</span><span class="sxs-lookup"><span data-stu-id="03d91-112">About this tutorial</span></span>
<span data-ttu-id="03d91-113">В этом руководстве мы создадим два консольных приложения, демонстрирующих создание и использование подписанных URL-адресов для контейнеров и больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="03d91-113">In this tutorial, we create two console applications that demonstrate creating and using shared access signatures for containers and blobs:</span></span>

<span data-ttu-id="03d91-114">**Приложение 1.** Приложение управления.</span><span class="sxs-lookup"><span data-stu-id="03d91-114">**Application 1**: The management application.</span></span> <span data-ttu-id="03d91-115">Создает подписанный URL-адрес для контейнера и большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="03d91-115">Generates a shared access signature for a container and a blob.</span></span> <span data-ttu-id="03d91-116">Включает ключ доступа учетной записи в исходном коде.</span><span class="sxs-lookup"><span data-stu-id="03d91-116">Includes the storage account access key in source code.</span></span>

<span data-ttu-id="03d91-117">**Приложение 2.** Клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="03d91-117">**Application 2**: The client application.</span></span> <span data-ttu-id="03d91-118">Обращается к ресурсам контейнера и большого двоичного объекта с использованием подписанных URL-адресов, созданных с помощью первого приложения.</span><span class="sxs-lookup"><span data-stu-id="03d91-118">Accesses container and blob resources using the shared access signatures created with the first application.</span></span> <span data-ttu-id="03d91-119">Использует только подписанные URL-адреса для доступа к ресурсам контейнера и большого двоичного объекта. Оно *не* включает ключ доступа к учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="03d91-119">Uses only the shared access signatures to access container and blob resources--it does *not* include the storage account access key.</span></span>

## <a name="part-1-create-a-console-application-to-generate-shared-access-signatures"></a><span data-ttu-id="03d91-120">Часть 1. Создание консольного приложения для создания подписанных URL-адресов</span><span class="sxs-lookup"><span data-stu-id="03d91-120">Part 1: Create a console application to generate shared access signatures</span></span>
<span data-ttu-id="03d91-121">Прежде всего убедитесь, что установлена библиотека клиента хранения Azure для .NET.</span><span class="sxs-lookup"><span data-stu-id="03d91-121">First, ensure that you have the Azure Storage Client Library for .NET installed.</span></span> <span data-ttu-id="03d91-122">Вы можете установить [пакет NuGet](http://nuget.org/packages/WindowsAzure.Storage/ "пакет NuGet"), содержащий самые новые сборки для клиентской библиотеки.</span><span class="sxs-lookup"><span data-stu-id="03d91-122">You can install the [NuGet package](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet package") containing the most up-to-date assemblies for the client library.</span></span> <span data-ttu-id="03d91-123">Так вы будете получать все последние исправления.</span><span class="sxs-lookup"><span data-stu-id="03d91-123">This is the recommended method for ensuring that you have the most recent fixes.</span></span> <span data-ttu-id="03d91-124">Клиентскую библиотеку также можно скачать в составе последней версии [пакета Azure SDK для .NET](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="03d91-124">You can also download the client library as part of the most recent version of the [Azure SDK for .NET](https://azure.microsoft.com/downloads/).</span></span>

<span data-ttu-id="03d91-125">В Visual Studio создайте новое консольное приложение Windows и назовите его **GenerateSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="03d91-125">In Visual Studio, create a new Windows console application and name it **GenerateSharedAccessSignatures**.</span></span> <span data-ttu-id="03d91-126">Добавьте ссылки на [Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) и [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), используя один из следующих методов.</span><span class="sxs-lookup"><span data-stu-id="03d91-126">Add references to [Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) by using one of the following approaches:</span></span>

* <span data-ttu-id="03d91-127">Воспользуйтесь [диспетчером пакетов NuGet](https://docs.nuget.org/consume/installing-nuget) в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="03d91-127">Use the [NuGet package manager](https://docs.nuget.org/consume/installing-nuget) in Visual Studio.</span></span> <span data-ttu-id="03d91-128">Выберите **Проект** > **Управление пакетами NuGet**, выполните поиск в Интернете для каждого пакета (Microsoft.WindowsAzure.ConfigurationManager и WindowsAzure.Storage) и установите их.</span><span class="sxs-lookup"><span data-stu-id="03d91-128">Select **Project** > **Manage NuGet Packages**, search online for each package (Microsoft.WindowsAzure.ConfigurationManager and WindowsAzure.Storage) and install them.</span></span>
* <span data-ttu-id="03d91-129">Вы также можете найти нужные сборки в установленных файлах пакета SDK Azure и добавить ссылки на них:</span><span class="sxs-lookup"><span data-stu-id="03d91-129">Alternatively, locate these assemblies in your installation of the Azure SDK and add references to them:</span></span>
  * <span data-ttu-id="03d91-130">Microsoft.WindowsAzure.Configuration.dll.</span><span class="sxs-lookup"><span data-stu-id="03d91-130">Microsoft.WindowsAzure.Configuration.dll</span></span>
  * <span data-ttu-id="03d91-131">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="03d91-131">Microsoft.WindowsAzure.Storage.dll</span></span>

<span data-ttu-id="03d91-132">Добавьте в начало файла Program.cs следующие директивы **using**:</span><span class="sxs-lookup"><span data-stu-id="03d91-132">At the top of the Program.cs file, add the following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="03d91-133">Измените файл app.config, содержащий параметр конфигурации со строкой подключения, которая указывает на вашу учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="03d91-133">Edit the app.config file so that it contains a configuration setting with a connection string that points to your storage account.</span></span> <span data-ttu-id="03d91-134">Файл app.config должен иметь примерно такой вид:</span><span class="sxs-lookup"><span data-stu-id="03d91-134">Your app.config file should look similar to this one:</span></span>

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

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a><span data-ttu-id="03d91-135">Создание универсального кода ресурса (URI) подписанного URL-адреса для контейнера</span><span class="sxs-lookup"><span data-stu-id="03d91-135">Generate a shared access signature URI for a container</span></span>
<span data-ttu-id="03d91-136">Для начала мы добавим метод для создания подписанного URL-адреса для нового контейнера.</span><span class="sxs-lookup"><span data-stu-id="03d91-136">To begin with, we add a method to generate a shared access signature on a new container.</span></span> <span data-ttu-id="03d91-137">В этом случае подпись не связана с хранимой политикой доступа, поэтому содержит сведения URI с указанием времени окончания срока действия подписи и предоставляемых ей разрешений.</span><span class="sxs-lookup"><span data-stu-id="03d91-137">In this case, the signature is not associated with a stored access policy, so it carries on the URI the information indicating its expiry time and the permissions it grants.</span></span>

<span data-ttu-id="03d91-138">Во-первых, добавьте код для метода **Main()** , чтобы проверить подлинности доступа к вашей учетной записи хранения и создать новый контейнер:</span><span class="sxs-lookup"><span data-stu-id="03d91-138">First, add code to the **Main()** method to authenticate access to your storage account and create a new container:</span></span>

```csharp
static void Main(string[] args)
{
    //Parse the connection string and return a reference to the storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create the blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference to a container to use for the sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Insert calls to the methods created below here...

    //Require user input before closing the console window.
    Console.ReadLine();
}
```

<span data-ttu-id="03d91-139">Затем добавьте метод, который создает подписанный URL-адрес для контейнера и возвращает URI подписи:</span><span class="sxs-lookup"><span data-stu-id="03d91-139">Next, add a method that generates the shared access signature for the container and returns the signature URI:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
    //Set the expiry time and permissions for the container.
    //In this case no start time is specified, so the shared access signature becomes valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Write;

    //Generate the shared access signature on the container, setting the constraints directly on the signature.
    string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

    //Return the URI string for the container, including the SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="03d91-140">В нижнюю часть метода **Main()** перед вызовом **Console.ReadLine()** добавьте следующие строки для вызова метода **GetContainerSasUri()** и вывода URI подписи в окно консоли:</span><span class="sxs-lookup"><span data-stu-id="03d91-140">Add the following lines at the bottom of the **Main()** method, before the call to **Console.ReadLine()**, to call **GetContainerSasUri()** and write the signature URI to the console window:</span></span>

```csharp
//Generate a SAS URI for the container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="03d91-141">Скомпилируйте и запустите выходные данные URI подписи общего доступа для нового контейнера.</span><span class="sxs-lookup"><span data-stu-id="03d91-141">Compile and run to output the shared access signature URI for the new container.</span></span> <span data-ttu-id="03d91-142">Этот URI будет похож на следующий:</span><span class="sxs-lookup"><span data-stu-id="03d91-142">The URI will be similar to the following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

<span data-ttu-id="03d91-143">После выполнения кода созданный для контейнера подписанный URL-адрес будет действителен в течение следующих 24 часов.</span><span class="sxs-lookup"><span data-stu-id="03d91-143">Once you have run the code, the shared access signature you created for the container will be valid for the next 24 hours.</span></span> <span data-ttu-id="03d91-144">Эта подпись предоставляет клиенту разрешение на перечисление больших двоичных объектов в контейнере и на запись новых больших двоичных объектов в контейнер.</span><span class="sxs-lookup"><span data-stu-id="03d91-144">The signature grants a client permission to list blobs in the container and to write new blobs to the container.</span></span>

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a><span data-ttu-id="03d91-145">Создание URI подписанного URL-адреса для большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="03d91-145">Generate a shared access signature URI for a blob</span></span>
<span data-ttu-id="03d91-146">Далее мы напишем аналогичный код, создающий большой двоичный объект в контейнере и подписанный URL-адрес для него.</span><span class="sxs-lookup"><span data-stu-id="03d91-146">Next, we write similar code to create a new blob within the container and generate a shared access signature for it.</span></span> <span data-ttu-id="03d91-147">Этот подписанный URL-адрес не связан с хранимой политикой доступа, поэтому он включает в себя время начала действия, время окончания действия и разрешения в виде URI.</span><span class="sxs-lookup"><span data-stu-id="03d91-147">This shared access signature is not associated with a stored access policy, so it includes the start time, expiry time, and permission information in the URI.</span></span>

<span data-ttu-id="03d91-148">Добавьте новый метод, который создает большой двоичный объект и записывает туда какой-либо текст, а затем создает подписанный URL-адрес и возвращает URI подписи:</span><span class="sxs-lookup"><span data-stu-id="03d91-148">Add a new method that creates a new blob and writes some text to it, then generates a shared access signature and returns the signature URI:</span></span>

```csharp
static string GetBlobSasUri(CloudBlobContainer container)
{
    //Get a reference to a blob within the container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblob.txt");

    //Upload text to the blob. If the blob does not yet exist, it will be created.
    //If the blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible to clients via a shared access signature (SAS).";
    blob.UploadText(blobContent);

    //Set the expiry time and permissions for the blob.
    //In this case, the start time is specified as a few minutes in the past, to mitigate clock skew.
    //The shared access signature will be valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessStartTime = DateTimeOffset.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write;

    //Generate the shared access signature on the blob, setting the constraints directly on the signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="03d91-149">Добавьте следующие строки в нижнюю часть метода **Main()**, чтобы вызвать метод **GetBlobSasUri()** перед вызовом **Console.ReadLine()** и вывести подписанный URL-адрес в окно консоли:</span><span class="sxs-lookup"><span data-stu-id="03d91-149">At the bottom of the **Main()** method, add the following lines to call **GetBlobSasUri()**, before the call to **Console.ReadLine()**, and write the shared access signature URI to the console window:</span></span>

```csharp
//Generate a SAS URI for a blob within the container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="03d91-150">Скомпилируйте и запустите выходные данные URI подписи общего доступа для нового BLOB-объекта.</span><span class="sxs-lookup"><span data-stu-id="03d91-150">Compile and run to output the shared access signature URI for the new blob.</span></span> <span data-ttu-id="03d91-151">Этот URI будет похож на следующий:</span><span class="sxs-lookup"><span data-stu-id="03d91-151">The URI will be similar to the following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-the-container"></a><span data-ttu-id="03d91-152">Создание хранимой политики доступа для контейнера</span><span class="sxs-lookup"><span data-stu-id="03d91-152">Create a stored access policy on the container</span></span>
<span data-ttu-id="03d91-153">Теперь давайте создадим хранимую политику доступа для контейнера, которая будет определять ограничения для всех связанных с ней подписей общего доступа.</span><span class="sxs-lookup"><span data-stu-id="03d91-153">Now let's create a stored access policy on the container, which will define the constraints for any shared access signatures that are associated with it.</span></span>

<span data-ttu-id="03d91-154">В предыдущих примерах мы указали время начала действия (явно или косвенно), время истечения срока действия, а также разрешения в самом URI подписи общего доступа.</span><span class="sxs-lookup"><span data-stu-id="03d91-154">In the previous examples, we specified the start time (implicitly or explicitly), the expiry time, and the permissions on the shared access signature URI itself.</span></span> <span data-ttu-id="03d91-155">В следующих примерах мы укажем эти сведения в хранимой политике доступа, а не в подписанном URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="03d91-155">In the following examples, we specify these on the stored access policy, not on the shared access signature.</span></span> <span data-ttu-id="03d91-156">Это позволяет нам изменять такие ограничения без повторного выпуска подписи общего доступа.</span><span class="sxs-lookup"><span data-stu-id="03d91-156">Doing so enables us to change these constraints without reissuing the shared access signature.</span></span>

<span data-ttu-id="03d91-157">В подписанном URL-адресе можно использовать одно или несколько ограничений, а остальные ограничения задать в хранимой политике доступа.</span><span class="sxs-lookup"><span data-stu-id="03d91-157">It's possible to have one or more of the constraints on the shared access signature, and the remainder on the stored access policy.</span></span> <span data-ttu-id="03d91-158">Однако время начала действия, время окончания срока действия и разрешения можно указать только в одном из этих двух ресурсов.</span><span class="sxs-lookup"><span data-stu-id="03d91-158">However, you can only specify the start time, expiry time, and permissions in one place or the other.</span></span> <span data-ttu-id="03d91-159">Например, нельзя задать разрешения в подписанном URL-адресе, а также в хранимой политике доступа.</span><span class="sxs-lookup"><span data-stu-id="03d91-159">For example, you can't specify permissions on the shared access signature and also specify them on the stored access policy.</span></span>

<span data-ttu-id="03d91-160">При добавлении хранимой политики доступа к контейнеру, необходимо получить имеющиеся разрешения контейнера, добавить новую политику доступа, а потом задать разрешения контейнера.</span><span class="sxs-lookup"><span data-stu-id="03d91-160">When you add a stored access policy to a container, you must get the container's existing permissions, add the new access policy, and then set the container's permissions.</span></span>

<span data-ttu-id="03d91-161">Добавьте новый метод, который создает новую хранимую политику доступа в контейнере и возвращает имя политики.</span><span class="sxs-lookup"><span data-stu-id="03d91-161">Add a new method that creates a new stored access policy on a container and returns the name of the policy:</span></span>

```csharp
static void CreateSharedAccessPolicy(CloudBlobClient blobClient, CloudBlobContainer container,
    string policyName)
{
    //Get the container's existing permissions.
    BlobContainerPermissions permissions = container.GetPermissions();

    //Create a new shared access policy and define its constraints.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Read
    };

    //Add the new policy to the container's permissions, and set the container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    container.SetPermissions(permissions);
}
```

<span data-ttu-id="03d91-162">В нижнюю часть метода **Main()** перед вызовом **Console.ReadLine()** добавьте следующие строки, чтобы сначала удалить все имеющиеся политики доступа, а потом вызвать метод **CreateSharedAccessPolicy()**:</span><span class="sxs-lookup"><span data-stu-id="03d91-162">At the bottom of the **Main()** method, before the call to **Console.ReadLine()**, add the following lines to first clear any existing access policies, and then call the **CreateSharedAccessPolicy()** method:</span></span>

```csharp
//Clear any existing access policies on container.
BlobContainerPermissions perms = container.GetPermissions();
perms.SharedAccessPolicies.Clear();
container.SetPermissions(perms);

//Create a new access policy on the container, which may be optionally used to provide constraints for
//shared access signatures on the container and the blob.
string sharedAccessPolicyName = "tutorialpolicy";
CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);
```

<span data-ttu-id="03d91-163">Когда вы удаляете политики доступа в контейнере, необходимо сначала получить его имеющиеся разрешения, удалить их, а затем снова задать.</span><span class="sxs-lookup"><span data-stu-id="03d91-163">When you clear the access policies on a container, you must first get the container's existing permissions, then clear the permissions, then set the permissions again.</span></span>

### <a name="generate-a-shared-access-signature-uri-on-the-container-that-uses-an-access-policy"></a><span data-ttu-id="03d91-164">Создание URI подписанного URL-адреса для контейнера, использующего политику доступа</span><span class="sxs-lookup"><span data-stu-id="03d91-164">Generate a shared access signature URI on the container that uses an access policy</span></span>
<span data-ttu-id="03d91-165">Далее мы создадим другой подписанный URL-адрес для созданного ранее контейнера, но на этот раз мы свяжем подпись с хранимой политикой доступа, созданной в предыдущем примере.</span><span class="sxs-lookup"><span data-stu-id="03d91-165">Next, we create another shared access signature for the container that we created earlier, but this time we associate the signature with the stored access policy we created in the previous example.</span></span>

<span data-ttu-id="03d91-166">Добавьте новый метод для создания другого подписанного URL-адреса для контейнера:</span><span class="sxs-lookup"><span data-stu-id="03d91-166">Add a new method to generate another shared access signature for the container:</span></span>

```csharp
static string GetContainerSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Generate the shared access signature on the container. In this case, all of the constraints for the
    //shared access signature are specified on the stored access policy.
    string sasContainerToken = container.GetSharedAccessSignature(null, policyName);

    //Return the URI string for the container, including the SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="03d91-167">В нижнюю часть метода **Main()** перед вызовом **Console.ReadLine()** добавьте следующие строки, чтобы вызвать метод **GetContainerSasUriWithPolicy**:</span><span class="sxs-lookup"><span data-stu-id="03d91-167">At the bottom of the **Main()** method, before the call to **Console.ReadLine()**, add the following lines to call the **GetContainerSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for the container, using a stored access policy to set constraints on the SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-the-blob-that-uses-an-access-policy"></a><span data-ttu-id="03d91-168">Создание URI подписи общего доступа для BLOB-объекта, использующей политику доступа</span><span class="sxs-lookup"><span data-stu-id="03d91-168">Generate a Shared Access Signature URI on the Blob That Uses an Access Policy</span></span>
<span data-ttu-id="03d91-169">Наконец мы добавим аналогичный метод для создания другого большого двоичного объекта и подписанного URL-адреса, сопоставленного с хранимой политикой доступа.</span><span class="sxs-lookup"><span data-stu-id="03d91-169">Finally, we add a similar method to create another blob and generate a shared access signature that's associated with a stored access policy.</span></span>

<span data-ttu-id="03d91-170">Добавьте новый метод для создания BLOB-объекта и подписи общего доступа:</span><span class="sxs-lookup"><span data-stu-id="03d91-170">Add a new method to create a blob and generate a shared access signature:</span></span>

```csharp
static string GetBlobSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Get a reference to a blob within the container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblobpolicy.txt");

    //Upload text to the blob. If the blob does not yet exist, it will be created.
    //If the blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible to clients via a shared access signature. " +
    "A stored access policy defines the constraints for the signature.";
    MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    ms.Position = 0;
    using (ms)
    {
        blob.UploadFromStream(ms);
    }

    //Generate the shared access signature on the blob.
    string sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

    //Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="03d91-171">В нижнюю часть метода **Main()** перед вызовом **Console.ReadLine()** добавьте следующие строки, чтобы вызвать метод **GetBlobSasUriWithPolicy**:</span><span class="sxs-lookup"><span data-stu-id="03d91-171">At the bottom of the **Main()** method, before the call to **Console.ReadLine()**, add the following lines to call the **GetBlobSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for a blob within the container, using a stored access policy to set constraints on the SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

<span data-ttu-id="03d91-172">Теперь метод **Main()** должен выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="03d91-172">The **Main()** method should now look like this in its entirety.</span></span> <span data-ttu-id="03d91-173">Запустите его, чтобы записать URI подписей общего доступа в окне консоли, а затем скопируйте и вставьте их в текстовый файл для использования во второй части учебника.</span><span class="sxs-lookup"><span data-stu-id="03d91-173">Run it to write the shared access signature URIs to the console window, then copy and paste them into a text file for use in the second part of this tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    //Parse the connection string and return a reference to the storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create the blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference to a container to use for the sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Generate a SAS URI for the container, without a stored access policy.
    Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
    Console.WriteLine();

    //Generate a SAS URI for a blob within the container, without a stored access policy.
    Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
    Console.WriteLine();

    //Clear any existing access policies on container.
    BlobContainerPermissions perms = container.GetPermissions();
    perms.SharedAccessPolicies.Clear();
    container.SetPermissions(perms);

    //Create a new access policy on the container, which may be optionally used to provide constraints for
    //shared access signatures on the container and the blob.
    string sharedAccessPolicyName = "tutorialpolicy";
    CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);

    //Generate a SAS URI for the container, using a stored access policy to set constraints on the SAS.
    Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    //Generate a SAS URI for a blob within the container, using a stored access policy to set constraints on the SAS.
    Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    Console.ReadLine();
}
```

<span data-ttu-id="03d91-174">При запуске консольного приложения GenerateSharedAccessSignatures его результат должен быть аналогичен приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="03d91-174">When you run the GenerateSharedAccessSignatures console application, you'll see output similar to the following.</span></span> <span data-ttu-id="03d91-175">Это подписанные URL-адреса, которые используются во второй части руководства.</span><span class="sxs-lookup"><span data-stu-id="03d91-175">These are the shared access signatures you use in Part 2 of the tutorial.</span></span>

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-to-test-the-shared-access-signatures"></a><span data-ttu-id="03d91-176">Часть 2. Создание консольного приложения для проверки подписанных URL-адресов</span><span class="sxs-lookup"><span data-stu-id="03d91-176">Part 2: Create a console application to test the shared access signatures</span></span>
<span data-ttu-id="03d91-177">Чтобы проверить подписанные URL-адреса, созданные в предыдущих примерах, мы создадим второе консольное приложение, использующее подписи для выполнения операций с контейнером и большим двоичным объектом.</span><span class="sxs-lookup"><span data-stu-id="03d91-177">To test the shared access signatures created in the previous examples, we create a second console application that uses the signatures to perform operations on the container and on a blob.</span></span>

> [!NOTE]
> <span data-ttu-id="03d91-178">Если с момента прохождения первой части учебника прошло больше 24 часов, созданные подписи будут недействительными.</span><span class="sxs-lookup"><span data-stu-id="03d91-178">If more than 24 hours have passed since you completed the first part of the tutorial, the signatures you generated will no longer be valid.</span></span> <span data-ttu-id="03d91-179">В этом случае следует запустить код в первом консольном приложении для создания новых подписей общего доступа, которые можно использовать во второй части учебника.</span><span class="sxs-lookup"><span data-stu-id="03d91-179">In this case, you should run the code in the first console application to generate fresh shared access signatures for use in the second part of the tutorial.</span></span>
>

<span data-ttu-id="03d91-180">В Visual Studio создайте новое консольное приложение Windows и назовите его **ConsumeSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="03d91-180">In Visual Studio, create a new Windows console application and name it **ConsumeSharedAccessSignatures**.</span></span> <span data-ttu-id="03d91-181">Как и раньше, добавьте ссылки на [Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) и [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="03d91-181">Add references to [Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), as you did previously.</span></span>

<span data-ttu-id="03d91-182">Добавьте в начало файла Program.cs следующие директивы **using**:</span><span class="sxs-lookup"><span data-stu-id="03d91-182">At the top of the Program.cs file, add the following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="03d91-183">В тело метода **Main()** добавьте следующие строковые константы и измените их значения на подписанные URL-адреса, созданные в первой части руководства.</span><span class="sxs-lookup"><span data-stu-id="03d91-183">In the body of the **Main()** method, add the following string constants, changing their values to the shared access signatures you generated in part 1 of the tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-to-try-container-operations-using-a-shared-access-signature"></a><span data-ttu-id="03d91-184">Добавление метода для оценки операций с контейнером с использованием подписанного URL-адреса</span><span class="sxs-lookup"><span data-stu-id="03d91-184">Add a method to try container operations using a shared access signature</span></span>
<span data-ttu-id="03d91-185">Далее мы добавим метод, который проверяет некоторые операции с контейнером, используя подписанный URL-адрес для этого контейнера.</span><span class="sxs-lookup"><span data-stu-id="03d91-185">Next, we add a method that tests some container operations using a shared access signature for the container.</span></span> <span data-ttu-id="03d91-186">Подписанный URL-адрес используется для возврата ссылки на контейнер, обеспечивая проверку подлинности доступа к контейнеру на основании одной подписи.</span><span class="sxs-lookup"><span data-stu-id="03d91-186">The shared access signature is used to return a reference to the container, authenticating access to the container based on the signature alone.</span></span>

<span data-ttu-id="03d91-187">Добавьте в класс Program.cs следующий метод:</span><span class="sxs-lookup"><span data-stu-id="03d91-187">Add the following method to Program.cs:</span></span>

```csharp
static void UseContainerSAS(string sas)
{
    //Try performing container operations with the SAS provided.

    //Return a reference to the container using the SAS URI.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(sas));

    //Create a list to store blob URIs returned by a listing operation on the container.
    List<ICloudBlob> blobList = new List<ICloudBlob>();

    //Write operation: write a new blob to the container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference("blobCreatedViaSAS.txt");
        string blobContent = "This blob was created with a shared access signature granting write permissions to the container. ";
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

    //List operation: List the blobs in the container.
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

    //Read operation: Get a reference to one of the blobs in the container and read it.
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

    //Delete operation: Delete a blob in the container.
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

<span data-ttu-id="03d91-188">Измените метод **Main()** для вызова **UseContainerSAS()** с обоими подписанными URL-адресами, созданными в контейнере:</span><span class="sxs-lookup"><span data-stu-id="03d91-188">Update the **Main()** method to call **UseContainerSAS()** with both of the shared access signatures you created on the container:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call the test methods with the shared access signatures created on the container, with and without the access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    Console.ReadLine();
}
```

### <a name="add-a-method-to-try-blob-operations-using-a-shared-access-signature"></a><span data-ttu-id="03d91-189">Добавление метода для оценки операций с большим двоичным объектом с использованием подписанного URL-адреса</span><span class="sxs-lookup"><span data-stu-id="03d91-189">Add a method to try blob operations using a shared access signature</span></span>
<span data-ttu-id="03d91-190">Наконец, мы добавим метод, который проверяет некоторые операции с большим двоичным объектом, используя подписанный URL-адрес для этого большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="03d91-190">Finally, we add a method that tests some blob operations using a shared access signature on the blob.</span></span> <span data-ttu-id="03d91-191">В этом случае мы используем конструктор **CloudBlockBlob(String)**, передавая подписанный URL-адрес, чтобы возвратить ссылку на большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="03d91-191">In this case, we use the constructor **CloudBlockBlob(String)**, passing in the shared access signature, to return a reference to the blob.</span></span> <span data-ttu-id="03d91-192">Никакая другая проверка подлинности не требуется, она основана только на подписи.</span><span class="sxs-lookup"><span data-stu-id="03d91-192">No other authentication is required; it's based on the signature alone.</span></span>

<span data-ttu-id="03d91-193">Добавьте в класс Program.cs следующий метод:</span><span class="sxs-lookup"><span data-stu-id="03d91-193">Add the following method to Program.cs:</span></span>

```csharp
static void UseBlobSAS(string sas)
{
    //Try performing blob operations using the SAS provided.

    //Return a reference to the blob using the SAS URI.
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(sas));

    //Write operation: Write a new blob to the container.
    try
    {
        string blobContent = "This blob was created with a shared access signature granting write permissions to the blob. ";
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

    //Read operation: Read the contents of the blob.
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

    //Delete operation: Delete the blob.
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

<span data-ttu-id="03d91-194">Измените метод **Main()** для вызова **UseBlobSAS()** с обоими подписанными URL-адресами, созданными для BLOB-объекта:</span><span class="sxs-lookup"><span data-stu-id="03d91-194">Update the **Main()** method to call **UseBlobSAS()** with both of the shared access signatures that you created on the blob:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call the test methods with the shared access signatures created on the container, with and without the access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    //Call the test methods with the shared access signatures created on the blob, with and without the access policy.
    UseBlobSAS(blobSAS);
    UseBlobSAS(blobSASWithAccessPolicy);

    Console.ReadLine();
}
```

<span data-ttu-id="03d91-195">Запустите консольное приложение и просмотрите выходные данные, чтобы узнать, какие операции разрешены для разных подписей.</span><span class="sxs-lookup"><span data-stu-id="03d91-195">Run the console application and observe the output to see which operations are permitted for which signatures.</span></span> <span data-ttu-id="03d91-196">Выходные данные в окне консоли будут выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="03d91-196">The output in the console window will look similar to the following:</span></span>

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: The remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: The remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a><span data-ttu-id="03d91-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="03d91-197">Next Steps</span></span>

* [<span data-ttu-id="03d91-198">Подписанные URL-адреса. Часть 1: общие сведения о модели SAS</span><span class="sxs-lookup"><span data-stu-id="03d91-198">Shared Access Signatures, Part 1: Understanding the SAS Model</span></span>](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="03d91-199">Управление анонимным доступом на чтение к контейнерам и большим двоичным объектам</span><span class="sxs-lookup"><span data-stu-id="03d91-199">Manage anonymous read access to containers and blobs</span></span>](storage-manage-access-to-resources.md)
* <span data-ttu-id="03d91-200">[Delegating Access with a Shared Access Signature](http://msdn.microsoft.com/library/azure/ee395415.aspx) (Делегирование доступа с помощью подписанного URL-адреса)</span><span class="sxs-lookup"><span data-stu-id="03d91-200">[Delegating access with a shared access signature (REST API)](http://msdn.microsoft.com/library/azure/ee395415.aspx)</span></span>
* [<span data-ttu-id="03d91-201">Введение в использование SAS таблиц и очередей</span><span class="sxs-lookup"><span data-stu-id="03d91-201">Introducing Table and Queue SAS</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
