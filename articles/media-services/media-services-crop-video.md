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
# <a name="crop-videos-with-media-encoder-standard"></a>Обрезка видео с помощью стандартного кодировщика мультимедиа
Можно использовать Media Encoder стандартных (MES) toocrop видео входные данные. Обрезка — hello процесс выбора прямоугольное окно в пределах кадра видео hello, а также кодирование просто hello пикселей в этом окне. Следующая схема Hello помогает иллюстрируют процесс hello.

![Обрезка видео](./media/media-services-crop-video/media-services-crop-video01.png)

Предположим, что имеется в качестве входного видео с разрешением 1920 x 1080 пикселей (соотношение сторон 16:9), но имеет черные полосы (опорный ячейки) на hello влево и вправо, чтобы только окна 4:3 или 1440 x 1080 пикселей содержит активные видео. Можно использовать MES toocrop или отредактируйте hello черной полосы и кодирования hello 1440 x 1080 области.

Обрезка в MES настолько стадии предварительной обработки, hello обрезки в hello предустановку параметры toohello исходного входного видео. Кодирование-это следующий этап, и параметры ширины или высоты hello применяются toohello *предварительно обработанный* видео и toohello исходного видео. При разработке создания требуется следующее hello toodo: (a) выберите параметры обрезки hello, основанные на исходный входной видео hello и (б) выберите ваш кодирования параметров на основании hello обрезку видео. Если вы не соответствуют вашей обрезку видео toohello параметры кодирования, hello выходные данные не будут, как ожидалось.

Hello [следующие](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) разделе показано, как toocreate задания кодирования с MES и как toospecify пользовательской конфигурации для hello задачу кодирования. 

## <a name="creating-a-custom-preset"></a>Создание пользовательской предустановки
В примере hello hello иллюстрации:

1. Разрешение исходного видео — 1920 x 1080.
2. Он должен toobe обрезку выходные данные tooan 1440 x 1080, выравнивается по центру в кадре входной hello
3. Это означает, что смещение по оси X равно 240 ((1920 – 1440)/2), а смещение по оси Y равно нулю.
4. Hello ширину и высоту прямоугольника обрезки hello — 1440 и 1080, соответственно
5. В hello кодирования этапе hello запрашивать имеет три уровня tooproduce, приведены разрешения 1440 x 1080, 960 x 720 и 480 x 360, соответственно

### <a name="json-preset"></a>Предустановка JSON
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


## <a name="restrictions-on-cropping"></a>Ограничения при обрезке
Обрезка функции Hello предназначен toobe вручную. Вы должны были tooload входные данные видео в подходящее средство редактирования, позволяющее выбрать кадры интерес, поместите hello курсор toodetermine смещения для hello прямоугольника обрезки, toodetermine hello предустановку, настроенной для этого конкретного видео, и т. д. Эта функция не предназначена tooenable таких вещей, как: автоматическое обнаружение и удаление границ черным letterbox/pillarbox в видео входные данные.

Обрезка функция toohello применяются следующие ограничения. Если они не выполняются, hello кодирования задач может завершиться ошибкой или непредвиденный результат.

1. Hello координаты и размер прямоугольника обрезки hello имеют toofit внутри hello входное видео
2. Как упоминалось выше, hello ширину и высоту в hello кодирования параметры имеют toohello toocorrespond обрезку видео
3. Обрезка применяется toovideos, записанные в альбомной ориентации (т. е. не применяется toovideos записи со смартфоном удерживаются по вертикали или в книжной ориентации)
4. Рекомендуется применять к прогрессивному видео, которое записывается в пикселях широкоформатного кадра.

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Дальнейшие действия
В разделе обучения toohelp пути узнать удобных функций, предлагаемых AMS служб мультимедиа Azure.  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
