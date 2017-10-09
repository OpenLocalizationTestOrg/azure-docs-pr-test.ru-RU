---
title: "aaaGet работы с Visual Studio и хранилище больших двоичных объектов подключенных служб (для проектов веб-задания) | Документы Microsoft"
description: "Запуск с помощью хранилища больших двоичных объектов в проекте веб-задания после подключения tooan хранилища Azure с помощью Visual Studio tooget подключенные службы."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 324c9376-0225-4092-9825-5d1bd5550058
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: cb2cecacbb1a59f093d5453a91fae33e0f279d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a>Начало работы с подключенными службами хранилища больших двоичных объектов Azure и Visual Studio (проекты веб-заданий)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Обзор
В этой статье приведены C# образцы кода, Показать как tootrigger процесса при создании или обновлении большого двоичного объекта Azure. Примеры кода Hello использовать hello [SDK веб-заданий](../app-service-web/websites-dotnet-webjobs-sdk.md) версии 1.x. При добавлении проекта веб-задания tooa учетной записи хранилища с помощью Visual Studio hello **Добавление подключенных служб** диалогового окна, установлен соответствующий пакет NuGet хранилища Azure hello, соответствующие ссылки .NET hello будут добавлены toohello в файле App.config hello обновляются проекта и строки подключения для учетной записи хранения hello.

## <a name="how-tootrigger-a-function-when-a-blob-is-created-or-updated"></a>Как tootrigger функции при создании или обновлении большого двоичного объекта
В этом разделе показано, как toouse hello **BlobTrigger** атрибута.

 **Примечание:** hello toowatch SDK веб-заданий сканирования журнала файлов для новых или измененных больших двоичных объектов. Этот процесс является по своей природе медленным; функция может не происходит до нескольких минут или больше после создания большого двоичного объекта hello.  Если приложению требуются большие двоичные объекты tooprocess немедленно, hello рекомендуется метод, который toocreate сообщения в очереди, при создании большого двоичного объекта hello и использовать hello [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) вместо hello атрибута **BlobTrigger** атрибут hello функция, которая обрабатывает hello большого двоичного объекта.

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

## <a name="types-that-you-can-bind-tooblobs"></a>Типы, что вы можете привязать tooblobs
Можно использовать hello **BlobTrigger** атрибут hello следующие типы:

* **string**
* **TextReader;**
* **Поток**
* **ICloudBlob;**
* **CloudBlockBlob**
* **CloudPageBlob.**
* другие типы, десериализованные с помощью [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)

Если требуется toowork непосредственно с hello учетной записи хранилища Azure, можно добавить **CloudStorageAccount** сигнатура метода toohello параметра.

## <a name="getting-text-blob-content-by-binding-toostring"></a>Получение текстового содержимого больших двоичных объектов с toostring привязки
Если ожидаются текст больших двоичных объектов, **BlobTrigger** может быть применен tooa **строка** параметра. Hello следующий код привязывает большого двоичного объекта текст tooa **строка** параметр с именем **logMessage**. функция Hello использует этот параметр toowrite hello содержимое toohello hello большого двоичного объекта панели мониторинга пакета SDK веб-заданий.

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a>Получение содержимого сериализованного большого двоичного объекта с помощью ICloudBlobStreamBinder
Hello следующий код использует класс, реализующий **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** атрибута toobind toohello большого двоичного объекта **WebImage** типа.

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

Hello **WebImage** предоставлены привязки кода в **WebImageBinder** класс, производный от **ICloudBlobStreamBinder**.

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

## <a name="how-toohandle-poison-blobs"></a>Способ обработки подозрительных сообщений toohandle больших двоичных объектов
Когда **BlobTrigger** функция завершается с ошибкой, hello SDK вызывает ее еще раз, в случае сбоя hello было вызвано временной ошибкой. Если причиной сбоя hello является hello содержимое большого двоичного объекта hello, функции hello завершается ошибкой, каждый раз, он пытается tooprocess hello больших двоичных объектов. По умолчанию hello SDK вызывает функцию too5 времени для данного большого двоичного объекта. В случае попробуйте пятый hello hello SDK добавляет tooa очереди сообщений с именем *веб-заданий blobtrigger обработки подозрительных сообщений*.

Максимальное число повторных попыток для Hello настраивается. Здравствуйте же [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) параметр используется для обработки подозрительных большого двоичного объекта и обработки сообщений в очереди подозрительных сообщений.

приветственное сообщение очереди подозрительных больших двоичных объектов является объект JSON, содержащий hello следующие свойства:

