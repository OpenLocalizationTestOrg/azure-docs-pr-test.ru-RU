---
title: "aaaOverview и сравнение Azure на требование кодировщики мультимедиа | Документы Microsoft"
description: "В этой статье приводится обзор и сравнение кодировщиков мультимедиа Azure по запросу."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 24a3e0a16162b1bebfcde290b6baf2dd8dbfff17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a><span data-ttu-id="60ed0-103">Обзор и сравнение кодировщиков мультимедиа Azure по запросу</span><span class="sxs-lookup"><span data-stu-id="60ed0-103">Overview and comparison of Azure on demand media encoders</span></span>
## <a name="encoding-overview"></a><span data-ttu-id="60ed0-104">Общие сведения о Службе кодирования</span><span class="sxs-lookup"><span data-stu-id="60ed0-104">Encoding overview</span></span>
<span data-ttu-id="60ed0-105">Службы мультимедиа Azure предоставляют несколько параметров для кодирования hello носителя в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="60ed0-105">Azure Media Services provides multiple options for hello encoding of media in hello cloud.</span></span>

<span data-ttu-id="60ed0-106">При запуске с помощью служб мультимедиа, это важно toounderstand hello разницу между кодеками и форматами файлов.</span><span class="sxs-lookup"><span data-stu-id="60ed0-106">When starting out with Media Services, it is important toounderstand hello difference between codecs and file formats.</span></span>
<span data-ttu-id="60ed0-107">Кодеки — hello программное обеспечение, которое реализует hello алгоритмы сжатия и распаковки, тогда как форматы файлов являются контейнерами, содержащими hello сжатия видео.</span><span class="sxs-lookup"><span data-stu-id="60ed0-107">Codecs are hello software that implements hello compression/decompression algorithms whereas file formats are containers that hold hello compressed video.</span></span>

<span data-ttu-id="60ed0-108">Служба Media Services предоставляет динамической упаковки, позволяющий toodeliver с адаптивным битрейтом MP4 или Smooth Streaming кодировке содержимого в потоковом форматы, поддерживаемые службами мультимедиа (MPEG DASH, HLS, Smooth Streaming) без необходимости toore-package в такие Потоковая передача форматы.</span><span class="sxs-lookup"><span data-stu-id="60ed0-108">Media Services provides dynamic packaging which allows you toodeliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having toore-package into these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="60ed0-109">При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния.</span><span class="sxs-lookup"><span data-stu-id="60ed0-109">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="60ed0-110">Потоковая передача вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования toostart hello конечной точки потоковой передачи, из которого нужно имеет содержимое toostream toobe в hello **под управлением** состояния.</span><span class="sxs-lookup"><span data-stu-id="60ed0-110">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> <span data-ttu-id="60ed0-111">преимущества tootake [динамической упаковки](media-services-dynamic-packaging-overview.md), требуется toodo hello следующее:</span><span class="sxs-lookup"><span data-stu-id="60ed0-111">tootake advantage of [dynamic packaging](media-services-dynamic-packaging-overview.md), you need toodo hello following:</span></span>
>
><span data-ttu-id="60ed0-112">Кроме того кодирование файла исходного кода в набор файлов MP4 с адаптивной скоростью или файлы Smooth Streaming с адаптивной скоростью (hello кодирования действия приведены далее в этом учебнике).</span><span class="sxs-lookup"><span data-stu-id="60ed0-112">Also, encode your source file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files (hello encoding steps are demonstrated later in this tutorial).</span></span>

<span data-ttu-id="60ed0-113">Службы мультимедиа поддерживают следующие hello по запросу кодировщиков, описанных в этой статье:</span><span class="sxs-lookup"><span data-stu-id="60ed0-113">Media Services supports hello following on demand encoders that are described in this article:</span></span>

