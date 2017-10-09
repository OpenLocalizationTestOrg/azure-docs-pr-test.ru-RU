---
title: "aaaStream аналитика в реальном времени обработки для функций Azure | Документы Microsoft"
description: "Узнайте, как toouse функцию Azure подключаться очередь Service Bus toopopulate кэша Redis Azure hello в выходных данных задания Stream Analytics."
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
ms.openlocfilehash: 5ef4fe76c2cadf896a80eeaf421f010c315918af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostore-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a><span data-ttu-id="387f5-104">Как toostore данные из Azure Stream Analytics в кэше Redis для Azure с помощью функций Azure</span><span class="sxs-lookup"><span data-stu-id="387f5-104">How toostore data from Azure Stream Analytics in an Azure Redis Cache using Azure Functions</span></span>
<span data-ttu-id="387f5-105">Azure Stream Analytics позволяет быстро разрабатывать и развертывать решения недорогих toogain в режиме реального времени полезных сведений из устройств, датчиков, инфраструктуры и приложений или любой поток данных.</span><span class="sxs-lookup"><span data-stu-id="387f5-105">Azure Stream Analytics lets you rapidly develop and deploy low-cost solutions toogain real-time insights from devices, sensors, infrastructure, and applications, or any stream of data.</span></span> <span data-ttu-id="387f5-106">Azure Stream Analytics обеспечивает различные варианты использования, в том числе управление и мониторинг в реальном времени, контроль и управление, обнаружение мошенничества, автомобили с сетевыми возможностями и многое другое.</span><span class="sxs-lookup"><span data-stu-id="387f5-106">It enables various use cases such as real-time management and monitoring, command and control, fraud detection, connected cars and many more.</span></span> <span data-ttu-id="387f5-107">Во многих таких сценариях может потребоваться toostore данные, выдаваемые Azure Stream Analytics в хранилище распределенных данных, например для кэша Azure Redis.</span><span class="sxs-lookup"><span data-stu-id="387f5-107">In many such scenarios, you may want toostore data outputted by Azure Stream Analytics into a distributed data store such as an Azure Redis cache.</span></span>

<span data-ttu-id="387f5-108">Предположим, что вы работаете в телекоммуникационной компании.</span><span class="sxs-lookup"><span data-stu-id="387f5-108">Suppose you are part of a telecommunications company.</span></span> <span data-ttu-id="387f5-109">Вы пытаетесь toodetect SIM мошенничества, где несколько вызовов, поступающих от hello одинаковый идентификатор, на hello же время, но в разных географически расположения.</span><span class="sxs-lookup"><span data-stu-id="387f5-109">You are trying toodetect SIM fraud where multiple calls coming from hello same identity, at hello same time, but in different geographically locations.</span></span> <span data-ttu-id="387f5-110">Вам нужно хранение всех hello потенциальных мошеннические телефонных звонков в кэш Azure Redis.</span><span class="sxs-lookup"><span data-stu-id="387f5-110">You are tasked with storing all hello potential fraudulent phone calls in an Azure Redis cache.</span></span> <span data-ttu-id="387f5-111">В этом блоге мы опишем, как можно легко выполнить вашу задачу.</span><span class="sxs-lookup"><span data-stu-id="387f5-111">In this blog, we provide guidance on how you can easily complete your task.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="387f5-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="387f5-112">Prerequisites</span></span>
<span data-ttu-id="387f5-113">Полный hello [мошенничества в реальном времени] [ fraud-detection] Пошаговое руководство для ASA</span><span class="sxs-lookup"><span data-stu-id="387f5-113">Complete hello [Real-time Fraud Detection][fraud-detection] walk-through for ASA</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="387f5-114">Общие сведения об архитектуре</span><span class="sxs-lookup"><span data-stu-id="387f5-114">Architecture Overview</span></span>
![Снимок экрана: архитектура](./media/stream-analytics-functions-redis/architecture-overview.png)

<span data-ttu-id="387f5-116">Как показано в предшествующих рисунок hello Stream Analytics позволяет потоковой передачи toobe входных данных запроса и отправляются tooan выходных данных.</span><span class="sxs-lookup"><span data-stu-id="387f5-116">As shown in hello preceding figure, Stream Analytics allows streaming input data toobe queried and sent tooan output.</span></span> <span data-ttu-id="387f5-117">На основании вывода hello, функции Azure можно активировать определенного типа события.</span><span class="sxs-lookup"><span data-stu-id="387f5-117">Based on hello output, Azure Functions can then trigger some type of event.</span></span> 

