---
title: "Stream Analytics: обработка в реальном времени для функций Azure | Документация Майкрософт"
description: "Узнайте, как использовать функцию Azure, подключенную к очереди служебной шины, для заполнения кэша Redis для Azure выходными данными задания Stream Analytics."
keywords: "Поток данных, кэш Redis, очередь служебной шины"
services: stream-analytics
author: ryancrawcour
manager: jhubbard
documentationcenter: 
ms.assetid: d428bb33-4244-4001-b93d-c77bed816527
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: ryancraw
ms.openlocfilehash: ad14cc858ff513573e2718a26a9ab5c524e1adc6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-store-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a><span data-ttu-id="d7f71-104">Как сохранять данные из Azure Stream Analytics в кэш Redis для Azure с помощью функций Azure</span><span class="sxs-lookup"><span data-stu-id="d7f71-104">How to store data from Azure Stream Analytics in an Azure Redis Cache using Azure Functions</span></span>
<span data-ttu-id="d7f71-105">Azure Stream Analytics обеспечивает быстрое развертывание и внедрение бюджетных аналитических решений для анализа в реальном времени данных с устройств, датчиков, из инфраструктуры и приложений, а также любого потока данных.</span><span class="sxs-lookup"><span data-stu-id="d7f71-105">Azure Stream Analytics lets you rapidly develop and deploy low-cost solutions to gain real-time insights from devices, sensors, infrastructure, and applications, or any stream of data.</span></span> <span data-ttu-id="d7f71-106">Azure Stream Analytics обеспечивает различные варианты использования, в том числе управление и мониторинг в реальном времени, контроль и управление, обнаружение мошенничества, автомобили с сетевыми возможностями и многое другое.</span><span class="sxs-lookup"><span data-stu-id="d7f71-106">It enables various use cases such as real-time management and monitoring, command and control, fraud detection, connected cars and many more.</span></span> <span data-ttu-id="d7f71-107">Во многих подобных сценариях может потребоваться сохранять данные, выдаваемые Azure Stream Analytics, в распределенном хранилище данных, например кэш Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f71-107">In many such scenarios, you may want to store data outputted by Azure Stream Analytics into a distributed data store such as an Azure Redis cache.</span></span>

<span data-ttu-id="d7f71-108">Предположим, что вы работаете в телекоммуникационной компании.</span><span class="sxs-lookup"><span data-stu-id="d7f71-108">Suppose you are part of a telecommunications company.</span></span> <span data-ttu-id="d7f71-109">Вы пытаетесь обнаружить мошенничество с SIM-картами, при котором один человек выполняет несколько вызовов в одно и то же время, но из разных географических расположений.</span><span class="sxs-lookup"><span data-stu-id="d7f71-109">You are trying to detect SIM fraud where multiple calls coming from the same identity, at the same time, but in different geographically locations.</span></span> <span data-ttu-id="d7f71-110">Перед вами поставили задачу сохранять все потенциальные мошеннические телефонные звонки в кэше Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f71-110">You are tasked with storing all the potential fraudulent phone calls in an Azure Redis cache.</span></span> <span data-ttu-id="d7f71-111">В этом блоге мы опишем, как можно легко выполнить вашу задачу.</span><span class="sxs-lookup"><span data-stu-id="d7f71-111">In this blog, we provide guidance on how you can easily complete your task.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d7f71-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d7f71-112">Prerequisites</span></span>
<span data-ttu-id="d7f71-113">Изучите пошаговое руководство по [выявлению мошенничества в реальном времени][fraud-detection] для ASA.</span><span class="sxs-lookup"><span data-stu-id="d7f71-113">Complete the [Real-time Fraud Detection][fraud-detection] walk-through for ASA</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="d7f71-114">Общие сведения об архитектуре</span><span class="sxs-lookup"><span data-stu-id="d7f71-114">Architecture Overview</span></span>
![Снимок экрана: архитектура](./media/stream-analytics-functions-redis/architecture-overview.png)

