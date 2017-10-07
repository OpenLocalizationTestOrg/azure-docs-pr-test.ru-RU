---
title: "aaaDetect начертания и эмоций с медиа-аналитика Azure | Документы Microsoft"
description: "В этом разделе показано, как грани toodetect и эмоций с медиа-аналитика Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5ca4692c-23f1-451d-9d82-cbc8bf0fd707
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: f58d81d82dde08a694cdb4d92c6bab6a40a9c157
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a><span data-ttu-id="3ad8c-103">Обнаружение лиц и определение эмоций с помощью медиа-аналитики Azure</span><span class="sxs-lookup"><span data-stu-id="3ad8c-103">Detect Face and Emotion with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="3ad8c-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="3ad8c-104">Overview</span></span>
<span data-ttu-id="3ad8c-105">Hello **детектор лицевой стороны Azure Media** обработчик мультимедиа (MP) позволяет toocount, перемещений отслеживания и даже участие аудитории датчика и реакция через выражения лица.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-105">hello **Azure Media Face Detector** media processor (MP) enables you toocount, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="3ad8c-106">В этой службе реализованы две функции:</span><span class="sxs-lookup"><span data-stu-id="3ad8c-106">This service contains two features:</span></span> 

* <span data-ttu-id="3ad8c-107">**Обнаружение лиц**</span><span class="sxs-lookup"><span data-stu-id="3ad8c-107">**Face detection**</span></span>
  
    <span data-ttu-id="3ad8c-108">Функция обнаружения лиц используется для обнаружения и отслеживания человеческих лиц на видео.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-108">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="3ad8c-109">Несколько фрагментов могут быть обнаружены и впоследствии отслеживаются перемещения, с hello времени и расположение метаданных, возвращаемых в файле JSON.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-109">Multiple faces can be detected and subsequently be tracked as they move around, with hello time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="3ad8c-110">Во время отслеживания, он попытается toogive согласованного toohello идентификатор же сталкиваются при hello пользователь перемещается на экране, даже в том случае, если они являются действия или кратко оставьте hello кадра.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-110">During tracking, it will attempt toogive a consistent ID toohello same face while hello person is moving around on screen, even if they are obstructed or briefly leave hello frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="3ad8c-111">Эта служба не поддерживает распознавание лиц.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-111">This service does not perform facial recognition.</span></span> <span data-ttu-id="3ad8c-112">Лицо, которое отправляется hello кадра или становится действия для слишком долго получает новый идентификатор при подключении.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-112">An individual who leaves hello frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="3ad8c-113">**Определение эмоций**</span><span class="sxs-lookup"><span data-stu-id="3ad8c-113">**Emotion detection**</span></span>
  
    <span data-ttu-id="3ad8c-114">Обнаружение эмоций — это необязательный компонент hello обработчик мультимедиа обнаружения начертания, возвращающий анализа на несколько атрибутов этому из hello гарнитуры обнаружено, включая счастье, sadness, опасаясь, anger и многое другое.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-114">Emotion Detection is an optional component of hello Face Detection Media Processor that returns analysis on multiple emotional attributes from hello faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

<span data-ttu-id="3ad8c-115">Hello **детектор лицевой стороны Azure Media** MP в настоящее время находится в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-115">hello **Azure Media Face Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="3ad8c-116">В этом разделе приведены подробные сведения о **детектор лицевой стороны Azure Media** и показано, как toouse с помощью пакета SDK служб мультимедиа для .NET.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-116">This topic gives details about  **Azure Media Face Detector** and shows how toouse it with Media Services SDK for .NET.</span></span>

## <a name="face-detector-input-files"></a><span data-ttu-id="3ad8c-117">Входные файлы детектора лиц</span><span class="sxs-lookup"><span data-stu-id="3ad8c-117">Face Detector input files</span></span>
<span data-ttu-id="3ad8c-118">Видеофайлы.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-118">Video files.</span></span> <span data-ttu-id="3ad8c-119">В настоящее время поддерживаются следующие форматы hello: MP4, MOV и WMV.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-119">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="face-detector-output-files"></a><span data-ttu-id="3ad8c-120">Выходные файлы детектора лиц</span><span class="sxs-lookup"><span data-stu-id="3ad8c-120">Face Detector output files</span></span>
<span data-ttu-id="3ad8c-121">API обнаружения и отслеживания начертания Hello предоставляет высокой точности начертания расположение обнаружения и отслеживания для определения вверх too64 человека фрагменты в видео.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-121">hello face detection and tracking API provides high precision face location detection and tracking that can detect up too64 human faces in a video.</span></span> <span data-ttu-id="3ad8c-122">Распознавания фронтальных видов лица предоставляют hello лучшей при боковые и небольшие фрагменты (меньше или равно too24x24 пикселей) не может быть точным.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-122">Frontal faces provide hello best results, while side faces and small faces (less than or equal too24x24 pixels) might not be as accurate.</span></span>

