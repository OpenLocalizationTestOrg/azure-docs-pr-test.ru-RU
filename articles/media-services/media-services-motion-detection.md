---
title: "Обнаружение движения с помощью медиа-аналитики Azure | Документация Майкрософт"
description: "Обработчик мультимедиа, детектор движения мультимедиа Azure, позволяет эффективно определять представляющие интерес области в обычно продолжительном и бессобытийном видеоматериале."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: d144f813-1a55-442f-a895-5c4cb6d0aeae
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: milanga;juliako;
ms.openlocfilehash: 115ad9dfd88062f23d5d17eed8897ce5d2ca8484
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a><span data-ttu-id="8a0f0-103">Обнаружение движения с помощью медиа-аналитики Azure</span><span class="sxs-lookup"><span data-stu-id="8a0f0-103">Detect Motions with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="8a0f0-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="8a0f0-104">Overview</span></span>
<span data-ttu-id="8a0f0-105">Обработчик мультимедиа (MP) **Azure Media Motion Detector (детектор движения мультимедиа Azure)** позволяет эффективно определять представляющие интерес фрагменты в обычно продолжительном и бессобытийном видеоматериале.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-105">The **Azure Media Motion Detector** media processor (MP) enables you to efficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="8a0f0-106">Функцию обнаружения движения можно использовать при съемке стационарной камерой для определения тех областей видео, где происходит движение.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-106">Motion detection can be used on static camera footage to identify sections of the video where motion occurs.</span></span> <span data-ttu-id="8a0f0-107">Она создает JSON-файл, содержащий метаданные с метками времени и ограничивающую область, где возникло событие.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-107">It generates a JSON file containing a metadata with timestamps and the bounding region where the event occurred.</span></span>

<span data-ttu-id="8a0f0-108">Эта технология предназначена для видеоканалов в системе обеспечения безопасности. Она способна классифицировать движения на нужные события и ложноположительные срабатывания, происходящие, например, при изменении освещения и появлении теней.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-108">Targeted towards security video feeds, this technology is able to categorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="8a0f0-109">Это позволяет создавать оповещения системы безопасности при съемке и не обращать внимание на многочисленные неактуальные события, а также извлекать представляющие интерес фрагменты из продолжительных материалов видеонаблюдения.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-109">This allows you to generate security alerts from camera feeds without being spammed with endless irrelevant events, while being able to extract moments of interest from extremely long surveillance videos.</span></span>

<span data-ttu-id="8a0f0-110">Сейчас обработчик мультимедиа **Azure Media Motion Detector** доступен в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-110">The **Azure Media Motion Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="8a0f0-111">В этом разделе приводятся сведения об **Azure Media Motion Detector** и демонстрируется использование этого обработчика с пакетом SDK служб мультимедиа для .NET.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-111">This topic gives details about  **Azure Media Motion Detector** and shows how to use it with Media Services SDK for .NET</span></span>

## <a name="motion-detector-input-files"></a><span data-ttu-id="8a0f0-112">Входные файлы детектора движения</span><span class="sxs-lookup"><span data-stu-id="8a0f0-112">Motion Detector input files</span></span>
<span data-ttu-id="8a0f0-113">Видеофайлы.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-113">Video files.</span></span> <span data-ttu-id="8a0f0-114">Сейчас поддерживаются следующие форматы: MP4, MOV и WMV.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-114">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="8a0f0-115">Конфигурация задачи (предустановка)</span><span class="sxs-lookup"><span data-stu-id="8a0f0-115">Task configuration (preset)</span></span>
<span data-ttu-id="8a0f0-116">При создании задачи с использованием **Azure Media Motion Detector**необходимо задать предустановку конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span></span> 

### <a name="parameters"></a><span data-ttu-id="8a0f0-117">Параметры</span><span class="sxs-lookup"><span data-stu-id="8a0f0-117">Parameters</span></span>
<span data-ttu-id="8a0f0-118">Вы можете использовать следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="8a0f0-118">You can use the following parameters:</span></span>

