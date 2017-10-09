---
title: "Задание экспорта импорта и экспорта Azure - v1 aaaRepairing | Документы Microsoft"
description: "Узнайте, как задание экспорта, который был создан и выполняются с использованием toorepair hello импорта и экспорта Azure службы."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 728e2a42-04ce-4be8-9375-e9e2bc6827a5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: e54bc66495c8a3473b8ec51bb254bce8bdc9eab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-export-job"></a>Исправление задания экспорта
После завершения задания экспорта, можно запустить средство импорта и экспорта Microsoft Azure локально для hello:  
  
1.  Загружайте никакие файлы, что служба импорта и экспорта Azure hello находилась tooexport не удается.  
  
2.  Проверьте, правильно экспортированы hello файлов на диске hello.  
  
Необходимо иметь toouse хранения tooAzure подключения к этой функции.  
  
Команда Hello для исправления задания импорта: **RepairExport**.

## <a name="repairexport-parameters"></a>Параметры RepairExport

Hello могут быть указаны следующие параметры с **RepairExport**:  
  
|Параметр|Описание|  
|---------------|-----------------|  
|**/r:<файл_восстановления\>**|Обязательный элемент. Путь toohello восстановить файл, который отслеживает ход выполнения восстановления hello hello и позволяет при tooresume прерванное восстановление. Каждый диск должен быть связан с одним и только одним файлом восстановления. При запуске восстановления для заданного диска вы передаете hello путь tooa файлу восстановления, который еще не существует. tooresume прерванное восстановление, необходимо передать в качестве имени hello существующего файла восстановления. всегда необходимо указать Hello восстановления файла соответствующий toohello целевой диск.|  
|**/logdir:<каталог_журнала\>**|необязательный параметр. каталог журнала Hello. Подробные журналы будут записаны toothis каталога. Если журнал каталога не указан, текущий каталог hello будет использоваться как каталог журнала hello.|  
|**/d:<целевой_каталог\>**|Обязательный элемент. каталог toovalidate Hello и восстановления. Обычно это hello корневой каталог диска экспорта hello, но может также быть сетевую общую папку с копией hello экспортировать файлы.|  
|**/bk:<ключ_BitLocker\>**|необязательный параметр. Ключ BitLocker hello следует указывать, если требуется toounlock средство hello хранятся зашифрованные который hello экспортироваться файлы.|  
|**/sn:<учетная_запись_хранения\>**|Обязательный элемент. Задание экспорта Hello имя учетной записи хранения hello hello.|  
|**/sk:<ключ_учетной_записи_хранения\>**|**Требуется**, только если не указан SAS контейнера. Задание экспорта Hello ключ учетной записи хранилища hello для hello.|  
|**/csas:<SAS_контейнера\>**|**Требуется** только в том случае, если не указан ключ учетной записи хранения hello. Hello SAS контейнера для доступа к большим двоичным объектам hello, связанный с заданием экспорта hello.|  
|**/CopyLogFile:<файл_журнала\>**|Обязательный элемент. Hello путь toohello файлу журнала копирования диска. файл Hello формируется hello службы импорта и экспорта Windows Azure и можно загрузить из хранилища больших двоичных объектов hello, связанный с заданием hello. файл журнала копирования Hello содержит сведения о неудачных больших двоичных объектов или файлов, являющихся toobe исправить.|  
|**/ ManifestFile:<файл_манифеста_диска\>**|необязательный параметр. файл манифеста toohello экспорта Hello путь диска. Этот файл создается службой импорта и экспорта Windows Azure hello и сохраняется на диске экспорта hello и при необходимости в большом двоичном объекте в учетной записи хранения hello, связанный с заданием hello.<br /><br /> Hello содержимое hello файлов на диске hello экспорта будет проверено с MD5-хэшей hello в этом файле содержится. Все файлы, определяется toobe поврежден, будут загружены и перезаписанного toohello целевые каталоги.|  
  
## <a name="using-repairexport-mode-toocorrect-failed-exports"></a>Использование режима RepairExport toocorrect режим не удалось выполнить экспорт  
Можно использовать файлы toodownload средство импорта и экспорта Azure hello, не прошедшие tooexport. файл журнала копирования Hello будет содержать список файлов, которые не удалось tooexport.  
  
Hello причины сбоев экспорта hello следующие возможности:  
  
-   повреждение дисков;  
  
-   ключ учетной записи хранения Hello, изменился в процессе передачи hello  
  
Средство toorun hello в **RepairExport** режиме, необходимо сначала tooconnect hello диск, содержащий компьютер tooyour hello экспортированные файлы. После этого запустите средство импорта и экспорта Azure, при указании hello путь toothat диска с hello hello `/d` параметра. Необходимо также файлу журнала копирования путь toohello toospecify hello диска загруженный. Hello следующий пример командной строки запускает средство toorepair hello все файлы, которые не удалось выполнить tooexport:  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
Hello ниже приведен пример файла журнала копирования, показано, что один блок в tooexport hello больших двоичных объектов не удалось:  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/desert.jpg</BlobPath>  
    <FilePath>\pictures\wild\desert.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList>  
      <Block Offset="65536" Length="65536" Id="AQAAAA==" Status="Failed" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
