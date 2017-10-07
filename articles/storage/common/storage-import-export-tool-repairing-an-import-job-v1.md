---
title: "Задание импорта импорта и экспорта Azure - v1 aaaRepairing | Документы Microsoft"
description: "Узнайте, каким образом задание импорта, который был создан и выполняются с использованием toorepair hello импорта и экспорта Azure службы."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: b1cb7d7832276a05c0912cf57505e2a5d79e7846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-import-job"></a>Исправление задания импорта
Hello службы импорта и экспорта Microsoft Azure может завершиться ошибкой toocopy некоторые файлы или части файлов toohello службы больших двоичных объектов Windows Azure. Это может происходить по следующим причинам:  
  
-   файлы повреждены;  
  
-   повреждение дисков;  
  
-   ключ учетной записи хранилища Hello изменился во время передачи файла hello.  
  
Можно запустить hello средство импорта и экспорта Microsoft Azure с помощью задания импорта hello копии журнала файлов и hello средство передачи hello отсутствующие файлы (или части файлов) tooyour Windows Azure хранилища учетной записи toocomplete hello импорта.  
  
## <a name="repairimport-parameters"></a>Параметры RepairImport

Hello могут быть указаны следующие параметры с **RepairImport**: 
  
|||  
|-|-|  
|**/r:**<RepairFile\>|**Обязательный параметр.** Путь toohello восстановить файл, который отслеживает ход выполнения восстановления hello hello и позволяет при tooresume прерванное восстановление. Каждый диск должен быть связан с одним и только одним файлом восстановления. При запуске восстановления для данного диска, передайте файл tooa восстановления hello путь, который еще не существует. tooresume прерванное восстановление, необходимо передать в качестве имени hello существующего файла восстановления. всегда необходимо указать Hello восстановления файла соответствующий toohello целевой диск.|  
|**/logdir:**<каталог_журнала\>|**Необязательный параметр.** каталог журнала Hello. Файлы подробных журналов записываются toothis каталога. Если журнал каталога не указан, текущий каталог hello используется как каталог журнала hello.|  
|**/d:**<TargetDirectories\>|**Обязательный параметр.** Один или несколько каталогов разделенных точкой с запятой, которые содержат hello исходные файлы, которые были импортированы. диск импорта Hello также может использоваться, но не является обязательным, если доступны альтернативного расположения исходных файлов.|  
|**/bk:**<ключ_BitLocker\>|**Необязательный параметр.** Ключ BitLocker hello следует указывать, если требуется, чтобы средство hello toounlock зашифрованный диск, где находятся исходные файлы hello.|  
|**/sn:**<StorageAccountName\>|**Обязательный параметр.** Имя учетной записи хранилища hello Hello для hello задания импорта.|  
|**/sk:**<ключ_учетной_записи_хранения\>|**Требуется**, только если не указан SAS контейнера. Задание импорта Hello ключ учетной записи хранилища hello для hello.|  
|**/csas:**<SAS_контейнера\>|**Требуется** только в том случае, если не указан ключ учетной записи хранения hello. Hello SAS контейнера для доступа к большим двоичным объектам hello, связанный с заданием импорта hello.|  
|**/CopyLogFile:**<DriveCopyLogFile\>|**Обязательный параметр.** Путь к toohello файлу журнала копирования диска (подробного журнала или журнала ошибок). файл Hello формируется hello службы импорта и экспорта Windows Azure и можно загрузить из хранилища больших двоичных объектов hello, связанный с заданием hello. файл журнала копирования Hello содержит сведения о неудачных больших двоичных объектов или файлы, которые являются toobe исправить.|  
|**/PathMapFile:**<DrivePathMapFile\>|**Необязательный параметр.** Путь tooa текстовый файл, который может использоваться tooresolve неоднозначности при наличии нескольких файлов с hello одинаковые имена, которые импортировались в hello того же задания. Hello первый раз hello средство запускается, оно может заполнить этот файл со всеми неоднозначные имена hello. Последующих запусках средство hello использовать этот файл tooresolve hello неоднозначности.|  
  