* [<span data-ttu-id="60ed0-114">Стандартный кодировщик служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="60ed0-114">Media Encoder Standard</span></span>](media-services-encode-asset.md#media-encoder-standard)
* [<span data-ttu-id="60ed0-115">Рабочий процесс Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="60ed0-115">Media Encoder Premium Workflow</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

<span data-ttu-id="60ed0-116">В этой статье предоставляет краткий обзор по запросу мультимедиа кодировщиков и предоставляет tooarticles ссылки, которая позволяет получить более подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="60ed0-116">This article gives a brief overview of on demand media encoders and provides links tooarticles that give more detailed information.</span></span> <span data-ttu-id="60ed0-117">Hello раздел также содержит сравнения кодировщиков hello.</span><span class="sxs-lookup"><span data-stu-id="60ed0-117">hello topic also provides comparison of hello encoders.</span></span>

>[!NOTE]
><span data-ttu-id="60ed0-118">По умолчанию каждая учетная запись служб мультимедиа может выполнять одну активную задачу кодирования в текущий момент.</span><span class="sxs-lookup"><span data-stu-id="60ed0-118">By default each Media Services account can have one active encoding task at a time.</span></span> <span data-ttu-id="60ed0-119">Можно зарезервировать единицы кодирования, которые позволят вам toohave несколько задачи кодирования параллельно; одна для зарезервированную единицу кодирования приобретения.</span><span class="sxs-lookup"><span data-stu-id="60ed0-119">You can reserve encoding units that allow you toohave multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span></span> <span data-ttu-id="60ed0-120">Дополнительные сведения см. в статье [Обзор масштабирования обработка мультимедиа](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="60ed0-120">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span></span>

## <a name="media-encoder-standard"></a><span data-ttu-id="60ed0-121">Стандартный кодировщик служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="60ed0-121">Media Encoder Standard</span></span>
### <a name="how-toouse"></a><span data-ttu-id="60ed0-122">Как toouse</span><span class="sxs-lookup"><span data-stu-id="60ed0-122">How toouse</span></span>
[<span data-ttu-id="60ed0-123">Как tooencode стандарту кодировщика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="60ed0-123">How tooencode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a><span data-ttu-id="60ed0-124">Форматы</span><span class="sxs-lookup"><span data-stu-id="60ed0-124">Formats</span></span>
[<span data-ttu-id="60ed0-125">Форматы и кодеки</span><span class="sxs-lookup"><span data-stu-id="60ed0-125">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a><span data-ttu-id="60ed0-126">Предустановки</span><span class="sxs-lookup"><span data-stu-id="60ed0-126">Presets</span></span>
<span data-ttu-id="60ed0-127">Стандартный кодировщик мультимедиа настраивается с помощью одного из описанных предустановки кодировщика hello [здесь](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="60ed0-127">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="60ed0-128">Входные и выходные метаданные</span><span class="sxs-lookup"><span data-stu-id="60ed0-128">Input and output metadata</span></span>
<span data-ttu-id="60ed0-129">Hello входных метаданных кодировщики описан [здесь](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="60ed0-129">hello encoders input metadata is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="60ed0-130">Hello кодировщики выходные метаданные описан [здесь](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="60ed0-130">hello encoders output metadata is described [here](media-services-output-metadata-schema.md).</span></span>

### <a name="generate-thumbnails"></a><span data-ttu-id="60ed0-131">Создание эскизов</span><span class="sxs-lookup"><span data-stu-id="60ed0-131">Generate thumbnails</span></span>
<span data-ttu-id="60ed0-132">Сведения см. в разделе [как эскизы toogenerate, с помощью Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span><span class="sxs-lookup"><span data-stu-id="60ed0-132">For information, see [How toogenerate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span></span>

### <a name="trim-videos-clipping"></a><span data-ttu-id="60ed0-133">Усечение видео (обрезка)</span><span class="sxs-lookup"><span data-stu-id="60ed0-133">Trim videos (clipping)</span></span>
<span data-ttu-id="60ed0-134">Сведения см. в разделе [как tootrim видео, с помощью Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span><span class="sxs-lookup"><span data-stu-id="60ed0-134">For information, see [How tootrim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span></span>

### <a name="create-overlays"></a><span data-ttu-id="60ed0-135">Создание наложений</span><span class="sxs-lookup"><span data-stu-id="60ed0-135">Create overlays</span></span>
<span data-ttu-id="60ed0-136">Сведения см. в разделе [как toocreate слои с помощью Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="60ed0-136">For information, see [How toocreate overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

### <a name="see-also"></a><span data-ttu-id="60ed0-137">См. также</span><span class="sxs-lookup"><span data-stu-id="60ed0-137">See also</span></span>
[<span data-ttu-id="60ed0-138">Блог Hello служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="60ed0-138">hello Media Services blog</span></span>](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a><span data-ttu-id="60ed0-139">Расширенный рабочий процесс кодировщика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="60ed0-139">Media Encoder Premium Workflow</span></span>
### <a name="overview"></a><span data-ttu-id="60ed0-140">Обзор</span><span class="sxs-lookup"><span data-stu-id="60ed0-140">Overview</span></span>
[<span data-ttu-id="60ed0-141">Знакомство со Службой кодирования категории "Премиум" в службах мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="60ed0-141">Introducing Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-toouse"></a><span data-ttu-id="60ed0-142">Как toouse</span><span class="sxs-lookup"><span data-stu-id="60ed0-142">How toouse</span></span>
<span data-ttu-id="60ed0-143">Рабочий процесс Premium кодировщика мультимедиа настраивается с помощью сложных рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="60ed0-143">Media Encoder Premium Workflow is configured using complex workflows.</span></span> <span data-ttu-id="60ed0-144">Файлы рабочего процесса может быть создан и обновлен с использованием hello [конструктора рабочих процессов](media-services-workflow-designer.md) средства.</span><span class="sxs-lookup"><span data-stu-id="60ed0-144">Workflow files could be created and updated using hello [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

[<span data-ttu-id="60ed0-145">Как tooUse расширенной кодировки в службах мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="60ed0-145">How tooUse Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a><span data-ttu-id="60ed0-146">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="60ed0-146">Known issues</span></span>
<span data-ttu-id="60ed0-147">Если входной видео не содержит титров, hello выходной ресурс по-прежнему будет содержать пустой файл TTML.</span><span class="sxs-lookup"><span data-stu-id="60ed0-147">If your input video does not contain closed captioning, hello output Asset will still contain an empty TTML file.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="60ed0-148">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="60ed0-148">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="60ed0-149">Отзывы</span><span class="sxs-lookup"><span data-stu-id="60ed0-149">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="60ed0-150">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="60ed0-150">Related articles</span></span>
* [<span data-ttu-id="60ed0-151">Выполняйте расширенные задачи кодирования путем настройки предустановок стандартного кодировщика служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="60ed0-151">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="60ed0-152">Квоты и ограничения</span><span class="sxs-lookup"><span data-stu-id="60ed0-152">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
