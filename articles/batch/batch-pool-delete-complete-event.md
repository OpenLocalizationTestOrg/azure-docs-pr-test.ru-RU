---
title: "Событие завершения удаления пула пакетной службы Azure | Документы Майкрософт"
description: "Справочник по событию завершения удаления пула пакетной службы."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 890f2ba7fda37060c56177868d6214d517d91831
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="pool-delete-complete-event"></a><span data-ttu-id="92866-103">Событие завершения удаления пула</span><span class="sxs-lookup"><span data-stu-id="92866-103">Pool delete complete event</span></span>

 <span data-ttu-id="92866-104">Это событие создается при завершении операции удаления пула.</span><span class="sxs-lookup"><span data-stu-id="92866-104">This event is emitted when a pool delete operation has completed.</span></span>

 <span data-ttu-id="92866-105">Ниже приведен пример текста для события завершения удаления пула.</span><span class="sxs-lookup"><span data-stu-id="92866-105">The following example shows the body of a pool delete complete event.</span></span>

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|<span data-ttu-id="92866-106">Элемент</span><span class="sxs-lookup"><span data-stu-id="92866-106">Element</span></span>|<span data-ttu-id="92866-107">Тип</span><span class="sxs-lookup"><span data-stu-id="92866-107">Type</span></span>|<span data-ttu-id="92866-108">Примечания</span><span class="sxs-lookup"><span data-stu-id="92866-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="92866-109">id</span><span class="sxs-lookup"><span data-stu-id="92866-109">id</span></span>|<span data-ttu-id="92866-110">string</span><span class="sxs-lookup"><span data-stu-id="92866-110">String</span></span>|<span data-ttu-id="92866-111">Идентификатор пула.</span><span class="sxs-lookup"><span data-stu-id="92866-111">The id of the pool.</span></span>|
|<span data-ttu-id="92866-112">startTime</span><span class="sxs-lookup"><span data-stu-id="92866-112">startTime</span></span>|<span data-ttu-id="92866-113">DateTime</span><span class="sxs-lookup"><span data-stu-id="92866-113">DateTime</span></span>|<span data-ttu-id="92866-114">Время, когда было начато удаление пула.</span><span class="sxs-lookup"><span data-stu-id="92866-114">The time the pool delete started.</span></span>|
|<span data-ttu-id="92866-115">endTime</span><span class="sxs-lookup"><span data-stu-id="92866-115">endTime</span></span>|<span data-ttu-id="92866-116">DateTime</span><span class="sxs-lookup"><span data-stu-id="92866-116">DateTime</span></span>|<span data-ttu-id="92866-117">Время, когда удаление пула было завершено.</span><span class="sxs-lookup"><span data-stu-id="92866-117">The time the pool delete completed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="92866-118">Примечания</span><span class="sxs-lookup"><span data-stu-id="92866-118">Remarks</span></span>
<span data-ttu-id="92866-119">Дополнительные сведения о состояниях и кодах ошибок для операции изменения размера пула см. в статье [Удаление пула из учетной записи](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span><span class="sxs-lookup"><span data-stu-id="92866-119">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span></span>