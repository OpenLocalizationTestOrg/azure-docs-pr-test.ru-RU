---
title: "схем выходных метаданных aaaAzure Media Services | Документы Microsoft"
description: "Hello разделе приводится обзор схем выходных метаданных служб мультимедиа Azure."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 1ed84c88-eea5-4a24-9c4f-f2428157d08a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 7f07d6accbe0b171d0408b15d5e1e6b5afd6c367
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="output-metadata"></a><span data-ttu-id="b01df-103">Выходные метаданные</span><span class="sxs-lookup"><span data-stu-id="b01df-103">Output Metadata</span></span>
## <a name="overview"></a><span data-ttu-id="b01df-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="b01df-104">Overview</span></span>
<span data-ttu-id="b01df-105">Задание кодирования связано с входным активом (или активами) для которого необходимо tooperform некоторые задачи кодирования.</span><span class="sxs-lookup"><span data-stu-id="b01df-105">An encoding job is associated with an input asset (or assets) on which you want tooperform some encoding tasks.</span></span> <span data-ttu-id="b01df-106">Например, кодирование MP4 файл tooH.264 MP4 с адаптивной скоростью задает; Создание эскиза; Создание наложений.</span><span class="sxs-lookup"><span data-stu-id="b01df-106">For example, encode an MP4 file tooH.264 MP4 adaptive bitrate sets; create a thumbnail; create overlays.</span></span> <span data-ttu-id="b01df-107">После выполнения задачи создается выходной ресурс-контейнер.</span><span class="sxs-lookup"><span data-stu-id="b01df-107">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="b01df-108">Hello выходной актив содержит видеофайлы, аудиофайлы, эскизы, т. д. hello выходной актив содержит файл метаданных выходного актива hello.</span><span class="sxs-lookup"><span data-stu-id="b01df-108">hello output asset contains video, audio, thumbnails, etc. hello output asset also contains a file with metadata about hello output asset.</span></span> <span data-ttu-id="b01df-109">Hello hello метаданных XML-файлу имеет следующий формат hello: &lt;имя_исходного_файла&gt;_manifest.xml (например, BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="b01df-109">hello name of hello metadata XML file has hello following format: &lt;source_file_name&gt;_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span>  

<span data-ttu-id="b01df-110">Если требуется файл метаданных tooexamine hello, можно создать **SAS** обнаружения и загрузки hello файл tooyour локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="b01df-110">If you want tooexamine hello metadata file, you can create a **SAS** locator and download hello file tooyour local computer.</span></span>  

<span data-ttu-id="b01df-111">В этом разделе рассматривается hello элементы и типы XML-схемы hello на какие метаданными вывода hello (&lt;имя_исходного_файла&gt;_manifest.xml) основана.</span><span class="sxs-lookup"><span data-stu-id="b01df-111">This topic discusses hello elements and types of hello XML schema on which hello output metada (&lt;source_file_name&gt;_manifest.xml) is based.</span></span> <span data-ttu-id="b01df-112">Сведения о файле hello, который содержит метаданные о входном активе hello. в разделе [входных метаданных](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="b01df-112">For information about hello file that contains metadata about hello input asset, see [Input Metadata](media-services-input-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="b01df-113">Можно найти полную схему кода hello и пример XML-файла в конце hello в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="b01df-113">You can find hello complete schema code and XML example at hello end of this topic.</span></span>  
>
>

## <span data-ttu-id="b01df-114"><a name="AssetFiles "></a> Корневой элемент AssetFiles</span><span class="sxs-lookup"><span data-stu-id="b01df-114"><a name="AssetFiles "></a> AssetFiles root element</span></span>
<span data-ttu-id="b01df-115">Коллекция записей AssetFile для задания кодирования hello.</span><span class="sxs-lookup"><span data-stu-id="b01df-115">Collection of AssetFile entries for hello encoding job.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="b01df-116">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="b01df-116">Child elements</span></span>
| <span data-ttu-id="b01df-117">Имя</span><span class="sxs-lookup"><span data-stu-id="b01df-117">Name</span></span> | <span data-ttu-id="b01df-118">Описание</span><span class="sxs-lookup"><span data-stu-id="b01df-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b01df-119">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="b01df-119">**AssetFile**</span></span><br/><br/> <span data-ttu-id="b01df-120">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="b01df-120">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="b01df-121">[Элемент AssetFile](media-services-output-metadata-schema.md) , являющийся частью коллекции AssetFiles hello.</span><span class="sxs-lookup"><span data-stu-id="b01df-121">An [AssetFile element](media-services-output-metadata-schema.md) that is part of hello AssetFiles collection.</span></span> |

## <span data-ttu-id="b01df-122"><a name="AssetFile "></a> Элемент AssetFile</span><span class="sxs-lookup"><span data-stu-id="b01df-122"><a name="AssetFile "></a> AssetFile element</span></span>
<span data-ttu-id="b01df-123">Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="b01df-123">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="b01df-124">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="b01df-124">Attributes</span></span>
| <span data-ttu-id="b01df-125">Имя</span><span class="sxs-lookup"><span data-stu-id="b01df-125">Name</span></span> | <span data-ttu-id="b01df-126">Тип</span><span class="sxs-lookup"><span data-stu-id="b01df-126">Type</span></span> | <span data-ttu-id="b01df-127">Описание</span><span class="sxs-lookup"><span data-stu-id="b01df-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b01df-128">**Имя**</span><span class="sxs-lookup"><span data-stu-id="b01df-128">**Name**</span></span><br/><br/> <span data-ttu-id="b01df-129">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-129">Required</span></span> |<span data-ttu-id="b01df-130">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="b01df-130">**xs:string**</span></span> |<span data-ttu-id="b01df-131">Имя файла актива мультимедиа Hello.</span><span class="sxs-lookup"><span data-stu-id="b01df-131">hello media asset file name.</span></span> |
| <span data-ttu-id="b01df-132">**Размер**</span><span class="sxs-lookup"><span data-stu-id="b01df-132">**Size**</span></span><br/><br/> <span data-ttu-id="b01df-133">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="b01df-133">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="b01df-134">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-134">Required</span></span> |<span data-ttu-id="b01df-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="b01df-135">**xs:long**</span></span> |<span data-ttu-id="b01df-136">Размер файла актива hello в байтах.</span><span class="sxs-lookup"><span data-stu-id="b01df-136">Size of hello asset file in bytes.</span></span> |
| <span data-ttu-id="b01df-137">**Duration**</span><span class="sxs-lookup"><span data-stu-id="b01df-137">**Duration**</span></span><br/><br/> <span data-ttu-id="b01df-138">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-138">Required</span></span> |<span data-ttu-id="b01df-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="b01df-139">**xs:duration**</span></span> |<span data-ttu-id="b01df-140">Длительность воспроизведения содержимого.</span><span class="sxs-lookup"><span data-stu-id="b01df-140">Content play back duration.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="b01df-141">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="b01df-141">Child elements</span></span>
| <span data-ttu-id="b01df-142">Имя</span><span class="sxs-lookup"><span data-stu-id="b01df-142">Name</span></span> | <span data-ttu-id="b01df-143">Описание</span><span class="sxs-lookup"><span data-stu-id="b01df-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b01df-144">**Источники**</span><span class="sxs-lookup"><span data-stu-id="b01df-144">**Sources**</span></span> |<span data-ttu-id="b01df-145">Коллекция входных/исходных файлов мультимедиа, который был обработан в заказ tooproduce этого AssetFile.</span><span class="sxs-lookup"><span data-stu-id="b01df-145">Collection of input/source media files, that was processed in order tooproduce this AssetFile.</span></span> <span data-ttu-id="b01df-146">Дополнительные сведения см. в разделе [Элемент Source](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="b01df-146">For more information, see [Source element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="b01df-147">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="b01df-147">**VideoTracks**</span></span><br/><br/> <span data-ttu-id="b01df-148">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="b01df-148">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="b01df-149">Каждый физический файл ресурса-контейнера может содержать ноль или более видеодорожек, чередуемых в соответствующем формате ресурса-контейнера.</span><span class="sxs-lookup"><span data-stu-id="b01df-149">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="b01df-150">Это коллекция всех таких видеодорожек hello.</span><span class="sxs-lookup"><span data-stu-id="b01df-150">This is hello collection of all those video tracks.</span></span> <span data-ttu-id="b01df-151">Дополнительные сведения см. в разделе [Элемент VideoTracks](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="b01df-151">For more information, see [VideoTracks element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="b01df-152">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="b01df-152">**AudioTracks**</span></span><br/><br/> <span data-ttu-id="b01df-153">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="b01df-153">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="b01df-154">Каждый физический файл ресурса-контейнера может содержать ноль или более звуковых дорожек, чередуемых в соответствующем формате ресурса-контейнера.</span><span class="sxs-lookup"><span data-stu-id="b01df-154">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="b01df-155">Это коллекция всех таких аудиодорожек hello.</span><span class="sxs-lookup"><span data-stu-id="b01df-155">This is hello collection of all those audio tracks.</span></span> <span data-ttu-id="b01df-156">Дополнительные сведения см. в разделе [Элемент AudioTracks](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="b01df-156">For more information, see [AudioTracks element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="b01df-157"><a name="Sources "></a> Элемент Sources</span><span class="sxs-lookup"><span data-stu-id="b01df-157"><a name="Sources "></a> Sources element</span></span>
<span data-ttu-id="b01df-158">Коллекция входных/исходных файлов мультимедиа, который был обработан в заказ tooproduce этого AssetFile.</span><span class="sxs-lookup"><span data-stu-id="b01df-158">Collection of input/source media files, that was processed in order tooproduce this AssetFile.</span></span>  

<span data-ttu-id="b01df-159">Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="b01df-159">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="b01df-160">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="b01df-160">Child elements</span></span>
| <span data-ttu-id="b01df-161">Имя</span><span class="sxs-lookup"><span data-stu-id="b01df-161">Name</span></span> | <span data-ttu-id="b01df-162">Описание</span><span class="sxs-lookup"><span data-stu-id="b01df-162">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b01df-163">**Источник**</span><span class="sxs-lookup"><span data-stu-id="b01df-163">**Source**</span></span><br/><br/> <span data-ttu-id="b01df-164">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="b01df-164">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="b01df-165">Входной или исходный файл, используемый при создании этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="b01df-165">An input/source file used when generating this asset.</span></span> <span data-ttu-id="b01df-166">Дополнительные сведения см. в разделе [Элемент Source](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="b01df-166">For more information see [Source element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="b01df-167"><a name="Source "></a> Элемент Source</span><span class="sxs-lookup"><span data-stu-id="b01df-167"><a name="Source "></a> Source element</span></span>
<span data-ttu-id="b01df-168">Входной или исходный файл, используемый при создании этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="b01df-168">An input/source file used when generating this asset.</span></span>  

<span data-ttu-id="b01df-169">Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="b01df-169">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="b01df-170">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="b01df-170">Attributes</span></span>
| <span data-ttu-id="b01df-171">Имя</span><span class="sxs-lookup"><span data-stu-id="b01df-171">Name</span></span> | <span data-ttu-id="b01df-172">Тип</span><span class="sxs-lookup"><span data-stu-id="b01df-172">Type</span></span> | <span data-ttu-id="b01df-173">Описание</span><span class="sxs-lookup"><span data-stu-id="b01df-173">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b01df-174">**Имя**</span><span class="sxs-lookup"><span data-stu-id="b01df-174">**Name**</span></span><br/><br/> <span data-ttu-id="b01df-175">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-175">Required</span></span> |<span data-ttu-id="b01df-176">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="b01df-176">**xs:string**</span></span> |<span data-ttu-id="b01df-177">Имя входного исходного файла.</span><span class="sxs-lookup"><span data-stu-id="b01df-177">Input source file name.</span></span> |

## <span data-ttu-id="b01df-178"><a name="VideoTracks "></a> Элемент VideoTracks</span><span class="sxs-lookup"><span data-stu-id="b01df-178"><a name="VideoTracks "></a> VideoTracks element</span></span>
<span data-ttu-id="b01df-179">Каждый физический файл ресурса-контейнера может содержать ноль или более видеодорожек, чередуемых в соответствующем формате ресурса-контейнера.</span><span class="sxs-lookup"><span data-stu-id="b01df-179">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="b01df-180">Это коллекция всех таких видеодорожек hello.</span><span class="sxs-lookup"><span data-stu-id="b01df-180">This is hello collection of all those video tracks.</span></span>  

<span data-ttu-id="b01df-181">Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="b01df-181">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="b01df-182">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="b01df-182">Child elements</span></span>
| <span data-ttu-id="b01df-183">Имя</span><span class="sxs-lookup"><span data-stu-id="b01df-183">Name</span></span> | <span data-ttu-id="b01df-184">Описание</span><span class="sxs-lookup"><span data-stu-id="b01df-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b01df-185">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="b01df-185">**VideoTrack**</span></span><br/><br/> <span data-ttu-id="b01df-186">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="b01df-186">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="b01df-187">Конкретная Видеодорожка в родительском hello AssetFile.</span><span class="sxs-lookup"><span data-stu-id="b01df-187">A specific video track in hello parent AssetFile.</span></span> <span data-ttu-id="b01df-188">Дополнительные сведения см. в разделе [Элемент VideoTrack](media-services-output-metadata-schema.md#VideoTrack).</span><span class="sxs-lookup"><span data-stu-id="b01df-188">For more information, see [VideoTrack element](media-services-output-metadata-schema.md#VideoTrack).</span></span> |

## <span data-ttu-id="b01df-189"><a name="VideoTrack"></a> Элемент VideoTrack</span><span class="sxs-lookup"><span data-stu-id="b01df-189"><a name="VideoTrack"></a> VideoTrack element</span></span>
<span data-ttu-id="b01df-190">Конкретная Видеодорожка в родительском hello AssetFile.</span><span class="sxs-lookup"><span data-stu-id="b01df-190">A specific video track in hello parent AssetFile.</span></span>  

<span data-ttu-id="b01df-191">Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="b01df-191">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="b01df-192">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="b01df-192">Attributes</span></span>
| <span data-ttu-id="b01df-193">Имя</span><span class="sxs-lookup"><span data-stu-id="b01df-193">Name</span></span> | <span data-ttu-id="b01df-194">Тип</span><span class="sxs-lookup"><span data-stu-id="b01df-194">Type</span></span> | <span data-ttu-id="b01df-195">Описание</span><span class="sxs-lookup"><span data-stu-id="b01df-195">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b01df-196">**Id**</span><span class="sxs-lookup"><span data-stu-id="b01df-196">**Id**</span></span><br/><br/> <span data-ttu-id="b01df-197">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="b01df-197">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="b01df-198">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-198">Required</span></span> |<span data-ttu-id="b01df-199">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="b01df-199">**xs:int**</span></span> |<span data-ttu-id="b01df-200">Отсчитываемый от нуля индекс видеодорожки. **Примечание:** не обязательно hello trackid, который используется в MP4-файле.</span><span class="sxs-lookup"><span data-stu-id="b01df-200">Zero-based index of this video track. **Note:**  This is not necessarily hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="b01df-201">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="b01df-201">**FourCC**</span></span><br/><br/> <span data-ttu-id="b01df-202">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-202">Required</span></span> |<span data-ttu-id="b01df-203">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="b01df-203">**xs:string**</span></span> |<span data-ttu-id="b01df-204">Код FourCC видеокодека.</span><span class="sxs-lookup"><span data-stu-id="b01df-204">Video codec FourCC code.</span></span> |
| <span data-ttu-id="b01df-205">**Профиль**</span><span class="sxs-lookup"><span data-stu-id="b01df-205">**Profile**</span></span> |<span data-ttu-id="b01df-206">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="b01df-206">**xs:string**</span></span> |<span data-ttu-id="b01df-207">Профиль H264 (только кодека tooH264 применимо).</span><span class="sxs-lookup"><span data-stu-id="b01df-207">H264 profile (only applicable tooH264 codec).</span></span> |
| <span data-ttu-id="b01df-208">**Level**</span><span class="sxs-lookup"><span data-stu-id="b01df-208">**Level**</span></span> |<span data-ttu-id="b01df-209">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="b01df-209">**xs:string**</span></span> |<span data-ttu-id="b01df-210">Уровень H264 (только кодека tooH264 применимо).</span><span class="sxs-lookup"><span data-stu-id="b01df-210">H264 level (only applicable tooH264 codec).</span></span> |
| <span data-ttu-id="b01df-211">**Width**</span><span class="sxs-lookup"><span data-stu-id="b01df-211">**Width**</span></span><br/><br/> <span data-ttu-id="b01df-212">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="b01df-212">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="b01df-213">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-213">Required</span></span> |<span data-ttu-id="b01df-214">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="b01df-214">**xs:int**</span></span> |<span data-ttu-id="b01df-215">Ширина закодированного видео в пикселях.</span><span class="sxs-lookup"><span data-stu-id="b01df-215">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="b01df-216">**Height**</span><span class="sxs-lookup"><span data-stu-id="b01df-216">**Height**</span></span><br/><br/> <span data-ttu-id="b01df-217">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="b01df-217">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="b01df-218">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-218">Required</span></span> |<span data-ttu-id="b01df-219">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="b01df-219">**xs:int**</span></span> |<span data-ttu-id="b01df-220">Высота закодированного видео в пикселях.</span><span class="sxs-lookup"><span data-stu-id="b01df-220">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="b01df-221">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="b01df-221">**DisplayAspectRatioNumerator**</span></span><br/><br/> <span data-ttu-id="b01df-222">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="b01df-222">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="b01df-223">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-223">Required</span></span> |<span data-ttu-id="b01df-224">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="b01df-224">**xs:double**</span></span> |<span data-ttu-id="b01df-225">Числитель пропорции отображения видео.</span><span class="sxs-lookup"><span data-stu-id="b01df-225">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="b01df-226">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="b01df-226">**DisplayAspectRatioDenominator**</span></span><br/><br/> <span data-ttu-id="b01df-227">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="b01df-227">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="b01df-228">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-228">Required</span></span> |<span data-ttu-id="b01df-229">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="b01df-229">**xs:double**</span></span> |<span data-ttu-id="b01df-230">Знаменатель пропорции отображения видео.</span><span class="sxs-lookup"><span data-stu-id="b01df-230">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="b01df-231">**Framerate**</span><span class="sxs-lookup"><span data-stu-id="b01df-231">**Framerate**</span></span><br/><br/> <span data-ttu-id="b01df-232">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="b01df-232">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="b01df-233">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-233">Required</span></span> |<span data-ttu-id="b01df-234">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="b01df-234">**xs:decimal**</span></span> |<span data-ttu-id="b01df-235">Измеренная частота видеокадров в формате 3F.</span><span class="sxs-lookup"><span data-stu-id="b01df-235">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="b01df-236">**TargetFramerate**</span><span class="sxs-lookup"><span data-stu-id="b01df-236">**TargetFramerate**</span></span><br/><br/> <span data-ttu-id="b01df-237">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="b01df-237">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="b01df-238">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-238">Required</span></span> |<span data-ttu-id="b01df-239">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="b01df-239">**xs:decimal**</span></span> |<span data-ttu-id="b01df-240">Предустановленная частота кадров целевого видео в формате 3F.</span><span class="sxs-lookup"><span data-stu-id="b01df-240">Preset target video frame rate in .3f format.</span></span> |
| <span data-ttu-id="b01df-241">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="b01df-241">**Bitrate**</span></span><br/><br/> <span data-ttu-id="b01df-242">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="b01df-242">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="b01df-243">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-243">Required</span></span> |<span data-ttu-id="b01df-244">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="b01df-244">**xs:int**</span></span> |<span data-ttu-id="b01df-245">Средняя скорость видеопотока в килобитах в секунду, вычисленная из hello AssetFile.</span><span class="sxs-lookup"><span data-stu-id="b01df-245">Average video bit rate in kilobits per second, as calculated from hello AssetFile.</span></span> <span data-ttu-id="b01df-246">Подсчитывает только полезные данные элементарного потока hello и не включает hello затрат на упаковку.</span><span class="sxs-lookup"><span data-stu-id="b01df-246">Counts only hello elementary stream payload, and does not include hello packaging overhead.</span></span> |
| <span data-ttu-id="b01df-247">**TargetBitrate**</span><span class="sxs-lookup"><span data-stu-id="b01df-247">**TargetBitrate**</span></span><br/><br/> <span data-ttu-id="b01df-248">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="b01df-248">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="b01df-249">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-249">Required</span></span> |<span data-ttu-id="b01df-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="b01df-250">**xs:int**</span></span> |<span data-ttu-id="b01df-251">Целевая Средняя скорость для данной видеодорожки, запрошенная предустановкой кодирования Предустановка hello, в килобитах в секунду.</span><span class="sxs-lookup"><span data-stu-id="b01df-251">Target average bitrate for this video track, as requested via hello encoding preset, in kilobits per second.</span></span> |
| <span data-ttu-id="b01df-252">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="b01df-252">**MaxGOPBitrate**</span></span><br/><br/> <span data-ttu-id="b01df-253">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="b01df-253">minInclusive ="0"</span></span> |<span data-ttu-id="b01df-254">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="b01df-254">**xs:int**</span></span> |<span data-ttu-id="b01df-255">Максимальная средняя скорость группы изображений (GOP) для данной видеодорожки в килобитах в секунду.</span><span class="sxs-lookup"><span data-stu-id="b01df-255">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |

## <span data-ttu-id="b01df-256"><a name="AudioTracks "></a> Элемент AudioTracks</span><span class="sxs-lookup"><span data-stu-id="b01df-256"><a name="AudioTracks "></a> AudioTracks element</span></span>
<span data-ttu-id="b01df-257">Каждый физический файл ресурса-контейнера может содержать ноль или более звуковых дорожек, чередуемых в соответствующем формате ресурса-контейнера.</span><span class="sxs-lookup"><span data-stu-id="b01df-257">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="b01df-258">Это коллекция всех таких аудиодорожек hello.</span><span class="sxs-lookup"><span data-stu-id="b01df-258">This is hello collection of all those audio tracks.</span></span>  

<span data-ttu-id="b01df-259">Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="b01df-259">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="b01df-260">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="b01df-260">Child elements</span></span>
| <span data-ttu-id="b01df-261">Имя</span><span class="sxs-lookup"><span data-stu-id="b01df-261">Name</span></span> | <span data-ttu-id="b01df-262">Описание</span><span class="sxs-lookup"><span data-stu-id="b01df-262">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b01df-263">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="b01df-263">**AudioTrack**</span></span><br/><br/> <span data-ttu-id="b01df-264">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="b01df-264">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="b01df-265">Конкретная Аудиодорожка в родительском hello AssetFile.</span><span class="sxs-lookup"><span data-stu-id="b01df-265">A specific audio track in hello parent AssetFile.</span></span> <span data-ttu-id="b01df-266">Дополнительные сведения см. в разделе [Элемент AudioTrack](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="b01df-266">For more information, see [AudioTrack element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="b01df-267"><a name="AudioTrack "></a> Элемент AudioTrack</span><span class="sxs-lookup"><span data-stu-id="b01df-267"><a name="AudioTrack "></a> AudioTrack element</span></span>
<span data-ttu-id="b01df-268">Конкретная Аудиодорожка в родительском hello AssetFile.</span><span class="sxs-lookup"><span data-stu-id="b01df-268">A specific audio track in hello parent AssetFile.</span></span>  

<span data-ttu-id="b01df-269">Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="b01df-269">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="b01df-270">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="b01df-270">Attributes</span></span>
| <span data-ttu-id="b01df-271">Имя</span><span class="sxs-lookup"><span data-stu-id="b01df-271">Name</span></span> | <span data-ttu-id="b01df-272">Тип</span><span class="sxs-lookup"><span data-stu-id="b01df-272">Type</span></span> | <span data-ttu-id="b01df-273">Описание</span><span class="sxs-lookup"><span data-stu-id="b01df-273">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b01df-274">**Id**</span><span class="sxs-lookup"><span data-stu-id="b01df-274">**Id**</span></span><br/><br/> <span data-ttu-id="b01df-275">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="b01df-275">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="b01df-276">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-276">Required</span></span> |<span data-ttu-id="b01df-277">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="b01df-277">**xs:int**</span></span> |<span data-ttu-id="b01df-278">Отсчитываемый от нуля индекс звуковой дорожки. **Примечание:** не обязательно hello trackid, который используется в MP4-файле.</span><span class="sxs-lookup"><span data-stu-id="b01df-278">Zero-based index of this audio track. **Note:**  This is not necessarily hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="b01df-279">**Codec**</span><span class="sxs-lookup"><span data-stu-id="b01df-279">**Codec**</span></span> |<span data-ttu-id="b01df-280">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="b01df-280">**xs:string**</span></span> |<span data-ttu-id="b01df-281">Строка кодека звуковой дорожки.</span><span class="sxs-lookup"><span data-stu-id="b01df-281">Audio track codec string.</span></span> |
| <span data-ttu-id="b01df-282">**EncoderVersion**</span><span class="sxs-lookup"><span data-stu-id="b01df-282">**EncoderVersion**</span></span> |<span data-ttu-id="b01df-283">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="b01df-283">**xs:string**</span></span> |<span data-ttu-id="b01df-284">Дополнительная строка версии кодировщика, требуемая для EAC3.</span><span class="sxs-lookup"><span data-stu-id="b01df-284">Optional encoder version string, required for EAC3.</span></span> |
| <span data-ttu-id="b01df-285">**Channels**</span><span class="sxs-lookup"><span data-stu-id="b01df-285">**Channels**</span></span><br/><br/> <span data-ttu-id="b01df-286">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="b01df-286">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="b01df-287">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-287">Required</span></span> |<span data-ttu-id="b01df-288">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="b01df-288">**xs:int**</span></span> |<span data-ttu-id="b01df-289">Число аудиоканалов.</span><span class="sxs-lookup"><span data-stu-id="b01df-289">Number of audio channels.</span></span> |
| <span data-ttu-id="b01df-290">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="b01df-290">**SamplingRate**</span></span><br/><br/> <span data-ttu-id="b01df-291">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="b01df-291">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="b01df-292">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-292">Required</span></span> |<span data-ttu-id="b01df-293">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="b01df-293">**xs:int**</span></span> |<span data-ttu-id="b01df-294">Частота аудиовыборки: выборок/с или Гц.</span><span class="sxs-lookup"><span data-stu-id="b01df-294">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="b01df-295">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="b01df-295">**Bitrate**</span></span><br/><br/> <span data-ttu-id="b01df-296">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="b01df-296">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="b01df-297">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-297">Required</span></span> |<span data-ttu-id="b01df-298">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="b01df-298">**xs:int**</span></span> |<span data-ttu-id="b01df-299">Средняя скорость аудиопотока в битах в секунду, вычисленная из hello AssetFile.</span><span class="sxs-lookup"><span data-stu-id="b01df-299">Average audio bit rate in bits per second, as calculated from hello AssetFile.</span></span> <span data-ttu-id="b01df-300">Подсчитывает только полезные данные элементарного потока hello и не включает hello затрат на упаковку.</span><span class="sxs-lookup"><span data-stu-id="b01df-300">Counts only hello elementary stream payload, and does not include hello packaging overhead.</span></span> |
| <span data-ttu-id="b01df-301">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="b01df-301">**BitsPerSample**</span></span><br/><br/> <span data-ttu-id="b01df-302">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="b01df-302">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="b01df-303">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-303">Required</span></span> |<span data-ttu-id="b01df-304">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="b01df-304">**xs:int**</span></span> |<span data-ttu-id="b01df-305">Введите бит на компонент wFormatTag формата hello.</span><span class="sxs-lookup"><span data-stu-id="b01df-305">Bits per sample for hello wFormatTag format type.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="b01df-306">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="b01df-306">Child elements</span></span>
| <span data-ttu-id="b01df-307">Имя</span><span class="sxs-lookup"><span data-stu-id="b01df-307">Name</span></span> | <span data-ttu-id="b01df-308">Описание</span><span class="sxs-lookup"><span data-stu-id="b01df-308">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b01df-309">**LoudnessMeteringResultParameters**</span><span class="sxs-lookup"><span data-stu-id="b01df-309">**LoudnessMeteringResultParameters**</span></span><br/><br/> <span data-ttu-id="b01df-310">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="b01df-310">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="b01df-311">Параметры результата измерения громкости.</span><span class="sxs-lookup"><span data-stu-id="b01df-311">Loudness metering result parameters.</span></span> <span data-ttu-id="b01df-312">Дополнительные сведения см. в разделе [Элемент LoudnessMeteringResultParameter](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="b01df-312">For more information, see [LoudnessMeteringResultParameters element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="b01df-313"><a name="LoudnessMeteringResultParameters "></a> Элемент LoudnessMeteringResultParameters</span><span class="sxs-lookup"><span data-stu-id="b01df-313"><a name="LoudnessMeteringResultParameters "></a> LoudnessMeteringResultParameters element</span></span>
<span data-ttu-id="b01df-314">Параметры результата измерения громкости.</span><span class="sxs-lookup"><span data-stu-id="b01df-314">Loudness metering result parameters.</span></span>  

<span data-ttu-id="b01df-315">Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="b01df-315">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="b01df-316">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="b01df-316">Attributes</span></span>
| <span data-ttu-id="b01df-317">Имя</span><span class="sxs-lookup"><span data-stu-id="b01df-317">Name</span></span> | <span data-ttu-id="b01df-318">Тип</span><span class="sxs-lookup"><span data-stu-id="b01df-318">Type</span></span> | <span data-ttu-id="b01df-319">Описание</span><span class="sxs-lookup"><span data-stu-id="b01df-319">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b01df-320">**DPLMVersionInformation**</span><span class="sxs-lookup"><span data-stu-id="b01df-320">**DPLMVersionInformation**</span></span> |<span data-ttu-id="b01df-321">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="b01df-321">**xs:string**</span></span> |<span data-ttu-id="b01df-322">Версия комплекта разработчика **Dolby** Professional Loudness Metering (DPLM).</span><span class="sxs-lookup"><span data-stu-id="b01df-322">**Dolby** professional loudness metering development kit version.</span></span> |
| <span data-ttu-id="b01df-323">**DialogNormalization**</span><span class="sxs-lookup"><span data-stu-id="b01df-323">**DialogNormalization**</span></span><br/><br/> <span data-ttu-id="b01df-324">minInclusive="-31" maxInclusive="-1"</span><span class="sxs-lookup"><span data-stu-id="b01df-324">minInclusive="-31" maxInclusive="-1"</span></span><br/><br/> <span data-ttu-id="b01df-325">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-325">Required</span></span> |<span data-ttu-id="b01df-326">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="b01df-326">**xs:int**</span></span> |<span data-ttu-id="b01df-327">DialogNormalization, созданный с помощью DPLM, необходим при установке LoudnessMetering.</span><span class="sxs-lookup"><span data-stu-id="b01df-327">DialogNormalization generated through DPLM, required when LoudnessMetering is set</span></span> |
| <span data-ttu-id="b01df-328">**IntegratedLoudness**</span><span class="sxs-lookup"><span data-stu-id="b01df-328">**IntegratedLoudness**</span></span><br/><br/> <span data-ttu-id="b01df-329">minInclusive="-70" maxInclusive="10"</span><span class="sxs-lookup"><span data-stu-id="b01df-329">minInclusive="-70" maxInclusive="10"</span></span><br/><br/> <span data-ttu-id="b01df-330">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-330">Required</span></span> |<span data-ttu-id="b01df-331">**xs: float**</span><span class="sxs-lookup"><span data-stu-id="b01df-331">**xs:float**</span></span> |<span data-ttu-id="b01df-332">Интегрированная громкость</span><span class="sxs-lookup"><span data-stu-id="b01df-332">Integrated loudness</span></span> |
| <span data-ttu-id="b01df-333">**IntegratedLoudnessUnit**</span><span class="sxs-lookup"><span data-stu-id="b01df-333">**IntegratedLoudnessUnit**</span></span><br/><br/> <span data-ttu-id="b01df-334">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-334">Required</span></span> |<span data-ttu-id="b01df-335">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="b01df-335">**xs:string**</span></span> |<span data-ttu-id="b01df-336">Единица измерения интегрированной громкости.</span><span class="sxs-lookup"><span data-stu-id="b01df-336">Integrated loudness unit.</span></span> |
| <span data-ttu-id="b01df-337">**IntegratedLoudnessGatingMethod**</span><span class="sxs-lookup"><span data-stu-id="b01df-337">**IntegratedLoudnessGatingMethod**</span></span><br/><br/> <span data-ttu-id="b01df-338">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-338">Required</span></span> |<span data-ttu-id="b01df-339">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="b01df-339">**xs:string**</span></span> |<span data-ttu-id="b01df-340">Идентификатор стробирования</span><span class="sxs-lookup"><span data-stu-id="b01df-340">Gating identifier</span></span> |
| <span data-ttu-id="b01df-341">**IntegratedLoudnessSpeechPercentage**</span><span class="sxs-lookup"><span data-stu-id="b01df-341">**IntegratedLoudnessSpeechPercentage**</span></span><br/><br/> <span data-ttu-id="b01df-342">minInclusive ="0" maxInclusive="100"</span><span class="sxs-lookup"><span data-stu-id="b01df-342">minInclusive ="0" maxInclusive="100"</span></span> |<span data-ttu-id="b01df-343">**xs: float**</span><span class="sxs-lookup"><span data-stu-id="b01df-343">**xs:float**</span></span> |<span data-ttu-id="b01df-344">Речи hello программы, в процентах.</span><span class="sxs-lookup"><span data-stu-id="b01df-344">Speech content over hello program, as a percentage.</span></span> |
| <span data-ttu-id="b01df-345">**SamplePeak**</span><span class="sxs-lookup"><span data-stu-id="b01df-345">**SamplePeak**</span></span><br/><br/> <span data-ttu-id="b01df-346">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-346">Required</span></span> |<span data-ttu-id="b01df-347">**xs: float**</span><span class="sxs-lookup"><span data-stu-id="b01df-347">**xs:float**</span></span> |<span data-ttu-id="b01df-348">Пиковое абсолютное опорное значение в канале после сброса или последней очистки.</span><span class="sxs-lookup"><span data-stu-id="b01df-348">Peak absolute sample value, since reset or since it was last cleared, per channel.</span></span>  <span data-ttu-id="b01df-349">Единицы измерения — dBFS.</span><span class="sxs-lookup"><span data-stu-id="b01df-349">Units are dBFS.</span></span> |
| <span data-ttu-id="b01df-350">**SamplePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="b01df-350">**SamplePeakUnit**</span></span><br/><br/> <span data-ttu-id="b01df-351">fixed="dBFS"</span><span class="sxs-lookup"><span data-stu-id="b01df-351">fixed="dBFS"</span></span><br/><br/> <span data-ttu-id="b01df-352">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-352">Required</span></span> |<span data-ttu-id="b01df-353">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="b01df-353">**xs:anySimpleType**</span></span> |<span data-ttu-id="b01df-354">Единица измерения пикового опорного значения.</span><span class="sxs-lookup"><span data-stu-id="b01df-354">Sample peak unit.</span></span> |
| <span data-ttu-id="b01df-355">**TruePeak**</span><span class="sxs-lookup"><span data-stu-id="b01df-355">**TruePeak**</span></span><br/><br/> <span data-ttu-id="b01df-356">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-356">Required</span></span> |<span data-ttu-id="b01df-357">**xs: float**</span><span class="sxs-lookup"><span data-stu-id="b01df-357">**xs:float**</span></span> |<span data-ttu-id="b01df-358">Наибольшее абсолютное пиковое значение в канале, соответствующее ITU-R BS.1770-2, после сброса или последней очистки.</span><span class="sxs-lookup"><span data-stu-id="b01df-358">Maximum true peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.</span></span> <span data-ttu-id="b01df-359">Единицы измерения — dBTP.</span><span class="sxs-lookup"><span data-stu-id="b01df-359">Units are dBTP.</span></span> |
| <span data-ttu-id="b01df-360">**TruePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="b01df-360">**TruePeakUnit**</span></span><br/><br/> <span data-ttu-id="b01df-361">fixed="dBTP"</span><span class="sxs-lookup"><span data-stu-id="b01df-361">fixed="dBTP"</span></span><br/><br/> <span data-ttu-id="b01df-362">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b01df-362">Required</span></span> |<span data-ttu-id="b01df-363">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="b01df-363">**xs:anySimpleType**</span></span> |<span data-ttu-id="b01df-364">Единица измерения наибольшего абсолютного опорного значения.</span><span class="sxs-lookup"><span data-stu-id="b01df-364">True peak unit.</span></span> |

## <a name="schema-code"></a><span data-ttu-id="b01df-365">Код схемы</span><span class="sxs-lookup"><span data-stu-id="b01df-365">Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.2"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               elementFormDefault="qualified">  
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
                  <xs:element name="Sources">  
                    <xs:annotation>  
                      <xs:documentation>Collection of input/source media files, that was processed in order tooproduce this AssetFile</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Source" minOccurs="1" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>An input/source file used when generating this asset</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:attribute name="Name" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>input source file name</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
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
                            <xs:attribute name="FourCC" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>video codec FourCC code</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Profile" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 profile (only appliable for H264 codec)</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Level" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 level (only appliable for H264 codec)</xs:documentation>  
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
                            <xs:attribute name="Framerate" use="required">  
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
                            <xs:attribute name="TargetFramerate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>preset target video frame rate in .3f format</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:decimal">  
                                  <xs:minInclusive value="0"/>  
                                  <xs:fractionDigits value="3"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="TargetBitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>target average bitrate for this video track, as requested via hello encoding preset, in kilobits per second</xs:documentation>  
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
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:sequence>  
                              <xs:element name="LoudnessMeteringResultParameters" minOccurs="0" maxOccurs="1">  
                                <xs:annotation>  
                                  <xs:documentation>Loudness Metering Result Parameters</xs:documentation>  
                                </xs:annotation>  
                                <xs:complexType>  
                                  <xs:attribute name="DPLMVersionInformation" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Dolby Professional Loudness Metering Development Kit Version</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="DialogNormalization" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation> DialogNormalization generated through DPLM, required when LoudnessMetering is set</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:int">  
                                        <xs:minInclusive value="-31"/>  
                                        <xs:maxInclusive value="-1"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudness" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation>Integrated loudness</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="-70"/>  
                                        <xs:maxInclusive value="10"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessUnit" use="required" type="xs:string">  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessGatingMethod" use="required" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Gating identifier</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessSpeechPercentage">  
                                    <xs:annotation>  
                                      <xs:documentation>Speech content over hello program, as a percentage.</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="0"/>  
                                        <xs:maxInclusive value="100"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Peak absolute sample value, since reset or since it was last cleared, per channel.  Units are dBFS.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeakUnit" use="required" fixed="dBFS">  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Maximum True Peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.  Units are dBTP.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeakUnit" use="required" fixed="dBTP">  
                                  </xs:attribute>  
                                </xs:complexType>  
                              </xs:element>  
                            </xs:sequence>  
                            <xs:attribute name="Id" use="required">  
                              <xs:annotation>  
                                <xs:documentation>zero-based index of this audio track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Codec" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>audio track codec string</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="EncoderVersion" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>optional encoder version string, required for EAC3</xs:documentation>  
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
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="BitsPerSample" use="required">  
                              <xs:annotation>  
                                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
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
                <xs:attribute name="Duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:duration"/>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  



## <span data-ttu-id="b01df-366"><a name="xml"></a> Пример XML-файла</span><span class="sxs-lookup"><span data-stu-id="b01df-366"><a name="xml"></a> XML example</span></span>
 <span data-ttu-id="b01df-367">Hello ниже приведен пример hello выходного файла метаданных.</span><span class="sxs-lookup"><span data-stu-id="b01df-367">hello following is an example of hello Output metadata file.</span></span>  

    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
                xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata">  
      <AssetFile Name="BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4" Size="4646283" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.2" Width="1280" Height="720" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="4250" TargetBitrate="3400" MaxGOPBitrate="5514"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4" Size="3166728" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="2846" TargetBitrate="2250" MaxGOPBitrate="3630"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4" Size="2205095" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1932" TargetBitrate="1500" MaxGOPBitrate="2513"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4" Size="1508567" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1271" TargetBitrate="1000" MaxGOPBitrate="1527"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4" Size="1057155" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="843" TargetBitrate="650" MaxGOPBitrate="1086"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4" Size="699262" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="1.3" Width="320" Height="180" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="503" TargetBitrate="400" MaxGOPBitrate="661"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_96kbps.mp4" Size="166780" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_56kbps.mp4" Size="124576" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="53" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a><span data-ttu-id="b01df-368">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b01df-368">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b01df-369">Отзывы</span><span class="sxs-lookup"><span data-stu-id="b01df-369">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
