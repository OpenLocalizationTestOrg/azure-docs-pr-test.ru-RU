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
ms.openlocfilehash: 96c674fc7c697c37882fb2980c340303896ac6c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-export-job"></a><span data-ttu-id="1b68a-103">Исправление задания экспорта</span><span class="sxs-lookup"><span data-stu-id="1b68a-103">Repairing an export job</span></span>
<span data-ttu-id="1b68a-104">После завершения задания экспорта, можно запустить средство импорта и экспорта Microsoft Azure локально для hello:</span><span class="sxs-lookup"><span data-stu-id="1b68a-104">After an export job has completed, you can run hello Microsoft Azure Import/Export Tool on-premises to:</span></span>  
  
1.  <span data-ttu-id="1b68a-105">Загружайте никакие файлы, что служба импорта и экспорта Azure hello находилась tooexport не удается.</span><span class="sxs-lookup"><span data-stu-id="1b68a-105">Download any files that hello Azure Import/Export service was unable tooexport.</span></span>  
  
2.  <span data-ttu-id="1b68a-106">Проверьте, правильно экспортированы hello файлов на диске hello.</span><span class="sxs-lookup"><span data-stu-id="1b68a-106">Validate that hello files on hello drive were correctly exported.</span></span>  
  
<span data-ttu-id="1b68a-107">Необходимо иметь toouse хранения tooAzure подключения к этой функции.</span><span class="sxs-lookup"><span data-stu-id="1b68a-107">You must have connectivity tooAzure Storage toouse this functionality.</span></span>  
  
<span data-ttu-id="1b68a-108">Команда Hello для исправления задания импорта: **RepairExport**.</span><span class="sxs-lookup"><span data-stu-id="1b68a-108">hello command for repairing an import job is **RepairExport**.</span></span>

## <a name="repairexport-parameters"></a><span data-ttu-id="1b68a-109">Параметры RepairExport</span><span class="sxs-lookup"><span data-stu-id="1b68a-109">RepairExport parameters</span></span>

<span data-ttu-id="1b68a-110">Hello могут быть указаны следующие параметры с **RepairExport**:</span><span class="sxs-lookup"><span data-stu-id="1b68a-110">hello following parameters can be specified with **RepairExport**:</span></span>  
  
