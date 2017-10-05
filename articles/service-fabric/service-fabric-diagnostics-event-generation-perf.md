---
title: "Мониторинг производительности Azure Service Fabric | Документация Майкрософт"
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
ms.openlocfilehash: 9d63148c182c705b6b49733c59ed8fdd13872d72
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="performance-metrics"></a><span data-ttu-id="cb177-103">Метрики производительности</span><span class="sxs-lookup"><span data-stu-id="cb177-103">Performance metrics</span></span>

<span data-ttu-id="cb177-104">Метрики следует собирать для анализа производительности кластера, а также приложений, выполняющихся в нем.</span><span class="sxs-lookup"><span data-stu-id="cb177-104">Metrics should be collected to understand the performance of your cluster as well as the applications running in it.</span></span> <span data-ttu-id="cb177-105">Для кластеров Service Fabric рекомендуется собирать данные следующих счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="cb177-105">For Service Fabric clusters, we recommend collecting the following performance counters.</span></span>

## <a name="nodes"></a><span data-ttu-id="cb177-106">Nodes</span><span class="sxs-lookup"><span data-stu-id="cb177-106">Nodes</span></span>

<span data-ttu-id="cb177-107">Для компьютеров в кластере рассмотрите возможность сбора приведенных ниже счетчиков производительности, чтобы лучше понимать нагрузку на каждом компьютере и принимать соответствующие решения о масштабировании кластера.</span><span class="sxs-lookup"><span data-stu-id="cb177-107">For the machines in your cluster, consider collecting the following performance counters to better understand the load on each machine and make appropriate cluster scaling decisions.</span></span>

