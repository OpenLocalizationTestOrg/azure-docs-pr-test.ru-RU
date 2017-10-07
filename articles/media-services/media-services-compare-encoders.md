---
title: "aaaComparison платформы Azure по запросу мультимедиа кодировщики | Документы Microsoft"
description: "В этом разделе сравнивается hello кодирования возможности ** Media Encoder Standard ** и ** Media Encoder Premium рабочего процесса **."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: a79437c0-4832-423a-bca8-82632b2c47cc
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: ee04ad10d8e7c5f4f3c6e91e9b7679c2aba82c99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-of-azure-on-demand-media-encoders"></a>Сравнение кодировщиков мультимедиа Azure по запросу

В этом разделе сравнивается hello кодирования возможности **Media Encoder Стандартная** и **расширенного рабочего процесса кодировщика мультимедиа**.

## <a name="video-and-audio-processing-capabilities"></a>Возможности обработки видео и звука

Привет, в следующей таблице сравниваются функции hello между Media Encoder стандартных (MES) и Media Encoder Premium рабочего процесса (MEPW). 

|Функция|Стандартный кодировщик служб мультимедиа|Расширенный рабочий процесс кодировщика мультимедиа|
|---|---|---|
|Применение условной логики при кодировании<br/>(например, если входные данные hello HD, затем кодировать звук 5.1)|Нет|Да|
|Субтитры стандарта|Нет|[Да](media-services-premium-workflow-encoder-formats.md#closed_captioning)|
|[Dolby® Professional Loudness Correction](http://www.dolby.com/us/en/technologies/dolby-professional-loudness-solutions.pdf)<br/> с Dialogue Intelligence™|Нет|Да|
|Устранение чересстрочности, обратное преобразование видео|базовая;|Качество трансляции|
|Обнаружение и удаление черных границ <br/>(вертикальные и горизонтальные рамки)|Нет|Да|
|Создание эскизов|[Да](media-services-dotnet-generate-thumbnail-with-mes.md)|[Да](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)|
|Обрезание и совмещение видео|[Да](media-services-advanced-encoding-with-mes.md#trim_video)|Да|
|Наложение звука или видео|[Да](media-services-advanced-encoding-with-mes.md#overlay)|[Да](media-services-media-encoder-premium-workflow-multiplefilesinput.md#example-1--overlay-an-image-on-top-of-the-video)|
|Наложение изображений|Из источников изображений|Из источников изображений и текста|
|Несколько аудиодорожек на разных языках|Ограничено|[Да](media-services-media-encoder-premium-workflow-multiplefilesinput.md#example-2--multiple-audio-language-encoding)|

## <a id="billing"></a>Тарифные единицы, используемые кодировщиками
| Имя обработчика мультимедиа | Применимые цены | Примечания |
| --- | --- | --- |
| **Стандартный кодировщик служб мультимедиа** |КОДИРОВЩИК |Кодировки задачи будет изменена на основании hello-общая продолжительность в минутах, с которой все файлы мультимедиа hello, созданные в качестве выходных данных указано скоростью hello [здесь][1], КОДИРОВЩИК столбце hello. |
| **Рабочий процесс Media Encoder Premium** |РАСШИРЕННЫЙ КОДИРОВЩИК |Кодировки задачи будет изменена на основании hello-общая продолжительность в минутах, с которой все файлы мультимедиа hello, созданные в качестве выходных данных указано скоростью hello [здесь][1], hello КОДИРОВЩИКА PREMIUM в столбце. |

## <a name="input-containerfile-formats"></a>Контейнер ввода и форматы файлов
| Контейнер ввода/ форматы файлов | Стандартный кодировщик служб мультимедиа | Расширенный рабочий процесс кодировщика мультимедиа |
| --- | --- | --- |
| Adobe® Flash® F4V |Да |Да |
| MXF/SMPTE 377M |Да |Да |
| GXF |Да |Да |
| Транспортные потоки MPEG-2 |Да |Да |
| Программные потоки MPEG-2 |Да |Да |
| MPEG-4/MP4 |Да |Да |
| Windows Media/ASF |Да |Да |
| AVI (без сжатия 8 бит/10 бит) |Да |Да |
| 3GPP/3GPP2 |Да |Нет |
| Формат файлов Smooth Streaming (PIFF 1.3) |Да |Нет |
| [Microsoft Digital Video Recording(DVR-MS)](https://msdn.microsoft.com/library/windows/desktop/dd692984) |Да |Нет |
| Matroska/WebM |Да |Нет |
| QuickTime (.mov) |Да |Нет |

## <a name="input-video-codecs"></a>Входные видеокодеки
| Входные видеокодеки | Стандартный кодировщик служб мультимедиа | Расширенный рабочий процесс кодировщика мультимедиа |
| --- | --- | --- |
| AVC 8-разрядное/10-битный, копирование too4:2:2, включая AVCIntra |8 бит 4:2:0 и 4:2:2 |Да |
| Avid DNxHD (в MXF) |Да |Да |
| DVCPro/DVCProHD (в MXF) |Да |Да |
| JPEG2000 |Да |Да |
| MPEG-2 (профиль too422 и высокого уровня, включая варианты, такие как XDCAM, XDCAM HD, XDCAM IMX, CableLabs® и D10) |Профиль too422 |Да |
| MPEG-1 |Да |Да |
| Windows Media Video/VC-1 |Да |Да |
| Canopus HQ/HQX |Нет |Нет |
| MPEG-4, часть 2 |Да |Нет |
| [Theora](https://en.wikipedia.org/wiki/Theora) |Да |Нет |
| Apple ProRes 422 |Да |Нет |
| Apple ProRes 422 LT |Да |Нет |
| Apple ProRes 422 HQ |Да |Нет |
| Apple ProRes Proxy |Да |Нет |
| Apple ProRes 4444 |Да |Нет |
| Apple ProRes 4444 XQ |Да |Нет |

## <a name="input-audio-codecs"></a>Входные аудиокодеки
| Входные аудиокодеки | Стандартный кодировщик служб мультимедиа | Расширенный рабочий процесс кодировщика мультимедиа |
| --- | --- | --- |
| AES (SMPTE 331M и 302M, AES3-2003) |Нет |Да |
| Dolby® E |Нет |Да |
| Dolby® Digital (AC3) |Нет |Да |
| Dolby® Digital Plus (E-AC3) |Нет |Да |
| AAC (AAC-LC и AAC-HE, AAC HEv2; копирование too5.1) |Да |Да |
| MPEG Layer 2 |Да |Да |
| MP3 (MPEG-1 Audio Layer 3) |Да |Да |
| Windows Media Audio |Да |Да |
| WAV/PCM |Да |Да |
| [FLAC](https://en.wikipedia.org/wiki/FLAC)</a> |Да |Нет |
| [Opus](https://en.wikipedia.org/wiki/Opus_\(audio_format\)) |Да |Нет |
| [Vorbis](https://en.wikipedia.org/wiki/Vorbis)</a> |Да |Нет |

## <a name="output-containerfile-formats"></a>Контейнер вывода и форматы файлов
| Контейнер вывода/ форматы файлов | Стандартный кодировщик служб мультимедиа | Расширенный рабочий процесс кодировщика мультимедиа |
| --- | --- | --- |
| Adobe® Flash® F4V |Нет |Да |
| MXF (OP1a, XDCAM и AS02) |Нет |Да |
| DPP (включая AS11) |Нет |Да |
| GXF |Нет |Да |
| MPEG-4/MP4 |Да |Да |
| MPEG-TS |Да |Да |
| Windows Media/ASF |Нет |Да |
| AVI (без сжатия 8 бит/10 бит) |Нет |Да |
| Формат файлов Smooth Streaming (PIFF 1.3) |Нет |Да |

## <a name="output-video-codecs"></a>Выходные видеокодеки
| Выходные видеокодеки | Стандартный кодировщик служб мультимедиа | Расширенный рабочий процесс кодировщика мультимедиа |
| --- | --- | --- |
| AVC (H.264; 8-разрядное; Настройка tooHigh профиля, уровень 5.2; Ultra HD 4 КБ; Внутри AVC) |Только 8 бит 4:2:0 |Да |
| Avid DNxHD (в MXF) |Нет |Да |
| MPEG-2 (профиль too422 и высокого уровня, включая варианты, такие как XDCAM, XDCAM HD, XDCAM IMX, CableLabs® и D10) |Нет |Да |
| MPEG-1 |Нет |Да |
| Windows Media Video/VC-1 |Нет |Да |
| Создание эскизов JPEG |Да |Да |
| Создание эскизов PNG |Да |Да |
| Создание эскизов BMP |Да |Нет |

## <a name="output-audio-codecs"></a>Выходные аудиокодеки
| Выходные аудиокодеки | Стандартный кодировщик служб мультимедиа | Расширенный рабочий процесс кодировщика мультимедиа |
| --- | --- | --- |
| AES (SMPTE 331M и 302M, AES3-2003) |Нет |Да |
| Dolby® Digital (AC3) |Нет |Да |
| Dolby® Digital Plus (E-AC3) вверх too7.1 |Нет |Да |
| AAC (AAC-LC и AAC-HE, AAC HEv2; копирование too5.1) |Да |Да |
| MPEG Layer 2 |Нет |Да |
| MP3 (MPEG-1 Audio Layer 3) |Нет |Да |
| Windows Media Audio |Нет |Да |

>[!NOTE]
>Если кодирование tooDolby® Digital (AC3) hello вывода можно записать только в ISO MP4-файл.

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Связанные статьи
* [Выполняйте расширенные задачи кодирования путем настройки предустановок стандартного кодировщика служб мультимедиа](media-services-custom-mes-presets-with-dotnet.md)
* [Квоты и ограничения](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
