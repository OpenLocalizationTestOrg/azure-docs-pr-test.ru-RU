---
title: "Обнаружение лиц и определение эмоций с помощью медиа-аналитики Azure | Документация Майкрософт"
description: "В этом разделе содержатся сведения об обнаружении лиц и определении эмоций с помощью медиа-аналитики Azure."
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
ms.openlocfilehash: d7f3bc6c0d21db7adbb0c16c752d4ce49e99da5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a><span data-ttu-id="e8a4e-103">Обнаружение лиц и определение эмоций с помощью медиа-аналитики Azure</span><span class="sxs-lookup"><span data-stu-id="e8a4e-103">Detect Face and Emotion with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="e8a4e-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="e8a4e-104">Overview</span></span>
<span data-ttu-id="e8a4e-105">Обработчик мультимедиа (MP) **Azure Media Face Detector (детектор лиц мультимедиа Azure)** позволяет подсчитывать и отслеживать движения и даже определять заинтересованность и реакции людей с помощью выражений лиц.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-105">The **Azure Media Face Detector** media processor (MP) enables you to count, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="e8a4e-106">В этой службе реализованы две функции:</span><span class="sxs-lookup"><span data-stu-id="e8a4e-106">This service contains two features:</span></span> 

* <span data-ttu-id="e8a4e-107">**Обнаружение лиц**</span><span class="sxs-lookup"><span data-stu-id="e8a4e-107">**Face detection**</span></span>
  
    <span data-ttu-id="e8a4e-108">Функция обнаружения лиц используется для обнаружения и отслеживания человеческих лиц на видео.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-108">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="e8a4e-109">Поддерживается одновременное обнаружение множества лиц и их отслеживание по мере перемещения, в результате чего в JSON-файле будут возвращены метаданные времени и расположения.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-109">Multiple faces can be detected and subsequently be tracked as they move around, with the time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="e8a4e-110">Во время отслеживания и перемещения человека на экране предпринимается попытка получения согласованного ИД для одного и того же лица, даже если это лицо загораживает какой-либо объект или человек ненадолго выходит из кадра.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-110">During tracking, it will attempt to give a consistent ID to the same face while the person is moving around on screen, even if they are obstructed or briefly leave the frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="e8a4e-111">Эта служба не поддерживает распознавание лиц.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-111">This service does not perform facial recognition.</span></span> <span data-ttu-id="e8a4e-112">Человек, который выходит из кадра или остается закрытым каким-либо объектом в течение слишком долгого времени, после возвращения в кадр получит новый идентификатор.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-112">An individual who leaves the frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="e8a4e-113">**Определение эмоций**</span><span class="sxs-lookup"><span data-stu-id="e8a4e-113">**Emotion detection**</span></span>
  
    <span data-ttu-id="e8a4e-114">Определение эмоций представляет собой дополнительный компонент обработчика мультимедиа для обнаружения лиц. Он анализирует несколько выражений эмоций на обнаруженных лицах и определяет реакцию (или чувство) человека, например счастье, печаль, страх, гнев и многое другое.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-114">Emotion Detection is an optional component of the Face Detection Media Processor that returns analysis on multiple emotional attributes from the faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

<span data-ttu-id="e8a4e-115">Сейчас обработчик мультимедиа **Azure Media Face Detector** доступен в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-115">The **Azure Media Face Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="e8a4e-116">В этой статье приводятся сведения об обработчике **Azure Media Face Detector** и демонстрируется его использование с пакетом SDK служб мультимедиа для .NET.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-116">This topic gives details about  **Azure Media Face Detector** and shows how to use it with Media Services SDK for .NET.</span></span>

## <a name="face-detector-input-files"></a><span data-ttu-id="e8a4e-117">Входные файлы детектора лиц</span><span class="sxs-lookup"><span data-stu-id="e8a4e-117">Face Detector input files</span></span>
<span data-ttu-id="e8a4e-118">Видеофайлы.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-118">Video files.</span></span> <span data-ttu-id="e8a4e-119">Сейчас поддерживаются следующие форматы: MP4, MOV и WMV.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-119">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="face-detector-output-files"></a><span data-ttu-id="e8a4e-120">Выходные файлы детектора лиц</span><span class="sxs-lookup"><span data-stu-id="e8a4e-120">Face Detector output files</span></span>
<span data-ttu-id="e8a4e-121">API обнаружения и отслеживания лиц обеспечивает высокую точность обнаружения и отслеживания лиц с возможностью определения до 64 человеческих лиц на видео.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-121">The face detection and tracking API provides high precision face location detection and tracking that can detect up to 64 human faces in a video.</span></span> <span data-ttu-id="e8a4e-122">Лица в анфас позволяют получить лучшие результаты, тогда как значения по лицам в профиль или небольшим лицам (не более 24 x 24 пикселей) могут быть неточными.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-122">Frontal faces provide the best results, while side faces and small faces (less than or equal to 24x24 pixels) might not be as accurate.</span></span>

