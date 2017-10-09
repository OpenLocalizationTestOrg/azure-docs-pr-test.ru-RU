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
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a>Образец рабочего процесса tooprepare жесткие диски для задания импорта
В этом разделе рассматриваются hello полный процесс подготовки дисков для задания импорта.  
  
В этом примере импортируются следующие данные в учетной записи хранилища Windows Azure с именем hello `mystorageaccount`:  
  
|Расположение|Описание|  
|--------------|-----------------|  
|H:\Video|Коллекция видео, общий размер которой составляет 5 ТБ.|  
|H:\Photo|Коллекция фотографий, общий размер которой составляет 30 ГБ.|  
|K:\Temp\FavoriteMovie.ISO|Образ диска Blu-Ray™, размер которого составляет 25 ГБ.|  
|\\\bigshare\john\music|Коллекция музыкальных файлов в сетевой папке, общий размер которой составляет 10 ГБ.|  
  
Задание импорта Hello импортирует эти данные в следующие назначения в учетной записи хранения hello hello:  
  
|Источник|Целевой виртуальный каталог или большой двоичный объект.|  
|------------|-------------------------------------------|  
|H:\Video|https://mystorageaccount.blob.core.windows.net/video|  
|H:\Photo|https://mystorageaccount.blob.core.windows.net/photo|  
|K:\Temp\FavoriteMovie.ISO|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO|  
|\\\bigshare\john\music|https://mystorageaccount.blob.core.windows.net/music|  
  
В этом сопоставлении hello файл `H:\Video\Drama\GreatMovie.mov` — большой двоичный объект импортированных toohello `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.  
  
Далее, toodetermine требуются сколько жестких дисков, размер hello вычислений hello данных:  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
Для нашего примера будет достаточно двух жестких дисков объемом 3 ТБ каждый. Однако, поскольку исходный каталог hello `H:\Video` содержит 5 ТБ данных, а емкость вашей одного жесткого диска составляет всего 3 ТБ, это необходимые toobreak `H:\Video` на два каталога меньшего размера: `H:\Video1` и `H:\Video2`, прежде чем выполнение hello Microsoft Средство импорта и экспорта Azure. Этот шаг создает следующие исходные каталоги hello:  
  
|Расположение|Размер|Целевой виртуальный каталог или большой двоичный объект.|  
|--------------|----------|-------------------------------------------|  
|H:\Video1|2,5 TБ|https://mystorageaccount.blob.core.windows.net/video|  
|H:\Video2|2,5 TБ|https://mystorageaccount.blob.core.windows.net/video|  
|H:\Photo|30 ГБ|https://mystorageaccount.blob.core.windows.net/photo|  
|K:\Temp\FavoriteMovies.ISO|25 ГБ|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO|  
|\\\bigshare\john\music|10 ГБ|https://mystorageaccount.blob.core.windows.net/music|  
  
 Здравствуйте, даже если `H:\Video`каталог разбит tootwo каталогов, они указывают toohello один целевой виртуальный каталог в учетной записи хранения hello. Таким образом, все видеофайлы содержатся в одном `video` контейнера в учетной записи хранения hello.  
  
 Затем hello предыдущих исходных каталогов — равномерно распределенные toohello два жестких диска.  
  
||||  
|-|-|-|  
|Жесткий диск|Исходные каталоги|Общий размер|  
|Первый диск|H:\Video1|2,5 ТБ + 30 ГБ|  
||H:\Photo||  
|Второй диск|H:\Video2|2,5 ТБ + 35 ГБ|  
||K:\Temp\BlueRay.ISO||  
||\\\bigshare\john\music||  
  
Кроме того можно задать следующие метаданные для всех файлов hello.  
  
-   **UploadMethod:** Microsoft Azure Import/Export service  
  
-   **DataSetName:** SampleData  
  
-   **CreationDate:** 10/1/2013  
  
метаданные tooset hello импорта файлов, создайте текстовый файл, `c:\WAImportExport\SampleMetadata.txt`, с hello после содержимого:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
Можно также задать некоторые свойства для hello `FavoriteMovie.ISO` больших двоичных объектов:  
  
-   **Content-Type:** application/octet-stream  
  
-   **Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==  
  
-   **Cache-Control:** no-cache  
  
tooset эти свойства, создайте текстовый файл, `c:\WAImportExport\SampleProperties.txt`:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
Теперь все готово toorun hello средство импорта и экспорта Azure tooprepare hello два жестких диска. Обратите внимание на следующее.  
  
-   Hello первый диск подключается как диск X.  
  
-   Hello второй диск подключается как диск Y.  
  
-   Hello ключ учетной записи хранения hello `mystorageaccount` — `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a>Подготовка диска для импорта, когда данные предварительно загружены
 
 Если импортировать toobe данных hello уже существует на диске hello, используйте флаг /skipwrite hello. значение Hello/t и /srcdir должны оба диска точки toohello подготовлено для импорта. Если все импортированные toobe данных hello не будет toohello же целевой виртуальный каталог или корневой учетной записи хранения hello, выполнения hello же отдельно, команды для каждой целевой каталог указывать значение hello /id hello же между запусками все.

>[!NOTE] 
>Не указывайте параметр/Format, как он будет очистить hello данные на диске hello. Можно указать / шифрования или /bk в зависимости от того, было ли hello диск уже зашифрован или нет. 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a>Сеансы копирования — первый диск

Первый диск hello запустите hello средство импорта и экспорта Azure дважды hello toocopy два источника каталоги:  

**Первый сеанс копирования**
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

**Второй сеанс копирования**

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a>Сеансы копирования — второй диск
 
Для hello второго диска запустите hello средство импорта и экспорта Azure три раза, после каждого hello исходные каталоги и один раз для автономного hello Blu-Ray™ файл изображения):  
  
**Первый сеанс копирования** 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
**Второй сеанс копирования**

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
**Третий сеанс копирования**  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a>Завершение сеанса копирования

После завершения сеансов копирования hello можно отключиться от компьютера копирования hello hello двух дисков и их отправке toohello соответствующий центр данных Windows Azure. Отправка hello двух файлов журнала, `FirstDrive.jrn` и `SecondDrive.jrn`, при создании задания импорта hello в hello [портал Windows Azure](https://manage.windowsazure.com/).  
  
## <a name="next-steps"></a>Дальнейшие действия

* [Подготовка жестких дисков для задания импорта](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Краткий справочник по часто используемым командам](../storage-import-export-tool-quick-reference-v1.md) 
