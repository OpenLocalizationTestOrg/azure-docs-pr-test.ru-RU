---
title: "aaaGet к работе с хранилищем очередей Azure и Visual Studio подключения службы (ASP.NET) | Документы Microsoft"
description: "Как tooget запущена с помощью хранилища очередей Azure в проект ASP.NET в Visual Studio после подключения tooa учетной записи хранилища с помощью Visual Studio подключенные службы"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 94ca3413-5497-433f-abbe-836f83a9de72
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/23/2016
ms.author: tarcher
ms.openlocfilehash: a9d6ecb1e8d61d75f59658d0ea3fa63d26fd7354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="da553-103">Приступая к работе с хранилищем очередей Azure и подключенными службами Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="da553-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="da553-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="da553-104">Overview</span></span>

<span data-ttu-id="da553-105">Хранилище очередей Azure — это служба, обеспечивающая обмен сообщениями в облаке между компонентами приложения.</span><span class="sxs-lookup"><span data-stu-id="da553-105">Azure queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="da553-106">При разработке приложений для масштабирования компоненты приложения часто не связаны между собой, так что они могут масштабироваться независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="da553-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="da553-107">Хранилище очередей обеспечивает асинхронный обмен сообщениями для взаимодействия между компонентами приложения, ли они выполняются в облаке hello, на рабочем столе hello, на локальном сервере или на мобильном устройстве.</span><span class="sxs-lookup"><span data-stu-id="da553-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="da553-108">Хранилище очередей также поддерживает управление асинхронными задачами и создание рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="da553-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

<span data-ttu-id="da553-109">В этом учебнике показано, как toowrite ASP.NET кода в некоторых распространенных сценариях, с помощью сущностей хранилища очереди Azure.</span><span class="sxs-lookup"><span data-stu-id="da553-109">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure queue storage entities.</span></span> <span data-ttu-id="da553-110">Сюда относятся такие задачи, как создание очереди Azure, а также добавление, изменение, чтение и удаление сообщений очереди.</span><span class="sxs-lookup"><span data-stu-id="da553-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="da553-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="da553-111">Prerequisites</span></span>

