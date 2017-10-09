---
title: "aaaOn локальное приложение с хранилищем больших двоичных объектов (Java) | Документы Microsoft"
description: "Узнайте, как toocreate консольное приложение, которое передает tooAzure образа, а затем отображает hello изображения в браузере. Примеры кода написаны на Java."
services: storage
documentationcenter: java
author: mmacy
manager: carmonm
editor: tysonn
ms.assetid: ccc9a7d7-6fe4-467b-b7fd-a73f17539e3f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/17/2016
ms.author: marsma
ms.openlocfilehash: ed8eb4c1045691c25abe94bf6c1b18b797adc3e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="on-premises-application-with-blob-storage"></a>Локальное приложение с хранилищем больших двоичных объектов
## <a name="overview"></a>Обзор
Hello пример при использовании хранилища Azure для хранения изображений в Azure. Hello в этой статье приведен для консольное приложение, которое передает tooAzure образа, а затем создает HTML-файл, которое отображает hello изображения в браузере.

## <a name="prerequisites"></a>Предварительные требования
* Установленный пакет Java Developer Kit (JDK) версии 1.6 или более поздней.
* Hello Azure SDK установлен.
* Hello JAR hello библиотек Azure для Java и JAR-файлов любые применимые зависимостей, установлены и находятся в пути сборки hello, используемые компилятором Java. Сведения об установке hello библиотек Azure для Java см. в разделе [hello загрузки пакета Azure SDK для Java](../java-download-azure-sdk.md).
* Настроенная учетная запись хранения Azure. Hello имя учетной записи и ключ учетной записи хранилища hello будет использоваться кода hello в этой статье. В разделе [как tooCreate учетной записи хранилища](storage-create-storage-account.md#create-a-storage-account) сведения о создании учетной записи хранилища и [представление и скопируйте ключи доступа к хранилищу](storage-create-storage-account.md#view-and-copy-storage-access-keys) сведения о получении ключа учетной записи hello.
* Созданный файл с именем локального изображения хранятся на hello path c:\\myimages\\image1.jpg. Кроме того, изменить **FileInputStream** конструктор в примере hello toouse другое изображение путь и имя файла.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="toouse-azure-blob-storage-tooupload-a-file"></a>tooupload хранилища BLOB-объектов Azure toouse файла
В этом разделе описывается пошаговая процедура. Если вы хотите tooskip вперед, далее в этой статье представлены hello весь код.

Начать кода hello, включая Импорт для классы хранения Azure core hello, hello BLOB-объектов Azure клиентские классы, классы ввода-ВЫВОДА Java hello и hello **URISyntaxException** класса.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

Объявите класс с именем **StorageSample**и включать hello открывающей скобки, **{**.

```java
public class StorageSample {
```

В рамках hello **StorageSample** объявите строковую переменную, которая будет содержать протокол конечной точки по умолчанию hello, имя учетной записи хранилища и ключи доступа к хранилищу, как указано в вашей учетной записи хранилища Azure. Замените значения заполнителей hello **вашей\_учетной записи\_имя** и **вашей\_учетной записи\_ключ** имя учетной записи и ключ учетной записи соответственно.

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

Добавьте в объявление для **основной**, включают **повторите** блокировку и включить необходимые открывающими скобками hello, **{**.

```java
    public static void main(String[] args)
    {
        try
        {
```

Объявления переменных hello после типа (приветствия, описание их использования в этом примере):

* **CloudStorageAccount**: hello tooinitialize используется объект учетной записи с именем учетной записи хранилища Azure и ключ и toocreate большой двоичный объект клиента.
* **CloudBlobClient**: использовать службы BLOB-объектов tooaccess hello.
* **CloudBlobContainer**: используется toocreate контейнер больших двоичных объектов перечисление BLOB-объектов в контейнере hello и удаления контейнера hello.
* **CloudBlockBlob**: используется tooupload контейнер toothe образ в локальный файл.

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

Назначьте toohello значение **учетной записи** переменной.

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

Назначьте toohello значение **serviceClient** переменной.

```java
serviceClient = account.createCloudBlobClient();
```

Назначьте toohello значение **контейнера** переменной. Мы получаем ссылки tooa контейнер **Приступая к работе**.

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

Создание контейнера hello. Если он не существует, этот метод создаст контейнер hello (и возвращают **true**). Если hello контейнер существует, он будет возвращать **false**. Альтернативы слишком**createIfNotExists** — hello **создания** метод (которая будет возвращена ошибка, если контейнер hello уже существует).

```java
container.createIfNotExists();
```

Задать анонимного доступа для контейнера hello.

```java
// Set anonymous access on hello container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

Получите ссылку toohello большого двоичного объекта, который будет представлять hello BLOB-объектов в хранилище Azure.

```java
blob = container.getBlockBlobReference("image1.jpg");
```

Используйте hello **файл** конструктор tooget toohello локально созданные ссылочного файла, который будет передан. Убедитесь, что вы создали этот файл перед запуском кода hello.

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

Hello локального компьютера файл через toohello вызов **CloudBlockBlob.upload** метод. Здравствуйте, первый параметр toohello **CloudBlockBlob.upload** метод **FileInputStream** объекта, представляет hello локальный файл, будут отправлены tooAzure хранилища. Второй параметр Hello — hello размер файла в байтах, hello.

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

Вызовите вспомогательную функцию с именем **MakeHTMLPage**, страница toomake простой HTML-документ, содержащий  **&lt;изображения&gt;**  элемент с hello исходного набора toohello большого двоичного объекта, работающего в Azure Учетная запись хранения. Здравствуйте, код для **MakeHTMLPage** обсуждаются далее в этой статье.

```java
MakeHTMLPage(container);
```

Выводит сообщения о состоянии и сведения о hello, создаваемую страницу HTML.

```java
System.out.println("Processing complete.");
System.out.println("Open index.html toosee hello images stored in your storage account.");
```

Закрыть hello **повторите** блока, вставив закрывающая квадратная скобка: **}**

Дескриптор hello следующие исключения:

* **FileNotFoundException**: могут создаваться инфраструктурой hello **FileInputStream** или **FileOutputStream** конструкторы.
* **StorageException**: создаваемые библиотекой хранилища Azure клиента hello.
* **URISyntaxException**: могут создаваться инфраструктурой hello **ListBlobItem.getUri** метод.
* **Исключение**: обработка универсального исключения.

<!-- -->

```java
catch (FileNotFoundException fileNotFoundException)
{
    System.out.print("FileNotFoundException encountered: ");
    System.out.println(fileNotFoundException.getMessage());
    System.exit(-1);
}
catch (StorageException storageException)
{
    System.out.print("StorageException encountered: ");
    System.out.println(storageException.getMessage());
    System.exit(-1);
}
catch (URISyntaxException uriSyntaxException)
{
    System.out.print("URISyntaxException encountered: ");
    System.out.println(uriSyntaxException.getMessage());
    System.exit(-1);
}
catch (Exception e)
{
    System.out.print("Exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Закройте **main**, вставив закрывающую скобку: **}**

Создайте метод с именем **MakeHTMLPage** toocreate основные HTML-страницы. Этот метод имеет параметр типа **CloudBlobContainer**, которое будет используется tooiterate через список hello отправленного больших двоичных объектов. Этот метод будет выдавать исключения типа **FileNotFoundException**, которой могут создаваться инфраструктурой hello **FileOutputStream** конструктор, и **URISyntaxException**, которого можно вызывается hello **ListBlobItem.getUri** метод. Вставьте открывающую скобку **{**.

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

Создайте локальный файл с именем **index.html**.

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

Записи toohello локального файла, добавление в hello  **&lt;html&gt;**,  **&lt;заголовок&gt;**, и  **&lt;текст&gt;**  элементов.

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

Итерации списка hello загруженного BLOB-объектов. Для каждого большого двоичного объекта hello HTML странице, создайте  **&lt;img&gt;**  элемент, имеющий его **src** атрибут, отправляемые hello URI большого двоичного объекта hello, которое существовало в вашей учетной записи хранилища Azure.
Хотя в этот пример было добавлено всего одно изображение, при добавлении нескольких изображений код будет выполнять итерации по всем изображениям.

Для простоты в этом примере предполагается, что каждый отправленный BLOB-объект является изображением. Если вы обновили больших двоичных объектов, кроме изображений или страничных больших двоичных объектов вместо блочных больших двоичных объектов, настройте код hello при необходимости.

```java
// Enumerate hello uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in hello HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

Закрыть hello  **&lt;текст&gt;**  элемент и hello  **&lt;html&gt;**  элемента.

```java
stream.println("</body>");
stream.println("</html>");
```

Закрыть hello в локальный файл.

```java
stream.close();
```

Закройте **MakeHTMLPage**, вставив закрывающую скобку: **}**

Закройте **StorageSample**, вставив закрывающую скобку: **}**

Hello ниже приведен полный код этого примера hello. Запомнить значения заполнителей hello toomodify **вашей\_учетной записи\_имя** и **вашей\_учетной записи\_ключ** toouse имя учетной записи и учетной записи ключ, соответственно.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;

// Create an image, c:\myimages\image1.jpg, prior toorunning this sample.
// Alternatively, change hello value used by hello FileInputStream constructor
// toouse a different image path and file that you have already created.
public class StorageSample {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                    "AccountName=your_account_name;" +
                    "AccountKey=your_account_name";

    public static void main(String[] args) {
        try {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;
            CloudBlockBlob blob;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.createIfNotExists();

            // Set anonymous access on hello container.
            BlobContainerPermissions containerPermissions;
            containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // Upload an image file.
            blob = container.getBlockBlobReference("image1.jpg");

            File fileReference = new File("c:\\myimages\\image1.jpg");
            blob.upload(new FileInputStream(fileReference), fileReference.length());

            // At this point hello image is uploaded.
            // Next, create an HTML page that lists all of hello uploaded images.
            MakeHTMLPage(container);

            System.out.println("Processing complete.");
            System.out.println("Open index.html toosee hello images stored in your storage account.");

        } catch (FileNotFoundException fileNotFoundException) {
            System.out.print("FileNotFoundException encountered: ");
            System.out.println(fileNotFoundException.getMessage());
            System.exit(-1);
        } catch (StorageException storageException) {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        } catch (URISyntaxException uriSyntaxException) {
            System.out.print("URISyntaxException encountered: ");
            System.out.println(uriSyntaxException.getMessage());
            System.exit(-1);
        } catch (Exception e) {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }

    // Create an HTML page that can be used toodisplay hello uploaded images.
    // This example assumes all of hello blobs are for images.
    public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
    {
        PrintStream stream;
        stream = new PrintStream(new FileOutputStream("index.html"));

        // Create hello opening <html>, <header>, and <body> elements.
        stream.println("<html>");
        stream.println("<header/>");
        stream.println("<body>");

        // Enumerate hello uploaded blobs.
        for (ListBlobItem blobItem : container.listBlobs()) {
            // List each blob as an <img> element in hello HTML body.
            stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
        }

        stream.println("</body>");

        // Complete hello <html> element and close hello file.
        stream.println("</html>");
        stream.close();
    }
}
```

В дополнение toouploading файл tooAzure хранилище локального изображения, hello пример кода создает namedindex.html локальный файл, который можно открыть в ваш браузер toosee загруженного образа.

Так как код hello содержит имя учетной записи и ключ учетной записи, гарантирует исходный код безопасности.

## <a name="toodelete-a-container"></a>toodelete контейнера
Поскольку плата взимается для хранения данных, возможно, стоит toodelete **Приступая к работе** контейнер после выполнения экспериментов с этим примером. toodelete является контейнером, используйте hello **CloudBlobContainer.delete** метод.

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

toocall hello **CloudBlobContainer.delete** метод, процесс инициализации hello **CloudStorageAccount**, **ClodBlobClient**, и  **CloudBlobContainer** объектов Здравствуйте, так же, как показано для **createIfNotExist** метод. Hello ниже приведен полный пример, что операции удаления hello контейнер с именем **Приступая к работе**.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;

public class DeleteContainer {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                "AccountName=your_account_name;" +
                "AccountKey=your_account_key";

    public static void main(String[] args)
    {
        try
        {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.delete();

            System.out.println("Container deleted.");

        }
        catch (StorageException storageException)
        {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        }
        catch (Exception e)
        {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }
}
```

Обзор другие классы хранения больших двоичных объектов и методов см. в разделе [как хранилище больших двоичных объектов из Java toouse](storage-java-how-to-use-blob-storage.md).

## <a name="next-steps"></a>Дальнейшие действия
Выполните эти дополнительные сведения о более сложных задач хранилища toolearn ссылки.

* [Пакет SDK для службы хранилища Azure для Java](https://github.com/azure/azure-storage-java)
* [справочнике по пакету SDK для клиента службы хранилища Azure](http://dl.windowsazure.com/storage/javadoc/)
* [API-интерфейс REST служб хранилища Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Блог рабочей группы службы хранилища Azure](http://blogs.msdn.com/b/windowsazurestorage/)