<span data-ttu-id="3ad8c-123">Hello обнаружены и отслеживаемых гарнитуры возвращаются с координатами (left, top, ширину и высоту), указывающий положение hello граней в hello изображения в пикселях, а также начертания идентификатор число, указывающее, hello, отдельные отслеживание.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-123">hello detected and tracked faces are returned with coordinates (left, top, width, and height) indicating hello location of faces in hello image in pixels, as well as a face ID number indicating hello tracking of that individual.</span></span> <span data-ttu-id="3ad8c-124">Идентификаторы начертания, имеют ошибкам tooreset обстоятельствах при утере или перекрываются в кадре hello фронтального лица hello в результате некоторых пользователей, назначении нескольких идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-124">Face ID numbers are prone tooreset under circumstances when hello frontal face is lost or overlapped in hello frame, resulting in some individuals getting assigned multiple IDs.</span></span>

## <span data-ttu-id="3ad8c-125"><a id="output_elements"></a>Элементы hello выходных данных JSON-файла</span><span class="sxs-lookup"><span data-stu-id="3ad8c-125"><a id="output_elements"></a>Elements of hello output JSON file</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

<span data-ttu-id="3ad8c-126">Детектор начертания использует методы фрагментации (где hello метаданные могут быть классифицированы фрагментами синхронизированного и можно загрузить только необходимые) и сегментации (где hello события сгруппированы в случае, если они получают слишком большое).</span><span class="sxs-lookup"><span data-stu-id="3ad8c-126">Face Detector uses techniques of fragmentation (where hello metadata can be broken up in time-based chunks and you can download only what you need), and segmentation (where hello events are broken up in case they get too large).</span></span> <span data-ttu-id="3ad8c-127">Несколько простых вычислений поможет вам преобразовывать данные hello.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-127">Some simple calculations can help you transform hello data.</span></span> <span data-ttu-id="3ad8c-128">Например, если событие началось в 6 300 (тактов) с шкалой времени 2 997 (тактов в секунду) и частотой кадров 29,97 (кадров в секунду), то:</span><span class="sxs-lookup"><span data-stu-id="3ad8c-128">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and framerate of 29.97 (frames/sec), then:</span></span>

* <span data-ttu-id="3ad8c-129">начало/шкала времени = 2,1 секунды</span><span class="sxs-lookup"><span data-stu-id="3ad8c-129">Start/Timescale = 2.1 seconds</span></span>
* <span data-ttu-id="3ad8c-130">Время (с) x частота кадров = 63 кадра</span><span class="sxs-lookup"><span data-stu-id="3ad8c-130">Seconds x Framerate = 63 frames</span></span>

