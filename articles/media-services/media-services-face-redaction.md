---
title: "грани aaaRedact с медиа-аналитика Azure | Документы Microsoft"
description: "В этом разделе показано, как tooredact сталкивается с мультимедиа Azure analytics."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5b6d8b8c-5f4d-4fef-b3d6-dc22c6b5a0f5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;
ms.openlocfilehash: 1f5688a8c6374151c526a9c702b904d8c3e46164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a><span data-ttu-id="c4ad5-103">Скрытие лиц с помощью аналитики мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="c4ad5-103">Redact faces with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="c4ad5-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="c4ad5-104">Overview</span></span>
<span data-ttu-id="c4ad5-105">**Azure Media Redactor** — [медиа-аналитика Azure](media-services-analytics-overview.md) обработчик мультимедиа (MP), который предлагает исправления масштабируемой лицевой стороны в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="c4ad5-106">Исправления лицевой стороны позволяет вам toomodify видео в гранях tooblur порядок выбранных сотрудников.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-106">Face redaction enables you toomodify your video in order tooblur faces of selected individuals.</span></span> <span data-ttu-id="c4ad5-107">Вы можете toouse hello начертания исправления службы в общих сценариях безопасности и новости мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-107">You may want toouse hello face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="c4ad5-108">Через несколько минут, содержащий несколько начертаний материал может занять tooredact часы вручную, но с этой службы hello начертания процесс исправления потребуется всего несколько простых шагов.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-108">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service hello face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="c4ad5-109">Дополнительные сведения см. в [этом блоге](https://azure.microsoft.com/blog/azure-media-redactor/).</span><span class="sxs-lookup"><span data-stu-id="c4ad5-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="c4ad5-110">В этом разделе приведены подробные сведения о **Redactor мультимедиа Azure** и показано, как toouse с помощью пакета SDK служб мультимедиа для .NET.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-110">This topic gives details about **Azure Media Redactor** and shows how toouse it with Media Services SDK for .NET.</span></span>

<span data-ttu-id="c4ad5-111">Hello **Redactor мультимедиа Azure** MP в настоящее время находится в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-111">hello **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="c4ad5-112">Он доступен во всех общедоступных регионах Azure, а также в центрах обработки данных для государственных организаций США и для Китая.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-112">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="c4ad5-113">В настоящее время эта предварительная версия предоставляется бесплатно.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-113">This preview is currently free of charge.</span></span> 

## <a name="face-redaction-modes"></a><span data-ttu-id="c4ad5-114">Режимы скрытия лиц</span><span class="sxs-lookup"><span data-stu-id="c4ad5-114">Face redaction modes</span></span>
<span data-ttu-id="c4ad5-115">Лица исправления работает путем обнаружения лиц в каждом кадре видео и отслеживания начертания hello объекта оба вперед и назад по времени, чтобы hello же человек может быть размытое из других углы наклона.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-115">Facial redaction works by detecting faces in every frame of video and tracking hello face object both forwards and backwards in time, so that hello same individual can be blurred from other angles as well.</span></span> <span data-ttu-id="c4ad5-116">Hello автоматические исправления процесс очень сложный и не всегда выдает 100% нужного выходных данных, поэтому медиа-аналитика обеспечивает несколько способов toomodify hello конечного результата.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-116">hello automated redaction process is very complex and does not always produce 100% of desired output, for this reason Media Analytics provides you with a couple of ways toomodify hello final output.</span></span>

<span data-ttu-id="c4ad5-117">В полностью автоматическом режиме Добавление tooa нет двухпроходный рабочий процесс, который позволяет hello выбора или деактивировать-selection найден сторон через список идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-117">In addition tooa fully automatic mode, there is a two-pass workflow which allows hello selection/de-selection of found faces via a list of IDs.</span></span> <span data-ttu-id="c4ad5-118">Кроме того произвольный каждого кадра корректировки hello MP toomake использует файл метаданных в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-118">Also, toomake arbitrary per frame adjustments hello MP uses a metadata file in JSON format.</span></span> <span data-ttu-id="c4ad5-119">Этот рабочий процесс разделен на два режима: **анализ** и **скрытие**.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-119">This workflow is split into **Analyze** and **Redact** modes.</span></span> <span data-ttu-id="c4ad5-120">Можно объединить два режима hello за один проход, выполняет обе задачи в одно задание; Этот режим называется **объединенное**.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-120">You can combine hello two modes in a single pass that runs both tasks in one job; this mode is called **Combined**.</span></span>

