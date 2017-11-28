---
title: "Настройка инструмента импорта и экспорта Azure | Документация Майкрософт"
description: "Узнайте, как настроить инструмент подготовки и исправления дисков для службы импорта и экспорта Azure."
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
ms.openlocfilehash: 5b73fec119a88cd86e68537199e7567afa3fdba8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="setting-up-the-azure-importexport-tool"></a><span data-ttu-id="754da-103">Настройка инструмента импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="754da-103">Setting up the Azure Import/Export Tool</span></span>

<span data-ttu-id="754da-104">Инструмент импорта и экспорта Microsoft Azure используется в службе импорта и экспорта Microsoft Azure для подготовки и исправления дисков.</span><span class="sxs-lookup"><span data-stu-id="754da-104">The Microsoft Azure Import/Export Tool is the drive preparation and repair tool that you can use with the Microsoft Azure Import/Export service.</span></span> <span data-ttu-id="754da-105">Это средство может выполнять перечисленные ниже функции.</span><span class="sxs-lookup"><span data-stu-id="754da-105">You can use the tool for the following functions:</span></span>

* <span data-ttu-id="754da-106">С его помощью перед созданием задания импорта можно скопировать данные на жесткие диски, которые будут отправлены в центр обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="754da-106">Before creating an import job, you can use this tool to copy data to the hard drives you are going to ship to an Azure data center.</span></span>
* <span data-ttu-id="754da-107">После завершения задания импорта это средство можно использовать для восстановления поврежденных, отсутствующих или конфликтных больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="754da-107">After an import job has completed, you can use this tool to repair any blobs that were corrupted, were missing, or conflicted with other blobs.</span></span>
* <span data-ttu-id="754da-108">Это средство также позволяет восстанавливать на дисках поврежденные или отсутствующие файлы после завершения задания экспорта.</span><span class="sxs-lookup"><span data-stu-id="754da-108">After you receive the drives from a completed export job, you can use this tool to repair any files that were corrupted or missing on the drives.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="754da-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="754da-109">Prerequisites</span></span>

<span data-ttu-id="754da-110">При **подготовке дисков** для задания импорта необходимо выполнить следующие условия.</span><span class="sxs-lookup"><span data-stu-id="754da-110">If you are **preparing drives** for an import job, the following prerequisites must be met:</span></span>

* <span data-ttu-id="754da-111">У вас должна быть активная подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="754da-111">You must have an active Azure subscription.</span></span>
* <span data-ttu-id="754da-112">Она должна содержать учетную запись хранения с достаточным объемом свободного пространства для хранения файлов, которые будут импортированы.</span><span class="sxs-lookup"><span data-stu-id="754da-112">Your subscription must include a storage account with enough available space to store the files you are going to import.</span></span>
* <span data-ttu-id="754da-113">Требуется по крайней мере один из ключей доступа учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="754da-113">You need at least one of the storage account access keys.</span></span>
* <span data-ttu-id="754da-114">Необходим компьютер ("компьютер для копирования") с Windows 7, Windows Server 2008 R2 или более новой операционной системой Windows.</span><span class="sxs-lookup"><span data-stu-id="754da-114">You need a computer (the "copy machine") with Windows 7, Windows Server 2008 R2, or a newer Windows operating system installed.</span></span>
* <span data-ttu-id="754da-115">На этом компьютере должен быть установлен компонент .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="754da-115">The .NET Framework 4 must be installed on the copy machine.</span></span>
* <span data-ttu-id="754da-116">На компьютере для копирования должна быть включена служба BitLocker.</span><span class="sxs-lookup"><span data-stu-id="754da-116">BitLocker must be enabled on the copy machine.</span></span>
* <span data-ttu-id="754da-117">Требуется один или несколько пустых 3,5-дюймовых дисков SATA, подключенных к целевому компьютеру.</span><span class="sxs-lookup"><span data-stu-id="754da-117">You need one or more empty 3.5-inch SATA hard drives connected to the copy machine.</span></span>
* <span data-ttu-id="754da-118">Файлы, которые нужно импортировать, должны быть доступными на целевом компьютере, независимо от того, где они сохранены: в сетевой папке или на локальном жестком диске.</span><span class="sxs-lookup"><span data-stu-id="754da-118">The files you plan to import must be accessible from the copy machine, whether they are on a network share or a local hard drive.</span></span>

<span data-ttu-id="754da-119">Если вы пытаетесь **исправить операцию импорта**, которая была частично не выполнена, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="754da-119">If you are attempting to **repair an import** that has partially failed, you need:</span></span>

