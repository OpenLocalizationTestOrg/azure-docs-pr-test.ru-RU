---
title: "Настройка предустановок MES для расширенного кодирования | Документация Майкрософт"
description: "В этом разделе показано, как выполнять расширенные задачи кодирования, настраивая предустановки задач Media Encoder Standard."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 2a4ade25-e600-4bce-a66e-e29cf4a38369
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 8de3bdd45261c84a0e1bb90f1c58863ad740dd5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a><span data-ttu-id="2a33f-103">Настройка предустановок MES для расширенного кодирования</span><span class="sxs-lookup"><span data-stu-id="2a33f-103">Perform advanced encoding by customizing MES presets</span></span> 

## <a name="overview"></a><span data-ttu-id="2a33f-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="2a33f-104">Overview</span></span>

<span data-ttu-id="2a33f-105">В этом разделе показано, как настроить предустановки Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="2a33f-105">This topic shows how to customize Media Encoder Standard presets.</span></span> <span data-ttu-id="2a33f-106">В разделе [Настройка предустановок Media Encoder Standard](media-services-custom-mes-presets-with-dotnet.md) показано, как использовать .NET для создания задачи кодирования и задания, которое выполняет эту задачу.</span><span class="sxs-lookup"><span data-stu-id="2a33f-106">The [Encoding with Media Encoder Standard using custom presets](media-services-custom-mes-presets-with-dotnet.md) topic shows how to use .NET to create an encoding task and a job that executes this task.</span></span> <span data-ttu-id="2a33f-107">Настроив предустановку, укажите пользовательские предустановки для задачи кодирования.</span><span class="sxs-lookup"><span data-stu-id="2a33f-107">Once you customize a preset, supply the custom presets to the encoding task.</span></span> 

>[!NOTE]
><span data-ttu-id="2a33f-108">При использовании предустановки XML обязательно сохраните порядок элементов, как показано в примерах XML ниже (например, элемент KeyFrameInterval должен предшествовать элементу SceneChangeDetection).</span><span class="sxs-lookup"><span data-stu-id="2a33f-108">If using an XML preset, make sure to preserve the order of elements, as shown in XML samples below (for example, KeyFrameInterval should precede SceneChangeDetection).</span></span>
>

<span data-ttu-id="2a33f-109">В этом разделе демонстрируются пользовательские предустановки, которые выполняют следующие задачи кодирования.</span><span class="sxs-lookup"><span data-stu-id="2a33f-109">In this topic, the custom presets that perform the following encoding tasks are demonstrated.</span></span>

## <a name="support-for-relative-sizes"></a><span data-ttu-id="2a33f-110">Поддержка относительных размеров</span><span class="sxs-lookup"><span data-stu-id="2a33f-110">Support for relative sizes</span></span>

<span data-ttu-id="2a33f-111">При создании эскизов вам не нужно всегда указывать выходную ширину и высоту в пикселях.</span><span class="sxs-lookup"><span data-stu-id="2a33f-111">When generating thumbnails, you do not need to always specify output width and height in pixels.</span></span> <span data-ttu-id="2a33f-112">Эти значения можно указать в процентах, используя диапазон [1%, ..., 100%].</span><span class="sxs-lookup"><span data-stu-id="2a33f-112">You can specify them in percentages, in the range [1%, …, 100%].</span></span>

### <a name="json-preset"></a><span data-ttu-id="2a33f-113">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="2a33f-113">JSON preset</span></span>
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a><span data-ttu-id="2a33f-114">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="2a33f-114">XML preset</span></span>
    <Width>100%</Width>
    <Height>100%</Height>

## <span data-ttu-id="2a33f-115"><a id="thumbnails"></a>Создание эскизов</span><span class="sxs-lookup"><span data-stu-id="2a33f-115"><a id="thumbnails"></a>Generate thumbnails</span></span>

<span data-ttu-id="2a33f-116">В этом разделе показано, как настроить предустановку, которая создает эскизы.</span><span class="sxs-lookup"><span data-stu-id="2a33f-116">This section shows how to customize a preset that generates thumbnails.</span></span> <span data-ttu-id="2a33f-117">Предустановка, определенная ниже, содержит сведения о том, как должен кодироваться файл, а также сведения, необходимые для создания эскизов.</span><span class="sxs-lookup"><span data-stu-id="2a33f-117">The preset defined below contains information on how you want to encode your file as well as information needed to generate thumbnails.</span></span> <span data-ttu-id="2a33f-118">Вы можете использовать любую из предустановок Media Encoder Standard (MES), которые приведены в [этом](media-services-mes-presets-overview.md) разделе, и добавить в нее код для создания эскизов.</span><span class="sxs-lookup"><span data-stu-id="2a33f-118">You can take any of the MES presets documented [this](media-services-mes-presets-overview.md) section and add code that generates thumbnails.</span></span>  

> [!NOTE]
> <span data-ttu-id="2a33f-119">Если видео преобразуется в односкоростной формат, параметр **SceneChangeDetection** в следующей конфигурации может иметь только значение True.</span><span class="sxs-lookup"><span data-stu-id="2a33f-119">The **SceneChangeDetection** setting in the following preset can only be set to true if you are encoding to a single  bitrate video.</span></span> <span data-ttu-id="2a33f-120">Если видео преобразуется в формат с несколькими скоростями, а параметр **SceneChangeDetection** имеет значение True, то кодировщик выдает ошибку.</span><span class="sxs-lookup"><span data-stu-id="2a33f-120">If you are encoding to a multi-bitrate video and set **SceneChangeDetection** to true, the encoder returns an error.</span></span>  
>
>

