---
title: "Настройка свойств и метаданных с помощью инструмента импорта и экспорта Azure версии 1 | Документация Майкрософт"
description: "Узнайте, как указать свойства и метаданные, используемые для настройки целевых больших двоичных объектов, при запуске инструмента импорта и экспорта Azure для подготовки дисков. Приведенная информация относится к инструменту импорта и экспорта версии 1."
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
ms.openlocfilehash: 77bdaa5559de86cd1de9f30e70656e47fd5719e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="setting-properties-and-metadata-during-the-import-process"></a><span data-ttu-id="5590e-104">Настройка свойств и метаданных во время импорта</span><span class="sxs-lookup"><span data-stu-id="5590e-104">Setting properties and metadata during the import process</span></span>
<span data-ttu-id="5590e-105">При запуске инструмента импорта и экспорта Microsoft Azure для подготовки дисков вы можете указать свойства и метаданные, предназначенные для настройки целевых больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="5590e-105">When you run the Microsoft Azure Import/Export Tool to prepare your drives, you can specify properties and metadata to be set on the destination blobs.</span></span> <span data-ttu-id="5590e-106">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5590e-106">Follow these steps:</span></span>  
  
1.  <span data-ttu-id="5590e-107">Чтобы задать свойства больших двоичных объектов, создайте текстовый файл на локальном компьютере, определяющий имена и значения свойств.</span><span class="sxs-lookup"><span data-stu-id="5590e-107">To set blob properties, create a text file on your local computer that specifies property names and values.</span></span>  
  
2.  <span data-ttu-id="5590e-108">Чтобы задать метаданные больших двоичных объектов, создайте текстовый файл на локальном компьютере, определяющий имена и значения метаданных.</span><span class="sxs-lookup"><span data-stu-id="5590e-108">To set blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>  
  
3.  <span data-ttu-id="5590e-109">Передайте полный путь к одну или обоим файлам в инструмент импорта и экспорта Azure в ходе операции `PrepImport`.</span><span class="sxs-lookup"><span data-stu-id="5590e-109">Pass the full path to one or both of these files to the Azure Import/Export Tool as part of the `PrepImport` operation.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5590e-110">При указании файла свойств или метаданных в рамках сеанса копирования они задаются для каждого большого двоичного объекта, импортируемого в рамках этого сеанса копирования.</span><span class="sxs-lookup"><span data-stu-id="5590e-110">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="5590e-111">Если вы хотите задать другой набор свойств или метаданных для определенных импортируемых больших двоичных объектов, необходимо создать отдельный сеанс копирования с другими файлами свойств и метаданных.</span><span class="sxs-lookup"><span data-stu-id="5590e-111">If you want to specify a different set of properties or metadata for some of the blobs being imported, you'll need to create a separate copy session with different properties or metadata files.</span></span>  
  
## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="5590e-112">Указание свойств большого двоичного объекта в текстовом файле</span><span class="sxs-lookup"><span data-stu-id="5590e-112">Specify Blob Properties in a Text File</span></span>  
<span data-ttu-id="5590e-113">Чтобы задать свойства больших двоичных объектов, создайте локальный текстовый файл и добавьте элемент XML, определяющий имена свойств в качестве элементов, а значения свойств в качестве значений.</span><span class="sxs-lookup"><span data-stu-id="5590e-113">To specify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="5590e-114">Ниже приведен пример указания некоторых значений свойств.</span><span class="sxs-lookup"><span data-stu-id="5590e-114">Here's an example that specifies some property values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="5590e-115">Сохраните файл в локальном расположении, например `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="5590e-115">Save the file to a local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>  
  
## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="5590e-116">Указание метаданных большого двоичного объекта в текстовом файле</span><span class="sxs-lookup"><span data-stu-id="5590e-116">Specify Blob Metadata in a Text File</span></span>  
<span data-ttu-id="5590e-117">Аналогичным образом, чтобы задать метаданные больших двоичных объектов, создайте локальный текстовый файл, определяющий имена метаданных в качестве элементов и значения метаданных в качестве значений.</span><span class="sxs-lookup"><span data-stu-id="5590e-117">Similarly, to specify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="5590e-118">Ниже приведен пример указания некоторых значений метаданных.</span><span class="sxs-lookup"><span data-stu-id="5590e-118">Here's an example that specifies some metadata values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="5590e-119">Сохраните файл в локальном расположении, например `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="5590e-119">Save the file to a local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>  
  
## <a name="create-a-copy-session-including-the-properties-or-metadata-files"></a><span data-ttu-id="5590e-120">Создание сеанса копирования, содержащего файлы свойств и метаданных</span><span class="sxs-lookup"><span data-stu-id="5590e-120">Create a Copy Session Including the Properties or Metadata Files</span></span>  
<span data-ttu-id="5590e-121">При запуске инструмента импорта и экспорта Azure для подготовки задания импорта укажите в командной строке файл свойств, используя параметр `PropertyFile`.</span><span class="sxs-lookup"><span data-stu-id="5590e-121">When you run the Azure Import/Export Tool to prepare the import job, specify the properties file on the command line using the `PropertyFile` parameter.</span></span> <span data-ttu-id="5590e-122">Для указания файла метаданных используйте параметр `/MetadataFile`.</span><span class="sxs-lookup"><span data-stu-id="5590e-122">Specify the metadata file on the command line using the `/MetadataFile` parameter.</span></span> <span data-ttu-id="5590e-123">Ниже приведен пример указания обоих файлов.</span><span class="sxs-lookup"><span data-stu-id="5590e-123">Here's an example that specifies both files:</span></span>  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a><span data-ttu-id="5590e-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5590e-124">Next steps</span></span>

* [<span data-ttu-id="5590e-125">Формат файла свойств и метаданных службы импорта и экспорта</span><span class="sxs-lookup"><span data-stu-id="5590e-125">Import/Export service metadata and properties file format</span></span>](../storage-import-export-file-format-metadata-and-properties.md)
