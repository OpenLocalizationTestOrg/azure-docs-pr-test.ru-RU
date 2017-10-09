---
title: "aaaDigitize текста с помощью Azure Media Analytics OCR | Документы Microsoft"
description: "Аналитика OCR Azure Media (распознавания) позволяет tooconvert текстовое содержимое в файлы видео в цифровой текст редактируемый, с возможностью поиска.  Это позволяет tooautomate извлечение метаданных может применяться hello из hello видеосигнала мультимедиа."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 307c196e-3a50-4f4b-b982-51585448ffc6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 0476c3ba3942b2c5182a34a429909adbf5c75ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-analytics-tooconvert-text-content-in-video-files-into-digital-text"></a><span data-ttu-id="6e147-104">Используйте Azure медиа-аналитика tooconvert текстовое содержимое в файлы видео в цифровой текст</span><span class="sxs-lookup"><span data-stu-id="6e147-104">Use Azure Media Analytics tooconvert text content in video files into digital text</span></span>
## <a name="overview"></a><span data-ttu-id="6e147-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="6e147-105">Overview</span></span>
<span data-ttu-id="6e147-106">Если нужно tooextract текстового содержимого из видеофайлы и создание цифрового текста для редактирования, с возможностью поиска, следует использовать Azure Media Analytics OCR (распознавание символов).</span><span class="sxs-lookup"><span data-stu-id="6e147-106">If you need tooextract text content from your video files and generate an editable, searchable digital text, you should use Azure Media Analytics OCR (optical character recognition).</span></span> <span data-ttu-id="6e147-107">Этот обработчик мультимедиа Azure обнаруживает текстовое содержимое в видеофайлах и создает текстовые файлы, готовые к использованию.</span><span class="sxs-lookup"><span data-stu-id="6e147-107">This Azure Media Processor detects text content in your video files and generates text files for your use.</span></span> <span data-ttu-id="6e147-108">OCR позволяет вам tooautomate hello извлечение значимых метаданных из hello видеосигнала мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="6e147-108">OCR enables you tooautomate hello extraction of meaningful metadata from hello video signal of your media.</span></span>

<span data-ttu-id="6e147-109">При использовании в сочетании с помощью поисковой системы, можно легко проиндексировать мультимедиа, текст и повышения возможности обнаружения hello содержимого.</span><span class="sxs-lookup"><span data-stu-id="6e147-109">When used in conjunction with a search engine, you can easily index your media by text, and enhance hello discoverability of your content.</span></span> <span data-ttu-id="6e147-110">Это очень полезно, если видео содержит много текста, например, если это видеозапись или снимки экрана какой-либо презентации в режиме слайд-шоу.</span><span class="sxs-lookup"><span data-stu-id="6e147-110">This is extremely useful in highly textual video, like a video recording or screen-capture of a slideshow presentation.</span></span> <span data-ttu-id="6e147-111">Hello обработчика мультимедиа Azure OCR оптимизирован для цифровых текста.</span><span class="sxs-lookup"><span data-stu-id="6e147-111">hello Azure OCR Media Processor is optimized for digital text.</span></span>

<span data-ttu-id="6e147-112">Hello **Azure Media OCR** обработчик мультимедиа в данный момент находится в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="6e147-112">hello **Azure Media OCR** media processor is currently in Preview.</span></span>

