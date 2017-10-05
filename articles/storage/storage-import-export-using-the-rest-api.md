---
title: "Использование REST API службы импорта и экспорта Azure | Документация Майкрософт"
description: "Узнайте, где найти документацию по использованию REST API службы импорта и экспорта Azure, включая практические руководства и справочные материалы."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 233f80e9-2e7f-48e0-9639-5c7785e7d743
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: e4f5ca289f4bd87574e448d37a1154b222f221f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-importexport-service-rest-api"></a><span data-ttu-id="e892e-103">Использование REST API службы импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="e892e-103">Using the Azure Import/Export service REST API</span></span>

<span data-ttu-id="e892e-104">Служба импорта и экспорта Microsoft Azure предоставляет REST API для программного управления заданиями импорта и экспорта.</span><span class="sxs-lookup"><span data-stu-id="e892e-104">The Microsoft Azure Import/Export service exposes a REST API to enable programmatic control of import/export jobs.</span></span> <span data-ttu-id="e892e-105">REST API можно использовать для всех операций импорта и экспорта, которые можно выполнять с помощью [портала Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e892e-105">You can use the REST API to perform all of the import/export operations that you can perform with the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="e892e-106">Кроме того, с помощью REST API можно выполнять определенные детализированные операции (например, запросить процент завершения задания), которые в настоящее время недоступны на классическом портале.</span><span class="sxs-lookup"><span data-stu-id="e892e-106">Additionally, you can use the REST API to perform certain granular operations, such as querying the percentage completion of a job, which are not currently available in the classic portal.</span></span>

<span data-ttu-id="e892e-107">Общие сведения о службе импорта и экспорта, а также руководство по использованию классического портала Azure для создания заданий импорта и экспорта и управления ими см. в статье [Использование службы импорта и экспорта Azure для передачи данных в хранилище BLOB-объектов](storage-import-export-service.md).</span><span class="sxs-lookup"><span data-stu-id="e892e-107">See [Using the Microsoft Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the classic portal to create and manage import and export jobs.</span></span>

## <a name="service-endpoints"></a><span data-ttu-id="e892e-108">Конечные точки службы</span><span class="sxs-lookup"><span data-stu-id="e892e-108">Service endpoints</span></span>

<span data-ttu-id="e892e-109">Служба импорта и экспорта Azure представляет собой поставщик ресурсов для Azure Resource Manager. Она предоставляет набор интерфейсов REST API для управления заданиями импорта и экспорта в следующей конечной точке HTTPS:</span><span class="sxs-lookup"><span data-stu-id="e892e-109">The Azure Import/Export service is a resource provider for Azure Resource Manager and provides a set of REST APIs at the following HTTPS endpoint for managing import/export jobs:</span></span>

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a><span data-ttu-id="e892e-110">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="e892e-110">Versioning</span></span>

<span data-ttu-id="e892e-111">В запросах к службе импорта и экспорта необходимо указать параметр `api-version` со значением `2016-11-01`.</span><span class="sxs-lookup"><span data-stu-id="e892e-111">Requests to the Import/Export service must specify the `api-version` parameter and set its value to `2016-11-01`.</span></span>

## <a name="importexport-service-operations"></a><span data-ttu-id="e892e-112">Операции службы импорта и экспорта</span><span class="sxs-lookup"><span data-stu-id="e892e-112">Import/Export service operations</span></span>

[<span data-ttu-id="e892e-113">Создание задания импорта</span><span class="sxs-lookup"><span data-stu-id="e892e-113">Creating an import job</span></span>](storage-import-export-creating-an-import-job.md)

[<span data-ttu-id="e892e-114">Создание задания экспорта</span><span class="sxs-lookup"><span data-stu-id="e892e-114">Creating an export job</span></span>](storage-import-export-creating-an-export-job.md)

[<span data-ttu-id="e892e-115">Получение сведений о состоянии задания</span><span class="sxs-lookup"><span data-stu-id="e892e-115">Retrieving state information for a job</span></span>](storage-import-export-retrieving-state-info-for-a-job.md)

[<span data-ttu-id="e892e-116">Перечисление заданий</span><span class="sxs-lookup"><span data-stu-id="e892e-116">Enumerating jobs</span></span>](storage-import-export-enumerating-jobs.md)

[<span data-ttu-id="e892e-117">Отмена и удаление заданий</span><span class="sxs-lookup"><span data-stu-id="e892e-117">Cancelling and deleting jobs</span></span>](storage-import-export-cancelling-and-deleting-jobs.md)

[<span data-ttu-id="e892e-118">Архивация манифестов дисков</span><span class="sxs-lookup"><span data-stu-id="e892e-118">Backing Up drive manifests</span></span>](storage-import-export-backing-up-drive-manifests.md)

[<span data-ttu-id="e892e-119">Диагностика и восстановление после ошибок для заданий импорта и экспорта</span><span class="sxs-lookup"><span data-stu-id="e892e-119">Diagnostics and error recovery for Import/Export jobs</span></span>](storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="e892e-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e892e-120">Next steps</span></span>

* <span data-ttu-id="e892e-121">[Storage Import/Export REST](/rest/api/storageimportexport) (Справочник по API REST служб хранилища импорта и экспорта)</span><span class="sxs-lookup"><span data-stu-id="e892e-121">[Storage Import/Export REST](/rest/api/storageimportexport)</span></span>
