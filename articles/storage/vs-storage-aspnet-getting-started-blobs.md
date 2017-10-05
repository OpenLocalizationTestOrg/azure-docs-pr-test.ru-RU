---
title: "Приступая к работе с хранилищем BLOB-объектов Azure и подключенными службами Visual Studio (ASP.NET) | Документация Майкрософт"
description: "Как приступить к работе, используя хранилище BLOB-объектов Azure в проекте ASP.NET в Visual Studio после подключения к учетной записи хранения с помощью подключенных служб Visual Studio."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: b3497055-bef8-4c95-8567-181556b50d95
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: tarcher
ms.openlocfilehash: 8fd13efdbdd98c6d7dff1b88a6b232a08aa5a13d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="5d8a5-103">Приступая к работе с хранилищем BLOB-объектов Azure и подключенными службами Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="5d8a5-103">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="5d8a5-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="5d8a5-104">Overview</span></span>

<span data-ttu-id="5d8a5-105">Хранилище BLOB-объектов Azure — это служба, которая хранит неструктурированные данные в облаке в качестве объектов или больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-105">Azure blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="5d8a5-106">В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="5d8a5-107">Хранилище BLOB-объектов иногда также называют хранилищем объектов.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="5d8a5-108">В этом руководстве показано, как написать код ASP.NET для некоторых распространенных сценариев с использованием хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-108">This tutorial shows how to write ASP.NET code for some common scenarios using Azure blob storage.</span></span> <span data-ttu-id="5d8a5-109">В частности, здесь рассматриваются такие сценарии, как создание контейнера больших двоичных объектов, а также скачивание, получение списка, скачивание и удаление больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-109">Scenarios include creating a blob container, and uploading, listing, downloading, and deleting blobs.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="5d8a5-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5d8a5-110">Prerequisites</span></span>

