---
title: "Как использовать хранилище больших двоичных объектов Azure с пакетом SDK для WebJob"
description: "Информация об использовании хранилища больших двоичных объектов Azure с пакетом SDK для WebJob Вызов процесса при появлении нового большого двоичного объекта в контейнере и обработка подозрительных больших двоичных объектов."
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
ms.openlocfilehash: e0a792ccdf8097d5cde254d6d4690a64838378ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-blob-storage-with-the-webjobs-sdk"></a><span data-ttu-id="baeb0-104">Как использовать хранилище больших двоичных объектов Azure с пакетом SDK для WebJob</span><span class="sxs-lookup"><span data-stu-id="baeb0-104">How to use Azure blob storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="baeb0-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="baeb0-105">Overview</span></span>
<span data-ttu-id="baeb0-106">В этом руководстве приведены примеры кода на C# для запуска процессов при создании или обновлении большого двоичного объекта Azure.</span><span class="sxs-lookup"><span data-stu-id="baeb0-106">This guide provides C# code samples that show how to trigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="baeb0-107">В примерах кода используется [пакет SDK для веб-заданий](websites-dotnet-webjobs-sdk.md) версии 1.x.</span><span class="sxs-lookup"><span data-stu-id="baeb0-107">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="baeb0-108">Примеры кода для создания больших двоичных объектов см. в статье [Использование пакета SDK веб-заданий для работы с хранилищем очередей Azure](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="baeb0-108">For code samples that show how to create blobs, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="baeb0-109">В этом руководстве предполагается, что вы уже знаете, [как создать проект веб-задания в Visual Studio со строками подключения, указывающими на вашу учетную запись хранения](websites-dotnet-webjobs-sdk-get-started.md) или [несколько учетных записей хранения](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="baeb0-109">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

## <span data-ttu-id="baeb0-110"><a id="trigger"></a> Как вызывать функцию при создании или обновлении большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="baeb0-110"><a id="trigger"></a> How to trigger a function when a blob is created or updated</span></span>
<span data-ttu-id="baeb0-111">В этом разделе показано, как использовать атрибут `BlobTrigger` .</span><span class="sxs-lookup"><span data-stu-id="baeb0-111">This section shows how to use the `BlobTrigger` attribute.</span></span> 

