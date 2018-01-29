---
title: "Безопасный доступ к данным приложения в облаке с помощью службы хранилища Azure | Документы Майкрософт"
description: "Использование маркеров SAS, шифрования и HTTPS для защиты данных приложения в облаке"
services: storage
documentationcenter: 
author: georgewallace
manager: timlt
editor: 
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 09/19/2017
ms.author: gwallace
ms.custom: mvc
ms.openlocfilehash: c43165e230a00b6a4408637fd2290a21800d07b9
ms.sourcegitcommit: 3cdc82a5561abe564c318bd12986df63fc980a5a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2018
---
# <a name="secure-access-to-an-applications-data-in-the-cloud"></a>Безопасный доступ к данным приложения в облаке

Этот учебник представляет первую часть цикла. Вы узнаете, как обеспечить безопасность доступа к учетной записи хранения. 

В третьей части цикла вы узнаете, как выполнять такие задачи:

> [!div class="checklist"]
> * Использование маркеров SAS для доступа к эскизам изображений
> * Включение шифрования на стороне сервера
> * Включение транспорта только по протоколу HTTPS

[Хранилище BLOB-объектов](../common/storage-introduction.md#blob-storage) представляет собой надежную службу для хранения файлов для приложений. Этот учебник дополняет сведения в [предыдущем разделе][previous-tutorial] и описывает процедуру защиты доступа к учетной записи хранения из веб-приложения. По окончании работы изображения шифруются, и для доступа к эскизам веб-приложение использует маркеры безопасности SAS.

## <a name="prerequisites"></a>Технические условия

Чтобы пройти действия в этом учебнике, необходимо выполнить задачи в предыдущим учебнике по хранилищу: [Автоматическое изменение размера переданных изображений с помощью сетки событий][previous-tutorial]. 

## <a name="set-container-public-access"></a>Установка общего доступа к контейнеру

В этой части серии учебников для доступа к эскизам используются маркеры SAS. На этом шаге вы установите `off` в качестве значения общего доступа к контейнеру _thumbs_.

```azurecli-interactive 
blobStorageAccount=<blob_storage_account>

blobStorageAccountKey=$(az storage account keys list -g myResourceGroup \
-n $blobStorageAccount --query [0].value --output tsv) 

az storage container set-permission \ --account-name $blobStorageAccount \ --account-key $blobStorageAccountKey \ --name thumbs  \
--public-access off
``` 

## <a name="configure-sas-tokens-for-thumbnails"></a>Настройка маркеров SAS для эскизов

В первой части этой серии учебников в веб-приложении отображались изображения из общедоступного контейнера. В этой части вы будете использовать [маркеры SAS](../common/storage-dotnet-shared-access-signature-part-1.md#what-is-a-shared-access-signature) для получения изображений эскизов. Маркеры SAS позволяют предоставлять ограниченный доступ к контейнеру или BLOB-объекту на основе IP-адреса, протокола, интервала времени или имеющихся прав.

В этом примере репозиторий исходного кода использует ветвь `sasTokens` с примером обновленного кода. Удалите существующее развертывание GitHub с помощью команды [az webapp deployment source delete](/cli/azure/webapp/deployment/source#az_webapp_deployment_source_delete). Затем настройте для веб-приложения развертывание GitHub с помощью команды [az webapp deployment source config](/cli/azure/webapp/deployment/source#az_webapp_deployment_source_config).  

В следующей команде `<web-app>` — это имя веб-приложения.  

```azurecli-interactive 
az webapp deployment source delete --name <web-app> --resource-group myResourceGroup

az webapp deployment source config --name <web_app> \
--resource-group myResourceGroup --branch sasTokens --manual-integration \
--repo-url https://github.com/Azure-Samples/storage-blob-upload-from-webapp
``` 

Ветвь `sasTokens` репозитория обновляет файл `StorageHelper.cs`. Она заменяет задачу `GetThumbNailUrls` на пример кода ниже. Обновленная задача получает URL-адреса эскиза путем задания класса [SharedAccessBlobPolicy](/dotnet/api/microsoft.windowsazure.storage.blob.sharedaccessblobpolicy?view=azure-dotnet), чтобы указать время начала, время окончания и разрешения для маркера SAS. Развернутое веб-приложение получает эскизы с URL-адресом с помощью токена SAS. В следующем примере показана обновленная задача.
    
```csharp
public static async Task<List<string>> GetThumbNailUrls(AzureStorageConfig _storageConfig)
{
    List<string> thumbnailUrls = new List<string>();

    // Create storagecredentials object by reading the values from the configuration (appsettings.json)
    StorageCredentials storageCredentials = new StorageCredentials(_storageConfig.AccountName, _storageConfig.AccountKey);

    // Create cloudstorage account by passing the storagecredentials
    CloudStorageAccount storageAccount = new CloudStorageAccount(storageCredentials, true);

    // Create blob client
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get reference to the container
    CloudBlobContainer container = blobClient.GetContainerReference(_storageConfig.ThumbnailContainer);

    // Set the permission of the container to public
    await container.SetPermissionsAsync(new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });

    BlobContinuationToken continuationToken = null;

    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate the result segment returned, while the continuation token is non-null.
    //When the continuation token is null, the last page has been returned and execution can exit the loop.
    do
    {
        //This overload allows control of the page size. You can return all remaining results by passing null for the maxResults parameter,
        //or by calling a different overload.
        resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);

        foreach (var blobItem in resultSegment.Results)
        {
            CloudBlockBlob blob = blobItem as CloudBlockBlob;
            //Set the expiry time and permissions for the blob.
            //In this case, the start time is specified as a few minutes in the past, to mitigate clock skew.
            //The shared access signature will be valid immediately.
            SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();

            sasConstraints.SharedAccessStartTime = DateTimeOffset.UtcNow.AddMinutes(-5);

            sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);

            sasConstraints.Permissions = SharedAccessBlobPermissions.Read;

            //Generate the shared access signature on the blob, setting the constraints directly on the signature.
            string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

            //Return the URI string for the container, including the SAS token.
            thumbnailUrls.Add(blob.Uri + sasBlobToken);

        }

        //Get the continuation token.
        continuationToken = resultSegment.ContinuationToken;
    }

    while (continuationToken != null);

    return await Task.FromResult(thumbnailUrls);
}
```

В предыдущей задаче используются следующие классы, свойства и методы:

|Класс  |properties| Методы  |
|---------|---------|---------|
|[StorageCredentials](/dotnet/api/microsoft.windowsazure.storage.auth.storagecredentials?view=azure-dotnet)    |         |
|[CloudStorageAccount](/dotnet/api/microsoft.windowsazure.storage.cloudstorageaccount?view=azure-dotnet)     | |[CreateCloudBlobClient](/dotnet/api/microsoft.windowsazure.storage.cloudstorageaccount.createcloudblobclient?view=azure-dotnet#Microsoft_WindowsAzure_Storage_CloudStorageAccount_CreateCloudBlobClient)        |
|[CloudBlobClient](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblobclient?view=azure-dotnet)     | |[GetContainerReference](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblobclient.getcontainerreference?view=azure-dotnet#Microsoft_WindowsAzure_Storage_Blob_CloudBlobClient_GetContainerReference_System_String_)         |
|[CloudBlobContainer](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblobcontainer?view=azure-dotnet)     | |[SetPermissionsAsync](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblobcontainer.setpermissionsasync?view=azure-dotnet#Microsoft_WindowsAzure_Storage_Blob_CloudBlobContainer_SetPermissionsAsync_Microsoft_WindowsAzure_Storage_Blob_BlobContainerPermissions_) <br> [ListBlobsSegmentedAsync](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblobcontainer.listblobssegmentedasync?view=azure-dotnet#Microsoft_WindowsAzure_Storage_Blob_CloudBlobContainer_ListBlobsSegmentedAsync_System_String_System_Boolean_Microsoft_WindowsAzure_Storage_Blob_BlobListingDetails_System_Nullable_System_Int32__Microsoft_WindowsAzure_Storage_Blob_BlobContinuationToken_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_)       |
|[BlobContinuationToken](/dotnet/api/microsoft.windowsazure.storage.blob.blobcontinuationtoken?view=azure-dotnet)     |         |
|[BlobResultSegment](/dotnet/api/microsoft.windowsazure.storage.blob.blobresultsegment?view=azure-dotnet)    | [Результаты](/dotnet/api/microsoft.windowsazure.storage.blob.blobresultsegment.results?view=azure-dotnet#Microsoft_WindowsAzure_Storage_Blob_BlobResultSegment_Results)         |
|[CloudBlockBlob](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azure-dotnet)    |         | [GetSharedAccessSignature](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.getsharedaccesssignature?view=azure-dotnet#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_GetSharedAccessSignature_Microsoft_WindowsAzure_Storage_Blob_SharedAccessBlobPolicy_)
|[SharedAccessBlobPolicy](/dotnet/api/microsoft.windowsazure.storage.blob.sharedaccessblobpolicy?view=azure-dotnet)     | [SharedAccessStartTime](/dotnet/api/microsoft.windowsazure.storage.blob.sharedaccessblobpolicy.sharedaccessstarttime?view=azure-dotnet#Microsoft_WindowsAzure_Storage_Blob_SharedAccessBlobPolicy_SharedAccessStartTime)<br>[SharedAccessExpiryTime](/dotnet/api/microsoft.windowsazure.storage.blob.sharedaccessblobpolicy.sharedaccessexpirytime?view=azure-dotnet#Microsoft_WindowsAzure_Storage_Blob_SharedAccessBlobPolicy_SharedAccessExpiryTime)<br>[Разрешения](/dotnet/api/microsoft.windowsazure.storage.blob.sharedaccessblobpolicy.permissions?view=azure-dotnet#Microsoft_WindowsAzure_Storage_Blob_SharedAccessBlobPolicy_Permissions) |        |

## <a name="server-side-encryption"></a>Шифрование на стороне сервера

[Шифрование службы хранилища Azure (SSE)](../common/storage-service-encryption.md) помогает защитить данные. SSE шифрует данные при хранении, выполняя обработку шифрования, расшифровки и управление ключами. Используется 256-битное [шифрование AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), самая надежная технология блочного шифрования на сегодняшний день.

В следующем примере показано включение шифрования для BLOB-объектов. Существующие BLOB-объекты, созданные до включения шифрования, не шифруются. В заголовке `x-ms-server-encrypted` в запросе на BLOB-объект показано состояние шифрования BLOB-объекта.

```azurecli-interactive
az storage account update --encryption-services blob --name <storage-account-name> --resource-group myResourceGroup
```

Теперь, когда шифрование включено, отправьте новое изображение в веб-приложение.

Используя `curl` с параметром `-I` только для извлечения заголовков, подставьте собственные значения для `<storage-account-name>`, `<container>` и `<blob-name>`.  

```azurecli-interactive
sasToken=$(az storage blob generate-sas \
    --account-name <storage-account-name> \
    --account-key <storage-account-key> \
    --container-name <container> \
    --name <blob-name> \
    --permissions r \
    --expiry `date --date="next day" +%Y-%m-%d` \
    --output tsv)

curl https://<storage-account-name>.blob.core.windows.net/<container>/<blob-name>?$sasToken -I
```

Обратите внимание, что в ответе в заголовке `x-ms-server-encrypted` показано `true`. Этот заголовок определяет, что теперь данные зашифрованы с помощью SSE.

```
HTTP/1.1 200 OK
Content-Length: 209489
Content-Type: image/png
Last-Modified: Mon, 11 Sep 2017 19:27:42 GMT
Accept-Ranges: bytes
ETag: "0x8D4F94B2BE76D45"
Server: Windows-Azure-Blob/1.0 Microsoft-HTTPAPI/2.0
x-ms-request-id: 57047db3-001e-0050-3e34-2ba769000000
x-ms-version: 2017-04-17
x-ms-lease-status: unlocked
x-ms-lease-state: available
x-ms-blob-type: BlockBlob
x-ms-server-encrypted: true
Date: Mon, 11 Sep 2017 19:27:46 GMT
```

## <a name="enable-https-only"></a>Включение только HTTPS

Чтобы обеспечить безопасность запросов данных в учетную запись хранения и из нее, можно разрешить только запросы HTTPS. Обновите необходимый протокол для учетной записи хранения с помощью команды [az storage account update](/cli/azure/storage/account#az_storage_account_update).

```azurecli-interactive
az storage account update --resource-group myresourcegroup --name <storage-account-name> --https-only true
```

Протестируйте подключение, использующее `curl`, с помощью протокола `HTTP`.

```azurecli-interactive
curl http://<storage-account-name>.blob.core.windows.net/<container>/<blob-name> -I
```

Теперь, когда требуется безопасная передача, появляется следующее сообщение:

```
HTTP/1.1 400 The account being accessed does not support http.
```

## <a name="next-steps"></a>Дальнейшие действия

В третьей части серии вы узнали, как обеспечить безопасность доступа к учетной записи хранения путем выполнения приведенных ниже задач.

> [!div class="checklist"]
> * Использование маркеров SAS для доступа к эскизам изображений
> * Включение шифрования на стороне сервера
> * Включение транспорта только по протоколу HTTPS

Перейдите к четвертой части, чтобы узнать, как отслеживать приложение облачного хранилища и устранять его неполадки.

> [!div class="nextstepaction"]
> [Мониторинг и устранение неполадок приложения облачного хранилища](storage-monitor-troubleshoot-storage-application.md)

[previous-tutorial]: ../../event-grid/resize-images-on-storage-blob-upload-event.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json