| <span data-ttu-id="8a0f0-119">Имя</span><span class="sxs-lookup"><span data-stu-id="8a0f0-119">Name</span></span> | <span data-ttu-id="8a0f0-120">Параметры</span><span class="sxs-lookup"><span data-stu-id="8a0f0-120">Options</span></span> | <span data-ttu-id="8a0f0-121">Описание</span><span class="sxs-lookup"><span data-stu-id="8a0f0-121">Description</span></span> | <span data-ttu-id="8a0f0-122">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="8a0f0-122">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8a0f0-123">sensitivityLevel</span><span class="sxs-lookup"><span data-stu-id="8a0f0-123">sensitivityLevel</span></span> |<span data-ttu-id="8a0f0-124">Строка: low, medium, high</span><span class="sxs-lookup"><span data-stu-id="8a0f0-124">String:'low', 'medium', 'high'</span></span> |<span data-ttu-id="8a0f0-125">Задает уровень чувствительности, используемый при предоставлении сведений о движениях.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-125">Sets the sensitivity level at which motions is reported.</span></span> <span data-ttu-id="8a0f0-126">Измените его, чтобы отрегулировать величину ложных срабатываний</span><span class="sxs-lookup"><span data-stu-id="8a0f0-126">Adjust this to adjust amount of false positives.</span></span> |<span data-ttu-id="8a0f0-127">medium</span><span class="sxs-lookup"><span data-stu-id="8a0f0-127">'medium'</span></span> |
| <span data-ttu-id="8a0f0-128">frameSamplingValue</span><span class="sxs-lookup"><span data-stu-id="8a0f0-128">frameSamplingValue</span></span> |<span data-ttu-id="8a0f0-129">Положительное целое число</span><span class="sxs-lookup"><span data-stu-id="8a0f0-129">Positive integer</span></span> |<span data-ttu-id="8a0f0-130">Задает частоту, с которой выполняется алгоритм.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-130">Sets the frequency at which algorithm runs.</span></span> <span data-ttu-id="8a0f0-131">1 соответствует каждому кадру, 2 — каждому второму кадру и т. д.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-131">1 equals every frame, 2 means every 2nd frame, and so on.</span></span> |<span data-ttu-id="8a0f0-132">1</span><span class="sxs-lookup"><span data-stu-id="8a0f0-132">1</span></span> |
| <span data-ttu-id="8a0f0-133">detectLightChange</span><span class="sxs-lookup"><span data-stu-id="8a0f0-133">detectLightChange</span></span> |<span data-ttu-id="8a0f0-134">Логическое значение: true или false</span><span class="sxs-lookup"><span data-stu-id="8a0f0-134">Boolean:'true', 'false'</span></span> |<span data-ttu-id="8a0f0-135">Определяет, будут ли сведения об изменениях освещения отображены в результатах</span><span class="sxs-lookup"><span data-stu-id="8a0f0-135">Sets whether light changes are reported in the results</span></span> |<span data-ttu-id="8a0f0-136">False</span><span class="sxs-lookup"><span data-stu-id="8a0f0-136">'False'</span></span> |
| <span data-ttu-id="8a0f0-137">mergeTimeThreshold</span><span class="sxs-lookup"><span data-stu-id="8a0f0-137">mergeTimeThreshold</span></span> |<span data-ttu-id="8a0f0-138">xs-time: "ЧЧ:ММ:СС", </span><span class="sxs-lookup"><span data-stu-id="8a0f0-138">Xs-time: Hh:mm:ss</span></span><br/><span data-ttu-id="8a0f0-139">например 00:00:03</span><span class="sxs-lookup"><span data-stu-id="8a0f0-139">Example: 00:00:03</span></span> |<span data-ttu-id="8a0f0-140">Указывает промежуток времени между событиями движения. Произошедшие в рамках этого промежутка 2 события объединяются и отображаются в результатах как 1 событие.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-140">Specifies the time window between motion events where 2 events will be combined and reported as 1.</span></span> |<span data-ttu-id="8a0f0-141">00:00:00</span><span class="sxs-lookup"><span data-stu-id="8a0f0-141">00:00:00</span></span> |
| <span data-ttu-id="8a0f0-142">detectionZones</span><span class="sxs-lookup"><span data-stu-id="8a0f0-142">detectionZones</span></span> |<span data-ttu-id="8a0f0-143">Массив зон обнаружения: </span><span class="sxs-lookup"><span data-stu-id="8a0f0-143">An array of detection zones:</span></span><br/><span data-ttu-id="8a0f0-144">зона обнаружения представляет собой массив из трех или более точек 3;</span><span class="sxs-lookup"><span data-stu-id="8a0f0-144">- Detection Zone is an array of 3 or more points</span></span><br/><span data-ttu-id="8a0f0-145">точка — это координата по оси x и y в диапазоне от 0 до 1.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-145">- Point is a x and y coordinate from 0 to 1.</span></span> |<span data-ttu-id="8a0f0-146">Выводит список многоугольных зон обнаружения, которые будут использоваться.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-146">Describes the list of polygonal detection zones to be used.</span></span><br/><span data-ttu-id="8a0f0-147">В результатах в качестве зон отображаются идентификаторы (первый идентификатор — 0).</span><span class="sxs-lookup"><span data-stu-id="8a0f0-147">Results will be reported with the zones as an ID, with the first one being 'id':0</span></span> |<span data-ttu-id="8a0f0-148">Отдельная зона, которая охватывает весь кадр</span><span class="sxs-lookup"><span data-stu-id="8a0f0-148">Single zone which covers the entire frame.</span></span> |

