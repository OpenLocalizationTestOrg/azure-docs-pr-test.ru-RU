---
title: "aaaDetect движения с медиа-аналитика Azure | Документы Microsoft"
description: "Здравствуйте Детектор движения мультимедиа Azure media процессора (MP) позволяет вам tooefficiently указывают разделы интерес в видео, в противном случае длинные и процедура."
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
ms.openlocfilehash: cb431375c92222053ed2239dd4e45767524dab68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a><span data-ttu-id="9d673-103">Обнаружение движения с помощью медиа-аналитики Azure</span><span class="sxs-lookup"><span data-stu-id="9d673-103">Detect Motions with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="9d673-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="9d673-104">Overview</span></span>
<span data-ttu-id="9d673-105">Hello **Детектор движения Azure Media** media процессора (MP) позволяет вам tooefficiently указывают разделы интерес в видео, в противном случае длинные и процедура.</span><span class="sxs-lookup"><span data-stu-id="9d673-105">hello **Azure Media Motion Detector** media processor (MP) enables you tooefficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="9d673-106">Обнаружение движения может использоваться с камеры статических материал tooidentify разделами видео hello которой происходит движения.</span><span class="sxs-lookup"><span data-stu-id="9d673-106">Motion detection can be used on static camera footage tooidentify sections of hello video where motion occurs.</span></span> <span data-ttu-id="9d673-107">Он создает JSON-файл, содержащий метаданные с метки времени и hello, ограничивающий область, где произошло событие hello.</span><span class="sxs-lookup"><span data-stu-id="9d673-107">It generates a JSON file containing a metadata with timestamps and hello bounding region where hello event occurred.</span></span>

<span data-ttu-id="9d673-108">Ориентирован видео безопасности веб-каналы, эта технология является движения может toocategorize в соответствующие события и ложных положительных результатов, такие как изменение освещения и тени.</span><span class="sxs-lookup"><span data-stu-id="9d673-108">Targeted towards security video feeds, this technology is able toocategorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="9d673-109">Это позволяет toogenerate оповещений системы безопасности из каналов камеры без личного веб-узла с событиями бесконечные значения, не может tooextract моменты процент от видео с очень длинными наблюдения.</span><span class="sxs-lookup"><span data-stu-id="9d673-109">This allows you toogenerate security alerts from camera feeds without being spammed with endless irrelevant events, while being able tooextract moments of interest from extremely long surveillance videos.</span></span>

<span data-ttu-id="9d673-110">Hello **Детектор движения Azure Media** MP в настоящее время находится в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="9d673-110">hello **Azure Media Motion Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="9d673-111">В этом разделе приведены подробные сведения о **Детектор движения Azure Media** и показано, как toouse с помощью пакета SDK служб мультимедиа для .NET</span><span class="sxs-lookup"><span data-stu-id="9d673-111">This topic gives details about  **Azure Media Motion Detector** and shows how toouse it with Media Services SDK for .NET</span></span>

## <a name="motion-detector-input-files"></a><span data-ttu-id="9d673-112">Входные файлы детектора движения</span><span class="sxs-lookup"><span data-stu-id="9d673-112">Motion Detector input files</span></span>
<span data-ttu-id="9d673-113">Видеофайлы.</span><span class="sxs-lookup"><span data-stu-id="9d673-113">Video files.</span></span> <span data-ttu-id="9d673-114">В настоящее время поддерживаются следующие форматы hello: MP4, MOV и WMV.</span><span class="sxs-lookup"><span data-stu-id="9d673-114">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="9d673-115">Конфигурация задачи (предустановка)</span><span class="sxs-lookup"><span data-stu-id="9d673-115">Task configuration (preset)</span></span>
<span data-ttu-id="9d673-116">При создании задачи с использованием **Azure Media Motion Detector**необходимо задать предустановку конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9d673-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span></span> 

### <a name="parameters"></a><span data-ttu-id="9d673-117">Параметры</span><span class="sxs-lookup"><span data-stu-id="9d673-117">Parameters</span></span>
<span data-ttu-id="9d673-118">Можно использовать следующие параметры hello.</span><span class="sxs-lookup"><span data-stu-id="9d673-118">You can use hello following parameters:</span></span>