<span data-ttu-id="e8a4e-123">Обнаруженные и отслеживаемые лица возвращаются с указанием координат (слева, вверху, ширина и высота), которые обозначают расположение лиц на изображении в пикселях, а также с идентификационным номером лица, означающим отслеживание этого человека.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-123">The detected and tracked faces are returned with coordinates (left, top, width, and height) indicating the location of faces in the image in pixels, as well as a face ID number indicating the tracking of that individual.</span></span> <span data-ttu-id="e8a4e-124">Если лицо в анфас теряется или перекрывается в кадре, его идентификационный номер может быть сброшен, в результате чего нескольким людям назначаются несколько идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-124">Face ID numbers are prone to reset under circumstances when the frontal face is lost or overlapped in the frame, resulting in some individuals getting assigned multiple IDs.</span></span>

## <span data-ttu-id="e8a4e-125"><a id="output_elements"></a>Элементы выходного JSON-файла</span><span class="sxs-lookup"><span data-stu-id="e8a4e-125"><a id="output_elements"></a>Elements of the output JSON file</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

<span data-ttu-id="e8a4e-126">Детектор лиц использует методы фрагментации (с разделением метаданных на временные фрагменты и возможностью загрузки только необходимых частей) и сегментации (с разделением событий в случае, если они становятся слишком продолжительными).</span><span class="sxs-lookup"><span data-stu-id="e8a4e-126">Face Detector uses techniques of fragmentation (where the metadata can be broken up in time-based chunks and you can download only what you need), and segmentation (where the events are broken up in case they get too large).</span></span> <span data-ttu-id="e8a4e-127">Выполнив простые вычисления, вы сможете преобразовать данные.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-127">Some simple calculations can help you transform the data.</span></span> <span data-ttu-id="e8a4e-128">Например, если событие началось в 6 300 (тактов) с шкалой времени 2 997 (тактов в секунду) и частотой кадров 29,97 (кадров в секунду), то:</span><span class="sxs-lookup"><span data-stu-id="e8a4e-128">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and framerate of 29.97 (frames/sec), then:</span></span>

* <span data-ttu-id="e8a4e-129">начало/шкала времени = 2,1 секунды</span><span class="sxs-lookup"><span data-stu-id="e8a4e-129">Start/Timescale = 2.1 seconds</span></span>
* <span data-ttu-id="e8a4e-130">Время (с) x частота кадров = 63 кадра</span><span class="sxs-lookup"><span data-stu-id="e8a4e-130">Seconds x Framerate = 63 frames</span></span>

