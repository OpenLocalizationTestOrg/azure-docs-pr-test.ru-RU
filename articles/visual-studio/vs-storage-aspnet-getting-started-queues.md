---
title: "aaaGet к работе с хранилищем очередей Azure и Visual Studio подключения службы (ASP.NET) | Документы Microsoft"
description: "Как tooget запущена с помощью хранилища очередей Azure в проект ASP.NET в Visual Studio после подключения tooa учетной записи хранилища с помощью Visual Studio подключенные службы"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94ca3413-5497-433f-abbe-836f83a9de72
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/23/2016
ms.author: kraigb
ms.openlocfilehash: 415a437c4ce60b1e2e328f8e937c73b0d5c50e78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a>Приступая к работе с хранилищем очередей Azure и подключенными службами Visual Studio (ASP.NET)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Обзор

Хранилище очередей Azure — это служба, обеспечивающая обмен сообщениями в облаке между компонентами приложения. При разработке приложений для масштабирования компоненты приложения часто не связаны между собой, так что они могут масштабироваться независимо друг от друга. Хранилище очередей обеспечивает асинхронный обмен сообщениями для взаимодействия между компонентами приложения, ли они выполняются в облаке hello, на рабочем столе hello, на локальном сервере или на мобильном устройстве. Хранилище очередей также поддерживает управление асинхронными задачами и создание рабочих процессов.

В этом учебнике показано, как toowrite ASP.NET кода в некоторых распространенных сценариях, с помощью сущностей хранилища очереди Azure. Сюда относятся такие задачи, как создание очереди Azure, а также добавление, изменение, чтение и удаление сообщений очереди.

##<a name="prerequisites"></a>Предварительные требования

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Учетная запись хранения Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Создание контроллера MVC 