* <span data-ttu-id="754da-120">файлы журнала копирования;</span><span class="sxs-lookup"><span data-stu-id="754da-120">The copy log files</span></span>
* <span data-ttu-id="754da-121">ключ учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="754da-121">The storage account key</span></span>

<span data-ttu-id="754da-122">Если вы пытаетесь **исправить операцию экспорта**, которая была частично не выполнена, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="754da-122">If you are attempting to **repair an export**  that has partially failed, you need:</span></span>

* <span data-ttu-id="754da-123">файлы журнала копирования;</span><span class="sxs-lookup"><span data-stu-id="754da-123">The copy log files</span></span>
* <span data-ttu-id="754da-124">файлы манифеста (необязательно);</span><span class="sxs-lookup"><span data-stu-id="754da-124">The manifest files (optional)</span></span>
* <span data-ttu-id="754da-125">ключ учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="754da-125">The storage account key</span></span>

## <a name="installing-the-azure-importexport-tool"></a><span data-ttu-id="754da-126">Установка средства импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="754da-126">Installing the Azure Import/Export Tool</span></span>

<span data-ttu-id="754da-127">Сначала [скачайте инструмент импорта и экспорта Azure](https://www.microsoft.com/download/details.aspx?id=55280) и извлеките его в каталог на компьютере, например `c:\WAImportExport`.</span><span class="sxs-lookup"><span data-stu-id="754da-127">First, [download the Azure Import/Export Tool](https://www.microsoft.com/download/details.aspx?id=55280) and extract it to a directory on your computer, for example `c:\WAImportExport`.</span></span>

<span data-ttu-id="754da-128">Инструмент импорта и экспорта Azure состоит из следующих файлов:</span><span class="sxs-lookup"><span data-stu-id="754da-128">The Azure Import/Export Tool consists of the following files:</span></span>

* <span data-ttu-id="754da-129">dataset.csv</span><span class="sxs-lookup"><span data-stu-id="754da-129">dataset.csv</span></span>
* <span data-ttu-id="754da-130">driveset.csv</span><span class="sxs-lookup"><span data-stu-id="754da-130">driveset.csv</span></span>
* <span data-ttu-id="754da-131">hddid.dll</span><span class="sxs-lookup"><span data-stu-id="754da-131">hddid.dll</span></span>
* <span data-ttu-id="754da-132">Microsoft.Data.Services.Client.dll</span><span class="sxs-lookup"><span data-stu-id="754da-132">Microsoft.Data.Services.Client.dll</span></span>
* <span data-ttu-id="754da-133">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="754da-133">Microsoft.WindowsAzure.Storage.dll</span></span>
* <span data-ttu-id="754da-134">Microsoft.WindowsAzure.Storage.pdb</span><span class="sxs-lookup"><span data-stu-id="754da-134">Microsoft.WindowsAzure.Storage.pdb</span></span>
* <span data-ttu-id="754da-135">Microsoft.WindowsAzure.Storage.xml</span><span class="sxs-lookup"><span data-stu-id="754da-135">Microsoft.WindowsAzure.Storage.xml</span></span>
* <span data-ttu-id="754da-136">WAImportExport.exe</span><span class="sxs-lookup"><span data-stu-id="754da-136">WAImportExport.exe</span></span>
* <span data-ttu-id="754da-137">WAImportExport.exe.config</span><span class="sxs-lookup"><span data-stu-id="754da-137">WAImportExport.exe.config</span></span>
* <span data-ttu-id="754da-138">WAImportExport.pdb</span><span class="sxs-lookup"><span data-stu-id="754da-138">WAImportExport.pdb</span></span>
* <span data-ttu-id="754da-139">WAImportExportCore.dll</span><span class="sxs-lookup"><span data-stu-id="754da-139">WAImportExportCore.dll</span></span>
* <span data-ttu-id="754da-140">WAImportExportCore.pdb</span><span class="sxs-lookup"><span data-stu-id="754da-140">WAImportExportCore.pdb</span></span>
* <span data-ttu-id="754da-141">WAImportExportRepair.dll</span><span class="sxs-lookup"><span data-stu-id="754da-141">WAImportExportRepair.dll</span></span>
* <span data-ttu-id="754da-142">WAImportExportRepair.pdb</span><span class="sxs-lookup"><span data-stu-id="754da-142">WAImportExportRepair.pdb</span></span>

<span data-ttu-id="754da-143">После этого откройте окно командной строки с **правами администратора** и перейдите в каталог, содержащий извлеченные файлы.</span><span class="sxs-lookup"><span data-stu-id="754da-143">Next, open a Command Prompt window in **Administrator mode**, and change into the directory containing the extracted files.</span></span>

<span data-ttu-id="754da-144">Чтобы вывести справку по командам, запустите инструмент (`WAImportExport.exe`) без параметров.</span><span class="sxs-lookup"><span data-stu-id="754da-144">To output help for the command, run the tool (`WAImportExport.exe`) without parameters:</span></span>

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
        - Required. Path to the journal file. A journal file tracks a set of drives and
          records the progress in preparing these drives. The journal file must always
          be specified.
    /logdir:<LogDirectory>
        - Optional. The log directory. Verbose log files as well as some temporary
          files will be written to this directory. If not specified, current directory
          will be used as the log directory. The log directory can be specified only
          once for the same journal file.
    /id:<SessionId>
        - Optional. The session Id is used to identify a copy session. It is used to
          ensure accurate recovery of an interrupted copy session.
    /ResumeSession
        - Optional. If the last copy session was terminated abnormally, this parameter
          can be specified to resume the session.
    /AbortSession
        - Optional. If the last copy session was terminated abnormally, this parameter
          can be specified to abort the session.
    /sn:<StorageAccountName>
        - Required. Only applicable for RepairImport and RepairExport. The name of
          the storage account.
    /sk:<StorageAccountKey>
        - Required. The key of the storage account.
    /InitialDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of drives to prepare.
    /AdditionalDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of additional drives to be added.
    /r:<RepairFile>
        - Required. Only applicable for RepairImport and RepairExport.
          Path to the file for tracking repair progress. Each drive must have one
          and only one repair file.
    /d:<TargetDirectories>
        - Required. Only applicable for RepairImport and RepairExport.
          For RepairImport, one or more semicolon-separated directories to repair;
          For RepairExport, one directory to repair, e.g. root directory of the drive.
    /CopyLogFile:<DriveCopyLogFile>
        - Required. Only applicable for RepairImport and RepairExport. Path to the
          drive copy log file (verbose or error).
    /ManifestFile:<DriveManifestFile>
        - Required. Only applicable for RepairExport. Path to the drive manifest file.
    /PathMapFile:<DrivePathMapFile>
        - Optional. Only applicable for RepairImport. Path to the file containing
          mappings of file paths relative to the drive root to locations of actual files
          (tab-delimited). When first specified, it will be populated with file paths
          with empty targets, which means either they are not found in TargetDirectories,
          access denied, with invalid name, or they exist in multiple directories. The
          path map file can be manually edited to include the correct target paths and
          specified again for the tool to resolve the file paths correctly.
    /ExportBlobListFile:<ExportBlobListFile>
        - Required. Path to the XML file containing list of blob paths or blob path
          prefixes for the blobs to be exported. The file format is the same as the
          blob list blob format in the Put Job operation of the Import/Export Service
          REST API.
    /DriveSize:<DriveSize>
        - Required. Size of drives to be used for export. For example, 500GB, 1.5TB.
          Note: 1 GB = 1,000,000,000 bytes
                1 TB = 1,000,000,000,000 bytes
    /DataSet:<dataset.csv>
        - Required. A .csv file that contains a list of directories and/or a list files
          to be copied to target drives.

    /silentmode
        - Optional. If not specified, it will remind you the requirement of drives and
          need your confirmation to continue.

Examples:

    Copy a data set to a drive:
    WAImportExport.exe PrepImport
        /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GEL
        xmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /InitialDriveSet:driveset1.csv
        /DataSet:data.csv

    Copy another dataset to the same drive following the above command:
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

## <a name="next-steps"></a><span data-ttu-id="754da-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="754da-145">Next steps</span></span>

* [<span data-ttu-id="754da-146">Подготовка жестких дисков для задания импорта</span><span class="sxs-lookup"><span data-stu-id="754da-146">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="754da-147">Предварительный просмотр использования дисков для задания экспорта</span><span class="sxs-lookup"><span data-stu-id="754da-147">Previewing drive usage for an export job</span></span>](../storage-import-export-tool-previewing-drive-usage-export-v1.md)
* [<span data-ttu-id="754da-148">Просмотр состояния задания с помощью файлов журнала копирования</span><span class="sxs-lookup"><span data-stu-id="754da-148">Reviewing job status with copy log files</span></span>](../storage-import-export-tool-reviewing-job-status-v1.md)
* [<span data-ttu-id="754da-149">Подготовка задания импорта</span><span class="sxs-lookup"><span data-stu-id="754da-149">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)
* [<span data-ttu-id="754da-150">Подготовка задания экспорта</span><span class="sxs-lookup"><span data-stu-id="754da-150">Repairing an export job</span></span>](../storage-import-export-tool-repairing-an-export-job-v1.md)
* [<span data-ttu-id="754da-151">Устранение неполадок со средством импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="754da-151">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
