---
title: "aaaEncode ресурс с помощью стандартных кодировщик мультимедиа с hello портал Azure | Документы Microsoft"
description: "Этот учебник поможет выполнить кодирование актива с hello портал Azure с помощью Media Encoder стандартные шаги hello."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 107d9e9a-71e9-43e5-b17c-6e00983aceab
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 0d118bbbe1fa9f4ba0bfa3ea3b10fb541d1d6379
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a>Закодировать ресурс с помощью стандартных кодировщик мультимедиа с hello портал Azure
> [!NOTE]
> toocomplete этого учебника необходима учетная запись Azure. Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

При работе со службами мультимедиа Azure одним из наиболее распространенных сценариев hello разрабатывает tooyour клиентам потоковой передачи с адаптивной скоростью. Службы мультимедиа поддерживают следующие технологии потоковой передачи с адаптивной скоростью hello: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH. tooprepare видео для потоковой передачи с адаптивной скоростью необходимо tooencode источника видео в файлы с разными скоростями. Следует использовать hello **Media Encoder Стандартная** tooencode кодировщик видео.  

Службы мультимедиа также предоставляют динамическую упаковку, позволяющий toodeliver вашей MP4-файлов с несколькими скоростями в hello следующие форматы потоковой передачи: MPEG DASH, HLS, Smooth Streaming, без необходимости toore-package в такие форматы потоковой передачи. При использовании динамической упаковки достаточно toostore и оплаты для hello файлов в едином формате хранилища и службы мультимедиа будут создавать и обслуживать соответствующий ответ hello на основе запросов клиента.

tootake преимущества динамической упаковки необходимо tooencode файла исходного кода в набор MP4-файлов с несколькими скоростями (hello кодирования шаги демонстрируются позже в этом разделе).

носители tooscale обработки, см. [это](media-services-portal-scale-media-processing.md) раздела.

## <a name="encode-with-hello-azure-portal"></a>Кодирование с помощью портала Azure hello
В этом разделе описывается hello может занять tooencode свое содержимое в стандартный кодировщик мультимедиа.

1. В hello [портал Azure](https://portal.azure.com/), выберите учетную запись служб мультимедиа Azure.
2. В hello **параметры** выберите **активы**.  
3. В hello **активы** окно, выберите hello активов, желательно tooencode.
4. Нажмите клавишу hello **Encode** кнопки.
5. В hello **закодировать ресурс** окно, выберите hello «Стандартный кодировщик мультимедиа» процессор и стиль. Дополнительные сведения о предустановках см. в статьях [Использование стандартной версии кодировщика мультимедиа Azure для автоматического создания схемы скоростей](media-services-autogen-bitrate-ladder-with-mes.md) и [Предустановки задач для Media Encoder Standard](media-services-mes-presets-overview.md). Если планируется использовать какие предустановку toocontrol, имейте в виду: важно tooselect hello стиль, лучше всего подходит для ввода видео. Например, если вы знаете, входной видео с разрешением 1920 x 1080 пикселей, затем можно использовать hello «H264 Multiple Bitrate 1080p» стиль. Если у вас есть видео с низким разрешением (640 x 360), не следует использовать предустановку H264 Multiple Bitrate 1080p.
   
   Чтобы упростить управление имеется возможность редактирования hello имя выходной актив hello и hello имя задания hello.
   
   ![Кодирование ресурсов](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. Нажмите кнопку **Создать**.

## <a name="next-step"></a>Дальнейшие действия
Можно отслеживать кодирования ход выполнения задания с hello портал Azure, как описано в [это](media-services-portal-check-job-progress.md) статьи.  

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

