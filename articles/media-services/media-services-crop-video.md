---
title: "Как обрезать видео с помощью Media Encoder Standard в Azure | Документация Майкрософт"
description: "В этой статье показано, как обрезать видео с помощью стандартного кодировщика служб мультимедиа."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 7628f674-2005-4531-8b61-d7a4f53e46ba
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/09/2017
ms.author: anilmur;juliako;
ms.openlocfilehash: 60d0ce14a271fcbe698559da95ca011cb888b221
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="crop-videos-with-media-encoder-standard"></a><span data-ttu-id="5d393-103">Обрезка видео с помощью стандартного кодировщика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="5d393-103">Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="5d393-104">Для обрезки входного видео можно использовать стандартный кодировщик служб мультимедиа (MES).</span><span class="sxs-lookup"><span data-stu-id="5d393-104">You can use Media Encoder Standard (MES) to crop your input video.</span></span> <span data-ttu-id="5d393-105">Обрезка заключается в выборе прямоугольного окна в пределах видеокадра и кодировании в нем пикселей.</span><span class="sxs-lookup"><span data-stu-id="5d393-105">Cropping is the process of selecting a rectangular window within the video frame, and encoding just the pixels within that window.</span></span> <span data-ttu-id="5d393-106">Этот процесс продемонстрирован на схеме ниже.</span><span class="sxs-lookup"><span data-stu-id="5d393-106">The following diagram helps illustrate the process.</span></span>

![Обрезка видео](./media/media-services-crop-video/media-services-crop-video01.png)

<span data-ttu-id="5d393-108">Предположим, у вас есть входное видео с разрешением 1920 x 1080 пикселей (соотношение сторон 16:9), но по бокам экрана есть черные полосы. Таким образом, активное видео имеет разрешение 1440 x 1080 пикселей или соотношение сторон 4:3.</span><span class="sxs-lookup"><span data-stu-id="5d393-108">Suppose you have as input a video that has a resolution of 1920x1080 pixels (16:9 aspect ratio), but has black bars (pillar boxes) at the left and right, so that only a 4:3 window or 1440x1080 pixels contains active video.</span></span> <span data-ttu-id="5d393-109">Чтобы обрезать или изменить черные полосы и закодировать область с разрешением 1440 x 1080, можно использовать стандартный кодировщик служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="5d393-109">You can use MES to crop or edit out the black bars, and encode the 1440x1080 region.</span></span>

<span data-ttu-id="5d393-110">Обрезка в MES — это стадия предварительной обработки. Поэтому параметры обрезки в предустановке кодирования применяются к исходному видео.</span><span class="sxs-lookup"><span data-stu-id="5d393-110">Cropping in MES is a pre-processing stage, so the cropping parameters in the encoding preset apply to the original input video.</span></span> <span data-ttu-id="5d393-111">Кодирование — это последующая стадия. Параметры ширины и высоты применяются к *предварительно обработанному* видео, а не к исходному.</span><span class="sxs-lookup"><span data-stu-id="5d393-111">Encoding is a subsequent stage, and the width/height settings apply to the *pre-processed* video, and not to the original video.</span></span> <span data-ttu-id="5d393-112">При создании предустановки необходимо сделать следующее: a) выбрать параметры обрезки на основе исходного видео; б) выбрать параметры кодирования на основе обрезанного видео.</span><span class="sxs-lookup"><span data-stu-id="5d393-112">When designing your preset you need to do the following: (a) select the crop parameters based on the original input video, and (b) select your encode settings based on the cropped video.</span></span> <span data-ttu-id="5d393-113">Если параметры кодирования не сопоставлены с обрезанным видео, выходное видео не будет выглядеть должным образом.</span><span class="sxs-lookup"><span data-stu-id="5d393-113">If you do not match your encode settings to the cropped video, the output will not be as you expect.</span></span>