| <span data-ttu-id="9d673-119">Имя</span><span class="sxs-lookup"><span data-stu-id="9d673-119">Name</span></span> | <span data-ttu-id="9d673-120">Параметры</span><span class="sxs-lookup"><span data-stu-id="9d673-120">Options</span></span> | <span data-ttu-id="9d673-121">Описание</span><span class="sxs-lookup"><span data-stu-id="9d673-121">Description</span></span> | <span data-ttu-id="9d673-122">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="9d673-122">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9d673-123">sensitivityLevel</span><span class="sxs-lookup"><span data-stu-id="9d673-123">sensitivityLevel</span></span> |<span data-ttu-id="9d673-124">Строка: low, medium, high</span><span class="sxs-lookup"><span data-stu-id="9d673-124">String:'low', 'medium', 'high'</span></span> |<span data-ttu-id="9d673-125">Задает уровень чувствительности hello в какой движения сообщается.</span><span class="sxs-lookup"><span data-stu-id="9d673-125">Sets hello sensitivity level at which motions is reported.</span></span> <span data-ttu-id="9d673-126">Измените эту сумму tooadjust ложных положительных результатов.</span><span class="sxs-lookup"><span data-stu-id="9d673-126">Adjust this tooadjust amount of false positives.</span></span> |<span data-ttu-id="9d673-127">medium</span><span class="sxs-lookup"><span data-stu-id="9d673-127">'medium'</span></span> |
| <span data-ttu-id="9d673-128">frameSamplingValue</span><span class="sxs-lookup"><span data-stu-id="9d673-128">frameSamplingValue</span></span> |<span data-ttu-id="9d673-129">Положительное целое число</span><span class="sxs-lookup"><span data-stu-id="9d673-129">Positive integer</span></span> |<span data-ttu-id="9d673-130">Задает частоту hello, в которой работает алгоритм.</span><span class="sxs-lookup"><span data-stu-id="9d673-130">Sets hello frequency at which algorithm runs.</span></span> <span data-ttu-id="9d673-131">1 соответствует каждому кадру, 2 — каждому второму кадру и т. д.</span><span class="sxs-lookup"><span data-stu-id="9d673-131">1 equals every frame, 2 means every 2nd frame, and so on.</span></span> |<span data-ttu-id="9d673-132">1</span><span class="sxs-lookup"><span data-stu-id="9d673-132">1</span></span> |
| <span data-ttu-id="9d673-133">detectLightChange</span><span class="sxs-lookup"><span data-stu-id="9d673-133">detectLightChange</span></span> |<span data-ttu-id="9d673-134">Логическое значение: true или false</span><span class="sxs-lookup"><span data-stu-id="9d673-134">Boolean:'true', 'false'</span></span> |<span data-ttu-id="9d673-135">Задает признак светлой изменения отображаются в результатах hello</span><span class="sxs-lookup"><span data-stu-id="9d673-135">Sets whether light changes are reported in hello results</span></span> |<span data-ttu-id="9d673-136">False</span><span class="sxs-lookup"><span data-stu-id="9d673-136">'False'</span></span> |
| <span data-ttu-id="9d673-137">mergeTimeThreshold</span><span class="sxs-lookup"><span data-stu-id="9d673-137">mergeTimeThreshold</span></span> |<span data-ttu-id="9d673-138">xs-time: "ЧЧ:ММ:СС", </span><span class="sxs-lookup"><span data-stu-id="9d673-138">Xs-time: Hh:mm:ss</span></span><br/><span data-ttu-id="9d673-139">например 00:00:03</span><span class="sxs-lookup"><span data-stu-id="9d673-139">Example: 00:00:03</span></span> |<span data-ttu-id="9d673-140">Указывает hello интервал времени между событиями движения, где объединяются и возвращаются с 1 2 события.</span><span class="sxs-lookup"><span data-stu-id="9d673-140">Specifies hello time window between motion events where 2 events will be combined and reported as 1.</span></span> |<span data-ttu-id="9d673-141">00:00:00</span><span class="sxs-lookup"><span data-stu-id="9d673-141">00:00:00</span></span> |
| <span data-ttu-id="9d673-142">detectionZones</span><span class="sxs-lookup"><span data-stu-id="9d673-142">detectionZones</span></span> |<span data-ttu-id="9d673-143">Массив зон обнаружения: </span><span class="sxs-lookup"><span data-stu-id="9d673-143">An array of detection zones:</span></span><br/><span data-ttu-id="9d673-144">зона обнаружения представляет собой массив из трех или более точек 3;</span><span class="sxs-lookup"><span data-stu-id="9d673-144">- Detection Zone is an array of 3 or more points</span></span><br/><span data-ttu-id="9d673-145">-Точка — x и y из 0 too1 координат.</span><span class="sxs-lookup"><span data-stu-id="9d673-145">- Point is a x and y coordinate from 0 too1.</span></span> |<span data-ttu-id="9d673-146">Описание обнаружения многоугольных зон toobe используется список hello.</span><span class="sxs-lookup"><span data-stu-id="9d673-146">Describes hello list of polygonal detection zones toobe used.</span></span><br/><span data-ttu-id="9d673-147">Результаты будут считаться с зонами hello идентификатора, первый из них выполняется «id» hello: 0</span><span class="sxs-lookup"><span data-stu-id="9d673-147">Results will be reported with hello zones as an ID, with hello first one being 'id':0</span></span> |<span data-ttu-id="9d673-148">Одной зоне, который охватывает всю рамку hello.</span><span class="sxs-lookup"><span data-stu-id="9d673-148">Single zone which covers hello entire frame.</span></span> |