### <a name="combined-mode"></a><span data-ttu-id="c4ad5-121">Объединенный режим</span><span class="sxs-lookup"><span data-stu-id="c4ad5-121">Combined mode</span></span>
<span data-ttu-id="c4ad5-122">В результате вы получите MP4-файл с автоматическим скрытием, который не нужно править вручную.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-122">This will produce a redacted mp4 automatically without any manual input.</span></span>

| <span data-ttu-id="c4ad5-123">Этап</span><span class="sxs-lookup"><span data-stu-id="c4ad5-123">Stage</span></span> | <span data-ttu-id="c4ad5-124">Имя файла</span><span class="sxs-lookup"><span data-stu-id="c4ad5-124">File Name</span></span> | <span data-ttu-id="c4ad5-125">Примечания</span><span class="sxs-lookup"><span data-stu-id="c4ad5-125">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c4ad5-126">Входной ресурс-контейнер</span><span class="sxs-lookup"><span data-stu-id="c4ad5-126">Input asset</span></span> |<span data-ttu-id="c4ad5-127">foo.bar</span><span class="sxs-lookup"><span data-stu-id="c4ad5-127">foo.bar</span></span> |<span data-ttu-id="c4ad5-128">Видео в формате WMV, MOV или MP4</span><span class="sxs-lookup"><span data-stu-id="c4ad5-128">Video in WMV, MOV, or MP4 format</span></span> |
| <span data-ttu-id="c4ad5-129">Входная конфигурация</span><span class="sxs-lookup"><span data-stu-id="c4ad5-129">Input config</span></span> |<span data-ttu-id="c4ad5-130">Конфигурация задания (предустановка)</span><span class="sxs-lookup"><span data-stu-id="c4ad5-130">Job configuration preset</span></span> |<span data-ttu-id="c4ad5-131">{'version':'1.0', 'options': {'mode':'combined'}}</span><span class="sxs-lookup"><span data-stu-id="c4ad5-131">{'version':'1.0', 'options': {'mode':'combined'}}</span></span> |
| <span data-ttu-id="c4ad5-132">Выходной ресурс-контейнер</span><span class="sxs-lookup"><span data-stu-id="c4ad5-132">Output asset</span></span> |<span data-ttu-id="c4ad5-133">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="c4ad5-133">foo_redacted.mp4</span></span> |<span data-ttu-id="c4ad5-134">Видео с размытием</span><span class="sxs-lookup"><span data-stu-id="c4ad5-134">Video with blurring applied</span></span> |