> [!NOTE]
> <span data-ttu-id="baeb0-112">Пакет SDK для веб-заданий проверяет файлы журнала и отслеживает новые или измененные большие двоичные объекты.</span><span class="sxs-lookup"><span data-stu-id="baeb0-112">The WebJobs SDK scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="baeb0-113">Это не происходит в режиме реального времени. После создания большого двоичного объекта функция может не вызываться несколько минут или даже дольше.</span><span class="sxs-lookup"><span data-stu-id="baeb0-113">This process is not real-time; a function might not get triggered until several minutes or longer after the blob is created.</span></span> <span data-ttu-id="baeb0-114">Кроме того, [журналы службы хранилища создаются по принципу лучшего из возможного](https://msdn.microsoft.com/library/azure/hh343262.aspx), то есть не гарантируется регистрация всех событий.</span><span class="sxs-lookup"><span data-stu-id="baeb0-114">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; there is no guarantee that all events will be captured.</span></span> <span data-ttu-id="baeb0-115">В некоторых случаях журналы могут пропускаться.</span><span class="sxs-lookup"><span data-stu-id="baeb0-115">Under some conditions, logs might be missed.</span></span> <span data-ttu-id="baeb0-116">Если ограниченная скорость и надежность триггеров больших двоичных объектов для вашего приложения неприемлемы, советуем во время создания большого двоичного объекта создать сообщение очереди и использовать атрибут [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) вместо атрибута `BlobTrigger` в функции, которая обрабатывает этот большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="baeb0-116">If the speed and reliability limitations of blob triggers are not acceptable for your application, the recommended method is to create a queue message when you create the blob, and use the [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of the `BlobTrigger` attribute on the function that processes the blob.</span></span>
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="baeb0-117">Один заполнитель для имени большого двоичного объекта и расширения</span><span class="sxs-lookup"><span data-stu-id="baeb0-117">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="baeb0-118">Следующий пример кода копирует текстовые большие двоичные объекты, которые появляются в контейнере *input*, в контейнер *output*.</span><span class="sxs-lookup"><span data-stu-id="baeb0-118">The following code sample copies text blobs that appear in the *input* container to the *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="baeb0-119">Конструктор атрибута принимает параметр строки, который указывает имя контейнера и заполнитель для имени большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="baeb0-119">The attribute constructor takes a string parameter that specifies the container name and a placeholder for the blob name.</span></span> <span data-ttu-id="baeb0-120">В этом примере при создании большого двоичного объекта с именем *Blob1.txt* в контейнере *input* функция создает большой двоичный объект *Blob1.txt* в контейнере *output*.</span><span class="sxs-lookup"><span data-stu-id="baeb0-120">In this example, if a blob named *Blob1.txt* is created in the *input* container, the function creates a blob named *Blob1.txt* in the *output* container.</span></span> 

<span data-ttu-id="baeb0-121">Можно указать шаблон имени с заполнителем имени большого двоичного объекта, как показано в следующем примере кода:</span><span class="sxs-lookup"><span data-stu-id="baeb0-121">You can specify a name pattern with the blob name placeholder, as shown in the following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="baeb0-122">Этот код копируется только большие двоичные объекты, имена которых начинаются с original-.</span><span class="sxs-lookup"><span data-stu-id="baeb0-122">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="baeb0-123">Например, *original-Blob1.txt* в контейнере *input* копируется в *copy-Blob1.txt* в контейнере *output*.</span><span class="sxs-lookup"><span data-stu-id="baeb0-123">For example, *original-Blob1.txt* in the *input* container is copied to *copy-Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="baeb0-124">Если необходимо указать шаблон для имен больших двоичных объектов с фигурными скобками, используйте две фигурные скобки.</span><span class="sxs-lookup"><span data-stu-id="baeb0-124">If you need to specify a name pattern for blob names that have curly braces in the name, double the curly braces.</span></span> <span data-ttu-id="baeb0-125">Например, если нужно найти большие двоичные объекты в контейнере *images* с такими именами:</span><span class="sxs-lookup"><span data-stu-id="baeb0-125">For example, if you want to find blobs in the *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="baeb0-126">используйте следующую команду для своего шаблона:</span><span class="sxs-lookup"><span data-stu-id="baeb0-126">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="baeb0-127">В этом примере у заполнителя *name* будет значение *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="baeb0-127">In the example, the *name* placeholder value would be *soundfile.mp3*.</span></span> 

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="baeb0-128">Отдельные заполнители для имени большого двоичного объекта и расширения</span><span class="sxs-lookup"><span data-stu-id="baeb0-128">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="baeb0-129">Следующий пример кода изменяет расширение файла во время копирования больших двоичных объектов, которые появляются в контейнере *input*, в контейнер *output*.</span><span class="sxs-lookup"><span data-stu-id="baeb0-129">The following code sample changes the file extension as it copies blobs that appear in the *input* container to the *output* container.</span></span> <span data-ttu-id="baeb0-130">Код записывает в журнал расширение большого двоичного объекта в *input* и задает для большого двоичного объекта в *output* расширение *TXT*.</span><span class="sxs-lookup"><span data-stu-id="baeb0-130">The code logs the extension of the *input* blob and sets the extension of the *output* blob to *.txt*.</span></span>

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

## <span data-ttu-id="baeb0-131"><a id="types"></a> Типы, которые можно привязать к большим двоичным объектам</span><span class="sxs-lookup"><span data-stu-id="baeb0-131"><a id="types"></a> Types that you can bind to blobs</span></span>
<span data-ttu-id="baeb0-132">Атрибут `BlobTrigger` можно использовать со следующими типами:</span><span class="sxs-lookup"><span data-stu-id="baeb0-132">You can use the `BlobTrigger` attribute on the following types:</span></span>

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
* <span data-ttu-id="baeb0-133">другие типы, десериализованные с помощью [ICloudBlobStreamBinder](#icbsb)</span><span class="sxs-lookup"><span data-stu-id="baeb0-133">Other types deserialized by [ICloudBlobStreamBinder](#icbsb)</span></span> 

<span data-ttu-id="baeb0-134">При работе непосредственно с учетной записью хранения Azure можно также добавить параметр `CloudStorageAccount` в сигнатуру метода.</span><span class="sxs-lookup"><span data-stu-id="baeb0-134">If you want to work directly with the Azure storage account, you can also add a `CloudStorageAccount` parameter to the method signature.</span></span>

<span data-ttu-id="baeb0-135">Примеры приведены в [коде привязки больших двоичных объектов в репозитории azure-webjobs-sdk на сайте GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="baeb0-135">For examples, see the [blob binding code in the azure-webjobs-sdk repository on GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span></span>

## <span data-ttu-id="baeb0-136"><a id="string"></a> Получение содержимого большого двоичного объекта с помощью привязки к строке</span><span class="sxs-lookup"><span data-stu-id="baeb0-136"><a id="string"></a> Getting text blob content by binding to string</span></span>
<span data-ttu-id="baeb0-137">Если будут использоваться большие двоичные объекты, можно применить `BlobTrigger` к параметру `string`.</span><span class="sxs-lookup"><span data-stu-id="baeb0-137">If text blobs are expected, `BlobTrigger` can be applied to a `string` parameter.</span></span> <span data-ttu-id="baeb0-138">Следующий пример кода привязывает большой двоичный объект к параметру `string` с именем `logMessage`.</span><span class="sxs-lookup"><span data-stu-id="baeb0-138">The following code sample binds a text blob to a `string` parameter named `logMessage`.</span></span> <span data-ttu-id="baeb0-139">Функция использует этот параметр для записи содержимого большого двоичного объекта на панель мониторинга пакета SDK для заданий WebJob.</span><span class="sxs-lookup"><span data-stu-id="baeb0-139">The function uses that parameter to write the contents of the blob to the WebJobs SDK dashboard.</span></span> 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <span data-ttu-id="baeb0-140"><a id="icbsb"></a> Получение содержимого сериализованного большого двоичного объекта с помощью ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="baeb0-140"><a id="icbsb"></a> Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="baeb0-141">В следующем примере кода используется класс, реализующий `ICloudBlobStreamBinder`, что позволяет атрибуту `BlobTrigger` привязать большой двоичный объект к типу `WebImage`.</span><span class="sxs-lookup"><span data-stu-id="baeb0-141">The following code sample uses a class that implements `ICloudBlobStreamBinder` to enable the `BlobTrigger` attribute to bind a blob to the `WebImage` type.</span></span>

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

<span data-ttu-id="baeb0-142">Код привязки `WebImage` предусмотрен в классе `WebImageBinder`, который является производным от `ICloudBlobStreamBinder`.</span><span class="sxs-lookup"><span data-stu-id="baeb0-142">The `WebImage` binding code is provided in a `WebImageBinder` class that derives from `ICloudBlobStreamBinder`.</span></span>

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

## <a name="getting-the-blob-path-for-the-triggering-blob"></a><span data-ttu-id="baeb0-143">Получение пути большого двоичного объекта для активации большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="baeb0-143">Getting the blob path for the triggering blob</span></span>
<span data-ttu-id="baeb0-144">Чтобы получить имя контейнера и имя большого двоичного объекта, который активировал функцию, добавьте строковый параметр `blobTrigger` в сигнатуру функции.</span><span class="sxs-lookup"><span data-stu-id="baeb0-144">To get the container name and blob name of the blob that has triggered the function, include a `blobTrigger` string parameter in the function signature.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <span data-ttu-id="baeb0-145"><a id="poison"></a> Способ обработки подозрительных больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="baeb0-145"><a id="poison"></a> How to handle poison blobs</span></span>
<span data-ttu-id="baeb0-146">При сбое функции `BlobTrigger` пакет SDK вызывает ее снова, если сбой вызван временной ошибкой.</span><span class="sxs-lookup"><span data-stu-id="baeb0-146">When a `BlobTrigger` function fails, the SDK calls it again, in case the failure was caused by a transient error.</span></span> <span data-ttu-id="baeb0-147">Если сбой вызван содержимым большого двоичного объекта, каждый раз при попытке обработать большой двоичный объект будет происходить сбой функции.</span><span class="sxs-lookup"><span data-stu-id="baeb0-147">If the failure is caused by the content of the blob, the function fails every time it tries to process the blob.</span></span> <span data-ttu-id="baeb0-148">По умолчанию пакет SDK вызывает функцию до 5 раз для заданного большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="baeb0-148">By default, the SDK calls a function up to 5 times for a given blob.</span></span> <span data-ttu-id="baeb0-149">Если при пятой попытке происходит сбой, пакет SDK добавляет сообщение в очередь с именем *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="baeb0-149">If the fifth try fails, the SDK adds a message to a queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="baeb0-150">Можно настроить максимальное количество попыток.</span><span class="sxs-lookup"><span data-stu-id="baeb0-150">The maximum number of retries is configurable.</span></span> <span data-ttu-id="baeb0-151">Тот же параметр [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) используется для обработки подозрительных больших двоичных объектов и подозрительных сообщений очереди.</span><span class="sxs-lookup"><span data-stu-id="baeb0-151">The same [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span> 

<span data-ttu-id="baeb0-152">Сообщением очереди для подозрительных больших двоичных объектов является объект JSON, содержащий следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="baeb0-152">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="baeb0-153">FunctionId (в формате *{имя_веб-задания}*.Functions.*{имя_функции}*, например: WebJob1.Functions.CopyBlob);</span><span class="sxs-lookup"><span data-stu-id="baeb0-153">FunctionId (in the format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="baeb0-154">BlobType (BlockBlob или PageBlob);</span><span class="sxs-lookup"><span data-stu-id="baeb0-154">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="baeb0-155">ContainerName;</span><span class="sxs-lookup"><span data-stu-id="baeb0-155">ContainerName</span></span>
* <span data-ttu-id="baeb0-156">BlobName</span><span class="sxs-lookup"><span data-stu-id="baeb0-156">BlobName</span></span>
* <span data-ttu-id="baeb0-157">ETag (идентификатор версии BLOB-объектов, например 0x8D1DC6E70A277EF)</span><span class="sxs-lookup"><span data-stu-id="baeb0-157">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="baeb0-158">В следующем примере кода функция `CopyBlob` содержит код, который приводит к сбою при каждом вызове функции.</span><span class="sxs-lookup"><span data-stu-id="baeb0-158">In the following code sample, the `CopyBlob` function has code that causes it to fail every time it's called.</span></span> <span data-ttu-id="baeb0-159">После того, как пакет SDK вызывает ее максимальное количество раз, в очереди подозрительных больших двоичных объектов создается сообщение и оно обрабатывается функцией `LogPoisonBlob` .</span><span class="sxs-lookup"><span data-stu-id="baeb0-159">After the SDK calls it for the maximum number of retries, a message is created on the poison blob queue, and that message is processed by the `LogPoisonBlob` function.</span></span> 

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

<span data-ttu-id="baeb0-160">Пакет SDK автоматически выполняет десериализацию сообщения JSON.</span><span class="sxs-lookup"><span data-stu-id="baeb0-160">The SDK automatically deserializes the JSON message.</span></span> <span data-ttu-id="baeb0-161">Так выглядит класс `PoisonBlobMessage` :</span><span class="sxs-lookup"><span data-stu-id="baeb0-161">Here is the `PoisonBlobMessage` class:</span></span> 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <span data-ttu-id="baeb0-162"><a id="polling"></a> Алгоритм опроса больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="baeb0-162"><a id="polling"></a> Blob polling algorithm</span></span>
<span data-ttu-id="baeb0-163">Пакет SDK для веб-заданий проверяет все контейнеры, задаваемые атрибутами `BlobTrigger` при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="baeb0-163">The WebJobs SDK scans all containers specified by `BlobTrigger` attributes at application start.</span></span> <span data-ttu-id="baeb0-164">Такая проверка может занять некоторое время в большой учетной записи хранения. Поэтому для поиска новых больших двоичных объектов и выполнения функций `BlobTrigger` может потребоваться много времени.</span><span class="sxs-lookup"><span data-stu-id="baeb0-164">In a large storage account this scan can take some time, so it might be a while before new blobs are found and `BlobTrigger` functions are executed.</span></span>

<span data-ttu-id="baeb0-165">Чтобы обнаружить новые или измененные большие двоичные объекты после запуска приложения, пакет SDK периодически проверяет записи в журналах хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="baeb0-165">To detect new or changed blobs after application start, the SDK periodically reads from the blob storage logs.</span></span> <span data-ttu-id="baeb0-166">Журналы больших двоичных объектов помещаются в буфер, а физическая запись происходит каждые 10 минут или около того. Поэтому после создания или обновления большого двоичного объекта соответствующая функция `BlobTrigger` может выполняться со значительной задержкой.</span><span class="sxs-lookup"><span data-stu-id="baeb0-166">The blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before the corresponding `BlobTrigger` function executes.</span></span> 

<span data-ttu-id="baeb0-167">Существует одно исключение для больших двоичных объектов, создаваемых с помощью атрибута `Blob` .</span><span class="sxs-lookup"><span data-stu-id="baeb0-167">There is an exception for blobs that you create by using the `Blob` attribute.</span></span> <span data-ttu-id="baeb0-168">Когда пакет SDK для веб-заданий создает новый большой двоичный объект, он немедленно передает его любой соответствующей функции `BlobTrigger` .</span><span class="sxs-lookup"><span data-stu-id="baeb0-168">When the WebJobs SDK creates a new blob, it passes the new blob immediately to any matching `BlobTrigger` functions.</span></span> <span data-ttu-id="baeb0-169">Поэтому при объединении входящих и исходящих больших двоичных объектов в цепочку пакет SDK может их эффективно обрабатывать.</span><span class="sxs-lookup"><span data-stu-id="baeb0-169">Therefore if you have a chain of blob inputs and outputs, the SDK can process them efficiently.</span></span> <span data-ttu-id="baeb0-170">Но если при выполнении функций обработки больших двоичных объектов, созданных или обновленных другими способами, нужны малые задержки, советуем использовать `QueueTrigger` вместо `BlobTrigger`.</span><span class="sxs-lookup"><span data-stu-id="baeb0-170">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using `QueueTrigger` rather than `BlobTrigger`.</span></span>

### <span data-ttu-id="baeb0-171"><a id="receipts"></a> Уведомления о получении большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="baeb0-171"><a id="receipts"></a> Blob receipts</span></span>
<span data-ttu-id="baeb0-172">Пакет SDK для веб-заданий гарантирует, что для одного и того же нового или обновленного большого двоичного объекта функция `BlobTrigger` будет вызываться только один раз.</span><span class="sxs-lookup"><span data-stu-id="baeb0-172">The WebJobs SDK makes sure that no `BlobTrigger` function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="baeb0-173">Это достигается за счет сохранения *уведомлений о получении большого двоичного объекта* , которые позволяют определить, обработана ли версия этого большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="baeb0-173">It does this by maintaining *blob receipts* in order to determine if a given blob version has been processed.</span></span>

<span data-ttu-id="baeb0-174">Уведомления о получении большого двоичного объекта хранятся в контейнере с именем *azure-webjobs-hosts* в учетной записи хранения Azure, указанной в строке подключения AzureWebJobsStorage.</span><span class="sxs-lookup"><span data-stu-id="baeb0-174">Blob receipts are stored in a container named *azure-webjobs-hosts* in the Azure storage account specified by the AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="baeb0-175">Уведомление о получении большого двоичного объекта содержит следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="baeb0-175">A blob receipt has the following  information:</span></span>

* <span data-ttu-id="baeb0-176">функция, вызванная для большого двоичного объекта (*{имя_веб-задания}*.Functions.*{имя_функции}*, например WebJob1.Functions.CopyBlob);</span><span class="sxs-lookup"><span data-stu-id="baeb0-176">The function that was called for the blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="baeb0-177">имя контейнера;</span><span class="sxs-lookup"><span data-stu-id="baeb0-177">The container name</span></span>
* <span data-ttu-id="baeb0-178">тип большого двоичного объекта (BlockBlob или PageBlob);</span><span class="sxs-lookup"><span data-stu-id="baeb0-178">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="baeb0-179">имя большого двоичного объекта;</span><span class="sxs-lookup"><span data-stu-id="baeb0-179">The blob name</span></span>
* <span data-ttu-id="baeb0-180">ETag (идентификатор версии больших двоичных объектов, например 0x8D1DC6E70A277EF).</span><span class="sxs-lookup"><span data-stu-id="baeb0-180">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="baeb0-181">Если вам необходимо выполнить принудительную повторную обработку большого двоичного объекта, уведомление о получении этого большого двоичного объекта можно удалить из контейнера *azure-webjobs-hosts* вручную.</span><span class="sxs-lookup"><span data-stu-id="baeb0-181">If you want to force reprocessing of a blob, you can manually delete the blob receipt for that blob from the *azure-webjobs-hosts* container.</span></span>

## <span data-ttu-id="baeb0-182"><a id="queues"></a>Связанные разделы, которые описаны в статье об очередях</span><span class="sxs-lookup"><span data-stu-id="baeb0-182"><a id="queues"></a>Related topics covered by the queues article</span></span>
<span data-ttu-id="baeb0-183">Дополнительную информацию об обработке больших двоичных объектов, которая инициируется сообщением очереди, а также несвязанные с обработкой больших двоичных объектов сценарии для пакета SDK для веб-заданий см. в статье [Использование пакета SDK веб-заданий для работы с хранилищем очередей Azure](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="baeb0-183">For information about how to handle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific to blob processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="baeb0-184">В этой статье рассматриваются следующие связанные разделы:</span><span class="sxs-lookup"><span data-stu-id="baeb0-184">Related topics covered in that article include the following:</span></span>

* <span data-ttu-id="baeb0-185">Асинхронные функции</span><span class="sxs-lookup"><span data-stu-id="baeb0-185">Async functions</span></span>
* <span data-ttu-id="baeb0-186">Выполнение на нескольких экземплярах</span><span class="sxs-lookup"><span data-stu-id="baeb0-186">Multiple instances</span></span>
* <span data-ttu-id="baeb0-187">Корректное завершение работы</span><span class="sxs-lookup"><span data-stu-id="baeb0-187">Graceful shutdown</span></span>
* <span data-ttu-id="baeb0-188">Использование атрибутов пакета SDK для заданий WebJob очереди в теле функции</span><span class="sxs-lookup"><span data-stu-id="baeb0-188">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="baeb0-189">Установка строк подключения пакета SDK в коде.</span><span class="sxs-lookup"><span data-stu-id="baeb0-189">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="baeb0-190">Установка значений параметров конструктора пакета SDK для заданий WebJob в коде</span><span class="sxs-lookup"><span data-stu-id="baeb0-190">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="baeb0-191">Настройка `MaxDequeueCount` для обработки подозрительных больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="baeb0-191">Configure `MaxDequeueCount` for poison blob handling.</span></span>
* <span data-ttu-id="baeb0-192">Вызов функции вручную</span><span class="sxs-lookup"><span data-stu-id="baeb0-192">Trigger a function manually</span></span>
* <span data-ttu-id="baeb0-193">Запись журналов</span><span class="sxs-lookup"><span data-stu-id="baeb0-193">Write logs</span></span>

## <span data-ttu-id="baeb0-194"><a id="nextsteps"></a> Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="baeb0-194"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="baeb0-195">В этом руководстве предоставлены примеры кода обработки обычных сценариев для работы с большими двоичными объектами Azure.</span><span class="sxs-lookup"><span data-stu-id="baeb0-195">This guide has provided code samples that show how to handle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="baeb0-196">Дополнительную информацию об использовании веб-заданий Azure и пакета SDK для веб-заданий см. в [рекомендуемых ресурсах для веб-заданий Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="baeb0-196">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