### <a name="json-example"></a><span data-ttu-id="9d673-149">Пример JSON-файла</span><span class="sxs-lookup"><span data-stu-id="9d673-149">JSON example</span></span>
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


## <a name="motion-detector-output-files"></a><span data-ttu-id="9d673-150">Выходные файлы детектора движения</span><span class="sxs-lookup"><span data-stu-id="9d673-150">Motion Detector output files</span></span>
<span data-ttu-id="9d673-151">Обнаружение движения задания будет возвращать JSON-файла в hello выходной актив, который описывает предупреждения движения hello и их категорий, в пределах hello видео.</span><span class="sxs-lookup"><span data-stu-id="9d673-151">A motion detection job will return a JSON file in hello output asset which describes hello motion alerts, and their categories, within hello video.</span></span> <span data-ttu-id="9d673-152">Hello файл будет содержать сведения о времени и длительности перемещений в видео hello hello.</span><span class="sxs-lookup"><span data-stu-id="9d673-152">hello file will contain information about hello time and duration of motion detected in hello video.</span></span>

<span data-ttu-id="9d673-153">API обнаружения движения Hello предоставляет индикаторы после движущихся объектов в основных фоновое видео (например наблюдения видео).</span><span class="sxs-lookup"><span data-stu-id="9d673-153">hello Motion Detector API provides indicators once there are objects in motion in a fixed background video (e.g. a surveillance video).</span></span> <span data-ttu-id="9d673-154">Hello Детектор движения является обученной tooreduce ложные сигналы, такие как изменение тени и освещение.</span><span class="sxs-lookup"><span data-stu-id="9d673-154">hello Motion Detector is trained tooreduce false alarms, such as lighting and shadow changes.</span></span> <span data-ttu-id="9d673-155">Текущие ограничения алгоритмов hello включают ночь концепции видео, прозрачные объекты и небольших объектов.</span><span class="sxs-lookup"><span data-stu-id="9d673-155">Current limitations of hello algorithms include night vision videos, semi-transparent objects, and small objects.</span></span>

### <span data-ttu-id="9d673-156"><a id="output_elements"></a>Элементы hello выходных данных JSON-файла</span><span class="sxs-lookup"><span data-stu-id="9d673-156"><a id="output_elements"></a>Elements of hello output JSON file</span></span>
> [!NOTE]
> <span data-ttu-id="9d673-157">В последнем выпуске hello формат вывода JSON hello изменилась и может представлять является критическим изменением для некоторых клиентов.</span><span class="sxs-lookup"><span data-stu-id="9d673-157">In hello latest release, hello Output JSON format has changed and may represent a breaking change for some customers.</span></span>
> 
> 

<span data-ttu-id="9d673-158">Hello следующей таблице описываются элементы hello выходных данных JSON-файла.</span><span class="sxs-lookup"><span data-stu-id="9d673-158">hello following table describes elements of hello output JSON file.</span></span>