|<span data-ttu-id="1b68a-111">Параметр</span><span class="sxs-lookup"><span data-stu-id="1b68a-111">Parameter</span></span>|<span data-ttu-id="1b68a-112">Описание</span><span class="sxs-lookup"><span data-stu-id="1b68a-112">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="1b68a-113">**/r:<файл_восстановления\>**</span><span class="sxs-lookup"><span data-stu-id="1b68a-113">**/r:<RepairFile\>**</span></span>|<span data-ttu-id="1b68a-114">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="1b68a-114">Required.</span></span> <span data-ttu-id="1b68a-115">Путь toohello восстановить файл, который отслеживает ход выполнения восстановления hello hello и позволяет при tooresume прерванное восстановление.</span><span class="sxs-lookup"><span data-stu-id="1b68a-115">Path toohello repair file, which tracks hello progress of hello repair, and allows you tooresume an interrupted repair.</span></span> <span data-ttu-id="1b68a-116">Каждый диск должен быть связан с одним и только одним файлом восстановления.</span><span class="sxs-lookup"><span data-stu-id="1b68a-116">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="1b68a-117">При запуске восстановления для заданного диска вы передаете hello путь tooa файлу восстановления, который еще не существует.</span><span class="sxs-lookup"><span data-stu-id="1b68a-117">When you start a repair for a given drive, you will pass in hello path tooa repair file which does not yet exist.</span></span> <span data-ttu-id="1b68a-118">tooresume прерванное восстановление, необходимо передать в качестве имени hello существующего файла восстановления.</span><span class="sxs-lookup"><span data-stu-id="1b68a-118">tooresume an interrupted repair, you should pass in hello name of an existing repair file.</span></span> <span data-ttu-id="1b68a-119">всегда необходимо указать Hello восстановления файла соответствующий toohello целевой диск.</span><span class="sxs-lookup"><span data-stu-id="1b68a-119">hello repair file corresponding toohello target drive must always be specified.</span></span>|  
|<span data-ttu-id="1b68a-120">**/logdir:<каталог_журнала\>**</span><span class="sxs-lookup"><span data-stu-id="1b68a-120">**/logdir:<LogDirectory\>**</span></span>|<span data-ttu-id="1b68a-121">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="1b68a-121">Optional.</span></span> <span data-ttu-id="1b68a-122">каталог журнала Hello.</span><span class="sxs-lookup"><span data-stu-id="1b68a-122">hello log directory.</span></span> <span data-ttu-id="1b68a-123">Подробные журналы будут записаны toothis каталога.</span><span class="sxs-lookup"><span data-stu-id="1b68a-123">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="1b68a-124">Если журнал каталога не указан, текущий каталог hello будет использоваться как каталог журнала hello.</span><span class="sxs-lookup"><span data-stu-id="1b68a-124">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="1b68a-125">**/d:<целевой_каталог\>**</span><span class="sxs-lookup"><span data-stu-id="1b68a-125">**/d:<TargetDirectory\>**</span></span>|<span data-ttu-id="1b68a-126">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="1b68a-126">Required.</span></span> <span data-ttu-id="1b68a-127">каталог toovalidate Hello и восстановления.</span><span class="sxs-lookup"><span data-stu-id="1b68a-127">hello directory toovalidate and repair.</span></span> <span data-ttu-id="1b68a-128">Обычно это hello корневой каталог диска экспорта hello, но может также быть сетевую общую папку с копией hello экспортировать файлы.</span><span class="sxs-lookup"><span data-stu-id="1b68a-128">This is usually hello root directory of hello export drive, but could also be a network file share containing a copy of hello exported files.</span></span>|  
|<span data-ttu-id="1b68a-129">**/bk:<ключ_BitLocker\>**</span><span class="sxs-lookup"><span data-stu-id="1b68a-129">**/bk:<BitLockerKey\>**</span></span>|<span data-ttu-id="1b68a-130">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="1b68a-130">Optional.</span></span> <span data-ttu-id="1b68a-131">Ключ BitLocker hello следует указывать, если требуется toounlock средство hello хранятся зашифрованные который hello экспортироваться файлы.</span><span class="sxs-lookup"><span data-stu-id="1b68a-131">You should specify hello BitLocker key if you want hello tool toounlock an encrypted where hello exported files are stored.</span></span>|  
|<span data-ttu-id="1b68a-132">**/sn:<учетная_запись_хранения\>**</span><span class="sxs-lookup"><span data-stu-id="1b68a-132">**/sn:<StorageAccountName\>**</span></span>|<span data-ttu-id="1b68a-133">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="1b68a-133">Required.</span></span> <span data-ttu-id="1b68a-134">Задание экспорта Hello имя учетной записи хранения hello hello.</span><span class="sxs-lookup"><span data-stu-id="1b68a-134">hello name of hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="1b68a-135">**/sk:<ключ_учетной_записи_хранения\>**</span><span class="sxs-lookup"><span data-stu-id="1b68a-135">**/sk:<StorageAccountKey\>**</span></span>|<span data-ttu-id="1b68a-136">**Требуется**, только если не указан SAS контейнера.</span><span class="sxs-lookup"><span data-stu-id="1b68a-136">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="1b68a-137">Задание экспорта Hello ключ учетной записи хранилища hello для hello.</span><span class="sxs-lookup"><span data-stu-id="1b68a-137">hello account key for hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="1b68a-138">**/csas:<SAS_контейнера\>**</span><span class="sxs-lookup"><span data-stu-id="1b68a-138">**/csas:<ContainerSas\>**</span></span>|<span data-ttu-id="1b68a-139">**Требуется** только в том случае, если не указан ключ учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="1b68a-139">**Required** if and only if hello storage account key is not specified.</span></span> <span data-ttu-id="1b68a-140">Hello SAS контейнера для доступа к большим двоичным объектам hello, связанный с заданием экспорта hello.</span><span class="sxs-lookup"><span data-stu-id="1b68a-140">hello container SAS for accessing hello blobs associated with hello export job.</span></span>|  
|<span data-ttu-id="1b68a-141">**/CopyLogFile:<файл_журнала\>**</span><span class="sxs-lookup"><span data-stu-id="1b68a-141">**/CopyLogFile:<DriveCopyLogFile\>**</span></span>|<span data-ttu-id="1b68a-142">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="1b68a-142">Required.</span></span> <span data-ttu-id="1b68a-143">Hello путь toohello файлу журнала копирования диска.</span><span class="sxs-lookup"><span data-stu-id="1b68a-143">hello path toohello drive copy log file.</span></span> <span data-ttu-id="1b68a-144">файл Hello формируется hello службы импорта и экспорта Windows Azure и можно загрузить из хранилища больших двоичных объектов hello, связанный с заданием hello.</span><span class="sxs-lookup"><span data-stu-id="1b68a-144">hello file is generated by hello Windows Azure Import/Export service and can be downloaded from hello blob storage associated with hello job.</span></span> <span data-ttu-id="1b68a-145">файл журнала копирования Hello содержит сведения о неудачных больших двоичных объектов или файлов, являющихся toobe исправить.</span><span class="sxs-lookup"><span data-stu-id="1b68a-145">hello copy log file contains information about failed blobs or files which are toobe repaired.</span></span>|  
|<span data-ttu-id="1b68a-146">**/ ManifestFile:<файл_манифеста_диска\>**</span><span class="sxs-lookup"><span data-stu-id="1b68a-146">**/ManifestFile:<DriveManifestFile\>**</span></span>|<span data-ttu-id="1b68a-147">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="1b68a-147">Optional.</span></span> <span data-ttu-id="1b68a-148">файл манифеста toohello экспорта Hello путь диска.</span><span class="sxs-lookup"><span data-stu-id="1b68a-148">hello path toohello export drive's manifest file.</span></span> <span data-ttu-id="1b68a-149">Этот файл создается службой импорта и экспорта Windows Azure hello и сохраняется на диске экспорта hello и при необходимости в большом двоичном объекте в учетной записи хранения hello, связанный с заданием hello.</span><span class="sxs-lookup"><span data-stu-id="1b68a-149">This file is generated by hello Windows Azure Import/Export service and stored on hello export drive, and optionally in a blob in hello storage account associated with hello job.</span></span><br /><br /> <span data-ttu-id="1b68a-150">Hello содержимое hello файлов на диске hello экспорта будет проверено с MD5-хэшей hello в этом файле содержится.</span><span class="sxs-lookup"><span data-stu-id="1b68a-150">hello content of hello files on hello export drive will be verified with hello MD5 hashes contained in this file.</span></span> <span data-ttu-id="1b68a-151">Все файлы, определяется toobe поврежден, будут загружены и перезаписанного toohello целевые каталоги.</span><span class="sxs-lookup"><span data-stu-id="1b68a-151">Any files that are determined toobe corrupted will be downloaded and rewritten toohello target directories.</span></span>|  
  
