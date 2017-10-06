---
title: "aaaPerform advanced кодирования, настроив предустановок MES | Документы Microsoft"
description: "В этом разделе показано, как tooperform advanced кодирования, настроив Media Encoder Стандартная предустановки задачи."
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
ms.openlocfilehash: 9caa68fafacaf51f91f0554c5bafe491928d8c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a><span data-ttu-id="cb770-103">Настройка предустановок MES для расширенного кодирования</span><span class="sxs-lookup"><span data-stu-id="cb770-103">Perform advanced encoding by customizing MES presets</span></span> 

## <a name="overview"></a><span data-ttu-id="cb770-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="cb770-104">Overview</span></span>

<span data-ttu-id="cb770-105">В этом разделе показано, как стили toocustomize стандартный кодировщик мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="cb770-105">This topic shows how toocustomize Media Encoder Standard presets.</span></span> <span data-ttu-id="cb770-106">Hello [кодирование стандарту Media Encoder с помощью пользовательские стили](media-services-custom-mes-presets-with-dotnet.md) разделе показано, как задача toocreate .NET toouse кодировку, а также заданий, в которой выполняется эта задача.</span><span class="sxs-lookup"><span data-stu-id="cb770-106">hello [Encoding with Media Encoder Standard using custom presets](media-services-custom-mes-presets-with-dotnet.md) topic shows how toouse .NET toocreate an encoding task and a job that executes this task.</span></span> <span data-ttu-id="cb770-107">После настройки стиля, задачу кодирования toohello пользовательские стили hello питания.</span><span class="sxs-lookup"><span data-stu-id="cb770-107">Once you customize a preset, supply hello custom presets toohello encoding task.</span></span> 

>[!NOTE]
><span data-ttu-id="cb770-108">При использовании XML-Предустановка, выполнения убедиться, что порядок hello toopreserve элементов, как показано в ниже примеров XML (например, KeyFrameInterval должны предваряться SceneChangeDetection).</span><span class="sxs-lookup"><span data-stu-id="cb770-108">If using an XML preset, make sure toopreserve hello order of elements, as shown in XML samples below (for example, KeyFrameInterval should precede SceneChangeDetection).</span></span>
>

<span data-ttu-id="cb770-109">В этом разделе приведены hello пользовательские стили, которые выполняют следующие задачи кодирования hello.</span><span class="sxs-lookup"><span data-stu-id="cb770-109">In this topic, hello custom presets that perform hello following encoding tasks are demonstrated.</span></span>

## <a name="support-for-relative-sizes"></a><span data-ttu-id="cb770-110">Поддержка относительных размеров</span><span class="sxs-lookup"><span data-stu-id="cb770-110">Support for relative sizes</span></span>

<span data-ttu-id="cb770-111">При создании эскизов, не требуется задать tooalways вывода ширину и высоту в пикселях.</span><span class="sxs-lookup"><span data-stu-id="cb770-111">When generating thumbnails, you do not need tooalways specify output width and height in pixels.</span></span> <span data-ttu-id="cb770-112">Можно указать их в процентах в диапазоне hello [1%,..., 100%].</span><span class="sxs-lookup"><span data-stu-id="cb770-112">You can specify them in percentages, in hello range [1%, …, 100%].</span></span>

### <a name="json-preset"></a><span data-ttu-id="cb770-113">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="cb770-113">JSON preset</span></span>
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a><span data-ttu-id="cb770-114">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="cb770-114">XML preset</span></span>
    <Width>100%</Width>
    <Height>100%</Height>

## <span data-ttu-id="cb770-115"><a id="thumbnails"></a>Создание эскизов</span><span class="sxs-lookup"><span data-stu-id="cb770-115"><a id="thumbnails"></a>Generate thumbnails</span></span>

<span data-ttu-id="cb770-116">В этом разделе показано, как toocustomize предварительной установки, создает эскизы.</span><span class="sxs-lookup"><span data-stu-id="cb770-116">This section shows how toocustomize a preset that generates thumbnails.</span></span> <span data-ttu-id="cb770-117">Hello стиль указанных ниже содержит сведения о способе tooencode файле также сведения, необходимые toogenerate эскизы.</span><span class="sxs-lookup"><span data-stu-id="cb770-117">hello preset defined below contains information on how you want tooencode your file as well as information needed toogenerate thumbnails.</span></span> <span data-ttu-id="cb770-118">Может принимать любую из предустановок MES hello задокументированы [это](media-services-mes-presets-overview.md) статьи и добавьте код, который создает эскизы.</span><span class="sxs-lookup"><span data-stu-id="cb770-118">You can take any of hello MES presets documented [this](media-services-mes-presets-overview.md) section and add code that generates thumbnails.</span></span>  

