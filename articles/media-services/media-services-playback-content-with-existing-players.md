---
title: "Использование существующих проигрывателей для воспроизведения содержимого в Azure | Документация Майкрософт"
description: "В этой статье перечислены существующие проигрыватели, которые можно использовать для воспроизведения содержимого."
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
ms.openlocfilehash: 48f373b013b1192c353352b801876d706d91dd28
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="playing-your-content-with-existing-players"></a><span data-ttu-id="78954-103">Воспроизведение содержимого с помощью существующих проигрывателей</span><span class="sxs-lookup"><span data-stu-id="78954-103">Playing your content with existing players</span></span>
<span data-ttu-id="78954-104">Службы мультимедиа Azure поддерживают многие популярные форматы потоковой передачи, например Smooth Streaming, HTTP Live Streaming и MPEG-Dash.</span><span class="sxs-lookup"><span data-stu-id="78954-104">Azure Media Services supports many popular streaming formats, such as Smooth Streaming, HTTP Live Streaming, and MPEG-Dash.</span></span> <span data-ttu-id="78954-105">В этой статье описываются имеющиеся проигрыватели, которые можно использовать для тестирования потоков.</span><span class="sxs-lookup"><span data-stu-id="78954-105">This topic points you to existing players that you can use to test your streams.</span></span>

### <a name="the-azure-portal-media-services-content-player"></a><span data-ttu-id="78954-106">Проигрыватель содержимого служб мультимедиа портала Azure</span><span class="sxs-lookup"><span data-stu-id="78954-106">The Azure portal Media Services content player</span></span>
<span data-ttu-id="78954-107">Портал **Azure** предлагает проигрыватель содержимого, с помощью которого можно проверить видео.</span><span class="sxs-lookup"><span data-stu-id="78954-107">The **Azure** portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="78954-108">Выберите нужное видео (убедитесь, что оно [опубликовано](media-services-portal-publish.md)) и нажмите кнопку **Воспроизвести** в нижней части портала.</span><span class="sxs-lookup"><span data-stu-id="78954-108">Click on the desired video (make sure it was [published](media-services-portal-publish.md)) and click the **Play** button at the bottom of the portal.</span></span>

<span data-ttu-id="78954-109">Важные особенности</span><span class="sxs-lookup"><span data-stu-id="78954-109">Some considerations apply:</span></span>

* <span data-ttu-id="78954-110">**ПРОИГРЫВАТЕЛЬ КОНТЕНТА СЛУЖБ МУЛЬТИМЕДИА** выполняет воспроизведение из конечной точки потоковой передачи по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="78954-110">The **MEDIA SERVICES CONTENT PLAYER** plays from the default streaming endpoint.</span></span> <span data-ttu-id="78954-111">Если требуется воспроизвести из конечной точке потоковой передачи не по умолчанию, используйте другой проигрыватель.</span><span class="sxs-lookup"><span data-stu-id="78954-111">If you want to play from a non-default streaming endpoint, use another player.</span></span> <span data-ttu-id="78954-112">Например, [Проигрыватель мультимедиа Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="78954-112">For example, [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a><span data-ttu-id="78954-114">Проигрыватель мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="78954-114">Azure Media Player</span></span>
<span data-ttu-id="78954-115">Используйте [Проигрыватель мультимедиа Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html) для воспроизведения содержимого (незашифрованного или защищенного) в любом из следующих форматов:</span><span class="sxs-lookup"><span data-stu-id="78954-115">Use [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to playback your content (clear or protected) in any of the following formats:</span></span>

* <span data-ttu-id="78954-116">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="78954-116">Smooth Streaming</span></span>
* <span data-ttu-id="78954-117">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="78954-117">MPEG DASH</span></span>
* <span data-ttu-id="78954-118">HLS</span><span class="sxs-lookup"><span data-stu-id="78954-118">HLS</span></span>
* <span data-ttu-id="78954-119">Последовательный MP4</span><span class="sxs-lookup"><span data-stu-id="78954-119">Progressive MP4</span></span>

### <a name="flash-player"></a><span data-ttu-id="78954-120">Flash Player</span><span class="sxs-lookup"><span data-stu-id="78954-120">Flash Player</span></span>
#### <a name="aes-encrypted-with-token"></a><span data-ttu-id="78954-121">Шифрование AES с маркером</span><span class="sxs-lookup"><span data-stu-id="78954-121">AES-encrypted with Token</span></span>
[<span data-ttu-id="78954-122">http://aestoken.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="78954-122">http://aestoken.azurewebsites.net</span></span>](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a><span data-ttu-id="78954-123">Проигрыватели Silverlight</span><span class="sxs-lookup"><span data-stu-id="78954-123">Silverlight Players</span></span>
#### <a name="monitoring"></a><span data-ttu-id="78954-124">Мониторинг</span><span class="sxs-lookup"><span data-stu-id="78954-124">Monitoring</span></span>
[<span data-ttu-id="78954-125">http://smf.cloudapp.net/healthmonitor</span><span class="sxs-lookup"><span data-stu-id="78954-125">http://smf.cloudapp.net/healthmonitor</span></span>](http://smf.cloudapp.net/healthmonitor)

#### <a name="playready-with-token"></a><span data-ttu-id="78954-126">PlayReady с маркером</span><span class="sxs-lookup"><span data-stu-id="78954-126">PlayReady with Token</span></span>
[<span data-ttu-id="78954-127">http://sltoken.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="78954-127">http://sltoken.azurewebsites.net</span></span>](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a><span data-ttu-id="78954-128">Проигрыватели DASH</span><span class="sxs-lookup"><span data-stu-id="78954-128">DASH Players</span></span>
[<span data-ttu-id="78954-129">http://dashplayer.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="78954-129">http://dashplayer.azurewebsites.net</span></span>](http://dashplayer.azurewebsites.net)

[<span data-ttu-id="78954-130">http://dashif.org</span><span class="sxs-lookup"><span data-stu-id="78954-130">http://dashif.org</span></span>](http://dashif.org)

### <a name="other"></a><span data-ttu-id="78954-131">Другие</span><span class="sxs-lookup"><span data-stu-id="78954-131">Other</span></span>
<span data-ttu-id="78954-132">Для проверки URL-адресов HLS также можно использовать:</span><span class="sxs-lookup"><span data-stu-id="78954-132">To test HLS URLs you can also use:</span></span>

* <span data-ttu-id="78954-133">**Safari** на устройстве iOS или</span><span class="sxs-lookup"><span data-stu-id="78954-133">**Safari** on an iOS device or</span></span>
* <span data-ttu-id="78954-134">**3ivx HLS Player** в Windows.</span><span class="sxs-lookup"><span data-stu-id="78954-134">**3ivx HLS Player** on Windows.</span></span>

## <a name="developing-video-players"></a><span data-ttu-id="78954-135">Разработка видеопроигрывателей</span><span class="sxs-lookup"><span data-stu-id="78954-135">Developing video players</span></span>
<span data-ttu-id="78954-136">Сведения о том, как разрабатывать собственные проигрыватели, см. в статье [Разработка приложений видеопроигрывателя](media-services-develop-video-players.md).</span><span class="sxs-lookup"><span data-stu-id="78954-136">For information about how to develop your own players, see [Developing video players](media-services-develop-video-players.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="78954-137">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="78954-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="78954-138">Отзывы</span><span class="sxs-lookup"><span data-stu-id="78954-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