<span data-ttu-id="387f5-118">В этом блоге мы Обратите внимание на часть функций Azure hello этот конвейер или точнее hello инициацию событие, которое хранит мошеннические данные в кэш hello.</span><span class="sxs-lookup"><span data-stu-id="387f5-118">In this blog, we focus on hello Azure Functions part of this pipeline, or more specifically hello triggering of an event that stores fraudulent data into hello cache.</span></span>
<span data-ttu-id="387f5-119">После завершения hello [мошенничества в реальном времени] [ fraud-detection] учебник, у вас есть входных данных (концентратор событий), запрос и вывод (хранилище blob) уже настроен и запущен.</span><span class="sxs-lookup"><span data-stu-id="387f5-119">After completing hello [Real-time Fraud Detection][fraud-detection] tutorial, you have an input (an event hub), a query, and an output (blob storage) already configured and running.</span></span> <span data-ttu-id="387f5-120">В этом блоге мы изменить toouse вывода hello очередь служебной шины.</span><span class="sxs-lookup"><span data-stu-id="387f5-120">In this blog, we change hello output toouse a Service Bus Queue instead.</span></span> <span data-ttu-id="387f5-121">После этого мы подключаемся к очереди Azure функция toothis.</span><span class="sxs-lookup"><span data-stu-id="387f5-121">After that, we connect an Azure Function toothis queue.</span></span> 