### <a name="json-example"></a><span data-ttu-id="8a0f0-149">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="8a0f0-149">JSON example</span></span>
    {
      "version": "1.0",
      "options": {
        "sensitivityLevel": "medium",
        "frameSamplingValue": 1,
        "detectLightChange": "False",
        "mergeTimeThreshold":
        "00:00:02",
        "detectionZones": [
          [
            {"x": 0, "y": 0},
            {"x": 0.5, "y": 0},
            {"x": 0, "y": 1}
           ],
          [
            {"x": 0.3, "y": 0.3},
            {"x": 0.55, "y": 0.3},
            {"x": 0.8, "y": 0.3},
            {"x": 0.8, "y": 0.55},
            {"x": 0.8, "y": 0.8},
            {"x": 0.55, "y": 0.8},
            {"x": 0.3, "y": 0.8},
            {"x": 0.3, "y": 0.55}
          ]
        ]
      }
    }


## <a name="motion-detector-output-files"></a><span data-ttu-id="8a0f0-150">Выходные файлы детектора движения</span><span class="sxs-lookup"><span data-stu-id="8a0f0-150">Motion Detector output files</span></span>
<span data-ttu-id="8a0f0-151">Задание обнаружения движения возвращает в выходной ресурс-контейнер JSON-файл, описывающей оповещения о движении и их категории на видео.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-151">A motion detection job will return a JSON file in the output asset which describes the motion alerts, and their categories, within the video.</span></span> <span data-ttu-id="8a0f0-152">Файл будет содержать сведения о времени и длительности движения, обнаруженного на видео.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-152">The file will contain information about the time and duration of motion detected in the video.</span></span>

<span data-ttu-id="8a0f0-153">Обнаруженные движущиеся объекты на видео с неподвижным фоном (например, в режиме видеонаблюдения) API детектора движения отмечает визуальными индикаторами.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-153">The Motion Detector API provides indicators once there are objects in motion in a fixed background video (e.g. a surveillance video).</span></span> <span data-ttu-id="8a0f0-154">Детектор движения способен исключать ложные срабатывания, возникающие, например, при изменении освещения и затенении.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-154">The Motion Detector is trained to reduce false alarms, such as lighting and shadow changes.</span></span> <span data-ttu-id="8a0f0-155">В число текущих ограничений для действия алгоритмов входит съемка в режиме ночного видения, полупрозрачные и небольшие объекты.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-155">Current limitations of the algorithms include night vision videos, semi-transparent objects, and small objects.</span></span>

### <span data-ttu-id="8a0f0-156"><a id="output_elements"></a>Элементы выходного JSON-файла</span><span class="sxs-lookup"><span data-stu-id="8a0f0-156"><a id="output_elements"></a>Elements of the output JSON file</span></span>
> [!NOTE]
> <span data-ttu-id="8a0f0-157">В последнем выпуске формат выходного JSON-файла изменен. Для некоторых клиентов это может быть критическое изменение.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-157">In the latest release, the Output JSON format has changed and may represent a breaking change for some customers.</span></span>
> 
> 

<span data-ttu-id="8a0f0-158">В следующей таблице описаны элементы выходных данных JSON-файла.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-158">The following table describes elements of the output JSON file.</span></span>

