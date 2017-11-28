---
title: "aaaAzure импорта и экспорта метаданных и свойств формат файла | Документы Microsoft"
description: "Узнайте, как toospecify метаданных и свойств для одного или нескольких больших двоичных объектов, являются частью Импорт или экспорт заданий."
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
ms.openlocfilehash: bb13c1f1a27baea77298cb224970cd521d02d8c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a><span data-ttu-id="13e2b-103">Формат файла свойств и файла метаданных службы импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="13e2b-103">Azure Import/Export service metadata and properties file format</span></span>
<span data-ttu-id="13e2b-104">В рамках задания импорта или экспорта можно указать метаданные и свойства для одного или нескольких больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="13e2b-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span></span> <span data-ttu-id="13e2b-105">tooset метаданных или свойств для больших двоичных объектов, которые создаются в рамках задания импорта, можно указать файл метаданных или свойств на hello жесткий диск, содержащий toobe данных hello импортированы.</span><span class="sxs-lookup"><span data-stu-id="13e2b-105">tooset metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on hello hard drive containing hello data toobe imported.</span></span> <span data-ttu-id="13e2b-106">Для задания экспорта метаданные и свойства записываются tooa файл метаданных или свойств, который включается на жестком диске hello возвращается tooyou.</span><span class="sxs-lookup"><span data-stu-id="13e2b-106">For an export job, metadata and properties are written tooa metadata or properties file that is included on hello hard drive returned tooyou.</span></span>  
  
