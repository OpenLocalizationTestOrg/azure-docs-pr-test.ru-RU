---
title: "aaaHow toouse хранилище больших двоичных объектов с hello SDK веб-заданий"
description: "Узнайте, как toouse Azure хранилище больших двоичных объектов с hello SDK веб-заданий. Вызов процесса при появлении нового большого двоичного объекта в контейнере и обработка подозрительных больших двоичных объектов."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.assetid: bf32f919-f7bc-4aaa-916e-461c02f2e26c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: b34ea8cffee7c0475641886150dee521130a3132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-with-hello-webjobs-sdk"></a>Как toouse Azure хранилище больших двоичных объектов с hello SDK веб-заданий
## <a name="overview"></a>Обзор
В этом руководстве содержатся C# образцы кода, Показать как tootrigger процесса при создании или обновлении большого двоичного объекта Azure. Используйте образцы кода Hello [SDK веб-заданий](websites-dotnet-webjobs-sdk.md) версии 1.x.

Примеры кода, которые показывают, как toocreate больших двоичных объектов см. в разделе [как хранилище с hello SDK веб-заданий очередей toouse Azure](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Hello руководстве предполагается, вы знаете [как toocreate проект веб-задания в Visual Studio с подключением строки этой учетной записи хранения точки tooyour](websites-dotnet-webjobs-sdk-get-started.md) или слишком[нескольких учетных записей хранения](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

## <a id="trigger"></a>Как tootrigger функции при создании или обновлении большого двоичного объекта
В этом разделе показано, как toouse hello `BlobTrigger` атрибута. 

> [!NOTE]
> Здравствуйте, toowatch SDK веб-заданий сканирования журнала файлов для новых или измененных больших двоичных объектов. Этот процесс не находится в режиме реального времени; функция может не происходит до нескольких минут или больше после создания большого двоичного объекта hello. Кроме того, [журналы службы хранилища создаются по принципу лучшего из возможного](https://msdn.microsoft.com/library/azure/hh343262.aspx), то есть не гарантируется регистрация всех событий. В некоторых случаях журналы могут пропускаться. Hello скорость и надежность ограничения триггеров больших двоичных объектов, не подходящий для вашего приложения, hello рекомендуется метод, который toocreate сообщения в очереди, при создании большого двоичного объекта hello и использовать hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) вместо атрибута Hello `BlobTrigger` атрибут hello функция, которая обрабатывает hello большого двоичного объекта.
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a>Один заполнитель для имени большого двоичного объекта и расширения
Hello следующий код копирует текст больших двоичных объектов, которые отображаются в hello *ввода* toohello контейнера *вывода* контейнера:

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

Конструктор атрибута Hello принимает строковый параметр, указывающий имя контейнера hello и hello имя большого двоичного объекта. В этом примере, если большой двоичный объект с именем *Blob1.txt* создается в hello *ввода* контейнер, функции hello создает большой двоичный объект с именем *Blob1.txt* в hello *выходных данных*  контейнера. 

Можно указать шаблон имени с прототипа имя большого двоичного объекта hello, как показано в hello следующий образец кода:

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

Этот код копируется только большие двоичные объекты, имена которых начинаются с original-. Например *Blob1.txt исходный* в hello *ввода* контейнера копируется слишком*копирования Blob1.txt* в hello *выходные данные* контейнера.

Если вам требуется шаблон имени toospecify имена больших двоичных объектов, имеющих фигурные скобки в имени hello, двойные фигурные скобки hello. Например, если вы хотите toofind большие двоичные объекты в hello *изображения* контейнер с именами следующим образом:

        {20140101}-soundfile.mp3

используйте следующую команду для своего шаблона:

        images/{{20140101}}-{name}

В примере hello hello *имя* бы значение заполнителя *soundfile.mp3*. 

### <a name="separate-blob-name-and-extension-placeholders"></a>Отдельные заполнители для имени большого двоичного объекта и расширения
Hello следующие изменения кода образца hello расширение файла его по мере копирования больших двоичных объектов, которые отображаются в hello *ввода* toohello контейнера *вывода* контейнера. Hello код регистрирует расширение hello hello *ввода* больших двоичных объектов и задает расширение hello hello *вывода* слишком большой двоичный объект*.txt*.

        public static void CopyBlobToTxtFile([BlobTrigger("input/{name}.{ext}")] TextReader input,
            [Blob("output/{name}.txt")] out string output,
            string name,
            string ext,
            TextWriter logger)
        {
            logger.WriteLine("Blob name:" + name);
            logger.WriteLine("Blob extension:" + ext);
            output = input.ReadToEnd();
        }

## <a id="types"></a>Типы, что вы можете привязать tooblobs
Можно использовать hello `BlobTrigger` атрибут hello следующие типы:

* `string`
* `TextReader`
* `Stream`
* `ICloudBlob`
* `CloudBlockBlob`
* `CloudPageBlob`
* `CloudBlobContainer`
* `CloudBlobDirectory`
* `IEnumerable<CloudBlockBlob>`
* `IEnumerable<CloudPageBlob>`
* другие типы, десериализованные с помощью [ICloudBlobStreamBinder](#icbsb) 

Если требуется toowork непосредственно с hello учетной записи хранилища Azure, можно добавить `CloudStorageAccount` сигнатура метода toohello параметра.

Примеры см. в разделе hello [больших двоичных объектов код привязки в репозитории hello пакет sdk веб-заданий azure на GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).

## <a id="string"></a>Получение текстового содержимого больших двоичных объектов с toostring привязки
Если ожидаются текст больших двоичных объектов, `BlobTrigger` может быть применен tooa `string` параметра. Hello следующий код привязывает большого двоичного объекта текст tooa `string` параметр с именем `logMessage`. функция Hello использует этот параметр toowrite hello содержимое toohello hello большого двоичного объекта панели мониторинга пакета SDK веб-заданий. 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a id="icbsb"></a> Получение содержимого сериализованного большого двоичного объекта с помощью ICloudBlobStreamBinder
Hello следующий код использует класс, реализующий `ICloudBlobStreamBinder` tooenable hello `BlobTrigger` атрибута toobind toohello большой двоичный объект `WebImage` типа.

        public static void WaterMark(
            [BlobTrigger("images3/{name}")] WebImage input,
            [Blob("images3-watermarked/{name}")] out WebImage output)
        {
            output = input.AddTextWatermark("WebJobs SDK", 
                horizontalAlign: "Center", verticalAlign: "Middle",
                fontSize: 48, opacity: 50);
        }
        public static void Resize(
            [BlobTrigger("images3-watermarked/{name}")] WebImage input,
            [Blob("images3-resized/{name}")] out WebImage output)
        {
            var width = 180;
            var height = Convert.ToInt32(input.Height * 180 / input.Width);
            output = input.Resize(width, height);
        }

Hello `WebImage` предоставлены привязки кода в `WebImageBinder` класс, производный от `ICloudBlobStreamBinder`.

        public class WebImageBinder : ICloudBlobStreamBinder<WebImage>
        {
            public Task<WebImage> ReadFromStreamAsync(Stream input, 
                System.Threading.CancellationToken cancellationToken)
            {
                return Task.FromResult<WebImage>(new WebImage(input));
            }
            public Task WriteToStreamAsync(WebImage value, Stream output,
                System.Threading.CancellationToken cancellationToken)
            {
                var bytes = value.GetBytes();
                return output.WriteAsync(bytes, 0, bytes.Length, cancellationToken);
            }
        }

## <a name="getting-hello-blob-path-for-hello-triggering-blob"></a>Получение пути к BLOB-объектов hello для hello, активируя больших двоичных объектов
Имя контейнера tooget hello и больших двоичных объектов для hello BLOB-объект, который инициировал функции hello включают `blobTrigger` строковый параметр в сигнатуре функции hello.

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <a id="poison"></a>Способ обработки подозрительных сообщений toohandle больших двоичных объектов
Если `BlobTrigger` функция завершается с ошибкой, hello SDK вызывает ее еще раз, в случае сбоя hello было вызвано временной ошибкой. Если причиной сбоя hello является hello содержимое большого двоичного объекта hello, функции hello завершается ошибкой, каждый раз, он пытается tooprocess hello больших двоичных объектов. По умолчанию hello SDK вызывает функцию too5 времени для данного большого двоичного объекта. В случае попробуйте пятый hello hello SDK добавляет tooa очереди сообщений с именем *веб-заданий blobtrigger обработки подозрительных сообщений*.

Максимальное число повторных попыток для Hello настраивается. Здравствуйте же [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) параметр используется для обработки подозрительных большого двоичного объекта и обработки сообщений в очереди подозрительных сообщений. 

приветственное сообщение очереди подозрительных больших двоичных объектов является объект JSON, содержащий hello следующие свойства:

* Идентификатор FunctionId (в формате hello *{имя веб-задания}*. Функции. *{Имя функции}*, например: WebJob1.Functions.CopyBlob)
* BlobType (BlockBlob или PageBlob);
* ContainerName;
* BlobName
* ETag (идентификатор версии BLOB-объектов, например 0x8D1DC6E70A277EF)

В следующих hello образец кода, hello `CopyBlob` функция имеет код, который вызывает toofail при каждом вызове. После его вызывает hello пакета SDK для hello максимальное число повторных попыток, создается сообщение в очереди подозрительных blob hello и этого сообщение обрабатывается hello `LogPoisonBlob` функции. 

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("textblobs/output-{name}")] out string output)
        {
            throw new Exception("Exception for testing poison blob handling");
            output = input.ReadToEnd();
        }

        public static void LogPoisonBlob(
        [QueueTrigger("webjobs-blobtrigger-poison")] PoisonBlobMessage message,
            TextWriter logger)
        {
            logger.WriteLine("FunctionId: {0}", message.FunctionId);
            logger.WriteLine("BlobType: {0}", message.BlobType);
            logger.WriteLine("ContainerName: {0}", message.ContainerName);
            logger.WriteLine("BlobName: {0}", message.BlobName);
            logger.WriteLine("ETag: {0}", message.ETag);
        }

Hello SDK автоматически десериализует сообщение hello JSON. Вот hello `PoisonBlobMessage` класса: 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a id="polling"></a> Алгоритм опроса больших двоичных объектов
Hello SDK веб-заданий просматривает все контейнеры, указанные по `BlobTrigger` атрибуты при запуске приложения. Такая проверка может занять некоторое время в большой учетной записи хранения. Поэтому для поиска новых больших двоичных объектов и выполнения функций `BlobTrigger` может потребоваться много времени.

toodetect новые или измененные BLOB-объектов после запуска приложения hello, которые пакет SDK периодически считывает из хранилища больших двоичных объектов hello заносит в журнал. Hello большого двоичного объекта помещаются в буфер и журналы только физически записываются каждые 10 минут или таким образом, поэтому могут существовать значительные задержки после большой двоичный объект создается или обновляется перед соответствующими hello `BlobTrigger` функция выполняет. 

Существует одно исключение для больших двоичных объектов, которые создаются с помощью hello `Blob` атрибута. Когда hello SDK веб-задания создается новый большой двоичный объект, он передает новый большой двоичный объект hello немедленно сопоставления tooany `BlobTrigger` функции. Таким образом Если цепочка blob входы и выходы, hello SDK можно их эффективной обработки. Но если при выполнении функций обработки больших двоичных объектов, созданных или обновленных другими способами, нужны малые задержки, советуем использовать `QueueTrigger` вместо `BlobTrigger`.

### <a id="receipts"></a> Уведомления о получении большого двоичного объекта
Hello SDK веб-заданий гарантирует, что не `BlobTrigger` функция вызывается несколько раз для hello же новые или обновлении большого двоичного объекта. Это делается путем сохранения *большого двоичного объекта уведомления* в порядке toodetermine обработанными версии данного большого двоичного объекта.

BLOB-объект уведомления хранятся в контейнер с именем *размещаемые на веб-заданий для azure* в учетной записи хранилища Azure hello, hello AzureWebJobsStorage строку подключения. Получение большого двоичного объекта имеет hello следующую информацию:

* Здравствуйте, функция, которая была вызвана для hello большого двоичного объекта (»*{имя веб-задания}*. Функции. *{Имя функции}*», например: «WebJob1.Functions.CopyBlob»)
* Имя контейнера Hello
* Тип большого двоичного объекта Hello («BlockBlob» или «PageBlob»)
* Имя BLOB-объекта Hello
* Hello ETag (идентификатор версии большого двоичного объекта, например: «0x8D1DC6E70A277EF»)

Если требуется повторная обработка tooforce большого двоичного объекта, можно вручную удалить уведомление hello больших двоичных объектов для данного большого двоичного объекта из hello *размещаемые на веб-заданий для azure* контейнера.

## <a id="queues"></a>Связанные разделы, охватываемых статьи очереди hello
Сведения о обработки больших двоичных объектов toohandle запуска, очереди сообщений и для веб-задания сценариев SDK не содержатся определенные tooblob обработки, [как хранилище с hello SDK веб-заданий очередей toouse Azure](websites-dotnet-webjobs-sdk-storage-queues-how-to.md). 

Связанные разделы, описанные в этой статье hello следующие:

* Асинхронные функции
* Выполнение на нескольких экземплярах
* Корректное завершение работы
* Использование пакета SDK веб-задания атрибутов в теле функции hello
* Задать строки подключения пакета SDK для hello в коде.
* Установка значений параметров конструктора пакета SDK для заданий WebJob в коде
* Настройка `MaxDequeueCount` для обработки подозрительных больших двоичных объектов
* Вызов функции вручную
* Запись журналов

## <a id="nextsteps"></a> Дальнейшие действия
Это руководство предоставляет образцы кода где показано, как большие двоичные объекты toohandle распространенные сценарии для работы с Azure. Дополнительные сведения о статье toouse веб-заданий Azure и hello SDK веб-заданий [рекомендуется заданиям Azure](http://go.microsoft.com/fwlink/?linkid=390226).

