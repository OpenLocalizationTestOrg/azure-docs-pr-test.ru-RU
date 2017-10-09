---
title: "aaaAzure наблюдения за производительностью службы структуры | Документы Microsoft"
description: "Узнайте о счетчиках производительности для мониторинга и диагностики кластеров Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 54d4c62b7250a1f70b0898ba07ae5a37716f4cf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="performance-metrics"></a><span data-ttu-id="6201c-103">Метрики производительности</span><span class="sxs-lookup"><span data-stu-id="6201c-103">Performance metrics</span></span>

<span data-ttu-id="6201c-104">Метрики должно быть производительности hello собранных toounderstand кластера, а также в нем приложения hello.</span><span class="sxs-lookup"><span data-stu-id="6201c-104">Metrics should be collected toounderstand hello performance of your cluster as well as hello applications running in it.</span></span> <span data-ttu-id="6201c-105">Для кластеров Service Fabric рекомендуется сбор hello следующие счетчики производительности.</span><span class="sxs-lookup"><span data-stu-id="6201c-105">For Service Fabric clusters, we recommend collecting hello following performance counters.</span></span>

## <a name="nodes"></a><span data-ttu-id="6201c-106">Nodes</span><span class="sxs-lookup"><span data-stu-id="6201c-106">Nodes</span></span>

<span data-ttu-id="6201c-107">Для машин hello в кластере рассмотрите возможность сбора hello следующие счетчики производительности, toobetter понять hello нагрузки на каждом компьютере и внесите соответствующие кластера масштабирования решения.</span><span class="sxs-lookup"><span data-stu-id="6201c-107">For hello machines in your cluster, consider collecting hello following performance counters toobetter understand hello load on each machine and make appropriate cluster scaling decisions.</span></span>