<span data-ttu-id="2a33f-121">Сведения о схеме см. [здесь](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="2a33f-121">For information about schema, see [this](media-services-mes-schema.md) topic.</span></span>

<span data-ttu-id="2a33f-122">Обязательно изучите раздел [Рекомендации](#considerations) .</span><span class="sxs-lookup"><span data-stu-id="2a33f-122">Make sure to review the [Considerations](#considerations) section.</span></span>

### <span data-ttu-id="2a33f-123"><a id="json"></a>Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="2a33f-123"><a id="json"></a>JSON preset</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"

            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": 640,
              "Height": 360,
            }
          ],
          "Start": "00:00:01",
          "Step": "00:00:10",
          "Range": "00:00:58",
          "Type": "PngImage"
        },
        {
          "BmpLayers": [
            {
              "Type": "BmpLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "10%",
          "Step": "10%",
          "Range": "90%",
          "Type": "BmpImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "BmpFormat"
          }
        },
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <span data-ttu-id="2a33f-124"><a id="xml"></a>Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="2a33f-124"><a id="xml"></a>XML preset</span></span>
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <SceneChangeDetection>true</SceneChangeDetection>
          <H264Layers>
            <H264Layer>
              <Bitrate>4500</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>4500</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>640</Width>
              <Height>360</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
        <BmpImage Start="10%" Step="10%" Range="90%">
          <BmpLayers>
            <BmpLayer>
              <Width>640</Width>
              <Height>360</Height>
            </BmpLayer>
          </BmpLayers>
        </BmpImage>
        <PngImage Start="00:00:01" Step="00:00:10" Range="00:00:58">
          <PngLayers>
            <PngLayer>
              <Width>640</Width>
              <Height>360</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <BmpFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

### <a name="considerations"></a><span data-ttu-id="2a33f-125">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="2a33f-125">Considerations</span></span>

<span data-ttu-id="2a33f-126">Действительны следующие условия.</span><span class="sxs-lookup"><span data-stu-id="2a33f-126">The following considerations apply:</span></span>

* <span data-ttu-id="2a33f-127">Использование явных меток времени для элементов Start, Step или Range предполагает, что входные данные составляют не менее одной минуты.</span><span class="sxs-lookup"><span data-stu-id="2a33f-127">The use of explicit timestamps for Start/Step/Range assumes that the input source is at least 1 minute long.</span></span>
* <span data-ttu-id="2a33f-128">Элементы Jpg, Png и BmpImage обладают строковыми атрибутами Start, Step и Range, которые можно интерпретировать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2a33f-128">Jpg/Png/BmpImage elements have Start, Step, and Range string attributes – these can be interpreted as:</span></span>

  * <span data-ttu-id="2a33f-129">номер кадра, если эти атрибуты выражены неотрицательными целыми числами, например "Start": "120";</span><span class="sxs-lookup"><span data-stu-id="2a33f-129">Frame Number if they are non-negative integers, for example "Start": "120",</span></span>
  * <span data-ttu-id="2a33f-130">значение относительно длительности источника, если атрибуты указаны с суффиксом "%", например "Start": "15%";</span><span class="sxs-lookup"><span data-stu-id="2a33f-130">Relative to source duration if expressed as %-suffixed, for example "Start": "15%", OR</span></span>
  * <span data-ttu-id="2a33f-131">Отметка времени, если атрибуты имеют формат</span><span class="sxs-lookup"><span data-stu-id="2a33f-131">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="2a33f-132">ЧЧ:ММ:СС, например "Start" : "00:01:00".</span><span class="sxs-lookup"><span data-stu-id="2a33f-132">format, for example "Start" : "00:01:00"</span></span>

    <span data-ttu-id="2a33f-133">При желании условные обозначения можно комбинировать.</span><span class="sxs-lookup"><span data-stu-id="2a33f-133">You can mix and match notations as you please.</span></span>

    <span data-ttu-id="2a33f-134">Кроме того, атрибут Start поддерживает также специальный макрос {Best}, который пытается определить первый "интересный" кадр содержимого NOTE: (если атрибут Start имеет значение {Best}, атрибуты Step и Range игнорируются)</span><span class="sxs-lookup"><span data-stu-id="2a33f-134">Additionally, Start also supports a special Macro:{Best}, which attempts to determine the first “interesting” frame of the content NOTE: (Step and Range are ignored when Start is set to {Best})</span></span>
  * <span data-ttu-id="2a33f-135">По умолчанию Start:{Best}</span><span class="sxs-lookup"><span data-stu-id="2a33f-135">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="2a33f-136">Для атрибута Image должен быть указан формат выходных данных: Jpg/Png/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="2a33f-136">Output format needs to be explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="2a33f-137">Если он присутствует, Media Encoder Standard сопоставляет JpgVideo с JpgFormat и т. д.</span><span class="sxs-lookup"><span data-stu-id="2a33f-137">When present, MES matches JpgVideo to JpgFormat and so on.</span></span> <span data-ttu-id="2a33f-138">OutputFormat представляет новый макрос, связанный с кодеком изображений: {Index}, который необходимо указывать для форматов вывода изображений (один и только один раз).</span><span class="sxs-lookup"><span data-stu-id="2a33f-138">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs to be present (once and only once) for image output formats.</span></span>

## <span data-ttu-id="2a33f-139"><a id="trim_video"></a>Монтаж видео (обрезка)</span><span class="sxs-lookup"><span data-stu-id="2a33f-139"><a id="trim_video"></a>Trim a video (clipping)</span></span>
<span data-ttu-id="2a33f-140">В этом разделе рассказывается об изменении предустановок кодировщика для обрезки входного видеоролика, при котором входной видеоролик представляет собой так называемый мезонинный файл или файл по требованию.</span><span class="sxs-lookup"><span data-stu-id="2a33f-140">This section talks about modifying the encoder presets to clip or trim the input video where the input is a so-called mezzanine file or on-demand file.</span></span> <span data-ttu-id="2a33f-141">Кодировщик может также использоваться для обрезки ресурса-контейнера, который записывается или архивируется из потока в реальном времени. Подробные сведения об этом см. в [этом блоге](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="2a33f-141">The encoder can also be used to clip or trim an asset, which is captured or archived from a live stream – the details for this are available in [this blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span></span>

<span data-ttu-id="2a33f-142">Для обрезки видео можно взять любую из предустановок стандартного кодировщика мультимедиа, которые описаны в [этом](media-services-mes-presets-overview.md) разделе, и изменить элемент **Sources** (как показано ниже).</span><span class="sxs-lookup"><span data-stu-id="2a33f-142">To trim your videos, you can take any of the MES presets documented [this](media-services-mes-presets-overview.md) section and modify the **Sources** element (as shown below).</span></span> <span data-ttu-id="2a33f-143">Значение StartTime должно соответствовать абсолютной метке времени входящего видео.</span><span class="sxs-lookup"><span data-stu-id="2a33f-143">The value of StartTime needs to match the absolute timestamps of the input video.</span></span> <span data-ttu-id="2a33f-144">Например, если первый кадр входящего видео имеет отметку времени "12:00:10.000", значение StartTime должно равняться или быть больше 12:00:10.000.</span><span class="sxs-lookup"><span data-stu-id="2a33f-144">For example, if the first frame of the input video has a timestamp of 12:00:10.000, then StartTime should be at least 12:00:10.000 and greater.</span></span> <span data-ttu-id="2a33f-145">В приведенном ниже примере мы предполагаем, что входящее видео имеет отметку времени начала, равную нулю.</span><span class="sxs-lookup"><span data-stu-id="2a33f-145">In the example below, we assume that the input video has a starting timestamp of zero.</span></span> <span data-ttu-id="2a33f-146">**Sources** должен размещаться в начале предустановки.</span><span class="sxs-lookup"><span data-stu-id="2a33f-146">**Sources** should be placed at the beginning of the preset.</span></span>

### <span data-ttu-id="2a33f-147"><a id="json"></a>Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="2a33f-147"><a id="json"></a>JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "StartTime": "00:00:04",
          "Duration": "00:00:16"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1500,
              "MaxBitrate": 1500,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1000,
              "MaxBitrate": 1000,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 650,
              "MaxBitrate": 650,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 400,
              "MaxBitrate": 400,
              "BufferWindow": "00:00:05",
              "Width": 320,
              "Height": 180,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="xml-preset"></a><span data-ttu-id="2a33f-148">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="2a33f-148">XML preset</span></span>
<span data-ttu-id="2a33f-149">Для обрезки видео можно взять любую из предустановок стандартного кодировщика мультимедиа, которые описаны [здесь](media-services-mes-presets-overview.md) , и изменить элемент **Sources** (как показано ниже).</span><span class="sxs-lookup"><span data-stu-id="2a33f-149">To trim your videos, you can take any of the MES presets documented [here](media-services-mes-presets-overview.md) and modify the **Sources** element (as shown below).</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source StartTime="PT4S" Duration="PT14S"/>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>3400</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>3400</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>2250</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>2250</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1500</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1500</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1000</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1000</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>650</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>650</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>400</Bitrate>
              <Width>320</Width>
              <Height>180</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>400</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>

## <span data-ttu-id="2a33f-150"><a id="overlay"></a>Создание наложения</span><span class="sxs-lookup"><span data-stu-id="2a33f-150"><a id="overlay"></a>Create an overlay</span></span>

<span data-ttu-id="2a33f-151">Стандартный кодировщик служб мультимедиа позволяет наложить изображение на существующее видео.</span><span class="sxs-lookup"><span data-stu-id="2a33f-151">The Media Encoder Standard allows you to overlay an image onto an existing video.</span></span> <span data-ttu-id="2a33f-152">В настоящее время поддерживаются следующие форматы: png, jpg, gif и bmp.</span><span class="sxs-lookup"><span data-stu-id="2a33f-152">Currently, the following formats are supported: png, jpg, gif, and bmp.</span></span> <span data-ttu-id="2a33f-153">Предустановка, определенная ниже, представляет собой базовый пример наложения видео.</span><span class="sxs-lookup"><span data-stu-id="2a33f-153">The preset defined below is a basic example  of a video overlay.</span></span>

<span data-ttu-id="2a33f-154">Наряду с определением файла предустановки также необходимо сообщить службам мультимедиа, какой файл в ресурсе-контейнере содержит изображение для наложения, а какой — исходное видео, на которое вы хотите наложить изображение.</span><span class="sxs-lookup"><span data-stu-id="2a33f-154">In addition to defining a preset file, you also have to let Media Services know which file in the asset is the overlay image and which file is the source video onto which you want to overlay the image.</span></span> <span data-ttu-id="2a33f-155">Видеофайл должен быть **первичным** файлом.</span><span class="sxs-lookup"><span data-stu-id="2a33f-155">The video file has to be the **primary** file.</span></span>

<span data-ttu-id="2a33f-156">При использовании .NET добавьте две приведенные ниже функции в пример .NET, определенный в [этом](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) разделе.</span><span class="sxs-lookup"><span data-stu-id="2a33f-156">If you are using .NET, add the following two functions to the .NET example defined in [this](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic.</span></span> <span data-ttu-id="2a33f-157">Функция **UploadMediaFilesFromFolder** передает файлы из папки (например, BigBuckBunny.mp4 и Image001.png) и задает MP4-файл в качестве первичного файла в ресурсе-контейнере.</span><span class="sxs-lookup"><span data-stu-id="2a33f-157">The **UploadMediaFilesFromFolder** function uploads files from a folder (for example, BigBuckBunny.mp4 and Image001.png) and sets the mp4 file to be the primary file in the asset.</span></span> <span data-ttu-id="2a33f-158">Функция **EncodeWithOverlay** использует настраиваемый файл предустановки, который был передан в нее (например, приведенную ниже предустановку), для создания задачи кодирования.</span><span class="sxs-lookup"><span data-stu-id="2a33f-158">The **EncodeWithOverlay** function uses the custom preset file that was passed to it (for example, the preset that follows) to create the encoding task.</span></span>


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // The following code assumes 
            // you have an input folder with one MP4 and one overlay image file.
            if (af.Name.Contains(".mp4"))
                af.IsPrimary = true;
            else
                af.IsPrimary = false;
    
            af.Update();
        }
    
        return asset;
    }

    static public IAsset EncodeWithOverlay(IAsset assetSource, string customPresetFileName)
    {
        // Declare a new job.
        IJob job = _context.Jobs.Create("Media Encoder Standard Job");
        // Get a media processor reference, and pass to it the name of the 
        // processor to use for the specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load the XML (or JSON) from the local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify the input assets to be encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset to contain the results of the job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> <span data-ttu-id="2a33f-159">Текущие ограничения:</span><span class="sxs-lookup"><span data-stu-id="2a33f-159">Current limitations:</span></span>
>
> <span data-ttu-id="2a33f-160">Настройка прозрачности наложения не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="2a33f-160">The overlay opacity setting is not supported.</span></span>
>
> <span data-ttu-id="2a33f-161">Исходный видеофайл и файл образа наложения должны находиться в одном ресурсе, причем видеофайл должен быть задан как основной файл в этом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="2a33f-161">Your source video file and the overlay image file have to be in the same asset, and the video file needs to be set as the primary file in this asset.</span></span>
>
>

### <a name="json-preset"></a><span data-ttu-id="2a33f-162">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="2a33f-162">JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "VideoOverlay": {
              "Position": {
                "X": 100,
                "Y": 100,
                "Width": 100,
                "Height": 50
              },
              "AudioGainLevel": 0.0,
              "MediaParams": [
                {
                  "OverlayLoopCount": 1
                },
                {
                  "IsOverlay": true,
                  "OverlayLoopCount": 1,
                  "InputLoop": true
                }
              ],
              "Source": "Image001.png",
              "Clip": {
                "Duration": "00:00:05"
              },
              "FadeInDuration": {
                "Duration": "00:00:01"
              },
              "FadeOutDuration": {
                "StartTime": "00:00:03",
                "Duration": "00:00:04"
              }
            }
          },
          "Pad": true
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1045,
              "MaxBitrate": 1045,
              "BufferWindow": "00:00:05",
              "ReferenceFrames": 3,
              "EntropyMode": "Cavlc",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Type": "CopyAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}{Extension}",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a name="xml-preset"></a><span data-ttu-id="2a33f-163">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="2a33f-163">XML preset</span></span>
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source>
          <Streams />
          <Filters>
            <VideoOverlay>
              <Source>Image001.png</Source>
              <Clip Duration="PT5S" />
              <FadeInDuration Duration="PT1S" />
              <FadeOutDuration StartTime="PT3S" Duration="PT4S" />
              <Position X="100" Y="100" Width="100" Height="50" />
              <Opacity>0</Opacity>
              <AudioGainLevel>0</AudioGainLevel>
              <MediaParams>
                <MediaParam>
                  <IsOverlay>false</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>false</InputLoop>
                </MediaParam>
                <MediaParam>
                  <IsOverlay>true</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>true</InputLoop>
                </MediaParam>
              </MediaParams>
            </VideoOverlay>
          </Filters>
          <Pad>true</Pad>
        </Source>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>1045</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>0</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cavlc</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1045</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <CopyAudio />
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}{Extension}">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>


