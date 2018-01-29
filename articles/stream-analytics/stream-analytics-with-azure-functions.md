---
title: "Запуск службы \"Функции Azure\" с помощью заданий Azure Stream Analytics | Документация Майкрософт"
description: "Узнайте, как настроить службу \"Функции Azure\" в качестве приемника выходных данных для заданий Stream Analytics."
keywords: "выходные данные, потоковая передача данных, функция Azure"
documentationcenter: 
services: stream-analytics
author: SnehaGunda
manager: kfile
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 12/19/2017
ms.author: sngun
ms.openlocfilehash: f2f4a8d8cda752dc6ed197b8402119f7cbcaf58f
ms.sourcegitcommit: 28178ca0364e498318e2630f51ba6158e4a09a89
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/24/2018
---
# <a name="run-azure-functions-with-azure-stream-analytics-jobs"></a>Запуск службы "Функции Azure" с помощью заданий Azure Stream Analytics 

Службу "Функции Azure" можно запустить с помощью Azure Stream Analytics, настроив службу "Функции" в качестве приемника выходных данных для задания Stream Analytics. Служба "Функции" — это ориентированная на события среда вычислений по требованию, которая позволяет реализовывать код, активируемый по событиям, возникающим в Azure или в сторонних службах. Эта возможность службы "Функции" реагировать на триггеры упрощает вывод данных в задания Stream Analytics.

Stream Analytics вызывает службу "Функции" с помощью триггеров HTTP. Выходной адаптер службы "Функции" позволяет пользователям подключать службу "Функции" к Stream Analytics таким образом, что события могут запускаться на основе запросов Stream Analytics. 

В этом руководстве показано, как подключать Azure Stream Analytics к [кэшу Redis для Azure](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md) с помощью службы ["Функции Azure"](../azure-functions/functions-overview.md). 

## <a name="configure-a-stream-analytics-job-to-run-a-function"></a>Настройка задания Stream Analytics для запуска функции 

В этом разделе показано, как настроить задание Stream Analytics для запуска функции, которая записывает данные в кэш Redis для Azure. Задание Stream Analytics считывает события из концентраторов событий Azure, и выполняется запрос, который вызывает функцию. Эта функция считывает данные из задания Stream Analytics и записывает его в кэш Redis для Azure.

![Схема, на которой показаны связи между службами Azure](./media/stream-analytics-with-azure-functions/image1.png)

