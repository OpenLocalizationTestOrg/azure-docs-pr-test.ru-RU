---
title: "aaaMedia расширенного рабочего процесса кодировщика форматы и кодеки | Документы Microsoft"
description: "В этом разделе содержится обзор форматов и кодеков расширенного рабочего процесса кодировщика мультимедиа."
services: media-services
documentationcenter: 
author: juliako
manager: erik43
editor: 
ms.assetid: b197fce8-3b9b-4189-8d08-486810c0426f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;anilmur
ms.openlocfilehash: e781384ca8f08926f00c83b6710fd413ce2a3e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-premium-workflow-formats-and-codecs"></a><span data-ttu-id="14b64-103">Форматы и кодеки рабочего процесса Premium Media Encoder</span><span class="sxs-lookup"><span data-stu-id="14b64-103">Media Encoder Premium Workflow formats and codecs</span></span>
> [!NOTE]
> <span data-ttu-id="14b64-104">Вопросы о кодировщике Premium направляйте по адресу mepd@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="14b64-104">For premium encoder questions, email mepd at Microsoft.com.</span></span>
> 
> <span data-ttu-id="14b64-105">Обработчик мультимедиа расширенного рабочего процесса кодировщика мультимедиа, рассматриваемый в этом разделе, недоступен в Китае.</span><span class="sxs-lookup"><span data-stu-id="14b64-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span> 
> 
> 

<span data-ttu-id="14b64-106">Этот документ содержит список входных и выходных файлов форматы и кодеки, поддерживаемыми hello общедоступной предварительной версии hello **расширенного рабочего процесса кодировщика мультимедиа** кодировщика.</span><span class="sxs-lookup"><span data-stu-id="14b64-106">This document contains a list of input and output file formats and codecs that are supported by hello public preview version of hello **Media Encoder Premium Workflow** encoder.</span></span>

