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
# <a name="how-toouse-blob-storage-from-java"></a><span data-ttu-id="c66a2-103">Как toouse хранилища BLOB-объектов из Java</span><span class="sxs-lookup"><span data-stu-id="c66a2-103">How toouse Blob storage from Java</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="c66a2-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="c66a2-104">Overview</span></span>
<span data-ttu-id="c66a2-105">Хранилище больших двоичных объектов Azure — это служба, неструктурированные данные хранятся в облаке hello как большие двоичные объекты и объекты.</span><span class="sxs-lookup"><span data-stu-id="c66a2-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="c66a2-106">В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений.</span><span class="sxs-lookup"><span data-stu-id="c66a2-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="c66a2-107">Хранилище больших двоичных объектов также является ссылка tooas объекта хранилища.</span><span class="sxs-lookup"><span data-stu-id="c66a2-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="c66a2-108">В этой статье показано, как tooperform распространенных сценариев использования hello хранилища больших двоичных объектов Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c66a2-108">This article will show you how tooperform common scenarios using hello Microsoft Azure Blob storage.</span></span> <span data-ttu-id="c66a2-109">Hello примеры написаны на Java и использовать hello [пакет SDK хранилища Azure для Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="c66a2-109">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="c66a2-110">Hello сценарии включают **передачи**, **вывод**, **Загрузка**, и **удаление** больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="c66a2-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="c66a2-111">Дополнительные сведения о больших двоичных объектов см. в разделе hello [дальнейшие действия](#Next-Steps) раздела.</span><span class="sxs-lookup"><span data-stu-id="c66a2-111">For more information on blobs, see hello [Next Steps](#Next-Steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="c66a2-112">Пакет SDK доступен разработчикам, использующим хранилище Azure на устройствах Android.</span><span class="sxs-lookup"><span data-stu-id="c66a2-112">An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="c66a2-113">Дополнительные сведения см. в разделе hello [пакет SDK хранилища Azure для Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="c66a2-113">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>
>
>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="c66a2-114">Создание приложения Java</span><span class="sxs-lookup"><span data-stu-id="c66a2-114">Create a Java application</span></span>
<span data-ttu-id="c66a2-115">В этой статье будут использоваться компоненты хранилища, которые могут быть вызваны локально в приложении Java или в коде, работающем в веб-роли или рабочей роли в Azure.</span><span class="sxs-lookup"><span data-stu-id="c66a2-115">In this article, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="c66a2-116">toodo таким образом, вам потребуется tooinstall hello Java Development Kit (JDK) и создать учетную запись хранилища Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="c66a2-116">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure Storage account in your Azure subscription.</span></span> <span data-ttu-id="c66a2-117">Как только вы делали, вам потребуется tooverify, разработки система удовлетворяет минимальным требованиям hello и зависимости, которые указаны в hello [пакет SDK хранилища Azure для Java] [ Azure Storage SDK for Java] репозитория в GitHub.</span><span class="sxs-lookup"><span data-stu-id="c66a2-117">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="c66a2-118">Если компьютер соответствует этим требованиям, можно выполнить hello инструкции по загрузке и установке hello библиотеки хранилища Azure для Java в вашей системе из этого репозитория.</span><span class="sxs-lookup"><span data-stu-id="c66a2-118">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="c66a2-119">После завершения этих задач можно будет toocreate приложения Java, использующего hello примеры в этой статье.</span><span class="sxs-lookup"><span data-stu-id="c66a2-119">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-blob-storage"></a><span data-ttu-id="c66a2-120">Настройка вашего приложения tooaccess хранилища больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="c66a2-120">Configure your application tooaccess Blob storage</span></span>
<span data-ttu-id="c66a2-121">Добавьте hello после импорта инструкций toohello вверху hello Java файл, где toouse hello API-интерфейсов хранилища Azure tooaccess больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="c66a2-121">Add hello following import statements toohello top of hello Java file where you want toouse hello Azure Storage APIs tooaccess blobs.</span></span>

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="c66a2-122">Настройка строки подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="c66a2-122">Set up an Azure Storage connection string</span></span>
<span data-ttu-id="c66a2-123">Клиент хранилища Azure использует хранилища конечные точки toostore соединения строки и учетные данные для доступа к службам данных управления.</span><span class="sxs-lookup"><span data-stu-id="c66a2-123">An Azure Storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="c66a2-124">При работе в клиентском приложении, необходимо указать строку соединения хранения hello в hello следующая формата, используя hello имя учетной записи и hello первичный ключ доступа для учетной записи хранения hello, перечисленные в hello [портал Azure](https://portal.azure.com)для hello *AccountName* и *AccountKey* значения.</span><span class="sxs-lookup"><span data-stu-id="c66a2-124">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="c66a2-125">Hello следующем примере показано, как объявить строки подключения hello toohold статического поля.</span><span class="sxs-lookup"><span data-stu-id="c66a2-125">hello following example shows how you can declare a static field toohold hello connection string.</span></span>

```java
// Define hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="c66a2-126">Эта строка в приложения, запущенного в рамках роли в Microsoft Azure, могут храниться в файле конфигурации службы hello, *ServiceConfiguration.cscfg*и можно осуществить с помощью toohello вызова  **RoleEnvironment.getConfigurationSettings** метод.</span><span class="sxs-lookup"><span data-stu-id="c66a2-126">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="c66a2-127">Hello следующий пример возвращает строку hello подключения из **параметр** элемента с именем *StorageConnectionString* в файле конфигурации службы hello.</span><span class="sxs-lookup"><span data-stu-id="c66a2-127">hello following example gets hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file.</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="c66a2-128">Hello следующие образцы предполагается, что используется один из этих двух методов tooget hello строки подключения к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="c66a2-128">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="c66a2-129">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="c66a2-129">Create a container</span></span>
<span data-ttu-id="c66a2-130">Объект **CloudBlobClient** позволяет получить объекты ссылки для контейнеров и больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="c66a2-130">A **CloudBlobClient** object lets you get reference objects for containers and blobs.</span></span> <span data-ttu-id="c66a2-131">Hello следующий код создает **CloudBlobClient** объекта.</span><span class="sxs-lookup"><span data-stu-id="c66a2-131">hello following code creates a **CloudBlobClient** object.</span></span>

> [!NOTE]
> <span data-ttu-id="c66a2-132">Существуют дополнительные способы toocreate **CloudStorageAccount** объектов; Дополнительные сведения см. в разделе **CloudStorageAccount** в hello [ссылку на пакет SDK клиента хранилища Azure].</span><span class="sxs-lookup"><span data-stu-id="c66a2-132">There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="c66a2-133">Используйте hello **CloudBlobClient** tooget требуется toouse контейнер toohello ссылку объекта.</span><span class="sxs-lookup"><span data-stu-id="c66a2-133">Use hello **CloudBlobClient** object tooget a reference toohello container you want toouse.</span></span> <span data-ttu-id="c66a2-134">Hello контейнер можно создать, если она не существовала hello **createIfNotExists** метод, который в противном случае возвращает hello существующий контейнер.</span><span class="sxs-lookup"><span data-stu-id="c66a2-134">You can create hello container if it doesn't exist with hello **createIfNotExists** method, which will otherwise return hello existing container.</span></span> <span data-ttu-id="c66a2-135">По умолчанию hello новый контейнер является закрытым, поэтому необходимо указать ключи доступа к хранилищу (как это было сделано ранее) toodownload большие двоичные объекты из этого контейнера.</span><span class="sxs-lookup"><span data-stu-id="c66a2-135">By default, hello new container is private, so you must specify your storage access key (as you did earlier) toodownload blobs from this container.</span></span>

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

### <a name="optional-configure-a-container-for-public-access"></a><span data-ttu-id="c66a2-136">Необязательно. Настройте контейнер для открытого доступа</span><span class="sxs-lookup"><span data-stu-id="c66a2-136">Optional: Configure a container for public access</span></span>
<span data-ttu-id="c66a2-137">Разрешения контейнера, настроенных для частного доступа по умолчанию, но можно легко настроить контейнера разрешения tooallow открытым и доступным только для чтения доступ для всех пользователей на hello Интернет:</span><span class="sxs-lookup"><span data-stu-id="c66a2-137">A container's permissions are configured for private access by default, but you can easily configure a container's permissions tooallow public, read-only access for all users on hello Internet:</span></span>

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in hello permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set hello permissions on hello container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="c66a2-138">Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="c66a2-138">Upload a blob into a container</span></span>
<span data-ttu-id="c66a2-139">tooupload большой двоичный объект tooa файл получить ссылку на контейнер и использовать его tooget ссылку на большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="c66a2-139">tooupload a file tooa blob, get a container reference and use it tooget a blob reference.</span></span> <span data-ttu-id="c66a2-140">Получив ссылку на большой двоичный объект, можно передать любой поток, вызвав передачи по ссылке hello BLOB-объектов на.</span><span class="sxs-lookup"><span data-stu-id="c66a2-140">Once you have a blob reference, you can upload any stream by calling upload on hello blob reference.</span></span> <span data-ttu-id="c66a2-141">Эта операция создаст hello большого двоичного объекта, если она не существует, или перезаписать его, если это так.</span><span class="sxs-lookup"><span data-stu-id="c66a2-141">This operation will create hello blob if it doesn't exist, or overwrite it if it does.</span></span> <span data-ttu-id="c66a2-142">Здравствуйте, следующий образец кода показывает это и предполагается, что уже был создан этот контейнер hello.</span><span class="sxs-lookup"><span data-stu-id="c66a2-142">hello following code sample shows this, and assumes that hello container has already been created.</span></span>

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

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="c66a2-143">Перечисление hello больших двоичных объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="c66a2-143">List hello blobs in a container</span></span>
<span data-ttu-id="c66a2-144">toolist hello BLOB-объектов в контейнере, сначала получить ссылку контейнера, как это было сделано tooupload большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="c66a2-144">toolist hello blobs in a container, first get a container reference like you did tooupload a blob.</span></span> <span data-ttu-id="c66a2-145">Можно использовать контейнер hello **listBlobs** метод с **для** цикла.</span><span class="sxs-lookup"><span data-stu-id="c66a2-145">You can use hello container's **listBlobs** method with a **for** loop.</span></span> <span data-ttu-id="c66a2-146">Hello следующий код выводит hello Uri каждого большого двоичного объекта в контейнер toohello консоли.</span><span class="sxs-lookup"><span data-stu-id="c66a2-146">hello following code outputs hello Uri of each blob in a container toohello console.</span></span>

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

<span data-ttu-id="c66a2-147">Обратите внимание, что в именах больших двоичных объектов можно указывать пути к каталогу.</span><span class="sxs-lookup"><span data-stu-id="c66a2-147">Note that you can name blobs with path information in their names.</span></span> <span data-ttu-id="c66a2-148">Таким образом, создается такая структура виртуальных каталогов, которую можно организовывать и просматривать, как и традиционную файловую систему.</span><span class="sxs-lookup"><span data-stu-id="c66a2-148">This creates a virtual directory structure that you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="c66a2-149">Обратите внимание, что структура каталогов hello виртуального только - hello только доступные ресурсы в хранилище больших двоичных объектов, контейнеры и большие двоичные объекты.</span><span class="sxs-lookup"><span data-stu-id="c66a2-149">Note that hello directory structure is virtual only - hello only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="c66a2-150">Однако клиентская библиотека hello предлагает **CloudBlobDirectory** объекта виртуального каталога tooa toorefer и упростить процесс работы с большими двоичными объектами, которые упорядочены таким образом hello.</span><span class="sxs-lookup"><span data-stu-id="c66a2-150">However, hello client library offers a **CloudBlobDirectory** object toorefer tooa virtual directory and simplify hello process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="c66a2-151">Например, можно использовать контейнер с именем "photos", в который можно отправить BLOB-объекты с именами "rootphoto1", "2010/photo1", "2010/photo2" и "2011/photo1".</span><span class="sxs-lookup"><span data-stu-id="c66a2-151">For example, you could have a container named "photos", in which you might upload blobs named "rootphoto1", "2010/photo1", "2010/photo2", and "2011/photo1".</span></span> <span data-ttu-id="c66a2-152">В этом случает возникнут hello виртуальные каталоги «2010» и «2011 г.» в контейнере «фотографии» hello.</span><span class="sxs-lookup"><span data-stu-id="c66a2-152">This would create hello virtual directories "2010" and "2011" within hello "photos" container.</span></span> <span data-ttu-id="c66a2-153">При вызове **listBlobs** в контейнере «фотографии» hello, возвращаемая коллекция hello будет содержать **CloudBlobDirectory** и **CloudBlob** объекты, представляющие hello каталоги и большие двоичные объекты, содержащиеся на верхнем уровне hello.</span><span class="sxs-lookup"><span data-stu-id="c66a2-153">When you call **listBlobs** on hello "photos" container, hello collection returned will contain **CloudBlobDirectory** and **CloudBlob** objects representing hello directories and blobs contained at hello top level.</span></span> <span data-ttu-id="c66a2-154">В этом случае будут возвращены каталоги "2010" и "2011", а также "rootphoto1".</span><span class="sxs-lookup"><span data-stu-id="c66a2-154">In this case, directories "2010" and "2011", as well as photo "rootphoto1" would be returned.</span></span> <span data-ttu-id="c66a2-155">Можно использовать hello **instanceof** оператор toodistinguish этих объектов.</span><span class="sxs-lookup"><span data-stu-id="c66a2-155">You can use hello **instanceof** operator toodistinguish these objects.</span></span>

<span data-ttu-id="c66a2-156">При необходимости можно передать в параметры toohello **listBlobs** метод с hello **useFlatBlobListing** tootrue значение параметра.</span><span class="sxs-lookup"><span data-stu-id="c66a2-156">Optionally, you can pass in parameters toohello **listBlobs** method with hello **useFlatBlobListing** parameter set tootrue.</span></span> <span data-ttu-id="c66a2-157">Это приведет к возвращению всех больших двоичных объектов независимо от каталога.</span><span class="sxs-lookup"><span data-stu-id="c66a2-157">This will result in every blob being returned, regardless of directory.</span></span> <span data-ttu-id="c66a2-158">Дополнительные сведения см. в разделе **CloudBlobContainer.listBlobs** в hello [ссылку на пакет SDK клиента хранилища Azure].</span><span class="sxs-lookup"><span data-stu-id="c66a2-158">For more information, see **CloudBlobContainer.listBlobs** in hello [Azure Storage Client SDK Reference].</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="c66a2-159">Загрузка BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="c66a2-159">Download a blob</span></span>
<span data-ttu-id="c66a2-160">большие двоичные объекты toodownload, следуйте hello же шаги, что и для передачи большого двоичного объекта в порядке tooget ссылку на большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="c66a2-160">toodownload blobs, follow hello same steps as you did for uploading a blob in order tooget a blob reference.</span></span> <span data-ttu-id="c66a2-161">В отправке пример hello вызывается передачи на hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="c66a2-161">In hello uploading example, you called upload on hello blob object.</span></span> <span data-ttu-id="c66a2-162">В следующем примере hello, вызов загрузки tootransfer hello blob содержимое tooa поток объекта как **FileOutputStream** , можно использовать локальный файл большого двоичного объекта hello tooa toopersist.</span><span class="sxs-lookup"><span data-stu-id="c66a2-162">In hello following example, call download tootransfer hello blob contents tooa stream object such as a **FileOutputStream** that you can use toopersist hello blob tooa local file.</span></span>

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

## <a name="delete-a-blob"></a><span data-ttu-id="c66a2-163">Удаление большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="c66a2-163">Delete a blob</span></span>
<span data-ttu-id="c66a2-164">toodelete большого двоичного объекта, получение большого двоичного объекта ссылки, а также вызвать **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="c66a2-164">toodelete a blob, get a blob reference, and call **deleteIfExists**.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="c66a2-165">Удаление контейнера blob-объектов</span><span class="sxs-lookup"><span data-stu-id="c66a2-165">Delete a blob container</span></span>
<span data-ttu-id="c66a2-166">Наконец, toodelete контейнер больших двоичных объектов получение большого двоичного объекта ссылка контейнера, а вызов **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="c66a2-166">Finally, toodelete a blob container, get a blob container reference, and call **deleteIfExists**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c66a2-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c66a2-167">Next steps</span></span>
<span data-ttu-id="c66a2-168">Теперь, когда вы узнали основы hello хранилища больших двоичных объектов, выполните эти ссылки toolearn о более сложных задач хранилища.</span><span class="sxs-lookup"><span data-stu-id="c66a2-168">Now that you've learned hello basics of Blob storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="c66a2-169">[Пакет SDK службы хранилища Azure для Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="c66a2-169">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="c66a2-170">[ссылку на пакет SDK клиента хранилища Azure][ссылку на пакет SDK клиента хранилища Azure]</span><span class="sxs-lookup"><span data-stu-id="c66a2-170">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="c66a2-171">[REST API службы хранилища Azure][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="c66a2-171">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="c66a2-172">[Блог рабочей группы службы хранилища Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="c66a2-172">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="c66a2-173">Дополнительные сведения см. также: hello [центра разработчиков Java](/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="c66a2-173">For more information, see also hello [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[ссылку на пакет SDK клиента хранилища Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
