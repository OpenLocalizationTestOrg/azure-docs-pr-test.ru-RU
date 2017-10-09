---
title: "aaaGet работы с Visual Studio и хранилище больших двоичных объектов подключенных служб (для проектов веб-задания) | Документы Microsoft"
description: "Запуск с помощью хранилища больших двоичных объектов в проекте веб-задания после подключения tooan хранилища Azure с помощью Visual Studio tooget подключенные службы."
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 324c9376-0225-4092-9825-5d1bd5550058
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 29f2d5e19426d37d815cdf9a1e00abfb1e07ccf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="a2d12-103">Начало работы с подключенными службами хранилища больших двоичных объектов Azure и Visual Studio (проекты веб-заданий)</span><span class="sxs-lookup"><span data-stu-id="a2d12-103">Get started with Azure Blob storage and Visual Studio connected services (WebJob projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="a2d12-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="a2d12-104">Overview</span></span>
<span data-ttu-id="a2d12-105">В этой статье приведены C# образцы кода, Показать как tootrigger процесса при создании или обновлении большого двоичного объекта Azure.</span><span class="sxs-lookup"><span data-stu-id="a2d12-105">This article provides C# code samples that show how tootrigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="a2d12-106">Примеры кода Hello использовать hello [SDK веб-заданий](../app-service-web/websites-dotnet-webjobs-sdk.md) версии 1.x.</span><span class="sxs-lookup"><span data-stu-id="a2d12-106">hello code samples use hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span> <span data-ttu-id="a2d12-107">При добавлении проекта веб-задания tooa учетной записи хранилища с помощью Visual Studio hello **Добавление подключенных служб** диалогового окна, установлен соответствующий пакет NuGet хранилища Azure hello, соответствующие ссылки .NET hello будут добавлены toohello в файле App.config hello обновляются проекта и строки подключения для учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="a2d12-107">When you add a storage account tooa WebJob project by using hello Visual Studio **Add Connected Services** dialog, hello appropriate Azure Storage NuGet package is installed, hello appropriate .NET references are added toohello project, and connection strings for hello storage account are updated in hello App.config file.</span></span>

## <a name="how-tootrigger-a-function-when-a-blob-is-created-or-updated"></a><span data-ttu-id="a2d12-108">Как tootrigger функции при создании или обновлении большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="a2d12-108">How tootrigger a function when a blob is created or updated</span></span>
<span data-ttu-id="a2d12-109">В этом разделе показано, как toouse hello **BlobTrigger** атрибута.</span><span class="sxs-lookup"><span data-stu-id="a2d12-109">This section shows how toouse hello **BlobTrigger** attribute.</span></span>

 <span data-ttu-id="a2d12-110">**Примечание:** hello toowatch SDK веб-заданий сканирования журнала файлов для новых или измененных больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="a2d12-110">**Note:** hello WebJobs SDK scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="a2d12-111">Этот процесс является по своей природе медленным; функция может не происходит до нескольких минут или больше после создания большого двоичного объекта hello.</span><span class="sxs-lookup"><span data-stu-id="a2d12-111">This process is inherently slow; a function might not get triggered until several minutes or longer after hello blob is created.</span></span>  <span data-ttu-id="a2d12-112">Если приложению требуются большие двоичные объекты tooprocess немедленно, hello рекомендуется метод, который toocreate сообщения в очереди, при создании большого двоичного объекта hello и использовать hello [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) вместо hello атрибута **BlobTrigger** атрибут hello функция, которая обрабатывает hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="a2d12-112">If your application needs tooprocess blobs immediately, hello recommended method is toocreate a queue message when you create hello blob, and use hello [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of hello **BlobTrigger** attribute on hello function that processes hello blob.</span></span>

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="a2d12-113">Один заполнитель для имени большого двоичного объекта и расширения</span><span class="sxs-lookup"><span data-stu-id="a2d12-113">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="a2d12-114">Hello следующий код копирует текст больших двоичных объектов, которые отображаются в hello *ввода* toohello контейнера *вывода* контейнера:</span><span class="sxs-lookup"><span data-stu-id="a2d12-114">hello following code sample copies text blobs that appear in hello *input* container toohello *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="a2d12-115">Конструктор атрибута Hello принимает строковый параметр, указывающий имя контейнера hello и hello имя большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="a2d12-115">hello attribute constructor takes a string parameter that specifies hello container name and a placeholder for hello blob name.</span></span> <span data-ttu-id="a2d12-116">В этом примере, если большой двоичный объект с именем *Blob1.txt* создается в hello *ввода* контейнер, функции hello создает большой двоичный объект с именем *Blob1.txt* в hello *выходных данных*  контейнера.</span><span class="sxs-lookup"><span data-stu-id="a2d12-116">In this example, if a blob named *Blob1.txt* is created in hello *input* container, hello function creates a blob named *Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="a2d12-117">Можно указать шаблон имени с прототипа имя большого двоичного объекта hello, как показано в hello следующий образец кода:</span><span class="sxs-lookup"><span data-stu-id="a2d12-117">You can specify a name pattern with hello blob name placeholder, as shown in hello following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="a2d12-118">Этот код копируется только большие двоичные объекты, имена которых начинаются с original-.</span><span class="sxs-lookup"><span data-stu-id="a2d12-118">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="a2d12-119">Например *Blob1.txt исходный* в hello *ввода* контейнера копируется слишком*копирования Blob1.txt* в hello *выходные данные* контейнера.</span><span class="sxs-lookup"><span data-stu-id="a2d12-119">For example, *original-Blob1.txt* in hello *input* container is copied too*copy-Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="a2d12-120">Если вам требуется шаблон имени toospecify имена больших двоичных объектов, имеющих фигурные скобки в имени hello, двойные фигурные скобки hello.</span><span class="sxs-lookup"><span data-stu-id="a2d12-120">If you need toospecify a name pattern for blob names that have curly braces in hello name, double hello curly braces.</span></span> <span data-ttu-id="a2d12-121">Например, если вы хотите toofind большие двоичные объекты в hello *изображения* контейнер с именами следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a2d12-121">For example, if you want toofind blobs in hello *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="a2d12-122">используйте следующую команду для своего шаблона:</span><span class="sxs-lookup"><span data-stu-id="a2d12-122">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="a2d12-123">В примере hello hello *имя* бы значение заполнителя *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="a2d12-123">In hello example, hello *name* placeholder value would be *soundfile.mp3*.</span></span>

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="a2d12-124">Отдельные заполнители для имени большого двоичного объекта и расширения</span><span class="sxs-lookup"><span data-stu-id="a2d12-124">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="a2d12-125">Hello следующие изменения кода образца hello расширение файла его по мере копирования больших двоичных объектов, которые отображаются в hello *ввода* toohello контейнера *вывода* контейнера.</span><span class="sxs-lookup"><span data-stu-id="a2d12-125">hello following code sample changes hello file extension as it copies blobs that appear in hello *input* container toohello *output* container.</span></span> <span data-ttu-id="a2d12-126">Hello код регистрирует расширение hello hello *ввода* больших двоичных объектов и задает расширение hello hello *вывода* слишком большой двоичный объект*.txt*.</span><span class="sxs-lookup"><span data-stu-id="a2d12-126">hello code logs hello extension of hello *input* blob and sets hello extension of hello *output* blob too*.txt*.</span></span>

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

## <a name="types-that-you-can-bind-tooblobs"></a><span data-ttu-id="a2d12-127">Типы, что вы можете привязать tooblobs</span><span class="sxs-lookup"><span data-stu-id="a2d12-127">Types that you can bind tooblobs</span></span>
<span data-ttu-id="a2d12-128">Можно использовать hello **BlobTrigger** атрибут hello следующие типы:</span><span class="sxs-lookup"><span data-stu-id="a2d12-128">You can use hello **BlobTrigger** attribute on hello following types:</span></span>

* <span data-ttu-id="a2d12-129">**string**</span><span class="sxs-lookup"><span data-stu-id="a2d12-129">**string**</span></span>
* <span data-ttu-id="a2d12-130">**TextReader;**</span><span class="sxs-lookup"><span data-stu-id="a2d12-130">**TextReader**</span></span>
* <span data-ttu-id="a2d12-131">**Поток**</span><span class="sxs-lookup"><span data-stu-id="a2d12-131">**Stream**</span></span>
* <span data-ttu-id="a2d12-132">**ICloudBlob;**</span><span class="sxs-lookup"><span data-stu-id="a2d12-132">**ICloudBlob**</span></span>
* <span data-ttu-id="a2d12-133">**CloudBlockBlob**</span><span class="sxs-lookup"><span data-stu-id="a2d12-133">**CloudBlockBlob**</span></span>
* <span data-ttu-id="a2d12-134">**CloudPageBlob.**</span><span class="sxs-lookup"><span data-stu-id="a2d12-134">**CloudPageBlob**</span></span>
* <span data-ttu-id="a2d12-135">другие типы, десериализованные с помощью [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span><span class="sxs-lookup"><span data-stu-id="a2d12-135">Other types deserialized by [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span></span>

<span data-ttu-id="a2d12-136">Если требуется toowork непосредственно с hello учетной записи хранилища Azure, можно добавить **CloudStorageAccount** сигнатура метода toohello параметра.</span><span class="sxs-lookup"><span data-stu-id="a2d12-136">If you want toowork directly with hello Azure storage account, you can also add a **CloudStorageAccount** parameter toohello method signature.</span></span>

## <a name="getting-text-blob-content-by-binding-toostring"></a><span data-ttu-id="a2d12-137">Получение текстового содержимого больших двоичных объектов с toostring привязки</span><span class="sxs-lookup"><span data-stu-id="a2d12-137">Getting text blob content by binding toostring</span></span>
<span data-ttu-id="a2d12-138">Если ожидаются текст больших двоичных объектов, **BlobTrigger** может быть применен tooa **строка** параметра.</span><span class="sxs-lookup"><span data-stu-id="a2d12-138">If text blobs are expected, **BlobTrigger** can be applied tooa **string** parameter.</span></span> <span data-ttu-id="a2d12-139">Hello следующий код привязывает большого двоичного объекта текст tooa **строка** параметр с именем **logMessage**.</span><span class="sxs-lookup"><span data-stu-id="a2d12-139">hello following code sample binds a text blob tooa **string** parameter named **logMessage**.</span></span> <span data-ttu-id="a2d12-140">функция Hello использует этот параметр toowrite hello содержимое toohello hello большого двоичного объекта панели мониторинга пакета SDK веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="a2d12-140">hello function uses that parameter toowrite hello contents of hello blob toohello WebJobs SDK dashboard.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a><span data-ttu-id="a2d12-141">Получение содержимого сериализованного большого двоичного объекта с помощью ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="a2d12-141">Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="a2d12-142">Hello следующий код использует класс, реализующий **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** атрибута toobind toohello большого двоичного объекта **WebImage** типа.</span><span class="sxs-lookup"><span data-stu-id="a2d12-142">hello following code sample uses a class that implements **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** attribute toobind a blob toohello **WebImage** type.</span></span>

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

<span data-ttu-id="a2d12-143">Hello **WebImage** предоставлены привязки кода в **WebImageBinder** класс, производный от **ICloudBlobStreamBinder**.</span><span class="sxs-lookup"><span data-stu-id="a2d12-143">hello **WebImage** binding code is provided in a **WebImageBinder** class that derives from **ICloudBlobStreamBinder**.</span></span>

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

## <a name="how-toohandle-poison-blobs"></a><span data-ttu-id="a2d12-144">Способ обработки подозрительных сообщений toohandle больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="a2d12-144">How toohandle poison blobs</span></span>
<span data-ttu-id="a2d12-145">Когда **BlobTrigger** функция завершается с ошибкой, hello SDK вызывает ее еще раз, в случае сбоя hello было вызвано временной ошибкой.</span><span class="sxs-lookup"><span data-stu-id="a2d12-145">When a **BlobTrigger** function fails, hello SDK calls it again, in case hello failure was caused by a transient error.</span></span> <span data-ttu-id="a2d12-146">Если причиной сбоя hello является hello содержимое большого двоичного объекта hello, функции hello завершается ошибкой, каждый раз, он пытается tooprocess hello больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="a2d12-146">If hello failure is caused by hello content of hello blob, hello function fails every time it tries tooprocess hello blob.</span></span> <span data-ttu-id="a2d12-147">По умолчанию hello SDK вызывает функцию too5 времени для данного большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="a2d12-147">By default, hello SDK calls a function up too5 times for a given blob.</span></span> <span data-ttu-id="a2d12-148">В случае попробуйте пятый hello hello SDK добавляет tooa очереди сообщений с именем *веб-заданий blobtrigger обработки подозрительных сообщений*.</span><span class="sxs-lookup"><span data-stu-id="a2d12-148">If hello fifth try fails, hello SDK adds a message tooa queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="a2d12-149">Максимальное число повторных попыток для Hello настраивается.</span><span class="sxs-lookup"><span data-stu-id="a2d12-149">hello maximum number of retries is configurable.</span></span> <span data-ttu-id="a2d12-150">Здравствуйте же [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) параметр используется для обработки подозрительных большого двоичного объекта и обработки сообщений в очереди подозрительных сообщений.</span><span class="sxs-lookup"><span data-stu-id="a2d12-150">hello same [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span>

<span data-ttu-id="a2d12-151">приветственное сообщение очереди подозрительных больших двоичных объектов является объект JSON, содержащий hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="a2d12-151">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="a2d12-152">Идентификатор FunctionId (в формате hello *{имя веб-задания}*. Функции. *{Имя функции}*, например: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="a2d12-152">FunctionId (in hello format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="a2d12-153">BlobType (BlockBlob или PageBlob);</span><span class="sxs-lookup"><span data-stu-id="a2d12-153">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="a2d12-154">ContainerName;</span><span class="sxs-lookup"><span data-stu-id="a2d12-154">ContainerName</span></span>
* <span data-ttu-id="a2d12-155">BlobName</span><span class="sxs-lookup"><span data-stu-id="a2d12-155">BlobName</span></span>
* <span data-ttu-id="a2d12-156">ETag (идентификатор версии BLOB-объектов, например 0x8D1DC6E70A277EF)</span><span class="sxs-lookup"><span data-stu-id="a2d12-156">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="a2d12-157">В следующих hello образец кода, hello **CopyBlob** функция имеет код, который вызывает toofail при каждом вызове.</span><span class="sxs-lookup"><span data-stu-id="a2d12-157">In hello following code sample, hello **CopyBlob** function has code that causes it toofail every time it's called.</span></span> <span data-ttu-id="a2d12-158">После его вызывает hello пакета SDK для hello максимальное число повторных попыток, создается сообщение в очереди подозрительных blob hello и этого сообщение обрабатывается hello **LogPoisonBlob** функции.</span><span class="sxs-lookup"><span data-stu-id="a2d12-158">After hello SDK calls it for hello maximum number of retries, a message is created on hello poison blob queue, and that message is processed by hello **LogPoisonBlob** function.</span></span>

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

<span data-ttu-id="a2d12-159">Hello SDK автоматически десериализует сообщение hello JSON.</span><span class="sxs-lookup"><span data-stu-id="a2d12-159">hello SDK automatically deserializes hello JSON message.</span></span> <span data-ttu-id="a2d12-160">Вот hello **PoisonBlobMessage** класса:</span><span class="sxs-lookup"><span data-stu-id="a2d12-160">Here is hello **PoisonBlobMessage** class:</span></span>

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a><span data-ttu-id="a2d12-161">Алгоритм опроса больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="a2d12-161">Blob polling algorithm</span></span>
<span data-ttu-id="a2d12-162">Hello SDK веб-заданий просматривает все контейнеры, указанные по **BlobTrigger** атрибуты при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="a2d12-162">hello WebJobs SDK scans all containers specified by **BlobTrigger** attributes at application start.</span></span> <span data-ttu-id="a2d12-163">Такая проверка может занять некоторое время в большой учетной записи хранения. Поэтому для поиска новых больших двоичных объектов и выполнения функций **BlobTrigger** может потребоваться заметное количество времени.</span><span class="sxs-lookup"><span data-stu-id="a2d12-163">In a large storage account this scan can take some time, so it might be a while before new blobs are found and **BlobTrigger** functions are executed.</span></span>

<span data-ttu-id="a2d12-164">toodetect новые или измененные BLOB-объектов после запуска приложения hello, которые пакет SDK периодически считывает из хранилища больших двоичных объектов hello заносит в журнал.</span><span class="sxs-lookup"><span data-stu-id="a2d12-164">toodetect new or changed blobs after application start, hello SDK periodically reads from hello blob storage logs.</span></span> <span data-ttu-id="a2d12-165">Hello большого двоичного объекта помещаются в буфер и журналы только физически записываются каждые 10 минут или таким образом, поэтому могут существовать значительные задержки после большой двоичный объект создается или обновляется перед соответствующими hello **BlobTrigger** функция выполняет.</span><span class="sxs-lookup"><span data-stu-id="a2d12-165">hello blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before hello corresponding **BlobTrigger** function executes.</span></span>

<span data-ttu-id="a2d12-166">Существует одно исключение для больших двоичных объектов, которые создаются с помощью hello **большого двоичного объекта** атрибута.</span><span class="sxs-lookup"><span data-stu-id="a2d12-166">There is an exception for blobs that you create by using hello **Blob** attribute.</span></span> <span data-ttu-id="a2d12-167">Когда hello SDK веб-задания создается новый большой двоичный объект, он передает новый большой двоичный объект hello немедленно сопоставления tooany **BlobTrigger** функции.</span><span class="sxs-lookup"><span data-stu-id="a2d12-167">When hello WebJobs SDK creates a new blob, it passes hello new blob immediately tooany matching **BlobTrigger** functions.</span></span> <span data-ttu-id="a2d12-168">Таким образом Если цепочка blob входы и выходы, hello SDK можно их эффективной обработки.</span><span class="sxs-lookup"><span data-stu-id="a2d12-168">Therefore if you have a chain of blob inputs and outputs, hello SDK can process them efficiently.</span></span> <span data-ttu-id="a2d12-169">Но если при выполнении функций обработки больших двоичных объектов, созданных или обновленных другими способами, нужны малые задержки, мы советуем использовать **QueueTrigger** вместо **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="a2d12-169">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using **QueueTrigger** rather than **BlobTrigger**.</span></span>

### <a name="blob-receipts"></a><span data-ttu-id="a2d12-170">Уведомления о получении большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="a2d12-170">Blob receipts</span></span>
<span data-ttu-id="a2d12-171">Hello SDK веб-заданий гарантирует, что не **BlobTrigger** функция вызывается несколько раз для hello же новые или обновлении большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="a2d12-171">hello WebJobs SDK makes sure that no **BlobTrigger** function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="a2d12-172">Это делается путем сохранения *большого двоичного объекта уведомления* в порядке toodetermine обработанными версии данного большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="a2d12-172">It does this by maintaining *blob receipts* in order toodetermine if a given blob version has been processed.</span></span>

<span data-ttu-id="a2d12-173">BLOB-объект уведомления хранятся в контейнер с именем *размещаемые на веб-заданий для azure* в учетной записи хранилища Azure hello, hello AzureWebJobsStorage строку подключения.</span><span class="sxs-lookup"><span data-stu-id="a2d12-173">Blob receipts are stored in a container named *azure-webjobs-hosts* in hello Azure storage account specified by hello AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="a2d12-174">Получение большого двоичного объекта имеет hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="a2d12-174">A blob receipt has hello following  information:</span></span>

* <span data-ttu-id="a2d12-175">Здравствуйте, функция, которая была вызвана для hello большого двоичного объекта (»*{имя веб-задания}*. Функции. *{Имя функции}*», например: «WebJob1.Functions.CopyBlob»)</span><span class="sxs-lookup"><span data-stu-id="a2d12-175">hello function that was called for hello blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="a2d12-176">Имя контейнера Hello</span><span class="sxs-lookup"><span data-stu-id="a2d12-176">hello container name</span></span>
* <span data-ttu-id="a2d12-177">Тип большого двоичного объекта Hello («BlockBlob» или «PageBlob»)</span><span class="sxs-lookup"><span data-stu-id="a2d12-177">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="a2d12-178">Имя BLOB-объекта Hello</span><span class="sxs-lookup"><span data-stu-id="a2d12-178">hello blob name</span></span>
* <span data-ttu-id="a2d12-179">Hello ETag (идентификатор версии большого двоичного объекта, например: «0x8D1DC6E70A277EF»)</span><span class="sxs-lookup"><span data-stu-id="a2d12-179">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="a2d12-180">Если требуется повторная обработка tooforce большого двоичного объекта, можно вручную удалить уведомление hello больших двоичных объектов для данного большого двоичного объекта из hello *размещаемые на веб-заданий для azure* контейнера.</span><span class="sxs-lookup"><span data-stu-id="a2d12-180">If you want tooforce reprocessing of a blob, you can manually delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container.</span></span>

## <a name="related-topics-covered-by-hello-queues-article"></a><span data-ttu-id="a2d12-181">Связанные разделы, охватываемых статьи очереди hello</span><span class="sxs-lookup"><span data-stu-id="a2d12-181">Related topics covered by hello queues article</span></span>
<span data-ttu-id="a2d12-182">Сведения о обработки больших двоичных объектов toohandle запуска, очереди сообщений и для веб-задания сценариев SDK не содержатся определенные tooblob обработки, [как хранилище с hello SDK веб-заданий очередей toouse Azure](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="a2d12-182">For information about how toohandle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific tooblob processing, see [How toouse Azure queue storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span>

<span data-ttu-id="a2d12-183">Связанные разделы, описанные в этой статье hello следующие:</span><span class="sxs-lookup"><span data-stu-id="a2d12-183">Related topics covered in that article include hello following:</span></span>

* <span data-ttu-id="a2d12-184">Асинхронные функции</span><span class="sxs-lookup"><span data-stu-id="a2d12-184">Async functions</span></span>
* <span data-ttu-id="a2d12-185">Выполнение на нескольких экземплярах</span><span class="sxs-lookup"><span data-stu-id="a2d12-185">Multiple instances</span></span>
* <span data-ttu-id="a2d12-186">Корректное завершение работы</span><span class="sxs-lookup"><span data-stu-id="a2d12-186">Graceful shutdown</span></span>
* <span data-ttu-id="a2d12-187">Использование пакета SDK веб-задания атрибутов в теле функции hello</span><span class="sxs-lookup"><span data-stu-id="a2d12-187">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="a2d12-188">Задать строки подключения пакета SDK для hello в коде.</span><span class="sxs-lookup"><span data-stu-id="a2d12-188">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="a2d12-189">Установка значений параметров конструктора пакета SDK для заданий WebJob в коде</span><span class="sxs-lookup"><span data-stu-id="a2d12-189">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="a2d12-190">Настройте **MaxDequeueCount** для обработки подозрительных больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="a2d12-190">Configure **MaxDequeueCount** for poison blob handling.</span></span>
* <span data-ttu-id="a2d12-191">Вызов функции вручную</span><span class="sxs-lookup"><span data-stu-id="a2d12-191">Trigger a function manually</span></span>
* <span data-ttu-id="a2d12-192">Запись журналов</span><span class="sxs-lookup"><span data-stu-id="a2d12-192">Write logs</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2d12-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a2d12-193">Next steps</span></span>
<span data-ttu-id="a2d12-194">В этой статье был дан образцы кода где показано, как большие двоичные объекты toohandle распространенные сценарии для работы с Azure.</span><span class="sxs-lookup"><span data-stu-id="a2d12-194">This article has provided code samples that show how toohandle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="a2d12-195">Дополнительные сведения о статье toouse веб-заданий Azure и hello SDK веб-заданий [ресурсы документации веб-заданий Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="a2d12-195">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