| <span data-ttu-id="8a0f0-159">Элемент</span><span class="sxs-lookup"><span data-stu-id="8a0f0-159">Element</span></span> | <span data-ttu-id="8a0f0-160">Описание</span><span class="sxs-lookup"><span data-stu-id="8a0f0-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8a0f0-161">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="8a0f0-161">Version</span></span> |<span data-ttu-id="8a0f0-162">Версия API видео.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-162">This refers to the version of the Video API.</span></span> <span data-ttu-id="8a0f0-163">Текущая версия — 2</span><span class="sxs-lookup"><span data-stu-id="8a0f0-163">The current version is 2.</span></span> |
| <span data-ttu-id="8a0f0-164">Шкала времени</span><span class="sxs-lookup"><span data-stu-id="8a0f0-164">Timescale</span></span> |<span data-ttu-id="8a0f0-165">Количество тактов в секунду видео.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-165">"Ticks" per second of the video.</span></span> |
| <span data-ttu-id="8a0f0-166">Offset</span><span class="sxs-lookup"><span data-stu-id="8a0f0-166">Offset</span></span> |<span data-ttu-id="8a0f0-167">Смещение времени для отметки времени в тактах.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-167">The time offset for timestamps in "ticks".</span></span> <span data-ttu-id="8a0f0-168">В API видео версии 1.0 это значение всегда равно 0.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-168">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="8a0f0-169">В будущих поддерживаемых сценариях это значение может измениться.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-169">In future scenarios we support, this value may change.</span></span> |
| <span data-ttu-id="8a0f0-170">Framerate</span><span class="sxs-lookup"><span data-stu-id="8a0f0-170">Framerate</span></span> |<span data-ttu-id="8a0f0-171">Количество кадров в секунду видео.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-171">Frames per second of the video.</span></span> |
| <span data-ttu-id="8a0f0-172">Width, Height</span><span class="sxs-lookup"><span data-stu-id="8a0f0-172">Width, Height</span></span> |<span data-ttu-id="8a0f0-173">Ширина и высота изображения в пикселях.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-173">Refers to the width and height of the video in pixels.</span></span> |
| <span data-ttu-id="8a0f0-174">Начало</span><span class="sxs-lookup"><span data-stu-id="8a0f0-174">Start</span></span> |<span data-ttu-id="8a0f0-175">Метка времени начала в тактах.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-175">The start timestamp in "ticks".</span></span> |
| <span data-ttu-id="8a0f0-176">Длительность</span><span class="sxs-lookup"><span data-stu-id="8a0f0-176">Duration</span></span> |<span data-ttu-id="8a0f0-177">Продолжительность события в тактах.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-177">The length of the event, in "ticks".</span></span> |
| <span data-ttu-id="8a0f0-178">Интервал</span><span class="sxs-lookup"><span data-stu-id="8a0f0-178">Interval</span></span> |<span data-ttu-id="8a0f0-179">Интервал каждой записи события в тактах.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-179">The interval of each entry in the event, in "ticks".</span></span> |
| <span data-ttu-id="8a0f0-180">События</span><span class="sxs-lookup"><span data-stu-id="8a0f0-180">Events</span></span> |<span data-ttu-id="8a0f0-181">Каждый фрагмент события содержит движение, обнаруженное в течение этого промежутка времени.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-181">Each event fragment contains the motion detected within that time duration.</span></span> |
| <span data-ttu-id="8a0f0-182">Тип</span><span class="sxs-lookup"><span data-stu-id="8a0f0-182">Type</span></span> |<span data-ttu-id="8a0f0-183">В текущей версии — всегда значение 2 для универсального движения.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-183">In the current version, this is always ‘2’ for generic motion.</span></span> <span data-ttu-id="8a0f0-184">Эта метка позволяет API видео гибко классифицировать движение в будущих версиях.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-184">This label gives Video APIs the flexibility to categorize motion in future versions.</span></span> |
| <span data-ttu-id="8a0f0-185">RegionID</span><span class="sxs-lookup"><span data-stu-id="8a0f0-185">RegionID</span></span> |<span data-ttu-id="8a0f0-186">Как упоминалось выше, в этой версии всегда будет использоваться значение 0.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-186">As explained above, this will always be 0 in this version.</span></span> <span data-ttu-id="8a0f0-187">Эта метка позволяет API видео эффективно обнаруживать движение в различных областях в будущих версиях.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-187">This label gives Video API the flexibility to find motion in various regions in future versions.</span></span> |
| <span data-ttu-id="8a0f0-188">регионы</span><span class="sxs-lookup"><span data-stu-id="8a0f0-188">Regions</span></span> |<span data-ttu-id="8a0f0-189">Область в видео, где необходимо отслеживать движение.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-189">Refers to the area in your video where you care about motion.</span></span> <br/><br/><span data-ttu-id="8a0f0-190">id — это область отслеживания. В этой версии есть только ID 0.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-190">-"id" represents the region area – in this version there is only one, ID 0.</span></span> <br/><span data-ttu-id="8a0f0-191">type — это форма области, движение в которой нужно отслеживать.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-191">-"type" represents the shape of the region you care about for motion.</span></span> <span data-ttu-id="8a0f0-192">Сейчас поддерживаются прямоугольник и многоугольник.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-192">Currently, "rectangle" and "polygon" are supported.</span></span><br/> <span data-ttu-id="8a0f0-193">Если используется прямоугольник, то размеры области выражаются в значениях координат X, Y, ширины и высоты.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-193">If you specified "rectangle", the region has dimensions in X, Y, Width, and Height.</span></span> <span data-ttu-id="8a0f0-194">Координаты X и Y представляют верхние левые координаты X и Y области по нормализованной шкале от 0,0 до 1,0.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-194">The X and Y coordinates represent the upper left hand XY coordinates of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="8a0f0-195">Ширина и высота представляют размер области по нормализованной шкале от 0,0 до 1,0.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-195">The width and height represent the size of the region in a normalized scale of 0.0 to 1.0.</span></span> <span data-ttu-id="8a0f0-196">В текущей версии значения координат X, Y, ширины и высоты всегда фиксированы в позициях 0,0 и 1,1.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-196">In the current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span></span> <br/><span data-ttu-id="8a0f0-197">Если используется многоугольник, размеры области выражаются в точках.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-197">If you specified "polygon", the region has dimensions in points.</span></span> <br/> |
| <span data-ttu-id="8a0f0-198">Fragments</span><span class="sxs-lookup"><span data-stu-id="8a0f0-198">Fragments</span></span> |<span data-ttu-id="8a0f0-199">Метаданные разделены на разные сегменты, называемые фрагментами.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-199">The metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="8a0f0-200">Каждый фрагмент имеет начало, длительность, номер интервала и события.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-200">Each fragment contains a start, duration, interval number, and event(s).</span></span> <span data-ttu-id="8a0f0-201">Фрагмент без событий означает, что с момента начала и в течение продолжительности события движение обнаружено не было.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-201">A fragment with no events means that no motion was detected during that start time and duration.</span></span> |
| <span data-ttu-id="8a0f0-202">Квадратные скобки []</span><span class="sxs-lookup"><span data-stu-id="8a0f0-202">Brackets []</span></span> |<span data-ttu-id="8a0f0-203">Каждая скобка представляет один интервал в событии.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-203">Each bracket represents one interval in the event.</span></span> <span data-ttu-id="8a0f0-204">Пустые скобки для этого интервала означают, что движение не обнаружено.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-204">Empty brackets for that interval means that no motion was detected.</span></span> |
| <span data-ttu-id="8a0f0-205">locations</span><span class="sxs-lookup"><span data-stu-id="8a0f0-205">locations</span></span> |<span data-ttu-id="8a0f0-206">В этом новом элементе в разделе событий указывается место, где возникло движение.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-206">This new entry under events lists the location where the motion occurred.</span></span> <span data-ttu-id="8a0f0-207">Оно более точное, чем зона обнаружения.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-207">This is more specific than the detection zones.</span></span> |