## <a name="metadata-file-format"></a><span data-ttu-id="13e2b-107">Формат файла метаданных</span><span class="sxs-lookup"><span data-stu-id="13e2b-107">Metadata file format</span></span>  
<span data-ttu-id="13e2b-108">Hello файла метаданных имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="13e2b-108">hello format of a metadata file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|<span data-ttu-id="13e2b-109">XML-элемент</span><span class="sxs-lookup"><span data-stu-id="13e2b-109">XML Element</span></span>|<span data-ttu-id="13e2b-110">Тип</span><span class="sxs-lookup"><span data-stu-id="13e2b-110">Type</span></span>|<span data-ttu-id="13e2b-111">Описание</span><span class="sxs-lookup"><span data-stu-id="13e2b-111">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Metadata`|<span data-ttu-id="13e2b-112">Корневой элемент</span><span class="sxs-lookup"><span data-stu-id="13e2b-112">Root element</span></span>|<span data-ttu-id="13e2b-113">корневой элемент файла метаданных hello Hello.</span><span class="sxs-lookup"><span data-stu-id="13e2b-113">hello root element of hello metadata file.</span></span>|  
|`metadata-name`|<span data-ttu-id="13e2b-114">Строка</span><span class="sxs-lookup"><span data-stu-id="13e2b-114">String</span></span>|<span data-ttu-id="13e2b-115">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="13e2b-115">Optional.</span></span> <span data-ttu-id="13e2b-116">Hello-XML-элемент указывает имя hello hello метаданных для большого двоичного объекта hello и его значение указывает значение параметра метаданных hello hello.</span><span class="sxs-lookup"><span data-stu-id="13e2b-116">hello XML element specifies hello name of hello metadata for hello blob, and its value specifies hello value of hello metadata setting.</span></span>|  
  
## <a name="properties-file-format"></a><span data-ttu-id="13e2b-117">Формат файла свойств</span><span class="sxs-lookup"><span data-stu-id="13e2b-117">Properties file format</span></span>  
<span data-ttu-id="13e2b-118">Hello файл свойств имеет следующий формат:</span><span class="sxs-lookup"><span data-stu-id="13e2b-118">hello format of a properties file is as follows:</span></span>  
  
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
  
|<span data-ttu-id="13e2b-119">XML-элемент</span><span class="sxs-lookup"><span data-stu-id="13e2b-119">XML Element</span></span>|<span data-ttu-id="13e2b-120">Тип</span><span class="sxs-lookup"><span data-stu-id="13e2b-120">Type</span></span>|<span data-ttu-id="13e2b-121">Описание</span><span class="sxs-lookup"><span data-stu-id="13e2b-121">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Properties`|<span data-ttu-id="13e2b-122">Корневой элемент</span><span class="sxs-lookup"><span data-stu-id="13e2b-122">Root element</span></span>|<span data-ttu-id="13e2b-123">корневой элемент файла свойств hello Hello.</span><span class="sxs-lookup"><span data-stu-id="13e2b-123">hello root element of hello properties file.</span></span>|  
|`Last-Modified`|<span data-ttu-id="13e2b-124">Строка</span><span class="sxs-lookup"><span data-stu-id="13e2b-124">String</span></span>|<span data-ttu-id="13e2b-125">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="13e2b-125">Optional.</span></span> <span data-ttu-id="13e2b-126">Hello время последнего изменения для hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="13e2b-126">hello last-modified time for hello blob.</span></span> <span data-ttu-id="13e2b-127">Только для заданий экспорта.</span><span class="sxs-lookup"><span data-stu-id="13e2b-127">For export jobs only.</span></span>|  
|`Etag`|<span data-ttu-id="13e2b-128">Строка</span><span class="sxs-lookup"><span data-stu-id="13e2b-128">String</span></span>|<span data-ttu-id="13e2b-129">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="13e2b-129">Optional.</span></span> <span data-ttu-id="13e2b-130">Здравствуйте, значение ETag большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="13e2b-130">hello blob's ETag value.</span></span> <span data-ttu-id="13e2b-131">Только для заданий экспорта.</span><span class="sxs-lookup"><span data-stu-id="13e2b-131">For export jobs only.</span></span>|  
|`Content-Length`|<span data-ttu-id="13e2b-132">Строка</span><span class="sxs-lookup"><span data-stu-id="13e2b-132">String</span></span>|<span data-ttu-id="13e2b-133">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="13e2b-133">Optional.</span></span> <span data-ttu-id="13e2b-134">размер Hello hello большого двоичного объекта в байтах.</span><span class="sxs-lookup"><span data-stu-id="13e2b-134">hello size of hello blob in bytes.</span></span> <span data-ttu-id="13e2b-135">Только для заданий экспорта.</span><span class="sxs-lookup"><span data-stu-id="13e2b-135">For export jobs only.</span></span>|  
|`Content-Type`|<span data-ttu-id="13e2b-136">Строка</span><span class="sxs-lookup"><span data-stu-id="13e2b-136">String</span></span>|<span data-ttu-id="13e2b-137">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="13e2b-137">Optional.</span></span> <span data-ttu-id="13e2b-138">Тип содержимого Hello hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="13e2b-138">hello content type of hello blob.</span></span>|  
|`Content-MD5`|<span data-ttu-id="13e2b-139">Строка</span><span class="sxs-lookup"><span data-stu-id="13e2b-139">String</span></span>|<span data-ttu-id="13e2b-140">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="13e2b-140">Optional.</span></span> <span data-ttu-id="13e2b-141">Здравствуйте хэш MD5 большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="13e2b-141">hello blob's MD5 hash.</span></span>|  
|`Content-Encoding`|<span data-ttu-id="13e2b-142">Строка</span><span class="sxs-lookup"><span data-stu-id="13e2b-142">String</span></span>|<span data-ttu-id="13e2b-143">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="13e2b-143">Optional.</span></span> <span data-ttu-id="13e2b-144">Здравствуйте, содержимое большого двоичного объекта кодирования.</span><span class="sxs-lookup"><span data-stu-id="13e2b-144">hello blob's content encoding.</span></span>|  
|`Content-Language`|<span data-ttu-id="13e2b-145">Строка</span><span class="sxs-lookup"><span data-stu-id="13e2b-145">String</span></span>|<span data-ttu-id="13e2b-146">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="13e2b-146">Optional.</span></span> <span data-ttu-id="13e2b-147">Здравствуйте, язык содержимого большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="13e2b-147">hello blob's content language.</span></span>|  
|`Cache-Control`|<span data-ttu-id="13e2b-148">Строка</span><span class="sxs-lookup"><span data-stu-id="13e2b-148">String</span></span>|<span data-ttu-id="13e2b-149">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="13e2b-149">Optional.</span></span> <span data-ttu-id="13e2b-150">Hello строку управления кэшем для большого двоичного объекта hello.</span><span class="sxs-lookup"><span data-stu-id="13e2b-150">hello cache control string for hello blob.</span></span>|  

## <a name="next-steps"></a><span data-ttu-id="13e2b-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="13e2b-151">Next steps</span></span>

<span data-ttu-id="13e2b-152">Дополнительные правила настройки свойств и метаданных больших двоичных объектов см. в статьях [Set Blob Properties](/rest/api/storageservices/set-blob-properties) (Задание свойств большого двоичного объекта), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata) (Задание метаданных большого двоичного объекта) и [Setting and Retrieving Properties and Metadata for Blob Resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) (Задание и получение свойств и метаданных для ресурсов больших двоичных объектов).</span><span class="sxs-lookup"><span data-stu-id="13e2b-152">See [Set blob properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span></span>
