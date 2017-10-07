---
title: "AAA» событие начала удаления пула пакетной службы Azure | Документы Microsoft»"
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
ms.openlocfilehash: 79bb28bffc760a49cc0a95062f5086dc96c6a795
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-start-event"></a><span data-ttu-id="00f94-103">Событие начала удаления пула</span><span class="sxs-lookup"><span data-stu-id="00f94-103">Pool delete start event</span></span>

 <span data-ttu-id="00f94-104">Это событие создается при запуске операции удаления пула.</span><span class="sxs-lookup"><span data-stu-id="00f94-104">This event is emitted when a pool delete operation has started.</span></span> <span data-ttu-id="00f94-105">Так как удаление пула hello асинхронного события, можно ожидать завершения toobe событие завершения удаления пула, создается после операции удаления hello.</span><span class="sxs-lookup"><span data-stu-id="00f94-105">Since hello pool delete is an asynchronous event, you can expect a pool delete complete event toobe emitted once hello delete operation completes.</span></span>

 <span data-ttu-id="00f94-106">Hello следующем примере показан текст hello события начала удаления пула.</span><span class="sxs-lookup"><span data-stu-id="00f94-106">hello following example shows hello body of a pool delete start event.</span></span>

```
{
    "id": "myPool1"
}
```

|<span data-ttu-id="00f94-107">Элемент</span><span class="sxs-lookup"><span data-stu-id="00f94-107">Element</span></span>|<span data-ttu-id="00f94-108">Тип</span><span class="sxs-lookup"><span data-stu-id="00f94-108">Type</span></span>|<span data-ttu-id="00f94-109">Примечания</span><span class="sxs-lookup"><span data-stu-id="00f94-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="00f94-110">id</span><span class="sxs-lookup"><span data-stu-id="00f94-110">id</span></span>|<span data-ttu-id="00f94-111">Строка</span><span class="sxs-lookup"><span data-stu-id="00f94-111">String</span></span>|<span data-ttu-id="00f94-112">Идентификатор Hello hello пула.</span><span class="sxs-lookup"><span data-stu-id="00f94-112">hello id of hello pool.</span></span>|