## <a name="face-detection-input-and-output-example"></a><span data-ttu-id="e8a4e-131">Пример входных и выходных данных обнаружения лиц</span><span class="sxs-lookup"><span data-stu-id="e8a4e-131">Face detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="e8a4e-132">Входные видеоданные</span><span class="sxs-lookup"><span data-stu-id="e8a4e-132">Input video</span></span>
[<span data-ttu-id="e8a4e-133">Входные видеоданные</span><span class="sxs-lookup"><span data-stu-id="e8a4e-133">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="e8a4e-134">Конфигурация задачи (предустановка)</span><span class="sxs-lookup"><span data-stu-id="e8a4e-134">Task configuration (preset)</span></span>
<span data-ttu-id="e8a4e-135">При создании задачи с помощью **Azure Media Face Detector**необходимо указать предустановку конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-135">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="e8a4e-136">Следующая предустановка конфигурации предназначена только для обнаружения лиц.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-136">The following configuration preset is just for face detection.</span></span>

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a><span data-ttu-id="e8a4e-137">Описания атрибутов</span><span class="sxs-lookup"><span data-stu-id="e8a4e-137">Attribute descriptions</span></span>
| <span data-ttu-id="e8a4e-138">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="e8a4e-138">Attribute name</span></span> | <span data-ttu-id="e8a4e-139">Описание</span><span class="sxs-lookup"><span data-stu-id="e8a4e-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e8a4e-140">Режим</span><span class="sxs-lookup"><span data-stu-id="e8a4e-140">Mode</span></span> |<span data-ttu-id="e8a4e-141">Fast: быстрая скорость обработки, но с меньшей точностью (по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="e8a4e-141">Fast - fast processing speed, but less accurate (default).</span></span>|

### <a name="json-output"></a><span data-ttu-id="e8a4e-142">Выходные данные JSON</span><span class="sxs-lookup"><span data-stu-id="e8a4e-142">JSON output</span></span>
<span data-ttu-id="e8a4e-143">Следующий пример выходных данных JSON был сокращен.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-143">The following example of JSON output was truncated.</span></span>

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

## <a name="emotion-detection-input-and-output-example"></a><span data-ttu-id="e8a4e-144">Пример входных и выходных данных определения эмоций</span><span class="sxs-lookup"><span data-stu-id="e8a4e-144">Emotion detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="e8a4e-145">Входные видеоданные</span><span class="sxs-lookup"><span data-stu-id="e8a4e-145">Input video</span></span>
[<span data-ttu-id="e8a4e-146">Входные видеоданные</span><span class="sxs-lookup"><span data-stu-id="e8a4e-146">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="e8a4e-147">Конфигурация задачи (предустановка)</span><span class="sxs-lookup"><span data-stu-id="e8a4e-147">Task configuration (preset)</span></span>
<span data-ttu-id="e8a4e-148">При создании задачи с помощью **Azure Media Face Detector**необходимо указать предустановку конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-148">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="e8a4e-149">Следующая предустановка конфигурации используется для создания JSON на основе определения эмоций.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-149">The following configuration preset specifies to create JSON based on the emotion detection.</span></span>

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a><span data-ttu-id="e8a4e-150">Описания атрибутов</span><span class="sxs-lookup"><span data-stu-id="e8a4e-150">Attribute descriptions</span></span>
| <span data-ttu-id="e8a4e-151">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="e8a4e-151">Attribute name</span></span> | <span data-ttu-id="e8a4e-152">Описание</span><span class="sxs-lookup"><span data-stu-id="e8a4e-152">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e8a4e-153">Режим</span><span class="sxs-lookup"><span data-stu-id="e8a4e-153">Mode</span></span> |<span data-ttu-id="e8a4e-154">Faces: только обнаружение лиц.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-154">Faces: Only face detection.</span></span><br/><span data-ttu-id="e8a4e-155">PerFaceEmotion: эмоции возвращаются отдельно для каждого обнаружения лиц.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-155">PerFaceEmotion: Return emotion independently for each face detection.</span></span><br/><span data-ttu-id="e8a4e-156">AggregateEmotion. Возвращаются средние значения эмоций для всех лиц в кадре.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-156">AggregateEmotion: Return average emotion values for all faces in frame.</span></span> |
| <span data-ttu-id="e8a4e-157">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="e8a4e-157">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="e8a4e-158">Используется, если выбран режим AggregateEmotion.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-158">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="e8a4e-159">Указывает длину видео для получения каждого совокупного результата в миллисекундах.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-159">Specifies the length of video used to produce each aggregate result, in milliseconds.</span></span> |
| <span data-ttu-id="e8a4e-160">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="e8a4e-160">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="e8a4e-161">Используется, если выбран режим AggregateEmotion.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-161">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="e8a4e-162">Указывает частоту для получения совокупных результатов.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-162">Specifies with what frequency to produce aggregate results.</span></span> |

#### <a name="aggregate-defaults"></a><span data-ttu-id="e8a4e-163">Совокупные значения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e8a4e-163">Aggregate defaults</span></span>
<span data-ttu-id="e8a4e-164">Ниже приведены рекомендуемые значения для совокупных параметров окна и интервала.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-164">Below are recommended values for the aggregate window and interval settings.</span></span> <span data-ttu-id="e8a4e-165">Значение AggregateEmotionWindowMs должно быть больше значения AggregateEmotionIntervalMs.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-165">AggregateEmotionWindowMs should be longer than AggregateEmotionIntervalMs.</span></span>

|| <span data-ttu-id="e8a4e-166">Значения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e8a4e-166">Defaults(s)</span></span> | <span data-ttu-id="e8a4e-167">Минимальные</span><span class="sxs-lookup"><span data-stu-id="e8a4e-167">Min(s)</span></span> | <span data-ttu-id="e8a4e-168">Максимальные</span><span class="sxs-lookup"><span data-stu-id="e8a4e-168">Max(s)</span></span> |
|--- | --- | --- | --- |
| <span data-ttu-id="e8a4e-169">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="e8a4e-169">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="e8a4e-170">0,5</span><span class="sxs-lookup"><span data-stu-id="e8a4e-170">0.5</span></span> |<span data-ttu-id="e8a4e-171">2</span><span class="sxs-lookup"><span data-stu-id="e8a4e-171">2</span></span> |<span data-ttu-id="e8a4e-172">0,25</span><span class="sxs-lookup"><span data-stu-id="e8a4e-172">0.25</span></span>|
| <span data-ttu-id="e8a4e-173">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="e8a4e-173">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="e8a4e-174">0,5</span><span class="sxs-lookup"><span data-stu-id="e8a4e-174">0.5</span></span> |<span data-ttu-id="e8a4e-175">1</span><span class="sxs-lookup"><span data-stu-id="e8a4e-175">1</span></span> |<span data-ttu-id="e8a4e-176">0,25</span><span class="sxs-lookup"><span data-stu-id="e8a4e-176">0.25</span></span>|

### <a name="json-output"></a><span data-ttu-id="e8a4e-177">Выходные данные JSON</span><span class="sxs-lookup"><span data-stu-id="e8a4e-177">JSON output</span></span>
<span data-ttu-id="e8a4e-178">Выходные данные JSON для совокупных эмоций (сокращенные).</span><span class="sxs-lookup"><span data-stu-id="e8a4e-178">JSON output for aggregate emotion (truncated):</span></span>

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

## <a name="limitations"></a><span data-ttu-id="e8a4e-179">Ограничения</span><span class="sxs-lookup"><span data-stu-id="e8a4e-179">Limitations</span></span>
* <span data-ttu-id="e8a4e-180">Поддерживаемые входные видеоформаты: MP4, MOV и WMV.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-180">The supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="e8a4e-181">Диапазон размеров обнаруживаемых лиц — от 24 x 24 до 2048 x 2048 пикселей.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-181">The detectable face size range is 24x24 to 2048x2048 pixels.</span></span> <span data-ttu-id="e8a4e-182">Лица вне этого диапазона не обнаруживаются.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-182">The faces out of this range will not be detected.</span></span>
* <span data-ttu-id="e8a4e-183">Максимальное количество возвращаемых лиц для каждого видео — 64.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-183">For each video, the maximum number of faces returned is 64.</span></span>
* <span data-ttu-id="e8a4e-184">Некоторые лица могут не обнаруживаться из-за технических проблем, например слишком большой лицевой угол (поворот головы) и существенное перекрытие.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-184">Some faces may not be detected due to technical challenges; e.g. very large face angles (head-pose), and large occlusion.</span></span> <span data-ttu-id="e8a4e-185">Лучшие результаты определяются для лиц в анфас или практически в анфас.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-185">Frontal and near-frontal faces have the best results.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="e8a4e-186">Пример кода .NET</span><span class="sxs-lookup"><span data-stu-id="e8a4e-186">.NET sample code</span></span>

<span data-ttu-id="e8a4e-187">В следующей программе показано, как выполнить следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-187">The following program shows how to:</span></span>

1. <span data-ttu-id="e8a4e-188">Создание ресурса-контейнера и отправка в него файла мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-188">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="e8a4e-189">Создание задания с задачей обнаружения лиц на основе файла конфигурации, содержащего следующую предустановку JSON.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-189">Create a job with a face detection task based on a configuration file that contains the following json preset.</span></span> 
   
        {
            "version": "1.0"
        }
3. <span data-ttu-id="e8a4e-190">Загрузка выходных JSON-файлов.</span><span class="sxs-lookup"><span data-stu-id="e8a4e-190">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="e8a4e-191">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e8a4e-191">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="e8a4e-192">Настройте среду разработки и укажите в файле app.config сведения о подключении, как описано в статье [Разработка служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="e8a4e-192">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="e8a4e-193">Пример</span><span class="sxs-lookup"><span data-stu-id="e8a4e-193">Example</span></span>

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

                // Run the FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference to Azure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

                // Use the following event handler to check job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch the job.
                job.Submit();

                // Check job execution and wait for job to finish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, the event handling
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="e8a4e-194">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="e8a4e-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e8a4e-195">Отзывы</span><span class="sxs-lookup"><span data-stu-id="e8a4e-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="e8a4e-196">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="e8a4e-196">Related links</span></span>
[<span data-ttu-id="e8a4e-197">Общие сведения об аналитике служб мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="e8a4e-197">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="e8a4e-198">Демонстрационные материалы для медиааналитики Azure</span><span class="sxs-lookup"><span data-stu-id="e8a4e-198">Azure Media Analytics demos</span></span>](http://amslabs.azurewebsites.net/demos/Analytics.html)

