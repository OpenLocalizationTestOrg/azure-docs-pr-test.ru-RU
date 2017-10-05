---
title: "Событие начала удаления пула пакетной службы Azure | Документы Майкрософт"
description: "Справочник по событию начала удаления пула пакетной службы."
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
ms.openlocfilehash: f8a5241dce422e5c826ab428da6d7bc93284a1cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="pool-delete-start-event"></a><span data-ttu-id="f94d8-103">Событие начала удаления пула</span><span class="sxs-lookup"><span data-stu-id="f94d8-103">Pool delete start event</span></span>

 <span data-ttu-id="f94d8-104">Это событие создается при запуске операции удаления пула.</span><span class="sxs-lookup"><span data-stu-id="f94d8-104">This event is emitted when a pool delete operation has started.</span></span> <span data-ttu-id="f94d8-105">Так как удаление пула является асинхронным событием, можно ожидать, что после окончания этой операции возникнет событие завершения удаления пула.</span><span class="sxs-lookup"><span data-stu-id="f94d8-105">Since the pool delete is an asynchronous event, you can expect a pool delete complete event to be emitted once the delete operation completes.</span></span>

 <span data-ttu-id="f94d8-106">Ниже приведен пример текста для события начала удаления пула.</span><span class="sxs-lookup"><span data-stu-id="f94d8-106">The following example shows the body of a pool delete start event.</span></span>

```
{
    "id": "myPool1"
}
```

|<span data-ttu-id="f94d8-107">Элемент</span><span class="sxs-lookup"><span data-stu-id="f94d8-107">Element</span></span>|<span data-ttu-id="f94d8-108">Тип</span><span class="sxs-lookup"><span data-stu-id="f94d8-108">Type</span></span>|<span data-ttu-id="f94d8-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="f94d8-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="f94d8-110">id</span><span class="sxs-lookup"><span data-stu-id="f94d8-110">id</span></span>|<span data-ttu-id="f94d8-111">string</span><span class="sxs-lookup"><span data-stu-id="f94d8-111">String</span></span>|<span data-ttu-id="f94d8-112">Идентификатор пула.</span><span class="sxs-lookup"><span data-stu-id="f94d8-112">The id of the pool.</span></span>|