<span data-ttu-id="d7f71-116">Как показано на предыдущем рисунке, Stream Analytics позволяет запрашивать потоковые входные данные и отправлять в качестве выходных данных.</span><span class="sxs-lookup"><span data-stu-id="d7f71-116">As shown in the preceding figure, Stream Analytics allows streaming input data to be queried and sent to an output.</span></span> <span data-ttu-id="d7f71-117">Затем, в зависимости от выходных данных, функции Azure могут активировать события определенного типа.</span><span class="sxs-lookup"><span data-stu-id="d7f71-117">Based on the output, Azure Functions can then trigger some type of event.</span></span> 

<span data-ttu-id="d7f71-118">В этом блоге мы рассмотрим функции Azure, входящие в этот конвейер, а точнее — активацию события, которое сохраняет мошеннические данные в кэш.</span><span class="sxs-lookup"><span data-stu-id="d7f71-118">In this blog, we focus on the Azure Functions part of this pipeline, or more specifically the triggering of an event that stores fraudulent data into the cache.</span></span>
<span data-ttu-id="d7f71-119">После изучения руководства [Приступая к работе с Azure Stream Analytics: выявление мошенничества в режиме реального времени][fraud-detection] у вас должны быть уже настроены рабочие входные данные (концентратор событий), запрос и выходные данные (хранилище BLOB-объектов).</span><span class="sxs-lookup"><span data-stu-id="d7f71-119">After completing the [Real-time Fraud Detection][fraud-detection] tutorial, you have an input (an event hub), a query, and an output (blob storage) already configured and running.</span></span> <span data-ttu-id="d7f71-120">В этом блоге мы изменим выходные данные, чтобы вместо них использовать очередь служебной шины.</span><span class="sxs-lookup"><span data-stu-id="d7f71-120">In this blog, we change the output to use a Service Bus Queue instead.</span></span> <span data-ttu-id="d7f71-121">После этого мы подключим функцию Azure к этой очереди.</span><span class="sxs-lookup"><span data-stu-id="d7f71-121">After that, we connect an Azure Function to this queue.</span></span> 

