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
ms.openlocfilehash: 3d8897f2783112e07123669f1ba5b22576770e60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-hello-azure-importexport-tool"></a><span data-ttu-id="f24ce-103">Настройка hello средство импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="f24ce-103">Setting up hello Azure Import/Export Tool</span></span>

<span data-ttu-id="f24ce-104">Hello средство импорта и экспорта Microsoft Azure — hello диск средство подготовки и восстановления, можно использовать с hello службы импорта и экспорта Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f24ce-104">hello Microsoft Azure Import/Export Tool is hello drive preparation and repair tool that you can use with hello Microsoft Azure Import/Export service.</span></span> <span data-ttu-id="f24ce-105">Можно использовать средство hello для hello, следующие функции:</span><span class="sxs-lookup"><span data-stu-id="f24ce-105">You can use hello tool for hello following functions:</span></span>

* <span data-ttu-id="f24ce-106">Перед созданием задания импорта, можно использовать этот инструмент toocopy данных toohello жестких дисков будет центр обработки данных Azure tooan tooship.</span><span class="sxs-lookup"><span data-stu-id="f24ce-106">Before creating an import job, you can use this tool toocopy data toohello hard drives you are going tooship tooan Azure data center.</span></span>
* <span data-ttu-id="f24ce-107">После завершения задания импорта, можно использовать этот инструмент toorepair все большие двоичные объекты, которые были повреждены, были потеряны или конфликтуют с другими большими двоичными объектами.</span><span class="sxs-lookup"><span data-stu-id="f24ce-107">After an import job has completed, you can use this tool toorepair any blobs that were corrupted, were missing, or conflicted with other blobs.</span></span>
* <span data-ttu-id="f24ce-108">После получения hello диски с выполненным заданием экспорта, можно использовать этот инструмент toorepair все файлы, которые были повреждены или отсутствуют на дисках hello.</span><span class="sxs-lookup"><span data-stu-id="f24ce-108">After you receive hello drives from a completed export job, you can use this tool toorepair any files that were corrupted or missing on hello drives.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f24ce-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f24ce-109">Prerequisites</span></span>

<span data-ttu-id="f24ce-110">Если вы являетесь **Подготовка дисков** для задания импорта, должны быть выполнены следующие предварительные требования hello:</span><span class="sxs-lookup"><span data-stu-id="f24ce-110">If you are **preparing drives** for an import job, hello following prerequisites must be met:</span></span>

* <span data-ttu-id="f24ce-111">У вас должна быть активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="f24ce-111">You must have an active Azure subscription.</span></span>
* <span data-ttu-id="f24ce-112">Ваша подписка должна включать учетную запись хранения с файлами hello toostore достаточно свободного места будет tooimport.</span><span class="sxs-lookup"><span data-stu-id="f24ce-112">Your subscription must include a storage account with enough available space toostore hello files you are going tooimport.</span></span>
* <span data-ttu-id="f24ce-113">Требуется по крайней мере один из ключей доступа учетных записей хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="f24ce-113">You need at least one of hello storage account access keys.</span></span>
* <span data-ttu-id="f24ce-114">Необходимо иметь компьютер (hello «машина для копирования») с Windows 7, Windows Server 2008 R2 или более новой операционной системы Windows.</span><span class="sxs-lookup"><span data-stu-id="f24ce-114">You need a computer (hello "copy machine") with Windows 7, Windows Server 2008 R2, or a newer Windows operating system installed.</span></span>
* <span data-ttu-id="f24ce-115">.NET Framework 4 Hello должны быть установлены на компьютере копии hello.</span><span class="sxs-lookup"><span data-stu-id="f24ce-115">hello .NET Framework 4 must be installed on hello copy machine.</span></span>
* <span data-ttu-id="f24ce-116">Необходимо включить BitLocker на компьютере копии hello.</span><span class="sxs-lookup"><span data-stu-id="f24ce-116">BitLocker must be enabled on hello copy machine.</span></span>
* <span data-ttu-id="f24ce-117">Требуется один или несколько пустых 3,5 дюймовых SATA жестких дисков toohello копирования машина подключена.</span><span class="sxs-lookup"><span data-stu-id="f24ce-117">You need one or more empty 3.5-inch SATA hard drives connected toohello copy machine.</span></span>
* <span data-ttu-id="f24ce-118">Планирование tooimport файлы Hello должен быть доступен с компьютера копирования hello, ли они находятся в общей сетевой папке или на локальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="f24ce-118">hello files you plan tooimport must be accessible from hello copy machine, whether they are on a network share or a local hard drive.</span></span>

