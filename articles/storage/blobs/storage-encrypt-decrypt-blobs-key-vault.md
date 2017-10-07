---
title: "Руководство. Шифрование и расшифровка больших двоичных объектов в службе хранилища Azure с помощью Azure Key Vault | Документация Майкрософт"
description: "Как tooencrypt и расшифровки большого двоичного объекта, с помощью шифрования на стороне клиента для службы хранилища Microsoft Azure с хранилищем ключей Azure."
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
ms.openlocfilehash: e387dd419a51b5b1df62d10ead97268e8295ff56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a><span data-ttu-id="bf16e-103">Шифрование и расшифровка BLOB-объектов в хранилище Microsoft Azure с помощью хранилища ключей Azure</span><span class="sxs-lookup"><span data-stu-id="bf16e-103">Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="bf16e-104">Введение</span><span class="sxs-lookup"><span data-stu-id="bf16e-104">Introduction</span></span>
<span data-ttu-id="bf16e-105">В этом учебнике описано, как использовать toomake шифрования хранилища на стороне клиента с хранилищем ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="bf16e-105">This tutorial covers how toomake use of client-side storage encryption with Azure Key Vault.</span></span> <span data-ttu-id="bf16e-106">Оно описано, как tooencrypt и расшифровки большого двоичного объекта в консольное приложение с использованием этих технологий.</span><span class="sxs-lookup"><span data-stu-id="bf16e-106">It walks you through how tooencrypt and decrypt a blob in a console application using these technologies.</span></span>

<span data-ttu-id="bf16e-107">**Предполагаемое время toocomplete:** 20 минут</span><span class="sxs-lookup"><span data-stu-id="bf16e-107">**Estimated time toocomplete:** 20 minutes</span></span>