## <a name="create-and-connect-a-service-bus-queue-output"></a><span data-ttu-id="d7f71-122">Создание и подключение выходных данных очереди служебной шины</span><span class="sxs-lookup"><span data-stu-id="d7f71-122">Create and connect a Service Bus Queue output</span></span>
<span data-ttu-id="d7f71-123">Чтобы создать очередь служебной шины, выполните шаги 1 и 2 раздела о .NET статьи [Начало работы с очередями служебной шины][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="d7f71-123">To create a Service Bus Queue, follow steps 1 and 2 of the .NET section in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span>
<span data-ttu-id="d7f71-124">Теперь подключим очередь к заданию Stream Analytics, которое было создано в более раннем пошаговом руководстве по выявлению мошенничества.</span><span class="sxs-lookup"><span data-stu-id="d7f71-124">Now let's connect the queue to the Stream Analytics job that was created in the earlier fraud detection walk-through.</span></span>

1. <span data-ttu-id="d7f71-125">На портале Azure перейдите к колонке **Выходные данные** своего задания и выберите **Добавить** в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="d7f71-125">In the Azure portal, go to the **Outputs** blade of your job and select **Add** at the top of the page.</span></span>
   
    ![Добавление выходных данных](./media/stream-analytics-functions-redis/adding-outputs.png)
2. <span data-ttu-id="d7f71-127">Выберите значение **Очередь служебной шины** для параметра **Приемник** и следуйте инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="d7f71-127">Choose **Service Bus Queue** as the **Sink** and follow the instructions on the screen.</span></span> <span data-ttu-id="d7f71-128">Обязательно выберите пространство имен очереди служебной шины, созданное при изучении руководства [Начало работы с очередями служебной шины][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="d7f71-128">Be sure to choose the namespace of the Service Bus Queue you created in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span> <span data-ttu-id="d7f71-129">По завершении нажмите кнопку со стрелкой вправо.</span><span class="sxs-lookup"><span data-stu-id="d7f71-129">Click the "right" button when you are finished.</span></span>
3. <span data-ttu-id="d7f71-130">Укажите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="d7f71-130">Specify the following values:</span></span>
   
   * <span data-ttu-id="d7f71-131">**Формат сериализатора событий**: JSON;</span><span class="sxs-lookup"><span data-stu-id="d7f71-131">**Event Serializer Format**: JSON</span></span>
   * <span data-ttu-id="d7f71-132">**Кодировка**: UTF8.</span><span class="sxs-lookup"><span data-stu-id="d7f71-132">**Encoding**: UTF8</span></span>
   * <span data-ttu-id="d7f71-133">**ФОРМАТ**: строки-разделители.</span><span class="sxs-lookup"><span data-stu-id="d7f71-133">**FORMAT**: Line separated</span></span>
4. <span data-ttu-id="d7f71-134">Нажмите кнопку **Создать** , чтобы добавить этот источник и убедиться, что служба Stream Analytics может успешно подключаться к учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="d7f71-134">Click the **Create** button to add this source and to verify that Stream Analytics can successfully connect to the storage account.</span></span>
5. <span data-ttu-id="d7f71-135">На вкладке **Запрос** замените текущий запрос следующим.</span><span class="sxs-lookup"><span data-stu-id="d7f71-135">In the **Query** tab, replace the current query with the following.</span></span> <span data-ttu-id="d7f71-136">Замените *[YOUR SERVICE BUS NAME]* именем выходных данных, созданных на шаге 3.</span><span class="sxs-lookup"><span data-stu-id="d7f71-136">Replace *[YOUR SERVICE BUS NAME] * with the output name you created in step 3.</span></span> 
   
    ```    
   
        SELECT 
            System.Timestamp as Time, CS1.CallingIMSI, CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, CS1.SwitchNum as Switch1, CS2.SwitchNum as Switch2
   
        INTO [YOUR SERVICE BUS NAME]
   
        FROM CallStream CS1 TIMESTAMP BY CallRecTime
        JOIN CallStream CS2 TIMESTAMP BY CallRecTime
            ON CS1.CallingIMSI = CS2.CallingIMSI AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5
   
        WHERE CS1.SwitchNum != CS2.SwitchNum
   
    ```

## <a name="create-an-azure-redis-cache"></a><span data-ttu-id="d7f71-137">Создание кэша Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="d7f71-137">Create an Azure Redis Cache</span></span>
<span data-ttu-id="d7f71-138">Создайте кэш Redis для Azure, следуя указаниям из раздела о .NET статьи [Как использовать кэш Redis для Azure][use-rediscache] вплоть до раздела ***Настройка клиентов кэша***.</span><span class="sxs-lookup"><span data-stu-id="d7f71-138">Create an Azure Redis cache by following the .NET section in [How to Use Azure Redis Cache][use-rediscache] until the section called ***Configure the cache clients***.</span></span>
<span data-ttu-id="d7f71-139">После выполнения всех указаний у вас будет новый кэш Redis.</span><span class="sxs-lookup"><span data-stu-id="d7f71-139">Once complete, you have a new Redis Cache.</span></span> <span data-ttu-id="d7f71-140">В разделе **Все параметры** выберите **Ключи доступа** и запишите значение ***Первичная строка подключения***.</span><span class="sxs-lookup"><span data-stu-id="d7f71-140">Under **All settings**, select **Access keys** and note down the ***Primary connection string***.</span></span>

![Снимок экрана: архитектура](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a><span data-ttu-id="d7f71-142">Создание функции Azure</span><span class="sxs-lookup"><span data-stu-id="d7f71-142">Create an Azure Function</span></span>
<span data-ttu-id="d7f71-143">Следуйте указаниям руководства [Создание первой функции Azure][functions-getstarted], чтобы начать работу с Функциями Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f71-143">Follow [Create your first Azure Function][functions-getstarted] tutorial to get started with Azure Functions.</span></span> <span data-ttu-id="d7f71-144">Если у вас уже имеется функция Azure, которую вы бы хотели использовать, перейдите к разделу [Запись в кэш Redis](#Writing-to-Redis-Cache)</span><span class="sxs-lookup"><span data-stu-id="d7f71-144">If you already have an Azure function you would like to use, then skip ahead to [Writing to Redis Cache](#Writing-to-Redis-Cache)</span></span>

1. <span data-ttu-id="d7f71-145">На портале выберите "Службы приложений" в области навигации слева, затем щелкните имя своего приложения-функции Azure, чтобы получить веб-сайт приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="d7f71-145">In the portal, select App Services from the left-hand navigation, then click your Azure function app name to get to the Function's app website.</span></span>
    <span data-ttu-id="d7f71-146">![Снимок экрана: список функций службы приложений](./media/stream-analytics-functions-redis/app-services-function-list.png)</span><span class="sxs-lookup"><span data-stu-id="d7f71-146">![Screenshot of app services function list](./media/stream-analytics-functions-redis/app-services-function-list.png)</span></span>
2. <span data-ttu-id="d7f71-147">Щелкните **Создать функцию > ServiceBusQueueTrigger — C#**.</span><span class="sxs-lookup"><span data-stu-id="d7f71-147">Click **New Function > ServiceBusQueueTrigger – C#**.</span></span> <span data-ttu-id="d7f71-148">Для заполнения следующих полей выполните приведенные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="d7f71-148">For the following fields, follow these instructions:</span></span>
   
   * <span data-ttu-id="d7f71-149">**Имя очереди.** Имя, введенное при создании очереди в руководстве [Начало работы с очередями служебной шины][servicebus-getstarted] (не имя служебной шины).</span><span class="sxs-lookup"><span data-stu-id="d7f71-149">**Queue name**: The same name as the name you entered when you created the queue in [Get Started with Service Bus Queues][servicebus-getstarted] (not the name of the service bus).</span></span> <span data-ttu-id="d7f71-150">Убедитесь, что используется очередь, подключенная к выходным данным Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="d7f71-150">Make sure you use the queue that is connected to the Stream Analytics output.</span></span>
   * <span data-ttu-id="d7f71-151">**Подключение к служебной шине.** Выберите **Добавить строку подключения**.</span><span class="sxs-lookup"><span data-stu-id="d7f71-151">**Service Bus connection**: Select **Add a connection string**.</span></span> <span data-ttu-id="d7f71-152">Чтобы найти строку подключения, перейдите на классический портал, выберите **Служебная шина**, а затем выберите служебную шину, которую вы создали, и щелкните **Сведения о подключении** в нижней части экрана.</span><span class="sxs-lookup"><span data-stu-id="d7f71-152">To find the connection string, go to the classic portal, select **Service Bus**, the service bus you created, and **CONNECTION INFORMATION** at the bottom of the screen.</span></span> <span data-ttu-id="d7f71-153">Убедитесь, что на этой странице отображается главный экран.</span><span class="sxs-lookup"><span data-stu-id="d7f71-153">Make sure you are on the main screen on this page.</span></span> <span data-ttu-id="d7f71-154">Скопируйте и вставьте строку подключения.</span><span class="sxs-lookup"><span data-stu-id="d7f71-154">Copy and paste the connection string.</span></span> <span data-ttu-id="d7f71-155">Вы можете ввести любое имя подключения.</span><span class="sxs-lookup"><span data-stu-id="d7f71-155">Feel free to enter any connection name.</span></span>
     
       ![Снимок экрана: подключение к служебной шине](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * <span data-ttu-id="d7f71-157">**AccessRights**: выберите **Управление**.</span><span class="sxs-lookup"><span data-stu-id="d7f71-157">**AccessRights**: Choose **Manage**</span></span>
3. <span data-ttu-id="d7f71-158">Нажмите кнопку **Создать**</span><span class="sxs-lookup"><span data-stu-id="d7f71-158">Click **Create**</span></span>

## <a name="writing-to-redis-cache"></a><span data-ttu-id="d7f71-159">Запись в кэш Redis</span><span class="sxs-lookup"><span data-stu-id="d7f71-159">Writing to Redis Cache</span></span>
<span data-ttu-id="d7f71-160">Мы создали функцию Azure, которая считывает данные из очереди служебной шины.</span><span class="sxs-lookup"><span data-stu-id="d7f71-160">We have now created an Azure Function that reads from a Service Bus Queue.</span></span> <span data-ttu-id="d7f71-161">Все, что осталось сделать, — использовать нашу функцию для записи данных в кэш Redis.</span><span class="sxs-lookup"><span data-stu-id="d7f71-161">All that is left to do is use our Function to write this data to the Redis Cache.</span></span> 

1. <span data-ttu-id="d7f71-162">Выберите только что созданный **ServiceBusQueueTrigger** и щелкните **Параметры приложения-функции** в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="d7f71-162">Select your newly created **ServiceBusQueueTrigger**, and click **Function app settings** on the top right corner.</span></span> <span data-ttu-id="d7f71-163">Выберите **Перейти к параметрам службы приложений > Параметры > Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="d7f71-163">Select **Go to App Service Settings > Settings > Application settings**</span></span>
2. <span data-ttu-id="d7f71-164">В разделе "Строка подключения" создайте имя в разделе **Имя** .</span><span class="sxs-lookup"><span data-stu-id="d7f71-164">In the Connection strings section, create a name in the **Name** section.</span></span> <span data-ttu-id="d7f71-165">Вставьте первичную строку подключения, записанную на шаге **Создание кэша Redis**, в раздел **Значение**.</span><span class="sxs-lookup"><span data-stu-id="d7f71-165">Paste the primary connection string you found in the **Create a Redis Cache** step into the **Value** section.</span></span> <span data-ttu-id="d7f71-166">Выберите значение **Пользовательская** из списка со значением **База данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="d7f71-166">Select **Custom** where it says **SQL Database**.</span></span>
3. <span data-ttu-id="d7f71-167">Щелкните **Сохранить** в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="d7f71-167">Click **Save** at the top.</span></span>
   
    ![Снимок экрана: подключение к служебной шине](./media/stream-analytics-functions-redis/function-connection-string.png)
4. <span data-ttu-id="d7f71-169">Теперь вернитесь к параметрам службы приложений и выберите **Инструменты > Редактор службы приложений (предварительная версия) > Вкл. > Перейти**.</span><span class="sxs-lookup"><span data-stu-id="d7f71-169">Now go back to the App Service Settings and select **Tools > App Service Editor (Preview) > On > Go**.</span></span>
   
    ![Снимок экрана: подключение к служебной шине](./media/stream-analytics-functions-redis/app-service-editor.png)
5. <span data-ttu-id="d7f71-171">В редакторе по своему усмотрению создайте JSON-файл **project.json** с приведенным ниже содержимым и сохраните его на локальный диск.</span><span class="sxs-lookup"><span data-stu-id="d7f71-171">In an editor of your choice, create a JSON file named **project.json** with the following and save it to your local disk.</span></span>
   
        {
            "frameworks": {
                "net46": {
                    "dependencies": {
                        "StackExchange.Redis":"1.1.603",
                        "Newtonsoft.Json": "9.0.1"
                    }
                }
            }
        }
6. <span data-ttu-id="d7f71-172">Передайте этот файл в корневой каталог своей функции (не WWWROOT).</span><span class="sxs-lookup"><span data-stu-id="d7f71-172">Upload this file into the root directory of your function (not WWWROOT).</span></span> <span data-ttu-id="d7f71-173">Автоматически должен появиться файл **project.lock.json**. Его появление подтверждает, что пакеты NuGet StackExchange.Redis и Newtonsoft.Json импортированы.</span><span class="sxs-lookup"><span data-stu-id="d7f71-173">You should see a file named **project.lock.json** automatically appear, confirming that the Nuget packages “StackExchange.Redis” and “Newtonsoft.Json” have been imported.</span></span>
7. <span data-ttu-id="d7f71-174">В файле **run.csx** замените предварительно созданный код приведенным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="d7f71-174">In the **run.csx** file, replace the pre-generated code with the following code.</span></span> <span data-ttu-id="d7f71-175">В функции lazyConnection замените CONN NAME именем, созданным на шаге 2 процедуры **сохранения данных в кэш Redis**.</span><span class="sxs-lookup"><span data-stu-id="d7f71-175">In the lazyConnection function, replace “CONN NAME” with the name you created in step 2 of **Store data into the Redis cache**.</span></span>

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers to a property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract the time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using the cache object...
        // Simple put of integral data types into the cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from the cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect to the Service Bus
    private static Lazy<ConnectionMultiplexer> lazyConnection = 
        new Lazy<ConnectionMultiplexer>(() =>
            {
                var cnn = ConfigurationManager.ConnectionStrings["CONN NAME"].ConnectionString
                return ConnectionMultiplexer.Connect();
            });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

````

## <a name="start-the-stream-analytics-job"></a><span data-ttu-id="d7f71-176">Запуск задания Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d7f71-176">Start the Stream Analytics job</span></span>
1. <span data-ttu-id="d7f71-177">Запустите приложение telcodatagen.exe.</span><span class="sxs-lookup"><span data-stu-id="d7f71-177">Start the telcodatagen.exe application.</span></span> <span data-ttu-id="d7f71-178">Оно используется следующим образом. ````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span><span class="sxs-lookup"><span data-stu-id="d7f71-178">The usage is as follows: ````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span></span>
2. <span data-ttu-id="d7f71-179">В колонке задания Stream Analytics на портале щелкните **Запустить** в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="d7f71-179">From the Stream Analytics Job blade in the portal, click **Start** at the top of the page.</span></span>
   
    ![Снимок экрана: запуск задания](./media/stream-analytics-functions-redis/starting-job.png)
3. <span data-ttu-id="d7f71-181">В отобразившейся колонке **Запуск задания** выберите **Сейчас** и нажмите кнопку **Запустить** в нижней части экрана.</span><span class="sxs-lookup"><span data-stu-id="d7f71-181">In the **Start job** blade that appears, select **Now** and then click the **Start** button at the bottom of the screen.</span></span> <span data-ttu-id="d7f71-182">Состояние задания изменится на "Запускается", а спустя некоторое время — на "Выполняется".</span><span class="sxs-lookup"><span data-stu-id="d7f71-182">The job status changes to Starting and after some time changes to Running.</span></span>
   
    ![Снимок экрана: выбора времени начала задания](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a><span data-ttu-id="d7f71-184">Запуск решения и проверка результатов</span><span class="sxs-lookup"><span data-stu-id="d7f71-184">Run solution and check results</span></span>
<span data-ttu-id="d7f71-185">Вернувшись на страницу **ServiceBusQueueTrigger** , вы должны увидеть журнал инструкций.</span><span class="sxs-lookup"><span data-stu-id="d7f71-185">Going back to your **ServiceBusQueueTrigger** page, you should now see log statements.</span></span> <span data-ttu-id="d7f71-186">В этих журналах показано, что данные были получены из очереди служебной шины, помещены в базу данных и получены из нее с использованием времени в качестве ключа!</span><span class="sxs-lookup"><span data-stu-id="d7f71-186">These logs show that you got something from the Service Bus Queue, put it into the database, and fetched it out using the time as the key!</span></span>

<span data-ttu-id="d7f71-187">Чтобы убедиться, что данные находятся в кэше Redis, перейдите на страницу кэша Redis на новом портале (как показано на предыдущем шаге [Создание кэша Redis для Azure](#Create-an-Azure-Redis-Cache) ) и выберите "Консоль".</span><span class="sxs-lookup"><span data-stu-id="d7f71-187">To verify that your data is in your Redis cache, go to your Redis cache page in the new portal (as shown in the preceding [Create an Azure Redis Cache](#Create-an-Azure-Redis-Cache) step) and select Console.</span></span>

<span data-ttu-id="d7f71-188">Теперь можно ввести команды Redis, чтобы убедиться, что данные на самом деле находятся в кэше.</span><span class="sxs-lookup"><span data-stu-id="d7f71-188">Now you can write Redis commands to confirm that data is in fact in the cache.</span></span>

![Снимок экрана: консоль Redis](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a><span data-ttu-id="d7f71-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d7f71-190">Next steps</span></span>
<span data-ttu-id="d7f71-191">Мы рады новым возможностям, которые обеспечивает совместное использование функций Azure и Stream Analytics, и надеемся, что это откроет новые возможности для вас.</span><span class="sxs-lookup"><span data-stu-id="d7f71-191">We’re excited about the new things Azure Functions and Stream analytics can do together, and we hope this unlocks new possibilities for you.</span></span> <span data-ttu-id="d7f71-192">Если вы хотите оставить отзыв о том, что хотели бы получить в дальнейшем, то можете воспользоваться [сайтом Azure UserVoice](https://feedback.azure.com/forums/270577-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="d7f71-192">If you have any feedback on what you want next, feel free to use the [Azure UserVoice site](https://feedback.azure.com/forums/270577-stream-analytics).</span></span>

<span data-ttu-id="d7f71-193">Если вы еще не работали с Microsoft Azure, то мы предлагаем вам ознакомиться с этой средой, зарегистрировавшись для получения [бесплатной пробной учетной записи Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d7f71-193">If you are new Microsoft Azure, we invite you to try it out by signing up for a [free Azure trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="d7f71-194">Если вы не работали со Stream Analytics, то мы предлагаем вам [создать свое первое задание Stream Analytics](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="d7f71-194">If you are new to Stream Analytics, then we invite you to [create your first Stream Analytics job](stream-analytics-create-a-job.md).</span></span>

<span data-ttu-id="d7f71-195">Если вам нужна помощь или ответы на вопросы, напишите об этом на форуме [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) или [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="d7f71-195">If you need any help or have questions, post on [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) or [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forums.</span></span> 

<span data-ttu-id="d7f71-196">Кроме того, вы можете ознакомиться со следующими материалами.</span><span class="sxs-lookup"><span data-stu-id="d7f71-196">You can also see the following resources:</span></span>

* [<span data-ttu-id="d7f71-197">Справочник разработчика по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="d7f71-197">Azure Functions developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="d7f71-198">Справочник разработчика C# по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="d7f71-198">Azure Functions C# developer reference</span></span>](../azure-functions/functions-reference-csharp.md)
* [<span data-ttu-id="d7f71-199">Справочник разработчика F# по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="d7f71-199">Azure Functions F# developer reference</span></span>](../azure-functions/functions-reference-fsharp.md)
* [<span data-ttu-id="d7f71-200">Справочник разработчика NodeJS по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="d7f71-200">Azure Functions NodeJS developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="d7f71-201">Триггеры и привязки в функциях Azure</span><span class="sxs-lookup"><span data-stu-id="d7f71-201">Azure Functions triggers and bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
* [<span data-ttu-id="d7f71-202">Как отслеживать кэш Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="d7f71-202">How to monitor Azure Redis Cache</span></span>](../redis-cache/cache-how-to-monitor.md)

<span data-ttu-id="d7f71-203">Чтобы быть в курсе последних новостей и функций, подпишитесь на [@AzureStreaming](https://twitter.com/AzureStreaming) в Twitter.</span><span class="sxs-lookup"><span data-stu-id="d7f71-203">To stay up-to-date on all the latest news and features, follow [@AzureStreaming](https://twitter.com/AzureStreaming) on Twitter.</span></span>

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
