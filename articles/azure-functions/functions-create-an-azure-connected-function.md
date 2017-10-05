---
title: "Создание функции, которая подключается к службам Azure | Документация Майкрософт"
description: "Используйте службу функций Azure для создания бессерверных приложений, которые подключаются к другим службам Azure."
services: functions
documentationcenter: dev-center-name
author: yochay
manager: manager-alias
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, веб-перехватчики, динамические вычисления, независимая архитектура"
ms.assetid: ab86065d-6050-46c9-a336-1bfc1fa4b5a1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 65964a322f0adab4f648fb350bedb77b46bf9054
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-functions-to-create-a-function-that-connects-to-other-azure-services"></a><span data-ttu-id="7f6b7-104">Создание функции, которая подключается к другим службам Azure, с помощью службы функций Azure</span><span class="sxs-lookup"><span data-stu-id="7f6b7-104">Use Azure Functions to create a function that connects to other Azure services</span></span>

<span data-ttu-id="7f6b7-105">В этой статье показано, как создать функцию в службе функций Azure, прослушивающую сообщения в очереди службы хранилища Azure и копирующую их в строки таблицы в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-105">This topic shows you how to create a function in Azure Functions that listens to messages on an Azure Storage queue and copies the messages to rows in an Azure Storage table.</span></span> <span data-ttu-id="7f6b7-106">Функция, активируемая с помощью таймера, используется для загрузки сообщений в очередь.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-106">A timer triggered function is used to load messages into the queue.</span></span> <span data-ttu-id="7f6b7-107">Вторая функция считывает из очереди и записывает сообщения в таблицу.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-107">A second function reads from the queue and writes messages to the table.</span></span> <span data-ttu-id="7f6b7-108">Функции Azure создают очередь и таблицу автоматически на основе определений привязки.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-108">Both the queue and the table are created for you by Azure Functions based on the binding definitions.</span></span> 

<span data-ttu-id="7f6b7-109">Чтобы усложнить задачу, одна функция написана на языке JavaScript, а другая — с использованием скрипта C#.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-109">To make things more interesting, one function is written in JavaScript and the other is written in C# script.</span></span> <span data-ttu-id="7f6b7-110">На этом примере показано, что приложение-функция может содержать функции на разных языках.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-110">This demonstrates how a function app can have functions in various languages.</span></span> 

