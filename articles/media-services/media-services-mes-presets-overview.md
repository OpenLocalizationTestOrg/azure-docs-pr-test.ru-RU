---
title: "aaaTask предустановки для MES (стандартный кодировщик мультимедиа) | Документы Microsoft"
description: "раздел содержит Hello и обзор предустановки задачи для MES (стандартный кодировщик мультимедиа)."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: f243ed1c-ac9c-4300-a5f7-f092cf9853b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 56e098d6d8c8f84031421ec59f087f20370ba111
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="task-presets-for-mes-media-encoder-standard"></a>Предустановки задач для Media Encoder Standard

**Media Encoder Standard** определяет набор предустановок кодирования, которые можно использовать при создании заданий кодирования. Рекомендуется toouse hello, «Адаптивной потоковой передачи» предварительную настройку, если вы хотите tooencode видео для потоковой передачи с помощью служб мультимедиа. Если указать эту предустановку, то Media Encoder Standard [автоматически создаст таблицу скоростей и разрешений](media-services-autogen-bitrate-ladder-with-mes.md). 

Тем не менее если требуется toocustomize предустановку следует один из стандартных параметров, заданные в этом разделе в качестве шаблона для пользовательской конфигурации кодирования hello. Объяснение какие каждого элемента в этих стилей означает и hello допустимые значения для каждого элемента в разделе hello [Media Encoder стандартной схеме](media-services-mes-schema.md) раздела.  
  
> [!NOTE]
>  При использовании стиля кодирует 4 КБ, вы должны получить hello `S3` зарезервировано тип единицы измерения. Дополнительные сведения см. в разделе [как tooScale кодировка](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).  
  
