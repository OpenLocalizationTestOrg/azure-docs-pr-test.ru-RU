---
title: "Обзор записи концентраторов событий Azure | Документация Майкрософт"
description: "Запись телеметрических данных с помощью записи концентраторов событий."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e53cdeea-8a6a-474e-9f96-59d43c0e8562
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: sethm;darosa
ms.openlocfilehash: 9ae6aa57200b99f382c6e60565db9cfc69f1d3c6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-event-hubs-capture"></a><span data-ttu-id="2c3ef-103">Запись концентраторов событий Azure</span><span class="sxs-lookup"><span data-stu-id="2c3ef-103">Azure Event Hubs Capture</span></span>

<span data-ttu-id="2c3ef-104">Запись концентраторов событий Azure позволяет автоматически доставлять определенный объем потоковых данных из концентраторов событий в учетную запись [хранилища BLOB-объектов Azure](https://azure.microsoft.com/services/storage/blobs/) или [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) с указанным интервалом времени и размера.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-104">Azure Event Hubs Capture enables you to automatically deliver the streaming data in Event Hubs to an [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account of your choice, with the added flexibility of specifying a time or size interval.</span></span> <span data-ttu-id="2c3ef-105">Настройка записи выполняется быстро, ее использование не влечет дополнительных административных расходов, а масштабирование осуществляется автоматически на основе [единиц пропускной способности](event-hubs-features.md#capacity) концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-105">Setting up Capture is fast, there are no administrative costs to run it, and it scales automatically with Event Hubs [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="2c3ef-106">Запись концентраторов событий — это самый удобный способ передачи потоковых данных в Azure. Он позволяет сосредоточиться на обработке данных, а не на их записи.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-106">Event Hubs Capture is the easiest way to load streaming data into Azure, and enables you to focus on data processing rather than on data capture.</span></span>

<span data-ttu-id="2c3ef-107">Кроме того, запись концентраторов событий обеспечивает обработку конвейеров в режиме реального времени и на основе пакетов в одном потоке,</span><span class="sxs-lookup"><span data-stu-id="2c3ef-107">Event Hubs Capture enables you to process real-time and batch-based pipelines on the same stream.</span></span> <span data-ttu-id="2c3ef-108">благодаря чему вы можете создавать решения, масштабируемые по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-108">This means you can build solutions that grow with your needs over time.</span></span> <span data-ttu-id="2c3ef-109">Независимо от того, что вам нужно (создать системы на основе пакетов с учетом будущих потребностей в обработке данных в режиме реального времени или добавить эффективный холодный путь к имеющемуся решению для обработки в режиме реального времени), запись концентраторов событий упрощает работу с потоковыми данными.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-109">Whether you're building batch-based systems today with an eye towards future real-time processing, or you want to add an efficient cold path to an existing real-time solution, Event Hubs Capture makes working with streaming data easier.</span></span>

## <a name="how-event-hubs-capture-works"></a><span data-ttu-id="2c3ef-110">Принцип работы записи концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="2c3ef-110">How Event Hubs Capture works</span></span>

<span data-ttu-id="2c3ef-111">Концентраторы событий — это устойчивый буфер для хранения входящих данных телеметрии в течение определенного времени, подобный распределенному журналу.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-111">Event Hubs is a time-retention durable buffer for telemetry ingress, similar to a distributed log.</span></span> <span data-ttu-id="2c3ef-112">Масштабирование в концентраторах событий выполняется в рамках [модели секционированных потребителей](event-hubs-features.md#partitions).</span><span class="sxs-lookup"><span data-stu-id="2c3ef-112">The key to scaling in Event Hubs is the [partitioned consumer model](event-hubs-features.md#partitions).</span></span> <span data-ttu-id="2c3ef-113">Каждая секция — это независимый сегмент данных, потребление которого осуществляется отдельно.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-113">Each partition is an independent segment of data and is consumed independently.</span></span> <span data-ttu-id="2c3ef-114">По истечении настроенного срока хранения эти данные устаревают,</span><span class="sxs-lookup"><span data-stu-id="2c3ef-114">Over time this data ages off, based on the configurable retention period.</span></span> <span data-ttu-id="2c3ef-115">поэтому определенный концентратор событий никогда не заполняется полностью.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-115">As a result, a given event hub never gets "too full."</span></span>

<span data-ttu-id="2c3ef-116">Запись концентраторов событий позволяет указать собственную учетную запись хранилища BLOB-объектов Azure и контейнер, или учетную запись Azure Data Lake Store, используемые для хранения собранных данных.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-116">Event Hubs Capture enables you to specify your own Azure Blob storage account and container, or Azure Data Lake Store account, which are used to store the captured data.</span></span> <span data-ttu-id="2c3ef-117">Эти учетные записи могут находиться в том же регионе, что и концентратор событий, или в другом. Это расширяет гибкость записи концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-117">These accounts can be in the same region as your event hub or in another region, adding to the flexibility of the Event Hubs Capture feature.</span></span>

<span data-ttu-id="2c3ef-118">Собранные данные записываются в формате [Apache Avro][Apache Avro] — сжатый быстрый двоичный формат, обеспечивающий эффективную структуру данных за счет встроенной схемы.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-118">Captured data is written in [Apache Avro][Apache Avro] format: a compact, fast, binary format that provides rich data structures with inline schema.</span></span> <span data-ttu-id="2c3ef-119">Этот формат широко используется в экосистеме Hadoop, Stream Analytics и фабрике данных Azure.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-119">This format is widely used in the Hadoop ecosystem, Stream Analytics, and Azure Data Factory.</span></span> <span data-ttu-id="2c3ef-120">Работа с Avro более подробно описана далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-120">More information about working with Avro is available later in this article.</span></span>

### <a name="capture-windowing"></a><span data-ttu-id="2c3ef-121">Управление окнами в записи</span><span class="sxs-lookup"><span data-stu-id="2c3ef-121">Capture windowing</span></span>

<span data-ttu-id="2c3ef-122">В функции записи концентраторов событий можно настроить окно управления записью.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-122">Event Hubs Capture enables you to set up a window to control capturing.</span></span> <span data-ttu-id="2c3ef-123">Это окно с минимальным размером и продолжительностью, для которого предусмотрена политика "побеждает первый". Это означает, что первый обнаруженный триггер активирует операцию записи.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-123">This window is a minimum size and time configuration with a "first wins policy," meaning that the first trigger encountered causes a capture operation.</span></span> <span data-ttu-id="2c3ef-124">При наличии окна записи размером в 100 МБ и продолжительностью 15 минут для отправки данных со скоростью 1 МБ/с сначала используется окно размера, а затем — окно времени.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-124">If you have a fifteen-minute, 100 MB capture window and send 1 MB per second, the size window triggers before the time window.</span></span> <span data-ttu-id="2c3ef-125">Запись каждой секции выполняется отдельно, а запись выполненного блочного BLOB-объекта осуществляется в процессе записи. Имя блочного BLOB-объекта зависит от времени создания записи.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-125">Each partition captures independently and writes a completed block blob at the time of capture, named for the time at which the capture interval was encountered.</span></span> <span data-ttu-id="2c3ef-126">Соглашение об именовании хранилища выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2c3ef-126">The storage naming convention is as follows:</span></span>

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-to-throughput-units"></a><span data-ttu-id="2c3ef-127">Масштабирование единиц пропускной способности</span><span class="sxs-lookup"><span data-stu-id="2c3ef-127">Scaling to throughput units</span></span>

<span data-ttu-id="2c3ef-128">Трафик концентраторов событий контролируется с помощью [единиц пропускной способности](event-hubs-features.md#capacity).</span><span class="sxs-lookup"><span data-stu-id="2c3ef-128">Event Hubs traffic is controlled by [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="2c3ef-129">Одна единица пропускной способности разрешает передачу до 1 МБ/с или 1000 событий/с для входящих данных или до 2 МБ/с или 2000 событий/с для исходящих данных.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-129">A single throughput unit allows 1 MB per second or 1000 events per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="2c3ef-130">Для концентраторов событий (цен. категория "Стандартный") можно настроить от 1 до 20 единиц пропускной способности. Кроме того, можно отправить запрос на увеличение квоты в [службу поддержки][support request].</span><span class="sxs-lookup"><span data-stu-id="2c3ef-130">Standard Event Hubs can be configured with 1-20 throughput units, and you can purchase more with a quota increase [support request][support request].</span></span> <span data-ttu-id="2c3ef-131">Использование единиц пропускной способности свыше приобретенного количества регулируется.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-131">Usage beyond your purchased throughput units is throttled.</span></span> <span data-ttu-id="2c3ef-132">Функция записи концентраторов событий копирует данные непосредственно из внутреннего хранилища концентраторов событий. При этом выполняется обход квоты на единицы пропускной способности для исходящего трафика, а этот трафик сохраняется для других средств обработки, например Stream Analytics или Spark.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-132">Event Hubs Capture copies data directly from the internal Event Hubs storage, bypassing throughput unit egress quotas and saving your egress for other processing readers, such as Stream Analytics or Spark.</span></span>

<span data-ttu-id="2c3ef-133">После настройки функция записи концентраторов событий автоматически запускается при отправке первого события и продолжает работать.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-133">Once configured, Event Hubs Capture runs automatically when you send your first event, and continues running.</span></span> <span data-ttu-id="2c3ef-134">Чтобы позволить операции последующей обработки установить, что процесс выполняется, при отсутствии данных концентраторы событий записывают пустые файлы.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-134">To make it easier for your downstream processing to know that the process is working, Event Hubs writes empty files when there is no data.</span></span> <span data-ttu-id="2c3ef-135">Этот процесс обеспечивает прогнозируемую периодичность и позволяет получить маркер, необходимый для пакетных обработчиков.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-135">This process provides a predictable cadence and marker that can feed your batch processors.</span></span>

## <a name="setting-up-event-hubs-capture"></a><span data-ttu-id="2c3ef-136">Настройка записи концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="2c3ef-136">Setting up Event Hubs Capture</span></span>

<span data-ttu-id="2c3ef-137">Запись можно настроить при создании концентратора событий с помощью [портала Azure](https://portal.azure.com) или с помощью шаблонов Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-137">You can configure Capture at the event hub creation time using the [Azure portal](https://portal.azure.com), or using Azure Resource Manager templates.</span></span> <span data-ttu-id="2c3ef-138">Дополнительные сведения см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="2c3ef-138">For more information, see the following articles:</span></span>

- [<span data-ttu-id="2c3ef-139">Включение записи концентраторов событий с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="2c3ef-139">Enable Event Hubs Capture using the Azure portal</span></span>](event-hubs-capture-enable-through-portal.md)
- [<span data-ttu-id="2c3ef-140">Создание пространства имен концентраторов событий с концентратором событий и включение записи с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2c3ef-140">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-the-captured-files-and-working-with-avro"></a><span data-ttu-id="2c3ef-141">Просмотр собранных файлов и работа с Avro</span><span class="sxs-lookup"><span data-stu-id="2c3ef-141">Exploring the captured files and working with Avro</span></span>

<span data-ttu-id="2c3ef-142">Функция записи концентраторов событий создает файлы в формате Avro, как указано в настроенном окне времени.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-142">Event Hubs Capture creates files in Avro format, as specified on the configured time window.</span></span> <span data-ttu-id="2c3ef-143">Эти файлы можно просмотреть в любом инструменте, например в [Azure Storage Explorer][Azure Storage Explorer].</span><span class="sxs-lookup"><span data-stu-id="2c3ef-143">You can view these files in any tool such as [Azure Storage Explorer][Azure Storage Explorer].</span></span> <span data-ttu-id="2c3ef-144">Чтобы выполнить определенные действия с этими файлами, их можно скачать локально.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-144">You can download the files locally to work on them.</span></span>

<span data-ttu-id="2c3ef-145">Файлы, созданные записью концентраторов событий, имеют следующую схему Avro.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-145">The files produced by Event Hubs Capture have the following Avro schema:</span></span>

![][3]

<span data-ttu-id="2c3ef-146">Файлы Avro можно легко просмотреть с помощью [инструментов Avro][Avro Tools] (JAR-файла) из Apache.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-146">An easy way to explore Avro files is by using the [Avro Tools][Avro Tools] jar from Apache.</span></span> <span data-ttu-id="2c3ef-147">После того как вы скачали этот JAR-файл, чтобы просмотреть схему определенного файла Avro, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2c3ef-147">After downloading this jar, you can see the schema of a specific Avro file by running the following command:</span></span>

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

<span data-ttu-id="2c3ef-148">Эта команда возвращает следующее:</span><span class="sxs-lookup"><span data-stu-id="2c3ef-148">This command returns</span></span>

```
{

    "type":"record",
    "name":"EventData",
    "namespace":"Microsoft.ServiceBus.Messaging",
    "fields":[
                 {"name":"SequenceNumber","type":"long"},
                 {"name":"Offset","type":"string"},
                 {"name":"EnqueuedTimeUtc","type":"string"},
                 {"name":"SystemProperties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Properties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Body","type":["null","bytes"]}
             ]
}
```

<span data-ttu-id="2c3ef-149">Средства Avro можно также использовать для преобразования файлов в формат JSON и выполнения других задач обработки.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-149">You can also use Avro Tools to convert the file to JSON format and perform other processing.</span></span>

<span data-ttu-id="2c3ef-150">Чтобы выполнить более расширенную обработку, скачайте и установите Avro для определенной платформы.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-150">To perform more advanced processing, download and install Avro for your choice of platform.</span></span> <span data-ttu-id="2c3ef-151">На момент написания статьи средства Avro доступны для следующих платформ: C, C++, C\#, Java, NodeJS, Perl, PHP, Python и Ruby.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-151">At the time of this writing, there are implementations available for C, C++, C\#, Java, NodeJS, Perl, PHP, Python, and Ruby.</span></span>

<span data-ttu-id="2c3ef-152">Apache Avro предоставляет руководства по началу работы для платформ [Java][Java] и [Python][Python].</span><span class="sxs-lookup"><span data-stu-id="2c3ef-152">Apache Avro has complete Getting Started guides for [Java][Java] and [Python][Python].</span></span> <span data-ttu-id="2c3ef-153">Дополнительные сведения см. в статье [Пошаговое руководство. Использование записи концентраторов событий с Python](event-hubs-capture-python.md).</span><span class="sxs-lookup"><span data-stu-id="2c3ef-153">You can also read the [Getting started with Event Hubs Capture](event-hubs-capture-python.md) article.</span></span>

## <a name="how-event-hubs-capture-is-charged"></a><span data-ttu-id="2c3ef-154">Выставление счета за запись концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="2c3ef-154">How Event Hubs Capture is charged</span></span>

<span data-ttu-id="2c3ef-155">Выставление счета за запись концентраторов событий осуществляется подобно тарификации за единицы пропускной способности, то есть каждый час.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-155">Event Hubs Capture is metered similarly to throughput units: as an hourly charge.</span></span> <span data-ttu-id="2c3ef-156">Размер платы прямо пропорционален количеству единиц пропускной способности, приобретенных для пространства имен.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-156">The charge is directly proportional to the number of throughput units purchased for the namespace.</span></span> <span data-ttu-id="2c3ef-157">Так же как и с единицами пропускной способности, размер записи концентраторов событий можно регулировать, чтобы обеспечить соответствующую производительность.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-157">As throughput units are increased and decreased, Event Hubs Capture meters increase and decrease to provide matching performance.</span></span> <span data-ttu-id="2c3ef-158">Единицы измерения действуют совместно.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-158">The meters occur in tandem.</span></span> <span data-ttu-id="2c3ef-159">Дополнительные сведения о ценах см. на странице цен на [концентраторы событий](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="2c3ef-159">For pricing details, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2c3ef-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2c3ef-160">Next steps</span></span>

<span data-ttu-id="2c3ef-161">Запись концентраторов событий — это самый быстрый способ передать данные в Azure.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-161">Event Hubs Capture is the easiest way to get data into Azure.</span></span> <span data-ttu-id="2c3ef-162">С помощью знакомых средств и платформ (Azure Data Lake, фабрики данных Azure и Azure HDInsight) можно выполнять необходимую пакетную обработку и другие операции анализа в любом масштабе.</span><span class="sxs-lookup"><span data-stu-id="2c3ef-162">Using Azure Data Lake, Azure Data Factory, and Azure HDInsight, you can perform batch processing and other analytics using familiar tools and platforms of your choosing, at any scale you need.</span></span>

<span data-ttu-id="2c3ef-163">Дополнительные сведения о концентраторах событий см. в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="2c3ef-163">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="2c3ef-164">Отправка событий в концентраторы событий Azure с помощью платформы .NET Framework</span><span class="sxs-lookup"><span data-stu-id="2c3ef-164">Get started sending and receiving events</span></span>](event-hubs-dotnet-framework-getstarted-send.md)
* <span data-ttu-id="2c3ef-165">Полный [пример приложения, использующего концентраторы событий][sample application that uses Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="2c3ef-165">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs]</span></span>
* <span data-ttu-id="2c3ef-166">[Обзор концентраторов событий Azure][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="2c3ef-166">[Event Hubs overview][Event Hubs overview]</span></span>

[Apache Avro]: http://avro.apache.org/
[support request]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[Azure Storage Explorer]: http://azurestorageexplorer.codeplex.com/
[3]: ./media/event-hubs-capture-overview/event-hubs-capture3.png
[Avro Tools]: http://www-us.apache.org/dist/avro/avro-1.8.2/java/avro-tools-1.8.2.jar
[Java]: http://avro.apache.org/docs/current/gettingstartedjava.html
[Python]: http://avro.apache.org/docs/current/gettingstartedpython.html
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
