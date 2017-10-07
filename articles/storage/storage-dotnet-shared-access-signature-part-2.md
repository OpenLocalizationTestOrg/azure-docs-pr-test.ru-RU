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
ms.openlocfilehash: 629f5c0aee3f41115a0d514a2010d8cc0187126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a>Подписанные URL-адреса. Часть 2: создание и использование подписанного URL-адреса в службе BLOB-объектов

[В части 1](storage-dotnet-shared-access-signature-part-1.md) этого учебника приведен обзор подписей общего доступа (SAS), а также даны советы и рекомендации по их использованию. Часть 2 показано, как toogenerate, а затем использовать общий доступ к подписи с помощью хранилища больших двоичных объектов. Hello примеры написаны на C# и используйте hello клиентская библиотека хранилища Azure для .NET. Примеры Hello в этом учебнике.

* Создание подписанного URL-адреса для контейнера.
* Создание подписанного URL-адреса для большого двоичного объекта.
* Создание подписей toomanage политики доступа в ресурсы контейнера
* Тестовые подписи hello общего доступа в клиентском приложении

## <a name="about-this-tutorial"></a>О данном учебнике
В этом руководстве мы создадим два консольных приложения, демонстрирующих создание и использование подписанных URL-адресов для контейнеров и больших двоичных объектов.

**Приложение 1**: hello приложение для управления. Создает подписанный URL-адрес для контейнера и большого двоичного объекта. Содержит ключ доступа учетной записи хранения hello в исходном коде.

**Приложение 2**: hello клиентское приложение. Обращается к контейнера и большого двоичного объекта ресурсов с помощью URL-адреса hello совместно с первого приложения hello. Использует только hello общего доступа подписи tooaccess контейнера и больших двоичных объектов ресурсов — это происходит *не* включают hello ключ доступа учетной записи хранилища.

