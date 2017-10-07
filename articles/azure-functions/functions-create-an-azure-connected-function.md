---
title: "aaaCreate функцию, которая подключается tooAzure services | Документы Microsoft"
description: "Использовать функции Azure toocreate без сервера приложение, которое подключается tooother Azure службы."
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
ms.openlocfilehash: 9d1f7d3b236f8d2c1a404c76aee410f6d458fb7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-toocreate-a-function-that-connects-tooother-azure-services"></a><span data-ttu-id="05160-104">Использовать функции Azure toocreate функцию, которая подключается tooother Azure службы</span><span class="sxs-lookup"><span data-stu-id="05160-104">Use Azure Functions toocreate a function that connects tooother Azure services</span></span>

<span data-ttu-id="05160-105">В этом разделе показано, как функции в функции Azure, ожидающий toomessages на хранилища Azure, очереди и копии hello toocreate сообщения toorows в таблице хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="05160-105">This topic shows you how toocreate a function in Azure Functions that listens toomessages on an Azure Storage queue and copies hello messages toorows in an Azure Storage table.</span></span> <span data-ttu-id="05160-106">Таймер запускается функция является используется tooload сообщения в очередь hello.</span><span class="sxs-lookup"><span data-stu-id="05160-106">A timer triggered function is used tooload messages into hello queue.</span></span> <span data-ttu-id="05160-107">Вторая функция считывает из очереди hello и записывает сообщения toohello таблицы.</span><span class="sxs-lookup"><span data-stu-id="05160-107">A second function reads from hello queue and writes messages toohello table.</span></span> <span data-ttu-id="05160-108">Hello очереди и таблицы hello создаются автоматически на основе hello привязки определений функций Azure.</span><span class="sxs-lookup"><span data-stu-id="05160-108">Both hello queue and hello table are created for you by Azure Functions based on hello binding definitions.</span></span> 

<span data-ttu-id="05160-109">наиболее интересных вещей toomake, одна функция написан на языке JavaScript и другие hello записывается в скрипт C#.</span><span class="sxs-lookup"><span data-stu-id="05160-109">toomake things more interesting, one function is written in JavaScript and hello other is written in C# script.</span></span> <span data-ttu-id="05160-110">На этом примере показано, что приложение-функция может содержать функции на разных языках.</span><span class="sxs-lookup"><span data-stu-id="05160-110">This demonstrates how a function app can have functions in various languages.</span></span> 