<span data-ttu-id="bf16e-108">Общие сведения о хранилище ключей Azure см. в статье [Что такое хранилище ключей Azure?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="bf16e-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="bf16e-109">Общие сведения о шифровании на стороне клиента для службы хранилища Azure см. в статье [Шифрование на стороне клиента для службы хранилища Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bf16e-109">For overview information about client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf16e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bf16e-110">Prerequisites</span></span>
<span data-ttu-id="bf16e-111">toocomplete этого учебника необходимо иметь следующие hello:</span><span class="sxs-lookup"><span data-stu-id="bf16e-111">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="bf16e-112">Учетная запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="bf16e-112">An Azure Storage account</span></span>
* <span data-ttu-id="bf16e-113">Visual Studio 2013 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="bf16e-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="bf16e-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf16e-114">Azure PowerShell</span></span>

## <a name="overview-of-client-side-encryption"></a><span data-ttu-id="bf16e-115">Обзор шифрования на стороне клиента</span><span class="sxs-lookup"><span data-stu-id="bf16e-115">Overview of client-side encryption</span></span>
<span data-ttu-id="bf16e-116">Общие сведения о шифровании на стороне клиента для службы хранилища Azure см. в статье [Шифрование на стороне клиента для службы хранилища Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bf16e-116">For an overview of client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)</span></span>

<span data-ttu-id="bf16e-117">Вот краткое описание того, как работает шифрование на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="bf16e-117">Here is a brief description of how client side encryption works:</span></span>

1. <span data-ttu-id="bf16e-118">пакет SDK для клиента службы хранилища Azure Hello создает ключ шифрования содержимого (CEK), который является симметричным ключом, используйте один раз.</span><span class="sxs-lookup"><span data-stu-id="bf16e-118">hello Azure Storage client SDK generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="bf16e-119">Данные пользователей шифруются с помощью этого ключа CEK.</span><span class="sxs-lookup"><span data-stu-id="bf16e-119">Customer data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="bf16e-120">Hello CEK заключается в оболочку (зашифрованный) с помощью ключа hello ключа шифрования (ключ обмена Ключами).</span><span class="sxs-lookup"><span data-stu-id="bf16e-120">hello CEK is then wrapped (encrypted) using hello key encryption key (KEK).</span></span> <span data-ttu-id="bf16e-121">Hello KEK идентифицируется идентификатора ключа и может быть пары асимметричных ключей или симметричного ключа; его можно управлять локально и хранится в хранилище ключей Azure.</span><span class="sxs-lookup"><span data-stu-id="bf16e-121">hello KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vault.</span></span> <span data-ttu-id="bf16e-122">сам клиент хранилища Hello никогда не имеет доступа toohello ключа обмена Ключами.</span><span class="sxs-lookup"><span data-stu-id="bf16e-122">hello Storage client itself never has access toohello KEK.</span></span> <span data-ttu-id="bf16e-123">Он просто вызывает hello упаковка ключа алгоритма, предоставляемые хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="bf16e-123">It just invokes hello key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="bf16e-124">Клиенты могут выбрать toouse настраиваемых поставщиков для ключа, перенос и развертывание по желанию.</span><span class="sxs-lookup"><span data-stu-id="bf16e-124">Customers can choose toouse custom providers for key wrapping/unwrapping if they want.</span></span>
4. <span data-ttu-id="bf16e-125">Hello зашифрованные данные будет отправлен службе toohello хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="bf16e-125">hello encrypted data is then uploaded toohello Azure Storage service.</span></span>

## <a name="set-up-your-azure-key-vault"></a><span data-ttu-id="bf16e-126">Настройка хранилища ключей Azure</span><span class="sxs-lookup"><span data-stu-id="bf16e-126">Set up your Azure Key Vault</span></span>
<span data-ttu-id="bf16e-127">В порядке tooproceed к этому учебнику, необходим hello toodo следующие шаги, которые описаны в учебнике hello [приступить к работе с хранилищем ключей Azure](../../key-vault/key-vault-get-started.md):</span><span class="sxs-lookup"><span data-stu-id="bf16e-127">In order tooproceed with this tutorial, you need toodo hello following steps, which are outlined in hello tutorial  [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md):</span></span>

* <span data-ttu-id="bf16e-128">Создать хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="bf16e-128">Create a key vault.</span></span>
* <span data-ttu-id="bf16e-129">Добавление ключа или секретного toohello хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="bf16e-129">Add a key or secret toohello key vault.</span></span>
* <span data-ttu-id="bf16e-130">Зарегистрировать приложение в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bf16e-130">Register an application with Azure Active Directory.</span></span>
* <span data-ttu-id="bf16e-131">Авторизуйте hello приложения toouse hello ключа или секрета.</span><span class="sxs-lookup"><span data-stu-id="bf16e-131">Authorize hello application toouse hello key or secret.</span></span>

<span data-ttu-id="bf16e-132">Сделать заметку hello ClientID и ClientSecret, сформированные при регистрации приложения в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bf16e-132">Make note of hello ClientID and ClientSecret that were generated when registering an application with Azure Active Directory.</span></span>

<span data-ttu-id="bf16e-133">Создайте оба ключа в хранилище ключей hello.</span><span class="sxs-lookup"><span data-stu-id="bf16e-133">Create both keys in hello key vault.</span></span> <span data-ttu-id="bf16e-134">Мы предполагаем оставшейся hello hello учебника вы использовали hello следующие имена: ContosoKeyVault и TestRSAKey1.</span><span class="sxs-lookup"><span data-stu-id="bf16e-134">We assume for hello rest of hello tutorial that you have used hello following names: ContosoKeyVault and TestRSAKey1.</span></span>

## <a name="create-a-console-application-with-packages-and-appsettings"></a><span data-ttu-id="bf16e-135">Создание консольного приложения с пакетами и AppSettings</span><span class="sxs-lookup"><span data-stu-id="bf16e-135">Create a console application with packages and AppSettings</span></span>
<span data-ttu-id="bf16e-136">Создайте новое консольное приложение в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bf16e-136">In Visual Studio, create a new console application.</span></span>

<span data-ttu-id="bf16e-137">Добавление пакетов nuget, необходимые в hello консоль диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="bf16e-137">Add necessary nuget packages in hello Package Manager Console.</span></span>

```
Install-Package WindowsAzure.Storage

// This is hello latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

<span data-ttu-id="bf16e-138">Добавьте AppSettings toohello App.Config.</span><span class="sxs-lookup"><span data-stu-id="bf16e-138">Add AppSettings toohello App.Config.</span></span>

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

<span data-ttu-id="bf16e-139">Добавьте следующее hello `using` инструкций и убедитесь, что tooadd tooSystem.Configuration toohello ссылки проекта.</span><span class="sxs-lookup"><span data-stu-id="bf16e-139">Add hello following `using` statements and make sure tooadd a reference tooSystem.Configuration toohello project.</span></span>

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

## <a name="add-a-method-tooget-a-token-tooyour-console-application"></a><span data-ttu-id="bf16e-140">Добавьте метод tooget маркера tooyour консольного приложения</span><span class="sxs-lookup"><span data-stu-id="bf16e-140">Add a method tooget a token tooyour console application</span></span>
<span data-ttu-id="bf16e-141">Hello следующий метод используется классами хранилище ключей, tooauthenticate для хранилища ключей tooyour доступа.</span><span class="sxs-lookup"><span data-stu-id="bf16e-141">hello following method is used by Key Vault classes that need tooauthenticate for access tooyour key vault.</span></span>

```csharp
private async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);
    ClientCredential clientCred = new ClientCredential(
        ConfigurationManager.AppSettings["clientId"],
        ConfigurationManager.AppSettings["clientSecret"]);
    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)
        throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

