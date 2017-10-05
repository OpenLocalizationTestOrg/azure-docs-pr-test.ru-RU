---
title: "Формат файла свойств и файла метаданных импорта и экспорта Azure | Документация Майкрософт"
description: "Узнайте, как указать метаданные и свойства для одного или нескольких больших двоичных объектов, входящих в задание импорта или экспорта."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 840364c6-d9a8-4b43-a9f3-f7441c625069
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 3f728ad94cdcbd32092b677f11a737ae91376720
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a><span data-ttu-id="227b6-103">Формат файла свойств и файла метаданных службы импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="227b6-103">Azure Import/Export service metadata and properties file format</span></span>
<span data-ttu-id="227b6-104">В рамках задания импорта или экспорта можно указать метаданные и свойства для одного или нескольких больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="227b6-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span></span> <span data-ttu-id="227b6-105">Чтобы задать метаданные и свойства для больших двоичных объектов, созданных в рамках задания импорта, на жестком диске необходимо создать файл метаданных или файл свойств, содержащий импортируемые данные.</span><span class="sxs-lookup"><span data-stu-id="227b6-105">To set metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on the hard drive containing the data to be imported.</span></span> <span data-ttu-id="227b6-106">Для задания экспорта метаданные и свойства записываются в файл метаданных или файл свойств, содержащийся на жестком диске, возвращаемом пользователю.</span><span class="sxs-lookup"><span data-stu-id="227b6-106">For an export job, metadata and properties are written to a metadata or properties file that is included on the hard drive returned to you.</span></span>  
  
## <a name="metadata-file-format"></a><span data-ttu-id="227b6-107">Формат файла метаданных</span><span class="sxs-lookup"><span data-stu-id="227b6-107">Metadata file format</span></span>  
<span data-ttu-id="227b6-108">Файл метаданных имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="227b6-108">The format of a metadata file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|<span data-ttu-id="227b6-109">XML-элемент</span><span class="sxs-lookup"><span data-stu-id="227b6-109">XML Element</span></span>|<span data-ttu-id="227b6-110">Тип</span><span class="sxs-lookup"><span data-stu-id="227b6-110">Type</span></span>|<span data-ttu-id="227b6-111">Описание</span><span class="sxs-lookup"><span data-stu-id="227b6-111">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Metadata`|<span data-ttu-id="227b6-112">Корневой элемент</span><span class="sxs-lookup"><span data-stu-id="227b6-112">Root element</span></span>|<span data-ttu-id="227b6-113">Корневой элемент файла метаданных.</span><span class="sxs-lookup"><span data-stu-id="227b6-113">The root element of the metadata file.</span></span>|  
|`metadata-name`|<span data-ttu-id="227b6-114">Строка</span><span class="sxs-lookup"><span data-stu-id="227b6-114">String</span></span>|<span data-ttu-id="227b6-115">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="227b6-115">Optional.</span></span> <span data-ttu-id="227b6-116">XML-элемент указывает имя метаданных большого двоичного объекта, а его значение определяет значение параметра метаданных.</span><span class="sxs-lookup"><span data-stu-id="227b6-116">The XML element specifies the name of the metadata for the blob, and its value specifies the value of the metadata setting.</span></span>|  
  
## <a name="properties-file-format"></a><span data-ttu-id="227b6-117">Формат файла свойств</span><span class="sxs-lookup"><span data-stu-id="227b6-117">Properties file format</span></span>  
<span data-ttu-id="227b6-118">Файл свойств имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="227b6-118">The format of a properties file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
[<Last-Modified>date-time-value</Last-Modified>]  
[<Etag>etag</Etag>]  
[<Content-Length>size-in-bytes<Content-Length>]  
[<Content-Type>content-type</Content-Type>]  
[<Content-MD5>content-md5</Content-MD5>]  
[<Content-Encoding>content-encoding</Content-Encoding>]  
[<Content-Language>content-language</Content-Language>]  
[<Cache-Control>cache-control</Cache-Control>]  
</Properties>  
```
  
