---
title: "aaaAzure схем входных метаданных служб Media Services | Документы Microsoft"
description: "Hello разделе приводится обзор схем входных метаданных служб мультимедиа Azure."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d72848e2-4b65-4c84-94bc-e2a90a6e7f47
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 9b72c6ff317aa98451ea75548465dc6023b44a55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="input-metadata"></a><span data-ttu-id="60565-103">Входные метаданные</span><span class="sxs-lookup"><span data-stu-id="60565-103">Input Metadata</span></span>
<span data-ttu-id="60565-104">Задание кодирования связано с входным активом (или активами) для которого необходимо tooperform некоторые задачи кодирования.</span><span class="sxs-lookup"><span data-stu-id="60565-104">An encoding job is associated with an input asset (or assets) on which you want tooperform some encoding tasks.</span></span>  <span data-ttu-id="60565-105">После выполнения задачи создается выходной ресурс-контейнер.</span><span class="sxs-lookup"><span data-stu-id="60565-105">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="60565-106">Hello выходной актив содержит видео, аудио-и эскизов, файл манифеста, т. д. hello выходной актив содержит файл, содержащий метаданные о входном активе hello.</span><span class="sxs-lookup"><span data-stu-id="60565-106">hello output asset contains video, audio, thumbnails, manifest, etc. hello output asset also contains a file with metadata about hello input asset.</span></span> <span data-ttu-id="60565-107">Hello hello метаданных XML-файлу имеет следующий формат hello: &lt;идентификатор_актива&gt;_metadata.xml (например, 41114ad3-eb5e - 4c 57 8d 92-5354e2b7d4a4_metadata.xml), где &lt;идентификатор_актива&gt; — hello AssetId значение входного актива hello.</span><span class="sxs-lookup"><span data-stu-id="60565-107">hello name of hello metadata XML file has hello following format: &lt;asset_id&gt;_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where &lt;asset_id&gt; is hello AssetId value of hello input asset.</span></span>  

