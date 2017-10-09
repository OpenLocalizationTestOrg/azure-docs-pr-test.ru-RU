---
title: "внутренние компоненты диспетчер состояния надежного структуры службы и надежного коллекции aaaAzure | Документы Microsoft"
description: "Углубленное рассмотрение концепции и проектирования надежных коллекций в Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 651bfb52785a2475e4840cd471e87220d1936391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a><span data-ttu-id="3e209-103">Внутренние компоненты диспетчера надежных состояний и надежных коллекций Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3e209-103">Azure Service Fabric Reliable State Manager and Reliable Collection internals</span></span>
<span data-ttu-id="3e209-104">В этом документе углубляется внутри надежного диспетчер состояния и надежного коллекции toosee как основные компоненты работают в фоновом hello.</span><span class="sxs-lookup"><span data-stu-id="3e209-104">This document delves inside Reliable State Manager and Reliable Collections toosee how core components work behind hello scenes.</span></span>

> [!NOTE]
> <span data-ttu-id="3e209-105">Этот документ находится на стадии разработки.</span><span class="sxs-lookup"><span data-stu-id="3e209-105">This document is work in-progress.</span></span> <span data-ttu-id="3e209-106">Добавьте комментарии toothis статью tootell нам теме хотелось бы Дополнительные сведения о toolearn.</span><span class="sxs-lookup"><span data-stu-id="3e209-106">Add comments toothis article tootell us what topic you would like toolearn more about.</span></span>
>

##  <a name="local-persistence-model-log-and-checkpoint"></a><span data-ttu-id="3e209-107">Модель локальной сохраняемости: журнал и контрольная точка</span><span class="sxs-lookup"><span data-stu-id="3e209-107">Local persistence model: log and checkpoint</span></span>
<span data-ttu-id="3e209-108">Hello надежного диспетчер состояния и надежного коллекций следуйте сохраняемости модель, которая называется журналов и контрольных точек.</span><span class="sxs-lookup"><span data-stu-id="3e209-108">hello Reliable State Manager and Reliable Collections follow a persistence model that is called Log and Checkpoint.</span></span>
<span data-ttu-id="3e209-109">В этой модели каждое изменение состояния сначала регистрируется на диске, а затем применяется в памяти.</span><span class="sxs-lookup"><span data-stu-id="3e209-109">In this model, each state change is logged on disk first and then applied in memory.</span></span>
<span data-ttu-id="3e209-110">Hello завершения самого сохраняется состояние лишь время от времени (так)</span><span class="sxs-lookup"><span data-stu-id="3e209-110">hello complete state itself is persisted only occasionally (a.k.a.</span></span> <span data-ttu-id="3e209-111">контрольная точка).</span><span class="sxs-lookup"><span data-stu-id="3e209-111">Checkpoint).</span></span>
<span data-ttu-id="3e209-112">Hello преимущество в том, что дельты, преобразуются в дополняющие записи на диск для повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="3e209-112">hello benefit is that deltas are turned into sequential append-only writes on disk for improved performance.</span></span>

<span data-ttu-id="3e209-113">toobetter понять hello журнала и модели контрольная точка, давайте сначала посмотрим сценарий бесконечный дисков hello.</span><span class="sxs-lookup"><span data-stu-id="3e209-113">toobetter understand hello Log and Checkpoint model, let’s first look at hello infinite disk scenario.</span></span>
<span data-ttu-id="3e209-114">Прежде чем они реплицируются Hello надежного диспетчер состояния заносит в журнал каждой операции.</span><span class="sxs-lookup"><span data-stu-id="3e209-114">hello Reliable State Manager logs every operation before it is replicated.</span></span>
<span data-ttu-id="3e209-115">Ведение журнала позволяет hello надежного коллекций tooapply hello операцию только в памяти.</span><span class="sxs-lookup"><span data-stu-id="3e209-115">Logging allows hello Reliable Collections tooapply hello operation only in memory.</span></span>
<span data-ttu-id="3e209-116">Поскольку журналы, сохраняются, и даже в том случае, когда hello реплики завершается ошибкой и перезапуска toobe hello надежного диспетчер состояний имеет достаточно сведений в его tooreplay журнала всех операций hello, потерял hello реплики.</span><span class="sxs-lookup"><span data-stu-id="3e209-116">Since logs are persisted, even when hello replica fails and needs toobe restarted, hello Reliable State Manager has enough information in its log tooreplay all hello operations hello replica has lost.</span></span>
<span data-ttu-id="3e209-117">Как диск hello является бесконечным, записи журнала не требуется удалить toobe и hello надежного коллекции должен toomanage только hello в оперативной памяти.</span><span class="sxs-lookup"><span data-stu-id="3e209-117">As hello disk is infinite, log records never need toobe removed and hello Reliable Collection needs toomanage only hello in-memory state.</span></span>

