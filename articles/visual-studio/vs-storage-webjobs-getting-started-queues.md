---
title: "aaaGetting работы с хранилищем очередей и Visual Studio подключенных служб (для проектов веб-задания) | Документы Microsoft"
description: "Как tooget запущена с помощью хранилища очередей Azure в проекте веб-задания после подключения tooa учетной записи хранилища с помощью Visual Studio подключения службы."
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 47a446aa5c6bbf25526339823db4952ac1a8802f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a>Приступая к работе с подключенными службами хранилища очередей Azure и Visual Studio (проекты веб-заданий)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Обзор
В этой статье описывается, как получить работы с использованием очередей Azure hello хранилища в проект веб-задания Azure Visual Studio после создания или ссылка на учетную запись хранения Azure с помощью Visual Studio **Добавление подключенных служб** диалоговое окно. При добавлении проекта веб-задания tooa учетной записи хранилища с помощью Visual Studio hello **Добавление подключенных служб** диалогового окна, установлены соответствующие пакеты NuGet хранилища Azure hello, соответствующие ссылки .NET hello будут добавлены toohello в файле App.config hello обновляются проекта и строки подключения для учетной записи хранения hello.  

Эта статья содержит примеры кода C#, которые показывают, как toouse hello веб-заданий Azure SDK версии 1.x hello службы хранилища очередей Azure.

