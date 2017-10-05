---
title: "Использование партнеров для доставки лицензий Widevine для служб мультимедиа Azure | Документация Майкрософт"
description: "В этой статье описывается использование служб мультимедиа Azure (AMS) для доставки потока, который зашифрован динамически службой AMS, с помощью лицензий DRM PlayReady и Widevine. Лицензию PlayReady выдает сервер лицензирования служб мультимедиа PlayReady, а лицензию Widevine — сервер лицензирования castLabs."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5bcad5a4-c0bb-4871-9cce-808a913c53e6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 6867e4f910970121df3858516c6bab3114c3c6f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="using-partners-to-deliver-widevine-licenses-to-azure-media-services"></a><span data-ttu-id="9512c-104">Использование партнеров для доставки лицензий Widevine для служб мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="9512c-104">Using partners to deliver Widevine licenses to Azure Media Services</span></span>
## <a name="overview"></a><span data-ttu-id="9512c-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="9512c-105">Overview</span></span>
<span data-ttu-id="9512c-106">Службы мультимедиа Microsoft Azure позволяет доставлять MPEG-DASH c защитой по технологии Widevine DRM, который соответствует спецификации общего шифрования (CENC).</span><span class="sxs-lookup"><span data-stu-id="9512c-106">Microsoft Azure Media Services enables you to deliver MPEG-DASH protected with Widevine DRM, which is encrypted per the Common Encryption (CENC) specification.</span></span>

<span data-ttu-id="9512c-107">Начиная с версии 3.5.2 пакета SDK служб мультимедиа для .NET, службы мультимедиа позволяют настраивать шаблоны лицензии Widevine и получать лицензии Widevine.</span><span class="sxs-lookup"><span data-stu-id="9512c-107">Starting with the Media Services .NET SDK version 3.5.2, Media Services enables you to configure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="9512c-108">Для доставки лицензий Widevine можно использовать следующих партнеров AMS: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="9512c-108">You can also use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

## <a name="castlabs"></a><span data-ttu-id="9512c-109">castLabs</span><span class="sxs-lookup"><span data-stu-id="9512c-109">castLabs</span></span>
<span data-ttu-id="9512c-110">Для доставки лицензий Widevine можно использовать [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="9512c-110">You can use [castLabs](http://castlabs.com/company/partners/azure/) to deliver Widevine licenses.</span></span> <span data-ttu-id="9512c-111">Дополнительные сведения см. в статье [Использование castLabs для доставки лицензий DRM в службы мультимедиа Azure](media-services-castlabs-integration.md).</span><span class="sxs-lookup"><span data-stu-id="9512c-111">For more information, see [Using castLabs to deliver DRM licenses to Azure Media Services](media-services-castlabs-integration.md)</span></span>

## <a name="axinom"></a><span data-ttu-id="9512c-112">Axinom</span><span class="sxs-lookup"><span data-stu-id="9512c-112">Axinom</span></span>
<span data-ttu-id="9512c-113">Для доставки лицензий Widevine можно использовать [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/).</span><span class="sxs-lookup"><span data-stu-id="9512c-113">You can use [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) to deliver Widevine licenses.</span></span> <span data-ttu-id="9512c-114">Дополнительные сведения см. в статье [Использование Axinom для доставки лицензий DRM в службы мультимедиа Azure](media-services-axinom-integration.md).</span><span class="sxs-lookup"><span data-stu-id="9512c-114">For more information, see [Using Axinom to deliver DRM licenses to Azure Media Services](media-services-axinom-integration.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="9512c-115">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="9512c-115">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9512c-116">Отзывы</span><span class="sxs-lookup"><span data-stu-id="9512c-116">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="9512c-117">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="9512c-117">See also</span></span>
[<span data-ttu-id="9512c-118">Дополнительные сведения см. в статье Использование общего динамического шифрования PlayReady и (или) Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="9512c-118">Using PlayReady and/or Widevine dynamic common encryption</span></span>](media-services-protect-with-drm.md)

[<span data-ttu-id="9512c-119">Блог по Mingfei</span><span class="sxs-lookup"><span data-stu-id="9512c-119">Mingfei’s blog</span></span>](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/)