1. В hello **обозревателе решений**, щелкните правой кнопкой мыши **контроллеров**и в контекстном меню hello, выберите **Добавить -> контроллер**.

    ![Добавление контроллера tooan приложение ASP.NET MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. На hello **Добавление формирования шаблонов** диалогового окна выберите **контроллер MVC 5 - пустой**и выберите **добавить**.

    ![Выбор типа контроллера MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. На hello **добавления контроллера** диалогового окна, имя контроллера hello *QueuesController*и выберите **добавить**.

    ![Имя контроллера MVC hello](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. Добавьте следующее hello *с помощью* toohello директивы `QueuesController.cs` файла:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a>Создать очередь

Hello ниже показано, как toocreate очереди:

> [!NOTE]
> 
> В этом разделе предполагается шаги hello [настроить среду разработки hello](#set-up-the-development-environment). 

1. Откройте hello `QueuesController.cs` файла. 

1. Добавьте метод **CreateQueue**, который возвращает **ActionResult**.

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. В пределах hello **CreateQueue** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения. Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Получите объект **CloudQueueClient**, представляющий клиента службы очередей.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. Получить **CloudQueue** , представляющий имя нужной очереди toohello ссылки. Hello **CloudQueueClient.GetQueueReference** метод не выполняет запрос к очереди хранилища. независимо от того, имеется ли hello очередь существует, возвращается ссылка Hello. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Вызовите hello **CloudQueue.CreateIfNotExists** метод toocreate hello очереди, если она еще не существует. Hello **CloudQueue.CreateIfNotExists** возвращает **true** Если hello очередь не существует и успешно создан. В противном случае возвращается значение **false**.    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. Обновление hello **ViewBag** с именем hello hello очереди.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **очереди**и в контекстном меню hello выберите **Добавить -> Просмотр**.

1. На hello **добавить представление** диалоговое окно, введите **CreateQueue** hello имя представления, а также выберите **добавить**.

1. Откройте `CreateQueue.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.

1. После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. Запустите приложение hello и выберите **создать очередь** toosee результаты, аналогичные toohello следующий снимок экрана:
  
    ![Создание очереди](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    Как упоминалось ранее, hello **CloudQueue.CreateIfNotExists** возвращает **true** только когда hello очередь не существует и создается. Таким образом, если при запуске приложение hello hello очередь существует, метод hello возвращает **false**. приложение hello toorun несколько раз, необходимо удалить очередь hello перед повторным запуском приложения hello. Удаление очереди hello можно сделать с помощью hello **CloudQueue.Delete** метод. Можно также удалить очередь hello, с помощью hello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) или hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="add-a-message-tooa-queue"></a>Добавить tooa очереди сообщений

После [была создана очередь](#create-a-queue), можно добавить toothat сообщений в очереди. В этом разделе описывается добавление очередью сообщений tooa *тестировать очередь*. 

> [!NOTE]
> 
> В этом разделе предполагается шаги hello [настроить среду разработки hello](#set-up-the-development-environment). 

1. Откройте hello `QueuesController.cs` файла.

1. Добавьте метод **AddMessage**, который возвращает **ActionResult**.

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. В пределах hello **AddMessage** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения. Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Получите объект **CloudQueueClient**, представляющий клиента службы очередей.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Получить **CloudQueueContainer** , представляющий toohello ссылка на очередь. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Создать hello **CloudQueueMessage** объект, представляющий сообщение hello tooadd toohello очереди. Для создания объекта **CloudQueueMessage** можно использовать либо строку (в формате UTF-8), либо массив типа byte.

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. Вызовите hello **CloudQueue.AddMessage** метод tooadd hello корреляции toohello очереди.

    ```csharp
    queue.AddMessage(message);
    ```

1. Создайте и задайте несколько **ViewBag** свойства для отображения в представлении hello.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **очереди**и в контекстном меню hello выберите **Добавить -> Просмотр**.

1. На hello **добавить представление** диалоговое окно, введите **AddMessage** hello имя представления, а также выберите **добавить**.

1. Откройте `AddMessage.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.

1. После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. Запустите приложение hello и выберите **добавить сообщение** toosee результаты, аналогичные toohello следующий снимок экрана:
  
    ![Добавление сообщения](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

Здравствуйте, два раздела - [чтения сообщения из очереди, не удаляя его](#read-a-message-from-a-queue-without-removing-it) и [чтение и удаление сообщения из очереди](#read-and-remove-a-message-from-a-queue) -показывают, как tooread сообщений из очереди.  

## <a name="read-a-message-from-a-queue-without-removing-it"></a>Чтение сообщения из очереди, не удаляя его

В этом разделе показано, как toopeek в сообщение из очереди (чтения hello первого сообщения без его удаления).  

> [!NOTE]
> 
> В этом разделе предполагается шаги hello [настроить среду разработки hello](#set-up-the-development-environment). 

1. Откройте hello `QueuesController.cs` файла.

1. Добавьте метод **PeekMessage**, который возвращает **ActionResult**.

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. В пределах hello **PeekMessage** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения. Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Получите объект **CloudQueueClient**, представляющий клиента службы очередей.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Получить **CloudQueueContainer** , представляющий toohello ссылка на очередь. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Вызовите hello **CloudQueue.PeekMessage** метод tooread hello первого сообщения в очереди hello, не удаляя его из очереди hello. 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. Обновление hello **ViewBag** с двумя значениями: имя очереди hello и приветственное сообщение, которое было прочитано. Hello **CloudQueueMessage** объект предоставляет два свойства для получения значения hello объекта: **CloudQueueMessage.AsBytes** и **CloudQueueMessage.AsString**. **AsString** (который используется в этом примере) возвращает строку, а **AsBytes** возвращает массив байтов.

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **очереди**и в контекстном меню hello выберите **Добавить -> Просмотр**.

1. На hello **добавить представление** диалоговое окно, введите **PeekMessage** hello имя представления, а также выберите **добавить**.

1. Откройте `PeekMessage.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:

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

1. В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.

1. После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. Запустите приложение hello и выберите **считывания сообщения** toosee результаты, аналогичные toohello следующий снимок экрана:
  
    ![Просмотр сообщения](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a>Чтение и удаление сообщения из очереди

В этом разделе вы узнаете, как tooread и удалять сообщение из очереди.   

> [!NOTE]
> 
> В этом разделе предполагается шаги hello [настроить среду разработки hello](#set-up-the-development-environment). 

1. Откройте hello `QueuesController.cs` файла.

1. Добавьте метод **ReadMessage**, который возвращает **ActionResult**.

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. В пределах hello **ReadMessage** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения. Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Получите объект **CloudQueueClient**, представляющий клиента службы очередей.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Получить **CloudQueueContainer** , представляющий toohello ссылка на очередь. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Вызовите hello **CloudQueue.GetMessage** метод tooread hello первого сообщения в очереди hello. Hello **CloudQueue.GetMessage** метод делает hello другой код, чтение сообщений, чтобы никакой другой код можно изменить или удалить сообщение hello при к обработке сообщений невидимым для tooany 30 секунд (по умолчанию). объем времени приветственное сообщение hello toochange выполняется без внешних проявлений, измените hello **visibilityTimeout** параметром, передаваемым toohello **CloudQueue.GetMessage** метод.

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. Вызовите hello **CloudQueueMessage.Delete** метод toodelete приветственное сообщение из очереди hello.

    ```csharp
    queue.DeleteMessage(message);
    ```

1. Обновление hello **ViewBag** hello сообщение удалено, а hello имя очереди hello.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **очереди**и в контекстном меню hello выберите **Добавить -> Просмотр**.

1. На hello **добавить представление** диалоговое окно, введите **ReadMessage** hello имя представления, а также выберите **добавить**.

1. Откройте `ReadMessage.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:

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

1. В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.

1. После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. Запустите приложение hello и выберите **чтение и удаление сообщений** toosee результаты, аналогичные toohello следующий снимок экрана:
  
    ![Чтение и удаление сообщения](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a>Получает длину очереди hello

В этом разделе показано, как tooget hello длина очереди (число сообщений). 

> [!NOTE]
> 
> В этом разделе предполагается шаги hello [настроить среду разработки hello](#set-up-the-development-environment). 

1. Откройте hello `QueuesController.cs` файла.

1. Добавьте метод **GetQueueLength**, который возвращает **ActionResult**.

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. В пределах hello **ReadMessage** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения. Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Получите объект **CloudQueueClient**, представляющий клиента службы очередей.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Получить **CloudQueueContainer** , представляющий toohello ссылка на очередь. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Вызовите hello **CloudQueue.FetchAttributes** атрибуты метода tooretrieve hello очереди (в том числе его длина). 

    ```csharp
    queue.FetchAttributes();
    ```

6. Hello доступа **CloudQueue.ApproximateMessageCount** длина очереди для свойства tooget hello.
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. Обновление hello **ViewBag** с именем hello hello очереди и ее длину.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **очереди**и в контекстном меню hello выберите **Добавить -> Просмотр**.

1. На hello **добавить представление** диалоговое окно, введите **GetQueueLength** hello имя представления, а также выберите **добавить**.

1. Откройте `GetQueueLengthMessage.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.

1. После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. Запустите приложение hello и выберите **длина очереди получения** toosee результаты, аналогичные toohello следующий снимок экрана:
  
    ![Получение длины очереди](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a>Удаление очереди
В этом разделе показано, как toodelete очереди. 

> [!NOTE]
> 
> В этом разделе предполагается шаги hello [настроить среду разработки hello](#set-up-the-development-environment). 

1. Откройте hello `QueuesController.cs` файла.

1. Добавьте метод **DeleteQueue**, который возвращает **ActionResult**.

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. В пределах hello **DeleteQueue** метода получения **CloudStorageAccount** , представляющий сведения об учетной записи хранения. Используйте hello следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello: (изменение  *&lt;имя учетной записи хранения >* toohello имя hello хранилища Azure Учетная запись, которой осуществляется доступ.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Получите объект **CloudQueueClient**, представляющий клиента службы очередей.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Получить **CloudQueueContainer** , представляющий toohello ссылка на очередь. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Вызовите hello **CloudQueue.Delete** очереди hello toodelete метод, представленный hello **CloudQueue** объекта.

    ```csharp
    queue.Delete();
    ```

1. Обновление hello **ViewBag** с именем hello hello очереди и ее длину.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. В hello **обозреватель решений**, разверните hello **представления** папку, щелкните правой кнопкой мыши **очереди**и в контекстном меню hello выберите **Добавить -> Просмотр**.

1. На hello **добавить представление** диалоговое окно, введите **DeleteQueue** hello имя представления, а также выберите **добавить**.

1. Откройте `DeleteQueue.cshtml`и измените его, чтобы он выглядел hello, следующий фрагмент кода:

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. В hello **обозревателе решений**, разверните hello **представления -> Shared** , а откройте `_Layout.cshtml`.

1. После hello последнего **Html.ActionLink**, добавьте следующее hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. Запустите приложение hello и выберите **длина очереди получения** toosee результаты, аналогичные toohello следующий снимок экрана:
  
    ![Удаление очереди.](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите дополнительные toolearn функция руководства о дополнительных параметрах для хранения данных в Azure.

  * [Приступая к работе с хранилищем BLOB-объектов Azure и подключенными службами Visual Studio (ASP.NET)](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [Начало работы с хранилищем таблиц Azure и подключенными службами Visual Studio (ASP.NET)](vs-storage-aspnet-getting-started-tables.md)