## <span data-ttu-id="2a33f-164"><a id="silent_audio"></a>Вставка звуковой дорожки с тишиной, если входные данные не содержат звука</span><span class="sxs-lookup"><span data-stu-id="2a33f-164"><a id="silent_audio"></a>Insert a silent audio track when input has no audio</span></span>
<span data-ttu-id="2a33f-165">По умолчанию при отправке кодировщику входных данных, которые содержат только видео и не содержат звука, выходной ресурс-контейнер будет содержать файлы только с видеоданными.</span><span class="sxs-lookup"><span data-stu-id="2a33f-165">By default, if you send an input to the encoder that contains only video, and no audio, then the output asset contains files that contain only video data.</span></span> <span data-ttu-id="2a33f-166">Некоторые проигрыватели не смогут обработать такие выходные потоки.</span><span class="sxs-lookup"><span data-stu-id="2a33f-166">Some players may not be able to handle such output streams.</span></span> <span data-ttu-id="2a33f-167">Этот параметр можно использовать для принудительного добавления кодировщиком звуковой дорожки с тишиной к выходным данным в этом сценарии.</span><span class="sxs-lookup"><span data-stu-id="2a33f-167">You can use this setting to force the encoder to add a silent audio track to the output in that scenario.</span></span>

<span data-ttu-id="2a33f-168">Чтобы заставить кодировщик создать ресурс, содержащий звуковую дорожку с тишиной, когда входные данные не содержат звука, укажите значение "InsertSilenceIfNoAudio".</span><span class="sxs-lookup"><span data-stu-id="2a33f-168">To force the encoder to produce an asset that contains a silent audio track when input has no audio, specify the "InsertSilenceIfNoAudio" value.</span></span>

