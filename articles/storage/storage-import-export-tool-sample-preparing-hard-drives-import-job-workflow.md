---
title: "Задание импорта aaaSample рабочего процесса tooprep жестких дисков для импорта и экспорта Azure | Документы Microsoft"
description: "См. пошаговое руководство для hello завершения процесса подготовки дисков для задания импорта в hello службы импорта и экспорта Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: muralikk
ms.openlocfilehash: 560220b7dc9f87416f1fec1ff30fa5cd65812ce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="2f460-103">Образец рабочего процесса tooprepare жесткие диски для задания импорта</span><span class="sxs-lookup"><span data-stu-id="2f460-103">Sample workflow tooprepare hard drives for an import job</span></span>

<span data-ttu-id="2f460-104">В этой статье рассматриваются hello полный процесс подготовки дисков для задания импорта.</span><span class="sxs-lookup"><span data-stu-id="2f460-104">This article walks you through hello complete process of preparing drives for an import job.</span></span>

## <a name="sample-data"></a><span data-ttu-id="2f460-105">Пример данных</span><span class="sxs-lookup"><span data-stu-id="2f460-105">Sample data</span></span>

<span data-ttu-id="2f460-106">В этом примере импортируются следующие данные в учетную запись хранилища Azure с именем hello `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="2f460-106">This example imports hello following data into an Azure storage account named `mystorageaccount`:</span></span>

|<span data-ttu-id="2f460-107">Расположение</span><span class="sxs-lookup"><span data-stu-id="2f460-107">Location</span></span>|<span data-ttu-id="2f460-108">Описание</span><span class="sxs-lookup"><span data-stu-id="2f460-108">Description</span></span>|<span data-ttu-id="2f460-109">Размер данных</span><span class="sxs-lookup"><span data-stu-id="2f460-109">Data size</span></span>|
|--------------|-----------------|-----|
|<span data-ttu-id="2f460-110">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="2f460-110">H:\Video\\</span></span> |<span data-ttu-id="2f460-111">Коллекция видео.</span><span class="sxs-lookup"><span data-stu-id="2f460-111">A collection of videos</span></span>|<span data-ttu-id="2f460-112">12 ТБ</span><span class="sxs-lookup"><span data-stu-id="2f460-112">12 TB</span></span>|
|<span data-ttu-id="2f460-113">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="2f460-113">H:\Photo\\</span></span> |<span data-ttu-id="2f460-114">Коллекция фотографий.</span><span class="sxs-lookup"><span data-stu-id="2f460-114">A collection of photos</span></span>|<span data-ttu-id="2f460-115">30 ГБ</span><span class="sxs-lookup"><span data-stu-id="2f460-115">30 GB</span></span>|
|<span data-ttu-id="2f460-116">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="2f460-116">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="2f460-117">Образ диска Blu-Ray™.</span><span class="sxs-lookup"><span data-stu-id="2f460-117">A Blu-Ray™ disk image</span></span>|<span data-ttu-id="2f460-118">25 ГБ</span><span class="sxs-lookup"><span data-stu-id="2f460-118">25 GB</span></span>|
|<span data-ttu-id="2f460-119">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="2f460-119">\\\bigshare\john\music\\</span></span>|<span data-ttu-id="2f460-120">Коллекция музыкальных файлов в сетевой папке.</span><span class="sxs-lookup"><span data-stu-id="2f460-120">A collection of music files on a network share</span></span>|<span data-ttu-id="2f460-121">10 ГБ</span><span class="sxs-lookup"><span data-stu-id="2f460-121">10 GB</span></span>|

## <a name="storage-account-destinations"></a><span data-ttu-id="2f460-122">Целевые каталоги в учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="2f460-122">Storage account destinations</span></span>

<span data-ttu-id="2f460-123">Задание Hello импортирует hello данных в следующие назначения в учетной записи хранения hello hello:</span><span class="sxs-lookup"><span data-stu-id="2f460-123">hello import job will import hello data into hello following destinations in hello storage account:</span></span>

|<span data-ttu-id="2f460-124">Источник</span><span class="sxs-lookup"><span data-stu-id="2f460-124">Source</span></span>|<span data-ttu-id="2f460-125">Целевой виртуальный каталог или большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="2f460-125">Destination virtual directory or blob</span></span>|
|------------|-------------------------------------------|
|<span data-ttu-id="2f460-126">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="2f460-126">H:\Video\\</span></span> |<span data-ttu-id="2f460-127">video/</span><span class="sxs-lookup"><span data-stu-id="2f460-127">video/</span></span>|
|<span data-ttu-id="2f460-128">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="2f460-128">H:\Photo\\</span></span> |<span data-ttu-id="2f460-129">photo/</span><span class="sxs-lookup"><span data-stu-id="2f460-129">photo/</span></span>|
|<span data-ttu-id="2f460-130">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="2f460-130">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="2f460-131">favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="2f460-131">favorite/FavoriteMovies.ISO</span></span>|
|<span data-ttu-id="2f460-132">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="2f460-132">\\\bigshare\john\music\\</span></span> |<span data-ttu-id="2f460-133">music</span><span class="sxs-lookup"><span data-stu-id="2f460-133">music</span></span>|

<span data-ttu-id="2f460-134">В этом сопоставлении hello файл `H:\Video\Drama\GreatMovie.mov` будет импортированных toohello большого двоичного объекта `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="2f460-134">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` will be imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>

## <a name="determine-hard-drive-requirements"></a><span data-ttu-id="2f460-135">Определение требований к жестким дискам</span><span class="sxs-lookup"><span data-stu-id="2f460-135">Determine hard drive requirements</span></span>

<span data-ttu-id="2f460-136">Далее, toodetermine требуются сколько жестких дисков, размер hello вычислений hello данных:</span><span class="sxs-lookup"><span data-stu-id="2f460-136">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

<span data-ttu-id="2f460-137">Для нашего примера будет достаточно двух жестких дисков объемом в 8 ТБ каждый.</span><span class="sxs-lookup"><span data-stu-id="2f460-137">For this example, two 8TB hard drives should be sufficient.</span></span> <span data-ttu-id="2f460-138">Однако, поскольку исходный каталог hello `H:\Video` содержит 12 ТБ данных, а емкость вашей одного жесткого диска составляет 8 ТБ, можно будет toospecify в hello следующие образом hello **driveset.csv** файла:</span><span class="sxs-lookup"><span data-stu-id="2f460-138">However, since hello source directory `H:\Video` has 12TB of data and your single hard drive's capacity is only 8TB, you will be able toospecify this in hello following way in hello **driveset.csv** file:</span></span>

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
<span data-ttu-id="2f460-139">Средство Hello будет распределить данные на два жестких диска оптимальным образом.</span><span class="sxs-lookup"><span data-stu-id="2f460-139">hello tool will distribute data across two hard drives in an optimized way.</span></span>

## <a name="attach-drives-and-configure-hello-job"></a><span data-ttu-id="2f460-140">Присоединение дисков и настроить задание hello</span><span class="sxs-lookup"><span data-stu-id="2f460-140">Attach drives and configure hello job</span></span>
<span data-ttu-id="2f460-141">Будет подключить оба машине toohello диски и создавать тома.</span><span class="sxs-lookup"><span data-stu-id="2f460-141">You will attach both disks toohello machine and create volumes.</span></span> <span data-ttu-id="2f460-142">Затем создайте файл **dataset.csv**:</span><span class="sxs-lookup"><span data-stu-id="2f460-142">Then author **dataset.csv** file:</span></span>
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

<span data-ttu-id="2f460-143">Кроме того можно задать следующие метаданные для всех файлов hello.</span><span class="sxs-lookup"><span data-stu-id="2f460-143">In addition, you can set hello following metadata for all files:</span></span>

* <span data-ttu-id="2f460-144">**UploadMethod:** Microsoft Azure Import/Export service</span><span class="sxs-lookup"><span data-stu-id="2f460-144">**UploadMethod:** Windows Azure Import/Export service</span></span>
* <span data-ttu-id="2f460-145">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="2f460-145">**DataSetName:** SampleData</span></span>
* <span data-ttu-id="2f460-146">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="2f460-146">**CreationDate:** 10/1/2013</span></span>

<span data-ttu-id="2f460-147">метаданные tooset hello импорта файлов, создайте текстовый файл, `c:\WAImportExport\SampleMetadata.txt`, с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="2f460-147">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="2f460-148">Можно также задать некоторые свойства для hello `FavoriteMovie.ISO` больших двоичных объектов:</span><span class="sxs-lookup"><span data-stu-id="2f460-148">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>

* <span data-ttu-id="2f460-149">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="2f460-149">**Content-Type:** application/octet-stream</span></span>
* <span data-ttu-id="2f460-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="2f460-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>
* <span data-ttu-id="2f460-151">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="2f460-151">**Cache-Control:** no-cache</span></span>

<span data-ttu-id="2f460-152">tooset эти свойства, создайте текстовый файл, `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="2f460-152">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a><span data-ttu-id="2f460-153">Hello выполнения средства импорта и экспорта Azure (WAImportExport.exe)</span><span class="sxs-lookup"><span data-stu-id="2f460-153">Run hello Azure Import/Export Tool (WAImportExport.exe)</span></span>

