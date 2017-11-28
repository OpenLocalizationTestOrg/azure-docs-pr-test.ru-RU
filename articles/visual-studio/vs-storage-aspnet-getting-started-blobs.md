---
title: "aaaGet работы с BLOB-объектов Azure и Visual Studio подключения службы (ASP.NET) | Документы Microsoft"
description: "Как tooget запущена с помощью хранилища BLOB-объектов Azure в проект ASP.NET в Visual Studio после подключения tooa учетной записи хранилища с помощью Visual Studio подключенные службы"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: b3497055-bef8-4c95-8567-181556b50d95
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: kraig
ms.openlocfilehash: 7b3e160da5bb95967ca4650b124afb8e867c03d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="2a017-103">Приступая к работе с хранилищем BLOB-объектов Azure и подключенными службами Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="2a017-103">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="2a017-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="2a017-104">Overview</span></span>

<span data-ttu-id="2a017-105">Хранилище больших двоичных объектов — это служба, неструктурированные данные хранятся в облаке hello как большие двоичные объекты и объекты.</span><span class="sxs-lookup"><span data-stu-id="2a017-105">Azure blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="2a017-106">В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений.</span><span class="sxs-lookup"><span data-stu-id="2a017-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="2a017-107">Хранилище больших двоичных объектов также является ссылка tooas объекта хранилища.</span><span class="sxs-lookup"><span data-stu-id="2a017-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="2a017-108">В этом учебнике показано, как toowrite ASP.NET кода в некоторых распространенных сценариях, с помощью хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="2a017-108">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure blob storage.</span></span> <span data-ttu-id="2a017-109">В частности, здесь рассматриваются такие сценарии, как создание контейнера больших двоичных объектов, а также скачивание, получение списка, скачивание и удаление больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="2a017-109">Scenarios include creating a blob container, and uploading, listing, downloading, and deleting blobs.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="2a017-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2a017-110">Prerequisites</span></span>

