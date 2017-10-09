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
# <a name="how-toostore-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a>Как toostore данные из Azure Stream Analytics в кэше Redis для Azure с помощью функций Azure
Azure Stream Analytics позволяет быстро разрабатывать и развертывать решения недорогих toogain в режиме реального времени полезных сведений из устройств, датчиков, инфраструктуры и приложений или любой поток данных. Azure Stream Analytics обеспечивает различные варианты использования, в том числе управление и мониторинг в реальном времени, контроль и управление, обнаружение мошенничества, автомобили с сетевыми возможностями и многое другое. Во многих таких сценариях может потребоваться toostore данные, выдаваемые Azure Stream Analytics в хранилище распределенных данных, например для кэша Azure Redis.

Предположим, что вы работаете в телекоммуникационной компании. Вы пытаетесь toodetect SIM мошенничества, где несколько вызовов, поступающих от hello одинаковый идентификатор, на hello же время, но в разных географически расположения. Вам нужно хранение всех hello потенциальных мошеннические телефонных звонков в кэш Azure Redis. В этом блоге мы опишем, как можно легко выполнить вашу задачу. 

## <a name="prerequisites"></a>Предварительные требования
Полный hello [мошенничества в реальном времени] [ fraud-detection] Пошаговое руководство для ASA

## <a name="architecture-overview"></a>Общие сведения об архитектуре
![Снимок экрана: архитектура](./media/stream-analytics-functions-redis/architecture-overview.png)

Как показано в предшествующих рисунок hello Stream Analytics позволяет потоковой передачи toobe входных данных запроса и отправляются tooan выходных данных. На основании вывода hello, функции Azure можно активировать определенного типа события. 

В этом блоге мы Обратите внимание на часть функций Azure hello этот конвейер или точнее hello инициацию событие, которое хранит мошеннические данные в кэш hello.
После завершения hello [мошенничества в реальном времени] [ fraud-detection] учебник, у вас есть входных данных (концентратор событий), запрос и вывод (хранилище blob) уже настроен и запущен. В этом блоге мы изменить toouse вывода hello очередь служебной шины. После этого мы подключаемся к очереди Azure функция toothis. 

## <a name="create-and-connect-a-service-bus-queue-output"></a>Создание и подключение выходных данных очереди служебной шины
toocreate очередь служебной шины, выполните шаги 1 и 2 раздела .NET hello в [начало работы с очередями шины обслуживания][servicebus-getstarted].
Теперь подключим задания Stream Analytics toohello очереди hello, созданный в hello руководство по применению предыдущих обнаружения мошенничества.

1. В hello портал Azure, перейдите toohello **выходные данные** колонке задание и выберите **добавить** вверху hello страницы приветствия.
   
    ![Добавление выходных данных](./media/stream-analytics-functions-redis/adding-outputs.png)
2. Выберите **очередь Service Bus** как hello **приемника** и следуйте инструкциям, hello на экране приветствия. Убедиться, что toochoose hello пространство имен hello очереди шины обслуживания можно создать в [начало работы с очередями шины обслуживания][servicebus-getstarted]. Нажмите кнопку «правый» hello, когда вы закончите.
3. Укажите hello следующие значения:
   
   * **Формат сериализатора событий**: JSON;
   * **Кодировка**: UTF8.
   * **ФОРМАТ**: строки-разделители.
4. Нажмите кнопку hello **создать** этого источника и tooverify успешного подключения учетной записи хранилища toohello Stream Analytics, нажмите кнопку tooadd.
5. В hello **запроса** вкладки, замените следующие hello hello текущего запроса. Замените * [имя вашей службы ШИНЫ] * с именем hello выходных данных, созданный на шаге 3. 
   
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

## <a name="create-an-azure-redis-cache"></a>Создание кэша Redis для Azure
Создать кэш Azure Redis ниже hello .NET раздела [как tooUse кэш Azure Redis] [ use-rediscache] до вызова hello раздел ***Настройка клиентов кэша hello***.
После выполнения всех указаний у вас будет новый кэш Redis. В разделе **все параметры**выберите **ключи доступа** и запишите hello ***основная строка подключения***.