<span data-ttu-id="f24ce-119">Если вы пытаетесь слишком**восстановить Импорт** , частично завершился ошибкой, необходимо:</span><span class="sxs-lookup"><span data-stu-id="f24ce-119">If you are attempting too**repair an import** that has partially failed, you need:</span></span>

* <span data-ttu-id="f24ce-120">файлы журнала копирования Hello</span><span class="sxs-lookup"><span data-stu-id="f24ce-120">hello copy log files</span></span>
* <span data-ttu-id="f24ce-121">ключ учетной записи хранения Hello</span><span class="sxs-lookup"><span data-stu-id="f24ce-121">hello storage account key</span></span>

<span data-ttu-id="f24ce-122">Если вы пытаетесь слишком**восстановить Экспорт** , частично завершился ошибкой, необходимо:</span><span class="sxs-lookup"><span data-stu-id="f24ce-122">If you are attempting too**repair an export**  that has partially failed, you need:</span></span>

* <span data-ttu-id="f24ce-123">файлы журнала копирования Hello</span><span class="sxs-lookup"><span data-stu-id="f24ce-123">hello copy log files</span></span>
* <span data-ttu-id="f24ce-124">файлы манифеста Hello (необязательно)</span><span class="sxs-lookup"><span data-stu-id="f24ce-124">hello manifest files (optional)</span></span>
* <span data-ttu-id="f24ce-125">ключ учетной записи хранения Hello</span><span class="sxs-lookup"><span data-stu-id="f24ce-125">hello storage account key</span></span>

## <a name="installing-hello-azure-importexport-tool"></a><span data-ttu-id="f24ce-126">Установка средства импорта и экспорта Azure hello</span><span class="sxs-lookup"><span data-stu-id="f24ce-126">Installing hello Azure Import/Export Tool</span></span>

