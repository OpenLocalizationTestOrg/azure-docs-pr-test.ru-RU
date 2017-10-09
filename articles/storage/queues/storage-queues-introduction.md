---
title: "aaaIntroduction tooAzure хранилища очередей | Документы Microsoft"
description: "Введение tooAzure хранилища очередей"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: robinsh
ms.openlocfilehash: 669effedff7beedde8a119c350a2a70edafedcf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooqueues"></a><span data-ttu-id="5d8bb-103">Введение tooQueues</span><span class="sxs-lookup"><span data-stu-id="5d8bb-103">Introduction tooQueues</span></span>

<span data-ttu-id="5d8bb-104">Хранилище Azure очереди — это служба для хранения большого количества сообщений, которые может осуществляться из любого места в Здравствуй, мир! через вызовы прошедшего проверку подлинности, протокол HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5d8bb-104">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="5d8bb-105">Сообщение одной очереди может быть вверх too64 КБ и очередь может содержать миллионы сообщений вверх toohello предел общая емкость учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5d8bb-105">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

## <a name="common-uses"></a><span data-ttu-id="5d8bb-106">Распространенные варианты использования</span><span class="sxs-lookup"><span data-stu-id="5d8bb-106">Common uses</span></span>

<span data-ttu-id="5d8bb-107">Наиболее частые способы использования хранилища очередей включают:</span><span class="sxs-lookup"><span data-stu-id="5d8bb-107">Common uses of Queue storage include:</span></span>

* <span data-ttu-id="5d8bb-108">Создание невыполненной работы tooprocess асинхронно</span><span class="sxs-lookup"><span data-stu-id="5d8bb-108">Creating a backlog of work tooprocess asynchronously</span></span>
* <span data-ttu-id="5d8bb-109">Передача сообщений из Azure web роли tooan рабочей роли Azure</span><span class="sxs-lookup"><span data-stu-id="5d8bb-109">Passing messages from an Azure web role tooan Azure worker role</span></span>

## <a name="queue-service-concepts"></a><span data-ttu-id="5d8bb-110">Основные понятия службы очередей</span><span class="sxs-lookup"><span data-stu-id="5d8bb-110">Queue service concepts</span></span>

<span data-ttu-id="5d8bb-111">Служба очередей Hello содержит hello следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="5d8bb-111">hello Queue service contains hello following components:</span></span>

![Понятия очереди](./media/storage-queues-introduction/queue1.png)

* <span data-ttu-id="5d8bb-113">**Формат URL-адреса:** очереди можно с помощью hello следующий формат URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="5d8bb-113">**URL format:** Queues are addressable using hello following URL format:</span></span>   
    <span data-ttu-id="5d8bb-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span><span class="sxs-lookup"><span data-stu-id="5d8bb-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span></span> 
  
    <span data-ttu-id="5d8bb-115">URL-адреса Hello адреса очереди в диаграмме hello:</span><span class="sxs-lookup"><span data-stu-id="5d8bb-115">hello following URL addresses a queue in hello diagram:</span></span>  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* <span data-ttu-id="5d8bb-116">**Учетная запись хранения:** обращаться к tooAzure хранилища осуществляется через учетную запись хранилища.</span><span class="sxs-lookup"><span data-stu-id="5d8bb-116">**Storage account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="5d8bb-117">Сведения об емкости учетной записи хранения см. в статье [Целевые показатели масштабируемости и производительности службы хранилища Azure](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5d8bb-117">See [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) for details about storage account capacity.</span></span>

* <span data-ttu-id="5d8bb-118">**Очередь**. Очередь содержит набор сообщений.</span><span class="sxs-lookup"><span data-stu-id="5d8bb-118">**Queue:** A queue contains a set of messages.</span></span> <span data-ttu-id="5d8bb-119">Все сообщения должны находиться в очереди.</span><span class="sxs-lookup"><span data-stu-id="5d8bb-119">All messages must be in a queue.</span></span> <span data-ttu-id="5d8bb-120">Обратите внимание, что это имя очереди hello должны указываться прописными буквами.</span><span class="sxs-lookup"><span data-stu-id="5d8bb-120">Note that hello queue name must be all lowercase.</span></span> <span data-ttu-id="5d8bb-121">Дополнительные сведения см. в статье о [присвоении имен очередям и метаданным](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="5d8bb-121">For information on naming queues, see [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

* <span data-ttu-id="5d8bb-122">**Сообщение об ошибке:** A-сообщения, в любом формате из копии too64 КБ.</span><span class="sxs-lookup"><span data-stu-id="5d8bb-122">**Message:** A message, in any format, of up too64 KB.</span></span> <span data-ttu-id="5d8bb-123">Максимальное время Hello, сообщение может оставаться в очереди hello составляет семь дней.</span><span class="sxs-lookup"><span data-stu-id="5d8bb-123">hello maximum time that a message can remain in hello queue is seven days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d8bb-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5d8bb-124">Next steps</span></span>

* [<span data-ttu-id="5d8bb-125">создать учетную запись хранения;</span><span class="sxs-lookup"><span data-stu-id="5d8bb-125">Create a storage account</span></span>](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="5d8bb-126">Начало работы с очередями с использованием .NET</span><span class="sxs-lookup"><span data-stu-id="5d8bb-126">Getting started with Queues using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