| <span data-ttu-id="6201c-108">Категория счетчика</span><span class="sxs-lookup"><span data-stu-id="6201c-108">Counter Category</span></span> | <span data-ttu-id="6201c-109">Имя счетчика</span><span class="sxs-lookup"><span data-stu-id="6201c-109">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="6201c-110">Физический диск (а диск)</span><span class="sxs-lookup"><span data-stu-id="6201c-110">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6201c-111">Среднее Длина очереди чтения с диска</span><span class="sxs-lookup"><span data-stu-id="6201c-111">Avg. Disk Read Queue Length</span></span> |
| <span data-ttu-id="6201c-112">Физический диск (а диск)</span><span class="sxs-lookup"><span data-stu-id="6201c-112">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6201c-113">Среднее Длина очереди записи на диск</span><span class="sxs-lookup"><span data-stu-id="6201c-113">Avg. Disk Write Queue Length</span></span> |
| <span data-ttu-id="6201c-114">Физический диск (а диск)</span><span class="sxs-lookup"><span data-stu-id="6201c-114">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6201c-115">Среднее время чтения с диска (с)</span><span class="sxs-lookup"><span data-stu-id="6201c-115">Avg. Disk sec/Read</span></span> |
| <span data-ttu-id="6201c-116">Физический диск (а диск)</span><span class="sxs-lookup"><span data-stu-id="6201c-116">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6201c-117">Среднее время записи на диск (с)</span><span class="sxs-lookup"><span data-stu-id="6201c-117">Avg. Disk sec/Write</span></span> |
| <span data-ttu-id="6201c-118">Физический диск (а диск)</span><span class="sxs-lookup"><span data-stu-id="6201c-118">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6201c-119">Операций чтения с диска в секунду </span><span class="sxs-lookup"><span data-stu-id="6201c-119">Disk Reads/sec</span></span> |
| <span data-ttu-id="6201c-120">Физический диск (а диск)</span><span class="sxs-lookup"><span data-stu-id="6201c-120">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6201c-121">Скорость чтения с диска (байт/с) </span><span class="sxs-lookup"><span data-stu-id="6201c-121">Disk Read Bytes/sec</span></span> |
| <span data-ttu-id="6201c-122">Физический диск (а диск)</span><span class="sxs-lookup"><span data-stu-id="6201c-122">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6201c-123">Операций записи на диск в секунду</span><span class="sxs-lookup"><span data-stu-id="6201c-123">Disk Writes/sec</span></span> |
| <span data-ttu-id="6201c-124">Физический диск (а диск)</span><span class="sxs-lookup"><span data-stu-id="6201c-124">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6201c-125">Скорость записи на диск (байт/с)</span><span class="sxs-lookup"><span data-stu-id="6201c-125">Disk Write Bytes/sec</span></span> |
| <span data-ttu-id="6201c-126">Память</span><span class="sxs-lookup"><span data-stu-id="6201c-126">Memory</span></span> | <span data-ttu-id="6201c-127">Доступный объем в МБ</span><span class="sxs-lookup"><span data-stu-id="6201c-127">Available MBytes</span></span> |
| <span data-ttu-id="6201c-128">Файл подкачки</span><span class="sxs-lookup"><span data-stu-id="6201c-128">PagingFile</span></span> | <span data-ttu-id="6201c-129">% использования</span><span class="sxs-lookup"><span data-stu-id="6201c-129">% Usage</span></span> |
| <span data-ttu-id="6201c-130">Обработка (всего)</span><span class="sxs-lookup"><span data-stu-id="6201c-130">Process(Total)</span></span> | <span data-ttu-id="6201c-131">% загруженности процессора</span><span class="sxs-lookup"><span data-stu-id="6201c-131">% Processor Time</span></span> |
| <span data-ttu-id="6201c-132">Обработка (на службу)</span><span class="sxs-lookup"><span data-stu-id="6201c-132">Process (per service)</span></span> | <span data-ttu-id="6201c-133">% загруженности процессора</span><span class="sxs-lookup"><span data-stu-id="6201c-133">% Processor Time</span></span> |
| <span data-ttu-id="6201c-134">Обработка (на службу)</span><span class="sxs-lookup"><span data-stu-id="6201c-134">Process (per service)</span></span> | <span data-ttu-id="6201c-135">Идентификатор процесса</span><span class="sxs-lookup"><span data-stu-id="6201c-135">ID Process</span></span> |
| <span data-ttu-id="6201c-136">Обработка (на службу)</span><span class="sxs-lookup"><span data-stu-id="6201c-136">Process (per service)</span></span> | <span data-ttu-id="6201c-137">Байты исключительного пользования</span><span class="sxs-lookup"><span data-stu-id="6201c-137">Private Bytes</span></span> |
| <span data-ttu-id="6201c-138">Обработка (на службу)</span><span class="sxs-lookup"><span data-stu-id="6201c-138">Process (per service)</span></span> | <span data-ttu-id="6201c-139">Счетчик потоков</span><span class="sxs-lookup"><span data-stu-id="6201c-139">Thread Count</span></span> |
| <span data-ttu-id="6201c-140">Обработка (на службу)</span><span class="sxs-lookup"><span data-stu-id="6201c-140">Process (per service)</span></span> | <span data-ttu-id="6201c-141">Байт виртуальной памяти</span><span class="sxs-lookup"><span data-stu-id="6201c-141">Virtual Bytes</span></span> |
| <span data-ttu-id="6201c-142">Обработка (на службу)</span><span class="sxs-lookup"><span data-stu-id="6201c-142">Process (per service)</span></span> | <span data-ttu-id="6201c-143">Рабочий набор</span><span class="sxs-lookup"><span data-stu-id="6201c-143">Working Set</span></span> |
| <span data-ttu-id="6201c-144">Обработка (на службу)</span><span class="sxs-lookup"><span data-stu-id="6201c-144">Process (per service)</span></span> | <span data-ttu-id="6201c-145">Рабочий набор (частный)</span><span class="sxs-lookup"><span data-stu-id="6201c-145">Working Set - Private</span></span> |

## <a name="net-applications-and-services"></a><span data-ttu-id="6201c-146">Приложения и службы .NET</span><span class="sxs-lookup"><span data-stu-id="6201c-146">.NET applications and services</span></span>

<span data-ttu-id="6201c-147">Собирать следующие счетчики при развертывании кластера tooyour .NET services hello.</span><span class="sxs-lookup"><span data-stu-id="6201c-147">Collect hello following counters if you are deploying .NET services tooyour cluster.</span></span> 