## <a name="face-detection-input-and-output-example"></a><span data-ttu-id="3ad8c-131">Пример входных и выходных данных обнаружения лиц</span><span class="sxs-lookup"><span data-stu-id="3ad8c-131">Face detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="3ad8c-132">Входные видеоданные</span><span class="sxs-lookup"><span data-stu-id="3ad8c-132">Input video</span></span>
[<span data-ttu-id="3ad8c-133">Входные видеоданные</span><span class="sxs-lookup"><span data-stu-id="3ad8c-133">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="3ad8c-134">Конфигурация задачи (предустановка)</span><span class="sxs-lookup"><span data-stu-id="3ad8c-134">Task configuration (preset)</span></span>
<span data-ttu-id="3ad8c-135">При создании задачи с помощью **Azure Media Face Detector**необходимо указать предустановку конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-135">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="3ad8c-136">Привет, следующая Предустановка конфигурации необходимо только для обнаружения лицевой стороны.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-136">hello following configuration preset is just for face detection.</span></span>

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a><span data-ttu-id="3ad8c-137">Описания атрибутов</span><span class="sxs-lookup"><span data-stu-id="3ad8c-137">Attribute descriptions</span></span>
| <span data-ttu-id="3ad8c-138">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="3ad8c-138">Attribute name</span></span> | <span data-ttu-id="3ad8c-139">Описание</span><span class="sxs-lookup"><span data-stu-id="3ad8c-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3ad8c-140">Режим</span><span class="sxs-lookup"><span data-stu-id="3ad8c-140">Mode</span></span> |<span data-ttu-id="3ad8c-141">Fast: быстрая скорость обработки, но с меньшей точностью (по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="3ad8c-141">Fast - fast processing speed, but less accurate (default).</span></span>|

### <a name="json-output"></a><span data-ttu-id="3ad8c-142">Выходные данные JSON</span><span class="sxs-lookup"><span data-stu-id="3ad8c-142">JSON output</span></span>
<span data-ttu-id="3ad8c-143">Следующий пример выходных данных JSON Hello был усечен.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-143">hello following example of JSON output was truncated.</span></span>

    {
    "version": 1,
    "timescale": 30000,
    "offset": 0,
    "framerate": 29.97,
    "width": 1280,
    "height": 720,
    "fragments": [
        {
        "start": 0,
        "duration": 60060
        },
        {
        "start": 60060,
        "duration": 60060,
        "interval": 1001,
        "events": [
            [
            {
                "id": 0,
                "x": 0.519531,
                "y": 0.180556,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517969,
                "y": 0.181944,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517187,
                "y": 0.183333,
                "width": 0.0851562,
                "height": 0.151389
            }
            ],

        . . . 

## <a name="emotion-detection-input-and-output-example"></a><span data-ttu-id="3ad8c-144">Пример входных и выходных данных определения эмоций</span><span class="sxs-lookup"><span data-stu-id="3ad8c-144">Emotion detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="3ad8c-145">Входные видеоданные</span><span class="sxs-lookup"><span data-stu-id="3ad8c-145">Input video</span></span>
[<span data-ttu-id="3ad8c-146">Входные видеоданные</span><span class="sxs-lookup"><span data-stu-id="3ad8c-146">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="3ad8c-147">Конфигурация задачи (предустановка)</span><span class="sxs-lookup"><span data-stu-id="3ad8c-147">Task configuration (preset)</span></span>
<span data-ttu-id="3ad8c-148">При создании задачи с помощью **Azure Media Face Detector**необходимо указать предустановку конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-148">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="3ad8c-149">следующие конфигурации Предустановка Hello указывает toocreate JSON на основании обнаружения эмоций hello.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-149">hello following configuration preset specifies toocreate JSON based on hello emotion detection.</span></span>

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a><span data-ttu-id="3ad8c-150">Описания атрибутов</span><span class="sxs-lookup"><span data-stu-id="3ad8c-150">Attribute descriptions</span></span>
| <span data-ttu-id="3ad8c-151">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="3ad8c-151">Attribute name</span></span> | <span data-ttu-id="3ad8c-152">Описание</span><span class="sxs-lookup"><span data-stu-id="3ad8c-152">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3ad8c-153">Режим</span><span class="sxs-lookup"><span data-stu-id="3ad8c-153">Mode</span></span> |<span data-ttu-id="3ad8c-154">Faces: только обнаружение лиц.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-154">Faces: Only face detection.</span></span><br/><span data-ttu-id="3ad8c-155">PerFaceEmotion: эмоции возвращаются отдельно для каждого обнаружения лиц.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-155">PerFaceEmotion: Return emotion independently for each face detection.</span></span><br/><span data-ttu-id="3ad8c-156">AggregateEmotion. Возвращаются средние значения эмоций для всех лиц в кадре.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-156">AggregateEmotion: Return average emotion values for all faces in frame.</span></span> |
| <span data-ttu-id="3ad8c-157">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="3ad8c-157">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="3ad8c-158">Используется, если выбран режим AggregateEmotion.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-158">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="3ad8c-159">Указывает длину hello видео используется tooproduce каждого итоговый результат, в миллисекундах.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-159">Specifies hello length of video used tooproduce each aggregate result, in milliseconds.</span></span> |
| <span data-ttu-id="3ad8c-160">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="3ad8c-160">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="3ad8c-161">Используется, если выбран режим AggregateEmotion.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-161">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="3ad8c-162">Указывает агрегат tooproduce какие частоты приводит.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-162">Specifies with what frequency tooproduce aggregate results.</span></span> |

#### <a name="aggregate-defaults"></a><span data-ttu-id="3ad8c-163">Совокупные значения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3ad8c-163">Aggregate defaults</span></span>
<span data-ttu-id="3ad8c-164">Ниже, рекомендуется использовать значения статистической оконной hello и параметры интервала.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-164">Below are recommended values for hello aggregate window and interval settings.</span></span> <span data-ttu-id="3ad8c-165">Значение AggregateEmotionWindowMs должно быть больше значения AggregateEmotionIntervalMs.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-165">AggregateEmotionWindowMs should be longer than AggregateEmotionIntervalMs.</span></span>

|| <span data-ttu-id="3ad8c-166">Значения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3ad8c-166">Defaults(s)</span></span> | <span data-ttu-id="3ad8c-167">Минимальные</span><span class="sxs-lookup"><span data-stu-id="3ad8c-167">Min(s)</span></span> | <span data-ttu-id="3ad8c-168">Максимальные</span><span class="sxs-lookup"><span data-stu-id="3ad8c-168">Max(s)</span></span> |
|--- | --- | --- | --- |
| <span data-ttu-id="3ad8c-169">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="3ad8c-169">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="3ad8c-170">0,5</span><span class="sxs-lookup"><span data-stu-id="3ad8c-170">0.5</span></span> |<span data-ttu-id="3ad8c-171">2</span><span class="sxs-lookup"><span data-stu-id="3ad8c-171">2</span></span> |<span data-ttu-id="3ad8c-172">0,25</span><span class="sxs-lookup"><span data-stu-id="3ad8c-172">0.25</span></span>|
| <span data-ttu-id="3ad8c-173">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="3ad8c-173">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="3ad8c-174">0,5</span><span class="sxs-lookup"><span data-stu-id="3ad8c-174">0.5</span></span> |<span data-ttu-id="3ad8c-175">1</span><span class="sxs-lookup"><span data-stu-id="3ad8c-175">1</span></span> |<span data-ttu-id="3ad8c-176">0,25</span><span class="sxs-lookup"><span data-stu-id="3ad8c-176">0.25</span></span>|

### <a name="json-output"></a><span data-ttu-id="3ad8c-177">Выходные данные JSON</span><span class="sxs-lookup"><span data-stu-id="3ad8c-177">JSON output</span></span>
<span data-ttu-id="3ad8c-178">Выходные данные JSON для совокупных эмоций (сокращенные).</span><span class="sxs-lookup"><span data-stu-id="3ad8c-178">JSON output for aggregate emotion (truncated):</span></span>

    {
     "version": 1,
     "timescale": 30000,
     "offset": 0,
     "framerate": 29.97,
     "width": 1280,
     "height": 720,
     "fragments": [
       {
         "start": 0,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ]
         ]
       },
       {
         "start": 60060,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0.688541,
                 "happiness": 0.0586323,
                 "surprise": 0.227184,
                 "sadness": 0.00945675,
                 "anger": 0.00592107,
                 "disgust": 0.00154993,
                 "fear": 0.00450447,
                 "contempt": 0.0042109
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,

## <a name="limitations"></a><span data-ttu-id="3ad8c-179">Ограничения</span><span class="sxs-lookup"><span data-stu-id="3ad8c-179">Limitations</span></span>
* <span data-ttu-id="3ad8c-180">формат ввода видео Hello поддерживается включают MP4, MOV и WMV.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-180">hello supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="3ad8c-181">размер диапазона Hello выявляемых лицевой стороны — too2048x2048 24 x 24 пикселя.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-181">hello detectable face size range is 24x24 too2048x2048 pixels.</span></span> <span data-ttu-id="3ad8c-182">не будет обнаружен гарнитуры Hello за пределами этого диапазона.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-182">hello faces out of this range will not be detected.</span></span>
* <span data-ttu-id="3ad8c-183">Для каждого видео hello гарнитуры возвращается не более 64.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-183">For each video, hello maximum number of faces returned is 64.</span></span>
* <span data-ttu-id="3ad8c-184">Некоторые лица могут не обнаруживаться из-за проблем tootechnical; Например очень больших углы лицевой стороны (head позы) и больших перекрытия.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-184">Some faces may not be detected due tootechnical challenges; e.g. very large face angles (head-pose), and large occlusion.</span></span> <span data-ttu-id="3ad8c-185">Фрагменты фронтальных и около фронтальных имеют hello наилучших результатов.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-185">Frontal and near-frontal faces have hello best results.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="3ad8c-186">Пример кода .NET</span><span class="sxs-lookup"><span data-stu-id="3ad8c-186">.NET sample code</span></span>

<span data-ttu-id="3ad8c-187">Hello следующей программе показано как:</span><span class="sxs-lookup"><span data-stu-id="3ad8c-187">hello following program shows how to:</span></span>

1. <span data-ttu-id="3ad8c-188">Создание актива и отправка файла мультимедиа в актив hello.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-188">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="3ad8c-189">Создание задания с задачу обнаружения лиц на основе файла конфигурации, содержащий hello, следующая Предустановка json.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-189">Create a job with a face detection task based on a configuration file that contains hello following json preset.</span></span> 
   
        {
            "version": "1.0"
        }
3. <span data-ttu-id="3ad8c-190">Загрузка файлов JSON hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="3ad8c-190">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="3ad8c-191">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3ad8c-191">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="3ad8c-192">Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="3ad8c-192">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="3ad8c-193">Пример</span><span class="sxs-lookup"><span data-stu-id="3ad8c-193">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace FaceDetection
    {
        class Program
        {
            private static readonly string _AADTenantDomain =
                      ConfigurationManager.AppSettings["AADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
                      ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

            // Field for service context.
            private static CloudMediaContext _context = null;

            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

                // Run hello FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference tooAzure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

                // Use hello following event handler toocheck job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch hello job.
                job.Submit();

                // Check job execution and wait for job toofinish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, hello event handling
                // method for job progress should log errors.  Here we check
                // for error state and exit if needed.
                if (job.State == JobState.Error)
                {
                    ErrorDetail error = job.Tasks.First().ErrorDetails.First();
                    Console.WriteLine(string.Format("Error: {0}. {1}",
                                                    error.Code,
                                                    error.Message));
                    return null;
                }

                return job.OutputMediaAssets[0];
            }

            static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
            {
                IAsset asset = _context.Assets.Create(assetName, options);

                var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
                assetFile.Upload(filePath);

                return asset;
            }

            static void DownloadAsset(IAsset asset, string outputDirectory)
            {
                foreach (IAssetFile file in asset.AssetFiles)
                {
                    file.Download(Path.Combine(outputDirectory, file.Name));
                }
            }

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

            static private void StateChanged(object sender, JobStateChangedEventArgs e)
            {
                Console.WriteLine("Job state changed event:");
                Console.WriteLine("  Previous state: " + e.PreviousState);
                Console.WriteLine("  Current state: " + e.CurrentState);

                switch (e.CurrentState)
                {
                    case JobState.Finished:
                        Console.WriteLine();
                        Console.WriteLine("Job is finished.");
                        Console.WriteLine();
                        break;
                    case JobState.Canceling:
                    case JobState.Queued:
                    case JobState.Scheduled:
                    case JobState.Processing:
                        Console.WriteLine("Please wait...\n");
                        break;
                    case JobState.Canceled:
                    case JobState.Error:
                        // Cast sender as a job.
                        IJob job = (IJob)sender;
                        // Display or log error details as needed.
                        // LogJobStop(job.Id);
                        break;
                    default:
                        break;
                }
            }
        }
    }

## <a name="media-services-learning-paths"></a><span data-ttu-id="3ad8c-194">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="3ad8c-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3ad8c-195">Отзывы</span><span class="sxs-lookup"><span data-stu-id="3ad8c-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="3ad8c-196">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="3ad8c-196">Related links</span></span>
[<span data-ttu-id="3ad8c-197">Общие сведения об аналитике служб мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="3ad8c-197">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="3ad8c-198">Демонстрационные материалы для медиааналитики Azure</span><span class="sxs-lookup"><span data-stu-id="3ad8c-198">Azure Media Analytics demos</span></span>](http://amslabs.azurewebsites.net/demos/Analytics.html)