## <a name="using-repairexport-mode-toocorrect-failed-exports"></a><span data-ttu-id="1b68a-152">Использование режима RepairExport toocorrect режим не удалось выполнить экспорт</span><span class="sxs-lookup"><span data-stu-id="1b68a-152">Using RepairExport mode toocorrect failed exports</span></span>  
<span data-ttu-id="1b68a-153">Можно использовать файлы toodownload средство импорта и экспорта Azure hello, не прошедшие tooexport.</span><span class="sxs-lookup"><span data-stu-id="1b68a-153">You can use hello Azure Import/Export Tool toodownload files that failed tooexport.</span></span> <span data-ttu-id="1b68a-154">файл журнала копирования Hello будет содержать список файлов, которые не удалось tooexport.</span><span class="sxs-lookup"><span data-stu-id="1b68a-154">hello copy log file will contain a list of files that failed tooexport.</span></span>  
  
<span data-ttu-id="1b68a-155">Hello причины сбоев экспорта hello следующие возможности:</span><span class="sxs-lookup"><span data-stu-id="1b68a-155">hello causes of export failures include hello following possibilities:</span></span>  
  
-   <span data-ttu-id="1b68a-156">повреждение дисков;</span><span class="sxs-lookup"><span data-stu-id="1b68a-156">Damaged drives</span></span>  
  
