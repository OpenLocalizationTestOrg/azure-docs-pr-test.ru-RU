---
title: "aaaDevelop для хранения файлов Azure с Java | Документы Microsoft"
description: "Узнайте, как данные файлов toodevelop Java приложений и служб, использующих toostore хранилище файлов Azure."
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 3bfbfa7f-d378-4fb4-8df3-e0b6fcea5b27
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 05/27/2017
ms.author: robinsh
ms.openlocfilehash: b50703815daf2c829e7e9a9a4196c31a2b8727e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a><span data-ttu-id="aacb1-103">Разработка для хранилища файлов Azure на языке Java</span><span class="sxs-lookup"><span data-stu-id="aacb1-103">Develop for Azure File storage with Java</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="aacb1-104">О данном учебнике</span><span class="sxs-lookup"><span data-stu-id="aacb1-104">About this tutorial</span></span>
<span data-ttu-id="aacb1-105">Этот учебник продемонстрируют hello основные принципы использования Java toodevelop приложений или служб, которые используют данные файла toostore хранилище файлов Azure.</span><span class="sxs-lookup"><span data-stu-id="aacb1-105">This tutorial will demonstrate hello basics of using Java toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="aacb1-106">В этом учебнике мы создайте простое консольное приложение и Показать как tooperform базовые действия с хранилищем, Java и файлов Azure:</span><span class="sxs-lookup"><span data-stu-id="aacb1-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Java and Azure File storage:</span></span>

* <span data-ttu-id="aacb1-107">Создание и удаление общих папок Azure.</span><span class="sxs-lookup"><span data-stu-id="aacb1-107">Create and delete Azure File shares</span></span>
* <span data-ttu-id="aacb1-108">Создание и удаление каталогов.</span><span class="sxs-lookup"><span data-stu-id="aacb1-108">Create and delete directories</span></span>
* <span data-ttu-id="aacb1-109">Перечисление файлов и каталогов в файловом ресурсе Azure.</span><span class="sxs-lookup"><span data-stu-id="aacb1-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="aacb1-110">Передача, загрузка и удаление файлов.</span><span class="sxs-lookup"><span data-stu-id="aacb1-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="aacb1-111">Поскольку хранилище файлов Azure может осуществляться по протоколу SMB, вполне возможно toowrite простых приложений, получающих доступ к папке файлов Azure hello, с помощью стандартных классов ввода-вывода Java hello.</span><span class="sxs-lookup"><span data-stu-id="aacb1-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Java I/O classes.</span></span> <span data-ttu-id="aacb1-112">В этой статье описывается, как toowrite приложения, использующие hello SDK Java хранилища Azure, которая использует hello [хранилища Azure File API-интерфейса REST](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure хранилища файлов.</span><span class="sxs-lookup"><span data-stu-id="aacb1-112">This article will describe how toowrite applications that use hello Azure Storage Java SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="aacb1-113">Создание приложения Java</span><span class="sxs-lookup"><span data-stu-id="aacb1-113">Create a Java application</span></span>
<span data-ttu-id="aacb1-114">образцы toobuild hello, необходимо будет hello Java Development Kit (JDK) и hello [пакет SDK хранилища Azure для Java] [].</span><span class="sxs-lookup"><span data-stu-id="aacb1-114">toobuild hello samples, you will need hello Java Development Kit (JDK) and hello [Azure Storage SDK for Java][].</span></span> <span data-ttu-id="aacb1-115">Вам также необходимо создать учетную запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="aacb1-115">You should also have created an Azure storage account.</span></span>

## <a name="setup-your-application-toouse-azure-file-storage"></a><span data-ttu-id="aacb1-116">Настройка вашего приложения toouse хранилища Azure File</span><span class="sxs-lookup"><span data-stu-id="aacb1-116">Setup your application toouse Azure File storage</span></span>
<span data-ttu-id="aacb1-117">hello toouse хранилища Azure API-интерфейсы, добавить hello, следующая инструкция toohello вверху hello файл Java, где планируется службы хранения hello tooaccess из.</span><span class="sxs-lookup"><span data-stu-id="aacb1-117">toouse hello Azure storage APIs, add hello following statement toohello top of hello Java file where you intend tooaccess hello storage service from.</span></span>

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="aacb1-118">Настройка строки подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="aacb1-118">Setup an Azure storage connection string</span></span>
<span data-ttu-id="aacb1-119">toouse хранилища Azure File, необходима учетная запись хранилища Azure tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="aacb1-119">toouse Azure File storage, you need tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="aacb1-120">Hello первым шагом будет tooconfigure строку подключения, которая будет использоваться учетная запись хранения tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="aacb1-120">hello first step would be tooconfigure a connection string which we'll use tooconnect tooyour storage account.</span></span> <span data-ttu-id="aacb1-121">Определим статических переменных toodo.</span><span class="sxs-lookup"><span data-stu-id="aacb1-121">Let's define a static variable toodo that.</span></span>

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> <span data-ttu-id="aacb1-122">Замените your_storage_account_name и your_storage_account_key hello фактические значения для вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="aacb1-122">Replace your_storage_account_name and your_storage_account_key with hello actual values for your storage account.</span></span>
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a><span data-ttu-id="aacb1-123">Учетной записи хранилища Azure tooan подключения</span><span class="sxs-lookup"><span data-stu-id="aacb1-123">Connecting tooan Azure storage account</span></span>
<span data-ttu-id="aacb1-124">Учетная запись хранения tooyour tooconnect необходимо toouse hello **CloudStorageAccount** объекта, передавая tooits строка подключения **синтаксический анализ** метод.</span><span class="sxs-lookup"><span data-stu-id="aacb1-124">tooconnect tooyour storage account, you need toouse hello **CloudStorageAccount** object, passing a connection string tooits **parse** method.</span></span>

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