* [<span data-ttu-id="5d8a5-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5d8a5-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="5d8a5-112">Учетная запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="5d8a5-112">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="5d8a5-113">Создание контроллера MVC</span><span class="sxs-lookup"><span data-stu-id="5d8a5-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="5d8a5-114">В **обозревателе решений** щелкните правой кнопкой мыши **Контроллеры** и в контекстном меню выберите **Добавить -> Контроллер**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-114">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![Добавление контроллера в приложение ASP.NET MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. <span data-ttu-id="5d8a5-116">В диалоговом окне **Добавление шаблона** выберите **Контроллер MVC5 — пустой** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-116">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Выбор типа контроллера MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. <span data-ttu-id="5d8a5-118">В диалоговом окне **Добавление контроллера** назовите контроллер *BlobsController* и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-118">On the **Add Controller** dialog, name the controller *BlobsController*, and select **Add**.</span></span>

    ![Назначение имени для контроллера MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. <span data-ttu-id="5d8a5-120">Добавьте в файл `BlobsController.cs` следующие директивы *using*:</span><span class="sxs-lookup"><span data-stu-id="5d8a5-120">Add the following *using* directives to the `BlobsController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a><span data-ttu-id="5d8a5-121">Создание контейнера BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="5d8a5-121">Create a blob container</span></span>

<span data-ttu-id="5d8a5-122">Контейнер больших двоичных объектов — это вложенная иерархия больших двоичных объектов и папок.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-122">A blob container is a nested hierarchy of blobs and folders.</span></span> <span data-ttu-id="5d8a5-123">Чтобы создать контейнер больших двоичных объектов, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="5d8a5-123">The following steps illustrate how to create a blob container:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="5d8a5-124">Прежде чем работать с кодом в этом разделе, выполните все действия, описанные в разделе [Настройка среды разработки](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="5d8a5-124">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="5d8a5-125">Откройте файл `BlobsController.cs` .</span><span class="sxs-lookup"><span data-stu-id="5d8a5-125">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="5d8a5-126">Добавьте метод **CreateBlobContainer**, который возвращает **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-126">Add a method called **CreateBlobContainer** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="5d8a5-127">В рамках метода **CreateBlobContainer** получите объект **CloudStorageAccount**, представляющий сведения об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-127">Within the **CreateBlobContainer** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="5d8a5-128">Используйте следующий код, чтобы получить строку подключения и сведения об учетной записи хранения из конфигурации службы Azure.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-128">Use the following code to get the storage connection string and storage account information from the Azure service configuration.</span></span> <span data-ttu-id="5d8a5-129">(Замените *&lt;storage-account-name>* на имя учетной записи хранения Azure, к которой осуществляется доступ.)</span><span class="sxs-lookup"><span data-stu-id="5d8a5-129">(Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="5d8a5-130">Получите объект **CloudBlobClient**, который представляет клиента службы BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-130">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="5d8a5-131">Получите объект **CloudBlobContainer**, который представляет ссылку на нужное имя контейнера больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-131">Get a **CloudBlobContainer** object that represents a reference to the desired blob container name.</span></span> <span data-ttu-id="5d8a5-132">Метод **CloudBlobClient.GetContainerReference** не выполняет запрос в отношении хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-132">The **CloudBlobClient.GetContainerReference** method does not make a request against blob storage.</span></span> <span data-ttu-id="5d8a5-133">Ссылка возвращается вне зависимости от того, существует ли контейнер больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-133">The reference is returned whether or not the blob container exists.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="5d8a5-134">Вызовите метод **CloudBlobContainer.CreateIfNotExists**, чтобы создать контейнер, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-134">Call the **CloudBlobContainer.CreateIfNotExists** method to create the container if it does not yet exist.</span></span> <span data-ttu-id="5d8a5-135">Метод **CloudBlobContainer.CreateIfNotExists** возвращает значение **true**, если контейнер не существует и если он успешно создан.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-135">The **CloudBlobContainer.CreateIfNotExists** method returns **true** if the container does not exist, and is successfully created.</span></span> <span data-ttu-id="5d8a5-136">В противном случае возвращается значение **false**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-136">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. <span data-ttu-id="5d8a5-137">Обновите **ViewBag** именем контейнера больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-137">Update the **ViewBag** with the name of the blob container.</span></span>

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. <span data-ttu-id="5d8a5-138">В **обозревателе решений** разверните папку **Представления**, щелкните правой кнопкой мыши **BLOB-объекты**, а затем в контекстном меню выберите **Добавить -> Представление**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-138">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="5d8a5-139">В диалоговом окне **Добавление представления** введите **CreateBlobContainer** для имени представления и выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-139">On the **Add View** dialog, enter **CreateBlobContainer** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="5d8a5-140">Откройте файл `CreateBlobContainer.cshtml` и измените его таким образом, чтобы он выглядел, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-140">Open `CreateBlobContainer.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="5d8a5-141">В **обозревателе решений** разверните папку **Представления -> Общие** и откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-141">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="5d8a5-142">После последней ссылки **Html.ActionLink** добавьте следующую ссылку **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="5d8a5-142">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. <span data-ttu-id="5d8a5-143">Запустите приложение и выберите **Create Blob Container** (Создать контейнер больших двоичных объектов), чтобы увидеть результаты, как на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-143">Run the application, and select **Create Blob Container** to see results similar to the following screen shot:</span></span>
  
    ![Создание контейнера больших двоичных объектов](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    <span data-ttu-id="5d8a5-145">Как упоминалось ранее, метод **CloudBlobContainer.CreateIfNotExists** возвращает значение **true**, только если контейнер не существует или же уже был создан.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-145">As mentioned previously, the **CloudBlobContainer.CreateIfNotExists** method returns **true** only when the container doesn't exist and is created.</span></span> <span data-ttu-id="5d8a5-146">Таким образом, если вы запустите приложение, когда контейнер существует, метод вернет значение **false**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-146">Therefore, if you run the app when the container exists, the method returns **false**.</span></span> <span data-ttu-id="5d8a5-147">Чтобы запустить приложение несколько раз, вам нужно удалить контейнер перед повторным запуском.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-147">To run the app multiple times, you must delete the container before running the app again.</span></span> <span data-ttu-id="5d8a5-148">Удалить контейнер можно с помощью метода **CloudBlobContainer.Delete**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-148">Deleting the container can be done via the **CloudBlobContainer.Delete** method.</span></span> <span data-ttu-id="5d8a5-149">Его также можно удалить на [портале Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) или в [обозревателе хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="5d8a5-149">You can also delete the container using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="upload-a-blob-into-a-blob-container"></a><span data-ttu-id="5d8a5-150">Отправка большого двоичного объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="5d8a5-150">Upload a blob into a blob container</span></span>

<span data-ttu-id="5d8a5-151">После того как вы создали [контейнер больших двоичных объектов](#create-a-blob-container), вы можете передать в него файлы.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-151">Once you've [created a blob container](#create-a-blob-container), you can upload files into that container.</span></span> <span data-ttu-id="5d8a5-152">В этом разделе показано, как отправить локальные файлы в контейнер больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-152">This section walks you through uploading a local file to a blob container.</span></span> <span data-ttu-id="5d8a5-153">В описанных здесь действиях предполагается, что вы уже создали контейнер больших двоичных объектов с именем *test-blob-container*.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-153">The steps assume you've created a blob container named *test-blob-container*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="5d8a5-154">Прежде чем работать с кодом в этом разделе, выполните все действия, описанные в разделе [Настройка среды разработки](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="5d8a5-154">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="5d8a5-155">Откройте файл `BlobsController.cs` .</span><span class="sxs-lookup"><span data-stu-id="5d8a5-155">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="5d8a5-156">Добавьте метод **UploadBlob**, который возвращает **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-156">Add a method called **UploadBlob** that returns an **EmptyResult**.</span></span>

    ```csharp
    public EmptyResult UploadBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="5d8a5-157">В рамках метода **CreateBlobContainer** получите объект **CloudStorageAccount**, который представляет сведения об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-157">Within the **UploadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="5d8a5-158">Используйте следующий фрагмент кода, чтобы получить строку подключения к хранилищу и сведения об учетной записи хранения из конфигурации службы Azure. (Измените *&lt;storage-account-name>* на имя учетной записи хранения Azure, к которой вы получаете доступ.)</span><span class="sxs-lookup"><span data-stu-id="5d8a5-158">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="5d8a5-159">Получите объект **CloudBlobClient**, который представляет клиента службы BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-159">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="5d8a5-160">Получите объект **CloudBlobContainer**, который представляет ссылку на имя контейнера больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-160">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="5d8a5-161">Как объяснялось ранее, служба хранилища Azure поддерживает различные типы больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-161">As explained earlier, Azure storage supports different blob types.</span></span> <span data-ttu-id="5d8a5-162">Чтобы получить ссылку на страничный BLOB-объект, используйте метод **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-162">To retrieve a reference to a page blob, call the **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="5d8a5-163">Чтобы получить ссылку на блочный BLOB-объект, используйте метод **CloudBlobContainer.GetBlockBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-163">To retrieve a reference to a block blob, call the **CloudBlobContainer.GetBlockBlobReference** method.</span></span> <span data-ttu-id="5d8a5-164">В большинстве случаев рекомендуется использовать блочные BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-164">Usually, block blob is the recommended type to use.</span></span> <span data-ttu-id="5d8a5-165">(Измените <blob-name>* на имя, которое нужно присвоить загруженному большому двоичному объекту.)</span><span class="sxs-lookup"><span data-stu-id="5d8a5-165">(Change <blob-name>* to the name you want to give the blob once uploaded.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="5d8a5-166">Получив ссылку на большой двоичный объект, вы можете отправить в него любой поток данных, используя метод **UploadFromStream** для объекта ссылки.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-166">Once you have a blob reference, you can upload any data stream to it by calling the blob reference object's **UploadFromStream** method.</span></span> <span data-ttu-id="5d8a5-167">Метод **UploadFromStream** создает большой двоичный объект, если он еще не существует, или заменяет уже существующий.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-167">The **UploadFromStream** method creates the blob if it doesn't exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="5d8a5-168">(Измените *&lt;file-to-upload>* на полный путь к файлу, который вы хотите передать.)</span><span class="sxs-lookup"><span data-stu-id="5d8a5-168">(Change *&lt;file-to-upload>* to a fully qualified path to the file you want to upload.)</span></span>

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. <span data-ttu-id="5d8a5-169">В **обозревателе решений** разверните папку **Представления**, щелкните правой кнопкой мыши **BLOB-объекты**, а затем в контекстном меню выберите **Добавить -> Представление**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-169">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="5d8a5-170">В **обозревателе решений** разверните папку **Представления -> Общие** и откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-170">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="5d8a5-171">После последней ссылки **Html.ActionLink** добавьте следующую ссылку **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="5d8a5-171">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="5d8a5-172">Запустите приложение и выберите **Передать BLOB-объект**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-172">Run the application, and select **Upload blob**.</span></span>  
  
<span data-ttu-id="5d8a5-173">Сведения о том, как получить список больших двоичных объектов в контейнере, см. в разделе [Получение списка больших двоичных объектов в контейнере](#list-the-blobs-in-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="5d8a5-173">The section - [List the blobs in a blob container](#list-the-blobs-in-a-blob-container) - illustrates how to list the blobs in a blob container.</span></span>    

## <a name="list-the-blobs-in-a-blob-container"></a><span data-ttu-id="5d8a5-174">Получение списка больших двоичных объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="5d8a5-174">List the blobs in a blob container</span></span>

<span data-ttu-id="5d8a5-175">В этом разделе вы узнаете, как получить список больших двоичных объектов в контейнере.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-175">This section illustrates how to list the blobs in a blob container.</span></span> <span data-ttu-id="5d8a5-176">Примеры кода приведены для контейнера *test-blob-container*, созданного при работе с разделом [Создание контейнера больших двоичных объектов](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="5d8a5-176">The sample code references the *test-blob-container* created in the section, [Create a blob container](#create-a-blob-container).</span></span>

> [!NOTE]
> 
> <span data-ttu-id="5d8a5-177">Прежде чем работать с кодом в этом разделе, выполните все действия, описанные в разделе [Настройка среды разработки](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="5d8a5-177">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="5d8a5-178">Откройте файл `BlobsController.cs` .</span><span class="sxs-lookup"><span data-stu-id="5d8a5-178">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="5d8a5-179">Добавьте метод **ListBlobs**, который возвращает **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-179">Add a method called **ListBlobs** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ListBlobs()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="5d8a5-180">В рамках метода **ListBlobs** получите объект **CloudStorageAccount**, который представляет сведения об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-180">Within the **ListBlobs** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="5d8a5-181">Используйте следующий фрагмент кода, чтобы получить строку подключения к хранилищу и сведения об учетной записи хранения из конфигурации службы Azure. (Измените *&lt;storage-account-name>* на имя учетной записи хранения Azure, к которой вы получаете доступ.)</span><span class="sxs-lookup"><span data-stu-id="5d8a5-181">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="5d8a5-182">Получите объект **CloudBlobClient**, который представляет клиента службы BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-182">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="5d8a5-183">Получите объект **CloudBlobContainer**, который представляет ссылку на имя контейнера больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-183">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="5d8a5-184">Чтобы получить список больших двоичных объектов в контейнере, используйте метод **CloudBlobContainer.ListBlobs**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-184">To list the blobs in a blob container, use the **CloudBlobContainer.ListBlobs** method.</span></span> <span data-ttu-id="5d8a5-185">Метод **CloudBlobContainer.ListBlobs** возвращает объект **IListBlobItem**, который вы можете преобразовать в **CloudBlockBlob**, **CloudPageBlob** или объект **CloudBlobDirectory**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-185">The **CloudBlobContainer.ListBlobs** method returns an **IListBlobItem** object that you cast to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="5d8a5-186">В следующем фрагменте кода перечисляются все большие двоичные объекты в контейнере.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-186">The following code snippet enumerates all the blobs in a blob container.</span></span> <span data-ttu-id="5d8a5-187">Каждый большой двоичный объект преобразовывается в соответствующий объект в зависимости от его типа, и в список добавляется его имя (или универсальный код ресурса (URI), если это объект **CloudBlobDirectory**).</span><span class="sxs-lookup"><span data-stu-id="5d8a5-187">Each blob is cast to the appropriate object based on its type, and its name (or URI in the case of a **CloudBlobDirectory**) is added to a list.</span></span>

    ```csharp
    List<string> blobs = new List<string>();

    foreach (IListBlobItem item in container.ListBlobs(null, false))
    {
        if (item.GetType() == typeof(CloudBlockBlob))
        {
            CloudBlockBlob blob = (CloudBlockBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudPageBlob))
        {
            CloudPageBlob blob = (CloudPageBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudBlobDirectory))
        {
            CloudBlobDirectory dir = (CloudBlobDirectory)item;
            blobs.Add(dir.Uri.ToString());
        }
    }

    return View(blobs);
    ```

    <span data-ttu-id="5d8a5-188">Помимо больших двоичных объектов контейнеры могут также содержать каталоги.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-188">In addition to blobs, blob containers can contain directories.</span></span> <span data-ttu-id="5d8a5-189">Предположим, у вас есть контейнер больших двоичных объектов с именем *test-blob-container* со следующей иерархией:</span><span class="sxs-lookup"><span data-stu-id="5d8a5-189">Let's suppose you have a blob container called *test-blob-container* with the following hierarchy:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

    <span data-ttu-id="5d8a5-190">Исходя из приведенного выше примера кода, список строк **blobs** содержит значения, аналогичные следующим:</span><span class="sxs-lookup"><span data-stu-id="5d8a5-190">Using the preceding code example, the **blobs** string list contains values similar to the following:</span></span>

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    <span data-ttu-id="5d8a5-191">Как видно, список включает сущности только верхнего уровня и не содержит вложенные сущности (*bar.png* и *baz.png*).</span><span class="sxs-lookup"><span data-stu-id="5d8a5-191">As you can see, the list includes only the top-level entities; not the nested ones (*bar.png* and *baz.png*).</span></span> <span data-ttu-id="5d8a5-192">Чтобы получить список всех сущностей, которые содержит контейнер больших двоичных объектов, нужно вызвать метод **CloudBlobContainer.ListBlobs** и установить значение **true** для параметра **useFlatBlobListing**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-192">To list all the entities within a blob container, you must call the **CloudBlobContainer.ListBlobs** method and pass **true** for the **useFlatBlobListing** parameter.</span></span>    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    <span data-ttu-id="5d8a5-193">Если установить для параметра **useFlatBlobListing** значение **true**, будет возвращен неструктурированный список всех сущностей в контейнере:</span><span class="sxs-lookup"><span data-stu-id="5d8a5-193">Setting the **useFlatBlobListing** parameter to **true** returns a flat listing of all entities in the blob container, and yields the following results:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

1. <span data-ttu-id="5d8a5-194">В **обозревателе решений** разверните папку **Представления**, щелкните правой кнопкой мыши **BLOB-объекты**, а затем в контекстном меню выберите **Добавить -> Представление**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-194">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="5d8a5-195">В диалоговом окне **Добавление представления** введите **ListBlobs** для имени представления и выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-195">On the **Add View** dialog, enter **ListBlobs** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="5d8a5-196">Откройте файл `ListBlobs.cshtml` и измените его таким образом, чтобы он выглядел, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-196">Open `ListBlobs.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```html
    @model List<string>
    @{
        ViewBag.Title = "List blobs";
    }
    
    <h2>List blobs</h2>
    
    <ul>
        @foreach (var item in Model)
        {
        <li>@item</li>
        }
    </ul>
    ```

1. <span data-ttu-id="5d8a5-197">В **обозревателе решений** разверните папку **Представления -> Общие** и откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-197">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="5d8a5-198">После последней ссылки **Html.ActionLink** добавьте следующую ссылку **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="5d8a5-198">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. <span data-ttu-id="5d8a5-199">Запустите приложение и выберите **List Blobs** (Вывод списка больших двоичных объектов	), чтобы увидеть результаты, как на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-199">Run the application, and select **List blobs** to see results similar to the following screen shot:</span></span>
  
    ![Получение списка больших двоичных объектов](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a><span data-ttu-id="5d8a5-201">Скачивание больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="5d8a5-201">Download blobs</span></span>

<span data-ttu-id="5d8a5-202">В этом разделе рассказывается, как скачать большие двоичные объекты и сохранить их в локальном хранилище или преобразовать содержимое в строку.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-202">This section illustrates how to download a blob and either persist it to local storage or read the contents into a string.</span></span> <span data-ttu-id="5d8a5-203">Примеры кода приведены для контейнера *test-blob-container*, созданного при работе с разделом [Создание контейнера больших двоичных объектов](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="5d8a5-203">The sample code references the *test-blob-container* created in the section, [Create a blob container](#create-a-blob-container).</span></span>

1. <span data-ttu-id="5d8a5-204">Откройте файл `BlobsController.cs` .</span><span class="sxs-lookup"><span data-stu-id="5d8a5-204">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="5d8a5-205">Добавьте метод **DownloadBlob**, который возвращает **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-205">Add a method called **DownloadBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="5d8a5-206">В рамках метода **DownloadBlob** получите объект **CloudStorageAccount**, который представляет сведения об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-206">Within the **DownloadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="5d8a5-207">Используйте следующий фрагмент кода, чтобы получить строку подключения к хранилищу и сведения об учетной записи хранения из конфигурации службы Azure. (Измените *&lt;storage-account-name>* на имя учетной записи хранения Azure, к которой вы получаете доступ.)</span><span class="sxs-lookup"><span data-stu-id="5d8a5-207">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="5d8a5-208">Получите объект **CloudBlobClient**, который представляет клиента службы BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-208">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="5d8a5-209">Получите объект **CloudBlobContainer**, который представляет ссылку на имя контейнера больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-209">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="5d8a5-210">Получить объект большого двоичного объекта можно, вызвав следующие методы: **CloudBlobContainer.GetBlockBlobReference** или **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-210">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="5d8a5-211">(Измените *&lt;blob-name>* на имя большого двоичного объекта, который вы скачиваете.)</span><span class="sxs-lookup"><span data-stu-id="5d8a5-211">(Change *&lt;blob-name>* to the name of the blob you are downloading.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="5d8a5-212">Чтобы скачать большой двоичный объект, используйте методы **CloudBlockBlob.DownloadToStream** или **CloudPageBlob.DownloadToStream** в зависимости от типа большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-212">To download a blob, use the **CloudBlockBlob.DownloadToStream** or **CloudPageBlob.DownloadToStream** method, depending on the blob type.</span></span> <span data-ttu-id="5d8a5-213">В следующем фрагменте кода используется метод **CloudBlockBlob.DownloadToStream**, чтобы передать содержимое большого двоичного объекта в объект потока, который затем сохраняется в локальный файл. (Измените *local-file-name>&lt;* на полное имя файла, куда будет скачан большой двоичный объект.)</span><span class="sxs-lookup"><span data-stu-id="5d8a5-213">The following code snippet uses the **CloudBlockBlob.DownloadToStream** method to transfer a blob's contents to a stream object that is then persisted to a local file: (Change *&lt;local-file-name>* to the fully qualified file name representing where you want the blob downloaded.)</span></span> 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. <span data-ttu-id="5d8a5-214">В **обозревателе решений** разверните папку **Представления -> Общие** и откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-214">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="5d8a5-215">После последней ссылки **Html.ActionLink** добавьте следующую ссылку **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="5d8a5-215">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="5d8a5-216">Запустите приложение и выберите **Скачать BLOB-объект**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-216">Run the application, and select **Download blob** to download the blob.</span></span> <span data-ttu-id="5d8a5-217">Большой двоичный объект, указанный в вызове метода **CloudBlobContainer.GetBlockBlobReference**, скачивается в расположение, которое вы указали в вызове метода **File.OpenWrite**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-217">The blob specified in the **CloudBlobContainer.GetBlockBlobReference** method call downloads to the location you specify in the **File.OpenWrite** method call.</span></span> 

## <a name="delete-blobs"></a><span data-ttu-id="5d8a5-218">Удаление blob-объектов</span><span class="sxs-lookup"><span data-stu-id="5d8a5-218">Delete blobs</span></span>

<span data-ttu-id="5d8a5-219">Чтобы удалить большой двоичный объект, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="5d8a5-219">The following steps illustrate how to delete a blob:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="5d8a5-220">Прежде чем работать с кодом в этом разделе, выполните все действия, описанные в разделе [Настройка среды разработки](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="5d8a5-220">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="5d8a5-221">Откройте файл `BlobsController.cs` .</span><span class="sxs-lookup"><span data-stu-id="5d8a5-221">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="5d8a5-222">Добавьте метод **DeleteBlob**, который возвращает **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-222">Add a method called **DeleteBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```

1. <span data-ttu-id="5d8a5-223">Получите объект **CloudStorageAccount** , представляющий данные учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-223">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="5d8a5-224">Используйте следующий фрагмент кода, чтобы получить строку подключения к хранилищу и сведения об учетной записи хранения из конфигурации службы Azure. (Измените *&lt;storage-account-name>* на имя учетной записи хранения Azure, к которой вы получаете доступ.)</span><span class="sxs-lookup"><span data-stu-id="5d8a5-224">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="5d8a5-225">Получите объект **CloudBlobClient**, который представляет клиента службы BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-225">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="5d8a5-226">Получите объект **CloudBlobContainer**, который представляет ссылку на имя контейнера больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-226">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="5d8a5-227">Получить объект большого двоичного объекта можно, вызвав следующие методы: **CloudBlobContainer.GetBlockBlobReference** или **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-227">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="5d8a5-228">(Измените *&lt;blob-name>* на имя большого двоичного объекта, который вы удаляете.)</span><span class="sxs-lookup"><span data-stu-id="5d8a5-228">(Change *&lt;blob-name>* to the name of the blob you are deleting.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. To delete a blob, use the **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. <span data-ttu-id="5d8a5-229">В **обозревателе решений** разверните папку **Представления -> Общие** и откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-229">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="5d8a5-230">После последней ссылки **Html.ActionLink** добавьте следующую ссылку **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="5d8a5-230">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="5d8a5-231">Запустите приложение и выберите **Удалить большой двоичный объект**, чтобы удалить объект, указанный в вызове метода **CloudBlobContainer.GetBlockBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-231">Run the application, and select **Delete blob** to delete the blob specified in the **CloudBlobContainer.GetBlockBlobReference** method call.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5d8a5-232">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5d8a5-232">Next steps</span></span>
<span data-ttu-id="5d8a5-233">Просмотрите дополнительные руководства, чтобы изучить дополнительные возможности хранения данных в Azure.</span><span class="sxs-lookup"><span data-stu-id="5d8a5-233">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="5d8a5-234">Начало работы с хранилищем таблиц Azure и подключенными службами Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="5d8a5-234">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-tables.md)
  * [<span data-ttu-id="5d8a5-235">Начало работы с хранилищем очередей Azure и подключенными службами Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5d8a5-235">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-queues.md)
