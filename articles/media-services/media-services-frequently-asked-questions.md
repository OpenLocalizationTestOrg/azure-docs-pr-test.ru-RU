---
title: "aaaAzure Media Services часто задаваемые вопросы | Документы Microsoft"
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
ms.openlocfilehash: 6d48a5c1291f3c2559d8445921d571718d0a0a6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions"></a><span data-ttu-id="bebad-103">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="bebad-103">Frequently asked questions</span></span>

<span data-ttu-id="bebad-104">В этой статье рассматриваются часто задаваемые вопросы hello сообщества пользователей служб мультимедиа Azure (AMS).</span><span class="sxs-lookup"><span data-stu-id="bebad-104">This article addresses frequently asked questions raised by hello Azure Media Services (AMS) user community.</span></span>

## <a name="general-ams-faqs"></a><span data-ttu-id="bebad-105">Общие часто задаваемые вопросы об AMS и ответы на них</span><span class="sxs-lookup"><span data-stu-id="bebad-105">General AMS FAQs</span></span>
<span data-ttu-id="bebad-106">Вопрос. Как осуществляется масштабирование индексирования?</span><span class="sxs-lookup"><span data-stu-id="bebad-106">Q: How do you scale indexing?</span></span>

<span data-ttu-id="bebad-107">Ответ hello зарезервированных единиц hello же для кодировки и задачи индексирования.</span><span class="sxs-lookup"><span data-stu-id="bebad-107">A: hello reserved units are hello same for Encoding and Indexing tasks.</span></span> <span data-ttu-id="bebad-108">Следуйте инструкциям на [как кодирование зарезервированных единиц tooScale](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bebad-108">Follow instructions on [How tooScale Encoding Reserved Units](media-services-scale-media-processing-overview.md).</span></span> <span data-ttu-id="bebad-109">**Обратите внимание**, что производительность индексирования не зависит от типа зарезервированных единиц.</span><span class="sxs-lookup"><span data-stu-id="bebad-109">**Note** that Indexer performance is not affected by Reserved Unit Type.</span></span>

<span data-ttu-id="bebad-110">Вопрос. Видео отправлено, закодировано и опубликовано.</span><span class="sxs-lookup"><span data-stu-id="bebad-110">Q: I uploaded, encoded, and published a video.</span></span> <span data-ttu-id="bebad-111">Было бы hello причина hello видео не воспроизводится при попытке toostream его?</span><span class="sxs-lookup"><span data-stu-id="bebad-111">What would be hello reason hello video does not play when I try toostream it?</span></span>

<span data-ttu-id="bebad-112">Ответ один из hello, чаще всего причин, по которой необходимо hello, из которого вы пытаетесь tooplayback в hello конечной точки потоковой передачи **под управлением** состояния.</span><span class="sxs-lookup"><span data-stu-id="bebad-112">A: One of hello most common reasons is you do not have hello streaming endpoint from which you are trying tooplayback in hello **Running** state.</span></span>  

<span data-ttu-id="bebad-113">Вопрос. Можно ли объединять видео в динамическом потоке?</span><span class="sxs-lookup"><span data-stu-id="bebad-113">Q: Can I do compositing on a live stream?</span></span>

<span data-ttu-id="bebad-114">Ответ компоновка на обновляющиеся потоки в настоящее время не содержится в Azure Media Services, потребовалось бы toopre-составлено на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="bebad-114">A: Compositing on live streams is currently not offered in Azure Media Services, so you would need toopre-compose on your computer.</span></span>

<span data-ttu-id="bebad-115">Вопрос. Можно ли использовать Azure CDN с динамической потоковой передачей?</span><span class="sxs-lookup"><span data-stu-id="bebad-115">Q: Can I use Azure CDN with Live Streaming?</span></span>

<span data-ttu-id="bebad-116">Ответ Media Services позволяет интегрировать сети доставки Содержимого Azure (Дополнительные сведения см. в разделе [как tooManage потоковые конечные точки в учетную запись служб мультимедиа](media-services-portal-manage-streaming-endpoints.md)).</span><span class="sxs-lookup"><span data-stu-id="bebad-116">A: Media Services supports integration with Azure CDN (for more information, see [How tooManage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)).</span></span>  <span data-ttu-id="bebad-117">Вы можете использовать динамическую потоковую передачу с CDN.</span><span class="sxs-lookup"><span data-stu-id="bebad-117">You can use Live streaming with CDN.</span></span> <span data-ttu-id="bebad-118">Службы мультимедиа Azure предоставляют выходные данные в форматах Smooth Streaming, HLS и MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="bebad-118">Azure Media Services provides Smooth Streaming, HLS and MPEG-DASH outputs.</span></span> <span data-ttu-id="bebad-119">Все они используют протокол HTTP для передачи данных, а также кэширование HTTP.</span><span class="sxs-lookup"><span data-stu-id="bebad-119">All these formats use HTTP for transferring data and get benefits of HTTP caching.</span></span> <span data-ttu-id="bebad-120">В динамической потоковой передачи фактических данных аудио/видео разделенная toofragments и это отдельные фрагменты помещаться в CDN.</span><span class="sxs-lookup"><span data-stu-id="bebad-120">In live streaming actual video/audio data is divided toofragments and this individual fragments get cached in CDN.</span></span> <span data-ttu-id="bebad-121">Только данные потребностей toobe обновленные данные hello манифеста.</span><span class="sxs-lookup"><span data-stu-id="bebad-121">Only data needs toobe refreshed is hello manifest data.</span></span> <span data-ttu-id="bebad-122">CDN периодически обновляет данные манифеста.</span><span class="sxs-lookup"><span data-stu-id="bebad-122">CDN periodically refreshes manifest data.</span></span>

<span data-ttu-id="bebad-123">Вопрос. Службы мультимедиа Azure поддерживают хранение изображений?</span><span class="sxs-lookup"><span data-stu-id="bebad-123">Q: Does Azure Media services support storing images?</span></span>

<span data-ttu-id="bebad-124">Ответ, если требуется просто toostore JPEG или PNG-изображений, следует хранить в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="bebad-124">A: If you are just looking toostore JPEG or PNG images, you should keep those in Azure Blob Storage.</span></span> <span data-ttu-id="bebad-125">Нет не tooputting преимущество, их в службах мультимедиа учетной записи, если не требуется, чтобы tookeep их, связанной с видео или аудио активы.</span><span class="sxs-lookup"><span data-stu-id="bebad-125">There is no benefit tooputting them in your Media Services account unless you want tookeep them associated with your Video or Audio Assets.</span></span> <span data-ttu-id="bebad-126">Или, если возможно toouse необходимость hello изображения как слои в кодировщик видео hello. Стандартный кодировщик мультимедиа поддерживает изображения наложения объектов поверх видео и, что перечислены JPEG или PNG, поддерживаемой форматы входных данных.</span><span class="sxs-lookup"><span data-stu-id="bebad-126">Or if you might have a need toouse hello images as overlays in hello video encoder.Media Encoder Standard supports overlaying images on top of videos, and that is what it lists JPEG and PNG as supported input formats.</span></span> <span data-ttu-id="bebad-127">Дополнительные сведения см. в статье [Создание наложений](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="bebad-127">For more information, see [Creating Overlays](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

<span data-ttu-id="bebad-128">Вопрос. как копировать ресурсы из одного tooanother учетной записи служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="bebad-128">Q: How can I copy assets from one Media Services account tooanother.</span></span>

<span data-ttu-id="bebad-129">Ответ toocopy ресурсам с помощью одной учетной записи службы мультимедиа tooanother, с помощью .NET, используйте [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) метод расширения, доступные в hello [расширения SDK .NET служб мультимедиа Azure](https://github.com/Azure/azure-sdk-for-media-services-extensions/) репозитория.</span><span class="sxs-lookup"><span data-stu-id="bebad-129">A: toocopy assets from one Media Services account tooanother using .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) extension method available in hello [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span></span> <span data-ttu-id="bebad-130">Дополнительные сведения см. в [этой теме форума](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices).</span><span class="sxs-lookup"><span data-stu-id="bebad-130">For more information, see [this](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span></span>

<span data-ttu-id="bebad-131">Вопрос. что hello поддерживаются символы для имен файлов, при работе с AMS?</span><span class="sxs-lookup"><span data-stu-id="bebad-131">Q: What are hello supported characters for naming files when working with AMS?</span></span>

<span data-ttu-id="bebad-132">Ответ службы мультимедиа использует значение hello hello свойство IAssetFile.Name при построении URL-адреса для hello, потоковая передача содержимого (например, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) По этой причине кодирование с помощью знака процента не допускается.</span><span class="sxs-lookup"><span data-stu-id="bebad-132">A: Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="bebad-133">Здравствуйте, значение hello **имя** свойство не может иметь любой из следующих hello [процентов зарезервированные символы](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! * "();: @& = + $, /? % # []».</span><span class="sxs-lookup"><span data-stu-id="bebad-133">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="bebad-134">Кроме того, может использоваться только один знак ".".</span><span class="sxs-lookup"><span data-stu-id="bebad-134">Also, there can only be one ‘.’</span></span> <span data-ttu-id="bebad-135">для расширения имени файла hello.</span><span class="sxs-lookup"><span data-stu-id="bebad-135">for hello file name extension.</span></span>

<span data-ttu-id="bebad-136">Вопрос. как tooconnect с помощью REST?</span><span class="sxs-lookup"><span data-stu-id="bebad-136">Q: How tooconnect using REST?</span></span>

<span data-ttu-id="bebad-137">Ответ для получения сведений о как tooconnect toohello AMS API, см. статью [hello доступа к API служб мультимедиа Azure с проверкой подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="bebad-137">A: For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> <span data-ttu-id="bebad-138">После успешного подключения toohttps://media.windows.net, будет получено перенаправление 301 указывающее другой URI служб Media Services.</span><span class="sxs-lookup"><span data-stu-id="bebad-138">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="bebad-139">Необходимо внести toohello последующих вызовов новый URI.</span><span class="sxs-lookup"><span data-stu-id="bebad-139">You must make subsequent calls toohello new URI.</span></span> 

<span data-ttu-id="bebad-140">Вопрос. как поворот видео во время кодирования процесса hello.</span><span class="sxs-lookup"><span data-stu-id="bebad-140">Q: How can I rotate a video during hello encoding process.</span></span>

<span data-ttu-id="bebad-141">Ответ Здравствуйте, [Media Encoder Стандартная](media-services-dotnet-encode-with-media-encoder-standard.md) поддерживает поворот по углы 90, 180 или 270.</span><span class="sxs-lookup"><span data-stu-id="bebad-141">A: hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 90/180/270.</span></span> <span data-ttu-id="bebad-142">поведение по умолчанию Hello является «Auto», где она пытается toodetect hello поворота метаданных в файл MP4 или MOV входящих hello и компенсации для него.</span><span class="sxs-lookup"><span data-stu-id="bebad-142">hello default behavior is "Auto", where it tries toodetect hello rotation metadata in hello incoming MP4/MOV file and compensate for it.</span></span> <span data-ttu-id="bebad-143">Включить следующие hello **источников** tooone элемент определен предустановок json hello [здесь](media-services-mes-presets-overview.md):</span><span class="sxs-lookup"><span data-stu-id="bebad-143">Include hello following **Sources** element tooone of hello json presets defined [here](media-services-mes-presets-overview.md):</span></span>

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


## <a name="media-services-learning-paths"></a><span data-ttu-id="bebad-144">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="bebad-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="bebad-145">Отзывы</span><span class="sxs-lookup"><span data-stu-id="bebad-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
