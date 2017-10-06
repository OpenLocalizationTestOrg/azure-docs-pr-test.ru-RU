---
title: "aaaUse существующих проигрывателей tooplayback контент - Azure | Документы Microsoft"
description: "В этом разделе перечислены существующих проигрывателей, которые можно использовать tooplayback контента."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7e9fcf89-0fb6-4fa4-96cb-666320684d69
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: 54817345a19a9d3b18f1e7b352c3342043a569b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="playing-your-content-with-existing-players"></a><span data-ttu-id="2ceda-103">Воспроизведение содержимого с помощью существующих проигрывателей</span><span class="sxs-lookup"><span data-stu-id="2ceda-103">Playing your content with existing players</span></span>
<span data-ttu-id="2ceda-104">Службы мультимедиа Azure поддерживают многие популярные форматы потоковой передачи, например Smooth Streaming, HTTP Live Streaming и MPEG-Dash.</span><span class="sxs-lookup"><span data-stu-id="2ceda-104">Azure Media Services supports many popular streaming formats, such as Smooth Streaming, HTTP Live Streaming, and MPEG-Dash.</span></span> <span data-ttu-id="2ceda-105">В этом подразделе описываются tooexisting проигрыватели, которые можно использовать tootest потоков.</span><span class="sxs-lookup"><span data-stu-id="2ceda-105">This topic points you tooexisting players that you can use tootest your streams.</span></span>

### <a name="hello-azure-portal-media-services-content-player"></a><span data-ttu-id="2ceda-106">проигрывателя содержимого портала Azure Media Services Hello</span><span class="sxs-lookup"><span data-stu-id="2ceda-106">hello Azure portal Media Services content player</span></span>
<span data-ttu-id="2ceda-107">Hello **Azure** портал предоставляет проигрыватель контента, которые можно использовать tootest видео.</span><span class="sxs-lookup"><span data-stu-id="2ceda-107">hello **Azure** portal provides a content player that you can use tootest your video.</span></span>

<span data-ttu-id="2ceda-108">Щелкните здесь hello требуемого видео (Убедитесь, что он был [опубликованных](media-services-portal-publish.md)) и нажмите кнопку hello **воспроизведение** кнопку в нижней части hello hello портала.</span><span class="sxs-lookup"><span data-stu-id="2ceda-108">Click on hello desired video (make sure it was [published](media-services-portal-publish.md)) and click hello **Play** button at hello bottom of hello portal.</span></span>

<span data-ttu-id="2ceda-109">Важные особенности</span><span class="sxs-lookup"><span data-stu-id="2ceda-109">Some considerations apply:</span></span>

