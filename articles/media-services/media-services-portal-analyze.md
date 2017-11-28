---
title: "aaaAnalyze носителя с помощью hello портал Azure | Документы Microsoft"
description: "В этом разделе рассматриваются как tooprocess мультимедиа с помощью обработчиков мультимедиа медиа-аналитика (MP) с помощью hello портал Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a><span data-ttu-id="9458b-103">Анализ мультимедиа с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="9458b-103">Analyze your media using hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="9458b-104">toocomplete этого учебника необходима учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="9458b-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="9458b-105">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9458b-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

## <a name="overview"></a><span data-ttu-id="9458b-106">Обзор</span><span class="sxs-lookup"><span data-stu-id="9458b-106">Overview</span></span>
<span data-ttu-id="9458b-107">Azure Media Services Analytics — это коллекция речи и представление компонентов (на корпоративном уровне соответствия, безопасности и глобальный доступ), упрощают процесс принятия решений tooderive предприятия и организации их видеофайлов.</span><span class="sxs-lookup"><span data-stu-id="9458b-107">Azure Media Services Analytics is a collection of speech and vision components (at enterprise scale, compliance, security and global reach) that make it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="9458b-108">Подробные сведения об аналитике служб мультимедиа Azure см. в [этой статье](media-services-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9458b-108">For more detailed overview of Azure Media Services Analytics see [this](media-services-analytics-overview.md) topic.</span></span> 

<span data-ttu-id="9458b-109">В этом разделе рассматриваются как tooprocess мультимедиа с помощью обработчиков мультимедиа медиа-аналитика (MP) с помощью hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9458b-109">This topic discusses how tooprocess your media with Media Analytics media processors (MPs) using hello Azure portal.</span></span> <span data-ttu-id="9458b-110">Обработчики мультимедийных данных служб медиааналитики создают файлы в формате MP4 или JSON.</span><span class="sxs-lookup"><span data-stu-id="9458b-110">Media Analytics MPs produce MP4 files or JSON files.</span></span> <span data-ttu-id="9458b-111">Если обработчик мультимедиа созданы MP4-файл, можно загрузить файл hello постепенно.</span><span class="sxs-lookup"><span data-stu-id="9458b-111">If a media processor produced an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="9458b-112">Если обработчик мультимедиа созданы JSON-файл, можно загрузить файл hello из hello хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="9458b-112">If a media processor produced a JSON file, you can download hello file from hello Azure blob storage.</span></span> 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a><span data-ttu-id="9458b-113">Выберите средства, которые должны tooanalyze</span><span class="sxs-lookup"><span data-stu-id="9458b-113">Choose an asset that you want tooanalyze</span></span>
1. <span data-ttu-id="9458b-114">В hello [портал Azure](https://portal.azure.com/), выберите учетную запись служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="9458b-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="9458b-115">В hello **параметры** выберите **активы**.</span><span class="sxs-lookup"><span data-stu-id="9458b-115">In hello **Settings** window, select **Assets**.</span></span>  
   <span data-ttu-id="9458b-116">.</span><span class="sxs-lookup"><span data-stu-id="9458b-116">.</span></span>
    <span data-ttu-id="9458b-117">![Анализ видео](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span><span class="sxs-lookup"><span data-stu-id="9458b-117">![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span></span>
3. <span data-ttu-id="9458b-118">Выберите hello активов, которые будут tooanalyze и нажмите клавишу hello **анализ** кнопки.</span><span class="sxs-lookup"><span data-stu-id="9458b-118">Select hello asset that you would like tooanalyze and press hello **Analyze** button.</span></span>
   
    ![Анализ видео](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. <span data-ttu-id="9458b-120">В hello **процесса актив мультимедиа с медиа-аналитика** окно, выберите hello процессора.</span><span class="sxs-lookup"><span data-stu-id="9458b-120">In hello **Process media asset with  Media Analytics** window, select hello processor.</span></span> 
   
    <span data-ttu-id="9458b-121">Hello оставшейся части статьи hello объясняется, почему и как toouse каждого процессора.</span><span class="sxs-lookup"><span data-stu-id="9458b-121">hello rest of hello article explains why and how toouse each processor.</span></span> 
5. <span data-ttu-id="9458b-122">Нажмите клавишу **создать** toohello запуска задания.</span><span class="sxs-lookup"><span data-stu-id="9458b-122">Press **Create** toohello start a job.</span></span>

## <a name="azure-media-indexer"></a><span data-ttu-id="9458b-123">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="9458b-123">Azure Media Indexer</span></span>
<span data-ttu-id="9458b-124">Hello **индексатора мультимедиа Azure** обработчик мультимедиа позволяет toomake файлы и контент мультимедиа с возможностью поиска, а также создавать дорожек со скрытыми субтитрами.</span><span class="sxs-lookup"><span data-stu-id="9458b-124">hello **Azure Media Indexer** media processor enables you toomake media files and content searchable, as well as generate closed captioning tracks.</span></span> <span data-ttu-id="9458b-125">В этих разделах подробно описываются некоторые сведения о параметрах, которые можно указать для обработчика мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="9458b-125">This sections gives some details about options that you can specify for this MP.</span></span>

![Анализ видео](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a><span data-ttu-id="9458b-127">Язык</span><span class="sxs-lookup"><span data-stu-id="9458b-127">Language</span></span>
<span data-ttu-id="9458b-128">Здравствуйте, распознаваемые в файл мультимедиа hello toobe естественного языка.</span><span class="sxs-lookup"><span data-stu-id="9458b-128">hello natural language toobe recognized in hello multimedia file.</span></span> <span data-ttu-id="9458b-129">например английский или испанский.</span><span class="sxs-lookup"><span data-stu-id="9458b-129">For example, English or Spanish.</span></span> 

### <a name="captions"></a><span data-ttu-id="9458b-130">Субтитры</span><span class="sxs-lookup"><span data-stu-id="9458b-130">Captions</span></span>
<span data-ttu-id="9458b-131">Вы можете выбрать формат субтитров, который будет создаваться из контента.</span><span class="sxs-lookup"><span data-stu-id="9458b-131">You can choose a caption format that will be generated from your content.</span></span> <span data-ttu-id="9458b-132">Задание индексирования можно создать файлы титров hello следующие форматы:</span><span class="sxs-lookup"><span data-stu-id="9458b-132">An indexing job can generate closed caption files in hello following formats:</span></span>  

* <span data-ttu-id="9458b-133">**SAMI**</span><span class="sxs-lookup"><span data-stu-id="9458b-133">**SAMI**</span></span>
* <span data-ttu-id="9458b-134">**TTML**</span><span class="sxs-lookup"><span data-stu-id="9458b-134">**TTML**</span></span>
* <span data-ttu-id="9458b-135">**WebVTT**</span><span class="sxs-lookup"><span data-stu-id="9458b-135">**WebVTT**</span></span>

<span data-ttu-id="9458b-136">Закрытых субтитров (CC) файлов в этих форматах можно использовать toomake аудио и видео файлы доступны toopeople возможностями слуха.</span><span class="sxs-lookup"><span data-stu-id="9458b-136">Closed Caption (CC) files in these formats can be used toomake audio and video files accessible toopeople with hearing disability.</span></span>

### <a name="aib-file"></a><span data-ttu-id="9458b-137">Файл AIB</span><span class="sxs-lookup"><span data-stu-id="9458b-137">AIB file</span></span>
<span data-ttu-id="9458b-138">Выберите этот параметр, если вы бы как файл toogenerate hello аудио индекс большого двоичного объекта, для использования с hello пользовательский фильтр IFilter SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9458b-138">Select this option if you would like toogenerate hello Audio Index Blob file for use with hello custom SQL Server IFilter.</span></span> <span data-ttu-id="9458b-139">Дополнительную информацию см. в [этом](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) блоге.</span><span class="sxs-lookup"><span data-stu-id="9458b-139">For more information, see [this](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span></span>

### <a name="keywords"></a><span data-ttu-id="9458b-140">Ключевые слова</span><span class="sxs-lookup"><span data-stu-id="9458b-140">Keywords</span></span>
<span data-ttu-id="9458b-141">Выберите этот параметр, если вы хотите toogenerate файл XML ключевые слова.</span><span class="sxs-lookup"><span data-stu-id="9458b-141">Select this option if you would like toogenerate a keywords XML file.</span></span> <span data-ttu-id="9458b-142">Этот файл содержит ключевые слова, извлеченные из голосового содержимого hello, с частотой и сведения о смещении.</span><span class="sxs-lookup"><span data-stu-id="9458b-142">This file contains keywords extracted from hello speech content, with frequency and offset information.</span></span>

### <a name="job-name"></a><span data-ttu-id="9458b-143">Имя задания</span><span class="sxs-lookup"><span data-stu-id="9458b-143">Job name</span></span>
<span data-ttu-id="9458b-144">Понятное имя, позволяющее определить задания hello.</span><span class="sxs-lookup"><span data-stu-id="9458b-144">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="9458b-145">[Это](media-services-portal-check-job-progress.md) статье описывается, как можно отслеживать ход выполнения задания hello.</span><span class="sxs-lookup"><span data-stu-id="9458b-145">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="9458b-146">Выходной файл</span><span class="sxs-lookup"><span data-stu-id="9458b-146">Output file</span></span>
<span data-ttu-id="9458b-147">Понятное имя, позволяющее определить hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="9458b-147">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-hyperlapse"></a><span data-ttu-id="9458b-148">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="9458b-148">Azure Media Hyperlapse</span></span>
<span data-ttu-id="9458b-149">Azure Media Hyperlapse — это обработчик мультимедиа, который создает плавное замедленное видео от первого лица или контент, характерный для экшн-камер.</span><span class="sxs-lookup"><span data-stu-id="9458b-149">Azure Media Hyperlapse is an MP that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="9458b-150">Дополнительные сведения см. в [этой статье](media-services-hyperlapse-content.md).</span><span class="sxs-lookup"><span data-stu-id="9458b-150">For more information, see [this](media-services-hyperlapse-content.md) topic.</span></span> <span data-ttu-id="9458b-151">В этих разделах подробно описываются некоторые сведения о параметрах, которые можно указать для обработчика мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="9458b-151">This sections gives some details about options that you can specify for this MP.</span></span>

![Анализ видео](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a><span data-ttu-id="9458b-153">Speed</span><span class="sxs-lookup"><span data-stu-id="9458b-153">Speed</span></span>
<span data-ttu-id="9458b-154">Укажите скорость hello с какой toospeed hello входного видео.</span><span class="sxs-lookup"><span data-stu-id="9458b-154">Specify hello speed with which toospeed up hello input video.</span></span> <span data-ttu-id="9458b-155">Hello выводится представление hello входное видео в стабилизации и промежуток времени.</span><span class="sxs-lookup"><span data-stu-id="9458b-155">hello output is a stabilized and time-lapsed rendition of hello input video.</span></span>

### <a name="job-name"></a><span data-ttu-id="9458b-156">Имя задания</span><span class="sxs-lookup"><span data-stu-id="9458b-156">Job name</span></span>
<span data-ttu-id="9458b-157">Понятное имя, позволяющее определить задания hello.</span><span class="sxs-lookup"><span data-stu-id="9458b-157">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="9458b-158">[Это](media-services-portal-check-job-progress.md) статье описывается, как можно отслеживать ход выполнения задания hello.</span><span class="sxs-lookup"><span data-stu-id="9458b-158">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="9458b-159">Выходной файл</span><span class="sxs-lookup"><span data-stu-id="9458b-159">Output file</span></span>
<span data-ttu-id="9458b-160">Понятное имя, позволяющее определить hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="9458b-160">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-face-detector"></a><span data-ttu-id="9458b-161">Azure Media Face Detector</span><span class="sxs-lookup"><span data-stu-id="9458b-161">Azure Media Face Detector</span></span>
<span data-ttu-id="9458b-162">Hello **детектор лицевой стороны Azure Media** обработчик мультимедиа (MP) позволяет toocount, перемещений отслеживания и даже участие аудитории датчика и реакция через выражения лица.</span><span class="sxs-lookup"><span data-stu-id="9458b-162">hello **Azure Media Face Detector** media processor (MP) enables you toocount, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="9458b-163">В этой службе реализованы две функции:</span><span class="sxs-lookup"><span data-stu-id="9458b-163">This service contains two features:</span></span> 

* <span data-ttu-id="9458b-164">**Обнаружение лиц**</span><span class="sxs-lookup"><span data-stu-id="9458b-164">**Face detection**</span></span>
  
    <span data-ttu-id="9458b-165">Функция обнаружения лиц используется для обнаружения и отслеживания человеческих лиц на видео.</span><span class="sxs-lookup"><span data-stu-id="9458b-165">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="9458b-166">Несколько фрагментов могут быть обнаружены и впоследствии отслеживаются перемещения, с hello времени и расположение метаданных, возвращаемых в файле JSON.</span><span class="sxs-lookup"><span data-stu-id="9458b-166">Multiple faces can be detected and subsequently be tracked as they move around, with hello time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="9458b-167">Во время отслеживания, он попытается toogive согласованного toohello идентификатор же сталкиваются при hello пользователь перемещается на экране, даже в том случае, если они являются действия или кратко оставьте hello кадра.</span><span class="sxs-lookup"><span data-stu-id="9458b-167">During tracking, it will attempt toogive a consistent ID toohello same face while hello person is moving around on screen, even if they are obstructed or briefly leave hello frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="9458b-168">Эта служба не поддерживает распознавание лиц.</span><span class="sxs-lookup"><span data-stu-id="9458b-168">This services does not perform facial recognition.</span></span> <span data-ttu-id="9458b-169">Лицо, которое отправляется hello кадра или становится действия для слишком долго получает новый идентификатор при подключении.</span><span class="sxs-lookup"><span data-stu-id="9458b-169">An individual who leaves hello frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="9458b-170">**Определение эмоций**</span><span class="sxs-lookup"><span data-stu-id="9458b-170">**Emotion detection**</span></span>
  
    <span data-ttu-id="9458b-171">Обнаружение эмоций — это необязательный компонент hello обработчик мультимедиа обнаружения начертания, возвращающий анализа на несколько атрибутов этому из hello гарнитуры обнаружено, включая счастье, sadness, опасаясь, anger и многое другое.</span><span class="sxs-lookup"><span data-stu-id="9458b-171">Emotion Detection is an optional component of hello Face Detection Media Processor that returns analysis on multiple emotional attributes from hello faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

![Анализ видео](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a><span data-ttu-id="9458b-173">Режим распознавания</span><span class="sxs-lookup"><span data-stu-id="9458b-173">Detection mode</span></span>
<span data-ttu-id="9458b-174">Можно использовать один из следующих режимов hello обработчиком hello:</span><span class="sxs-lookup"><span data-stu-id="9458b-174">One of hello following modes can be used by hello processor:</span></span>

* <span data-ttu-id="9458b-175">обнаружение лиц;</span><span class="sxs-lookup"><span data-stu-id="9458b-175">face detection</span></span>
* <span data-ttu-id="9458b-176">распознавание эмоций отдельных лиц;</span><span class="sxs-lookup"><span data-stu-id="9458b-176">per face emotion detection</span></span>
* <span data-ttu-id="9458b-177">распознавание общих эмоций.</span><span class="sxs-lookup"><span data-stu-id="9458b-177">aggregate emotion detection</span></span>

### <a name="job-name"></a><span data-ttu-id="9458b-178">Имя задания</span><span class="sxs-lookup"><span data-stu-id="9458b-178">Job name</span></span>
<span data-ttu-id="9458b-179">Понятное имя, позволяющее определить задания hello.</span><span class="sxs-lookup"><span data-stu-id="9458b-179">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="9458b-180">[Это](media-services-portal-check-job-progress.md) статье описывается, как можно отслеживать ход выполнения задания hello.</span><span class="sxs-lookup"><span data-stu-id="9458b-180">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="9458b-181">Выходной файл</span><span class="sxs-lookup"><span data-stu-id="9458b-181">Output file</span></span>
<span data-ttu-id="9458b-182">Понятное имя, позволяющее определить hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="9458b-182">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-motion-detector"></a><span data-ttu-id="9458b-183">Azure Media Motion Detector</span><span class="sxs-lookup"><span data-stu-id="9458b-183">Azure Media Motion Detector</span></span>
<span data-ttu-id="9458b-184">Hello **Детектор движения Azure Media** media процессора (MP) позволяет вам tooefficiently указывают разделы интерес в видео, в противном случае длинные и процедура.</span><span class="sxs-lookup"><span data-stu-id="9458b-184">hello **Azure Media Motion Detector** media processor (MP) enables you tooefficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="9458b-185">Обнаружение движения может использоваться с камеры статических материал tooidentify разделами видео hello которой происходит движения.</span><span class="sxs-lookup"><span data-stu-id="9458b-185">Motion detection can be used on static camera footage tooidentify sections of hello video where motion occurs.</span></span> <span data-ttu-id="9458b-186">Он создает JSON-файл, содержащий метаданные с метки времени и hello, ограничивающий область, где произошло событие hello.</span><span class="sxs-lookup"><span data-stu-id="9458b-186">It generates a JSON file containing a metadata with timestamps and hello bounding region where hello event occurred.</span></span>

<span data-ttu-id="9458b-187">Ориентирован видео безопасности веб-каналы, эта технология является движения может toocategorize в соответствующие события и ложных положительных результатов, такие как изменение освещения и тени.</span><span class="sxs-lookup"><span data-stu-id="9458b-187">Targeted towards security video feeds, this technology is able toocategorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="9458b-188">Это позволяет toogenerate оповещений системы безопасности из каналов камеры без личного веб-узла с событиями бесконечные значения, не может tooextract моменты процент от видео с очень длинными наблюдения.</span><span class="sxs-lookup"><span data-stu-id="9458b-188">This allows you toogenerate security alerts from camera feeds without being spammed with endless irrelevant events, while being able tooextract moments of interest from extremely long surveillance videos.</span></span>

![Анализ видео](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a><span data-ttu-id="9458b-190">Azure Media Video Thumbnails</span><span class="sxs-lookup"><span data-stu-id="9458b-190">Azure Media Video Thumbnails</span></span>
<span data-ttu-id="9458b-191">Этот процессор помогают создавать сводки по видеофайлов большого размера, выбрав автоматически интересные фрагменты hello источника видео.</span><span class="sxs-lookup"><span data-stu-id="9458b-191">This processor can help you create summaries of long videos by automatically selecting interesting snippets from hello source video.</span></span> <span data-ttu-id="9458b-192">Это полезно при необходимости tooprovide краткий обзор какие tooexpect в длинного видео.</span><span class="sxs-lookup"><span data-stu-id="9458b-192">This is useful when you want tooprovide a quick overview of what tooexpect in a long video.</span></span> <span data-ttu-id="9458b-193">Подробные сведения и примеры см. в разделе [tooCreate используйте Azure Media Video эскизы сводку видео](media-services-video-summarization.md)</span><span class="sxs-lookup"><span data-stu-id="9458b-193">For detailed information and examples, see [Use Azure Media Video Thumbnails tooCreate a Video Summarization](media-services-video-summarization.md)</span></span>

![Анализ видео](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a><span data-ttu-id="9458b-195">Имя задания</span><span class="sxs-lookup"><span data-stu-id="9458b-195">Job name</span></span>
<span data-ttu-id="9458b-196">Понятное имя, позволяющее определить задания hello.</span><span class="sxs-lookup"><span data-stu-id="9458b-196">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="9458b-197">[Это](media-services-portal-check-job-progress.md) статье описывается, как можно отслеживать ход выполнения задания hello.</span><span class="sxs-lookup"><span data-stu-id="9458b-197">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="9458b-198">Выходной файл</span><span class="sxs-lookup"><span data-stu-id="9458b-198">Output file</span></span>
<span data-ttu-id="9458b-199">Понятное имя, позволяющее определить hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="9458b-199">A friendly name that lets you identify hello output content.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9458b-200">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9458b-200">Next steps</span></span>
<span data-ttu-id="9458b-201">Просмотрите схемы обучения работе со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="9458b-201">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9458b-202">Отзывы</span><span class="sxs-lookup"><span data-stu-id="9458b-202">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