| <span data-ttu-id="cb177-108">Категория счетчика</span><span class="sxs-lookup"><span data-stu-id="cb177-108">Counter Category</span></span> | <span data-ttu-id="cb177-109">Имя счетчика</span><span class="sxs-lookup"><span data-stu-id="cb177-109">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="cb177-110">Физический диск (а диск)</span><span class="sxs-lookup"><span data-stu-id="cb177-110">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="cb177-111">Среднее</span><span class="sxs-lookup"><span data-stu-id="cb177-111">Avg.</span></span> <span data-ttu-id="cb177-112">Длина очереди чтения с диска</span><span class="sxs-lookup"><span data-stu-id="cb177-112">Disk Read Queue Length</span></span> |
| <span data-ttu-id="cb177-113">Физический диск (а диск)</span><span class="sxs-lookup"><span data-stu-id="cb177-113">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="cb177-114">Среднее</span><span class="sxs-lookup"><span data-stu-id="cb177-114">Avg.</span></span> <span data-ttu-id="cb177-115">Длина очереди записи на диск</span><span class="sxs-lookup"><span data-stu-id="cb177-115">Disk Write Queue Length</span></span> |
| <span data-ttu-id="cb177-116">Физический диск (а диск)</span><span class="sxs-lookup"><span data-stu-id="cb177-116">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="cb177-117">Среднее</span><span class="sxs-lookup"><span data-stu-id="cb177-117">Avg.</span></span> <span data-ttu-id="cb177-118">время чтения с диска (с)</span><span class="sxs-lookup"><span data-stu-id="cb177-118">Disk sec/Read</span></span> |
| <span data-ttu-id="cb177-119">Физический диск (а диск)</span><span class="sxs-lookup"><span data-stu-id="cb177-119">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="cb177-120">Среднее</span><span class="sxs-lookup"><span data-stu-id="cb177-120">Avg.</span></span> <span data-ttu-id="cb177-121">время записи на диск (с)</span><span class="sxs-lookup"><span data-stu-id="cb177-121">Disk sec/Write</span></span> |
| <span data-ttu-id="cb177-122">Физический диск (а диск)</span><span class="sxs-lookup"><span data-stu-id="cb177-122">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="cb177-123">Операций чтения с диска в секунду </span><span class="sxs-lookup"><span data-stu-id="cb177-123">Disk Reads/sec</span></span> |
| <span data-ttu-id="cb177-124">Физический диск (а диск)</span><span class="sxs-lookup"><span data-stu-id="cb177-124">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="cb177-125">Скорость чтения с диска (байт/с) </span><span class="sxs-lookup"><span data-stu-id="cb177-125">Disk Read Bytes/sec</span></span> |
| <span data-ttu-id="cb177-126">Физический диск (а диск)</span><span class="sxs-lookup"><span data-stu-id="cb177-126">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="cb177-127">Операций записи на диск в секунду</span><span class="sxs-lookup"><span data-stu-id="cb177-127">Disk Writes/sec</span></span> |
| <span data-ttu-id="cb177-128">Физический диск (а диск)</span><span class="sxs-lookup"><span data-stu-id="cb177-128">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="cb177-129">Скорость записи на диск (байт/с)</span><span class="sxs-lookup"><span data-stu-id="cb177-129">Disk Write Bytes/sec</span></span> |
| <span data-ttu-id="cb177-130">Память</span><span class="sxs-lookup"><span data-stu-id="cb177-130">Memory</span></span> | <span data-ttu-id="cb177-131">Доступный объем в МБ</span><span class="sxs-lookup"><span data-stu-id="cb177-131">Available MBytes</span></span> |
| <span data-ttu-id="cb177-132">Файл подкачки</span><span class="sxs-lookup"><span data-stu-id="cb177-132">PagingFile</span></span> | <span data-ttu-id="cb177-133">% использования</span><span class="sxs-lookup"><span data-stu-id="cb177-133">% Usage</span></span> |
| <span data-ttu-id="cb177-134">Обработка (всего)</span><span class="sxs-lookup"><span data-stu-id="cb177-134">Process(Total)</span></span> | <span data-ttu-id="cb177-135">% загруженности процессора</span><span class="sxs-lookup"><span data-stu-id="cb177-135">% Processor Time</span></span> |
| <span data-ttu-id="cb177-136">Обработка (на службу)</span><span class="sxs-lookup"><span data-stu-id="cb177-136">Process (per service)</span></span> | <span data-ttu-id="cb177-137">% загруженности процессора</span><span class="sxs-lookup"><span data-stu-id="cb177-137">% Processor Time</span></span> |
| <span data-ttu-id="cb177-138">Обработка (на службу)</span><span class="sxs-lookup"><span data-stu-id="cb177-138">Process (per service)</span></span> | <span data-ttu-id="cb177-139">Идентификатор процесса</span><span class="sxs-lookup"><span data-stu-id="cb177-139">ID Process</span></span> |
| <span data-ttu-id="cb177-140">Обработка (на службу)</span><span class="sxs-lookup"><span data-stu-id="cb177-140">Process (per service)</span></span> | <span data-ttu-id="cb177-141">Байты исключительного пользования</span><span class="sxs-lookup"><span data-stu-id="cb177-141">Private Bytes</span></span> |
| <span data-ttu-id="cb177-142">Обработка (на службу)</span><span class="sxs-lookup"><span data-stu-id="cb177-142">Process (per service)</span></span> | <span data-ttu-id="cb177-143">Счетчик потоков</span><span class="sxs-lookup"><span data-stu-id="cb177-143">Thread Count</span></span> |
| <span data-ttu-id="cb177-144">Обработка (на службу)</span><span class="sxs-lookup"><span data-stu-id="cb177-144">Process (per service)</span></span> | <span data-ttu-id="cb177-145">Байт виртуальной памяти</span><span class="sxs-lookup"><span data-stu-id="cb177-145">Virtual Bytes</span></span> |
| <span data-ttu-id="cb177-146">Обработка (на службу)</span><span class="sxs-lookup"><span data-stu-id="cb177-146">Process (per service)</span></span> | <span data-ttu-id="cb177-147">Рабочий набор</span><span class="sxs-lookup"><span data-stu-id="cb177-147">Working Set</span></span> |
| <span data-ttu-id="cb177-148">Обработка (на службу)</span><span class="sxs-lookup"><span data-stu-id="cb177-148">Process (per service)</span></span> | <span data-ttu-id="cb177-149">Рабочий набор (частный)</span><span class="sxs-lookup"><span data-stu-id="cb177-149">Working Set - Private</span></span> |

## <a name="net-applications-and-services"></a><span data-ttu-id="cb177-150">Приложения и службы .NET</span><span class="sxs-lookup"><span data-stu-id="cb177-150">.NET applications and services</span></span>

<span data-ttu-id="cb177-151">Собирайте приведенные ниже счетчики, если вы развертываете службы .NET в кластере.</span><span class="sxs-lookup"><span data-stu-id="cb177-151">Collect the following counters if you are deploying .NET services to your cluster.</span></span> 

