---
title: "Задание - v1 импорта aaaSample рабочего процесса tooprep жестких дисков для импорта и экспорта Azure | Документы Microsoft"
description: "См. пошаговое руководство для hello завершения процесса подготовки дисков для задания импорта в hello службы импорта и экспорта Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 6eb1b1b7-c69f-4365-b5ef-3cd5e05eb72a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: eb77831a88c16c14838179a6432ddb06503067dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="ce2ed-103">Образец рабочего процесса tooprepare жесткие диски для задания импорта</span><span class="sxs-lookup"><span data-stu-id="ce2ed-103">Sample workflow tooprepare hard drives for an import job</span></span>
<span data-ttu-id="ce2ed-104">В этом разделе рассматриваются hello полный процесс подготовки дисков для задания импорта.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-104">This topic walks you through hello complete process of preparing drives for an import job.</span></span>  
  
<span data-ttu-id="ce2ed-105">В этом примере импортируются следующие данные в учетной записи хранилища Windows Azure с именем hello `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="ce2ed-105">This example imports hello following data into a Window Azure storage account named `mystorageaccount`:</span></span>  
  
|<span data-ttu-id="ce2ed-106">Расположение</span><span class="sxs-lookup"><span data-stu-id="ce2ed-106">Location</span></span>|<span data-ttu-id="ce2ed-107">Описание</span><span class="sxs-lookup"><span data-stu-id="ce2ed-107">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="ce2ed-108">H:\Video</span><span class="sxs-lookup"><span data-stu-id="ce2ed-108">H:\Video</span></span>|<span data-ttu-id="ce2ed-109">Коллекция видео, общий размер которой составляет 5 ТБ.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-109">A collection of videos, 5 TB in total.</span></span>|  
|<span data-ttu-id="ce2ed-110">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="ce2ed-110">H:\Photo</span></span>|<span data-ttu-id="ce2ed-111">Коллекция фотографий, общий размер которой составляет 30 ГБ.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-111">A collection of photos, 30 GB in total.</span></span>|  
|<span data-ttu-id="ce2ed-112">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="ce2ed-112">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="ce2ed-113">Образ диска Blu-Ray™, размер которого составляет 25 ГБ.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-113">A Blu-Ray™ disk image, 25 GB.</span></span>|  
|<span data-ttu-id="ce2ed-114">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="ce2ed-114">\\\bigshare\john\music</span></span>|<span data-ttu-id="ce2ed-115">Коллекция музыкальных файлов в сетевой папке, общий размер которой составляет 10 ГБ.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-115">A collection of music files on a network share, 10 GB in total.</span></span>|  
  
<span data-ttu-id="ce2ed-116">Задание импорта Hello импортирует эти данные в следующие назначения в учетной записи хранения hello hello:</span><span class="sxs-lookup"><span data-stu-id="ce2ed-116">hello import job imports this data into hello following destinations in hello storage account:</span></span>  
  
|<span data-ttu-id="ce2ed-117">Источник</span><span class="sxs-lookup"><span data-stu-id="ce2ed-117">Source</span></span>|<span data-ttu-id="ce2ed-118">Целевой виртуальный каталог или большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-118">Destination virtual directory or blob</span></span>|  
|------------|-------------------------------------------|  
|<span data-ttu-id="ce2ed-119">H:\Video</span><span class="sxs-lookup"><span data-stu-id="ce2ed-119">H:\Video</span></span>|<span data-ttu-id="ce2ed-120">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="ce2ed-120">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="ce2ed-121">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="ce2ed-121">H:\Photo</span></span>|<span data-ttu-id="ce2ed-122">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="ce2ed-122">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="ce2ed-123">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="ce2ed-123">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="ce2ed-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="ce2ed-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="ce2ed-125">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="ce2ed-125">\\\bigshare\john\music</span></span>|<span data-ttu-id="ce2ed-126">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="ce2ed-126">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
<span data-ttu-id="ce2ed-127">В этом сопоставлении hello файл `H:\Video\Drama\GreatMovie.mov` — большой двоичный объект импортированных toohello `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-127">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` is imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>  
  
