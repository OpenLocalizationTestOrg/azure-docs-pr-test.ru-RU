---
title: "Общие сведения о динамической упаковки служб мультимедиа aaaAzure | Документы Microsoft"
description: "раздел содержит Hello и общие сведения о динамической упаковки."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0d9e4f54-5daa-45c1-bfaa-cf09ca89b812
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 970e24eba800e098774172c87f56629430b227a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-packaging"></a><span data-ttu-id="99b99-103">Динамическая упаковка</span><span class="sxs-lookup"><span data-stu-id="99b99-103">Dynamic packaging</span></span>
## <a name="overview"></a><span data-ttu-id="99b99-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="99b99-104">Overview</span></span>
<span data-ttu-id="99b99-105">Службы мультимедиа Microsoft Azure можно использовать toodeliver много media source форматы файлов, форматов потоковой передачи мультимедиа и защиты содержимого форматы tooa разных технологиях клиента (например, iOS, XBOX, Silverlight, Windows 8).</span><span class="sxs-lookup"><span data-stu-id="99b99-105">Microsoft Azure Media Services can be used toodeliver many media source file formats, media streaming formats, and content protection formats tooa variety of client technologies (for example, iOS, XBOX, Silverlight, Windows 8).</span></span> <span data-ttu-id="99b99-106">Эти клиенты работают по разным протоколам: например, для iOS используется формат потоковой трансляции HTTP (HLS) V4, а для технологий Silverlight и Xbox необходимо использовать формат Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="99b99-106">These clients understand different protocols, for example iOS requires an HTTP Live Streaming (HLS) V4 format and Silverlight and Xbox require Smooth Streaming.</span></span> <span data-ttu-id="99b99-107">Если у вас есть набор с адаптивной скоростью (с несколькими скоростями) MP4 файлов (ISO Base Media 14496-12) или набор файлов Smooth Streaming с адаптивной скоростью, которые должны tooclients tooserve понимают MPEG DASH, HLS или Smooth Streaming, следует воспользоваться преимуществами мультимедиа Динамическая упаковка служб.</span><span class="sxs-lookup"><span data-stu-id="99b99-107">If you have a set of adaptive bitrate (multi-bitrate) MP4 (ISO Base Media 14496-12) files or a set of adaptive bitrate Smooth Streaming files that you want tooserve tooclients that understand MPEG DASH, HLS or Smooth Streaming, you should take advantage of Media Services dynamic packaging.</span></span>

<span data-ttu-id="99b99-108">С помощью динамической упаковки достаточно — toocreate актив, содержащий набор файлов MP4 с адаптивным битрейтом или файлов Smooth Streaming с адаптивной скоростью.</span><span class="sxs-lookup"><span data-stu-id="99b99-108">With dynamic packaging all you need is toocreate an asset that contains a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="99b99-109">Затем на основе заданного формата hello в манифесте hello или фрагмента запроса, hello server проверит Получение потока hello в протоколе hello, которую вы выбрали потоковой передачи по требованию.</span><span class="sxs-lookup"><span data-stu-id="99b99-109">Then, based on hello specified format in hello manifest or fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="99b99-110">В результате достаточно toostore и оплаты для hello файлов в едином формате хранилища и службы мультимедиа будут создавать и обслуживать соответствующий ответ hello на основе запросов клиента.</span><span class="sxs-lookup"><span data-stu-id="99b99-110">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="99b99-111">Hello следующей схеме показан hello традиционное кодирование и статическая упаковка рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="99b99-111">hello following diagram shows hello traditional encoding and static packaging workflow.</span></span>

