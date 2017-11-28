---
title: "aaaDiagnostics и восстановление после ошибок для заданий импорта и экспорта Azure | Документы Microsoft"
description: "Узнайте, как ведение подробного журнала tooenable для импорта и экспорта Microsoft Azure службы заданий."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 096cc795-9af6-4335-9fe8-fffa9f239a17
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 48164279e7904c78fed802aa3cff66e589c3f12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a><span data-ttu-id="c513e-103">Диагностика и восстановление после ошибок для заданий импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="c513e-103">Diagnostics and error recovery for Azure Import/Export jobs</span></span>
<span data-ttu-id="c513e-104">Для каждого обрабатываемого диска hello службы импорта и экспорта Azure создает журнал ошибок в учетной записи хранения связанных hello.</span><span class="sxs-lookup"><span data-stu-id="c513e-104">For each drive processed, hello Azure Import/Export service creates an error log in hello associated storage account.</span></span> <span data-ttu-id="c513e-105">Можно также включить ведение подробного журнала, задание hello `LogLevel` свойство слишком`Verbose` при вызове hello [вставки задания](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) или [обновления свойств задания](/rest/api/storageimportexport/jobs#Jobs_Update) операций.</span><span class="sxs-lookup"><span data-stu-id="c513e-105">You can also enable verbose logging by setting hello `LogLevel` property too`Verbose` when calling hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span></span>

 <span data-ttu-id="c513e-106">По умолчанию журналы записываются tooa контейнер с именем `waimportexport`.</span><span class="sxs-lookup"><span data-stu-id="c513e-106">By default, logs are written tooa container named `waimportexport`.</span></span> <span data-ttu-id="c513e-107">Можно указать другое имя, установка hello `DiagnosticsPath` свойства при вызове hello `Put Job` или `Update Job Properties` операций.</span><span class="sxs-lookup"><span data-stu-id="c513e-107">You can specify a different name by setting hello `DiagnosticsPath` property when calling hello `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="c513e-108">Hello журналы хранятся в виде блочных больших двоичных объектов с hello следующее соглашение об именовании: `waies/jobname_driveid_timestamp_logtype.xml`.</span><span class="sxs-lookup"><span data-stu-id="c513e-108">hello logs are stored as block blobs with hello following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.</span></span>

 <span data-ttu-id="c513e-109">Вы можете получить hello URI журналов заданий hello, вызывающему Привет [получения задания](/rest/api/storageimportexport/jobs#Jobs_Get) операции.</span><span class="sxs-lookup"><span data-stu-id="c513e-109">You can retrieve hello URI of hello logs for a job by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="c513e-110">Hello URI для hello подробного журнала возвращается в hello `VerboseLogUri` свойство для каждого диска, а hello URI для журнала ошибок hello возвращается в hello `ErrorLogUri` свойство.</span><span class="sxs-lookup"><span data-stu-id="c513e-110">hello URI for hello verbose log is returned in hello `VerboseLogUri` property for each drive, while hello URI for hello error log is returned in hello `ErrorLogUri` property.</span></span>

<span data-ttu-id="c513e-111">Можно использовать hello, ведение журнала данных tooidentify hello следующих ситуаций.</span><span class="sxs-lookup"><span data-stu-id="c513e-111">You can use hello logging data tooidentify hello following issues.</span></span>

## <a name="drive-errors"></a><span data-ttu-id="c513e-112">Ошибки диска</span><span class="sxs-lookup"><span data-stu-id="c513e-112">Drive errors</span></span>

<span data-ttu-id="c513e-113">Hello следующих элементов относятся ошибки диска:</span><span class="sxs-lookup"><span data-stu-id="c513e-113">hello following items are classified as drive errors:</span></span>

-   <span data-ttu-id="c513e-114">Ошибки доступа или чтении hello файла манифеста</span><span class="sxs-lookup"><span data-stu-id="c513e-114">Errors in accessing or reading hello manifest file</span></span>

-   <span data-ttu-id="c513e-115">Неправильные ключи BitLocker.</span><span class="sxs-lookup"><span data-stu-id="c513e-115">Incorrect BitLocker keys</span></span>

-   <span data-ttu-id="c513e-116">Ошибки операций чтения или записи с диском.</span><span class="sxs-lookup"><span data-stu-id="c513e-116">Drive read/write errors</span></span>

## <a name="blob-errors"></a><span data-ttu-id="c513e-117">Ошибки больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="c513e-117">Blob errors</span></span>

<span data-ttu-id="c513e-118">Hello следующих элементов относятся ошибки больших двоичных объектов:</span><span class="sxs-lookup"><span data-stu-id="c513e-118">hello following items are classified as blob errors:</span></span>

-   <span data-ttu-id="c513e-119">Неправильные либо конфликтующие большие двоичные объекты или их имена.</span><span class="sxs-lookup"><span data-stu-id="c513e-119">Incorrect or conflicting blob or names</span></span>

-   <span data-ttu-id="c513e-120">Отсутствуют файлы.</span><span class="sxs-lookup"><span data-stu-id="c513e-120">Missing files</span></span>

-   <span data-ttu-id="c513e-121">Не удалось найти большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="c513e-121">Blob not found</span></span>

-   <span data-ttu-id="c513e-122">Усеченные файлы (файлы hello на диске hello меньше, чем указано в манифесте hello)</span><span class="sxs-lookup"><span data-stu-id="c513e-122">Truncated files (hello files on hello disk are smaller than specified in hello manifest)</span></span>

-   <span data-ttu-id="c513e-123">Повреждено содержимое файла (для заданий импорта, выявляется по несовпадению контрольной суммы MD5).</span><span class="sxs-lookup"><span data-stu-id="c513e-123">Corrupted file content (for import jobs, detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="c513e-124">Повреждены файлы метаданных и свойств большого двоичного объекта (обнаружено несовпадение контрольной суммы MD5).</span><span class="sxs-lookup"><span data-stu-id="c513e-124">Corrupted blob metadata and property files (detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="c513e-125">Неверная схема для свойства большого двоичного объекта hello или файлов метаданных</span><span class="sxs-lookup"><span data-stu-id="c513e-125">Incorrect schema for hello blob properties and/or metadata files</span></span>

<span data-ttu-id="c513e-126">Возможны ситуации, где некоторые части задания импорта или экспорта не завершаются успешно, хотя hello в целом по-прежнему завершения задания.</span><span class="sxs-lookup"><span data-stu-id="c513e-126">There may be cases where some parts of an import or export job do not complete successfully, while hello overall job still completes.</span></span> <span data-ttu-id="c513e-127">В этом случае можно передать или загрузить hello отсутствует части hello данных по сети, или можно создать новые данные hello tootransfer задания.</span><span class="sxs-lookup"><span data-stu-id="c513e-127">In this case, you can either upload or download hello missing pieces of hello data over network, or you can create a new job tootransfer hello data.</span></span> <span data-ttu-id="c513e-128">В разделе hello [Справочник средство импорта и экспорта Azure](storage-import-export-tool-how-to-v1.md) toolearn как toorepair hello данных по сети.</span><span class="sxs-lookup"><span data-stu-id="c513e-128">See hello [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) toolearn how toorepair hello data over network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c513e-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c513e-129">Next steps</span></span>

* [<span data-ttu-id="c513e-130">С помощью REST API службы импорта и экспорта hello</span><span class="sxs-lookup"><span data-stu-id="c513e-130">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
