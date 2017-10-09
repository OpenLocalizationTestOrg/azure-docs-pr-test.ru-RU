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
# <a name="on-premises-application-with-blob-storage"></a><span data-ttu-id="be1f9-104">Локальное приложение с хранилищем больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="be1f9-104">On-premises application with blob storage</span></span>
## <a name="overview"></a><span data-ttu-id="be1f9-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="be1f9-105">Overview</span></span>
<span data-ttu-id="be1f9-106">Hello пример при использовании хранилища Azure для хранения изображений в Azure.</span><span class="sxs-lookup"><span data-stu-id="be1f9-106">hello following example shows you how you can use Azure storage to store images in Azure.</span></span> <span data-ttu-id="be1f9-107">Hello в этой статье приведен для консольное приложение, которое передает tooAzure образа, а затем создает HTML-файл, которое отображает hello изображения в браузере.</span><span class="sxs-lookup"><span data-stu-id="be1f9-107">hello code in this article is for a console application that uploads an image tooAzure, and then creates an HTML file that displays hello image in your browser.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be1f9-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="be1f9-108">Prerequisites</span></span>
* <span data-ttu-id="be1f9-109">Установленный пакет Java Developer Kit (JDK) версии 1.6 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="be1f9-109">A Java Developer Kit (JDK), version 1.6 or later, is installed.</span></span>
* <span data-ttu-id="be1f9-110">Hello Azure SDK установлен.</span><span class="sxs-lookup"><span data-stu-id="be1f9-110">hello Azure SDK is installed.</span></span>
* <span data-ttu-id="be1f9-111">Hello JAR hello библиотек Azure для Java и JAR-файлов любые применимые зависимостей, установлены и находятся в пути сборки hello, используемые компилятором Java.</span><span class="sxs-lookup"><span data-stu-id="be1f9-111">hello JAR for hello Azure Libraries for Java, and any applicable dependency JARs, are installed and are in hello build path used by your Java compiler.</span></span> <span data-ttu-id="be1f9-112">Сведения об установке hello библиотек Azure для Java см. в разделе [hello загрузки пакета Azure SDK для Java](../java-download-azure-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="be1f9-112">For information about installing hello Azure Libraries for Java, see [Download hello Azure SDK for Java](../java-download-azure-sdk.md).</span></span>
* <span data-ttu-id="be1f9-113">Настроенная учетная запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="be1f9-113">An Azure storage account has been set up.</span></span> <span data-ttu-id="be1f9-114">Hello имя учетной записи и ключ учетной записи хранилища hello будет использоваться кода hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="be1f9-114">hello account name and account key for hello storage account will be used by hello code in this article.</span></span> <span data-ttu-id="be1f9-115">В разделе [как tooCreate учетной записи хранилища](storage-create-storage-account.md#create-a-storage-account) сведения о создании учетной записи хранилища и [представление и скопируйте ключи доступа к хранилищу](storage-create-storage-account.md#view-and-copy-storage-access-keys) сведения о получении ключа учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="be1f9-115">See [How tooCreate a Storage Account](storage-create-storage-account.md#create-a-storage-account) for information about creating a storage account, and [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys) for information about retrieving hello account key.</span></span>
* <span data-ttu-id="be1f9-116">Созданный файл с именем локального изображения хранятся на hello path c:\\myimages\\image1.jpg.</span><span class="sxs-lookup"><span data-stu-id="be1f9-116">You have created a local image file named stored at hello path c:\\myimages\\image1.jpg.</span></span> <span data-ttu-id="be1f9-117">Кроме того, изменить **FileInputStream** конструктор в примере hello toouse другое изображение путь и имя файла.</span><span class="sxs-lookup"><span data-stu-id="be1f9-117">Alternatively, modify the **FileInputStream** constructor in hello example toouse a different image path and file name.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="toouse-azure-blob-storage-tooupload-a-file"></a><span data-ttu-id="be1f9-118">tooupload хранилища BLOB-объектов Azure toouse файла</span><span class="sxs-lookup"><span data-stu-id="be1f9-118">toouse Azure blob storage tooupload a file</span></span>
<span data-ttu-id="be1f9-119">В этом разделе описывается пошаговая процедура.</span><span class="sxs-lookup"><span data-stu-id="be1f9-119">A step-by-step procedure is presented here.</span></span> <span data-ttu-id="be1f9-120">Если вы хотите tooskip вперед, далее в этой статье представлены hello весь код.</span><span class="sxs-lookup"><span data-stu-id="be1f9-120">If you'd like tooskip ahead, hello entire code is presented later in this article.</span></span>

<span data-ttu-id="be1f9-121">Начать кода hello, включая Импорт для классы хранения Azure core hello, hello BLOB-объектов Azure клиентские классы, классы ввода-ВЫВОДА Java hello и hello **URISyntaxException** класса.</span><span class="sxs-lookup"><span data-stu-id="be1f9-121">Begin hello code by including imports for hello Azure core storage classes, hello Azure blob client classes, hello Java IO classes, and hello **URISyntaxException** class.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

<span data-ttu-id="be1f9-122">Объявите класс с именем **StorageSample**и включать hello открывающей скобки, **{**.</span><span class="sxs-lookup"><span data-stu-id="be1f9-122">Declare a class named **StorageSample**, and include hello open bracket, **{**.</span></span>

```java
public class StorageSample {
```

<span data-ttu-id="be1f9-123">В рамках hello **StorageSample** объявите строковую переменную, которая будет содержать протокол конечной точки по умолчанию hello, имя учетной записи хранилища и ключи доступа к хранилищу, как указано в вашей учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="be1f9-123">Within hello **StorageSample** class, declare a string variable that will contain hello default endpoint protocol, your storage account name, and your storage access key, as specified in your Azure storage account.</span></span> <span data-ttu-id="be1f9-124">Замените значения заполнителей hello **вашей\_учетной записи\_имя** и **вашей\_учетной записи\_ключ** имя учетной записи и ключ учетной записи соответственно.</span><span class="sxs-lookup"><span data-stu-id="be1f9-124">Replace hello placeholder values **your\_account\_name** and **your\_account\_key** with your own account name and account key, respectively.</span></span>

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

<span data-ttu-id="be1f9-125">Добавьте в объявление для **основной**, включают **повторите** блокировку и включить необходимые открывающими скобками hello, **{**.</span><span class="sxs-lookup"><span data-stu-id="be1f9-125">Add in your declaration for **main**, include a **try** block, and include hello necessary open brackets, **{**.</span></span>

```java
    public static void main(String[] args)
    {
        try
        {
```

<span data-ttu-id="be1f9-126">Объявления переменных hello после типа (приветствия, описание их использования в этом примере):</span><span class="sxs-lookup"><span data-stu-id="be1f9-126">Declare variables of hello following type (hello descriptions are for how they are used in this example):</span></span>

* <span data-ttu-id="be1f9-127">**CloudStorageAccount**: hello tooinitialize используется объект учетной записи с именем учетной записи хранилища Azure и ключ и toocreate большой двоичный объект клиента.</span><span class="sxs-lookup"><span data-stu-id="be1f9-127">**CloudStorageAccount**: Used tooinitialize hello account object with your Azure storage account name and key, and toocreate the blob client object.</span></span>
* <span data-ttu-id="be1f9-128">**CloudBlobClient**: использовать службы BLOB-объектов tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="be1f9-128">**CloudBlobClient**: Used tooaccess hello blob service.</span></span>
* <span data-ttu-id="be1f9-129">**CloudBlobContainer**: используется toocreate контейнер больших двоичных объектов перечисление BLOB-объектов в контейнере hello и удаления контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="be1f9-129">**CloudBlobContainer**: Used toocreate a blob container, list the blobs in hello container, and delete hello container.</span></span>
* <span data-ttu-id="be1f9-130">**CloudBlockBlob**: используется tooupload контейнер toothe образ в локальный файл.</span><span class="sxs-lookup"><span data-stu-id="be1f9-130">**CloudBlockBlob**: Used tooupload a local image file toothe container.</span></span>

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

<span data-ttu-id="be1f9-131">Назначьте toohello значение **учетной записи** переменной.</span><span class="sxs-lookup"><span data-stu-id="be1f9-131">Assign a value toohello **account** variable.</span></span>

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

<span data-ttu-id="be1f9-132">Назначьте toohello значение **serviceClient** переменной.</span><span class="sxs-lookup"><span data-stu-id="be1f9-132">Assign a value toohello **serviceClient** variable.</span></span>

```java
serviceClient = account.createCloudBlobClient();
```

<span data-ttu-id="be1f9-133">Назначьте toohello значение **контейнера** переменной.</span><span class="sxs-lookup"><span data-stu-id="be1f9-133">Assign a value toohello **container** variable.</span></span> <span data-ttu-id="be1f9-134">Мы получаем ссылки tooa контейнер **Приступая к работе**.</span><span class="sxs-lookup"><span data-stu-id="be1f9-134">We'll get a reference tooa container named **gettingstarted**.</span></span>

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

<span data-ttu-id="be1f9-135">Создание контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="be1f9-135">Create hello container.</span></span> <span data-ttu-id="be1f9-136">Если он не существует, этот метод создаст контейнер hello (и возвращают **true**).</span><span class="sxs-lookup"><span data-stu-id="be1f9-136">This method will create hello container if it doesn't exist (and return **true**).</span></span> <span data-ttu-id="be1f9-137">Если hello контейнер существует, он будет возвращать **false**.</span><span class="sxs-lookup"><span data-stu-id="be1f9-137">If hello container does exist, it will return **false**.</span></span> <span data-ttu-id="be1f9-138">Альтернативы слишком**createIfNotExists** — hello **создания** метод (которая будет возвращена ошибка, если контейнер hello уже существует).</span><span class="sxs-lookup"><span data-stu-id="be1f9-138">An alternative too**createIfNotExists** is hello **create** method (which will return an error if hello container already exists).</span></span>

```java
container.createIfNotExists();
```

<span data-ttu-id="be1f9-139">Задать анонимного доступа для контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="be1f9-139">Set anonymous access for hello container.</span></span>

```java
// Set anonymous access on hello container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

<span data-ttu-id="be1f9-140">Получите ссылку toohello большого двоичного объекта, который будет представлять hello BLOB-объектов в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="be1f9-140">Get a reference toohello block blob, which will represent hello blob in Azure storage.</span></span>

```java
blob = container.getBlockBlobReference("image1.jpg");
```

<span data-ttu-id="be1f9-141">Используйте hello **файл** конструктор tooget toohello локально созданные ссылочного файла, который будет передан.</span><span class="sxs-lookup"><span data-stu-id="be1f9-141">Use hello **File** constructor tooget a reference toohello locally created file that you will upload.</span></span> <span data-ttu-id="be1f9-142">Убедитесь, что вы создали этот файл перед запуском кода hello.</span><span class="sxs-lookup"><span data-stu-id="be1f9-142">Ensure you have created this file before running hello code.</span></span>

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

<span data-ttu-id="be1f9-143">Hello локального компьютера файл через toohello вызов **CloudBlockBlob.upload** метод.</span><span class="sxs-lookup"><span data-stu-id="be1f9-143">Upload hello local file through a call toohello **CloudBlockBlob.upload** method.</span></span> <span data-ttu-id="be1f9-144">Здравствуйте, первый параметр toohello **CloudBlockBlob.upload** метод **FileInputStream** объекта, представляет hello локальный файл, будут отправлены tooAzure хранилища.</span><span class="sxs-lookup"><span data-stu-id="be1f9-144">hello first parameter toohello **CloudBlockBlob.upload** method is a **FileInputStream** object that represents hello local file that will be uploaded tooAzure storage.</span></span> <span data-ttu-id="be1f9-145">Второй параметр Hello — hello размер файла в байтах, hello.</span><span class="sxs-lookup"><span data-stu-id="be1f9-145">hello second parameter is hello size, in bytes, of hello file.</span></span>

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

<span data-ttu-id="be1f9-146">Вызовите вспомогательную функцию с именем **MakeHTMLPage**, страница toomake простой HTML-документ, содержащий  **&lt;изображения&gt;**  элемент с hello исходного набора toohello большого двоичного объекта, работающего в Azure Учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="be1f9-146">Call a helper function named **MakeHTMLPage**, toomake a basic HTML page that contains an **&lt;image&gt;** element with hello source set toohello blob that is now in your Azure storage account.</span></span> <span data-ttu-id="be1f9-147">Здравствуйте, код для **MakeHTMLPage** обсуждаются далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="be1f9-147">hello code for **MakeHTMLPage** will be discussed later in this article.</span></span>

```java
MakeHTMLPage(container);
```

<span data-ttu-id="be1f9-148">Выводит сообщения о состоянии и сведения о hello, создаваемую страницу HTML.</span><span class="sxs-lookup"><span data-stu-id="be1f9-148">Print out a status message and information about hello created HTML page.</span></span>

```java
System.out.println("Processing complete.");
System.out.println("Open index.html toosee hello images stored in your storage account.");
```

<span data-ttu-id="be1f9-149">Закрыть hello **повторите** блока, вставив закрывающая квадратная скобка: **}**</span><span class="sxs-lookup"><span data-stu-id="be1f9-149">Close hello **try** block by inserting a close bracket: **}**</span></span>

<span data-ttu-id="be1f9-150">Дескриптор hello следующие исключения:</span><span class="sxs-lookup"><span data-stu-id="be1f9-150">Handle hello following exceptions:</span></span>

* <span data-ttu-id="be1f9-151">**FileNotFoundException**: могут создаваться инфраструктурой hello **FileInputStream** или **FileOutputStream** конструкторы.</span><span class="sxs-lookup"><span data-stu-id="be1f9-151">**FileNotFoundException**: Can be thrown by hello **FileInputStream** or **FileOutputStream** constructors.</span></span>
* <span data-ttu-id="be1f9-152">**StorageException**: создаваемые библиотекой хранилища Azure клиента hello.</span><span class="sxs-lookup"><span data-stu-id="be1f9-152">**StorageException**: Can be thrown by hello Azure client storage library.</span></span>
* <span data-ttu-id="be1f9-153">**URISyntaxException**: могут создаваться инфраструктурой hello **ListBlobItem.getUri** метод.</span><span class="sxs-lookup"><span data-stu-id="be1f9-153">**URISyntaxException**: Can be thrown by hello **ListBlobItem.getUri** method.</span></span>
* <span data-ttu-id="be1f9-154">**Исключение**: обработка универсального исключения.</span><span class="sxs-lookup"><span data-stu-id="be1f9-154">**Exception**: Generic exception handling.</span></span>

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

<span data-ttu-id="be1f9-155">Закройте **main**, вставив закрывающую скобку: **}**</span><span class="sxs-lookup"><span data-stu-id="be1f9-155">Close **main** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="be1f9-156">Создайте метод с именем **MakeHTMLPage** toocreate основные HTML-страницы.</span><span class="sxs-lookup"><span data-stu-id="be1f9-156">Create a method named **MakeHTMLPage** toocreate a basic HTML page.</span></span> <span data-ttu-id="be1f9-157">Этот метод имеет параметр типа **CloudBlobContainer**, которое будет используется tooiterate через список hello отправленного больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="be1f9-157">This method has a parameter of type **CloudBlobContainer**, which will be used tooiterate through hello list of uploaded blobs.</span></span> <span data-ttu-id="be1f9-158">Этот метод будет выдавать исключения типа **FileNotFoundException**, которой могут создаваться инфраструктурой hello **FileOutputStream** конструктор, и **URISyntaxException**, которого можно вызывается hello **ListBlobItem.getUri** метод.</span><span class="sxs-lookup"><span data-stu-id="be1f9-158">This method will throw exceptions of type **FileNotFoundException**, which can be thrown by hello **FileOutputStream** constructor, and **URISyntaxException**, which can be thrown by hello **ListBlobItem.getUri** method.</span></span> <span data-ttu-id="be1f9-159">Вставьте открывающую скобку **{**.</span><span class="sxs-lookup"><span data-stu-id="be1f9-159">Include the opening bracket, **{**.</span></span>

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

<span data-ttu-id="be1f9-160">Создайте локальный файл с именем **index.html**.</span><span class="sxs-lookup"><span data-stu-id="be1f9-160">Create a local file named **index.html**.</span></span>

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

<span data-ttu-id="be1f9-161">Записи toohello локального файла, добавление в hello  **&lt;html&gt;**,  **&lt;заголовок&gt;**, и  **&lt;текст&gt;**  элементов.</span><span class="sxs-lookup"><span data-stu-id="be1f9-161">Write toohello local file, adding in hello **&lt;html&gt;**, **&lt;header&gt;**, and **&lt;body&gt;** elements.</span></span>

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

<span data-ttu-id="be1f9-162">Итерации списка hello загруженного BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="be1f9-162">Iterate through hello list of uploaded blobs.</span></span> <span data-ttu-id="be1f9-163">Для каждого большого двоичного объекта hello HTML странице, создайте  **&lt;img&gt;**  элемент, имеющий его **src** атрибут, отправляемые hello URI большого двоичного объекта hello, которое существовало в вашей учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="be1f9-163">For each blob, in hello HTML page create an **&lt;img&gt;** element that has its **src** attribute sent to hello URI of hello blob as it exists in your Azure storage account.</span></span>
<span data-ttu-id="be1f9-164">Хотя в этот пример было добавлено всего одно изображение, при добавлении нескольких изображений код будет выполнять итерации по всем изображениям.</span><span class="sxs-lookup"><span data-stu-id="be1f9-164">Although you added only one image in this sample, if you added more, this code would iterate all of them.</span></span>

<span data-ttu-id="be1f9-165">Для простоты в этом примере предполагается, что каждый отправленный BLOB-объект является изображением.</span><span class="sxs-lookup"><span data-stu-id="be1f9-165">For simplicity, this example assumes each uploaded blob is an image.</span></span> <span data-ttu-id="be1f9-166">Если вы обновили больших двоичных объектов, кроме изображений или страничных больших двоичных объектов вместо блочных больших двоичных объектов, настройте код hello при необходимости.</span><span class="sxs-lookup"><span data-stu-id="be1f9-166">If you've updated blobs other than images, or page blobs instead of block blobs, adjust hello code as needed.</span></span>

```java
// Enumerate hello uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in hello HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

<span data-ttu-id="be1f9-167">Закрыть hello  **&lt;текст&gt;**  элемент и hello  **&lt;html&gt;**  элемента.</span><span class="sxs-lookup"><span data-stu-id="be1f9-167">Close hello **&lt;body&gt;** element and hello **&lt;html&gt;** element.</span></span>

```java
stream.println("</body>");
stream.println("</html>");
```

<span data-ttu-id="be1f9-168">Закрыть hello в локальный файл.</span><span class="sxs-lookup"><span data-stu-id="be1f9-168">Close hello local file.</span></span>

```java
stream.close();
```

<span data-ttu-id="be1f9-169">Закройте **MakeHTMLPage**, вставив закрывающую скобку: **}**</span><span class="sxs-lookup"><span data-stu-id="be1f9-169">Close **MakeHTMLPage** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="be1f9-170">Закройте **StorageSample**, вставив закрывающую скобку: **}**</span><span class="sxs-lookup"><span data-stu-id="be1f9-170">Close **StorageSample** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="be1f9-171">Hello ниже приведен полный код этого примера hello.</span><span class="sxs-lookup"><span data-stu-id="be1f9-171">hello following is hello complete code for this example.</span></span> <span data-ttu-id="be1f9-172">Запомнить значения заполнителей hello toomodify **вашей\_учетной записи\_имя** и **вашей\_учетной записи\_ключ** toouse имя учетной записи и учетной записи ключ, соответственно.</span><span class="sxs-lookup"><span data-stu-id="be1f9-172">Remember toomodify hello placeholder values **your\_account\_name** and **your\_account\_key** toouse your account name and account key, respectively.</span></span>

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

<span data-ttu-id="be1f9-173">В дополнение toouploading файл tooAzure хранилище локального изображения, hello пример кода создает namedindex.html локальный файл, который можно открыть в ваш браузер toosee загруженного образа.</span><span class="sxs-lookup"><span data-stu-id="be1f9-173">In addition toouploading your local image file tooAzure storage, hello example code creates a local file namedindex.html, which you can open in your browser toosee your uploaded image.</span></span>

<span data-ttu-id="be1f9-174">Так как код hello содержит имя учетной записи и ключ учетной записи, гарантирует исходный код безопасности.</span><span class="sxs-lookup"><span data-stu-id="be1f9-174">Because hello code contains your account name and account key, ensure that your source code is secure.</span></span>

## <a name="toodelete-a-container"></a><span data-ttu-id="be1f9-175">toodelete контейнера</span><span class="sxs-lookup"><span data-stu-id="be1f9-175">toodelete a container</span></span>
<span data-ttu-id="be1f9-176">Поскольку плата взимается для хранения данных, возможно, стоит toodelete **Приступая к работе** контейнер после выполнения экспериментов с этим примером.</span><span class="sxs-lookup"><span data-stu-id="be1f9-176">Because you are charged for storage, you may want toodelete the **gettingstarted** container after you are done experimenting with this example.</span></span> <span data-ttu-id="be1f9-177">toodelete является контейнером, используйте hello **CloudBlobContainer.delete** метод.</span><span class="sxs-lookup"><span data-stu-id="be1f9-177">toodelete a container, use hello **CloudBlobContainer.delete** method.</span></span>

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

<span data-ttu-id="be1f9-178">toocall hello **CloudBlobContainer.delete** метод, процесс инициализации hello **CloudStorageAccount**, **ClodBlobClient**, и  **CloudBlobContainer** объектов Здравствуйте, так же, как показано для **createIfNotExist** метод.</span><span class="sxs-lookup"><span data-stu-id="be1f9-178">toocall hello **CloudBlobContainer.delete** method, hello process of initializing **CloudStorageAccount**, **ClodBlobClient**, and **CloudBlobContainer** objects is hello same as shown for the **createIfNotExist** method.</span></span> <span data-ttu-id="be1f9-179">Hello ниже приведен полный пример, что операции удаления hello контейнер с именем **Приступая к работе**.</span><span class="sxs-lookup"><span data-stu-id="be1f9-179">hello following is a complete example that deletes hello container named **gettingstarted**.</span></span>

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

<span data-ttu-id="be1f9-180">Обзор другие классы хранения больших двоичных объектов и методов см. в разделе [как хранилище больших двоичных объектов из Java toouse](storage-java-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="be1f9-180">For an overview of other blob storage classes and methods, see [How toouse Blob storage from Java](storage-java-how-to-use-blob-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="be1f9-181">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="be1f9-181">Next steps</span></span>
<span data-ttu-id="be1f9-182">Выполните эти дополнительные сведения о более сложных задач хранилища toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="be1f9-182">Follow these links toolearn more about more complex storage tasks.</span></span>

* [<span data-ttu-id="be1f9-183">Пакет SDK для службы хранилища Azure для Java</span><span class="sxs-lookup"><span data-stu-id="be1f9-183">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="be1f9-184">справочнике по пакету SDK для клиента службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="be1f9-184">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="be1f9-185">API-интерфейс REST служб хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="be1f9-185">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="be1f9-186">Блог рабочей группы службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="be1f9-186">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)

