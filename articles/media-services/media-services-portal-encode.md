---
title: "Кодирование ресурса-контейнера с использованием Media Encoder Standard на портале Azure | Документация Майкрософт"
description: "Этот учебник поможет закодировать ресурс-контейнер с помощью Media Encoder Standard на портале Azure."
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
ms.openlocfilehash: a299245e285c4caa68988b184799cd6f4d13e080
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="encode-an-asset-using-media-encoder-standard-with-the-azure-portal"></a><span data-ttu-id="44d83-103">Кодирование ресурса-контейнера с помощью Media Encoder Standard на портале Azure</span><span class="sxs-lookup"><span data-stu-id="44d83-103">Encode an asset using Media Encoder Standard with the Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="44d83-104">Для работы с этим учебником требуется учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="44d83-104">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="44d83-105">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44d83-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="44d83-106">При работе со службами мультимедиа Azure один из самых частых сценариев — доставка потоковой передачи с адаптивным битрейтом клиентам.</span><span class="sxs-lookup"><span data-stu-id="44d83-106">When working with Azure Media Services one of the most common scenarios is delivering adaptive bitrate streaming to your clients.</span></span> <span data-ttu-id="44d83-107">Службы мультимедиа поддерживают следующие технологии потоковой передачи с переменной скоростью: HTTP Live Streaming (HLS), Smooth Streaming и MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="44d83-107">Media Services supports the following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="44d83-108">Чтобы подготовить видео к потоковой передаче с переменной скоростью, необходимо закодировать исходное видео в файлы с поддержкой разных скоростей.</span><span class="sxs-lookup"><span data-stu-id="44d83-108">To prepare your videos for adaptive bitrate streaming, you need to encode your source video into multi-bitrate files.</span></span> <span data-ttu-id="44d83-109">Для кодирования этого видео следует использовать **Media Encoder Standard** .</span><span class="sxs-lookup"><span data-stu-id="44d83-109">You should use the **Media Encoder Standard** encoder to encode your videos.</span></span>  

<span data-ttu-id="44d83-110">Службы мультимедиа также обеспечивают динамическую упаковку, которая позволяет доставлять MP4-файлы с несколькими скоростями в форматах потоковой передачи (MPEG-DASH, HLS, Smooth Streaming) без необходимости повторной упаковки в эти форматы.</span><span class="sxs-lookup"><span data-stu-id="44d83-110">Media Services also provides dynamic packaging which allows you to deliver your multi-bitrate MP4s in the following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having to re-package into these streaming formats.</span></span> <span data-ttu-id="44d83-111">С динамической упаковкой потребуется хранить и оплачивать файлы только в одном формате хранения, а службы мультимедиа выполнят сборку и будут обслуживать соответствующий ответ на основе запросов клиента.</span><span class="sxs-lookup"><span data-stu-id="44d83-111">With dynamic packaging you only need to store and pay for the files in single storage format and Media Services will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="44d83-112">Чтобы воспользоваться динамической упаковкой, закодируйте исходный файл в набор MP4-файлов с поддержкой нескольких скоростей (шаги кодирования показаны далее в этом руководстве).</span><span class="sxs-lookup"><span data-stu-id="44d83-112">To take advantage of dynamic packaging, you need to encode your source file into a set of multi-bitrate MP4 files (the encoding steps are demonstrated later in this section).</span></span>

<span data-ttu-id="44d83-113">Масштабирование обработки мультимедиа описано в [этом](media-services-portal-scale-media-processing.md) разделе.</span><span class="sxs-lookup"><span data-stu-id="44d83-113">To scale media processing, see [this](media-services-portal-scale-media-processing.md) topic.</span></span>

## <a name="encode-with-the-azure-portal"></a><span data-ttu-id="44d83-114">Кодирование с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="44d83-114">Encode with the Azure portal</span></span>
<span data-ttu-id="44d83-115">В этом разделе описаны шаги, которые можно предпринять для кодирования содержимого с помощью стандартного кодировщика служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="44d83-115">This section describes the steps you can take to encode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="44d83-116">Создание учетной записи служб мультимедиа Azure с помощью [портале Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="44d83-116">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="44d83-117">В окне **Параметры** выберите элемент **Ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="44d83-117">In the **Settings** window, select **Assets**.</span></span>  
3. <span data-ttu-id="44d83-118">В окне **Ресурсы-контейнеры** выберите ресурс, который требуется закодировать.</span><span class="sxs-lookup"><span data-stu-id="44d83-118">In the **Assets** window, select the asset that you would like to encode.</span></span>
4. <span data-ttu-id="44d83-119">Нажмите кнопку **Кодировать** .</span><span class="sxs-lookup"><span data-stu-id="44d83-119">Press the **Encode** button.</span></span>
5. <span data-ttu-id="44d83-120">В окне**кодирования ресурса** выберите обработчик Media Encoder Standard с предустановкой.</span><span class="sxs-lookup"><span data-stu-id="44d83-120">In the **Encode an asset** window, select the "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="44d83-121">Дополнительные сведения о предустановках см. в статьях [Использование стандартной версии кодировщика мультимедиа Azure для автоматического создания схемы скоростей](media-services-autogen-bitrate-ladder-with-mes.md) и [Предустановки задач для Media Encoder Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="44d83-121">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="44d83-122">Если вы планируете контролировать используемую предустановку кодирования, не забывайте следующее правило: важно выбрать предустановку в соответствии с параметрами входного видео.</span><span class="sxs-lookup"><span data-stu-id="44d83-122">If you plan to control which encoding preset is used, keep this in mind: it is important to select the preset that is most appropriate for your input video.</span></span> <span data-ttu-id="44d83-123">Например, если известно, что исходное видео имеет разрешение 1920 x 1080 пикселей, можно использовать предустановку "H264 Multiple Bitrate 1080p".</span><span class="sxs-lookup"><span data-stu-id="44d83-123">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use the "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="44d83-124">Если у вас есть видео с низким разрешением (640 x 360), не следует использовать предустановку H264 Multiple Bitrate 1080p.</span><span class="sxs-lookup"><span data-stu-id="44d83-124">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="44d83-125">Для упрощения управления предусмотрена возможность изменения имени выходного ресурса и задания.</span><span class="sxs-lookup"><span data-stu-id="44d83-125">For easier management, you have an option of editing the name of the output asset, and the name of the job.</span></span>
   
   ![Кодирование ресурсов](./media/media-services-portal-vod-get-started/media-services-encode1.png)
6. <span data-ttu-id="44d83-127">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="44d83-127">Press **Create**.</span></span>

## <a name="next-step"></a><span data-ttu-id="44d83-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="44d83-128">Next step</span></span>
<span data-ttu-id="44d83-129">Можно отслеживать выполнение задания кодирования с помощью портала Azure, как описано в [этой](media-services-portal-check-job-progress.md) статье.</span><span class="sxs-lookup"><span data-stu-id="44d83-129">You can monitor encoding job progress with the Azure portal, as described in [this](media-services-portal-check-job-progress.md) article.</span></span>  

## <a name="media-services-learning-paths"></a><span data-ttu-id="44d83-130">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="44d83-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="44d83-131">Отзывы</span><span class="sxs-lookup"><span data-stu-id="44d83-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