## <a name="part-1-create-a-console-application-toogenerate-shared-access-signatures"></a>Часть 1: Создать toogenerate общего доступа приложения консоли подписи
Во-первых Обеспечьте hello клиентская библиотека хранилища Azure для установки .NET. Вы можете установить hello [пакет NuGet](http://nuget.org/packages/WindowsAzure.Storage/ "пакет NuGet") содержащих hello самые последние сборки для hello клиентской библиотеки. Это рекомендуется использовать метод, чтобы обеспечить наличие последних исправлений hello hello. Можно также загрузить клиентскую библиотеку hello как часть hello самую последнюю версию hello [Azure SDK для .NET](https://azure.microsoft.com/downloads/).

В Visual Studio создайте новое консольное приложение Windows и назовите его **GenerateSharedAccessSignatures**. Добавьте ссылки на слишком[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) и [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) с помощью одного из hello следующие подходы:

* Используйте hello [диспетчера пакетов NuGet](https://docs.nuget.org/consume/installing-nuget) в Visual Studio. Выберите **Проект** > **Управление пакетами NuGet**, выполните поиск в Интернете для каждого пакета (Microsoft.WindowsAzure.ConfigurationManager и WindowsAzure.Storage) и установите их.
* Можно также найти эти сборки в установке hello Azure SDK и добавьте ссылки на toothem:
  * Microsoft.WindowsAzure.Configuration.dll.
  * Microsoft.WindowsAzure.Storage.dll

Вверху hello hello файла Program.cs добавьте следующую hello **с помощью** директивы:

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

Измените файл app.config hello, чтобы он содержал параметр конфигурации со строкой соединения, указывающий tooyour учетной записи хранилища. Файл app.config должен выглядеть примерно toothis один:

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

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a>Создание универсального кода ресурса (URI) подписанного URL-адреса для контейнера
toobegin с добавляется метод toogenerate подписанного URL-адреса на новый контейнер. В этом случае hello подпись не связана с хранимой политикой доступа, предоставляет, он продолжает hello данные hello URI для его разрешения hello и время истечения срока действия.

Сначала добавьте код toohello **Main()** tooauthenticate метод доступа к учетной записи хранилища tooyour и создать новый контейнер:

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

Добавьте метод, который приводит к возникновению ошибки hello подписанный URL-адрес для контейнера hello и возвращает подпись hello URI.

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

Добавьте следующие строки внизу hello hello hello **Main()** метода, прежде чем hello вызвать слишком**Console.ReadLine()**, toocall **GetContainerSasUri()** и записи hello окно консоли toohello URI подписи:

```csharp
//Generate a SAS URI for hello container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

Скомпилируйте и запустите toooutput hello URI подписи коллективного доступа для нового контейнера hello. Hello URI будет иметь примерно следующий toohello:

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

После выполнения кода hello hello подписанный URL-адрес, созданный для контейнера hello допустимы для hello каждые 24 часа. подпись Hello предоставляет клиент разрешение toolist BLOB-объектов в контейнере hello и toowrite toohello контейнер больших двоичных объектов.

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a>Создание URI подписанного URL-адреса для большого двоичного объекта
Затем мы записать новый большой двоичный объект в контейнере hello аналогичные toocreate код и создать подпись общего доступа для него. Подписанный URL-адрес не связан с хранимой политикой доступа, включив в него hello время начала, срок действия и сведения о разрешениях в hello URI.

Добавьте новый метод, который создает новый большой двоичный объект и записывает некоторые tooit текста, затем создает подпись общего доступа и возвращает URI подписи hello:

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

Внизу hello hello **Main()** метод, добавить следующие строки toocall hello **GetBlobSasUri()**, прежде чем hello вызвать слишком**Console.ReadLine()**и записи совместно hello окно консоли toohello URI подписи доступа:

```csharp
//Generate a SAS URI for a blob within hello container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

Скомпилируйте и запустите toooutput hello подписанного URL-адреса URI hello новый большой двоичный объект. Hello URI будет иметь примерно следующий toohello:

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-hello-container"></a>Создание хранимой политики доступа на контейнер hello
Теперь давайте создадим хранимая политика доступа на контейнер hello, в котором будут определены ограничения hello для сигнатур общего доступа, связанные с ним.

В предыдущих примерах hello можно указать время начала hello (явно или неявно), hello срок действия и разрешения hello на hello подписанном URL-адресе URI сам. В следующих примерах hello мы задавать их hello хранимые политики доступа, отличный от hello подписанного URL-адреса. Это позволяет нам toochange эти ограничения без повторной выдачи hello общий доступ к подписи.

Это возможно toohave один или несколько ограничений hello на подписанный URL-адрес hello и остаток hello hello хранимой политике доступа. Тем не менее можно только указать hello время начала, время окончания и разрешения в одном месте или других hello. Например нельзя задать разрешения на подписанный URL-адрес hello и также указать их на hello хранимые политики доступа.

При добавлении контейнер tooa политики доступа, необходимо получить hello контейнера существующие разрешения, добавить новую политику доступа hello и установить разрешения контейнера hello.

Добавьте новый метод, который создает новую политику доступа на контейнер и возвращает имя hello hello политики:

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

Внизу hello hello **Main()** метода, прежде чем hello вызвать слишком**Console.ReadLine()**, добавьте следующие hello строк toofirst снимите все существующие политики доступа, а затем вызвать hello  **CreateSharedAccessPolicy()** метод:

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

При удалении hello политики доступа на контейнер, необходимо сначала получить hello контейнера существующие разрешения, а затем снимите hello разрешения, а затем снова установить разрешения hello.

### <a name="generate-a-shared-access-signature-uri-on-hello-container-that-uses-an-access-policy"></a>Создание подписанного URL-адреса URI в контейнере hello, который использует политику доступа
Далее мы создадим другой подписанный URL-адрес для контейнера hello, которая была создана ранее, но сейчас мы связать hello подписи с hello хранимые политики доступа, созданной в предыдущем примере hello.

Добавьте новый toogenerate метод другой подписанный URL-адрес для контейнера hello:

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

Внизу hello hello **Main()** метода, прежде чем hello вызвать слишком**Console.ReadLine()**, добавить следующие строки toocall hello hello **GetContainerSasUriWithPolicy** метод :

```csharp
//Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-hello-blob-that-uses-an-access-policy"></a>Создание URI подписи общего доступа на большой двоичный объект, использует hello политики доступа
Наконец мы добавьте аналогичные toocreate метод другой большой двоичный объект и создайте подписанный URL-адрес, связанный с хранимой политикой доступа.

Добавьте новый toocreate метод большого двоичного объекта и создайте подписанный URL-адрес:

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

Внизу hello hello **Main()** метода, прежде чем hello вызвать слишком**Console.ReadLine()**, добавить следующие строки toocall hello hello **GetBlobSasUriWithPolicy** метод:

```csharp
//Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

Hello **Main()** метод должен выглядеть следующим образом в полном объеме. Запустите его toowrite hello подписанный URL-адрес окна консоли toohello идентификаторы URI, затем скопируйте и вставьте их в текстовый файл для использования в hello во второй части этого учебника.

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

При запуске консольного приложения hello GenerateSharedAccessSignatures, вы увидите примерно toohello следующие выходные данные. Это hello общий URL-адреса, используемого во второй части учебника hello.

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-tootest-hello-shared-access-signatures"></a>Часть 2: Создание подписей консоли приложению tootest hello общий доступ
tootest hello подписи коллективного доступа созданные в предыдущих примерах hello, мы создаем второй консольное приложение, которое использует hello подписи tooperform операций на hello контейнера и большого двоичного объекта.

> [!NOTE]
> Если с завершена hello первой части учебника hello прошло более 24 часов, hello подписи, созданные больше не допустимы. В этом случае следует запустить кода hello hello первый консольного приложения toogenerate свежей подписанные URL-адреса для использования в hello во второй части учебника hello.
>

В Visual Studio создайте новое консольное приложение Windows и назовите его **ConsumeSharedAccessSignatures**. Добавьте ссылки на слишком[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) и [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), как это делалось ранее.

Вверху hello hello файла Program.cs добавьте следующую hello **с помощью** директивы:

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

В тексте hello hello **Main()** метод, добавить hello следующие строковые константы, изменения их значения toohello общего доступа подписей, созданные в части 1 руководства hello.

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-tootry-container-operations-using-a-shared-access-signature"></a>Добавьте контейнер операции tootry метод, с помощью подписанного URL-адреса
Далее мы добавить метод, который проверяет некоторые операции контейнера, с помощью подписи общего доступа для контейнера hello. подпись коллективного доступа Hello — используется tooreturn контейнер toohello ссылка проверки подлинности доступа toohello контейнера на основе сигнатуры hello сама по себе.

Добавьте следующий метод tooProgram.cs hello:

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

Обновление hello **Main()** toocall метод **UseContainerSAS()** с обоими hello подписи коллективного доступа на контейнер hello:

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

### <a name="add-a-method-tootry-blob-operations-using-a-shared-access-signature"></a>Добавьте метод операции tootry BLOB-объекта, с помощью подписанного URL-адреса
Наконец добавим метод, который проверяет некоторые операции BLOB-объекта с помощью подписанного URL-адреса для большого двоичного объекта hello. В этом случае мы используем hello конструктор **CloudBlockBlob(String)**, передавая hello подписанный URL-адрес tooreturn toohello эталонный BLOB-объект. Без проверки подлинности не требуется; он основан на подпись hello сама по себе.

Добавьте следующий метод tooProgram.cs hello:

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

Обновление hello **Main()** toocall метод **UseBlobSAS()** с обоими hello подписи коллективного доступа, созданные для hello большого двоичного объекта:

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

Запустите консольное приложение hello и просмотрите hello toosee выходные данные, какие операции разрешены какие подписи. результат Hello в окне консоли hello будет выглядеть аналогично toohello следующее:

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a>Дальнейшие действия

* [Подписи коллективного доступа, часть 1: Общие сведения о модели SAS hello](storage-dotnet-shared-access-signature-part-1.md)
* [Управление toocontainers анонимный доступ для чтения и больших двоичных объектов](storage-manage-access-to-resources.md)
* [Delegating Access with a Shared Access Signature](http://msdn.microsoft.com/library/azure/ee395415.aspx) (Делегирование доступа с помощью подписанного URL-адреса)
* [Введение в использование SAS таблиц и очередей](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