| <span data-ttu-id="9d673-159">Элемент</span><span class="sxs-lookup"><span data-stu-id="9d673-159">Element</span></span> | <span data-ttu-id="9d673-160">Описание</span><span class="sxs-lookup"><span data-stu-id="9d673-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9d673-161">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="9d673-161">Version</span></span> |<span data-ttu-id="9d673-162">Это относится toohello версии hello API видео.</span><span class="sxs-lookup"><span data-stu-id="9d673-162">This refers toohello version of hello Video API.</span></span> <span data-ttu-id="9d673-163">Текущая версия Hello — 2.</span><span class="sxs-lookup"><span data-stu-id="9d673-163">hello current version is 2.</span></span> |
| <span data-ttu-id="9d673-164">Шкала времени</span><span class="sxs-lookup"><span data-stu-id="9d673-164">Timescale</span></span> |<span data-ttu-id="9d673-165">«Тактах» в секунду hello видео.</span><span class="sxs-lookup"><span data-stu-id="9d673-165">"Ticks" per second of hello video.</span></span> |
| <span data-ttu-id="9d673-166">Offset</span><span class="sxs-lookup"><span data-stu-id="9d673-166">Offset</span></span> |<span data-ttu-id="9d673-167">Смещение времени Hello для отметки времени в «тактах».</span><span class="sxs-lookup"><span data-stu-id="9d673-167">hello time offset for timestamps in "ticks".</span></span> <span data-ttu-id="9d673-168">В API видео версии 1.0 это значение всегда равно 0.</span><span class="sxs-lookup"><span data-stu-id="9d673-168">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="9d673-169">В будущих поддерживаемых сценариях это значение может измениться.</span><span class="sxs-lookup"><span data-stu-id="9d673-169">In future scenarios we support, this value may change.</span></span> |
| <span data-ttu-id="9d673-170">Framerate</span><span class="sxs-lookup"><span data-stu-id="9d673-170">Framerate</span></span> |<span data-ttu-id="9d673-171">Кадров в секунду hello видео.</span><span class="sxs-lookup"><span data-stu-id="9d673-171">Frames per second of hello video.</span></span> |
| <span data-ttu-id="9d673-172">Width, Height</span><span class="sxs-lookup"><span data-stu-id="9d673-172">Width, Height</span></span> |<span data-ttu-id="9d673-173">Ссылается toohello ширину и высоту изображения в пикселях hello.</span><span class="sxs-lookup"><span data-stu-id="9d673-173">Refers toohello width and height of hello video in pixels.</span></span> |
| <span data-ttu-id="9d673-174">Начало</span><span class="sxs-lookup"><span data-stu-id="9d673-174">Start</span></span> |<span data-ttu-id="9d673-175">Hello запустите метки времени «тикает».</span><span class="sxs-lookup"><span data-stu-id="9d673-175">hello start timestamp in "ticks".</span></span> |
| <span data-ttu-id="9d673-176">Duration</span><span class="sxs-lookup"><span data-stu-id="9d673-176">Duration</span></span> |<span data-ttu-id="9d673-177">Длина Hello события hello в «тактах».</span><span class="sxs-lookup"><span data-stu-id="9d673-177">hello length of hello event, in "ticks".</span></span> |
| <span data-ttu-id="9d673-178">Интервал</span><span class="sxs-lookup"><span data-stu-id="9d673-178">Interval</span></span> |<span data-ttu-id="9d673-179">Интервал приветствия каждая запись в события hello в «тактах».</span><span class="sxs-lookup"><span data-stu-id="9d673-179">hello interval of each entry in hello event, in "ticks".</span></span> |
| <span data-ttu-id="9d673-180">События</span><span class="sxs-lookup"><span data-stu-id="9d673-180">Events</span></span> |<span data-ttu-id="9d673-181">Каждый фрагмент событие содержит движения hello обнаружен в течение этого промежутка времени.</span><span class="sxs-lookup"><span data-stu-id="9d673-181">Each event fragment contains hello motion detected within that time duration.</span></span> |
| <span data-ttu-id="9d673-182">Тип</span><span class="sxs-lookup"><span data-stu-id="9d673-182">Type</span></span> |<span data-ttu-id="9d673-183">В текущей версии hello всегда является "2" для универсального движения.</span><span class="sxs-lookup"><span data-stu-id="9d673-183">In hello current version, this is always ‘2’ for generic motion.</span></span> <span data-ttu-id="9d673-184">Эта метка предоставляет API-интерфейсы видео hello гибкость toocategorize движения в будущих версиях.</span><span class="sxs-lookup"><span data-stu-id="9d673-184">This label gives Video APIs hello flexibility toocategorize motion in future versions.</span></span> |
| <span data-ttu-id="9d673-185">RegionID</span><span class="sxs-lookup"><span data-stu-id="9d673-185">RegionID</span></span> |<span data-ttu-id="9d673-186">Как упоминалось выше, в этой версии всегда будет использоваться значение 0.</span><span class="sxs-lookup"><span data-stu-id="9d673-186">As explained above, this will always be 0 in this version.</span></span> <span data-ttu-id="9d673-187">Эта метка дает движения toofind API видео hello гибкость в различных регионах в будущих версиях.</span><span class="sxs-lookup"><span data-stu-id="9d673-187">This label gives Video API hello flexibility toofind motion in various regions in future versions.</span></span> |
| <span data-ttu-id="9d673-188">регионы</span><span class="sxs-lookup"><span data-stu-id="9d673-188">Regions</span></span> |<span data-ttu-id="9d673-189">Указывает область toohello видео, где важна движения.</span><span class="sxs-lookup"><span data-stu-id="9d673-189">Refers toohello area in your video where you care about motion.</span></span> <br/><br/><span data-ttu-id="9d673-190">-«id» представляет hello области — в этой версии имеется только один, идентификатор 0.</span><span class="sxs-lookup"><span data-stu-id="9d673-190">-"id" represents hello region area – in this version there is only one, ID 0.</span></span> <br/><span data-ttu-id="9d673-191">-«тип» представляет фигуры hello области hello важна для перемещения.</span><span class="sxs-lookup"><span data-stu-id="9d673-191">-"type" represents hello shape of hello region you care about for motion.</span></span> <span data-ttu-id="9d673-192">Сейчас поддерживаются прямоугольник и многоугольник.</span><span class="sxs-lookup"><span data-stu-id="9d673-192">Currently, "rectangle" and "polygon" are supported.</span></span><br/> <span data-ttu-id="9d673-193">Если вы указали «прямоугольник», hello области имеет измерений X, Y, ширину и высоту.</span><span class="sxs-lookup"><span data-stu-id="9d673-193">If you specified "rectangle", hello region has dimensions in X, Y, Width, and Height.</span></span> <span data-ttu-id="9d673-194">Hello X и Y координаты представляют координатами x и y верхний левый hello области hello в нормализованной масштабом too1.0 0,0.</span><span class="sxs-lookup"><span data-stu-id="9d673-194">hello X and Y coordinates represent hello upper left hand XY coordinates of hello region in a normalized scale of 0.0 too1.0.</span></span> <span data-ttu-id="9d673-195">Hello ширины и высоты представляют Привет размер области hello в масштабе нормализованный 0,0 too1.0.</span><span class="sxs-lookup"><span data-stu-id="9d673-195">hello width and height represent hello size of hello region in a normalized scale of 0.0 too1.0.</span></span> <span data-ttu-id="9d673-196">В текущей версии hello X, Y, ширина и высота всегда фиксируются в 0, 0 и 1, 1.</span><span class="sxs-lookup"><span data-stu-id="9d673-196">In hello current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span></span> <br/><span data-ttu-id="9d673-197">Если вы указали «многоугольник», область hello имеет измерений в пунктах.</span><span class="sxs-lookup"><span data-stu-id="9d673-197">If you specified "polygon", hello region has dimensions in points.</span></span> <br/> |
| <span data-ttu-id="9d673-198">Fragments</span><span class="sxs-lookup"><span data-stu-id="9d673-198">Fragments</span></span> |<span data-ttu-id="9d673-199">метаданные Hello фрагментирован вверх в разных сегментах, называемые фрагментами.</span><span class="sxs-lookup"><span data-stu-id="9d673-199">hello metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="9d673-200">Каждый фрагмент имеет начало, длительность, номер интервала и события.</span><span class="sxs-lookup"><span data-stu-id="9d673-200">Each fragment contains a start, duration, interval number, and event(s).</span></span> <span data-ttu-id="9d673-201">Фрагмент без событий означает, что с момента начала и в течение продолжительности события движение обнаружено не было.</span><span class="sxs-lookup"><span data-stu-id="9d673-201">A fragment with no events means that no motion was detected during that start time and duration.</span></span> |
| <span data-ttu-id="9d673-202">Квадратные скобки []</span><span class="sxs-lookup"><span data-stu-id="9d673-202">Brackets []</span></span> |<span data-ttu-id="9d673-203">Каждая скобка представляет один интервал в событии hello.</span><span class="sxs-lookup"><span data-stu-id="9d673-203">Each bracket represents one interval in hello event.</span></span> <span data-ttu-id="9d673-204">Пустые скобки для этого интервала означают, что движение не обнаружено.</span><span class="sxs-lookup"><span data-stu-id="9d673-204">Empty brackets for that interval means that no motion was detected.</span></span> |
| <span data-ttu-id="9d673-205">locations</span><span class="sxs-lookup"><span data-stu-id="9d673-205">locations</span></span> |<span data-ttu-id="9d673-206">Эту новую запись в списке событий перечислены hello расположение, где произошло hello движения.</span><span class="sxs-lookup"><span data-stu-id="9d673-206">This new entry under events lists hello location where hello motion occurred.</span></span> <span data-ttu-id="9d673-207">Это более точным определением, чем зоны обнаружения hello.</span><span class="sxs-lookup"><span data-stu-id="9d673-207">This is more specific than hello detection zones.</span></span> |

