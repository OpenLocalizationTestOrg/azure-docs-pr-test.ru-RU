---
title: "Часто задаваемые вопросы по службам мультимедиа Azure | Документация Майкрософт"
description: "Часто задаваемые вопросы (FAQ)"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 48f3924d44a084d61c1d38002cd5098094001acb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="frequently-asked-questions"></a><span data-ttu-id="565c8-103">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="565c8-103">Frequently asked questions</span></span>

<span data-ttu-id="565c8-104">В этой статье рассматриваются часто задаваемые вопросы сообщества пользователей служб мультимедиа Azure (AMS).</span><span class="sxs-lookup"><span data-stu-id="565c8-104">This article addresses frequently asked questions raised by the Azure Media Services (AMS) user community.</span></span>

## <a name="general-ams-faqs"></a><span data-ttu-id="565c8-105">Общие часто задаваемые вопросы об AMS и ответы на них</span><span class="sxs-lookup"><span data-stu-id="565c8-105">General AMS FAQs</span></span>
<span data-ttu-id="565c8-106">Вопрос. Как осуществляется масштабирование индексирования?</span><span class="sxs-lookup"><span data-stu-id="565c8-106">Q: How do you scale indexing?</span></span>

<span data-ttu-id="565c8-107">Ответ. Зарезервированные единицы одинаковы для задач кодирования и индексирования.</span><span class="sxs-lookup"><span data-stu-id="565c8-107">A: The reserved units are the same for Encoding and Indexing tasks.</span></span> <span data-ttu-id="565c8-108">Следуйте инструкциям в разделе о [масштабировании зарезервированных единиц кодирования](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="565c8-108">Follow instructions on [How to Scale Encoding Reserved Units](media-services-scale-media-processing-overview.md).</span></span> <span data-ttu-id="565c8-109">**Обратите внимание**, что производительность индексирования не зависит от типа зарезервированных единиц.</span><span class="sxs-lookup"><span data-stu-id="565c8-109">**Note** that Indexer performance is not affected by Reserved Unit Type.</span></span>

<span data-ttu-id="565c8-110">Вопрос. Видео отправлено, закодировано и опубликовано.</span><span class="sxs-lookup"><span data-stu-id="565c8-110">Q: I uploaded, encoded, and published a video.</span></span> <span data-ttu-id="565c8-111">Почему видео не воспроизводится?</span><span class="sxs-lookup"><span data-stu-id="565c8-111">What would be the reason the video does not play when I try to stream it?</span></span>

<span data-ttu-id="565c8-112">Ответ. Чаще всего это вызвано отсутствием конечной точки потоковой передачи, из которой выполняется попытка воспроизведения в состоянии **Выполняется**.</span><span class="sxs-lookup"><span data-stu-id="565c8-112">A: One of the most common reasons is you do not have the streaming endpoint from which you are trying to playback in the **Running** state.</span></span>  

<span data-ttu-id="565c8-113">Вопрос. Можно ли объединять видео в динамическом потоке?</span><span class="sxs-lookup"><span data-stu-id="565c8-113">Q: Can I do compositing on a live stream?</span></span>

<span data-ttu-id="565c8-114">Ответ. Объединение видео в динамических потоках в настоящее время не поддерживается в службах мультимедиа Azure, поэтому необходимо объединить видео заранее на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="565c8-114">A: Compositing on live streams is currently not offered in Azure Media Services, so you would need to pre-compose on your computer.</span></span>

<span data-ttu-id="565c8-115">Вопрос. Можно ли использовать Azure CDN с динамической потоковой передачей?</span><span class="sxs-lookup"><span data-stu-id="565c8-115">Q: Can I use Azure CDN with Live Streaming?</span></span>

<span data-ttu-id="565c8-116">Ответ. Службы мультимедиа поддерживают интеграцию с Azure CDN (дополнительные сведения см. в статье [Управление конечными точками потоковой передачи с помощью портала Azure](media-services-portal-manage-streaming-endpoints.md)).</span><span class="sxs-lookup"><span data-stu-id="565c8-116">A: Media Services supports integration with Azure CDN (for more information, see [How to Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)).</span></span>  <span data-ttu-id="565c8-117">Вы можете использовать динамическую потоковую передачу с CDN.</span><span class="sxs-lookup"><span data-stu-id="565c8-117">You can use Live streaming with CDN.</span></span> <span data-ttu-id="565c8-118">Службы мультимедиа Azure предоставляют выходные данные в форматах Smooth Streaming, HLS и MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="565c8-118">Azure Media Services provides Smooth Streaming, HLS and MPEG-DASH outputs.</span></span> <span data-ttu-id="565c8-119">Все они используют протокол HTTP для передачи данных, а также кэширование HTTP.</span><span class="sxs-lookup"><span data-stu-id="565c8-119">All these formats use HTTP for transferring data and get benefits of HTTP caching.</span></span> <span data-ttu-id="565c8-120">При динамической потоковой передаче фактические аудио- или видеоданные делятся на фрагменты, которые кэшируются в сети CDN.</span><span class="sxs-lookup"><span data-stu-id="565c8-120">In live streaming actual video/audio data is divided to fragments and this individual fragments get cached in CDN.</span></span> <span data-ttu-id="565c8-121">Обновлять необходимо только данные манифеста.</span><span class="sxs-lookup"><span data-stu-id="565c8-121">Only data needs to be refreshed is the manifest data.</span></span> <span data-ttu-id="565c8-122">CDN периодически обновляет данные манифеста.</span><span class="sxs-lookup"><span data-stu-id="565c8-122">CDN periodically refreshes manifest data.</span></span>

<span data-ttu-id="565c8-123">Вопрос. Службы мультимедиа Azure поддерживают хранение изображений?</span><span class="sxs-lookup"><span data-stu-id="565c8-123">Q: Does Azure Media services support storing images?</span></span>

<span data-ttu-id="565c8-124">Ответ. Если вы хотите просто хранить JPEG- или PNG-изображения, используйте для этого хранилище двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="565c8-124">A: If you are just looking to store JPEG or PNG images, you should keep those in Azure Blob Storage.</span></span> <span data-ttu-id="565c8-125">Не имеет смысла хранить их в вашей учетной записи служб мультимедиа, если вы не хотите связать их с видео- или аудиоресурсами.</span><span class="sxs-lookup"><span data-stu-id="565c8-125">There is no benefit to putting them in your Media Services account unless you want to keep them associated with your Video or Audio Assets.</span></span> <span data-ttu-id="565c8-126">Или вам может понадобиться использовать наложение изображений в видеокодировщике. Стандартный кодировщик мультимедиа поддерживает наложение изображений на видео, поэтому JPEG и PNG указаны как поддерживаемые форматы входных данных.</span><span class="sxs-lookup"><span data-stu-id="565c8-126">Or if you might have a need to use the images as overlays in the video encoder.Media Encoder Standard supports overlaying images on top of videos, and that is what it lists JPEG and PNG as supported input formats.</span></span> <span data-ttu-id="565c8-127">Дополнительные сведения см. в статье [Создание наложений](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="565c8-127">For more information, see [Creating Overlays](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

<span data-ttu-id="565c8-128">Вопрос. Как можно скопировать активы из одной учетной записи служб мультимедиа в другую?</span><span class="sxs-lookup"><span data-stu-id="565c8-128">Q: How can I copy assets from one Media Services account to another.</span></span>

<span data-ttu-id="565c8-129">Ответ. Для копирования ресурсов-контейнер из одной учетной записи служб мультимедиа в другую с помощью .NET используйте метод расширения [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354), доступный в репозитории [Расширения пакета SDK служб мультимедиа Azure для .NET](https://github.com/Azure/azure-sdk-for-media-services-extensions/).</span><span class="sxs-lookup"><span data-stu-id="565c8-129">A: To copy assets from one Media Services account to another using .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) extension method available in the [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span></span> <span data-ttu-id="565c8-130">Дополнительные сведения см. в [этой теме форума](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices).</span><span class="sxs-lookup"><span data-stu-id="565c8-130">For more information, see [this](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span></span>

<span data-ttu-id="565c8-131">Вопрос. Какие знаки поддерживаются в именах файлов при работе с AMS?</span><span class="sxs-lookup"><span data-stu-id="565c8-131">Q: What are the supported characters for naming files when working with AMS?</span></span>

<span data-ttu-id="565c8-132">Службы мультимедиа используют значение свойства IAssetFile.Name при создании URL-адресов для потоковой передачи содержимого (например, http://{учетная запись AMS}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) По этой причине кодирование с помощью знака процента не допускается.</span><span class="sxs-lookup"><span data-stu-id="565c8-132">A: Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="565c8-133">Значение свойства **Name** не может содержать такие [зарезервированные знаки, используемые для кодировки URL-адресов](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span><span class="sxs-lookup"><span data-stu-id="565c8-133">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="565c8-134">Кроме того, может использоваться только один знак ".".</span><span class="sxs-lookup"><span data-stu-id="565c8-134">Also, there can only be one ‘.’</span></span> <span data-ttu-id="565c8-135">Кроме того, может использоваться только один символ "." для расширения имени файла.</span><span class="sxs-lookup"><span data-stu-id="565c8-135">for the file name extension.</span></span>

<span data-ttu-id="565c8-136">Вопрос. Как можно подключиться с помощью REST?</span><span class="sxs-lookup"><span data-stu-id="565c8-136">Q: How to connect using REST?</span></span>

<span data-ttu-id="565c8-137">Ответ. Сведения о подключении к API AMS см. в разделе [Доступ к API служб мультимедиа Azure с помощью аутентификации Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="565c8-137">A: For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> <span data-ttu-id="565c8-138">После успешного подключения к https://media.windows.net вы получите ошибку 301 (перенаправление), в которой будет указан другой URI служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="565c8-138">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="565c8-139">Используйте для последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="565c8-139">You must make subsequent calls to the new URI.</span></span> 

<span data-ttu-id="565c8-140">Вопрос. Как повернуть видео в процессе кодирования?</span><span class="sxs-lookup"><span data-stu-id="565c8-140">Q: How can I rotate a video during the encoding process.</span></span>

<span data-ttu-id="565c8-141">Ответ. [Стандартный кодировщик служб мультимедиа](media-services-dotnet-encode-with-media-encoder-standard.md) поддерживает поворот на 90, 180 или 270 градусов.</span><span class="sxs-lookup"><span data-stu-id="565c8-141">A: The [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 90/180/270.</span></span> <span data-ttu-id="565c8-142">По умолчанию задается значение Auto, при котором система пытается обнаружить метаданные поворота во входящем файле MP4/MOV и обеспечить соответствующую компенсацию.</span><span class="sxs-lookup"><span data-stu-id="565c8-142">The default behavior is "Auto", where it tries to detect the rotation metadata in the incoming MP4/MOV file and compensate for it.</span></span> <span data-ttu-id="565c8-143">Включите следующий элемент **Sources** в одну из предустановок JSON, определенных [здесь](media-services-mes-presets-overview.md):</span><span class="sxs-lookup"><span data-stu-id="565c8-143">Include the following **Sources** element to one of the json presets defined [here](media-services-mes-presets-overview.md):</span></span>

    "Version": 1.0,
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...


## <a name="media-services-learning-paths"></a><span data-ttu-id="565c8-144">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="565c8-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="565c8-145">Отзывы</span><span class="sxs-lookup"><span data-stu-id="565c8-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
