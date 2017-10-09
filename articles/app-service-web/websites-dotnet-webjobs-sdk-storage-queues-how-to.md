---
title: "aaaHow toouse хранилища очереди Azure с hello SDK веб-заданий"
description: "Узнайте, как хранилище с hello SDK веб-заданий очередей toouse Azure. Создание и удаление очередей; вставка, обзор, получение и удаление сообщений очереди, а также многое другое."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: dbfac5d9-f4a0-4e3e-9ecc-af3d7bf80463
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 49f844436b0453489800b2762a5c7dc30b9db805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-queue-storage-with-hello-webjobs-sdk"></a>Как toouse Azure очередь хранилища с hello SDK веб-заданий
## <a name="overview"></a>Обзор
Это руководство содержит образцы кода C#, которые показывают, как toouse hello веб-заданий Azure SDK версии 1.x hello службы хранилища очередей Azure.

Hello руководстве предполагается, вы знаете [как toocreate проект веб-задания в Visual Studio с подключением строки этой учетной записи хранения точки tooyour](websites-dotnet-webjobs-sdk-get-started.md) или слишком[нескольких учетных записей хранения](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

Большинство фрагментов кода hello Показывать только функции, не hello код, создающий hello `JobHost` объекта, как показано в примере:

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

Hello руководство включает hello следующие вопросы:

* [Как tootrigger функции при получении сообщения в очереди](#trigger)
  * Строковые сообщения очереди
  * Сообщения очереди POCO
  * Асинхронные функции
  * Атрибут QueueTrigger hello типы работает с
  * Алгоритм опроса
  * Выполнение на нескольких экземплярах
  * Параллельное выполнение
  * Получение очереди или метаданных очереди сообщений
  * Корректное завершение работы
* [Как toocreate очереди сообщений во время обработки сообщения в очереди](#createqueue)
  * Строковые сообщения очереди
  * Сообщения очереди POCO
  * Создание нескольких сообщений или сообщений в асинхронных функциях
  * Атрибут очереди hello типы работает с
  * Использование пакета SDK веб-задания атрибутов в теле функции hello
* [Как tooread и записи больших двоичных объектов при обработке сообщения в очереди](#blobs)
  * Строковые сообщения очереди
  * Сообщения очереди POCO
  * Типы hello большого двоичного объекта атрибута работает с
* [Как toohandle подозрительные сообщения](#poison)
  * Автоматическая обработка сообщений
  * Ручная обработка подозрительных сообщений
* [Как параметры конфигурации tooset](#config)
  * Установка строк подключения пакета SDK в коде
  * Настройка параметров атрибута QueueTrigger
  * Установка значений параметров конструктора пакета SDK для заданий WebJob в коде
* [Как tootrigger функции вручную](#manual)
* [Каким образом ведет журнал toowrite](#logs)
* [Как toohandle ошибки и настроить время ожидания](#errors)
* [Дальнейшие действия](#nextsteps)

## <a id="trigger"></a>Как tootrigger функции при получении сообщения в очереди
вызывает функцию, которая hello SDK веб-заданий toowrite при получении сообщения в очереди, используйте hello `QueueTrigger` атрибута. Конструктор атрибута Hello принимает строковый параметр, задающий имя hello toopoll очереди hello. Вы также можете [динамически задать имя очереди hello](#config).

### <a name="string-queue-messages"></a>Строковые сообщения очереди
В следующем примере hello, hello очередь содержит строковое сообщение, поэтому `QueueTrigger` будет применен tooa строковый параметр с именем `logMessage` , содержащее содержимое очереди приветственное сообщение hello. Здравствуйте, функция [записывает toohello сообщение журнала мониторинга](#logs).

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

Помимо `string`, hello параметр может быть массив байтов `CloudQueueMessage` объекта или POCO, определяемому вами.

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>Сообщения очереди [POCO](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)
В следующем примере hello, сообщение hello очереди содержит JSON для `BlobInformation` объекта, который включает `BlobName` свойство. пакет SDK для Hello автоматически десериализует hello объекта.

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Hello SDK использует hello [пакет Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize и десериализации сообщений. При создании очереди сообщений в программе, которая не использует hello SDK веб-задания, можно написать код, как следующий пример toocreate POCO очереди сообщений hello приветствия, можно провести синтаксический анализ пакета SDK.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a>Асинхронные функции
После асинхронного функции Hello [записывает журнал toohello мониторинга](#logs).

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

Может потребоваться асинхронных функций [токен отмены](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), как показано в hello следующий пример, который копирует большой двоичный объект. (Объяснение hello `queueTrigger` заполнитель, в разделе hello [большие двоичные объекты](#blobs) раздел.)

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <a id="qtattributetypes"></a>Атрибут QueueTrigger hello типы работает с
Можно использовать `QueueTrigger` с hello следующие типы:

* `string`
* тип POCO, сериализованный как JSON;
* `byte[]`
* `CloudQueueMessage`

### <a id="polling"></a> Алгоритм опроса
Hello SDK реализует эффекта экспоненциальной отсрочки алгоритм случайных tooreduce hello простоя очереди опроса на транзакционные издержки хранения.  При обнаружении сообщение hello SDK ожидает в течение двух секунд и затем проверяет наличие другого сообщения; Если сообщение не найдено он ожидает около четырех секунд перед повторной попыткой. После tooget последующих неудачных попытках сообщения в очереди, время ожидания hello продолжается tooincrease, пока не достигнет hello максимальное время ожидания, какие значения по умолчанию tooone минуты. [Hello максимальное время ожидания настраивается](#config).

### <a id="instances"></a> Выполнение на нескольких экземплярах
Если веб-приложение выполняется на нескольких экземплярах, непрерывное веб-задание выполняется на каждом компьютере, и каждой машины будет ожидать триггеры и повторите toorun функции. Hello SDK веб-задания очереди триггера автоматически предотвращает функции обработки сообщения в очереди несколько раз. функции не имеют toobe записи toobe идемпотентными. Тем не менее, если требуется tooensure только одного экземпляра функции выполняется даже в том случае, если существует несколько экземпляров веб-приложения hello узла, можно использовать hello `Singleton` атрибута.

### <a id="parallel"></a> Параллельное выполнение
Если у вас есть несколько функций, которые прослушивают различные очереди, hello SDK вызывает их параллельно при получении сообщений одновременно.

Hello это верно и при получении нескольких сообщений для одной очереди. По умолчанию hello SDK получает пакет 16 очереди сообщений за раз и выполняет функции hello, обрабатывает их параллельно. [размер пакета Hello настраивается](#config). При получении hello число обрабатываемых вниз toohalf размера пакета hello, hello SDK возвращает другой пакет и начинает обработку этих сообщений. Поэтому hello максимальное количество одновременных сообщений, обрабатываемых каждой функции является размер пакета в полтора раза hello. Это ограничение применяется отдельно tooeach функции, которая имеет `QueueTrigger` атрибута.

Если вы не хотите параллельного выполнения для сообщений, полученных на одну очередь, можно задать размер too1 hello пакета. Ознакомьтесь также с подразделом **More control over Queue processing** (Больший контроль над обработкой очередей) в статье [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/) (Пакет SDK Azure для веб-заданий 1.1.0 RTM).

### <a id="queuemetadata"></a>Получение очереди или метаданных очереди сообщений
Можно получить следующие свойства сообщения, добавив параметры сигнатуры метода toohello hello:

* `DateTimeOffset` expirationTime;
* `DateTimeOffset` insertionTime;
* `DateTimeOffset` nextVisibleTime;
* `string` queueTrigger (содержит текст сообщения);
* `string` id;
* `string` popReceipt;
* `int` dequeueCount.

Если требуется toowork непосредственно с hello хранилища Azure API, можно добавить `CloudStorageAccount` параметра.

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

### <a id="graceful"></a>Нормальное завершение работы
Функция, которая выполняется в непрерывных веб-задания может принимать `CancellationToken` параметр, который позволяет функции hello операционной системы toonotify hello при hello веб-задания — о toobe завершен. Можно использовать toomake это уведомление о том, что функции hello не привести к непредвиденному завершению способом, который оставляет данных в несогласованном состоянии.

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

## <a id="createqueue"></a>Как toocreate очереди сообщений во время обработки сообщения в очереди
функция, которая создает новое сообщение очереди, используйте hello toowrite `Queue` атрибута. Как `QueueTrigger`, передав имя очереди hello в виде строки, или вы можете [динамически задать имя очереди hello](#config).

### <a name="string-queue-messages"></a>Строковые сообщения очереди
Следующий образец кода синхронные Hello создает новое сообщение очереди в очередь hello, с именем «outputqueue» с таким же содержимое, так как очередь приветственное сообщение получено в hello очереди с именем «inputqueue» hello. (Для асинхронных функций используйте `IAsyncCollector<T>` , следуя указаниям далее в этом разделе.)

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>Сообщения очереди [POCO](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)
toocreate очереди сообщение, содержащее POCO, а не строкой, pass hello POCO тип в качестве выходного параметра toohello `Queue` конструктор атрибута.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

пакет SDK для Hello автоматически сериализует tooJSON hello объекта. Очередь сообщений создается всегда, даже если hello объекта имеет значение null.

### <a name="create-multiple-messages-or-in-async-functions"></a>Создание нескольких сообщений или сообщений в асинхронных функциях
toocreate несколько сообщений сделать hello тип параметра для очереди вывода hello `ICollector<T>` или `IAsyncCollector<T>`, как показано в следующий пример hello.

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Каждое сообщение очереди создается сразу после hello `Add` вызывается метод.

### <a name="types-that-hello-queue-attribute-works-with"></a>Типы атрибута очереди hello работает с
Можно использовать hello `Queue` атрибутов на следующие типы параметра hello:

* `out string`(если значение параметра не равно null, при завершении функции hello создает сообщения в очереди)
* `out byte[]` (действует как `string`);
* `out CloudQueueMessage` (действует как `string`);
* `out POCO`(сериализуемый тип, создает сообщение с пустым объектом Если hello имеет значение null, при завершении функции hello)
* `ICollector`
* `IAsyncCollector`
* `CloudQueue`(для создания сообщений вручную с помощью API хранилища Azure hello непосредственно)

### <a id="ibinder"></a>Использование пакета SDK веб-задания атрибутов в теле функции hello
Если вам требуется toodo некоторые работать в функции перед использованием атрибут SDK веб-заданий, таких как `Queue`, `Blob`, или `Table`, можно использовать hello `IBinder` интерфейса.

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

Hello `IBinder` интерфейс может также использоваться с hello `Table` и `Blob` атрибуты.

## <a id="blobs"></a>Как tooread и записи больших двоичных объектов и таблиц во время обработки сообщения в очереди
Hello `Blob` и `Table` атрибуты позволяют tooread и записи больших двоичных объектов и таблиц. Hello образцы в этом разделе применяются tooblobs. Примеры кода, которые показывают, как tootrigger обрабатывает при создании или обновлении больших двоичных объектов см. в разделе [как toouse Azure хранилище больших двоичных объектов с hello SDK веб-заданий](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)и примеры кода, которые считывают и записывают таблиц см. в разделе [как toouse таблицы Azure хранилище с hello SDK веб-задания](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).

### <a name="string-queue-messages-triggering-blob-operations"></a>Сообщения очереди строк, которые запускают операции с большими двоичными объектами
Для очереди сообщение, содержащее строку `queueTrigger` — это, можно использовать в hello `Blob` атрибута `blobPath` параметра, который содержит содержимое приветственное сообщение hello.

Hello следующий пример использует `Stream` объектов tooread и записи больших двоичных объектов. приветственное сообщение очереди — hello имя BLOB-объектов, находящихся в контейнере textblobs hello. Копия hello большой двоичный объект с «-новые» присоединенных toohello имя создается в hello же контейнер.

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Hello `Blob` атрибута конструктор принимает `blobPath` параметр, определяющий hello контейнера и имя большого двоичного объекта. Дополнительные сведения об этом заполнитель см. в разделе [как toouse Azure хранилище больших двоичных объектов с hello SDK веб-заданий](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),

Если атрибут hello оформляет `Stream` другой конструктор указывает hello объекта `FileAccess` режим чтения, записи или чтения и записи.

Hello следующий пример использует `CloudBlockBlob` объекта toodelete большого двоичного объекта. приветственное сообщение очереди является именем hello hello большого двоичного объекта.

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a id="pocoblobs"></a> Сообщения очереди [POCO](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)
Для POCO, хранятся в очереди сообщение hello как JSON, можно использовать местозаполнители, имя свойства объекта hello в hello `Queue` атрибута `blobPath` параметра. Можно также использовать [имена свойства метаданных очереди](#queuemetadata) в качестве заполнителей.

Hello следующий пример копирует BLOB-объектов tooa новый большой двоичный объект с другим расширением. сообщение Hello очереди `BlobInformation` объект, который содержит `BlobName` и `BlobNameWithoutExtension` свойства. имена свойств Hello используются в качестве меток-заполнителей в пути hello больших двоичных объектов для hello `Blob` атрибуты.

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

Если вам требуется toodo некоторые работают в функции перед привязкой tooan большой двоичный объект, можно использовать атрибут hello в тексте hello функции hello [как показано выше, для атрибута очереди hello](#ibinder).

### <a id="blobattributetypes"></a>Типы, которые можно использовать hello атрибута с BLOB-объектов
Hello `Blob` атрибут может использоваться с hello следующие типы:

* `Stream`(чтение или запись, указанный с помощью параметра конструктора hello FileAccess)
* `TextReader`
* `TextWriter`
* `string` (чтение);
* `out string`(записи; создает большой двоичный объект только в том случае, если параметр строки hello отлично от null, при возврате из функции hello)
* POCO (чтение);
* out POCO (записи; всегда создает большой двоичный объект, создает как объект null, если параметр POCO имеет значение null, при возврате из функции hello)
* `CloudBlobStream` (запись);
* `ICloudBlob` (чтение или запись);
* `CloudBlockBlob` (чтение или запись);
* `CloudPageBlob` (чтение или запись);

## <a id="poison"></a>Как toohandle подозрительные сообщения
Сообщения, содержимое которого приводит toofail функции называются *сообщения о сбое*. При сбое функции hello, очередь приветственное сообщение не удаляется и в конечном счете передается еще раз, может вызвать toobe hello цикл повторяется. Hello SDK можно прервать цикл hello автоматически после ограниченного числа итераций, или это можно сделать вручную.

### <a name="automatic-poison-message-handling"></a>Автоматическая обработка сообщений
Hello SDK будет вызвать функцию копирования tooprocess раз too5 сообщения в очереди. При сбое hello пятый try, приветственное сообщение — перемещенный tooa очереди подозрительных сообщений. [Максимальное число повторных попыток для Hello настраивается](#config).

очередь подозрительных сообщений Hello называется *{originalqueuename}*-подозрительное. Можно написать tooprocess функция сообщения из очереди подозрительных сообщений hello ее регистрации или отправка уведомления о необходимости ручного вмешательства.

В следующий пример hello hello `CopyBlob` функция завершится ошибкой, если сообщения в очереди содержит hello имя большого двоичного объекта, который не существует. В этом случае приветственное сообщение перемещается из hello copyblobqueue очереди toohello copyblobqueue подозрительных очереди. Hello `ProcessPoisonMessage` то подозрительное сообщение hello журналы.

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

![Вывод консоли для обработки подозрительных сообщений](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a>Ручная обработка подозрительных сообщений
Hello количество обработки сообщения для обработки можно получить, добавив `int` параметр с именем `dequeueCount` tooyour функции. После этого можно hello проверьте количество в коде функция вывода из очереди и выполнять собственные подозрительное сообщение обработки при hello число превышает пороговое значение, как показано в следующий пример hello.

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

## <a id="config"></a>Как параметры конфигурации tooset
Можно использовать hello `JobHostConfiguration` hello tooset тип следующие параметры конфигурации:

* Задать строки подключения пакета SDK для hello в коде.
* Настройка таких параметров атрибута `QueueTrigger` , как максимальное значение счетчика вывода из очереди.
* Получение имен очередей из конфигурации

### <a id="setconnstr"></a>Установка строк подключения пакета SDK в коде
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

### <a id="configqueue"></a>Настройка параметров атрибута QueueTrigger
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

### <a id="setnamesincode"></a>Установка значений параметров конструктора пакета SDK для веб-заданий в коде
Иногда требуется toospecify имя очереди, имя BLOB-объекта или контейнера, или имя таблицы, в коде, вместо жестко его. Например, может потребоваться имя очереди hello toospecify для `QueueTrigger` в переменной среде или файла конфигурации.

Это можно сделать путем передачи `NameResolver` объекта toohello `JobHostConfiguration` типа. Включает специальные заполнители, заключенная в символы процента (%) в конструктор атрибута SDK веб-задания параметров и `NameResolver` кода задается toobe hello фактические значения, используемые вместо эти заполнители.

Например предположим, что нужно toouse очереди с именем, logqueuetest в тестовой среде hello и один именованный logqueueprod в рабочей среде. Вместо жестко очереди, необходимо, чтобы имя hello toospecify записи в hello `appSettings` коллекцию, которая будет иметь имя фактического очереди hello. Если hello `appSettings` ключа является logqueue, функция может выглядеть следующим образом hello в следующем примере.

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

Ваш `NameResolver` класс затем удалось получить имя очереди hello из `appSettings` как показано в следующий пример hello:

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

Передайте hello `NameResolver` класса в toohello `JobHost` объекта, как показано в следующий пример hello.

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

**Примечание:** очередей, таблиц и имена больших двоичных объектов не будут разрешены при каждом вызове функции, но имена контейнеров больших двоичных объектов разрешаются только при запуске приложения hello. Невозможно изменить имя контейнера больших двоичных объектов, пока выполняется задание hello.

## <a id="manual"></a>Как tootrigger функции вручную
tootrigger функцию вручную, используйте hello `Call` или `CallAsync` метод hello `JobHost` объекта и hello `NoAutomaticTrigger` атрибут функции hello, как показано в следующий пример hello.

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

## <a id="logs"></a>Каким образом ведет журнал toowrite
Hello панели мониторинга показывает журналы в двух местах: hello hello веб-задания и странице приветствия для конкретного вызова веб-задания.

![Журналы на странице задания WebJob](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![Журналы на странице вызова функций](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

Выходные данные консоли методы, вызываемые в функции или hello `Main()` метод отображается в странице панели мониторинга hello hello веб-задания, а не в страницу приветствия для вызова определенного метода. Выходные данные из объекта TextWriter hello, которое получается из параметра в подписи метода отображается на странице панели мониторинга hello для вызова метода.

Вывод на консоль не может быть вызова определенного метода связанного tooa, поскольку hello консоли является однопоточным, хотя многие функции задания, запущенные на hello то же время. Вот почему hello SDK предоставляет каждый вызов функции с свой собственный уникальный журнал объект модуля записи.

toowrite [журналы трассировки приложения](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), используйте `Console.Out` (создает журналы, которые помечены как информация) и `Console.Error` (создает журналы, которые помечены как ошибки). Альтернативным вариантом является toouse [трассировки или TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), который предоставляет подробные сведения, предупреждение, и критическое уровни tooInfo сложения и ошибки. Журналы трассировки приложения отображаются в файлах журналов приложения web hello, таблицы Azure или больших двоичных объектов Azure в зависимости от того, как настроить Azure веб-приложения. Имеет значение true, если все вывода на консоль, самых последних журналов 100 приложения hello также отображаются в странице панели мониторинга hello hello веб-задания, не странице приветствия для вызова функции.

Вывод на консоль будет hello панели мониторинга только в том случае, если программа hello выполняется в веб-задания Azure, не в том случае, если программа hello выполняется локально или в некоторых других условиях.

Отключите ведение журнала панели мониторинга для сценариев с высокой пропускной способностью. По умолчанию hello SDK записывает журналы toostorage, и это действие может привести к снижению производительности при обработке большого числа сообщений. toodisable ведения журнала, задайте соединение строку hello мониторинга toonull, как показано в следующий пример hello.

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

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

Здравствуйте, выходные данные hello в hello мониторинга SDK веб-заданий, `TextWriter` объектов появляется при открытии страницы toohello для какого-либо вызов функции и нажмите кнопку **переключить вывод**:

![Щелкнуть ссылку вызова функции](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![Журналы на странице вызова функций](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

В hello мониторинга SDK веб-заданий, hello последние 100 строк консоли вывода Показать вверх, если переход на страницу toohello для hello веб-задания (не для вызова функций hello) и нажмите кнопку **переключить вывод**.

![Нажать кнопку «Переключить вывод»](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

В непрерывное веб-задание, журнал приложений отображаются в/данных/задания и непрерывной/*{webjobname}*/job_log.txt в hello web app файловой системы.

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

В приложении hello BLOB-объектов Azure журналы будут выглядеть следующим образом: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Здравствуй, мир!, 2014-09-26T21:01:13 ошибки, contosoadsnew, 491e54, 635473620738373502,0,17404,19,Console.Error - Здравствуй, мир!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Здравствуй, мир!,

И в таблице Azure hello `Console.Out` и `Console.Error` журналы выглядеть следующим образом:

![Журнал Info в таблице](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![Журнал Error в таблице](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

Если требуется tooplug в собственные средства ведения журнала, см. раздел [в этом примере](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).

## <a id="errors"></a>Как toohandle ошибки и настроить время ожидания
Hello веб-заданий SDK также включает [время ожидания](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) атрибут, который можно использовать toocause toobe функция отменен, если не завершилось в течение указанного промежутка времени. Если требуется tooraise оповещение, когда происходит слишком много ошибок в течение указанного периода времени, можно использовать hello `ErrorTrigger` атрибута. Вот [пример ErrorTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    too= "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors toohello Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

Можно также динамически отключить и включить функции toocontrol ли они можно запустить, используя параметр конфигурации, который может быть параметра приложения или имя переменной среды. Пример кода, в разделе hello `Disable` атрибута в [hello SDK веб-заданий образцы репозитория](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).

## <a id="nextsteps"></a> Дальнейшие действия
В этом руководстве предоставила код образцы где показано, как toohandle распространенные сценарии для работы с очередями Azure. Дополнительные сведения о статье toouse веб-заданий Azure и hello SDK веб-заданий [рекомендуется заданиям Azure](http://go.microsoft.com/fwlink/?linkid=390226).
