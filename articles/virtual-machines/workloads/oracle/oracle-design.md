---
title: "Разработка базы данных Oracle и ее реализация в Azure | Документация Майкрософт"
description: "Разработка базы данных Oracle и ее реализация в среду Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/22/2017
ms.author: rclaus
ms.openlocfilehash: 1af7e1d40a0eb129875dd6a30ac899f2025bee13
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="design-and-implement-an-oracle-database-in-azure"></a><span data-ttu-id="73fd9-103">Разработка базы данных Oracle и ее реализация в Azure</span><span class="sxs-lookup"><span data-stu-id="73fd9-103">Design and implement an Oracle database in Azure</span></span>

## <a name="assumptions"></a><span data-ttu-id="73fd9-104">Предположения</span><span class="sxs-lookup"><span data-stu-id="73fd9-104">Assumptions</span></span>

- <span data-ttu-id="73fd9-105">Вы планируете перенести базу данных Oracle из локальной среды в Azure.</span><span class="sxs-lookup"><span data-stu-id="73fd9-105">You're planning to migrate an Oracle database from on-premises to Azure.</span></span>
- <span data-ttu-id="73fd9-106">У вас есть представление о разных метриках, используемых в отчетах Oracle AWR.</span><span class="sxs-lookup"><span data-stu-id="73fd9-106">You have an understanding of the various metrics in Oracle AWR reports.</span></span>
- <span data-ttu-id="73fd9-107">У вас есть базовое представление о производительности приложения и использовании платформы.</span><span class="sxs-lookup"><span data-stu-id="73fd9-107">You have a baseline understanding of application performance and platform utilization.</span></span>

## <a name="goals"></a><span data-ttu-id="73fd9-108">Цели</span><span class="sxs-lookup"><span data-stu-id="73fd9-108">Goals</span></span>

- <span data-ttu-id="73fd9-109">Получить сведения о том, как оптимизировать развертывание Oracle в Azure.</span><span class="sxs-lookup"><span data-stu-id="73fd9-109">Understand how to optimize your Oracle deployment in Azure.</span></span>
- <span data-ttu-id="73fd9-110">Изучить параметры настройки производительности для базы данных Oracle в среде Azure.</span><span class="sxs-lookup"><span data-stu-id="73fd9-110">Explore performance tuning options for an Oracle database in an Azure environment.</span></span>

## <a name="the-differences-between-an-on-premises-and-azure-implementation"></a><span data-ttu-id="73fd9-111">Различия между реализацией в локальной среде и среде Azure</span><span class="sxs-lookup"><span data-stu-id="73fd9-111">The differences between an on-premises and Azure implementation</span></span> 

<span data-ttu-id="73fd9-112">Ниже перечислены важные факторы, которые следует учитывать при миграции локальных приложений в Azure.</span><span class="sxs-lookup"><span data-stu-id="73fd9-112">Following are some important things to keep in mind when you're migrating on-premises applications to Azure.</span></span> 

<span data-ttu-id="73fd9-113">Важным отличием является то, что при реализации в Azure ресурсы (например, виртуальные машины, диски и виртуальные сети) можно совместно использовать с другими клиентами.</span><span class="sxs-lookup"><span data-stu-id="73fd9-113">One important difference is that in an Azure implementation, resources such as VMs, disks, and virtual networks are shared among other clients.</span></span> <span data-ttu-id="73fd9-114">Кроме того, ресурс можно регулировать в соответствии с требованиями.</span><span class="sxs-lookup"><span data-stu-id="73fd9-114">In addition, resources can be throttled based on the requirements.</span></span> <span data-ttu-id="73fd9-115">В Azure все нацелено не столько на предотвращение сбоев (MTBF), сколько на восстановление после них (MTTR).</span><span class="sxs-lookup"><span data-stu-id="73fd9-115">Instead of focusing on avoiding failing (MTBF), Azure is more focused on surviving the failure (MTTR).</span></span>

<span data-ttu-id="73fd9-116">В таблице ниже перечислены некоторые различия между реализацией базы данных Oracle в локальной среде и среде Azure.</span><span class="sxs-lookup"><span data-stu-id="73fd9-116">The following table lists some of the differences between an on-premises implementation and an Azure implementation of an Oracle database.</span></span>