## <a name="access-storage-and-key-vault-in-your-program"></a><span data-ttu-id="bf16e-142">Доступ к хранилищу данных и хранилищу ключей в программе.</span><span class="sxs-lookup"><span data-stu-id="bf16e-142">Access Storage and Key Vault in your program</span></span>
<span data-ttu-id="bf16e-143">В hello функции Main добавьте следующий код hello.</span><span class="sxs-lookup"><span data-stu-id="bf16e-143">In hello Main function, add hello following code.</span></span>

```csharp
// This is standard code toointeract with Blob storage.
StorageCredentials creds = new StorageCredentials(
    ConfigurationManager.AppSettings["accountName"],
       ConfigurationManager.AppSettings["accountKey"]);
CloudStorageAccount account = new CloudStorageAccount(creds, useHttps: true);
CloudBlobClient client = account.CreateCloudBlobClient();
CloudBlobContainer contain = client.GetContainerReference(ConfigurationManager.AppSettings["container"]);
contain.CreateIfNotExists();

// hello Resolver object is used toointeract with Key Vault for Azure Storage.
// This is where hello GetToken method from above is used.
KeyVaultKeyResolver cloudResolver = new KeyVaultKeyResolver(GetToken);
```

> [!NOTE]
> <span data-ttu-id="bf16e-144">Объектные модели хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="bf16e-144">Key Vault Object Models</span></span>
> 
> <span data-ttu-id="bf16e-145">Важно учитывать toobe моделирует toounderstand, фактически два объекта хранилища ключей: один основан на hello API REST (пространство имен KeyVault) и hello других — это расширение для шифрования на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="bf16e-145">It is important toounderstand that there are actually two Key Vault object models toobe aware of: one is based on hello REST API (KeyVault namespace) and hello other is an extension for client-side encryption.</span></span>
> 
> <span data-ttu-id="bf16e-146">Hello ключ хранилища клиента взаимодействует с API-интерфейса REST hello и понимает JSON Web ключи и секретные коды для hello два вида операций, которые находятся в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="bf16e-146">hello Key Vault Client interacts with hello REST API and understands JSON Web Keys and secrets for hello two kinds of things that are contained in Key Vault.</span></span>
> 
> <span data-ttu-id="bf16e-147">Hello ключ хранилища расширения — это классы, которые кажутся специально созданный для шифрования на стороне клиента в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="bf16e-147">hello Key Vault Extensions are classes that seem specifically created for client-side encryption in Azure Storage.</span></span> <span data-ttu-id="bf16e-148">Они содержат интерфейс для ключей (IKey) и классы, основанные на концепцию hello сопоставителя ключ.</span><span class="sxs-lookup"><span data-stu-id="bf16e-148">They contain an interface for keys (IKey) and classes based on hello concept of a Key Resolver.</span></span> <span data-ttu-id="bf16e-149">Существует два способа реализации необходимые tooknow IKey: RSAKey и SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="bf16e-149">There are two implementations of IKey that you need tooknow: RSAKey and SymmetricKey.</span></span> <span data-ttu-id="bf16e-150">Теперь выполняются toocoincide с hello вещей, которые находятся в хранилище ключей, но сейчас они независимых классы (то есть не реализуют IKey hello ключ и получить ключ хранилища клиента hello секрет).</span><span class="sxs-lookup"><span data-stu-id="bf16e-150">Now they happen toocoincide with hello things that are contained in a Key Vault, but at this point they are independent classes (so hello Key and Secret retrieved by hello Key Vault Client do not implement IKey).</span></span>
> 
> 

