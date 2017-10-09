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
# <a name="previewing-drive-usage-for-an-export-job"></a>Предварительный просмотр использования дисков для задания экспорта
Прежде чем создать задание экспорта, необходимо экспортировать набор больших двоичных объектов toobe toochoose. Hello службы импорта и экспорта Microsoft Azure позволяет toouse список путей больших двоичных объектов или toorepresent hello большие двоичные объекты, выбранные префиксов больших двоичных объектов.  
  
Далее необходимо toodetermine сколько дисков необходимо toosend. Средство импорта и экспорта Hello предоставляет hello `PreviewExport` выбран использования диска toopreview команды hello большие двоичные объекты, на основании размера hello hello дисков будет toouse.

## <a name="command-line-parameters"></a>Параметры командной строки

Можно использовать следующие параметры при использовании hello hello `PreviewExport` команде hello средство импорта и экспорта.

|Параметр командной строки|Описание|  
|--------------------------|-----------------|  
|**/logdir:**<каталог_журнала\>|необязательный параметр. каталог журнала Hello. Подробные журналы будут записаны toothis каталога. Если журнал каталога не указан, текущий каталог hello будет использоваться как каталог журнала hello.|  
|**/sn:**<StorageAccountName\>|Обязательный элемент. Задание экспорта Hello имя учетной записи хранения hello hello.|  
|**/sk:**<ключ_учетной_записи_хранения\>|Требуется, только если не указан SAS контейнера. Задание экспорта Hello ключ учетной записи хранилища hello для hello.|  
|**/csas:**<SAS_контейнера\>|Требуется, только если не указан ключ учетной записи хранения. Hello контейнер SAS для больших двоичных объектов toobe листинг hello экспортируются в задании экспорта hello.|  
|**/ExportBlobListFile:**<файл_списка_больших_двоичных_объектов_экспорта\>|Обязательный элемент. Путь toohello XML файлу, содержащему список путей больших двоичных объектов или префиксов для экспорта toobe большие двоичные объекты hello. формат файла Hello, используемый в hello `BlobListBlobPath` элемент в hello [вставки задания](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) работы hello REST API службы импорта и экспорта.|  
|**/DriveSize:**<размер_диска\>|Обязательный элемент. Здравствуйте, размер toouse дисков для задания экспорта, *например*, 500 ГБ, 1,5 ТБ.|  

## <a name="command-line-example"></a>Пример для командной строки

Hello ниже приведен пример hello `PreviewExport` команды:  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
Hello списка больших двоичных может содержать имена и префиксы больших двоичных объектов, как показано ниже:  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

списки средство импорта и экспорта Azure Hello toobe все большие двоичные объекты экспортированы и вычисляет, как их на диски hello указанный размер с учетом любых издержек, а затем определяет hello количество дисков toopack необходимые toohold hello больших двоичных объектов и использования диска сведения.  
  
Ниже приведен пример выходных данных hello, с опущены все информационные журналы:  
  
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
  
## <a name="next-steps"></a>Дальнейшие действия

* [Руководство по использованию инструмента импорта и экспорта](../storage-import-export-tool-how-to-v1.md)