> 
> |  | <span data-ttu-id="73fd9-117">**Реализация в локальной среде**</span><span class="sxs-lookup"><span data-stu-id="73fd9-117">**On-premises implementation**</span></span> | <span data-ttu-id="73fd9-118">**Реализация в Azure**</span><span class="sxs-lookup"><span data-stu-id="73fd9-118">**Azure implementation**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="73fd9-119">**Сеть**</span><span class="sxs-lookup"><span data-stu-id="73fd9-119">**Networking**</span></span> |<span data-ttu-id="73fd9-120">Локальная или глобальная сеть</span><span class="sxs-lookup"><span data-stu-id="73fd9-120">LAN/WAN</span></span>  |<span data-ttu-id="73fd9-121">SDN (программно-конфигурируемая сеть)</span><span class="sxs-lookup"><span data-stu-id="73fd9-121">SDN (software-defined networking)</span></span>|
> | <span data-ttu-id="73fd9-122">**Группа безопасности**</span><span class="sxs-lookup"><span data-stu-id="73fd9-122">**Security group**</span></span> |<span data-ttu-id="73fd9-123">Средства ограничения портов и IP-адресов</span><span class="sxs-lookup"><span data-stu-id="73fd9-123">IP/port restriction tools</span></span> |[<span data-ttu-id="73fd9-124">Группа безопасности сети</span><span class="sxs-lookup"><span data-stu-id="73fd9-124">Network Security Group (NSG)</span></span>](https://azure.microsoft.com/blog/network-security-groups) |
> | <span data-ttu-id="73fd9-125">**Устойчивость**</span><span class="sxs-lookup"><span data-stu-id="73fd9-125">**Resilience**</span></span> |<span data-ttu-id="73fd9-126">MTBF (среднее время безотказной работы)</span><span class="sxs-lookup"><span data-stu-id="73fd9-126">MTBF (mean time between failures)</span></span> |<span data-ttu-id="73fd9-127">MTTR (среднее время восстановления)</span><span class="sxs-lookup"><span data-stu-id="73fd9-127">MTTR (mean time to recovery)</span></span>|
> | <span data-ttu-id="73fd9-128">**Плановое техническое обслуживание**</span><span class="sxs-lookup"><span data-stu-id="73fd9-128">**Planned maintenance**</span></span> |<span data-ttu-id="73fd9-129">Установка исправлений и обновлений</span><span class="sxs-lookup"><span data-stu-id="73fd9-129">Patching/upgrades</span></span>|<span data-ttu-id="73fd9-130">[Группы доступности](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (установка исправлений и обновлений, управляемая Azure)</span><span class="sxs-lookup"><span data-stu-id="73fd9-130">[Availability sets](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) (patching/upgrades managed by Azure)</span></span> |
> | <span data-ttu-id="73fd9-131">**Ресурс**</span><span class="sxs-lookup"><span data-stu-id="73fd9-131">**Resource**</span></span> |<span data-ttu-id="73fd9-132">Выделенные</span><span class="sxs-lookup"><span data-stu-id="73fd9-132">Dedicated</span></span>  |<span data-ttu-id="73fd9-133">Совместное использование с другими клиентами</span><span class="sxs-lookup"><span data-stu-id="73fd9-133">Shared with other clients</span></span>|
> | <span data-ttu-id="73fd9-134">**Регионы**</span><span class="sxs-lookup"><span data-stu-id="73fd9-134">**Regions**</span></span> |<span data-ttu-id="73fd9-135">Центры обработки данных</span><span class="sxs-lookup"><span data-stu-id="73fd9-135">Datacenters</span></span> |[<span data-ttu-id="73fd9-136">Пары регионов</span><span class="sxs-lookup"><span data-stu-id="73fd9-136">Region pairs</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability)|
> | <span data-ttu-id="73fd9-137">**Хранилище**</span><span class="sxs-lookup"><span data-stu-id="73fd9-137">**Storage**</span></span> |<span data-ttu-id="73fd9-138">Сеть SAN и физические диски</span><span class="sxs-lookup"><span data-stu-id="73fd9-138">SAN/physical disks</span></span> |[<span data-ttu-id="73fd9-139">Хранилище под управлением Azure</span><span class="sxs-lookup"><span data-stu-id="73fd9-139">Azure-managed storage</span></span>](https://azure.microsoft.com/pricing/details/managed-disks/?v=17.23h)|
> | <span data-ttu-id="73fd9-140">**Масштабирование**</span><span class="sxs-lookup"><span data-stu-id="73fd9-140">**Scale**</span></span> |<span data-ttu-id="73fd9-141">Вертикальное масштабирование</span><span class="sxs-lookup"><span data-stu-id="73fd9-141">Vertical scale</span></span> |<span data-ttu-id="73fd9-142">Горизонтальное масштабирование</span><span class="sxs-lookup"><span data-stu-id="73fd9-142">Horizontal scale</span></span>|


### <a name="requirements"></a><span data-ttu-id="73fd9-143">Требования</span><span class="sxs-lookup"><span data-stu-id="73fd9-143">Requirements</span></span>

- <span data-ttu-id="73fd9-144">Определите скорость увеличения и размер базы данных.</span><span class="sxs-lookup"><span data-stu-id="73fd9-144">Determine the database size and growth rate.</span></span>
- <span data-ttu-id="73fd9-145">Определите требования к числу операций ввода-вывода, которое можно рассчитать на основе отчета Oracle AWR или других средств мониторинга сети.</span><span class="sxs-lookup"><span data-stu-id="73fd9-145">Determine the IOPS requirements, which you can estimate based on Oracle AWR reports or other network monitoring tools.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="73fd9-146">Варианты настройки</span><span class="sxs-lookup"><span data-stu-id="73fd9-146">Configuration options</span></span>

<span data-ttu-id="73fd9-147">В среде Azure есть четыре области, которые можно настроить для повышения производительности:</span><span class="sxs-lookup"><span data-stu-id="73fd9-147">There are four potential areas that you can tune to improve performance in an Azure environment:</span></span>

- <span data-ttu-id="73fd9-148">размер виртуальной машины;</span><span class="sxs-lookup"><span data-stu-id="73fd9-148">Virtual machine size</span></span>
- <span data-ttu-id="73fd9-149">Пропускная способность сети</span><span class="sxs-lookup"><span data-stu-id="73fd9-149">Network throughput</span></span>
- <span data-ttu-id="73fd9-150">Типы дисков и их конфигурации</span><span class="sxs-lookup"><span data-stu-id="73fd9-150">Disk types and configurations</span></span>
- <span data-ttu-id="73fd9-151">Настройки кэша дисков.</span><span class="sxs-lookup"><span data-stu-id="73fd9-151">Disk cache settings</span></span>

### <a name="generate-an-awr-report"></a><span data-ttu-id="73fd9-152">Создание отчета AWR</span><span class="sxs-lookup"><span data-stu-id="73fd9-152">Generate an AWR report</span></span>

<span data-ttu-id="73fd9-153">Если у вас уже есть база данных Oracle и вы планируете перенести ее в Azure, это можно сделать несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="73fd9-153">If you have an existing an Oracle database and are planning to migrate to Azure, you have several options.</span></span> <span data-ttu-id="73fd9-154">Запустите отчет Oracle AWR, чтобы получить метрики (операции ввода-вывода, Мбит/с, ГБ и т. д.).</span><span class="sxs-lookup"><span data-stu-id="73fd9-154">You can run the Oracle AWR report to get the metrics (IOPS, Mbps, GiBs, and so on).</span></span> <span data-ttu-id="73fd9-155">Затем выберите виртуальную машину на основе собранных метрик.</span><span class="sxs-lookup"><span data-stu-id="73fd9-155">Then choose the VM based on the metrics that you collected.</span></span> <span data-ttu-id="73fd9-156">Также можно обратиться в группу обслуживания инфраструктуры, чтобы получить аналогичные сведения.</span><span class="sxs-lookup"><span data-stu-id="73fd9-156">Or you can contact your infrastructure team to get similar information.</span></span>

<span data-ttu-id="73fd9-157">Вы можете запустить отчет AWR во время обычной и пиковой рабочей нагрузки, чтобы сравнить результаты.</span><span class="sxs-lookup"><span data-stu-id="73fd9-157">You might consider running your AWR report during both regular and peak workloads, so you can compare.</span></span> <span data-ttu-id="73fd9-158">С помощью этих отчетов можно настроить размер виртуальных машин на основе данных средней или максимальной рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="73fd9-158">Based on these reports, you can size the VMs based on either the average workload or the maximum workload.</span></span>

<span data-ttu-id="73fd9-159">Ниже приведен пример того, как создать отчет AWR:</span><span class="sxs-lookup"><span data-stu-id="73fd9-159">Following is an example of how to generate an AWR report:</span></span>

```bash
$ sqlplus / as sysdba
SQL> EXEC DBMS_WORKLOAD_REPOSITORY.CREATE_SNAPSHOT;
SQL> @?/rdbms/admin/awrrpt.sql
```

### <a name="key-metrics"></a><span data-ttu-id="73fd9-160">Ключевые метрики</span><span class="sxs-lookup"><span data-stu-id="73fd9-160">Key metrics</span></span>

<span data-ttu-id="73fd9-161">Ниже перечислены метрики, которые можно получить из отчета:</span><span class="sxs-lookup"><span data-stu-id="73fd9-161">Following are the metrics that you can obtain from the AWR report:</span></span>

- <span data-ttu-id="73fd9-162">общее число ядер;</span><span class="sxs-lookup"><span data-stu-id="73fd9-162">Total number of cores</span></span>
- <span data-ttu-id="73fd9-163">тактовая частота процессора;</span><span class="sxs-lookup"><span data-stu-id="73fd9-163">CPU clock speed</span></span>
- <span data-ttu-id="73fd9-164">общий объем памяти в ГБ;</span><span class="sxs-lookup"><span data-stu-id="73fd9-164">Total memory in GB</span></span>
- <span data-ttu-id="73fd9-165">загрузка ЦП;</span><span class="sxs-lookup"><span data-stu-id="73fd9-165">CPU utilization</span></span>
- <span data-ttu-id="73fd9-166">пиковая частота передачи данных;</span><span class="sxs-lookup"><span data-stu-id="73fd9-166">Peak data transfer rate</span></span>
- <span data-ttu-id="73fd9-167">частота изменения числа операций ввода-вывода (чтение и запись);</span><span class="sxs-lookup"><span data-stu-id="73fd9-167">Rate of I/O changes (read/write)</span></span>
- <span data-ttu-id="73fd9-168">скорость записи в журнал повторяемых операций (Мбит/с);</span><span class="sxs-lookup"><span data-stu-id="73fd9-168">Redo log rate (MBPs)</span></span>
- <span data-ttu-id="73fd9-169">Пропускная способность сети</span><span class="sxs-lookup"><span data-stu-id="73fd9-169">Network throughput</span></span>
- <span data-ttu-id="73fd9-170">показатель задержек сети (низкий и высокий уровень);</span><span class="sxs-lookup"><span data-stu-id="73fd9-170">Network latency rate (low/high)</span></span>
- <span data-ttu-id="73fd9-171">размер базы данных (в ГБ);</span><span class="sxs-lookup"><span data-stu-id="73fd9-171">Database size in GB</span></span>
- <span data-ttu-id="73fd9-172">число байт, полученных через SQL*Net из клиента и поступивших него.</span><span class="sxs-lookup"><span data-stu-id="73fd9-172">Bytes received via SQL*Net from/to client</span></span>

### <a name="virtual-machine-size"></a><span data-ttu-id="73fd9-173">размер виртуальной машины;</span><span class="sxs-lookup"><span data-stu-id="73fd9-173">Virtual machine size</span></span>

#### <a name="1-estimate-vm-size-based-on-cpu-memory-and-io-usage-from-the-awr-report"></a><span data-ttu-id="73fd9-174">1. Оценка необходимого размера виртуальных машин на основе использования ЦП, памяти или операций ввода-вывода из отчета AWR</span><span class="sxs-lookup"><span data-stu-id="73fd9-174">1. Estimate VM size based on CPU, memory, and I/O usage from the AWR report</span></span>

<span data-ttu-id="73fd9-175">Обратите внимание на пять первых событий переднего плана с наибольшим временем ожидания, которые указывают на проблемные места системы.</span><span class="sxs-lookup"><span data-stu-id="73fd9-175">One thing you might look at is the top five timed foreground events that indicate where the system bottlenecks are.</span></span>

<span data-ttu-id="73fd9-176">Например, в верхней строке представленной ниже схемы приведены данные синхронизации для файла журнала.</span><span class="sxs-lookup"><span data-stu-id="73fd9-176">For example, in the following diagram, the log file sync is at the top.</span></span> <span data-ttu-id="73fd9-177">В строке указано число периодов ожидания перед тем, как LGWR записывает содержимое буфера журнала в файл журнала повторяемых операций.</span><span class="sxs-lookup"><span data-stu-id="73fd9-177">It indicates the number of waits that are required before the LGWR writes the log buffer to the redo log file.</span></span> <span data-ttu-id="73fd9-178">Эти результаты указывают на то, что требуются более производительные диски или хранилище.</span><span class="sxs-lookup"><span data-stu-id="73fd9-178">These results indicate that better performing storage or disks are required.</span></span> <span data-ttu-id="73fd9-179">Кроме того, на схеме указано объем ЦП (число ядер) и объем памяти.</span><span class="sxs-lookup"><span data-stu-id="73fd9-179">In addition, the diagram also shows the number of CPU (cores) and the amount of memory.</span></span>

![Снимок экрана страницы отчета AWR](./media/oracle-design/cpu_memory_info.png)

<span data-ttu-id="73fd9-181">На следующей схеме представлены общие показатели операций ввода-вывода для чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="73fd9-181">The following diagram shows the total I/O of read and write.</span></span> <span data-ttu-id="73fd9-182">На момент создания отчета для операций чтения зафиксирован показатель 59 ГБ, а для операций записи — 247,3 ГБ.</span><span class="sxs-lookup"><span data-stu-id="73fd9-182">There were 59 GB read and 247.3 GB written during the time of the report.</span></span>

![Снимок экрана страницы отчета AWR](./media/oracle-design/io_info.png)

#### <a name="2-choose-a-vm"></a><span data-ttu-id="73fd9-184">2. Выбор виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="73fd9-184">2. Choose a VM</span></span>

<span data-ttu-id="73fd9-185">Далее на основе данных из отчета AWR следует выбрать размер виртуальной машины, который соответствует вашим требованиям.</span><span class="sxs-lookup"><span data-stu-id="73fd9-185">Based on the information that you collected from the AWR report, the next step is to choose a VM of a similar size that meets your requirements.</span></span> <span data-ttu-id="73fd9-186">Список доступных виртуальных машин см. в статье об [оптимизации для памяти](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span><span class="sxs-lookup"><span data-stu-id="73fd9-186">You can find a list of available VMs in the article [Memory optimized](https://docs.microsoft.com/azure/virtual-machinFine tune es/virtual-machines-windows-sizes-memory).</span></span>

#### <a name="3-fine-tune-the-vm-sizing-with-a-similar-vm-series-based-on-the-acu"></a><span data-ttu-id="73fd9-187">3. Выбор размера виртуальных машин аналогичной серии на основе ACU</span><span class="sxs-lookup"><span data-stu-id="73fd9-187">3. Fine-tune the VM sizing with a similar VM series based on the ACU</span></span>

<span data-ttu-id="73fd9-188">Выбрав виртуальные машины, обратите внимание на связанные единицы вычислений Azure (ACU).</span><span class="sxs-lookup"><span data-stu-id="73fd9-188">After you've chosen the VM, pay attention to the ACU for the VM.</span></span> <span data-ttu-id="73fd9-189">Можно выбрать разные виртуальные машины на основе значения ACU, которое соответствует вашим требованиям.</span><span class="sxs-lookup"><span data-stu-id="73fd9-189">You might choose a different VM based on the ACU value that better suits your requirements.</span></span> <span data-ttu-id="73fd9-190">Дополнительные сведения см. в статье [Единицы вычислений Azure (ACU)](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span><span class="sxs-lookup"><span data-stu-id="73fd9-190">For more information, see [Azure compute unit](https://docs.microsoft.com/azure/virtual-machines/windows/acu).</span></span>

![Снимок экрана со страницей единиц ACU](./media/oracle-design/acu_units.png)

### <a name="network-throughput"></a><span data-ttu-id="73fd9-192">Пропускная способность сети</span><span class="sxs-lookup"><span data-stu-id="73fd9-192">Network throughput</span></span>

<span data-ttu-id="73fd9-193">На следующей схеме показана связь между пропускной способностью и числом операций ввода-вывода в секунду:</span><span class="sxs-lookup"><span data-stu-id="73fd9-193">The following diagram shows the relation between throughput and IOPS:</span></span>

![Снимок экрана с показателями пропускной способности](./media/oracle-design/throughput.png)

<span data-ttu-id="73fd9-195">Общая пропускная способность сети зависит от следующих показателей:</span><span class="sxs-lookup"><span data-stu-id="73fd9-195">The total network throughput is estimated based on the following information:</span></span>
- <span data-ttu-id="73fd9-196">объем трафика SQL*Net;</span><span class="sxs-lookup"><span data-stu-id="73fd9-196">SQL*Net traffic</span></span>
- <span data-ttu-id="73fd9-197">Мбит/с x число серверов (исходящий поток, например Oracle Data Guard);</span><span class="sxs-lookup"><span data-stu-id="73fd9-197">MBps x number of servers (outbound stream such as Oracle Data Guard)</span></span>
- <span data-ttu-id="73fd9-198">другие факторы, такие как репликация приложений.</span><span class="sxs-lookup"><span data-stu-id="73fd9-198">Other factors, such as application replication</span></span>

![Снимок экрана пропускной способности SQL*Net](./media/oracle-design/sqlnet_info.png)

<span data-ttu-id="73fd9-200">С учетом требований к пропускной способности сети можно выбрать разные типы шлюзов.</span><span class="sxs-lookup"><span data-stu-id="73fd9-200">Based on your network bandwidth requirements, there are various gateway types for you to choose from.</span></span> <span data-ttu-id="73fd9-201">К ним относятся шлюзы категории "Базовый", VpnGw и Azure ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="73fd9-201">These include basic, VpnGw, and Azure ExpressRoute.</span></span> <span data-ttu-id="73fd9-202">Дополнительные сведения см. на странице с [ценами на VPN-шлюзы](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span><span class="sxs-lookup"><span data-stu-id="73fd9-202">For more information, see the [VPN gateway pricing page](https://azure.microsoft.com/en-us/pricing/details/vpn-gateway/?v=17.23h).</span></span>

<span data-ttu-id="73fd9-203">**рекомендации**;</span><span class="sxs-lookup"><span data-stu-id="73fd9-203">**Recommendations**</span></span>

- <span data-ttu-id="73fd9-204">Задержка в сети выше, чем в локальном развертывании.</span><span class="sxs-lookup"><span data-stu-id="73fd9-204">Network latency is higher compared to an on-premises deployment.</span></span> <span data-ttu-id="73fd9-205">Сокращение круговых путей по сети существенно влияет на производительность.</span><span class="sxs-lookup"><span data-stu-id="73fd9-205">Reducing network round trips can greatly improve performance.</span></span>
- <span data-ttu-id="73fd9-206">Консолидируйте приложения с высоким числом транзакций или активные приложения в пределах одной виртуальной машины, чтобы снизить число круговых путей.</span><span class="sxs-lookup"><span data-stu-id="73fd9-206">To reduce round-trips, consolidate applications that have high transactions or “chatty” apps on the same virtual machine.</span></span>

### <a name="disk-types-and-configurations"></a><span data-ttu-id="73fd9-207">Типы дисков и их конфигурации</span><span class="sxs-lookup"><span data-stu-id="73fd9-207">Disk types and configurations</span></span>

- <span data-ttu-id="73fd9-208">*Диски ОС по умолчанию.* Диски этого типа обеспечивают хранение постоянных данных и кэширование.</span><span class="sxs-lookup"><span data-stu-id="73fd9-208">*Default OS disks*: These disk types offer persistent data and caching.</span></span> <span data-ttu-id="73fd9-209">Они оптимизированы для доступа к ОС при запуске и не предназначены для транзакционных рабочих нагрузок или рабочих нагрузок хранилищ данных (аналитических нагрузок).</span><span class="sxs-lookup"><span data-stu-id="73fd9-209">They are optimized for OS access at startup, and aren't designed for either transactional or data warehouse (analytical) workloads.</span></span>

- <span data-ttu-id="73fd9-210">*Неуправляемые диски.* Диски этого типа позволяют управлять учетными записями хранения, используемыми для хранения VHD-файлов, которые соответствуют дискам виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="73fd9-210">*Unmanaged disks*: With these disk types, you manage the storage accounts that store the virtual hard disk (VHD) files that correspond to your VM disks.</span></span> <span data-ttu-id="73fd9-211">VHD-файлы хранятся в учетных записях хранения Azure как страничные BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="73fd9-211">VHD files are stored as page blobs in Azure storage accounts.</span></span>

- <span data-ttu-id="73fd9-212">*Управляемые диски.* Управлять учетными записями хранения, используемыми для дисков виртуальной машины, будет Azure.</span><span class="sxs-lookup"><span data-stu-id="73fd9-212">*Managed disks*: Azure manages the storage accounts that you use for your VM disks.</span></span> <span data-ttu-id="73fd9-213">Вы просто выбираете категорию (Premium или Standard) и размер диска.</span><span class="sxs-lookup"><span data-stu-id="73fd9-213">You specify the disk type (premium or standard) and the size of the disk that you need.</span></span> <span data-ttu-id="73fd9-214">Azure самостоятельно создаст диск и будет управлять им.</span><span class="sxs-lookup"><span data-stu-id="73fd9-214">Azure creates and manages the disk for you.</span></span>

- <span data-ttu-id="73fd9-215">*Диски хранилища класса Premium.* Диски этого типа лучше всего подходят для производственных рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="73fd9-215">*Premium storage disks*: These disk types are best suited for production workloads.</span></span> <span data-ttu-id="73fd9-216">Хранилище класса Premium поддерживает диски, которые можно подключить к виртуальным машинам определенных серий, включая DS, DSv2, GS и F.</span><span class="sxs-lookup"><span data-stu-id="73fd9-216">Premium storage supports VM disks that can be attached to specific size-series VMs, such as DS, DSv2, GS, and F series VMs.</span></span> <span data-ttu-id="73fd9-217">Размер диска класса Premium можно выбрать в диапазоне от 32 до 4096 ГБ.</span><span class="sxs-lookup"><span data-stu-id="73fd9-217">The premium disk comes with different sizes, and you can choose between disks ranging from 32 GB to 4,096 GB.</span></span> <span data-ttu-id="73fd9-218">Каждый из них имеет свои собственные характеристики производительности.</span><span class="sxs-lookup"><span data-stu-id="73fd9-218">Each disk size has its own performance specifications.</span></span> <span data-ttu-id="73fd9-219">В зависимости от потребностей приложения вы можете подключить один или несколько этих дисков к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="73fd9-219">Depending on your application requirements, you can attach one or more disks to your VM.</span></span>

<span data-ttu-id="73fd9-220">Создавая управляемый диск на портале, вы можете выбрать **тип учетной записи** для диска, который хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="73fd9-220">When you create a new managed disk from the portal, you can choose the **Account type** for the type of disk you want to use.</span></span> <span data-ttu-id="73fd9-221">Помните, что в раскрывающемся меню отображаются не все доступные диски.</span><span class="sxs-lookup"><span data-stu-id="73fd9-221">Keep in mind that not all available disks are shown in the drop-down menu.</span></span> <span data-ttu-id="73fd9-222">Когда вы выберете определенный размер виртуальной машины, в меню отобразятся только доступные номера SKU для хранилища класса Premium с учетом этого размера.</span><span class="sxs-lookup"><span data-stu-id="73fd9-222">After you choose a particular VM size, the menu shows only the available premium storage SKUs that are based on that VM size.</span></span>

![Снимок экрана страницы управляемых дисков](./media/oracle-design/premium_disk01.png)

<span data-ttu-id="73fd9-224">Дополнительные сведения см. в статье [High-performance Premium Storage and managed disks for VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage) (Высокопроизводительное хранилище класса Premium и управляемые диски для виртуальных машин).</span><span class="sxs-lookup"><span data-stu-id="73fd9-224">For more information, see [High-performance Premium Storage and managed disks for VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span></span>

<span data-ttu-id="73fd9-225">Настроив хранилище на виртуальной машине, вы можете выполнить нагрузочный тест дисков перед созданием базы данных.</span><span class="sxs-lookup"><span data-stu-id="73fd9-225">After you configure your storage on a VM, you might want to load test the disks before creating a database.</span></span> <span data-ttu-id="73fd9-226">Зная частоту операций ввода-вывода в контексте задержки и пропускной способности, вы сможете определить, поддерживает ли виртуальная машина ожидаемую пропускную способность с целевыми показателями задержки.</span><span class="sxs-lookup"><span data-stu-id="73fd9-226">Knowing the I/O rate in terms of both latency and throughput can help you determine if the VMs support the expected throughput with latency targets.</span></span>

<span data-ttu-id="73fd9-227">Есть несколько средств для нагрузочного тестирования приложения, например Oracle Orion, Sysbench и Fio.</span><span class="sxs-lookup"><span data-stu-id="73fd9-227">There are a number of tools for application load testing, such as Oracle Orion, Sysbench, and Fio.</span></span>

<span data-ttu-id="73fd9-228">Повторно запустите нагрузочный тест после развертывания базы данных Oracle.</span><span class="sxs-lookup"><span data-stu-id="73fd9-228">Run the load test again after you've deployed an Oracle database.</span></span> <span data-ttu-id="73fd9-229">Запустите обычные и пиковые рабочие нагрузки. В результатах отразятся основные показатели вашей среды.</span><span class="sxs-lookup"><span data-stu-id="73fd9-229">Start your regular and peak workloads, and the results show you the baseline of your environment.</span></span>

<span data-ttu-id="73fd9-230">Возможно, целесообразнее будет выбрать размер хранилища на основе частоты операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="73fd9-230">It might be more important to size the storage based on the IOPS rate rather than the storage size.</span></span> <span data-ttu-id="73fd9-231">Например, если требуемый показатель для операций ввода-вывода составляет 5000 ГБ, но вам нужно только 200 ГБ, вы по-прежнему можете использовать диск P30 класса Premium, хоть он и обеспечивает хранилище объемом более 200 ГБ.</span><span class="sxs-lookup"><span data-stu-id="73fd9-231">For example, if the required IOPS is 5,000, but you only need 200 GB, you might still get the P30 class premium disk even though it comes with more than 200 GB of storage.</span></span>

<span data-ttu-id="73fd9-232">Из отчета AWR можно узнать скорость операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="73fd9-232">The IOPS rate can be obtained from the AWR report.</span></span> <span data-ttu-id="73fd9-233">Она определяется журналом повторяемых операций, показателем физических операций чтения и скоростью операций записи.</span><span class="sxs-lookup"><span data-stu-id="73fd9-233">It's determined by the redo log, physical reads, and writes rate.</span></span>

![Снимок экрана страницы отчета AWR](./media/oracle-design/awr_report.png)

<span data-ttu-id="73fd9-235">Например, скорость повторяемых операций составляет 12,200,000 байт в секунду, что равно 11,63 Мбит/с.</span><span class="sxs-lookup"><span data-stu-id="73fd9-235">For example, the redo size is 12,200,000 bytes per second, which is equal to 11.63 MBPs.</span></span>
<span data-ttu-id="73fd9-236">Число операций ввода-вывода в секунду: 12 200 000 / 2358 = 5174.</span><span class="sxs-lookup"><span data-stu-id="73fd9-236">The IOPS is 12,200,000 / 2,358 = 5,174.</span></span>

<span data-ttu-id="73fd9-237">Получив четкое представление о требованиях к скорости операций ввода-вывода, можно выбрать оптимальное сочетание дисков.</span><span class="sxs-lookup"><span data-stu-id="73fd9-237">After you have a clear picture of the I/O requirements, you can choose a combination of drives that are best suited to meet those requirements.</span></span>

<span data-ttu-id="73fd9-238">**рекомендации**;</span><span class="sxs-lookup"><span data-stu-id="73fd9-238">**Recommendations**</span></span>

- <span data-ttu-id="73fd9-239">Для табличного пространства данных распределите рабочую нагрузку операций ввода-вывода между несколькими дисками с помощью управляемого хранилища или Oracle ASM.</span><span class="sxs-lookup"><span data-stu-id="73fd9-239">For data tablespace, spread the I/O workload across a number of disks by using managed storage or Oracle ASM.</span></span>
- <span data-ttu-id="73fd9-240">Добавляйте дополнительные диски данных по мере увеличения размера блока ввода-вывода для интенсивных операций чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="73fd9-240">As the I/O block size increases for read-intensive and write-intensive operations, add more data disks.</span></span>
- <span data-ttu-id="73fd9-241">Увеличьте размер блока для масштабных последовательных процессов.</span><span class="sxs-lookup"><span data-stu-id="73fd9-241">Increase the block size for large sequential processes.</span></span>
- <span data-ttu-id="73fd9-242">Используйте сжатие данных для сокращения числа операций ввода-вывода (для данных и индексов).</span><span class="sxs-lookup"><span data-stu-id="73fd9-242">Use data compression to reduce I/O (for both data and indexes).</span></span>
- <span data-ttu-id="73fd9-243">Используйте отдельные диски данных для журналов повторяемых операций, а также табличного пространства system, temp и undo.</span><span class="sxs-lookup"><span data-stu-id="73fd9-243">Separate redo logs, system, and temps, and undo TS on separate data disks.</span></span>
- <span data-ttu-id="73fd9-244">Не размещайте файлы приложений на дисках операционной системы по умолчанию (/dev/sda).</span><span class="sxs-lookup"><span data-stu-id="73fd9-244">Don't put any application files on default OS disks (/dev/sda).</span></span> <span data-ttu-id="73fd9-245">Эти диски не оптимизированы для быстрой загрузки виртуальной машины и не могут обеспечить высокую производительность приложений.</span><span class="sxs-lookup"><span data-stu-id="73fd9-245">These disks aren't optimized for fast VM boot times, and they might not provide good performance for your application.</span></span>

### <a name="disk-cache-settings"></a><span data-ttu-id="73fd9-246">Настройки кэша дисков.</span><span class="sxs-lookup"><span data-stu-id="73fd9-246">Disk cache settings</span></span>

<span data-ttu-id="73fd9-247">Существует три варианта кэширования узла:</span><span class="sxs-lookup"><span data-stu-id="73fd9-247">There are three options for host caching:</span></span>

- <span data-ttu-id="73fd9-248">*Только для чтения:* все запросы кэшируются для операций чтения в будущем.</span><span class="sxs-lookup"><span data-stu-id="73fd9-248">*Read-only*: All requests are cached for future reads.</span></span> <span data-ttu-id="73fd9-249">Все операции записи сохраняются непосредственно в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="73fd9-249">All writes are persisted directly to Azure Blob storage.</span></span>

- <span data-ttu-id="73fd9-250">*Чтение и запись:* это алгоритм упреждающего чтения.</span><span class="sxs-lookup"><span data-stu-id="73fd9-250">*Read-write*: This is a “read-ahead” algorithm.</span></span> <span data-ttu-id="73fd9-251">Операции чтения и записи кэшируются для будущих операций чтения.</span><span class="sxs-lookup"><span data-stu-id="73fd9-251">The reads and writes are cached for future reads.</span></span> <span data-ttu-id="73fd9-252">Операции несквозной записи сначала сохраняются в локальном кэше.</span><span class="sxs-lookup"><span data-stu-id="73fd9-252">Non-write-through writes are persisted to the local cache first.</span></span> <span data-ttu-id="73fd9-253">Для SQL Server операции записи сохраняются в службе хранилища Azure, так как используется сквозная запись.</span><span class="sxs-lookup"><span data-stu-id="73fd9-253">For SQL Server, writes are persisted to Azure Storage because it uses write-through.</span></span> <span data-ttu-id="73fd9-254">Кроме того, служба обеспечивает наименьшую задержку диска для незначительных рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="73fd9-254">It also provides the lowest disk latency for light workloads.</span></span>

- <span data-ttu-id="73fd9-255">*Нет* (отключено): с помощью этого параметра вы можете избежать кэширования.</span><span class="sxs-lookup"><span data-stu-id="73fd9-255">*None* (disabled): By using this option, you can bypass the cache.</span></span> <span data-ttu-id="73fd9-256">Все данные передаются на диск и хранятся в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="73fd9-256">All the data is transferred to disk and persisted to Azure Storage.</span></span> <span data-ttu-id="73fd9-257">Этот метод обеспечивает наивысшую скорость ввода-вывода для рабочих нагрузок с большим объемом операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="73fd9-257">This method gives you the highest I/O rate for I/O intensive workloads.</span></span> <span data-ttu-id="73fd9-258">Также необходимо учитывать стоимость транзакции.</span><span class="sxs-lookup"><span data-stu-id="73fd9-258">You also need to take “transaction cost” into consideration.</span></span>

<span data-ttu-id="73fd9-259">**рекомендации**;</span><span class="sxs-lookup"><span data-stu-id="73fd9-259">**Recommendations**</span></span>

<span data-ttu-id="73fd9-260">Чтобы максимально увеличить пропускную способность, рекомендуем начать с параметра **Нет** для кэширования узла.</span><span class="sxs-lookup"><span data-stu-id="73fd9-260">To maximize the throughput, we recommend that you  start with **None** for host caching.</span></span> <span data-ttu-id="73fd9-261">Помните, что для хранилища класса Premium необходимо отключить препятствующие факторы при подключении файловой системы с параметром **Только для чтения** или **Нет**.</span><span class="sxs-lookup"><span data-stu-id="73fd9-261">For Premium Storage, keep in mind that you must disable the "barriers" when you mount the file system with the **ReadOnly** or **None** options.</span></span> <span data-ttu-id="73fd9-262">Внесите значения UUID дисков в файл /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="73fd9-262">Update the /etc/fstab file with the UUID to the disks.</span></span>

<span data-ttu-id="73fd9-263">Дополнительные сведения см. в разделе [Хранилище класса Premium для виртуальных машин Linux](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span><span class="sxs-lookup"><span data-stu-id="73fd9-263">For more information, see [Premium Storage for Linux VMs](https://docs.microsoft.com/azure/storage/storage-premium-storage#premium-storage-for-linux-vms).</span></span>

![Снимок экрана страницы управляемых дисков](./media/oracle-design/premium_disk02.png)

- <span data-ttu-id="73fd9-265">Для дисков операционной системы используйте кэширование **Чтение и запись** по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="73fd9-265">For OS disks, use default **Read/Write** caching.</span></span>
- <span data-ttu-id="73fd9-266">Для кэширования SYSTEM, TEMP и UNDO используйте параметр **Нет**.</span><span class="sxs-lookup"><span data-stu-id="73fd9-266">For SYSTEM, TEMP, and UNDO use **None** for caching.</span></span>
- <span data-ttu-id="73fd9-267">Для кэширования DATA используйте параметр **Нет**.</span><span class="sxs-lookup"><span data-stu-id="73fd9-267">For DATA, use **None** for caching.</span></span> <span data-ttu-id="73fd9-268">Но если база данных предназначена только для чтения или интенсивного чтения, используйте кэширование **Только для чтения**.</span><span class="sxs-lookup"><span data-stu-id="73fd9-268">But if your database is read-only or read-intensive, use **Read-only** caching.</span></span>

<span data-ttu-id="73fd9-269">Сохранив настройки диска данных вы сможете изменить параметры кэширования узла, только отключив диск на уровне операционной системы, а затем снова подключив, когда изменения будут внесены.</span><span class="sxs-lookup"><span data-stu-id="73fd9-269">After your data disk setting is saved, you can't change the host cache setting unless you unmount the drive at the OS level and then remount it after you've made the change.</span></span>


## <a name="security"></a><span data-ttu-id="73fd9-270">Безопасность</span><span class="sxs-lookup"><span data-stu-id="73fd9-270">Security</span></span>

<span data-ttu-id="73fd9-271">Установив и настроив среду Azure, вы можете приступать к обеспечению защиты сети.</span><span class="sxs-lookup"><span data-stu-id="73fd9-271">After you have set up and configured your Azure environment, the next step is to secure your network.</span></span> <span data-ttu-id="73fd9-272">Вот несколько рекомендаций.</span><span class="sxs-lookup"><span data-stu-id="73fd9-272">Here are some recommendations:</span></span>

- <span data-ttu-id="73fd9-273">*Политика NSG:* NSG можно определить для подсети или сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="73fd9-273">*NSG policy*: NSG can be defined by a subnet or NIC.</span></span> <span data-ttu-id="73fd9-274">Чтобы обеспечить безопасность и принудительную маршрутизацию для таких компонентов, как приложения брандмауэра, проще управлять доступом на уровне подсети.</span><span class="sxs-lookup"><span data-stu-id="73fd9-274">It's simpler to control access at the subnet level both for security and force routing for things like application firewalls.</span></span>

- <span data-ttu-id="73fd9-275">*Jumpbox:* для более безопасного доступа администраторы не должны напрямую подключаться к службам приложений или базам данных.</span><span class="sxs-lookup"><span data-stu-id="73fd9-275">*Jumpbox*: For more secure access, administrators should not directly connect to the application service or database.</span></span> <span data-ttu-id="73fd9-276">jumpbox используется в качестве носителя между ресурсами Azure и компьютером администратора.</span><span class="sxs-lookup"><span data-stu-id="73fd9-276">A jumpbox is used as a media between the administrator machine and Azure resources.</span></span>
<span data-ttu-id="73fd9-277">![Снимок экрана страницы топологии Jumpbox](./media/oracle-design/jumpbox.png)</span><span class="sxs-lookup"><span data-stu-id="73fd9-277">![Screenshot of the Jumpbox topology page](./media/oracle-design/jumpbox.png)</span></span>

    <span data-ttu-id="73fd9-278">Компьютер администратора должен предоставлять доступ только к Jumpbox.</span><span class="sxs-lookup"><span data-stu-id="73fd9-278">The administrator machine should offer IP-restricted access to the jumpbox only.</span></span> <span data-ttu-id="73fd9-279">Для Jumpbox следует предоставить доступ к базам данных и приложениям.</span><span class="sxs-lookup"><span data-stu-id="73fd9-279">The jumpbox should have access to the application and database.</span></span>

- <span data-ttu-id="73fd9-280">*Частная сеть (подсети):* рекомендуем устанавливать службу приложений и базу данных в разных подсетях, чтобы политика NSG могла настроить расширенные возможности управления.</span><span class="sxs-lookup"><span data-stu-id="73fd9-280">*Private network* (subnets): We recommend that you have the application service and database on separate subnets, so better control can be set by NSG policy.</span></span>


## <a name="additional-reading"></a><span data-ttu-id="73fd9-281">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="73fd9-281">Additional reading</span></span>

- [<span data-ttu-id="73fd9-282">Настройка Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="73fd9-282">Configure Oracle ASM</span></span>](configure-oracle-asm.md)
- [<span data-ttu-id="73fd9-283">Реализация Oracle Data Guard на виртуальной машине Azure под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="73fd9-283">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="73fd9-284">Реализация Oracle Golden Gate на виртуальной машине Azure под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="73fd9-284">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="73fd9-285">Создание резервных копий и восстановление базы данных Oracle Database 12c на виртуальной машине Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="73fd9-285">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="73fd9-286">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="73fd9-286">Next steps</span></span>

- <span data-ttu-id="73fd9-287">Изучите [руководство по созданию высокодоступных виртуальных машин](../../linux/create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="73fd9-287">[Tutorial: Create highly available VMs](../../linux/create-cli-complete.md)</span></span>
- <span data-ttu-id="73fd9-288">[Изучите примеры развертывания виртуальных машин с помощью интерфейса командной строки](../../linux/cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="73fd9-288">[Explore VM deployment Azure CLI samples](../../linux/cli-samples.md)</span></span>