* [<span data-ttu-id="da553-112">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="da553-112">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="da553-113">Учетная запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="da553-113">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="da553-114">Создание контроллера MVC</span><span class="sxs-lookup"><span data-stu-id="da553-114">Create an MVC controller</span></span> 

1. <span data-ttu-id="da553-115">В hello **обозревателе решений**, щелкните правой кнопкой мыши **контроллеров**и в контекстном меню hello, выберите **Добавить -> контроллер**.</span><span class="sxs-lookup"><span data-stu-id="da553-115">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Добавление контроллера tooan приложение ASP.NET MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. <span data-ttu-id="da553-117">На hello **Добавление формирования шаблонов** диалогового окна выберите **контроллер MVC 5 - пустой**и выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="da553-117">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Выбор типа контроллера MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. <span data-ttu-id="da553-119">На hello **добавления контроллера** диалогового окна, имя контроллера hello *QueuesController*и выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="da553-119">On hello **Add Controller** dialog, name hello controller *QueuesController*, and select **Add**.</span></span>

    ![Имя контроллера MVC hello](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. <span data-ttu-id="da553-121">Добавьте следующее hello *с помощью* toohello директивы `QueuesController.cs` файла:</span><span class="sxs-lookup"><span data-stu-id="da553-121">Add hello following *using* directives toohello `QueuesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a><span data-ttu-id="da553-122">Создать очередь</span><span class="sxs-lookup"><span data-stu-id="da553-122">Create a queue</span></span>

<span data-ttu-id="da553-123">Hello ниже показано, как toocreate очереди:</span><span class="sxs-lookup"><span data-stu-id="da553-123">hello following steps illustrate how toocreate a queue:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="da553-124">В этом разделе предполагается шаги hello [настроить среду разработки hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="da553-124">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="da553-125">Откройте hello `QueuesController.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="da553-125">Open hello `QueuesController.cs` file.</span></span> 

1. <span data-ttu-id="da553-126">Добавьте метод **CreateQueue**, который возвращает **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="da553-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="da553-127">В пределах hello **CreateQueue** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="da553-127">Within hello **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="da553-128">Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)</span><span class="sxs-lookup"><span data-stu-id="da553-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="da553-129">Получите объект **CloudQueueClient**, представляющий клиента службы очередей.</span><span class="sxs-lookup"><span data-stu-id="da553-129">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. <span data-ttu-id="da553-130">Получить **CloudQueue** , представляющий имя нужной очереди toohello ссылки.</span><span class="sxs-lookup"><span data-stu-id="da553-130">Get a **CloudQueue** object that represents a reference toohello desired queue name.</span></span> <span data-ttu-id="da553-131">Hello **CloudQueueClient.GetQueueReference** метод не выполняет запрос к очереди хранилища.</span><span class="sxs-lookup"><span data-stu-id="da553-131">hello **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span></span> <span data-ttu-id="da553-132">независимо от того, имеется ли hello очередь существует, возвращается ссылка Hello.</span><span class="sxs-lookup"><span data-stu-id="da553-132">hello reference is returned whether or not hello queue exists.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="da553-133">Вызовите hello **CloudQueue.CreateIfNotExists** метод toocreate hello очереди, если она еще не существует.</span><span class="sxs-lookup"><span data-stu-id="da553-133">Call hello **CloudQueue.CreateIfNotExists** method toocreate hello queue if it does not yet exist.</span></span> <span data-ttu-id="da553-134">Hello **CloudQueue.CreateIfNotExists** возвращает **true** Если hello очередь не существует и успешно создан.</span><span class="sxs-lookup"><span data-stu-id="da553-134">hello **CloudQueue.CreateIfNotExists** method returns **true** if hello queue does not exist, and is successfully created.</span></span> <span data-ttu-id="da553-135">В противном случае возвращается значение **false**.</span><span class="sxs-lookup"><span data-stu-id="da553-135">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. <span data-ttu-id="da553-136">Обновление hello **ViewBag** с именем hello hello очереди.</span><span class="sxs-lookup"><span data-stu-id="da553-136">Update hello **ViewBag** with hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. <span data-ttu-id="da553-137">В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **очереди**и в контекстном меню hello выберите **Добавить -> Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="da553-137">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="da553-138">На hello **добавить представление** диалоговое окно, введите **CreateQueue** hello имя представления, а также выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="da553-138">On hello **Add View** dialog, enter **CreateQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="da553-139">Откройте `CreateQueue.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="da553-139">Open `CreateQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="da553-140">В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="da553-140">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="da553-141">После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="da553-141">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. <span data-ttu-id="da553-142">Запустите приложение hello и выберите **создать очередь** toosee результаты, аналогичные toohello следующий снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="da553-142">Run hello application, and select **Create queue** toosee results similar toohello following screen shot:</span></span>
  
    ![Создание очереди](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    <span data-ttu-id="da553-144">Как упоминалось ранее, hello **CloudQueue.CreateIfNotExists** возвращает **true** только когда hello очередь не существует и создается.</span><span class="sxs-lookup"><span data-stu-id="da553-144">As mentioned previously, hello **CloudQueue.CreateIfNotExists** method returns **true** only when hello queue doesn't exist and is created.</span></span> <span data-ttu-id="da553-145">Таким образом, если при запуске приложение hello hello очередь существует, метод hello возвращает **false**.</span><span class="sxs-lookup"><span data-stu-id="da553-145">Therefore, if you run hello app when hello queue exists, hello method returns **false**.</span></span> <span data-ttu-id="da553-146">приложение hello toorun несколько раз, необходимо удалить очередь hello перед повторным запуском приложения hello.</span><span class="sxs-lookup"><span data-stu-id="da553-146">toorun hello app multiple times, you must delete hello queue before running hello app again.</span></span> <span data-ttu-id="da553-147">Удаление очереди hello можно сделать с помощью hello **CloudQueue.Delete** метод.</span><span class="sxs-lookup"><span data-stu-id="da553-147">Deleting hello queue can be done via hello **CloudQueue.Delete** method.</span></span> <span data-ttu-id="da553-148">Можно также удалить очередь hello, с помощью hello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) или hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="da553-148">You can also delete hello queue using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="da553-149">Добавить tooa очереди сообщений</span><span class="sxs-lookup"><span data-stu-id="da553-149">Add a message tooa queue</span></span>

<span data-ttu-id="da553-150">После [была создана очередь](#create-a-queue), можно добавить toothat сообщений в очереди.</span><span class="sxs-lookup"><span data-stu-id="da553-150">Once you've [created a queue](#create-a-queue), you can add messages toothat queue.</span></span> <span data-ttu-id="da553-151">В этом разделе описывается добавление очередью сообщений tooa *тестировать очередь*.</span><span class="sxs-lookup"><span data-stu-id="da553-151">This section walks you through adding a message tooa queue *test-queue*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="da553-152">В этом разделе предполагается шаги hello [настроить среду разработки hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="da553-152">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="da553-153">Откройте hello `QueuesController.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="da553-153">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="da553-154">Добавьте метод **AddMessage**, который возвращает **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="da553-154">Add a method called **AddMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="da553-155">В пределах hello **AddMessage** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="da553-155">Within hello **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="da553-156">Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)</span><span class="sxs-lookup"><span data-stu-id="da553-156">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="da553-157">Получите объект **CloudQueueClient**, представляющий клиента службы очередей.</span><span class="sxs-lookup"><span data-stu-id="da553-157">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="da553-158">Получить **CloudQueueContainer** , представляющий toohello ссылка на очередь.</span><span class="sxs-lookup"><span data-stu-id="da553-158">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="da553-159">Создать hello **CloudQueueMessage** объект, представляющий сообщение hello tooadd toohello очереди.</span><span class="sxs-lookup"><span data-stu-id="da553-159">Create hello **CloudQueueMessage** object representing hello message you want tooadd toohello queue.</span></span> <span data-ttu-id="da553-160">Для создания объекта **CloudQueueMessage** можно использовать либо строку (в формате UTF-8), либо массив типа byte.</span><span class="sxs-lookup"><span data-stu-id="da553-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. <span data-ttu-id="da553-161">Вызовите hello **CloudQueue.AddMessage** метод tooadd hello корреляции toohello очереди.</span><span class="sxs-lookup"><span data-stu-id="da553-161">Call hello **CloudQueue.AddMessage** method tooadd hello messaged toohello queue.</span></span>

    ```csharp
    queue.AddMessage(message);
    ```

1. <span data-ttu-id="da553-162">Создайте и задайте несколько **ViewBag** свойства для отображения в представлении hello.</span><span class="sxs-lookup"><span data-stu-id="da553-162">Create and set a couple of **ViewBag** properties for display in hello view.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. <span data-ttu-id="da553-163">В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **очереди**и в контекстном меню hello выберите **Добавить -> Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="da553-163">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="da553-164">На hello **добавить представление** диалоговое окно, введите **AddMessage** hello имя представления, а также выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="da553-164">On hello **Add View** dialog, enter **AddMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="da553-165">Откройте `AddMessage.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="da553-165">Open `AddMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. <span data-ttu-id="da553-166">В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="da553-166">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="da553-167">После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="da553-167">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. <span data-ttu-id="da553-168">Запустите приложение hello и выберите **добавить сообщение** toosee результаты, аналогичные toohello следующий снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="da553-168">Run hello application, and select **Add message** toosee results similar toohello following screen shot:</span></span>
  
    ![Добавление сообщения](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

<span data-ttu-id="da553-170">Здравствуйте, два раздела - [чтения сообщения из очереди, не удаляя его](#read-a-message-from-a-queue-without-removing-it) и [чтение и удаление сообщения из очереди](#read-and-remove-a-message-from-a-queue) -показывают, как tooread сообщений из очереди.</span><span class="sxs-lookup"><span data-stu-id="da553-170">hello two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how tooread messages from a queue.</span></span>  

## <a name="read-a-message-from-a-queue-without-removing-it"></a><span data-ttu-id="da553-171">Чтение сообщения из очереди, не удаляя его</span><span class="sxs-lookup"><span data-stu-id="da553-171">Read a message from a queue without removing it</span></span>

<span data-ttu-id="da553-172">В этом разделе показано, как toopeek в сообщение из очереди (чтения hello первого сообщения без его удаления).</span><span class="sxs-lookup"><span data-stu-id="da553-172">This section illustrates how toopeek at a queued message (read hello first message without removing it).</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="da553-173">В этом разделе предполагается шаги hello [настроить среду разработки hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="da553-173">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="da553-174">Откройте hello `QueuesController.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="da553-174">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="da553-175">Добавьте метод **PeekMessage**, который возвращает **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="da553-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="da553-176">В пределах hello **PeekMessage** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="da553-176">Within hello **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="da553-177">Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)</span><span class="sxs-lookup"><span data-stu-id="da553-177">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="da553-178">Получите объект **CloudQueueClient**, представляющий клиента службы очередей.</span><span class="sxs-lookup"><span data-stu-id="da553-178">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="da553-179">Получить **CloudQueueContainer** , представляющий toohello ссылка на очередь.</span><span class="sxs-lookup"><span data-stu-id="da553-179">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="da553-180">Вызовите hello **CloudQueue.PeekMessage** метод tooread hello первого сообщения в очереди hello, не удаляя его из очереди hello.</span><span class="sxs-lookup"><span data-stu-id="da553-180">Call hello **CloudQueue.PeekMessage** method tooread hello first message in hello queue without removing it from hello queue.</span></span> 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. <span data-ttu-id="da553-181">Обновление hello **ViewBag** с двумя значениями: имя очереди hello и приветственное сообщение, которое было прочитано.</span><span class="sxs-lookup"><span data-stu-id="da553-181">Update hello **ViewBag** with two values: hello queue name and hello message that was read.</span></span> <span data-ttu-id="da553-182">Hello **CloudQueueMessage** объект предоставляет два свойства для получения значения hello объекта: **CloudQueueMessage.AsBytes** и **CloudQueueMessage.AsString**.</span><span class="sxs-lookup"><span data-stu-id="da553-182">hello **CloudQueueMessage** object exposes two properties for getting hello object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span></span> <span data-ttu-id="da553-183">**AsString** (который используется в этом примере) возвращает строку, а **AsBytes** возвращает массив байтов.</span><span class="sxs-lookup"><span data-stu-id="da553-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. <span data-ttu-id="da553-184">В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **очереди**и в контекстном меню hello выберите **Добавить -> Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="da553-184">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="da553-185">На hello **добавить представление** диалоговое окно, введите **PeekMessage** hello имя представления, а также выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="da553-185">On hello **Add View** dialog, enter **PeekMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="da553-186">Откройте `PeekMessage.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="da553-186">Open `PeekMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "PeekMessage";
    }
    
    <h2>Peek Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Peeked Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>    
    ```

1. <span data-ttu-id="da553-187">В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="da553-187">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="da553-188">После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="da553-188">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. <span data-ttu-id="da553-189">Запустите приложение hello и выберите **считывания сообщения** toosee результаты, аналогичные toohello следующий снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="da553-189">Run hello application, and select **Peek message** toosee results similar toohello following screen shot:</span></span>
  
    ![Просмотр сообщения](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a><span data-ttu-id="da553-191">Чтение и удаление сообщения из очереди</span><span class="sxs-lookup"><span data-stu-id="da553-191">Read and remove a message from a queue</span></span>

<span data-ttu-id="da553-192">В этом разделе вы узнаете, как tooread и удалять сообщение из очереди.</span><span class="sxs-lookup"><span data-stu-id="da553-192">In this section, you learn how tooread and remove a message from a queue.</span></span>   

> [!NOTE]
> 
> <span data-ttu-id="da553-193">В этом разделе предполагается шаги hello [настроить среду разработки hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="da553-193">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="da553-194">Откройте hello `QueuesController.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="da553-194">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="da553-195">Добавьте метод **ReadMessage**, который возвращает **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="da553-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="da553-196">В пределах hello **ReadMessage** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="da553-196">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="da553-197">Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)</span><span class="sxs-lookup"><span data-stu-id="da553-197">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="da553-198">Получите объект **CloudQueueClient**, представляющий клиента службы очередей.</span><span class="sxs-lookup"><span data-stu-id="da553-198">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="da553-199">Получить **CloudQueueContainer** , представляющий toohello ссылка на очередь.</span><span class="sxs-lookup"><span data-stu-id="da553-199">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="da553-200">Вызовите hello **CloudQueue.GetMessage** метод tooread hello первого сообщения в очереди hello.</span><span class="sxs-lookup"><span data-stu-id="da553-200">Call hello **CloudQueue.GetMessage** method tooread hello first message in hello queue.</span></span> <span data-ttu-id="da553-201">Hello **CloudQueue.GetMessage** метод делает hello другой код, чтение сообщений, чтобы никакой другой код можно изменить или удалить сообщение hello при к обработке сообщений невидимым для tooany 30 секунд (по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="da553-201">hello **CloudQueue.GetMessage** method makes hello message invisible for 30 seconds (by default) tooany other code reading messages so that no other code can modify or delete hello message while your processing it.</span></span> <span data-ttu-id="da553-202">объем времени приветственное сообщение hello toochange выполняется без внешних проявлений, измените hello **visibilityTimeout** параметром, передаваемым toohello **CloudQueue.GetMessage** метод.</span><span class="sxs-lookup"><span data-stu-id="da553-202">toochange hello amount of time hello message is invisible, modify hello **visibilityTimeout** parameter being passed toohello **CloudQueue.GetMessage** method.</span></span>

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. <span data-ttu-id="da553-203">Вызовите hello **CloudQueueMessage.Delete** метод toodelete приветственное сообщение из очереди hello.</span><span class="sxs-lookup"><span data-stu-id="da553-203">Call hello **CloudQueueMessage.Delete** method toodelete hello message from hello queue.</span></span>

    ```csharp
    queue.DeleteMessage(message);
    ```

1. <span data-ttu-id="da553-204">Обновление hello **ViewBag** hello сообщение удалено, а hello имя очереди hello.</span><span class="sxs-lookup"><span data-stu-id="da553-204">Update hello **ViewBag** with hello message deleted, and hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. <span data-ttu-id="da553-205">В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **очереди**и в контекстном меню hello выберите **Добавить -> Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="da553-205">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="da553-206">На hello **добавить представление** диалоговое окно, введите **ReadMessage** hello имя представления, а также выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="da553-206">On hello **Add View** dialog, enter **ReadMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="da553-207">Откройте `ReadMessage.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="da553-207">Open `ReadMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "ReadMessage";
    }
    
    <h2>Read Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Read (and Deleted) Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>
    ```

1. <span data-ttu-id="da553-208">В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="da553-208">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="da553-209">После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="da553-209">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. <span data-ttu-id="da553-210">Запустите приложение hello и выберите **чтение и удаление сообщений** toosee результаты, аналогичные toohello следующий снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="da553-210">Run hello application, and select **Read/Delete message** toosee results similar toohello following screen shot:</span></span>
  
    ![Чтение и удаление сообщения](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a><span data-ttu-id="da553-212">Получает длину очереди hello</span><span class="sxs-lookup"><span data-stu-id="da553-212">Get hello queue length</span></span>

<span data-ttu-id="da553-213">В этом разделе показано, как tooget hello длина очереди (число сообщений).</span><span class="sxs-lookup"><span data-stu-id="da553-213">This section illustrates how tooget hello queue length (number of messages).</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="da553-214">В этом разделе предполагается шаги hello [настроить среду разработки hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="da553-214">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="da553-215">Откройте hello `QueuesController.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="da553-215">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="da553-216">Добавьте метод **GetQueueLength**, который возвращает **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="da553-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="da553-217">В пределах hello **ReadMessage** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="da553-217">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="da553-218">Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)</span><span class="sxs-lookup"><span data-stu-id="da553-218">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="da553-219">Получите объект **CloudQueueClient**, представляющий клиента службы очередей.</span><span class="sxs-lookup"><span data-stu-id="da553-219">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="da553-220">Получить **CloudQueueContainer** , представляющий toohello ссылка на очередь.</span><span class="sxs-lookup"><span data-stu-id="da553-220">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="da553-221">Вызовите hello **CloudQueue.FetchAttributes** атрибуты метода tooretrieve hello очереди (в том числе его длина).</span><span class="sxs-lookup"><span data-stu-id="da553-221">Call hello **CloudQueue.FetchAttributes** method tooretrieve hello queue's attributes (including its length).</span></span> 

    ```csharp
    queue.FetchAttributes();
    ```

6. <span data-ttu-id="da553-222">Hello доступа **CloudQueue.ApproximateMessageCount** длина очереди для свойства tooget hello.</span><span class="sxs-lookup"><span data-stu-id="da553-222">Access hello **CloudQueue.ApproximateMessageCount** property tooget hello queue's length.</span></span>
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. <span data-ttu-id="da553-223">Обновление hello **ViewBag** с именем hello hello очереди и ее длину.</span><span class="sxs-lookup"><span data-stu-id="da553-223">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. <span data-ttu-id="da553-224">В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **очереди**и в контекстном меню hello выберите **Добавить -> Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="da553-224">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="da553-225">На hello **добавить представление** диалоговое окно, введите **GetQueueLength** hello имя представления, а также выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="da553-225">On hello **Add View** dialog, enter **GetQueueLength** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="da553-226">Откройте `GetQueueLengthMessage.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="da553-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. <span data-ttu-id="da553-227">В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="da553-227">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="da553-228">После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="da553-228">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. <span data-ttu-id="da553-229">Запустите приложение hello и выберите **длина очереди получения** toosee результаты, аналогичные toohello следующий снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="da553-229">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![Получение длины очереди](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a><span data-ttu-id="da553-231">Удаление очереди</span><span class="sxs-lookup"><span data-stu-id="da553-231">Delete a queue</span></span>
<span data-ttu-id="da553-232">В этом разделе показано, как toodelete очереди.</span><span class="sxs-lookup"><span data-stu-id="da553-232">This section illustrates how toodelete a queue.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="da553-233">В этом разделе предполагается шаги hello [настроить среду разработки hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="da553-233">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="da553-234">Откройте hello `QueuesController.cs` файла.</span><span class="sxs-lookup"><span data-stu-id="da553-234">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="da553-235">Добавьте метод **DeleteQueue**, который возвращает **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="da553-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="da553-236">В пределах hello **DeleteQueue** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="da553-236">Within hello **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="da553-237">Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)</span><span class="sxs-lookup"><span data-stu-id="da553-237">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="da553-238">Получите объект **CloudQueueClient**, представляющий клиента службы очередей.</span><span class="sxs-lookup"><span data-stu-id="da553-238">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="da553-239">Получить **CloudQueueContainer** , представляющий toohello ссылка на очередь.</span><span class="sxs-lookup"><span data-stu-id="da553-239">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="da553-240">Вызовите hello **CloudQueue.Delete** очереди hello toodelete метод, представленный hello **CloudQueue** объекта.</span><span class="sxs-lookup"><span data-stu-id="da553-240">Call hello **CloudQueue.Delete** method toodelete hello queue represented by hello **CloudQueue** object.</span></span>

    ```csharp
    queue.Delete();
    ```

1. <span data-ttu-id="da553-241">Обновление hello **ViewBag** с именем hello hello очереди и ее длину.</span><span class="sxs-lookup"><span data-stu-id="da553-241">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. <span data-ttu-id="da553-242">В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **очереди**и в контекстном меню hello выберите **Добавить -> Просмотр**.</span><span class="sxs-lookup"><span data-stu-id="da553-242">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="da553-243">На hello **добавить представление** диалоговое окно, введите **DeleteQueue** hello имя представления, а также выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="da553-243">On hello **Add View** dialog, enter **DeleteQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="da553-244">Откройте `DeleteQueue.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="da553-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. <span data-ttu-id="da553-245">В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="da553-245">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="da553-246">После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="da553-246">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. <span data-ttu-id="da553-247">Запустите приложение hello и выберите **длина очереди получения** toosee результаты, аналогичные toohello следующий снимок экрана:</span><span class="sxs-lookup"><span data-stu-id="da553-247">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![Удаление очереди.](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a><span data-ttu-id="da553-249">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="da553-249">Next steps</span></span>
<span data-ttu-id="da553-250">Просмотрите дополнительные toolearn функция руководства о дополнительных параметрах для хранения данных в Azure.</span><span class="sxs-lookup"><span data-stu-id="da553-250">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="da553-251">Приступая к работе с хранилищем BLOB-объектов Azure и подключенными службами Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="da553-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="da553-252">Начало работы с хранилищем таблиц Azure и подключенными службами Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="da553-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-tables.md)