<span data-ttu-id="3e209-118">Теперь давайте рассмотрим сценарий конечное дисков hello.</span><span class="sxs-lookup"><span data-stu-id="3e209-118">Now let’s look at hello finite disk scenario.</span></span>
<span data-ttu-id="3e209-119">Записи журнала накапливаются, hello надежного диспетчер состояния запустите как недостаточно места на диске.</span><span class="sxs-lookup"><span data-stu-id="3e209-119">As log records accumulate, hello Reliable State Manager will run out of disk space.</span></span>
<span data-ttu-id="3e209-120">Прежде чем это произойдет, hello надежного диспетчер состояния должен tootruncate комнаты toomake журнала для новых записей hello.</span><span class="sxs-lookup"><span data-stu-id="3e209-120">Before that happens, hello Reliable State Manager needs tootruncate its log toomake room for hello newer records.</span></span>
<span data-ttu-id="3e209-121">Запросы диспетчера состояний надежное hello надежного коллекций toocheckpoint toodisk их состояние в памяти.</span><span class="sxs-lookup"><span data-stu-id="3e209-121">Reliable State Manager requests hello Reliable Collections toocheckpoint their in-memory state toodisk.</span></span>
<span data-ttu-id="3e209-122">На этом этапе hello надежного коллекций будет сохранять свое состояние в памяти.</span><span class="sxs-lookup"><span data-stu-id="3e209-122">At this point, hello Reliable Collections' would persist its in-memory state.</span></span>
<span data-ttu-id="3e209-123">После завершения их контрольные точки надежного коллекций hello hello надежного диспетчер состояния можно усечь toofree журнала hello места на диске.</span><span class="sxs-lookup"><span data-stu-id="3e209-123">Once hello Reliable Collections complete their checkpoints, hello Reliable State Manager can truncate hello log toofree up disk space.</span></span>
<span data-ttu-id="3e209-124">Когда hello реплике потребуется перезапустить toobe, надежные коллекций восстановить свое состояние контрольными точками и hello надежного диспетчер состояния восстанавливает воспроизводит все изменения состояния hello, произошедших с момента последней контрольной точки hello.</span><span class="sxs-lookup"><span data-stu-id="3e209-124">When hello replica needs toobe restarted, Reliable Collections recover their checkpointed state, and hello Reliable State Manager recovers and plays back all hello state changes that occurred since hello last checkpoint.</span></span>

<span data-ttu-id="3e209-125">Еще одно преимущество создания контрольных точек состоит в том, что в типичных сценариях они сокращают время восстановления.</span><span class="sxs-lookup"><span data-stu-id="3e209-125">Another value add of checkpointing is that it improves recovery times in common scenarios.</span></span> <span data-ttu-id="3e209-126">Журнал содержит все операции, которые произошли с момента последней контрольной точки hello.</span><span class="sxs-lookup"><span data-stu-id="3e209-126">Log contains all operations that have happened since hello last checkpoint.</span></span>
<span data-ttu-id="3e209-127">Поэтому он может включать несколько версий элемента, например несколько значений для конкретной строки в надежном словаре.</span><span class="sxs-lookup"><span data-stu-id="3e209-127">So it may include multiple versions of an item like multiple values for a given row in Reliable Dictionary.</span></span>
<span data-ttu-id="3e209-128">Напротив контрольные точки надежного коллекции hello только последнюю версию каждого значения для ключа.</span><span class="sxs-lookup"><span data-stu-id="3e209-128">In contrast, a Reliable Collection checkpoints only hello latest version of each value for a key.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e209-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3e209-129">Next steps</span></span>
* [<span data-ttu-id="3e209-130">Транзакции и блокировки</span><span class="sxs-lookup"><span data-stu-id="3e209-130">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