При работе с Media Encoder Standard поворот включен по умолчанию. Если видео записываются на смартфоне или другого мобильного устройства в книжной ориентации, то эти стили по умолчанию вращается их tooLandscape tooencoding предыдущий режим (в отличие от, при работе с Azure Media Encoder, где видео поворота — вручную, как описано в документе [это](http://azure.microsoft.com/blog/2014/08/21/advanced-encoding-features-in-azure-media-encoder/) блога, в разделе «Видео поворота»).  
  
Доступные предустановки:  
  
 [H264 Multiple Bitrate 1080p звук 5.1](media-services-mes-preset-H264-Multiple-Bitrate-1080p-Audio-5.1.md) создается набор 8 GOP-файлами формата MP4, начиная от 6000 Кбит/с too400, Кбит/с и звук AAC 5.1.  
  
 [H264 Multiple Bitrate 1080p](media-services-mes-preset-H264-Multiple-Bitrate-1080p.md) создается набор 8 GOP-файлами формата MP4, начиная от 6000 Кбит/с too400, Кбит/с и стереозвук AAC.  
  
 [H264 Multiple Bitrate 16 x 9 для iOS](media-services-mes-preset-H264-Multiple-Bitrate-16x9-for-iOS.md) создается набор 8 GOP-файлами формата MP4, начиная от Кбит/с too200 8500 Кбит/с и стереозвук AAC.  
  
 [H264 Multiple Bitrate 16 x 9 SD звук 5.1](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD-Audio-5.1.md) создается набор 5 GOP-файлами формата MP4, начиная от 1900 Кбит/с too400, Кбит/с и звук AAC 5.1.  
  
 [H264 Multiple Bitrate 16 x 9 SD](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD.md) создается набор 5 GOP-файлами формата MP4, начиная от 1900 Кбит/с too400, Кбит/с и стереозвук AAC.  
  
 [H264 Multiple Bitrate 4K звук 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4K-Audio-5.1.md) создается набор 12 GOP-файлами формата MP4, начиная от 20000 Кбит/с too1000 Кбит/с и звук AAC 5.1.  
  
 [H264 Multiple Bitrate 4K](media-services-mes-preset-H264-Multiple-Bitrate-4K.md) создается набор 12 GOP-файлами формата MP4, начиная от 20000 Кбит/с too1000 Кбит/с и стереозвук AAC.  
  
 [H264 Multiple Bitrate 4 x 3 для iOS](media-services-mes-preset-H264-Multiple-Bitrate-4x3-for-iOS.md) создается набор 8 GOP-файлами формата MP4, начиная от Кбит/с too200 8500 Кбит/с и стереозвук AAC.  
  
 [H264 Multiple Bitrate 4 x 3 SD звук 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD-Audio-5.1.md) создается набор 5 GOP-файлами формата MP4, начиная от Кбит/с too400 1600 Кбит/с и звук AAC 5.1.  
  
 [H264 Multiple Bitrate 4 x 3 SD](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD.md) создается набор 5 GOP-файлами формата MP4, начиная от Кбит/с too400 1600 Кбит/с и стереозвук AAC.  
  
 [H264 Multiple Bitrate 720p звук 5.1](media-services-mes-preset-H264-Multiple-Bitrate-720p-Audio-5.1.md) создается набор 6 GOP-файлами формата MP4, начиная от 3400 Кбит/с too400, Кбит/с и звук AAC 5.1.  
  
 [H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) создается набор 6 GOP-файлами формата MP4, начиная от 3400 Кбит/с too400, Кбит/с и стереозвук AAC.  
  
 [H264 Single Bitrate 1080p Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-1080p-Audio-5.1.md). Данная предустановка создает отдельный MP4-файл со скоростью 6750 Кбит/с и звуком в формате AAC 5.1.  
  
 [H264 Single Bitrate 1080p](media-services-mes-preset-H264-Single-Bitrate-1080p.md). Данная предустановка создает отдельный MP4-файл со скоростью 6750 Кбит/с и стереофоническим звуком в формате AAC.  
  
 [H264 Single Bitrate 4K Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4K-Audio-5.1.md). Данная предустановка создает отдельный MP4-файл со скоростью 18 000 Кбит/с и звуком в формате AAC 5.1.  
  
 [H264 Single Bitrate 4K](media-services-mes-preset-H264-Single-Bitrate-4K.md). Данная предустановка создает отдельный MP4-файл со скоростью 18 000 Кбит/с и стереофоническим звуком в формате AAC.  
  
 [H264 Single Bitrate 4x3 SD Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4x3-SD-Audio-5.1.md). Данная предустановка создает отдельный MP4-файл со скоростью 1800 Кбит/с и звуком в формате AAC 5.1.  
  
 [H264 Single Bitrate 4x3 SD](media-services-mes-preset-H264-Single-Bitrate-4x3-SD.md). Данная предустановка создает отдельный MP4-файл со скоростью 1800 Кбит/с и стереофоническим звуком в формате AAC.  
  
 [H264 Single Bitrate 16x9 SD Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-16x9-SD-Audio-5.1.md). Данная предустановка создает отдельный MP4-файл со скоростью 2200 Кбит/с и звуком в формате AAC 5.1.  
  
 [H264 Single Bitrate 16x9 SD](media-services-mes-preset-H264-Single-Bitrate-16x9-SD.md). Данная предустановка создает отдельный MP4-файл со скоростью 2200 Кбит/с и стереофоническим звуком в формате AAC.  
  
 [H264 Single Bitrate 720p Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-720p-Audio-5.1.md). Данная предустановка создает отдельный MP4-файл со скоростью 4500 Кбит/с и звуком в формате AAC 5.1.  
  
 [H264 Single Bitrate 720p для Android](media-services-mes-preset-H264-Single-Bitrate-720p-for-Android.md). Данная предустановка создает отдельный MP4-файл со скоростью 2000 Кбит/с и стереофоническим звуком в формате AAC.  
  
 [H264 Single Bitrate 720p](media-services-mes-preset-H264-Single-Bitrate-720p.md). Данная предустановка создает отдельный MP4-файл со скоростью 4500 Кбит/с и стереофоническим звуком в формате AAC.  
  
 [H264 Single Bitrate High Quality SD для Android](media-services-mes-preset-H264-Single-Bitrate-High-Quality-SD-for-Android.md). Данная предустановка создает отдельный MP4-файл со скоростью 500 Кбит/с и стереофоническим звуком в формате AAC.  
  
 [H264 Single Bitrate Low Quality SD для Android](media-services-mes-preset-H264-Single-Bitrate-Low-Quality-SD-for-Android.md). Данная предустановка создает отдельный MP4-файл со скоростью 56 Кбит/с и стереофоническим звуком в формате AAC.  
  
 Дополнительные сведения см. связанные tooMedia кодировщика служб, [кодирования по запросу с помощью служб мультимедиа Azure](https://azure.microsoft.com/en-us/documentation/articles/media-services-encode-asset/).
