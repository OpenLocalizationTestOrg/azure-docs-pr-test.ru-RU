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
# <a name="encode-an-asset-using-media-encoder-standard-with-hello-azure-portal"></a><span data-ttu-id="d5d8c-103">Закодировать ресурс с помощью стандартных кодировщик мультимедиа с hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="d5d8c-103">Encode an asset using Media Encoder Standard with hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="d5d8c-104">toocomplete этого учебника необходима учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="d5d8c-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="d5d8c-105">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d5d8c-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="d5d8c-106">При работе со службами мультимедиа Azure одним из наиболее распространенных сценариев hello разрабатывает tooyour клиентам потоковой передачи с адаптивной скоростью.</span><span class="sxs-lookup"><span data-stu-id="d5d8c-106">When working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="d5d8c-107">Службы мультимедиа поддерживают следующие технологии потоковой передачи с адаптивной скоростью hello: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="d5d8c-107">Media Services supports hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="d5d8c-108">tooprepare видео для потоковой передачи с адаптивной скоростью необходимо tooencode источника видео в файлы с разными скоростями.</span><span class="sxs-lookup"><span data-stu-id="d5d8c-108">tooprepare your videos for adaptive bitrate streaming, you need tooencode your source video into multi-bitrate files.</span></span> <span data-ttu-id="d5d8c-109">Следует использовать hello **Media Encoder Стандартная** tooencode кодировщик видео.</span><span class="sxs-lookup"><span data-stu-id="d5d8c-109">You should use hello **Media Encoder Standard** encoder tooencode your videos.</span></span>  

<span data-ttu-id="d5d8c-110">Службы мультимедиа также предоставляют динамическую упаковку, позволяющий toodeliver вашей MP4-файлов с несколькими скоростями в hello следующие форматы потоковой передачи: MPEG DASH, HLS, Smooth Streaming, без необходимости toore-package в такие форматы потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="d5d8c-110">Media Services also provides dynamic packaging which allows you toodeliver your multi-bitrate MP4s in hello following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having toore-package into these streaming formats.</span></span> <span data-ttu-id="d5d8c-111">При использовании динамической упаковки достаточно toostore и оплаты для hello файлов в едином формате хранилища и службы мультимедиа будут создавать и обслуживать соответствующий ответ hello на основе запросов клиента.</span><span class="sxs-lookup"><span data-stu-id="d5d8c-111">With dynamic packaging you only need toostore and pay for hello files in single storage format and Media Services will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="d5d8c-112">tootake преимущества динамической упаковки необходимо tooencode файла исходного кода в набор MP4-файлов с несколькими скоростями (hello кодирования шаги демонстрируются позже в этом разделе).</span><span class="sxs-lookup"><span data-stu-id="d5d8c-112">tootake advantage of dynamic packaging, you need tooencode your source file into a set of multi-bitrate MP4 files (hello encoding steps are demonstrated later in this section).</span></span>

<span data-ttu-id="d5d8c-113">носители tooscale обработки, см. [это](media-services-portal-scale-media-processing.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="d5d8c-113">tooscale media processing, see [this](media-services-portal-scale-media-processing.md) topic.</span></span>

## <a name="encode-with-hello-azure-portal"></a><span data-ttu-id="d5d8c-114">Кодирование с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="d5d8c-114">Encode with hello Azure portal</span></span>
<span data-ttu-id="d5d8c-115">В этом разделе описывается hello может занять tooencode свое содержимое в стандартный кодировщик мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="d5d8c-115">This section describes hello steps you can take tooencode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="d5d8c-116">В hello [портал Azure](https://portal.azure.com/), выберите учетную запись служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="d5d8c-116">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="d5d8c-117">В hello **параметры** выберите **активы**.</span><span class="sxs-lookup"><span data-stu-id="d5d8c-117">In hello **Settings** window, select **Assets**.</span></span>  
3. <span data-ttu-id="d5d8c-118">В hello **активы** окно, выберите hello активов, желательно tooencode.</span><span class="sxs-lookup"><span data-stu-id="d5d8c-118">In hello **Assets** window, select hello asset that you would like tooencode.</span></span>
4. <span data-ttu-id="d5d8c-119">Нажмите клавишу hello **Encode** кнопки.</span><span class="sxs-lookup"><span data-stu-id="d5d8c-119">Press hello **Encode** button.</span></span>
5. <span data-ttu-id="d5d8c-120">В hello **закодировать ресурс** окно, выберите hello «Стандартный кодировщик мультимедиа» процессор и стиль.</span><span class="sxs-lookup"><span data-stu-id="d5d8c-120">In hello **Encode an asset** window, select hello "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="d5d8c-121">Дополнительные сведения о предустановках см. в статьях [Использование стандартной версии кодировщика мультимедиа Azure для автоматического создания схемы скоростей](media-services-autogen-bitrate-ladder-with-mes.md) и [Предустановки задач для Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d5d8c-121">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="d5d8c-122">Если планируется использовать какие предустановку toocontrol, имейте в виду: важно tooselect hello стиль, лучше всего подходит для ввода видео.</span><span class="sxs-lookup"><span data-stu-id="d5d8c-122">If you plan toocontrol which encoding preset is used, keep this in mind: it is important tooselect hello preset that is most appropriate for your input video.</span></span> <span data-ttu-id="d5d8c-123">Например, если вы знаете, входной видео с разрешением 1920 x 1080 пикселей, затем можно использовать hello «H264 Multiple Bitrate 1080p» стиль.</span><span class="sxs-lookup"><span data-stu-id="d5d8c-123">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use hello "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="d5d8c-124">Если у вас есть видео с низким разрешением (640 x 360), не следует использовать предустановку H264 Multiple Bitrate 1080p.</span><span class="sxs-lookup"><span data-stu-id="d5d8c-124">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="d5d8c-125">Чтобы упростить управление имеется возможность редактирования hello имя выходной актив hello и hello имя задания hello.</span><span class="sxs-lookup"><span data-stu-id="d5d8c-125">For easier management, you have an option of editing hello name of hello output asset, and hello name of hello job.</span></span>
   
   ![Кодирование ресурсов](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. <span data-ttu-id="d5d8c-127">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d5d8c-127">Press **Create**.</span></span>

## <a name="next-step"></a><span data-ttu-id="d5d8c-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d5d8c-128">Next step</span></span>
<span data-ttu-id="d5d8c-129">Можно отслеживать кодирования ход выполнения задания с hello портал Azure, как описано в [это](media-services-portal-check-job-progress.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="d5d8c-129">You can monitor encoding job progress with hello Azure portal, as described in [this](media-services-portal-check-job-progress.md) article.</span></span>  

## <a name="media-services-learning-paths"></a><span data-ttu-id="d5d8c-130">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="d5d8c-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d5d8c-131">Отзывы</span><span class="sxs-lookup"><span data-stu-id="d5d8c-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