<span data-ttu-id="6e147-113">В этом разделе приведены подробные сведения о **Azure Media OCR** и показано, как toouse с помощью пакета SDK служб мультимедиа для .NET.</span><span class="sxs-lookup"><span data-stu-id="6e147-113">This topic gives details about  **Azure Media OCR** and shows how toouse it with Media Services SDK for .NET.</span></span> <span data-ttu-id="6e147-114">Дополнительные сведения и примеры см. в [этом блоге](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span><span class="sxs-lookup"><span data-stu-id="6e147-114">For additional information and examples, see [this blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span></span>

## <a name="ocr-input-files"></a><span data-ttu-id="6e147-115">Входные файлы OCR</span><span class="sxs-lookup"><span data-stu-id="6e147-115">OCR input files</span></span>
<span data-ttu-id="6e147-116">Видеофайлы.</span><span class="sxs-lookup"><span data-stu-id="6e147-116">Video files.</span></span> <span data-ttu-id="6e147-117">В настоящее время поддерживаются следующие форматы hello: MP4, MOV и WMV.</span><span class="sxs-lookup"><span data-stu-id="6e147-117">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration"></a><span data-ttu-id="6e147-118">Конфигурация задачи</span><span class="sxs-lookup"><span data-stu-id="6e147-118">Task configuration</span></span>
<span data-ttu-id="6e147-119">Конфигурация задачи (предустановка).</span><span class="sxs-lookup"><span data-stu-id="6e147-119">Task configuration (preset).</span></span> <span data-ttu-id="6e147-120">При создании задачи с помощью **Azure Media OCR** необходимо указать предустановку конфигурации, используя JSON- или XML-файл.</span><span class="sxs-lookup"><span data-stu-id="6e147-120">When creating a task with **Azure Media OCR**, you must specify a configuration preset using JSON  or XML.</span></span> 

>[!NOTE]
><span data-ttu-id="6e147-121">механизм распознавания текста Hello занимает область изображения с минимальным 40 пикселей toomaximum 32000 как допустимые входные данные в обоих высоты и ширины.</span><span class="sxs-lookup"><span data-stu-id="6e147-121">hello OCR engine only takes an image region with minimum 40 pixels toomaximum 32000 pixels as a valid input in both height/width.</span></span>
>

### <a name="attribute-descriptions"></a><span data-ttu-id="6e147-122">Описания атрибутов</span><span class="sxs-lookup"><span data-stu-id="6e147-122">Attribute descriptions</span></span>
| <span data-ttu-id="6e147-123">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="6e147-123">Attribute name</span></span> | <span data-ttu-id="6e147-124">Описание</span><span class="sxs-lookup"><span data-stu-id="6e147-124">Description</span></span> |
| --- | --- |
|<span data-ttu-id="6e147-125">AdvancedOutput</span><span class="sxs-lookup"><span data-stu-id="6e147-125">AdvancedOutput</span></span>| <span data-ttu-id="6e147-126">Если задать AdvancedOutput tootrue hello JSON выход будет содержать позиционные данные для каждого отдельного слова (в дополнение toophrases и регионы).</span><span class="sxs-lookup"><span data-stu-id="6e147-126">If you set AdvancedOutput tootrue, hello JSON output will contain positional data for every single word (in addition toophrases and regions).</span></span> <span data-ttu-id="6e147-127">Если вы не хотите toosee эти сведения, установите флаг toofalse hello.</span><span class="sxs-lookup"><span data-stu-id="6e147-127">If you do not want toosee these details, set hello flag toofalse.</span></span> <span data-ttu-id="6e147-128">значение по умолчанию Hello имеет значение false.</span><span class="sxs-lookup"><span data-stu-id="6e147-128">hello default value is false.</span></span> <span data-ttu-id="6e147-129">Дополнительную информацию см. в [этом блоге](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span><span class="sxs-lookup"><span data-stu-id="6e147-129">For more information, see [this blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span></span>|
| <span data-ttu-id="6e147-130">Язык</span><span class="sxs-lookup"><span data-stu-id="6e147-130">Language</span></span> |<span data-ttu-id="6e147-131">(необязательно) описание языка hello какие toolook текста.</span><span class="sxs-lookup"><span data-stu-id="6e147-131">(optional) describes hello language of text for which toolook.</span></span> <span data-ttu-id="6e147-132">Одно из следующих hello: автообнаружение (по умолчанию), арабский, китайского, вместе, чешский датский, голландский, английский, финский, французский, немецкий, греческий, венгерский, итальянский, японский, корейский, норвежский, польский, португальский, румынский, русский, SerbianCyrillic, SerbianLatin, словацкий, испанский, шведский, турецкий.</span><span class="sxs-lookup"><span data-stu-id="6e147-132">One of hello following: AutoDetect (default), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German,  Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span></span> |
| <span data-ttu-id="6e147-133">TextOrientation</span><span class="sxs-lookup"><span data-stu-id="6e147-133">TextOrientation</span></span> |<span data-ttu-id="6e147-134">(необязательно) описание hello ориентацию текста для какой toolook.</span><span class="sxs-lookup"><span data-stu-id="6e147-134">(optional) describes hello orientation of text for which toolook.</span></span>  <span data-ttu-id="6e147-135">«Левый» означает, что hello вверху все буквы указывают указатели по направлению к левому hello.</span><span class="sxs-lookup"><span data-stu-id="6e147-135">"Left" means that hello top of all letters are pointed towards hello left.</span></span>  <span data-ttu-id="6e147-136">По умолчанию текст (как, например, в книге) имеет ориентацию "Up", то есть буквы направлены вверх.</span><span class="sxs-lookup"><span data-stu-id="6e147-136">Default text (like that which can be found in a book) can be called "Up" oriented.</span></span>  <span data-ttu-id="6e147-137">Одно из следующих hello: автообнаружение (по умолчанию), до, правой, вниз, влево.</span><span class="sxs-lookup"><span data-stu-id="6e147-137">One of hello following: AutoDetect (default), Up, Right, Down, Left.</span></span> |
| <span data-ttu-id="6e147-138">TimeInterval</span><span class="sxs-lookup"><span data-stu-id="6e147-138">TimeInterval</span></span> |<span data-ttu-id="6e147-139">(необязательно) описание hello частоту выборки.</span><span class="sxs-lookup"><span data-stu-id="6e147-139">(optional) describes hello sampling rate.</span></span>  <span data-ttu-id="6e147-140">Значение по умолчанию — каждые полсекунды.</span><span class="sxs-lookup"><span data-stu-id="6e147-140">Default is every 1/2 second.</span></span><br/><span data-ttu-id="6e147-141">Формат JSON — ЧЧ:мм:сс.ССС (по умолчанию — 00:00:00.500)</span><span class="sxs-lookup"><span data-stu-id="6e147-141">JSON format – HH:mm:ss.SSS (default 00:00:00.500)</span></span><br/><span data-ttu-id="6e147-142">Формат XML: минимальная длительность W3C XSD (по умолчанию — PT0.5).</span><span class="sxs-lookup"><span data-stu-id="6e147-142">XML format – W3C XSD duration primitive (default PT0.5)</span></span> |
| <span data-ttu-id="6e147-143">DetectRegions</span><span class="sxs-lookup"><span data-stu-id="6e147-143">DetectRegions</span></span> |<span data-ttu-id="6e147-144">(необязательно) Массив объектов DetectRegion указания областей в пределах кадра видео hello в какой toodetect текст.</span><span class="sxs-lookup"><span data-stu-id="6e147-144">(optional) An array of DetectRegion objects specifying regions within hello video frame in which toodetect text.</span></span><br/><span data-ttu-id="6e147-145">Объект DetectRegion состоит из hello следующие четыре целочисленных значений:</span><span class="sxs-lookup"><span data-stu-id="6e147-145">A DetectRegion object is made of hello following four integer values:</span></span><br/><span data-ttu-id="6e147-146">Left — пикселей от левого поля hello</span><span class="sxs-lookup"><span data-stu-id="6e147-146">Left – pixels from hello left-margin</span></span><br/><span data-ttu-id="6e147-147">Начало — пикселей верхнее hello</span><span class="sxs-lookup"><span data-stu-id="6e147-147">Top – pixels from hello top-margin</span></span><br/><span data-ttu-id="6e147-148">Ширина: ширина области hello в пикселях</span><span class="sxs-lookup"><span data-stu-id="6e147-148">Width – width of hello region in pixels</span></span><br/><span data-ttu-id="6e147-149">Высота: высота области hello в пикселях</span><span class="sxs-lookup"><span data-stu-id="6e147-149">Height – height of hello region in pixels</span></span> |

#### <a name="json-preset-example"></a><span data-ttu-id="6e147-150">Пример предустановки JSON</span><span class="sxs-lookup"><span data-stu-id="6e147-150">JSON preset example</span></span>

    {
        "Version":1.0, 
        "Options": 
        {
            "AdvancedOutput":"true",
            "Language":"English", 
            "TimeInterval":"00:00:01.5",
            "TextOrientation":"Up",
            "DetectRegions": [
                    {
                       "Left": 10,
                       "Top": 10,
                       "Width": 100,
                       "Height": 50
                    }
             ]
        }
    }


#### <a name="xml-preset-example"></a><span data-ttu-id="6e147-151">Пример предустановки XML</span><span class="sxs-lookup"><span data-stu-id="6e147-151">XML preset example</span></span>
    <?xml version=""1.0"" encoding=""utf-16""?>
    <VideoOcrPreset xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" Version=""1.0"" xmlns=""http://www.windowsazure.com/media/encoding/Preset/2014/03"">
      <Options>
         <AdvancedOutput>true</AdvancedOutput>
         <Language>English</Language>
         <TimeInterval>PT1.5S</TimeInterval>
         <DetectRegions>
             <DetectRegion>
                   <Left>10</Left>
                   <Top>10</Top>
                   <Width>100</Width>
                   <Height>50</Height>
            </DetectRegion>
       </DetectRegions>
       <TextOrientation>Up</TextOrientation>
      </Options>
    </VideoOcrPreset>

## <a name="ocr-output-files"></a><span data-ttu-id="6e147-152">Выходные файлы OCR</span><span class="sxs-lookup"><span data-stu-id="6e147-152">OCR output files</span></span>
<span data-ttu-id="6e147-153">выходные данные Hello обработчик мультимедиа OCR hello является файлом JSON.</span><span class="sxs-lookup"><span data-stu-id="6e147-153">hello output of hello OCR media processor is a JSON file.</span></span>

### <a name="elements-of-hello-output-json-file"></a><span data-ttu-id="6e147-154">Элементы hello выходных данных JSON-файла</span><span class="sxs-lookup"><span data-stu-id="6e147-154">Elements of hello output JSON file</span></span>
<span data-ttu-id="6e147-155">Выход видео OCR Hello обеспечивает время сегментированных данных на hello символы, входящие в видео.</span><span class="sxs-lookup"><span data-stu-id="6e147-155">hello Video OCR output provides time-segmented data on hello characters found in your video.</span></span>  <span data-ttu-id="6e147-156">Можно использовать атрибуты, такие как язык или ориентацией toohone в точно hello слов, которые нужно в анализ.</span><span class="sxs-lookup"><span data-stu-id="6e147-156">You can use attributes such as language or orientation toohone-in on exactly hello words that you are interested in analyzing.</span></span> 

<span data-ttu-id="6e147-157">Hello выходные данные содержат hello следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="6e147-157">hello output contains hello following attributes:</span></span>

| <span data-ttu-id="6e147-158">Элемент</span><span class="sxs-lookup"><span data-stu-id="6e147-158">Element</span></span> | <span data-ttu-id="6e147-159">Описание</span><span class="sxs-lookup"><span data-stu-id="6e147-159">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6e147-160">Шкала времени</span><span class="sxs-lookup"><span data-stu-id="6e147-160">Timescale</span></span> |<span data-ttu-id="6e147-161">«тактах» в секунду hello видео</span><span class="sxs-lookup"><span data-stu-id="6e147-161">"ticks" per second of hello video</span></span> |
| <span data-ttu-id="6e147-162">Offset</span><span class="sxs-lookup"><span data-stu-id="6e147-162">Offset</span></span> |<span data-ttu-id="6e147-163">Смещение времени для отметки времени.</span><span class="sxs-lookup"><span data-stu-id="6e147-163">time offset for timestamps.</span></span> <span data-ttu-id="6e147-164">В API видео версии 1.0 это значение всегда равно 0.</span><span class="sxs-lookup"><span data-stu-id="6e147-164">In version 1.0 of Video APIs, this will always be 0.</span></span> |
| <span data-ttu-id="6e147-165">Framerate</span><span class="sxs-lookup"><span data-stu-id="6e147-165">Framerate</span></span> |<span data-ttu-id="6e147-166">Кадров в секунду hello видео</span><span class="sxs-lookup"><span data-stu-id="6e147-166">Frames per second of hello video</span></span> |
| <span data-ttu-id="6e147-167">width</span><span class="sxs-lookup"><span data-stu-id="6e147-167">width</span></span> |<span data-ttu-id="6e147-168">Ширина hello видео в пикселях</span><span class="sxs-lookup"><span data-stu-id="6e147-168">width of hello video in pixels</span></span> |
| <span data-ttu-id="6e147-169">height</span><span class="sxs-lookup"><span data-stu-id="6e147-169">height</span></span> |<span data-ttu-id="6e147-170">Высота изображения в пикселях hello</span><span class="sxs-lookup"><span data-stu-id="6e147-170">height of hello video in pixels</span></span> |
| <span data-ttu-id="6e147-171">Fragments</span><span class="sxs-lookup"><span data-stu-id="6e147-171">Fragments</span></span> |<span data-ttu-id="6e147-172">Массив из фрагментов видео, в которой hello фрагментирован метаданных на основе времени</span><span class="sxs-lookup"><span data-stu-id="6e147-172">array of time-based chunks of video into which hello metadata is chunked</span></span> |
| <span data-ttu-id="6e147-173">start</span><span class="sxs-lookup"><span data-stu-id="6e147-173">start</span></span> |<span data-ttu-id="6e147-174">Время начала фрагмента в тактах</span><span class="sxs-lookup"><span data-stu-id="6e147-174">start time of a fragment in "ticks"</span></span> |
| <span data-ttu-id="6e147-175">длительность</span><span class="sxs-lookup"><span data-stu-id="6e147-175">duration</span></span> |<span data-ttu-id="6e147-176">Продолжительность фрагмента в тактах</span><span class="sxs-lookup"><span data-stu-id="6e147-176">length of a fragment in "ticks"</span></span> |
| <span data-ttu-id="6e147-177">interval</span><span class="sxs-lookup"><span data-stu-id="6e147-177">interval</span></span> |<span data-ttu-id="6e147-178">Интервал каждого события в пределах заданного фрагмента hello</span><span class="sxs-lookup"><span data-stu-id="6e147-178">interval of each event within hello given fragment</span></span> |
| <span data-ttu-id="6e147-179">events</span><span class="sxs-lookup"><span data-stu-id="6e147-179">events</span></span> |<span data-ttu-id="6e147-180">Массив, содержащий области</span><span class="sxs-lookup"><span data-stu-id="6e147-180">array containing regions</span></span> |
| <span data-ttu-id="6e147-181">region</span><span class="sxs-lookup"><span data-stu-id="6e147-181">region</span></span> |<span data-ttu-id="6e147-182">Объект, представляющий обнаруженные слова или фразы</span><span class="sxs-lookup"><span data-stu-id="6e147-182">object representing detected words or phrases</span></span> |
| <span data-ttu-id="6e147-183">Язык</span><span class="sxs-lookup"><span data-stu-id="6e147-183">language</span></span> |<span data-ttu-id="6e147-184">язык обнаружена в области текста hello</span><span class="sxs-lookup"><span data-stu-id="6e147-184">language of hello text detected within a region</span></span> |
| <span data-ttu-id="6e147-185">orientation</span><span class="sxs-lookup"><span data-stu-id="6e147-185">orientation</span></span> |<span data-ttu-id="6e147-186">ориентацию текста hello обнаружена в области</span><span class="sxs-lookup"><span data-stu-id="6e147-186">orientation of hello text detected within a region</span></span> |
| <span data-ttu-id="6e147-187">lines</span><span class="sxs-lookup"><span data-stu-id="6e147-187">lines</span></span> |<span data-ttu-id="6e147-188">Массив строк текста, обнаруженного в пределах области</span><span class="sxs-lookup"><span data-stu-id="6e147-188">array of lines of text detected within a region</span></span> |
| <span data-ttu-id="6e147-189">text</span><span class="sxs-lookup"><span data-stu-id="6e147-189">text</span></span> |<span data-ttu-id="6e147-190">Фактический текст Hello</span><span class="sxs-lookup"><span data-stu-id="6e147-190">hello actual text</span></span> |

### <a name="json-output-example"></a><span data-ttu-id="6e147-191">Пример выходных данных JSON</span><span class="sxs-lookup"><span data-stu-id="6e147-191">JSON output example</span></span>
<span data-ttu-id="6e147-192">Hello следующий пример выходных данных содержит общие сведения видео hello и несколько фрагментов видео.</span><span class="sxs-lookup"><span data-stu-id="6e147-192">hello following output example contains hello general video information and several video fragments.</span></span> <span data-ttu-id="6e147-193">В каждый фрагмент видео в нем каждого региона, в которой обнаружен OCR MP с языком hello и его ориентацию текста.</span><span class="sxs-lookup"><span data-stu-id="6e147-193">In every video fragment, it contains every region which is detected by OCR MP with hello language and its text orientation.</span></span> <span data-ttu-id="6e147-194">Hello область также содержит каждой строки слова в этом регионе с текстом hello строки, положение строки hello и сведения каждого word (содержимого word, положение и достоверности) в этой строке.</span><span class="sxs-lookup"><span data-stu-id="6e147-194">hello region also contains every word line in this region with hello line’s text, hello line’s position, and every word information (word content, position and confidence) in this line.</span></span> <span data-ttu-id="6e147-195">Hello ниже приведен пример и переводе некоторые встроенные комментарии.</span><span class="sxs-lookup"><span data-stu-id="6e147-195">hello following is an example, and I put some comments inline.</span></span>

    {
        "version": 1, 
        "timescale": 90000, 
        "offset": 0, 
        "framerate": 30, 
        "width": 640, 
        "height": 480,  // general video information
        "fragments": [
            {
                "start": 0, 
                "duration": 180000, 
                "interval": 90000,  // hello time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // hello detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including hello text and hello position
                                    {
                                        "text": "One Two", 
                                        "left": 10, 
                                        "top": 10, 
                                        "right": 210, 
                                        "bottom": 110, 
                                        "word": [  // word information array in this line
                                            {
                                                "text": "One", 
                                                "left": 10, 
                                                "top": 10, 
                                                "right": 110, 
                                                "bottom": 110, 
                                                "confidence": 900
                                            }, 
                                            {
                                                "text": "Two", 
                                                "left": 110, 
                                                "top": 10, 
                                                "right": 210, 
                                                "bottom": 110, 
                                                "confidence": 910
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                ]
            }
        ]
    }

## <a name="net-sample-code"></a><span data-ttu-id="6e147-196">Пример кода .NET</span><span class="sxs-lookup"><span data-stu-id="6e147-196">.NET sample code</span></span>

<span data-ttu-id="6e147-197">Hello следующей программе показано как:</span><span class="sxs-lookup"><span data-stu-id="6e147-197">hello following program shows how to:</span></span>

1. <span data-ttu-id="6e147-198">Создание актива и отправка файла мультимедиа в актив hello.</span><span class="sxs-lookup"><span data-stu-id="6e147-198">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="6e147-199">Создание задания с помощью файла конфигурации или файла предустановки OCR.</span><span class="sxs-lookup"><span data-stu-id="6e147-199">Create a job with an OCR configuration/preset file.</span></span>
3. <span data-ttu-id="6e147-200">Загрузка файлов JSON hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="6e147-200">Download hello output JSON files.</span></span> 
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="6e147-201">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6e147-201">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="6e147-202">Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="6e147-202">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="6e147-203">Пример</span><span class="sxs-lookup"><span data-stu-id="6e147-203">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace OCR
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

                // Run hello OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference tooAzure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="6e147-204">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="6e147-204">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6e147-205">Отзывы</span><span class="sxs-lookup"><span data-stu-id="6e147-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="6e147-206">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="6e147-206">Related links</span></span>
[<span data-ttu-id="6e147-207">Общие сведения об аналитике служб мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="6e147-207">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