* <span data-ttu-id="2ceda-110">Hello **ПРОИГРЫВАТЕЛЬ КОНТЕНТА СЛУЖБ МУЛЬТИМЕДИА** воспроизводит контент из конечной точки потоковой передачи по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="2ceda-110">hello **MEDIA SERVICES CONTENT PLAYER** plays from hello default streaming endpoint.</span></span> <span data-ttu-id="2ceda-111">Если вы хотите tooplay из конечной точки потоковой передачи не по умолчанию, используйте другой проигрыватель.</span><span class="sxs-lookup"><span data-stu-id="2ceda-111">If you want tooplay from a non-default streaming endpoint, use another player.</span></span> <span data-ttu-id="2ceda-112">Например, [Проигрыватель мультимедиа Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="2ceda-112">For example, [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a><span data-ttu-id="2ceda-114">Проигрыватель мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="2ceda-114">Azure Media Player</span></span>
<span data-ttu-id="2ceda-115">Используйте [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tooplayback содержимого (открытым или защищенным) в любом из следующих форматов hello:</span><span class="sxs-lookup"><span data-stu-id="2ceda-115">Use [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tooplayback your content (clear or protected) in any of hello following formats:</span></span>

* <span data-ttu-id="2ceda-116">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="2ceda-116">Smooth Streaming</span></span>
* <span data-ttu-id="2ceda-117">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="2ceda-117">MPEG DASH</span></span>
* <span data-ttu-id="2ceda-118">HLS</span><span class="sxs-lookup"><span data-stu-id="2ceda-118">HLS</span></span>
* <span data-ttu-id="2ceda-119">Последовательный MP4</span><span class="sxs-lookup"><span data-stu-id="2ceda-119">Progressive MP4</span></span>

### <a name="flash-player"></a><span data-ttu-id="2ceda-120">Flash Player</span><span class="sxs-lookup"><span data-stu-id="2ceda-120">Flash Player</span></span>
#### <a name="aes-encrypted-with-token"></a><span data-ttu-id="2ceda-121">Шифрование AES с маркером</span><span class="sxs-lookup"><span data-stu-id="2ceda-121">AES-encrypted with Token</span></span>
[<span data-ttu-id="2ceda-122">http://aestoken.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="2ceda-122">http://aestoken.azurewebsites.net</span></span>](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a><span data-ttu-id="2ceda-123">Проигрыватели Silverlight</span><span class="sxs-lookup"><span data-stu-id="2ceda-123">Silverlight Players</span></span>
#### <a name="monitoring"></a><span data-ttu-id="2ceda-124">Мониторинг</span><span class="sxs-lookup"><span data-stu-id="2ceda-124">Monitoring</span></span>
[<span data-ttu-id="2ceda-125">http://smf.cloudapp.net/healthmonitor</span><span class="sxs-lookup"><span data-stu-id="2ceda-125">http://smf.cloudapp.net/healthmonitor</span></span>](http://smf.cloudapp.net/healthmonitor)

#### <a name="playready-with-token"></a><span data-ttu-id="2ceda-126">PlayReady с маркером</span><span class="sxs-lookup"><span data-stu-id="2ceda-126">PlayReady with Token</span></span>
[<span data-ttu-id="2ceda-127">http://sltoken.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="2ceda-127">http://sltoken.azurewebsites.net</span></span>](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a><span data-ttu-id="2ceda-128">Проигрыватели DASH</span><span class="sxs-lookup"><span data-stu-id="2ceda-128">DASH Players</span></span>
[<span data-ttu-id="2ceda-129">http://dashplayer.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="2ceda-129">http://dashplayer.azurewebsites.net</span></span>](http://dashplayer.azurewebsites.net)

[<span data-ttu-id="2ceda-130">http://dashif.org</span><span class="sxs-lookup"><span data-stu-id="2ceda-130">http://dashif.org</span></span>](http://dashif.org)

### <a name="other"></a><span data-ttu-id="2ceda-131">Другие</span><span class="sxs-lookup"><span data-stu-id="2ceda-131">Other</span></span>
<span data-ttu-id="2ceda-132">tootest HLS URL-адреса, можно также использовать:</span><span class="sxs-lookup"><span data-stu-id="2ceda-132">tootest HLS URLs you can also use:</span></span>

* <span data-ttu-id="2ceda-133">**Safari** на устройстве iOS или</span><span class="sxs-lookup"><span data-stu-id="2ceda-133">**Safari** on an iOS device or</span></span>
* <span data-ttu-id="2ceda-134">**3ivx HLS Player** в Windows.</span><span class="sxs-lookup"><span data-stu-id="2ceda-134">**3ivx HLS Player** on Windows.</span></span>

## <a name="developing-video-players"></a><span data-ttu-id="2ceda-135">Разработка видеопроигрывателей</span><span class="sxs-lookup"><span data-stu-id="2ceda-135">Developing video players</span></span>
<span data-ttu-id="2ceda-136">Сведения о том, как toodevelop собственных проигрывателей отображается [разработке видеопроигрывателей](media-services-develop-video-players.md)</span><span class="sxs-lookup"><span data-stu-id="2ceda-136">For information about how toodevelop your own players, see [Developing video players](media-services-develop-video-players.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="2ceda-137">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="2ceda-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2ceda-138">Отзывы</span><span class="sxs-lookup"><span data-stu-id="2ceda-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
