---
title: "Как использовать хранилище BLOB-объектов Azure (хранилище объектов) из Java | Документация Майкрософт"
description: "Хранение неструктурированных данных в облаке в хранилище BLOB-объектов Azure."
services: storage
documentationcenter: java
author: tamram
manager: timlt
editor: tysonn
ms.assetid: 2e223b38-92de-4c2f-9254-346374545d32
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 12/08/2016
ms.author: tamram
ms.openlocfilehash: 91ef09916dbb587305572ea640fb4408ea9aebb6
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-use-blob-storage-from-java"></a>Использование хранилища BLOB-объектов из Java
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a>Обзор
Хранилище BLOB-объектов Azure — это служба, которая хранит неструктурированные данные в облаке в качестве объектов или больших двоичных объектов. В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений. Хранилище BLOB-объектов иногда также называют хранилищем объектов.

В этой статье показано, как реализовать типичные сценарии с использованием хранилища больших двоичных объектов Microsoft Azure. Примеры написаны на Java и используют [пакет SDK службы хранилища Azure для Java][Azure Storage SDK for Java]. Здесь описаны такие сценарии, как **отправка**, **перечисление**, **скачивание** и **удаление** BLOB-объектов. Дополнительные сведения о больших двоичных объектах см. в разделе [Дальнейшие действия](#Next-Steps).

> [!NOTE]
> Пакет SDK доступен разработчикам, использующим хранилище Azure на устройствах Android. Дополнительные сведения см. в разделе [Microsoft Azure Storage SDK for Android][Azure Storage SDK for Android] (Пакет SDK хранилища Azure для Android).
>
>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Создание приложения Java
В этой статье будут использоваться компоненты хранилища, которые могут быть вызваны локально в приложении Java или в коде, работающем в веб-роли или рабочей роли в Azure.

Для этого необходимо установить пакет SDK для Java (JDK) и создать учетную запись хранения Azure в подписке Azure. После того, как это будет сделано, необходимо убедиться, что ваша система разработки отвечает минимальным требованиям и зависимостям, указанным в репозитории [пакета SDK службы хранилища Azure для Java][Azure Storage SDK for Java] на сайте GitHub. Если ваша система отвечает указанным требованиям можно приступить к выполнению инструкций по загрузке библиотек хранилища Azure для Java из репозитория и их установке на своей системе. После завершение этих задач вы сможете приступить к созданию приложения Java с использованием примеров из данной статьи.

## <a name="configure-your-application-to-access-blob-storage"></a>Настройка приложения для доступа к хранилищу больших двоичных объектов
Если нужно использовать API службы хранилища Azure для доступа к большим двоичным объектам, добавьте следующие операторы импорта в верхнюю часть файла Java:

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>Настройка строки подключения к службе хранилища Azure
Клиент службы хранилища Azure использует строку подключения с целью хранения конечных точек и учетных данных для доступа к службам управления данными. При работе в клиентском приложении необходимо указать для хранилища строку подключения в следующем формате, используя имя своей учетной записи хранения и первичный ключ доступа для учетной записи хранения, указанные на [портале Azure](https://portal.azure.com) значениями *AccountName* и *AccountKey*. В следующем примере показано, как объявить статическое поле для размещения строки подключения.

```java
// Define the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

Если приложение выполняется в роли на платформе Microsoft Azure, эта строка может храниться в файле конфигурации службы *ServiceConfiguration.cscfg*, для доступа к которой можно использовать вызов метода **RoleEnvironment.getConfigurationSettings** . Ниже приведен пример получения строки подключения из элемента **Setting** с именем *StorageConnectionString* в файле конфигурации службы.

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

В приведенных ниже примерах предполагается, что вы использовали одно из этих двух определений для получения строки подключения к хранилищу.

## <a name="create-a-container"></a>Создание контейнера
Объект **CloudBlobClient** позволяет получить объекты ссылки для контейнеров и больших двоичных объектов. Следующий код создает объект **CloudBlobClient** .

> [!NOTE]
> Существуют также другие способы создания объектов **CloudStorageAccount**. Дополнительную информацию см. в разделе **CloudStorageAccount** [справочнике по пакету SDK для клиента службы хранилища Azure].
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

С помощью объекта **CloudBlobClient** получите ссылку контейнер, который собираетесь использовать. Если контейнер не существует, его можно создать с помощью метода **createIfNotExist** , который в противном случае возвратит существующий контейнер. По умолчанию новый контейнер является закрытым, поэтому необходимо указать ключ доступа к хранилищу (как делалось раньше), чтобы скачать большие двоичные объекты из этого контейнера.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Get a reference to a container.
    // The container name must be lower case
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Create the container if it does not exist.
    container.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

### <a name="optional-configure-a-container-for-public-access"></a>Необязательно. Настройте контейнер для открытого доступа
Разрешения контейнера по умолчанию настроены для закрытого доступа. Однако, можно легко настроить разрешения контейнера на открытый доступ с правами только на чтение для всех пользователей в Интернете.

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in the permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set the permissions on the container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a>Отправка BLOB-объекта в контейнер
Для отправки файла в BLOB-объект получите ссылку на контейнер и используйте ее для получения ссылки на BLOB-объект. Получив ссылку на BLOB-объект, можно отправить в него любой поток данных, вызывая передачу по ссылке для BLOB-объекта. Эта операция создает BLOB-объект, если он еще не существует, или заменяет его, если он существует. Далее приведен соответствующий пример кода, в котором предполагается, что контейнер уже создан.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Define the path to a local file.
    final String filePath = "C:\\myimages\\myimage.jpg";

    // Create or overwrite the "myimage.jpg" blob with contents from a local file.
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");
    File source = new File(filePath);
    blob.upload(new FileInputStream(source), source.length());
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="list-the-blobs-in-a-container"></a>Перечисление BLOB-объектов в контейнере
Для перечисления BLOB-объектов в контейнере сначала необходимо получить ссылку на контейнер, как при отправке BLOB-объекта. Можно использовать метод **listBlobs** контейнера с циклом **for**. Следующий код выводит на консоль URI каждого BLOB-объекта в контейнере.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop over blobs within the container and output the URI to each of them.
    for (ListBlobItem blobItem : container.listBlobs()) {
        System.out.println(blobItem.getUri());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

Обратите внимание, что в именах больших двоичных объектов можно указывать пути к каталогу. Таким образом, создается такая структура виртуальных каталогов, которую можно организовывать и просматривать, как и традиционную файловую систему. Обратите внимание, что используется только структура виртуальных каталогов, так как единственные ресурсы, доступные в хранилище больших двоичных объектов, — контейнеры и большие двоичные объекты. Тем не менее клиентская библиотека содержит объект **CloudBlobDirectory** , который позволяет обращаться к виртуальному каталогу, что упрощает работу с большими двоичными объектами, так упорядоченными.

Например, можно использовать контейнер с именем "photos", в который можно отправить BLOB-объекты с именами "rootphoto1", "2010/photo1", "2010/photo2" и "2011/photo1". При этом в контейнере "photos" будут созданы виртуальные каталоги "2010" и "2011". При вызове метода **listBlobs** в контейнере "photos" (как в примере выше) возвращаемая коллекция будет содержать объекты **CloudBlobDirectory** и **CloudBlob**, представляющие собой каталоги и BLOB-объекты верхнего уровня. В этом случае будут возвращены каталоги "2010" и "2011", а также "rootphoto1". Чтобы различать эти объекты, можно использовать оператор **instanceof** .

При необходимости можно передать параметры в метод **listBlobs**, задав параметру **useFlatBlobListing** значение true. Это приведет к возвращению всех больших двоичных объектов независимо от каталога. Дополнительные сведения см. в разделе **CloudBlobContainer.listBlobs** [справочнике по пакету SDK для клиента службы хранилища Azure].

## <a name="download-a-blob"></a>Загрузка BLOB-объектов
Для загрузки BLOB-объектов выполните те же действия, что и для отправки BLOB-объекта, чтобы получить ссылку на BLOB-объект. В приведенном примере отправки вызывалась передача BLOB-объекта. В следующем примере вызовите загрузку для передачи содержимого BLOB-объекта в потоковый объект, например в **FileOutputStream** , который можно использовать для сохранения BLOB-объекта в локальном файле.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop through each blob item in the container.
    for (ListBlobItem blobItem : container.listBlobs()) {
        // If the item is a blob, not a virtual directory.
        if (blobItem instanceof CloudBlob) {
            // Download the item and save it to a file with the same name.
            CloudBlob blob = (CloudBlob) blobItem;
            blob.download(new FileOutputStream("C:\\mydownloads\\" + blob.getName()));
        }
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob"></a>Удаление большого двоичного объекта
Чтобы удалить BLOB-объект, получите ссылку на BLOB-объект и вызовите метод **deleteifExits**.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Retrieve reference to a blob named "myimage.jpg".
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");

    // Delete the blob.
    blob.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob-container"></a>Удаление контейнера blob-объектов
Для удаления контейнера больших двоичных объектов нужно получить ссылку на такой контейнер, а затем вызвать метод **deleteIfExists**.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Delete the blob container.
    container.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a>Дальнейшие действия
Вы изучили основную информацию о хранилище больших двоичных объектов. Дополнительную информацию о более сложных задачах по использованию хранилища можно найти по следующим ссылкам.

* [Пакет SDK службы хранилища Azure для Java][Azure Storage SDK for Java]
* [справочнике по пакету SDK для клиента службы хранилища Azure][справочнике по пакету SDK для клиента службы хранилища Azure]
* [REST API службы хранилища Azure][Azure Storage REST API]
* [Блог рабочей группы службы хранилища Azure][Azure Storage Team Blog]

Дополнительные сведения см. также в разделе [Azure for Java developers](/java/azure) (Azure для разработчиков Java).

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[справочнике по пакету SDK для клиента службы хранилища Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
