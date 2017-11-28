---
title: "aaaSetting свойства и метаданные с помощью импорта и экспорта Azure - v1 | Документы Microsoft"
description: "Узнайте, как свойства и метаданные toobe toospecify задать на hello целевые большие двоичные объекты при запуске средства импорта и экспорта Azure tooprepare hello дисков. Это относится toov1 из hello средство импорта и экспорта."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: e8541695-bcfb-4bf0-84d9-72c9de32a0a8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 5b7b1c346ecde8a26d985bd5de7efcf7d86eb9e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a><span data-ttu-id="1a591-104">Настройка свойств и метаданных во время hello процессе импорта</span><span class="sxs-lookup"><span data-stu-id="1a591-104">Setting properties and metadata during hello import process</span></span>
<span data-ttu-id="1a591-105">При запуске средства импорта и экспорта Microsoft Azure tooprepare hello дисков можно указать свойства и метаданные toobe на hello целевых больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="1a591-105">When you run hello Microsoft Azure Import/Export Tool tooprepare your drives, you can specify properties and metadata toobe set on hello destination blobs.</span></span> <span data-ttu-id="1a591-106">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="1a591-106">Follow these steps:</span></span>  
  
1.  <span data-ttu-id="1a591-107">свойства большого двоичного объекта tooset, создайте текстовый файл на локальном компьютере, который определяет имена и значения свойств.</span><span class="sxs-lookup"><span data-stu-id="1a591-107">tooset blob properties, create a text file on your local computer that specifies property names and values.</span></span>  
  
2.  <span data-ttu-id="1a591-108">tooset метаданные больших двоичных объектов, создайте текстовый файл на локальном компьютере, который определяет имена и значения метаданных.</span><span class="sxs-lookup"><span data-stu-id="1a591-108">tooset blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>  
  
3.  <span data-ttu-id="1a591-109">Передайте полный путь tooone hello или оба эти файлы toohello средство импорта и экспорта Azure как часть hello `PrepImport` операции.</span><span class="sxs-lookup"><span data-stu-id="1a591-109">Pass hello full path tooone or both of these files toohello Azure Import/Export Tool as part of hello `PrepImport` operation.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="1a591-110">При указании файла свойств или метаданных в рамках сеанса копирования они задаются для каждого большого двоичного объекта, импортируемого в рамках этого сеанса копирования.</span><span class="sxs-lookup"><span data-stu-id="1a591-110">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="1a591-111">Если требуется toospecify набор свойств или метаданных для некоторых импортируемых больших двоичных объектов hello, вам потребуется toocreate отдельную скопировать сеанс работы с файлами различных свойств или метаданных.</span><span class="sxs-lookup"><span data-stu-id="1a591-111">If you want toospecify a different set of properties or metadata for some of hello blobs being imported, you'll need toocreate a separate copy session with different properties or metadata files.</span></span>  
  
## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="1a591-112">Указание свойств большого двоичного объекта в текстовом файле</span><span class="sxs-lookup"><span data-stu-id="1a591-112">Specify Blob Properties in a Text File</span></span>  
<span data-ttu-id="1a591-113">toospecify свойства большого двоичного объекта, создайте локальный текстовый файл и включите XML-ФАЙЛ, содержащий имена свойств в элементы и значения свойств в значениях.</span><span class="sxs-lookup"><span data-stu-id="1a591-113">toospecify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="1a591-114">Ниже приведен пример указания некоторых значений свойств.</span><span class="sxs-lookup"><span data-stu-id="1a591-114">Here's an example that specifies some property values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="1a591-115">Сохранить hello файл tooa папку, например `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="1a591-115">Save hello file tooa local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>  
  
## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="1a591-116">Указание метаданных большого двоичного объекта в текстовом файле</span><span class="sxs-lookup"><span data-stu-id="1a591-116">Specify Blob Metadata in a Text File</span></span>  
<span data-ttu-id="1a591-117">Аналогичным образом toospecify метаданные больших двоичных объектов, создайте локальный текстовый файл, содержащий имена метаданных как элементы и значения метаданных как значения.</span><span class="sxs-lookup"><span data-stu-id="1a591-117">Similarly, toospecify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="1a591-118">Ниже приведен пример указания некоторых значений метаданных.</span><span class="sxs-lookup"><span data-stu-id="1a591-118">Here's an example that specifies some metadata values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="1a591-119">Сохранить hello файл tooa папку, например `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="1a591-119">Save hello file tooa local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>  
  
## <a name="create-a-copy-session-including-hello-properties-or-metadata-files"></a><span data-ttu-id="1a591-120">Создать hello, включая сеанс копирования файлами свойств или метаданных</span><span class="sxs-lookup"><span data-stu-id="1a591-120">Create a Copy Session Including hello Properties or Metadata Files</span></span>  
<span data-ttu-id="1a591-121">При запуске средства импорта и экспорта Azure tooprepare hello hello-задания импорта укажите файл свойств hello в командной строке hello hello `PropertyFile` параметра.</span><span class="sxs-lookup"><span data-stu-id="1a591-121">When you run hello Azure Import/Export Tool tooprepare hello import job, specify hello properties file on hello command line using hello `PropertyFile` parameter.</span></span> <span data-ttu-id="1a591-122">Укажите файл метаданных hello в командной строке hello hello `/MetadataFile` параметра.</span><span class="sxs-lookup"><span data-stu-id="1a591-122">Specify hello metadata file on hello command line using hello `/MetadataFile` parameter.</span></span> <span data-ttu-id="1a591-123">Ниже приведен пример указания обоих файлов.</span><span class="sxs-lookup"><span data-stu-id="1a591-123">Here's an example that specifies both files:</span></span>  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a><span data-ttu-id="1a591-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1a591-124">Next steps</span></span>

* [<span data-ttu-id="1a591-125">Формат файла свойств и метаданных службы импорта и экспорта</span><span class="sxs-lookup"><span data-stu-id="1a591-125">Import/Export service metadata and properties file format</span></span>](../storage-import-export-file-format-metadata-and-properties.md)