<span data-ttu-id="f24ce-127">Во-первых, [загрузить средство импорта и экспорта Azure hello](https://www.microsoft.com/download/details.aspx?id=55280) и извлеките его tooa каталог на локальном компьютере, например `c:\WAImportExport`.</span><span class="sxs-lookup"><span data-stu-id="f24ce-127">First, [download hello Azure Import/Export Tool](https://www.microsoft.com/download/details.aspx?id=55280) and extract it tooa directory on your computer, for example `c:\WAImportExport`.</span></span>

<span data-ttu-id="f24ce-128">Hello средство импорта и экспорта Azure состоит из hello следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="f24ce-128">hello Azure Import/Export Tool consists of hello following files:</span></span>

* <span data-ttu-id="f24ce-129">dataset.csv</span><span class="sxs-lookup"><span data-stu-id="f24ce-129">dataset.csv</span></span>
* <span data-ttu-id="f24ce-130">driveset.csv</span><span class="sxs-lookup"><span data-stu-id="f24ce-130">driveset.csv</span></span>
* <span data-ttu-id="f24ce-131">hddid.dll</span><span class="sxs-lookup"><span data-stu-id="f24ce-131">hddid.dll</span></span>
* <span data-ttu-id="f24ce-132">Microsoft.Data.Services.Client.dll</span><span class="sxs-lookup"><span data-stu-id="f24ce-132">Microsoft.Data.Services.Client.dll</span></span>
* <span data-ttu-id="f24ce-133">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="f24ce-133">Microsoft.WindowsAzure.Storage.dll</span></span>
* <span data-ttu-id="f24ce-134">Microsoft.WindowsAzure.Storage.pdb</span><span class="sxs-lookup"><span data-stu-id="f24ce-134">Microsoft.WindowsAzure.Storage.pdb</span></span>
* <span data-ttu-id="f24ce-135">Microsoft.WindowsAzure.Storage.xml</span><span class="sxs-lookup"><span data-stu-id="f24ce-135">Microsoft.WindowsAzure.Storage.xml</span></span>
* <span data-ttu-id="f24ce-136">WAImportExport.exe</span><span class="sxs-lookup"><span data-stu-id="f24ce-136">WAImportExport.exe</span></span>
* <span data-ttu-id="f24ce-137">WAImportExport.exe.config</span><span class="sxs-lookup"><span data-stu-id="f24ce-137">WAImportExport.exe.config</span></span>
* <span data-ttu-id="f24ce-138">WAImportExport.pdb</span><span class="sxs-lookup"><span data-stu-id="f24ce-138">WAImportExport.pdb</span></span>
* <span data-ttu-id="f24ce-139">WAImportExportCore.dll</span><span class="sxs-lookup"><span data-stu-id="f24ce-139">WAImportExportCore.dll</span></span>
* <span data-ttu-id="f24ce-140">WAImportExportCore.pdb</span><span class="sxs-lookup"><span data-stu-id="f24ce-140">WAImportExportCore.pdb</span></span>
* <span data-ttu-id="f24ce-141">WAImportExportRepair.dll</span><span class="sxs-lookup"><span data-stu-id="f24ce-141">WAImportExportRepair.dll</span></span>
* <span data-ttu-id="f24ce-142">WAImportExportRepair.pdb</span><span class="sxs-lookup"><span data-stu-id="f24ce-142">WAImportExportRepair.pdb</span></span>

<span data-ttu-id="f24ce-143">Затем откройте окно командной строки в **администратора**, и изменения в каталог hello, содержащий hello извлеченные файлы.</span><span class="sxs-lookup"><span data-stu-id="f24ce-143">Next, open a Command Prompt window in **Administrator mode**, and change into hello directory containing hello extracted files.</span></span>

<span data-ttu-id="f24ce-144">toooutput справку по команде hello, запустите средство hello (`WAImportExport.exe`) без параметров:</span><span class="sxs-lookup"><span data-stu-id="f24ce-144">toooutput help for hello command, run hello tool (`WAImportExport.exe`) without parameters:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f24ce-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f24ce-145">Next steps</span></span>

* [<span data-ttu-id="f24ce-146">Подготовка жестких дисков для задания импорта</span><span class="sxs-lookup"><span data-stu-id="f24ce-146">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="f24ce-147">Предварительный просмотр использования дисков для задания экспорта</span><span class="sxs-lookup"><span data-stu-id="f24ce-147">Previewing drive usage for an export job</span></span>](../storage-import-export-tool-previewing-drive-usage-export-v1.md)
* [<span data-ttu-id="f24ce-148">Просмотр состояния задания с помощью файлов журнала копирования</span><span class="sxs-lookup"><span data-stu-id="f24ce-148">Reviewing job status with copy log files</span></span>](../storage-import-export-tool-reviewing-job-status-v1.md)
* [<span data-ttu-id="f24ce-149">Подготовка задания импорта</span><span class="sxs-lookup"><span data-stu-id="f24ce-149">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)
* [<span data-ttu-id="f24ce-150">Подготовка задания экспорта</span><span class="sxs-lookup"><span data-stu-id="f24ce-150">Repairing an export job</span></span>](../storage-import-export-tool-repairing-an-export-job-v1.md)
* [<span data-ttu-id="f24ce-151">Устранение неполадок средства импорта и экспорта Azure hello</span><span class="sxs-lookup"><span data-stu-id="f24ce-151">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
