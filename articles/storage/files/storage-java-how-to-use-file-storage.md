---
title: "Разработка для хранилища файлов Azure на языке Java | Документация Майкрософт"
description: "Узнайте, как разрабатывать приложения и службы Java, использующие хранилище файлов Azure для хранения файлов данных."
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
ms.openlocfilehash: ce38944b9d5e663505c5808864ba61a5e2284f3b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a><span data-ttu-id="c1f42-103">Разработка для хранилища файлов Azure на языке Java</span><span class="sxs-lookup"><span data-stu-id="c1f42-103">Develop for Azure File storage with Java</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="c1f42-104">О данном учебнике</span><span class="sxs-lookup"><span data-stu-id="c1f42-104">About this tutorial</span></span>
<span data-ttu-id="c1f42-105">В этом руководстве мы рассмотрим основы использования Java для разработки приложений и служб, использующих хранилище файлов Azure для хранения данных файлов.</span><span class="sxs-lookup"><span data-stu-id="c1f42-105">This tutorial will demonstrate the basics of using Java to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="c1f42-106">В рамках этого руководства мы создадим простое консольное приложение, а также покажем, как выполнять базовые действия с Java и хранилищем файлов Azure.</span><span class="sxs-lookup"><span data-stu-id="c1f42-106">In this tutorial, we will create a simple console application and show how to perform basic actions with Java and Azure File storage:</span></span>

* <span data-ttu-id="c1f42-107">Создание и удаление общих папок Azure.</span><span class="sxs-lookup"><span data-stu-id="c1f42-107">Create and delete Azure File shares</span></span>
* <span data-ttu-id="c1f42-108">Создание и удаление каталогов.</span><span class="sxs-lookup"><span data-stu-id="c1f42-108">Create and delete directories</span></span>
* <span data-ttu-id="c1f42-109">Перечисление файлов и каталогов в файловом ресурсе Azure.</span><span class="sxs-lookup"><span data-stu-id="c1f42-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="c1f42-110">Передача, загрузка и удаление файлов.</span><span class="sxs-lookup"><span data-stu-id="c1f42-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="c1f42-111">Так как к хранилищу файлов Azure можно обращаться через SMB, вы можете создавать простые приложения, которые получают доступ к общей папке Azure с использованием стандартных классов ввода-вывода в Java.</span><span class="sxs-lookup"><span data-stu-id="c1f42-111">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard Java I/O classes.</span></span> <span data-ttu-id="c1f42-112">Из этой статьи вы узнаете, как применять в приложениях пакет SDK Java для службы хранилища Azure, который использует [REST API хранилища файлов Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) для взаимодействия с хранилищем файлов Azure.</span><span class="sxs-lookup"><span data-stu-id="c1f42-112">This article will describe how to write applications that use the Azure Storage Java SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="c1f42-113">Создание приложения Java</span><span class="sxs-lookup"><span data-stu-id="c1f42-113">Create a Java application</span></span>
<span data-ttu-id="c1f42-114">Для создания примеров вам потребуется комплект разработчика Java (JDK) и [Пакет SDK для службы хранилища Azure для Java][].</span><span class="sxs-lookup"><span data-stu-id="c1f42-114">To build the samples, you will need the Java Development Kit (JDK) and the [Azure Storage SDK for Java][].</span></span> <span data-ttu-id="c1f42-115">Вам также необходимо создать учетную запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="c1f42-115">You should also have created an Azure storage account.</span></span>

## <a name="setup-your-application-to-use-azure-file-storage"></a><span data-ttu-id="c1f42-116">Настройка приложения для работы с хранилищем файлов Azure</span><span class="sxs-lookup"><span data-stu-id="c1f42-116">Setup your application to use Azure File storage</span></span>
<span data-ttu-id="c1f42-117">Чтобы использовать API-интерфейсы хранилища Azure, добавьте следующую инструкцию в верхнюю часть файла Java, откуда планируется осуществлять доступ к службе хранилища.</span><span class="sxs-lookup"><span data-stu-id="c1f42-117">To use the Azure storage APIs, add the following statement to the top of the Java file where you intend to access the storage service from.</span></span>

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="c1f42-118">Настройка строки подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="c1f42-118">Setup an Azure storage connection string</span></span>
<span data-ttu-id="c1f42-119">Чтобы начать работу с хранилищем файлов Azure, необходимо подключиться к учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="c1f42-119">To use Azure File storage, you need to connect to your Azure storage account.</span></span> <span data-ttu-id="c1f42-120">Для начала потребуется настроить строку подключения, которая будет использоваться для подключения к учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="c1f42-120">The first step would be to configure a connection string which we'll use to connect to your storage account.</span></span> <span data-ttu-id="c1f42-121">Для этого определим статическую переменную.</span><span class="sxs-lookup"><span data-stu-id="c1f42-121">Let's define a static variable to do that.</span></span>

