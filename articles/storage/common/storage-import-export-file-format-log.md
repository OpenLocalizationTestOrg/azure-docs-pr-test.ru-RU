---
title: "формат файла журнала импорта и экспорта aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о формате hello hello файлов журналов, созданные при выполнении шагов для задания службы импорта и экспорта."
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
ms.openlocfilehash: 15a652455aa947922af0aa39ccefe68811a3db19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-log-file-format"></a><span data-ttu-id="edd84-103">Формат файла журнала службы импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="edd84-103">Azure Import/Export service log file format</span></span>
<span data-ttu-id="edd84-104">Когда hello службы импорта и экспорта Microsoft Azure выполняет действия на диске в рамках задания импорта или экспорта, журналы записываются tooblock большие двоичные объекты в учетной записи хранения hello, связанной с этим заданием.</span><span class="sxs-lookup"><span data-stu-id="edd84-104">When hello Microsoft Azure Import/Export service performs an action on a drive as part of an import job or an export job, logs are written tooblock blobs in hello storage account associated with that job.</span></span>  
  
<span data-ttu-id="edd84-105">Существует два журнала, которые могут записывать hello службы импорта и экспорта.</span><span class="sxs-lookup"><span data-stu-id="edd84-105">There are two logs that may be written by hello Import/Export service:</span></span>  
  
-   <span data-ttu-id="edd84-106">Hello журнал ошибок всегда создается в hello события ошибки.</span><span class="sxs-lookup"><span data-stu-id="edd84-106">hello error log is always generated in hello event of an error.</span></span>  
  