| <span data-ttu-id="6201c-148">Категория счетчика</span><span class="sxs-lookup"><span data-stu-id="6201c-148">Counter Category</span></span> | <span data-ttu-id="6201c-149">Имя счетчика</span><span class="sxs-lookup"><span data-stu-id="6201c-149">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="6201c-150">Память CLR .NET (на службу)</span><span class="sxs-lookup"><span data-stu-id="6201c-150">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6201c-151">ИД процесса</span><span class="sxs-lookup"><span data-stu-id="6201c-151">Process ID</span></span> |
| <span data-ttu-id="6201c-152">Память CLR .NET (на службу)</span><span class="sxs-lookup"><span data-stu-id="6201c-152">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6201c-153">Всего фиксировано байт</span><span class="sxs-lookup"><span data-stu-id="6201c-153"># Total committed Bytes</span></span> |
| <span data-ttu-id="6201c-154">Память CLR .NET (на службу)</span><span class="sxs-lookup"><span data-stu-id="6201c-154">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6201c-155">Всего зарезервировано байт</span><span class="sxs-lookup"><span data-stu-id="6201c-155"># Total reserved Bytes</span></span> |
| <span data-ttu-id="6201c-156">Память CLR .NET (на службу)</span><span class="sxs-lookup"><span data-stu-id="6201c-156">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6201c-157">Байт во всех кучах</span><span class="sxs-lookup"><span data-stu-id="6201c-157"># Bytes in all Heaps</span></span> |
| <span data-ttu-id="6201c-158">Память CLR .NET (на службу)</span><span class="sxs-lookup"><span data-stu-id="6201c-158">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6201c-159">Сборов мусора для поколения 0</span><span class="sxs-lookup"><span data-stu-id="6201c-159"># Gen 0 Collections</span></span> |
| <span data-ttu-id="6201c-160">Память CLR .NET (на службу)</span><span class="sxs-lookup"><span data-stu-id="6201c-160">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6201c-161">Сборов мусора для поколения 1</span><span class="sxs-lookup"><span data-stu-id="6201c-161"># Gen 1 Collections</span></span> |
| <span data-ttu-id="6201c-162">Память CLR .NET (на службу)</span><span class="sxs-lookup"><span data-stu-id="6201c-162">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6201c-163">Сборов мусора для поколения 2</span><span class="sxs-lookup"><span data-stu-id="6201c-163"># Gen 2 Collections</span></span> |
| <span data-ttu-id="6201c-164">Память CLR .NET (на службу)</span><span class="sxs-lookup"><span data-stu-id="6201c-164">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6201c-165">Время на сборку мусора, %</span><span class="sxs-lookup"><span data-stu-id="6201c-165">% Time in GC</span></span> |

### <a name="service-fabrics-custom-performance-counters"></a><span data-ttu-id="6201c-166">Настраиваемые счетчики производительности Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6201c-166">Service Fabric's custom performance counters</span></span>

<span data-ttu-id="6201c-167">Service Fabric создает достаточное число настраиваемых счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="6201c-167">Service Fabric generates a substantial amount of custom performance counters.</span></span> <span data-ttu-id="6201c-168">Если пакет SDK для hello, вы увидите hello полный список на компьютере Windows на монитор производительности приложения (Пуск > системный монитор).</span><span class="sxs-lookup"><span data-stu-id="6201c-168">If you have hello SDK installed, you can see hello comprehensive list on your Windows machine in your Performance Monitor application (Start > Performance Monitor).</span></span> 

<span data-ttu-id="6201c-169">В приложениях hello развертывании tooyour кластера, при использовании службы Reliable Actor добавьте countes из `Service Fabric Actor` и `Service Fabric Actor Method` категории (см. [диагностики субъекты надежные службы структуры](service-fabric-reliable-actors-diagnostics.md)).</span><span class="sxs-lookup"><span data-stu-id="6201c-169">In hello applications you are deploying tooyour cluster, if you are using Reliable Actors, add countes from `Service Fabric Actor` and `Service Fabric Actor Method` categories (see [Service Fabric Reliable Actors Diagnostics](service-fabric-reliable-actors-diagnostics.md)).</span></span>

<span data-ttu-id="6201c-170">Для Reliable Services имеются аналогичные категории счетчиков `Service Fabric Service` и `Service Fabric Service Method`, данные которых следует собирать.</span><span class="sxs-lookup"><span data-stu-id="6201c-170">If you use Reliable Services, we similarly have `Service Fabric Service` and `Service Fabric Service Method` counter categories that you should collect counters from.</span></span> 

<span data-ttu-id="6201c-171">При использовании надежного коллекций, рекомендуется добавить hello `Avg. Transaction ms/Commit` из hello `Service Fabric Transactional Replicator` задержки фиксации среднее hello toocollect каждой метрики транзакции.</span><span class="sxs-lookup"><span data-stu-id="6201c-171">If you use Reliable Collections, we recommend adding hello `Avg. Transaction ms/Commit` from hello `Service Fabric Transactional Replicator` toocollect hello average commit latency per transaction metric.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6201c-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6201c-172">Next steps</span></span>

* <span data-ttu-id="6201c-173">Дополнительные сведения о [созданием события на уровне платформы hello](service-fabric-diagnostics-event-generation-infra.md) в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6201c-173">Learn more about [event generation at hello platform level](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span></span>
* <span data-ttu-id="6201c-174">Собирайте метрики производительности с помощью [системы диагностики Azure](service-fabric-diagnostics-event-aggregation-wad.md).</span><span class="sxs-lookup"><span data-stu-id="6201c-174">Collect performance metrics through [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span></span>