<span data-ttu-id="2a33f-169">Вы можете использовать любую из предустановок MES, которые определены в [этом](media-services-mes-presets-overview.md) разделе, и внести в нее следующие изменения.</span><span class="sxs-lookup"><span data-stu-id="2a33f-169">You can take any of the MES presets documented in [this](media-services-mes-presets-overview.md) section, and make the following modification:</span></span>

### <a name="json-preset"></a><span data-ttu-id="2a33f-170">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="2a33f-170">JSON preset</span></span>
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a><span data-ttu-id="2a33f-171">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="2a33f-171">XML preset</span></span>
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <span data-ttu-id="2a33f-172"><a id="deinterlacing"></a>Отключение автоматического устранения чересстрочной развертки</span><span class="sxs-lookup"><span data-stu-id="2a33f-172"><a id="deinterlacing"></a>Disable auto de-interlacing</span></span>
<span data-ttu-id="2a33f-173">Клиентам не нужно ничего делать, если они хотят, чтобы содержимое в чересстрочной развертке автоматически устранялось.</span><span class="sxs-lookup"><span data-stu-id="2a33f-173">Customers don’t need to do anything if they like the interlace contents to be automatically de-interlaced.</span></span> <span data-ttu-id="2a33f-174">Если автоматическое устранение чересстрочной развертки включено (по умолчанию), стандартный кодировщик мультимедиа не выполняет автоматическое обнаружение чересстрочных кадров и устраняет чересстрочную развертку кадров, которые помечены как чересстрочные.</span><span class="sxs-lookup"><span data-stu-id="2a33f-174">When the auto de-interlacing is on (default) the MES does the auto detection of interlaced frames and only de-interlaces frames marked as interlaced.</span></span>

