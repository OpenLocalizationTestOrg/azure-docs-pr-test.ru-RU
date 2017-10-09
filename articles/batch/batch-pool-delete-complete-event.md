---
title: "AAA» событие завершения удаления пула | Документы Microsoft»"
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
ms.openlocfilehash: 494c371e48ebfb1bf3d2973a7401829a939ba141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-complete-event"></a><span data-ttu-id="85cad-103">Событие завершения удаления пула</span><span class="sxs-lookup"><span data-stu-id="85cad-103">Pool delete complete event</span></span>

 <span data-ttu-id="85cad-104">Это событие создается при завершении операции удаления пула.</span><span class="sxs-lookup"><span data-stu-id="85cad-104">This event is emitted when a pool delete operation has completed.</span></span>

 <span data-ttu-id="85cad-105">Hello примере показан текст hello событие завершения удаления пула.</span><span class="sxs-lookup"><span data-stu-id="85cad-105">hello following example shows hello body of a pool delete complete event.</span></span>

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|<span data-ttu-id="85cad-106">Элемент</span><span class="sxs-lookup"><span data-stu-id="85cad-106">Element</span></span>|<span data-ttu-id="85cad-107">Тип</span><span class="sxs-lookup"><span data-stu-id="85cad-107">Type</span></span>|<span data-ttu-id="85cad-108">Примечания</span><span class="sxs-lookup"><span data-stu-id="85cad-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="85cad-109">id</span><span class="sxs-lookup"><span data-stu-id="85cad-109">id</span></span>|<span data-ttu-id="85cad-110">Строка</span><span class="sxs-lookup"><span data-stu-id="85cad-110">String</span></span>|<span data-ttu-id="85cad-111">Идентификатор Hello hello пула.</span><span class="sxs-lookup"><span data-stu-id="85cad-111">hello id of hello pool.</span></span>|
|<span data-ttu-id="85cad-112">startTime</span><span class="sxs-lookup"><span data-stu-id="85cad-112">startTime</span></span>|<span data-ttu-id="85cad-113">DateTime</span><span class="sxs-lookup"><span data-stu-id="85cad-113">DateTime</span></span>|<span data-ttu-id="85cad-114">Удаление пула hello время Hello запуска.</span><span class="sxs-lookup"><span data-stu-id="85cad-114">hello time hello pool delete started.</span></span>|
|<span data-ttu-id="85cad-115">endTime</span><span class="sxs-lookup"><span data-stu-id="85cad-115">endTime</span></span>|<span data-ttu-id="85cad-116">DateTime</span><span class="sxs-lookup"><span data-stu-id="85cad-116">DateTime</span></span>|<span data-ttu-id="85cad-117">Hello время удаления пула hello завершения.</span><span class="sxs-lookup"><span data-stu-id="85cad-117">hello time hello pool delete completed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="85cad-118">Примечания</span><span class="sxs-lookup"><span data-stu-id="85cad-118">Remarks</span></span>
<span data-ttu-id="85cad-119">Дополнительные сведения о состояниях и кодах ошибок для операции изменения размера пула см. в статье [Удаление пула из учетной записи](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span><span class="sxs-lookup"><span data-stu-id="85cad-119">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span></span>