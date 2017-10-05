---
title: "Вывод списка всех заданий импорта и экспорта Azure | Документация Майкрософт"
description: "Узнайте, как вывести список всех заданий службы импорта и экспорта Azure в подписке."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f2e619be-1bbd-4a54-9472-9e2f70a83b64
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 1977bfc0e516088310f45ecdd960287eeed2c2d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="enumerating-jobs-in-the-azure-importexport-service"></a><span data-ttu-id="d07eb-103">Перечисление заданий в службе импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="d07eb-103">Enumerating jobs in the Azure Import/Export service</span></span>
<span data-ttu-id="d07eb-104">Чтобы перечислить все задания в подписке, вызовите операцию [List Jobs](/rest/api/storageimportexport/jobs#Jobs_List).</span><span class="sxs-lookup"><span data-stu-id="d07eb-104">To enumerate all jobs in a subscription, call the [List Jobs](/rest/api/storageimportexport/jobs#Jobs_List) operation.</span></span> <span data-ttu-id="d07eb-105">`List Jobs` возвращает список заданий, а также перечисленные ниже атрибуты:</span><span class="sxs-lookup"><span data-stu-id="d07eb-105">`List Jobs` returns a list of jobs as well as the following attributes:</span></span>

-   <span data-ttu-id="d07eb-106">тип задания (импорт или экспорт);</span><span class="sxs-lookup"><span data-stu-id="d07eb-106">The type of job (Import or Export)</span></span>

-   <span data-ttu-id="d07eb-107">текущее состояние задания;</span><span class="sxs-lookup"><span data-stu-id="d07eb-107">The current job state</span></span>

-   <span data-ttu-id="d07eb-108">связанная с задание учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="d07eb-108">The job's associated storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="d07eb-109">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d07eb-109">Next steps</span></span>

* [<span data-ttu-id="d07eb-110">Использование REST API службы импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="d07eb-110">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
