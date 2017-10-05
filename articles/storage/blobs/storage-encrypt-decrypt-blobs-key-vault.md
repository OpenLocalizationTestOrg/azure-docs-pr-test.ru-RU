---
title: "Руководство. Шифрование и расшифровка больших двоичных объектов в службе хранилища Azure с помощью Azure Key Vault | Документация Майкрософт"
description: "Как выполнять шифрование и расшифровку большого двоичного объекта путем шифрования на стороне клиента для службы хранилища Microsoft Azure с помощью Azure Key Vault."
services: storage
documentationcenter: 
author: adhurwit
manager: jasonsav
editor: tysonn
ms.assetid: 027e8631-c1bf-48c1-9d9b-f6843e88b583
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 01/23/2017
ms.author: adhurwit
ms.openlocfilehash: a2a3a4773d33fe6b8589ad8d9d219acda4d1015e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a><span data-ttu-id="83a8b-103">Шифрование и расшифровка BLOB-объектов в хранилище Microsoft Azure с помощью хранилища ключей Azure</span><span class="sxs-lookup"><span data-stu-id="83a8b-103">Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="83a8b-104">Введение</span><span class="sxs-lookup"><span data-stu-id="83a8b-104">Introduction</span></span>
<span data-ttu-id="83a8b-105">В этом учебнике описывается, как использовать хранилище ключей Azure для шифрования хранилища на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="83a8b-105">This tutorial covers how to make use of client-side storage encryption with Azure Key Vault.</span></span> <span data-ttu-id="83a8b-106">Учебник включает пошаговое руководство по шифрованию и расшифровке большого двоичного объекта в консольном приложении с помощью этих технологий.</span><span class="sxs-lookup"><span data-stu-id="83a8b-106">It walks you through how to encrypt and decrypt a blob in a console application using these technologies.</span></span>

<span data-ttu-id="83a8b-107">**Предполагаемое время выполнения:** 20 минут</span><span class="sxs-lookup"><span data-stu-id="83a8b-107">**Estimated time to complete:** 20 minutes</span></span>

