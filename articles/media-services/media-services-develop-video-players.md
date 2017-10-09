---
title: "aaaDevelop приложений видеопроигрывателя"
description: "Hello разделе приводятся ссылки tooPlayer платформ и подключаемых модулей, которые можно использовать toodevelop собственных клиентских приложений, способных использовать потоковое мультимедиа из служб мультимедиа."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 55e419fc-4c39-4902-9c62-f41cfcd86c6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: a66daa4f006a1f05271cc9ed6a02ea7ee460321d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="develop-video-player-applications"></a>Разработка приложений видеопроигрывателя
## <a name="overview"></a>Обзор
Службы мультимедиа Azure предоставляют средства hello, вы должны toocreate rich динамических клиентских приложений проигрывателя для большинства платформ, включая: операций ввода-вывода устройства, устройства Android, Windows, Windows Phone, Xbox и абонентских поля. Здесь также приведены ссылки tooSDKs и платформы проигрывателя, которые можно использовать toodevelop собственных клиентских приложений, способных использовать потоковое мультимедиа из служб мультимедиа Azure.

>[!NOTE]
>При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния. Потоковая передача вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования toostart hello конечной точки потоковой передачи, из которого нужно имеет содержимое toostream toobe в hello **под управлением** состояния. 
 
## <a name="azure-media-player"></a>Проигрыватель мультимедиа Azure
[Azure Media Player](http://aka.ms/ampinfo) видеопроигрыватель web строится tooplay назад мультимедийного содержимого из службы мультимедиа Microsoft Azure на самых разнообразных браузерах и устройствах. Azure Media Player использует отраслевые стандарты, такие как HTML5, Media Source Extensions (MSE) и зашифрованы мультимедиа расширения (EME) tooprovide интерфейс обогащенный адаптивной потоковой передачи. Если эти стандарты недоступны на устройстве или в браузере, Проигрыватель мультимедиа Azure использует Flash и Silverlight. Независимо от технологии воспроизведения hello используемой разработчики будет иметь единый интерфейс tooaccess JavaScript API-интерфейсы. Это позволяет для содержимого, обслуживаемых toobe служб мультимедиа Azure воспроизводиться для широкого спектра устройств и браузеров без дополнительных усилий.

Службы мультимедиа Microsoft Azure обеспечивает toobe содержимого, предоставляемого DASH, Smooth Streaming и HLS tooplay форматы потоковой передачи обратно содержимое. Azure Media Player учитывает эти форматы и автоматически играет hello наиболее связи на основе возможностей браузера platform/hello. Службы мультимедиа Microsoft Azure также позволяют динамически шифровать ресурсы с использованием PlayReady или 128-битного шифрования AES. Проигрыватель мультимедиа Azure поддерживает расшифровку содержимого, зашифрованного с помощью PlayReady и 128-битного алгоритма шифрования AES, если заданы соответствующие параметры. 

Дополнительные сведения

* [Проигрыватель мультимедиа Azure](http://aka.ms/ampinfo)
* [Документация по Проигрывателю мультимедиа Azure](http://aka.ms/ampdocs) 
* [Блог о начале работы с Проигрывателем мультимедиа Azure](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/)
* [Регистрация toostay копирование toodate с hello последняя версия проигрывателя мультимедиа Azure](http://aka.ms/ampsignup)
* [Запрос новых функций, ваши идеи и отзывы](http://aka.ms/ampuservoice) 

## <a name="other-tools-for-creating-player-applications"></a>Другие средства для создания приложений проигрывателя
Также можно использовать любой из следующих пакетов SDK hello:

* [клиентский пакет SDK Smooth Streaming;](http://www.iis.net/downloads/microsoft/smooth-streaming) 
* [приложение магазина Windows с потоковой передачей Smooth Streaming;](media-services-build-smooth-streaming-apps.md)
* [платформа проигрывателя Microsoft Media Platform;](http://playerframework.codeplex.com/) 
* [документация по платформе проигрывателя HTML5;](http://playerframework.codeplex.com/wikipage?title=HTML5%20Player&referringTitle=Documentation) 
* [подключаемый модуль Microsoft Smooth Streaming для OSMF;](https://www.microsoft.com/download/details.aspx?id=36057) 
* [Лицензирование пакета для портирования клиента бесперебойной потоковой передачи Microsoft® Smooth Streaming](http://aka.ms/sspk) 
* [Разработка приложений для воспроизведения видео на XBOX](http://xbox.create.msdn.com/) 

## <a name="advertising"></a>Реклама
Службы мультимедиа Azure обеспечивает поддержку вставки рекламы посредством hello Windows Media Platform: платформы проигрывателя. Платформы проигрывателя с поддержкой рекламы доступны для устройств Windows 8, Silverlight, Windows Phone 8 и iOS. Каждая платформа проигрывателя содержит образец кода, которое показывает, как tooimplement приложение проигрывателя. В мультимедиасодержимое можно вставить три вида рекламы:

Линейная реклама полного кадра паузы hello основного видео

Нелинейная реклама, которая отображается поверх основного видео hello воспроизводится, обычно это логотип или другие статическое изображение, размещенное в проигрывателе hello

Сопутствующая реклама, отображаемых за пределами проигрывателя hello

Рекламу можно размещать в любой точке временной шкалы основного видео hello. Необходимо сообщить hello проигрывателя при tooplay hello ad и который tooplay рекламы. Для этого используется набор стандартных XML-файлов: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST) и Digital Video Player Ad Interface Definition (VPAID). VAST-файлы указывают, какие toodisplay рекламы. VMAP-файлы указывают, когда tooplay различные рекламные ролики и содержат XML-код VAST. MAST-файлы являются другим способом toosequence рекламы, они также содержат XML-код VAST. VPAID-файлы определяют интерфейс между видеопроигрывателем hello и hello ad или на сервере ad. Дополнительные сведения см. в статье [Вставка рекламы на стороне клиента](https://msdn.microsoft.com/library/dn387398.aspx).

Сведения о поддержке субтитров и рекламы в динамических потоковых видео см. в статье [Общие сведения о динамической потоковой передаче с использованием служб мультимедиа Azure](https://msdn.microsoft.com/library/c49e0b4d-357e-4cca-95e5-2288924d1ff3#caption_ad).

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>См. также
[Встраивание адаптивного потокового видео MPEG-DASH в приложение HTML5 с помощью DASH.js](media-services-embed-mpeg-dash-in-html5.md)

[Репозиторий dash.js на GitHub](https://github.com/Dash-Industry-Forum/dash.js)