<span data-ttu-id="7f6b7-111">Этот сценарий можно просмотреть в [видеоролике на сайте Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span><span class="sxs-lookup"><span data-stu-id="7f6b7-111">You can see this scenario demonstrated in a [video on Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span></span>

## <a name="create-a-function-that-writes-to-the-queue"></a><span data-ttu-id="7f6b7-112">Создание функции, выполняющей запись в очередь</span><span class="sxs-lookup"><span data-stu-id="7f6b7-112">Create a function that writes to the queue</span></span>

<span data-ttu-id="7f6b7-113">Перед подключением к очереди хранилища необходимо создать функцию, загружающую очередь сообщений.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-113">Before you can connect to a storage queue, you need to create a function that loads the message queue.</span></span> <span data-ttu-id="7f6b7-114">Эта функция JavaScript использует триггер с таймером, записывающий сообщение в очередь каждые 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-114">This JavaScript function uses a timer trigger that writes a message to the queue every 10 seconds.</span></span> <span data-ttu-id="7f6b7-115">Если у вас нет учетной записи Azure, попробуйте использовать [Функции Azure](https://functions.azure.com/try) или [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="7f6b7-115">If you don't already have an Azure account, check out the [Try Azure Functions](https://functions.azure.com/try) experience, or [create your free Azure account](https://azure.microsoft.com/free/).</span></span>

1. <span data-ttu-id="7f6b7-116">Войдите на портал Azure и найдите свое приложение-функцию.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-116">Go to the Azure portal and locate your function app.</span></span>

2. <span data-ttu-id="7f6b7-117">Щелкните **Новая функция** > **TimerTrigger-JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-117">Click **New Function** > **TimerTrigger-JavaScript**.</span></span> 

3. <span data-ttu-id="7f6b7-118">Присвойте функции имя **FunctionsBindingsDemo1**, введите значение выражения CRON `0/10 * * * * *` в поле **Расписание** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-118">Name the function **FunctionsBindingsDemo1**, enter a cron expression value of `0/10 * * * * *` for **Schedule**, and then click **Create**.</span></span>
   
    ![Добавление функции, активируемой с помощью таймера](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    <span data-ttu-id="7f6b7-120">Вы создали функцию, активируемую с помощью таймера, которая запускается каждые 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-120">You have now created a timer triggered function that runs every 10 seconds.</span></span>

5. <span data-ttu-id="7f6b7-121">На вкладке **Разработка** щелкните **Журналы** и просмотрите действия в журнале.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-121">On the **Develop** tab, click **Logs** and view the activity in the log.</span></span> <span data-ttu-id="7f6b7-122">Каждые 10 секунд в журнале будет появляться запись.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-122">You see a log entry written every 10 seconds.</span></span>
   
    ![Просмотр журнала для проверки выполнения функции](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a><span data-ttu-id="7f6b7-124">Добавление выходной привязки очереди сообщений</span><span class="sxs-lookup"><span data-stu-id="7f6b7-124">Add a message queue output binding</span></span>

1. <span data-ttu-id="7f6b7-125">На вкладке **Интегрировать** выберите **Новые выходные данные** > **Хранилище очередей Azure** > **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-125">On the **Integrate** tab, choose **New Output** > **Azure Queue Storage** > **Select**.</span></span>

    ![Добавление функции триггера с таймером](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. <span data-ttu-id="7f6b7-127">Введите `myQueueItem` в поле **Имя параметра сообщения** и `functions-bindings` — в поле **Имя очереди**. Выберите существующее **подключение к учетной записи хранения** или щелкните **new** (создать), чтобы создать подключение к учетной записи хранения, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-127">Enter `myQueueItem` for **Message parameter name** and `functions-bindings` for **Queue name**, select an existing **Storage account connection** or click **new** to create a storage account connection, and then click **Save**.</span></span>  

    ![Создание выходной привязки для очереди хранилища](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. <span data-ttu-id="7f6b7-129">Вернитесь к вкладке **Разработка** и добавьте следующий код в функцию:</span><span class="sxs-lookup"><span data-stu-id="7f6b7-129">Back in the **Develop** tab, append the following code to the function:</span></span>
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. <span data-ttu-id="7f6b7-130">Найдите оператор *if* в строке 9 функции и вставьте после него следующий оператор.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-130">Locate the *if* statement around line 9 of the function, and insert the following code after that statement.</span></span>
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    <span data-ttu-id="7f6b7-131">Этот код создает элемент **myQueueItem** и задает для его свойства **time** текущую метку времени.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-131">This code creates a **myQueueItem** and sets its **time** property to the current timeStamp.</span></span> <span data-ttu-id="7f6b7-132">Затем он добавляет новый элемент очереди в привязку **myQueue** контекста.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-132">It then adds the new queue item to the context's **myQueueItem** binding.</span></span>

3. <span data-ttu-id="7f6b7-133">Щелкните **Сохранить и запустить**.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-133">Click **Save and Run**.</span></span>

## <a name="view-storage-updates-by-using-storage-explorer"></a><span data-ttu-id="7f6b7-134">Просмотр обновлений хранилища с помощью обозревателя службы хранилища</span><span class="sxs-lookup"><span data-stu-id="7f6b7-134">View storage updates by using Storage Explorer</span></span>
<span data-ttu-id="7f6b7-135">Выполнение функции можно проверить, просмотрев сообщения в созданной очереди.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-135">You can verify that your function is working by viewing messages in the queue you created.</span></span>  <span data-ttu-id="7f6b7-136">Подключиться к очереди хранилища можно с помощью Cloud Explorer в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-136">You can connect to your storage queue by using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="7f6b7-137">Тем не менее благодаря обозревателю службы хранилища Microsoft Azure подключение к учетной записи хранения на портале упрощено.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-137">However, the portal makes it easy to connect to your storage account by using Microsoft Azure Storage Explorer.</span></span>

1. <span data-ttu-id="7f6b7-138">На вкладке **Интегрировать** щелкните выходную привязку очереди и элемент **Документация**, раскройте узел со строкой подключения для учетной записи хранения и скопируйте значение.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-138">In the **Integrate** tab, click your queue output binding > **Documentation**, then unhide the Connection String for your storage account and copy the value.</span></span> <span data-ttu-id="7f6b7-139">Это значение используется для подключения к учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-139">You use this value to connect to your storage account.</span></span>

    ![Скачивание обозревателя службы хранилища Azure](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. <span data-ttu-id="7f6b7-141">Если это еще не сделано, скачайте и установите [обозреватель службы хранилища Microsoft Azure](http://storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="7f6b7-141">If you haven't already done so, download and install [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span></span> 
 
3. <span data-ttu-id="7f6b7-142">В обозревателе службы хранилища щелкните значок для подключения к службе хранилища Azure, вставьте строку подключения в поле и завершите работу с мастером.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-142">In Storage Explorer, click the connect to Azure Storage icon, paste the connection string in the field, and complete the wizard.</span></span>

    ![Добавление подключения в обозревателе службы хранилища](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. <span data-ttu-id="7f6b7-144">В разделе **Local and attached** (Локальные и присоединенные) разверните узел **Учетные записи хранения** > ваша учетная запись хранения > **Очереди** > **functions-bindings** и убедитесь, что сообщения записываются в очередь.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-144">Under **Local and attached**, expand **Storage Accounts** > your storage account > **Queues** > **functions-bindings** and verify that messages are written to the queue.</span></span>

    ![Просмотр сообщений в очереди](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    <span data-ttu-id="7f6b7-146">Если очередь не существует или она пустая, скорее всего, произошла проблема с привязкой или кодом функции.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-146">If the queue does not exist or is empty, there is most likely a problem with your function binding or code.</span></span>

## <a name="create-a-function-that-reads-from-the-queue"></a><span data-ttu-id="7f6b7-147">Создание функции, выполняющей чтение из очереди</span><span class="sxs-lookup"><span data-stu-id="7f6b7-147">Create a function that reads from the queue</span></span>

<span data-ttu-id="7f6b7-148">Создав функцию для добавления сообщений в очередь, можно создать другую функцию, выполняющую чтение из очереди и окончательную запись сообщений в таблицы службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-148">Now that you have messages being added to the queue, you can create another function that reads from the queue and writes the messages permanently to an Azure Storage table.</span></span>

1. <span data-ttu-id="7f6b7-149">Щелкните **Новая функция** > **QueueTrigger-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-149">Click **New Function** > **QueueTrigger-CSharp**.</span></span> 
 
2. <span data-ttu-id="7f6b7-150">Присвойте функции имя `FunctionsBindingsDemo2`, введите **functions-bindings** в поле **Имя очереди**, выберите существующую учетную запись хранения или создайте ее и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-150">Name the function `FunctionsBindingsDemo2`, enter **functions-bindings** in the **Queue name** field, select an existing storage account or create one, and then click **Create**.</span></span>

    ![Добавление функции таймера выходной очереди](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. <span data-ttu-id="7f6b7-152">(Необязательно.) Вы можете проверить, выполняется ли новая функция, просмотрев новую очередь в обозревателе службы хранилища, как и раньше.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-152">(Optional) You can verify that the new function works by viewing the new queue in Storage Explorer as before.</span></span> <span data-ttu-id="7f6b7-153">Кроме того, можно использовать Cloud Explorer в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-153">You can also use Cloud Explorer in Visual Studio.</span></span>  

4. <span data-ttu-id="7f6b7-154">(Необязательно.) Обновите очередь **functions-bindings**. Обратите внимание, что элементы удалены из очереди.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-154">(Optional) Refresh the **functions-bindings** queue and notice that items have been removed from the queue.</span></span> <span data-ttu-id="7f6b7-155">Это происходит, так как функция привязана к очереди **functions-bindings** в качестве входного триггера и она считывает очередь.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-155">The removal occurs because the function is bound to the **functions-bindings** queue as an input trigger and the function reads the queue.</span></span> 
 
## <a name="add-a-table-output-binding"></a><span data-ttu-id="7f6b7-156">Добавление выходной привязки таблицы</span><span class="sxs-lookup"><span data-stu-id="7f6b7-156">Add a table output binding</span></span>

1. <span data-ttu-id="7f6b7-157">В FunctionsBindingsDemo2 щелкните **Интегрировать** > **Новые выходные данные** > **Хранилище таблиц Azure** > **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-157">In FunctionsBindingsDemo2, click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

    ![Добавление привязки в таблицу службы хранилища Azure](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. <span data-ttu-id="7f6b7-159">Введите `functionbindings` в поле **Имя таблицы** и `myTable` — в поле **Имя параметра таблицы**, выберите **подключение к учетной записи хранения** или создайте его и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-159">Enter `functionbindings` for **Table name** and `myTable` for **Table parameter name**, choose a **Storage account connection** or create a new one, and then click **Save**.</span></span>

    ![Настройка привязки таблицы службы хранилища](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. <span data-ttu-id="7f6b7-161">На вкладке **Разработка** замените имеющийся код функции на приведенный ниже:</span><span class="sxs-lookup"><span data-stu-id="7f6b7-161">In the **Develop** tab, replace the existing function code with the following:</span></span>
   
    ```cs
    
    using System;
    
    public static void Run(QItem myQueueItem, ICollector<TableItem> myTable, TraceWriter log)
    {    
        TableItem myItem = new TableItem
        {
            PartitionKey = "key",
            RowKey = Guid.NewGuid().ToString(),
            Time = DateTime.Now.ToString("hh.mm.ss.ffffff"),
            Msg = myQueueItem.Msg,
            OriginalTime = myQueueItem.Time    
        };
        
        // Add the item to the table binding collection.
        myTable.Add(myItem);
    
        log.Verbose($"C# Queue trigger function processed: {myItem.RowKey} | {myItem.Msg} | {myItem.Time}");
    }
    
    public class TableItem
    {
        public string PartitionKey {get; set;}
        public string RowKey {get; set;}
        public string Time {get; set;}
        public string Msg {get; set;}
        public string OriginalTime {get; set;}
    }
    
    public class QItem
    {
        public string Msg { get; set;}
        public string Time { get; set;}
    }
    ```
    <span data-ttu-id="7f6b7-162">Класс **TableItem** представляет собой строку в таблице службы хранилища. Добавьте элемент в коллекцию `myTable` объектов **TableItem**.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-162">The **TableItem** class represents a row in the storage table, and you add the item to the `myTable` collection of **TableItem** objects.</span></span> <span data-ttu-id="7f6b7-163">Необходимо задать свойства **PartitionKey** и **RowKey** для вставки в таблицу.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-163">You must set the **PartitionKey** and **RowKey** properties to be able to insert into the table.</span></span>

4. <span data-ttu-id="7f6b7-164">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-164">Click **Save**.</span></span>  <span data-ttu-id="7f6b7-165">Вы можете проверить, выполняется ли функция, просмотрев таблицу в обозревателе службы хранилищ или Cloud Explorer в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-165">Finally, you can verify the function works by viewing the table in Storage explorer or Visual Studio Cloud Explorer.</span></span>

5. <span data-ttu-id="7f6b7-166">(Необязательно.) В учетной записи хранения в обозревателе службы хранилища разверните узел **Таблицы** > **functionsbindings** и убедитесь, что строки добавляются в таблицу.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-166">(Optional) In your storage account in Storage Explorer, expand **Tables** > **functionsbindings** and verify that rows are added to the table.</span></span> <span data-ttu-id="7f6b7-167">Это также можно сделать в Cloud Explorer в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-167">You can do the same in Cloud Explorer in Visual Studio.</span></span>

    ![Просмотр строк в таблице](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    <span data-ttu-id="7f6b7-169">Если таблица не существует или она пустая, скорее всего, произошла проблема с привязкой или кодом функции.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-169">If the table does not exist or is empty, there is most likely a problem with your function binding or code.</span></span> 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a><span data-ttu-id="7f6b7-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7f6b7-170">Next steps</span></span>
<span data-ttu-id="7f6b7-171">Дополнительные сведения о функциях Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="7f6b7-171">For more information about Azure Functions, see the following topics:</span></span>

* [<span data-ttu-id="7f6b7-172">Справочник разработчика по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="7f6b7-172">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="7f6b7-173">Справочник программиста по созданию функций, а также определению триггеров и привязок.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-173">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="7f6b7-174">Testing Azure Functions</span><span class="sxs-lookup"><span data-stu-id="7f6b7-174">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="7f6b7-175">Описание различных средств и методов тестирования функций.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-175">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="7f6b7-176">Масштабирование функций Azure</span><span class="sxs-lookup"><span data-stu-id="7f6b7-176">How to scale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="7f6b7-177">Обсуждение планов обслуживания, доступных для использования с функциями Azure (включая план потребления), а также выбор подходящего плана.</span><span class="sxs-lookup"><span data-stu-id="7f6b7-177">Discusses service plans available with Azure Functions, including the Consumption hosting plan, and how to choose the right plan.</span></span> 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