<span data-ttu-id="ce2ed-128">Далее, toodetermine требуются сколько жестких дисков, размер hello вычислений hello данных:</span><span class="sxs-lookup"><span data-stu-id="ce2ed-128">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
<span data-ttu-id="ce2ed-129">Для нашего примера будет достаточно двух жестких дисков объемом 3 ТБ каждый.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-129">For this example, two 3-TB hard drives should be sufficient.</span></span> <span data-ttu-id="ce2ed-130">Однако, поскольку исходный каталог hello `H:\Video` содержит 5 ТБ данных, а емкость вашей одного жесткого диска составляет всего 3 ТБ, это необходимые toobreak `H:\Video` на два каталога меньшего размера: `H:\Video1` и `H:\Video2`, прежде чем выполнение hello Microsoft Средство импорта и экспорта Azure.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-130">However, since hello source directory `H:\Video` has 5 TB of data and your single hard drive's capacity is only 3 TB, it's necessary toobreak `H:\Video` into two smaller directories: `H:\Video1` and `H:\Video2`, before running hello Microsoft Azure Import/Export Tool.</span></span> <span data-ttu-id="ce2ed-131">Этот шаг создает следующие исходные каталоги hello:</span><span class="sxs-lookup"><span data-stu-id="ce2ed-131">This step yields hello following source directories:</span></span>  
  
|<span data-ttu-id="ce2ed-132">Расположение</span><span class="sxs-lookup"><span data-stu-id="ce2ed-132">Location</span></span>|<span data-ttu-id="ce2ed-133">Размер</span><span class="sxs-lookup"><span data-stu-id="ce2ed-133">Size</span></span>|<span data-ttu-id="ce2ed-134">Целевой виртуальный каталог или большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-134">Destination virtual directory or blob</span></span>|  
|--------------|----------|-------------------------------------------|  
|<span data-ttu-id="ce2ed-135">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="ce2ed-135">H:\Video1</span></span>|<span data-ttu-id="ce2ed-136">2,5 TБ</span><span class="sxs-lookup"><span data-stu-id="ce2ed-136">2.5 TB</span></span>|<span data-ttu-id="ce2ed-137">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="ce2ed-137">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="ce2ed-138">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="ce2ed-138">H:\Video2</span></span>|<span data-ttu-id="ce2ed-139">2,5 TБ</span><span class="sxs-lookup"><span data-stu-id="ce2ed-139">2.5 TB</span></span>|<span data-ttu-id="ce2ed-140">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="ce2ed-140">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="ce2ed-141">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="ce2ed-141">H:\Photo</span></span>|<span data-ttu-id="ce2ed-142">30 ГБ</span><span class="sxs-lookup"><span data-stu-id="ce2ed-142">30 GB</span></span>|<span data-ttu-id="ce2ed-143">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="ce2ed-143">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="ce2ed-144">K:\Temp\FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="ce2ed-144">K:\Temp\FavoriteMovies.ISO</span></span>|<span data-ttu-id="ce2ed-145">25 ГБ</span><span class="sxs-lookup"><span data-stu-id="ce2ed-145">25 GB</span></span>|<span data-ttu-id="ce2ed-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="ce2ed-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="ce2ed-147">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="ce2ed-147">\\\bigshare\john\music</span></span>|<span data-ttu-id="ce2ed-148">10 ГБ</span><span class="sxs-lookup"><span data-stu-id="ce2ed-148">10 GB</span></span>|<span data-ttu-id="ce2ed-149">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="ce2ed-149">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
 <span data-ttu-id="ce2ed-150">Здравствуйте, даже если `H:\Video`каталог разбит tootwo каталогов, они указывают toohello один целевой виртуальный каталог в учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-150">Even though hello `H:\Video`directory has been split tootwo directories, they point toohello same destination virtual directory in hello storage account.</span></span> <span data-ttu-id="ce2ed-151">Таким образом, все видеофайлы содержатся в одном `video` контейнера в учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-151">This way, all video files are maintained under a single `video` container in hello storage account.</span></span>  
  
 <span data-ttu-id="ce2ed-152">Затем hello предыдущих исходных каталогов — равномерно распределенные toohello два жестких диска.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-152">Next, hello previous source directories are evenly distributed toohello two hard drives:</span></span>  
  