<span data-ttu-id="2f460-154">Теперь все готово toorun hello средство импорта и экспорта Azure tooprepare hello два жестких диска.</span><span class="sxs-lookup"><span data-stu-id="2f460-154">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span>

<span data-ttu-id="2f460-155">**Для hello первого сеанса:**</span><span class="sxs-lookup"><span data-stu-id="2f460-155">**For hello first session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

<span data-ttu-id="2f460-156">Если любые дополнительные данные, должен добавить toobe, создайте другой файл набора данных (формате Initialdataset).</span><span class="sxs-lookup"><span data-stu-id="2f460-156">If any more data needs toobe added, create another dataset file (same format as Initialdataset).</span></span>

<span data-ttu-id="2f460-157">**Для hello второй сеанс:**</span><span class="sxs-lookup"><span data-stu-id="2f460-157">**For hello second session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

<span data-ttu-id="2f460-158">После завершения сеансов копирования hello можно отключиться от компьютера копирования hello hello двух дисков и их отправке toohello соответствующий ЦОД Azure.</span><span class="sxs-lookup"><span data-stu-id="2f460-158">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Azure data center.</span></span> <span data-ttu-id="2f460-159">Вы отправите hello двух файлов журнала, `<FirstDriveSerialNumber>.xml` и `<SecondDriveSerialNumber>.xml`при создании задания импорта hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2f460-159">You'll upload hello two journal files, `<FirstDriveSerialNumber>.xml` and `<SecondDriveSerialNumber>.xml`, when you create hello import job in hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f460-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2f460-160">Next steps</span></span>

* [<span data-ttu-id="2f460-161">Подготовка жестких дисков для задания импорта</span><span class="sxs-lookup"><span data-stu-id="2f460-161">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="2f460-162">Краткий справочник по часто используемым командам</span><span class="sxs-lookup"><span data-stu-id="2f460-162">Quick reference for frequently used commands</span></span>](storage-import-export-tool-quick-reference.md)
