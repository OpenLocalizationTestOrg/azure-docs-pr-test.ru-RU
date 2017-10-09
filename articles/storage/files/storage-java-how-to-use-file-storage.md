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
ms.openlocfilehash: be71a946604da8af0130f101f2eb6135c5e08abd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a>Разработка для хранилища файлов Azure на языке Java
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a>О данном учебнике
Этот учебник продемонстрируют hello основные принципы использования Java toodevelop приложений или служб, которые используют данные файла toostore хранилище файлов Azure. В этом учебнике мы создайте простое консольное приложение и Показать как tooperform базовые действия с хранилищем, Java и файлов Azure:

* Создание и удаление общих папок Azure.
* Создание и удаление каталогов.
* Перечисление файлов и каталогов в файловом ресурсе Azure.
* Передача, загрузка и удаление файлов.

> [!Note]  
> Поскольку хранилище файлов Azure может осуществляться по протоколу SMB, вполне возможно toowrite простых приложений, получающих доступ к папке файлов Azure hello, с помощью стандартных классов ввода-вывода Java hello. В этой статье описывается, как toowrite приложения, использующие hello SDK Java хранилища Azure, которая использует hello [хранилища Azure File API-интерфейса REST](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure хранилища файлов.

## <a name="create-a-java-application"></a>Создание приложения Java
образцы toobuild hello, необходимо будет hello Java Development Kit (JDK) и hello [пакет SDK хранилища Azure для Java] []. Вам также необходимо создать учетную запись хранилища Azure.

## <a name="setup-your-application-toouse-azure-file-storage"></a>Настройка вашего приложения toouse хранилища Azure File
hello toouse хранилища Azure API-интерфейсы, добавить hello, следующая инструкция toohello вверху hello файл Java, где планируется службы хранения hello tooaccess из.

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Настройка строки подключения к службе хранилища Azure
toouse хранилища Azure File, необходима учетная запись хранилища Azure tooyour tooconnect. Hello первым шагом будет tooconfigure строку подключения, которая будет использоваться учетная запись хранения tooyour tooconnect. Определим статических переменных toodo.

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> Замените your_storage_account_name и your_storage_account_key hello фактические значения для вашей учетной записи.
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a>Учетной записи хранилища Azure tooan подключения
Учетная запись хранения tooyour tooconnect необходимо toouse hello **CloudStorageAccount** объекта, передавая tooits строка подключения **синтаксический анализ** метод.

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

**CloudStorageAccount.parse** выдает InvalidKeyException, поэтому вам понадобится tooput его внутри try/catch блока.

## <a name="create-an-azure-file-share"></a>Создание файлового ресурса Azure
Все файлы и каталоги в хранилище файлов Azure размещаются в контейнере, который называется общей папкой (**Share**). Учетная запись хранения может иметь столько общих папок, насколько позволяет емкость вашей учетной записи. tooobtain доступа tooa общей папки и ее содержимое, необходимо toouse клиент хранилища файлов Azure.

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

С помощью клиента хранилища Azure файл hello, это позволяет получить общую папку tooa ссылки.

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

tooactually создать общий ресурс hello, используйте hello **createIfNotExists** метод объекта CloudFileShare hello.

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

На этом этапе **совместное использование** содержит общую папку tooa ссылку с именем **sampleshare**.

## <a name="delete-an-azure-file-share"></a>Удаление общей папки Azure
Удаление общей папки выполняется путем вызова hello **deleteIfExists** метод на объекте CloudFileShare. Ниже приведен пример кода, который выполняет это действие.

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

## <a name="create-a-directory"></a>Создайте каталог
Кроме того, можно организовать хранилища путем помещения файлов в подкаталоги вместо их все в корневом каталоге hello. Хранилище файлов Azure позволяет toocreate как разрешить много каталоги, как будет вашей учетной записи. Приведенный ниже код Hello будет создавать вложенный каталог с именем **sampledir** в корневом каталоге hello.

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

## <a name="delete-a-directory"></a>Удаление каталога
Удаление каталога является достаточно простой задачей, однако следует отметить, что нельзя удалить каталог, по-прежнему содержащий файлы или другие каталоги.

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

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Перечисление файлов и каталогов в файловом ресурсе Azure
Получить список файлов и каталогов в общей папке довольно просто, вызвав метод **listFilesAndDirectories** по ссылке CloudFileDirectory. метод Hello возвращает список объектов ListFileItem, которые можно выполнять итерацию по. В качестве примера hello следующий код будет список файлов и каталогов в корневой каталог hello.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a>Отправить файл.
Общая папка содержит в hello очень бы файл Azure, корневой каталог, где находятся файлы, можно. В этом разделе вы узнаете, как tooupload файла из локального хранилища на hello корневой каталог общего ресурса.

Первым шагом Hello в передаче файла является tooobtain каталог toohello ссылок, где он находится. Это делается путем вызова hello **getRootDirectoryReference** метод hello объекта общей папки.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

Теперь, когда имеется ссылка toohello корневой каталог общего ресурса hello, можно отправить файл на него с помощью hello, следующий код.

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a>Скачивание файла
Одной из более частая операции, которые будут выполняться с хранилища Azure File hello является toodownload файлов. В следующем примере hello hello код загружает SampleFile.txt и отображает его содержимое.

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

## <a name="delete-a-file"></a>Удаление файла
Следующая распространенная операция в хранилище файлов Azure — это удаление файлов. Hello следующий код удаляет файл с именем SampleFile.txt, хранящийся в каталоге с именем **sampledir**.

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

## <a name="next-steps"></a>Дальнейшие действия
Если вы хотите toolearn Дополнительные сведения о других хранилища Azure API-интерфейсы, приведены по следующим ссылкам.

* [Azure for Java developers](/java/azure) (Azure для разработчиков Java)
* [Пакет SDK для службы хранилища Azure для Java](https://github.com/azure/azure-storage-java)
* [Microsoft Azure Storage SDK for Android](https://github.com/azure/azure-storage-android)
* [справочнике по пакету SDK для клиента службы хранилища Azure](http://dl.windowsazure.com/storage/javadoc/)
* [API-интерфейс REST служб хранилища Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Блог рабочей группы службы хранилища Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* [Перенесите данные с помощью служебной программы командной строки AzCopy hello](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)