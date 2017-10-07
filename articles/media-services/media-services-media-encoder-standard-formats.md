---
title: "aaaMedia кодировщика стандартные форматы и кодеки"
description: "В этом разделе приведен обзор кодеков и форматов стандартного кодировщика мультимедиа."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: f334b1ce-2f56-4968-a019-f0a2b0016d9f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 51a67f372dff579383ffcfa988e8f4d38ad44a72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-standard-formats-and-codecs"></a>Форматы и кодеки стандартного кодировщика служб мультимедиа
Этот документ содержит список наиболее распространенных импорта hello и форматы экспорта, которые можно использовать со стандартной кодировщика мультимедиа.

## <a name="input-containerfile-formats"></a>Контейнер ввода/ форматы файлов
| Форматы файлов (расширения файлов) | Поддерживаются |
| --- | --- | --- | --- |
| FLV (с кодеками H.264 и AAC) (.flv) |Да |
| MXF (.mxf) |Да |
| GXF (.gxf) |Да |
| MPEG2-PS, MPEG2-TS, 3GP (.ts, .ps, .3gp, .3gpp, .mpg) |Да |
| Windows Media Video (WMV)/ASF (.wmv, .asf) |Да |
| AVI (без сжатия 8 бит/10 бит) (.avi) |Да |
| MP4 (MP4, M4A, M4V) и ISMV (ISMA, ISMV) |Да |
| [Microsoft Digital Video Recording(DVR-MS)](https://msdn.microsoft.com/library/windows/desktop/dd692984) (.dvr-ms) |Да |
| Matroska/WebM (.mkv) |Да |
| WAVE/WAV (.wav) |Да |
| QuickTime (.mov) |Да |

> [!NOTE]
> Выше приведен список расширений файлов, более часто встречающихся hello. Стандартный кодировщик служб мультимедиа поддерживает многие другие стандарты (например, M2TS, MPEG2VIDEO, QT). Если при tooencode файл, вы получаете сообщение об ошибке о формате hello не поддерживается, оставьте отзыв [здесь](https://feedback.azure.com/forums/169396-media-services/category/144411-encoding-and-processing/).
> 
> 

### <a name="audio-formats-in-input-containers"></a>Форматы аудио во входных контейнерах
Стандартный кодировщик мультимедиа поддерживает хранение hello следующие форматы звука в контейнерах ввода:

* файлы MXF, GXF и QuickTime со звуковыми дорожками с чередованием стерео или форматом 5.1;

или

* Файлы MXF, GXF и QuickTime, где аудио hello передается как отдельный отслеживает PCM, но сопоставления канала hello (toostereo или 5.1) могут быть выведены из метаданных файла hello

Обратите внимание, поддерживающих для канала, явные и пользовательские сопоставления будет предоставляться в hello ближайшее будущее.

## <a name="input-video-codecs"></a>Входные видеокодеки
| Входные видеокодеки | Поддерживаются |
| --- | --- | --- | --- |
| AVC 8-разрядное/10-битный, копирование too4:2:2, включая AVCIntra |8 бит 4:2:0 и 4:2:2 |
| Avid DNxHD (в MXF) |Да |
| DVCPro/DVCProHD (в MXF) |Да |
| Цифровое видео (DV) (в AVI-файлах) |Да |
| JPEG 2000 |Да |
| MPEG-2 (профиль too422 и высокого уровня, включая варианты, такие как XDCAM, XDCAM HD, XDCAM IMX, CableLabs® и D10) |Профиль too422 |
| MPEG-1 |Да |
| VC-1/WMV9 |Да |
| Canopus HQ/HQX |Нет |
| MPEG-4, часть 2 |Да |
| [Theora](https://en.wikipedia.org/wiki/Theora) |Да |
| YUV420 без сжатия или мезонинный файл |Да |
| Apple ProRes 422 |Да |
| Apple ProRes 422 LT |Да |
| Apple ProRes 422 HQ |Да |
| Apple ProRes Proxy |Да |
| Apple ProRes 4444 |Да |
| Apple ProRes 4444 XQ |Да |

## <a name="input-audio-codecs"></a>Входные аудиокодеки
| Входные аудиокодеки | Поддерживаются |
| --- | --- | --- | --- |
| AAC (AAC-LC и AAC-HE, AAC HEv2; копирование too5.1) |Да |
| MPEG Layer 2 |Да |
| MP3 (MPEG-1 Audio Layer 3) |Да |
| Windows Media Audio |Да |
| WAV/PCM |Да |
| [FLAC](https://en.wikipedia.org/wiki/FLAC)</a> |Да |
| [Opus](http://go.microsoft.com/fwlink/?LinkId=822667) |Да |
| [Vorbis](https://en.wikipedia.org/wiki/Vorbis)</a> |Да |
| AMR (adaptive multi-rate) |Да |
| AES (SMPTE 331M и 302M, AES3-2003) |Нет |
| Dolby® E |Нет |
| Dolby® Digital (AC3) |Нет |
| Dolby® Digital Plus (E-AC3) |Нет |

## <a name="output-formats-and-codecs"></a>Выходные форматы и кодеки
Привет, в следующей таблице перечислены hello кодеки и форматы, поддерживаемые для экспорта.

| Формат файла | Видеокодек | Аудиокодек |
| --- | --- | --- |
| MP4  <br/><br/>(включая контейнеры MP4 с несколькими скоростями) |H.264 (профили High, Main и Baselin) |AAC-LC, HE-AAC v1, HE-AAC v2 |
| MPEG2-TS |H.264 (профили High, Main и Baselin) |AAC-LC, HE-AAC v1, HE-AAC v2 |

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Дополнительные материалы
[Кодирование содержимого по запросу с помощью служб мультимедиа Azure](media-services-encode-asset.md)

[Как tooencode стандарту кодировщика мультимедиа](media-services-dotnet-encode-with-media-encoder-standard.md)

