---
title: "aaaHow toouse хранилища больших двоичных объектов Azure (объект хранилища) из Java | Документы Microsoft"
description: "Храните неструктурированные данные в облаке hello с хранилищем больших двоичных объектов Azure (хранилище объектов)."
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 2e223b38-92de-4c2f-9254-346374545d32
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 6dd6efdf688161c32b9d73a65fa7f3a98f2fad74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-java"></a>Как toouse хранилища BLOB-объектов из Java
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a>Обзор
Хранилище больших двоичных объектов Azure — это служба, неструктурированные данные хранятся в облаке hello как большие двоичные объекты и объекты. В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений. Хранилище больших двоичных объектов также является ссылка tooas объекта хранилища.

В этой статье показано, как tooperform распространенных сценариев использования hello хранилища больших двоичных объектов Microsoft Azure. Hello примеры написаны на Java и использовать hello [пакет SDK хранилища Azure для Java][Azure Storage SDK for Java]. Hello сценарии включают **передачи**, **вывод**, **Загрузка**, и **удаление** больших двоичных объектов. Дополнительные сведения о больших двоичных объектов см. в разделе hello [дальнейшие действия](#Next-Steps) раздела.

> [!NOTE]
> Пакет SDK доступен разработчикам, использующим хранилище Azure на устройствах Android. Дополнительные сведения см. в разделе hello [пакет SDK хранилища Azure для Android][Azure Storage SDK for Android].
>
>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Создание приложения Java
В этой статье будут использоваться компоненты хранилища, которые могут быть вызваны локально в приложении Java или в коде, работающем в веб-роли или рабочей роли в Azure.

toodo таким образом, вам потребуется tooinstall hello Java Development Kit (JDK) и создать учетную запись хранилища Azure в подписке Azure. Как только вы делали, вам потребуется tooverify, разработки система удовлетворяет минимальным требованиям hello и зависимости, которые указаны в hello [пакет SDK хранилища Azure для Java] [ Azure Storage SDK for Java] репозитория в GitHub. Если компьютер соответствует этим требованиям, можно выполнить hello инструкции по загрузке и установке hello библиотеки хранилища Azure для Java в вашей системе из этого репозитория. После завершения этих задач можно будет toocreate приложения Java, использующего hello примеры в этой статье.

## <a name="configure-your-application-tooaccess-blob-storage"></a>Настройка вашего приложения tooaccess хранилища больших двоичных объектов
Добавьте hello после импорта инструкций toohello вверху hello Java файл, где toouse hello API-интерфейсов хранилища Azure tooaccess больших двоичных объектов.

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>Настройка строки подключения к службе хранилища Azure
Клиент хранилища Azure использует хранилища конечные точки toostore соединения строки и учетные данные для доступа к службам данных управления. При работе в клиентском приложении, необходимо указать строку соединения хранения hello в hello следующая формата, используя hello имя учетной записи и hello первичный ключ доступа для учетной записи хранения hello, перечисленные в hello [портал Azure](https://portal.azure.com)для hello *AccountName* и *AccountKey* значения. Hello следующем примере показано, как объявить строки подключения hello toohold статического поля.

```java
// Define hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

Эта строка в приложения, запущенного в рамках роли в Microsoft Azure, могут храниться в файле конфигурации службы hello, *ServiceConfiguration.cscfg*и можно осуществить с помощью toohello вызова  **RoleEnvironment.getConfigurationSettings** метод. Hello следующий пример возвращает строку hello подключения из **параметр** элемента с именем *StorageConnectionString* в файле конфигурации службы hello.

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Hello следующие образцы предполагается, что используется один из этих двух методов tooget hello строки подключения к хранилищу.

## <a name="create-a-container"></a>Создание контейнера
Объект **CloudBlobClient** позволяет получить объекты ссылки для контейнеров и больших двоичных объектов. Hello следующий код создает **CloudBlobClient** объекта.

> [!NOTE]
> Существуют дополнительные способы toocreate **CloudStorageAccount** объектов; Дополнительные сведения см. в разделе **CloudStorageAccount** в hello [ссылку на пакет SDK клиента хранилища Azure].
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Используйте hello **CloudBlobClient** tooget требуется toouse контейнер toohello ссылку объекта. Hello контейнер можно создать, если она не существовала hello **createIfNotExists** метод, который в противном случае возвращает hello существующий контейнер. По умолчанию hello новый контейнер является закрытым, поэтому необходимо указать ключи доступа к хранилищу (как это было сделано ранее) toodownload большие двоичные объекты из этого контейнера.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Get a reference tooa container.
    // hello container name must be lower case
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Create hello container if it does not exist.
    container.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

### <a name="optional-configure-a-container-for-public-access"></a>Необязательно. Настройте контейнер для открытого доступа
Разрешения контейнера, настроенных для частного доступа по умолчанию, но можно легко настроить контейнера разрешения tooallow открытым и доступным только для чтения доступ для всех пользователей на hello Интернет:

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in hello permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set hello permissions on hello container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a>Отправка BLOB-объекта в контейнер
tooupload большой двоичный объект tooa файл получить ссылку на контейнер и использовать его tooget ссылку на большой двоичный объект. Получив ссылку на большой двоичный объект, можно передать любой поток, вызвав передачи по ссылке hello BLOB-объектов на. Эта операция создаст hello большого двоичного объекта, если она не существует, или перезаписать его, если это так. Здравствуйте, следующий образец кода показывает это и предполагается, что уже был создан этот контейнер hello.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Define hello path tooa local file.
    final String filePath = "C:\\myimages\\myimage.jpg";

    // Create or overwrite hello "myimage.jpg" blob with contents from a local file.
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");
    File source = new File(filePath);
    blob.upload(new FileInputStream(source), source.length());
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="list-hello-blobs-in-a-container"></a>Перечисление hello больших двоичных объектов в контейнере
toolist hello BLOB-объектов в контейнере, сначала получить ссылку контейнера, как это было сделано tooupload большого двоичного объекта. Можно использовать контейнер hello **listBlobs** метод с **для** цикла. Hello следующий код выводит hello Uri каждого большого двоичного объекта в контейнер toohello консоли.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop over blobs within hello container and output hello URI tooeach of them.
    for (ListBlobItem blobItem : container.listBlobs()) {
        System.out.println(blobItem.getUri());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

Обратите внимание, что в именах больших двоичных объектов можно указывать пути к каталогу. Таким образом, создается такая структура виртуальных каталогов, которую можно организовывать и просматривать, как и традиционную файловую систему. Обратите внимание, что структура каталогов hello виртуального только - hello только доступные ресурсы в хранилище больших двоичных объектов, контейнеры и большие двоичные объекты. Однако клиентская библиотека hello предлагает **CloudBlobDirectory** объекта виртуального каталога tooa toorefer и упростить процесс работы с большими двоичными объектами, которые упорядочены таким образом hello.

Например, можно использовать контейнер с именем "photos", в который можно отправить BLOB-объекты с именами "rootphoto1", "2010/photo1", "2010/photo2" и "2011/photo1". В этом случает возникнут hello виртуальные каталоги «2010» и «2011 г.» в контейнере «фотографии» hello. При вызове **listBlobs** в контейнере «фотографии» hello, возвращаемая коллекция hello будет содержать **CloudBlobDirectory** и **CloudBlob** объекты, представляющие hello каталоги и большие двоичные объекты, содержащиеся на верхнем уровне hello. В этом случае будут возвращены каталоги "2010" и "2011", а также "rootphoto1". Можно использовать hello **instanceof** оператор toodistinguish этих объектов.

При необходимости можно передать в параметры toohello **listBlobs** метод с hello **useFlatBlobListing** tootrue значение параметра. Это приведет к возвращению всех больших двоичных объектов независимо от каталога. Дополнительные сведения см. в разделе **CloudBlobContainer.listBlobs** в hello [ссылку на пакет SDK клиента хранилища Azure].

## <a name="download-a-blob"></a>Загрузка BLOB-объектов
большие двоичные объекты toodownload, следуйте hello же шаги, что и для передачи большого двоичного объекта в порядке tooget ссылку на большой двоичный объект. В отправке пример hello вызывается передачи на hello большого двоичного объекта. В следующем примере hello, вызов загрузки tootransfer hello blob содержимое tooa поток объекта как **FileOutputStream** , можно использовать локальный файл большого двоичного объекта hello tooa toopersist.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop through each blob item in hello container.
    for (ListBlobItem blobItem : container.listBlobs()) {
        // If hello item is a blob, not a virtual directory.
        if (blobItem instanceof CloudBlob) {
            // Download hello item and save it tooa file with hello same name.
            CloudBlob blob = (CloudBlob) blobItem;
            blob.download(new FileOutputStream("C:\\mydownloads\\" + blob.getName()));
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob"></a>Удаление большого двоичного объекта
toodelete большого двоичного объекта, получение большого двоичного объекта ссылки, а также вызвать **deleteIfExists**.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Retrieve reference tooa blob named "myimage.jpg".
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");

    // Delete hello blob.
    blob.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob-container"></a>Удаление контейнера blob-объектов
Наконец, toodelete контейнер больших двоичных объектов получение большого двоичного объекта ссылка контейнера, а вызов **deleteIfExists**.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Delete hello blob container.
    container.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello хранилища больших двоичных объектов, выполните эти ссылки toolearn о более сложных задач хранилища.

* [Пакет SDK службы хранилища Azure для Java][Azure Storage SDK for Java]
* [ссылку на пакет SDK клиента хранилища Azure][ссылку на пакет SDK клиента хранилища Azure]
* [REST API службы хранилища Azure][Azure Storage REST API]
* [Блог рабочей группы службы хранилища Azure][Azure Storage Team Blog]

Дополнительные сведения см. также: hello [центра разработчиков Java](/develop/java/).

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[ссылку на пакет SDK клиента хранилища Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