файл журнала копирования Hello указывает, что сбой произошел, когда hello службы импорта и экспорта Windows Azure загружала один hello большого двоичного объекта файла toohello блоков на диске экспорта hello. Здравствуйте, другие компоненты успешно загружены файл hello и hello длина файла была задана правильно. В этом случае средство hello откройте hello файл на диске hello, загрузить hello блок из учетной записи хранения hello и записать их в диапазон файлов toohello, начиная со смещения 65536 с длиной 65536.  
  
## <a name="using-repairexport-toovalidate-drive-contents"></a>С помощью содержимого диска toovalidate RepairExport  
Можно также использовать импорта и экспорта Azure с hello **RepairExport** параметр toovalidate hello содержимое на диске hello заданы правильно. файл манифеста Hello на каждом диске экспорта содержит MD5-хэши для содержимого hello hello диска.  
  
Hello службы импорта и экспорта Azure также можно сохранить файлы манифеста hello tooa учетной записи хранения во время процесса экспорта hello. Hello расположения файлов манифеста hello доступен через hello [получения задания](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) операцию при завершении задания hello. В разделе [службы импорта и экспорта формат файла манифеста](storage-import-export-file-format-metadata-and-properties.md) Дополнительные сведения о формате hello файла манифеста диска.  
  
Hello следующем примере показано, как toorun hello средство импорта и экспорта Azure с hello **/ManifestFile** и **/CopyLogFile** параметры:  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
Hello ниже приведен пример файла манифеста:  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveManifest Version="2011-10-01">  
  <Drive>  
    <DriveId>9WM35C3U</DriveId>  
    <ClientCreator>Windows Azure Import/Export service</ClientCreator>  
    <BlobList>
      <Blob>  
        <BlobPath>pictures/city/redmond.jpg</BlobPath>  
        <FilePath>\pictures\city\redmond.jpg</FilePath>  
        <Length>15360</Length>  
        <PageRangeList>  
          <PageRange Offset="0" Length="3584" Hash="72FC55ED9AFDD40A0C8D5C4193208416" />  
          <PageRange Offset="3584" Length="3584" Hash="68B28A561B73D1DA769D4C24AA427DB8" />  
          <PageRange Offset="7168" Length="512" Hash="F521DF2F50C46BC5F9EA9FB787A23EED" />  
        </PageRangeList>  
        <PropertiesPath Hash="E72A22EA959566066AD89E3B49020C0A">\pictures\city\redmond.jpg.properties</PropertiesPath>  
      </Blob>  
      <Blob>  
        <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
        <FilePath>\pictures\wild\canyon.jpg</FilePath>  
        <Length>10884</Length>  
        <BlockList>  
          <Block Offset="0" Length="2721" Id="AAAAAA==" Hash="263DC9C4B99C2177769C5EBE04787037" />  
          <Block Offset="2721" Length="2721" Id="AQAAAA==" Hash="0C52BAE2CC20EFEC15CC1E3045517AA6" />  
          <Block Offset="5442" Length="2721" Id="AgAAAA==" Hash="73D1CB62CB426230C34C9F57B7148F10" />  
          <Block Offset="8163" Length="2721" Id="AwAAAA==" Hash="11210E665C5F8E7E4F136D053B243E6A" />  
        </BlockList>  
        <PropertiesPath Hash="81D7F81B2C29F10D6E123D386C3A4D5A">\pictures\wild\canyon.jpg.properties</PropertiesPath>  
      </Blob> 
    </BlobList>  
 </Drive>  
</DriveManifest>  
``` 
  
После завершения процесса восстановления hello программа hello прочтите каждый файл, указанный в файле манифеста hello и проверки целостности файла hello с hello MD5-хэшей. Манифест hello выше он проходит через hello следующие компоненты.  

```  
G:\pictures\city\redmond.jpg, offset 0, length 3584  
  
G:\pictures\city\redmond.jpg, offset 3584, length 3584  
  
G:\pictures\city\redmond.jpg, offset 7168, length 3584  
  
G:\pictures\city\redmond.jpg.properties  
  
G:\pictures\wild\canyon.jpg, offset 0, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 2721, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 5442, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 8163, length 2721  
  
G:\pictures\wild\canyon.jpg.properties  
```

Любой компонент, сбой проверки hello загружается средством hello и переписать toohello тот же файл на диске hello.  
  
## <a name="next-steps"></a>Дальнейшие действия
 
* [Установка hello средство импорта и экспорта Azure](storage-import-export-tool-setup-v1.md)   
* [Подготовка жестких дисков для задания импорта](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Просмотр состояния задания с помощью файлов журнала копирования](storage-import-export-tool-reviewing-job-status-v1.md)   
* [Подготовка задания импорта](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [Устранение неполадок средства импорта и экспорта Azure hello](storage-import-export-tool-troubleshooting-v1.md)
