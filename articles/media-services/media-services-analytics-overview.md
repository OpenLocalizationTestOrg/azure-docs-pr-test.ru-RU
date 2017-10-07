---
title: "aaaMedia аналитика на платформе служб мультимедиа hello | Документы Microsoft"
description: "Обзор общедоступной предварительной версии служб медиа-аналитики — коллекции голосовых служб и служб компьютерного зрения для обеспечения соответствия нормам, безопасности и предоставления глобального доступа на корпоративном уровне."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c56e3781-8510-4f7f-b5ff-a218c1bb6f4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2017
ms.author: milanga;juliako;johndeu
ms.openlocfilehash: 7545f0532d7618164ebe65e2f4232c5f63453cfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="media-analytics-on-hello-media-services-platform"></a><span data-ttu-id="39f6a-103">Медиа-аналитика на платформе служб мультимедиа hello</span><span class="sxs-lookup"><span data-stu-id="39f6a-103">Media Analytics on hello Media Services platform</span></span>
## <a name="overview"></a><span data-ttu-id="39f6a-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="39f6a-104">Overview</span></span>
<span data-ttu-id="39f6a-105">Другие организации видео как hello предпочтительный средний tootrain своим сотрудникам, используется привлекать клиентами и документ бизнес-функции.</span><span class="sxs-lookup"><span data-stu-id="39f6a-105">More organizations are using video as hello preferred medium tootrain their employees, engage their customers, and document business functions.</span></span> <span data-ttu-id="39f6a-106">Облачные вычисления предоставляет toostore способом доступ к этим файлам мультимедиа большого объема и потока.</span><span class="sxs-lookup"><span data-stu-id="39f6a-106">Cloud computing provides a way toostore, stream, and access these large media files.</span></span> <span data-ttu-id="39f6a-107">Но по мере роста компании библиотеки содержимого, видео, он должен столь же эффективным средством извлечения аналитики из содержимого hello.</span><span class="sxs-lookup"><span data-stu-id="39f6a-107">But as a company's library of video content grows, it needs an equally effective means of extracting insights from hello content.</span></span> 

<span data-ttu-id="39f6a-108">tooaddress этой растущей потребности служб мультимедиа Azure предлагает медиа-аналитика Azure.</span><span class="sxs-lookup"><span data-stu-id="39f6a-108">tooaddress this growing need, Azure Media Services offers Azure Media Analytics.</span></span> <span data-ttu-id="39f6a-109">Медиа-аналитика — это совокупность компоненты речи и концепции, упрощающее для принятия решений tooderive предприятия и организации их видеофайлов.</span><span class="sxs-lookup"><span data-stu-id="39f6a-109">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="39f6a-110">Сборка с использованием hello основных компонентов платформы служб мультимедиа, медиа-аналитика может обрабатывать мультимедиа в любом масштабе на один день.</span><span class="sxs-lookup"><span data-stu-id="39f6a-110">Built by using hello core Media Services platform components, Media Analytics can handle media processing at scale on day one.</span></span>

<span data-ttu-id="39f6a-111">С помощью медиа-аналитики разработчики могут быстро внедрить расширенные функциональные возможности видео в приложения.</span><span class="sxs-lookup"><span data-stu-id="39f6a-111">With Media Analytics, developers can quickly bring advanced video functionality into applications.</span></span> <span data-ttu-id="39f6a-112">Он предоставляет корпоративных средах полнофункциональных hello, безопасности и требования глобальный доступ, необходимые для крупных организаций.</span><span class="sxs-lookup"><span data-stu-id="39f6a-112">It provides enterprise environments with hello full scale, compliance, security, and global reach required by large organizations.</span></span>

<span data-ttu-id="39f6a-113">Hello следующей схеме показан медиа-аналитика и другие основные части платформы служб мультимедиа hello.</span><span class="sxs-lookup"><span data-stu-id="39f6a-113">hello following diagram shows Media Analytics and other major parts of hello Media Services platform.</span></span> 

