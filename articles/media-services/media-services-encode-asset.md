---
title: "Обзор и сравнение кодировщиков мультимедиа Azure по запросу | Документация Майкрософт"
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
ms.openlocfilehash: 538a6ab60168735c2626a93cdeedd8d4999a6efc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a><span data-ttu-id="ee724-103">Обзор и сравнение кодировщиков мультимедиа Azure по запросу</span><span class="sxs-lookup"><span data-stu-id="ee724-103">Overview and comparison of Azure on demand media encoders</span></span>
## <a name="encoding-overview"></a><span data-ttu-id="ee724-104">Общие сведения о Службе кодирования</span><span class="sxs-lookup"><span data-stu-id="ee724-104">Encoding overview</span></span>
<span data-ttu-id="ee724-105">Службы мультимедиа Azure предоставляют несколько вариантов для кодирования мультимедиа в облаке.</span><span class="sxs-lookup"><span data-stu-id="ee724-105">Azure Media Services provides multiple options for the encoding of media in the cloud.</span></span>

<span data-ttu-id="ee724-106">При начале работы со службами мультимедиа важно понимать разницу между кодеками и форматами файлов.</span><span class="sxs-lookup"><span data-stu-id="ee724-106">When starting out with Media Services, it is important to understand the difference between codecs and file formats.</span></span>
<span data-ttu-id="ee724-107">Кодеки — это программное обеспечение, которое реализует алгоритмы сжатия и распаковки, тогда как форматы файлов являются контейнерами, в которых хранится сжатое видео.</span><span class="sxs-lookup"><span data-stu-id="ee724-107">Codecs are the software that implements the compression/decompression algorithms whereas file formats are containers that hold the compressed video.</span></span>

<span data-ttu-id="ee724-108">Службы мультимедиа обеспечивают динамическую упаковку, которая позволяет доставлять закодированное содержимое MP4-файлов с переменной скоростью или Smooth Streaming в форматах потоковой передачи с поддержкой служб мультимедиа (MPEG-DASH, HLS, Smooth Streaming) без необходимости повторной упаковки в эти форматы потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="ee724-108">Media Services provides dynamic packaging which allows you to deliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having to re-package into these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="ee724-109">При создании учетной записи AMS в нее добавляется конечная точка потоковой передачи **по умолчанию** в состоянии **Остановлена**.</span><span class="sxs-lookup"><span data-stu-id="ee724-109">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="ee724-110">Чтобы начать потоковую передачу содержимого и воспользоваться динамической упаковкой и динамическим шифрованием, конечная точка потоковой передачи, из которой необходимо выполнять потоковую передачу содержимого, должна находиться в состоянии **Выполняется**.</span><span class="sxs-lookup"><span data-stu-id="ee724-110">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> <span data-ttu-id="ee724-111">Чтобы воспользоваться преимуществом [динамической упаковки](media-services-dynamic-packaging-overview.md), необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ee724-111">To take advantage of [dynamic packaging](media-services-dynamic-packaging-overview.md), you need to do the following:</span></span>
>
><span data-ttu-id="ee724-112">Кроме того, закодируйте исходный файл в набор MP4-файлов с переменной скоростью или в набор файлов Smooth Streaming (шаги кодирования показаны далее в этом руководстве).</span><span class="sxs-lookup"><span data-stu-id="ee724-112">Also, encode your source file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files (the encoding steps are demonstrated later in this tutorial).</span></span>

<span data-ttu-id="ee724-113">Службы мультимедиа поддерживают следующие кодировщики по запросу, описанные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="ee724-113">Media Services supports the following on demand encoders that are described in this article:</span></span>