## <a name="encrypt-blob-and-upload"></a><span data-ttu-id="bf16e-151">Шифрование и передача BLOB-объекта</span><span class="sxs-lookup"><span data-stu-id="bf16e-151">Encrypt blob and upload</span></span>
<span data-ttu-id="bf16e-152">Добавьте следующую hello кода tooencrypt большой двоичный объект и передать его tooyour учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="bf16e-152">Add hello following code tooencrypt a blob and upload it tooyour Azure storage account.</span></span> <span data-ttu-id="bf16e-153">Hello **ResolveKeyAsync** IKey возвращает метод, который используется.</span><span class="sxs-lookup"><span data-stu-id="bf16e-153">hello **ResolveKeyAsync** method that is used returns an IKey.</span></span>

```csharp
// Retrieve hello key that you created previously.
// hello IKey that is returned here is an RsaKey.
// Remember that we used hello names contosokeyvault and testrsakey1.
var rsa = cloudResolver.ResolveKeyAsync("https://contosokeyvault.vault.azure.net/keys/TestRSAKey1", CancellationToken.None).GetAwaiter().GetResult();

// Now you simply use hello RSA key tooencrypt by setting it in hello BlobEncryptionPolicy.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(rsa, null);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

// Reference a block blob.
CloudBlockBlob blob = contain.GetBlockBlobReference("MyFile.txt");

// Upload using hello UploadFromStream method.
using (var stream = System.IO.File.OpenRead(@"C:\data\MyFile.txt"))
    blob.UploadFromStream(stream, stream.Length, null, options, null);
```