<span data-ttu-id="9d673-208">Hello ниже приведен пример выходных данных JSON</span><span class="sxs-lookup"><span data-stu-id="9d673-208">hello following is a JSON output example</span></span>

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
## <a name="limitations"></a><span data-ttu-id="9d673-209">Ограничения</span><span class="sxs-lookup"><span data-stu-id="9d673-209">Limitations</span></span>
* <span data-ttu-id="9d673-210">формат ввода видео Hello поддерживается включают MP4, MOV и WMV.</span><span class="sxs-lookup"><span data-stu-id="9d673-210">hello supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="9d673-211">Функция обнаружения движения оптимизирована для видео с неподвижными фонами.</span><span class="sxs-lookup"><span data-stu-id="9d673-211">Motion Detection is optimized for stationary background videos.</span></span> <span data-ttu-id="9d673-212">алгоритм Hello основное внимание уделяется уменьшение ложные сигналы, такие как изменения освещения и тени.</span><span class="sxs-lookup"><span data-stu-id="9d673-212">hello algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span></span>
* <span data-ttu-id="9d673-213">Некоторые движения могут не обнаруживаться из-за проблем tootechnical; Например ночь концепции видео, прозрачные объекты и небольшие объекты.</span><span class="sxs-lookup"><span data-stu-id="9d673-213">Some motion may not be detected due tootechnical challenges; e.g. night vision videos, semi-transparent objects, and small objects.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="9d673-214">Пример кода .NET</span><span class="sxs-lookup"><span data-stu-id="9d673-214">.NET sample code</span></span>