-   <span data-ttu-id="1b68a-157">ключ учетной записи хранения Hello, изменился в процессе передачи hello</span><span class="sxs-lookup"><span data-stu-id="1b68a-157">hello storage account key changed during hello transfer process</span></span>  
  
<span data-ttu-id="1b68a-158">Средство toorun hello в **RepairExport** режиме, необходимо сначала tooconnect hello диск, содержащий компьютер tooyour hello экспортированные файлы.</span><span class="sxs-lookup"><span data-stu-id="1b68a-158">toorun hello tool in **RepairExport** mode, you first need tooconnect hello drive containing hello exported files tooyour computer.</span></span> <span data-ttu-id="1b68a-159">После этого запустите средство импорта и экспорта Azure, при указании hello путь toothat диска с hello hello `/d` параметра.</span><span class="sxs-lookup"><span data-stu-id="1b68a-159">Next, run hello Azure Import/Export Tool, specifying hello path toothat drive with hello `/d` parameter.</span></span> <span data-ttu-id="1b68a-160">Необходимо также файлу журнала копирования путь toohello toospecify hello диска загруженный.</span><span class="sxs-lookup"><span data-stu-id="1b68a-160">You also need toospecify hello path toohello drive's copy log file that you downloaded.</span></span> <span data-ttu-id="1b68a-161">Hello следующий пример командной строки запускает средство toorepair hello все файлы, которые не удалось выполнить tooexport:</span><span class="sxs-lookup"><span data-stu-id="1b68a-161">hello following command line example below runs hello tool toorepair any files that failed tooexport:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
<span data-ttu-id="1b68a-162">Hello ниже приведен пример файла журнала копирования, показано, что один блок в tooexport hello больших двоичных объектов не удалось:</span><span class="sxs-lookup"><span data-stu-id="1b68a-162">hello following is an example of a copy log file that shows that one block in hello blob failed tooexport:</span></span>  
  
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
  
<span data-ttu-id="1b68a-163">файл журнала копирования Hello указывает, что сбой произошел, когда hello службы импорта и экспорта Windows Azure загружала один hello большого двоичного объекта файла toohello блоков на диске экспорта hello.</span><span class="sxs-lookup"><span data-stu-id="1b68a-163">hello copy log file indicates that a failure occurred while hello Windows Azure Import/Export service was downloading one of hello blob's blocks toohello file on hello export drive.</span></span> <span data-ttu-id="1b68a-164">Здравствуйте, другие компоненты успешно загружены файл hello и hello длина файла была задана правильно.</span><span class="sxs-lookup"><span data-stu-id="1b68a-164">hello other components of hello file downloaded successfully, and hello file length was correctly set.</span></span> <span data-ttu-id="1b68a-165">В этом случае средство hello откройте hello файл на диске hello, загрузить hello блок из учетной записи хранения hello и записать их в диапазон файлов toohello, начиная со смещения 65536 с длиной 65536.</span><span class="sxs-lookup"><span data-stu-id="1b68a-165">In this case, hello tool will open hello file on hello drive, download hello block from hello storage account, and write it toohello file range starting from offset 65536 with length 65536.</span></span>  
  