Хранилище Azure очереди — это служба для хранения большого количества сообщений, которые может осуществляться из любого места в Здравствуй, мир! через вызовы прошедшего проверку подлинности, протокол HTTP или HTTPS. Сообщение одной очереди может быть вверх too64 КБ и очередь может содержать миллионы сообщений вверх toohello предел общая емкость учетной записи хранения. Дополнительные сведения см. в разделе [Приступая к работе с хранилищем очередей Azure с помощью .NET](../storage/queues/storage-dotnet-how-to-use-queues.md). Дополнительные сведения см. на сайте [ASP.NET](http://www.asp.net).

## <a name="how-tootrigger-a-function-when-a-queue-message-is-received"></a>Как tootrigger функции при получении сообщения в очереди
вызывает функцию, которая hello SDK веб-заданий toowrite при получении сообщения в очереди, используйте hello **QueueTrigger** атрибута. Конструктор атрибута Hello принимает строковый параметр, задающий имя hello toopoll очереди hello. toosee как tooset hello имя очереди динамически, извлечь [как tooset параметры конфигурации](#how-to-set-configuration-options).

### <a name="string-queue-messages"></a>Строковые сообщения очереди
В следующем примере hello, hello очередь содержит строковое сообщение, поэтому **QueueTrigger** будет применен tooa строковый параметр с именем **logMessage** , содержащее содержимое очереди приветственное сообщение hello. Здравствуйте, функция [записывает toohello сообщение журнала мониторинга](#how-to-write-logs).

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

Помимо **строка**, hello параметр может быть массив байтов, **CloudQueueMessage** объекта или POCO, определяемому вами.

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>Сообщения очереди [POCO](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)
В следующем примере hello, сообщение hello очереди содержит JSON для **BlobInformation** объекта, который включает **BlobName** свойство. пакет SDK для Hello автоматически десериализует hello объекта.

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Hello SDK использует hello [пакет Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize и десериализации сообщений. При создании очереди сообщений в программе, которая не использует hello SDK веб-задания, можно написать код, как следующий пример toocreate POCO очереди сообщений hello приветствия, можно провести синтаксический анализ пакета SDK.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a>Асинхронные функции
После асинхронного функции Hello [записывает журнал toohello мониторинга](#how-to-write-logs).

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

Может потребоваться асинхронных функций [токен отмены](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), как показано в hello следующий пример, который копирует большой двоичный объект. (Объяснение hello **queueTrigger** заполнитель, в разделе hello [большие двоичные объекты](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) раздел.)

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-hello-queuetrigger-attribute-works-with"></a>Атрибут QueueTrigger hello типы работает с
Можно использовать **QueueTrigger** с hello следующие типы:

* **string**
* тип POCO, сериализованный как JSON;
* **byte[]**
* **CloudQueueMessage**

## <a name="polling-algorithm"></a>Алгоритм опроса
Hello SDK реализует эффекта экспоненциальной отсрочки алгоритм случайных tooreduce hello простоя очереди опроса на транзакционные издержки хранения.  При обнаружении сообщение hello SDK ожидает в течение двух секунд и затем проверяет наличие другого сообщения; Если сообщение не найдено он ожидает около четырех секунд перед повторной попыткой. После tooget последующих неудачных попытках сообщения в очереди, время ожидания hello продолжается tooincrease, пока не достигнет hello максимальное время ожидания, какие значения по умолчанию tooone минуты. [Hello максимальное время ожидания настраивается](#how-to-set-configuration-options).

## <a name="multiple-instances"></a>Выполнение на нескольких экземплярах
Если веб-приложение выполняется на нескольких экземплярах, непрерывные веб-задания выполняется на каждом компьютере, и каждой машины будет ожидать триггеры и повторите toorun функции. В некоторых случаях это может привести toosome функции обработки дважды, hello и те же данные, поэтому функции должны быть идемпотентными (написаны так, несколько раз вызывать их с приветствия же входных данных не может создать повторяющиеся результаты).  

## <a name="parallel-execution"></a>Параллельное выполнение
Если у вас есть несколько функций, которые прослушивают различные очереди, hello SDK вызывает их параллельно при получении сообщений одновременно.

Hello это верно и при получении нескольких сообщений для одной очереди. По умолчанию hello SDK получает пакет 16 очереди сообщений за раз и выполняет функции hello, обрабатывает их параллельно. [размер пакета Hello настраивается](#how-to-set-configuration-options). При получении hello число обрабатываемых вниз toohalf размера пакета hello, hello SDK возвращает другой пакет и начинает обработку этих сообщений. Поэтому hello максимальное количество одновременных сообщений, обрабатываемых каждой функции является размер пакета в полтора раза hello. Это ограничение применяется отдельно tooeach функции, которая имеет **QueueTrigger** атрибута. Если вы не хотите параллельного выполнения для сообщений, полученных на одну очередь, установите too1 размер пакета hello.

## <a name="get-queue-or-queue-message-metadata"></a>Получение очереди или метаданных очереди сообщений
Можно получить следующие свойства сообщения, добавив параметры сигнатуры метода toohello hello:

* **DateTimeOffset** expirationTime
* **DateTimeOffset** insertionTime
* **DateTimeOffset** nextVisibleTime
* **string** queueTrigger (содержит текст сообщения)
* **string** id
* **string** popReceipt
* **int** dequeueCount

Если требуется toowork непосредственно с hello хранилища Azure API, можно добавить **CloudStorageAccount** параметра.

Hello следующий пример записывает все журнал этого приложения tooan метаданных. В примере hello logMessage и queueTrigger содержимым hello hello очереди сообщения.

        public static void WriteLog([QueueTrigger("logqueue")] string logMessage,
            DateTimeOffset expirationTime,
            DateTimeOffset insertionTime,
            DateTimeOffset nextVisibleTime,
            string id,
            string popReceipt,
            int dequeueCount,
            string queueTrigger,
            CloudStorageAccount cloudStorageAccount,
            TextWriter logger)
        {
            logger.WriteLine(
                "logMessage={0}\n" +
            "expirationTime={1}\ninsertionTime={2}\n" +
                "nextVisibleTime={3}\n" +
                "id={4}\npopReceipt={5}\ndequeueCount={6}\n" +
                "queue endpoint={7} queueTrigger={8}",
                logMessage, expirationTime,
                insertionTime,
                nextVisibleTime, id,
                popReceipt, dequeueCount,
                cloudStorageAccount.QueueEndpoint,
                queueTrigger);
        }

Ниже приведен пример журнала записываются в примере кода hello.

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a>Корректное завершение работы
Функция, которая выполняется в непрерывных веб-задания может принимать **CancellationToken** параметр, который позволяет функции hello операционной системы toonotify hello при hello веб-задания — о toobe завершен. Можно использовать toomake это уведомление о том, что функции hello не привести к непредвиденному завершению способом, который оставляет данных в несогласованном состоянии.

Следующий пример показывает как Hello toocheck увольнения предстоящем веб-задания в функции.

    public static void GracefulShutdownDemo(
                [QueueTrigger("inputqueue")] string inputText,
                TextWriter logger,
                CancellationToken token)
    {
        for (int i = 0; i < 100; i++)
        {
            if (token.IsCancellationRequested)
            {
                logger.WriteLine("Function was cancelled at iteration {0}", i);
                break;
            }
            Thread.Sleep(1000);
            logger.WriteLine("Normal processing for queue message={0}", inputText);
        }
    }

**Примечание:** hello панели мониторинга может показывать правильно состояние hello и выходные данные функции, которые была завершена.

Дополнительную информацию см. в статье [Нормальное завершение работы веб-заданий](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).   

## <a name="how-toocreate-a-queue-message-while-processing-a-queue-message"></a>Как toocreate очереди сообщений во время обработки сообщения в очереди
функция, которая создает новое сообщение очереди, используйте hello toowrite **очереди** атрибута. Как **QueueTrigger**, передав имя очереди hello в виде строки, или вы можете [динамически задать имя очереди hello](#how-to-set-configuration-options).

### <a name="string-queue-messages"></a>Строковые сообщения очереди
Следующий образец кода синхронные Hello создает новое сообщение очереди в очередь hello, с именем «outputqueue» с таким же содержимое, так как очередь приветственное сообщение получено в hello очереди с именем «inputqueue» hello. (Для асинхронных функций используйте параметр **IAsyncCollector;<T>** , следуя указаниям далее в этом разделе.)

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>Сообщения очереди [POCO](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)
toocreate очереди сообщение, содержащее POCO, а не строкой, pass hello POCO тип в качестве выходного параметра toohello **очереди** конструктор атрибута.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

пакет SDK для Hello автоматически сериализует tooJSON hello объекта. Очередь сообщений создается всегда, даже если hello объекта имеет значение null.

### <a name="create-multiple-messages-or-in-async-functions"></a>Создание нескольких сообщений или сообщений в асинхронных функциях
toocreate несколько сообщений сделать hello тип параметра для очереди вывода hello **ICollector<T>**  или **IAsyncCollector<T>**, как показано в следующий пример hello.

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Каждое сообщение очереди создается сразу после hello **добавить** вызывается метод.

### <a name="types-that-hello-queue-attribute-works-with"></a>Типы атрибута очереди hello работает с
Можно использовать hello **очереди** атрибутов на следующие типы параметра hello:

* **строки** (создает сообщения в очереди, если значение параметра не равно null, при завершении функции hello)
* **out byte[]** (работает как параметр **string**);
* **out CloudQueueMessage** (работает как параметр **string**);
* **out POCO** (сериализуемый тип, создает сообщение с пустым объектом Если hello имеет значение null, при завершении функции hello)
* **ICollector;**
* **IAsyncCollector;**
* **CloudQueue** (для создания сообщений вручную с помощью hello API хранилища Azure непосредственно)

### <a name="use-webjobs-sdk-attributes-in-hello-body-of-a-function"></a>Использование пакета SDK веб-задания атрибутов в теле функции hello
Если вам требуется toodo некоторые работать в функции перед использованием атрибут SDK веб-заданий, таких как **очереди**, **большого двоичного объекта**, или **таблицы**, можно использовать hello **IBinder** интерфейса.

Следующий пример Hello принимает сообщение входной очереди и создает новое сообщение с hello же содержимого, в очереди вывода. Имя очереди вывода Hello задается код в теле hello функции hello.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

Hello **IBinder** интерфейс может также использоваться с hello **таблицы** и **большого двоичного объекта** атрибуты.

## <a name="how-tooread-and-write-blobs-and-tables-while-processing-a-queue-message"></a>Как tooread и записи больших двоичных объектов и таблиц во время обработки сообщения в очереди
Hello **большого двоичного объекта** и **таблицы** атрибуты позволяют tooread и записи больших двоичных объектов и таблиц. Hello образцы в этом разделе применяются tooblobs. Примеры кода, которые показывают, как tootrigger обрабатывает при создании или обновлении больших двоичных объектов см. в разделе [как toouse Azure хранилище больших двоичных объектов с hello SDK веб-заданий](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)и примеры кода, которые считывают и записывают таблиц см. в разделе [как toouse таблицы Azure хранилище с hello SDK веб-задания](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).

### <a name="string-queue-messages-triggering-blob-operations"></a>Сообщения очереди строк, которые запускают операции с большими двоичными объектами
Для очереди сообщение, содержащее строку **queueTrigger** — это, можно использовать в hello **большого двоичного объекта** атрибута **blobPath** параметра, который содержит содержимое hello сообщение Hello.

Hello следующий пример использует **поток** объектов tooread и записи больших двоичных объектов. приветственное сообщение очереди — hello имя BLOB-объектов, находящихся в контейнере textblobs hello. Копия hello большой двоичный объект с «-новые» присоединенных toohello имя создается в hello же контейнер.

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Hello **большого двоичного объекта** атрибута конструктор принимает **blobPath** параметр, определяющий hello контейнера и имя большого двоичного объекта. Дополнительные сведения об этом заполнитель см. в разделе [как toouse Azure хранилище больших двоичных объектов с hello SDK веб-задания](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).

Если атрибут hello оформляет **поток** другой конструктор указывает hello объекта **FileAccess** режим чтения, записи или чтения и записи.

Hello следующий пример использует **CloudBlockBlob** объекта toodelete большого двоичного объекта. приветственное сообщение очереди является именем hello hello большого двоичного объекта.

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>Сообщения очереди [POCO](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)
Для POCO, хранятся в очереди сообщение hello как JSON, можно использовать местозаполнители, имя свойства объекта hello в hello **очереди** атрибута **blobPath** параметра. Можно также использовать имена свойства метаданных очереди в качестве заполнителей. Ознакомьтесь с разделом [Получение метаданных очереди или сообщения в очереди](#get-queue-or-queue-message-metadata).

Hello следующий пример копирует BLOB-объектов tooa новый большой двоичный объект с другим расширением. сообщение Hello очереди **BlobInformation** объект, который содержит **BlobName** и **BlobNameWithoutExtension** свойства. имена свойств Hello используются в качестве меток-заполнителей в пути hello больших двоичных объектов для hello **большого двоичного объекта** атрибуты.

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Hello SDK использует hello [пакет Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize и десериализации сообщений. При создании очереди сообщений в программе, которая не использует hello SDK веб-задания, можно написать код, как следующий пример toocreate POCO очереди сообщений hello приветствия, можно провести синтаксический анализ пакета SDK.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

Если вам требуется toodo некоторые работают в функции перед привязкой tooan большой двоичный объект, можно использовать атрибут hello в текст hello функции hello, как показано в [использовать пакет SDK веб-задания атрибутов в теле функции hello](#use-webjobs-sdk-attributes-in-the-body-of-a-function).

### <a name="types-you-can-use-hello-blob-attribute-with"></a>Типы, которые можно использовать hello атрибута с BLOB-объектов
Hello **большого двоичного объекта** атрибут может использоваться с hello следующие типы:

* **Поток** (чтение или запись, указанный с помощью параметра конструктора hello FileAccess)
* **TextReader;**
* **TextWriter**
* **string** (чтение);
* **строки** (записи; создает большой двоичный объект только в том случае, если параметр строки hello отлично от null, при возврате из функции hello)
* POCO (чтение);
* out POCO (записи; всегда создает большой двоичный объект, создает как объект null, если параметр POCO имеет значение null, при возврате из функции hello)
* **CloudBlobStream** (запись);
* **ICloudBlob** (чтение или запись);
* **CloudBlockBlob** (чтение или запись);
* **CloudPageBlob** (чтение или запись).

## <a name="how-toohandle-poison-messages"></a>Как toohandle подозрительные сообщения
Сообщения, содержимое которого приводит toofail функции называются *сообщения о сбое*. При сбое функции hello, очередь приветственное сообщение не удаляется и в конечном счете передается еще раз, может вызвать toobe hello цикл повторяется. Hello SDK можно прервать цикл hello автоматически после ограниченного числа итераций, или это можно сделать вручную.

### <a name="automatic-poison-message-handling"></a>Автоматическая обработка сообщений
Hello SDK будет вызвать функцию копирования tooprocess раз too5 сообщения в очереди. При сбое hello пятый try, приветственное сообщение — перемещенный tooa очереди подозрительных сообщений. Вы увидите, как tooconfigure hello максимальное число повторных попыток в [как параметры конфигурации tooset](#how-to-set-configuration-options).

очередь подозрительных сообщений Hello называется *{originalqueuename}*-подозрительное. Можно написать tooprocess функция сообщения из очереди подозрительных сообщений hello ее регистрации или отправка уведомления о необходимости ручного вмешательства.

В следующий пример hello hello **CopyBlob** функция завершится ошибкой, если сообщения в очереди содержит hello имя большого двоичного объекта, который не существует. В этом случае приветственное сообщение перемещается из hello copyblobqueue очереди toohello copyblobqueue подозрительных очереди. Hello **ProcessPoisonMessage** то подозрительное сообщение hello журналы.

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

        public static void ProcessPoisonMessage(
            [QueueTrigger("copyblobqueue-poison")] string blobName, TextWriter logger)
        {
            logger.WriteLine("Failed toocopy blob, name=" + blobName);
        }

Hello ниже показан вывод на консоль из этих функций при обработке подозрительных сообщений.

![Вывод консоли для обработки подозрительных сообщений](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a>Ручная обработка подозрительных сообщений
Hello количество обработки сообщения для обработки можно получить, добавив **int** параметр с именем **dequeueCount** tooyour функции. После этого можно hello проверьте количество в коде функция вывода из очереди и выполнять собственные подозрительное сообщение обработки при hello число превышает пороговое значение, как показано в следующий пример hello.

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed toocopy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a name="how-tooset-configuration-options"></a>Как параметры конфигурации tooset
Можно использовать hello **JobHostConfiguration** hello tooset тип следующие параметры конфигурации:

* Задать строки подключения пакета SDK для hello в коде.
* Настройка таких параметров атрибута **QueueTrigger** , как максимальное значение счетчика вывода из очереди.
* Получение имен очередей из конфигурации

### <a name="set-sdk-connection-strings-in-code"></a>Установка строк подключения пакета SDK в коде
Задание строк подключения пакета SDK для hello в коде позволяет вы toouse собственные имена строку соединения в файлах конфигурации или переменные среды, как показано в следующий пример hello.

        static void Main(string[] args)
        {
            var _storageConn = ConfigurationManager
                .ConnectionStrings["MyStorageConnection"].ConnectionString;

            var _dashboardConn = ConfigurationManager
                .ConnectionStrings["MyDashboardConnection"].ConnectionString;

            var _serviceBusConn = ConfigurationManager
                .ConnectionStrings["MyServiceBusConnection"].ConnectionString;

            JobHostConfiguration config = new JobHostConfiguration();
            config.StorageConnectionString = _storageConn;
            config.DashboardConnectionString = _dashboardConn;
            config.ServiceBusConnectionString = _serviceBusConn;
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="configure-queuetrigger--settings"></a>Настройка параметров атрибута QueueTrigger
Можно настроить следующие параметры, которые применяются для обработки сообщений в очереди toohello hello.

* Здравствуйте, максимальное количество сообщений, которые извлекаются одновременно toobe параллельного выполнения (по умолчанию — 16).
* Здравствуйте, максимальное число повторных попыток перед отправкой сообщения в очереди tooa очереди подозрительных сообщений (по умолчанию — 5).
* Hello максимальное время ожидания перед запросом еще раз, когда очередь пуста (по умолчанию — 1 минута).

Следующий пример показывает как Hello tooconfigure эти параметры:

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a>Установка значений параметров конструктора пакета SDK для заданий WebJob в коде
Иногда требуется toospecify имя очереди, имя BLOB-объекта или контейнера, или имя таблицы, в коде, вместо жестко его. Например, может потребоваться имя очереди hello toospecify для **QueueTrigger** в переменной среде или файла конфигурации.

Это можно сделать путем передачи **NameResolver** объекта toohello **JobHostConfiguration** типа. Включает специальные заполнители, заключенная в символы процента (%) в конструктор атрибута SDK веб-задания параметров и **NameResolver** код задает toobe hello фактические значения, используемые вместо эти заполнители.

Например предположим, что нужно toouse очереди с именем, logqueuetest в тестовой среде hello и один именованный logqueueprod в рабочей среде. Вместо жестко очереди, необходимо, чтобы имя hello toospecify записи в hello **appSettings** коллекцию, которая будет иметь имя фактического очереди hello. Если hello **appSettings** ключа является logqueue, функция может выглядеть следующим образом hello в следующем примере.

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

Ваш **NameResolver** класс затем удалось получить имя очереди hello из **appSettings** как показано в следующий пример hello:

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

Передайте hello **NameResolver** класса в toohello **JobHost** объекта, как показано в следующий пример hello.

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

**Примечание:** очередей, таблиц и имена больших двоичных объектов не будут разрешены при каждом вызове функции, но имена контейнеров больших двоичных объектов разрешаются только при запуске приложения hello. Невозможно изменить имя контейнера больших двоичных объектов, пока выполняется задание hello.

## <a name="how-tootrigger-a-function-manually"></a>Как tootrigger функции вручную
tootrigger функцию вручную, используйте hello **вызвать** или **CallAsync** метод hello **JobHost** объекта и hello **NoAutomaticTrigger** атрибут функции hello, как показано в следующий пример hello.

        public class Program
        {
            static void Main(string[] args)
            {
                JobHost host = new JobHost();
                host.Call(typeof(Program).GetMethod("CreateQueueMessage"), new { value = "Hello world!" });
            }

            [NoAutomaticTrigger]
            public static void CreateQueueMessage(
                TextWriter logger,
                string value,
                [Queue("outputqueue")] out string message)
            {
                message = value;
                logger.WriteLine("Creating queue message: ", message);
            }
        }

## <a name="how-toowrite-logs"></a>Каким образом ведет журнал toowrite
Hello панели мониторинга показывает журналы в двух местах: hello hello веб-задания и странице приветствия для конкретного вызова веб-задания.

![Журналы на странице задания WebJob](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![Журналы на странице вызова функций](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

Выходные данные консоли методы, вызываемые в функции или hello **Main()** метод отображается в странице панели мониторинга hello hello веб-задания, а не в страницу приветствия для вызова определенного метода. Выходные данные из объекта TextWriter hello, которое получается из параметра в подписи метода отображается на странице панели мониторинга hello для вызова метода.

Вывод на консоль не может быть вызова определенного метода связанного tooa, поскольку hello консоли является однопоточным, хотя многие функции задания, запущенные на hello то же время. Вот почему hello SDK предоставляет каждый вызов функции с свой собственный уникальный журнал объект модуля записи.

toowrite [журналы трассировки приложения](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), используйте **Console.Out** (создает журналы, которые помечены как информация) и **Console.Error** (создает журналы, которые помечены как ошибки). Альтернативным вариантом является toouse [трассировки или TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), который предоставляет подробные сведения, предупреждение, и критическое уровни tooInfo сложения и ошибки. Журналы трассировки приложения отображаются в файлах журналов приложения web hello, таблицы Azure или больших двоичных объектов Azure в зависимости от того, как настроить Azure веб-приложения. Имеет значение true, если все вывода на консоль, самых последних журналов 100 приложения hello также отображаются в странице панели мониторинга hello hello веб-задания, не странице приветствия для вызова функции.

Вывод на консоль будет hello панели мониторинга только в том случае, если программа hello выполняется в веб-задания Azure, не в том случае, если программа hello выполняется локально или в некоторых других условиях.

Ведение журнала можно отключить, установив подключение строку hello мониторинга toonull. Дополнительные сведения см. в разделе [как tooset параметры конфигурации](#how-to-set-configuration-options).

Hello следующем примере показано несколько способов toowrite журналы:

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

Здравствуйте, выходные данные hello в hello мониторинга SDK веб-заданий, **TextWriter** объекта появляется при открытии страницы toohello для какого-либо вызов функции и выберите **переключить вывод**:

![Ссылка для вызова](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![Журналы на странице вызова функций](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

В hello мониторинга SDK веб-заданий, hello последние 100 строк консоли вывода Показать вверх, если переход на страницу toohello для hello веб-задания (не для вызова функций hello) и выберите **переключить вывод**.

![Переключить выходные данные](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

В непрерывное веб-задание, журнал приложений отображаются в/данных/задания и непрерывной/*{webjobname}*/job_log.txt в hello web app файловой системы.

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

В приложении hello BLOB-объектов Azure журналы будут выглядеть следующим образом: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Здравствуй, мир!, 2014-09-26T21:01:13 ошибки, contosoadsnew, 491e54, 635473620738373502,0,17404,19,Console.Error - Здравствуй, мир!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Здравствуй, мир!,

И в таблице Azure hello **Console.Out** и **Console.Error** журналы выглядеть следующим образом:

![Журнал Info в таблице](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Журнал Error в таблице](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a>Дальнейшие действия
В этой статье был дан код образцы где показано, как toohandle распространенные сценарии для работы с очередями Azure. Дополнительные сведения о статье toouse веб-заданий Azure и hello SDK веб-заданий [ресурсы документации веб-заданий Azure](http://go.microsoft.com/fwlink/?linkid=390226).