![Снимок экрана: архитектура](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a>Создание функции Azure
Выполните [создания вашего первого функции Azure] [ functions-getstarted] tooget учебника работы с функциями Azure. Если уже имеется функция Azure необходимо как toouse, а затем пропускать слишком[записи tooRedis кэша](#Writing-to-Redis-Cache)

1. Hello портала выберите службы приложений hello левой панели навигации, а затем щелкните веб-сайт вашей Azure функция приложения имя tooget toohello функции приложения.
    ![Снимок экрана: список функций службы приложений](./media/stream-analytics-functions-redis/app-services-function-list.png)
2. Щелкните **Создать функцию > ServiceBusQueueTrigger — C#**. Для hello следующие поля, выполните следующие действия:
   
   * **Имя очереди**: hello точно такое же имя, как имя hello, введенное при создании очереди hello в [начало работы с очередями шины обслуживания] [ servicebus-getstarted] (не hello именем hello служебной шины). Убедитесь, что используется очередь hello, подключенных toohello, output Stream Analytics.
   * **Подключение к служебной шине.** Выберите **Добавить строку подключения**. Строка подключения hello toofind, последовательно выберите toohello классический портал, выберите **Service Bus**, hello служебной шины, вы создали и **сведения о СОЕДИНЕНИИ** hello нижней части экрана приветствия. Убедитесь, что на главном экране приветствия на этой странице. Скопируйте и вставьте строку подключения hello. При желании вы свободного tooenter любое имя подключения.
     
       ![Снимок экрана: подключение к служебной шине](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * **AccessRights**: выберите **Управление**.
3. Нажмите кнопку **Создать**

## <a name="writing-tooredis-cache"></a>TooRedis записи кэша
Мы создали функцию Azure, которая считывает данные из очереди служебной шины. Все, что остается toodo — используйте наши toowrite функции этого toohello данных кэша Redis. 

1. Выберите только что созданный **ServiceBusQueueTrigger**и нажмите кнопку **функции параметров приложения** на hello правом верхнем углу. Выберите **перейти параметры службы tooApp > Параметры > Параметры приложения**
2. В hello раздел со строками соединения, создайте имя в hello **имя** раздела. Вставьте строку hello первичным соединением, найденный в hello **создавать кэш Redis** шаг с заходом hello **значение** раздела. Выберите значение **Пользовательская** из списка со значением **База данных SQL**.
3. Нажмите кнопку **Сохранить** вверху hello.
   
    ![Снимок экрана: подключение к служебной шине](./media/stream-analytics-functions-redis/function-connection-string.png)
4. Теперь вернитесь toohello параметры службы приложения и выберите **Сервис > редактор службы приложений (Предварительная версия) > на > Go**.
   
    ![Снимок экрана: подключение к служебной шине](./media/stream-analytics-functions-redis/app-service-editor.png)
5. В редакторе по своему усмотрению, создания JSON-файла с именем **project.json** с hello следующие и сохраните его tooyour локальный диск.
   
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
6. Отправьте этот файл в корневом каталоге hello функции (не WWWROOT). Вы увидите файл с именем **project.lock.json** автоматически отображаются, подтверждающее, что hello Nuget пакеты «StackExchange.Redis» и «Newtonsoft.Json» были импортированы.
7. В hello **run.csx** файла, замените hello предварительно созданный код после кода hello. В функции lazyConnection hello, замените «CONN NAME» с именем hello, созданный на шаге 2 **хранения данных в кэш Redis hello**.

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

## <a name="start-hello-stream-analytics-job"></a>Запустить задание Stream Analytics hello
1. Запустите приложение telcodatagen.exe hello. Использование Hello выглядит следующим образом:````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````
2. Из колонки задание Stream Analytics hello hello портала, нажмите кнопку **запустить** вверху hello страницы приветствия.
   
    ![Снимок экрана: запуск задания](./media/stream-analytics-functions-redis/starting-job.png)
3. В hello **запуска задания** колонки, отображается, выберите **теперь** и нажмите кнопку hello **запустить** кнопку hello нижней части экрана приветствия. состояние задания Hello изменяет tooStarting и через некоторое время tooRunning изменения.
   
    ![Снимок экрана: выбора времени начала задания](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a>Запуск решения и проверка результатов
Вернемся tooyour **ServiceBusQueueTrigger** должна появиться страница входа инструкций. Эти журналы Показать есть из hello очередь Service Bus, поместите его в базу данных hello и извлечь его с помощью hello времени в качестве ключа hello!

tooverify, данные хранятся в кэше Redis, переход на страницу кэша Redis tooyour на новом портале hello (как показано в предыдущем hello [создать кэш Azure Redis](#Create-an-Azure-Redis-Cache) шаг) и выберите консоли.

Теперь можно написать tooconfirm команды Redis, фактически является данных в кэше hello.

![Снимок экрана: консоль Redis](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a>Дальнейшие действия
Мы рады hello новинок функции Azure Stream analytics можно сделать друг с другом и мы надеемся, что это разблокирует новые возможности для вас. При наличии любых отзывов на то, что нужно рядом чувствовать себя hello свободного toouse [сайт Azure UserVoice](https://feedback.azure.com/forums/270577-stream-analytics).

Если новый Microsoft Azure, мы приглашаем вас tootry он помещает, зарегистрировавшись для [освободить пробной учетной записи Azure](https://azure.microsoft.com/pricing/free-trial/). Если указаны новые tooStream аналитики, а затем мы приглашаем вас слишком[создания вашего первого задания Stream Analytics](stream-analytics-create-a-job.md).

Если вам нужна помощь или ответы на вопросы, напишите об этом на форуме [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) или [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics). 

Можно также просмотреть hello следующие ресурсы:

* [Справочник разработчика по функциям Azure](../azure-functions/functions-reference.md)
* [Справочник разработчика C# по функциям Azure](../azure-functions/functions-reference-csharp.md)
* [Справочник разработчика F# по функциям Azure](../azure-functions/functions-reference-fsharp.md)
* [Справочник разработчика NodeJS по функциям Azure](../azure-functions/functions-reference.md)
* [Azure Functions triggers and bindings (Триггеры и привязки в Функциях Azure)](../azure-functions/functions-triggers-bindings.md)
* [Как toomonitor Redis для Azure кэша](../redis-cache/cache-how-to-monitor.md)

Выполните toostay, актуальные на все последние новости hello и возможности, [ @AzureStreaming ](https://twitter.com/AzureStreaming) в Twitter.

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
