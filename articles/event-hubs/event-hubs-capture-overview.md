---
title: "aaaOverview из записи концентраторов событий Azure | Документы Microsoft"
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
ms.openlocfilehash: 0238cae712a0ed7bdf3e87ee93a069a553cb65df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-event-hubs-capture"></a><span data-ttu-id="287d3-103">Запись концентраторов событий Azure</span><span class="sxs-lookup"><span data-stu-id="287d3-103">Azure Event Hubs Capture</span></span>

<span data-ttu-id="287d3-104">Записать Azure концентраторов событий позволяет hello доставки tooautomatically потоковой передачи данных в концентраторы событий tooan [хранилища больших двоичных объектов Azure](https://azure.microsoft.com/services/storage/blobs/) или [хранилища Озера данных Azure](https://azure.microsoft.com/services/data-lake-store/) добавить учетную запись по своему усмотрению с hello гибкость указания времени или размер интервала.</span><span class="sxs-lookup"><span data-stu-id="287d3-104">Azure Event Hubs Capture enables you tooautomatically deliver hello streaming data in Event Hubs tooan [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account of your choice, with hello added flexibility of specifying a time or size interval.</span></span> <span data-ttu-id="287d3-105">Настройка отслеживания очень быстро, существуют не toorun расходы на администрирование, он и он автоматически масштабируется с концентраторами событий [единиц производительности](event-hubs-features.md#capacity).</span><span class="sxs-lookup"><span data-stu-id="287d3-105">Setting up Capture is fast, there are no administrative costs toorun it, and it scales automatically with Event Hubs [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="287d3-106">Записать концентраторов событий является наиболее простым способом tooload hello потоковой передачи данных в Azure, а также позволяет toofocus обработки данных, а не система отслеживания измененных данных.</span><span class="sxs-lookup"><span data-stu-id="287d3-106">Event Hubs Capture is hello easiest way tooload streaming data into Azure, and enables you toofocus on data processing rather than on data capture.</span></span>

<span data-ttu-id="287d3-107">Записать концентраторов событий позволяет tooprocess в режиме реального времени и пакетные конвейеры на hello того же потока.</span><span class="sxs-lookup"><span data-stu-id="287d3-107">Event Hubs Capture enables you tooprocess real-time and batch-based pipelines on hello same stream.</span></span> <span data-ttu-id="287d3-108">благодаря чему вы можете создавать решения, масштабируемые по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="287d3-108">This means you can build solutions that grow with your needs over time.</span></span> <span data-ttu-id="287d3-109">Вы создаете системах на базе пакета сегодня с глазу для будущей обработки в режиме реального времени или вы хотите tooadd эффективный путь холодного tooan существующее в реальном времени решение, записать концентраторов событий упрощает работу с потоковой передачи данных.</span><span class="sxs-lookup"><span data-stu-id="287d3-109">Whether you're building batch-based systems today with an eye towards future real-time processing, or you want tooadd an efficient cold path tooan existing real-time solution, Event Hubs Capture makes working with streaming data easier.</span></span>

## <a name="how-event-hubs-capture-works"></a><span data-ttu-id="287d3-110">Принцип работы записи концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="287d3-110">How Event Hubs Capture works</span></span>

<span data-ttu-id="287d3-111">Концентраторы событий является буфером устойчивых время хранения для входящих данных телеметрии, аналогичные tooa распределенных журнала.</span><span class="sxs-lookup"><span data-stu-id="287d3-111">Event Hubs is a time-retention durable buffer for telemetry ingress, similar tooa distributed log.</span></span> <span data-ttu-id="287d3-112">tooscaling ключа Hello в концентраторы событий — hello [модели](event-hubs-features.md#partitions).</span><span class="sxs-lookup"><span data-stu-id="287d3-112">hello key tooscaling in Event Hubs is hello [partitioned consumer model](event-hubs-features.md#partitions).</span></span> <span data-ttu-id="287d3-113">Каждая секция — это независимый сегмент данных, потребление которого осуществляется отдельно.</span><span class="sxs-lookup"><span data-stu-id="287d3-113">Each partition is an independent segment of data and is consumed independently.</span></span> <span data-ttu-id="287d3-114">Со временем эти данные устаревают, off на основании hello заданного срока хранения.</span><span class="sxs-lookup"><span data-stu-id="287d3-114">Over time this data ages off, based on hello configurable retention period.</span></span> <span data-ttu-id="287d3-115">поэтому определенный концентратор событий никогда не заполняется полностью.</span><span class="sxs-lookup"><span data-stu-id="287d3-115">As a result, a given event hub never gets "too full."</span></span>

<span data-ttu-id="287d3-116">Захвата концентраторов событий позволяет вам toospecify учетной записи хранилища больших двоичных объектов Azure и контейнер или учетной записи хранилища Озера данных Azure, которая используется toostore hello собранных данных.</span><span class="sxs-lookup"><span data-stu-id="287d3-116">Event Hubs Capture enables you toospecify your own Azure Blob storage account and container, or Azure Data Lake Store account, which are used toostore hello captured data.</span></span> <span data-ttu-id="287d3-117">Эти учетные записи могут находиться в hello же регионе, как концентратора событий или в другой области, добавление toohello гибкость функция сбора концентраторов событий hello.</span><span class="sxs-lookup"><span data-stu-id="287d3-117">These accounts can be in hello same region as your event hub or in another region, adding toohello flexibility of hello Event Hubs Capture feature.</span></span>

<span data-ttu-id="287d3-118">Собранные данные записываются в формате [Apache Avro][Apache Avro] — сжатый быстрый двоичный формат, обеспечивающий эффективную структуру данных за счет встроенной схемы.</span><span class="sxs-lookup"><span data-stu-id="287d3-118">Captured data is written in [Apache Avro][Apache Avro] format: a compact, fast, binary format that provides rich data structures with inline schema.</span></span> <span data-ttu-id="287d3-119">Этот формат широко используется в экосистеме Hadoop hello, Stream Analytics и фабрики данных Azure.</span><span class="sxs-lookup"><span data-stu-id="287d3-119">This format is widely used in hello Hadoop ecosystem, Stream Analytics, and Azure Data Factory.</span></span> <span data-ttu-id="287d3-120">Работа с Avro более подробно описана далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="287d3-120">More information about working with Avro is available later in this article.</span></span>

### <a name="capture-windowing"></a><span data-ttu-id="287d3-121">Управление окнами в записи</span><span class="sxs-lookup"><span data-stu-id="287d3-121">Capture windowing</span></span>

<span data-ttu-id="287d3-122">Записать концентраторов событий позволяет tooset копирование захват toocontrol окна.</span><span class="sxs-lookup"><span data-stu-id="287d3-122">Event Hubs Capture enables you tooset up a window toocontrol capturing.</span></span> <span data-ttu-id="287d3-123">Это окно будет минимальный размер и время конфигурации с «первый wins политики «это означает, что операции записи, hello пределов обнаружил триггер.</span><span class="sxs-lookup"><span data-stu-id="287d3-123">This window is a minimum size and time configuration with a "first wins policy," meaning that hello first trigger encountered causes a capture operation.</span></span> <span data-ttu-id="287d3-124">При наличии пятнадцать минут 100 МБ окна сбора данных и отправки 1 МБ в секунду, hello размер окна триггеры перед hello временного окна.</span><span class="sxs-lookup"><span data-stu-id="287d3-124">If you have a fifteen-minute, 100 MB capture window and send 1 MB per second, hello size window triggers before hello time window.</span></span> <span data-ttu-id="287d3-125">Каждая секция захватывает независимо друг от друга и записывает завершенного большого двоичного объекта на момент hello захвата, с именем hello времени, на какие hello обнаружена интервал захвата.</span><span class="sxs-lookup"><span data-stu-id="287d3-125">Each partition captures independently and writes a completed block blob at hello time of capture, named for hello time at which hello capture interval was encountered.</span></span> <span data-ttu-id="287d3-126">соглашение об именовании хранилища Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="287d3-126">hello storage naming convention is as follows:</span></span>

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-toothroughput-units"></a><span data-ttu-id="287d3-127">Единицы масштабирования toothroughput</span><span class="sxs-lookup"><span data-stu-id="287d3-127">Scaling toothroughput units</span></span>

<span data-ttu-id="287d3-128">Трафик концентраторов событий контролируется с помощью [единиц пропускной способности](event-hubs-features.md#capacity).</span><span class="sxs-lookup"><span data-stu-id="287d3-128">Event Hubs traffic is controlled by [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="287d3-129">Одна единица пропускной способности разрешает передачу до 1 МБ/с или 1000 событий/с для входящих данных или до 2 МБ/с или 2000 событий/с для исходящих данных.</span><span class="sxs-lookup"><span data-stu-id="287d3-129">A single throughput unit allows 1 MB per second or 1000 events per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="287d3-130">Для концентраторов событий (цен. категория "Стандартный") можно настроить от 1 до 20 единиц пропускной способности. Кроме того, можно отправить запрос на увеличение квоты в [службу поддержки][support request].</span><span class="sxs-lookup"><span data-stu-id="287d3-130">Standard Event Hubs can be configured with 1-20 throughput units, and you can purchase more with a quota increase [support request][support request].</span></span> <span data-ttu-id="287d3-131">Использование единиц пропускной способности свыше приобретенного количества регулируется.</span><span class="sxs-lookup"><span data-stu-id="287d3-131">Usage beyond your purchased throughput units is throttled.</span></span> <span data-ttu-id="287d3-132">Записать концентраторов событий копирует данные напрямую из внутреннего хранилища концентраторов событий hello, обход квоты исходящих единицы пропускной способности и сохранение на исходящие данные для других модулей чтения обработки, например Stream Analytics или Spark.</span><span class="sxs-lookup"><span data-stu-id="287d3-132">Event Hubs Capture copies data directly from hello internal Event Hubs storage, bypassing throughput unit egress quotas and saving your egress for other processing readers, such as Stream Analytics or Spark.</span></span>

<span data-ttu-id="287d3-133">После настройки функция записи концентраторов событий автоматически запускается при отправке первого события и продолжает работать.</span><span class="sxs-lookup"><span data-stu-id="287d3-133">Once configured, Event Hubs Capture runs automatically when you send your first event, and continues running.</span></span> <span data-ttu-id="287d3-134">toomake, облегчить работу вашей последующей обработки tooknow работы процесса hello концентраторов событий записывает пустые файлы при нет данных.</span><span class="sxs-lookup"><span data-stu-id="287d3-134">toomake it easier for your downstream processing tooknow that hello process is working, Event Hubs writes empty files when there is no data.</span></span> <span data-ttu-id="287d3-135">Этот процесс обеспечивает прогнозируемую периодичность и позволяет получить маркер, необходимый для пакетных обработчиков.</span><span class="sxs-lookup"><span data-stu-id="287d3-135">This process provides a predictable cadence and marker that can feed your batch processors.</span></span>

## <a name="setting-up-event-hubs-capture"></a><span data-ttu-id="287d3-136">Настройка записи концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="287d3-136">Setting up Event Hubs Capture</span></span>

<span data-ttu-id="287d3-137">Можно настроить записи время hello события концентратора создания с помощью hello [портал Azure](https://portal.azure.com), или с помощью шаблонов диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="287d3-137">You can configure Capture at hello event hub creation time using hello [Azure portal](https://portal.azure.com), or using Azure Resource Manager templates.</span></span> <span data-ttu-id="287d3-138">Дополнительные сведения см. в разделе hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="287d3-138">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="287d3-139">Разрешить отслеживание концентраторов событий с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="287d3-139">Enable Event Hubs Capture using hello Azure portal</span></span>](event-hubs-capture-enable-through-portal.md)
- [<span data-ttu-id="287d3-140">Создание пространства имен концентраторов событий с концентратором событий и включение записи с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="287d3-140">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-hello-captured-files-and-working-with-avro"></a><span data-ttu-id="287d3-141">Исследование hello собранных файлов и работа с Avro</span><span class="sxs-lookup"><span data-stu-id="287d3-141">Exploring hello captured files and working with Avro</span></span>

<span data-ttu-id="287d3-142">Записать концентраторов событий создает файлы в формате Avro, как указано на hello настроить интервал времени.</span><span class="sxs-lookup"><span data-stu-id="287d3-142">Event Hubs Capture creates files in Avro format, as specified on hello configured time window.</span></span> <span data-ttu-id="287d3-143">Эти файлы можно просмотреть в любом инструменте, например в [Azure Storage Explorer][Azure Storage Explorer].</span><span class="sxs-lookup"><span data-stu-id="287d3-143">You can view these files in any tool such as [Azure Storage Explorer][Azure Storage Explorer].</span></span> <span data-ttu-id="287d3-144">Вы можете загрузить hello файлы локально toowork на них.</span><span class="sxs-lookup"><span data-stu-id="287d3-144">You can download hello files locally toowork on them.</span></span>

<span data-ttu-id="287d3-145">Hello файлы, созданные системой отслеживания концентраторов событий имеют следующие схемы Avro hello.</span><span class="sxs-lookup"><span data-stu-id="287d3-145">hello files produced by Event Hubs Capture have hello following Avro schema:</span></span>

![][3]

<span data-ttu-id="287d3-146">Можно легко tooexplore Avro файлы с помощью hello [средства Avro] [ Avro Tools] jar с Apache.</span><span class="sxs-lookup"><span data-stu-id="287d3-146">An easy way tooexplore Avro files is by using hello [Avro Tools][Avro Tools] jar from Apache.</span></span> <span data-ttu-id="287d3-147">Загрузив этот JAR-файл, можно просмотреть схемы hello конкретного файла, Avro, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="287d3-147">After downloading this jar, you can see hello schema of a specific Avro file by running hello following command:</span></span>

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

<span data-ttu-id="287d3-148">Эта команда возвращает следующее:</span><span class="sxs-lookup"><span data-stu-id="287d3-148">This command returns</span></span>

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

<span data-ttu-id="287d3-149">Можно также использовать формат Avro средства tooconvert hello файла tooJSON и выполнять другие операции по обработке.</span><span class="sxs-lookup"><span data-stu-id="287d3-149">You can also use Avro Tools tooconvert hello file tooJSON format and perform other processing.</span></span>

<span data-ttu-id="287d3-150">tooperform более сложных обработки, загрузите и установите Avro для выбора платформы.</span><span class="sxs-lookup"><span data-stu-id="287d3-150">tooperform more advanced processing, download and install Avro for your choice of platform.</span></span> <span data-ttu-id="287d3-151">На момент написания этой статьи hello, существуют реализации для C, C++, C\#, Java, NodeJS, Perl, PHP, Python и Ruby.</span><span class="sxs-lookup"><span data-stu-id="287d3-151">At hello time of this writing, there are implementations available for C, C++, C\#, Java, NodeJS, Perl, PHP, Python, and Ruby.</span></span>

<span data-ttu-id="287d3-152">Apache Avro предоставляет руководства по началу работы для платформ [Java][Java] и [Python][Python].</span><span class="sxs-lookup"><span data-stu-id="287d3-152">Apache Avro has complete Getting Started guides for [Java][Java] and [Python][Python].</span></span> <span data-ttu-id="287d3-153">Можно также прочитать hello [Приступая к работе с захвата концентраторов событий](event-hubs-capture-python.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="287d3-153">You can also read hello [Getting started with Event Hubs Capture](event-hubs-capture-python.md) article.</span></span>

## <a name="how-event-hubs-capture-is-charged"></a><span data-ttu-id="287d3-154">Выставление счета за запись концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="287d3-154">How Event Hubs Capture is charged</span></span>

<span data-ttu-id="287d3-155">Записать концентраторов событий измеряется аналогично toothroughput единицы: как почасовой издержки.</span><span class="sxs-lookup"><span data-stu-id="287d3-155">Event Hubs Capture is metered similarly toothroughput units: as an hourly charge.</span></span> <span data-ttu-id="287d3-156">Hello взимается прямо пропорционально toohello количество единиц производительности, приобретенных для пространства имен hello.</span><span class="sxs-lookup"><span data-stu-id="287d3-156">hello charge is directly proportional toohello number of throughput units purchased for hello namespace.</span></span> <span data-ttu-id="287d3-157">Как единицы увеличиваются и уменьшаются, метрах захвата концентраторов событий увеличения и уменьшения tooprovide сопоставления производительности.</span><span class="sxs-lookup"><span data-stu-id="287d3-157">As throughput units are increased and decreased, Event Hubs Capture meters increase and decrease tooprovide matching performance.</span></span> <span data-ttu-id="287d3-158">Hello метрах возникают вместе.</span><span class="sxs-lookup"><span data-stu-id="287d3-158">hello meters occur in tandem.</span></span> <span data-ttu-id="287d3-159">Дополнительные сведения о ценах см. на странице цен на [концентраторы событий](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="287d3-159">For pricing details, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="287d3-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="287d3-160">Next steps</span></span>

<span data-ttu-id="287d3-161">Записать концентраторов событий — hello простым способом tooget данные в Azure.</span><span class="sxs-lookup"><span data-stu-id="287d3-161">Event Hubs Capture is hello easiest way tooget data into Azure.</span></span> <span data-ttu-id="287d3-162">С помощью знакомых средств и платформ (Azure Data Lake, фабрики данных Azure и Azure HDInsight) можно выполнять необходимую пакетную обработку и другие операции анализа в любом масштабе.</span><span class="sxs-lookup"><span data-stu-id="287d3-162">Using Azure Data Lake, Azure Data Factory, and Azure HDInsight, you can perform batch processing and other analytics using familiar tools and platforms of your choosing, at any scale you need.</span></span>

<span data-ttu-id="287d3-163">На сайте ссылкам hello, изучите более подробную концентраторов событий:</span><span class="sxs-lookup"><span data-stu-id="287d3-163">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="287d3-164">Отправка событий в концентраторы событий Azure с помощью платформы .NET Framework</span><span class="sxs-lookup"><span data-stu-id="287d3-164">Get started sending and receiving events</span></span>](event-hubs-dotnet-framework-getstarted-send.md)
* <span data-ttu-id="287d3-165">Полный [пример приложения, использующего концентраторы событий][sample application that uses Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="287d3-165">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs]</span></span>
* <span data-ttu-id="287d3-166">[Обзор концентраторов событий Azure][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="287d3-166">[Event Hubs overview][Event Hubs overview]</span></span>

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
