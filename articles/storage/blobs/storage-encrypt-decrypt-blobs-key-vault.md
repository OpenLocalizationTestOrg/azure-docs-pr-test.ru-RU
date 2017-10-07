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
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a>Шифрование и расшифровка BLOB-объектов в хранилище Microsoft Azure с помощью хранилища ключей Azure
## <a name="introduction"></a>Введение
В этом учебнике описано, как использовать toomake шифрования хранилища на стороне клиента с хранилищем ключей Azure. Оно описано, как tooencrypt и расшифровки большого двоичного объекта в консольное приложение с использованием этих технологий.

**Предполагаемое время toocomplete:** 20 минут

Общие сведения о хранилище ключей Azure см. в статье [Что такое хранилище ключей Azure?](../../key-vault/key-vault-whatis.md)

Общие сведения о шифровании на стороне клиента для службы хранилища Azure см. в статье [Шифрование на стороне клиента для службы хранилища Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

## <a name="prerequisites"></a>Предварительные требования
toocomplete этого учебника необходимо иметь следующие hello:

* Учетная запись хранения Azure
* Visual Studio 2013 или более поздней версии
* Azure PowerShell

## <a name="overview-of-client-side-encryption"></a>Обзор шифрования на стороне клиента
Общие сведения о шифровании на стороне клиента для службы хранилища Azure см. в статье [Шифрование на стороне клиента для службы хранилища Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

Вот краткое описание того, как работает шифрование на стороне клиента.

1. пакет SDK для клиента службы хранилища Azure Hello создает ключ шифрования содержимого (CEK), который является симметричным ключом, используйте один раз.
2. Данные пользователей шифруются с помощью этого ключа CEK.
3. Hello CEK заключается в оболочку (зашифрованный) с помощью ключа hello ключа шифрования (ключ обмена Ключами). Hello KEK идентифицируется идентификатора ключа и может быть пары асимметричных ключей или симметричного ключа; его можно управлять локально и хранится в хранилище ключей Azure. сам клиент хранилища Hello никогда не имеет доступа toohello ключа обмена Ключами. Он просто вызывает hello упаковка ключа алгоритма, предоставляемые хранилища ключей. Клиенты могут выбрать toouse настраиваемых поставщиков для ключа, перенос и развертывание по желанию.
4. Hello зашифрованные данные будет отправлен службе toohello хранилища Azure.

## <a name="set-up-your-azure-key-vault"></a>Настройка хранилища ключей Azure
В порядке tooproceed к этому учебнику, необходим hello toodo следующие шаги, которые описаны в учебнике hello [приступить к работе с хранилищем ключей Azure](../../key-vault/key-vault-get-started.md):

* Создать хранилище ключей.
* Добавление ключа или секретного toohello хранилища ключей.
* Зарегистрировать приложение в Azure Active Directory.
* Авторизуйте hello приложения toouse hello ключа или секрета.

Сделать заметку hello ClientID и ClientSecret, сформированные при регистрации приложения в Azure Active Directory.

Создайте оба ключа в хранилище ключей hello. Мы предполагаем оставшейся hello hello учебника вы использовали hello следующие имена: ContosoKeyVault и TestRSAKey1.

## <a name="create-a-console-application-with-packages-and-appsettings"></a>Создание консольного приложения с пакетами и AppSettings
Создайте новое консольное приложение в Visual Studio.

Добавление пакетов nuget, необходимые в hello консоль диспетчера пакетов.

```
Install-Package WindowsAzure.Storage

// This is hello latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

Добавьте AppSettings toohello App.Config.

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

Добавьте следующее hello `using` инструкций и убедитесь, что tooadd tooSystem.Configuration toohello ссылки проекта.

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

## <a name="add-a-method-tooget-a-token-tooyour-console-application"></a>Добавьте метод tooget маркера tooyour консольного приложения
Hello следующий метод используется классами хранилище ключей, tooauthenticate для хранилища ключей tooyour доступа.

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

## <a name="access-storage-and-key-vault-in-your-program"></a>Доступ к хранилищу данных и хранилищу ключей в программе.
В hello функции Main добавьте следующий код hello.

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
> Объектные модели хранилища ключей
> 
> Важно учитывать toobe моделирует toounderstand, фактически два объекта хранилища ключей: один основан на hello API REST (пространство имен KeyVault) и hello других — это расширение для шифрования на стороне клиента.
> 
> Hello ключ хранилища клиента взаимодействует с API-интерфейса REST hello и понимает JSON Web ключи и секретные коды для hello два вида операций, которые находятся в хранилище ключей.
> 
> Hello ключ хранилища расширения — это классы, которые кажутся специально созданный для шифрования на стороне клиента в хранилище Azure. Они содержат интерфейс для ключей (IKey) и классы, основанные на концепцию hello сопоставителя ключ. Существует два способа реализации необходимые tooknow IKey: RSAKey и SymmetricKey. Теперь выполняются toocoincide с hello вещей, которые находятся в хранилище ключей, но сейчас они независимых классы (то есть не реализуют IKey hello ключ и получить ключ хранилища клиента hello секрет).
> 
> 

## <a name="encrypt-blob-and-upload"></a>Шифрование и передача BLOB-объекта
Добавьте следующую hello кода tooencrypt большой двоичный объект и передать его tooyour учетной записи хранилища Azure. Hello **ResolveKeyAsync** IKey возвращает метод, который используется.

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

Ниже приведен снимок экрана из hello [классический портал Azure](https://manage.windowsazure.com) для больших двоичных объектов, которые были зашифрованы при помощи ключа, хранящегося в хранилище ключей шифрования на стороне клиента. Hello **KeyId** свойство — hello URI для hello ключа в хранилище ключей, функционирующий как hello ключа обмена Ключами. Hello **EncryptedKey** свойство содержит зашифрованную версию hello hello CEK.

![Снимок экрана, показывающий метаданные большого двоичного объекта, содержащие метаданные шифрования](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> Если взглянуть на конструктор BlobEncryptionPolicy hello, вы увидите, он может принять ключ и/или сопоставителя. Необходимо помнить, что сейчас сопоставитель нельзя использовать для шифрования, так как он не поддерживает ключ по умолчанию.
> 
> 

## <a name="decrypt-blob-and-download"></a>Расшифруйте BLOB-объект и загрузите его
Расшифровка на самом деле при с помощью hello Сопоставитель классы смысла. Идентификатор Hello hello ключа, используемого для шифрования связан с hello большого двоичного объекта в его метаданных, нет причин для вас tooretrieve hello ключа и запоминать hello связь между ключом и больших двоичных объектов. Достаточно toomake том, что разделу hello остается в хранилище ключей.   

Hello закрытый ключ остается ключ RSA в хранилище ключей, поэтому для toooccur расшифровки hello зашифрованный ключ из метаданных hello BLOB-объект, содержащий приветствия CEK отправляется tooKey хранилище для расшифровки.

Добавьте следующие toodecrypt hello BLOB-объекта, только что переданный hello.

```csharp
// In this case, we will not pass a key and only pass hello resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> Существует несколько других видов управления ключами toomake арбитры, проще, включая: AggregateKeyResolver и CachingKeyResolver.
> 
> 

## <a name="use-key-vault-secrets"></a>Использование секретов хранилища ключей
toouse Hello способ секретный код, с помощью шифрования на стороне клиента осуществляется через hello SymmetricKey класса, поскольку секрет — по существу это симметричный ключ. Но, как указано выше, секрет в хранилище ключей не сопоставляет ровно tooa SymmetricKey. Существует несколько вещей toounderstand:

* ключ Hello в SymmetricKey имеет toobe фиксированной длины: 128, 192, 256, 384 и 512 бит.
* ключ Hello в SymmetricKey должно быть в кодировке Base64.
* Секрета хранилища ключей, который будет использоваться в качестве SymmetricKey должен toohave тип содержимого «application/octet-stream» в хранилище ключей.

Ниже приведен пример использования PowerShell для создания в хранилище ключей секрета, который можно использовать как SymmetricKey.
Пожалуйста Обратите внимание, что значение hello жестких закодированных, $key, только в демонстрационных целях. В своем коде вы решите toogenerate этот ключ.

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

В консольного приложения можно использовать hello же, как перед вызвать tooretrieve этот секретный как SymmetricKey.

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
Вот и все. Так просто!

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об использовании службы хранилища Microsoft Azure с C# см. в статье [Клиентская библиотека службы хранилища Microsoft Azure для .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Дополнительные сведения о hello API REST BLOB-объектов см. в разделе [API REST службы BLOB-объектов](https://msdn.microsoft.com/library/azure/dd135733.aspx).

Hello последние сведения о службе хранилища Microsoft Azure, перейдите toohello [блоге разработчиков хранилища Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/).
