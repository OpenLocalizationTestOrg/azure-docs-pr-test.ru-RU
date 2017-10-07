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
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a>Приступая к работе с хранилищем BLOB-объектов Azure и подключенными службами Visual Studio (ASP.NET)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Обзор

Хранилище больших двоичных объектов — это служба, неструктурированные данные хранятся в облаке hello как большие двоичные объекты и объекты. В хранилище BLOB-объектов могут храниться текстовые или двоичные данные любого типа, например документы, файлы мультимедиа или установщики приложений. Хранилище больших двоичных объектов также является ссылка tooas объекта хранилища.

В этом учебнике показано, как toowrite ASP.NET кода в некоторых распространенных сценариях, с помощью хранилища BLOB-объектов Azure. В частности, здесь рассматриваются такие сценарии, как создание контейнера больших двоичных объектов, а также скачивание, получение списка, скачивание и удаление больших двоичных объектов.

##<a name="prerequisites"></a>Предварительные требования

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Учетная запись хранения Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Создание контроллера MVC 

1. В hello **обозревателе решений**, щелкните правой кнопкой мыши **контроллеров**и в контекстном меню hello, выберите **Добавить -> контроллер**.

    ![Добавление контроллера tooan приложение ASP.NET MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. На hello **Добавление формирования шаблонов** диалогового окна выберите **контроллер MVC 5 - пустой**и выберите **добавить**.

    ![Выбор типа контроллера MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. На hello **добавления контроллера** диалогового окна, имя контроллера hello *BlobsController*и выберите **добавить**.

    ![Имя контроллера MVC hello](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. Добавьте следующее hello *с помощью* toohello директивы `BlobsController.cs` файла:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a>Создание контейнера BLOB-объектов

Контейнер больших двоичных объектов — это вложенная иерархия больших двоичных объектов и папок. Hello ниже показано, как toocreate контейнер больших двоичных объектов:

> [!NOTE]
> 
> Hello кода в этом разделе предполагается, что выполнены действия hello в разделе "hello" [настроить среду разработки hello](#set-up-the-development-environment). 

1. Откройте hello `BlobsController.cs` файла.

1. Добавьте метод **CreateBlobContainer**, который возвращает **ActionResult**.

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. В пределах hello **CreateBlobContainer** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения. Используйте следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello hello. (Изменение  *&lt;имя учетной записи хранения >* toohello имя hello вы запрашиваете доступ к учетной записи хранилища Azure.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Получите объект **CloudBlobClient**, который представляет клиента службы BLOB-объектов.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Получить **CloudBlobContainer** , представляющий имени ссылки toohello требуемый BLOB-объект контейнера. Hello **CloudBlobClient.GetContainerReference** метод не выполняет запрос к хранилищу BLOB-объектов. ли контейнер больших двоичных объектов hello существует, возвращается ссылка Hello. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Вызовите hello **CloudBlobContainer.CreateIfNotExists** метод toocreate hello контейнера, если он еще не существует. Hello **CloudBlobContainer.CreateIfNotExists** возвращает **true** Если hello контейнер не существует и успешно создан. В противном случае возвращается значение **false**.    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. Обновление hello **ViewBag** с именем hello hello контейнера BLOB-объектов.

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. В hello **обозреватель решений**, разверните hello **представления** папки, щелкните правой кнопкой мыши **большие двоичные объекты**и в контекстном меню hello выберите **Добавить -> Просмотр**.

1. На hello **добавить представление** диалоговое окно, введите **CreateBlobContainer** hello имя представления, а также выберите **добавить**.

1. Откройте `CreateBlobContainer.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.

1. После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. Запустите приложение hello и выберите **создать контейнер больших двоичных объектов** toosee результаты, аналогичные toohello следующий снимок экрана:
  
    ![Создание контейнера больших двоичных объектов](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    Как упоминалось ранее, hello **CloudBlobContainer.CreateIfNotExists** возвращает **true** только когда hello контейнер не существует и создается. Таким образом, если при запуске приложение hello hello контейнер существует, метод hello возвращает **false**. приложение hello toorun несколько раз, необходимо удалить контейнер hello перед повторным запуском приложения hello. Удаление контейнера hello можно сделать с помощью hello **CloudBlobContainer.Delete** метод. Можно также удалить hello контейнера при помощи hello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) или hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="upload-a-blob-into-a-blob-container"></a>Отправка большого двоичного объекта в контейнер

После того как вы создали [контейнер больших двоичных объектов](#create-a-blob-container), вы можете передать в него файлы. В этом разделе описывается загрузка контейнер больших двоичных объектов tooa локального файла. Hello предполагается, что вы создали контейнер больших двоичных объектов с именем *тест контейнер больших двоичных объектов*. 

> [!NOTE]
> 
> Hello кода в этом разделе предполагается, что выполнены действия hello в разделе "hello" [настроить среду разработки hello](#set-up-the-development-environment). 

1. Откройте hello `BlobsController.cs` файла.

1. Добавьте метод **UploadBlob**, который возвращает **EmptyResult**.

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. В пределах hello **UploadBlob** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения. Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Получите объект **CloudBlobClient**, который представляет клиента службы BLOB-объектов.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Получить **CloudBlobContainer** , представляющий имя контейнера больших двоичных объектов toohello ссылки. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Как объяснялось ранее, служба хранилища Azure поддерживает различные типы больших двоичных объектов. tooretrieve большой двоичный объект страницы ссылка tooa hello вызовов **CloudBlobContainer.GetPageBlobReference** метод. tooretrieve большой двоичный объект блока ссылка tooa hello вызовов **CloudBlobContainer.GetBlockBlobReference** метод. Как правило блочного BLOB-объекта — hello, рекомендуется toouse типа. (Изменение < имя большого двоичного объекта > * имя toohello требуется один раз отправить большой двоичный объект hello toogive.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. Получив ссылку на большой двоичный объект, можно передать любой tooit потока данных путем вызова hello большого двоичного объекта ссылка объекта **UploadFromStream** метод. Hello **UploadFromStream** метод создает hello большой двоичный объект, если он не существует, или перезаписывает его, если он существует. (Изменение  *&lt;передачу файла >* tooa полный путь к файлу toohello требуется tooupload.)

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. В hello **обозреватель решений**, разверните hello **представления** папки, щелкните правой кнопкой мыши **большие двоичные объекты**и в контекстном меню hello выберите **Добавить -> Просмотр**.

1. В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.

1. После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. Запустите приложение hello и выберите **передачи BLOB-объекта**.  
  
Здравствуйте, раздел - [hello двоичные объекты перечислены в контейнер больших двоичных объектов](#list-the-blobs-in-a-blob-container) -показано, как toolist hello большие двоичные объекты в контейнере больших двоичных объектов.  

## <a name="list-hello-blobs-in-a-blob-container"></a>Перечисление больших двоичных объектов hello в контейнер больших двоичных объектов

В этом разделе показано, как toolist hello большие двоичные объекты в контейнере больших двоичных объектов. код образца Hello ссылается hello *тест контейнер больших двоичных объектов* создан в разделе hello [создать контейнер больших двоичных объектов](#create-a-blob-container).

> [!NOTE]
> 
> Hello кода в этом разделе предполагается, что выполнены действия hello в разделе "hello" [настроить среду разработки hello](#set-up-the-development-environment). 

1. Откройте hello `BlobsController.cs` файла.

1. Добавьте метод **ListBlobs**, который возвращает **ActionResult**.

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. В пределах hello **ListBlobs** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения. Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Получите объект **CloudBlobClient**, который представляет клиента службы BLOB-объектов.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Получить **CloudBlobContainer** , представляющий имя контейнера больших двоичных объектов toohello ссылки. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. toolist hello BLOB-объектов в контейнере больших двоичных объектов, используйте hello **CloudBlobContainer.ListBlobs** метод. Hello **CloudBlobContainer.ListBlobs** возвращает **IListBlobItem** объекта приведение tooa **CloudBlockBlob**, **CloudPageBlob**, или **CloudBlobDirectory** объекта. Hello следующий фрагмент кода перечисляет все большие двоичные объекты hello в контейнер больших двоичных объектов. Каждый BLOB-объект — привести toohello соответствующий объект на основе ее типа и его имя (или URI в случае hello **CloudBlobDirectory**) добавляется в список tooa.

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

    В tooblobs добавление контейнеров больших двоичных объектов может содержать каталоги. Предположим, у вас есть контейнер BLOB-объекта с именем *тест контейнер больших двоичных объектов* с hello следующая иерархия:

        foo.png
        dir1/bar.png
        dir2/baz.png

    Здравствуйте, используя предшествующие примере кода hello, **большие двоичные объекты** список строк содержит аналогичные toohello следующие значения:

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    Как видите, hello список включает только hello сущности верхнего уровня; не hello вложенных областей (*bar.png* и *baz.png*). toolist все hello сущностям в контейнер больших двоичных объектов, необходимо вызвать hello **CloudBlobContainer.ListBlobs** метод и передайте **true** для hello **useFlatBlobListing** параметр.    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    Параметр hello **useFlatBlobListing** параметр слишком**true** возвращает плоский список всех сущностей в контейнер больших двоичных объектов hello и выдает hello следующие результаты:

        foo.png
        dir1/bar.png
        dir2/baz.png

1. В hello **обозреватель решений**, разверните hello **представления** папки, щелкните правой кнопкой мыши **большие двоичные объекты**и в контекстном меню hello выберите **Добавить -> Просмотр**.

1. На hello **добавить представление** диалоговое окно, введите **ListBlobs** hello имя представления, а также выберите **добавить**.

1. Откройте `ListBlobs.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:

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

1. В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.

1. После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. Запустите приложение hello и выберите **перечисление больших двоичных объектов** toosee результаты, аналогичные toohello следующий снимок экрана:
  
    ![Получение списка больших двоичных объектов](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a>Скачивание больших двоичных объектов

В этом разделе показано, как toodownload большого двоичного объекта и либо ее сохранения toolocal хранилища или чтения hello содержимое в строку. код образца Hello ссылается hello *тест контейнер больших двоичных объектов* создан в разделе hello [создать контейнер больших двоичных объектов](#create-a-blob-container).

1. Откройте hello `BlobsController.cs` файла.

1. Добавьте метод **DownloadBlob**, который возвращает **ActionResult**.

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. В пределах hello **DownloadBlob** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения. Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Получите объект **CloudBlobClient**, который представляет клиента службы BLOB-объектов.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Получить **CloudBlobContainer** , представляющий имя контейнера больших двоичных объектов toohello ссылки. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Получить объект большого двоичного объекта можно, вызвав следующие методы: **CloudBlobContainer.GetBlockBlobReference** или **CloudBlobContainer.GetPageBlobReference**. (Изменение  *&lt;имя большого двоичного объекта >* toohello имя большого двоичного объекта hello вы загружаете.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. toodownload большого двоичного объекта используйте hello **CloudBlockBlob.DownloadToStream** или **CloudPageBlob.DownloadToStream** метод в зависимости от типа hello большого двоичного объекта. Hello следующий фрагмент кода использует hello **CloudBlockBlob.DownloadToStream** tootransfer метод объект потока tooa содержимое большого двоичного объекта, затем сохраняется локальный файл tooa: (изменение  *&lt;локального файла >* toohello полное имя, представляющее имя файла место загрузки blob hello.) 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.

1. После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. Запустите приложение hello и выберите **загрузки больших двоичных объектов** toodownload hello большого двоичного объекта. Hello BLOB-объект, указанный в hello **CloudBlobContainer.GetBlockBlobReference** вызова метода загрузки toohello расположении, указанном в hello **File.OpenWrite** вызова метода. 

## <a name="delete-blobs"></a>Удаление blob-объектов

Hello ниже показано, как toodelete большого двоичного объекта:

> [!NOTE]
> 
> Hello кода в этом разделе предполагается, что выполнены действия hello в разделе "hello" [настроить среду разработки hello](#set-up-the-development-environment). 

1. Откройте hello `BlobsController.cs` файла.

1. Добавьте метод **DeleteBlob**, который возвращает **ActionResult**.

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. Получите объект **CloudStorageAccount** , представляющий данные учетной записи хранения. Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Получите объект **CloudBlobClient**, который представляет клиента службы BLOB-объектов.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Получить **CloudBlobContainer** , представляющий имя контейнера больших двоичных объектов toohello ссылки. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Получить объект большого двоичного объекта можно, вызвав следующие методы: **CloudBlobContainer.GetBlockBlobReference** или **CloudBlobContainer.GetPageBlobReference**. (Изменение  *&lt;имя большого двоичного объекта >* имя toohello hello большого двоичного объекта, вы удаляете.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.

1. После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. Запустите приложение hello и выберите **удаления большого двоичного объекта** toodelete hello BLOB-объект, указанный в hello **CloudBlobContainer.GetBlockBlobReference** вызова метода. 

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите дополнительные toolearn функция руководства о дополнительных параметрах для хранения данных в Azure.

  * [Начало работы с хранилищем таблиц Azure и подключенными службами Visual Studio (ASP.NET)](vs-storage-aspnet-getting-started-tables.md)
  * [Начало работы с хранилищем очередей Azure и подключенными службами Visual Studio](vs-storage-aspnet-getting-started-queues.md)
