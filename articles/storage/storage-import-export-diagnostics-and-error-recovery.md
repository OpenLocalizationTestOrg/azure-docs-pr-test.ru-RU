---
title: "Диагностика и восстановление после ошибок для заданий импорта и экспорта Azure | Документация Майкрософт"
description: "Узнайте, как включить подробное ведение журнала для заданий службы импорта и экспорта Microsoft Azure."
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
ms.openlocfilehash: 0068aae9d6780aa41a070db0eb191d0d5a165d21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a><span data-ttu-id="e10ee-103">Диагностика и восстановление после ошибок для заданий импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="e10ee-103">Diagnostics and error recovery for Azure Import/Export jobs</span></span>
<span data-ttu-id="e10ee-104">Для каждого обрабатываемого диска служба импорта и экспорта Azure создает журнал ошибок в соответствующей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="e10ee-104">For each drive processed, the Azure Import/Export service creates an error log in the associated storage account.</span></span> <span data-ttu-id="e10ee-105">Можно также включить ведение подробного журнала, задав для свойства `LogLevel` значение `Verbose` при вызове операции [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) или [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update).</span><span class="sxs-lookup"><span data-stu-id="e10ee-105">You can also enable verbose logging by setting the `LogLevel` property to `Verbose` when calling the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span></span>

 <span data-ttu-id="e10ee-106">По умолчанию журналы записываются в контейнер `waimportexport`.</span><span class="sxs-lookup"><span data-stu-id="e10ee-106">By default, logs are written to a container named `waimportexport`.</span></span> <span data-ttu-id="e10ee-107">При вызове операции `Put Job` или `Update Job Properties` в свойстве `DiagnosticsPath` можно указать другое имя.</span><span class="sxs-lookup"><span data-stu-id="e10ee-107">You can specify a different name by setting the `DiagnosticsPath` property when calling the `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="e10ee-108">Журналы хранятся в виде блочных BLOB-объектов, для которых действует следующее соглашение об именовании: `waies/jobname_driveid_timestamp_logtype.xml`.</span><span class="sxs-lookup"><span data-stu-id="e10ee-108">The logs are stored as block blobs with the following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.</span></span>

 <span data-ttu-id="e10ee-109">Универсальный код ресурса (URI) журналов для задания можно получить, вызвав операцию [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get).</span><span class="sxs-lookup"><span data-stu-id="e10ee-109">You can retrieve the URI of the logs for a job by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="e10ee-110">Универсальный код ресурса (URI) подробного журнала возвращается в свойство `VerboseLogUri` для каждого диска, а универсальный код ресурса (URI) журнала ошибок — в свойство `ErrorLogUri`.</span><span class="sxs-lookup"><span data-stu-id="e10ee-110">The URI for the verbose log is returned in the `VerboseLogUri` property for each drive, while the URI for the error log is returned in the `ErrorLogUri` property.</span></span>

<span data-ttu-id="e10ee-111">Данные журнала можно использовать для выявления следующих проблем.</span><span class="sxs-lookup"><span data-stu-id="e10ee-111">You can use the logging data to identify the following issues.</span></span>

## <a name="drive-errors"></a><span data-ttu-id="e10ee-112">Ошибки диска</span><span class="sxs-lookup"><span data-stu-id="e10ee-112">Drive errors</span></span>

<span data-ttu-id="e10ee-113">К ошибкам диска относятся следующие ошибки:</span><span class="sxs-lookup"><span data-stu-id="e10ee-113">The following items are classified as drive errors:</span></span>

-   <span data-ttu-id="e10ee-114">Ошибки при доступе к файлу манифеста или его чтении.</span><span class="sxs-lookup"><span data-stu-id="e10ee-114">Errors in accessing or reading the manifest file</span></span>

-   <span data-ttu-id="e10ee-115">Неправильные ключи BitLocker.</span><span class="sxs-lookup"><span data-stu-id="e10ee-115">Incorrect BitLocker keys</span></span>

-   <span data-ttu-id="e10ee-116">Ошибки операций чтения или записи с диском.</span><span class="sxs-lookup"><span data-stu-id="e10ee-116">Drive read/write errors</span></span>

## <a name="blob-errors"></a><span data-ttu-id="e10ee-117">Ошибки больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="e10ee-117">Blob errors</span></span>

<span data-ttu-id="e10ee-118">К ошибкам больших двоичных объектов относятся следующие ошибки:</span><span class="sxs-lookup"><span data-stu-id="e10ee-118">The following items are classified as blob errors:</span></span>

-   <span data-ttu-id="e10ee-119">Неправильные либо конфликтующие большие двоичные объекты или их имена.</span><span class="sxs-lookup"><span data-stu-id="e10ee-119">Incorrect or conflicting blob or names</span></span>

-   <span data-ttu-id="e10ee-120">Отсутствуют файлы.</span><span class="sxs-lookup"><span data-stu-id="e10ee-120">Missing files</span></span>

-   <span data-ttu-id="e10ee-121">Не удалось найти большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="e10ee-121">Blob not found</span></span>

-   <span data-ttu-id="e10ee-122">Усеченные файлы (файлы на диске меньше, чем указано в манифесте).</span><span class="sxs-lookup"><span data-stu-id="e10ee-122">Truncated files (the files on the disk are smaller than specified in the manifest)</span></span>

-   <span data-ttu-id="e10ee-123">Повреждено содержимое файла (для заданий импорта, выявляется по несовпадению контрольной суммы MD5).</span><span class="sxs-lookup"><span data-stu-id="e10ee-123">Corrupted file content (for import jobs, detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="e10ee-124">Повреждены файлы метаданных и свойств большого двоичного объекта (обнаружено несовпадение контрольной суммы MD5).</span><span class="sxs-lookup"><span data-stu-id="e10ee-124">Corrupted blob metadata and property files (detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="e10ee-125">Неправильная схема для файлов свойств и (или) метаданных большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="e10ee-125">Incorrect schema for the blob properties and/or metadata files</span></span>

<span data-ttu-id="e10ee-126">Возможны ситуации, когда некоторые части задания импорта или экспорта не завершаются успешно, хотя само задание считается выполненным.</span><span class="sxs-lookup"><span data-stu-id="e10ee-126">There may be cases where some parts of an import or export job do not complete successfully, while the overall job still completes.</span></span> <span data-ttu-id="e10ee-127">В этом случае можно передать или скачать отсутствующие части данных по сети, можно также создать новое задание для передачи данных.</span><span class="sxs-lookup"><span data-stu-id="e10ee-127">In this case, you can either upload or download the missing pieces of the data over network, or you can create a new job to transfer the data.</span></span> <span data-ttu-id="e10ee-128">Ознакомьтесь со [справочником по инструменту импорта и экспорта Azure](storage-import-export-tool-how-to-v1.md), чтобы узнать, как восстанавливать данные по сети.</span><span class="sxs-lookup"><span data-stu-id="e10ee-128">See the [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) to learn how to repair the data over network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e10ee-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e10ee-129">Next steps</span></span>

* [<span data-ttu-id="e10ee-130">Использование REST API службы импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="e10ee-130">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