<span data-ttu-id="2a33f-175">Автоматическое удаление чересстрочной развертки можно отключить.</span><span class="sxs-lookup"><span data-stu-id="2a33f-175">You can turn the auto de-interlacing off.</span></span> <span data-ttu-id="2a33f-176">Однако это делать не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="2a33f-176">This option is not recommended.</span></span>

### <a name="json-preset"></a><span data-ttu-id="2a33f-177">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="2a33f-177">JSON preset</span></span>
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a><span data-ttu-id="2a33f-178">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="2a33f-178">XML preset</span></span>
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <span data-ttu-id="2a33f-179"><a id="audio_only"></a>Предустановки только для звука</span><span class="sxs-lookup"><span data-stu-id="2a33f-179"><a id="audio_only"></a>Audio-only presets</span></span>
<span data-ttu-id="2a33f-180">В этом разделе демонстрируются две предустановки стандартного кодировщика мультимедиа только для звука: "Звук в формате AAC" и "Звук в формате AAC хорошего качества".</span><span class="sxs-lookup"><span data-stu-id="2a33f-180">This section demonstrates two audio-only MES presets: AAC Audio and AAC Good Quality Audio.</span></span>

### <a name="aac-audio"></a><span data-ttu-id="2a33f-181">Звук в формате AAC</span><span class="sxs-lookup"><span data-stu-id="2a33f-181">AAC Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="aac-good-quality-audio"></a><span data-ttu-id="2a33f-182">Звук в формате AAC хорошего качества</span><span class="sxs-lookup"><span data-stu-id="2a33f-182">AAC Good Quality Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 192,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="2a33f-183"><a id="concatenate"></a>Сцепка нескольких видеофайлов</span><span class="sxs-lookup"><span data-stu-id="2a33f-183"><a id="concatenate"></a>Concatenate two or more video files</span></span>

<span data-ttu-id="2a33f-184">В следующем примере показано, как создать предустановку для сцепления двух или более видеофайлов.</span><span class="sxs-lookup"><span data-stu-id="2a33f-184">The following example illustrates how you can generate a preset to concatenate two or more video files.</span></span> <span data-ttu-id="2a33f-185">Наиболее распространенный сценарий — это добавление названия или трейлера к основному видео.</span><span class="sxs-lookup"><span data-stu-id="2a33f-185">The most common scenario is when you want to add a header or a trailer to the main video.</span></span> <span data-ttu-id="2a33f-186">Используется, когда совместно редактируемые видеофайлы имеют одинаковые свойства (разрешение видео, частоту кадров, количество аудиодорожек и т. д.).</span><span class="sxs-lookup"><span data-stu-id="2a33f-186">The intended use is when the video files being edited together share  properties (video resolution, frame rate, audio track count, etc.).</span></span> <span data-ttu-id="2a33f-187">Не следует комбинировать видео с разной частотой кадров или разным количеством аудиодорожек.</span><span class="sxs-lookup"><span data-stu-id="2a33f-187">You should take care not to mix videos of different frame rates, or with different number of audio tracks.</span></span>