## <a name="using-hello-repairimport-command"></a>С помощью команды RepairImport hello  
toorepair Импорт данных при потоковой передачи данных hello hello сети, необходимо указать hello hello каталоги, содержащие hello исходные файлы, которые импортировались с помощью `/d` параметра. Необходимо также указать файл журнала копирования hello, загруженный из вашей учетной записи хранилища. Стандартная Командная строка toorepair задание импорта, частично завершившегося выглядит следующим образом.  
  
```  
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log  
```  
  
В hello примере файл журнала копирования 64 K часть файла поврежден на диске hello, который был указан для задания импорта hello. Так как это hello единственный сбой, остальные hello hello большие двоичные объекты в задании hello успешно импортированы.  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
 <DriveId>9WM35C2V</DriveId>  
 <Blob Status="CompletedWithErrors">  
 <BlobPath>pictures/animals/koala.jpg</BlobPath>  
 <FilePath>\animals\koala.jpg</FilePath>  
 <Length>163840</Length>  
 <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
 <PageRangeList>  
  <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted" />  
 </PageRangeList>  
 </Blob>  
 <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
При передаче этого журнала копирования toohello средство импорта и экспорта Azure, средство hello не попытается toofinish hello импорт этого файла, скопировав отсутствующие содержимое hello hello сети. Следующие hello приведенном выше примере hello ищет инструмент hello исходный файл `\animals\koala.jpg` в каталогах hello двух `C:\Users\bob\Pictures` и `X:\BobBackup\photos`. Если hello файл `C:\Users\bob\Pictures\animals\koala.jpg` существует, средство импорта и экспорта Azure копирует hello отсутствующий диапазон данных, соответствующей toohello большой двоичный объект hello `http://bobmediaaccount.blob.core.windows.net/pictures/animals/koala.jpg`.  
  
## <a name="resolving-conflicts-when-using-repairimport"></a>Разрешение конфликтов при использовании RepairImport  
В некоторых случаях средство hello не может быть, может toofind или Привет открыть необходимый файл по одной из следующих причин hello: не удалось найти файл hello, hello файл становится недоступным, hello имя файла является неоднозначным или содержимое hello hello файла является некорректным.  
  
Неоднозначный ошибка может возникать, если средство hello пытается toolocate `\animals\koala.jpg` и есть файл с таким именем и `C:\Users\bob\pictures` и `X:\BobBackup\photos`. То есть, и `C:\Users\bob\pictures\animals\koala.jpg` и `X:\BobBackup\photos\animals\koala.jpg` существует на дисках задания импорта hello.  
  
Hello `/PathMapFile` параметр позволяет tooresolve эти ошибки. Можно указать имя hello hello файл, содержащий список файлов, hello средство hello не смогла определить toocorrectly. Hello следующий пример командной строки заполняет `9WM35C2V_pathmap.txt`:  
  
```
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log /PathMapFile:C:\WAImportExport\9WM35C2V_pathmap.txt  
```
  
Hello затем средство запишет проблемные пути hello слишком`9WM35C2V_pathmap.txt`, одному в каждой строке. Например hello файл может содержать следующие записи после выполнения команды hello hello:  
 
```
\animals\koala.jpg  
\animals\kangaroo.jpg  
```
  
 Для каждого файла в списке hello следует установить toolocate и откройте файл tooensure hello, это средство доступных toohello. Средство hello tootell явным образом, где toofind файла можно изменить путь hello файл карты и добавить hello путь к файлу tooeach на hello одной строке, разделенные символом табуляции:  
  
```
\animals\koala.jpg           C:\Users\bob\Pictures\animals\koala.jpg  
\animals\kangaroo.jpg        X:\BobBackup\photos\animals\kangaroo.jpg  
```
  
После внесения hello необходимые файлы toohello доступные средства, или при обновлении hello путь файла карты можно повторно запустить процесс импорта hello toocomplete средство hello.  
  
## <a name="next-steps"></a>Дальнейшие действия
 
* [Установка hello средство импорта и экспорта Azure](storage-import-export-tool-setup-v1.md)   
* [Подготовка жестких дисков для задания импорта](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Просмотр состояния задания с помощью файлов журнала копирования](storage-import-export-tool-reviewing-job-status-v1.md)   
* [Подготовка задания экспорта](../storage-import-export-tool-repairing-an-export-job-v1.md)   
* [Устранение неполадок средства импорта и экспорта Azure hello](storage-import-export-tool-troubleshooting-v1.md)