![Рабочий процесс для видео по запросу](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

<span data-ttu-id="39f6a-115">Обработчики мультимедийных данных служб медиа-аналитики создают файлы в формате MP4 или JSON.</span><span class="sxs-lookup"><span data-stu-id="39f6a-115">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="39f6a-116">Если обработчик мультимедиа создает MP4-файл, можно загрузить файл hello постепенно.</span><span class="sxs-lookup"><span data-stu-id="39f6a-116">If a media processor produces an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="39f6a-117">Если обработчик мультимедиа создает JSON-файл, можно загрузить файл hello из хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="39f6a-117">If a media processor produces a JSON file, you can download hello file from Azure Blob storage.</span></span> 

## <a name="media-analytics-services"></a><span data-ttu-id="39f6a-118">Службы медиа-аналитики</span><span class="sxs-lookup"><span data-stu-id="39f6a-118">Media Analytics services</span></span>

### <a name="indexer"></a><span data-ttu-id="39f6a-119">Индексатор</span><span class="sxs-lookup"><span data-stu-id="39f6a-119">Indexer</span></span>
<span data-ttu-id="39f6a-120">Индексатор мультимедийных данных Azure позволяет сделать содержимое доступным для поиска, а также создавать дорожки скрытых субтитров.</span><span class="sxs-lookup"><span data-stu-id="39f6a-120">With Azure Media Indexer, you can make content searchable and generate closed-captioning tracks.</span></span> <span data-ttu-id="39f6a-121">Сравниваемые toohello предыдущей версии, предварительной версии 2 индексатора мультимедиа Azure имеет быстрее индексирования и широкие языковой поддержки.</span><span class="sxs-lookup"><span data-stu-id="39f6a-121">Compared toohello previous version, Azure Media Indexer 2 Preview has faster indexing and broader language support.</span></span> <span data-ttu-id="39f6a-122">В число поддерживаемых языков входят английский, испанский, французский, немецкий, итальянский, китайский, португальский и арабский.</span><span class="sxs-lookup"><span data-stu-id="39f6a-122">Supported languages include English, Spanish, French, German, Italian, Chinese, Portuguese, and Arabic.</span></span> <span data-ttu-id="39f6a-123">Дополнительные сведения и примеры приведены в статье [Индексирование файлов мультимедиа с помощью индексатора мультимедийных данных Azure 2 (предварительная версия)](media-services-process-content-with-indexer2.md).</span><span class="sxs-lookup"><span data-stu-id="39f6a-123">For detailed information and examples, see [Process videos with Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span></span>
### <a name="hyperlapse"></a><span data-ttu-id="39f6a-124">Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="39f6a-124">Hyperlapse</span></span>
<span data-ttu-id="39f6a-125">Microsoft Hyperlapse объединяет стабилизации видео и промежутка времени возможность toocreate быстрый, к использованию видео с длинной форме контента.</span><span class="sxs-lookup"><span data-stu-id="39f6a-125">Microsoft Hyperlapse combines video stabilization and time-lapse capability toocreate quick, consumable videos from your long-form content.</span></span> <span data-ttu-id="39f6a-126">Помимо создания видео промежуток времени, можно использовать Hyperlapse toocreate стабильный видео из shaky видео записывались через мобильные телефоны и видеокамер.</span><span class="sxs-lookup"><span data-stu-id="39f6a-126">Besides creating time-lapse video, you can use Hyperlapse toocreate stable videos from shaky videos captured via cell phones and camcorders.</span></span> <span data-ttu-id="39f6a-127">Дополнительные сведения и примеры приведены в статье [Файлы мультимедиа Hyperlapse с Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span><span class="sxs-lookup"><span data-stu-id="39f6a-127">For detailed information and examples, see [Hyperlapse media files with Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span></span>
### <a name="motion-detector"></a><span data-ttu-id="39f6a-128">Детектор движения</span><span class="sxs-lookup"><span data-stu-id="39f6a-128">Motion Detector</span></span>
<span data-ttu-id="39f6a-129">Детектор движения toodetect перемещения можно использовать в видео с стационарным фон.</span><span class="sxs-lookup"><span data-stu-id="39f6a-129">You can use Motion Detector toodetect motion in a video with stationary backgrounds.</span></span> <span data-ttu-id="39f6a-130">В результате возможно toocheck для ложных положительных результатов на события перемещения, обнаруживаемый камеры системы наблюдения.</span><span class="sxs-lookup"><span data-stu-id="39f6a-130">This makes it possible toocheck for false positives on motion events detected by surveillance cameras.</span></span> <span data-ttu-id="39f6a-131">Дополнительные сведения и примеры приведены в статье [Обнаружение движения с помощью медиа-аналитики Azure](media-services-motion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="39f6a-131">For detailed information and examples, see [Motion detection for Azure Media Analytics](media-services-motion-detection.md).</span></span>
### <a name="face-detector"></a><span data-ttu-id="39f6a-132">Обнаружение лиц</span><span class="sxs-lookup"><span data-stu-id="39f6a-132">Face Detector</span></span>
<span data-ttu-id="39f6a-133">Face Detector позволяет обнаруживать лица людей и определять их эмоции, включая радость, грусть и удивление.</span><span class="sxs-lookup"><span data-stu-id="39f6a-133">By using Face Detector, you can detect people’s faces and their emotions, including happiness, sadness, and surprise.</span></span> <span data-ttu-id="39f6a-134">Эту службу целесообразно использовать в ряде описанных ниже областей, включая объединение и анализ реакции людей, принимающих участие в мероприятии.</span><span class="sxs-lookup"><span data-stu-id="39f6a-134">This has several useful industry applications, described later, including aggregating and analyzing reactions of people attending an event.</span></span> <span data-ttu-id="39f6a-135">Дополнительные сведения и примеры приведены в статье [Обнаружение лиц и определение эмоций с помощью медиа-аналитики Azure](media-services-face-and-emotion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="39f6a-135">For detailed information and examples, see [Face and emotion detection for Azure Media Analytics](media-services-face-and-emotion-detection.md).</span></span>
### <a name="video-summarization"></a><span data-ttu-id="39f6a-136">Сводные видео</span><span class="sxs-lookup"><span data-stu-id="39f6a-136">Video summarization</span></span>
<span data-ttu-id="39f6a-137">Видео формирования сводных данных поможет вам создать сводные видеофайлов большого размера, выбрав интересные фрагменты автоматически из источника видео hello.</span><span class="sxs-lookup"><span data-stu-id="39f6a-137">Video summarization can help you create summaries of long videos by automatically selecting interesting snippets from hello source video.</span></span> <span data-ttu-id="39f6a-138">Эта возможность полезна при необходимости tooprovide краткий обзор какие tooexpect в длинного видео.</span><span class="sxs-lookup"><span data-stu-id="39f6a-138">This ability is useful when you want tooprovide a quick overview of what tooexpect in a long video.</span></span> <span data-ttu-id="39f6a-139">Подробные сведения и примеры см. в разделе [видео сводку использования Azure Media видео эскизы toocreate](media-services-video-summarization.md).</span><span class="sxs-lookup"><span data-stu-id="39f6a-139">For detailed information and examples, see [Use Azure Media Video Thumbnails toocreate video summarization](media-services-video-summarization.md).</span></span>
### <a name="optical-character-recognition"></a><span data-ttu-id="39f6a-140">Оптическое распознавание символов</span><span class="sxs-lookup"><span data-stu-id="39f6a-140">Optical character recognition</span></span>
<span data-ttu-id="39f6a-141">Функция OCR (оптическое распознавание символов) служб медиа-аналитики Azure позволяет преобразовывать текстовое содержимое в видеофайлах в редактируемый и поддерживающий поиск цифровой текст.</span><span class="sxs-lookup"><span data-stu-id="39f6a-141">With Azure Media OCR (optical character recognition), you can convert text content in video files into editable, searchable digital text.</span></span> <span data-ttu-id="39f6a-142">Затем можно автоматизировать извлечение hello значимых метаданных из hello видеосигнала мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="39f6a-142">You can then automate hello extraction of meaningful metadata from hello video signal of your media.</span></span>
### <a name="scalable-face-redaction"></a><span data-ttu-id="39f6a-143">Масштабируемое скрытие лиц</span><span class="sxs-lookup"><span data-stu-id="39f6a-143">Scalable face redaction</span></span>
<span data-ttu-id="39f6a-144">Azure Media Redactor является обработчиком мультимедиа медиа-аналитика, предлагает исправления масштабируемой лицевой стороны в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="39f6a-144">Azure Media Redactor is a Media Analytics media processor that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="39f6a-145">С помощью исправления лиц, вы можете изменить лиц на видео tooblur выбранных сотрудников.</span><span class="sxs-lookup"><span data-stu-id="39f6a-145">By using face redaction, you can modify your video tooblur faces of selected individuals.</span></span> <span data-ttu-id="39f6a-146">Может потребоваться исправления toouse hello лицевой стороны службы в новостей носителя или при используется общественной безопасности.</span><span class="sxs-lookup"><span data-stu-id="39f6a-146">You might want toouse hello face redaction service in news media or when public safety is involved.</span></span> <span data-ttu-id="39f6a-147">Через несколько минут, содержащий несколько начертаний материал может занять tooredact часы вручную, но с этой службой исправления лицевой стороны занимает всего несколько простых шагов.</span><span class="sxs-lookup"><span data-stu-id="39f6a-147">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service, face redaction takes just a few simple steps.</span></span> <span data-ttu-id="39f6a-148">Дополнительные сведения см. в разделе hello [исправить грани с медиа-аналитика Azure](media-services-face-redaction.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="39f6a-148">For more information, see hello [Redact faces with Azure Media Analytics](media-services-face-redaction.md) article.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="39f6a-149">Распространенные сценарии</span><span class="sxs-lookup"><span data-stu-id="39f6a-149">Common scenarios</span></span>
<span data-ttu-id="39f6a-150">Службы медиа-аналитики помогают организациям и предприятиям получать новую ценную информацию из видео и более эффективно управлять большими объемами видеосодержимого.</span><span class="sxs-lookup"><span data-stu-id="39f6a-150">Media Analytics can help organizations and enterprises glean new insights from video and more effectively manage large volumes of video content.</span></span> <span data-ttu-id="39f6a-151">Ниже приведено несколько сценариев.</span><span class="sxs-lookup"><span data-stu-id="39f6a-151">Here are several scenarios:</span></span>

* <span data-ttu-id="39f6a-152">**Центры обработки вызовов**.</span><span class="sxs-lookup"><span data-stu-id="39f6a-152">**Call centers**.</span></span> <span data-ttu-id="39f6a-153">Даже с появлением hello социальных сетей центр обработки вызовов клиента по-прежнему упрощения большая часть операций обслуживания клиентов.</span><span class="sxs-lookup"><span data-stu-id="39f6a-153">Even with hello advent of social media, customer call centers still facilitate a large percentage of customer-service transactions.</span></span> <span data-ttu-id="39f6a-154">В этом звуковых данных — большой объем сведения о клиенте, может быть проанализирован tooachieve выше удовлетворенности.</span><span class="sxs-lookup"><span data-stu-id="39f6a-154">Encoded in this audio data is a large amount of customer information that can be analyzed tooachieve higher customer satisfaction.</span></span> <span data-ttu-id="39f6a-155">С помощью индексатора мультимедийных данных организации могут извлекать текст и создавать индексы поиска и панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="39f6a-155">By using Media Indexer, organizations can extract text and build search indexes and dashboards.</span></span> <span data-ttu-id="39f6a-156">Затем они могут извлекать аналитику по распространенным жалобам, источникам жалоб и другим связанным данным.</span><span class="sxs-lookup"><span data-stu-id="39f6a-156">Then they can extract intelligence around common complaints, sources of complaints, and other relevant data.</span></span>
* <span data-ttu-id="39f6a-157">**Модерация создаваемого пользователями содержимого**.</span><span class="sxs-lookup"><span data-stu-id="39f6a-157">**User-generated content moderation**.</span></span> <span data-ttu-id="39f6a-158">Из отделов toopolice торговцам мультимедиа новости во многих организациях имеет публичный веб-порталы, принимающие носителя, созданного пользователем, например видео и изображения.</span><span class="sxs-lookup"><span data-stu-id="39f6a-158">From news media outlets toopolice departments, many organizations have public-facing portals that accept user-generated media such as videos and images.</span></span> <span data-ttu-id="39f6a-159">из-за события toounexpected можно скачки Hello объемами содержимого.</span><span class="sxs-lookup"><span data-stu-id="39f6a-159">hello volume of content can spike due toounexpected events.</span></span> <span data-ttu-id="39f6a-160">В этих сценариях это сложно tooconduct действующие вручную проверки содержимого для целесообразность.</span><span class="sxs-lookup"><span data-stu-id="39f6a-160">In these scenarios, it is difficult tooconduct effective manual reviews of content for appropriateness.</span></span> <span data-ttu-id="39f6a-161">Клиенты могут использовать hello toofocus службы умеренность содержимое на содержимое, которое подходит.</span><span class="sxs-lookup"><span data-stu-id="39f6a-161">Customers can rely on hello content-moderation service toofocus on content that is appropriate.</span></span>
* <span data-ttu-id="39f6a-162">**Видеонаблюдение**.</span><span class="sxs-lookup"><span data-stu-id="39f6a-162">**Surveillance**.</span></span> <span data-ttu-id="39f6a-163">Рост использования камер IP hello появилась растущих инвентаризации видео наблюдения.</span><span class="sxs-lookup"><span data-stu-id="39f6a-163">With hello growth in use of IP cameras comes a growing inventory of surveillance video.</span></span> <span data-ttu-id="39f6a-164">Просмотр видео наблюдения вручную возникает ошибка времени toohuman служб с интенсивными вычислениями и ошибкам.</span><span class="sxs-lookup"><span data-stu-id="39f6a-164">Manually reviewing surveillance video is time intensive and prone toohuman error.</span></span> <span data-ttu-id="39f6a-165">Медиа-аналитика предоставляет службы, такие как обнаружение движения, обнаружения лицевой стороны и Hyperlapse toomake hello процесса проверки, управления и создания производных проще.</span><span class="sxs-lookup"><span data-stu-id="39f6a-165">Media Analytics provides services such as motion detection, face detection, and Hyperlapse toomake hello process of reviewing, managing, and creating derivatives easier.</span></span>

## <a name="media-analytics-media-processors"></a><span data-ttu-id="39f6a-166">Обработчики мультимедиа медиа-аналитики</span><span class="sxs-lookup"><span data-stu-id="39f6a-166">Media Analytics media processors</span></span>
<span data-ttu-id="39f6a-167">В этом разделе обработчиков мультимедиа медиа-аналитика списки hello и показывает, как toouse .NET или REST tooget объект мультимедиа процессора (MP).</span><span class="sxs-lookup"><span data-stu-id="39f6a-167">This section lists hello Media Analytics media processors and shows how toouse .NET or REST tooget a media processor (MP) object.</span></span>

### <a name="mp-names"></a><span data-ttu-id="39f6a-168">Названия обработчиков мультимедиа</span><span class="sxs-lookup"><span data-stu-id="39f6a-168">MP names</span></span>
* <span data-ttu-id="39f6a-169">Azure Media Indexer 2 (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="39f6a-169">Azure Media Indexer 2 Preview</span></span>
* <span data-ttu-id="39f6a-170">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="39f6a-170">Azure Media Indexer</span></span>
* <span data-ttu-id="39f6a-171">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="39f6a-171">Azure Media Hyperlapse</span></span>
* <span data-ttu-id="39f6a-172">Azure Media Face Detector</span><span class="sxs-lookup"><span data-stu-id="39f6a-172">Azure Media Face Detector</span></span>
* <span data-ttu-id="39f6a-173">Azure Media Motion Detector</span><span class="sxs-lookup"><span data-stu-id="39f6a-173">Azure Media Motion Detector</span></span>
* <span data-ttu-id="39f6a-174">Azure Media Video Thumbnails</span><span class="sxs-lookup"><span data-stu-id="39f6a-174">Azure Media Video Thumbnails</span></span>
* <span data-ttu-id="39f6a-175">Azure Media OCR</span><span class="sxs-lookup"><span data-stu-id="39f6a-175">Azure Media OCR</span></span>

### <a name="net"></a><span data-ttu-id="39f6a-176">.NET</span><span class="sxs-lookup"><span data-stu-id="39f6a-176">.NET</span></span>
<span data-ttu-id="39f6a-177">Следующая функция принимает один из hello Hello указан MP имен и возвращает объект пакета Управления.</span><span class="sxs-lookup"><span data-stu-id="39f6a-177">hello following function takes one of hello specified MP names and returns an MP object.</span></span>

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
            .Where(p => p.Name == mediaProcessorName)
            .ToList()
            .OrderBy(p => new Version(p.Version))
            .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }


### <a name="rest"></a><span data-ttu-id="39f6a-178">REST</span><span class="sxs-lookup"><span data-stu-id="39f6a-178">REST</span></span>
<span data-ttu-id="39f6a-179">Запрос:</span><span class="sxs-lookup"><span data-stu-id="39f6a-179">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

<span data-ttu-id="39f6a-180">Ответ:</span><span class="sxs-lookup"><span data-stu-id="39f6a-180">Response:</span></span>

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:074c3899-d9fb-448f-9ae1-4ebcbe633056",
             "Description":"Azure Media OCR",
             "Name":"Azure Media OCR",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

## <a name="demos"></a><span data-ttu-id="39f6a-181">Демонстрационные материалы</span><span class="sxs-lookup"><span data-stu-id="39f6a-181">Demos</span></span>
<span data-ttu-id="39f6a-182">Просмотрите [ролики о медиа-аналитике Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span><span class="sxs-lookup"><span data-stu-id="39f6a-182">See [Azure Media Analytics demos](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="39f6a-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="39f6a-183">Next steps</span></span>
<span data-ttu-id="39f6a-184">Просмотрите схемы обучения работе со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="39f6a-184">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="39f6a-185">Отзывы</span><span class="sxs-lookup"><span data-stu-id="39f6a-185">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="39f6a-186">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="39f6a-186">Related articles</span></span>
<span data-ttu-id="39f6a-187">Ознакомьтесь с разделом [Общие сведения об аналитике служб мультимедиа](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span><span class="sxs-lookup"><span data-stu-id="39f6a-187">See [Media Services Analytics announcement](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span></span>

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