## <a name="create-and-connect-a-service-bus-queue-output"></a><span data-ttu-id="387f5-122">Создание и подключение выходных данных очереди служебной шины</span><span class="sxs-lookup"><span data-stu-id="387f5-122">Create and connect a Service Bus Queue output</span></span>
<span data-ttu-id="387f5-123">toocreate очередь служебной шины, выполните шаги 1 и 2 раздела .NET hello в [начало работы с очередями шины обслуживания][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="387f5-123">toocreate a Service Bus Queue, follow steps 1 and 2 of hello .NET section in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span>
<span data-ttu-id="387f5-124">Теперь подключим задания Stream Analytics toohello очереди hello, созданный в hello руководство по применению предыдущих обнаружения мошенничества.</span><span class="sxs-lookup"><span data-stu-id="387f5-124">Now let's connect hello queue toohello Stream Analytics job that was created in hello earlier fraud detection walk-through.</span></span>

1. <span data-ttu-id="387f5-125">В hello портал Azure, перейдите toohello **выходные данные** колонке задание и выберите **добавить** вверху hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="387f5-125">In hello Azure portal, go toohello **Outputs** blade of your job and select **Add** at hello top of hello page.</span></span>
   
    ![Добавление выходных данных](./media/stream-analytics-functions-redis/adding-outputs.png)
2. <span data-ttu-id="387f5-127">Выберите **очередь Service Bus** как hello **приемника** и следуйте инструкциям, hello на экране приветствия.</span><span class="sxs-lookup"><span data-stu-id="387f5-127">Choose **Service Bus Queue** as hello **Sink** and follow hello instructions on hello screen.</span></span> <span data-ttu-id="387f5-128">Убедиться, что toochoose hello пространство имен hello очереди шины обслуживания можно создать в [начало работы с очередями шины обслуживания][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="387f5-128">Be sure toochoose hello namespace of hello Service Bus Queue you created in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span> <span data-ttu-id="387f5-129">Нажмите кнопку «правый» hello, когда вы закончите.</span><span class="sxs-lookup"><span data-stu-id="387f5-129">Click hello "right" button when you are finished.</span></span>
3. <span data-ttu-id="387f5-130">Укажите hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="387f5-130">Specify hello following values:</span></span>
   
   * <span data-ttu-id="387f5-131">**Формат сериализатора событий**: JSON;</span><span class="sxs-lookup"><span data-stu-id="387f5-131">**Event Serializer Format**: JSON</span></span>
   * <span data-ttu-id="387f5-132">**Кодировка**: UTF8.</span><span class="sxs-lookup"><span data-stu-id="387f5-132">**Encoding**: UTF8</span></span>
   * <span data-ttu-id="387f5-133">**ФОРМАТ**: строки-разделители.</span><span class="sxs-lookup"><span data-stu-id="387f5-133">**FORMAT**: Line separated</span></span>
4. <span data-ttu-id="387f5-134">Нажмите кнопку hello **создать** этого источника и tooverify успешного подключения учетной записи хранилища toohello Stream Analytics, нажмите кнопку tooadd.</span><span class="sxs-lookup"><span data-stu-id="387f5-134">Click hello **Create** button tooadd this source and tooverify that Stream Analytics can successfully connect toohello storage account.</span></span>
5. <span data-ttu-id="387f5-135">В hello **запроса** вкладки, замените следующие hello hello текущего запроса.</span><span class="sxs-lookup"><span data-stu-id="387f5-135">In hello **Query** tab, replace hello current query with hello following.</span></span> <span data-ttu-id="387f5-136">Замените * [имя вашей службы ШИНЫ] * с именем hello выходных данных, созданный на шаге 3.</span><span class="sxs-lookup"><span data-stu-id="387f5-136">Replace *[YOUR SERVICE BUS NAME] * with hello output name you created in step 3.</span></span> 
   
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

## <a name="create-an-azure-redis-cache"></a><span data-ttu-id="387f5-137">Создание кэша Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="387f5-137">Create an Azure Redis Cache</span></span>
<span data-ttu-id="387f5-138">Создать кэш Azure Redis ниже hello .NET раздела [как tooUse кэш Azure Redis] [ use-rediscache] до вызова hello раздел ***Настройка клиентов кэша hello***.</span><span class="sxs-lookup"><span data-stu-id="387f5-138">Create an Azure Redis cache by following hello .NET section in [How tooUse Azure Redis Cache][use-rediscache] until hello section called ***Configure hello cache clients***.</span></span>
<span data-ttu-id="387f5-139">После выполнения всех указаний у вас будет новый кэш Redis.</span><span class="sxs-lookup"><span data-stu-id="387f5-139">Once complete, you have a new Redis Cache.</span></span> <span data-ttu-id="387f5-140">В разделе **все параметры**выберите **ключи доступа** и запишите hello ***основная строка подключения***.</span><span class="sxs-lookup"><span data-stu-id="387f5-140">Under **All settings**, select **Access keys** and note down hello ***Primary connection string***.</span></span>

![Снимок экрана: архитектура](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a><span data-ttu-id="387f5-142">Создание функции Azure</span><span class="sxs-lookup"><span data-stu-id="387f5-142">Create an Azure Function</span></span>
<span data-ttu-id="387f5-143">Выполните [создания вашего первого функции Azure] [ functions-getstarted] tooget учебника работы с функциями Azure.</span><span class="sxs-lookup"><span data-stu-id="387f5-143">Follow [Create your first Azure Function][functions-getstarted] tutorial tooget started with Azure Functions.</span></span> <span data-ttu-id="387f5-144">Если уже имеется функция Azure необходимо как toouse, а затем пропускать слишком[записи tooRedis кэша](#Writing-to-Redis-Cache)</span><span class="sxs-lookup"><span data-stu-id="387f5-144">If you already have an Azure function you would like toouse, then skip ahead too[Writing tooRedis Cache](#Writing-to-Redis-Cache)</span></span>

1. <span data-ttu-id="387f5-145">Hello портала выберите службы приложений hello левой панели навигации, а затем щелкните веб-сайт вашей Azure функция приложения имя tooget toohello функции приложения.</span><span class="sxs-lookup"><span data-stu-id="387f5-145">In hello portal, select App Services from hello left-hand navigation, then click your Azure function app name tooget toohello Function's app website.</span></span>
    <span data-ttu-id="387f5-146">![Снимок экрана: список функций службы приложений](./media/stream-analytics-functions-redis/app-services-function-list.png)</span><span class="sxs-lookup"><span data-stu-id="387f5-146">![Screenshot of app services function list](./media/stream-analytics-functions-redis/app-services-function-list.png)</span></span>
2. <span data-ttu-id="387f5-147">Щелкните **Создать функцию > ServiceBusQueueTrigger — C#**.</span><span class="sxs-lookup"><span data-stu-id="387f5-147">Click **New Function > ServiceBusQueueTrigger – C#**.</span></span> <span data-ttu-id="387f5-148">Для hello следующие поля, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="387f5-148">For hello following fields, follow these instructions:</span></span>
   
   * <span data-ttu-id="387f5-149">**Имя очереди**: hello точно такое же имя, как имя hello, введенное при создании очереди hello в [начало работы с очередями шины обслуживания] [ servicebus-getstarted] (не hello именем hello служебной шины).</span><span class="sxs-lookup"><span data-stu-id="387f5-149">**Queue name**: hello same name as hello name you entered when you created hello queue in [Get Started with Service Bus Queues][servicebus-getstarted] (not hello name of hello service bus).</span></span> <span data-ttu-id="387f5-150">Убедитесь, что используется очередь hello, подключенных toohello, output Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="387f5-150">Make sure you use hello queue that is connected toohello Stream Analytics output.</span></span>
   * <span data-ttu-id="387f5-151">**Подключение к служебной шине.** Выберите **Добавить строку подключения**.</span><span class="sxs-lookup"><span data-stu-id="387f5-151">**Service Bus connection**: Select **Add a connection string**.</span></span> <span data-ttu-id="387f5-152">Строка подключения hello toofind, последовательно выберите toohello классический портал, выберите **Service Bus**, hello служебной шины, вы создали и **сведения о СОЕДИНЕНИИ** hello нижней части экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="387f5-152">toofind hello connection string, go toohello classic portal, select **Service Bus**, hello service bus you created, and **CONNECTION INFORMATION** at hello bottom of hello screen.</span></span> <span data-ttu-id="387f5-153">Убедитесь, что на главном экране приветствия на этой странице.</span><span class="sxs-lookup"><span data-stu-id="387f5-153">Make sure you are on hello main screen on this page.</span></span> <span data-ttu-id="387f5-154">Скопируйте и вставьте строку подключения hello.</span><span class="sxs-lookup"><span data-stu-id="387f5-154">Copy and paste hello connection string.</span></span> <span data-ttu-id="387f5-155">При желании вы свободного tooenter любое имя подключения.</span><span class="sxs-lookup"><span data-stu-id="387f5-155">Feel free tooenter any connection name.</span></span>
     
       ![Снимок экрана: подключение к служебной шине](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * <span data-ttu-id="387f5-157">**AccessRights**: выберите **Управление**.</span><span class="sxs-lookup"><span data-stu-id="387f5-157">**AccessRights**: Choose **Manage**</span></span>
3. <span data-ttu-id="387f5-158">Нажмите кнопку **Создать**</span><span class="sxs-lookup"><span data-stu-id="387f5-158">Click **Create**</span></span>

## <a name="writing-tooredis-cache"></a><span data-ttu-id="387f5-159">TooRedis записи кэша</span><span class="sxs-lookup"><span data-stu-id="387f5-159">Writing tooRedis Cache</span></span>
<span data-ttu-id="387f5-160">Мы создали функцию Azure, которая считывает данные из очереди служебной шины.</span><span class="sxs-lookup"><span data-stu-id="387f5-160">We have now created an Azure Function that reads from a Service Bus Queue.</span></span> <span data-ttu-id="387f5-161">Все, что остается toodo — используйте наши toowrite функции этого toohello данных кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="387f5-161">All that is left toodo is use our Function toowrite this data toohello Redis Cache.</span></span> 

1. <span data-ttu-id="387f5-162">Выберите только что созданный **ServiceBusQueueTrigger**и нажмите кнопку **функции параметров приложения** на hello правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="387f5-162">Select your newly created **ServiceBusQueueTrigger**, and click **Function app settings** on hello top right corner.</span></span> <span data-ttu-id="387f5-163">Выберите **перейти параметры службы tooApp > Параметры > Параметры приложения**</span><span class="sxs-lookup"><span data-stu-id="387f5-163">Select **Go tooApp Service Settings > Settings > Application settings**</span></span>
2. <span data-ttu-id="387f5-164">В hello раздел со строками соединения, создайте имя в hello **имя** раздела.</span><span class="sxs-lookup"><span data-stu-id="387f5-164">In hello Connection strings section, create a name in hello **Name** section.</span></span> <span data-ttu-id="387f5-165">Вставьте строку hello первичным соединением, найденный в hello **создавать кэш Redis** шаг с заходом hello **значение** раздела.</span><span class="sxs-lookup"><span data-stu-id="387f5-165">Paste hello primary connection string you found in hello **Create a Redis Cache** step into hello **Value** section.</span></span> <span data-ttu-id="387f5-166">Выберите значение **Пользовательская** из списка со значением **База данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="387f5-166">Select **Custom** where it says **SQL Database**.</span></span>
3. <span data-ttu-id="387f5-167">Нажмите кнопку **Сохранить** вверху hello.</span><span class="sxs-lookup"><span data-stu-id="387f5-167">Click **Save** at hello top.</span></span>
   
    ![Снимок экрана: подключение к служебной шине](./media/stream-analytics-functions-redis/function-connection-string.png)
4. <span data-ttu-id="387f5-169">Теперь вернитесь toohello параметры службы приложения и выберите **Сервис > редактор службы приложений (Предварительная версия) > на > Go**.</span><span class="sxs-lookup"><span data-stu-id="387f5-169">Now go back toohello App Service Settings and select **Tools > App Service Editor (Preview) > On > Go**.</span></span>
   
    ![Снимок экрана: подключение к служебной шине](./media/stream-analytics-functions-redis/app-service-editor.png)
5. <span data-ttu-id="387f5-171">В редакторе по своему усмотрению, создания JSON-файла с именем **project.json** с hello следующие и сохраните его tooyour локальный диск.</span><span class="sxs-lookup"><span data-stu-id="387f5-171">In an editor of your choice, create a JSON file named **project.json** with hello following and save it tooyour local disk.</span></span>
   
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
6. <span data-ttu-id="387f5-172">Отправьте этот файл в корневом каталоге hello функции (не WWWROOT).</span><span class="sxs-lookup"><span data-stu-id="387f5-172">Upload this file into hello root directory of your function (not WWWROOT).</span></span> <span data-ttu-id="387f5-173">Вы увидите файл с именем **project.lock.json** автоматически отображаются, подтверждающее, что hello Nuget пакеты «StackExchange.Redis» и «Newtonsoft.Json» были импортированы.</span><span class="sxs-lookup"><span data-stu-id="387f5-173">You should see a file named **project.lock.json** automatically appear, confirming that hello Nuget packages “StackExchange.Redis” and “Newtonsoft.Json” have been imported.</span></span>
7. <span data-ttu-id="387f5-174">В hello **run.csx** файла, замените hello предварительно созданный код после кода hello.</span><span class="sxs-lookup"><span data-stu-id="387f5-174">In hello **run.csx** file, replace hello pre-generated code with hello following code.</span></span> <span data-ttu-id="387f5-175">В функции lazyConnection hello, замените «CONN NAME» с именем hello, созданный на шаге 2 **хранения данных в кэш Redis hello**.</span><span class="sxs-lookup"><span data-stu-id="387f5-175">In hello lazyConnection function, replace “CONN NAME” with hello name you created in step 2 of **Store data into hello Redis cache**.</span></span>

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers tooa property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract hello time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using hello cache object...
        // Simple put of integral data types into hello cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from hello cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect toohello Service Bus
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

## <a name="start-hello-stream-analytics-job"></a><span data-ttu-id="387f5-176">Запустить задание Stream Analytics hello</span><span class="sxs-lookup"><span data-stu-id="387f5-176">Start hello Stream Analytics job</span></span>
1. <span data-ttu-id="387f5-177">Запустите приложение telcodatagen.exe hello.</span><span class="sxs-lookup"><span data-stu-id="387f5-177">Start hello telcodatagen.exe application.</span></span> <span data-ttu-id="387f5-178">Использование Hello выглядит следующим образом:````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span><span class="sxs-lookup"><span data-stu-id="387f5-178">hello usage is as follows: ````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span></span>
2. <span data-ttu-id="387f5-179">Из колонки задание Stream Analytics hello hello портала, нажмите кнопку **запустить** вверху hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="387f5-179">From hello Stream Analytics Job blade in hello portal, click **Start** at hello top of hello page.</span></span>
   
    ![Снимок экрана: запуск задания](./media/stream-analytics-functions-redis/starting-job.png)
3. <span data-ttu-id="387f5-181">В hello **запуска задания** колонки, отображается, выберите **теперь** и нажмите кнопку hello **запустить** кнопку hello нижней части экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="387f5-181">In hello **Start job** blade that appears, select **Now** and then click hello **Start** button at hello bottom of hello screen.</span></span> <span data-ttu-id="387f5-182">состояние задания Hello изменяет tooStarting и через некоторое время tooRunning изменения.</span><span class="sxs-lookup"><span data-stu-id="387f5-182">hello job status changes tooStarting and after some time changes tooRunning.</span></span>
   
    ![Снимок экрана: выбора времени начала задания](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a><span data-ttu-id="387f5-184">Запуск решения и проверка результатов</span><span class="sxs-lookup"><span data-stu-id="387f5-184">Run solution and check results</span></span>
<span data-ttu-id="387f5-185">Вернемся tooyour **ServiceBusQueueTrigger** должна появиться страница входа инструкций.</span><span class="sxs-lookup"><span data-stu-id="387f5-185">Going back tooyour **ServiceBusQueueTrigger** page, you should now see log statements.</span></span> <span data-ttu-id="387f5-186">Эти журналы Показать есть из hello очередь Service Bus, поместите его в базу данных hello и извлечь его с помощью hello времени в качестве ключа hello!</span><span class="sxs-lookup"><span data-stu-id="387f5-186">These logs show that you got something from hello Service Bus Queue, put it into hello database, and fetched it out using hello time as hello key!</span></span>

<span data-ttu-id="387f5-187">tooverify, данные хранятся в кэше Redis, переход на страницу кэша Redis tooyour на новом портале hello (как показано в предыдущем hello [создать кэш Azure Redis](#Create-an-Azure-Redis-Cache) шаг) и выберите консоли.</span><span class="sxs-lookup"><span data-stu-id="387f5-187">tooverify that your data is in your Redis cache, go tooyour Redis cache page in hello new portal (as shown in hello preceding [Create an Azure Redis Cache](#Create-an-Azure-Redis-Cache) step) and select Console.</span></span>

<span data-ttu-id="387f5-188">Теперь можно написать tooconfirm команды Redis, фактически является данных в кэше hello.</span><span class="sxs-lookup"><span data-stu-id="387f5-188">Now you can write Redis commands tooconfirm that data is in fact in hello cache.</span></span>

![Снимок экрана: консоль Redis](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a><span data-ttu-id="387f5-190">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="387f5-190">Next steps</span></span>
<span data-ttu-id="387f5-191">Мы рады hello новинок функции Azure Stream analytics можно сделать друг с другом и мы надеемся, что это разблокирует новые возможности для вас.</span><span class="sxs-lookup"><span data-stu-id="387f5-191">We’re excited about hello new things Azure Functions and Stream analytics can do together, and we hope this unlocks new possibilities for you.</span></span> <span data-ttu-id="387f5-192">При наличии любых отзывов на то, что нужно рядом чувствовать себя hello свободного toouse [сайт Azure UserVoice](https://feedback.azure.com/forums/270577-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="387f5-192">If you have any feedback on what you want next, feel free toouse hello [Azure UserVoice site](https://feedback.azure.com/forums/270577-stream-analytics).</span></span>

<span data-ttu-id="387f5-193">Если новый Microsoft Azure, мы приглашаем вас tootry он помещает, зарегистрировавшись для [освободить пробной учетной записи Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="387f5-193">If you are new Microsoft Azure, we invite you tootry it out by signing up for a [free Azure trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="387f5-194">Если указаны новые tooStream аналитики, а затем мы приглашаем вас слишком[создания вашего первого задания Stream Analytics](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="387f5-194">If you are new tooStream Analytics, then we invite you too[create your first Stream Analytics job](stream-analytics-create-a-job.md).</span></span>

<span data-ttu-id="387f5-195">Если вам нужна помощь или ответы на вопросы, напишите об этом на форуме [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) или [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="387f5-195">If you need any help or have questions, post on [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) or [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forums.</span></span> 

<span data-ttu-id="387f5-196">Можно также просмотреть hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="387f5-196">You can also see hello following resources:</span></span>

* [<span data-ttu-id="387f5-197">Справочник разработчика по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="387f5-197">Azure Functions developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="387f5-198">Справочник разработчика C# по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="387f5-198">Azure Functions C# developer reference</span></span>](../azure-functions/functions-reference-csharp.md)
* [<span data-ttu-id="387f5-199">Справочник разработчика F# по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="387f5-199">Azure Functions F# developer reference</span></span>](../azure-functions/functions-reference-fsharp.md)
* [<span data-ttu-id="387f5-200">Справочник разработчика NodeJS по функциям Azure</span><span class="sxs-lookup"><span data-stu-id="387f5-200">Azure Functions NodeJS developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="387f5-201">Azure Functions triggers and bindings (Триггеры и привязки в Функциях Azure)</span><span class="sxs-lookup"><span data-stu-id="387f5-201">Azure Functions triggers and bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
* [<span data-ttu-id="387f5-202">Как toomonitor Redis для Azure кэша</span><span class="sxs-lookup"><span data-stu-id="387f5-202">How toomonitor Azure Redis Cache</span></span>](../redis-cache/cache-how-to-monitor.md)

<span data-ttu-id="387f5-203">Выполните toostay, актуальные на все последние новости hello и возможности, [ @AzureStreaming ](https://twitter.com/AzureStreaming) в Twitter.</span><span class="sxs-lookup"><span data-stu-id="387f5-203">toostay up-to-date on all hello latest news and features, follow [@AzureStreaming](https://twitter.com/AzureStreaming) on Twitter.</span></span>

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