|<span data-ttu-id="227b6-119">XML-элемент</span><span class="sxs-lookup"><span data-stu-id="227b6-119">XML Element</span></span>|<span data-ttu-id="227b6-120">Тип</span><span class="sxs-lookup"><span data-stu-id="227b6-120">Type</span></span>|<span data-ttu-id="227b6-121">Описание</span><span class="sxs-lookup"><span data-stu-id="227b6-121">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Properties`|<span data-ttu-id="227b6-122">Корневой элемент</span><span class="sxs-lookup"><span data-stu-id="227b6-122">Root element</span></span>|<span data-ttu-id="227b6-123">Корневой элемент файла свойств.</span><span class="sxs-lookup"><span data-stu-id="227b6-123">The root element of the properties file.</span></span>|  
|`Last-Modified`|<span data-ttu-id="227b6-124">Строка</span><span class="sxs-lookup"><span data-stu-id="227b6-124">String</span></span>|<span data-ttu-id="227b6-125">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="227b6-125">Optional.</span></span> <span data-ttu-id="227b6-126">Время последнего изменения большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="227b6-126">The last-modified time for the blob.</span></span> <span data-ttu-id="227b6-127">Только для заданий экспорта.</span><span class="sxs-lookup"><span data-stu-id="227b6-127">For export jobs only.</span></span>|  
|`Etag`|<span data-ttu-id="227b6-128">Строка</span><span class="sxs-lookup"><span data-stu-id="227b6-128">String</span></span>|<span data-ttu-id="227b6-129">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="227b6-129">Optional.</span></span> <span data-ttu-id="227b6-130">Значение ETag большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="227b6-130">The blob's ETag value.</span></span> <span data-ttu-id="227b6-131">Только для заданий экспорта.</span><span class="sxs-lookup"><span data-stu-id="227b6-131">For export jobs only.</span></span>|  
|`Content-Length`|<span data-ttu-id="227b6-132">Строка</span><span class="sxs-lookup"><span data-stu-id="227b6-132">String</span></span>|<span data-ttu-id="227b6-133">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="227b6-133">Optional.</span></span> <span data-ttu-id="227b6-134">Размер большого двоичного объекта в байтах.</span><span class="sxs-lookup"><span data-stu-id="227b6-134">The size of the blob in bytes.</span></span> <span data-ttu-id="227b6-135">Только для заданий экспорта.</span><span class="sxs-lookup"><span data-stu-id="227b6-135">For export jobs only.</span></span>|  
|`Content-Type`|<span data-ttu-id="227b6-136">Строка</span><span class="sxs-lookup"><span data-stu-id="227b6-136">String</span></span>|<span data-ttu-id="227b6-137">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="227b6-137">Optional.</span></span> <span data-ttu-id="227b6-138">Тип содержимого большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="227b6-138">The content type of the blob.</span></span>|  
|`Content-MD5`|<span data-ttu-id="227b6-139">Строка</span><span class="sxs-lookup"><span data-stu-id="227b6-139">String</span></span>|<span data-ttu-id="227b6-140">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="227b6-140">Optional.</span></span> <span data-ttu-id="227b6-141">Хэш MD5 большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="227b6-141">The blob's MD5 hash.</span></span>|  
|`Content-Encoding`|<span data-ttu-id="227b6-142">Строка</span><span class="sxs-lookup"><span data-stu-id="227b6-142">String</span></span>|<span data-ttu-id="227b6-143">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="227b6-143">Optional.</span></span> <span data-ttu-id="227b6-144">Кодирование содержимого большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="227b6-144">The blob's content encoding.</span></span>|  
|`Content-Language`|<span data-ttu-id="227b6-145">string</span><span class="sxs-lookup"><span data-stu-id="227b6-145">String</span></span>|<span data-ttu-id="227b6-146">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="227b6-146">Optional.</span></span> <span data-ttu-id="227b6-147">Язык содержимого большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="227b6-147">The blob's content language.</span></span>|  
|`Cache-Control`|<span data-ttu-id="227b6-148">Строка</span><span class="sxs-lookup"><span data-stu-id="227b6-148">String</span></span>|<span data-ttu-id="227b6-149">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="227b6-149">Optional.</span></span> <span data-ttu-id="227b6-150">Строка управления кэшем для большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="227b6-150">The cache control string for the blob.</span></span>|  

## <a name="next-steps"></a><span data-ttu-id="227b6-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="227b6-151">Next steps</span></span>

<span data-ttu-id="227b6-152">Дополнительные правила настройки свойств и метаданных больших двоичных объектов см. в статьях [Set Blob Properties](/rest/api/storageservices/set-blob-properties) (Задание свойств большого двоичного объекта), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata) (Задание метаданных большого двоичного объекта) и [Setting and Retrieving Properties and Metadata for Blob Resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) (Задание и получение свойств и метаданных для ресурсов больших двоичных объектов).</span><span class="sxs-lookup"><span data-stu-id="227b6-152">See [Set blob properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span></span>