* [<span data-ttu-id="2a017-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2a017-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="2a017-112">Учетная запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="2a017-112">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="2a017-113">Создание контроллера MVC</span><span class="sxs-lookup"><span data-stu-id="2a017-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="2a017-114">В hello **обозревателе решений**, щелкните правой кнопкой мыши **контроллеров**и в контекстном меню hello, выберите **Добавить -> контроллер**.</span><span class="sxs-lookup"><span data-stu-id="2a017-114">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Добавление контроллера tooan приложение ASP.NET MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. <span data-ttu-id="2a017-116">На hello **Добавление формирования шаблонов** диалогового окна выберите **контроллер MVC 5 - пустой**и выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="2a017-116">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Выбор типа контроллера MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. <span data-ttu-id="2a017-118">На hello **добавления контроллера** диалогового окна, имя контроллера hello *BlobsController*и выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="2a017-118">On hello **Add Controller** dialog, name hello controller *BlobsController*, and select **Add**.</span></span>

    ![Имя контроллера MVC hello](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. <span data-ttu-id="2a017-120">Добавьте следующее hello *с помощью* toohello директивы `BlobsController.cs` файла:</span><span class="sxs-lookup"><span data-stu-id="2a017-120">Add hello following *using* directives toohello `BlobsController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a><span data-ttu-id="2a017-121">Создание контейнера BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="2a017-121">Create a blob container</span></span>

<span data-ttu-id="2a017-122">Контейнер больших двоичных объектов — это вложенная иерархия больших двоичных объектов и папок.</span><span class="sxs-lookup"><span data-stu-id="2a017-122">A blob container is a nested hierarchy of blobs and folders.</span></span> <span data-ttu-id="2a017-123">Hello ниже показано, как toocreate контейнер больших двоичных объектов:</span><span class="sxs-lookup"><span data-stu-id="2a017-123">hello following steps illustrate how toocreate a blob container:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="2a017-124">Hello кода в этом разделе предполагается, что выполнены действия hello в разделе "hello" [настроить среду разработки hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="2a017-124">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="2a017-125">Откройте hello `BlobsController.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="2a017-125">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="2a017-126">Добавьте метод **CreateBlobContainer**, который возвращает **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="2a017-126">Add a method called **CreateBlobContainer** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="2a017-127">В пределах hello **CreateBlobContainer** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="2a017-127">Within hello **CreateBlobContainer** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="2a017-128">Используйте следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="2a017-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration.</span></span> <span data-ttu-id="2a017-129">(Изменение  *&lt;имя учетной записи хранения >* toohello имя hello вы запрашиваете доступ к учетной записи хранилища Azure.)</span><span class="sxs-lookup"><span data-stu-id="2a017-129">(Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="2a017-130">Получите объект **CloudBlobClient**, который представляет клиента службы BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="2a017-130">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="2a017-131">Получить **CloudBlobContainer** , представляющий имени ссылки toohello требуемый BLOB-объект контейнера.</span><span class="sxs-lookup"><span data-stu-id="2a017-131">Get a **CloudBlobContainer** object that represents a reference toohello desired blob container name.</span></span> <span data-ttu-id="2a017-132">Hello **CloudBlobClient.GetContainerReference** метод не выполняет запрос к хранилищу BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="2a017-132">hello **CloudBlobClient.GetContainerReference** method does not make a request against blob storage.</span></span> <span data-ttu-id="2a017-133">ли контейнер больших двоичных объектов hello существует, возвращается ссылка Hello.</span><span class="sxs-lookup"><span data-stu-id="2a017-133">hello reference is returned whether or not hello blob container exists.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="2a017-134">Вызовите hello **CloudBlobContainer.CreateIfNotExists** метод toocreate hello контейнера, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="2a017-134">Call hello **CloudBlobContainer.CreateIfNotExists** method toocreate hello container if it does not yet exist.</span></span> <span data-ttu-id="2a017-135">Hello **CloudBlobContainer.CreateIfNotExists** возвращает **true** Если hello контейнер не существует и успешно создан.</span><span class="sxs-lookup"><span data-stu-id="2a017-135">hello **CloudBlobContainer.CreateIfNotExists** method returns **true** if hello container does not exist, and is successfully created.</span></span> <span data-ttu-id="2a017-136">В противном случае возвращается значение **false**.</span><span class="sxs-lookup"><span data-stu-id="2a017-136">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. <span data-ttu-id="2a017-137">Обновление hello **ViewBag** с именем hello hello контейнера BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="2a017-137">Update hello **ViewBag** with hello name of hello blob container.</span></span>

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. <span data-ttu-id="2a017-138">В hello **обозреватель решений**, разверните hello **представления** папки, щелкните правой кнопкой мыши **большие двоичные объекты**и в контекстном меню hello выберите **Добавить -> Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="2a017-138">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="2a017-139">На hello **добавить представление** диалоговое окно, введите **CreateBlobContainer** hello имя представления, а также выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="2a017-139">On hello **Add View** dialog, enter **CreateBlobContainer** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="2a017-140">Откройте `CreateBlobContainer.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="2a017-140">Open `CreateBlobContainer.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="2a017-141">В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="2a017-141">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="2a017-142">После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="2a017-142">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. <span data-ttu-id="2a017-143">Запустите приложение hello и выберите **создать контейнер больших двоичных объектов** toosee результаты, аналогичные toohello следующий снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="2a017-143">Run hello application, and select **Create Blob Container** toosee results similar toohello following screen shot:</span></span>
  
    ![Создание контейнера больших двоичных объектов](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    <span data-ttu-id="2a017-145">Как упоминалось ранее, hello **CloudBlobContainer.CreateIfNotExists** возвращает **true** только когда hello контейнер не существует и создается.</span><span class="sxs-lookup"><span data-stu-id="2a017-145">As mentioned previously, hello **CloudBlobContainer.CreateIfNotExists** method returns **true** only when hello container doesn't exist and is created.</span></span> <span data-ttu-id="2a017-146">Таким образом, если при запуске приложение hello hello контейнер существует, метод hello возвращает **false**.</span><span class="sxs-lookup"><span data-stu-id="2a017-146">Therefore, if you run hello app when hello container exists, hello method returns **false**.</span></span> <span data-ttu-id="2a017-147">приложение hello toorun несколько раз, необходимо удалить контейнер hello перед повторным запуском приложения hello.</span><span class="sxs-lookup"><span data-stu-id="2a017-147">toorun hello app multiple times, you must delete hello container before running hello app again.</span></span> <span data-ttu-id="2a017-148">Удаление контейнера hello можно сделать с помощью hello **CloudBlobContainer.Delete** метод.</span><span class="sxs-lookup"><span data-stu-id="2a017-148">Deleting hello container can be done via hello **CloudBlobContainer.Delete** method.</span></span> <span data-ttu-id="2a017-149">Можно также удалить hello контейнера при помощи hello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) или hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="2a017-149">You can also delete hello container using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="upload-a-blob-into-a-blob-container"></a><span data-ttu-id="2a017-150">Отправка большого двоичного объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="2a017-150">Upload a blob into a blob container</span></span>

<span data-ttu-id="2a017-151">После того как вы создали [контейнер больших двоичных объектов](#create-a-blob-container), вы можете передать в него файлы.</span><span class="sxs-lookup"><span data-stu-id="2a017-151">Once you've [created a blob container](#create-a-blob-container), you can upload files into that container.</span></span> <span data-ttu-id="2a017-152">В этом разделе описывается загрузка контейнер больших двоичных объектов tooa локального файла.</span><span class="sxs-lookup"><span data-stu-id="2a017-152">This section walks you through uploading a local file tooa blob container.</span></span> <span data-ttu-id="2a017-153">Hello предполагается, что вы создали контейнер больших двоичных объектов с именем *тест контейнер больших двоичных объектов*.</span><span class="sxs-lookup"><span data-stu-id="2a017-153">hello steps assume you've created a blob container named *test-blob-container*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="2a017-154">Hello кода в этом разделе предполагается, что выполнены действия hello в разделе "hello" [настроить среду разработки hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="2a017-154">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="2a017-155">Откройте hello `BlobsController.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="2a017-155">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="2a017-156">Добавьте метод **UploadBlob**, который возвращает **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="2a017-156">Add a method called **UploadBlob** that returns an **EmptyResult**.</span></span>

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="2a017-157">В пределах hello **UploadBlob** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="2a017-157">Within hello **UploadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="2a017-158">Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)</span><span class="sxs-lookup"><span data-stu-id="2a017-158">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="2a017-159">Получите объект **CloudBlobClient**, который представляет клиента службы BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="2a017-159">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="2a017-160">Получить **CloudBlobContainer** , представляющий имя контейнера больших двоичных объектов toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="2a017-160">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="2a017-161">Как объяснялось ранее, служба хранилища Azure поддерживает различные типы больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="2a017-161">As explained earlier, Azure storage supports different blob types.</span></span> <span data-ttu-id="2a017-162">tooretrieve большой двоичный объект страницы ссылка tooa hello вызовов **CloudBlobContainer.GetPageBlobReference** метод.</span><span class="sxs-lookup"><span data-stu-id="2a017-162">tooretrieve a reference tooa page blob, call hello **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="2a017-163">tooretrieve большой двоичный объект блока ссылка tooa hello вызовов **CloudBlobContainer.GetBlockBlobReference** метод.</span><span class="sxs-lookup"><span data-stu-id="2a017-163">tooretrieve a reference tooa block blob, call hello **CloudBlobContainer.GetBlockBlobReference** method.</span></span> <span data-ttu-id="2a017-164">Как правило блочного BLOB-объекта — hello, рекомендуется toouse типа.</span><span class="sxs-lookup"><span data-stu-id="2a017-164">Usually, block blob is hello recommended type toouse.</span></span> <span data-ttu-id="2a017-165">(Изменение < имя большого двоичного объекта > * имя toohello требуется один раз отправить большой двоичный объект hello toogive.)</span><span class="sxs-lookup"><span data-stu-id="2a017-165">(Change <blob-name>* toohello name you want toogive hello blob once uploaded.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="2a017-166">Получив ссылку на большой двоичный объект, можно передать любой tooit потока данных путем вызова hello большого двоичного объекта ссылка объекта **UploadFromStream** метод.</span><span class="sxs-lookup"><span data-stu-id="2a017-166">Once you have a blob reference, you can upload any data stream tooit by calling hello blob reference object's **UploadFromStream** method.</span></span> <span data-ttu-id="2a017-167">Hello **UploadFromStream** метод создает hello большой двоичный объект, если он не существует, или перезаписывает его, если он существует.</span><span class="sxs-lookup"><span data-stu-id="2a017-167">hello **UploadFromStream** method creates hello blob if it doesn't exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="2a017-168">(Изменение  *&lt;передачу файла >* tooa полный путь к файлу toohello требуется tooupload.)</span><span class="sxs-lookup"><span data-stu-id="2a017-168">(Change *&lt;file-to-upload>* tooa fully qualified path toohello file you want tooupload.)</span></span>

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. <span data-ttu-id="2a017-169">В hello **обозреватель решений**, разверните hello **представления** папки, щелкните правой кнопкой мыши **большие двоичные объекты**и в контекстном меню hello выберите **Добавить -> Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="2a017-169">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="2a017-170">В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="2a017-170">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="2a017-171">После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="2a017-171">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="2a017-172">Запустите приложение hello и выберите **передачи BLOB-объекта**.</span><span class="sxs-lookup"><span data-stu-id="2a017-172">Run hello application, and select **Upload blob**.</span></span>  
  
<span data-ttu-id="2a017-173">Здравствуйте, раздел - [hello двоичные объекты перечислены в контейнер больших двоичных объектов](#list-the-blobs-in-a-blob-container) -показано, как toolist hello большие двоичные объекты в контейнере больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="2a017-173">hello section - [List hello blobs in a blob container](#list-the-blobs-in-a-blob-container) - illustrates how toolist hello blobs in a blob container.</span></span>  

## <a name="list-hello-blobs-in-a-blob-container"></a><span data-ttu-id="2a017-174">Перечисление больших двоичных объектов hello в контейнер больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="2a017-174">List hello blobs in a blob container</span></span>

<span data-ttu-id="2a017-175">В этом разделе показано, как toolist hello большие двоичные объекты в контейнере больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="2a017-175">This section illustrates how toolist hello blobs in a blob container.</span></span> <span data-ttu-id="2a017-176">код образца Hello ссылается hello *тест контейнер больших двоичных объектов* создан в разделе hello [создать контейнер больших двоичных объектов](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="2a017-176">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

> [!NOTE]
> 
> <span data-ttu-id="2a017-177">Hello кода в этом разделе предполагается, что выполнены действия hello в разделе "hello" [настроить среду разработки hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="2a017-177">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="2a017-178">Откройте hello `BlobsController.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="2a017-178">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="2a017-179">Добавьте метод **ListBlobs**, который возвращает **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="2a017-179">Add a method called **ListBlobs** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="2a017-180">В пределах hello **ListBlobs** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="2a017-180">Within hello **ListBlobs** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="2a017-181">Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)</span><span class="sxs-lookup"><span data-stu-id="2a017-181">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="2a017-182">Получите объект **CloudBlobClient**, который представляет клиента службы BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="2a017-182">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="2a017-183">Получить **CloudBlobContainer** , представляющий имя контейнера больших двоичных объектов toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="2a017-183">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="2a017-184">toolist hello BLOB-объектов в контейнере больших двоичных объектов, используйте hello **CloudBlobContainer.ListBlobs** метод.</span><span class="sxs-lookup"><span data-stu-id="2a017-184">toolist hello blobs in a blob container, use hello **CloudBlobContainer.ListBlobs** method.</span></span> <span data-ttu-id="2a017-185">Hello **CloudBlobContainer.ListBlobs** возвращает **IListBlobItem** объекта приведение tooa **CloudBlockBlob**, **CloudPageBlob**, или **CloudBlobDirectory** объекта.</span><span class="sxs-lookup"><span data-stu-id="2a017-185">hello **CloudBlobContainer.ListBlobs** method returns an **IListBlobItem** object that you cast tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="2a017-186">Hello следующий фрагмент кода перечисляет все большие двоичные объекты hello в контейнер больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="2a017-186">hello following code snippet enumerates all hello blobs in a blob container.</span></span> <span data-ttu-id="2a017-187">Каждый BLOB-объект — привести toohello соответствующий объект на основе ее типа и его имя (или URI в случае hello **CloudBlobDirectory**) добавляется в список tooa.</span><span class="sxs-lookup"><span data-stu-id="2a017-187">Each blob is cast toohello appropriate object based on its type, and its name (or URI in hello case of a **CloudBlobDirectory**) is added tooa list.</span></span>

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

    <span data-ttu-id="2a017-188">В tooblobs добавление контейнеров больших двоичных объектов может содержать каталоги.</span><span class="sxs-lookup"><span data-stu-id="2a017-188">In addition tooblobs, blob containers can contain directories.</span></span> <span data-ttu-id="2a017-189">Предположим, у вас есть контейнер BLOB-объекта с именем *тест контейнер больших двоичных объектов* с hello следующая иерархия:</span><span class="sxs-lookup"><span data-stu-id="2a017-189">Let's suppose you have a blob container called *test-blob-container* with hello following hierarchy:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

    <span data-ttu-id="2a017-190">Здравствуйте, используя предшествующие примере кода hello, **большие двоичные объекты** список строк содержит аналогичные toohello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="2a017-190">Using hello preceding code example, hello **blobs** string list contains values similar toohello following:</span></span>

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    <span data-ttu-id="2a017-191">Как видите, hello список включает только hello сущности верхнего уровня; не hello вложенных областей (*bar.png* и *baz.png*).</span><span class="sxs-lookup"><span data-stu-id="2a017-191">As you can see, hello list includes only hello top-level entities; not hello nested ones (*bar.png* and *baz.png*).</span></span> <span data-ttu-id="2a017-192">toolist все hello сущностям в контейнер больших двоичных объектов, необходимо вызвать hello **CloudBlobContainer.ListBlobs** метод и передайте **true** для hello **useFlatBlobListing** параметр.</span><span class="sxs-lookup"><span data-stu-id="2a017-192">toolist all hello entities within a blob container, you must call hello **CloudBlobContainer.ListBlobs** method and pass **true** for hello **useFlatBlobListing** parameter.</span></span>    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    <span data-ttu-id="2a017-193">Параметр hello **useFlatBlobListing** параметр слишком**true** возвращает плоский список всех сущностей в контейнер больших двоичных объектов hello и выдает hello следующие результаты:</span><span class="sxs-lookup"><span data-stu-id="2a017-193">Setting hello **useFlatBlobListing** parameter too**true** returns a flat listing of all entities in hello blob container, and yields hello following results:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

1. <span data-ttu-id="2a017-194">В hello **обозреватель решений**, разверните hello **представления** папки, щелкните правой кнопкой мыши **большие двоичные объекты**и в контекстном меню hello выберите **Добавить -> Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="2a017-194">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="2a017-195">На hello **добавить представление** диалоговое окно, введите **ListBlobs** hello имя представления, а также выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="2a017-195">On hello **Add View** dialog, enter **ListBlobs** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="2a017-196">Откройте `ListBlobs.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="2a017-196">Open `ListBlobs.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="2a017-197">В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="2a017-197">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="2a017-198">После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="2a017-198">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. <span data-ttu-id="2a017-199">Запустите приложение hello и выберите **перечисление больших двоичных объектов** toosee результаты, аналогичные toohello следующий снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="2a017-199">Run hello application, and select **List blobs** toosee results similar toohello following screen shot:</span></span>
  
    ![Получение списка больших двоичных объектов](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a><span data-ttu-id="2a017-201">Скачивание больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="2a017-201">Download blobs</span></span>

<span data-ttu-id="2a017-202">В этом разделе показано, как toodownload большого двоичного объекта и либо ее сохранения toolocal хранилища или чтения hello содержимое в строку.</span><span class="sxs-lookup"><span data-stu-id="2a017-202">This section illustrates how toodownload a blob and either persist it toolocal storage or read hello contents into a string.</span></span> <span data-ttu-id="2a017-203">код образца Hello ссылается hello *тест контейнер больших двоичных объектов* создан в разделе hello [создать контейнер больших двоичных объектов](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="2a017-203">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

1. <span data-ttu-id="2a017-204">Откройте hello `BlobsController.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="2a017-204">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="2a017-205">Добавьте метод **DownloadBlob**, который возвращает **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="2a017-205">Add a method called **DownloadBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="2a017-206">В пределах hello **DownloadBlob** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="2a017-206">Within hello **DownloadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="2a017-207">Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)</span><span class="sxs-lookup"><span data-stu-id="2a017-207">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="2a017-208">Получите объект **CloudBlobClient**, который представляет клиента службы BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="2a017-208">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="2a017-209">Получить **CloudBlobContainer** , представляющий имя контейнера больших двоичных объектов toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="2a017-209">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="2a017-210">Получить объект большого двоичного объекта можно, вызвав следующие методы: **CloudBlobContainer.GetBlockBlobReference** или **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="2a017-210">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="2a017-211">(Изменение  *&lt;имя большого двоичного объекта >* toohello имя большого двоичного объекта hello вы загружаете.)</span><span class="sxs-lookup"><span data-stu-id="2a017-211">(Change *&lt;blob-name>* toohello name of hello blob you are downloading.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="2a017-212">toodownload большого двоичного объекта используйте hello **CloudBlockBlob.DownloadToStream** или **CloudPageBlob.DownloadToStream** метод в зависимости от типа hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="2a017-212">toodownload a blob, use hello **CloudBlockBlob.DownloadToStream** or **CloudPageBlob.DownloadToStream** method, depending on hello blob type.</span></span> <span data-ttu-id="2a017-213">Hello следующий фрагмент кода использует hello **CloudBlockBlob.DownloadToStream** tootransfer метод объект потока tooa содержимое большого двоичного объекта, затем сохраняется локальный файл tooa: (изменение  *&lt;локального файла >* toohello полное имя, представляющее имя файла место загрузки blob hello.)</span><span class="sxs-lookup"><span data-stu-id="2a017-213">hello following code snippet uses hello **CloudBlockBlob.DownloadToStream** method tootransfer a blob's contents tooa stream object that is then persisted tooa local file: (Change *&lt;local-file-name>* toohello fully qualified file name representing where you want hello blob downloaded.)</span></span> 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. <span data-ttu-id="2a017-214">В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="2a017-214">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="2a017-215">После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="2a017-215">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="2a017-216">Запустите приложение hello и выберите **загрузки больших двоичных объектов** toodownload hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="2a017-216">Run hello application, and select **Download blob** toodownload hello blob.</span></span> <span data-ttu-id="2a017-217">Hello BLOB-объект, указанный в hello **CloudBlobContainer.GetBlockBlobReference** вызова метода загрузки toohello расположении, указанном в hello **File.OpenWrite** вызова метода.</span><span class="sxs-lookup"><span data-stu-id="2a017-217">hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call downloads toohello location you specify in hello **File.OpenWrite** method call.</span></span> 

## <a name="delete-blobs"></a><span data-ttu-id="2a017-218">Удаление blob-объектов</span><span class="sxs-lookup"><span data-stu-id="2a017-218">Delete blobs</span></span>

<span data-ttu-id="2a017-219">Hello ниже показано, как toodelete большого двоичного объекта:</span><span class="sxs-lookup"><span data-stu-id="2a017-219">hello following steps illustrate how toodelete a blob:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="2a017-220">Hello кода в этом разделе предполагается, что выполнены действия hello в разделе "hello" [настроить среду разработки hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="2a017-220">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="2a017-221">Откройте hello `BlobsController.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="2a017-221">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="2a017-222">Добавьте метод **DeleteBlob**, который возвращает **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="2a017-222">Add a method called **DeleteBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. <span data-ttu-id="2a017-223">Получите объект **CloudStorageAccount** , представляющий данные учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="2a017-223">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="2a017-224">Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)</span><span class="sxs-lookup"><span data-stu-id="2a017-224">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="2a017-225">Получите объект **CloudBlobClient**, который представляет клиента службы BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="2a017-225">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="2a017-226">Получить **CloudBlobContainer** , представляющий имя контейнера больших двоичных объектов toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="2a017-226">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="2a017-227">Получить объект большого двоичного объекта можно, вызвав следующие методы: **CloudBlobContainer.GetBlockBlobReference** или **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="2a017-227">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="2a017-228">(Изменение  *&lt;имя большого двоичного объекта >* имя toohello hello большого двоичного объекта, вы удаляете.)</span><span class="sxs-lookup"><span data-stu-id="2a017-228">(Change *&lt;blob-name>* toohello name of hello blob you are deleting.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. <span data-ttu-id="2a017-229">В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="2a017-229">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="2a017-230">После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="2a017-230">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="2a017-231">Запустите приложение hello и выберите **удаления большого двоичного объекта** toodelete hello BLOB-объект, указанный в hello **CloudBlobContainer.GetBlockBlobReference** вызова метода.</span><span class="sxs-lookup"><span data-stu-id="2a017-231">Run hello application, and select **Delete blob** toodelete hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2a017-232">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2a017-232">Next steps</span></span>
<span data-ttu-id="2a017-233">Просмотрите дополнительные toolearn функция руководства о дополнительных параметрах для хранения данных в Azure.</span><span class="sxs-lookup"><span data-stu-id="2a017-233">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="2a017-234">Начало работы с хранилищем таблиц Azure и подключенными службами Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="2a017-234">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-tables.md)
  * [<span data-ttu-id="2a017-235">Начало работы с хранилищем очередей Azure и подключенными службами Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2a017-235">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-queues.md)
