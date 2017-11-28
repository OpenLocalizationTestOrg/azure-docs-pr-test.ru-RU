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
# <a name="how-toouse-azure-blob-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="7b7b1-104">Как toouse Azure хранилище больших двоичных объектов с hello SDK веб-заданий</span><span class="sxs-lookup"><span data-stu-id="7b7b1-104">How toouse Azure blob storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="7b7b1-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="7b7b1-105">Overview</span></span>
<span data-ttu-id="7b7b1-106">В этом руководстве содержатся C# образцы кода, Показать как tootrigger процесса при создании или обновлении большого двоичного объекта Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-106">This guide provides C# code samples that show how tootrigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="7b7b1-107">Используйте образцы кода Hello [SDK веб-заданий](websites-dotnet-webjobs-sdk.md) версии 1.x.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-107">hello code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="7b7b1-108">Примеры кода, которые показывают, как toocreate больших двоичных объектов см. в разделе [как хранилище с hello SDK веб-заданий очередей toouse Azure](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="7b7b1-108">For code samples that show how toocreate blobs, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="7b7b1-109">Hello руководстве предполагается, вы знаете [как toocreate проект веб-задания в Visual Studio с подключением строки этой учетной записи хранения точки tooyour](websites-dotnet-webjobs-sdk-get-started.md) или слишком[нескольких учетных записей хранения](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="7b7b1-109">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

## <span data-ttu-id="7b7b1-110"><a id="trigger"></a>Как tootrigger функции при создании или обновлении большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="7b7b1-110"><a id="trigger"></a> How tootrigger a function when a blob is created or updated</span></span>
<span data-ttu-id="7b7b1-111">В этом разделе показано, как toouse hello `BlobTrigger` атрибута.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-111">This section shows how toouse hello `BlobTrigger` attribute.</span></span> 

