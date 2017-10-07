---
title: "aaaSetting копирование hello средство импорта и экспорта Azure | Документы Microsoft"
description: "Узнайте, как tooset копирование hello диска средство подготовки и восстановления для службы импорта и экспорта Azure hello."
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
ms.date: 06/29/2017
ms.author: muralikk
ms.openlocfilehash: ee5bb99bd84ea5ee2f6b6e99c5a375b215e94ea8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-hello-azure-importexport-tool"></a>Настройка hello средство импорта и экспорта Azure

Hello средство импорта и экспорта Microsoft Azure — hello диск средство подготовки и восстановления, можно использовать с hello службы импорта и экспорта Microsoft Azure. Можно использовать средство hello для hello, следующие функции:

* Перед созданием задания импорта, можно использовать этот инструмент toocopy данных toohello жестких дисков будет центр обработки данных Azure tooan tooship.
* После завершения задания импорта, можно использовать этот инструмент toorepair все большие двоичные объекты, которые были повреждены, были потеряны или конфликтуют с другими большими двоичными объектами.
* После получения hello диски с выполненным заданием экспорта, можно использовать этот инструмент toorepair все файлы, которые были повреждены или отсутствуют на дисках hello.

## <a name="prerequisites"></a>Предварительные требования

Если вы являетесь **Подготовка дисков** для задания импорта, должны быть выполнены следующие предварительные требования hello:

* У вас должна быть активная подписка Azure.
* Ваша подписка должна включать учетную запись хранения с файлами hello toostore достаточно свободного места будет tooimport.
* Требуется по крайней мере один из ключей доступа учетных записей хранилища hello.
* Необходимо иметь компьютер (hello «машина для копирования») с Windows 7, Windows Server 2008 R2 или более новой операционной системы Windows.
* .NET Framework 4 Hello должны быть установлены на компьютере копии hello.
* Необходимо включить BitLocker на компьютере копии hello.
* Требуется один или несколько пустых 3,5 дюймовых SATA жестких дисков toohello копирования машина подключена.
* Планирование tooimport файлы Hello должен быть доступен с компьютера копирования hello, ли они находятся в общей сетевой папке или на локальный жесткий диск.

Если вы пытаетесь слишком**восстановить Импорт** , частично завершился ошибкой, необходимо:

* файлы журнала копирования Hello
* ключ учетной записи хранения Hello

Если вы пытаетесь слишком**восстановить Экспорт** , частично завершился ошибкой, необходимо:

* файлы журнала копирования Hello
* файлы манифеста Hello (необязательно)
* ключ учетной записи хранения Hello

## <a name="installing-hello-azure-importexport-tool"></a>Установка средства импорта и экспорта Azure hello