||||  
|-|-|-|  
|<span data-ttu-id="ce2ed-153">Жесткий диск</span><span class="sxs-lookup"><span data-stu-id="ce2ed-153">Hard drive</span></span>|<span data-ttu-id="ce2ed-154">Исходные каталоги</span><span class="sxs-lookup"><span data-stu-id="ce2ed-154">Source directories</span></span>|<span data-ttu-id="ce2ed-155">Общий размер</span><span class="sxs-lookup"><span data-stu-id="ce2ed-155">Total size</span></span>|  
|<span data-ttu-id="ce2ed-156">Первый диск</span><span class="sxs-lookup"><span data-stu-id="ce2ed-156">First Drive</span></span>|<span data-ttu-id="ce2ed-157">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="ce2ed-157">H:\Video1</span></span>|<span data-ttu-id="ce2ed-158">2,5 ТБ + 30 ГБ</span><span class="sxs-lookup"><span data-stu-id="ce2ed-158">2.5 TB + 30 GB</span></span>|  
||<span data-ttu-id="ce2ed-159">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="ce2ed-159">H:\Photo</span></span>||  
|<span data-ttu-id="ce2ed-160">Второй диск</span><span class="sxs-lookup"><span data-stu-id="ce2ed-160">Second Drive</span></span>|<span data-ttu-id="ce2ed-161">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="ce2ed-161">H:\Video2</span></span>|<span data-ttu-id="ce2ed-162">2,5 ТБ + 35 ГБ</span><span class="sxs-lookup"><span data-stu-id="ce2ed-162">2.5 TB + 35 GB</span></span>|  
||<span data-ttu-id="ce2ed-163">K:\Temp\BlueRay.ISO</span><span class="sxs-lookup"><span data-stu-id="ce2ed-163">K:\Temp\BlueRay.ISO</span></span>||  
||<span data-ttu-id="ce2ed-164">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="ce2ed-164">\\\bigshare\john\music</span></span>||  
  
<span data-ttu-id="ce2ed-165">Кроме того можно задать следующие метаданные для всех файлов hello.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-165">In addition, you can set hello following metadata for all files:</span></span>  
  
-   <span data-ttu-id="ce2ed-166">**UploadMethod:** Microsoft Azure Import/Export service</span><span class="sxs-lookup"><span data-stu-id="ce2ed-166">**UploadMethod:** Windows Azure Import/Export service</span></span>  
  
-   <span data-ttu-id="ce2ed-167">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="ce2ed-167">**DataSetName:** SampleData</span></span>  
  
-   <span data-ttu-id="ce2ed-168">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="ce2ed-168">**CreationDate:** 10/1/2013</span></span>  
  
<span data-ttu-id="ce2ed-169">метаданные tooset hello импорта файлов, создайте текстовый файл, `c:\WAImportExport\SampleMetadata.txt`, с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="ce2ed-169">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="ce2ed-170">Можно также задать некоторые свойства для hello `FavoriteMovie.ISO` больших двоичных объектов:</span><span class="sxs-lookup"><span data-stu-id="ce2ed-170">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>  
  
-   <span data-ttu-id="ce2ed-171">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="ce2ed-171">**Content-Type:** application/octet-stream</span></span>  
  
-   <span data-ttu-id="ce2ed-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="ce2ed-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>  
  
-   <span data-ttu-id="ce2ed-173">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="ce2ed-173">**Cache-Control:** no-cache</span></span>  
  
<span data-ttu-id="ce2ed-174">tooset эти свойства, создайте текстовый файл, `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="ce2ed-174">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="ce2ed-175">Теперь все готово toorun hello средство импорта и экспорта Azure tooprepare hello два жестких диска.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-175">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span> <span data-ttu-id="ce2ed-176">Обратите внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-176">Note that:</span></span>  
  
-   <span data-ttu-id="ce2ed-177">Hello первый диск подключается как диск X.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-177">hello first drive is mounted as drive X.</span></span>  
  
-   <span data-ttu-id="ce2ed-178">Hello второй диск подключается как диск Y.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-178">hello second drive is mounted as drive Y.</span></span>  
  
-   <span data-ttu-id="ce2ed-179">Hello ключ учетной записи хранения hello `mystorageaccount` — `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-179">hello key for hello storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span></span>  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a><span data-ttu-id="ce2ed-180">Подготовка диска для импорта, когда данные предварительно загружены</span><span class="sxs-lookup"><span data-stu-id="ce2ed-180">Preparing disk for import when data is pre-loaded</span></span>
 
 <span data-ttu-id="ce2ed-181">Если импортировать toobe данных hello уже существует на диске hello, используйте флаг /skipwrite hello.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-181">If hello data toobe imported is already present on hello disk, use hello flag /skipwrite.</span></span> <span data-ttu-id="ce2ed-182">значение Hello/t и /srcdir должны оба диска точки toohello подготовлено для импорта.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-182">hello value of /t and /srcdir should both point toohello disk being prepared for import.</span></span> <span data-ttu-id="ce2ed-183">Если все импортированные toobe данных hello не будет toohello же целевой виртуальный каталог или корневой учетной записи хранения hello, выполнения hello же отдельно, команды для каждой целевой каталог указывать значение hello /id hello же между запусками все.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-183">If all of hello data toobe imported is not going toohello same destination virtual directory or root of hello storage account, run hello same command for each destination directory separately, keeping hello value of /id hello same across all runs.</span></span>

