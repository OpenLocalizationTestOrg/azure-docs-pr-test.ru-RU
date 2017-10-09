---
title: "Использование aaaPreviewing дисков для задания экспорта импорта и экспорта Azure - v1 | Документы Microsoft"
description: "Узнайте, как toopreview hello список больших двоичных объектов, выбранных для задания экспорта службы импорта и экспорта Azure hello."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 7707d744-7ec7-4de8-ac9b-93a18608dc9a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 7378c159f6d11702cda9ae7654e84d85f9b671b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a><span data-ttu-id="4e4a1-103">Предварительный просмотр использования дисков для задания экспорта</span><span class="sxs-lookup"><span data-stu-id="4e4a1-103">Previewing drive usage for an export job</span></span>
<span data-ttu-id="4e4a1-104">Прежде чем создать задание экспорта, необходимо экспортировать набор больших двоичных объектов toobe toochoose.</span><span class="sxs-lookup"><span data-stu-id="4e4a1-104">Before you create an export job, you need toochoose a set of blobs toobe exported.</span></span> <span data-ttu-id="4e4a1-105">Hello службы импорта и экспорта Microsoft Azure позволяет toouse список путей больших двоичных объектов или toorepresent hello большие двоичные объекты, выбранные префиксов больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="4e4a1-105">hello Microsoft Azure Import/Export service allows you toouse a list of blob paths or blob prefixes toorepresent hello blobs you've selected.</span></span>  
  
<span data-ttu-id="4e4a1-106">Далее необходимо toodetermine сколько дисков необходимо toosend.</span><span class="sxs-lookup"><span data-stu-id="4e4a1-106">Next, you need toodetermine how many drives you need toosend.</span></span> <span data-ttu-id="4e4a1-107">Средство импорта и экспорта Hello предоставляет hello `PreviewExport` выбран использования диска toopreview команды hello большие двоичные объекты, на основании размера hello hello дисков будет toouse.</span><span class="sxs-lookup"><span data-stu-id="4e4a1-107">hello Import/Export Tool provides hello `PreviewExport` command toopreview drive usage for hello blobs you selected, based on hello size of hello drives you are going toouse.</span></span>

## <a name="command-line-parameters"></a><span data-ttu-id="4e4a1-108">Параметры командной строки</span><span class="sxs-lookup"><span data-stu-id="4e4a1-108">Command-line parameters</span></span>

<span data-ttu-id="4e4a1-109">Можно использовать следующие параметры при использовании hello hello `PreviewExport` команде hello средство импорта и экспорта.</span><span class="sxs-lookup"><span data-stu-id="4e4a1-109">You can use hello following parameters when using hello `PreviewExport` command of hello Import/Export Tool.</span></span>