<span data-ttu-id="5d393-114">В [следующем](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) разделе показано, как создать задание кодирования с помощью MES и указать пользовательскую предустановку для задачи кодирования.</span><span class="sxs-lookup"><span data-stu-id="5d393-114">The [following](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic shows how to create an encoding job with MES and how to specify a custom preset for the encoding task.</span></span> 

## <a name="creating-a-custom-preset"></a><span data-ttu-id="5d393-115">Создание пользовательской предустановки</span><span class="sxs-lookup"><span data-stu-id="5d393-115">Creating a custom preset</span></span>
<span data-ttu-id="5d393-116">Пример, приведенный на схеме:</span><span class="sxs-lookup"><span data-stu-id="5d393-116">In the example shown in the diagram:</span></span>

1. <span data-ttu-id="5d393-117">Разрешение исходного видео — 1920 x 1080.</span><span class="sxs-lookup"><span data-stu-id="5d393-117">Original input is 1920x1080</span></span>
2. <span data-ttu-id="5d393-118">Его необходимо обрезать, чтобы получилось видео с разрешением 1440 x 1080, расположенное по центру входного кадра.</span><span class="sxs-lookup"><span data-stu-id="5d393-118">It needs to be cropped to an output of 1440x1080, which is centered in the input frame</span></span>
3. <span data-ttu-id="5d393-119">Это означает, что смещение по оси X равно 240 ((1920 – 1440)/2), а смещение по оси Y равно нулю.</span><span class="sxs-lookup"><span data-stu-id="5d393-119">This means an X offset of (1920 – 1440)/2 = 240, and a Y offset of zero</span></span>
4. <span data-ttu-id="5d393-120">Ширина и высота прямоугольника обрезки — 1440 и 1080 соответственно.</span><span class="sxs-lookup"><span data-stu-id="5d393-120">The Width and Height of the Crop rectangle are 1440 and 1080, respectively</span></span>
5. <span data-ttu-id="5d393-121">На стадии кодирования необходимо создать три уровня с разрешениями 1440 x 1080, 960 x 720 и 480 x 360 соответственно.</span><span class="sxs-lookup"><span data-stu-id="5d393-121">In the encode stage, the ask is to produce three layers, are resolutions 1440x1080, 960x720 and 480x360, respectively</span></span>

### <a name="json-preset"></a><span data-ttu-id="5d393-122">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="5d393-122">JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "Crop": {
                "X": 240,
                "Y": 0,
                "Width": 1440,
                "Height": 1080
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
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1440,
              "Height": 1080,
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
              "Bitrate": 1250,
              "MaxBitrate": 1250,
              "BufferWindow": "00:00:05",
              "Width": 480,
              "Height": 360,
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


## <a name="restrictions-on-cropping"></a><span data-ttu-id="5d393-123">Ограничения при обрезке</span><span class="sxs-lookup"><span data-stu-id="5d393-123">Restrictions on cropping</span></span>
<span data-ttu-id="5d393-124">Обрезка должна выполняться вручную.</span><span class="sxs-lookup"><span data-stu-id="5d393-124">The cropping feature is meant to be manual.</span></span> <span data-ttu-id="5d393-125">Необходимо загрузить входное видео в подходящее средство редактирования. Там вы сможете выбрать нужные кадры, установить курсор, чтобы определить смещение для прямоугольника обрезки, а также определить предустановку кодирования, настроенную для этого конкретного видео и т. д. Эта функция не поддерживает автоматическое определение и удаление черных границ letterbox или pillarbox во входном видео.</span><span class="sxs-lookup"><span data-stu-id="5d393-125">You would need to load your input video into a suitable editing tool that lets you select frames of interest, position the cursor to determine offsets for the cropping rectangle, to determine the encoding preset that is tuned for that particular video, etc. This feature is not meant to enable things like: automatic detection and removal of black letterbox/pillarbox borders in your input video.</span></span>

<span data-ttu-id="5d393-126">К функции обрезки также применяются приведенные ниже ограничения.</span><span class="sxs-lookup"><span data-stu-id="5d393-126">Following constraints apply to the cropping feature.</span></span> <span data-ttu-id="5d393-127">В случае их несоблюдения задача кодирования может завершиться сбоем или вывести непредвиденный результат.</span><span class="sxs-lookup"><span data-stu-id="5d393-127">If these are not met, the encode Task can fail, or produce an unexpected output.</span></span>

1. <span data-ttu-id="5d393-128">Координаты и размер прямоугольника обрезки должны соответствовать входному видео.</span><span class="sxs-lookup"><span data-stu-id="5d393-128">The co-ordinates and size of the Crop rectangle have to fit within the input video</span></span>
2. <span data-ttu-id="5d393-129">Как уже говорилось, значения ширины и высоты в параметрах кодирования должны соответствовать обрезанному видео.</span><span class="sxs-lookup"><span data-stu-id="5d393-129">As mentioned above, the Width & Height in the encode settings have to correspond to the cropped video</span></span>
3. <span data-ttu-id="5d393-130">Обрезка применяется к видео, записанному в альбомном режиме (т. е. она не применяется к видео, которое записано с использованием смартфона, повернутого вертикально или настроенного на книжный режим).</span><span class="sxs-lookup"><span data-stu-id="5d393-130">Cropping applies to videos captured in landscape mode (i.e. not applicable to videos recorded with a smartphone held vertically or in portrait mode)</span></span>
4. <span data-ttu-id="5d393-131">Рекомендуется применять к прогрессивному видео, которое записывается в пикселях широкоформатного кадра.</span><span class="sxs-lookup"><span data-stu-id="5d393-131">Works best with progressive video captured with square pixels</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="5d393-132">Отзывы</span><span class="sxs-lookup"><span data-stu-id="5d393-132">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="5d393-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5d393-133">Next step</span></span>
<span data-ttu-id="5d393-134">См. схемы обучения по службам мультимедиа Azure, которые позволят вам узнать о возможностях, предлагаемых AMS.</span><span class="sxs-lookup"><span data-stu-id="5d393-134">See Azure Media Services learning paths to help you learn about great features offered by AMS.</span></span>  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
