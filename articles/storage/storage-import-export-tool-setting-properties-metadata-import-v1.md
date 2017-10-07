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
ms.openlocfilehash: 66e55c2076fbcda9b78302f17b5ff2cf96bb24e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a>Настройка свойств и метаданных во время hello процессе импорта
При запуске средства импорта и экспорта Microsoft Azure tooprepare hello дисков можно указать свойства и метаданные toobe на hello целевых больших двоичных объектов. Выполните следующие действия.  
  
1.  свойства большого двоичного объекта tooset, создайте текстовый файл на локальном компьютере, который определяет имена и значения свойств.  
  
2.  tooset метаданные больших двоичных объектов, создайте текстовый файл на локальном компьютере, который определяет имена и значения метаданных.  
  
3.  Передайте полный путь tooone hello или оба эти файлы toohello средство импорта и экспорта Azure как часть hello `PrepImport` операции.  
  
> [!NOTE]
>  При указании файла свойств или метаданных в рамках сеанса копирования они задаются для каждого большого двоичного объекта, импортируемого в рамках этого сеанса копирования. Если требуется toospecify набор свойств или метаданных для некоторых импортируемых больших двоичных объектов hello, вам потребуется toocreate отдельную скопировать сеанс работы с файлами различных свойств или метаданных.  
  
## <a name="specify-blob-properties-in-a-text-file"></a>Указание свойств большого двоичного объекта в текстовом файле  
toospecify свойства большого двоичного объекта, создайте локальный текстовый файл и включите XML-ФАЙЛ, содержащий имена свойств в элементы и значения свойств в значениях. Ниже приведен пример указания некоторых значений свойств.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
Сохранить hello файл tooa папку, например `C:\WAImportExport\ImportProperties.txt`.  
  
## <a name="specify-blob-metadata-in-a-text-file"></a>Указание метаданных большого двоичного объекта в текстовом файле  
Аналогичным образом toospecify метаданные больших двоичных объектов, создайте локальный текстовый файл, содержащий имена метаданных как элементы и значения метаданных как значения. Ниже приведен пример указания некоторых значений метаданных.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
Сохранить hello файл tooa папку, например `C:\WAImportExport\ImportMetadata.txt`.  
  
## <a name="create-a-copy-session-including-hello-properties-or-metadata-files"></a>Создать hello, включая сеанс копирования файлами свойств или метаданных  
При запуске средства импорта и экспорта Azure tooprepare hello hello-задания импорта укажите файл свойств hello в командной строке hello hello `PropertyFile` параметра. Укажите файл метаданных hello в командной строке hello hello `/MetadataFile` параметра. Ниже приведен пример указания обоих файлов.  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a>Дальнейшие действия

* [Формат файла свойств и метаданных службы импорта и экспорта](storage-import-export-file-format-metadata-and-properties.md)