```java
// Configure the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> <span data-ttu-id="c1f42-122">Замените your_storage_account_name и your_storage_account_key на фактические значения для вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="c1f42-122">Replace your_storage_account_name and your_storage_account_key with the actual values for your storage account.</span></span>
> 
> 

## <a name="connecting-to-an-azure-storage-account"></a><span data-ttu-id="c1f42-123">Подключение к учетной записи хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="c1f42-123">Connecting to an Azure storage account</span></span>
<span data-ttu-id="c1f42-124">Чтобы подключиться к учетной записи хранения, необходимо использовать объект **CloudStorageAccount**, передав строку подключения для метода **parse**.</span><span class="sxs-lookup"><span data-stu-id="c1f42-124">To connect to your storage account, you need to use the **CloudStorageAccount** object, passing a connection string to its **parse** method.</span></span>

```java
// Use the CloudStorageAccount object to connect to your storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle the exception
}
```

<span data-ttu-id="c1f42-125">**CloudStorageAccount.parse** вызывает прерывание InvalidKeyException, поэтому необходимо поместить его в блок try-catch.</span><span class="sxs-lookup"><span data-stu-id="c1f42-125">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need to put it inside a try/catch block.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="c1f42-126">Создание файлового ресурса Azure</span><span class="sxs-lookup"><span data-stu-id="c1f42-126">Create an Azure File share</span></span>
<span data-ttu-id="c1f42-127">Все файлы и каталоги в хранилище файлов Azure размещаются в контейнере, который называется общей папкой (**Share**).</span><span class="sxs-lookup"><span data-stu-id="c1f42-127">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="c1f42-128">Учетная запись хранения может иметь столько общих папок, насколько позволяет емкость вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="c1f42-128">Your storage account can have as much shares as your account capacity allows.</span></span> <span data-ttu-id="c1f42-129">Чтобы получить доступ к общей папке и ее содержимому, необходимо использовать клиент хранилища файлов Azure.</span><span class="sxs-lookup"><span data-stu-id="c1f42-129">To obtain access to a share and its contents, you need to use a Azure File storage client.</span></span>

```java
// Create the Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

<span data-ttu-id="c1f42-130">С помощью клиента хранилища файлов Azure вы получите ссылку на общую папку.</span><span class="sxs-lookup"><span data-stu-id="c1f42-130">Using the Azure File storage client, you can then obtain a reference to a share.</span></span>

```java
// Get a reference to the file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

<span data-ttu-id="c1f42-131">Чтобы создать общий ресурс, используйте метод **createIfNotExists** объекта CloudFileShare.</span><span class="sxs-lookup"><span data-stu-id="c1f42-131">To actually create the share, use the **createIfNotExists** method of the CloudFileShare object.</span></span>

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

<span data-ttu-id="c1f42-132">На этом этапе объект **share** содержит ссылку на общую папку с именем **sampleshare**.</span><span class="sxs-lookup"><span data-stu-id="c1f42-132">At this point, **share** holds a reference to a share named **sampleshare**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="c1f42-133">Удаление общей папки Azure</span><span class="sxs-lookup"><span data-stu-id="c1f42-133">Delete an Azure File share</span></span>
<span data-ttu-id="c1f42-134">Удалить общую папку можно путем вызова метода **deleteIfExists** объекта CloudFileShare.</span><span class="sxs-lookup"><span data-stu-id="c1f42-134">Deleting a share is done by calling the **deleteIfExists** method on a CloudFileShare object.</span></span> <span data-ttu-id="c1f42-135">Ниже приведен пример кода, который выполняет это действие.</span><span class="sxs-lookup"><span data-stu-id="c1f42-135">Here's sample code that does that.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference to the file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a><span data-ttu-id="c1f42-136">Создайте каталог</span><span class="sxs-lookup"><span data-stu-id="c1f42-136">Create a directory</span></span>
<span data-ttu-id="c1f42-137">Вы также можете организовать хранилище, помещая файлы в подкаталоги вместо их размещения в корневом каталоге.</span><span class="sxs-lookup"><span data-stu-id="c1f42-137">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span></span> <span data-ttu-id="c1f42-138">Хранилище файлов Azure позволяет создать столько каталогов, сколько допускает учетная запись.</span><span class="sxs-lookup"><span data-stu-id="c1f42-138">Azure File storage allows you to create as much directories as your account will allow.</span></span> <span data-ttu-id="c1f42-139">В следующем примере кода в корневом каталоге создается вложенный каталог с именем **sampledir** .</span><span class="sxs-lookup"><span data-stu-id="c1f42-139">The code below will create a sub-directory named **sampledir** under the root directory.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference to the sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a><span data-ttu-id="c1f42-140">Удаление каталога</span><span class="sxs-lookup"><span data-stu-id="c1f42-140">Delete a directory</span></span>
<span data-ttu-id="c1f42-141">Удаление каталога является достаточно простой задачей, однако следует отметить, что нельзя удалить каталог, по-прежнему содержащий файлы или другие каталоги.</span><span class="sxs-lookup"><span data-stu-id="c1f42-141">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```java
// Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference to the directory you want to delete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete the directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="c1f42-142">Перечисление файлов и каталогов в файловом ресурсе Azure</span><span class="sxs-lookup"><span data-stu-id="c1f42-142">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="c1f42-143">Получить список файлов и каталогов в общей папке довольно просто, вызвав метод **listFilesAndDirectories** по ссылке CloudFileDirectory.</span><span class="sxs-lookup"><span data-stu-id="c1f42-143">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span></span> <span data-ttu-id="c1f42-144">Метод возвращает список объектов ListFileItem, с которым вы можете производить дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="c1f42-144">The method returns a list of ListFileItem objects which you can iterate on.</span></span> <span data-ttu-id="c1f42-145">Например следующий код отображает все файлы и каталоги, содержащиеся в корневом каталоге.</span><span class="sxs-lookup"><span data-stu-id="c1f42-145">As an example, the following code will list files and directories inside the root directory.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a><span data-ttu-id="c1f42-146">Отправить файл.</span><span class="sxs-lookup"><span data-stu-id="c1f42-146">Upload a file</span></span>
<span data-ttu-id="c1f42-147">Общая папка Azure содержит по меньшей мере один каталог для размещения файлов (корневой каталог).</span><span class="sxs-lookup"><span data-stu-id="c1f42-147">An Azure File share contains at the very least, a root directory where files can reside.</span></span> <span data-ttu-id="c1f42-148">В этом разделе вы узнаете, как отправить файл из локального хранилища в корневой каталог общего ресурса.</span><span class="sxs-lookup"><span data-stu-id="c1f42-148">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="c1f42-149">Первым шагом при отправке файла является получение ссылки на каталог, где файл будет находиться.</span><span class="sxs-lookup"><span data-stu-id="c1f42-149">The first step in uploading a file is to obtain a reference to the directory where it should reside.</span></span> <span data-ttu-id="c1f42-150">Это делается путем вызова метода **getRootDirectoryReference** объекта общей папки.</span><span class="sxs-lookup"><span data-stu-id="c1f42-150">You do this by calling the **getRootDirectoryReference** method of the share object.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

