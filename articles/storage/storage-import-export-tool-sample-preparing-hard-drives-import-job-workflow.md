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
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a>Образец рабочего процесса tooprepare жесткие диски для задания импорта

В этой статье рассматриваются hello полный процесс подготовки дисков для задания импорта.

## <a name="sample-data"></a>Пример данных

В этом примере импортируются следующие данные в учетную запись хранилища Azure с именем hello `mystorageaccount`:

|Расположение|Описание|Размер данных|
|--------------|-----------------|-----|
|H:\Video\ |Коллекция видео.|12 ТБ|
|H:\Photo\ |Коллекция фотографий.|30 ГБ|
|K:\Temp\FavoriteMovie.ISO|Образ диска Blu-Ray™.|25 ГБ|
|\\\bigshare\john\music\|Коллекция музыкальных файлов в сетевой папке.|10 ГБ|

## <a name="storage-account-destinations"></a>Целевые каталоги в учетной записи хранения

Задание Hello импортирует hello данных в следующие назначения в учетной записи хранения hello hello:

|Источник|Целевой виртуальный каталог или большой двоичный объект.|
|------------|-------------------------------------------|
|H:\Video\ |video/|
|H:\Photo\ |photo/|
|K:\Temp\FavoriteMovie.ISO|favorite/FavoriteMovies.ISO|
|\\\bigshare\john\music\ |music|

В этом сопоставлении hello файл `H:\Video\Drama\GreatMovie.mov` будет импортированных toohello большого двоичного объекта `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.

## <a name="determine-hard-drive-requirements"></a>Определение требований к жестким дискам

Далее, toodetermine требуются сколько жестких дисков, размер hello вычислений hello данных:

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

Для нашего примера будет достаточно двух жестких дисков объемом в 8 ТБ каждый. Однако, поскольку исходный каталог hello `H:\Video` содержит 12 ТБ данных, а емкость вашей одного жесткого диска составляет 8 ТБ, можно будет toospecify в hello следующие образом hello **driveset.csv** файла:

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
Средство Hello будет распределить данные на два жестких диска оптимальным образом.

## <a name="attach-drives-and-configure-hello-job"></a>Присоединение дисков и настроить задание hello
Будет подключить оба машине toohello диски и создавать тома. Затем создайте файл **dataset.csv**:
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

Кроме того можно задать следующие метаданные для всех файлов hello.

* **UploadMethod:** Microsoft Azure Import/Export service
* **DataSetName:** SampleData
* **CreationDate:** 10/1/2013

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

* **Content-Type:** application/octet-stream
* **Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==
* **Cache-Control:** no-cache

tooset эти свойства, создайте текстовый файл, `c:\WAImportExport\SampleProperties.txt`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a>Hello выполнения средства импорта и экспорта Azure (WAImportExport.exe)

Теперь все готово toorun hello средство импорта и экспорта Azure tooprepare hello два жестких диска.

**Для hello первого сеанса:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

Если любые дополнительные данные, должен добавить toobe, создайте другой файл набора данных (формате Initialdataset).

**Для hello второй сеанс:**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

После завершения сеансов копирования hello можно отключиться от компьютера копирования hello hello двух дисков и их отправке toohello соответствующий ЦОД Azure. Вы отправите hello двух файлов журнала, `<FirstDriveSerialNumber>.xml` и `<SecondDriveSerialNumber>.xml`при создании задания импорта hello в hello портал Azure.

## <a name="next-steps"></a>Дальнейшие действия

* [Подготовка жестких дисков для задания импорта](storage-import-export-tool-preparing-hard-drives-import.md)
* [Краткий справочник по часто используемым командам](storage-import-export-tool-quick-reference.md)
