---
title: "hello aaaUsing REST API службы импорта и экспорта Azure | Документы Microsoft"
description: "Узнайте, где toofind ресурсы для hello импорта и экспорта Azure с помощью службы REST API, включая обоих tooand как справочные материалы."
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
ms.openlocfilehash: fc7e1007ad632cf6f771c2545644f8de43c8f181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-service-rest-api"></a><span data-ttu-id="f9d21-103">С помощью REST API службы импорта и экспорта Azure hello</span><span class="sxs-lookup"><span data-stu-id="f9d21-103">Using hello Azure Import/Export service REST API</span></span>

<span data-ttu-id="f9d21-104">Hello службы импорта и экспорта Microsoft Azure предоставляет API-Интерфейс REST tooenable программное управление заданиями импорта и экспорта.</span><span class="sxs-lookup"><span data-stu-id="f9d21-104">hello Microsoft Azure Import/Export service exposes a REST API tooenable programmatic control of import/export jobs.</span></span> <span data-ttu-id="f9d21-105">Можно использовать API-Интерфейс REST hello tooperform все hello импорта и экспорта операций, которые можно выполнять с hello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f9d21-105">You can use hello REST API tooperform all of hello import/export operations that you can perform with hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="f9d21-106">Кроме того можно использовать API-интерфейса REST tooperform hello определенных детализированных операций, таких как запрос hello процент завершения задания, которое в настоящее время недоступно в hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f9d21-106">Additionally, you can use hello REST API tooperform certain granular operations, such as querying hello percentage completion of a job, which is not currently available in hello Azure classic portal.</span></span>

<span data-ttu-id="f9d21-107">В разделе [tooBlob hello импорта и экспорта Microsoft Azure службы tooTransfer данные хранилища с помощью](../storage-import-export-service.md) Обзор службы импорта и экспорта hello и учебник, в котором показано, как toouse hello классического портала toocreate и управления импортом и задания экспорта.</span><span class="sxs-lookup"><span data-stu-id="f9d21-107">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](../storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello classic portal toocreate and manage import and export jobs.</span></span>

## <a name="service-endpoints"></a><span data-ttu-id="f9d21-108">Конечные точки службы</span><span class="sxs-lookup"><span data-stu-id="f9d21-108">Service endpoints</span></span>

<span data-ttu-id="f9d21-109">Hello службы импорта и экспорта Azure — это поставщик ресурсов для диспетчера ресурсов Azure и предоставляет набор интерфейсов API REST в hello, следующая конечная точка HTTPS для управления заданиями импорта и экспорта:</span><span class="sxs-lookup"><span data-stu-id="f9d21-109">hello Azure Import/Export service is a resource provider for Azure Resource Manager and provides a set of REST APIs at hello following HTTPS endpoint for managing import/export jobs:</span></span>

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a><span data-ttu-id="f9d21-110">Управление версиями</span><span class="sxs-lookup"><span data-stu-id="f9d21-110">Versioning</span></span>

<span data-ttu-id="f9d21-111">Запросы, toohello службы импорта и экспорта необходимо указать hello `api-version` параметр и присвойте ему значение слишком`2016-11-01`.</span><span class="sxs-lookup"><span data-stu-id="f9d21-111">Requests toohello Import/Export service must specify hello `api-version` parameter and set its value too`2016-11-01`.</span></span>

## <a name="importexport-service-operations"></a><span data-ttu-id="f9d21-112">Операции службы импорта и экспорта</span><span class="sxs-lookup"><span data-stu-id="f9d21-112">Import/Export service operations</span></span>

[<span data-ttu-id="f9d21-113">Создание задания импорта</span><span class="sxs-lookup"><span data-stu-id="f9d21-113">Creating an import job</span></span>](../storage-import-export-creating-an-import-job.md)

[<span data-ttu-id="f9d21-114">Создание задания экспорта</span><span class="sxs-lookup"><span data-stu-id="f9d21-114">Creating an export job</span></span>](../storage-import-export-creating-an-export-job.md)

[<span data-ttu-id="f9d21-115">Получение сведений о состоянии задания</span><span class="sxs-lookup"><span data-stu-id="f9d21-115">Retrieving state information for a job</span></span>](storage-import-export-retrieving-state-info-for-a-job.md)

[<span data-ttu-id="f9d21-116">Перечисление заданий</span><span class="sxs-lookup"><span data-stu-id="f9d21-116">Enumerating jobs</span></span>](../storage-import-export-enumerating-jobs.md)

[<span data-ttu-id="f9d21-117">Отмена и удаление заданий</span><span class="sxs-lookup"><span data-stu-id="f9d21-117">Cancelling and deleting jobs</span></span>](storage-import-export-cancelling-and-deleting-jobs.md)

[<span data-ttu-id="f9d21-118">Архивация манифестов дисков</span><span class="sxs-lookup"><span data-stu-id="f9d21-118">Backing Up drive manifests</span></span>](../storage-import-export-backing-up-drive-manifests.md)

[<span data-ttu-id="f9d21-119">Диагностика и восстановление после ошибок для заданий импорта и экспорта</span><span class="sxs-lookup"><span data-stu-id="f9d21-119">Diagnostics and error recovery for Import/Export jobs</span></span>](../storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="f9d21-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f9d21-120">Next steps</span></span>

* <span data-ttu-id="f9d21-121">[Storage Import/Export REST](/rest/api/storageimportexport) (Справочник по API REST служб хранилища импорта и экспорта)</span><span class="sxs-lookup"><span data-stu-id="f9d21-121">[Storage Import/Export REST](/rest/api/storageimportexport)</span></span>