| <span data-ttu-id="cb177-152">Категория счетчика</span><span class="sxs-lookup"><span data-stu-id="cb177-152">Counter Category</span></span> | <span data-ttu-id="cb177-153">Имя счетчика</span><span class="sxs-lookup"><span data-stu-id="cb177-153">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="cb177-154">Память CLR .NET (на службу)</span><span class="sxs-lookup"><span data-stu-id="cb177-154">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="cb177-155">ИД процесса</span><span class="sxs-lookup"><span data-stu-id="cb177-155">Process ID</span></span> |
| <span data-ttu-id="cb177-156">Память CLR .NET (на службу)</span><span class="sxs-lookup"><span data-stu-id="cb177-156">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="cb177-157">Всего фиксировано байт</span><span class="sxs-lookup"><span data-stu-id="cb177-157"># Total committed Bytes</span></span> |
| <span data-ttu-id="cb177-158">Память CLR .NET (на службу)</span><span class="sxs-lookup"><span data-stu-id="cb177-158">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="cb177-159">Всего зарезервировано байт</span><span class="sxs-lookup"><span data-stu-id="cb177-159"># Total reserved Bytes</span></span> |
| <span data-ttu-id="cb177-160">Память CLR .NET (на службу)</span><span class="sxs-lookup"><span data-stu-id="cb177-160">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="cb177-161">Байт во всех кучах</span><span class="sxs-lookup"><span data-stu-id="cb177-161"># Bytes in all Heaps</span></span> |
| <span data-ttu-id="cb177-162">Память CLR .NET (на службу)</span><span class="sxs-lookup"><span data-stu-id="cb177-162">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="cb177-163">Сборов мусора для поколения 0</span><span class="sxs-lookup"><span data-stu-id="cb177-163"># Gen 0 Collections</span></span> |
| <span data-ttu-id="cb177-164">Память CLR .NET (на службу)</span><span class="sxs-lookup"><span data-stu-id="cb177-164">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="cb177-165">Сборов мусора для поколения 1</span><span class="sxs-lookup"><span data-stu-id="cb177-165"># Gen 1 Collections</span></span> |
| <span data-ttu-id="cb177-166">Память CLR .NET (на службу)</span><span class="sxs-lookup"><span data-stu-id="cb177-166">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="cb177-167">Сборов мусора для поколения 2</span><span class="sxs-lookup"><span data-stu-id="cb177-167"># Gen 2 Collections</span></span> |
| <span data-ttu-id="cb177-168">Память CLR .NET (на службу)</span><span class="sxs-lookup"><span data-stu-id="cb177-168">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="cb177-169">Время на сборку мусора, %</span><span class="sxs-lookup"><span data-stu-id="cb177-169">% Time in GC</span></span> |

### <a name="service-fabrics-custom-performance-counters"></a><span data-ttu-id="cb177-170">Настраиваемые счетчики производительности Service Fabric</span><span class="sxs-lookup"><span data-stu-id="cb177-170">Service Fabric's custom performance counters</span></span>

<span data-ttu-id="cb177-171">Service Fabric создает достаточное число настраиваемых счетчиков производительности.</span><span class="sxs-lookup"><span data-stu-id="cb177-171">Service Fabric generates a substantial amount of custom performance counters.</span></span> <span data-ttu-id="cb177-172">Если у вас установлен пакет SDK, то полный список счетчиков можно просмотреть на компьютере Windows в приложении системного монитора ("Пуск" > "Системный монитор").</span><span class="sxs-lookup"><span data-stu-id="cb177-172">If you have the SDK installed, you can see the comprehensive list on your Windows machine in your Performance Monitor application (Start > Performance Monitor).</span></span> 

<span data-ttu-id="cb177-173">Если используется Reliable Actors, то для приложений, которые вы развертываете в кластере, добавьте счетчики из категорий `Service Fabric Actor` и `Service Fabric Actor Method` (см. раздел [Диагностика и мониторинг производительности в Reliable Actors](service-fabric-reliable-actors-diagnostics.md)).</span><span class="sxs-lookup"><span data-stu-id="cb177-173">In the applications you are deploying to your cluster, if you are using Reliable Actors, add countes from `Service Fabric Actor` and `Service Fabric Actor Method` categories (see [Service Fabric Reliable Actors Diagnostics](service-fabric-reliable-actors-diagnostics.md)).</span></span>

<span data-ttu-id="cb177-174">Для Reliable Services имеются аналогичные категории счетчиков `Service Fabric Service` и `Service Fabric Service Method`, данные которых следует собирать.</span><span class="sxs-lookup"><span data-stu-id="cb177-174">If you use Reliable Services, we similarly have `Service Fabric Service` and `Service Fabric Service Method` counter categories that you should collect counters from.</span></span> 

<span data-ttu-id="cb177-175">При использовании Reliable Collections рекомендуется добавить `Avg. Transaction ms/Commit` из `Service Fabric Transactional Replicator` для сбора метрики средней задержки при фиксации транзакции.</span><span class="sxs-lookup"><span data-stu-id="cb177-175">If you use Reliable Collections, we recommend adding the `Avg. Transaction ms/Commit` from the `Service Fabric Transactional Replicator` to collect the average commit latency per transaction metric.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cb177-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cb177-176">Next steps</span></span>

* <span data-ttu-id="cb177-177">Узнайте больше о [создании событий на уровне платформы](service-fabric-diagnostics-event-generation-infra.md) в Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cb177-177">Learn more about [event generation at the platform level](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span></span>
* <span data-ttu-id="cb177-178">Собирайте метрики производительности с помощью [системы диагностики Azure](service-fabric-diagnostics-event-aggregation-wad.md).</span><span class="sxs-lookup"><span data-stu-id="cb177-178">Collect performance metrics through [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span></span>