<span data-ttu-id="aacb1-125">**CloudStorageAccount.parse** выдает InvalidKeyException, поэтому вам понадобится tooput его внутри try/catch блока.</span><span class="sxs-lookup"><span data-stu-id="aacb1-125">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need tooput it inside a try/catch block.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="aacb1-126">Создание файлового ресурса Azure</span><span class="sxs-lookup"><span data-stu-id="aacb1-126">Create an Azure File share</span></span>
<span data-ttu-id="aacb1-127">Все файлы и каталоги в хранилище файлов Azure размещаются в контейнере, который называется общей папкой (**Share**).</span><span class="sxs-lookup"><span data-stu-id="aacb1-127">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="aacb1-128">Учетная запись хранения может иметь столько общих папок, насколько позволяет емкость вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="aacb1-128">Your storage account can have as much shares as your account capacity allows.</span></span> <span data-ttu-id="aacb1-129">tooobtain доступа tooa общей папки и ее содержимое, необходимо toouse клиент хранилища файлов Azure.</span><span class="sxs-lookup"><span data-stu-id="aacb1-129">tooobtain access tooa share and its contents, you need toouse a Azure File storage client.</span></span>

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

<span data-ttu-id="aacb1-130">С помощью клиента хранилища Azure файл hello, это позволяет получить общую папку tooa ссылки.</span><span class="sxs-lookup"><span data-stu-id="aacb1-130">Using hello Azure File storage client, you can then obtain a reference tooa share.</span></span>

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

<span data-ttu-id="aacb1-131">tooactually создать общий ресурс hello, используйте hello **createIfNotExists** метод объекта CloudFileShare hello.</span><span class="sxs-lookup"><span data-stu-id="aacb1-131">tooactually create hello share, use hello **createIfNotExists** method of hello CloudFileShare object.</span></span>

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

<span data-ttu-id="aacb1-132">На этом этапе **совместное использование** содержит общую папку tooa ссылку с именем **sampleshare**.</span><span class="sxs-lookup"><span data-stu-id="aacb1-132">At this point, **share** holds a reference tooa share named **sampleshare**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="aacb1-133">Удаление общей папки Azure</span><span class="sxs-lookup"><span data-stu-id="aacb1-133">Delete an Azure File share</span></span>
<span data-ttu-id="aacb1-134">Удаление общей папки выполняется путем вызова hello **deleteIfExists** метод на объекте CloudFileShare.</span><span class="sxs-lookup"><span data-stu-id="aacb1-134">Deleting a share is done by calling hello **deleteIfExists** method on a CloudFileShare object.</span></span> <span data-ttu-id="aacb1-135">Ниже приведен пример кода, который выполняет это действие.</span><span class="sxs-lookup"><span data-stu-id="aacb1-135">Here's sample code that does that.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference toohello file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a><span data-ttu-id="aacb1-136">Создайте каталог</span><span class="sxs-lookup"><span data-stu-id="aacb1-136">Create a directory</span></span>
<span data-ttu-id="aacb1-137">Кроме того, можно организовать хранилища путем помещения файлов в подкаталоги вместо их все в корневом каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="aacb1-137">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="aacb1-138">Хранилище файлов Azure позволяет toocreate как разрешить много каталоги, как будет вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="aacb1-138">Azure File storage allows you toocreate as much directories as your account will allow.</span></span> <span data-ttu-id="aacb1-139">Приведенный ниже код Hello будет создавать вложенный каталог с именем **sampledir** в корневом каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="aacb1-139">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a><span data-ttu-id="aacb1-140">Удаление каталога</span><span class="sxs-lookup"><span data-stu-id="aacb1-140">Delete a directory</span></span>
<span data-ttu-id="aacb1-141">Удаление каталога является достаточно простой задачей, однако следует отметить, что нельзя удалить каталог, по-прежнему содержащий файлы или другие каталоги.</span><span class="sxs-lookup"><span data-stu-id="aacb1-141">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory you want toodelete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete hello directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="aacb1-142">Перечисление файлов и каталогов в файловом ресурсе Azure</span><span class="sxs-lookup"><span data-stu-id="aacb1-142">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="aacb1-143">Получить список файлов и каталогов в общей папке довольно просто, вызвав метод **listFilesAndDirectories** по ссылке CloudFileDirectory.</span><span class="sxs-lookup"><span data-stu-id="aacb1-143">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span></span> <span data-ttu-id="aacb1-144">метод Hello возвращает список объектов ListFileItem, которые можно выполнять итерацию по.</span><span class="sxs-lookup"><span data-stu-id="aacb1-144">hello method returns a list of ListFileItem objects which you can iterate on.</span></span> <span data-ttu-id="aacb1-145">В качестве примера hello следующий код будет список файлов и каталогов в корневой каталог hello.</span><span class="sxs-lookup"><span data-stu-id="aacb1-145">As an example, hello following code will list files and directories inside hello root directory.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a><span data-ttu-id="aacb1-146">Отправить файл.</span><span class="sxs-lookup"><span data-stu-id="aacb1-146">Upload a file</span></span>
<span data-ttu-id="aacb1-147">Общая папка содержит в hello очень бы файл Azure, корневой каталог, где находятся файлы, можно.</span><span class="sxs-lookup"><span data-stu-id="aacb1-147">An Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="aacb1-148">В этом разделе вы узнаете, как tooupload файла из локального хранилища на hello корневой каталог общего ресурса.</span><span class="sxs-lookup"><span data-stu-id="aacb1-148">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="aacb1-149">Первым шагом Hello в передаче файла является tooobtain каталог toohello ссылок, где он находится.</span><span class="sxs-lookup"><span data-stu-id="aacb1-149">hello first step in uploading a file is tooobtain a reference toohello directory where it should reside.</span></span> <span data-ttu-id="aacb1-150">Это делается путем вызова hello **getRootDirectoryReference** метод hello объекта общей папки.</span><span class="sxs-lookup"><span data-stu-id="aacb1-150">You do this by calling hello **getRootDirectoryReference** method of hello share object.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