![Статическое кодирование](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

<span data-ttu-id="99b99-113">Hello следующей диаграмме показан рабочий процесс hello динамической упаковки.</span><span class="sxs-lookup"><span data-stu-id="99b99-113">hello following diagram shows hello dynamic packaging workflow.</span></span>

![Динамическое кодирование](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a><span data-ttu-id="99b99-115">Стандартный сценарий</span><span class="sxs-lookup"><span data-stu-id="99b99-115">Common scenario</span></span>
1. <span data-ttu-id="99b99-116">Отправьте входной файл (он также называется мезонинным).</span><span class="sxs-lookup"><span data-stu-id="99b99-116">Upload an input file (called a mezzanine file).</span></span> <span data-ttu-id="99b99-117">Например, H.264, MP4 или WMV (hello список поддерживаемых форматов см. [форматы, поддерживаемые Media Encoder Стандартная hello](media-services-media-encoder-standard-formats.md).</span><span class="sxs-lookup"><span data-stu-id="99b99-117">For example, H.264, MP4, or WMV (for hello list of supported formats see [Formats Supported by hello Media Encoder Standard](media-services-media-encoder-standard-formats.md).</span></span>
2. <span data-ttu-id="99b99-118">Закодируйте мезонинный файл tooH.264 MP4 с адаптивной скоростью наборов.</span><span class="sxs-lookup"><span data-stu-id="99b99-118">Encode your mezzanine file tooH.264 MP4 adaptive bitrate sets.</span></span>
3. <span data-ttu-id="99b99-119">Опубликуйте hello актив, содержащий hello, создав локатор по запросу hello набор MP4 с адаптивной скоростью.</span><span class="sxs-lookup"><span data-stu-id="99b99-119">Publish hello asset that contains hello adaptive bitrate MP4 set by creating hello On-Demand Locator.</span></span>
4. <span data-ttu-id="99b99-120">Построение hello tooaccess URL-адреса потоковой передачи и потоковую передачу контента.</span><span class="sxs-lookup"><span data-stu-id="99b99-120">Build hello streaming URLs tooaccess and stream your content.</span></span>

## <a name="preparing-assets-for-dynamic-streaming"></a><span data-ttu-id="99b99-121">Подготовка ресурсов для динамической потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="99b99-121">Preparing assets for dynamic streaming</span></span>
<span data-ttu-id="99b99-122">tooprepare актива для динамической потоковой передачи можно использовать два варианта:</span><span class="sxs-lookup"><span data-stu-id="99b99-122">tooprepare your asset for dynamic streaming you have two options:</span></span>

1. <span data-ttu-id="99b99-123">[Отправьте главный файл](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="99b99-123">[Upload a master file](media-services-dotnet-upload-files.md).</span></span>
2. <span data-ttu-id="99b99-124">[Использовать hello Media Encoder стандартный кодировщик tooproduce H.264 MP4 с адаптивной скоростью наборы](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="99b99-124">[Use hello Media Encoder Standard encoder tooproduce H.264 MP4 adaptive bitrate sets](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>
3. <span data-ttu-id="99b99-125">[Выполните потоковую передачу содержимого](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="99b99-125">[Stream your content](media-services-deliver-content-overview.md).</span></span>

## <span data-ttu-id="99b99-126"><a id="unsupported_formats"></a>Форматы, не поддерживаемые динамической упаковкой</span><span class="sxs-lookup"><span data-stu-id="99b99-126"><a id="unsupported_formats"></a>Formats that are not supported by dynamic packaging</span></span>
<span data-ttu-id="99b99-127">Hello следующие форматы исходных файлов не поддерживаются для динамической упаковки.</span><span class="sxs-lookup"><span data-stu-id="99b99-127">hello following source file formats are not supported by dynamic packaging.</span></span>

* <span data-ttu-id="99b99-128">MP4-файлы в формате Dolby Digital.</span><span class="sxs-lookup"><span data-stu-id="99b99-128">Dolby digital mp4 files.</span></span>
* <span data-ttu-id="99b99-129">Файлы Smooth в формате Dolby Digital.</span><span class="sxs-lookup"><span data-stu-id="99b99-129">Dolby digital smooth files.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="99b99-130">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="99b99-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="99b99-131">Отзывы</span><span class="sxs-lookup"><span data-stu-id="99b99-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

