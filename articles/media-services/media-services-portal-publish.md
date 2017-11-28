---
title: "AAA» публиковать содержимое посредством hello портал Azure | Документы Microsoft»"
description: "Этот учебник поможет выполнить шаги для публикации содержимого с портала Azure hello hello."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: a7a3867a6939b4b9da883176c6cc20c99d6c54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-content-with-hello-azure-portal"></a><span data-ttu-id="d43e4-103">Публиковать содержимое посредством hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="d43e4-103">Publish content with hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d43e4-104">Портал</span><span class="sxs-lookup"><span data-stu-id="d43e4-104">Portal</span></span>](media-services-portal-publish.md)
> * [<span data-ttu-id="d43e4-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d43e4-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="d43e4-106">REST</span><span class="sxs-lookup"><span data-stu-id="d43e4-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="d43e4-107">Обзор</span><span class="sxs-lookup"><span data-stu-id="d43e4-107">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="d43e4-108">toocomplete этого учебника необходима учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="d43e4-108">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="d43e4-109">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d43e4-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="d43e4-110">tooprovide на пользователя с URL-адрес, который можно использовать toostream или загрузить содержимое, сначала требуется слишком «публикации» актива путем создания локатора.</span><span class="sxs-lookup"><span data-stu-id="d43e4-110">tooprovide your user with a  URL that can be used toostream or download your content, you first need too"publish" your asset by creating a locator.</span></span> <span data-ttu-id="d43e4-111">Локаторы предоставляют доступ toofiles, содержащиеся в ресурсе hello.</span><span class="sxs-lookup"><span data-stu-id="d43e4-111">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="d43e4-112">Службы мультимедиа поддерживают два типа указателей:</span><span class="sxs-lookup"><span data-stu-id="d43e4-112">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="d43e4-113">Потоковая передача указателей (OnDemandOrigin), используемый для адаптивной потоковой передачи (например, toostream MPEG DASH, HLS или Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="d43e4-113">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, toostream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="d43e4-114">toocreate указатель потоковой передачи актива должно содержать ISM-файла.</span><span class="sxs-lookup"><span data-stu-id="d43e4-114">toocreate a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="d43e4-115">Последовательные указатели (SAS), используемые для доставки видео путем последовательного скачивания.</span><span class="sxs-lookup"><span data-stu-id="d43e4-115">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="d43e4-116">URL-адрес потоковой передачи имеет следующий формат hello и его можно использовать ресурсы Smooth Streaming tooplay.</span><span class="sxs-lookup"><span data-stu-id="d43e4-116">A streaming URL has hello following format and you can use it tooplay Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="d43e4-117">append toobuild на URL-адрес потоковой передачи HLS (format = m3u8-aapl) toohello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="d43e4-117">toobuild an HLS streaming URL, append (format=m3u8-aapl) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="d43e4-118">Добавление toobuild на URL-адрес потоковой передачи MPEG DASH (формат = mpd время csf) toohello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="d43e4-118">toobuild an  MPEG DASH streaming URL, append (format=mpd-time-csf) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

<span data-ttu-id="d43e4-119">URL-адрес SAS имеет следующий формат hello.</span><span class="sxs-lookup"><span data-stu-id="d43e4-119">A SAS URL has hello following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="d43e4-120">Дополнительные сведения см. в [обзоре доставки содержимого](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d43e4-120">For more information, see [Delivering content overview](media-services-deliver-content-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d43e4-121">Указатели с датой окончания срока действия два года были созданы, при использовании портала toocreate локаторов hello до марта 2015 г.</span><span class="sxs-lookup"><span data-stu-id="d43e4-121">If you used hello portal toocreate locators before March 2015, locators with a two year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="d43e4-122">tooupdate дату окончания срока действия на указатель, используйте [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) или [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="d43e4-122">tooupdate an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="d43e4-123">Обратите внимание, что при обновлении срок действия локатора SAS hello hello URL-адрес изменяется.</span><span class="sxs-lookup"><span data-stu-id="d43e4-123">Note that when you update hello expiration date of a SAS locator, hello URL changes.</span></span>

### <a name="toouse-hello-portal-toopublish-an-asset"></a><span data-ttu-id="d43e4-124">toouse hello портала toopublish актива</span><span class="sxs-lookup"><span data-stu-id="d43e4-124">toouse hello portal toopublish an asset</span></span>
<span data-ttu-id="d43e4-125">toouse hello портала toopublish актива, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d43e4-125">toouse hello portal toopublish an asset, do hello following:</span></span>

1. <span data-ttu-id="d43e4-126">В hello [портал Azure](https://portal.azure.com/), выберите учетную запись служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="d43e4-126">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="d43e4-127">Установите флажок **Параметры** > **Ресурсы-контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="d43e4-127">Select **Settings** > **Assets**.</span></span>
3. <span data-ttu-id="d43e4-128">Выберите требуемый toopublish средство hello.</span><span class="sxs-lookup"><span data-stu-id="d43e4-128">Select hello asset that you want toopublish.</span></span>
4. <span data-ttu-id="d43e4-129">Нажмите кнопку hello **публикации** кнопки.</span><span class="sxs-lookup"><span data-stu-id="d43e4-129">Click hello **Publish** button.</span></span>
5. <span data-ttu-id="d43e4-130">Выберите тип локатора hello.</span><span class="sxs-lookup"><span data-stu-id="d43e4-130">Select hello locator type.</span></span>
6. <span data-ttu-id="d43e4-131">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d43e4-131">Press **Add**.</span></span>
   
    ![Опубликовать](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="d43e4-133">Hello URL-адрес будет добавлен список toohello **URL-адреса в опубликованные**.</span><span class="sxs-lookup"><span data-stu-id="d43e4-133">hello URL will be added toohello list of **Published URLs**.</span></span>

## <a name="play-content-from-hello-portal"></a><span data-ttu-id="d43e4-134">Воспроизведение контента из портала hello</span><span class="sxs-lookup"><span data-stu-id="d43e4-134">Play content from hello portal</span></span>
<span data-ttu-id="d43e4-135">Hello портал Azure предоставляет проигрыватель контента, которые можно использовать tootest видео.</span><span class="sxs-lookup"><span data-stu-id="d43e4-135">hello Azure portal provides a content player that you can use tootest your video.</span></span>

<span data-ttu-id="d43e4-136">Выберите требуемого hello видео и нажмите кнопку hello **воспроизведение** кнопки.</span><span class="sxs-lookup"><span data-stu-id="d43e4-136">Click hello desired video and then click hello **Play** button.</span></span>

![Опубликовать](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="d43e4-138">Важные особенности</span><span class="sxs-lookup"><span data-stu-id="d43e4-138">Some considerations apply:</span></span>

* <span data-ttu-id="d43e4-139">Убедитесь, что опубликованный hello видео.</span><span class="sxs-lookup"><span data-stu-id="d43e4-139">Make sure hello video has been published.</span></span>
* <span data-ttu-id="d43e4-140">Это **проигрыватель** воспроизводит контент из конечной точки потоковой передачи по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="d43e4-140">This **Media player** plays from hello default streaming endpoint.</span></span> <span data-ttu-id="d43e4-141">Если требуется, чтобы tooplay из не по умолчанию потоковой передачи конечной точки, выберите URL-адрес toocopy hello и используйте другой проигрыватель.</span><span class="sxs-lookup"><span data-stu-id="d43e4-141">If you want tooplay from a non-default streaming endpoint, click toocopy hello URL and use another player.</span></span> <span data-ttu-id="d43e4-142">Например, [Проигрыватель служб мультимедиа Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="d43e4-142">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
* <span data-ttu-id="d43e4-143">Привет, из которого потоковой передачи конечной точки потоковой передачи должна быть запущена.</span><span class="sxs-lookup"><span data-stu-id="d43e4-143">hello streaming endpoint from which you are streaming must be running.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d43e4-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d43e4-144">Next steps</span></span>
<span data-ttu-id="d43e4-145">Просмотрите схемы обучения работе со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="d43e4-145">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d43e4-146">Отзывы</span><span class="sxs-lookup"><span data-stu-id="d43e4-146">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

