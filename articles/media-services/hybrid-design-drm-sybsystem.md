---
title: "Структура aaaHybrid subsystem(s) DRM, с помощью служб мультимедиа Azure | Документы Microsoft"
description: "Здесь рассматривается гибридная структура подсистем управления цифровыми правами (DRM) с использованием служб мультимедиа Azure."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 4206248420ccd4dbfc9a87a86f4763534c6254a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-design-of-drm-subsystems"></a>Гибридная структура подсистем DRM

Здесь рассматривается гибридная структура подсистем управления цифровыми правами (DRM) с использованием служб мультимедиа Azure.

## <a name="overview"></a>Обзор

Службы мультимедиа Azure поддерживает следующие три системе DRM hello:

* PlayReady
* Widevine (модульная);
* FairPlay

поддержка DRM Hello включает шифрование DRM (динамического шифрования) и доставки лицензий с помощью Azure Media Player, поддерживающие все 3 DRMs как пакет SDK проигрывателя браузера.

Подробные работу, DRM или CENC подсистемы проектирования и реализации, см. в разделе hello документ с названием [CENC с несколькими DRM и управление доступом](media-services-cenc-with-multidrm-access-control.md).

Несмотря на то, что мы обеспечивают полную поддержку трех систем управления цифровыми правами, иногда клиенты должны toouse различные части собственные инфраструктуры и подсистемами в toobuild Media Services tooAzure Добавление гибридного подсистемы управления цифровыми правами.

Ниже представлены некоторые часто задаваемые вопросы пользователей:

* Можно ли использовать собственные серверы лицензирования DRM? (В этом случае пользователи вложили средства в кластер серверов лицензирования DRM со встроенной бизнес-логикой.)
* Можно ли использовать доставку лицензий DRM в службах мультимедиа Azure без размещения содержимого в AMS?

## <a name="modularity-of-hello-ams-drm-platform"></a>Модульность hello AMS DRM платформы

Как часть комплексной облачной видеоплатформы, DRM служб мультимедиа Azure имеет гибкую и модульную структуру. Службы мультимедиа Azure можно использовать с любым hello следующие комбинации описано hello ниже в таблице (объяснение hello-Наура, используемой в таблице hello ниже). 

|**Размещение содержимого и источник**|**Шифрование содержимого**|**Доставка лицензий DRM**|
|---|---|---|
|AMS|AMS|AMS|
|AMS|AMS|Сторонний производитель|
|AMS|Сторонний производитель|AMS|
|AMS|Сторонний производитель|Сторонний производитель|
|Сторонний производитель|Сторонний производитель|AMS|

### <a name="content-hosting--origin"></a>Размещение содержимого и источник

* AMS: видеоресурсы размещаются в AMS, а потоковая передача ведется с помощью конечных точек потоковой передачи AMS (но не обязательно с динамической упаковкой).
* Сторонний производитель: видео размещается и доставляется с помощью платформы потоковой передачи стороннего производителя за пределами AMS.

### <a name="content-encryption"></a>Шифрование содержимого

* AMS: шифрование содержимого происходит динамически или по требованию с помощью динамического шифрования AMS.
* Сторонний производитель: шифрование содержимого выполняется за пределами AMS с использованием рабочего процесса предварительной обработки.

### <a name="drm-license-delivery"></a>Доставка лицензий DRM

* AMS: лицензию DRM доставляет служба доставки лицензий AMS.
* Сторонний производитель: лицензию DRM доставляет сервер лицензирования DRM стороннего производителя за пределами AMS.

## <a name="configure-based-on-your-hybrid-scenario"></a>Настройка на основе своего гибридного сценария

### <a name="content-key"></a>Ключ содержимого

Путем настройки ключа содержимого можно контролировать следующие атрибуты AMS динамического шифрования и службы доставки лицензий AMS hello:

* Hello содержимого ключ, используемый для динамического шифрования управления цифровыми правами.
* Toobe содержимого лицензии DRM, предоставляемых служб доставки лицензий: прав, ключ содержимого и ограничений.
* Тип **ограничения политики авторизации ключа содержимого**: открытое, IP-адрес или ограничение по токену.
* Если **маркера** тип **ограничение политики авторизации ключа контента используется**, hello **ограничений политики авторизации ключа содержимого** должны быть выполнены перед выдачей лицензию.

### <a name="asset-delivery-policy"></a>Политика доставки ресурсов

Через конфигурацию политики доставки активов можно управлять hello следующие атрибуты, используемые AMS работы динамического упаковщика и динамического шифрования AMS конечной точки потоковой передачи:

* Протокол потоковой передачи и комбинация шифрования DRM, например DASH в CENC (PlayReady и Widevine), Smooth Streaming в PlayReady, HLS в Widevine или PlayReady.
* Hello по умолчанию и внедренных лицензии доставки URL-адресов для каждого hello участвует DRMs.
* Содержат ли URL-адреса для приобретения лицензий (LA_URL) в DASH MPD или списке воспроизведения HLS строку запроса идентификатора ключа (KID) для Widevine и FairPlay соответственно.

## <a name="scenarios-and-samples"></a>Сценарии и примеры

В зависимости от описания hello в предыдущем разделе hello, hello следующие пять гибридные сценарии используйте соответствующие **ключ содержимого**-**политики доставки активов** сочетания конфигурации (hello образцы, упомянутые в последнем столбце hello выполните hello таблицы).

|**Размещение содержимого и источник**|**Шифрование DRM**|**Доставка лицензий DRM**|**Настройка ключа содержимого**|**Настройка политики доставки для ресурса-контейнера**|**Пример**|
|---|---|---|---|---|---|
|AMS|AMS|AMS|Да|Да|Пример 1|
|AMS|AMS|Сторонний производитель|Да|Да|Пример 2|
|AMS|Сторонний производитель|AMS|Да|Нет|Пример 3|
|AMS|Сторонний производитель|Внешняя|Нет|Нет|Пример 4|
|Сторонний производитель|Сторонний производитель|AMS|Да|Нет|    

В образцы hello защиты PlayReady работе DASH и smooth streaming. Hello видео URL-адреса smooth streaming URL-адреса. tooget Здравствуйте соответствующего URL-адреса, ТИРЕ, просто добавлять» (формат = mpd время csf)». Можно использовать hello [мультимедиа azure тестирования проигрывателя](http://aka.ms/amtest) tootest в браузере. Позволяет tooconfigure которого потоковой передачи toouse протокола, в которой технический. IE11 и MS Edge в Windows 10 поддерживают PlayReady через EME. Дополнительные сведения см. в разделе [средство тестирования, сведения о hello](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).

### <a name="sample-1"></a>Пример 1

* URL-адрес источника (основной): https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest 
* URL-адрес для приобретения лицензии PlayReady (DASH и Smooth Streaming): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/ 
* URL-адрес для приобретения лицензии Widevine (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4 
* URL-адрес для приобретения лицензии FairPlay (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8 

### <a name="sample-2"></a>Пример 2

* URL-адрес источника (основной): http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest 
* URL-адрес для приобретения лицензии PlayReady (DASH и Smooth Streaming): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx 

### <a name="sample-3"></a>Пример 3

* URL-адрес источника: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest 
* URL-адрес для приобретения лицензии PlayReady (DASH и Smooth Streaming): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/ 

### <a name="sample-4"></a>Пример 4

* URL-адрес источника: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest 
* URL-адрес для приобретения лицензии PlayReady (DASH и Smooth Streaming): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx 

## <a name="summary"></a>Сводка

Таким образом, компоненты DRM служб мультимедиа Azure являются гибкими. Их можно использовать в гибридных сценариях при правильной настройке ключа содержимого и политики доставки ресурсов, как описано в этой статье.

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите схемы обучения работе со службами мультимедиа.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