* Идентификатор FunctionId (в формате hello *{имя веб-задания}*. Функции. *{Имя функции}*, например: WebJob1.Functions.CopyBlob)
* BlobType (BlockBlob или PageBlob);
* ContainerName;
* BlobName
* ETag (идентификатор версии BLOB-объектов, например 0x8D1DC6E70A277EF)

В следующих hello образец кода, hello **CopyBlob** функция имеет код, который вызывает toofail при каждом вызове. После его вызывает hello пакета SDK для hello максимальное число повторных попыток, создается сообщение в очереди подозрительных blob hello и этого сообщение обрабатывается hello **LogPoisonBlob** функции.

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

Hello SDK автоматически десериализует сообщение hello JSON. Вот hello **PoisonBlobMessage** класса:

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a>Алгоритм опроса больших двоичных объектов
Hello SDK веб-заданий просматривает все контейнеры, указанные по **BlobTrigger** атрибуты при запуске приложения. Такая проверка может занять некоторое время в большой учетной записи хранения. Поэтому для поиска новых больших двоичных объектов и выполнения функций **BlobTrigger** может потребоваться заметное количество времени.

toodetect новые или измененные BLOB-объектов после запуска приложения hello, которые пакет SDK периодически считывает из хранилища больших двоичных объектов hello заносит в журнал. Hello большого двоичного объекта помещаются в буфер и журналы только физически записываются каждые 10 минут или таким образом, поэтому могут существовать значительные задержки после большой двоичный объект создается или обновляется перед соответствующими hello **BlobTrigger** функция выполняет.

Существует одно исключение для больших двоичных объектов, которые создаются с помощью hello **большого двоичного объекта** атрибута. Когда hello SDK веб-задания создается новый большой двоичный объект, он передает новый большой двоичный объект hello немедленно сопоставления tooany **BlobTrigger** функции. Таким образом Если цепочка blob входы и выходы, hello SDK можно их эффективной обработки. Но если при выполнении функций обработки больших двоичных объектов, созданных или обновленных другими способами, нужны малые задержки, мы советуем использовать **QueueTrigger** вместо **BlobTrigger**.

### <a name="blob-receipts"></a>Уведомления о получении большого двоичного объекта
Hello SDK веб-заданий гарантирует, что не **BlobTrigger** функция вызывается несколько раз для hello же новые или обновлении большого двоичного объекта. Это делается путем сохранения *большого двоичного объекта уведомления* в порядке toodetermine обработанными версии данного большого двоичного объекта.

BLOB-объект уведомления хранятся в контейнер с именем *размещаемые на веб-заданий для azure* в учетной записи хранилища Azure hello, hello AzureWebJobsStorage строку подключения. Получение большого двоичного объекта имеет hello следующую информацию:

* Здравствуйте, функция, которая была вызвана для hello большого двоичного объекта (»*{имя веб-задания}*. Функции. *{Имя функции}*», например: «WebJob1.Functions.CopyBlob»)
* Имя контейнера Hello
* Тип большого двоичного объекта Hello («BlockBlob» или «PageBlob»)
* Имя BLOB-объекта Hello
* Hello ETag (идентификатор версии большого двоичного объекта, например: «0x8D1DC6E70A277EF»)

Если требуется повторная обработка tooforce большого двоичного объекта, можно вручную удалить уведомление hello больших двоичных объектов для данного большого двоичного объекта из hello *размещаемые на веб-заданий для azure* контейнера.

## <a name="related-topics-covered-by-hello-queues-article"></a>Связанные разделы, охватываемых статьи очереди hello
Сведения о обработки больших двоичных объектов toohandle запуска, очереди сообщений и для веб-задания сценариев SDK не содержатся определенные tooblob обработки, [как хранилище с hello SDK веб-заданий очередей toouse Azure](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).

Связанные разделы, описанные в этой статье hello следующие:

* Асинхронные функции
* Выполнение на нескольких экземплярах
* Корректное завершение работы
* Использование пакета SDK веб-задания атрибутов в теле функции hello
* Задать строки подключения пакета SDK для hello в коде.
* Установка значений параметров конструктора пакета SDK для заданий WebJob в коде
* Настройте **MaxDequeueCount** для обработки подозрительных больших двоичных объектов.
* Вызов функции вручную
* Запись журналов

## <a name="next-steps"></a>Дальнейшие действия
В этой статье был дан образцы кода где показано, как большие двоичные объекты toohandle распространенные сценарии для работы с Azure. Дополнительные сведения о статье toouse веб-заданий Azure и hello SDK веб-заданий [ресурсы документации веб-заданий Azure](http://go.microsoft.com/fwlink/?linkid=390226).