>[!NOTE]
><span data-ttu-id="2a33f-188">Текущая структура функции сцепки предполагает, что исходные видеозаписи имеют согласованное разрешение, частоту кадров и т. д.</span><span class="sxs-lookup"><span data-stu-id="2a33f-188">The current design of the concatenation feature expects that the input video clips are consistent in terms of resolution, frame rate etc.</span></span> 

### <a name="requirements-and-considerations"></a><span data-ttu-id="2a33f-189">Требования и рекомендации</span><span class="sxs-lookup"><span data-stu-id="2a33f-189">Requirements and considerations</span></span>

* <span data-ttu-id="2a33f-190">В исходных видеофайлах должна быть только одна аудиодорожка.</span><span class="sxs-lookup"><span data-stu-id="2a33f-190">Input videos should only have one audio track.</span></span>
* <span data-ttu-id="2a33f-191">У всех исходных видеофайлов должна быть одинаковая частота кадров.</span><span class="sxs-lookup"><span data-stu-id="2a33f-191">Input videos should all have the same frame rate.</span></span>
* <span data-ttu-id="2a33f-192">Необходимо загрузить видеофайлы в отдельные ресурсы и задать видео как основной файл в каждом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="2a33f-192">You must upload your videos into separate assets and set the videos as the primary file in each asset.</span></span>
* <span data-ttu-id="2a33f-193">Необходимо знать длительность видеофайлов.</span><span class="sxs-lookup"><span data-stu-id="2a33f-193">You need to know the duration of your videos.</span></span>
* <span data-ttu-id="2a33f-194">Приведенные ниже примеры предустановок предполагают, что все исходные видеофайлы начинаются с нулевой отметки.</span><span class="sxs-lookup"><span data-stu-id="2a33f-194">The preset examples below assumes that all the input videos start with a timestamp of zero.</span></span> <span data-ttu-id="2a33f-195">Если видеофайлы начинаются с разных меток времени, необходимо изменить значения StartTime (как при работе с архивами прямых трансляций).</span><span class="sxs-lookup"><span data-stu-id="2a33f-195">You need to modify the StartTime values if the videos have different starting timestamp, as is typically the case with live archives.</span></span>
* <span data-ttu-id="2a33f-196">Предустановка JSON включает прямые ссылки на значения AssetID исходных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2a33f-196">The JSON preset makes explicit references to the AssetID values of the input assets.</span></span>
* <span data-ttu-id="2a33f-197">Образец кода предполагает, что предустановка JSON сохранена как локальный файл, например C:\supportFiles\preset.json.</span><span class="sxs-lookup"><span data-stu-id="2a33f-197">The sample code assumes that the JSON preset has been saved to a local file, such as "C:\supportFiles\preset.json".</span></span> <span data-ttu-id="2a33f-198">Кроме того, предполагается, что ресурсы созданы путем загрузки двух видеофайлов и что вам известны соответствующие значения AssetID.</span><span class="sxs-lookup"><span data-stu-id="2a33f-198">It also assumes that two assets have been created by uploading two video files, and that you know the resultant AssetID values.</span></span>
* <span data-ttu-id="2a33f-199">Фрагмент кода и предустановка JSON демонстрирует пример сцепления двух видеофайлов.</span><span class="sxs-lookup"><span data-stu-id="2a33f-199">The code snippet and JSON preset shows an example of concatenating two video files.</span></span> <span data-ttu-id="2a33f-200">Количество видеофайлов можно увеличить следующим образом.</span><span class="sxs-lookup"><span data-stu-id="2a33f-200">You can extend it to more than two videos by:</span></span>

  1. <span data-ttu-id="2a33f-201">Вызвать метод task.InputAssets.Add() несколько раз, чтобы добавить несколько видео по порядку.</span><span class="sxs-lookup"><span data-stu-id="2a33f-201">Calling task.InputAssets.Add() repeatedly to add more videos, in order.</span></span>
  2. <span data-ttu-id="2a33f-202">Внести соответствующие права в элемент Sources (Источники) файла JSON, добавив новые записи в том же порядке.</span><span class="sxs-lookup"><span data-stu-id="2a33f-202">Making corresponding edits to the "Sources" element in the JSON, by adding more entries, in the same order.</span></span>

### <a name="net-code"></a><span data-ttu-id="2a33f-203">Код .NET</span><span class="sxs-lookup"><span data-stu-id="2a33f-203">.NET code</span></span>

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass to it the name of the
    // processor to use for the specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load the XML (or JSON) from the local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify the input videos to be concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset to contain the results of the job.
    // This output is specified as AssetCreationOptions.None, which
    // means the output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a><span data-ttu-id="2a33f-204">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="2a33f-204">JSON preset</span></span>