Во-первых, [загрузить средство импорта и экспорта Azure hello](https://www.microsoft.com/download/details.aspx?id=55280) и извлеките его tooa каталог на локальном компьютере, например `c:\WAImportExport`.

Hello средство импорта и экспорта Azure состоит из hello следующие файлы:

* dataset.csv
* driveset.csv
* hddid.dll
* Microsoft.Data.Services.Client.dll
* Microsoft.WindowsAzure.Storage.dll
* Microsoft.WindowsAzure.Storage.pdb
* Microsoft.WindowsAzure.Storage.xml
* WAImportExport.exe
* WAImportExport.exe.config
* WAImportExport.pdb
* WAImportExportCore.dll
* WAImportExportCore.pdb
* WAImportExportRepair.dll
* WAImportExportRepair.pdb

Затем откройте окно командной строки в **администратора**, и изменения в каталог hello, содержащий hello извлеченные файлы.

toooutput справку по команде hello, запустите средство hello (`WAImportExport.exe`) без параметров:

```
WAImportExport, a client tool for Windows Azure Import/Export Service. Microsoft (c) 2013


Copy directories and/or files with a new copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>]
        [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>]
        DataSet:<dataset.csv>

Add more drives:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AdditionalDriveSet:<driveset.csv>

Abort an interrupted copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AbortSession

Resume an interrupted copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /ResumeSession

List drives:
    WAImportExport.exe PrepImport /j:<JournalFile> /ListDrives

List copy sessions:
    WAImportExport.exe PrepImport /j:<JournalFile> /ListCopySessions

Repair a Drive:
    WAImportExport.exe RepairImport | RepairExport
        /r:<RepairFile> [/logdir:<LogDirectory>]
        [/d:<TargetDirectories>] [/bk:<BitLockerKey>]
        /sn:<StorageAccountName> /sk:<StorageAccountKey>
        [/CopyLogFile:<DriveCopyLogFile>] [/ManifestFile:<DriveManifestFile>]
        [/PathMapFile:<DrivePathMapFile>]

Preview an Export Job:
    WAImportExport.exe PreviewExport
        [/logdir:<LogDirectory>]
        /sn:<StorageAccountName> /sk:<StorageAccountKey>
        /ExportBlobListFile:<ExportBlobListFile> /DriveSize:<DriveSize>

Parameters:

    /j:<JournalFile>
        - Required. Path toohello journal file. A journal file tracks a set of drives and
          records hello progress in preparing these drives. hello journal file must always
          be specified.
    /logdir:<LogDirectory>
        - Optional. hello log directory. Verbose log files as well as some temporary
          files will be written toothis directory. If not specified, current directory
          will be used as hello log directory. hello log directory can be specified only
          once for hello same journal file.
    /id:<SessionId>
        - Optional. hello session Id is used tooidentify a copy session. It is used to
          ensure accurate recovery of an interrupted copy session.
    /ResumeSession
        - Optional. If hello last copy session was terminated abnormally, this parameter
          can be specified tooresume hello session.
    /AbortSession
        - Optional. If hello last copy session was terminated abnormally, this parameter
          can be specified tooabort hello session.
    /sn:<StorageAccountName>
        - Required. Only applicable for RepairImport and RepairExport. hello name of
          hello storage account.
    /sk:<StorageAccountKey>
        - Required. hello key of hello storage account.
    /InitialDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of drives tooprepare.
    /AdditionalDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of additional drives toobe added.
    /r:<RepairFile>
        - Required. Only applicable for RepairImport and RepairExport.
          Path toohello file for tracking repair progress. Each drive must have one
          and only one repair file.
    /d:<TargetDirectories>
        - Required. Only applicable for RepairImport and RepairExport.
          For RepairImport, one or more semicolon-separated directories toorepair;
          For RepairExport, one directory toorepair, e.g. root directory of hello drive.
    /CopyLogFile:<DriveCopyLogFile>
        - Required. Only applicable for RepairImport and RepairExport. Path toothe
          drive copy log file (verbose or error).
    /ManifestFile:<DriveManifestFile>
        - Required. Only applicable for RepairExport. Path toohello drive manifest file.
    /PathMapFile:<DrivePathMapFile>
        - Optional. Only applicable for RepairImport. Path toohello file containing
          mappings of file paths relative toohello drive root toolocations of actual files
          (tab-delimited). When first specified, it will be populated with file paths
          with empty targets, which means either they are not found in TargetDirectories,
          access denied, with invalid name, or they exist in multiple directories. The
          path map file can be manually edited tooinclude hello correct target paths and
          specified again for hello tool tooresolve hello file paths correctly.
    /ExportBlobListFile:<ExportBlobListFile>
        - Required. Path toohello XML file containing list of blob paths or blob path
          prefixes for hello blobs toobe exported. hello file format is hello same as the
          blob list blob format in hello Put Job operation of hello Import/Export Service
          REST API.
    /DriveSize:<DriveSize>
        - Required. Size of drives toobe used for export. For example, 500GB, 1.5TB.
          Note: 1 GB = 1,000,000,000 bytes
                1 TB = 1,000,000,000,000 bytes
    /DataSet:<dataset.csv>
        - Required. A .csv file that contains a list of directories and/or a list files
          toobe copied tootarget drives.

    /silentmode
        - Optional. If not specified, it will remind you hello requirement of drives and
          need your confirmation toocontinue.

Examples:

    Copy a data set tooa drive:
    WAImportExport.exe PrepImport
        /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GEL
        xmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /InitialDriveSet:driveset1.csv
        /DataSet:data.csv

    Copy another dataset toohello same drive following hello above command:
    WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#2 /DataSet:dataset2.csv

    Preview how many 1.5 TB drives are needed for an export job:
    WAImportExport.exe PreviewExport
        /sn:mytestaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7K
        ysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\temp\myexportbloblist.xml
        /DriveSize:1.5TB

    Repair an finished import job:
    WAImportExport.exe RepairImport
        /r:9WM35C2V.rep /d:X:\ /bk:442926-020713-108086-436744-137335-435358-242242-2795
        98 /sn:mytestaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94
        f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\temp\9WM35C2V_error.log
```

## <a name="next-steps"></a>Дальнейшие действия

* [Подготовка жестких дисков для задания импорта](storage-import-export-tool-preparing-hard-drives-import.md)
* [Предварительный просмотр использования дисков для задания экспорта](storage-import-export-tool-previewing-drive-usage-export-v1.md)
* [Просмотр состояния задания с помощью файлов журнала копирования](storage-import-export-tool-reviewing-job-status-v1.md)
* [Подготовка задания импорта](storage-import-export-tool-repairing-an-import-job-v1.md)
* [Подготовка задания экспорта](storage-import-export-tool-repairing-an-export-job-v1.md)
* [Устранение неполадок средства импорта и экспорта Azure hello](storage-import-export-tool-troubleshooting-v1.md)
