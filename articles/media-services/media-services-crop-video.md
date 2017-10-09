---
title: "видео toocrop aaaHow стандарту Media Encoder - Azure | Документы Microsoft"
description: "В этой статье показано, как видео toocrop стандарту кодировщика мультимедиа."
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
ms.openlocfilehash: 2b4ac3d96228b93c890a38c57c4913988de1e8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="crop-videos-with-media-encoder-standard"></a><span data-ttu-id="0bb98-103">Обрезка видео с помощью стандартного кодировщика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="0bb98-103">Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="0bb98-104">Можно использовать Media Encoder стандартных (MES) toocrop видео входные данные.</span><span class="sxs-lookup"><span data-stu-id="0bb98-104">You can use Media Encoder Standard (MES) toocrop your input video.</span></span> <span data-ttu-id="0bb98-105">Обрезка — hello процесс выбора прямоугольное окно в пределах кадра видео hello, а также кодирование просто hello пикселей в этом окне.</span><span class="sxs-lookup"><span data-stu-id="0bb98-105">Cropping is hello process of selecting a rectangular window within hello video frame, and encoding just hello pixels within that window.</span></span> <span data-ttu-id="0bb98-106">Следующая схема Hello помогает иллюстрируют процесс hello.</span><span class="sxs-lookup"><span data-stu-id="0bb98-106">hello following diagram helps illustrate hello process.</span></span>

![Обрезка видео](./media/media-services-crop-video/media-services-crop-video01.png)

<span data-ttu-id="0bb98-108">Предположим, что имеется в качестве входного видео с разрешением 1920 x 1080 пикселей (соотношение сторон 16:9), но имеет черные полосы (опорный ячейки) на hello влево и вправо, чтобы только окна 4:3 или 1440 x 1080 пикселей содержит активные видео.</span><span class="sxs-lookup"><span data-stu-id="0bb98-108">Suppose you have as input a video that has a resolution of 1920x1080 pixels (16:9 aspect ratio), but has black bars (pillar boxes) at hello left and right, so that only a 4:3 window or 1440x1080 pixels contains active video.</span></span> <span data-ttu-id="0bb98-109">Можно использовать MES toocrop или отредактируйте hello черной полосы и кодирования hello 1440 x 1080 области.</span><span class="sxs-lookup"><span data-stu-id="0bb98-109">You can use MES toocrop or edit out hello black bars, and encode hello 1440x1080 region.</span></span>

<span data-ttu-id="0bb98-110">Обрезка в MES настолько стадии предварительной обработки, hello обрезки в hello предустановку параметры toohello исходного входного видео.</span><span class="sxs-lookup"><span data-stu-id="0bb98-110">Cropping in MES is a pre-processing stage, so hello cropping parameters in hello encoding preset apply toohello original input video.</span></span> <span data-ttu-id="0bb98-111">Кодирование-это следующий этап, и параметры ширины или высоты hello применяются toohello *предварительно обработанный* видео и toohello исходного видео.</span><span class="sxs-lookup"><span data-stu-id="0bb98-111">Encoding is a subsequent stage, and hello width/height settings apply toohello *pre-processed* video, and not toohello original video.</span></span> <span data-ttu-id="0bb98-112">При разработке создания требуется следующее hello toodo: (a) выберите параметры обрезки hello, основанные на исходный входной видео hello и (б) выберите ваш кодирования параметров на основании hello обрезку видео.</span><span class="sxs-lookup"><span data-stu-id="0bb98-112">When designing your preset you need toodo hello following: (a) select hello crop parameters based on hello original input video, and (b) select your encode settings based on hello cropped video.</span></span> <span data-ttu-id="0bb98-113">Если вы не соответствуют вашей обрезку видео toohello параметры кодирования, hello выходные данные не будут, как ожидалось.</span><span class="sxs-lookup"><span data-stu-id="0bb98-113">If you do not match your encode settings toohello cropped video, hello output will not be as you expect.</span></span>

