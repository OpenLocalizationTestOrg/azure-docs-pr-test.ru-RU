---
title: "aaaMedia расширенного рабочего процесса кодировщика форматы и кодеки | Документы Microsoft"
description: "В этом разделе содержится обзор форматов и кодеков расширенного рабочего процесса кодировщика мультимедиа."
services: media-services
documentationcenter: 
author: juliako
manager: erik43
editor: 
ms.assetid: b197fce8-3b9b-4189-8d08-486810c0426f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;anilmur
ms.openlocfilehash: e781384ca8f08926f00c83b6710fd413ce2a3e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-premium-workflow-formats-and-codecs"></a>Форматы и кодеки рабочего процесса Premium Media Encoder
> [!NOTE]
> Вопросы о кодировщике Premium направляйте по адресу mepd@microsoft.com.
> 
> Обработчик мультимедиа расширенного рабочего процесса кодировщика мультимедиа, рассматриваемый в этом разделе, недоступен в Китае. 
> 
> 

Этот документ содержит список входных и выходных файлов форматы и кодеки, поддерживаемыми hello общедоступной предварительной версии hello **расширенного рабочего процесса кодировщика мультимедиа** кодировщика.

[Входные форматы и кодеки расширенного рабочего процесса кодировщика мультимедиа](#input_formats)

[Выходные форматы и кодеки расширенного рабочего процесса кодировщика мультимедиа](#output_formats)

**Расширенный рабочий процесс кодировщика мультимедиа** поддерживает скрытые субтитры, описанные в [этом](#closed_captioning) разделе. 

## <a id="input_formats"></a>Входные форматы и кодеки расширенного рабочего процесса кодировщика мультимедиа
Привет, в следующем разделе перечислены hello кодеков и форматов файлов, этот обработчик мультимедиа поддерживает в качестве входных данных.

### <a name="input-containerfile-formats"></a>Контейнер ввода/ форматы файлов
* Adobe® Flash® F4V
* MXF/SMPTE 377M
* GXF
* Транспортные потоки MPEG-2
* Программные потоки MPEG-2
* MPEG-4/MP4
* Windows Media/ASF
* AVI (без сжатия 8 бит/10 бит)

### <a name="input-video-codecs"></a>Входные видеокодеки
* AVC 8-разрядное/10-битный, копирование too4:2:2, включая AVCIntra
* Avid DNxHD (в MXF)
* DVCPro/DVCProHD (в MXF)
* JPEG2000
* MPEG-2 (профиль too422 и высокого уровня, включая варианты, такие как XDCAM, XDCAM HD, XDCAM IMX, CableLabs® и D10)
* MPEG-1
* Windows Media Video/VC-1

### <a name="input-audio-codecs"></a>Входные аудиокодеки
* AES (SMPTE 331M и 302M, AES3-2003)
* Dolby® E
* Dolby® Digital (AC3)
* AAC (AAC-LC и AAC-HE, AAC HEv2; копирование too5.1)
* MPEG Layer 2
* MP3 (MPEG-1 Audio Layer 3)
* Windows Media Audio
* WAV/PCM

## <a id="output_format"></a>Выходные форматы и кодеки расширенного рабочего процесса кодировщика мультимедиа
Hello в подразделе ниже приведены hello кодеки и форматы, поддерживаемые в качестве выходных данных из этого обработчика мультимедиа.

### <a name="output-containerfile-formats"></a>Контейнер вывода/ форматы файлов
* Adobe® Flash® F4V
* MXF (OP1a, XDCAM и AS02)
* DPP (включая AS11)
* GXF
* MPEG-4/MP4
* Windows Media/ASF
* AVI (без сжатия 8 бит/10 бит)
* Формат файлов Smooth Streaming (PIFF 1.3)
* MPEG-TS 

### <a name="output-video-codecs"></a>Выходные видеокодеки
* AVC (H.264; 8-разрядное; Настройка tooHigh профиля, уровень 5.2; Ultra HD 4 КБ; Внутри AVC)
* Avid DNxHD (в MXF)
* DVCPro/DVCProHD (в MXF)
* MPEG-2 (профиль too422 и высокого уровня, включая варианты, такие как XDCAM, XDCAM HD, XDCAM IMX, CableLabs® и D10)
* MPEG-1
* Windows Media Video/VC-1
* Создание эскизов JPEG

### <a name="output-audio-codecs"></a>Выходные аудиокодеки
* AES (SMPTE 331M и 302M, AES3-2003)
* Dolby® Digital (AC3)
* Dolby® Digital Plus (E-AC3) вверх too7.1
* AAC (AAC-LC и AAC-HE, AAC HEv2; копирование too5.1)
* MPEG Layer 2
* MP3 (MPEG-1 Audio Layer 3)
* Windows Media Audio

>[!NOTE]
>Если кодирование tooDolby® Digital (AC3) hello вывода можно записать только в ISO MP4-файл.

## <a id="closed_captioning"></a>Поддержка скрытых титров
При приеме **расширенный рабочий процесс кодировщика мультимедиа** поддерживает:

1. файлы SCC
2. файлы SMPTE-TT
3. CEA-608/CEA-708 – переносятся как данные пользователя (сообщения SEI простейших потоков H.264, ATSC/53, SCTE20) или переносятся как вспомогательные данные в файлах MXF/GXF
4. Файлы субтитров STL

На выходе доступны следующие варианты hello.

1. Перевод CEA 608 tooCEA 708
2. Пропуск CEA-608/CEA-708 (встраиваются в сообщения SEI простейших потоков H.264 или переносятся как дополнительные данный в файлах MXF)
3. SCC
4. SMPTE Timed Text (из источника CEA-608 через SMPTE RP2052, включая создание файла DFXP)
5. Файл подзаголовка SRT
6. Потоки подзаголовка DVB

Примечание: не все hello выше выходных форматов поддерживаются для передачи с помощью потоковой передачи в службах мультимедиа Azure.

## <a name="known-issues"></a>Известные проблемы
Если входной видео не содержит титров, hello выходной ресурс по-прежнему будет содержать пустой файл TTML. 

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

