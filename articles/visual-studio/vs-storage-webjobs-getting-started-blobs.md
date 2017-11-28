---
title: "Приступая к работе с хранилищем BLOB-объектов Azure и подключенными службами Visual Studio (проекты веб-заданий) | Документация Майкрософт"
description: "Как приступить к работе, используя хранилище больших двоичных объектов в проекте веб-задания после подключения к хранилищу Azure с использованием подключенных служб Visual Studio."
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
ms.openlocfilehash: a50a265feff8c0aec28825eb0bc4e33585ea5a02
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="91808-103">Начало работы с подключенными службами хранилища больших двоичных объектов Azure и Visual Studio (проекты веб-заданий)</span><span class="sxs-lookup"><span data-stu-id="91808-103">Get started with Azure Blob storage and Visual Studio connected services (WebJob projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="91808-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="91808-104">Overview</span></span>
<span data-ttu-id="91808-105">В этой статье приведены примеры кода на C# для запуска процессов при создании или обновлении большого двоичного объекта Azure.</span><span class="sxs-lookup"><span data-stu-id="91808-105">This article provides C# code samples that show how to trigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="91808-106">В примерах кода используется [пакет SDK для веб-заданий](../app-service-web/websites-dotnet-webjobs-sdk.md) версии 1.x.</span><span class="sxs-lookup"><span data-stu-id="91808-106">The code samples use the [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span> <span data-ttu-id="91808-107">Когда вы добавляете учетную запись хранения в проект веб-задания с помощью диалогового окна **Добавление подключенных служб** в Visual Studio, устанавливается соответствующий пакет NuGet службы хранилища Azure. Также в проект добавляются соответствующие ссылки .NET, а в файле App.config обновляются строки подключения для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="91808-107">When you add a storage account to a WebJob project by using the Visual Studio **Add Connected Services** dialog, the appropriate Azure Storage NuGet package is installed, the appropriate .NET references are added to the project, and connection strings for the storage account are updated in the App.config file.</span></span>

## <a name="how-to-trigger-a-function-when-a-blob-is-created-or-updated"></a><span data-ttu-id="91808-108">Вызов функции при создании или обновлении большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="91808-108">How to trigger a function when a blob is created or updated</span></span>
<span data-ttu-id="91808-109">В этом разделе показано, как использовать атрибут **BlobTrigger** .</span><span class="sxs-lookup"><span data-stu-id="91808-109">This section shows how to use the **BlobTrigger** attribute.</span></span>

 <span data-ttu-id="91808-110">**Примечание**. Пакет SDK для веб-заданий проверяет файлы журнала и отслеживает создание и изменение больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="91808-110">**Note:** The WebJobs SDK scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="91808-111">Это медленный процесс. После создания большого двоичного объекта функция может не вызываться несколько минут или даже дольше.</span><span class="sxs-lookup"><span data-stu-id="91808-111">This process is inherently slow; a function might not get triggered until several minutes or longer after the blob is created.</span></span>  <span data-ttu-id="91808-112">Если вашему приложению нужно обработать большой двоичный объект немедленно, советуем во время его создания создать сообщение очереди и использовать атрибут [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) вместо атрибута **BlobTrigger** в функции, которая обрабатывает большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="91808-112">If your application needs to process blobs immediately, the recommended method is to create a queue message when you create the blob, and use the [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of the **BlobTrigger** attribute on the function that processes the blob.</span></span>

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="91808-113">Один заполнитель для имени большого двоичного объекта и расширения</span><span class="sxs-lookup"><span data-stu-id="91808-113">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="91808-114">Следующий пример кода копирует текстовые большие двоичные объекты, которые появляются в контейнере *input*, в контейнер *output*.</span><span class="sxs-lookup"><span data-stu-id="91808-114">The following code sample copies text blobs that appear in the *input* container to the *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="91808-115">Конструктор атрибута принимает параметр строки, который указывает имя контейнера и заполнитель для имени большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="91808-115">The attribute constructor takes a string parameter that specifies the container name and a placeholder for the blob name.</span></span> <span data-ttu-id="91808-116">В этом примере при создании большого двоичного объекта с именем *Blob1.txt* в контейнере *input* функция создает большой двоичный объект *Blob1.txt* в контейнере *output*.</span><span class="sxs-lookup"><span data-stu-id="91808-116">In this example, if a blob named *Blob1.txt* is created in the *input* container, the function creates a blob named *Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="91808-117">Можно указать шаблон имени с заполнителем имени большого двоичного объекта, как показано в следующем примере кода:</span><span class="sxs-lookup"><span data-stu-id="91808-117">You can specify a name pattern with the blob name placeholder, as shown in the following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="91808-118">Этот код копируется только большие двоичные объекты, имена которых начинаются с original-.</span><span class="sxs-lookup"><span data-stu-id="91808-118">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="91808-119">Например, *original-Blob1.txt* в контейнере *input* копируется в *copy-Blob1.txt* в контейнере *output*.</span><span class="sxs-lookup"><span data-stu-id="91808-119">For example, *original-Blob1.txt* in the *input* container is copied to *copy-Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="91808-120">Если необходимо указать шаблон для имен больших двоичных объектов с фигурными скобками, используйте две фигурные скобки.</span><span class="sxs-lookup"><span data-stu-id="91808-120">If you need to specify a name pattern for blob names that have curly braces in the name, double the curly braces.</span></span> <span data-ttu-id="91808-121">Например, если нужно найти большие двоичные объекты в контейнере *images* с такими именами:</span><span class="sxs-lookup"><span data-stu-id="91808-121">For example, if you want to find blobs in the *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="91808-122">используйте следующую команду для своего шаблона:</span><span class="sxs-lookup"><span data-stu-id="91808-122">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="91808-123">В этом примере у заполнителя *name* будет значение *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="91808-123">In the example, the *name* placeholder value would be *soundfile.mp3*.</span></span>

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="91808-124">Отдельные заполнители для имени большого двоичного объекта и расширения</span><span class="sxs-lookup"><span data-stu-id="91808-124">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="91808-125">Следующий пример кода изменяет расширение файла во время копирования больших двоичных объектов, которые появляются в контейнере *input*, в контейнер *output*.</span><span class="sxs-lookup"><span data-stu-id="91808-125">The following code sample changes the file extension as it copies blobs that appear in the *input* container to the *output* container.</span></span> <span data-ttu-id="91808-126">Код записывает в журнал расширение большого двоичного объекта в *input* и задает для большого двоичного объекта в *output* расширение *TXT*.</span><span class="sxs-lookup"><span data-stu-id="91808-126">The code logs the extension of the *input* blob and sets the extension of the *output* blob to *.txt*.</span></span>

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

## <a name="types-that-you-can-bind-to-blobs"></a><span data-ttu-id="91808-127">Типы, которые можно привязать к большим двоичным объектам</span><span class="sxs-lookup"><span data-stu-id="91808-127">Types that you can bind to blobs</span></span>
<span data-ttu-id="91808-128">Атрибут **BlobTrigger** можно использовать со следующими типами:</span><span class="sxs-lookup"><span data-stu-id="91808-128">You can use the **BlobTrigger** attribute on the following types:</span></span>

* <span data-ttu-id="91808-129">**string**</span><span class="sxs-lookup"><span data-stu-id="91808-129">**string**</span></span>
* <span data-ttu-id="91808-130">**TextReader;**</span><span class="sxs-lookup"><span data-stu-id="91808-130">**TextReader**</span></span>
* <span data-ttu-id="91808-131">**Поток**</span><span class="sxs-lookup"><span data-stu-id="91808-131">**Stream**</span></span>
* <span data-ttu-id="91808-132">**ICloudBlob;**</span><span class="sxs-lookup"><span data-stu-id="91808-132">**ICloudBlob**</span></span>
* <span data-ttu-id="91808-133">**CloudBlockBlob**</span><span class="sxs-lookup"><span data-stu-id="91808-133">**CloudBlockBlob**</span></span>
* <span data-ttu-id="91808-134">**CloudPageBlob.**</span><span class="sxs-lookup"><span data-stu-id="91808-134">**CloudPageBlob**</span></span>
* <span data-ttu-id="91808-135">другие типы, десериализованные с помощью [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span><span class="sxs-lookup"><span data-stu-id="91808-135">Other types deserialized by [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span></span>

<span data-ttu-id="91808-136">При работе непосредственно с учетной записью хранения Azure можно также добавить параметр **CloudStorageAccount** в сигнатуру метода.</span><span class="sxs-lookup"><span data-stu-id="91808-136">If you want to work directly with the Azure storage account, you can also add a **CloudStorageAccount** parameter to the method signature.</span></span>

## <a name="getting-text-blob-content-by-binding-to-string"></a><span data-ttu-id="91808-137">Получение содержимого текстового большого двоичного объекта путем привязки к строке</span><span class="sxs-lookup"><span data-stu-id="91808-137">Getting text blob content by binding to string</span></span>
<span data-ttu-id="91808-138">Если будут использоваться текстовые большие двоичные объекты, то можно применить к параметру **string** метод **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="91808-138">If text blobs are expected, **BlobTrigger** can be applied to a **string** parameter.</span></span> <span data-ttu-id="91808-139">Код в следующем примере привязывает текстовый большой двоичный объект к параметру **string** с именем **logMessage**.</span><span class="sxs-lookup"><span data-stu-id="91808-139">The following code sample binds a text blob to a **string** parameter named **logMessage**.</span></span> <span data-ttu-id="91808-140">Функция использует этот параметр для записи содержимого большого двоичного объекта на панель мониторинга пакета SDK для заданий WebJob.</span><span class="sxs-lookup"><span data-stu-id="91808-140">The function uses that parameter to write the contents of the blob to the WebJobs SDK dashboard.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a><span data-ttu-id="91808-141">Получение содержимого сериализованного большого двоичного объекта с помощью ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="91808-141">Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="91808-142">В следующем примере кода используется класс, который реализует привязку **ICloudBlobStreamBinder**, чтобы задействовать атрибут **BlobTrigger** для привязки большого двоичного объекта к типу **WebImage**.</span><span class="sxs-lookup"><span data-stu-id="91808-142">The following code sample uses a class that implements **ICloudBlobStreamBinder** to enable the **BlobTrigger** attribute to bind a blob to the **WebImage** type.</span></span>

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

<span data-ttu-id="91808-143">Код привязки **WebImage** предоставляется в классе **WebImageBinder**, производном от **ICloudBlobStreamBinder**.</span><span class="sxs-lookup"><span data-stu-id="91808-143">The **WebImage** binding code is provided in a **WebImageBinder** class that derives from **ICloudBlobStreamBinder**.</span></span>

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

## <a name="how-to-handle-poison-blobs"></a><span data-ttu-id="91808-144">Способ обработки подозрительных больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="91808-144">How to handle poison blobs</span></span>
<span data-ttu-id="91808-145">При сбое функции **BlobTrigger** пакет SDK вызывает ее снова, если сбой вызван временной ошибкой.</span><span class="sxs-lookup"><span data-stu-id="91808-145">When a **BlobTrigger** function fails, the SDK calls it again, in case the failure was caused by a transient error.</span></span> <span data-ttu-id="91808-146">Если сбой вызван содержимым большого двоичного объекта, каждый раз при попытке обработать большой двоичный объект будет происходить сбой функции.</span><span class="sxs-lookup"><span data-stu-id="91808-146">If the failure is caused by the content of the blob, the function fails every time it tries to process the blob.</span></span> <span data-ttu-id="91808-147">По умолчанию пакет SDK вызывает функцию до 5 раз для заданного большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="91808-147">By default, the SDK calls a function up to 5 times for a given blob.</span></span> <span data-ttu-id="91808-148">Если при пятой попытке происходит сбой, пакет SDK добавляет сообщение в очередь с именем *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="91808-148">If the fifth try fails, the SDK adds a message to a queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="91808-149">Можно настроить максимальное количество попыток.</span><span class="sxs-lookup"><span data-stu-id="91808-149">The maximum number of retries is configurable.</span></span> <span data-ttu-id="91808-150">Тот же параметр [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) используется для обработки подозрительных больших двоичных объектов и подозрительных сообщений очереди.</span><span class="sxs-lookup"><span data-stu-id="91808-150">The same [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span>

<span data-ttu-id="91808-151">Сообщением очереди для подозрительных больших двоичных объектов является объект JSON, содержащий следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="91808-151">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="91808-152">FunctionId (в формате *{имя_веб-задания}*.Functions.*{имя_функции}*, например: WebJob1.Functions.CopyBlob);</span><span class="sxs-lookup"><span data-stu-id="91808-152">FunctionId (in the format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="91808-153">BlobType (BlockBlob или PageBlob);</span><span class="sxs-lookup"><span data-stu-id="91808-153">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="91808-154">ContainerName;</span><span class="sxs-lookup"><span data-stu-id="91808-154">ContainerName</span></span>
* <span data-ttu-id="91808-155">BlobName</span><span class="sxs-lookup"><span data-stu-id="91808-155">BlobName</span></span>
* <span data-ttu-id="91808-156">ETag (идентификатор версии BLOB-объектов, например 0x8D1DC6E70A277EF)</span><span class="sxs-lookup"><span data-stu-id="91808-156">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="91808-157">В следующем примере кода функция **CopyBlob** содержит код, который приводит к сбою при каждом вызове функции.</span><span class="sxs-lookup"><span data-stu-id="91808-157">In the following code sample, the **CopyBlob** function has code that causes it to fail every time it's called.</span></span> <span data-ttu-id="91808-158">После того как пакет SDK вызывает ее максимальное количество раз, в очереди подозрительных больших двоичных объектов создается сообщение, и оно обрабатывается функцией **LogPoisonBlob** .</span><span class="sxs-lookup"><span data-stu-id="91808-158">After the SDK calls it for the maximum number of retries, a message is created on the poison blob queue, and that message is processed by the **LogPoisonBlob** function.</span></span>

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

<span data-ttu-id="91808-159">Пакет SDK автоматически выполняет десериализацию сообщения JSON.</span><span class="sxs-lookup"><span data-stu-id="91808-159">The SDK automatically deserializes the JSON message.</span></span> <span data-ttu-id="91808-160">Вот класс **PoisonBlobMessage** :</span><span class="sxs-lookup"><span data-stu-id="91808-160">Here is the **PoisonBlobMessage** class:</span></span>

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a><span data-ttu-id="91808-161">Алгоритм опроса больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="91808-161">Blob polling algorithm</span></span>
<span data-ttu-id="91808-162">Пакет SDK для веб-заданий проверяет все контейнеры, задаваемые атрибутами **BlobTrigger**, при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="91808-162">The WebJobs SDK scans all containers specified by **BlobTrigger** attributes at application start.</span></span> <span data-ttu-id="91808-163">Такая проверка может занять некоторое время в большой учетной записи хранения. Поэтому для поиска новых больших двоичных объектов и выполнения функций **BlobTrigger** может потребоваться заметное количество времени.</span><span class="sxs-lookup"><span data-stu-id="91808-163">In a large storage account this scan can take some time, so it might be a while before new blobs are found and **BlobTrigger** functions are executed.</span></span>

<span data-ttu-id="91808-164">Чтобы обнаружить новые или измененные большие двоичные объекты после запуска приложения, пакет SDK периодически проверяет записи в журналах хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="91808-164">To detect new or changed blobs after application start, the SDK periodically reads from the blob storage logs.</span></span> <span data-ttu-id="91808-165">Журналы больших двоичных объектов помещаются в буфер, а физическая запись происходит каждые 10 минут или около того. Поэтому после создания или обновления большого двоичного объекта соответствующая функция **BlobTrigger** может выполняться со значительной задержкой.</span><span class="sxs-lookup"><span data-stu-id="91808-165">The blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before the corresponding **BlobTrigger** function executes.</span></span>

<span data-ttu-id="91808-166">Существует одно исключение для больших двоичных объектов, создаваемых с помощью атрибута **BlobTrigger** .</span><span class="sxs-lookup"><span data-stu-id="91808-166">There is an exception for blobs that you create by using the **Blob** attribute.</span></span> <span data-ttu-id="91808-167">Когда пакет SDK для веб-заданий создает новый большой двоичный объект, он немедленно передает его любой соответствующей функции **BlobTrigger** .</span><span class="sxs-lookup"><span data-stu-id="91808-167">When the WebJobs SDK creates a new blob, it passes the new blob immediately to any matching **BlobTrigger** functions.</span></span> <span data-ttu-id="91808-168">Поэтому при объединении входящих и исходящих больших двоичных объектов в цепочку пакет SDK может их эффективно обрабатывать.</span><span class="sxs-lookup"><span data-stu-id="91808-168">Therefore if you have a chain of blob inputs and outputs, the SDK can process them efficiently.</span></span> <span data-ttu-id="91808-169">Но если при выполнении функций обработки больших двоичных объектов, созданных или обновленных другими способами, нужны малые задержки, мы советуем использовать **QueueTrigger** вместо **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="91808-169">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using **QueueTrigger** rather than **BlobTrigger**.</span></span>

### <a name="blob-receipts"></a><span data-ttu-id="91808-170">Уведомления о получении большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="91808-170">Blob receipts</span></span>
<span data-ttu-id="91808-171">Пакет SDK для веб-заданий гарантирует, что для одного и того же нового или обновленного большого двоичного объекта функция **BlobTrigger** будет вызываться только один раз.</span><span class="sxs-lookup"><span data-stu-id="91808-171">The WebJobs SDK makes sure that no **BlobTrigger** function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="91808-172">Это достигается за счет сохранения *уведомлений о получении большого двоичного объекта* , которые позволяют определить, обработана ли версия этого большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="91808-172">It does this by maintaining *blob receipts* in order to determine if a given blob version has been processed.</span></span>

<span data-ttu-id="91808-173">Уведомления о получении большого двоичного объекта хранятся в контейнере с именем *azure-webjobs-hosts* в учетной записи хранения Azure, указанной в строке подключения AzureWebJobsStorage.</span><span class="sxs-lookup"><span data-stu-id="91808-173">Blob receipts are stored in a container named *azure-webjobs-hosts* in the Azure storage account specified by the AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="91808-174">Уведомление о получении большого двоичного объекта содержит следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="91808-174">A blob receipt has the following  information:</span></span>

* <span data-ttu-id="91808-175">функция, вызванная для большого двоичного объекта (*{имя_веб-задания}*.Functions.*{имя_функции}*, например WebJob1.Functions.CopyBlob);</span><span class="sxs-lookup"><span data-stu-id="91808-175">The function that was called for the blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="91808-176">имя контейнера;</span><span class="sxs-lookup"><span data-stu-id="91808-176">The container name</span></span>
* <span data-ttu-id="91808-177">тип большого двоичного объекта (BlockBlob или PageBlob);</span><span class="sxs-lookup"><span data-stu-id="91808-177">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="91808-178">имя большого двоичного объекта;</span><span class="sxs-lookup"><span data-stu-id="91808-178">The blob name</span></span>
* <span data-ttu-id="91808-179">ETag (идентификатор версии больших двоичных объектов, например 0x8D1DC6E70A277EF).</span><span class="sxs-lookup"><span data-stu-id="91808-179">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="91808-180">Если вам необходимо выполнить принудительную повторную обработку большого двоичного объекта, уведомление о получении этого большого двоичного объекта можно удалить из контейнера *azure-webjobs-hosts* вручную.</span><span class="sxs-lookup"><span data-stu-id="91808-180">If you want to force reprocessing of a blob, you can manually delete the blob receipt for that blob from the *azure-webjobs-hosts* container.</span></span>

## <a name="related-topics-covered-by-the-queues-article"></a><span data-ttu-id="91808-181">Связанные разделы, которые описаны в статье об очередях</span><span class="sxs-lookup"><span data-stu-id="91808-181">Related topics covered by the queues article</span></span>
<span data-ttu-id="91808-182">Дополнительную информацию об обработке больших двоичных объектов, которая инициируется сообщением очереди, а также несвязанные с обработкой больших двоичных объектов сценарии для пакета SDK для веб-заданий см. в статье [Использование пакета SDK веб-заданий для работы с хранилищем очередей Azure](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="91808-182">For information about how to handle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific to blob processing, see [How to use Azure queue storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span>

<span data-ttu-id="91808-183">В этой статье рассматриваются следующие связанные разделы:</span><span class="sxs-lookup"><span data-stu-id="91808-183">Related topics covered in that article include the following:</span></span>

* <span data-ttu-id="91808-184">Асинхронные функции</span><span class="sxs-lookup"><span data-stu-id="91808-184">Async functions</span></span>
* <span data-ttu-id="91808-185">Выполнение на нескольких экземплярах</span><span class="sxs-lookup"><span data-stu-id="91808-185">Multiple instances</span></span>
* <span data-ttu-id="91808-186">Корректное завершение работы</span><span class="sxs-lookup"><span data-stu-id="91808-186">Graceful shutdown</span></span>
* <span data-ttu-id="91808-187">Использование атрибутов пакета SDK для заданий WebJob очереди в теле функции</span><span class="sxs-lookup"><span data-stu-id="91808-187">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="91808-188">Установка строк подключения пакета SDK в коде.</span><span class="sxs-lookup"><span data-stu-id="91808-188">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="91808-189">Установка значений параметров конструктора пакета SDK для заданий WebJob в коде</span><span class="sxs-lookup"><span data-stu-id="91808-189">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="91808-190">Настройте **MaxDequeueCount** для обработки подозрительных больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="91808-190">Configure **MaxDequeueCount** for poison blob handling.</span></span>
* <span data-ttu-id="91808-191">Вызов функции вручную</span><span class="sxs-lookup"><span data-stu-id="91808-191">Trigger a function manually</span></span>
* <span data-ttu-id="91808-192">Запись журналов</span><span class="sxs-lookup"><span data-stu-id="91808-192">Write logs</span></span>

## <a name="next-steps"></a><span data-ttu-id="91808-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="91808-193">Next steps</span></span>
<span data-ttu-id="91808-194">В этой статье приведены примеры кода обработки обычных сценариев для работы с большими двоичными объектами Azure.</span><span class="sxs-lookup"><span data-stu-id="91808-194">This article has provided code samples that show how to handle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="91808-195">Дополнительная информация об использовании веб-заданий Azure и пакета SDK для веб-заданий доступна в [ресурсах с документацией по веб-заданиям Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="91808-195">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