<span data-ttu-id="60565-108">Если требуется файл метаданных tooexamine hello, можно создать **SAS** обнаружения и загрузки hello файл tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="60565-108">If you want tooexamine hello metadata file, you can create a **SAS** locator and download hello file tooyour local computer.</span></span> <span data-ttu-id="60565-109">О том, как можно найти пример toocreate указателя SAS и загрузки файла [с помощью расширений SDK .NET служб мультимедиа hello](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="60565-109">You can find an example on how toocreate a SAS locator and download a file  [Using hello Media Services .NET SDK Extensions](media-services-dotnet-get-started.md).</span></span>  

<span data-ttu-id="60565-110">В этом разделе рассматривается hello элементы и типы XML-схемы hello на какие входные метаданными hello (&lt;идентификатор_актива&gt;_metadata.xml) основана.</span><span class="sxs-lookup"><span data-stu-id="60565-110">This topic discusses hello elements and types of hello XML schema on which hello input metada (&lt;asset_id&gt;_metadata.xml) is based.</span></span>  <span data-ttu-id="60565-111">Сведения о файле hello, содержащем метаданные выходного актива hello. в разделе [выходные метаданные](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="60565-111">For information about hello file that contains metadata about hello output asset, see [Output Metadata](media-services-output-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="60565-112">Можно найти hello [код схемы](media-services-input-metadata-schema.md#code) [пример XML-файла](media-services-input-metadata-schema.md#xml) в конце hello в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="60565-112">You can find hello [Schema Code](media-services-input-metadata-schema.md#code) an [XML example](media-services-input-metadata-schema.md#xml) at hello end of this topic.</span></span>  
> 
> 

## <span data-ttu-id="60565-113"><a name="AssetFiles"></a> Элемент AssetFiles (корневой элемент)</span><span class="sxs-lookup"><span data-stu-id="60565-113"><a name="AssetFiles"></a> AssetFiles element (root element)</span></span>
<span data-ttu-id="60565-114">Содержит коллекцию [элемент AssetFile](media-services-input-metadata-schema.md#AssetFile)s для задания кодирования hello.</span><span class="sxs-lookup"><span data-stu-id="60565-114">Contains a collection of [AssetFile element](media-services-input-metadata-schema.md#AssetFile)s for hello encoding job.</span></span>  

<span data-ttu-id="60565-115">См. пример XML в конце этого раздела в hello: [пример XML-файла](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="60565-115">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

| <span data-ttu-id="60565-116">Имя</span><span class="sxs-lookup"><span data-stu-id="60565-116">Name</span></span> | <span data-ttu-id="60565-117">Описание</span><span class="sxs-lookup"><span data-stu-id="60565-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="60565-118">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="60565-118">**AssetFile**</span></span><br /><br /> <span data-ttu-id="60565-119">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="60565-119">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="60565-120">Один дочерний элемент.</span><span class="sxs-lookup"><span data-stu-id="60565-120">A single child element.</span></span> <span data-ttu-id="60565-121">Дополнительные сведения см. в разделе [Элемент AssetFile](media-services-input-metadata-schema.md#AssetFile).</span><span class="sxs-lookup"><span data-stu-id="60565-121">For more information, see [AssetFile element](media-services-input-metadata-schema.md#AssetFile).</span></span> |

## <span data-ttu-id="60565-122"><a name="AssetFile"></a> Элемент AssetFile</span><span class="sxs-lookup"><span data-stu-id="60565-122"><a name="AssetFile"></a> AssetFile element</span></span>
 <span data-ttu-id="60565-123">Содержит атрибуты и элементы, описывающие файл ресурса-контейнера.</span><span class="sxs-lookup"><span data-stu-id="60565-123">Contains attributes and elements that describe an asset file.</span></span>  

 <span data-ttu-id="60565-124">См. пример XML в конце этого раздела в hello: [пример XML-файла](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="60565-124">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="60565-125">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="60565-125">Attributes</span></span>
| <span data-ttu-id="60565-126">Имя</span><span class="sxs-lookup"><span data-stu-id="60565-126">Name</span></span> | <span data-ttu-id="60565-127">Тип</span><span class="sxs-lookup"><span data-stu-id="60565-127">Type</span></span> | <span data-ttu-id="60565-128">Описание</span><span class="sxs-lookup"><span data-stu-id="60565-128">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60565-129">**Имя**</span><span class="sxs-lookup"><span data-stu-id="60565-129">**Name**</span></span><br /><br /> <span data-ttu-id="60565-130">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-130">Required</span></span> |<span data-ttu-id="60565-131">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="60565-131">**xs:string**</span></span> |<span data-ttu-id="60565-132">Имя файла ресурса-контейнера.</span><span class="sxs-lookup"><span data-stu-id="60565-132">Asset file name.</span></span> |
| <span data-ttu-id="60565-133">**Размер**</span><span class="sxs-lookup"><span data-stu-id="60565-133">**Size**</span></span><br /><br /> <span data-ttu-id="60565-134">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-134">Required</span></span> |<span data-ttu-id="60565-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="60565-135">**xs:long**</span></span> |<span data-ttu-id="60565-136">Размер файла актива hello в байтах.</span><span class="sxs-lookup"><span data-stu-id="60565-136">Size of hello asset file in bytes.</span></span> |
| <span data-ttu-id="60565-137">**Duration**</span><span class="sxs-lookup"><span data-stu-id="60565-137">**Duration**</span></span><br /><br /> <span data-ttu-id="60565-138">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-138">Required</span></span> |<span data-ttu-id="60565-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="60565-139">**xs:duration**</span></span> |<span data-ttu-id="60565-140">Длительность воспроизведения содержимого.</span><span class="sxs-lookup"><span data-stu-id="60565-140">Content play back duration.</span></span> <span data-ttu-id="60565-141">Пример: Duration="PT25M37.757S".</span><span class="sxs-lookup"><span data-stu-id="60565-141">Example: Duration="PT25M37.757S".</span></span> |
| <span data-ttu-id="60565-142">**NumberOfStreams**</span><span class="sxs-lookup"><span data-stu-id="60565-142">**NumberOfStreams**</span></span><br /><br /> <span data-ttu-id="60565-143">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-143">Required</span></span> |<span data-ttu-id="60565-144">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-144">**xs:int**</span></span> |<span data-ttu-id="60565-145">Количество потоков в файл актива hello.</span><span class="sxs-lookup"><span data-stu-id="60565-145">Number of streams in hello asset file.</span></span> |
| <span data-ttu-id="60565-146">**FormatNames**</span><span class="sxs-lookup"><span data-stu-id="60565-146">**FormatNames**</span></span><br /><br /> <span data-ttu-id="60565-147">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-147">Required</span></span> |<span data-ttu-id="60565-148">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="60565-148">**xs:string**</span></span> |<span data-ttu-id="60565-149">Имена форматов.</span><span class="sxs-lookup"><span data-stu-id="60565-149">Format names.</span></span> |
| <span data-ttu-id="60565-150">**FormatVerboseNames**</span><span class="sxs-lookup"><span data-stu-id="60565-150">**FormatVerboseNames**</span></span><br /><br /> <span data-ttu-id="60565-151">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-151">Required</span></span> |<span data-ttu-id="60565-152">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="60565-152">**xs:string**</span></span> |<span data-ttu-id="60565-153">Подробные имена форматов.</span><span class="sxs-lookup"><span data-stu-id="60565-153">Format verbose names.</span></span> |
| <span data-ttu-id="60565-154">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="60565-154">**StartTime**</span></span> |<span data-ttu-id="60565-155">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="60565-155">**xs:duration**</span></span> |<span data-ttu-id="60565-156">Время начала содержимого.</span><span class="sxs-lookup"><span data-stu-id="60565-156">Content start time.</span></span> <span data-ttu-id="60565-157">Пример: StartTime="PT2.669S".</span><span class="sxs-lookup"><span data-stu-id="60565-157">Example: StartTime="PT2.669S".</span></span> |
| <span data-ttu-id="60565-158">**OverallBitRate**</span><span class="sxs-lookup"><span data-stu-id="60565-158">**OverallBitRate**</span></span> |<span data-ttu-id="60565-159">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-159">**xs:int**</span></span> |<span data-ttu-id="60565-160">Средняя скорость файла актива hello в Кбит/с.</span><span class="sxs-lookup"><span data-stu-id="60565-160">Average bitrate of hello asset file in kbps.</span></span> |

> [!NOTE]
> <span data-ttu-id="60565-161">Hello следующие четыре дочерних элемента должны появляться последовательно.</span><span class="sxs-lookup"><span data-stu-id="60565-161">hello following 4 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="60565-162">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="60565-162">Child elements</span></span>
| <span data-ttu-id="60565-163">Имя</span><span class="sxs-lookup"><span data-stu-id="60565-163">Name</span></span> | <span data-ttu-id="60565-164">Тип</span><span class="sxs-lookup"><span data-stu-id="60565-164">Type</span></span> | <span data-ttu-id="60565-165">Описание</span><span class="sxs-lookup"><span data-stu-id="60565-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60565-166">**Programs**</span><span class="sxs-lookup"><span data-stu-id="60565-166">**Programs**</span></span><br /><br /> <span data-ttu-id="60565-167">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="60565-167">minOccurs="0"</span></span> | |<span data-ttu-id="60565-168">Коллекция всех [элемент программы](media-services-input-metadata-schema.md#Programs) при hello файл актива имеет формат MPEG-TS.</span><span class="sxs-lookup"><span data-stu-id="60565-168">Collection of all [Programs element](media-services-input-metadata-schema.md#Programs) when hello asset file is in MPEG-TS format.</span></span> |
| <span data-ttu-id="60565-169">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="60565-169">**VideoTracks**</span></span><br /><br /> <span data-ttu-id="60565-170">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="60565-170">minOccurs="0"</span></span> | |<span data-ttu-id="60565-171">Каждый физический файл ресурса-контейнера может содержать ноль или более видеодорожек, чередуемых в соответствующем формате ресурса-контейнера.</span><span class="sxs-lookup"><span data-stu-id="60565-171">Each physical asset file can contain zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="60565-172">Этот элемент содержит коллекцию всех [элемент VideoTracks](media-services-input-metadata-schema.md#VideoTracks) , которые являются частью файла актива hello.</span><span class="sxs-lookup"><span data-stu-id="60565-172">This element contains a collection of all [VideoTracks element](media-services-input-metadata-schema.md#VideoTracks) that are part of hello asset file.</span></span> |
| <span data-ttu-id="60565-173">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="60565-173">**AudioTracks**</span></span><br /><br /> <span data-ttu-id="60565-174">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="60565-174">minOccurs="0"</span></span> | |<span data-ttu-id="60565-175">Каждый физический файл ресурса-контейнера может содержать ноль или более звуковых дорожек, чередуемых в соответствующем формате ресурса-контейнера.</span><span class="sxs-lookup"><span data-stu-id="60565-175">Each physical asset file can contain zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="60565-176">Этот элемент содержит коллекцию всех [элемент AudioTracks](media-services-input-metadata-schema.md#AudioTracks) , которые являются частью файла актива hello.</span><span class="sxs-lookup"><span data-stu-id="60565-176">This element contains a collection of all [AudioTracks element](media-services-input-metadata-schema.md#AudioTracks) that are part of hello asset file.</span></span> |
| <span data-ttu-id="60565-177">**Metadata**</span><span class="sxs-lookup"><span data-stu-id="60565-177">**Metadata**</span></span><br /><br /> <span data-ttu-id="60565-178">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="60565-178">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="60565-179">MetadataType</span><span class="sxs-lookup"><span data-stu-id="60565-179">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="60565-180">Метаданные файла ресурса-контейнера, представленные в виде строки "ключ —значение".</span><span class="sxs-lookup"><span data-stu-id="60565-180">Asset file’s metadata represented as key\value strings.</span></span> <span data-ttu-id="60565-181">Например:</span><span class="sxs-lookup"><span data-stu-id="60565-181">For example:</span></span><br /><br /> <span data-ttu-id="60565-182">**&lt;Metadata key="language" value="eng" /&gt;**</span><span class="sxs-lookup"><span data-stu-id="60565-182">**&lt;Metadata key="language" value="eng" /&gt;**</span></span> |

## <span data-ttu-id="60565-183"><a name="TrackType"></a> TrackType</span><span class="sxs-lookup"><span data-stu-id="60565-183"><a name="TrackType"></a> TrackType</span></span>
<span data-ttu-id="60565-184">См. пример XML в конце этого раздела в hello: [пример XML-файла](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="60565-184">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="60565-185">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="60565-185">Attributes</span></span>
| <span data-ttu-id="60565-186">Имя</span><span class="sxs-lookup"><span data-stu-id="60565-186">Name</span></span> | <span data-ttu-id="60565-187">Тип</span><span class="sxs-lookup"><span data-stu-id="60565-187">Type</span></span> | <span data-ttu-id="60565-188">Описание</span><span class="sxs-lookup"><span data-stu-id="60565-188">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60565-189">**Id**</span><span class="sxs-lookup"><span data-stu-id="60565-189">**Id**</span></span><br /><br /> <span data-ttu-id="60565-190">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-190">Required</span></span> |<span data-ttu-id="60565-191">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-191">**xs:int**</span></span> |<span data-ttu-id="60565-192">Отсчитываемый от нуля индекс аудио- или видеодорожки.</span><span class="sxs-lookup"><span data-stu-id="60565-192">Zero-based index of this audio or video track.</span></span><br /><br /> <span data-ttu-id="60565-193">Это не обязательно, hello trackid, который используется в MP4-файле.</span><span class="sxs-lookup"><span data-stu-id="60565-193">This is not necessarily that hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="60565-194">**Codec**</span><span class="sxs-lookup"><span data-stu-id="60565-194">**Codec**</span></span> |<span data-ttu-id="60565-195">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="60565-195">**xs:string**</span></span> |<span data-ttu-id="60565-196">Строка кодека видеодорожки.</span><span class="sxs-lookup"><span data-stu-id="60565-196">Video track codec string.</span></span> |
| <span data-ttu-id="60565-197">**CodecLongName**</span><span class="sxs-lookup"><span data-stu-id="60565-197">**CodecLongName**</span></span> |<span data-ttu-id="60565-198">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="60565-198">**xs:string**</span></span> |<span data-ttu-id="60565-199">Полное имя кодека звуковой или видеодорожки.</span><span class="sxs-lookup"><span data-stu-id="60565-199">Audio or video track codec long name.</span></span> |
| <span data-ttu-id="60565-200">**TimeBase**</span><span class="sxs-lookup"><span data-stu-id="60565-200">**TimeBase**</span></span><br /><br /> <span data-ttu-id="60565-201">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-201">Required</span></span> |<span data-ttu-id="60565-202">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="60565-202">**xs:string**</span></span> |<span data-ttu-id="60565-203">Базовый счетчик времени.</span><span class="sxs-lookup"><span data-stu-id="60565-203">Time base.</span></span> <span data-ttu-id="60565-204">Пример: TimeBase="1/48000"</span><span class="sxs-lookup"><span data-stu-id="60565-204">Example: TimeBase="1/48000"</span></span> |
| <span data-ttu-id="60565-205">**NumberOfFrames**</span><span class="sxs-lookup"><span data-stu-id="60565-205">**NumberOfFrames**</span></span> |<span data-ttu-id="60565-206">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-206">**xs:int**</span></span> |<span data-ttu-id="60565-207">Количество кадров (для видеодорожек).</span><span class="sxs-lookup"><span data-stu-id="60565-207">Number of frames (present for video tracks).</span></span> |
| <span data-ttu-id="60565-208">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="60565-208">**StartTime**</span></span> |<span data-ttu-id="60565-209">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="60565-209">**xs:duration**</span></span> |<span data-ttu-id="60565-210">Время начала дорожки.</span><span class="sxs-lookup"><span data-stu-id="60565-210">Track start time.</span></span> <span data-ttu-id="60565-211">Пример: StartTime="PT2.669S"</span><span class="sxs-lookup"><span data-stu-id="60565-211">Example: StartTime="PT2.669S"</span></span> |
| <span data-ttu-id="60565-212">**Duration**</span><span class="sxs-lookup"><span data-stu-id="60565-212">**Duration**</span></span> |<span data-ttu-id="60565-213">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="60565-213">**xs:duration**</span></span> |<span data-ttu-id="60565-214">Продолжительность дорожки.</span><span class="sxs-lookup"><span data-stu-id="60565-214">Track duration.</span></span> <span data-ttu-id="60565-215">Пример: Duration="PTSampleFormat M37.757S".</span><span class="sxs-lookup"><span data-stu-id="60565-215">Example: Duration="PTSampleFormat M37.757S".</span></span> |

> [!NOTE]
> <span data-ttu-id="60565-216">Hello следующие 2 дочерние элементы должны появляться последовательно.</span><span class="sxs-lookup"><span data-stu-id="60565-216">hello following 2 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="60565-217">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="60565-217">Child elements</span></span>
| <span data-ttu-id="60565-218">Имя</span><span class="sxs-lookup"><span data-stu-id="60565-218">Name</span></span> | <span data-ttu-id="60565-219">Тип</span><span class="sxs-lookup"><span data-stu-id="60565-219">Type</span></span> | <span data-ttu-id="60565-220">Описание</span><span class="sxs-lookup"><span data-stu-id="60565-220">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60565-221">**Disposition**</span><span class="sxs-lookup"><span data-stu-id="60565-221">**Disposition**</span></span><br /><br /> <span data-ttu-id="60565-222">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="60565-222">minOccurs="0" maxOccurs="1"</span></span> |[<span data-ttu-id="60565-223">StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="60565-223">StreamDispositionType</span></span>](media-services-input-metadata-schema.md#StreamDispositionType) |<span data-ttu-id="60565-224">Содержит сведения о презентации (например, указывает, предназначена ли конкретная звуковая дорожка для людей с нарушениями зрения).</span><span class="sxs-lookup"><span data-stu-id="60565-224">Contains presentation information (for example, whether a particular audio track is for visually impaired viewers).</span></span> |
| <span data-ttu-id="60565-225">**Metadata**</span><span class="sxs-lookup"><span data-stu-id="60565-225">**Metadata**</span></span><br /><br /> <span data-ttu-id="60565-226">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="60565-226">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="60565-227">MetadataType</span><span class="sxs-lookup"><span data-stu-id="60565-227">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="60565-228">Строки универсальных ключей и значений, которые можно использовать toohold различные сведения.</span><span class="sxs-lookup"><span data-stu-id="60565-228">Generic key/value strings that can be used toohold a variety of information.</span></span> <span data-ttu-id="60565-229">Например, key="language" и value="eng".</span><span class="sxs-lookup"><span data-stu-id="60565-229">For example, key=”language”, and value=”eng”.</span></span> |

## <span data-ttu-id="60565-230"><a name="AudioTrackType"></a> AudioTrackType (наследуется из TrackType)</span><span class="sxs-lookup"><span data-stu-id="60565-230"><a name="AudioTrackType"></a> AudioTrackType (inherits from TrackType)</span></span>
 <span data-ttu-id="60565-231">**AudioTrackType** — это глобальный сложный тип, который наследуется из [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="60565-231">**AudioTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

 <span data-ttu-id="60565-232">Hello тип представляет конкретную аудиодорожку в файле актива hello.</span><span class="sxs-lookup"><span data-stu-id="60565-232">hello type represents a specific audio track in hello asset file.</span></span>  

 <span data-ttu-id="60565-233">См. пример XML в конце этого раздела в hello: [пример XML-файла](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="60565-233">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="60565-234">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="60565-234">Attributes</span></span>
| <span data-ttu-id="60565-235">Имя</span><span class="sxs-lookup"><span data-stu-id="60565-235">Name</span></span> | <span data-ttu-id="60565-236">Тип</span><span class="sxs-lookup"><span data-stu-id="60565-236">Type</span></span> | <span data-ttu-id="60565-237">Описание</span><span class="sxs-lookup"><span data-stu-id="60565-237">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60565-238">**SampleFormat**</span><span class="sxs-lookup"><span data-stu-id="60565-238">**SampleFormat**</span></span> |<span data-ttu-id="60565-239">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="60565-239">**xs:string**</span></span> |<span data-ttu-id="60565-240">Формат выборки.</span><span class="sxs-lookup"><span data-stu-id="60565-240">Sample format.</span></span> |
| <span data-ttu-id="60565-241">**ChannelLayout**</span><span class="sxs-lookup"><span data-stu-id="60565-241">**ChannelLayout**</span></span> |<span data-ttu-id="60565-242">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="60565-242">**xs:string**</span></span> |<span data-ttu-id="60565-243">Структура канала.</span><span class="sxs-lookup"><span data-stu-id="60565-243">Channel layout.</span></span> |
| <span data-ttu-id="60565-244">**Channels**</span><span class="sxs-lookup"><span data-stu-id="60565-244">**Channels**</span></span><br /><br /> <span data-ttu-id="60565-245">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-245">Required</span></span> |<span data-ttu-id="60565-246">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-246">**xs:int**</span></span> |<span data-ttu-id="60565-247">Количество (0 или более) аудиоканалов.</span><span class="sxs-lookup"><span data-stu-id="60565-247">Number (0 or more) of audio channels.</span></span> |
| <span data-ttu-id="60565-248">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="60565-248">**SamplingRate**</span></span><br /><br /> <span data-ttu-id="60565-249">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-249">Required</span></span> |<span data-ttu-id="60565-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-250">**xs:int**</span></span> |<span data-ttu-id="60565-251">Частота аудиовыборки: выборок/с или Гц.</span><span class="sxs-lookup"><span data-stu-id="60565-251">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="60565-252">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="60565-252">**Bitrate**</span></span> |<span data-ttu-id="60565-253">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-253">**xs:int**</span></span> |<span data-ttu-id="60565-254">Средняя скорость аудиопотока в битах в секунду, вычисленная из файла актива hello.</span><span class="sxs-lookup"><span data-stu-id="60565-254">Average audio bit rate in bits per second, as calculated from hello asset file.</span></span> <span data-ttu-id="60565-255">Подсчитываются только полезные данные элементарного потока hello и затрат на упаковку hello не относится к этой категории.</span><span class="sxs-lookup"><span data-stu-id="60565-255">Only hello elementary stream payload is counted, and hello packaging overhead is not included in this count.</span></span> |
| <span data-ttu-id="60565-256">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="60565-256">**BitsPerSample**</span></span> |<span data-ttu-id="60565-257">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-257">**xs:int**</span></span> |<span data-ttu-id="60565-258">Введите бит на компонент wFormatTag формата hello.</span><span class="sxs-lookup"><span data-stu-id="60565-258">Bits per sample for hello wFormatTag format type.</span></span> |

## <span data-ttu-id="60565-259"><a name="VideoTrackType"></a> VideoTrackType (наследуется из TrackType)</span><span class="sxs-lookup"><span data-stu-id="60565-259"><a name="VideoTrackType"></a> VideoTrackType (inherits from TrackType)</span></span>
<span data-ttu-id="60565-260">**VideoTrackType** — это глобальный сложный тип, который наследуется из [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="60565-260">**VideoTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

<span data-ttu-id="60565-261">Hello тип представляет конкретную видеодорожку в файле актива hello.</span><span class="sxs-lookup"><span data-stu-id="60565-261">hello type represents a specific video track in hello asset file.</span></span>  

<span data-ttu-id="60565-262">См. пример XML в конце этого раздела в hello: [пример XML-файла](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="60565-262">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="60565-263">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="60565-263">Attributes</span></span>
| <span data-ttu-id="60565-264">Имя</span><span class="sxs-lookup"><span data-stu-id="60565-264">Name</span></span> | <span data-ttu-id="60565-265">Тип</span><span class="sxs-lookup"><span data-stu-id="60565-265">Type</span></span> | <span data-ttu-id="60565-266">Описание</span><span class="sxs-lookup"><span data-stu-id="60565-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60565-267">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="60565-267">**FourCC**</span></span><br /><br /> <span data-ttu-id="60565-268">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-268">Required</span></span> |<span data-ttu-id="60565-269">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="60565-269">**xs:string**</span></span> |<span data-ttu-id="60565-270">Код FourCC видеокодека.</span><span class="sxs-lookup"><span data-stu-id="60565-270">Video codec FourCC code.</span></span> |
| <span data-ttu-id="60565-271">**Профиль**</span><span class="sxs-lookup"><span data-stu-id="60565-271">**Profile**</span></span> |<span data-ttu-id="60565-272">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="60565-272">**xs:string**</span></span> |<span data-ttu-id="60565-273">Профиль видеодорожки.</span><span class="sxs-lookup"><span data-stu-id="60565-273">Video track's profile.</span></span> |
| <span data-ttu-id="60565-274">**Level**</span><span class="sxs-lookup"><span data-stu-id="60565-274">**Level**</span></span> |<span data-ttu-id="60565-275">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="60565-275">**xs:string**</span></span> |<span data-ttu-id="60565-276">Уровень видеодорожки.</span><span class="sxs-lookup"><span data-stu-id="60565-276">Video track's level.</span></span> |
| <span data-ttu-id="60565-277">**PixelFormat**</span><span class="sxs-lookup"><span data-stu-id="60565-277">**PixelFormat**</span></span> |<span data-ttu-id="60565-278">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="60565-278">**xs:string**</span></span> |<span data-ttu-id="60565-279">Формат пикселей видеодорожки.</span><span class="sxs-lookup"><span data-stu-id="60565-279">Video track's pixel format.</span></span> |
| <span data-ttu-id="60565-280">**Width**</span><span class="sxs-lookup"><span data-stu-id="60565-280">**Width**</span></span><br /><br /> <span data-ttu-id="60565-281">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-281">Required</span></span> |<span data-ttu-id="60565-282">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-282">**xs:int**</span></span> |<span data-ttu-id="60565-283">Ширина закодированного видео в пикселях.</span><span class="sxs-lookup"><span data-stu-id="60565-283">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="60565-284">**Height**</span><span class="sxs-lookup"><span data-stu-id="60565-284">**Height**</span></span><br /><br /> <span data-ttu-id="60565-285">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-285">Required</span></span> |<span data-ttu-id="60565-286">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-286">**xs:int**</span></span> |<span data-ttu-id="60565-287">Высота закодированного видео в пикселях.</span><span class="sxs-lookup"><span data-stu-id="60565-287">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="60565-288">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="60565-288">**DisplayAspectRatioNumerator**</span></span><br /><br /> <span data-ttu-id="60565-289">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-289">Required</span></span> |<span data-ttu-id="60565-290">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="60565-290">**xs:double**</span></span> |<span data-ttu-id="60565-291">Числитель пропорции отображения видео.</span><span class="sxs-lookup"><span data-stu-id="60565-291">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="60565-292">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="60565-292">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="60565-293">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-293">Required</span></span> |<span data-ttu-id="60565-294">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="60565-294">**xs:double**</span></span> |<span data-ttu-id="60565-295">Знаменатель пропорции отображения видео.</span><span class="sxs-lookup"><span data-stu-id="60565-295">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="60565-296">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="60565-296">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="60565-297">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-297">Required</span></span> |<span data-ttu-id="60565-298">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="60565-298">**xs:double**</span></span> |<span data-ttu-id="60565-299">Числитель пропорции выборки видео.</span><span class="sxs-lookup"><span data-stu-id="60565-299">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="60565-300">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="60565-300">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="60565-301">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="60565-301">**xs:double**</span></span> |<span data-ttu-id="60565-302">Числитель пропорции выборки видео.</span><span class="sxs-lookup"><span data-stu-id="60565-302">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="60565-303">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="60565-303">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="60565-304">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="60565-304">**xs:double**</span></span> |<span data-ttu-id="60565-305">Знаменатель пропорции выборки видео.</span><span class="sxs-lookup"><span data-stu-id="60565-305">Video sample aspect ratio denominator.</span></span> |
| <span data-ttu-id="60565-306">**FrameRate**</span><span class="sxs-lookup"><span data-stu-id="60565-306">**FrameRate**</span></span><br /><br /> <span data-ttu-id="60565-307">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-307">Required</span></span> |<span data-ttu-id="60565-308">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="60565-308">**xs:decimal**</span></span> |<span data-ttu-id="60565-309">Измеренная частота видеокадров в формате 3F.</span><span class="sxs-lookup"><span data-stu-id="60565-309">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="60565-310">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="60565-310">**Bitrate**</span></span> |<span data-ttu-id="60565-311">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-311">**xs:int**</span></span> |<span data-ttu-id="60565-312">Средняя скорость видеопотока в килобитах в секунду, вычисленная из файла актива hello.</span><span class="sxs-lookup"><span data-stu-id="60565-312">Average video bit rate in kilobits per second, as calculated from hello asset file.</span></span> <span data-ttu-id="60565-313">Подсчитываются только полезные данные элементарного потока hello и затрат на упаковку hello не включено.</span><span class="sxs-lookup"><span data-stu-id="60565-313">Only hello elementary stream payload is counted, and hello packaging overhead is not included.</span></span> |
| <span data-ttu-id="60565-314">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="60565-314">**MaxGOPBitrate**</span></span> |<span data-ttu-id="60565-315">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-315">**xs:int**</span></span> |<span data-ttu-id="60565-316">Максимальная средняя скорость группы изображений (GOP) для данной видеодорожки в килобитах в секунду.</span><span class="sxs-lookup"><span data-stu-id="60565-316">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |
| <span data-ttu-id="60565-317">**HasBFrames**</span><span class="sxs-lookup"><span data-stu-id="60565-317">**HasBFrames**</span></span> |<span data-ttu-id="60565-318">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-318">**xs:int**</span></span> |<span data-ttu-id="60565-319">Количество видеодорожек с кадрами B.</span><span class="sxs-lookup"><span data-stu-id="60565-319">Video track number of B frames.</span></span> |

## <span data-ttu-id="60565-320"><a name="MetadataType"></a> MetadataType</span><span class="sxs-lookup"><span data-stu-id="60565-320"><a name="MetadataType"></a> MetadataType</span></span>
<span data-ttu-id="60565-321">**MetadataType** — глобальный сложный тип, описывающий метаданные файла ресурса-контейнера в виде строк "ключ —значение".</span><span class="sxs-lookup"><span data-stu-id="60565-321">**MetadataType** is a global complex type that describes metadata of an asset file as key/value strings.</span></span> <span data-ttu-id="60565-322">Например, key="language" и value="eng".</span><span class="sxs-lookup"><span data-stu-id="60565-322">For example, key=”language”, and value=”eng”.</span></span>  

<span data-ttu-id="60565-323">См. пример XML в конце этого раздела в hello: [пример XML-файла](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="60565-323">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="60565-324">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="60565-324">Attributes</span></span>
| <span data-ttu-id="60565-325">Имя</span><span class="sxs-lookup"><span data-stu-id="60565-325">Name</span></span> | <span data-ttu-id="60565-326">Тип</span><span class="sxs-lookup"><span data-stu-id="60565-326">Type</span></span> | <span data-ttu-id="60565-327">Описание</span><span class="sxs-lookup"><span data-stu-id="60565-327">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60565-328">**key**</span><span class="sxs-lookup"><span data-stu-id="60565-328">**key**</span></span><br /><br /> <span data-ttu-id="60565-329">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-329">Required</span></span> |<span data-ttu-id="60565-330">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="60565-330">**xs:string**</span></span> |<span data-ttu-id="60565-331">Hello ключ в паре ключ/значение hello.</span><span class="sxs-lookup"><span data-stu-id="60565-331">hello key in hello key/value pair.</span></span> |
| <span data-ttu-id="60565-332">**значение**</span><span class="sxs-lookup"><span data-stu-id="60565-332">**value**</span></span><br /><br /> <span data-ttu-id="60565-333">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-333">Required</span></span> |<span data-ttu-id="60565-334">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="60565-334">**xs:string**</span></span> |<span data-ttu-id="60565-335">значение Hello в hello пара ключ значение.</span><span class="sxs-lookup"><span data-stu-id="60565-335">hello value in hello key/value pair.</span></span> |

## <span data-ttu-id="60565-336"><a name="ProgramType"></a> ProgramType</span><span class="sxs-lookup"><span data-stu-id="60565-336"><a name="ProgramType"></a> ProgramType</span></span>
<span data-ttu-id="60565-337">**ProgramType** — глобальный сложный тип, описывающий программу.</span><span class="sxs-lookup"><span data-stu-id="60565-337">**ProgramType** is a global complex type that describes a program.</span></span>  

### <a name="attributes"></a><span data-ttu-id="60565-338">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="60565-338">Attributes</span></span>
| <span data-ttu-id="60565-339">Имя</span><span class="sxs-lookup"><span data-stu-id="60565-339">Name</span></span> | <span data-ttu-id="60565-340">Тип</span><span class="sxs-lookup"><span data-stu-id="60565-340">Type</span></span> | <span data-ttu-id="60565-341">Описание</span><span class="sxs-lookup"><span data-stu-id="60565-341">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60565-342">**ProgramId**</span><span class="sxs-lookup"><span data-stu-id="60565-342">**ProgramId**</span></span><br /><br /> <span data-ttu-id="60565-343">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-343">Required</span></span> |<span data-ttu-id="60565-344">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-344">**xs:int**</span></span> |<span data-ttu-id="60565-345">Идентификатор программы</span><span class="sxs-lookup"><span data-stu-id="60565-345">Program Id</span></span> |
| <span data-ttu-id="60565-346">**NumberOfPrograms**</span><span class="sxs-lookup"><span data-stu-id="60565-346">**NumberOfPrograms**</span></span><br /><br /> <span data-ttu-id="60565-347">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-347">Required</span></span> |<span data-ttu-id="60565-348">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-348">**xs:int**</span></span> |<span data-ttu-id="60565-349">Количество программ.</span><span class="sxs-lookup"><span data-stu-id="60565-349">Number of programs.</span></span> |
| <span data-ttu-id="60565-350">**PmtPid**</span><span class="sxs-lookup"><span data-stu-id="60565-350">**PmtPid**</span></span><br /><br /> <span data-ttu-id="60565-351">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-351">Required</span></span> |<span data-ttu-id="60565-352">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-352">**xs:int**</span></span> |<span data-ttu-id="60565-353">Таблицы сопоставления программ (PMT) содержат сведения о программах.</span><span class="sxs-lookup"><span data-stu-id="60565-353">Program Map Tables (PMTs) contain information about programs.</span></span>  <span data-ttu-id="60565-354">Дополнительные сведения см. в разделе [PMT](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span><span class="sxs-lookup"><span data-stu-id="60565-354">For more information, see [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span></span> |
| <span data-ttu-id="60565-355">**PcrPid**</span><span class="sxs-lookup"><span data-stu-id="60565-355">**PcrPid**</span></span><br /><br /> <span data-ttu-id="60565-356">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-356">Required</span></span> |<span data-ttu-id="60565-357">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-357">**xs:int**</span></span> |<span data-ttu-id="60565-358">Используется декодером.</span><span class="sxs-lookup"><span data-stu-id="60565-358">Used by decoder.</span></span> <span data-ttu-id="60565-359">Дополнительные сведения см. в разделе [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR).</span><span class="sxs-lookup"><span data-stu-id="60565-359">For more information, see [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span></span> |
| <span data-ttu-id="60565-360">**StartPTS**</span><span class="sxs-lookup"><span data-stu-id="60565-360">**StartPTS**</span></span> |<span data-ttu-id="60565-361">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="60565-361">**xs: long**</span></span> |<span data-ttu-id="60565-362">Метка времени начала презентации.</span><span class="sxs-lookup"><span data-stu-id="60565-362">Starting presentation time stamp.</span></span> |
| <span data-ttu-id="60565-363">**EndPTS**</span><span class="sxs-lookup"><span data-stu-id="60565-363">**EndPTS**</span></span> |<span data-ttu-id="60565-364">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="60565-364">**xs: long**</span></span> |<span data-ttu-id="60565-365">Метка времени окончания презентации.</span><span class="sxs-lookup"><span data-stu-id="60565-365">Ending presentation time stamp.</span></span> |

## <span data-ttu-id="60565-366"><a name="StreamDispositionType"></a> StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="60565-366"><a name="StreamDispositionType"></a> StreamDispositionType</span></span>
<span data-ttu-id="60565-367">**StreamDispositionType** — глобальный сложный тип, описывающий поток hello.</span><span class="sxs-lookup"><span data-stu-id="60565-367">**StreamDispositionType** is a global complex type that describes hello stream.</span></span>  

<span data-ttu-id="60565-368">См. пример XML в конце этого раздела в hello: [пример XML-файла](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="60565-368">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="60565-369">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="60565-369">Attributes</span></span>
| <span data-ttu-id="60565-370">Имя</span><span class="sxs-lookup"><span data-stu-id="60565-370">Name</span></span> | <span data-ttu-id="60565-371">Тип</span><span class="sxs-lookup"><span data-stu-id="60565-371">Type</span></span> | <span data-ttu-id="60565-372">Описание</span><span class="sxs-lookup"><span data-stu-id="60565-372">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60565-373">**По умолчанию**</span><span class="sxs-lookup"><span data-stu-id="60565-373">**Default**</span></span><br /><br /> <span data-ttu-id="60565-374">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-374">Required</span></span> |<span data-ttu-id="60565-375">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-375">**xs:int**</span></span> |<span data-ttu-id="60565-376">Задайте tooindicate too1 этот атрибут, это представление по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="60565-376">Set this attribute too1 tooindicate this is hello default presentation.</span></span> |
| <span data-ttu-id="60565-377">**Dub**</span><span class="sxs-lookup"><span data-stu-id="60565-377">**Dub**</span></span><br /><br /> <span data-ttu-id="60565-378">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-378">Required</span></span> |<span data-ttu-id="60565-379">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-379">**xs:int**</span></span> |<span data-ttu-id="60565-380">Задайте этот атрибут too1 tooindicate hello дублированных презентации.</span><span class="sxs-lookup"><span data-stu-id="60565-380">Set this attribute too1 tooindicate this is hello dubbed presentation.</span></span> |
| <span data-ttu-id="60565-381">**Original**</span><span class="sxs-lookup"><span data-stu-id="60565-381">**Original**</span></span><br /><br /> <span data-ttu-id="60565-382">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-382">Required</span></span> |<span data-ttu-id="60565-383">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-383">**xs:int**</span></span> |<span data-ttu-id="60565-384">Задайте этот атрибут tooindicate too1, возможно, Исходная презентация hello.</span><span class="sxs-lookup"><span data-stu-id="60565-384">Set this attribute too1 tooindicate this is hello original presentation.</span></span> |
| <span data-ttu-id="60565-385">**Comment**</span><span class="sxs-lookup"><span data-stu-id="60565-385">**Comment**</span></span><br /><br /> <span data-ttu-id="60565-386">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-386">Required</span></span> |<span data-ttu-id="60565-387">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-387">**xs:int**</span></span> |<span data-ttu-id="60565-388">Задайте этот атрибут too1 tooindicate дорожка содержит дикторский текст.</span><span class="sxs-lookup"><span data-stu-id="60565-388">Set this attribute too1 tooindicate this track contains commentary.</span></span> |
| <span data-ttu-id="60565-389">**Lyrics**</span><span class="sxs-lookup"><span data-stu-id="60565-389">**Lyrics**</span></span><br /><br /> <span data-ttu-id="60565-390">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-390">Required</span></span> |<span data-ttu-id="60565-391">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-391">**xs:int**</span></span> |<span data-ttu-id="60565-392">Задайте этот атрибут too1 tooindicate дорожка содержит лирику, установите.</span><span class="sxs-lookup"><span data-stu-id="60565-392">Set this attribute too1 tooindicate this track contains lyrics.</span></span> |
| <span data-ttu-id="60565-393">**Karaoke**</span><span class="sxs-lookup"><span data-stu-id="60565-393">**Karaoke**</span></span><br /><br /> <span data-ttu-id="60565-394">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-394">Required</span></span> |<span data-ttu-id="60565-395">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-395">**xs:int**</span></span> |<span data-ttu-id="60565-396">Задайте этот атрибут too1 tooindicate представляет hello отслеживания караоке (музыкальное сопровождение, без вокала).</span><span class="sxs-lookup"><span data-stu-id="60565-396">Set this attribute too1 tooindicate this represents hello karaoke track (background music, no vocals).</span></span> |
| <span data-ttu-id="60565-397">**Forced**</span><span class="sxs-lookup"><span data-stu-id="60565-397">**Forced**</span></span><br /><br /> <span data-ttu-id="60565-398">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-398">Required</span></span> |<span data-ttu-id="60565-399">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-399">**xs:int**</span></span> |<span data-ttu-id="60565-400">Задайте tooindicate too1 этот атрибут, это является hello принудительно презентацию.</span><span class="sxs-lookup"><span data-stu-id="60565-400">Set this attribute too1 tooindicate this is hello forced presentation.</span></span> |
| <span data-ttu-id="60565-401">**HearingImpaired**</span><span class="sxs-lookup"><span data-stu-id="60565-401">**HearingImpaired**</span></span><br /><br /> <span data-ttu-id="60565-402">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-402">Required</span></span> |<span data-ttu-id="60565-403">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-403">**xs:int**</span></span> |<span data-ttu-id="60565-404">Задайте этот атрибут tooindicate too1, — это дорожка для слабослышащих hello.</span><span class="sxs-lookup"><span data-stu-id="60565-404">Set this attribute too1 tooindicate this track is for hello hearing impaired.</span></span> |
| <span data-ttu-id="60565-405">**VisualImpaired**</span><span class="sxs-lookup"><span data-stu-id="60565-405">**VisualImpaired**</span></span><br /><br /> <span data-ttu-id="60565-406">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-406">Required</span></span> |<span data-ttu-id="60565-407">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-407">**xs:int**</span></span> |<span data-ttu-id="60565-408">Задайте этот атрибут tooindicate too1, этот курс предназначен для hello визуально с нарушениями.</span><span class="sxs-lookup"><span data-stu-id="60565-408">Set this attribute too1 tooindicate this track is for hello visually impaired.</span></span> |
| <span data-ttu-id="60565-409">**CleanEffects**</span><span class="sxs-lookup"><span data-stu-id="60565-409">**CleanEffects**</span></span><br /><br /> <span data-ttu-id="60565-410">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-410">Required</span></span> |<span data-ttu-id="60565-411">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-411">**xs:int**</span></span> |<span data-ttu-id="60565-412">Задайте этот атрибут tooindicate too1, которые эта дорожка содержит эффекты очистки.</span><span class="sxs-lookup"><span data-stu-id="60565-412">Set this attribute too1 tooindicate this track has clean effects.</span></span> |
| <span data-ttu-id="60565-413">**AttachedPic**</span><span class="sxs-lookup"><span data-stu-id="60565-413">**AttachedPic**</span></span><br /><br /> <span data-ttu-id="60565-414">Обязательно</span><span class="sxs-lookup"><span data-stu-id="60565-414">Required</span></span> |<span data-ttu-id="60565-415">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="60565-415">**xs:int**</span></span> |<span data-ttu-id="60565-416">Установка tooindicate too1 этот атрибут, который эта дорожка содержит изображений.</span><span class="sxs-lookup"><span data-stu-id="60565-416">Set this attribute too1 tooindicate this track has pictures.</span></span> |

## <span data-ttu-id="60565-417"><a name="Programs"></a> Элемент Programs</span><span class="sxs-lookup"><span data-stu-id="60565-417"><a name="Programs"></a> Programs element</span></span>
<span data-ttu-id="60565-418">Оболочечный элемент, содержащий несколько элементов **Program**.</span><span class="sxs-lookup"><span data-stu-id="60565-418">Wrapper element holding multiple **Program** elements.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="60565-419">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="60565-419">Child elements</span></span>
| <span data-ttu-id="60565-420">Имя</span><span class="sxs-lookup"><span data-stu-id="60565-420">Name</span></span> | <span data-ttu-id="60565-421">Тип</span><span class="sxs-lookup"><span data-stu-id="60565-421">Type</span></span> | <span data-ttu-id="60565-422">Описание</span><span class="sxs-lookup"><span data-stu-id="60565-422">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60565-423">**Program**</span><span class="sxs-lookup"><span data-stu-id="60565-423">**Program**</span></span><br /><br /> <span data-ttu-id="60565-424">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="60565-424">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="60565-425">ProgramType</span><span class="sxs-lookup"><span data-stu-id="60565-425">ProgramType</span></span>](media-services-input-metadata-schema.md#ProgramType) |<span data-ttu-id="60565-426">Для файлов активов, которые находятся в формате MPEG-TS содержит сведения о программах, в файл актива hello.</span><span class="sxs-lookup"><span data-stu-id="60565-426">For asset files that are in MPEG-TS format, contains information about programs in hello asset file.</span></span> |

## <span data-ttu-id="60565-427"><a name="VideoTracks"></a> Элемент VideoTracks</span><span class="sxs-lookup"><span data-stu-id="60565-427"><a name="VideoTracks"></a> VideoTracks element</span></span>
 <span data-ttu-id="60565-428">Оболочечный элемент, содержащий несколько элементов **VideoTrack**.</span><span class="sxs-lookup"><span data-stu-id="60565-428">Wrapper element holding multiple **VideoTrack** elements.</span></span>  

 <span data-ttu-id="60565-429">См. пример XML в конце этого раздела в hello: [пример XML-файла](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="60565-429">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="60565-430">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="60565-430">Child elements</span></span>
| <span data-ttu-id="60565-431">Имя</span><span class="sxs-lookup"><span data-stu-id="60565-431">Name</span></span> | <span data-ttu-id="60565-432">Тип</span><span class="sxs-lookup"><span data-stu-id="60565-432">Type</span></span> | <span data-ttu-id="60565-433">Описание</span><span class="sxs-lookup"><span data-stu-id="60565-433">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60565-434">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="60565-434">**VideoTrack**</span></span><br /><br /> <span data-ttu-id="60565-435">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="60565-435">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="60565-436">VideoTrackType (наследуется из TrackType)</span><span class="sxs-lookup"><span data-stu-id="60565-436">VideoTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#VideoTrackType) |<span data-ttu-id="60565-437">Содержит сведения о видеодорожках в файле актива hello.</span><span class="sxs-lookup"><span data-stu-id="60565-437">Contains information about video tracks in hello asset file.</span></span> |

## <span data-ttu-id="60565-438"><a name="AudioTracks"></a> Элемент AudioTracks</span><span class="sxs-lookup"><span data-stu-id="60565-438"><a name="AudioTracks"></a> AudioTracks element</span></span>
 <span data-ttu-id="60565-439">Оболочечный элемент, содержащий несколько элементов **AudioTrack**.</span><span class="sxs-lookup"><span data-stu-id="60565-439">Wrapper element holding multiple **AudioTrack** elements.</span></span>  

 <span data-ttu-id="60565-440">См. пример XML в конце этого раздела в hello: [пример XML-файла](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="60565-440">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="elements"></a><span data-ttu-id="60565-441">элементы</span><span class="sxs-lookup"><span data-stu-id="60565-441">elements</span></span>
| <span data-ttu-id="60565-442">Имя</span><span class="sxs-lookup"><span data-stu-id="60565-442">Name</span></span> | <span data-ttu-id="60565-443">Тип</span><span class="sxs-lookup"><span data-stu-id="60565-443">Type</span></span> | <span data-ttu-id="60565-444">Описание</span><span class="sxs-lookup"><span data-stu-id="60565-444">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60565-445">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="60565-445">**AudioTrack**</span></span><br /><br /> <span data-ttu-id="60565-446">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="60565-446">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="60565-447">AudioTrackType (наследуется из TrackType)</span><span class="sxs-lookup"><span data-stu-id="60565-447">AudioTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#AudioTrackType) |<span data-ttu-id="60565-448">Содержит сведения об аудиодорожках в файле актива hello.</span><span class="sxs-lookup"><span data-stu-id="60565-448">Contains information about audio tracks in hello asset file.</span></span> |

## <span data-ttu-id="60565-449"><a name="code"></a> Код схемы</span><span class="sxs-lookup"><span data-stu-id="60565-449"><a name="code"></a> Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.0"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               elementFormDefault="qualified">  

      <xs:complexType name="MetadataType">  
        <xs:attribute name="key"   type="xs:string" use="required"/>  
        <xs:attribute name="value" type="xs:string" use="required"/>  
      </xs:complexType>  

      <xs:complexType name="ProgramType">  
        <xs:attribute name="ProgramId" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Program Id</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfPrograms" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Number of programs</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PmtPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pmt pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PcrPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pcr pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="StartPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>start pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="EndPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>end pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="StreamDispositionType">  
        <xs:attribute name="Default"          type="xs:int" use="required" />  
        <xs:attribute name="Dub"              type="xs:int" use="required" />  
        <xs:attribute name="Original"         type="xs:int" use="required" />  
        <xs:attribute name="Comment"          type="xs:int" use="required" />  
        <xs:attribute name="Lyrics"           type="xs:int" use="required" />  
        <xs:attribute name="Karaoke"          type="xs:int" use="required" />  
        <xs:attribute name="Forced"           type="xs:int" use="required" />  
        <xs:attribute name="HearingImpaired"  type="xs:int" use="required" />  
        <xs:attribute name="VisualImpaired"   type="xs:int" use="required" />  
        <xs:attribute name="CleanEffects"     type="xs:int" use="required" />  
        <xs:attribute name="AttachedPic"      type="xs:int" use="required" />  
      </xs:complexType>  

      <xs:complexType name="TrackType" abstract="true">  
        <xs:sequence>  
          <xs:element name="Disposition" type="StreamDispositionType" minOccurs="0" maxOccurs="1"/>  
          <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded"/>  
        </xs:sequence>  
        <xs:attribute name="Id" use="required">  
          <xs:annotation>  
            <xs:documentation>zero-based index of this video track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="Codec" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec string</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="CodecLongName" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec long name</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="TimeBase"  type="xs:string" use="required">  
          <xs:annotation>  
            <xs:documentation>Time base. Example: TimeBase="1/48000"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfFrames">  
          <xs:annotation>  
            <xs:documentation>number of frames</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="StartTime" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track start time. Example: StartTime="PT2.669S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="Duration" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track duration. Example: Duration="PT25M37.757S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="VideoTrackType">  
        <xs:annotation>  
          <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="FourCC" type="xs:string" use="required">  
              <xs:annotation>  
                <xs:documentation>video codec FourCC code</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Profile" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>profile</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Level" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>level</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="PixelFormat" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>Video track's pixel format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Width" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video width in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Height" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video height in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioNumerator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioDenominator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioNumerator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioDenominator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="FrameRate" use="required">  
              <xs:annotation>  
                <xs:documentation>measured video frame rate in .3f format</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:decimal">  
                  <xs:minInclusive value="0"/>  
                  <xs:fractionDigits value="3"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="MaxGOPBitrate">  
              <xs:annotation>  
                <xs:documentation>Max GOP average bitrate for this video track, in kilobits per second</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="HasBFrames" type="xs:int">  
              <xs:annotation>  
                <xs:documentation>video track number of B frames</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:complexType name="AudioTrackType">  
        <xs:annotation>  
          <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="SampleFormat"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>sample format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="ChannelLayout"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>channel layout</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Channels" use="required">  
              <xs:annotation>  
                <xs:documentation>number of audio channels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SamplingRate" use="required">  
              <xs:annotation>  
                <xs:documentation>audio sampling rate in samples/sec or Hz</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for hello encoding job</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="AssetFile" minOccurs="1" maxOccurs="unbounded">  
              <xs:annotation>  
                <xs:documentation>asset file</xs:documentation>  
              </xs:annotation>  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="Programs" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>This is hello collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" type="AudioTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded" />  
                </xs:sequence>  
                <xs:attribute name="Name" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>hello media asset file name</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Size" use="required">  
                  <xs:annotation>  
                    <xs:documentation>size of file in bytes</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:long">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
                <xs:attribute name="Duration" type="xs:duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration. Example: Duration="PT25M37.757S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="NumberOfStreams" type="xs:int" use="required">  
                  <xs:annotation>  
                    <xs:documentation>number of streams in asset file</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatNames" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatVerboseName" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format verbose names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="StartTime" type="xs:duration">  
                  <xs:annotation>  
                    <xs:documentation>content start time. Example: StartTime="PT2.669S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="OverallBitRate">  
                  <xs:annotation>  
                    <xs:documentation>average bitrate of hello asset file in kbps</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:int">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  


## <span data-ttu-id="60565-450"><a name="xml"></a> Пример XML-файла</span><span class="sxs-lookup"><span data-stu-id="60565-450"><a name="xml"></a> XML example</span></span>
<span data-ttu-id="60565-451">Hello ниже приведен пример файла входных метаданных hello.</span><span class="sxs-lookup"><span data-stu-id="60565-451">hello following is an example of hello Input metadata file.</span></span>  

    <?xml version="1.0" encoding="utf-8"?>  
    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata">  
      <AssetFile Name="bear.mp4" Size="1973733" Duration="PT12.678S" NumberOfStreams="2" FormatNames="mov,mp4,m4a,3gp,3g2,mj2" FormatVerboseName="QuickTime / MOV" StartTime="PT0S" OverallBitRate="1245">  
        <VideoTracks>  
          <VideoTrack Id="1" Codec="h264" CodecLongName="H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10" TimeBase="1/29970" NumberOfFrames="375" StartTime="PT0.034S" Duration="PT12.645S" FourCC="avc1" Profile="High" Level="4.1" PixelFormat="yuv420p" Width="512" Height="384" DisplayAspectRatioNumerator="4" DisplayAspectRatioDenominator="3" SampleAspectRatioNumerator="1" SampleAspectRatioDenominator="1" FrameRate="29.656" Bitrate="1043" HasBFrames="1">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Video Media Handler" />  
          </VideoTrack>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="aac" CodecLongName="AAC (Advanced Audio Coding)" TimeBase="1/44100" NumberOfFrames="546" StartTime="PT0S" Duration="PT12.678S" SampleFormat="fltp" ChannelLayout="stereo" Channels="2" SamplingRate="44100" Bitrate="156" BitsPerSample="0">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Sound Media Handler" />  
          </AudioTrack>  
        </AudioTracks>  
        <Metadata key="major_brand" value="mp42" />  
        <Metadata key="minor_version" value="0" />  
        <Metadata key="compatible_brands" value="mp42mp41" />  
        <Metadata key="creation_time" value="2010-03-10 16:11:53" />  
        <Metadata key="comment" value="Courtesy of National Geographic.  Used by Permission." />  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a><span data-ttu-id="60565-452">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="60565-452">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="60565-453">Отзывы</span><span class="sxs-lookup"><span data-stu-id="60565-453">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