-   <span data-ttu-id="edd84-107">Hello подробного журнала не включено по умолчанию, но может быть включена путем установки hello `EnableVerboseLog` свойство [вставки задания](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) или [обновления свойств задания](/rest/api/storageimportexport/jobs#Jobs_Update) операции.</span><span class="sxs-lookup"><span data-stu-id="edd84-107">hello verbose log is not enabled by default, but may be enabled by setting hello `EnableVerboseLog` property on a [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation.</span></span>  
  
## <a name="log-file-location"></a><span data-ttu-id="edd84-108">Расположение файла журнала</span><span class="sxs-lookup"><span data-stu-id="edd84-108">Log file location</span></span>  
<span data-ttu-id="edd84-109">Hello журналы записываются tooblock большие двоичные объекты в контейнере hello или виртуальный каталог, заданный параметром hello `ImportExportStatesPath` параметр, который можно установить на `Put Job` операции.</span><span class="sxs-lookup"><span data-stu-id="edd84-109">hello logs are written tooblock blobs in hello container or virtual directory specified by hello `ImportExportStatesPath` setting, which you can set on a `Put Job` operation.</span></span> <span data-ttu-id="edd84-110">Hello расположение toowhich hello журналы записываются зависит от того, каким образом задана проверка подлинности для задания hello и hello значение, указанное для `ImportExportStatesPath`.</span><span class="sxs-lookup"><span data-stu-id="edd84-110">hello location toowhich hello logs are written depends on how authentication is specified for hello job, together with hello value specified for `ImportExportStatesPath`.</span></span> <span data-ttu-id="edd84-111">Проверка подлинности для задания hello может быть указан с помощью ключа учетной записи хранения или SAS (подписанного URL-адреса) контейнера.</span><span class="sxs-lookup"><span data-stu-id="edd84-111">Authentication for hello job may be specified via a storage account key, or a container SAS (shared access signature).</span></span>  
  
<span data-ttu-id="edd84-112">Имя Hello hello контейнер или виртуальный каталог может быть именем по умолчанию hello `waimportexport`, или другой контейнер или имя виртуального каталога.</span><span class="sxs-lookup"><span data-stu-id="edd84-112">hello name of hello container or virtual directory may either be hello default name of `waimportexport`, or another container or virtual directory name that you specify.</span></span>  
  
<span data-ttu-id="edd84-113">в следующей таблице Hello показаны hello возможные параметры:</span><span class="sxs-lookup"><span data-stu-id="edd84-113">hello table below shows hello possible options:</span></span>  
  
|<span data-ttu-id="edd84-114">Метод проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="edd84-114">Authentication Method</span></span>|<span data-ttu-id="edd84-115">Значение параметра `ImportExportStatesPath`Element</span><span class="sxs-lookup"><span data-stu-id="edd84-115">Value of `ImportExportStatesPath`Element</span></span>|<span data-ttu-id="edd84-116">Расположение больших двоичных объектов журналов</span><span class="sxs-lookup"><span data-stu-id="edd84-116">Location of Log Blobs</span></span>|  
|---------------------------|----------------------------------------------|---------------------------|  
|<span data-ttu-id="edd84-117">Ключ учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="edd84-117">Storage account key</span></span>|<span data-ttu-id="edd84-118">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="edd84-118">Default value</span></span>|<span data-ttu-id="edd84-119">Контейнер с именем `waimportexport`, который является контейнером по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-119">A container named `waimportexport`, which is hello default container.</span></span> <span data-ttu-id="edd84-120">Например:</span><span class="sxs-lookup"><span data-stu-id="edd84-120">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|<span data-ttu-id="edd84-121">Ключ учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="edd84-121">Storage account key</span></span>|<span data-ttu-id="edd84-122">Значение, заданное пользователем</span><span class="sxs-lookup"><span data-stu-id="edd84-122">User-specified value</span></span>|<span data-ttu-id="edd84-123">Контейнер с именем hello пользователь.</span><span class="sxs-lookup"><span data-stu-id="edd84-123">A container named by hello user.</span></span> <span data-ttu-id="edd84-124">Например:</span><span class="sxs-lookup"><span data-stu-id="edd84-124">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|<span data-ttu-id="edd84-125">SAS контейнера</span><span class="sxs-lookup"><span data-stu-id="edd84-125">Container SAS</span></span>|<span data-ttu-id="edd84-126">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="edd84-126">Default value</span></span>|<span data-ttu-id="edd84-127">Виртуальный каталог с именем `waimportexport`, которое является именем по умолчанию hello, контейнере hello, указанном в hello SAS.</span><span class="sxs-lookup"><span data-stu-id="edd84-127">A virtual directory named `waimportexport`, which is hello default name, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="edd84-128">Например, если hello SAS для задания hello является `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, то будет расположение журнала hello`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span><span class="sxs-lookup"><span data-stu-id="edd84-128">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span></span>|  
|<span data-ttu-id="edd84-129">SAS контейнера</span><span class="sxs-lookup"><span data-stu-id="edd84-129">Container SAS</span></span>|<span data-ttu-id="edd84-130">Значение, заданное пользователем</span><span class="sxs-lookup"><span data-stu-id="edd84-130">User-specified value</span></span>|<span data-ttu-id="edd84-131">Виртуальный каталог с именем пользователем hello контейнере hello, указанном в hello SAS.</span><span class="sxs-lookup"><span data-stu-id="edd84-131">A virtual directory named by hello user, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="edd84-132">Например, если hello SAS для hello задания является `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, с указанием hello виртуальный каталог называется `mylogblobs`, то расположением журнала hello будет `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span><span class="sxs-lookup"><span data-stu-id="edd84-132">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, and hello specified virtual directory is named `mylogblobs`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span></span>|  
  
<span data-ttu-id="edd84-133">Вы можете получить hello URL-адрес ошибки hello и подробных журналов, вызывающему Привет [получения задания](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) операции.</span><span class="sxs-lookup"><span data-stu-id="edd84-133">You can retrieve hello URL for hello error and verbose logs by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="edd84-134">Hello журналы доступны после завершения обработки диска hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-134">hello logs are available after processing of hello drive is complete.</span></span>  
  
## <a name="log-file-format"></a><span data-ttu-id="edd84-135">Формат файла журнала</span><span class="sxs-lookup"><span data-stu-id="edd84-135">Log file format</span></span>  
<span data-ttu-id="edd84-136">Hello формат у обоих журналов hello же: большой двоичный объект, содержащий XML-описания событий hello, возникших при копировании больших двоичных объектов между hello жестких дисков и счет клиента hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-136">hello format for both logs is hello same: a blob containing XML descriptions of hello events that occurred while copying blobs between hello hard drive and hello customer's account.</span></span>  
  
<span data-ttu-id="edd84-137">Hello подробный журнал содержит полные сведения о состоянии hello hello операции копирования для каждого большого двоичного объекта (для задания импорта) или файла (для задания экспорта), а hello журнал ошибок содержит только hello сведения о больших двоичных объектов или файлов, в которых обнаружены ошибки во время hello Импорт или экспорт заданий.</span><span class="sxs-lookup"><span data-stu-id="edd84-137">hello verbose log contains complete information about hello status of hello copy operation for every blob (for an import job) or file (for an export job), whereas hello error log contains only hello information for blobs or files that encountered errors during hello import or export job.</span></span>  
  
<span data-ttu-id="edd84-138">Далее приведен формат подробного журнала Hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-138">hello verbose log format is shown below.</span></span> <span data-ttu-id="edd84-139">журнал ошибок Hello имеет hello же структуру, но отфильтрованы успешные операции.</span><span class="sxs-lookup"><span data-stu-id="edd84-139">hello error log has hello same structure, but filters out successful operations.</span></span>  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

<span data-ttu-id="edd84-140">Hello следующей таблице описываются элементы hello hello файла журнала.</span><span class="sxs-lookup"><span data-stu-id="edd84-140">hello following table describes hello elements of hello log file.</span></span>  
  
|<span data-ttu-id="edd84-141">XML-элемент</span><span class="sxs-lookup"><span data-stu-id="edd84-141">XML Element</span></span>|<span data-ttu-id="edd84-142">Тип</span><span class="sxs-lookup"><span data-stu-id="edd84-142">Type</span></span>|<span data-ttu-id="edd84-143">Описание</span><span class="sxs-lookup"><span data-stu-id="edd84-143">Description</span></span>|  
|-----------------|----------|-----------------|  
|`DriveLog`|<span data-ttu-id="edd84-144">XML-элемент</span><span class="sxs-lookup"><span data-stu-id="edd84-144">XML Element</span></span>|<span data-ttu-id="edd84-145">Представляет журнал диска.</span><span class="sxs-lookup"><span data-stu-id="edd84-145">Represents a drive log.</span></span>|  
|`Version`|<span data-ttu-id="edd84-146">Атрибут, строка</span><span class="sxs-lookup"><span data-stu-id="edd84-146">Attribute, String</span></span>|<span data-ttu-id="edd84-147">версия формата журнала hello Hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-147">hello version of hello log format.</span></span>|  
|`DriveId`|<span data-ttu-id="edd84-148">Строка</span><span class="sxs-lookup"><span data-stu-id="edd84-148">String</span></span>|<span data-ttu-id="edd84-149">Здравствуйте, серийный номер диска.</span><span class="sxs-lookup"><span data-stu-id="edd84-149">hello drive's hardware serial number.</span></span>|  
|`Status`|<span data-ttu-id="edd84-150">Строка</span><span class="sxs-lookup"><span data-stu-id="edd84-150">String</span></span>|<span data-ttu-id="edd84-151">Состояние обработки диска hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-151">Status of hello drive processing.</span></span> <span data-ttu-id="edd84-152">В разделе hello `Drive Status Codes` таблицу ниже для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="edd84-152">See hello `Drive Status Codes` table below for more information.</span></span>|  
|`Blob`|<span data-ttu-id="edd84-153">Вложенный XML-элемент</span><span class="sxs-lookup"><span data-stu-id="edd84-153">Nested XML element</span></span>|<span data-ttu-id="edd84-154">Представляет большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="edd84-154">Represents a blob.</span></span>|  
|`Blob/BlobPath`|<span data-ttu-id="edd84-155">Строка</span><span class="sxs-lookup"><span data-stu-id="edd84-155">String</span></span>|<span data-ttu-id="edd84-156">Здравствуйте, URI большого двоичного объекта hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-156">hello URI of hello blob.</span></span>|  
|`Blob/FilePath`|<span data-ttu-id="edd84-157">Строка</span><span class="sxs-lookup"><span data-stu-id="edd84-157">String</span></span>|<span data-ttu-id="edd84-158">файл toohello Hello относительный путь на диске hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-158">hello relative path toohello file on hello drive.</span></span>|  
|`Blob/Snapshot`|<span data-ttu-id="edd84-159">DateTime</span><span class="sxs-lookup"><span data-stu-id="edd84-159">DateTime</span></span>|<span data-ttu-id="edd84-160">версия моментального снимка большого двоичного объекта hello, для задания экспорта только Hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-160">hello snapshot version of hello blob, for an export job only.</span></span>|  
|`Blob/Length`|<span data-ttu-id="edd84-161">Целое число </span><span class="sxs-lookup"><span data-stu-id="edd84-161">Integer</span></span>|<span data-ttu-id="edd84-162">Общая длина Hello hello большого двоичного объекта в байтах.</span><span class="sxs-lookup"><span data-stu-id="edd84-162">hello total length of hello blob in bytes.</span></span>|  
|`Blob/LastModified`|<span data-ttu-id="edd84-163">DateTime</span><span class="sxs-lookup"><span data-stu-id="edd84-163">DateTime</span></span>|<span data-ttu-id="edd84-164">Hello даты и времени последнего изменения большого двоичного объекта hello только задания экспорта.</span><span class="sxs-lookup"><span data-stu-id="edd84-164">hello date/time that hello blob was last modified, for an export job only.</span></span>|  
|`Blob/ImportDisposition`|<span data-ttu-id="edd84-165">Строка</span><span class="sxs-lookup"><span data-stu-id="edd84-165">String</span></span>|<span data-ttu-id="edd84-166">стратегией большого двоичного объекта hello, импорт только для задания импорта Hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-166">hello import disposition of hello blob, for an import job only.</span></span>|  
|`Blob/ImportDisposition/@Status`|<span data-ttu-id="edd84-167">Атрибут, строка</span><span class="sxs-lookup"><span data-stu-id="edd84-167">Attribute, String</span></span>|<span data-ttu-id="edd84-168">состояние Hello hello стратегией импорта.</span><span class="sxs-lookup"><span data-stu-id="edd84-168">hello status of hello import disposition.</span></span>|  
|`PageRangeList`|<span data-ttu-id="edd84-169">Вложенный XML-элемент</span><span class="sxs-lookup"><span data-stu-id="edd84-169">Nested XML element</span></span>|<span data-ttu-id="edd84-170">Представляет список диапазонов страниц для страничного BLOB-объекта.</span><span class="sxs-lookup"><span data-stu-id="edd84-170">Represents a list of page ranges for a page blob.</span></span>|  
|`PageRange`|<span data-ttu-id="edd84-171">XML-элемент</span><span class="sxs-lookup"><span data-stu-id="edd84-171">XML element</span></span>|<span data-ttu-id="edd84-172">Представляет диапазон страниц.</span><span class="sxs-lookup"><span data-stu-id="edd84-172">Represents a page range.</span></span>|  
|`PageRange/@Offset`|<span data-ttu-id="edd84-173">Атрибут, целое число</span><span class="sxs-lookup"><span data-stu-id="edd84-173">Attribute, Integer</span></span>|<span data-ttu-id="edd84-174">Начальное смещение диапазона страниц hello в большом двоичном объекте hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-174">Starting offset of hello page range in hello blob.</span></span>|  
|`PageRange/@Length`|<span data-ttu-id="edd84-175">Атрибут, целое число</span><span class="sxs-lookup"><span data-stu-id="edd84-175">Attribute, Integer</span></span>|<span data-ttu-id="edd84-176">Длина в байтах hello диапазона страниц.</span><span class="sxs-lookup"><span data-stu-id="edd84-176">Length in bytes of hello page range.</span></span>|  
|`PageRange/@Hash`|<span data-ttu-id="edd84-177">Атрибут, строка</span><span class="sxs-lookup"><span data-stu-id="edd84-177">Attribute, String</span></span>|<span data-ttu-id="edd84-178">Кодировке base16 MD5-хэш диапазона страниц hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-178">Base16-encoded MD5 hash of hello page range.</span></span>|  
|`PageRange/@Status`|<span data-ttu-id="edd84-179">Атрибут, строка</span><span class="sxs-lookup"><span data-stu-id="edd84-179">Attribute, String</span></span>|<span data-ttu-id="edd84-180">Состояние обработки диапазона страниц hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-180">Status of processing hello page range.</span></span>|  
|`BlockList`|<span data-ttu-id="edd84-181">Вложенный XML-элемент</span><span class="sxs-lookup"><span data-stu-id="edd84-181">Nested XML element</span></span>|<span data-ttu-id="edd84-182">Представляет список блоков блочного BLOB-объекта.</span><span class="sxs-lookup"><span data-stu-id="edd84-182">Represents a list of blocks for a block blob.</span></span>|  
|`Block`|<span data-ttu-id="edd84-183">XML-элемент</span><span class="sxs-lookup"><span data-stu-id="edd84-183">XML element</span></span>|<span data-ttu-id="edd84-184">Представляет блок.</span><span class="sxs-lookup"><span data-stu-id="edd84-184">Represents a block.</span></span>|  
|`Block/@Offset`|<span data-ttu-id="edd84-185">Атрибут, целое число</span><span class="sxs-lookup"><span data-stu-id="edd84-185">Attribute, Integer</span></span>|<span data-ttu-id="edd84-186">Начальное смещение блока hello в большом двоичном объекте hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-186">Starting offset of hello block in hello blob.</span></span>|  
|`Block/@Length`|<span data-ttu-id="edd84-187">Атрибут, целое число</span><span class="sxs-lookup"><span data-stu-id="edd84-187">Attribute, Integer</span></span>|<span data-ttu-id="edd84-188">Длина в байтах блока hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-188">Length in bytes of hello block.</span></span>|  
|`Block/@Id`|<span data-ttu-id="edd84-189">Атрибут, строка</span><span class="sxs-lookup"><span data-stu-id="edd84-189">Attribute, String</span></span>|<span data-ttu-id="edd84-190">Идентификатор блока Hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-190">hello block ID.</span></span>|  
|`Block/@Hash`|<span data-ttu-id="edd84-191">Атрибут, строка</span><span class="sxs-lookup"><span data-stu-id="edd84-191">Attribute, String</span></span>|<span data-ttu-id="edd84-192">Кодировке base16 MD5-хэш блока hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-192">Base16-encoded MD5 hash of hello block.</span></span>|  
|`Block/@Status`|<span data-ttu-id="edd84-193">Атрибут, строка</span><span class="sxs-lookup"><span data-stu-id="edd84-193">Attribute, String</span></span>|<span data-ttu-id="edd84-194">Состояние обработки блока hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-194">Status of processing hello block.</span></span>|  
|`Metadata`|<span data-ttu-id="edd84-195">Вложенный XML-элемент</span><span class="sxs-lookup"><span data-stu-id="edd84-195">Nested XML element</span></span>|<span data-ttu-id="edd84-196">Представляет метаданные hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="edd84-196">Represents hello blob's metadata.</span></span>|  
|`Metadata/@Status`|<span data-ttu-id="edd84-197">Атрибут, строка</span><span class="sxs-lookup"><span data-stu-id="edd84-197">Attribute, String</span></span>|<span data-ttu-id="edd84-198">Состояние обработки метаданных большого двоичного объекта hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-198">Status of processing of hello blob metadata.</span></span>|  
|`Metadata/GlobalPath`|<span data-ttu-id="edd84-199">Строка</span><span class="sxs-lookup"><span data-stu-id="edd84-199">String</span></span>|<span data-ttu-id="edd84-200">Относительный путь toohello глобального файла метаданных.</span><span class="sxs-lookup"><span data-stu-id="edd84-200">Relative path toohello global metadata file.</span></span>|  
|`Metadata/GlobalPath/@Hash`|<span data-ttu-id="edd84-201">Атрибут, строка</span><span class="sxs-lookup"><span data-stu-id="edd84-201">Attribute, String</span></span>|<span data-ttu-id="edd84-202">Кодировке base16 MD5-хэш hello глобального файла метаданных.</span><span class="sxs-lookup"><span data-stu-id="edd84-202">Base16-encoded MD5 hash of hello global metadata file.</span></span>|  
|`Metadata/Path`|<span data-ttu-id="edd84-203">Строка</span><span class="sxs-lookup"><span data-stu-id="edd84-203">String</span></span>|<span data-ttu-id="edd84-204">Относительный путь к файлу метаданных toohello.</span><span class="sxs-lookup"><span data-stu-id="edd84-204">Relative path toohello metadata file.</span></span>|  
|`Metadata/Path/@Hash`|<span data-ttu-id="edd84-205">Атрибут, строка</span><span class="sxs-lookup"><span data-stu-id="edd84-205">Attribute, String</span></span>|<span data-ttu-id="edd84-206">Кодировке base16 MD5-хэш файла метаданных hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-206">Base16-encoded MD5 hash of hello metadata file.</span></span>|  
|`Properties`|<span data-ttu-id="edd84-207">Вложенный XML-элемент</span><span class="sxs-lookup"><span data-stu-id="edd84-207">Nested XML element</span></span>|<span data-ttu-id="edd84-208">Представляет свойства большого двоичного объекта hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-208">Represents hello blob properties.</span></span>|  
|`Properties/@Status`|<span data-ttu-id="edd84-209">Атрибут, строка</span><span class="sxs-lookup"><span data-stu-id="edd84-209">Attribute, String</span></span>|<span data-ttu-id="edd84-210">Состояние обработки свойств большого двоичного объекта hello, например файл не найден, завершена.</span><span class="sxs-lookup"><span data-stu-id="edd84-210">Status of processing hello blob properties, e.g. file not found, completed.</span></span>|  
|`Properties/GlobalPath`|<span data-ttu-id="edd84-211">Строка</span><span class="sxs-lookup"><span data-stu-id="edd84-211">String</span></span>|<span data-ttu-id="edd84-212">Относительный путь toohello глобального файла свойств.</span><span class="sxs-lookup"><span data-stu-id="edd84-212">Relative path toohello global properties file.</span></span>|  
|`Properties/GlobalPath/@Hash`|<span data-ttu-id="edd84-213">Атрибут, строка</span><span class="sxs-lookup"><span data-stu-id="edd84-213">Attribute, String</span></span>|<span data-ttu-id="edd84-214">Кодировке base16 MD5-хэш файла hello глобальные свойства.</span><span class="sxs-lookup"><span data-stu-id="edd84-214">Base16-encoded MD5 hash of hello global properties file.</span></span>|  
|`Properties/Path`|<span data-ttu-id="edd84-215">Строка</span><span class="sxs-lookup"><span data-stu-id="edd84-215">String</span></span>|<span data-ttu-id="edd84-216">Файл свойств toohello относительный путь.</span><span class="sxs-lookup"><span data-stu-id="edd84-216">Relative path toohello properties file.</span></span>|  
|`Properties/Path/@Hash`|<span data-ttu-id="edd84-217">Атрибут, строка</span><span class="sxs-lookup"><span data-stu-id="edd84-217">Attribute, String</span></span>|<span data-ttu-id="edd84-218">Кодировке base16 MD5-хэш файла свойств hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-218">Base16-encoded MD5 hash of hello properties file.</span></span>|  
|`Blob/Status`|<span data-ttu-id="edd84-219">Строка</span><span class="sxs-lookup"><span data-stu-id="edd84-219">String</span></span>|<span data-ttu-id="edd84-220">Состояние обработки hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="edd84-220">Status of processing hello blob.</span></span>|  
  
# <a name="drive-status-codes"></a><span data-ttu-id="edd84-221">Коды состояний диска</span><span class="sxs-lookup"><span data-stu-id="edd84-221">Drive status codes</span></span>  
<span data-ttu-id="edd84-222">Hello следующей таблице перечислены коды состояния hello для обработки диска.</span><span class="sxs-lookup"><span data-stu-id="edd84-222">hello following table lists hello status codes for processing a drive.</span></span>  
  
|<span data-ttu-id="edd84-223">Код состояния</span><span class="sxs-lookup"><span data-stu-id="edd84-223">Status code</span></span>|<span data-ttu-id="edd84-224">Описание</span><span class="sxs-lookup"><span data-stu-id="edd84-224">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="edd84-225">диск Hello завершил обработку без ошибок.</span><span class="sxs-lookup"><span data-stu-id="edd84-225">hello drive has finished processing without any errors.</span></span>|  
|`CompletedWithWarnings`|<span data-ttu-id="edd84-226">Обработка с предупреждениями в один или несколько больших двоичных объектах в hello стратегией импорта, заданной для больших двоичных объектов hello завершилась Hello диска.</span><span class="sxs-lookup"><span data-stu-id="edd84-226">hello drive has finished processing with warnings in one or more blobs per hello import dispositions specified for hello blobs.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="edd84-227">Hello диска завершена с ошибками в одной или нескольких больших двоичных объектов или блоков.</span><span class="sxs-lookup"><span data-stu-id="edd84-227">hello drive has finished with errors in one or more blobs or chunks.</span></span>|  
|`DiskNotFound`|<span data-ttu-id="edd84-228">Диск не найден на диске hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-228">No disk is found on hello drive.</span></span>|  
|`VolumeNotNtfs`|<span data-ttu-id="edd84-229">Hello первый том данных на диске hello не в формате NTFS.</span><span class="sxs-lookup"><span data-stu-id="edd84-229">hello first data volume on hello disk is not in NTFS format.</span></span>|  
|`DiskOperationFailed`|<span data-ttu-id="edd84-230">Неизвестный сбой при выполнении операций на диске hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-230">An unknown failure occurred when performing operations on hello drive.</span></span>|  
|`BitLockerVolumeNotFound`|<span data-ttu-id="edd84-231">Не найден том, зашифрованный с помощью BitLocker.</span><span class="sxs-lookup"><span data-stu-id="edd84-231">No BitLocker encryptable volume is found.</span></span>|  
|`BitLockerNotActivated`|<span data-ttu-id="edd84-232">BitLocker не включена на томе hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-232">BitLocker is not enabled on hello volume.</span></span>|  
|`BitLockerProtectorNotFound`|<span data-ttu-id="edd84-233">на томе hello Hello числовой предохранитель ключа пароля не существует.</span><span class="sxs-lookup"><span data-stu-id="edd84-233">hello numerical password key protector does not exist on hello volume.</span></span>|  
|`BitLockerKeyInvalid`|<span data-ttu-id="edd84-234">Hello числовому паролю не удается разблокировать том hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-234">hello numerical password provided cannot unlock hello volume.</span></span>|  
|`BitLockerUnlockVolumeFailed`|<span data-ttu-id="edd84-235">Произошла неизвестная ошибка произошла при попытке toounlock hello тома.</span><span class="sxs-lookup"><span data-stu-id="edd84-235">Unknown failure has happened when trying toounlock hello volume.</span></span>|  
|`BitLockerFailed`|<span data-ttu-id="edd84-236">Произошла неизвестная ошибка при выполнении операций с BitLocker.</span><span class="sxs-lookup"><span data-stu-id="edd84-236">An unknown failure occurred while performing BitLocker operations.</span></span>|  
|`ManifestNameInvalid`|<span data-ttu-id="edd84-237">Недопустимое имя файла манифеста Hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-237">hello manifest file name is invalid.</span></span>|  
|`ManifestNameTooLong`|<span data-ttu-id="edd84-238">указано слишком длинное имя файла манифеста Hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-238">hello manifest file name is too long.</span></span>|  
|`ManifestNotFound`|<span data-ttu-id="edd84-239">не найден файл манифеста Hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-239">hello manifest file is not found.</span></span>|  
|`ManifestAccessDenied`|<span data-ttu-id="edd84-240">Файл манифеста toohello доступ запрещен.</span><span class="sxs-lookup"><span data-stu-id="edd84-240">Access toohello manifest file is denied.</span></span>|  
|`ManifestCorrupted`|<span data-ttu-id="edd84-241">Hello поврежден файл манифеста (hello содержимое не совпадает с хэшем).</span><span class="sxs-lookup"><span data-stu-id="edd84-241">hello manifest file is corrupted (hello content does not match its hash).</span></span>|  
|`ManifestFormatInvalid`|<span data-ttu-id="edd84-242">содержимое манифеста Hello не соответствует требуемому формату toohello.</span><span class="sxs-lookup"><span data-stu-id="edd84-242">hello manifest content does not conform toohello required format.</span></span>|  
|`ManifestDriveIdMismatch`|<span data-ttu-id="edd84-243">Здравствуйте, код в файле манифеста hello не соответствует hello одно чтение с диска hello диска.</span><span class="sxs-lookup"><span data-stu-id="edd84-243">hello drive ID in hello manifest file does not match hello one read from hello drive.</span></span>|  
|`ReadManifestFailed`|<span data-ttu-id="edd84-244">При чтении из файла манифеста hello произошла ошибка ввода-вывода диска.</span><span class="sxs-lookup"><span data-stu-id="edd84-244">A disk I/O failure occurred while reading from hello manifest.</span></span>|  
|`BlobListFormatInvalid`|<span data-ttu-id="edd84-245">Hello экспорта списка больших двоичных объектов не соответствует требуемому формату toohello.</span><span class="sxs-lookup"><span data-stu-id="edd84-245">hello export blob list blob does not conform toohello required format.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="edd84-246">Запрещен доступ toohello BLOB-объектов в учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-246">Access toohello blobs in hello storage account is forbidden.</span></span> <span data-ttu-id="edd84-247">Это может произойти из-за tooinvalid ключ учетной записи хранилища или SAS контейнера.</span><span class="sxs-lookup"><span data-stu-id="edd84-247">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`InternalError`|<span data-ttu-id="edd84-248">И произошла внутренняя ошибка при обработке диска hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-248">And internal error occurred while processing hello drive.</span></span>|  
  
## <a name="blob-status-codes"></a><span data-ttu-id="edd84-249">Коды состояний большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="edd84-249">Blob status codes</span></span>  
<span data-ttu-id="edd84-250">Hello следующей таблице перечислены коды состояния hello для обработки большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="edd84-250">hello following table lists hello status codes for processing a blob.</span></span>  
  
|<span data-ttu-id="edd84-251">Код состояния</span><span class="sxs-lookup"><span data-stu-id="edd84-251">Status code</span></span>|<span data-ttu-id="edd84-252">Описание</span><span class="sxs-lookup"><span data-stu-id="edd84-252">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="edd84-253">большой двоичный объект Hello обработка завершилась без ошибок.</span><span class="sxs-lookup"><span data-stu-id="edd84-253">hello blob has finished processing without errors.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="edd84-254">большой двоичный объект Hello завершения обработки ошибок в один или несколько диапазонов страниц или блоков, метаданных или свойств.</span><span class="sxs-lookup"><span data-stu-id="edd84-254">hello blob has finished processing with errors in one or more page ranges or blocks, metadata, or properties.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="edd84-255">Недопустимое имя файла Hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-255">hello file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="edd84-256">указано слишком длинное имя файла Hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-256">hello file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="edd84-257">Hello файл не найден.</span><span class="sxs-lookup"><span data-stu-id="edd84-257">hello file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="edd84-258">Файл toohello доступ запрещен.</span><span class="sxs-lookup"><span data-stu-id="edd84-258">Access toohello file is denied.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="edd84-259">Сбой запроса службы BLOB-объектов Hello что tooaccess hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="edd84-259">hello Blob service request tooaccess hello blob has failed.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="edd84-260">Hello большого двоичного объекта запроса службы tooaccess hello больших двоичных объектов запрещено.</span><span class="sxs-lookup"><span data-stu-id="edd84-260">hello Blob service request tooaccess hello blob is forbidden.</span></span> <span data-ttu-id="edd84-261">Это может произойти из-за tooinvalid ключ учетной записи хранилища или SAS контейнера.</span><span class="sxs-lookup"><span data-stu-id="edd84-261">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`RenameFailed`|<span data-ttu-id="edd84-262">Не удалось toorename hello blob (для задания импорта) или файл hello (для задания экспорта).</span><span class="sxs-lookup"><span data-stu-id="edd84-262">Failed toorename hello blob (for an import job) or hello file (for an export job).</span></span>|  
|`BlobUnexpectedChange`|<span data-ttu-id="edd84-263">Непредвиденное изменение произошла с hello больших двоичных объектов (для задания экспорта).</span><span class="sxs-lookup"><span data-stu-id="edd84-263">An unexpected change has occurred with hello blob (for an export job).</span></span>|  
|`LeasePresent`|<span data-ttu-id="edd84-264">Нет Аренда на большой двоичный объект hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-264">There is a lease present on hello blob.</span></span>|  
|`IOFailed`|<span data-ttu-id="edd84-265">Диск или сетевой ошибки ввода-вывода произошла при обработке больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-265">A disk or network I/O failure occurred while processing hello blob.</span></span>|  
|`Failed`|<span data-ttu-id="edd84-266">Неизвестная ошибка при обработке больших двоичных объектов hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-266">An unknown failure occurred while processing hello blob.</span></span>|  
  
## <a name="import-disposition-status-codes"></a><span data-ttu-id="edd84-267">Коды состояний метода обработки импорта</span><span class="sxs-lookup"><span data-stu-id="edd84-267">Import disposition status codes</span></span>  
<span data-ttu-id="edd84-268">Hello следующей таблице перечислены коды состояния hello для устранения ошибок стратегии импорта.</span><span class="sxs-lookup"><span data-stu-id="edd84-268">hello following table lists hello status codes for resolving an import disposition.</span></span>  
  
|<span data-ttu-id="edd84-269">Код состояния</span><span class="sxs-lookup"><span data-stu-id="edd84-269">Status code</span></span>|<span data-ttu-id="edd84-270">Описание</span><span class="sxs-lookup"><span data-stu-id="edd84-270">Description</span></span>|  
|-----------------|-----------------|  
|`Created`|<span data-ttu-id="edd84-271">Hello BLOB-объект был создан.</span><span class="sxs-lookup"><span data-stu-id="edd84-271">hello blob has been created.</span></span>|  
|`Renamed`|<span data-ttu-id="edd84-272">Hello большой двоичный объект переименован на переименование стратегии импорта.</span><span class="sxs-lookup"><span data-stu-id="edd84-272">hello blob has been renamed per rename import disposition.</span></span> <span data-ttu-id="edd84-273">Hello `Blob/BlobPath` элемент содержит hello URI для hello переименован большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="edd84-273">hello `Blob/BlobPath` element contains hello URI for hello renamed blob.</span></span>|  
|`Skipped`|<span data-ttu-id="edd84-274">Hello большой двоичный объект был пропущен в `no-overwrite` стратегией импорта.</span><span class="sxs-lookup"><span data-stu-id="edd84-274">hello blob has been skipped per `no-overwrite` import disposition.</span></span>|  
|`Overwritten`|<span data-ttu-id="edd84-275">Hello большой двоичный объект перезаписал существующий большой двоичный объект в `overwrite` стратегией импорта.</span><span class="sxs-lookup"><span data-stu-id="edd84-275">hello blob has overwritten an existing blob per `overwrite` import disposition.</span></span>|  
|`Cancelled`|<span data-ttu-id="edd84-276">Предыдущий сбой позволил продолжить обработку стратегии импорта hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-276">A prior failure has stopped further processing of hello import disposition.</span></span>|  
  
## <a name="page-rangeblock-status-codes"></a><span data-ttu-id="edd84-277">Коды состояний диапазона страниц или блока</span><span class="sxs-lookup"><span data-stu-id="edd84-277">Page range/block status codes</span></span>  
<span data-ttu-id="edd84-278">Hello следующей таблице перечислены коды состояния hello для обработки диапазона страниц или блока.</span><span class="sxs-lookup"><span data-stu-id="edd84-278">hello following table lists hello status codes for processing a page range or a block.</span></span>  
  
|<span data-ttu-id="edd84-279">Код состояния</span><span class="sxs-lookup"><span data-stu-id="edd84-279">Status code</span></span>|<span data-ttu-id="edd84-280">Описание</span><span class="sxs-lookup"><span data-stu-id="edd84-280">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="edd84-281">Hello диапазон или блок страниц завершил обработку без ошибок.</span><span class="sxs-lookup"><span data-stu-id="edd84-281">hello page range or block has finished processing without any errors.</span></span>|  
|`Committed`|<span data-ttu-id="edd84-282">Hello блок был зафиксирован, но не в hello полного списка блокировок из-за других блоков возникли ошибки или поместить полного списка блокировок не удалась.</span><span class="sxs-lookup"><span data-stu-id="edd84-282">hello block has been committed,  but not in hello full block list because other blocks have failed, or put full block list itself has failed.</span></span>|  
|`Uncommitted`|<span data-ttu-id="edd84-283">Hello блок загружен, но не были зафиксированы.</span><span class="sxs-lookup"><span data-stu-id="edd84-283">hello block is uploaded but not committed.</span></span>|  
|`Corrupted`|<span data-ttu-id="edd84-284">Hello диапазон или блок страниц поврежден (содержимое hello не совпадает с хэшем).</span><span class="sxs-lookup"><span data-stu-id="edd84-284">hello page range or block is corrupted (hello content does not match its hash).</span></span>|  
|`FileUnexpectedEnd`|<span data-ttu-id="edd84-285">Обнаружен непредвиденный конец файла.</span><span class="sxs-lookup"><span data-stu-id="edd84-285">An unexpected end of file has been encountered.</span></span>|  
|`BlobUnexpectedEnd`|<span data-ttu-id="edd84-286">Обнаружен непредвиденный конец большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="edd84-286">An unexpected end of blob has been encountered.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="edd84-287">Здравствуйте запроса службы BLOB-объектов tooaccess hello диапазона страниц или блок не удалось.</span><span class="sxs-lookup"><span data-stu-id="edd84-287">hello Blob service request tooaccess hello page range or block has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="edd84-288">Диск или сетевой ошибки ввода-вывода произошла при обработке hello диапазона или блока страниц.</span><span class="sxs-lookup"><span data-stu-id="edd84-288">A disk or network I/O failure occurred while processing hello page range or block.</span></span>|  
|`Failed`|<span data-ttu-id="edd84-289">Неизвестная ошибка при обработке hello диапазона или блока страниц.</span><span class="sxs-lookup"><span data-stu-id="edd84-289">An unknown failure occurred while processing hello page range or block.</span></span>|  
|`Cancelled`|<span data-ttu-id="edd84-290">Предыдущий сбой позволил продолжить обработку hello диапазона или блока страниц.</span><span class="sxs-lookup"><span data-stu-id="edd84-290">A prior failure has stopped further processing of hello page range or block.</span></span>|  
  
## <a name="metadata-status-codes"></a><span data-ttu-id="edd84-291">Коды состояний метаданных</span><span class="sxs-lookup"><span data-stu-id="edd84-291">Metadata status codes</span></span>  
<span data-ttu-id="edd84-292">Hello следующей таблице перечислены коды состояния hello для обработки метаданных большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="edd84-292">hello following table lists hello status codes for processing blob metadata.</span></span>  
  
|<span data-ttu-id="edd84-293">Код состояния</span><span class="sxs-lookup"><span data-stu-id="edd84-293">Status code</span></span>|<span data-ttu-id="edd84-294">Описание</span><span class="sxs-lookup"><span data-stu-id="edd84-294">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="edd84-295">метаданные Hello обработка завершилась без ошибок.</span><span class="sxs-lookup"><span data-stu-id="edd84-295">hello metadata has finished processing without errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="edd84-296">Недопустимое имя файла метаданных Hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-296">hello metadata file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="edd84-297">указано слишком длинное имя файла метаданных Hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-297">hello metadata file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="edd84-298">файл метаданных Hello не найден.</span><span class="sxs-lookup"><span data-stu-id="edd84-298">hello metadata file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="edd84-299">Файл метаданных toohello доступ запрещен.</span><span class="sxs-lookup"><span data-stu-id="edd84-299">Access toohello metadata file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="edd84-300">поврежден файл метаданных Hello (hello содержимое не совпадает с хэшем).</span><span class="sxs-lookup"><span data-stu-id="edd84-300">hello metadata file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="edd84-301">содержимое метаданных Hello не соответствует требуемому формату toohello.</span><span class="sxs-lookup"><span data-stu-id="edd84-301">hello metadata content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="edd84-302">Запись метаданных hello ошибка XML.</span><span class="sxs-lookup"><span data-stu-id="edd84-302">Writing hello metadata XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="edd84-303">Сбой запроса службы BLOB-объектов Hello что tooaccess hello метаданных.</span><span class="sxs-lookup"><span data-stu-id="edd84-303">hello Blob service request tooaccess hello metadata has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="edd84-304">Произошла ошибка ввода-вывода диска или сети при обработке метаданных hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-304">A disk or network I/O failure occurred while processing hello metadata.</span></span>|  
|`Failed`|<span data-ttu-id="edd84-305">Неизвестная ошибка при обработке метаданных hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-305">An unknown failure occurred while processing hello metadata.</span></span>|  
|`Cancelled`|<span data-ttu-id="edd84-306">Предыдущий сбой позволил продолжить обработку метаданных hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-306">A prior failure has stopped further processing of hello metadata.</span></span>|  
  
## <a name="properties-status-codes"></a><span data-ttu-id="edd84-307">Коды состояний свойств</span><span class="sxs-lookup"><span data-stu-id="edd84-307">Properties status codes</span></span>  
<span data-ttu-id="edd84-308">Hello следующей таблице перечислены коды состояния hello для обработки свойств большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="edd84-308">hello following table lists hello status codes for processing blob properties.</span></span>  
  
|<span data-ttu-id="edd84-309">Код состояния</span><span class="sxs-lookup"><span data-stu-id="edd84-309">Status code</span></span>|<span data-ttu-id="edd84-310">Описание</span><span class="sxs-lookup"><span data-stu-id="edd84-310">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="edd84-311">свойства Hello закончена обработка без ошибок.</span><span class="sxs-lookup"><span data-stu-id="edd84-311">hello properties have finished processing without any errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="edd84-312">Недопустимое имя файла свойств Hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-312">hello properties file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="edd84-313">указано слишком длинное имя файла свойств Hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-313">hello properties file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="edd84-314">файл свойств Hello не найден.</span><span class="sxs-lookup"><span data-stu-id="edd84-314">hello properties file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="edd84-315">Файл свойств toohello доступ запрещен.</span><span class="sxs-lookup"><span data-stu-id="edd84-315">Access toohello properties file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="edd84-316">поврежден файл свойств Hello (hello содержимое не совпадает с хэшем).</span><span class="sxs-lookup"><span data-stu-id="edd84-316">hello properties file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="edd84-317">содержимое свойства Hello не соответствует требуемому формату toohello.</span><span class="sxs-lookup"><span data-stu-id="edd84-317">hello properties content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="edd84-318">Запись свойства hello, ошибка XML.</span><span class="sxs-lookup"><span data-stu-id="edd84-318">Writing hello properties XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="edd84-319">Сбой запроса службы BLOB-объектов Hello что tooaccess hello свойства.</span><span class="sxs-lookup"><span data-stu-id="edd84-319">hello Blob service request tooaccess hello properties has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="edd84-320">Произошла ошибка ввода-вывода диска или сети при обработке свойств hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-320">A disk or network I/O failure occurred while processing hello properties.</span></span>|  
|`Failed`|<span data-ttu-id="edd84-321">Неизвестная ошибка при обработке свойств hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-321">An unknown failure occurred while processing hello properties.</span></span>|  
|`Cancelled`|<span data-ttu-id="edd84-322">Предыдущий сбой позволил продолжить обработку свойств hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-322">A prior failure has stopped further processing of hello properties.</span></span>|  
  
## <a name="sample-logs"></a><span data-ttu-id="edd84-323">Примеры журналов</span><span class="sxs-lookup"><span data-stu-id="edd84-323">Sample logs</span></span>  
<span data-ttu-id="edd84-324">Hello ниже приведен пример подробного журнала.</span><span class="sxs-lookup"><span data-stu-id="edd84-324">hello following is an example of verbose log.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
<span data-ttu-id="edd84-325">Ниже приведен соответствующий журнал ошибок Hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-325">hello corresponding error log is shown below.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 <span data-ttu-id="edd84-326">Hello журнал ошибок для задания импорта содержит ошибку о ненайденном файле на диске импорта hello.</span><span class="sxs-lookup"><span data-stu-id="edd84-326">hello follow error log for an import job contains an error about a file not found on hello import drive.</span></span> <span data-ttu-id="edd84-327">Обратите внимание, что состояние последующих компонентов hello `Cancelled`.</span><span class="sxs-lookup"><span data-stu-id="edd84-327">Note that hello status of subsequent components is `Cancelled`.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

<span data-ttu-id="edd84-328">Hello следующий журнал ошибок задания экспорта указывает, что содержимое большого двоичного объекта hello был успешно записан toohello диска, но что произошла ошибка при экспорте свойства hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="edd84-328">hello following error log for an export job indicates that hello blob content has been successfully written toohello drive, but that an error occurred while exporting hello blob's properties.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a><span data-ttu-id="edd84-329">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="edd84-329">Next steps</span></span>
 
* [<span data-ttu-id="edd84-330">Справочник по REST API импорта и экспорта службы хранилища</span><span class="sxs-lookup"><span data-stu-id="edd84-330">Storage Import/Export REST API</span></span>](/rest/api/storageimportexport/)
