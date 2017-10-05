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
# <a name="on-premises-application-with-blob-storage"></a><span data-ttu-id="a92d2-104">Локальное приложение с хранилищем больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="a92d2-104">On-premises application with blob storage</span></span>
## <a name="overview"></a><span data-ttu-id="a92d2-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="a92d2-105">Overview</span></span>
<span data-ttu-id="a92d2-106">В следующем примере показано, как использовать службу хранилища Azure для сохранения изображений в Azure.</span><span class="sxs-lookup"><span data-stu-id="a92d2-106">The following example shows you how you can use Azure storage to store images in Azure.</span></span> <span data-ttu-id="a92d2-107">В этой статье представлен код для консольного приложения, которое передает изображение в Azure, а затем создает HTML-файл, отображающий это изображение в браузере.</span><span class="sxs-lookup"><span data-stu-id="a92d2-107">The code in this article is for a console application that uploads an image to Azure, and then creates an HTML file that displays the image in your browser.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a92d2-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a92d2-108">Prerequisites</span></span>
* <span data-ttu-id="a92d2-109">Установленный пакет Java Developer Kit (JDK) версии 1.6 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="a92d2-109">A Java Developer Kit (JDK), version 1.6 or later, is installed.</span></span>
* <span data-ttu-id="a92d2-110">Установленный пакет Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="a92d2-110">The Azure SDK is installed.</span></span>
* <span data-ttu-id="a92d2-111">JAR-файл для библиотек Azure для Java и JAR-файлы для любых применимых зависимостей, установлены и указаны в пути сборки, который используется компилятором Java.</span><span class="sxs-lookup"><span data-stu-id="a92d2-111">The JAR for the Azure Libraries for Java, and any applicable dependency JARs, are installed and are in the build path used by your Java compiler.</span></span> <span data-ttu-id="a92d2-112">Сведения об установке библиотек Azure для Java см. в статье [Загрузка пакета Azure SDK для Java](../java-download-azure-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="a92d2-112">For information about installing the Azure Libraries for Java, see [Download the Azure SDK for Java](../java-download-azure-sdk.md).</span></span>
* <span data-ttu-id="a92d2-113">Настроенная учетная запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="a92d2-113">An Azure storage account has been set up.</span></span> <span data-ttu-id="a92d2-114">Имя и ключ учетной записи хранения используются в коде в этой статье.</span><span class="sxs-lookup"><span data-stu-id="a92d2-114">The account name and account key for the storage account will be used by the code in this article.</span></span> <span data-ttu-id="a92d2-115">Сведения о создании учетной записи хранения см. в разделе [Создание учетной записи хранения](storage-create-storage-account.md#create-a-storage-account). Сведения о получении ключа учетной записи см. в разделе [Просмотр и копирование ключей доступа к хранилищу](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="a92d2-115">See [How to Create a Storage Account](storage-create-storage-account.md#create-a-storage-account) for information about creating a storage account, and [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys) for information about retrieving the account key.</span></span>
* <span data-ttu-id="a92d2-116">Вы создали локальный файл изображения, который был сохранен с именем c:\\myimages\\image1.jpg.</span><span class="sxs-lookup"><span data-stu-id="a92d2-116">You have created a local image file named stored at the path c:\\myimages\\image1.jpg.</span></span> <span data-ttu-id="a92d2-117">Как вариант, можно изменить конструктор **FileInputStream** в данном примере, чтобы использовать другой путь и другое имя для изображения.</span><span class="sxs-lookup"><span data-stu-id="a92d2-117">Alternatively, modify the **FileInputStream** constructor in the example to use a different image path and file name.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="to-use-azure-blob-storage-to-upload-a-file"></a><span data-ttu-id="a92d2-118">Использование хранилища больших двоичных объектов Azure для отправки файла</span><span class="sxs-lookup"><span data-stu-id="a92d2-118">To use Azure blob storage to upload a file</span></span>
<span data-ttu-id="a92d2-119">В этом разделе описывается пошаговая процедура.</span><span class="sxs-lookup"><span data-stu-id="a92d2-119">A step-by-step procedure is presented here.</span></span> <span data-ttu-id="a92d2-120">Если вы желаете пропустить описание шагов, можно просмотреть полную версию кода далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="a92d2-120">If you'd like to skip ahead, the entire code is presented later in this article.</span></span>

<span data-ttu-id="a92d2-121">Начните код с операций импорта для базовых классов службы хранилища Azure, классов клиента больших двоичных объектов Azure, классов ввода-вывода Java и класса **URISyntaxException** .</span><span class="sxs-lookup"><span data-stu-id="a92d2-121">Begin the code by including imports for the Azure core storage classes, the Azure blob client classes, the Java IO classes, and the **URISyntaxException** class.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

<span data-ttu-id="a92d2-122">Объявите класс с именем **StorageSample** и включите открывающую скобку **{**.</span><span class="sxs-lookup"><span data-stu-id="a92d2-122">Declare a class named **StorageSample**, and include the open bracket, **{**.</span></span>

```java
public class StorageSample {
```

<span data-ttu-id="a92d2-123">В классе **StorageSample** объявите строковую переменную, которая будет содержать протокол конечной точки по умолчанию, имя вашей учетной записи хранения и ключ доступа к хранилищу, как указано в вашей учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="a92d2-123">Within the **StorageSample** class, declare a string variable that will contain the default endpoint protocol, your storage account name, and your storage access key, as specified in your Azure storage account.</span></span> <span data-ttu-id="a92d2-124">Замените значения заполнителей **your\_account\_name** и **your\_account\_key** именем и ключом своей учетной записи соответственно.</span><span class="sxs-lookup"><span data-stu-id="a92d2-124">Replace the placeholder values **your\_account\_name** and **your\_account\_key** with your own account name and account key, respectively.</span></span>

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

<span data-ttu-id="a92d2-125">Добавьте объявление **main**, укажите блок **try** и вставьте необходимые открывающие скобки **{**.</span><span class="sxs-lookup"><span data-stu-id="a92d2-125">Add in your declaration for **main**, include a **try** block, and include the necessary open brackets, **{**.</span></span>

```java
    public static void main(String[] args)
    {
        try
        {
```

<span data-ttu-id="a92d2-126">Объявите переменные следующего типа (описания их использования приведены в этом примере):</span><span class="sxs-lookup"><span data-stu-id="a92d2-126">Declare variables of the following type (the descriptions are for how they are used in this example):</span></span>

* <span data-ttu-id="a92d2-127">**CloudStorageAccount**: используется для инициализации объекта учетной записи с использованием имени и ключа учетной записи хранения Azure, а также для создания BLOB-объекта клиента.</span><span class="sxs-lookup"><span data-stu-id="a92d2-127">**CloudStorageAccount**: Used to initialize the account object with your Azure storage account name and key, and to create the blob client object.</span></span>
* <span data-ttu-id="a92d2-128">**CloudBlobClient**: используется для доступа к службе BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="a92d2-128">**CloudBlobClient**: Used to access the blob service.</span></span>
* <span data-ttu-id="a92d2-129">**CloudBlobContainer**: используется для создания контейнера больших двоичных объектов, перечисления BLOB-объектов в контейнере и удаления контейнера.</span><span class="sxs-lookup"><span data-stu-id="a92d2-129">**CloudBlobContainer**: Used to create a blob container, list the blobs in the container, and delete the container.</span></span>
* <span data-ttu-id="a92d2-130">**CloudBlockBlob**: используется для отправки локального файла изображения в контейнер.</span><span class="sxs-lookup"><span data-stu-id="a92d2-130">**CloudBlockBlob**: Used to upload a local image file to the container.</span></span>

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

<span data-ttu-id="a92d2-131">Присвойте значение переменной **account** .</span><span class="sxs-lookup"><span data-stu-id="a92d2-131">Assign a value to the **account** variable.</span></span>

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

<span data-ttu-id="a92d2-132">Присвойте значение переменной **serviceClient** .</span><span class="sxs-lookup"><span data-stu-id="a92d2-132">Assign a value to the **serviceClient** variable.</span></span>

```java
serviceClient = account.createCloudBlobClient();
```

<span data-ttu-id="a92d2-133">Присвойте значение переменной **container** .</span><span class="sxs-lookup"><span data-stu-id="a92d2-133">Assign a value to the **container** variable.</span></span> <span data-ttu-id="a92d2-134">В результате вы получите ссылку на контейнер с именем **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="a92d2-134">We'll get a reference to a container named **gettingstarted**.</span></span>

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

<span data-ttu-id="a92d2-135">Создайте контейнер.</span><span class="sxs-lookup"><span data-stu-id="a92d2-135">Create the container.</span></span> <span data-ttu-id="a92d2-136">Этот метод создает контейнер, если он не существует (и возвращает значение **true**).</span><span class="sxs-lookup"><span data-stu-id="a92d2-136">This method will create the container if it doesn't exist (and return **true**).</span></span> <span data-ttu-id="a92d2-137">Если контейнер не существует, метод вернет значение **false**.</span><span class="sxs-lookup"><span data-stu-id="a92d2-137">If the container does exist, it will return **false**.</span></span> <span data-ttu-id="a92d2-138">Вместо метода **createIfNotExists** можно использовать метод **create** (который возвращает ошибку, если контейнер уже существует).</span><span class="sxs-lookup"><span data-stu-id="a92d2-138">An alternative to **createIfNotExists** is the **create** method (which will return an error if the container already exists).</span></span>

```java
container.createIfNotExists();
```

<span data-ttu-id="a92d2-139">Настройте анонимный доступ к контейнеру.</span><span class="sxs-lookup"><span data-stu-id="a92d2-139">Set anonymous access for the container.</span></span>

```java
// Set anonymous access on the container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

<span data-ttu-id="a92d2-140">Получите ссылку на блочный BLOB-объект, который будет представлять BLOB-объект в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="a92d2-140">Get a reference to the block blob, which will represent the blob in Azure storage.</span></span>

```java
blob = container.getBlockBlobReference("image1.jpg");
```

<span data-ttu-id="a92d2-141">Используйте конструктор **File** , чтобы получить ссылку на локально созданный файл, который требуется отправить.</span><span class="sxs-lookup"><span data-stu-id="a92d2-141">Use the **File** constructor to get a reference to the locally created file that you will upload.</span></span> <span data-ttu-id="a92d2-142">(Перед выполнением этого кода убедитесь,что вы создали этот файл.)</span><span class="sxs-lookup"><span data-stu-id="a92d2-142">Ensure you have created this file before running the code.</span></span>

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

<span data-ttu-id="a92d2-143">Отправьте локальный файл путем вызова метода **CloudBlockBlob.upload** .</span><span class="sxs-lookup"><span data-stu-id="a92d2-143">Upload the local file through a call to the **CloudBlockBlob.upload** method.</span></span> <span data-ttu-id="a92d2-144">Первым параметром метода **CloudBlockBlob.upload** является объект **FileInputStream**, представляющий локальный файл, предназначенный для отправки в службу хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="a92d2-144">The first parameter to the **CloudBlockBlob.upload** method is a **FileInputStream** object that represents the local file that will be uploaded to Azure storage.</span></span> <span data-ttu-id="a92d2-145">Вторым параметром является размер файла в байтах.</span><span class="sxs-lookup"><span data-stu-id="a92d2-145">The second parameter is the size, in bytes, of the file.</span></span>

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

<span data-ttu-id="a92d2-146">Вызовите вспомогательную функцию с именем **MakeHTMLPage**, чтобы создать базовую страницу HTML, содержащую элемент **&lt;image&gt;** с источником в виде большого двоичного объекта, присутствующего в вашей учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="a92d2-146">Call a helper function named **MakeHTMLPage**, to make a basic HTML page that contains an **&lt;image&gt;** element with the source set to the blob that is now in your Azure storage account.</span></span> <span data-ttu-id="a92d2-147">Код для **MakeHTMLPage** описан ниже в этой статье.</span><span class="sxs-lookup"><span data-stu-id="a92d2-147">The code for **MakeHTMLPage** will be discussed later in this article.</span></span>

```java
MakeHTMLPage(container);
```

<span data-ttu-id="a92d2-148">Распечатайте сообщение о состоянии и сведения о созданной странице HTML.</span><span class="sxs-lookup"><span data-stu-id="a92d2-148">Print out a status message and information about the created HTML page.</span></span>

```java
System.out.println("Processing complete.");
System.out.println("Open index.html to see the images stored in your storage account.");
```

<span data-ttu-id="a92d2-149">Закройте блок **try**, вставив закрывающую скобку: **}**</span><span class="sxs-lookup"><span data-stu-id="a92d2-149">Close the **try** block by inserting a close bracket: **}**</span></span>

<span data-ttu-id="a92d2-150">Реализуйте обработку следующих исключений:</span><span class="sxs-lookup"><span data-stu-id="a92d2-150">Handle the following exceptions:</span></span>

* <span data-ttu-id="a92d2-151">**FileNotFoundException**: может вызываться конструктором **FileInputStream** или **FileOutputStream**.</span><span class="sxs-lookup"><span data-stu-id="a92d2-151">**FileNotFoundException**: Can be thrown by the **FileInputStream** or **FileOutputStream** constructors.</span></span>
* <span data-ttu-id="a92d2-152">**StorageException**: может вызываться клиентской библиотекой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="a92d2-152">**StorageException**: Can be thrown by the Azure client storage library.</span></span>
* <span data-ttu-id="a92d2-153">**URISyntaxException**: может вызываться методом **ListBlobItem.getUri**.</span><span class="sxs-lookup"><span data-stu-id="a92d2-153">**URISyntaxException**: Can be thrown by the **ListBlobItem.getUri** method.</span></span>
* <span data-ttu-id="a92d2-154">**Исключение**: обработка универсального исключения.</span><span class="sxs-lookup"><span data-stu-id="a92d2-154">**Exception**: Generic exception handling.</span></span>

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

<span data-ttu-id="a92d2-155">Закройте **main**, вставив закрывающую скобку: **}**</span><span class="sxs-lookup"><span data-stu-id="a92d2-155">Close **main** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="a92d2-156">Создайте метод с именем **MakeHTMLPage** для создания базовой страницы HTML.</span><span class="sxs-lookup"><span data-stu-id="a92d2-156">Create a method named **MakeHTMLPage** to create a basic HTML page.</span></span> <span data-ttu-id="a92d2-157">Этот метод содержит параметр типа **CloudBlobContainer**, который будет использоваться для выполнения итерации по списку отправленных BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="a92d2-157">This method has a parameter of type **CloudBlobContainer**, which will be used to iterate through the list of uploaded blobs.</span></span> <span data-ttu-id="a92d2-158">Данный метод вызовет исключения типа **FileNotFoundException**, которые могут быть обусловлены конструктором **FileOutputStream**, и типа **URISyntaxException**, которые могут быть обусловлены методом **ListBlobItem.getUri**.</span><span class="sxs-lookup"><span data-stu-id="a92d2-158">This method will throw exceptions of type **FileNotFoundException**, which can be thrown by the **FileOutputStream** constructor, and **URISyntaxException**, which can be thrown by the **ListBlobItem.getUri** method.</span></span> <span data-ttu-id="a92d2-159">Вставьте открывающую скобку **{**.</span><span class="sxs-lookup"><span data-stu-id="a92d2-159">Include the opening bracket, **{**.</span></span>

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

<span data-ttu-id="a92d2-160">Создайте локальный файл с именем **index.html**.</span><span class="sxs-lookup"><span data-stu-id="a92d2-160">Create a local file named **index.html**.</span></span>

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

<span data-ttu-id="a92d2-161">Выполните запись в локальный файл, добавив элементы **&lt;html&gt;**, **&lt;header&gt;** и **&lt;body&gt;**.</span><span class="sxs-lookup"><span data-stu-id="a92d2-161">Write to the local file, adding in the **&lt;html&gt;**, **&lt;header&gt;**, and **&lt;body&gt;** elements.</span></span>

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

<span data-ttu-id="a92d2-162">Выполните итерацию по списку отправленных BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="a92d2-162">Iterate through the list of uploaded blobs.</span></span> <span data-ttu-id="a92d2-163">Для каждого большого двоичного объекта на странице HTML создайте элемент **&lt;img&gt;**, атрибут **src** которого отправляется в URI большого двоичного объекта в том виде, в котором он существует в вашей учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="a92d2-163">For each blob, in the HTML page create an **&lt;img&gt;** element that has its **src** attribute sent to the URI of the blob as it exists in your Azure storage account.</span></span>
<span data-ttu-id="a92d2-164">Хотя в этот пример было добавлено всего одно изображение, при добавлении нескольких изображений код будет выполнять итерации по всем изображениям.</span><span class="sxs-lookup"><span data-stu-id="a92d2-164">Although you added only one image in this sample, if you added more, this code would iterate all of them.</span></span>

<span data-ttu-id="a92d2-165">Для простоты в этом примере предполагается, что каждый отправленный BLOB-объект является изображением.</span><span class="sxs-lookup"><span data-stu-id="a92d2-165">For simplicity, this example assumes each uploaded blob is an image.</span></span> <span data-ttu-id="a92d2-166">Если вы обновили большие двоичные объекты, отличные от изображений или которые являются страницами больших двоичных объектов, а не блоками больших двоичных объектов, скорректируйте код соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="a92d2-166">If you've updated blobs other than images, or page blobs instead of block blobs, adjust the code as needed.</span></span>

```java
// Enumerate the uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in the HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

<span data-ttu-id="a92d2-167">Закройте элементы **&lt;body&gt;** и **&lt;html&gt;**.</span><span class="sxs-lookup"><span data-stu-id="a92d2-167">Close the **&lt;body&gt;** element and the **&lt;html&gt;** element.</span></span>

```java
stream.println("</body>");
stream.println("</html>");
```

<span data-ttu-id="a92d2-168">Закройте локальный файл.</span><span class="sxs-lookup"><span data-stu-id="a92d2-168">Close the local file.</span></span>

```java
stream.close();
```

<span data-ttu-id="a92d2-169">Закройте **MakeHTMLPage**, вставив закрывающую скобку: **}**</span><span class="sxs-lookup"><span data-stu-id="a92d2-169">Close **MakeHTMLPage** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="a92d2-170">Закройте **StorageSample**, вставив закрывающую скобку: **}**</span><span class="sxs-lookup"><span data-stu-id="a92d2-170">Close **StorageSample** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="a92d2-171">Ниже приведен полный код для этого примера.</span><span class="sxs-lookup"><span data-stu-id="a92d2-171">The following is the complete code for this example.</span></span> <span data-ttu-id="a92d2-172">Не забудьте заменить значения заполнителей **your\_account\_name** и **your\_account\_key** именем и ключом своей учетной записи соответственно.</span><span class="sxs-lookup"><span data-stu-id="a92d2-172">Remember to modify the placeholder values **your\_account\_name** and **your\_account\_key** to use your account name and account key, respectively.</span></span>

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

<span data-ttu-id="a92d2-173">Кроме отправки локального файла изображения в хранилище Azure, в этом примере кода создается локальный файл с именем index.html, который можно открыть в браузере для просмотра отправленного изображения.</span><span class="sxs-lookup"><span data-stu-id="a92d2-173">In addition to uploading your local image file to Azure storage, the example code creates a local file namedindex.html, which you can open in your browser to see your uploaded image.</span></span>

<span data-ttu-id="a92d2-174">Поскольку код содержит имя учетной записи и ключ учетной записи, обеспечьте безопасность исходного кода.</span><span class="sxs-lookup"><span data-stu-id="a92d2-174">Because the code contains your account name and account key, ensure that your source code is secure.</span></span>

## <a name="to-delete-a-container"></a><span data-ttu-id="a92d2-175">Удаление контейнера</span><span class="sxs-lookup"><span data-stu-id="a92d2-175">To delete a container</span></span>
<span data-ttu-id="a92d2-176">Поскольку за использование хранилища начисляется плата, вам может потребоваться удалить контейнер **gettingstarted** после окончания работы с данным примером.</span><span class="sxs-lookup"><span data-stu-id="a92d2-176">Because you are charged for storage, you may want to delete the **gettingstarted** container after you are done experimenting with this example.</span></span> <span data-ttu-id="a92d2-177">Чтобы удалить контейнер, используйте метод **CloudBlobContainer.delete** .</span><span class="sxs-lookup"><span data-stu-id="a92d2-177">To delete a container, use the **CloudBlobContainer.delete** method.</span></span>

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

<span data-ttu-id="a92d2-178">Чтобы вызвать метод **CloudBlobContainer.delete**, необходимо выполнить процесс инициализации объектов **CloudStorageAccount**, **ClodBlobClient** и **CloudBlobContainer**, который аналогичен приведенному процессу для метода **createIfNotExist**.</span><span class="sxs-lookup"><span data-stu-id="a92d2-178">To call the **CloudBlobContainer.delete** method, the process of initializing **CloudStorageAccount**, **ClodBlobClient**, and **CloudBlobContainer** objects is the same as shown for the **createIfNotExist** method.</span></span> <span data-ttu-id="a92d2-179">Ниже приведен полный пример удаления контейнера с именем **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="a92d2-179">The following is a complete example that deletes the container named **gettingstarted**.</span></span>

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

<span data-ttu-id="a92d2-180">Обзор других классов и методов хранилища BLOB-объектов см. в статье [Использование хранилища BLOB-объектов из Java](storage-java-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="a92d2-180">For an overview of other blob storage classes and methods, see [How to use Blob storage from Java](storage-java-how-to-use-blob-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a92d2-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a92d2-181">Next steps</span></span>
<span data-ttu-id="a92d2-182">Дополнительную информацию о выполнении более сложных задач хранения см. по указанным ссылкам.</span><span class="sxs-lookup"><span data-stu-id="a92d2-182">Follow these links to learn more about more complex storage tasks.</span></span>

* [<span data-ttu-id="a92d2-183">Пакет SDK для службы хранилища Azure для Java</span><span class="sxs-lookup"><span data-stu-id="a92d2-183">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="a92d2-184">справочнике по пакету SDK для клиента службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="a92d2-184">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="a92d2-185">API-интерфейс REST служб хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="a92d2-185">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="a92d2-186">Блог рабочей группы службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="a92d2-186">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)