* [<span data-ttu-id="ee724-114">Стандартный кодировщик служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="ee724-114">Media Encoder Standard</span></span>](media-services-encode-asset.md#media-encoder-standard)
* [<span data-ttu-id="ee724-115">Расширенный рабочий процесс кодировщика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="ee724-115">Media Encoder Premium Workflow</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

<span data-ttu-id="ee724-116">В этом разделе предоставлен краткий обзор кодировщиков мультимедиа по запросу, а также приведены ссылки на разделы с подробными сведениями.</span><span class="sxs-lookup"><span data-stu-id="ee724-116">This article gives a brief overview of on demand media encoders and provides links to articles that give more detailed information.</span></span> <span data-ttu-id="ee724-117">В этой статье также приводится сравнение кодировщиков.</span><span class="sxs-lookup"><span data-stu-id="ee724-117">The topic also provides comparison of the encoders.</span></span>

>[!NOTE]
><span data-ttu-id="ee724-118">По умолчанию каждая учетная запись служб мультимедиа может выполнять одну активную задачу кодирования в текущий момент.</span><span class="sxs-lookup"><span data-stu-id="ee724-118">By default each Media Services account can have one active encoding task at a time.</span></span> <span data-ttu-id="ee724-119">Можно зарезервировать единицы кодирования, которые позволят выполнять несколько задач кодирования одновременно, по одной для каждой приобретенной единицы.</span><span class="sxs-lookup"><span data-stu-id="ee724-119">You can reserve encoding units that allow you to have multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span></span> <span data-ttu-id="ee724-120">Дополнительные сведения см. в статье [Обзор масштабирования обработка мультимедиа](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ee724-120">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span></span>

## <a name="media-encoder-standard"></a><span data-ttu-id="ee724-121">Стандартный кодировщик служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="ee724-121">Media Encoder Standard</span></span>
### <a name="how-to-use"></a><span data-ttu-id="ee724-122">Использование</span><span class="sxs-lookup"><span data-stu-id="ee724-122">How to use</span></span>
[<span data-ttu-id="ee724-123">Кодирование с помощью стандартного кодировщика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="ee724-123">How to encode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a><span data-ttu-id="ee724-124">Форматы</span><span class="sxs-lookup"><span data-stu-id="ee724-124">Formats</span></span>
[<span data-ttu-id="ee724-125">Форматы и кодеки</span><span class="sxs-lookup"><span data-stu-id="ee724-125">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a><span data-ttu-id="ee724-126">Предустановки</span><span class="sxs-lookup"><span data-stu-id="ee724-126">Presets</span></span>
<span data-ttu-id="ee724-127">Стандартный кодировщик мультимедиа настраивается с помощью одной из предустановок кодировщика, описанных [здесь](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="ee724-127">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="ee724-128">Входные и выходные метаданные</span><span class="sxs-lookup"><span data-stu-id="ee724-128">Input and output metadata</span></span>
<span data-ttu-id="ee724-129">Входные метаданные кодировщиков описаны [здесь](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="ee724-129">The encoders input metadata is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="ee724-130">Выходные метаданные кодировщиков описаны [здесь](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="ee724-130">The encoders output metadata is described [here](media-services-output-metadata-schema.md).</span></span>

### <a name="generate-thumbnails"></a><span data-ttu-id="ee724-131">Создание эскизов</span><span class="sxs-lookup"><span data-stu-id="ee724-131">Generate thumbnails</span></span>
<span data-ttu-id="ee724-132">Дополнительные сведения см. в разделе о [создании эскизов с помощью стандартного кодировщика служб мультимедиа](media-services-advanced-encoding-with-mes.md#thumbnails).</span><span class="sxs-lookup"><span data-stu-id="ee724-132">For information, see [How to generate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span></span>

### <a name="trim-videos-clipping"></a><span data-ttu-id="ee724-133">Усечение видео (обрезка)</span><span class="sxs-lookup"><span data-stu-id="ee724-133">Trim videos (clipping)</span></span>
<span data-ttu-id="ee724-134">Дополнительные сведения см. в разделе об [обрезке видео с помощью стандартного кодировщика мультимедиа](media-services-advanced-encoding-with-mes.md#trim_video).</span><span class="sxs-lookup"><span data-stu-id="ee724-134">For information, see [How to trim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span></span>

### <a name="create-overlays"></a><span data-ttu-id="ee724-135">Создание наложений</span><span class="sxs-lookup"><span data-stu-id="ee724-135">Create overlays</span></span>
<span data-ttu-id="ee724-136">Дополнительные сведения см. в разделе о [создании наложения с помощью стандартного кодировщика мультимедиа](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="ee724-136">For information, see [How to create overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

### <a name="see-also"></a><span data-ttu-id="ee724-137">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="ee724-137">See also</span></span>
[<span data-ttu-id="ee724-138">Блог, посвященный службам мультимедиа</span><span class="sxs-lookup"><span data-stu-id="ee724-138">The Media Services blog</span></span>](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a><span data-ttu-id="ee724-139">Расширенный рабочий процесс кодировщика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="ee724-139">Media Encoder Premium Workflow</span></span>
### <a name="overview"></a><span data-ttu-id="ee724-140">Обзор</span><span class="sxs-lookup"><span data-stu-id="ee724-140">Overview</span></span>
[<span data-ttu-id="ee724-141">Знакомство со Службой кодирования категории "Премиум" в службах мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="ee724-141">Introducing Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-to-use"></a><span data-ttu-id="ee724-142">Использование</span><span class="sxs-lookup"><span data-stu-id="ee724-142">How to use</span></span>
<span data-ttu-id="ee724-143">Рабочий процесс Premium кодировщика мультимедиа настраивается с помощью сложных рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="ee724-143">Media Encoder Premium Workflow is configured using complex workflows.</span></span> <span data-ttu-id="ee724-144">Файлы рабочих процессов можно создавать и обновлять с помощью [конструктора рабочих процессов](media-services-workflow-designer.md) .</span><span class="sxs-lookup"><span data-stu-id="ee724-144">Workflow files could be created and updated using the [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

[<span data-ttu-id="ee724-145">Использование Службы кодирования категории "Премиум" в службах мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="ee724-145">How to Use Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a><span data-ttu-id="ee724-146">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="ee724-146">Known issues</span></span>
<span data-ttu-id="ee724-147">Если входящее видео не содержит скрытых субтитров, выходящий ресурс по-прежнему будет содержать пустой файл TTML.</span><span class="sxs-lookup"><span data-stu-id="ee724-147">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="ee724-148">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="ee724-148">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ee724-149">Отзывы</span><span class="sxs-lookup"><span data-stu-id="ee724-149">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="ee724-150">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="ee724-150">Related articles</span></span>
* [<span data-ttu-id="ee724-151">Выполняйте расширенные задачи кодирования путем настройки предустановок стандартного кодировщика служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="ee724-151">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="ee724-152">Квоты и ограничения</span><span class="sxs-lookup"><span data-stu-id="ee724-152">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
