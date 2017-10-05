---
title: "Локальное приложение с хранилищем больших двоичных объектов (Java) | Документация Майкрософт"
description: "Вы узнаете, как использовать консольное приложение для загрузки изображения на Azure, а затем отобразить изображение в вашем браузере. Примеры кода написаны на Java."
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
ms.openlocfilehash: a172b881fa38a69f4510df94f5797b7a56940c52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="on-premises-application-with-blob-storage"></a>Локальное приложение с хранилищем больших двоичных объектов
## <a name="overview"></a>Обзор
В следующем примере показано, как использовать службу хранилища Azure для сохранения изображений в Azure. В этой статье представлен код для консольного приложения, которое передает изображение в Azure, а затем создает HTML-файл, отображающий это изображение в браузере.

## <a name="prerequisites"></a>Предварительные требования
* Установленный пакет Java Developer Kit (JDK) версии 1.6 или более поздней.
* Установленный пакет Azure SDK.
* JAR-файл для библиотек Azure для Java и JAR-файлы для любых применимых зависимостей, установлены и указаны в пути сборки, который используется компилятором Java. Сведения об установке библиотек Azure для Java см. в статье [Загрузка пакета Azure SDK для Java](../java-download-azure-sdk.md).
* Настроенная учетная запись хранения Azure. Имя и ключ учетной записи хранения используются в коде в этой статье. Сведения о создании учетной записи хранения см. в разделе [Создание учетной записи хранения](storage-create-storage-account.md#create-a-storage-account). Сведения о получении ключа учетной записи см. в разделе [Просмотр и копирование ключей доступа к хранилищу](storage-create-storage-account.md#view-and-copy-storage-access-keys).
* Вы создали локальный файл изображения, который был сохранен с именем c:\\myimages\\image1.jpg. Как вариант, можно изменить конструктор **FileInputStream** в данном примере, чтобы использовать другой путь и другое имя для изображения.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="to-use-azure-blob-storage-to-upload-a-file"></a>Использование хранилища больших двоичных объектов Azure для отправки файла
В этом разделе описывается пошаговая процедура. Если вы желаете пропустить описание шагов, можно просмотреть полную версию кода далее в этой статье.

Начните код с операций импорта для базовых классов службы хранилища Azure, классов клиента больших двоичных объектов Azure, классов ввода-вывода Java и класса **URISyntaxException** .

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

Объявите класс с именем **StorageSample** и включите открывающую скобку **{**.

```java
public class StorageSample {
```

В классе **StorageSample** объявите строковую переменную, которая будет содержать протокол конечной точки по умолчанию, имя вашей учетной записи хранения и ключ доступа к хранилищу, как указано в вашей учетной записи хранения Azure. Замените значения заполнителей **your\_account\_name** и **your\_account\_key** именем и ключом своей учетной записи соответственно.

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

Добавьте объявление **main**, укажите блок **try** и вставьте необходимые открывающие скобки **{**.

```java
    public static void main(String[] args)
    {
        try
        {
```

Объявите переменные следующего типа (описания их использования приведены в этом примере):

* **CloudStorageAccount**: используется для инициализации объекта учетной записи с использованием имени и ключа учетной записи хранения Azure, а также для создания BLOB-объекта клиента.
* **CloudBlobClient**: используется для доступа к службе BLOB-объектов.
* **CloudBlobContainer**: используется для создания контейнера больших двоичных объектов, перечисления BLOB-объектов в контейнере и удаления контейнера.
* **CloudBlockBlob**: используется для отправки локального файла изображения в контейнер.

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

Присвойте значение переменной **account** .

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

Присвойте значение переменной **serviceClient** .

```java
serviceClient = account.createCloudBlobClient();
```

Присвойте значение переменной **container** . В результате вы получите ссылку на контейнер с именем **gettingstarted**.

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

Создайте контейнер. Этот метод создает контейнер, если он не существует (и возвращает значение **true**). Если контейнер не существует, метод вернет значение **false**. Вместо метода **createIfNotExists** можно использовать метод **create** (который возвращает ошибку, если контейнер уже существует).

```java
container.createIfNotExists();
```

Настройте анонимный доступ к контейнеру.

```java
// Set anonymous access on the container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

Получите ссылку на блочный BLOB-объект, который будет представлять BLOB-объект в хранилище Azure.

```java
blob = container.getBlockBlobReference("image1.jpg");
```

Используйте конструктор **File** , чтобы получить ссылку на локально созданный файл, который требуется отправить. (Перед выполнением этого кода убедитесь,что вы создали этот файл.)

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

Отправьте локальный файл путем вызова метода **CloudBlockBlob.upload** . Первым параметром метода **CloudBlockBlob.upload** является объект **FileInputStream**, представляющий локальный файл, предназначенный для отправки в службу хранилища Azure. Вторым параметром является размер файла в байтах.

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

Вызовите вспомогательную функцию с именем **MakeHTMLPage**, чтобы создать базовую страницу HTML, содержащую элемент **&lt;image&gt;** с источником в виде большого двоичного объекта, присутствующего в вашей учетной записи хранения Azure. Код для **MakeHTMLPage** описан ниже в этой статье.

```java
MakeHTMLPage(container);
```

Распечатайте сообщение о состоянии и сведения о созданной странице HTML.

```java
System.out.println("Processing complete.");
System.out.println("Open index.html to see the images stored in your storage account.");
```

Закройте блок **try**, вставив закрывающую скобку: **}**

Реализуйте обработку следующих исключений:

* **FileNotFoundException**: может вызываться конструктором **FileInputStream** или **FileOutputStream**.
* **StorageException**: может вызываться клиентской библиотекой хранилища Azure.
* **URISyntaxException**: может вызываться методом **ListBlobItem.getUri**.
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

Создайте метод с именем **MakeHTMLPage** для создания базовой страницы HTML. Этот метод содержит параметр типа **CloudBlobContainer**, который будет использоваться для выполнения итерации по списку отправленных BLOB-объектов. Данный метод вызовет исключения типа **FileNotFoundException**, которые могут быть обусловлены конструктором **FileOutputStream**, и типа **URISyntaxException**, которые могут быть обусловлены методом **ListBlobItem.getUri**. Вставьте открывающую скобку **{**.

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

Создайте локальный файл с именем **index.html**.

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

Выполните запись в локальный файл, добавив элементы **&lt;html&gt;**, **&lt;header&gt;** и **&lt;body&gt;**.

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

Выполните итерацию по списку отправленных BLOB-объектов. Для каждого большого двоичного объекта на странице HTML создайте элемент **&lt;img&gt;**, атрибут **src** которого отправляется в URI большого двоичного объекта в том виде, в котором он существует в вашей учетной записи хранения Azure.
Хотя в этот пример было добавлено всего одно изображение, при добавлении нескольких изображений код будет выполнять итерации по всем изображениям.

Для простоты в этом примере предполагается, что каждый отправленный BLOB-объект является изображением. Если вы обновили большие двоичные объекты, отличные от изображений или которые являются страницами больших двоичных объектов, а не блоками больших двоичных объектов, скорректируйте код соответствующим образом.

```java
// Enumerate the uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in the HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

Закройте элементы **&lt;body&gt;** и **&lt;html&gt;**.

```java
stream.println("</body>");
stream.println("</html>");
```

Закройте локальный файл.

```java
stream.close();
```

Закройте **MakeHTMLPage**, вставив закрывающую скобку: **}**

Закройте **StorageSample**, вставив закрывающую скобку: **}**

Ниже приведен полный код для этого примера. Не забудьте заменить значения заполнителей **your\_account\_name** и **your\_account\_key** именем и ключом своей учетной записи соответственно.

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;

// Create an image, c:\myimages\image1.jpg, prior to running this sample.
// Alternatively, change the value used by the FileInputStream constructor
// to use a different image path and file that you have already created.
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

            // Set anonymous access on the container.
            BlobContainerPermissions containerPermissions;
            containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // Upload an image file.
            blob = container.getBlockBlobReference("image1.jpg");

            File fileReference = new File("c:\\myimages\\image1.jpg");
            blob.upload(new FileInputStream(fileReference), fileReference.length());

            // At this point the image is uploaded.
            // Next, create an HTML page that lists all of the uploaded images.
            MakeHTMLPage(container);

            System.out.println("Processing complete.");
            System.out.println("Open index.html to see the images stored in your storage account.");

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

    // Create an HTML page that can be used to display the uploaded images.
    // This example assumes all of the blobs are for images.
    public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
    {
        PrintStream stream;
        stream = new PrintStream(new FileOutputStream("index.html"));

        // Create the opening <html>, <header>, and <body> elements.
        stream.println("<html>");
        stream.println("<header/>");
        stream.println("<body>");

        // Enumerate the uploaded blobs.
        for (ListBlobItem blobItem : container.listBlobs()) {
            // List each blob as an <img> element in the HTML body.
            stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
        }

        stream.println("</body>");

        // Complete the <html> element and close the file.
        stream.println("</html>");
        stream.close();
    }
}
```

Кроме отправки локального файла изображения в хранилище Azure, в этом примере кода создается локальный файл с именем index.html, который можно открыть в браузере для просмотра отправленного изображения.

Поскольку код содержит имя учетной записи и ключ учетной записи, обеспечьте безопасность исходного кода.

## <a name="to-delete-a-container"></a>Удаление контейнера
Поскольку за использование хранилища начисляется плата, вам может потребоваться удалить контейнер **gettingstarted** после окончания работы с данным примером. Чтобы удалить контейнер, используйте метод **CloudBlobContainer.delete** .

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

Чтобы вызвать метод **CloudBlobContainer.delete**, необходимо выполнить процесс инициализации объектов **CloudStorageAccount**, **ClodBlobClient** и **CloudBlobContainer**, который аналогичен приведенному процессу для метода **createIfNotExist**. Ниже приведен полный пример удаления контейнера с именем **gettingstarted**.

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

Обзор других классов и методов хранилища BLOB-объектов см. в статье [Использование хранилища BLOB-объектов из Java](storage-java-how-to-use-blob-storage.md).

## <a name="next-steps"></a>Дальнейшие действия
Дополнительную информацию о выполнении более сложных задач хранения см. по указанным ссылкам.

* [Пакет SDK для службы хранилища Azure для Java](https://github.com/azure/azure-storage-java)
* [справочнике по пакету SDK для клиента службы хранилища Azure](http://dl.windowsazure.com/storage/javadoc/)
* [API-интерфейс REST служб хранилища Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Блог рабочей группы службы хранилища Azure](http://blogs.msdn.com/b/windowsazurestorage/)

