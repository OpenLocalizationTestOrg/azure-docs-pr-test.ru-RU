---
title: "Схема выходных метаданных служб мультимедиа Azure | Документация Майкрософт"
description: "Эта статья содержит обзор схемы выходных метаданных служб мультимедиа Azure."
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
ms.openlocfilehash: c175d359f93e7cd8cd73aa498ad8b71c4ec497f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="output-metadata"></a><span data-ttu-id="f5836-103">Выходные метаданные</span><span class="sxs-lookup"><span data-stu-id="f5836-103">Output Metadata</span></span>
## <a name="overview"></a><span data-ttu-id="f5836-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="f5836-104">Overview</span></span>
<span data-ttu-id="f5836-105">Задание кодирования связано с входным ресурсом-контейнером (или ресурсами-контейнерами), в котором нужно выполнить эти задачи.</span><span class="sxs-lookup"><span data-stu-id="f5836-105">An encoding job is associated with an input asset (or assets) on which you want to perform some encoding tasks.</span></span> <span data-ttu-id="f5836-106">Например, преобразуйте MP4-файл в набор мультискоростных MP4-файлов в формате H.264. Создайте эскиз и наложения.</span><span class="sxs-lookup"><span data-stu-id="f5836-106">For example, encode an MP4 file to H.264 MP4 adaptive bitrate sets; create a thumbnail; create overlays.</span></span> <span data-ttu-id="f5836-107">После выполнения задачи создается выходной ресурс-контейнер.</span><span class="sxs-lookup"><span data-stu-id="f5836-107">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="f5836-108">Он содержит видео- и аудиофайлы, эскизы и т. д. Выходной актив также содержит файл с метаданными выходного актива.</span><span class="sxs-lookup"><span data-stu-id="f5836-108">The output asset contains video, audio, thumbnails, etc. The output asset also contains a file with metadata about the output asset.</span></span> <span data-ttu-id="f5836-109">Имя XML-файла метаданных имеет следующий формат: &lt;имя_исходного_файла&gt;_manifest.xml (например, BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="f5836-109">The name of the metadata XML file has the following format: &lt;source_file_name&gt;_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span>  

<span data-ttu-id="f5836-110">Если вы хотите просмотреть файл метаданных, создайте указатель **SAS** и скачайте файл на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="f5836-110">If you want to examine the metadata file, you can create a **SAS** locator and download the file to your local computer.</span></span>  

<span data-ttu-id="f5836-111">В этой статье рассматриваются элементы и типы XML-схемы, на основе которой создаются выходные метаданные (&lt;имя_исходного_файла&gt;_metadata.xml).</span><span class="sxs-lookup"><span data-stu-id="f5836-111">This topic discusses the elements and types of the XML schema on which the output metada (&lt;source_file_name&gt;_manifest.xml) is based.</span></span> <span data-ttu-id="f5836-112">Сведения о файле, который содержит метаданные входного контейнера-ресурса, см. в статье [Input Metadata](media-services-input-metadata-schema.md) (Входные метаданные).</span><span class="sxs-lookup"><span data-stu-id="f5836-112">For information about the file that contains metadata about the input asset, see [Input Metadata](media-services-input-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="f5836-113">В конце этой статьи вы найдете код полной схемы и пример XML-файла.</span><span class="sxs-lookup"><span data-stu-id="f5836-113">You can find the complete schema code and XML example at the end of this topic.</span></span>  
>
>

## <span data-ttu-id="f5836-114"><a name="AssetFiles "></a> Корневой элемент AssetFiles</span><span class="sxs-lookup"><span data-stu-id="f5836-114"><a name="AssetFiles "></a> AssetFiles root element</span></span>
<span data-ttu-id="f5836-115">Коллекция записей AssetFile для задания кодирования.</span><span class="sxs-lookup"><span data-stu-id="f5836-115">Collection of AssetFile entries for the encoding job.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="f5836-116">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="f5836-116">Child elements</span></span>
| <span data-ttu-id="f5836-117">Имя</span><span class="sxs-lookup"><span data-stu-id="f5836-117">Name</span></span> | <span data-ttu-id="f5836-118">Описание</span><span class="sxs-lookup"><span data-stu-id="f5836-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f5836-119">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="f5836-119">**AssetFile**</span></span><br/><br/> <span data-ttu-id="f5836-120">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="f5836-120">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="f5836-121">[Элемент AssetFile](media-services-output-metadata-schema.md), который является частью коллекции AssetFiles.</span><span class="sxs-lookup"><span data-stu-id="f5836-121">An [AssetFile element](media-services-output-metadata-schema.md) that is part of the AssetFiles collection.</span></span> |

## <span data-ttu-id="f5836-122"><a name="AssetFile "></a> Элемент AssetFile</span><span class="sxs-lookup"><span data-stu-id="f5836-122"><a name="AssetFile "></a> AssetFile element</span></span>
<span data-ttu-id="f5836-123">Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="f5836-123">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="f5836-124">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="f5836-124">Attributes</span></span>
| <span data-ttu-id="f5836-125">Имя</span><span class="sxs-lookup"><span data-stu-id="f5836-125">Name</span></span> | <span data-ttu-id="f5836-126">Тип</span><span class="sxs-lookup"><span data-stu-id="f5836-126">Type</span></span> | <span data-ttu-id="f5836-127">Описание</span><span class="sxs-lookup"><span data-stu-id="f5836-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5836-128">**Имя**</span><span class="sxs-lookup"><span data-stu-id="f5836-128">**Name**</span></span><br/><br/> <span data-ttu-id="f5836-129">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-129">Required</span></span> |<span data-ttu-id="f5836-130">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="f5836-130">**xs:string**</span></span> |<span data-ttu-id="f5836-131">Имя файла ресурса мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="f5836-131">The media asset file name.</span></span> |
| <span data-ttu-id="f5836-132">**Размер**</span><span class="sxs-lookup"><span data-stu-id="f5836-132">**Size**</span></span><br/><br/> <span data-ttu-id="f5836-133">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="f5836-133">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="f5836-134">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-134">Required</span></span> |<span data-ttu-id="f5836-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="f5836-135">**xs:long**</span></span> |<span data-ttu-id="f5836-136">Размер файла ресурса-контейнера в байтах.</span><span class="sxs-lookup"><span data-stu-id="f5836-136">Size of the asset file in bytes.</span></span> |
| <span data-ttu-id="f5836-137">**Duration**</span><span class="sxs-lookup"><span data-stu-id="f5836-137">**Duration**</span></span><br/><br/> <span data-ttu-id="f5836-138">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-138">Required</span></span> |<span data-ttu-id="f5836-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="f5836-139">**xs:duration**</span></span> |<span data-ttu-id="f5836-140">Длительность воспроизведения содержимого.</span><span class="sxs-lookup"><span data-stu-id="f5836-140">Content play back duration.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="f5836-141">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="f5836-141">Child elements</span></span>
| <span data-ttu-id="f5836-142">Имя</span><span class="sxs-lookup"><span data-stu-id="f5836-142">Name</span></span> | <span data-ttu-id="f5836-143">Описание</span><span class="sxs-lookup"><span data-stu-id="f5836-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f5836-144">**Источники**</span><span class="sxs-lookup"><span data-stu-id="f5836-144">**Sources**</span></span> |<span data-ttu-id="f5836-145">Коллекция входных и исходных файлов мультимедиа, которая обрабатывалась для создания AssetFile.</span><span class="sxs-lookup"><span data-stu-id="f5836-145">Collection of input/source media files, that was processed in order to produce this AssetFile.</span></span> <span data-ttu-id="f5836-146">Дополнительные сведения см. в разделе [Элемент Source](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="f5836-146">For more information, see [Source element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="f5836-147">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="f5836-147">**VideoTracks**</span></span><br/><br/> <span data-ttu-id="f5836-148">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="f5836-148">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="f5836-149">Каждый физический файл ресурса-контейнера может содержать ноль или более видеодорожек, чередуемых в соответствующем формате ресурса-контейнера.</span><span class="sxs-lookup"><span data-stu-id="f5836-149">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="f5836-150">Это коллекция всех видеодорожек.</span><span class="sxs-lookup"><span data-stu-id="f5836-150">This is the collection of all those video tracks.</span></span> <span data-ttu-id="f5836-151">Дополнительные сведения см. в разделе [Элемент VideoTracks](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="f5836-151">For more information, see [VideoTracks element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="f5836-152">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="f5836-152">**AudioTracks**</span></span><br/><br/> <span data-ttu-id="f5836-153">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="f5836-153">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="f5836-154">Каждый физический файл ресурса-контейнера может содержать ноль или более звуковых дорожек, чередуемых в соответствующем формате ресурса-контейнера.</span><span class="sxs-lookup"><span data-stu-id="f5836-154">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="f5836-155">Это коллекция всех звуковых дорожек.</span><span class="sxs-lookup"><span data-stu-id="f5836-155">This is the collection of all those audio tracks.</span></span> <span data-ttu-id="f5836-156">Дополнительные сведения см. в разделе [Элемент AudioTracks](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="f5836-156">For more information, see [AudioTracks element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="f5836-157"><a name="Sources "></a> Элемент Sources</span><span class="sxs-lookup"><span data-stu-id="f5836-157"><a name="Sources "></a> Sources element</span></span>
<span data-ttu-id="f5836-158">Коллекция входных и исходных файлов мультимедиа, которая обрабатывалась для создания AssetFile.</span><span class="sxs-lookup"><span data-stu-id="f5836-158">Collection of input/source media files, that was processed in order to produce this AssetFile.</span></span>  

<span data-ttu-id="f5836-159">Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="f5836-159">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="f5836-160">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="f5836-160">Child elements</span></span>
| <span data-ttu-id="f5836-161">Имя</span><span class="sxs-lookup"><span data-stu-id="f5836-161">Name</span></span> | <span data-ttu-id="f5836-162">Описание</span><span class="sxs-lookup"><span data-stu-id="f5836-162">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f5836-163">**Источник**</span><span class="sxs-lookup"><span data-stu-id="f5836-163">**Source**</span></span><br/><br/> <span data-ttu-id="f5836-164">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="f5836-164">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="f5836-165">Входной или исходный файл, используемый при создании этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="f5836-165">An input/source file used when generating this asset.</span></span> <span data-ttu-id="f5836-166">Дополнительные сведения см. в разделе [Элемент Source](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="f5836-166">For more information see [Source element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="f5836-167"><a name="Source "></a> Элемент Source</span><span class="sxs-lookup"><span data-stu-id="f5836-167"><a name="Source "></a> Source element</span></span>
<span data-ttu-id="f5836-168">Входной или исходный файл, используемый при создании этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="f5836-168">An input/source file used when generating this asset.</span></span>  

<span data-ttu-id="f5836-169">Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="f5836-169">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="f5836-170">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="f5836-170">Attributes</span></span>
| <span data-ttu-id="f5836-171">Имя</span><span class="sxs-lookup"><span data-stu-id="f5836-171">Name</span></span> | <span data-ttu-id="f5836-172">Тип</span><span class="sxs-lookup"><span data-stu-id="f5836-172">Type</span></span> | <span data-ttu-id="f5836-173">Описание</span><span class="sxs-lookup"><span data-stu-id="f5836-173">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5836-174">**Имя**</span><span class="sxs-lookup"><span data-stu-id="f5836-174">**Name**</span></span><br/><br/> <span data-ttu-id="f5836-175">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-175">Required</span></span> |<span data-ttu-id="f5836-176">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="f5836-176">**xs:string**</span></span> |<span data-ttu-id="f5836-177">Имя входного исходного файла.</span><span class="sxs-lookup"><span data-stu-id="f5836-177">Input source file name.</span></span> |

## <span data-ttu-id="f5836-178"><a name="VideoTracks "></a> Элемент VideoTracks</span><span class="sxs-lookup"><span data-stu-id="f5836-178"><a name="VideoTracks "></a> VideoTracks element</span></span>
<span data-ttu-id="f5836-179">Каждый физический файл ресурса-контейнера может содержать ноль или более видеодорожек, чередуемых в соответствующем формате ресурса-контейнера.</span><span class="sxs-lookup"><span data-stu-id="f5836-179">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="f5836-180">Это коллекция всех видеодорожек.</span><span class="sxs-lookup"><span data-stu-id="f5836-180">This is the collection of all those video tracks.</span></span>  

<span data-ttu-id="f5836-181">Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="f5836-181">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="f5836-182">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="f5836-182">Child elements</span></span>
| <span data-ttu-id="f5836-183">Имя</span><span class="sxs-lookup"><span data-stu-id="f5836-183">Name</span></span> | <span data-ttu-id="f5836-184">Описание</span><span class="sxs-lookup"><span data-stu-id="f5836-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f5836-185">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="f5836-185">**VideoTrack**</span></span><br/><br/> <span data-ttu-id="f5836-186">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="f5836-186">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="f5836-187">Конкретная видеодорожка в родительском элементе AssetFile.</span><span class="sxs-lookup"><span data-stu-id="f5836-187">A specific video track in the parent AssetFile.</span></span> <span data-ttu-id="f5836-188">Дополнительные сведения см. в разделе [Элемент VideoTrack](media-services-output-metadata-schema.md#VideoTrack).</span><span class="sxs-lookup"><span data-stu-id="f5836-188">For more information, see [VideoTrack element](media-services-output-metadata-schema.md#VideoTrack).</span></span> |

## <span data-ttu-id="f5836-189"><a name="VideoTrack"></a> Элемент VideoTrack</span><span class="sxs-lookup"><span data-stu-id="f5836-189"><a name="VideoTrack"></a> VideoTrack element</span></span>
<span data-ttu-id="f5836-190">Конкретная видеодорожка в родительском элементе AssetFile.</span><span class="sxs-lookup"><span data-stu-id="f5836-190">A specific video track in the parent AssetFile.</span></span>  

<span data-ttu-id="f5836-191">Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="f5836-191">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="f5836-192">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="f5836-192">Attributes</span></span>
| <span data-ttu-id="f5836-193">Имя</span><span class="sxs-lookup"><span data-stu-id="f5836-193">Name</span></span> | <span data-ttu-id="f5836-194">Тип</span><span class="sxs-lookup"><span data-stu-id="f5836-194">Type</span></span> | <span data-ttu-id="f5836-195">Описание</span><span class="sxs-lookup"><span data-stu-id="f5836-195">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5836-196">**Id**</span><span class="sxs-lookup"><span data-stu-id="f5836-196">**Id**</span></span><br/><br/> <span data-ttu-id="f5836-197">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="f5836-197">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="f5836-198">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-198">Required</span></span> |<span data-ttu-id="f5836-199">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="f5836-199">**xs:int**</span></span> |<span data-ttu-id="f5836-200">Отсчитываемый от нуля индекс видеодорожки. **Примечание.** MP4-файл необязательно должен содержать идентификатор дорожки.</span><span class="sxs-lookup"><span data-stu-id="f5836-200">Zero-based index of this video track. **Note:**  This is not necessarily the TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="f5836-201">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="f5836-201">**FourCC**</span></span><br/><br/> <span data-ttu-id="f5836-202">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-202">Required</span></span> |<span data-ttu-id="f5836-203">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="f5836-203">**xs:string**</span></span> |<span data-ttu-id="f5836-204">Код FourCC видеокодека.</span><span class="sxs-lookup"><span data-stu-id="f5836-204">Video codec FourCC code.</span></span> |
| <span data-ttu-id="f5836-205">**Профиль**</span><span class="sxs-lookup"><span data-stu-id="f5836-205">**Profile**</span></span> |<span data-ttu-id="f5836-206">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="f5836-206">**xs:string**</span></span> |<span data-ttu-id="f5836-207">Профиль H264 (применим только для кодека H264).</span><span class="sxs-lookup"><span data-stu-id="f5836-207">H264 profile (only applicable to H264 codec).</span></span> |
| <span data-ttu-id="f5836-208">**Level**</span><span class="sxs-lookup"><span data-stu-id="f5836-208">**Level**</span></span> |<span data-ttu-id="f5836-209">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="f5836-209">**xs:string**</span></span> |<span data-ttu-id="f5836-210">Уровень H264 (применим только для кодека H264).</span><span class="sxs-lookup"><span data-stu-id="f5836-210">H264 level (only applicable to H264 codec).</span></span> |
| <span data-ttu-id="f5836-211">**Width**</span><span class="sxs-lookup"><span data-stu-id="f5836-211">**Width**</span></span><br/><br/> <span data-ttu-id="f5836-212">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="f5836-212">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="f5836-213">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-213">Required</span></span> |<span data-ttu-id="f5836-214">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="f5836-214">**xs:int**</span></span> |<span data-ttu-id="f5836-215">Ширина закодированного видео в пикселях.</span><span class="sxs-lookup"><span data-stu-id="f5836-215">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="f5836-216">**Height**</span><span class="sxs-lookup"><span data-stu-id="f5836-216">**Height**</span></span><br/><br/> <span data-ttu-id="f5836-217">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="f5836-217">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="f5836-218">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-218">Required</span></span> |<span data-ttu-id="f5836-219">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="f5836-219">**xs:int**</span></span> |<span data-ttu-id="f5836-220">Высота закодированного видео в пикселях.</span><span class="sxs-lookup"><span data-stu-id="f5836-220">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="f5836-221">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="f5836-221">**DisplayAspectRatioNumerator**</span></span><br/><br/> <span data-ttu-id="f5836-222">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="f5836-222">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="f5836-223">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-223">Required</span></span> |<span data-ttu-id="f5836-224">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="f5836-224">**xs:double**</span></span> |<span data-ttu-id="f5836-225">Числитель пропорции отображения видео.</span><span class="sxs-lookup"><span data-stu-id="f5836-225">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="f5836-226">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="f5836-226">**DisplayAspectRatioDenominator**</span></span><br/><br/> <span data-ttu-id="f5836-227">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="f5836-227">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="f5836-228">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-228">Required</span></span> |<span data-ttu-id="f5836-229">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="f5836-229">**xs:double**</span></span> |<span data-ttu-id="f5836-230">Знаменатель пропорции отображения видео.</span><span class="sxs-lookup"><span data-stu-id="f5836-230">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="f5836-231">**Framerate**</span><span class="sxs-lookup"><span data-stu-id="f5836-231">**Framerate**</span></span><br/><br/> <span data-ttu-id="f5836-232">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="f5836-232">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="f5836-233">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-233">Required</span></span> |<span data-ttu-id="f5836-234">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="f5836-234">**xs:decimal**</span></span> |<span data-ttu-id="f5836-235">Измеренная частота видеокадров в формате 3F.</span><span class="sxs-lookup"><span data-stu-id="f5836-235">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="f5836-236">**TargetFramerate**</span><span class="sxs-lookup"><span data-stu-id="f5836-236">**TargetFramerate**</span></span><br/><br/> <span data-ttu-id="f5836-237">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="f5836-237">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="f5836-238">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-238">Required</span></span> |<span data-ttu-id="f5836-239">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="f5836-239">**xs:decimal**</span></span> |<span data-ttu-id="f5836-240">Предустановленная частота кадров целевого видео в формате 3F.</span><span class="sxs-lookup"><span data-stu-id="f5836-240">Preset target video frame rate in .3f format.</span></span> |
| <span data-ttu-id="f5836-241">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="f5836-241">**Bitrate**</span></span><br/><br/> <span data-ttu-id="f5836-242">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="f5836-242">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="f5836-243">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-243">Required</span></span> |<span data-ttu-id="f5836-244">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="f5836-244">**xs:int**</span></span> |<span data-ttu-id="f5836-245">Средняя скорость аудиопотока в килобитах в секунду, вычисленная на основе файла ресурса-контейнера.</span><span class="sxs-lookup"><span data-stu-id="f5836-245">Average video bit rate in kilobits per second, as calculated from the AssetFile.</span></span> <span data-ttu-id="f5836-246">Подсчитываются только полезные данные элементарного потока, издержки на упаковку не включаются.</span><span class="sxs-lookup"><span data-stu-id="f5836-246">Counts only the elementary stream payload, and does not include the packaging overhead.</span></span> |
| <span data-ttu-id="f5836-247">**TargetBitrate**</span><span class="sxs-lookup"><span data-stu-id="f5836-247">**TargetBitrate**</span></span><br/><br/> <span data-ttu-id="f5836-248">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="f5836-248">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="f5836-249">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-249">Required</span></span> |<span data-ttu-id="f5836-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="f5836-250">**xs:int**</span></span> |<span data-ttu-id="f5836-251">Целевая средняя скорость для данной видеодорожки в килобитах в секунду, запрошенная на основе предустановки кодирования.</span><span class="sxs-lookup"><span data-stu-id="f5836-251">Target average bitrate for this video track, as requested via the encoding preset, in kilobits per second.</span></span> |
| <span data-ttu-id="f5836-252">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="f5836-252">**MaxGOPBitrate**</span></span><br/><br/> <span data-ttu-id="f5836-253">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="f5836-253">minInclusive ="0"</span></span> |<span data-ttu-id="f5836-254">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="f5836-254">**xs:int**</span></span> |<span data-ttu-id="f5836-255">Максимальная средняя скорость группы изображений (GOP) для данной видеодорожки в килобитах в секунду.</span><span class="sxs-lookup"><span data-stu-id="f5836-255">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |

## <span data-ttu-id="f5836-256"><a name="AudioTracks "></a> Элемент AudioTracks</span><span class="sxs-lookup"><span data-stu-id="f5836-256"><a name="AudioTracks "></a> AudioTracks element</span></span>
<span data-ttu-id="f5836-257">Каждый физический файл ресурса-контейнера может содержать ноль или более звуковых дорожек, чередуемых в соответствующем формате ресурса-контейнера.</span><span class="sxs-lookup"><span data-stu-id="f5836-257">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="f5836-258">Это коллекция всех звуковых дорожек.</span><span class="sxs-lookup"><span data-stu-id="f5836-258">This is the collection of all those audio tracks.</span></span>  

<span data-ttu-id="f5836-259">Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="f5836-259">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="f5836-260">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="f5836-260">Child elements</span></span>
| <span data-ttu-id="f5836-261">Имя</span><span class="sxs-lookup"><span data-stu-id="f5836-261">Name</span></span> | <span data-ttu-id="f5836-262">Описание</span><span class="sxs-lookup"><span data-stu-id="f5836-262">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f5836-263">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="f5836-263">**AudioTrack**</span></span><br/><br/> <span data-ttu-id="f5836-264">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="f5836-264">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="f5836-265">Конкретная звуковая дорожка в родительском элементе AssetFile.</span><span class="sxs-lookup"><span data-stu-id="f5836-265">A specific audio track in the parent AssetFile.</span></span> <span data-ttu-id="f5836-266">Дополнительные сведения см. в разделе [Элемент AudioTrack](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="f5836-266">For more information, see [AudioTrack element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="f5836-267"><a name="AudioTrack "></a> Элемент AudioTrack</span><span class="sxs-lookup"><span data-stu-id="f5836-267"><a name="AudioTrack "></a> AudioTrack element</span></span>
<span data-ttu-id="f5836-268">Конкретная звуковая дорожка в родительском элементе AssetFile.</span><span class="sxs-lookup"><span data-stu-id="f5836-268">A specific audio track in the parent AssetFile.</span></span>  

<span data-ttu-id="f5836-269">Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="f5836-269">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="f5836-270">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="f5836-270">Attributes</span></span>
| <span data-ttu-id="f5836-271">Имя</span><span class="sxs-lookup"><span data-stu-id="f5836-271">Name</span></span> | <span data-ttu-id="f5836-272">Тип</span><span class="sxs-lookup"><span data-stu-id="f5836-272">Type</span></span> | <span data-ttu-id="f5836-273">Описание</span><span class="sxs-lookup"><span data-stu-id="f5836-273">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5836-274">**Id**</span><span class="sxs-lookup"><span data-stu-id="f5836-274">**Id**</span></span><br/><br/> <span data-ttu-id="f5836-275">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="f5836-275">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="f5836-276">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-276">Required</span></span> |<span data-ttu-id="f5836-277">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="f5836-277">**xs:int**</span></span> |<span data-ttu-id="f5836-278">Отсчитываемый от нуля индекс звуковой дорожки. **Примечание.** MP4-файл необязательно должен содержать идентификатор дорожки.</span><span class="sxs-lookup"><span data-stu-id="f5836-278">Zero-based index of this audio track. **Note:**  This is not necessarily the TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="f5836-279">**Codec**</span><span class="sxs-lookup"><span data-stu-id="f5836-279">**Codec**</span></span> |<span data-ttu-id="f5836-280">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="f5836-280">**xs:string**</span></span> |<span data-ttu-id="f5836-281">Строка кодека звуковой дорожки.</span><span class="sxs-lookup"><span data-stu-id="f5836-281">Audio track codec string.</span></span> |
| <span data-ttu-id="f5836-282">**EncoderVersion**</span><span class="sxs-lookup"><span data-stu-id="f5836-282">**EncoderVersion**</span></span> |<span data-ttu-id="f5836-283">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="f5836-283">**xs:string**</span></span> |<span data-ttu-id="f5836-284">Дополнительная строка версии кодировщика, требуемая для EAC3.</span><span class="sxs-lookup"><span data-stu-id="f5836-284">Optional encoder version string, required for EAC3.</span></span> |
| <span data-ttu-id="f5836-285">**Channels**</span><span class="sxs-lookup"><span data-stu-id="f5836-285">**Channels**</span></span><br/><br/> <span data-ttu-id="f5836-286">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="f5836-286">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="f5836-287">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-287">Required</span></span> |<span data-ttu-id="f5836-288">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="f5836-288">**xs:int**</span></span> |<span data-ttu-id="f5836-289">Число аудиоканалов.</span><span class="sxs-lookup"><span data-stu-id="f5836-289">Number of audio channels.</span></span> |
| <span data-ttu-id="f5836-290">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="f5836-290">**SamplingRate**</span></span><br/><br/> <span data-ttu-id="f5836-291">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="f5836-291">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="f5836-292">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-292">Required</span></span> |<span data-ttu-id="f5836-293">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="f5836-293">**xs:int**</span></span> |<span data-ttu-id="f5836-294">Частота аудиовыборки: выборок/с или Гц.</span><span class="sxs-lookup"><span data-stu-id="f5836-294">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="f5836-295">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="f5836-295">**Bitrate**</span></span><br/><br/> <span data-ttu-id="f5836-296">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="f5836-296">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="f5836-297">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-297">Required</span></span> |<span data-ttu-id="f5836-298">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="f5836-298">**xs:int**</span></span> |<span data-ttu-id="f5836-299">Средняя скорость аудиопотока в битах в секунду, вычисленная на основе файла ресурса-контейнера.</span><span class="sxs-lookup"><span data-stu-id="f5836-299">Average audio bit rate in bits per second, as calculated from the AssetFile.</span></span> <span data-ttu-id="f5836-300">Подсчитываются только полезные данные элементарного потока, издержки на упаковку не включаются.</span><span class="sxs-lookup"><span data-stu-id="f5836-300">Counts only the elementary stream payload, and does not include the packaging overhead.</span></span> |
| <span data-ttu-id="f5836-301">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="f5836-301">**BitsPerSample**</span></span><br/><br/> <span data-ttu-id="f5836-302">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="f5836-302">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="f5836-303">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-303">Required</span></span> |<span data-ttu-id="f5836-304">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="f5836-304">**xs:int**</span></span> |<span data-ttu-id="f5836-305">Битов на выборку для формата wFormatTag.</span><span class="sxs-lookup"><span data-stu-id="f5836-305">Bits per sample for the wFormatTag format type.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="f5836-306">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="f5836-306">Child elements</span></span>
| <span data-ttu-id="f5836-307">Имя</span><span class="sxs-lookup"><span data-stu-id="f5836-307">Name</span></span> | <span data-ttu-id="f5836-308">Описание</span><span class="sxs-lookup"><span data-stu-id="f5836-308">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f5836-309">**LoudnessMeteringResultParameters**</span><span class="sxs-lookup"><span data-stu-id="f5836-309">**LoudnessMeteringResultParameters**</span></span><br/><br/> <span data-ttu-id="f5836-310">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="f5836-310">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="f5836-311">Параметры результата измерения громкости.</span><span class="sxs-lookup"><span data-stu-id="f5836-311">Loudness metering result parameters.</span></span> <span data-ttu-id="f5836-312">Дополнительные сведения см. в разделе [Элемент LoudnessMeteringResultParameter](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="f5836-312">For more information, see [LoudnessMeteringResultParameters element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="f5836-313"><a name="LoudnessMeteringResultParameters "></a> Элемент LoudnessMeteringResultParameters</span><span class="sxs-lookup"><span data-stu-id="f5836-313"><a name="LoudnessMeteringResultParameters "></a> LoudnessMeteringResultParameters element</span></span>
<span data-ttu-id="f5836-314">Параметры результата измерения громкости.</span><span class="sxs-lookup"><span data-stu-id="f5836-314">Loudness metering result parameters.</span></span>  

<span data-ttu-id="f5836-315">Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="f5836-315">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="f5836-316">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="f5836-316">Attributes</span></span>
| <span data-ttu-id="f5836-317">Имя</span><span class="sxs-lookup"><span data-stu-id="f5836-317">Name</span></span> | <span data-ttu-id="f5836-318">Тип</span><span class="sxs-lookup"><span data-stu-id="f5836-318">Type</span></span> | <span data-ttu-id="f5836-319">Описание</span><span class="sxs-lookup"><span data-stu-id="f5836-319">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f5836-320">**DPLMVersionInformation**</span><span class="sxs-lookup"><span data-stu-id="f5836-320">**DPLMVersionInformation**</span></span> |<span data-ttu-id="f5836-321">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="f5836-321">**xs:string**</span></span> |<span data-ttu-id="f5836-322">Версия комплекта разработчика **Dolby** Professional Loudness Metering (DPLM).</span><span class="sxs-lookup"><span data-stu-id="f5836-322">**Dolby** professional loudness metering development kit version.</span></span> |
| <span data-ttu-id="f5836-323">**DialogNormalization**</span><span class="sxs-lookup"><span data-stu-id="f5836-323">**DialogNormalization**</span></span><br/><br/> <span data-ttu-id="f5836-324">minInclusive="-31" maxInclusive="-1"</span><span class="sxs-lookup"><span data-stu-id="f5836-324">minInclusive="-31" maxInclusive="-1"</span></span><br/><br/> <span data-ttu-id="f5836-325">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-325">Required</span></span> |<span data-ttu-id="f5836-326">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="f5836-326">**xs:int**</span></span> |<span data-ttu-id="f5836-327">DialogNormalization, созданный с помощью DPLM, необходим при установке LoudnessMetering.</span><span class="sxs-lookup"><span data-stu-id="f5836-327">DialogNormalization generated through DPLM, required when LoudnessMetering is set</span></span> |
| <span data-ttu-id="f5836-328">**IntegratedLoudness**</span><span class="sxs-lookup"><span data-stu-id="f5836-328">**IntegratedLoudness**</span></span><br/><br/> <span data-ttu-id="f5836-329">minInclusive="-70" maxInclusive="10"</span><span class="sxs-lookup"><span data-stu-id="f5836-329">minInclusive="-70" maxInclusive="10"</span></span><br/><br/> <span data-ttu-id="f5836-330">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-330">Required</span></span> |<span data-ttu-id="f5836-331">**xs: float**</span><span class="sxs-lookup"><span data-stu-id="f5836-331">**xs:float**</span></span> |<span data-ttu-id="f5836-332">Интегрированная громкость</span><span class="sxs-lookup"><span data-stu-id="f5836-332">Integrated loudness</span></span> |
| <span data-ttu-id="f5836-333">**IntegratedLoudnessUnit**</span><span class="sxs-lookup"><span data-stu-id="f5836-333">**IntegratedLoudnessUnit**</span></span><br/><br/> <span data-ttu-id="f5836-334">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-334">Required</span></span> |<span data-ttu-id="f5836-335">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="f5836-335">**xs:string**</span></span> |<span data-ttu-id="f5836-336">Единица измерения интегрированной громкости.</span><span class="sxs-lookup"><span data-stu-id="f5836-336">Integrated loudness unit.</span></span> |
| <span data-ttu-id="f5836-337">**IntegratedLoudnessGatingMethod**</span><span class="sxs-lookup"><span data-stu-id="f5836-337">**IntegratedLoudnessGatingMethod**</span></span><br/><br/> <span data-ttu-id="f5836-338">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-338">Required</span></span> |<span data-ttu-id="f5836-339">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="f5836-339">**xs:string**</span></span> |<span data-ttu-id="f5836-340">Идентификатор стробирования</span><span class="sxs-lookup"><span data-stu-id="f5836-340">Gating identifier</span></span> |
| <span data-ttu-id="f5836-341">**IntegratedLoudnessSpeechPercentage**</span><span class="sxs-lookup"><span data-stu-id="f5836-341">**IntegratedLoudnessSpeechPercentage**</span></span><br/><br/> <span data-ttu-id="f5836-342">minInclusive ="0" maxInclusive="100"</span><span class="sxs-lookup"><span data-stu-id="f5836-342">minInclusive ="0" maxInclusive="100"</span></span> |<span data-ttu-id="f5836-343">**xs: float**</span><span class="sxs-lookup"><span data-stu-id="f5836-343">**xs:float**</span></span> |<span data-ttu-id="f5836-344">Речевое содержимое в программе в процентах.</span><span class="sxs-lookup"><span data-stu-id="f5836-344">Speech content over the program, as a percentage.</span></span> |
| <span data-ttu-id="f5836-345">**SamplePeak**</span><span class="sxs-lookup"><span data-stu-id="f5836-345">**SamplePeak**</span></span><br/><br/> <span data-ttu-id="f5836-346">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-346">Required</span></span> |<span data-ttu-id="f5836-347">**xs: float**</span><span class="sxs-lookup"><span data-stu-id="f5836-347">**xs:float**</span></span> |<span data-ttu-id="f5836-348">Пиковое абсолютное опорное значение в канале после сброса или последней очистки.</span><span class="sxs-lookup"><span data-stu-id="f5836-348">Peak absolute sample value, since reset or since it was last cleared, per channel.</span></span>  <span data-ttu-id="f5836-349">Единицы измерения — dBFS.</span><span class="sxs-lookup"><span data-stu-id="f5836-349">Units are dBFS.</span></span> |
| <span data-ttu-id="f5836-350">**SamplePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="f5836-350">**SamplePeakUnit**</span></span><br/><br/> <span data-ttu-id="f5836-351">fixed="dBFS"</span><span class="sxs-lookup"><span data-stu-id="f5836-351">fixed="dBFS"</span></span><br/><br/> <span data-ttu-id="f5836-352">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-352">Required</span></span> |<span data-ttu-id="f5836-353">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="f5836-353">**xs:anySimpleType**</span></span> |<span data-ttu-id="f5836-354">Единица измерения пикового опорного значения.</span><span class="sxs-lookup"><span data-stu-id="f5836-354">Sample peak unit.</span></span> |
| <span data-ttu-id="f5836-355">**TruePeak**</span><span class="sxs-lookup"><span data-stu-id="f5836-355">**TruePeak**</span></span><br/><br/> <span data-ttu-id="f5836-356">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-356">Required</span></span> |<span data-ttu-id="f5836-357">**xs: float**</span><span class="sxs-lookup"><span data-stu-id="f5836-357">**xs:float**</span></span> |<span data-ttu-id="f5836-358">Наибольшее абсолютное пиковое значение в канале, соответствующее ITU-R BS.1770-2, после сброса или последней очистки.</span><span class="sxs-lookup"><span data-stu-id="f5836-358">Maximum true peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.</span></span> <span data-ttu-id="f5836-359">Единицы измерения — dBTP.</span><span class="sxs-lookup"><span data-stu-id="f5836-359">Units are dBTP.</span></span> |
| <span data-ttu-id="f5836-360">**TruePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="f5836-360">**TruePeakUnit**</span></span><br/><br/> <span data-ttu-id="f5836-361">fixed="dBTP"</span><span class="sxs-lookup"><span data-stu-id="f5836-361">fixed="dBTP"</span></span><br/><br/> <span data-ttu-id="f5836-362">Обязательно</span><span class="sxs-lookup"><span data-stu-id="f5836-362">Required</span></span> |<span data-ttu-id="f5836-363">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="f5836-363">**xs:anySimpleType**</span></span> |<span data-ttu-id="f5836-364">Единица измерения наибольшего абсолютного опорного значения.</span><span class="sxs-lookup"><span data-stu-id="f5836-364">True peak unit.</span></span> |

## <a name="schema-code"></a><span data-ttu-id="f5836-365">Код схемы</span><span class="sxs-lookup"><span data-stu-id="f5836-365">Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.2"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               elementFormDefault="qualified">  
      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for the encoding job</xs:documentation>  
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
                      <xs:documentation>Collection of input/source media files, that was processed in order to produce this AssetFile</xs:documentation>  
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
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is the collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>A specific video track in the parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:attribute name="Id" use="required">  
                              <xs:annotation>  
                                <xs:documentation>zero-based index of this video track. Note: this is not necessarily the TrackID as used in an MP4 file</xs:documentation>  
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
                                <xs:documentation>average video bit rate in kilobits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="TargetBitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>target average bitrate for this video track, as requested via the encoding preset, in kilobits per second</xs:documentation>  
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
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is the collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>a specific audio track in the parent AssetFile</xs:documentation>  
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
                                      <xs:documentation>Speech content over the program, as a percentage.</xs:documentation>  
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
                                <xs:documentation>zero-based index of this audio track. Note: this is not necessarily the TrackID as used in an MP4 file</xs:documentation>  
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
                                <xs:documentation>average audio bit rate in bits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="BitsPerSample" use="required">  
                              <xs:annotation>  
                                <xs:documentation>Bits per sample for the wFormatTag format type</xs:documentation>  
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
                    <xs:documentation>the media asset file name</xs:documentation>  
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



## <span data-ttu-id="f5836-366"><a name="xml"></a> Пример XML-файла</span><span class="sxs-lookup"><span data-stu-id="f5836-366"><a name="xml"></a> XML example</span></span>
 <span data-ttu-id="f5836-367">Ниже приведен пример файла выходных метаданных.</span><span class="sxs-lookup"><span data-stu-id="f5836-367">The following is an example of the Output metadata file.</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="f5836-368">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f5836-368">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f5836-369">Отзывы</span><span class="sxs-lookup"><span data-stu-id="f5836-369">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