<span data-ttu-id="2a33f-205">Обновите настроенную вами предустановку, указав идентификаторы ресурсов, которые нужно сцепить, и соответствующий промежуток времени для каждого видеофайла.</span><span class="sxs-lookup"><span data-stu-id="2a33f-205">Update your custom preset with ids of the assets that you want to concatenate, and with the appropriate time segment for each video.</span></span>

    {
      "Version": 1.0,
      "Sources": [
        {
          "AssetID": "606db602-efd7-4436-97b4-c0b867ba195b",
          "StartTime": "00:00:01",
          "Duration": "00:00:15"
        },
        {
          "AssetID": "a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e",
          "StartTime": "00:00:02",
          "Duration": "00:00:05"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": true,
          "H264Layers": [
            {
              "Level": "auto",
              "Bitrate": 1800,
              "MaxBitrate": 1800,
              "BufferWindow": "00:00:05",
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="2a33f-206"><a id="crop"></a>Обрезка видео с помощью стандартного кодировщика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="2a33f-206"><a id="crop"></a>Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="2a33f-207">Ознакомьтесь с разделом [Обрезка видео с помощью стандартного кодировщика мультимедиа](media-services-crop-video.md) .</span><span class="sxs-lookup"><span data-stu-id="2a33f-207">See the [Crop videos with Media Encoder Standard](media-services-crop-video.md) topic.</span></span>

## <span data-ttu-id="2a33f-208"><a id="no_video"></a>Вставка видеодорожки, если во входных данных нет видео</span><span class="sxs-lookup"><span data-stu-id="2a33f-208"><a id="no_video"></a>Insert a video track when input has no video</span></span>

<span data-ttu-id="2a33f-209">По умолчанию при отправке кодировщику входных данных, которые содержат только звук и не содержат аудио, выходной ресурс-контейнер будет содержать файлы только с аудиоданными.</span><span class="sxs-lookup"><span data-stu-id="2a33f-209">By default, if you send an input to the encoder that contains only audio, and no video, then the output asset contains files that contain only audio data.</span></span> <span data-ttu-id="2a33f-210">Некоторые проигрыватели, в том числе Проигрыватель мультимедиа Azure ([подробнее здесь](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)), могут не поддерживать обработку таких потоков.</span><span class="sxs-lookup"><span data-stu-id="2a33f-210">Some players, including Azure Media Player (see [this](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) may not be able to handle such streams.</span></span> <span data-ttu-id="2a33f-211">Этот параметр можно использовать для принудительного добавления кодировщиком монохромной видеодорожки в выходные данные в этом сценарии.</span><span class="sxs-lookup"><span data-stu-id="2a33f-211">You can use this setting to force the encoder to add a monochrome video track to the output in that scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="2a33f-212">Это увеличивает размер выходного ресурса-контейнера, а, следовательно, и затраты на такую задачу кодирования.</span><span class="sxs-lookup"><span data-stu-id="2a33f-212">Forcing the encoder to insert an output video track increases the size of the output Asset, and thereby the cost incurred for the encoding Task.</span></span> <span data-ttu-id="2a33f-213">Следует выполнить тесты, чтобы убедиться, что результирующее увеличение незначительно влияет на ежемесячные расходы.</span><span class="sxs-lookup"><span data-stu-id="2a33f-213">You should run tests to verify that this resultant increase has only a modest impact on your monthly charges.</span></span>
>

### <a name="inserting-video-at-only-the-lowest-bitrate"></a><span data-ttu-id="2a33f-214">Вставка видео только с минимальной скоростью</span><span class="sxs-lookup"><span data-stu-id="2a33f-214">Inserting video at only the lowest bitrate</span></span>

<span data-ttu-id="2a33f-215">Предположим, что вы используете предустановку кодирования с несколькими скоростями, например [H264 Multiple Bitrate 720p](media-services-mes-preset-h264-multiple-bitrate-720p.md) , чтобы закодировать для потоковой передачи весь входной каталог, содержащий смесь видео- и аудиофайлов.</span><span class="sxs-lookup"><span data-stu-id="2a33f-215">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) to encode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="2a33f-216">В этом случае, если входные данные не содержат видео, может потребоваться указать кодировщику принудительно вставлять монохромную видеодорожку только с самой низкой скоростью, а не с каждой выходной скоростью.</span><span class="sxs-lookup"><span data-stu-id="2a33f-216">In this scenario, when the input has no video, you may want to force the encoder to insert a monochrome video track at just the lowest bitrate, as opposed to inserting video at every output bitrate.</span></span> <span data-ttu-id="2a33f-217">Для этого необходимо указать флаг **InsertBlackIfNoVideoBottomLayerOnly**.</span><span class="sxs-lookup"><span data-stu-id="2a33f-217">To achieve this, you need to use the **InsertBlackIfNoVideoBottomLayerOnly** flag.</span></span>

<span data-ttu-id="2a33f-218">Вы можете использовать любую из предустановок MES, которые определены в [этом](media-services-mes-presets-overview.md) разделе, и внести в нее следующие изменения.</span><span class="sxs-lookup"><span data-stu-id="2a33f-218">You can take any of the MES presets documented in [this](media-services-mes-presets-overview.md) section, and make the following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="2a33f-219">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="2a33f-219">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="2a33f-220">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="2a33f-220">XML preset</span></span>

<span data-ttu-id="2a33f-221">При использовании XML укажите Condition="InsertBlackIfNoVideoBottomLayerOnly" в качестве атрибута элемента **H264Video** и Condition="InsertSilenceIfNoAudio" — в качестве атрибута элемента **AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="2a33f-221">When using XML, use Condition="InsertBlackIfNoVideoBottomLayerOnly" as an attribute to the **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute to **AACAudio**.</span></span>

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideoBottomLayerOnly">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .
```

### <a name="inserting-video-at-all-output-bitrates"></a><span data-ttu-id="2a33f-222">Вставка видео со всеми выходными скоростями</span><span class="sxs-lookup"><span data-stu-id="2a33f-222">Inserting video at all output bitrates</span></span>
<span data-ttu-id="2a33f-223">Предположим, что вы используете предустановку кодирования с несколькими скоростями, например [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) , чтобы закодировать для потоковой передачи весь входной каталог, содержащий смесь видео- и аудиофайлов.</span><span class="sxs-lookup"><span data-stu-id="2a33f-223">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) to encode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="2a33f-224">В этом случае, если входные данные не содержат видео, может потребоваться указать кодировщику принудительно вставлять монохромную видеодорожку с каждой из выходных скоростей.</span><span class="sxs-lookup"><span data-stu-id="2a33f-224">In this scenario, when the input has no video, you may want to force the encoder to insert a monochrome video track at all the output bitrates.</span></span> <span data-ttu-id="2a33f-225">Это гарантирует, что выходные ресурсы-контейнеры будут однородны по количеству видео- и аудиодорожек.</span><span class="sxs-lookup"><span data-stu-id="2a33f-225">This ensures that your output Assets are all homogenous with respect to number of video tracks and audio tracks.</span></span> <span data-ttu-id="2a33f-226">Чтобы получить такой результат, необходимо указать флаг InsertBlackIfNoVideo.</span><span class="sxs-lookup"><span data-stu-id="2a33f-226">To achieve this, you need to specify the "InsertBlackIfNoVideo" flag.</span></span>

<span data-ttu-id="2a33f-227">Вы можете использовать любую из предустановок MES, которые определены в [этом](media-services-mes-presets-overview.md) разделе, и внести в нее следующие изменения.</span><span class="sxs-lookup"><span data-stu-id="2a33f-227">You can take any of the MES presets documented in [this](media-services-mes-presets-overview.md) section, and make the following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="2a33f-228">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="2a33f-228">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="2a33f-229">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="2a33f-229">XML preset</span></span>

<span data-ttu-id="2a33f-230">При использовании XML укажите Condition="InsertBlackIfNoVideo" в качестве атрибута элемента **H264Video** и Condition="InsertSilenceIfNoAudio" — в качестве атрибута элемента **AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="2a33f-230">When using XML, use Condition="InsertBlackIfNoVideo" as an attribute to the **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute to **AACAudio**.</span></span>

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideo">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .  
```

## <span data-ttu-id="2a33f-231"><a id="rotate_video"></a>Поворот видео</span><span class="sxs-lookup"><span data-stu-id="2a33f-231"><a id="rotate_video"></a>Rotate a video</span></span>
<span data-ttu-id="2a33f-232">[Стандартный кодировщик служб мультимедиа](media-services-dotnet-encode-with-media-encoder-standard.md) поддерживает поворот на 0, 90, 180 и 270 градусов.</span><span class="sxs-lookup"><span data-stu-id="2a33f-232">The [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 0/90/180/270.</span></span> <span data-ttu-id="2a33f-233">По умолчанию задается значение Auto, при котором система пытается обнаружить метаданные поворота во входящем видеофайле и обеспечить соответствующую компенсацию.</span><span class="sxs-lookup"><span data-stu-id="2a33f-233">The default behavior is "Auto", where it tries to detect the rotation metadata in the incoming video file and compensate for it.</span></span> <span data-ttu-id="2a33f-234">Включите приведенный ниже элемент **Sources** в одну из предустановок, определенных в [этом](media-services-mes-presets-overview.md) разделе.</span><span class="sxs-lookup"><span data-stu-id="2a33f-234">Include the following **Sources** element to one of the presets defined in [this](media-services-mes-presets-overview.md) section:</span></span>

### <a name="json-preset"></a><span data-ttu-id="2a33f-235">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="2a33f-235">JSON preset</span></span>
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...
### <a name="xml-preset"></a><span data-ttu-id="2a33f-236">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="2a33f-236">XML preset</span></span>
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

<span data-ttu-id="2a33f-237">Сведения о том, как кодировщик интерпретирует значения ширины и высоты в предустановке, когда запускается компенсация поворота, см. [здесь](media-services-mes-schema.md#PreserveResolutionAfterRotation).</span><span class="sxs-lookup"><span data-stu-id="2a33f-237">Also, see [this](media-services-mes-schema.md#PreserveResolutionAfterRotation) topic for more information on how the encoder interprets the Width and Height settings in the preset, when rotation compensation is triggered.</span></span>

<span data-ttu-id="2a33f-238">Если указать значение 0, кодировщик будет игнорировать метаданные поворота (если они есть) во входящем видеофайле.</span><span class="sxs-lookup"><span data-stu-id="2a33f-238">You can use the value "0" to indicate to the encoder to ignore rotation metadata, if present, in the input video.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="2a33f-239">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="2a33f-239">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2a33f-240">Отзывы</span><span class="sxs-lookup"><span data-stu-id="2a33f-240">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="2a33f-241">См. также</span><span class="sxs-lookup"><span data-stu-id="2a33f-241">See Also</span></span>
[<span data-ttu-id="2a33f-242">Обзор кодирования с помощью служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="2a33f-242">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)