<span data-ttu-id="0bb98-114">Hello [следующие](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) разделе показано, как toocreate задания кодирования с MES и как toospecify пользовательской конфигурации для hello задачу кодирования.</span><span class="sxs-lookup"><span data-stu-id="0bb98-114">hello [following](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic shows how toocreate an encoding job with MES and how toospecify a custom preset for hello encoding task.</span></span> 

## <a name="creating-a-custom-preset"></a><span data-ttu-id="0bb98-115">Создание пользовательской предустановки</span><span class="sxs-lookup"><span data-stu-id="0bb98-115">Creating a custom preset</span></span>
<span data-ttu-id="0bb98-116">В примере hello hello иллюстрации:</span><span class="sxs-lookup"><span data-stu-id="0bb98-116">In hello example shown in hello diagram:</span></span>

1. <span data-ttu-id="0bb98-117">Разрешение исходного видео — 1920 x 1080.</span><span class="sxs-lookup"><span data-stu-id="0bb98-117">Original input is 1920x1080</span></span>
2. <span data-ttu-id="0bb98-118">Он должен toobe обрезку выходные данные tooan 1440 x 1080, выравнивается по центру в кадре входной hello</span><span class="sxs-lookup"><span data-stu-id="0bb98-118">It needs toobe cropped tooan output of 1440x1080, which is centered in hello input frame</span></span>
3. <span data-ttu-id="0bb98-119">Это означает, что смещение по оси X равно 240 ((1920 – 1440)/2), а смещение по оси Y равно нулю.</span><span class="sxs-lookup"><span data-stu-id="0bb98-119">This means an X offset of (1920 – 1440)/2 = 240, and a Y offset of zero</span></span>
4. <span data-ttu-id="0bb98-120">Hello ширину и высоту прямоугольника обрезки hello — 1440 и 1080, соответственно</span><span class="sxs-lookup"><span data-stu-id="0bb98-120">hello Width and Height of hello Crop rectangle are 1440 and 1080, respectively</span></span>
5. <span data-ttu-id="0bb98-121">В hello кодирования этапе hello запрашивать имеет три уровня tooproduce, приведены разрешения 1440 x 1080, 960 x 720 и 480 x 360, соответственно</span><span class="sxs-lookup"><span data-stu-id="0bb98-121">In hello encode stage, hello ask is tooproduce three layers, are resolutions 1440x1080, 960x720 and 480x360, respectively</span></span>

### <a name="json-preset"></a><span data-ttu-id="0bb98-122">Предустановка JSON</span><span class="sxs-lookup"><span data-stu-id="0bb98-122">JSON preset</span></span>
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


## <a name="restrictions-on-cropping"></a><span data-ttu-id="0bb98-123">Ограничения при обрезке</span><span class="sxs-lookup"><span data-stu-id="0bb98-123">Restrictions on cropping</span></span>
<span data-ttu-id="0bb98-124">Обрезка функции Hello предназначен toobe вручную.</span><span class="sxs-lookup"><span data-stu-id="0bb98-124">hello cropping feature is meant toobe manual.</span></span> <span data-ttu-id="0bb98-125">Вы должны были tooload входные данные видео в подходящее средство редактирования, позволяющее выбрать кадры интерес, поместите hello курсор toodetermine смещения для hello прямоугольника обрезки, toodetermine hello предустановку, настроенной для этого конкретного видео, и т. д. Эта функция не предназначена tooenable таких вещей, как: автоматическое обнаружение и удаление границ черным letterbox/pillarbox в видео входные данные.</span><span class="sxs-lookup"><span data-stu-id="0bb98-125">You would need tooload your input video into a suitable editing tool that lets you select frames of interest, position hello cursor toodetermine offsets for hello cropping rectangle, toodetermine hello encoding preset that is tuned for that particular video, etc. This feature is not meant tooenable things like: automatic detection and removal of black letterbox/pillarbox borders in your input video.</span></span>

<span data-ttu-id="0bb98-126">Обрезка функция toohello применяются следующие ограничения.</span><span class="sxs-lookup"><span data-stu-id="0bb98-126">Following constraints apply toohello cropping feature.</span></span> <span data-ttu-id="0bb98-127">Если они не выполняются, hello кодирования задач может завершиться ошибкой или непредвиденный результат.</span><span class="sxs-lookup"><span data-stu-id="0bb98-127">If these are not met, hello encode Task can fail, or produce an unexpected output.</span></span>

1. <span data-ttu-id="0bb98-128">Hello координаты и размер прямоугольника обрезки hello имеют toofit внутри hello входное видео</span><span class="sxs-lookup"><span data-stu-id="0bb98-128">hello co-ordinates and size of hello Crop rectangle have toofit within hello input video</span></span>
2. <span data-ttu-id="0bb98-129">Как упоминалось выше, hello ширину и высоту в hello кодирования параметры имеют toohello toocorrespond обрезку видео</span><span class="sxs-lookup"><span data-stu-id="0bb98-129">As mentioned above, hello Width & Height in hello encode settings have toocorrespond toohello cropped video</span></span>
3. <span data-ttu-id="0bb98-130">Обрезка применяется toovideos, записанные в альбомной ориентации (т. е. не применяется toovideos записи со смартфоном удерживаются по вертикали или в книжной ориентации)</span><span class="sxs-lookup"><span data-stu-id="0bb98-130">Cropping applies toovideos captured in landscape mode (i.e. not applicable toovideos recorded with a smartphone held vertically or in portrait mode)</span></span>
4. <span data-ttu-id="0bb98-131">Рекомендуется применять к прогрессивному видео, которое записывается в пикселях широкоформатного кадра.</span><span class="sxs-lookup"><span data-stu-id="0bb98-131">Works best with progressive video captured with square pixels</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="0bb98-132">Отзывы</span><span class="sxs-lookup"><span data-stu-id="0bb98-132">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="0bb98-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0bb98-133">Next step</span></span>
<span data-ttu-id="0bb98-134">В разделе обучения toohelp пути узнать удобных функций, предлагаемых AMS служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="0bb98-134">See Azure Media Services learning paths toohelp you learn about great features offered by AMS.</span></span>  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