> [!NOTE]
> <span data-ttu-id="cb770-119">Hello **SceneChangeDetection** в следующих предустановленных hello можно только установить tootrue Если tooa постоянным битрейтом видео кодируется.</span><span class="sxs-lookup"><span data-stu-id="cb770-119">hello **SceneChangeDetection** setting in hello following preset can only be set tootrue if you are encoding tooa single  bitrate video.</span></span> <span data-ttu-id="cb770-120">Если кодирование выполняется с разными скоростями tooa видео- и задайте **SceneChangeDetection** tootrue, кодировщик hello возвращает сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="cb770-120">If you are encoding tooa multi-bitrate video and set **SceneChangeDetection** tootrue, hello encoder returns an error.</span></span>  
>
>

<span data-ttu-id="cb770-121">Сведения о схеме см. [здесь](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="cb770-121">For information about schema, see [this](media-services-mes-schema.md) topic.</span></span>

<span data-ttu-id="cb770-122">Убедитесь, что hello tooreview [вопросы](#considerations) раздела.</span><span class="sxs-lookup"><span data-stu-id="cb770-122">Make sure tooreview hello [Considerations](#considerations) section.</span></span>

### <span data-ttu-id="cb770-123"><a id="json"></a>Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="cb770-123"><a id="json"></a>JSON preset</span></span>
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


### <span data-ttu-id="cb770-124"><a id="xml"></a>Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="cb770-124"><a id="xml"></a>XML preset</span></span>
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

### <a name="considerations"></a><span data-ttu-id="cb770-125">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="cb770-125">Considerations</span></span>

<span data-ttu-id="cb770-126">применить Hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="cb770-126">hello following considerations apply:</span></span>

* <span data-ttu-id="cb770-127">Использование Hello явные отметки времени для начала/шаг или Range предполагается, что этот источник входных hello — менее 1 минуты long.</span><span class="sxs-lookup"><span data-stu-id="cb770-127">hello use of explicit timestamps for Start/Step/Range assumes that hello input source is at least 1 minute long.</span></span>
* <span data-ttu-id="cb770-128">Элементы Jpg, Png и BmpImage обладают строковыми атрибутами Start, Step и Range, которые можно интерпретировать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="cb770-128">Jpg/Png/BmpImage elements have Start, Step, and Range string attributes – these can be interpreted as:</span></span>

  * <span data-ttu-id="cb770-129">номер кадра, если эти атрибуты выражены неотрицательными целыми числами, например "Start": "120";</span><span class="sxs-lookup"><span data-stu-id="cb770-129">Frame Number if they are non-negative integers, for example "Start": "120",</span></span>
  * <span data-ttu-id="cb770-130">Длительность относительный toosource Если выразить в виде % суффиксом, например «Start»: «% 15», или</span><span class="sxs-lookup"><span data-stu-id="cb770-130">Relative toosource duration if expressed as %-suffixed, for example "Start": "15%", OR</span></span>
  * <span data-ttu-id="cb770-131">Отметка времени, если атрибуты имеют формат</span><span class="sxs-lookup"><span data-stu-id="cb770-131">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="cb770-132">ЧЧ:ММ:СС, например "Start" : "00:01:00".</span><span class="sxs-lookup"><span data-stu-id="cb770-132">format, for example "Start" : "00:01:00"</span></span>

    <span data-ttu-id="cb770-133">При желании условные обозначения можно комбинировать.</span><span class="sxs-lookup"><span data-stu-id="cb770-133">You can mix and match notations as you please.</span></span>

    <span data-ttu-id="cb770-134">Кроме того, также поддерживает запуск специального макроса: {наилучшим образом}, который осуществляет toodetermine hello первый «Город» кадр hello содержимого Примечание: (шаг и диапазон игнорируются при начале задано слишком {наиболее})</span><span class="sxs-lookup"><span data-stu-id="cb770-134">Additionally, Start also supports a special Macro:{Best}, which attempts toodetermine hello first “interesting” frame of hello content NOTE: (Step and Range are ignored when Start is set too{Best})</span></span>
  * <span data-ttu-id="cb770-135">По умолчанию Start:{Best}</span><span class="sxs-lookup"><span data-stu-id="cb770-135">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="cb770-136">Формат вывода должно явно предоставляться для каждого формата изображения toobe: Jpg, Png или BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="cb770-136">Output format needs toobe explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="cb770-137">При наличии MES соответствует JpgVideo tooJpgFormat и т. д.</span><span class="sxs-lookup"><span data-stu-id="cb770-137">When present, MES matches JpgVideo tooJpgFormat and so on.</span></span> <span data-ttu-id="cb770-138">Выходнойформат появился новый указанного макроса кодек изображений: {индекс}, требующие toobe присутствует (один раз и только один раз) для форматов вывода изображения.</span><span class="sxs-lookup"><span data-stu-id="cb770-138">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs toobe present (once and only once) for image output formats.</span></span>

## <span data-ttu-id="cb770-139"><a id="trim_video"></a>Монтаж видео (обрезка)</span><span class="sxs-lookup"><span data-stu-id="cb770-139"><a id="trim_video"></a>Trim a video (clipping)</span></span>
<span data-ttu-id="cb770-140">Этом разделе рассказывается об изменении кодировщика hello стили tooclip или trim hello входное видео, где hello ввода так называемого мезонинный файл или файл по требованию.</span><span class="sxs-lookup"><span data-stu-id="cb770-140">This section talks about modifying hello encoder presets tooclip or trim hello input video where hello input is a so-called mezzanine file or on-demand file.</span></span> <span data-ttu-id="cb770-141">Hello кодировщика можно также использовать tooclip или trim активов, который является захвата или архивированных из обновляющегося потока — hello подробные сведения для этого доступны в [этот блог](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="cb770-141">hello encoder can also be used tooclip or trim an asset, which is captured or archived from a live stream – hello details for this are available in [this blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span></span>

<span data-ttu-id="cb770-142">tootrim видео, можно использовать любой из предустановок MES hello описаны [это](media-services-mes-presets-overview.md) статьи и изменения hello **источников** (как показано ниже).</span><span class="sxs-lookup"><span data-stu-id="cb770-142">tootrim your videos, you can take any of hello MES presets documented [this](media-services-mes-presets-overview.md) section and modify hello **Sources** element (as shown below).</span></span> <span data-ttu-id="cb770-143">Hello значение StartTime должно toomatch hello абсолютный отметки времени hello входное видео.</span><span class="sxs-lookup"><span data-stu-id="cb770-143">hello value of StartTime needs toomatch hello absolute timestamps of hello input video.</span></span> <span data-ttu-id="cb770-144">Например, если hello первый кадр hello входное видео имеет отметку времени, 12:00:10.000, то время начала должно быть по крайней мере 12:00:10.000 и более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="cb770-144">For example, if hello first frame of hello input video has a timestamp of 12:00:10.000, then StartTime should be at least 12:00:10.000 and greater.</span></span> <span data-ttu-id="cb770-145">В следующем примере hello мы предположим, что входные данные hello видео имеет отметку времени начала равно нулю.</span><span class="sxs-lookup"><span data-stu-id="cb770-145">In hello example below, we assume that hello input video has a starting timestamp of zero.</span></span> <span data-ttu-id="cb770-146">**Источники** должны размещаться в начале hello Предустановка hello.</span><span class="sxs-lookup"><span data-stu-id="cb770-146">**Sources** should be placed at hello beginning of hello preset.</span></span>

### <span data-ttu-id="cb770-147"><a id="json"></a>Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="cb770-147"><a id="json"></a>JSON preset</span></span>
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

### <a name="xml-preset"></a><span data-ttu-id="cb770-148">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="cb770-148">XML preset</span></span>
<span data-ttu-id="cb770-149">tootrim видео, можно использовать любой из предустановок MES hello описаны [здесь](media-services-mes-presets-overview.md) и изменения hello **источников** (как показано ниже).</span><span class="sxs-lookup"><span data-stu-id="cb770-149">tootrim your videos, you can take any of hello MES presets documented [here](media-services-mes-presets-overview.md) and modify hello **Sources** element (as shown below).</span></span>

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

## <span data-ttu-id="cb770-150"><a id="overlay"></a>Создание наложения</span><span class="sxs-lookup"><span data-stu-id="cb770-150"><a id="overlay"></a>Create an overlay</span></span>

<span data-ttu-id="cb770-151">Стандартный кодировщик мультимедиа Hello позволяет toooverlay изображение на существующие видео.</span><span class="sxs-lookup"><span data-stu-id="cb770-151">hello Media Encoder Standard allows you toooverlay an image onto an existing video.</span></span> <span data-ttu-id="cb770-152">В настоящее время поддерживаются следующие форматы hello: png, jpg, gif и bmp.</span><span class="sxs-lookup"><span data-stu-id="cb770-152">Currently, hello following formats are supported: png, jpg, gif, and bmp.</span></span> <span data-ttu-id="cb770-153">Hello предустановки, заданной ниже представлен Простейший пример наложения видео.</span><span class="sxs-lookup"><span data-stu-id="cb770-153">hello preset defined below is a basic example  of a video overlay.</span></span>

<span data-ttu-id="cb770-154">В дополнение к этому toodefining файл набора параметров, также имеется toolet Media Services знать, какой файл в ресурсе hello является изображение перекрытия hello и файл, который является hello источник видео, на котором необходимо toooverlay hello изображение.</span><span class="sxs-lookup"><span data-stu-id="cb770-154">In addition toodefining a preset file, you also have toolet Media Services know which file in hello asset is hello overlay image and which file is hello source video onto which you want toooverlay hello image.</span></span> <span data-ttu-id="cb770-155">видеофайл Hello имеет toobe hello **основной** файла.</span><span class="sxs-lookup"><span data-stu-id="cb770-155">hello video file has toobe hello **primary** file.</span></span>

<span data-ttu-id="cb770-156">Если вы используете .NET, добавьте hello, следующие две функции, определенные toohello в следующем примере в [это](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) раздела.</span><span class="sxs-lookup"><span data-stu-id="cb770-156">If you are using .NET, add hello following two functions toohello .NET example defined in [this](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic.</span></span> <span data-ttu-id="cb770-157">Hello **UploadMediaFilesFromFolder** функция отправляет файлы из папки (например, BigBuckBunny.mp4 и Image001.png) и наборы hello mp4 toobe файл hello первичный файл актива hello.</span><span class="sxs-lookup"><span data-stu-id="cb770-157">hello **UploadMediaFilesFromFolder** function uploads files from a folder (for example, BigBuckBunny.mp4 and Image001.png) and sets hello mp4 file toobe hello primary file in hello asset.</span></span> <span data-ttu-id="cb770-158">Hello **EncodeWithOverlay** функция использует hello файла пользовательского стиля, переданный tooit (например, hello конфигурации, следующим) toocreate hello задачу кодирования.</span><span class="sxs-lookup"><span data-stu-id="cb770-158">hello **EncodeWithOverlay** function uses hello custom preset file that was passed tooit (for example, hello preset that follows) toocreate hello encoding task.</span></span>


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // hello following code assumes 
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
        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input assets toobe encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset toocontain hello results of hello job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> <span data-ttu-id="cb770-159">Текущие ограничения:</span><span class="sxs-lookup"><span data-stu-id="cb770-159">Current limitations:</span></span>
>
> <span data-ttu-id="cb770-160">прозрачность наложения приветствия не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="cb770-160">hello overlay opacity setting is not supported.</span></span>
>
> <span data-ttu-id="cb770-161">Ваш исходный файл и файл изображения наложения hello имеют toobe в hello одного средства и hello видеофайл потребностей toobe набор как основной файл hello в этом ресурсе.</span><span class="sxs-lookup"><span data-stu-id="cb770-161">Your source video file and hello overlay image file have toobe in hello same asset, and hello video file needs toobe set as hello primary file in this asset.</span></span>
>
>

### <a name="json-preset"></a><span data-ttu-id="cb770-162">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="cb770-162">JSON preset</span></span>
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


### <a name="xml-preset"></a><span data-ttu-id="cb770-163">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="cb770-163">XML preset</span></span>
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


## <span data-ttu-id="cb770-164"><a id="silent_audio"></a>Вставка звуковой дорожки с тишиной, если входные данные не содержат звука</span><span class="sxs-lookup"><span data-stu-id="cb770-164"><a id="silent_audio"></a>Insert a silent audio track when input has no audio</span></span>
<span data-ttu-id="cb770-165">По умолчанию при отправке входных toohello кодировщик, содержит только видео и без звука нажмите hello выходной актив содержит файлы, содержащие только видео данные.</span><span class="sxs-lookup"><span data-stu-id="cb770-165">By default, if you send an input toohello encoder that contains only video, and no audio, then hello output asset contains files that contain only video data.</span></span> <span data-ttu-id="cb770-166">Некоторые проигрыватели не удается toohandle такого потока вывода.</span><span class="sxs-lookup"><span data-stu-id="cb770-166">Some players may not be able toohandle such output streams.</span></span> <span data-ttu-id="cb770-167">В этом сценарии можно использовать этот параметр tooforce hello кодировщика tooadd является выходом toohello автоматической звуковой дорожки.</span><span class="sxs-lookup"><span data-stu-id="cb770-167">You can use this setting tooforce hello encoder tooadd a silent audio track toohello output in that scenario.</span></span>

<span data-ttu-id="cb770-168">tooforce hello кодировщика tooproduce актив, содержащий автоматической звуковой дорожки, когда входные данные не содержит звука, укажите значение «InsertSilenceIfNoAudio» hello.</span><span class="sxs-lookup"><span data-stu-id="cb770-168">tooforce hello encoder tooproduce an asset that contains a silent audio track when input has no audio, specify hello "InsertSilenceIfNoAudio" value.</span></span>

<span data-ttu-id="cb770-169">Можно использовать любой hello предустановок MES задокументированы в [это](media-services-mes-presets-overview.md) статьи и внесите следующие изменения hello:</span><span class="sxs-lookup"><span data-stu-id="cb770-169">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

### <a name="json-preset"></a><span data-ttu-id="cb770-170">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="cb770-170">JSON preset</span></span>
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a><span data-ttu-id="cb770-171">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="cb770-171">XML preset</span></span>
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <span data-ttu-id="cb770-172"><a id="deinterlacing"></a>Отключение автоматического устранения чересстрочной развертки</span><span class="sxs-lookup"><span data-stu-id="cb770-172"><a id="deinterlacing"></a>Disable auto de-interlacing</span></span>
<span data-ttu-id="cb770-173">Клиентам не требуется toodo ничего, если они как hello чередования toobe содержимое автоматически отменяется с чередованием.</span><span class="sxs-lookup"><span data-stu-id="cb770-173">Customers don’t need toodo anything if they like hello interlace contents toobe automatically de-interlaced.</span></span> <span data-ttu-id="cb770-174">При hello автоматически отменяется чередование на MES hello приветствия (по умолчанию) автоматического обнаружения чередующихся кадров, только отменить interlaces кадры с пометкой с чередованием.</span><span class="sxs-lookup"><span data-stu-id="cb770-174">When hello auto de-interlacing is on (default) hello MES does hello auto detection of interlaced frames and only de-interlaces frames marked as interlaced.</span></span>

<span data-ttu-id="cb770-175">Можно отключить hello автоматически отменяется чередование.</span><span class="sxs-lookup"><span data-stu-id="cb770-175">You can turn hello auto de-interlacing off.</span></span> <span data-ttu-id="cb770-176">Однако это делать не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="cb770-176">This option is not recommended.</span></span>

### <a name="json-preset"></a><span data-ttu-id="cb770-177">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="cb770-177">JSON preset</span></span>
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a><span data-ttu-id="cb770-178">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="cb770-178">XML preset</span></span>
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <span data-ttu-id="cb770-179"><a id="audio_only"></a>Предустановки только для звука</span><span class="sxs-lookup"><span data-stu-id="cb770-179"><a id="audio_only"></a>Audio-only presets</span></span>
<span data-ttu-id="cb770-180">В этом разделе демонстрируются две предустановки стандартного кодировщика мультимедиа только для звука: "Звук в формате AAC" и "Звук в формате AAC хорошего качества".</span><span class="sxs-lookup"><span data-stu-id="cb770-180">This section demonstrates two audio-only MES presets: AAC Audio and AAC Good Quality Audio.</span></span>

### <a name="aac-audio"></a><span data-ttu-id="cb770-181">Звук в формате AAC</span><span class="sxs-lookup"><span data-stu-id="cb770-181">AAC Audio</span></span>
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

### <a name="aac-good-quality-audio"></a><span data-ttu-id="cb770-182">Звук в формате AAC хорошего качества</span><span class="sxs-lookup"><span data-stu-id="cb770-182">AAC Good Quality Audio</span></span>
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

## <span data-ttu-id="cb770-183"><a id="concatenate"></a>Сцепка нескольких видеофайлов</span><span class="sxs-lookup"><span data-stu-id="cb770-183"><a id="concatenate"></a>Concatenate two or more video files</span></span>

<span data-ttu-id="cb770-184">Hello следующем примере показано, как можно создать стиль tooconcatenate два или несколько файлов.</span><span class="sxs-lookup"><span data-stu-id="cb770-184">hello following example illustrates how you can generate a preset tooconcatenate two or more video files.</span></span> <span data-ttu-id="cb770-185">наиболее распространенным сценарием Hello удобно, если нужно tooadd заголовок или основного видео с toohello прицепа.</span><span class="sxs-lookup"><span data-stu-id="cb770-185">hello most common scenario is when you want tooadd a header or a trailer toohello main video.</span></span> <span data-ttu-id="cb770-186">Hello предназначено применяется, когда hello видеофайлов редактируемого вместе обладают свойствами (разрешение экрана, частота кадров, число звуковой дорожки, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="cb770-186">hello intended use is when hello video files being edited together share  properties (video resolution, frame rate, audio track count, etc.).</span></span> <span data-ttu-id="cb770-187">Следует позаботиться не toomix видео частота кадров или с другим числом звуковые дорожки.</span><span class="sxs-lookup"><span data-stu-id="cb770-187">You should take care not toomix videos of different frame rates, or with different number of audio tracks.</span></span>

>[!NOTE]
><span data-ttu-id="cb770-188">Hello текущего конструктора функции объединения hello ожидает ввода, hello видеоклипы согласованы с точки зрения разрешение, частота кадров и т. д.</span><span class="sxs-lookup"><span data-stu-id="cb770-188">hello current design of hello concatenation feature expects that hello input video clips are consistent in terms of resolution, frame rate etc.</span></span> 

### <a name="requirements-and-considerations"></a><span data-ttu-id="cb770-189">Требования и рекомендации</span><span class="sxs-lookup"><span data-stu-id="cb770-189">Requirements and considerations</span></span>

* <span data-ttu-id="cb770-190">В исходных видеофайлах должна быть только одна аудиодорожка.</span><span class="sxs-lookup"><span data-stu-id="cb770-190">Input videos should only have one audio track.</span></span>
* <span data-ttu-id="cb770-191">Видео входных данных должны иметь hello же частота кадров.</span><span class="sxs-lookup"><span data-stu-id="cb770-191">Input videos should all have hello same frame rate.</span></span>
* <span data-ttu-id="cb770-192">Необходимо передать видео на отдельных средств и сделайте видео hello hello первичного файла в каждого средства.</span><span class="sxs-lookup"><span data-stu-id="cb770-192">You must upload your videos into separate assets and set hello videos as hello primary file in each asset.</span></span>
* <span data-ttu-id="cb770-193">Требуется длительность hello tooknow видео.</span><span class="sxs-lookup"><span data-stu-id="cb770-193">You need tooknow hello duration of your videos.</span></span>
* <span data-ttu-id="cb770-194">Hello предустановленную приведенных ниже примерах предполагается запуска всех hello входного видео с меткой времени, равной нулю.</span><span class="sxs-lookup"><span data-stu-id="cb770-194">hello preset examples below assumes that all hello input videos start with a timestamp of zero.</span></span> <span data-ttu-id="cb770-195">Требуется значения StartTime hello toomodify Если видео hello имеют другой меткой времени начала, как это обычно бывает hello динамической архивы.</span><span class="sxs-lookup"><span data-stu-id="cb770-195">You need toomodify hello StartTime values if hello videos have different starting timestamp, as is typically hello case with live archives.</span></span>
* <span data-ttu-id="cb770-196">Hello Предустановка JSON делает явные ссылки значения AssetID toohello входные активы hello.</span><span class="sxs-lookup"><span data-stu-id="cb770-196">hello JSON preset makes explicit references toohello AssetID values of hello input assets.</span></span>
* <span data-ttu-id="cb770-197">Образец Hello кода предполагается, что конфигурации JSON, приветствия был сохранен tooa локального файла, например «C:\supportFiles\preset.json».</span><span class="sxs-lookup"><span data-stu-id="cb770-197">hello sample code assumes that hello JSON preset has been saved tooa local file, such as "C:\supportFiles\preset.json".</span></span> <span data-ttu-id="cb770-198">Также предполагается, что два активы были созданы путем передачи двух видеофайлов и знать hello итоговые значения AssetID.</span><span class="sxs-lookup"><span data-stu-id="cb770-198">It also assumes that two assets have been created by uploading two video files, and that you know hello resultant AssetID values.</span></span>
* <span data-ttu-id="cb770-199">Здравствуйте, фрагмент кода и JSON Предустановка показан пример объединения двух файлов видео.</span><span class="sxs-lookup"><span data-stu-id="cb770-199">hello code snippet and JSON preset shows an example of concatenating two video files.</span></span> <span data-ttu-id="cb770-200">Вы можете расширить его toomore чем двух видео с:</span><span class="sxs-lookup"><span data-stu-id="cb770-200">You can extend it toomore than two videos by:</span></span>

  1. <span data-ttu-id="cb770-201">Задача для вызова метода. InputAssets.Add() многократно tooadd дополнительные видео, в порядке.</span><span class="sxs-lookup"><span data-stu-id="cb770-201">Calling task.InputAssets.Add() repeatedly tooadd more videos, in order.</span></span>
  2. <span data-ttu-id="cb770-202">Внесения соответствующих изменяет элемент toohello «источники» в hello JSON, добавив дополнительные записи в hello порядке.</span><span class="sxs-lookup"><span data-stu-id="cb770-202">Making corresponding edits toohello "Sources" element in hello JSON, by adding more entries, in hello same order.</span></span>

### <a name="net-code"></a><span data-ttu-id="cb770-203">Код .NET</span><span class="sxs-lookup"><span data-stu-id="cb770-203">.NET code</span></span>

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass tooit hello name of the
    // processor toouse for hello specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load hello XML (or JSON) from hello local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify hello input videos toobe concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset toocontain hello results of hello job.
    // This output is specified as AssetCreationOptions.None, which
    // means hello output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a><span data-ttu-id="cb770-204">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="cb770-204">JSON preset</span></span>

<span data-ttu-id="cb770-205">Обновите пользовательский стиль с идентификаторами, которые должны tooconcatenate активов hello и с сегментом hello подходящее время для каждого видео.</span><span class="sxs-lookup"><span data-stu-id="cb770-205">Update your custom preset with ids of hello assets that you want tooconcatenate, and with hello appropriate time segment for each video.</span></span>

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

## <span data-ttu-id="cb770-206"><a id="crop"></a>Обрезка видео с помощью стандартного кодировщика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="cb770-206"><a id="crop"></a>Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="cb770-207">. В разделе hello [обрезать видео стандарту кодировщик мультимедиа](media-services-crop-video.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="cb770-207">See hello [Crop videos with Media Encoder Standard](media-services-crop-video.md) topic.</span></span>

## <span data-ttu-id="cb770-208"><a id="no_video"></a>Вставка видеодорожки, если во входных данных нет видео</span><span class="sxs-lookup"><span data-stu-id="cb770-208"><a id="no_video"></a>Insert a video track when input has no video</span></span>

<span data-ttu-id="cb770-209">По умолчанию при отправке входных toohello кодировщик, содержит только аудио и видео не, то hello выходной актив содержит файлы, содержащие только звуковых данных.</span><span class="sxs-lookup"><span data-stu-id="cb770-209">By default, if you send an input toohello encoder that contains only audio, and no video, then hello output asset contains files that contain only audio data.</span></span> <span data-ttu-id="cb770-210">Проигрыватели, включая Azure Media Player (см. [это](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) может оказаться может toohandle такие потоки.</span><span class="sxs-lookup"><span data-stu-id="cb770-210">Some players, including Azure Media Player (see [this](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) may not be able toohandle such streams.</span></span> <span data-ttu-id="cb770-211">Можно использовать этот параметр tooforce hello кодировщика tooadd является выходом toohello монохромный видеодорожки в этом сценарии.</span><span class="sxs-lookup"><span data-stu-id="cb770-211">You can use this setting tooforce hello encoder tooadd a monochrome video track toohello output in that scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="cb770-212">Принудительное tooinsert кодировщика hello выходных данных повышает видеодорожки hello размер hello выходных активов и Здравствуйте, тем самым затраты на кодирование задачи hello.</span><span class="sxs-lookup"><span data-stu-id="cb770-212">Forcing hello encoder tooinsert an output video track increases hello size of hello output Asset, and thereby hello cost incurred for hello encoding Task.</span></span> <span data-ttu-id="cb770-213">Выполняйте тесты tooverify, этот итоговый увеличение имеет только ограниченное влияние на ваш ежемесячные расходы.</span><span class="sxs-lookup"><span data-stu-id="cb770-213">You should run tests tooverify that this resultant increase has only a modest impact on your monthly charges.</span></span>
>

### <a name="inserting-video-at-only-hello-lowest-bitrate"></a><span data-ttu-id="cb770-214">Вставка видео битрейтом hello низкий</span><span class="sxs-lookup"><span data-stu-id="cb770-214">Inserting video at only hello lowest bitrate</span></span>

<span data-ttu-id="cb770-215">Предположим, что вы используете несколько bitrate кодировку в конфигурации, такие как [«H264 Multiple Bitrate 720p»](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode всего входных данных каталога для потоковой передачи, которая содержит сочетание видеофайлов и файлов только со звуком.</span><span class="sxs-lookup"><span data-stu-id="cb770-215">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="cb770-216">В этом случае после ввода hello нет изображения можно tooforce hello кодировщика tooinsert отслеживать видео монохромный режим определяются в только что hello низкий битрейт, как противоположность tooinserting каждый выходной битрейте видео.</span><span class="sxs-lookup"><span data-stu-id="cb770-216">In this scenario, when hello input has no video, you may want tooforce hello encoder tooinsert a monochrome video track at just hello lowest bitrate, as opposed tooinserting video at every output bitrate.</span></span> <span data-ttu-id="cb770-217">tooachieve это, необходимо toouse hello **InsertBlackIfNoVideoBottomLayerOnly** флаг.</span><span class="sxs-lookup"><span data-stu-id="cb770-217">tooachieve this, you need toouse hello **InsertBlackIfNoVideoBottomLayerOnly** flag.</span></span>

<span data-ttu-id="cb770-218">Можно использовать любой hello предустановок MES задокументированы в [это](media-services-mes-presets-overview.md) статьи и внесите следующие изменения hello:</span><span class="sxs-lookup"><span data-stu-id="cb770-218">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="cb770-219">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="cb770-219">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="cb770-220">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="cb770-220">XML preset</span></span>

<span data-ttu-id="cb770-221">При использовании XML, использовать условие = «InsertBlackIfNoVideoBottomLayerOnly» как атрибут toohello **H264Video** элемент и условие = «InsertSilenceIfNoAudio» как атрибут слишком**AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="cb770-221">When using XML, use Condition="InsertBlackIfNoVideoBottomLayerOnly" as an attribute toohello **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute too**AACAudio**.</span></span>

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

### <a name="inserting-video-at-all-output-bitrates"></a><span data-ttu-id="cb770-222">Вставка видео со всеми выходными скоростями</span><span class="sxs-lookup"><span data-stu-id="cb770-222">Inserting video at all output bitrates</span></span>
<span data-ttu-id="cb770-223">Предположим, что вы используете несколько bitrate кодировку в конфигурации, такие как [«H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode всего входных данных каталога для потоковой передачи, которая содержит сочетание видеофайлов и файлов только со звуком.</span><span class="sxs-lookup"><span data-stu-id="cb770-223">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="cb770-224">В этом случае после ввода hello нет изображения можно tooforce hello кодировщика tooinsert монохромный Видеодорожка на всех битрейтах hello в выходных данных.</span><span class="sxs-lookup"><span data-stu-id="cb770-224">In this scenario, when hello input has no video, you may want tooforce hello encoder tooinsert a monochrome video track at all hello output bitrates.</span></span> <span data-ttu-id="cb770-225">Это гарантирует, что выходные данные средства — все однородные с относительно toonumber видеодорожек и звуковые дорожки.</span><span class="sxs-lookup"><span data-stu-id="cb770-225">This ensures that your output Assets are all homogenous with respect toonumber of video tracks and audio tracks.</span></span> <span data-ttu-id="cb770-226">tooachieve это, необходимо toospecify hello флаг «InsertBlackIfNoVideo».</span><span class="sxs-lookup"><span data-stu-id="cb770-226">tooachieve this, you need toospecify hello "InsertBlackIfNoVideo" flag.</span></span>

<span data-ttu-id="cb770-227">Можно использовать любой hello предустановок MES задокументированы в [это](media-services-mes-presets-overview.md) статьи и внесите следующие изменения hello:</span><span class="sxs-lookup"><span data-stu-id="cb770-227">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="cb770-228">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="cb770-228">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="cb770-229">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="cb770-229">XML preset</span></span>

<span data-ttu-id="cb770-230">При использовании XML, использовать условие = «InsertBlackIfNoVideo» как атрибут toohello **H264Video** элемент и условие = «InsertSilenceIfNoAudio» как атрибут слишком**AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="cb770-230">When using XML, use Condition="InsertBlackIfNoVideo" as an attribute toohello **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute too**AACAudio**.</span></span>

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

## <span data-ttu-id="cb770-231"><a id="rotate_video"></a>Поворот видео</span><span class="sxs-lookup"><span data-stu-id="cb770-231"><a id="rotate_video"></a>Rotate a video</span></span>
<span data-ttu-id="cb770-232">Hello [Media Encoder Стандартная](media-services-dotnet-encode-with-media-encoder-standard.md) поддерживает поворот по углы 0/90/180 или 270.</span><span class="sxs-lookup"><span data-stu-id="cb770-232">hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 0/90/180/270.</span></span> <span data-ttu-id="cb770-233">поведение по умолчанию Hello — «Авто», где пытается toodetect hello поворота метаданных в hello входящих видеофайлов и компенсации для него.</span><span class="sxs-lookup"><span data-stu-id="cb770-233">hello default behavior is "Auto", where it tries toodetect hello rotation metadata in hello incoming video file and compensate for it.</span></span> <span data-ttu-id="cb770-234">Включить следующие hello **источников** tooone элемент hello стилей, определенных в [это](media-services-mes-presets-overview.md) раздела:</span><span class="sxs-lookup"><span data-stu-id="cb770-234">Include hello following **Sources** element tooone of hello presets defined in [this](media-services-mes-presets-overview.md) section:</span></span>

### <a name="json-preset"></a><span data-ttu-id="cb770-235">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="cb770-235">JSON preset</span></span>
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
### <a name="xml-preset"></a><span data-ttu-id="cb770-236">Предустановка XML</span><span class="sxs-lookup"><span data-stu-id="cb770-236">XML preset</span></span>
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

<span data-ttu-id="cb770-237">Кроме того, в разделе [это](media-services-mes-schema.md#PreserveResolutionAfterRotation) приведены дополнительные сведения об как кодировщик hello интерпретирует hello параметры ширины и высоты в hello, то по умолчанию при запуске поворота компенсации.</span><span class="sxs-lookup"><span data-stu-id="cb770-237">Also, see [this](media-services-mes-schema.md#PreserveResolutionAfterRotation) topic for more information on how hello encoder interprets hello Width and Height settings in hello preset, when rotation compensation is triggered.</span></span>

<span data-ttu-id="cb770-238">Можно использовать hello значение «0» tooindicate toohello кодировщика tooignore поворота метаданных, если он имеется, входное видео hello.</span><span class="sxs-lookup"><span data-stu-id="cb770-238">You can use hello value "0" tooindicate toohello encoder tooignore rotation metadata, if present, in hello input video.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="cb770-239">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="cb770-239">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cb770-240">Отзывы</span><span class="sxs-lookup"><span data-stu-id="cb770-240">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="cb770-241">См. также</span><span class="sxs-lookup"><span data-stu-id="cb770-241">See Also</span></span>
[<span data-ttu-id="cb770-242">Обзор кодирования с помощью служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="cb770-242">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)