[<span data-ttu-id="14b64-107">Входные форматы и кодеки расширенного рабочего процесса кодировщика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="14b64-107">Media Encoder Premium Worflow Input Formats and Codecs</span></span>](#input_formats)

[<span data-ttu-id="14b64-108">Выходные форматы и кодеки расширенного рабочего процесса кодировщика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="14b64-108">Media Encoder Premium Worflow Output Formats and Codecs</span></span>](#output_formats)

<span data-ttu-id="14b64-109">**Расширенный рабочий процесс кодировщика мультимедиа** поддерживает скрытые субтитры, описанные в [этом](#closed_captioning) разделе.</span><span class="sxs-lookup"><span data-stu-id="14b64-109">**Media Encoder Premium Workflow** supports closed captioning described in [this](#closed_captioning) section.</span></span> 

## <span data-ttu-id="14b64-110"><a id="input_formats"></a>Входные форматы и кодеки расширенного рабочего процесса кодировщика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="14b64-110"><a id="input_formats"></a>Media Encoder Premium Workflow Input Formats and Codecs</span></span>
<span data-ttu-id="14b64-111">Привет, в следующем разделе перечислены hello кодеков и форматов файлов, этот обработчик мультимедиа поддерживает в качестве входных данных.</span><span class="sxs-lookup"><span data-stu-id="14b64-111">hello following section lists hello codecs and file formats that this media processor supports as input.</span></span>

### <a name="input-containerfile-formats"></a><span data-ttu-id="14b64-112">Контейнер ввода/ форматы файлов</span><span class="sxs-lookup"><span data-stu-id="14b64-112">Input Container/File Formats</span></span>
* <span data-ttu-id="14b64-113">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="14b64-113">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="14b64-114">MXF/SMPTE 377M</span><span class="sxs-lookup"><span data-stu-id="14b64-114">MXF/SMPTE 377M</span></span>
* <span data-ttu-id="14b64-115">GXF</span><span class="sxs-lookup"><span data-stu-id="14b64-115">GXF</span></span>
* <span data-ttu-id="14b64-116">Транспортные потоки MPEG-2</span><span class="sxs-lookup"><span data-stu-id="14b64-116">MPEG-2 Transport Streams</span></span>
* <span data-ttu-id="14b64-117">Программные потоки MPEG-2</span><span class="sxs-lookup"><span data-stu-id="14b64-117">MPEG-2 Program Streams</span></span>
* <span data-ttu-id="14b64-118">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="14b64-118">MPEG-4/MP4</span></span>
* <span data-ttu-id="14b64-119">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="14b64-119">Windows Media/ASF</span></span>
* <span data-ttu-id="14b64-120">AVI (без сжатия 8 бит/10 бит)</span><span class="sxs-lookup"><span data-stu-id="14b64-120">AVI (Uncompressed 8bit/10bit)</span></span>

### <a name="input-video-codecs"></a><span data-ttu-id="14b64-121">Входные видеокодеки</span><span class="sxs-lookup"><span data-stu-id="14b64-121">Input Video Codecs</span></span>
* <span data-ttu-id="14b64-122">AVC 8-разрядное/10-битный, копирование too4:2:2, включая AVCIntra</span><span class="sxs-lookup"><span data-stu-id="14b64-122">AVC 8-bit/10-bit, up too4:2:2, including AVCIntra</span></span>
* <span data-ttu-id="14b64-123">Avid DNxHD (в MXF)</span><span class="sxs-lookup"><span data-stu-id="14b64-123">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="14b64-124">DVCPro/DVCProHD (в MXF)</span><span class="sxs-lookup"><span data-stu-id="14b64-124">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="14b64-125">JPEG2000</span><span class="sxs-lookup"><span data-stu-id="14b64-125">JPEG2000</span></span>
* <span data-ttu-id="14b64-126">MPEG-2 (профиль too422 и высокого уровня, включая варианты, такие как XDCAM, XDCAM HD, XDCAM IMX, CableLabs® и D10)</span><span class="sxs-lookup"><span data-stu-id="14b64-126">MPEG-2 (up too422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="14b64-127">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="14b64-127">MPEG-1</span></span>
* <span data-ttu-id="14b64-128">Windows Media Video/VC-1</span><span class="sxs-lookup"><span data-stu-id="14b64-128">Windows Media Video/VC-1</span></span>

### <a name="input-audio-codecs"></a><span data-ttu-id="14b64-129">Входные аудиокодеки</span><span class="sxs-lookup"><span data-stu-id="14b64-129">Input Audio Codecs</span></span>
* <span data-ttu-id="14b64-130">AES (SMPTE 331M и 302M, AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="14b64-130">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="14b64-131">Dolby® E</span><span class="sxs-lookup"><span data-stu-id="14b64-131">Dolby® E</span></span>
* <span data-ttu-id="14b64-132">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="14b64-132">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="14b64-133">AAC (AAC-LC и AAC-HE, AAC HEv2; копирование too5.1)</span><span class="sxs-lookup"><span data-stu-id="14b64-133">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up too5.1)</span></span>
* <span data-ttu-id="14b64-134">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="14b64-134">MPEG Layer 2</span></span>
* <span data-ttu-id="14b64-135">MP3 (MPEG-1 Audio Layer 3)</span><span class="sxs-lookup"><span data-stu-id="14b64-135">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="14b64-136">Windows Media Audio</span><span class="sxs-lookup"><span data-stu-id="14b64-136">Windows Media Audio</span></span>
* <span data-ttu-id="14b64-137">WAV/PCM</span><span class="sxs-lookup"><span data-stu-id="14b64-137">WAV/PCM</span></span>

## <span data-ttu-id="14b64-138"><a id="output_format"></a>Выходные форматы и кодеки расширенного рабочего процесса кодировщика мультимедиа</span><span class="sxs-lookup"><span data-stu-id="14b64-138"><a id="output_format"></a>Media Encoder Premium Workflow Output Formats and Codecs</span></span>
<span data-ttu-id="14b64-139">Hello в подразделе ниже приведены hello кодеки и форматы, поддерживаемые в качестве выходных данных из этого обработчика мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="14b64-139">hello following section lists hello codecs and file formats that are supported as output from this media processor.</span></span>

### <a name="output-containerfile-formats"></a><span data-ttu-id="14b64-140">Контейнер вывода/ форматы файлов</span><span class="sxs-lookup"><span data-stu-id="14b64-140">Output Container/File Formats</span></span>
* <span data-ttu-id="14b64-141">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="14b64-141">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="14b64-142">MXF (OP1a, XDCAM и AS02)</span><span class="sxs-lookup"><span data-stu-id="14b64-142">MXF (OP1a, XDCAM and AS02)</span></span>
* <span data-ttu-id="14b64-143">DPP (включая AS11)</span><span class="sxs-lookup"><span data-stu-id="14b64-143">DPP (including AS11)</span></span>
* <span data-ttu-id="14b64-144">GXF</span><span class="sxs-lookup"><span data-stu-id="14b64-144">GXF</span></span>
* <span data-ttu-id="14b64-145">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="14b64-145">MPEG-4/MP4</span></span>
* <span data-ttu-id="14b64-146">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="14b64-146">Windows Media/ASF</span></span>
* <span data-ttu-id="14b64-147">AVI (без сжатия 8 бит/10 бит)</span><span class="sxs-lookup"><span data-stu-id="14b64-147">AVI (Uncompressed 8bit/10bit)</span></span>
* <span data-ttu-id="14b64-148">Формат файлов Smooth Streaming (PIFF 1.3)</span><span class="sxs-lookup"><span data-stu-id="14b64-148">Smooth Streaming File Format (PIFF 1.3)</span></span>
* <span data-ttu-id="14b64-149">MPEG-TS</span><span class="sxs-lookup"><span data-stu-id="14b64-149">MPEG-TS</span></span> 

### <a name="output-video-codecs"></a><span data-ttu-id="14b64-150">Выходные видеокодеки</span><span class="sxs-lookup"><span data-stu-id="14b64-150">Output Video Codecs</span></span>
* <span data-ttu-id="14b64-151">AVC (H.264; 8-разрядное; Настройка tooHigh профиля, уровень 5.2; Ultra HD 4 КБ; Внутри AVC)</span><span class="sxs-lookup"><span data-stu-id="14b64-151">AVC (H.264; 8-bit; up tooHigh Profile, Level 5.2; 4K Ultra HD; AVC Intra)</span></span>
* <span data-ttu-id="14b64-152">Avid DNxHD (в MXF)</span><span class="sxs-lookup"><span data-stu-id="14b64-152">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="14b64-153">DVCPro/DVCProHD (в MXF)</span><span class="sxs-lookup"><span data-stu-id="14b64-153">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="14b64-154">MPEG-2 (профиль too422 и высокого уровня, включая варианты, такие как XDCAM, XDCAM HD, XDCAM IMX, CableLabs® и D10)</span><span class="sxs-lookup"><span data-stu-id="14b64-154">MPEG-2 (up too422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="14b64-155">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="14b64-155">MPEG-1</span></span>
* <span data-ttu-id="14b64-156">Windows Media Video/VC-1</span><span class="sxs-lookup"><span data-stu-id="14b64-156">Windows Media Video/VC-1</span></span>
* <span data-ttu-id="14b64-157">Создание эскизов JPEG</span><span class="sxs-lookup"><span data-stu-id="14b64-157">JPEG thumbnail creation</span></span>

### <a name="output-audio-codecs"></a><span data-ttu-id="14b64-158">Выходные аудиокодеки</span><span class="sxs-lookup"><span data-stu-id="14b64-158">Output Audio Codecs</span></span>
* <span data-ttu-id="14b64-159">AES (SMPTE 331M и 302M, AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="14b64-159">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="14b64-160">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="14b64-160">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="14b64-161">Dolby® Digital Plus (E-AC3) вверх too7.1</span><span class="sxs-lookup"><span data-stu-id="14b64-161">Dolby® Digital Plus (E-AC3) up too7.1</span></span>
* <span data-ttu-id="14b64-162">AAC (AAC-LC и AAC-HE, AAC HEv2; копирование too5.1)</span><span class="sxs-lookup"><span data-stu-id="14b64-162">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up too5.1)</span></span>
* <span data-ttu-id="14b64-163">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="14b64-163">MPEG Layer 2</span></span>
* <span data-ttu-id="14b64-164">MP3 (MPEG-1 Audio Layer 3)</span><span class="sxs-lookup"><span data-stu-id="14b64-164">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="14b64-165">Windows Media Audio</span><span class="sxs-lookup"><span data-stu-id="14b64-165">Windows Media Audio</span></span>

>[!NOTE]
><span data-ttu-id="14b64-166">Если кодирование tooDolby® Digital (AC3) hello вывода можно записать только в ISO MP4-файл.</span><span class="sxs-lookup"><span data-stu-id="14b64-166">If you encode tooDolby® Digital (AC3), hello output can only be written into an ISO MP4 file.</span></span>

## <span data-ttu-id="14b64-167"><a id="closed_captioning"></a>Поддержка скрытых титров</span><span class="sxs-lookup"><span data-stu-id="14b64-167"><a id="closed_captioning"></a>Support for Closed Captioning</span></span>
<span data-ttu-id="14b64-168">При приеме **расширенный рабочий процесс кодировщика мультимедиа** поддерживает:</span><span class="sxs-lookup"><span data-stu-id="14b64-168">On ingest, **Media Encoder Premium Workflow** supports:</span></span>

1. <span data-ttu-id="14b64-169">файлы SCC</span><span class="sxs-lookup"><span data-stu-id="14b64-169">SCC files</span></span>
2. <span data-ttu-id="14b64-170">файлы SMPTE-TT</span><span class="sxs-lookup"><span data-stu-id="14b64-170">SMPTE-TT files</span></span>
3. <span data-ttu-id="14b64-171">CEA-608/CEA-708 – переносятся как данные пользователя (сообщения SEI простейших потоков H.264, ATSC/53, SCTE20) или переносятся как вспомогательные данные в файлах MXF/GXF</span><span class="sxs-lookup"><span data-stu-id="14b64-171">CEA-608/CEA-708 – carried as user data (SEI messages of H.264 elementary streams, ATSC/53, SCTE20) or carried as ancillary data in MXF/GXF files</span></span>
4. <span data-ttu-id="14b64-172">Файлы субтитров STL</span><span class="sxs-lookup"><span data-stu-id="14b64-172">STL subtitle files</span></span>

<span data-ttu-id="14b64-173">На выходе доступны следующие варианты hello.</span><span class="sxs-lookup"><span data-stu-id="14b64-173">On output, hello following options are available:</span></span>

1. <span data-ttu-id="14b64-174">Перевод CEA 608 tooCEA 708</span><span class="sxs-lookup"><span data-stu-id="14b64-174">CEA-608 tooCEA-708 translation</span></span>
2. <span data-ttu-id="14b64-175">Пропуск CEA-608/CEA-708 (встраиваются в сообщения SEI простейших потоков H.264 или переносятся как дополнительные данный в файлах MXF)</span><span class="sxs-lookup"><span data-stu-id="14b64-175">CEA-608/CEA-708 pass through (embedded in SEI messages of H.264 elementary streams, or carried as ancillary data in MXF files)</span></span>
3. <span data-ttu-id="14b64-176">SCC</span><span class="sxs-lookup"><span data-stu-id="14b64-176">SCC</span></span>
4. <span data-ttu-id="14b64-177">SMPTE Timed Text (из источника CEA-608 через SMPTE RP2052, включая создание файла DFXP)</span><span class="sxs-lookup"><span data-stu-id="14b64-177">SMPTE Timed Text (from source CEA-608 per SMPTE RP2052; including DFXP file creation)</span></span>
5. <span data-ttu-id="14b64-178">Файл подзаголовка SRT</span><span class="sxs-lookup"><span data-stu-id="14b64-178">SRT Subtitle file</span></span>
6. <span data-ttu-id="14b64-179">Потоки подзаголовка DVB</span><span class="sxs-lookup"><span data-stu-id="14b64-179">DVB subtitle streams</span></span>

<span data-ttu-id="14b64-180">Примечание: не все hello выше выходных форматов поддерживаются для передачи с помощью потоковой передачи в службах мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="14b64-180">Note: not all of hello above output formats are supported for delivery via streaming in Azure Media Services.</span></span>

## <a name="known-issues"></a><span data-ttu-id="14b64-181">Известные проблемы</span><span class="sxs-lookup"><span data-stu-id="14b64-181">Known issues</span></span>
<span data-ttu-id="14b64-182">Если входной видео не содержит титров, hello выходной ресурс по-прежнему будет содержать пустой файл TTML.</span><span class="sxs-lookup"><span data-stu-id="14b64-182">If your input video does not contain closed captioning, hello output Asset will still contain an empty TTML file.</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="14b64-183">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="14b64-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="14b64-184">Отзывы</span><span class="sxs-lookup"><span data-stu-id="14b64-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