<span data-ttu-id="83a8b-108">Общие сведения о хранилище ключей Azure см. в статье [Что такое хранилище ключей Azure?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="83a8b-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="83a8b-109">Общие сведения о шифровании на стороне клиента для службы хранилища Azure см. в статье [Шифрование на стороне клиента для службы хранилища Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="83a8b-109">For overview information about client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83a8b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="83a8b-110">Prerequisites</span></span>
<span data-ttu-id="83a8b-111">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="83a8b-111">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="83a8b-112">Учетная запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="83a8b-112">An Azure Storage account</span></span>
* <span data-ttu-id="83a8b-113">Visual Studio 2013 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="83a8b-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="83a8b-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="83a8b-114">Azure PowerShell</span></span>

## <a name="overview-of-client-side-encryption"></a><span data-ttu-id="83a8b-115">Обзор шифрования на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="83a8b-115">Overview of client-side encryption</span></span>
<span data-ttu-id="83a8b-116">Общие сведения о шифровании на стороне клиента для службы хранилища Azure см. в статье [Шифрование на стороне клиента для службы хранилища Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="83a8b-116">For an overview of client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)</span></span>

<span data-ttu-id="83a8b-117">Вот краткое описание того, как работает шифрование на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="83a8b-117">Here is a brief description of how client side encryption works:</span></span>

1. <span data-ttu-id="83a8b-118">Пакет SDK клиента хранилища Azure создает ключ шифрования содержимого (CEK), который является одноразовым симметричным ключом.</span><span class="sxs-lookup"><span data-stu-id="83a8b-118">The Azure Storage client SDK generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="83a8b-119">Данные пользователей шифруются с помощью этого ключа CEK.</span><span class="sxs-lookup"><span data-stu-id="83a8b-119">Customer data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="83a8b-120">Ключ CEK, в свою очередь, шифруется с помощью ключа шифрования ключа KEK.</span><span class="sxs-lookup"><span data-stu-id="83a8b-120">The CEK is then wrapped (encrypted) using the key encryption key (KEK).</span></span> <span data-ttu-id="83a8b-121">Ключ KEK определяется идентификатором ключа и может быть парой асимметричных ключей или симметричным ключом. Вы можете управлять им локально или хранить его в хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="83a8b-121">The KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vault.</span></span> <span data-ttu-id="83a8b-122">У самого клиента хранилища нет доступа к KEK.</span><span class="sxs-lookup"><span data-stu-id="83a8b-122">The Storage client itself never has access to the KEK.</span></span> <span data-ttu-id="83a8b-123">Он просто вызывает алгоритм шифрования ключа, предоставляемый хранилищем ключей.</span><span class="sxs-lookup"><span data-stu-id="83a8b-123">It just invokes the key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="83a8b-124">Пользователи могут при необходимости использовать настраиваемые поставщики для шифрования и расшифровки ключа.</span><span class="sxs-lookup"><span data-stu-id="83a8b-124">Customers can choose to use custom providers for key wrapping/unwrapping if they want.</span></span>
4. <span data-ttu-id="83a8b-125">Зашифрованные данные затем передаются в службу хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="83a8b-125">The encrypted data is then uploaded to the Azure Storage service.</span></span>

## <a name="set-up-your-azure-key-vault"></a><span data-ttu-id="83a8b-126">Настройка хранилища ключей Azure</span><span class="sxs-lookup"><span data-stu-id="83a8b-126">Set up your Azure Key Vault</span></span>
<span data-ttu-id="83a8b-127">Для продолжения работы с этим учебником необходимо выполнить следующие действия, описанные в руководстве [Приступая к работе с хранилищем ключей Azure](../../key-vault/key-vault-get-started.md):</span><span class="sxs-lookup"><span data-stu-id="83a8b-127">In order to proceed with this tutorial, you need to do the following steps, which are outlined in the tutorial  [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md):</span></span>

* <span data-ttu-id="83a8b-128">Создать хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="83a8b-128">Create a key vault.</span></span>
* <span data-ttu-id="83a8b-129">Добавить ключ или секрет в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="83a8b-129">Add a key or secret to the key vault.</span></span>
* <span data-ttu-id="83a8b-130">Зарегистрировать приложение в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="83a8b-130">Register an application with Azure Active Directory.</span></span>
* <span data-ttu-id="83a8b-131">Разрешить приложению использовать ключ или секрет.</span><span class="sxs-lookup"><span data-stu-id="83a8b-131">Authorize the application to use the key or secret.</span></span>

<span data-ttu-id="83a8b-132">Запишите ClientID и ClientSecret, сформированные при регистрации приложения в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="83a8b-132">Make note of the ClientID and ClientSecret that were generated when registering an application with Azure Active Directory.</span></span>

<span data-ttu-id="83a8b-133">Создайте оба ключа в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="83a8b-133">Create both keys in the key vault.</span></span> <span data-ttu-id="83a8b-134">В этом учебнике подразумевается, что вы использовали следующие имена: ContosoKeyVault и TestRSAKey1.</span><span class="sxs-lookup"><span data-stu-id="83a8b-134">We assume for the rest of the tutorial that you have used the following names: ContosoKeyVault and TestRSAKey1.</span></span>

## <a name="create-a-console-application-with-packages-and-appsettings"></a><span data-ttu-id="83a8b-135">Создание консольного приложения с пакетами и AppSettings</span><span class="sxs-lookup"><span data-stu-id="83a8b-135">Create a console application with packages and AppSettings</span></span>
<span data-ttu-id="83a8b-136">Создайте новое консольное приложение в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="83a8b-136">In Visual Studio, create a new console application.</span></span>

<span data-ttu-id="83a8b-137">Добавьте необходимые пакеты NuGet в консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="83a8b-137">Add necessary nuget packages in the Package Manager Console.</span></span>

```
Install-Package WindowsAzure.Storage

// This is the latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

<span data-ttu-id="83a8b-138">Добавьте AppSettings в файл App.Config.</span><span class="sxs-lookup"><span data-stu-id="83a8b-138">Add AppSettings to the App.Config.</span></span>

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

<span data-ttu-id="83a8b-139">Добавьте следующие инструкции `using` и обязательно добавьте в проект ссылку на System.Configuration.</span><span class="sxs-lookup"><span data-stu-id="83a8b-139">Add the following `using` statements and make sure to add a reference to System.Configuration to the project.</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Configuration;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.Azure.KeyVault;
using System.Threading;        
using System.IO;
```

## <a name="add-a-method-to-get-a-token-to-your-console-application"></a><span data-ttu-id="83a8b-140">Добавление метода получения токена в консольное приложение</span><span class="sxs-lookup"><span data-stu-id="83a8b-140">Add a method to get a token to your console application</span></span>
<span data-ttu-id="83a8b-141">Следующий метод используется классами хранилища ключей, когда необходимо пройти проверку подлинности для доступа к вашему хранилищу ключей.</span><span class="sxs-lookup"><span data-stu-id="83a8b-141">The following method is used by Key Vault classes that need to authenticate for access to your key vault.</span></span>

```csharp
private async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);
    ClientCredential clientCred = new ClientCredential(
        ConfigurationManager.AppSettings["clientId"],
        ConfigurationManager.AppSettings["clientSecret"]);
    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)
        throw new InvalidOperationException("Failed to obtain the JWT token");

    return result.AccessToken;
}
```

## <a name="access-storage-and-key-vault-in-your-program"></a><span data-ttu-id="83a8b-142">Доступ к хранилищу данных и хранилищу ключей в программе.</span><span class="sxs-lookup"><span data-stu-id="83a8b-142">Access Storage and Key Vault in your program</span></span>
<span data-ttu-id="83a8b-143">Добавьте следующий код в функцию Main:</span><span class="sxs-lookup"><span data-stu-id="83a8b-143">In the Main function, add the following code.</span></span>

```csharp
// This is standard code to interact with Blob storage.
StorageCredentials creds = new StorageCredentials(
    ConfigurationManager.AppSettings["accountName"],
       ConfigurationManager.AppSettings["accountKey"]);
CloudStorageAccount account = new CloudStorageAccount(creds, useHttps: true);
CloudBlobClient client = account.CreateCloudBlobClient();
CloudBlobContainer contain = client.GetContainerReference(ConfigurationManager.AppSettings["container"]);
contain.CreateIfNotExists();

// The Resolver object is used to interact with Key Vault for Azure Storage.
// This is where the GetToken method from above is used.
KeyVaultKeyResolver cloudResolver = new KeyVaultKeyResolver(GetToken);
```

> [!NOTE]
> <span data-ttu-id="83a8b-144">Объектные модели хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="83a8b-144">Key Vault Object Models</span></span>
> 
> <span data-ttu-id="83a8b-145">Важно понимать, что фактически существуют две объектные модели хранилища ключей, которые необходимо принимать во внимание: одна основана на API REST (пространство имен KeyVault), а другая представляет собой расширение для шифрования на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="83a8b-145">It is important to understand that there are actually two Key Vault object models to be aware of: one is based on the REST API (KeyVault namespace) and the other is an extension for client-side encryption.</span></span>
> 
> <span data-ttu-id="83a8b-146">Клиент хранилища ключей взаимодействует с REST API и понимает веб-ключи и секреты JSON для двух видов элементов, содержащихся в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="83a8b-146">The Key Vault Client interacts with the REST API and understands JSON Web Keys and secrets for the two kinds of things that are contained in Key Vault.</span></span>
> 
> <span data-ttu-id="83a8b-147">Расширения хранилища ключей — это классы, которые специально созданы для шифрования на стороне клиента в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="83a8b-147">The Key Vault Extensions are classes that seem specifically created for client-side encryption in Azure Storage.</span></span> <span data-ttu-id="83a8b-148">Они содержат интерфейс для ключей (IKey) и классов, основанный на концепции сопоставителя ключей.</span><span class="sxs-lookup"><span data-stu-id="83a8b-148">They contain an interface for keys (IKey) and classes based on the concept of a Key Resolver.</span></span> <span data-ttu-id="83a8b-149">Существуют две реализации IKey, которые необходимо знать, — RSAKey и SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="83a8b-149">There are two implementations of IKey that you need to know: RSAKey and SymmetricKey.</span></span> <span data-ttu-id="83a8b-150">Они совпадают с элементами, которые находятся в хранилище ключей, но на данный момент остаются независимыми классами (таким образом, ключ и секретный код, получаемые клиентом хранилища ключей, не реализуют IKey).</span><span class="sxs-lookup"><span data-stu-id="83a8b-150">Now they happen to coincide with the things that are contained in a Key Vault, but at this point they are independent classes (so the Key and Secret retrieved by the Key Vault Client do not implement IKey).</span></span>
> 
> 

## <a name="encrypt-blob-and-upload"></a><span data-ttu-id="83a8b-151">Шифрование и передача BLOB-объекта</span><span class="sxs-lookup"><span data-stu-id="83a8b-151">Encrypt blob and upload</span></span>
<span data-ttu-id="83a8b-152">Добавьте следующий код, чтобы зашифровать BLOB-объект и передать его в свою учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="83a8b-152">Add the following code to encrypt a blob and upload it to your Azure storage account.</span></span> <span data-ttu-id="83a8b-153">Затем используется метод **ResolveKeyAsync**, который возвращает IKey.</span><span class="sxs-lookup"><span data-stu-id="83a8b-153">The **ResolveKeyAsync** method that is used returns an IKey.</span></span>

```csharp
// Retrieve the key that you created previously.
// The IKey that is returned here is an RsaKey.
// Remember that we used the names contosokeyvault and testrsakey1.
var rsa = cloudResolver.ResolveKeyAsync("https://contosokeyvault.vault.azure.net/keys/TestRSAKey1", CancellationToken.None).GetAwaiter().GetResult();

// Now you simply use the RSA key to encrypt by setting it in the BlobEncryptionPolicy.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(rsa, null);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

// Reference a block blob.
CloudBlockBlob blob = contain.GetBlockBlobReference("MyFile.txt");

// Upload using the UploadFromStream method.
using (var stream = System.IO.File.OpenRead(@"C:\data\MyFile.txt"))
    blob.UploadFromStream(stream, stream.Length, null, options, null);
```

<span data-ttu-id="83a8b-154">Ниже приведен снимок экрана с [классического портала Azure](https://manage.windowsazure.com) для большого двоичного объекта, зашифрованного с помощью шифрования на стороне клиента с ключом, хранящимся в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="83a8b-154">Following is a screenshot from the [Azure Classic Portal](https://manage.windowsazure.com) for a blob that has been encrypted by using client-side encryption with a key stored in Key Vault.</span></span> <span data-ttu-id="83a8b-155">Свойство **KeyId** представляет собой URI данного ключа в хранилище ключей, которое выступает в качестве ключа шифрования ключей.</span><span class="sxs-lookup"><span data-stu-id="83a8b-155">The **KeyId** property is the URI for the key in Key Vault that acts as the KEK.</span></span> <span data-ttu-id="83a8b-156">Свойство **EncryptedKey** содержит зашифрованную версию ключа шифрования столбца.</span><span class="sxs-lookup"><span data-stu-id="83a8b-156">The **EncryptedKey** property contains the encrypted version of the CEK.</span></span>

![Снимок экрана, показывающий метаданные большого двоичного объекта, содержащие метаданные шифрования](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> <span data-ttu-id="83a8b-158">Если вы рассмотрите конструктор BlobEncryptionPolicy, вы увидите, что он может принимать ключ и (или) сопоставитель.</span><span class="sxs-lookup"><span data-stu-id="83a8b-158">If you look at the BlobEncryptionPolicy constructor, you will see that it can accept a key and/or a resolver.</span></span> <span data-ttu-id="83a8b-159">Необходимо помнить, что сейчас сопоставитель нельзя использовать для шифрования, так как он не поддерживает ключ по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="83a8b-159">Be aware that right now you cannot use a resolver for encryption because it does not currently support a default key.</span></span>
> 
> 

## <a name="decrypt-blob-and-download"></a><span data-ttu-id="83a8b-160">Расшифруйте BLOB-объект и загрузите его</span><span class="sxs-lookup"><span data-stu-id="83a8b-160">Decrypt blob and download</span></span>
<span data-ttu-id="83a8b-161">Расшифровка работает, когда использование классов сопоставителя имеет смысл.</span><span class="sxs-lookup"><span data-stu-id="83a8b-161">Decryption is really when using the Resolver classes make sense.</span></span> <span data-ttu-id="83a8b-162">Идентификатор ключа, используемого для шифрования, связан с BLOB-объектом в своих метаданных, поэтому не нужно извлекать ключ и запоминать связь между ключом и BLOB-объектом.</span><span class="sxs-lookup"><span data-stu-id="83a8b-162">The ID of the key used for encryption is associated with the blob in its metadata, so there is no reason for you to retrieve the key and remember the association between key and blob.</span></span> <span data-ttu-id="83a8b-163">Необходимо просто убедиться, что ключ по-прежнему находится в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="83a8b-163">You just have to make sure that the key remains in Key Vault.</span></span>   

<span data-ttu-id="83a8b-164">Закрытый ключ RSA Key остается в хранилище ключей, поэтому для расшифровки зашифрованный ключ из метаданных BLOB-объекта, содержащего CEК, отправляется в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="83a8b-164">The private key of an RSA Key remains in Key Vault, so for decryption to occur, the Encrypted Key from the blob metadata that contains the CEK is sent to Key Vault for decryption.</span></span>

<span data-ttu-id="83a8b-165">Добавьте следующий код для расшифровки отправленного большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="83a8b-165">Add the following to decrypt the blob that you just uploaded.</span></span>

```csharp
// In this case, we will not pass a key and only pass the resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> <span data-ttu-id="83a8b-166">Существует несколько других видов сопоставителей, которые облегчают управление ключами, например AggregateKeyResolver и CachingKeyResolver.</span><span class="sxs-lookup"><span data-stu-id="83a8b-166">There are a couple of other kinds of resolvers to make key management easier, including: AggregateKeyResolver and CachingKeyResolver.</span></span>
> 
> 

## <a name="use-key-vault-secrets"></a><span data-ttu-id="83a8b-167">Использование секретов хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="83a8b-167">Use Key Vault secrets</span></span>
<span data-ttu-id="83a8b-168">Секрет можно использовать для шифрования на стороне клиента с помощью класса SymmetricKey, так как он фактически является симметричным ключом.</span><span class="sxs-lookup"><span data-stu-id="83a8b-168">The way to use a secret with client-side encryption is via the SymmetricKey class because a secret is essentially a symmetric key.</span></span> <span data-ttu-id="83a8b-169">Но, как указано выше, секрет в хранилище ключей не сопоставляется точно с SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="83a8b-169">But, as noted above, a secret in Key Vault does not map exactly to a SymmetricKey.</span></span> <span data-ttu-id="83a8b-170">Необходимо понять несколько вещей.</span><span class="sxs-lookup"><span data-stu-id="83a8b-170">There are a few things to understand:</span></span>

* <span data-ttu-id="83a8b-171">Ключ в SymmetricKey должен быть фиксированной длины: 128, 192, 256, 384 или 512 бит.</span><span class="sxs-lookup"><span data-stu-id="83a8b-171">The key in a SymmetricKey has to be a fixed length: 128, 192, 256, 384, or 512 bits.</span></span>
* <span data-ttu-id="83a8b-172">Ключ в SymmetricKey должен быть в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="83a8b-172">The key in a SymmetricKey should be Base64 encoded.</span></span>
* <span data-ttu-id="83a8b-173">Секрет хранилища ключей, который будет использоваться в качестве SymmetricKey, должен иметь тип содержимого application/octet-stream в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="83a8b-173">A Key Vault secret that will be used as a SymmetricKey needs to have a Content Type of "application/octet-stream" in Key Vault.</span></span>

<span data-ttu-id="83a8b-174">Ниже приведен пример использования PowerShell для создания в хранилище ключей секрета, который можно использовать как SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="83a8b-174">Here is an example in PowerShell of creating a secret in Key Vault that can be used as a SymmetricKey.</span></span>
<span data-ttu-id="83a8b-175">Имейте ввиду, что жестко запрограммированное значение $key приводится только для примера.</span><span class="sxs-lookup"><span data-stu-id="83a8b-175">Please note that the hard coded value, $key, is for demonstration purpose only.</span></span> <span data-ttu-id="83a8b-176">Сгенерируйте этот ключ в своем собственном коде.</span><span class="sxs-lookup"><span data-stu-id="83a8b-176">In your own code you'll want to generate this key.</span></span>

```csharp
// Here we are making a 128-bit key so we have 16 characters.
//     The characters are in the ASCII range of UTF8 so they are
//    each 1 byte. 16 x 8 = 128.
$key = "qwertyuiopasdfgh"
$b = [System.Text.Encoding]::UTF8.GetBytes($key)
$enc = [System.Convert]::ToBase64String($b)
$secretvalue = ConvertTo-SecureString $enc -AsPlainText -Force

// Substitute the VaultName and Name in this command.
$secret = Set-AzureKeyVaultSecret -VaultName 'ContoseKeyVault' -Name 'TestSecret2' -SecretValue $secretvalue -ContentType "application/octet-stream"
```

<span data-ttu-id="83a8b-177">Для получения этого секрета как SymmetricKey в консольном приложении можно использовать тот же вызов, что и ранее.</span><span class="sxs-lookup"><span data-stu-id="83a8b-177">In your console application, you can use the same call as before to retrieve this secret as a SymmetricKey.</span></span>

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
<span data-ttu-id="83a8b-178">Вот и все.</span><span class="sxs-lookup"><span data-stu-id="83a8b-178">That's it.</span></span> <span data-ttu-id="83a8b-179">Так просто!</span><span class="sxs-lookup"><span data-stu-id="83a8b-179">Enjoy!</span></span>

## <a name="next-steps"></a><span data-ttu-id="83a8b-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="83a8b-180">Next steps</span></span>
<span data-ttu-id="83a8b-181">Дополнительные сведения об использовании службы хранилища Microsoft Azure с C# см. в статье [Клиентская библиотека службы хранилища Microsoft Azure для .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="83a8b-181">For more information about using Microsoft Azure Storage with C#, see [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="83a8b-182">Дополнительные сведения о REST API для больших двоичных объектов см. в статье [REST API службы BLOB-объектов](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span><span class="sxs-lookup"><span data-stu-id="83a8b-182">For more information about the Blob REST API, see [Blob Service REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span></span>

<span data-ttu-id="83a8b-183">Новости о службе хранилища Microsoft Azure см. в [блоге команды разработчиков службы хранилища Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="83a8b-183">For the latest information on Microsoft Azure Storage, go to the [Microsoft Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>
