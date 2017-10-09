---
title: "aaaSetting свойства и метаданные с помощью импорта и экспорта Azure | Документы Microsoft"
description: "Узнайте, как свойства и метаданные toobe toospecify задать на hello целевые большие двоичные объекты при запуске средства импорта и экспорта Azure tooprepare hello дисков."
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
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: c763237160f0e4b72ce88fd31e2958994bfe8e50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a><span data-ttu-id="a20de-103">Настройка свойств и метаданных во время hello процессе импорта</span><span class="sxs-lookup"><span data-stu-id="a20de-103">Setting properties and metadata during hello import process</span></span>

<span data-ttu-id="a20de-104">При запуске средства импорта и экспорта Microsoft Azure tooprepare hello дисков можно указать свойства и метаданные toobe на hello целевых больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="a20de-104">When you run hello Microsoft Azure Import/Export Tool tooprepare your drives, you can specify properties and metadata toobe set on hello destination blobs.</span></span> <span data-ttu-id="a20de-105">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a20de-105">Follow these steps:</span></span>

1.  <span data-ttu-id="a20de-106">свойства большого двоичного объекта tooset, создайте текстовый файл на локальном компьютере, который определяет имена и значения свойств.</span><span class="sxs-lookup"><span data-stu-id="a20de-106">tooset blob properties, create a text file on your local computer that specifies property names and values.</span></span>
2.  <span data-ttu-id="a20de-107">tooset метаданные больших двоичных объектов, создайте текстовый файл на локальном компьютере, который определяет имена и значения метаданных.</span><span class="sxs-lookup"><span data-stu-id="a20de-107">tooset blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>
3.  <span data-ttu-id="a20de-108">Передайте полный путь tooone hello или оба эти файлы toohello средство импорта и экспорта Azure как часть hello `PrepImport` операции.</span><span class="sxs-lookup"><span data-stu-id="a20de-108">Pass hello full path tooone or both of these files toohello Azure Import/Export Tool as part of hello `PrepImport` operation.</span></span>

> [!NOTE]
>  <span data-ttu-id="a20de-109">При указании файла свойств или метаданных в рамках сеанса копирования они задаются для каждого большого двоичного объекта, импортируемого в рамках этого сеанса копирования.</span><span class="sxs-lookup"><span data-stu-id="a20de-109">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="a20de-110">Если требуется toospecify набор свойств или метаданных для некоторых импортируемых больших двоичных объектов hello, вам потребуется toocreate отдельную скопировать сеанс работы с файлами различных свойств или метаданных.</span><span class="sxs-lookup"><span data-stu-id="a20de-110">If you want toospecify a different set of properties or metadata for some of hello blobs being imported, you'll need toocreate a separate copy session with different properties or metadata files.</span></span>

## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="a20de-111">Указание свойств большого двоичного объекта в текстовом файле</span><span class="sxs-lookup"><span data-stu-id="a20de-111">Specify blob properties in a text file</span></span>

<span data-ttu-id="a20de-112">toospecify свойства большого двоичного объекта, создайте локальный текстовый файл и включите XML-ФАЙЛ, содержащий имена свойств в элементы и значения свойств в значениях.</span><span class="sxs-lookup"><span data-stu-id="a20de-112">toospecify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="a20de-113">Ниже приведен пример указания некоторых значений свойств.</span><span class="sxs-lookup"><span data-stu-id="a20de-113">Here's an example that specifies some property values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

<span data-ttu-id="a20de-114">Сохранить hello файл tooa папку, например `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="a20de-114">Save hello file tooa local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>

## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="a20de-115">Указание метаданных большого двоичного объекта в текстовом файле</span><span class="sxs-lookup"><span data-stu-id="a20de-115">Specify blob metadata in a text file</span></span>

<span data-ttu-id="a20de-116">Аналогичным образом toospecify метаданные больших двоичных объектов, создайте локальный текстовый файл, содержащий имена метаданных как элементы и значения метаданных как значения.</span><span class="sxs-lookup"><span data-stu-id="a20de-116">Similarly, toospecify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="a20de-117">Ниже приведен пример указания некоторых значений метаданных.</span><span class="sxs-lookup"><span data-stu-id="a20de-117">Here's an example that specifies some metadata values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="a20de-118">Сохранить hello файл tooa папку, например `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="a20de-118">Save hello file tooa local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>

## <a name="add-hello-path-tooproperties-and-metadata-files-in-datasetcsv"></a><span data-ttu-id="a20de-119">Добавить файлы tooproperties и метаданные путь hello в dataset.csv</span><span class="sxs-lookup"><span data-stu-id="a20de-119">Add hello path tooproperties and metadata files in dataset.csv</span></span>

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a><span data-ttu-id="a20de-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a20de-120">Next steps</span></span>

* [<span data-ttu-id="a20de-121">Формат файла свойств и метаданных службы импорта и экспорта</span><span class="sxs-lookup"><span data-stu-id="a20de-121">Import/Export service metadata and properties file format</span></span>](../storage-import-export-file-format-metadata-and-properties.md)