#### <a name="input-example"></a><span data-ttu-id="c4ad5-135">Пример входных данных</span><span class="sxs-lookup"><span data-stu-id="c4ad5-135">Input example:</span></span>
[<span data-ttu-id="c4ad5-136">См. видео</span><span class="sxs-lookup"><span data-stu-id="c4ad5-136">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a><span data-ttu-id="c4ad5-137">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="c4ad5-137">Output example:</span></span>
[<span data-ttu-id="c4ad5-138">См. видео</span><span class="sxs-lookup"><span data-stu-id="c4ad5-138">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a><span data-ttu-id="c4ad5-139">Режим анализа</span><span class="sxs-lookup"><span data-stu-id="c4ad5-139">Analyze mode</span></span>
<span data-ttu-id="c4ad5-140">Hello **анализ** этап рабочего процесса двухпроходный hello входные видео и создает файл JSON расположений лицевой стороны, а изображений jpg каждого обнаруженного начертания.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-140">hello **analyze** pass of hello two-pass workflow takes a video input and produces a JSON file of face locations, and jpg images of each detected face.</span></span>

| <span data-ttu-id="c4ad5-141">Этап</span><span class="sxs-lookup"><span data-stu-id="c4ad5-141">Stage</span></span> | <span data-ttu-id="c4ad5-142">Имя файла</span><span class="sxs-lookup"><span data-stu-id="c4ad5-142">File Name</span></span> | <span data-ttu-id="c4ad5-143">Примечания</span><span class="sxs-lookup"><span data-stu-id="c4ad5-143">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c4ad5-144">Входной ресурс-контейнер</span><span class="sxs-lookup"><span data-stu-id="c4ad5-144">Input asset</span></span> |<span data-ttu-id="c4ad5-145">foo.bar</span><span class="sxs-lookup"><span data-stu-id="c4ad5-145">foo.bar</span></span> |<span data-ttu-id="c4ad5-146">Видео в формате WMV, MPV или MP4</span><span class="sxs-lookup"><span data-stu-id="c4ad5-146">Video in WMV, MPV, or MP4 format</span></span> |
| <span data-ttu-id="c4ad5-147">Входная конфигурация</span><span class="sxs-lookup"><span data-stu-id="c4ad5-147">Input config</span></span> |<span data-ttu-id="c4ad5-148">Конфигурация задания (предустановка)</span><span class="sxs-lookup"><span data-stu-id="c4ad5-148">Job configuration preset</span></span> |<span data-ttu-id="c4ad5-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span><span class="sxs-lookup"><span data-stu-id="c4ad5-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span></span> |
| <span data-ttu-id="c4ad5-150">Выходной ресурс-контейнер</span><span class="sxs-lookup"><span data-stu-id="c4ad5-150">Output asset</span></span> |<span data-ttu-id="c4ad5-151">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="c4ad5-151">foo_annotations.json</span></span> |<span data-ttu-id="c4ad5-152">Аннотация с данными о расположении лиц в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-152">Annotation data of face locations in JSON format.</span></span> <span data-ttu-id="c4ad5-153">Это можно изменить путем hello пользователя toomodify hello стирают ограничительные рамки.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-153">This can be edited by hello user toomodify hello blurring bounding boxes.</span></span> <span data-ttu-id="c4ad5-154">См. пример ниже.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-154">See sample below.</span></span> |
| <span data-ttu-id="c4ad5-155">Выходной ресурс-контейнер</span><span class="sxs-lookup"><span data-stu-id="c4ad5-155">Output asset</span></span> |<span data-ttu-id="c4ad5-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span><span class="sxs-lookup"><span data-stu-id="c4ad5-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span></span> |<span data-ttu-id="c4ad5-157">Обрезанное jpg каждого обнаружил лицо, где число hello указывает labelId hello гарнитур hello</span><span class="sxs-lookup"><span data-stu-id="c4ad5-157">A cropped jpg of each detected face, where hello number indicates hello labelId of hello face</span></span> |

#### <a name="output-example"></a><span data-ttu-id="c4ad5-158">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="c4ad5-158">Output example:</span></span>

    {
      "version": 1,
      "timescale": 24000,
      "offset": 0,
      "framerate": 23.976,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 48048,
          "interval": 1001,
          "events": [
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [
              {
                "index": 13,
                "id": 1138,
                "x": 0.29537,
                "y": -0.18987,
                "width": 0.36239,
                "height": 0.80335
              },
              {
                "index": 13,
                "id": 2028,
                "x": 0.60427,
                "y": 0.16098,
                "width": 0.26958,
                "height": 0.57943
              }
            ],

    … truncated

### <a name="redact-mode"></a><span data-ttu-id="c4ad5-159">Режим скрытия</span><span class="sxs-lookup"><span data-stu-id="c4ad5-159">Redact mode</span></span>
<span data-ttu-id="c4ad5-160">Hello второго этапа hello рабочего процесса имеет большее количество входных данных, которые должны быть объединены в один ресурс.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-160">hello second pass of hello workflow takes a larger number of inputs that must be combined into a single asset.</span></span>

<span data-ttu-id="c4ad5-161">Они включают список идентификаторов tooblur исходного видео hello и заметок hello JSON.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-161">This includes a list of IDs tooblur, hello original video, and hello annotations JSON.</span></span> <span data-ttu-id="c4ad5-162">Этот режим использует стирают tooapply hello заметок на входное видео hello.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-162">This mode uses hello annotations tooapply blurring on hello input video.</span></span>

<span data-ttu-id="c4ad5-163">Hello выходные данные этапа анализ hello не включает hello исходного видео.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-163">hello output from hello Analyze pass does not include hello original video.</span></span> <span data-ttu-id="c4ad5-164">Hello видео должен toobe отправлен в hello входного актива для задачи в режиме Redact hello и выбран в качестве первичного файла hello.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-164">hello video needs toobe uploaded into hello input asset for hello Redact mode task and selected as hello primary file.</span></span>

| <span data-ttu-id="c4ad5-165">Этап</span><span class="sxs-lookup"><span data-stu-id="c4ad5-165">Stage</span></span> | <span data-ttu-id="c4ad5-166">Имя файла</span><span class="sxs-lookup"><span data-stu-id="c4ad5-166">File Name</span></span> | <span data-ttu-id="c4ad5-167">Примечания</span><span class="sxs-lookup"><span data-stu-id="c4ad5-167">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c4ad5-168">Входной ресурс-контейнер</span><span class="sxs-lookup"><span data-stu-id="c4ad5-168">Input asset</span></span> |<span data-ttu-id="c4ad5-169">foo.bar</span><span class="sxs-lookup"><span data-stu-id="c4ad5-169">foo.bar</span></span> |<span data-ttu-id="c4ad5-170">Видео в формате WMV, MPV или MP4.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-170">Video in WMV, MPV, or MP4 format.</span></span> <span data-ttu-id="c4ad5-171">То же видео, что и на этапе 1.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-171">Same video as in step 1.</span></span> |
| <span data-ttu-id="c4ad5-172">Входной ресурс-контейнер</span><span class="sxs-lookup"><span data-stu-id="c4ad5-172">Input asset</span></span> |<span data-ttu-id="c4ad5-173">foo_annotations.json</span><span class="sxs-lookup"><span data-stu-id="c4ad5-173">foo_annotations.json</span></span> |<span data-ttu-id="c4ad5-174">Файл аннотации с метаданными, полученными на этапе 1, с необязательными изменениями.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-174">annotations metadata file from phase one, with optional modifications.</span></span> |
| <span data-ttu-id="c4ad5-175">Входной ресурс-контейнер</span><span class="sxs-lookup"><span data-stu-id="c4ad5-175">Input asset</span></span> |<span data-ttu-id="c4ad5-176">foo_IDList.txt (необязательный)</span><span class="sxs-lookup"><span data-stu-id="c4ad5-176">foo_IDList.txt (Optional)</span></span> |<span data-ttu-id="c4ad5-177">Необязательный новую строку запятыми список идентификаторов tooredact лицевой стороны.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-177">Optional new line separated list of face IDs tooredact.</span></span> <span data-ttu-id="c4ad5-178">Если оставить его пустым, будут размыты все лица.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-178">If left blank, this blurs all faces.</span></span> |
| <span data-ttu-id="c4ad5-179">Входная конфигурация</span><span class="sxs-lookup"><span data-stu-id="c4ad5-179">Input config</span></span> |<span data-ttu-id="c4ad5-180">Конфигурация задания (предустановка)</span><span class="sxs-lookup"><span data-stu-id="c4ad5-180">Job configuration preset</span></span> |<span data-ttu-id="c4ad5-181">{'version':'1.0', 'options': {'mode':'redact'}}</span><span class="sxs-lookup"><span data-stu-id="c4ad5-181">{'version':'1.0', 'options': {'mode':'redact'}}</span></span> |
| <span data-ttu-id="c4ad5-182">Выходной ресурс-контейнер</span><span class="sxs-lookup"><span data-stu-id="c4ad5-182">Output asset</span></span> |<span data-ttu-id="c4ad5-183">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="c4ad5-183">foo_redacted.mp4</span></span> |<span data-ttu-id="c4ad5-184">Видео с размытием, примененным на основе аннотаций</span><span class="sxs-lookup"><span data-stu-id="c4ad5-184">Video with blurring applied based on annotations</span></span> |

#### <a name="example-output"></a><span data-ttu-id="c4ad5-185">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="c4ad5-185">Example output</span></span>
<span data-ttu-id="c4ad5-186">Это hello вывод Список_идентификаторов с выбран один идентификатор.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-186">This is hello output from an IDList with one ID selected.</span></span>

[<span data-ttu-id="c4ad5-187">См. видео</span><span class="sxs-lookup"><span data-stu-id="c4ad5-187">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

<span data-ttu-id="c4ad5-188">Пример foo_IDList.txt</span><span class="sxs-lookup"><span data-stu-id="c4ad5-188">Example foo_IDList.txt</span></span>
 
     1
     2
     3

## <a name="blur-types"></a><span data-ttu-id="c4ad5-189">Типы размытия</span><span class="sxs-lookup"><span data-stu-id="c4ad5-189">Blur types</span></span>

<span data-ttu-id="c4ad5-190">В hello **объединенное** или **Redact** режиме существует 5 режима разных размытия, можно выбрать через входной конфигурации JSON hello: **Low**, **Med**, **Высокой**, **отладки**, и **черный**.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-190">In hello **Combined** or **Redact** mode, there are 5 different blur modes you can choose from via hello JSON input configuration: **Low**, **Med**, **High**, **Debug**, and **Black**.</span></span> <span data-ttu-id="c4ad5-191">По умолчанию используется режим **Med** (Средний).</span><span class="sxs-lookup"><span data-stu-id="c4ad5-191">By default **Med** is used.</span></span>

<span data-ttu-id="c4ad5-192">Можно найти примеры hello Размытие ниже типы.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-192">You can find samples of hello blur types below.</span></span>

### <a name="example-json"></a><span data-ttu-id="c4ad5-193">Пример JSON:</span><span class="sxs-lookup"><span data-stu-id="c4ad5-193">Example JSON:</span></span>

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a><span data-ttu-id="c4ad5-194">Низкий</span><span class="sxs-lookup"><span data-stu-id="c4ad5-194">Low</span></span>

![Низкий](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a><span data-ttu-id="c4ad5-196">Средний</span><span class="sxs-lookup"><span data-stu-id="c4ad5-196">Med</span></span>

![Средний](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a><span data-ttu-id="c4ad5-198">Высокий</span><span class="sxs-lookup"><span data-stu-id="c4ad5-198">High</span></span>

![Высокий](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a><span data-ttu-id="c4ad5-200">Отладка</span><span class="sxs-lookup"><span data-stu-id="c4ad5-200">Debug</span></span>

![Отладка](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a><span data-ttu-id="c4ad5-202">Черный</span><span class="sxs-lookup"><span data-stu-id="c4ad5-202">Black</span></span>

![Черный](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-hello-output-json-file"></a><span data-ttu-id="c4ad5-204">Элементы hello выходных данных JSON-файла</span><span class="sxs-lookup"><span data-stu-id="c4ad5-204">Elements of hello output JSON file</span></span>

<span data-ttu-id="c4ad5-205">Hello MP исправления предоставляет высокой точности начертания расположение обнаружения и отслеживания для определения вверх too64 человека граней в кадров видео.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-205">hello Redaction MP provides high precision face location detection and tracking that can detect up too64 human faces in a video frame.</span></span> <span data-ttu-id="c4ad5-206">Распознавания фронтальных видов лица предоставляют hello лучшей при боковые и небольшие фрагменты (меньше или равно too24x24 пикселей) требуют.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-206">Frontal faces provide hello best results, while side faces and small faces (less than or equal too24x24 pixels) are challenging.</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a><span data-ttu-id="c4ad5-207">Пример кода .NET</span><span class="sxs-lookup"><span data-stu-id="c4ad5-207">.NET sample code</span></span>

<span data-ttu-id="c4ad5-208">Hello следующей программе показано как:</span><span class="sxs-lookup"><span data-stu-id="c4ad5-208">hello following program shows how to:</span></span>

1. <span data-ttu-id="c4ad5-209">Создание актива и отправка файла мультимедиа в актив hello.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-209">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="c4ad5-210">Создание задания с задачей «исправление» начертания на основе файла конфигурации, содержащий hello, следующая Предустановка json.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-210">Create a job with a face redaction task based on a configuration file that contains hello following json preset.</span></span> 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
3. <span data-ttu-id="c4ad5-211">Загрузка файлов JSON hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="c4ad5-211">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="c4ad5-212">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c4ad5-212">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="c4ad5-213">Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="c4ad5-213">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="c4ad5-214">Пример</span><span class="sxs-lookup"><span data-stu-id="c4ad5-214">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace FaceRedaction
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

            // Run hello FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download hello job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload hello input media file toostorage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference tooAzure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from hello specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify hello input asset.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

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

## <a name="next-steps"></a><span data-ttu-id="c4ad5-215">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c4ad5-215">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c4ad5-216">Отзывы</span><span class="sxs-lookup"><span data-stu-id="c4ad5-216">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="c4ad5-217">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="c4ad5-217">Related links</span></span>
[<span data-ttu-id="c4ad5-218">Общие сведения об аналитике служб мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="c4ad5-218">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="c4ad5-219">Демонстрационные материалы для медиааналитики Azure</span><span class="sxs-lookup"><span data-stu-id="c4ad5-219">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