> [!NOTE]
> <span data-ttu-id="7b7b1-112">Здравствуйте, toowatch SDK веб-заданий сканирования журнала файлов для новых или измененных больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-112">hello WebJobs SDK scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="7b7b1-113">Этот процесс не находится в режиме реального времени; функция может не происходит до нескольких минут или больше после создания большого двоичного объекта hello.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-113">This process is not real-time; a function might not get triggered until several minutes or longer after hello blob is created.</span></span> <span data-ttu-id="7b7b1-114">Кроме того, [журналы службы хранилища создаются по принципу лучшего из возможного](https://msdn.microsoft.com/library/azure/hh343262.aspx), то есть не гарантируется регистрация всех событий.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-114">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; there is no guarantee that all events will be captured.</span></span> <span data-ttu-id="7b7b1-115">В некоторых случаях журналы могут пропускаться.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-115">Under some conditions, logs might be missed.</span></span> <span data-ttu-id="7b7b1-116">Hello скорость и надежность ограничения триггеров больших двоичных объектов, не подходящий для вашего приложения, hello рекомендуется метод, который toocreate сообщения в очереди, при создании большого двоичного объекта hello и использовать hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) вместо атрибута Hello `BlobTrigger` атрибут hello функция, которая обрабатывает hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-116">If hello speed and reliability limitations of blob triggers are not acceptable for your application, hello recommended method is toocreate a queue message when you create hello blob, and use hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of hello `BlobTrigger` attribute on hello function that processes hello blob.</span></span>
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="7b7b1-117">Один заполнитель для имени большого двоичного объекта и расширения</span><span class="sxs-lookup"><span data-stu-id="7b7b1-117">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="7b7b1-118">Hello следующий код копирует текст больших двоичных объектов, которые отображаются в hello *ввода* toohello контейнера *вывода* контейнера:</span><span class="sxs-lookup"><span data-stu-id="7b7b1-118">hello following code sample copies text blobs that appear in hello *input* container toohello *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="7b7b1-119">Конструктор атрибута Hello принимает строковый параметр, указывающий имя контейнера hello и hello имя большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-119">hello attribute constructor takes a string parameter that specifies hello container name and a placeholder for hello blob name.</span></span> <span data-ttu-id="7b7b1-120">В этом примере, если большой двоичный объект с именем *Blob1.txt* создается в hello *ввода* контейнер, функции hello создает большой двоичный объект с именем *Blob1.txt* в hello *выходных данных*  контейнера.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-120">In this example, if a blob named *Blob1.txt* is created in hello *input* container, hello function creates a blob named *Blob1.txt* in hello *output* container.</span></span> 

<span data-ttu-id="7b7b1-121">Можно указать шаблон имени с прототипа имя большого двоичного объекта hello, как показано в hello следующий образец кода:</span><span class="sxs-lookup"><span data-stu-id="7b7b1-121">You can specify a name pattern with hello blob name placeholder, as shown in hello following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="7b7b1-122">Этот код копируется только большие двоичные объекты, имена которых начинаются с original-.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-122">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="7b7b1-123">Например *Blob1.txt исходный* в hello *ввода* контейнера копируется слишком*копирования Blob1.txt* в hello *выходные данные* контейнера.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-123">For example, *original-Blob1.txt* in hello *input* container is copied too*copy-Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="7b7b1-124">Если вам требуется шаблон имени toospecify имена больших двоичных объектов, имеющих фигурные скобки в имени hello, двойные фигурные скобки hello.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-124">If you need toospecify a name pattern for blob names that have curly braces in hello name, double hello curly braces.</span></span> <span data-ttu-id="7b7b1-125">Например, если вы хотите toofind большие двоичные объекты в hello *изображения* контейнер с именами следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7b7b1-125">For example, if you want toofind blobs in hello *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="7b7b1-126">используйте следующую команду для своего шаблона:</span><span class="sxs-lookup"><span data-stu-id="7b7b1-126">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="7b7b1-127">В примере hello hello *имя* бы значение заполнителя *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-127">In hello example, hello *name* placeholder value would be *soundfile.mp3*.</span></span> 

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="7b7b1-128">Отдельные заполнители для имени большого двоичного объекта и расширения</span><span class="sxs-lookup"><span data-stu-id="7b7b1-128">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="7b7b1-129">Hello следующие изменения кода образца hello расширение файла его по мере копирования больших двоичных объектов, которые отображаются в hello *ввода* toohello контейнера *вывода* контейнера.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-129">hello following code sample changes hello file extension as it copies blobs that appear in hello *input* container toohello *output* container.</span></span> <span data-ttu-id="7b7b1-130">Hello код регистрирует расширение hello hello *ввода* больших двоичных объектов и задает расширение hello hello *вывода* слишком большой двоичный объект*.txt*.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-130">hello code logs hello extension of hello *input* blob and sets hello extension of hello *output* blob too*.txt*.</span></span>

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

## <span data-ttu-id="7b7b1-131"><a id="types"></a>Типы, что вы можете привязать tooblobs</span><span class="sxs-lookup"><span data-stu-id="7b7b1-131"><a id="types"></a> Types that you can bind tooblobs</span></span>
<span data-ttu-id="7b7b1-132">Можно использовать hello `BlobTrigger` атрибут hello следующие типы:</span><span class="sxs-lookup"><span data-stu-id="7b7b1-132">You can use hello `BlobTrigger` attribute on hello following types:</span></span>

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
* <span data-ttu-id="7b7b1-133">другие типы, десериализованные с помощью [ICloudBlobStreamBinder](#icbsb)</span><span class="sxs-lookup"><span data-stu-id="7b7b1-133">Other types deserialized by [ICloudBlobStreamBinder](#icbsb)</span></span> 

<span data-ttu-id="7b7b1-134">Если требуется toowork непосредственно с hello учетной записи хранилища Azure, можно добавить `CloudStorageAccount` сигнатура метода toohello параметра.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-134">If you want toowork directly with hello Azure storage account, you can also add a `CloudStorageAccount` parameter toohello method signature.</span></span>

<span data-ttu-id="7b7b1-135">Примеры см. в разделе hello [больших двоичных объектов код привязки в репозитории hello пакет sdk веб-заданий azure на GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="7b7b1-135">For examples, see hello [blob binding code in hello azure-webjobs-sdk repository on GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span></span>

## <span data-ttu-id="7b7b1-136"><a id="string"></a>Получение текстового содержимого больших двоичных объектов с toostring привязки</span><span class="sxs-lookup"><span data-stu-id="7b7b1-136"><a id="string"></a> Getting text blob content by binding toostring</span></span>
<span data-ttu-id="7b7b1-137">Если ожидаются текст больших двоичных объектов, `BlobTrigger` может быть применен tooa `string` параметра.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-137">If text blobs are expected, `BlobTrigger` can be applied tooa `string` parameter.</span></span> <span data-ttu-id="7b7b1-138">Hello следующий код привязывает большого двоичного объекта текст tooa `string` параметр с именем `logMessage`.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-138">hello following code sample binds a text blob tooa `string` parameter named `logMessage`.</span></span> <span data-ttu-id="7b7b1-139">функция Hello использует этот параметр toowrite hello содержимое toohello hello большого двоичного объекта панели мониторинга пакета SDK веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-139">hello function uses that parameter toowrite hello contents of hello blob toohello WebJobs SDK dashboard.</span></span> 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <span data-ttu-id="7b7b1-140"><a id="icbsb"></a> Получение содержимого сериализованного большого двоичного объекта с помощью ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="7b7b1-140"><a id="icbsb"></a> Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="7b7b1-141">Hello следующий код использует класс, реализующий `ICloudBlobStreamBinder` tooenable hello `BlobTrigger` атрибута toobind toohello большой двоичный объект `WebImage` типа.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-141">hello following code sample uses a class that implements `ICloudBlobStreamBinder` tooenable hello `BlobTrigger` attribute toobind a blob toohello `WebImage` type.</span></span>

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

<span data-ttu-id="7b7b1-142">Hello `WebImage` предоставлены привязки кода в `WebImageBinder` класс, производный от `ICloudBlobStreamBinder`.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-142">hello `WebImage` binding code is provided in a `WebImageBinder` class that derives from `ICloudBlobStreamBinder`.</span></span>

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

## <a name="getting-hello-blob-path-for-hello-triggering-blob"></a><span data-ttu-id="7b7b1-143">Получение пути к BLOB-объектов hello для hello, активируя больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="7b7b1-143">Getting hello blob path for hello triggering blob</span></span>
<span data-ttu-id="7b7b1-144">Имя контейнера tooget hello и больших двоичных объектов для hello BLOB-объект, который инициировал функции hello включают `blobTrigger` строковый параметр в сигнатуре функции hello.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-144">tooget hello container name and blob name of hello blob that has triggered hello function, include a `blobTrigger` string parameter in hello function signature.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <span data-ttu-id="7b7b1-145"><a id="poison"></a>Способ обработки подозрительных сообщений toohandle больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="7b7b1-145"><a id="poison"></a> How toohandle poison blobs</span></span>
<span data-ttu-id="7b7b1-146">Если `BlobTrigger` функция завершается с ошибкой, hello SDK вызывает ее еще раз, в случае сбоя hello было вызвано временной ошибкой.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-146">When a `BlobTrigger` function fails, hello SDK calls it again, in case hello failure was caused by a transient error.</span></span> <span data-ttu-id="7b7b1-147">Если причиной сбоя hello является hello содержимое большого двоичного объекта hello, функции hello завершается ошибкой, каждый раз, он пытается tooprocess hello больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-147">If hello failure is caused by hello content of hello blob, hello function fails every time it tries tooprocess hello blob.</span></span> <span data-ttu-id="7b7b1-148">По умолчанию hello SDK вызывает функцию too5 времени для данного большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-148">By default, hello SDK calls a function up too5 times for a given blob.</span></span> <span data-ttu-id="7b7b1-149">В случае попробуйте пятый hello hello SDK добавляет tooa очереди сообщений с именем *веб-заданий blobtrigger обработки подозрительных сообщений*.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-149">If hello fifth try fails, hello SDK adds a message tooa queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="7b7b1-150">Максимальное число повторных попыток для Hello настраивается.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-150">hello maximum number of retries is configurable.</span></span> <span data-ttu-id="7b7b1-151">Здравствуйте же [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) параметр используется для обработки подозрительных большого двоичного объекта и обработки сообщений в очереди подозрительных сообщений.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-151">hello same [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span> 

<span data-ttu-id="7b7b1-152">приветственное сообщение очереди подозрительных больших двоичных объектов является объект JSON, содержащий hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="7b7b1-152">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="7b7b1-153">Идентификатор FunctionId (в формате hello *{имя веб-задания}*. Функции. *{Имя функции}*, например: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="7b7b1-153">FunctionId (in hello format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="7b7b1-154">BlobType (BlockBlob или PageBlob);</span><span class="sxs-lookup"><span data-stu-id="7b7b1-154">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="7b7b1-155">ContainerName;</span><span class="sxs-lookup"><span data-stu-id="7b7b1-155">ContainerName</span></span>
* <span data-ttu-id="7b7b1-156">BlobName</span><span class="sxs-lookup"><span data-stu-id="7b7b1-156">BlobName</span></span>
* <span data-ttu-id="7b7b1-157">ETag (идентификатор версии BLOB-объектов, например 0x8D1DC6E70A277EF)</span><span class="sxs-lookup"><span data-stu-id="7b7b1-157">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="7b7b1-158">В следующих hello образец кода, hello `CopyBlob` функция имеет код, который вызывает toofail при каждом вызове.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-158">In hello following code sample, hello `CopyBlob` function has code that causes it toofail every time it's called.</span></span> <span data-ttu-id="7b7b1-159">После его вызывает hello пакета SDK для hello максимальное число повторных попыток, создается сообщение в очереди подозрительных blob hello и этого сообщение обрабатывается hello `LogPoisonBlob` функции.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-159">After hello SDK calls it for hello maximum number of retries, a message is created on hello poison blob queue, and that message is processed by hello `LogPoisonBlob` function.</span></span> 

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

<span data-ttu-id="7b7b1-160">Hello SDK автоматически десериализует сообщение hello JSON.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-160">hello SDK automatically deserializes hello JSON message.</span></span> <span data-ttu-id="7b7b1-161">Вот hello `PoisonBlobMessage` класса:</span><span class="sxs-lookup"><span data-stu-id="7b7b1-161">Here is hello `PoisonBlobMessage` class:</span></span> 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <span data-ttu-id="7b7b1-162"><a id="polling"></a> Алгоритм опроса больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="7b7b1-162"><a id="polling"></a> Blob polling algorithm</span></span>
<span data-ttu-id="7b7b1-163">Hello SDK веб-заданий просматривает все контейнеры, указанные по `BlobTrigger` атрибуты при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-163">hello WebJobs SDK scans all containers specified by `BlobTrigger` attributes at application start.</span></span> <span data-ttu-id="7b7b1-164">Такая проверка может занять некоторое время в большой учетной записи хранения. Поэтому для поиска новых больших двоичных объектов и выполнения функций `BlobTrigger` может потребоваться много времени.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-164">In a large storage account this scan can take some time, so it might be a while before new blobs are found and `BlobTrigger` functions are executed.</span></span>

<span data-ttu-id="7b7b1-165">toodetect новые или измененные BLOB-объектов после запуска приложения hello, которые пакет SDK периодически считывает из хранилища больших двоичных объектов hello заносит в журнал.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-165">toodetect new or changed blobs after application start, hello SDK periodically reads from hello blob storage logs.</span></span> <span data-ttu-id="7b7b1-166">Hello большого двоичного объекта помещаются в буфер и журналы только физически записываются каждые 10 минут или таким образом, поэтому могут существовать значительные задержки после большой двоичный объект создается или обновляется перед соответствующими hello `BlobTrigger` функция выполняет.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-166">hello blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before hello corresponding `BlobTrigger` function executes.</span></span> 

<span data-ttu-id="7b7b1-167">Существует одно исключение для больших двоичных объектов, которые создаются с помощью hello `Blob` атрибута.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-167">There is an exception for blobs that you create by using hello `Blob` attribute.</span></span> <span data-ttu-id="7b7b1-168">Когда hello SDK веб-задания создается новый большой двоичный объект, он передает новый большой двоичный объект hello немедленно сопоставления tooany `BlobTrigger` функции.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-168">When hello WebJobs SDK creates a new blob, it passes hello new blob immediately tooany matching `BlobTrigger` functions.</span></span> <span data-ttu-id="7b7b1-169">Таким образом Если цепочка blob входы и выходы, hello SDK можно их эффективной обработки.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-169">Therefore if you have a chain of blob inputs and outputs, hello SDK can process them efficiently.</span></span> <span data-ttu-id="7b7b1-170">Но если при выполнении функций обработки больших двоичных объектов, созданных или обновленных другими способами, нужны малые задержки, советуем использовать `QueueTrigger` вместо `BlobTrigger`.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-170">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using `QueueTrigger` rather than `BlobTrigger`.</span></span>

### <span data-ttu-id="7b7b1-171"><a id="receipts"></a> Уведомления о получении большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="7b7b1-171"><a id="receipts"></a> Blob receipts</span></span>
<span data-ttu-id="7b7b1-172">Hello SDK веб-заданий гарантирует, что не `BlobTrigger` функция вызывается несколько раз для hello же новые или обновлении большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-172">hello WebJobs SDK makes sure that no `BlobTrigger` function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="7b7b1-173">Это делается путем сохранения *большого двоичного объекта уведомления* в порядке toodetermine обработанными версии данного большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-173">It does this by maintaining *blob receipts* in order toodetermine if a given blob version has been processed.</span></span>

<span data-ttu-id="7b7b1-174">BLOB-объект уведомления хранятся в контейнер с именем *размещаемые на веб-заданий для azure* в учетной записи хранилища Azure hello, hello AzureWebJobsStorage строку подключения.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-174">Blob receipts are stored in a container named *azure-webjobs-hosts* in hello Azure storage account specified by hello AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="7b7b1-175">Получение большого двоичного объекта имеет hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="7b7b1-175">A blob receipt has hello following  information:</span></span>

* <span data-ttu-id="7b7b1-176">Здравствуйте, функция, которая была вызвана для hello большого двоичного объекта (»*{имя веб-задания}*. Функции. *{Имя функции}*», например: «WebJob1.Functions.CopyBlob»)</span><span class="sxs-lookup"><span data-stu-id="7b7b1-176">hello function that was called for hello blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="7b7b1-177">Имя контейнера Hello</span><span class="sxs-lookup"><span data-stu-id="7b7b1-177">hello container name</span></span>
* <span data-ttu-id="7b7b1-178">Тип большого двоичного объекта Hello («BlockBlob» или «PageBlob»)</span><span class="sxs-lookup"><span data-stu-id="7b7b1-178">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="7b7b1-179">Имя BLOB-объекта Hello</span><span class="sxs-lookup"><span data-stu-id="7b7b1-179">hello blob name</span></span>
* <span data-ttu-id="7b7b1-180">Hello ETag (идентификатор версии большого двоичного объекта, например: «0x8D1DC6E70A277EF»)</span><span class="sxs-lookup"><span data-stu-id="7b7b1-180">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="7b7b1-181">Если требуется повторная обработка tooforce большого двоичного объекта, можно вручную удалить уведомление hello больших двоичных объектов для данного большого двоичного объекта из hello *размещаемые на веб-заданий для azure* контейнера.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-181">If you want tooforce reprocessing of a blob, you can manually delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container.</span></span>

## <span data-ttu-id="7b7b1-182"><a id="queues"></a>Связанные разделы, охватываемых статьи очереди hello</span><span class="sxs-lookup"><span data-stu-id="7b7b1-182"><a id="queues"></a>Related topics covered by hello queues article</span></span>
<span data-ttu-id="7b7b1-183">Сведения о обработки больших двоичных объектов toohandle запуска, очереди сообщений и для веб-задания сценариев SDK не содержатся определенные tooblob обработки, [как хранилище с hello SDK веб-заданий очередей toouse Azure](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="7b7b1-183">For information about how toohandle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific tooblob processing, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="7b7b1-184">Связанные разделы, описанные в этой статье hello следующие:</span><span class="sxs-lookup"><span data-stu-id="7b7b1-184">Related topics covered in that article include hello following:</span></span>

* <span data-ttu-id="7b7b1-185">Асинхронные функции</span><span class="sxs-lookup"><span data-stu-id="7b7b1-185">Async functions</span></span>
* <span data-ttu-id="7b7b1-186">Выполнение на нескольких экземплярах</span><span class="sxs-lookup"><span data-stu-id="7b7b1-186">Multiple instances</span></span>
* <span data-ttu-id="7b7b1-187">Корректное завершение работы</span><span class="sxs-lookup"><span data-stu-id="7b7b1-187">Graceful shutdown</span></span>
* <span data-ttu-id="7b7b1-188">Использование пакета SDK веб-задания атрибутов в теле функции hello</span><span class="sxs-lookup"><span data-stu-id="7b7b1-188">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="7b7b1-189">Задать строки подключения пакета SDK для hello в коде.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-189">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="7b7b1-190">Установка значений параметров конструктора пакета SDK для заданий WebJob в коде</span><span class="sxs-lookup"><span data-stu-id="7b7b1-190">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="7b7b1-191">Настройка `MaxDequeueCount` для обработки подозрительных больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="7b7b1-191">Configure `MaxDequeueCount` for poison blob handling.</span></span>
* <span data-ttu-id="7b7b1-192">Вызов функции вручную</span><span class="sxs-lookup"><span data-stu-id="7b7b1-192">Trigger a function manually</span></span>
* <span data-ttu-id="7b7b1-193">Запись журналов</span><span class="sxs-lookup"><span data-stu-id="7b7b1-193">Write logs</span></span>

## <span data-ttu-id="7b7b1-194"><a id="nextsteps"></a> Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7b7b1-194"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="7b7b1-195">Это руководство предоставляет образцы кода где показано, как большие двоичные объекты toohandle распространенные сценарии для работы с Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7b1-195">This guide has provided code samples that show how toohandle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="7b7b1-196">Дополнительные сведения о статье toouse веб-заданий Azure и hello SDK веб-заданий [рекомендуется заданиям Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="7b7b1-196">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