## <a name="using-repairexport-toovalidate-drive-contents"></a><span data-ttu-id="1b68a-166">С помощью содержимого диска toovalidate RepairExport</span><span class="sxs-lookup"><span data-stu-id="1b68a-166">Using RepairExport toovalidate drive contents</span></span>  
<span data-ttu-id="1b68a-167">Можно также использовать импорта и экспорта Azure с hello **RepairExport** параметр toovalidate hello содержимое на диске hello заданы правильно.</span><span class="sxs-lookup"><span data-stu-id="1b68a-167">You can also use Azure Import/Export with hello **RepairExport** option toovalidate hello contents on hello drive are correct.</span></span> <span data-ttu-id="1b68a-168">файл манифеста Hello на каждом диске экспорта содержит MD5-хэши для содержимого hello hello диска.</span><span class="sxs-lookup"><span data-stu-id="1b68a-168">hello manifest file on each export drive contains MD5s for hello contents of hello drive.</span></span>  
  
<span data-ttu-id="1b68a-169">Hello службы импорта и экспорта Azure также можно сохранить файлы манифеста hello tooa учетной записи хранения во время процесса экспорта hello.</span><span class="sxs-lookup"><span data-stu-id="1b68a-169">hello Azure Import/Export service can also save hello manifest files tooa storage account during hello export process.</span></span> <span data-ttu-id="1b68a-170">Hello расположения файлов манифеста hello доступен через hello [получения задания](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) операцию при завершении задания hello.</span><span class="sxs-lookup"><span data-stu-id="1b68a-170">hello location of hello manifest files is available via hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation when hello job has completed.</span></span> <span data-ttu-id="1b68a-171">В разделе [службы импорта и экспорта формат файла манифеста](storage-import-export-file-format-metadata-and-properties.md) Дополнительные сведения о формате hello файла манифеста диска.</span><span class="sxs-lookup"><span data-stu-id="1b68a-171">See [Import/Export service Manifest File Format](storage-import-export-file-format-metadata-and-properties.md) for more information about hello format of a drive manifest file.</span></span>  
  
<span data-ttu-id="1b68a-172">Hello следующем примере показано, как toorun hello средство импорта и экспорта Azure с hello **/ManifestFile** и **/CopyLogFile** параметры:</span><span class="sxs-lookup"><span data-stu-id="1b68a-172">hello following example shows how toorun hello Azure Import/Export Tool with hello **/ManifestFile** and **/CopyLogFile** parameters:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
<span data-ttu-id="1b68a-173">Hello ниже приведен пример файла манифеста:</span><span class="sxs-lookup"><span data-stu-id="1b68a-173">hello following is an example of a manifest file:</span></span>  
  
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
  
<span data-ttu-id="1b68a-174">После завершения процесса восстановления hello программа hello прочтите каждый файл, указанный в файле манифеста hello и проверки целостности файла hello с hello MD5-хэшей.</span><span class="sxs-lookup"><span data-stu-id="1b68a-174">After finishing hello repair process, hello tool will read through each file referenced in hello manifest file and verify hello file's integrity with hello MD5 hashes.</span></span> <span data-ttu-id="1b68a-175">Манифест hello выше он проходит через hello следующие компоненты.</span><span class="sxs-lookup"><span data-stu-id="1b68a-175">For hello manifest above, it will go through hello following components.</span></span>  

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

<span data-ttu-id="1b68a-176">Любой компонент, сбой проверки hello загружается средством hello и переписать toohello тот же файл на диске hello.</span><span class="sxs-lookup"><span data-stu-id="1b68a-176">Any component failing hello verification will be downloaded by hello tool and rewritten toohello same file on hello drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="1b68a-177">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1b68a-177">Next steps</span></span>
 
* [<span data-ttu-id="1b68a-178">Установка hello средство импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="1b68a-178">Setting Up hello Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="1b68a-179">Подготовка жестких дисков для задания импорта</span><span class="sxs-lookup"><span data-stu-id="1b68a-179">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="1b68a-180">Просмотр состояния задания с помощью файлов журнала копирования</span><span class="sxs-lookup"><span data-stu-id="1b68a-180">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="1b68a-181">Подготовка задания импорта</span><span class="sxs-lookup"><span data-stu-id="1b68a-181">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="1b68a-182">Устранение неполадок средства импорта и экспорта Azure hello</span><span class="sxs-lookup"><span data-stu-id="1b68a-182">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