<span data-ttu-id="c1f42-151">Теперь, когда у вас имеется ссылка на корневой каталог общего ресурса, вы можете отправить туда файл с помощью следующего кода.</span><span class="sxs-lookup"><span data-stu-id="c1f42-151">Now that you have a reference to the root directory of the share, you can upload a file onto it using the following code.</span></span>

```java
        // Define the path to a local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a><span data-ttu-id="c1f42-152">Скачивание файла</span><span class="sxs-lookup"><span data-stu-id="c1f42-152">Download a file</span></span>
<span data-ttu-id="c1f42-153">Одной из наиболее частых операций, которые выполняются с хранилищем файлов Azure, является операция скачивания файлов.</span><span class="sxs-lookup"><span data-stu-id="c1f42-153">One of the more frequent operations you will perform against Azure File storage is to download files.</span></span> <span data-ttu-id="c1f42-154">В следующем примере происходит скачивание файла SampleFile.txt с последующим отображением его содержимого.</span><span class="sxs-lookup"><span data-stu-id="c1f42-154">In the following example, the code downloads SampleFile.txt and displays its contents.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference to the directory that contains the file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference to the file you want to download
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write the contents of the file to the console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a><span data-ttu-id="c1f42-155">Удаление файла</span><span class="sxs-lookup"><span data-stu-id="c1f42-155">Delete a file</span></span>
<span data-ttu-id="c1f42-156">Следующая распространенная операция в хранилище файлов Azure — это удаление файлов.</span><span class="sxs-lookup"><span data-stu-id="c1f42-156">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="c1f42-157">Следующий пример программы удаляет файл с именем SampleFile.txt, хранящийся в каталоге с именем **sampledir**.</span><span class="sxs-lookup"><span data-stu-id="c1f42-157">The following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span></span>

```java
// Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference to the directory where the file to be deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a><span data-ttu-id="c1f42-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c1f42-158">Next steps</span></span>
<span data-ttu-id="c1f42-159">Если вы хотите узнать больше о других API-интерфейсах Azure, пожалуйста перейдите по следующим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="c1f42-159">If you would like to learn more about other Azure storage APIs, follow these links.</span></span>

* <span data-ttu-id="c1f42-160">[Azure for Java developers](/java/azure) (Azure для разработчиков Java)</span><span class="sxs-lookup"><span data-stu-id="c1f42-160">[Azure for Java developers](/java/azure)/)</span></span>
* [<span data-ttu-id="c1f42-161">Пакет SDK для службы хранилища Azure для Java</span><span class="sxs-lookup"><span data-stu-id="c1f42-161">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="c1f42-162">Microsoft Azure Storage SDK for Android</span><span class="sxs-lookup"><span data-stu-id="c1f42-162">Azure Storage SDK for Android</span></span>](https://github.com/azure/azure-storage-android)
* [<span data-ttu-id="c1f42-163">справочнике по пакету SDK для клиента службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="c1f42-163">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="c1f42-164">API-интерфейс REST служб хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="c1f42-164">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="c1f42-165">Блог рабочей группы службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="c1f42-165">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="c1f42-166">[Приступая к работе со служебной программой командной строки AzCopy](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)</span><span class="sxs-lookup"><span data-stu-id="c1f42-166">[Transfer data with the AzCopy Command-Line Utility](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)</span></span>