>[!NOTE] 
><span data-ttu-id="ce2ed-184">Не указывайте параметр/Format, как он будет очистить hello данные на диске hello.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-184">Do not specify /format as it will wipe hello data on hello disk.</span></span> <span data-ttu-id="ce2ed-185">Можно указать / шифрования или /bk в зависимости от того, было ли hello диск уже зашифрован или нет.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-185">You can specify /encrypt or /bk depending on whether hello disk is already encrypted or not.</span></span> 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a><span data-ttu-id="ce2ed-186">Сеансы копирования — первый диск</span><span class="sxs-lookup"><span data-stu-id="ce2ed-186">Copy sessions - first drive</span></span>

<span data-ttu-id="ce2ed-187">Первый диск hello запустите hello средство импорта и экспорта Azure дважды hello toocopy два источника каталоги:</span><span class="sxs-lookup"><span data-stu-id="ce2ed-187">For hello first drive, run hello Azure Import/Export Tool twice toocopy hello two source directories:</span></span>  

<span data-ttu-id="ce2ed-188">**Первый сеанс копирования**</span><span class="sxs-lookup"><span data-stu-id="ce2ed-188">**First copy session**</span></span>
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

<span data-ttu-id="ce2ed-189">**Второй сеанс копирования**</span><span class="sxs-lookup"><span data-stu-id="ce2ed-189">**Second copy session**</span></span>

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a><span data-ttu-id="ce2ed-190">Сеансы копирования — второй диск</span><span class="sxs-lookup"><span data-stu-id="ce2ed-190">Copy sessions - second drive</span></span>
 
<span data-ttu-id="ce2ed-191">Для hello второго диска запустите hello средство импорта и экспорта Azure три раза, после каждого hello исходные каталоги и один раз для автономного hello Blu-Ray™ файл изображения):</span><span class="sxs-lookup"><span data-stu-id="ce2ed-191">For hello second drive, run hello Azure Import/Export Tool three times, once each for hello source directories, and once for hello standalone Blu-Ray™ image file):</span></span>  
  
<span data-ttu-id="ce2ed-192">**Первый сеанс копирования**</span><span class="sxs-lookup"><span data-stu-id="ce2ed-192">**First copy session**</span></span> 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
<span data-ttu-id="ce2ed-193">**Второй сеанс копирования**</span><span class="sxs-lookup"><span data-stu-id="ce2ed-193">**Second copy session**</span></span>

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
<span data-ttu-id="ce2ed-194">**Третий сеанс копирования**</span><span class="sxs-lookup"><span data-stu-id="ce2ed-194">**Third copy session**</span></span>  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a><span data-ttu-id="ce2ed-195">Завершение сеанса копирования</span><span class="sxs-lookup"><span data-stu-id="ce2ed-195">Copy session completion</span></span>

<span data-ttu-id="ce2ed-196">После завершения сеансов копирования hello можно отключиться от компьютера копирования hello hello двух дисков и их отправке toohello соответствующий центр данных Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="ce2ed-196">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Windows Azure data center.</span></span> <span data-ttu-id="ce2ed-197">Отправка hello двух файлов журнала, `FirstDrive.jrn` и `SecondDrive.jrn`, при создании задания импорта hello в hello [портал Windows Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="ce2ed-197">Upload hello two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create hello import job in hello [Windows Azure portal](https://manage.windowsazure.com/).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="ce2ed-198">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ce2ed-198">Next steps</span></span>

* [<span data-ttu-id="ce2ed-199">Подготовка жестких дисков для задания импорта</span><span class="sxs-lookup"><span data-stu-id="ce2ed-199">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="ce2ed-200">Краткий справочник по часто используемым командам</span><span class="sxs-lookup"><span data-stu-id="ce2ed-200">Quick reference for frequently used commands</span></span>](../storage-import-export-tool-quick-reference-v1.md) 