<span data-ttu-id="bf16e-154">Ниже приведен снимок экрана из hello [классический портал Azure](https://manage.windowsazure.com) для больших двоичных объектов, которые были зашифрованы при помощи ключа, хранящегося в хранилище ключей шифрования на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="bf16e-154">Following is a screenshot from hello [Azure Classic Portal](https://manage.windowsazure.com) for a blob that has been encrypted by using client-side encryption with a key stored in Key Vault.</span></span> <span data-ttu-id="bf16e-155">Hello **KeyId** свойство — hello URI для hello ключа в хранилище ключей, функционирующий как hello ключа обмена Ключами.</span><span class="sxs-lookup"><span data-stu-id="bf16e-155">hello **KeyId** property is hello URI for hello key in Key Vault that acts as hello KEK.</span></span> <span data-ttu-id="bf16e-156">Hello **EncryptedKey** свойство содержит зашифрованную версию hello hello CEK.</span><span class="sxs-lookup"><span data-stu-id="bf16e-156">hello **EncryptedKey** property contains hello encrypted version of hello CEK.</span></span>

![Снимок экрана, показывающий метаданные большого двоичного объекта, содержащие метаданные шифрования](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> <span data-ttu-id="bf16e-158">Если взглянуть на конструктор BlobEncryptionPolicy hello, вы увидите, он может принять ключ и/или сопоставителя.</span><span class="sxs-lookup"><span data-stu-id="bf16e-158">If you look at hello BlobEncryptionPolicy constructor, you will see that it can accept a key and/or a resolver.</span></span> <span data-ttu-id="bf16e-159">Необходимо помнить, что сейчас сопоставитель нельзя использовать для шифрования, так как он не поддерживает ключ по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="bf16e-159">Be aware that right now you cannot use a resolver for encryption because it does not currently support a default key.</span></span>
> 
> 

## <a name="decrypt-blob-and-download"></a><span data-ttu-id="bf16e-160">Расшифруйте BLOB-объект и загрузите его</span><span class="sxs-lookup"><span data-stu-id="bf16e-160">Decrypt blob and download</span></span>
<span data-ttu-id="bf16e-161">Расшифровка на самом деле при с помощью hello Сопоставитель классы смысла.</span><span class="sxs-lookup"><span data-stu-id="bf16e-161">Decryption is really when using hello Resolver classes make sense.</span></span> <span data-ttu-id="bf16e-162">Идентификатор Hello hello ключа, используемого для шифрования связан с hello большого двоичного объекта в его метаданных, нет причин для вас tooretrieve hello ключа и запоминать hello связь между ключом и больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="bf16e-162">hello ID of hello key used for encryption is associated with hello blob in its metadata, so there is no reason for you tooretrieve hello key and remember hello association between key and blob.</span></span> <span data-ttu-id="bf16e-163">Достаточно toomake том, что разделу hello остается в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="bf16e-163">You just have toomake sure that hello key remains in Key Vault.</span></span>   

<span data-ttu-id="bf16e-164">Hello закрытый ключ остается ключ RSA в хранилище ключей, поэтому для toooccur расшифровки hello зашифрованный ключ из метаданных hello BLOB-объект, содержащий приветствия CEK отправляется tooKey хранилище для расшифровки.</span><span class="sxs-lookup"><span data-stu-id="bf16e-164">hello private key of an RSA Key remains in Key Vault, so for decryption toooccur, hello Encrypted Key from hello blob metadata that contains hello CEK is sent tooKey Vault for decryption.</span></span>

<span data-ttu-id="bf16e-165">Добавьте следующие toodecrypt hello BLOB-объекта, только что переданный hello.</span><span class="sxs-lookup"><span data-stu-id="bf16e-165">Add hello following toodecrypt hello blob that you just uploaded.</span></span>

```csharp
// In this case, we will not pass a key and only pass hello resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> <span data-ttu-id="bf16e-166">Существует несколько других видов управления ключами toomake арбитры, проще, включая: AggregateKeyResolver и CachingKeyResolver.</span><span class="sxs-lookup"><span data-stu-id="bf16e-166">There are a couple of other kinds of resolvers toomake key management easier, including: AggregateKeyResolver and CachingKeyResolver.</span></span>
> 
> 

## <a name="use-key-vault-secrets"></a><span data-ttu-id="bf16e-167">Использование секретов хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="bf16e-167">Use Key Vault secrets</span></span>
<span data-ttu-id="bf16e-168">toouse Hello способ секретный код, с помощью шифрования на стороне клиента осуществляется через hello SymmetricKey класса, поскольку секрет — по существу это симметричный ключ.</span><span class="sxs-lookup"><span data-stu-id="bf16e-168">hello way toouse a secret with client-side encryption is via hello SymmetricKey class because a secret is essentially a symmetric key.</span></span> <span data-ttu-id="bf16e-169">Но, как указано выше, секрет в хранилище ключей не сопоставляет ровно tooa SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="bf16e-169">But, as noted above, a secret in Key Vault does not map exactly tooa SymmetricKey.</span></span> <span data-ttu-id="bf16e-170">Существует несколько вещей toounderstand:</span><span class="sxs-lookup"><span data-stu-id="bf16e-170">There are a few things toounderstand:</span></span>

* <span data-ttu-id="bf16e-171">ключ Hello в SymmetricKey имеет toobe фиксированной длины: 128, 192, 256, 384 и 512 бит.</span><span class="sxs-lookup"><span data-stu-id="bf16e-171">hello key in a SymmetricKey has toobe a fixed length: 128, 192, 256, 384, or 512 bits.</span></span>
* <span data-ttu-id="bf16e-172">ключ Hello в SymmetricKey должно быть в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="bf16e-172">hello key in a SymmetricKey should be Base64 encoded.</span></span>
* <span data-ttu-id="bf16e-173">Секрета хранилища ключей, который будет использоваться в качестве SymmetricKey должен toohave тип содержимого «application/octet-stream» в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="bf16e-173">A Key Vault secret that will be used as a SymmetricKey needs toohave a Content Type of "application/octet-stream" in Key Vault.</span></span>

<span data-ttu-id="bf16e-174">Ниже приведен пример использования PowerShell для создания в хранилище ключей секрета, который можно использовать как SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="bf16e-174">Here is an example in PowerShell of creating a secret in Key Vault that can be used as a SymmetricKey.</span></span>
<span data-ttu-id="bf16e-175">Пожалуйста Обратите внимание, что значение hello жестких закодированных, $key, только в демонстрационных целях.</span><span class="sxs-lookup"><span data-stu-id="bf16e-175">Please note that hello hard coded value, $key, is for demonstration purpose only.</span></span> <span data-ttu-id="bf16e-176">В своем коде вы решите toogenerate этот ключ.</span><span class="sxs-lookup"><span data-stu-id="bf16e-176">In your own code you'll want toogenerate this key.</span></span>

```csharp
// Here we are making a 128-bit key so we have 16 characters.
//     hello characters are in hello ASCII range of UTF8 so they are
//    each 1 byte. 16 x 8 = 128.
$key = "qwertyuiopasdfgh"
$b = [System.Text.Encoding]::UTF8.GetBytes($key)
$enc = [System.Convert]::ToBase64String($b)
$secretvalue = ConvertTo-SecureString $enc -AsPlainText -Force

// Substitute hello VaultName and Name in this command.
$secret = Set-AzureKeyVaultSecret -VaultName 'ContoseKeyVault' -Name 'TestSecret2' -SecretValue $secretvalue -ContentType "application/octet-stream"
```

<span data-ttu-id="bf16e-177">В консольного приложения можно использовать hello же, как перед вызвать tooretrieve этот секретный как SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="bf16e-177">In your console application, you can use hello same call as before tooretrieve this secret as a SymmetricKey.</span></span>

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
<span data-ttu-id="bf16e-178">Вот и все.</span><span class="sxs-lookup"><span data-stu-id="bf16e-178">That's it.</span></span> <span data-ttu-id="bf16e-179">Так просто!</span><span class="sxs-lookup"><span data-stu-id="bf16e-179">Enjoy!</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf16e-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bf16e-180">Next steps</span></span>
<span data-ttu-id="bf16e-181">Дополнительные сведения об использовании службы хранилища Microsoft Azure с C# см. в статье [Клиентская библиотека службы хранилища Microsoft Azure для .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf16e-181">For more information about using Microsoft Azure Storage with C#, see [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="bf16e-182">Дополнительные сведения о hello API REST BLOB-объектов см. в разделе [API REST службы BLOB-объектов](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf16e-182">For more information about hello Blob REST API, see [Blob Service REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span></span>

<span data-ttu-id="bf16e-183">Hello последние сведения о службе хранилища Microsoft Azure, перейдите toohello [блоге разработчиков хранилища Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="bf16e-183">For hello latest information on Microsoft Azure Storage, go toohello [Microsoft Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>
