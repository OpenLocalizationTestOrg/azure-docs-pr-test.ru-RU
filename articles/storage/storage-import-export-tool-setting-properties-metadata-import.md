---
title: "Настройка свойств и метаданных с помощью службы импорта и экспорта Azure | Документация Майкрософт"
description: "Узнайте, как указать свойства и метаданные, используемые для настройки целевых больших двоичных объектов, при запуске инструмента импорта и экспорта Azure для подготовки дисков."
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
ms.openlocfilehash: bdc7a53f82d1fbbb726e2b1bd5d96678a8563566
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="setting-properties-and-metadata-during-the-import-process"></a><span data-ttu-id="cb98f-103">Настройка свойств и метаданных во время импорта</span><span class="sxs-lookup"><span data-stu-id="cb98f-103">Setting properties and metadata during the import process</span></span>

<span data-ttu-id="cb98f-104">При запуске инструмента импорта и экспорта Microsoft Azure для подготовки дисков вы можете указать свойства и метаданные, предназначенные для настройки целевых больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="cb98f-104">When you run the Microsoft Azure Import/Export Tool to prepare your drives, you can specify properties and metadata to be set on the destination blobs.</span></span> <span data-ttu-id="cb98f-105">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="cb98f-105">Follow these steps:</span></span>

1.  <span data-ttu-id="cb98f-106">Чтобы задать свойства больших двоичных объектов, создайте текстовый файл на локальном компьютере, определяющий имена и значения свойств.</span><span class="sxs-lookup"><span data-stu-id="cb98f-106">To set blob properties, create a text file on your local computer that specifies property names and values.</span></span>
2.  <span data-ttu-id="cb98f-107">Чтобы задать метаданные больших двоичных объектов, создайте текстовый файл на локальном компьютере, определяющий имена и значения метаданных.</span><span class="sxs-lookup"><span data-stu-id="cb98f-107">To set blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>
3.  <span data-ttu-id="cb98f-108">Передайте полный путь к одну или обоим файлам в инструмент импорта и экспорта Azure в ходе операции `PrepImport`.</span><span class="sxs-lookup"><span data-stu-id="cb98f-108">Pass the full path to one or both of these files to the Azure Import/Export Tool as part of the `PrepImport` operation.</span></span>

> [!NOTE]
>  <span data-ttu-id="cb98f-109">При указании файла свойств или метаданных в рамках сеанса копирования они задаются для каждого большого двоичного объекта, импортируемого в рамках этого сеанса копирования.</span><span class="sxs-lookup"><span data-stu-id="cb98f-109">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="cb98f-110">Если вы хотите задать другой набор свойств или метаданных для определенных импортируемых больших двоичных объектов, необходимо создать отдельный сеанс копирования с другими файлами свойств и метаданных.</span><span class="sxs-lookup"><span data-stu-id="cb98f-110">If you want to specify a different set of properties or metadata for some of the blobs being imported, you'll need to create a separate copy session with different properties or metadata files.</span></span>

## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="cb98f-111">Указание свойств большого двоичного объекта в текстовом файле</span><span class="sxs-lookup"><span data-stu-id="cb98f-111">Specify blob properties in a text file</span></span>

<span data-ttu-id="cb98f-112">Чтобы задать свойства больших двоичных объектов, создайте локальный текстовый файл и добавьте элемент XML, определяющий имена свойств в качестве элементов, а значения свойств в качестве значений.</span><span class="sxs-lookup"><span data-stu-id="cb98f-112">To specify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="cb98f-113">Ниже приведен пример указания некоторых значений свойств.</span><span class="sxs-lookup"><span data-stu-id="cb98f-113">Here's an example that specifies some property values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

<span data-ttu-id="cb98f-114">Сохраните файл в локальном расположении, например `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="cb98f-114">Save the file to a local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>

## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="cb98f-115">Указание метаданных большого двоичного объекта в текстовом файле</span><span class="sxs-lookup"><span data-stu-id="cb98f-115">Specify blob metadata in a text file</span></span>

<span data-ttu-id="cb98f-116">Аналогичным образом, чтобы задать метаданные больших двоичных объектов, создайте локальный текстовый файл, определяющий имена метаданных в качестве элементов и значения метаданных в качестве значений.</span><span class="sxs-lookup"><span data-stu-id="cb98f-116">Similarly, to specify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="cb98f-117">Ниже приведен пример указания некоторых значений метаданных.</span><span class="sxs-lookup"><span data-stu-id="cb98f-117">Here's an example that specifies some metadata values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="cb98f-118">Сохраните файл в локальном расположении, например `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="cb98f-118">Save the file to a local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>

## <a name="add-the-path-to-properties-and-metadata-files-in-datasetcsv"></a><span data-ttu-id="cb98f-119">Добавьте путь к файлам свойств и метаданных в dataset.csv.</span><span class="sxs-lookup"><span data-stu-id="cb98f-119">Add the path to properties and metadata files in dataset.csv</span></span>

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a><span data-ttu-id="cb98f-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cb98f-120">Next steps</span></span>

* [<span data-ttu-id="cb98f-121">Формат файла свойств и метаданных службы импорта и экспорта</span><span class="sxs-lookup"><span data-stu-id="cb98f-121">Import/Export service metadata and properties file format</span></span>](storage-import-export-file-format-metadata-and-properties.md)