|<span data-ttu-id="4e4a1-110">Параметр командной строки</span><span class="sxs-lookup"><span data-stu-id="4e4a1-110">Command-line parameter</span></span>|<span data-ttu-id="4e4a1-111">Описание</span><span class="sxs-lookup"><span data-stu-id="4e4a1-111">Description</span></span>|  
|--------------------------|-----------------|  
|<span data-ttu-id="4e4a1-112">**/logdir:**<каталог_журнала\></span><span class="sxs-lookup"><span data-stu-id="4e4a1-112">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="4e4a1-113">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="4e4a1-113">Optional.</span></span> <span data-ttu-id="4e4a1-114">каталог журнала Hello.</span><span class="sxs-lookup"><span data-stu-id="4e4a1-114">hello log directory.</span></span> <span data-ttu-id="4e4a1-115">Подробные журналы будут записаны toothis каталога.</span><span class="sxs-lookup"><span data-stu-id="4e4a1-115">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="4e4a1-116">Если журнал каталога не указан, текущий каталог hello будет использоваться как каталог журнала hello.</span><span class="sxs-lookup"><span data-stu-id="4e4a1-116">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="4e4a1-117">**/sn:**<StorageAccountName\></span><span class="sxs-lookup"><span data-stu-id="4e4a1-117">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="4e4a1-118">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="4e4a1-118">Required.</span></span> <span data-ttu-id="4e4a1-119">Задание экспорта Hello имя учетной записи хранения hello hello.</span><span class="sxs-lookup"><span data-stu-id="4e4a1-119">hello name of hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="4e4a1-120">**/sk:**<ключ_учетной_записи_хранения\></span><span class="sxs-lookup"><span data-stu-id="4e4a1-120">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="4e4a1-121">Требуется, только если не указан SAS контейнера.</span><span class="sxs-lookup"><span data-stu-id="4e4a1-121">Required if and only if a container SAS is not specified.</span></span> <span data-ttu-id="4e4a1-122">Задание экспорта Hello ключ учетной записи хранилища hello для hello.</span><span class="sxs-lookup"><span data-stu-id="4e4a1-122">hello account key for hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="4e4a1-123">**/csas:**<SAS_контейнера\></span><span class="sxs-lookup"><span data-stu-id="4e4a1-123">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="4e4a1-124">Требуется, только если не указан ключ учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="4e4a1-124">Required if and only if a storage account key is not specified.</span></span> <span data-ttu-id="4e4a1-125">Hello контейнер SAS для больших двоичных объектов toobe листинг hello экспортируются в задании экспорта hello.</span><span class="sxs-lookup"><span data-stu-id="4e4a1-125">hello container SAS for listing hello blobs toobe exported in hello export job.</span></span>|  
|<span data-ttu-id="4e4a1-126">**/ExportBlobListFile:**<файл_списка_больших_двоичных_объектов_экспорта\></span><span class="sxs-lookup"><span data-stu-id="4e4a1-126">**/ExportBlobListFile:**<ExportBlobListFile\></span></span>|<span data-ttu-id="4e4a1-127">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="4e4a1-127">Required.</span></span> <span data-ttu-id="4e4a1-128">Путь toohello XML файлу, содержащему список путей больших двоичных объектов или префиксов для экспорта toobe большие двоичные объекты hello.</span><span class="sxs-lookup"><span data-stu-id="4e4a1-128">Path toohello XML file containing list of blob paths or blob path prefixes for hello blobs toobe exported.</span></span> <span data-ttu-id="4e4a1-129">формат файла Hello, используемый в hello `BlobListBlobPath` элемент в hello [вставки задания](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) работы hello REST API службы импорта и экспорта.</span><span class="sxs-lookup"><span data-stu-id="4e4a1-129">hello file format used in hello `BlobListBlobPath` element in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation of hello Import/Export service REST API.</span></span>|  
|<span data-ttu-id="4e4a1-130">**/DriveSize:**<размер_диска\></span><span class="sxs-lookup"><span data-stu-id="4e4a1-130">**/DriveSize:**<DriveSize\></span></span>|<span data-ttu-id="4e4a1-131">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="4e4a1-131">Required.</span></span> <span data-ttu-id="4e4a1-132">Здравствуйте, размер toouse дисков для задания экспорта, *например*, 500 ГБ, 1,5 ТБ.</span><span class="sxs-lookup"><span data-stu-id="4e4a1-132">hello size of drives toouse for an export job, *e.g.*, 500GB, 1.5TB.</span></span>|  

## <a name="command-line-example"></a><span data-ttu-id="4e4a1-133">Пример для командной строки</span><span class="sxs-lookup"><span data-stu-id="4e4a1-133">Command-line example</span></span>

<span data-ttu-id="4e4a1-134">Hello ниже приведен пример hello `PreviewExport` команды:</span><span class="sxs-lookup"><span data-stu-id="4e4a1-134">hello following example demonstrates hello `PreviewExport` command:</span></span>  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
<span data-ttu-id="4e4a1-135">Hello списка больших двоичных может содержать имена и префиксы больших двоичных объектов, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="4e4a1-135">hello export blob list file may contain blob names and blob prefixes, as shown here:</span></span>  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

<span data-ttu-id="4e4a1-136">списки средство импорта и экспорта Azure Hello toobe все большие двоичные объекты экспортированы и вычисляет, как их на диски hello указанный размер с учетом любых издержек, а затем определяет hello количество дисков toopack необходимые toohold hello больших двоичных объектов и использования диска сведения.</span><span class="sxs-lookup"><span data-stu-id="4e4a1-136">hello Azure Import/Export Tool lists all blobs toobe exported and calculates how toopack them into drives of hello specified size, taking into account any necessary overhead, then estimates hello number of drives needed toohold hello blobs and drive usage information.</span></span>  
  
<span data-ttu-id="4e4a1-137">Ниже приведен пример выходных данных hello, с опущены все информационные журналы:</span><span class="sxs-lookup"><span data-stu-id="4e4a1-137">Here is an example of hello output, with informational logs omitted:</span></span>  
  
```  
Number of unique blob paths/prefixes:   3  
Number of duplicate blob paths/prefixes:        0  
Number of nonexistent blob paths/prefixes:      1  
  
Drive size:     500.00 GB  
Number of blobs that can be exported:   6  
Number of blobs that cannot be exported:        2  
Number of drives needed:        3  
        Drive #1:       blobs = 1, occupied space = 454.74 GB  
        Drive #2:       blobs = 3, occupied space = 441.37 GB  
        Drive #3:       blobs = 2, occupied space = 131.28 GB    
```  
  
## <a name="next-steps"></a><span data-ttu-id="4e4a1-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4e4a1-138">Next steps</span></span>

* [<span data-ttu-id="4e4a1-139">Руководство по использованию инструмента импорта и экспорта</span><span class="sxs-lookup"><span data-stu-id="4e4a1-139">Azure Import/Export Tool reference</span></span>](../storage-import-export-tool-how-to-v1.md)