<span data-ttu-id="05160-111">Этот сценарий можно просмотреть в [видеоролике на сайте Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span><span class="sxs-lookup"><span data-stu-id="05160-111">You can see this scenario demonstrated in a [video on Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span></span>

## <a name="create-a-function-that-writes-toohello-queue"></a><span data-ttu-id="05160-112">Создайте функцию, которая записывает toohello очереди</span><span class="sxs-lookup"><span data-stu-id="05160-112">Create a function that writes toohello queue</span></span>

<span data-ttu-id="05160-113">Перед подключением tooa очередь хранилища необходимо toocreate функцию, которая загружает очереди сообщений hello.</span><span class="sxs-lookup"><span data-stu-id="05160-113">Before you can connect tooa storage queue, you need toocreate a function that loads hello message queue.</span></span> <span data-ttu-id="05160-114">Эта функция JavaScript использует триггер таймера, который записывает toohello очереди сообщений каждые 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="05160-114">This JavaScript function uses a timer trigger that writes a message toohello queue every 10 seconds.</span></span> <span data-ttu-id="05160-115">Если у вас еще нет учетной записи Azure, извлечь hello [повторите функции Azure](https://functions.azure.com/try) возникают, или [создать бесплатную учетную запись Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="05160-115">If you don't already have an Azure account, check out hello [Try Azure Functions](https://functions.azure.com/try) experience, or [create your free Azure account](https://azure.microsoft.com/free/).</span></span>

1. <span data-ttu-id="05160-116">Вернитесь к toohello портал Azure и найдите функции приложения.</span><span class="sxs-lookup"><span data-stu-id="05160-116">Go toohello Azure portal and locate your function app.</span></span>

2. <span data-ttu-id="05160-117">Щелкните **Новая функция** > **TimerTrigger-JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="05160-117">Click **New Function** > **TimerTrigger-JavaScript**.</span></span> 

3. <span data-ttu-id="05160-118">Имя функции hello **FunctionsBindingsDemo1**, введите значение выражения cron `0/10 * * * * *` для **расписания**, а затем нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="05160-118">Name hello function **FunctionsBindingsDemo1**, enter a cron expression value of `0/10 * * * * *` for **Schedule**, and then click **Create**.</span></span>
   
    ![Добавление функции, активируемой с помощью таймера](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    <span data-ttu-id="05160-120">Вы создали функцию, активируемую с помощью таймера, которая запускается каждые 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="05160-120">You have now created a timer triggered function that runs every 10 seconds.</span></span>

5. <span data-ttu-id="05160-121">На hello **разработка** щелкните **журналы** и просмотреть в журнале hello hello.</span><span class="sxs-lookup"><span data-stu-id="05160-121">On hello **Develop** tab, click **Logs** and view hello activity in hello log.</span></span> <span data-ttu-id="05160-122">Каждые 10 секунд в журнале будет появляться запись.</span><span class="sxs-lookup"><span data-stu-id="05160-122">You see a log entry written every 10 seconds.</span></span>
   
    ![Просмотр работы функции hello tooverify журнала hello](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a><span data-ttu-id="05160-124">Добавление выходной привязки очереди сообщений</span><span class="sxs-lookup"><span data-stu-id="05160-124">Add a message queue output binding</span></span>

1. <span data-ttu-id="05160-125">На hello **Интеграция** выберите **новый Выход** > **хранилища очередей Azure** > **выберите**.</span><span class="sxs-lookup"><span data-stu-id="05160-125">On hello **Integrate** tab, choose **New Output** > **Azure Queue Storage** > **Select**.</span></span>

    ![Добавление функции триггера с таймером](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. <span data-ttu-id="05160-127">Введите `myQueueItem` для **имя параметра сообщение** и `functions-bindings` для **имя очереди**, выберите существующую **подключения к учетной записи хранилища** или нажмите кнопку **новый** toocreate хранилища учетной записи подключения и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="05160-127">Enter `myQueueItem` for **Message parameter name** and `functions-bindings` for **Queue name**, select an existing **Storage account connection** or click **new** toocreate a storage account connection, and then click **Save**.</span></span>  

    ![Создание hello выходные данные привязки toohello хранилища очереди](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. <span data-ttu-id="05160-129">Вернитесь в hello **разработка** вкладку, добавьте следующие функции toohello кода hello:</span><span class="sxs-lookup"><span data-stu-id="05160-129">Back in hello **Develop** tab, append hello following code toohello function:</span></span>
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. <span data-ttu-id="05160-130">Найдите hello *Если* инструкции около строки 9 функции hello и вставки hello следующий код после этого оператора.</span><span class="sxs-lookup"><span data-stu-id="05160-130">Locate hello *if* statement around line 9 of hello function, and insert hello following code after that statement.</span></span>
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    <span data-ttu-id="05160-131">Этот код создает **myQueueItem** и задает его **время** Текущая отметка времени toohello свойство.</span><span class="sxs-lookup"><span data-stu-id="05160-131">This code creates a **myQueueItem** and sets its **time** property toohello current timeStamp.</span></span> <span data-ttu-id="05160-132">Затем он добавляет hello новой очереди toohello контекстного элемента **myQueueItem** привязки.</span><span class="sxs-lookup"><span data-stu-id="05160-132">It then adds hello new queue item toohello context's **myQueueItem** binding.</span></span>

3. <span data-ttu-id="05160-133">Щелкните **Сохранить и запустить**.</span><span class="sxs-lookup"><span data-stu-id="05160-133">Click **Save and Run**.</span></span>

## <a name="view-storage-updates-by-using-storage-explorer"></a><span data-ttu-id="05160-134">Просмотр обновлений хранилища с помощью обозревателя службы хранилища</span><span class="sxs-lookup"><span data-stu-id="05160-134">View storage updates by using Storage Explorer</span></span>
<span data-ttu-id="05160-135">Можно проверить работоспособность функции, просматривая сообщения в очереди hello, которую вы создали.</span><span class="sxs-lookup"><span data-stu-id="05160-135">You can verify that your function is working by viewing messages in hello queue you created.</span></span>  <span data-ttu-id="05160-136">Очередь хранилища tooyour можно подключиться с помощью Cloud Explorer в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="05160-136">You can connect tooyour storage queue by using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="05160-137">Однако портал hello делает его учетной записи хранилища tooyour легко tooconnect, используя обозреватель хранилищ Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="05160-137">However, hello portal makes it easy tooconnect tooyour storage account by using Microsoft Azure Storage Explorer.</span></span>

1. <span data-ttu-id="05160-138">В hello **Интеграция** щелкните очереди привязка для вывода > **документации**, Показать hello строку подключения для вашей учетной записи хранилища и скопируйте значение hello.</span><span class="sxs-lookup"><span data-stu-id="05160-138">In hello **Integrate** tab, click your queue output binding > **Documentation**, then unhide hello Connection String for your storage account and copy hello value.</span></span> <span data-ttu-id="05160-139">Можно использовать учетную запись хранения tooconnect tooyour это значение.</span><span class="sxs-lookup"><span data-stu-id="05160-139">You use this value tooconnect tooyour storage account.</span></span>

    ![Скачивание обозревателя службы хранилища Azure](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. <span data-ttu-id="05160-141">Если это еще не сделано, скачайте и установите [обозреватель службы хранилища Microsoft Azure](http://storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="05160-141">If you haven't already done so, download and install [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span></span> 
 
3. <span data-ttu-id="05160-142">В обозревателе хранилищ щелкните hello tooAzure хранилища значок подключения, вставьте строку подключения hello в поле hello и мастером hello.</span><span class="sxs-lookup"><span data-stu-id="05160-142">In Storage Explorer, click hello connect tooAzure Storage icon, paste hello connection string in hello field, and complete hello wizard.</span></span>

    ![Добавление подключения в обозревателе службы хранилища](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. <span data-ttu-id="05160-144">В разделе **локальной и вложенных**, разверните **учетные записи хранения** > учетной записи хранилища > **очереди** > **функции привязок**и убедитесь, что сообщения записываются toohello очереди.</span><span class="sxs-lookup"><span data-stu-id="05160-144">Under **Local and attached**, expand **Storage Accounts** > your storage account > **Queues** > **functions-bindings** and verify that messages are written toohello queue.</span></span>

    ![Представление сообщений в очереди hello](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    <span data-ttu-id="05160-146">Hello очередь не существует или является пустым, существует ли скорее проблема с привязка функции или кода.</span><span class="sxs-lookup"><span data-stu-id="05160-146">If hello queue does not exist or is empty, there is most likely a problem with your function binding or code.</span></span>

## <a name="create-a-function-that-reads-from-hello-queue"></a><span data-ttu-id="05160-147">Создайте функцию, которая считывает из очереди hello</span><span class="sxs-lookup"><span data-stu-id="05160-147">Create a function that reads from hello queue</span></span>

<span data-ttu-id="05160-148">Теперь, когда добавляется toohello очереди сообщений, можно создать другую функцию, которая считывает из очереди hello и hello записи без возможности восстановления сообщения tooan таблице хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="05160-148">Now that you have messages being added toohello queue, you can create another function that reads from hello queue and writes hello messages permanently tooan Azure Storage table.</span></span>

1. <span data-ttu-id="05160-149">Щелкните **Новая функция** > **QueueTrigger-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="05160-149">Click **New Function** > **QueueTrigger-CSharp**.</span></span> 
 
2. <span data-ttu-id="05160-150">Имя функции hello `FunctionsBindingsDemo2`, введите **функции привязок** в hello **имя очереди** поля, выберите существующую учетную запись хранения или создайте его и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="05160-150">Name hello function `FunctionsBindingsDemo2`, enter **functions-bindings** in hello **Queue name** field, select an existing storage account or create one, and then click **Create**.</span></span>

    ![Добавление функции таймера выходной очереди](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. <span data-ttu-id="05160-152">(Необязательно) Можно проверить работоспособность новой функции hello, просмотрев hello новую очередь в обозревателе хранилищ как перед.</span><span class="sxs-lookup"><span data-stu-id="05160-152">(Optional) You can verify that hello new function works by viewing hello new queue in Storage Explorer as before.</span></span> <span data-ttu-id="05160-153">Кроме того, можно использовать Cloud Explorer в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="05160-153">You can also use Cloud Explorer in Visual Studio.</span></span>  

4. <span data-ttu-id="05160-154">(Необязательно) Обновить hello **функции привязок** очередь и обратите внимание, что элементы были удалены из очереди hello.</span><span class="sxs-lookup"><span data-stu-id="05160-154">(Optional) Refresh hello **functions-bindings** queue and notice that items have been removed from hello queue.</span></span> <span data-ttu-id="05160-155">Hello удаления возникает из-за функции hello привязанного toohello **функции привязок** очередь, так как очередь hello считывает входной функции триггер и hello.</span><span class="sxs-lookup"><span data-stu-id="05160-155">hello removal occurs because hello function is bound toohello **functions-bindings** queue as an input trigger and hello function reads hello queue.</span></span> 
 
## <a name="add-a-table-output-binding"></a><span data-ttu-id="05160-156">Добавление выходной привязки таблицы</span><span class="sxs-lookup"><span data-stu-id="05160-156">Add a table output binding</span></span>

1. <span data-ttu-id="05160-157">В FunctionsBindingsDemo2 щелкните **Интегрировать** > **Новые выходные данные** > **Хранилище таблиц Azure** > **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="05160-157">In FunctionsBindingsDemo2, click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

    ![Добавление таблицы привязки tooan хранилища Azure](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. <span data-ttu-id="05160-159">Введите `functionbindings` в поле **Имя таблицы** и `myTable` — в поле **Имя параметра таблицы**, выберите **подключение к учетной записи хранения** или создайте его и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="05160-159">Enter `functionbindings` for **Table name** and `myTable` for **Table parameter name**, choose a **Storage account connection** or create a new one, and then click **Save**.</span></span>

    ![Настройка привязки таблицы хранилища hello](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. <span data-ttu-id="05160-161">В hello **разработка** вкладки, замените существующий код функции hello hello следующее:</span><span class="sxs-lookup"><span data-stu-id="05160-161">In hello **Develop** tab, replace hello existing function code with hello following:</span></span>
   
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
        
        // Add hello item toohello table binding collection.
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
    <span data-ttu-id="05160-162">Hello **TableItem** класса представляет строку в таблицу хранилища hello и добавить элемент toohello hello `myTable` коллекцию **TableItem** объектов.</span><span class="sxs-lookup"><span data-stu-id="05160-162">hello **TableItem** class represents a row in hello storage table, and you add hello item toohello `myTable` collection of **TableItem** objects.</span></span> <span data-ttu-id="05160-163">Необходимо задать hello **PartitionKey** и **RowKey** свойства toobe может tooinsert в таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="05160-163">You must set hello **PartitionKey** and **RowKey** properties toobe able tooinsert into hello table.</span></span>

4. <span data-ttu-id="05160-164">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="05160-164">Click **Save**.</span></span>  <span data-ttu-id="05160-165">Наконец можно проверить работы функции hello, просмотреть таблицу hello в обозреватель хранилищ или Visual Studio Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="05160-165">Finally, you can verify hello function works by viewing hello table in Storage explorer or Visual Studio Cloud Explorer.</span></span>

5. <span data-ttu-id="05160-166">(Необязательно) В вашей учетной записи хранения в обозревателе хранилищ разверните **таблиц** > **functionsbindings** и убедитесь, что toohello таблицы добавляются строки.</span><span class="sxs-lookup"><span data-stu-id="05160-166">(Optional) In your storage account in Storage Explorer, expand **Tables** > **functionsbindings** and verify that rows are added toohello table.</span></span> <span data-ttu-id="05160-167">Можно сделать же hello в Cloud Explorer в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="05160-167">You can do hello same in Cloud Explorer in Visual Studio.</span></span>

    ![Просмотр строк в таблице hello](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    <span data-ttu-id="05160-169">Hello таблицы не существует или является пустым, существует ли скорее проблема с привязка функции или кода.</span><span class="sxs-lookup"><span data-stu-id="05160-169">If hello table does not exist or is empty, there is most likely a problem with your function binding or code.</span></span> 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a><span data-ttu-id="05160-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="05160-170">Next steps</span></span>
<span data-ttu-id="05160-171">Дополнительные сведения о функциях Azure см. в разделе hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="05160-171">For more information about Azure Functions, see hello following topics:</span></span>

* [<span data-ttu-id="05160-172">Справочник разработчика по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="05160-172">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="05160-173">Справочник программиста по созданию функций, а также определению триггеров и привязок.</span><span class="sxs-lookup"><span data-stu-id="05160-173">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="05160-174">Testing Azure Functions</span><span class="sxs-lookup"><span data-stu-id="05160-174">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="05160-175">(Тестирование функций Azure) Описание различных средств и методов тестирования функций.</span><span class="sxs-lookup"><span data-stu-id="05160-175">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="05160-176">Как tooscale функции Azure</span><span class="sxs-lookup"><span data-stu-id="05160-176">How tooscale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="05160-177">Описание функций Azure, включая план размещения потребления hello и как toochoose hello продуманный план планов обслуживания.</span><span class="sxs-lookup"><span data-stu-id="05160-177">Discusses service plans available with Azure Functions, including hello Consumption hosting plan, and how toochoose hello right plan.</span></span> 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