Для этого необходимо выполнить следующие задачи:
* [создать задание Stream Analytics с концентраторами событий в качестве входных данных](#create-stream-analytics-job-with-event-hub-as-input);  
* [создать экземпляр кэша Redis для Azure](#create-an-azure-redis-cache);  
* [создать функцию в службе "Функции Azure", которая может записывать данные в кэш Redis для Azure](#create-an-azure-function-that-can-write-data-to-the-redis-cache);    
* [обновить задание Stream Analytics с использованием функции в качестве выходных данных](#update-the-stream-analytic-job-with-azure-function-as-output);  
* [проверить кэш Redis для Azure на наличие результатов](#check-redis-cache-for-results).  

## <a name="create-a-stream-analytics-job-with-event-hubs-as-input"></a>Создание задания Stream Analytics с концентраторами событий в качестве входных данных

Следуйте руководству [по выявлению мошенничества в режиме реального времени](stream-analytics-real-time-fraud-detection.md), чтобы создать концентратор событий, запустить приложение создания событий и создать задание Stream Analytics. (Пропустите шаги для создания запроса и выходных данных. Вместо этого см. следующие разделы, чтобы настроить выходные данные службы "Функции".)

## <a name="create-an-azure-redis-cache-instance"></a>Создание экземпляра кэша Redis для Azure

1. Создайте кэш в кэше Redis для Azure, выполнив действия, описанные в [этом](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache) разделе.  

2. После создания кэша в разделе **Параметры** выберите **Ключи доступа**. Запишите **основную строку подключения**.

   ![Снимок экрана строки подключения кэша Redis для Azure](./media/stream-analytics-with-azure-functions/image2.png)

## <a name="create-a-function-in-azure-functions-that-can-write-data-to-azure-redis-cache"></a>Создание функции в службе "Функции Azure", которая может записывать данные в кэш Redis для Azure

1. Сведения см. в разделе [Создание приложения-функции](../azure-functions/functions-create-first-azure-function.md#create-a-function-app) документации по службе "Функции". Здесь описано, как создать приложение-функцию и [функцию, активируемую с помощью HTTP, в службе "Функции Azure"](../azure-functions/functions-create-first-azure-function.md#create-function) с помощью языка CSharp.  

2. Перейдите к функции **run.csx**. Обновите ее, используя следующий код. (Необходимо заменить \<свою строку подключения к кэшу Redis\> основной строкой подключения кэша Redis для Azure, извлеченной в предыдущем разделе.)  

   ```csharp
   using System;
   using System.Net;
   using System.Threading.Tasks;
   using StackExchange.Redis;
   using Newtonsoft.Json;
   using System.Configuration;

   public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
   {
      log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");
    
      // Get the request body
      dynamic dataArray = await req.Content.ReadAsAsync<object>();

      // Throw an HTTP Request Entity Too Large exception when the incoming batch(dataArray) is greater than 256 KB. Make sure that the size value is consistent with the value entered in the Stream Analytics portal.

      if (dataArray.ToString().Length > 262144)
      {        
         return new HttpResponseMessage(HttpStatusCode.RequestEntityTooLarge);
      }
      var connection = ConnectionMultiplexer.Connect("<your redis cache connection string goes here>");
      log.Info($"Connection string.. {connection}");
    
      // Connection refers to a property that returns a ConnectionMultiplexer
      IDatabase db = connection.GetDatabase();
      log.Info($"Created database {db}");
    
      log.Info($"Message Count {dataArray.Count}");

      // Perform cache operations using the cache object. For example, the following code block adds few integral data types to the cache
      for (var i = 0; i < dataArray.Count; i++)
      {
        string time = dataArray[i].time;
        string callingnum1 = dataArray[i].callingnum1;
        string key = time + " - " + callingnum1;
        db.StringSet(key, dataArray[i].ToString());
        log.Info($"Object put in database. Key is {key} and value is {dataArray[i].ToString()}");
       
      // Simple get of data types from the cache
      string value = db.StringGet(key);
      log.Info($"Database got: {value}");
      }

      return req.CreateResponse(HttpStatusCode.OK, "Got");
    }    

   ```

   Когда Stream Analytics получает исключение "Сущность запроса HTTP слишком большая" из функции, размер пакетов, отправляемых в службу "Функции", уменьшается. Используйте в функции следующий код, чтобы убедиться, что Stream Analytics не отправляет пакеты слишком большого размера. Убедитесь, что максимальное количество пакетов и размеры значений, используемые в функции, соответствуют значениям, введенным на портале Stream Analytics.

   ```csharp
   if (dataArray.ToString().Length > 262144)
      {        
        return new HttpResponseMessage(HttpStatusCode.RequestEntityTooLarge);
      }
   ```

3. В выбранном текстовом редакторе создайте JSON-файл с именем **project.json**. Используйте следующий код и сохраните его на своем локальном компьютере. Этот файл содержит зависимости пакетов NuGet, необходимых для функции C#.  
   
   ```json
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

   ```
 
4. Вернитесь на портал Azure. С вкладки **Функции платформы** перейдите к своей функции. В разделе **Средства разработки** выберите **Редактор службы приложений**. 
 
   ![Снимок экрана редактора службы приложений](./media/stream-analytics-with-azure-functions/image3.png)

5. В редакторе службы приложений щелкните корневой каталог правой кнопкой мыши и отправьте файл **project.json**. После успешной отправки обновите страницу. Теперь вы должны увидеть автоматически сформированный файл с именем **project.lock.json**. Он содержит ссылки на DLL-файлы, указанные в файле project.json.  

   ![Снимок экрана редактора службы приложений](./media/stream-analytics-with-azure-functions/image4.png)

 

## <a name="update-the-stream-analytics-job-with-the-function-as-output"></a>Обновление задания Stream Analytics с использованием функции в качестве выходных данных

1. Откройте задание Stream Analytics на портале Azure.  

2. Перейдите к функции и выберите **Обзор** > **Выходные данные** > **Добавить**. Чтобы добавить новые выходные данные, выберите **Функция Azure** в качестве приемника. Доступен новый выходной адаптер службы "Функции" со следующими свойствами:  

   |**Имя свойства**|**Описание**|
   |---|---|
   |Псевдоним выходных данных| Понятное имя, используемое в запросах задания для ссылки на эти выходные данные. |
   |Вариант импорта| Вы можете использовать эту функцию из текущей подписки или указать параметры вручную, если функция находится в другой подписке. |
   |Приложение-функция| Имя приложения службы "Функции". |
   |Функция| Имя функции в приложении службы "Функции" (имя функции run.csx).|
   |Максимальный размер пакета|Задает максимальный размер каждого пакета выходных данных, который передается в функцию. По умолчанию установлено значение 256 КБ.|
   |Максимальное количество пакетов|Указывает максимальное число событий в каждом пакете, который отправляется в функцию. По умолчанию используется значение 100. Это необязательное свойство.|
   |Ключ|Позволяет использовать функцию из другой подписки. Укажите значение ключа для доступа к функции. Это необязательное свойство.|

3. Введите имя для выходного псевдонима. В этом руководстве это **saop1** (можно использовать любое имя по своему усмотрению). Заполните другие сведения.  

4. Откройте задание Stream Analytics и обновите запрос следующим образом. (Не забудьте заменить текст saop1, если приемник выходных данных имеет другое имя.)  

   ```sql
    SELECT 
            System.Timestamp as Time, CS1.CallingIMSI, CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, CS1.SwitchNum as Switch1, CS2.SwitchNum as Switch2
        INTO saop1
        FROM CallStream CS1 TIMESTAMP BY CallRecTime
           JOIN CallStream CS2 TIMESTAMP BY CallRecTime
            ON CS1.CallingIMSI = CS2.CallingIMSI AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5
        WHERE CS1.SwitchNum != CS2.SwitchNum
   ```

5. Запустите приложение telcodatagen.exe, выполнив следующую команду в командной строке (используйте формат `telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]`):  
   
   **telcodatagen.exe 1000 .2 2**
    
6.  Запустите задание Stream Analytics.

## <a name="check-azure-redis-cache-for-results"></a>Проверка кэша Redis для Azure на наличие результатов

1. Перейдите на портал Azure и найдите кэш Redis для Azure. Выберите **Консоль**.  

2. Используйте [команды кэша Redis](https://redis.io/commands), чтобы проверить правильность данных в кэше Redis. (Команда имеет формат Get {key}.) Например: 

   **Get "12/19/2017 21:32:24 - 123414732"**

   Эта команда должна вывести значение для указанного ключа:

   ![Снимок экрана выходных данных кэша Redis для Azure](./media/stream-analytics-with-azure-functions/image5.png)

## <a name="known-issues"></a>Известные проблемы

На портале Azure при попытке сброса значения максимального размера пакета или максимального числа пакетов до нуля (значения по умолчанию) после сохранения значение возвращается к ранее введенному. В этом случае введите значения по умолчанию для этих полей вручную.