<span data-ttu-id="9d673-215">Hello следующей программе показано как:</span><span class="sxs-lookup"><span data-stu-id="9d673-215">hello following program shows how to:</span></span>

1. <span data-ttu-id="9d673-216">Создание актива и отправка файла мультимедиа в актив hello.</span><span class="sxs-lookup"><span data-stu-id="9d673-216">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="9d673-217">Создание задания с задачу обнаружения движения видео на основе файла конфигурации, содержащий hello, следующая Предустановка json.</span><span class="sxs-lookup"><span data-stu-id="9d673-217">Create a job with a video motion detection task based on a configuration file that contains hello following json preset.</span></span> 
   
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
3. <span data-ttu-id="9d673-218">Загрузка файлов JSON hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="9d673-218">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="9d673-219">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9d673-219">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="9d673-220">Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="9d673-220">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="9d673-221">Пример</span><span class="sxs-lookup"><span data-stu-id="9d673-221">Example</span></span>


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
            // Read values from hello App.config file.
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

                // Run hello VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference tooAzure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="9d673-222">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="9d673-222">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9d673-223">Отзывы</span><span class="sxs-lookup"><span data-stu-id="9d673-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="9d673-224">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="9d673-224">Related links</span></span>
[<span data-ttu-id="9d673-225">Блог по инструменту Motion Detector служб Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="9d673-225">Azure Media Services Motion Detector blog</span></span>](https://azure.microsoft.com/blog/motion-detector-update/)

[<span data-ttu-id="9d673-226">Общие сведения об аналитике служб мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="9d673-226">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="9d673-227">Демонстрационные материалы для медиааналитики Azure</span><span class="sxs-lookup"><span data-stu-id="9d673-227">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