<span data-ttu-id="8a0f0-208">Ниже приведен пример выходного JSON-файла.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-208">The following is a JSON output example</span></span>

    {
      "version": 2,
      "timescale": 23976,
      "offset": 0,
      "framerate": 24,
      "width": 1280,
      "height": 720,
      "regions": [
        {
          "id": 0,
          "type": "polygon",
          "points": [{'x': 0, 'y': 0},
            {'x': 0.5, 'y': 0},
            {'x': 0, 'y': 1}]
        }
      ],
      "fragments": [
        {
          "start": 0,
          "duration": 226765
        },
        {
          "start": 226765,
          "duration": 47952,
          "interval": 999,
          "events": [
            [
              {
                "type": 2,
                "typeName": "motion",
                "locations": [
                  {
                    "x": 0.004184,
                    "y": 0.007463,
                    "width": 0.991667,
                    "height": 0.985185
                  }
                ],
                "regionId": 0
              }
            ],

    …
## <a name="limitations"></a><span data-ttu-id="8a0f0-209">Ограничения</span><span class="sxs-lookup"><span data-stu-id="8a0f0-209">Limitations</span></span>
* <span data-ttu-id="8a0f0-210">Поддерживаемые входные видеоформаты: MP4, MOV и WMV.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-210">The supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="8a0f0-211">Функция обнаружения движения оптимизирована для видео с неподвижными фонами.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-211">Motion Detection is optimized for stationary background videos.</span></span> <span data-ttu-id="8a0f0-212">Алгоритм разработан для сокращения числа ложных срабатываний, возникающих, например, при изменении освещения и появления теней.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-212">The algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span></span>
* <span data-ttu-id="8a0f0-213">Из-за ряда технических проблем некоторые виды движений могут не обнаруживаться. Примерами является видео в режиме ночной съемки, полупрозрачные и небольшие объекты.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-213">Some motion may not be detected due to technical challenges; e.g. night vision videos, semi-transparent objects, and small objects.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="8a0f0-214">Пример кода .NET</span><span class="sxs-lookup"><span data-stu-id="8a0f0-214">.NET sample code</span></span>

<span data-ttu-id="8a0f0-215">В следующей программе показано, как выполнить следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-215">The following program shows how to:</span></span>

1. <span data-ttu-id="8a0f0-216">Создание ресурса-контейнера и отправка в него файла мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-216">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="8a0f0-217">Создание задания с задачей обнаружения движения на видео на основе файла конфигурации, содержащего следующую предустановку JSON.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-217">Create a job with a video motion detection task based on a configuration file that contains the following json preset.</span></span> 
   
        {
          "Version": "1.0",
          "Options": {
            "SensitivityLevel": "medium",
            "FrameSamplingValue": 1,
            "DetectLightChange": "False",
            "MergeTimeThreshold":
            "00:00:02",
            "DetectionZones": [
              [
                {"x": 0, "y": 0},
                {"x": 0.5, "y": 0},
                {"x": 0, "y": 1}
               ],
              [
                {"x": 0.3, "y": 0.3},
                {"x": 0.55, "y": 0.3},
                {"x": 0.8, "y": 0.3},
                {"x": 0.8, "y": 0.55},
                {"x": 0.8, "y": 0.8},
                {"x": 0.55, "y": 0.8},
                {"x": 0.3, "y": 0.8},
                {"x": 0.3, "y": 0.55}
              ]
            ]
          }
        }
3. <span data-ttu-id="8a0f0-218">Загрузка выходных JSON-файлов.</span><span class="sxs-lookup"><span data-stu-id="8a0f0-218">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="8a0f0-219">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8a0f0-219">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="8a0f0-220">Настройте среду разработки и укажите в файле app.config сведения о подключении, как описано в статье [Разработка служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="8a0f0-220">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="8a0f0-221">Пример</span><span class="sxs-lookup"><span data-stu-id="8a0f0-221">Example</span></span>


    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoMotionDetection
    {
        class Program
        {
            // Read values from the App.config file.
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

                // Run the VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference to Azure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="8a0f0-222">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="8a0f0-222">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="8a0f0-223">Отзывы</span><span class="sxs-lookup"><span data-stu-id="8a0f0-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="8a0f0-224">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="8a0f0-224">Related links</span></span>
[<span data-ttu-id="8a0f0-225">Блог по инструменту Motion Detector служб Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="8a0f0-225">Azure Media Services Motion Detector blog</span></span>](https://azure.microsoft.com/blog/motion-detector-update/)

[<span data-ttu-id="8a0f0-226">Общие сведения об аналитике служб мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="8a0f0-226">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="8a0f0-227">Демонстрационные материалы для медиааналитики Azure</span><span class="sxs-lookup"><span data-stu-id="8a0f0-227">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