<span data-ttu-id="aacb1-151">Теперь, когда имеется ссылка toohello корневой каталог общего ресурса hello, можно отправить файл на него с помощью hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="aacb1-151">Now that you have a reference toohello root directory of hello share, you can upload a file onto it using hello following code.</span></span>

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a><span data-ttu-id="aacb1-152">Скачивание файла</span><span class="sxs-lookup"><span data-stu-id="aacb1-152">Download a file</span></span>
<span data-ttu-id="aacb1-153">Одной из более частая операции, которые будут выполняться с хранилища Azure File hello является toodownload файлов.</span><span class="sxs-lookup"><span data-stu-id="aacb1-153">One of hello more frequent operations you will perform against Azure File storage is toodownload files.</span></span> <span data-ttu-id="aacb1-154">В следующем примере hello hello код загружает SampleFile.txt и отображает его содержимое.</span><span class="sxs-lookup"><span data-stu-id="aacb1-154">In hello following example, hello code downloads SampleFile.txt and displays its contents.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello directory that contains hello file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference toohello file you want toodownload
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write hello contents of hello file toohello console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a><span data-ttu-id="aacb1-155">Удаление файла</span><span class="sxs-lookup"><span data-stu-id="aacb1-155">Delete a file</span></span>
<span data-ttu-id="aacb1-156">Следующая распространенная операция в хранилище файлов Azure — это удаление файлов.</span><span class="sxs-lookup"><span data-stu-id="aacb1-156">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="aacb1-157">Hello следующий код удаляет файл с именем SampleFile.txt, хранящийся в каталоге с именем **sampledir**.</span><span class="sxs-lookup"><span data-stu-id="aacb1-157">hello following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span></span>

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory where hello file toobe deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a><span data-ttu-id="aacb1-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aacb1-158">Next steps</span></span>
<span data-ttu-id="aacb1-159">Если вы хотите toolearn Дополнительные сведения о других хранилища Azure API-интерфейсы, приведены по следующим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="aacb1-159">If you would like toolearn more about other Azure storage APIs, follow these links.</span></span>

* [<span data-ttu-id="aacb1-160">Центр разработчика Java</span><span class="sxs-lookup"><span data-stu-id="aacb1-160">Java Developer Center</span></span>](http://azure.microsoft.com/develop/java/)
* [<span data-ttu-id="aacb1-161">Пакет SDK для службы хранилища Azure для Java</span><span class="sxs-lookup"><span data-stu-id="aacb1-161">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="aacb1-162">Microsoft Azure Storage SDK for Android</span><span class="sxs-lookup"><span data-stu-id="aacb1-162">Azure Storage SDK for Android</span></span>](https://github.com/azure/azure-storage-android)
* [<span data-ttu-id="aacb1-163">справочнике по пакету SDK для клиента службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="aacb1-163">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="aacb1-164">API-интерфейс REST служб хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="aacb1-164">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="aacb1-165">Блог рабочей группы службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="aacb1-165">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="aacb1-166">Перенесите данные с помощью служебной программы командной строки AzCopy hello</span><span class="sxs-lookup"><span data-stu-id="aacb1-166">Transfer data with hello AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)
