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
# <a name="playing-your-content-with-existing-players"></a>Воспроизведение содержимого с помощью существующих проигрывателей
Службы мультимедиа Azure поддерживают многие популярные форматы потоковой передачи, например Smooth Streaming, HTTP Live Streaming и MPEG-Dash. В этом подразделе описываются tooexisting проигрыватели, которые можно использовать tootest потоков.

### <a name="hello-azure-portal-media-services-content-player"></a>проигрывателя содержимого портала Azure Media Services Hello
Hello **Azure** портал предоставляет проигрыватель контента, которые можно использовать tootest видео.

Щелкните здесь hello требуемого видео (Убедитесь, что он был [опубликованных](media-services-portal-publish.md)) и нажмите кнопку hello **воспроизведение** кнопку в нижней части hello hello портала.

Важные особенности

* Hello **ПРОИГРЫВАТЕЛЬ КОНТЕНТА СЛУЖБ МУЛЬТИМЕДИА** воспроизводит контент из конечной точки потоковой передачи по умолчанию hello. Если вы хотите tooplay из конечной точки потоковой передачи не по умолчанию, используйте другой проигрыватель. Например, [Проигрыватель мультимедиа Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a>Проигрыватель мультимедиа Azure
Используйте [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tooplayback содержимого (открытым или защищенным) в любом из следующих форматов hello:

* Smooth Streaming
* MPEG DASH
* HLS
* Последовательный MP4

### <a name="flash-player"></a>Flash Player
#### <a name="aes-encrypted-with-token"></a>Шифрование AES с маркером
[http://aestoken.azurewebsites.net](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a>Проигрыватели Silverlight
#### <a name="monitoring"></a>Мониторинг
[http://smf.cloudapp.net/healthmonitor](http://smf.cloudapp.net/healthmonitor)

#### <a name="playready-with-token"></a>PlayReady с маркером
[http://sltoken.azurewebsites.net](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a>Проигрыватели DASH
[http://dashplayer.azurewebsites.net](http://dashplayer.azurewebsites.net)

[http://dashif.org](http://dashif.org)

### <a name="other"></a>Другие
tootest HLS URL-адреса, можно также использовать:

* **Safari** на устройстве iOS или
* **3ivx HLS Player** в Windows.

## <a name="developing-video-players"></a>Разработка видеопроигрывателей
Сведения о том, как toodevelop собственных проигрывателей отображается [разработке видеопроигрывателей](media-services-develop-video-players.md)

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
