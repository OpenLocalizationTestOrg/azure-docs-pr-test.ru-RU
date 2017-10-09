---
title: "aaaManage Azure диски с hello Azure PowerShell | Документы Microsoft"
description: "Учебник - Управление дисками Azure с hello Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2f61ad18bc94bab527d7ae593da603c6073adc89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-powershell"></a><span data-ttu-id="2f8f0-103">Управление дисками Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f8f0-103">Manage Azure disks with PowerShell</span></span>

<span data-ttu-id="2f8f0-104">Виртуальные машины Azure используют диски toostore hello виртуальные машины операционной системы, приложений и данных.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-104">Azure virtual machines use disks toostore hello VMs operating system, applications, and data.</span></span> <span data-ttu-id="2f8f0-105">При создании виртуальной Машины это важно toochoose размер диска и рабочей нагрузки соответствующие toohello ожидается конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-105">When creating a VM it is important toochoose a disk size and configuration appropriate toohello expected workload.</span></span> <span data-ttu-id="2f8f0-106">В этом руководстве рассматривается развертывание дисков виртуальных машин и управление ими.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="2f8f0-107">Здесь содержатся сведения о:</span><span class="sxs-lookup"><span data-stu-id="2f8f0-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2f8f0-108">дисках ОС и временных дисках;</span><span class="sxs-lookup"><span data-stu-id="2f8f0-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="2f8f0-109">Диски данных</span><span class="sxs-lookup"><span data-stu-id="2f8f0-109">Data disks</span></span>
> * <span data-ttu-id="2f8f0-110">дисками уровня "Стандартный" и "Премиум";</span><span class="sxs-lookup"><span data-stu-id="2f8f0-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="2f8f0-111">производительностью дисков;</span><span class="sxs-lookup"><span data-stu-id="2f8f0-111">Disk performance</span></span>
> * <span data-ttu-id="2f8f0-112">присоединением и подготовкой дисков данных;</span><span class="sxs-lookup"><span data-stu-id="2f8f0-112">Attaching and preparing data disks</span></span>

<span data-ttu-id="2f8f0-113">Этот учебник требует hello Azure PowerShell модуль версии 3.6 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="2f8f0-114">Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="2f8f0-115">Получить tooupgrade [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="2f8f0-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="default-azure-disks"></a><span data-ttu-id="2f8f0-116">Диски Azure по умолчанию</span><span class="sxs-lookup"><span data-stu-id="2f8f0-116">Default Azure disks</span></span>

<span data-ttu-id="2f8f0-117">При создании виртуальной машины Azure двух дисков являются toohello автоматически подключенных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-117">When an Azure virtual machine is created, two disks are automatically attached toohello virtual machine.</span></span> 

<span data-ttu-id="2f8f0-118">**Диск операционной системы** - дисков операционной системы можно изменять, но копирование too1 терабайт и узлы hello операционной системы виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-118">**Operating system disk** - Operating system disks can be sized up too1 terabyte, and hosts hello VMs operating system.</span></span>  <span data-ttu-id="2f8f0-119">диск ОС Hello назначается буква *c:* по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-119">hello OS disk is assigned a drive letter of *c:* by default.</span></span> <span data-ttu-id="2f8f0-120">кэширование конфигурацию диска ОС hello диска Hello оптимизирован для работы операционной системы.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-120">hello disk caching configuration of hello OS disk is optimized for OS performance.</span></span> <span data-ttu-id="2f8f0-121">диск ОС Hello **не должны** размещения приложений или данных.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-121">hello OS disk **should not** host applications or data.</span></span> <span data-ttu-id="2f8f0-122">Для приложений и данных используйте диск данных, который описан далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-122">For applications and data, use a data disk, which is detailed later in this article.</span></span>

<span data-ttu-id="2f8f0-123">**Временный диск** -временные диски используют твердотельного накопителя, которая находится на hello же Azure узле hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-123">**Temporary disk** - Temporary disks use a solid-state drive that is located on hello same Azure host as hello VM.</span></span> <span data-ttu-id="2f8f0-124">Временные диски обладают высокой производительностью и могут быть использованы для таких операций, как обработка временных данных.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-124">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="2f8f0-125">Данные, хранящиеся на временный диск удаляется, если hello виртуальной Машины, перемещенные tooa новый узел.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-125">However, if hello VM is moved tooa new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="2f8f0-126">размер Hello hello временного диска определяется hello размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-126">hello size of hello temporary disk is determined by hello VM size.</span></span> <span data-ttu-id="2f8f0-127">Для временных дисков по умолчанию назначается буква *d*.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-127">Temporary disks are assigned a drive letter of *d:* by default.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="2f8f0-128">Размеры временных дисков</span><span class="sxs-lookup"><span data-stu-id="2f8f0-128">Temporary disk sizes</span></span>

| <span data-ttu-id="2f8f0-129">Тип</span><span class="sxs-lookup"><span data-stu-id="2f8f0-129">Type</span></span> | <span data-ttu-id="2f8f0-130">Размер виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="2f8f0-130">VM Size</span></span> | <span data-ttu-id="2f8f0-131">Максимальный размер временного диска (ГБ)</span><span class="sxs-lookup"><span data-stu-id="2f8f0-131">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="2f8f0-132">Универсальные</span><span class="sxs-lookup"><span data-stu-id="2f8f0-132">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="2f8f0-133">Серии A и D</span><span class="sxs-lookup"><span data-stu-id="2f8f0-133">A and D series</span></span> | <span data-ttu-id="2f8f0-134">800</span><span class="sxs-lookup"><span data-stu-id="2f8f0-134">800</span></span> |
| [<span data-ttu-id="2f8f0-135">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="2f8f0-135">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="2f8f0-136">Серия F</span><span class="sxs-lookup"><span data-stu-id="2f8f0-136">F series</span></span> | <span data-ttu-id="2f8f0-137">800</span><span class="sxs-lookup"><span data-stu-id="2f8f0-137">800</span></span> |
| [<span data-ttu-id="2f8f0-138">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="2f8f0-138">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="2f8f0-139">Серии D и G</span><span class="sxs-lookup"><span data-stu-id="2f8f0-139">D and G series</span></span> | <span data-ttu-id="2f8f0-140">6144</span><span class="sxs-lookup"><span data-stu-id="2f8f0-140">6144</span></span> |
| [<span data-ttu-id="2f8f0-141">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="2f8f0-141">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="2f8f0-142">Серия L</span><span class="sxs-lookup"><span data-stu-id="2f8f0-142">L series</span></span> | <span data-ttu-id="2f8f0-143">5630</span><span class="sxs-lookup"><span data-stu-id="2f8f0-143">5630</span></span> |
| [<span data-ttu-id="2f8f0-144">GPU</span><span class="sxs-lookup"><span data-stu-id="2f8f0-144">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="2f8f0-145">Серия N</span><span class="sxs-lookup"><span data-stu-id="2f8f0-145">N series</span></span> | <span data-ttu-id="2f8f0-146">1440</span><span class="sxs-lookup"><span data-stu-id="2f8f0-146">1440</span></span> |
| [<span data-ttu-id="2f8f0-147">Высокопроизводительные</span><span class="sxs-lookup"><span data-stu-id="2f8f0-147">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="2f8f0-148">Серии A и H</span><span class="sxs-lookup"><span data-stu-id="2f8f0-148">A and H series</span></span> | <span data-ttu-id="2f8f0-149">2000</span><span class="sxs-lookup"><span data-stu-id="2f8f0-149">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="2f8f0-150">Диски данных Azure</span><span class="sxs-lookup"><span data-stu-id="2f8f0-150">Azure data disks</span></span>

<span data-ttu-id="2f8f0-151">Вы можете добавить дополнительные диски данных, чтобы установить приложения и хранить данные.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-151">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="2f8f0-152">Диски данных следует использовать в любой ситуации, где требуется надежное хранилище данных, обеспечивающее высокую скорость реагирования.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-152">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="2f8f0-153">Максимальная емкость каждого диска данных составляет 1 ТБ.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-153">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="2f8f0-154">Hello размера виртуальной машины hello определяет число дисков может быть tooa подключенных виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-154">hello size of hello virtual machine determines how many data disks can be attached tooa VM.</span></span> <span data-ttu-id="2f8f0-155">Для каждого ядра виртуальной машины можно подключить два диска данных.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-155">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="2f8f0-156">Максимальное число дисков данных на виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="2f8f0-156">Max data disks per VM</span></span>

| <span data-ttu-id="2f8f0-157">Тип</span><span class="sxs-lookup"><span data-stu-id="2f8f0-157">Type</span></span> | <span data-ttu-id="2f8f0-158">Размер виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="2f8f0-158">VM Size</span></span> | <span data-ttu-id="2f8f0-159">Максимальное число дисков данных на виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="2f8f0-159">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="2f8f0-160">Универсальные</span><span class="sxs-lookup"><span data-stu-id="2f8f0-160">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="2f8f0-161">Серии A и D</span><span class="sxs-lookup"><span data-stu-id="2f8f0-161">A and D series</span></span> | <span data-ttu-id="2f8f0-162">32</span><span class="sxs-lookup"><span data-stu-id="2f8f0-162">32</span></span> |
| [<span data-ttu-id="2f8f0-163">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="2f8f0-163">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="2f8f0-164">Серия F</span><span class="sxs-lookup"><span data-stu-id="2f8f0-164">F series</span></span> | <span data-ttu-id="2f8f0-165">32</span><span class="sxs-lookup"><span data-stu-id="2f8f0-165">32</span></span> |
| [<span data-ttu-id="2f8f0-166">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="2f8f0-166">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="2f8f0-167">Серии D и G</span><span class="sxs-lookup"><span data-stu-id="2f8f0-167">D and G series</span></span> | <span data-ttu-id="2f8f0-168">64</span><span class="sxs-lookup"><span data-stu-id="2f8f0-168">64</span></span> |
| [<span data-ttu-id="2f8f0-169">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="2f8f0-169">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="2f8f0-170">Серия L</span><span class="sxs-lookup"><span data-stu-id="2f8f0-170">L series</span></span> | <span data-ttu-id="2f8f0-171">64</span><span class="sxs-lookup"><span data-stu-id="2f8f0-171">64</span></span> |
| [<span data-ttu-id="2f8f0-172">GPU</span><span class="sxs-lookup"><span data-stu-id="2f8f0-172">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="2f8f0-173">Серия N</span><span class="sxs-lookup"><span data-stu-id="2f8f0-173">N series</span></span> | <span data-ttu-id="2f8f0-174">48</span><span class="sxs-lookup"><span data-stu-id="2f8f0-174">48</span></span> |
| [<span data-ttu-id="2f8f0-175">Высокопроизводительные</span><span class="sxs-lookup"><span data-stu-id="2f8f0-175">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="2f8f0-176">Серии A и H</span><span class="sxs-lookup"><span data-stu-id="2f8f0-176">A and H series</span></span> | <span data-ttu-id="2f8f0-177">32</span><span class="sxs-lookup"><span data-stu-id="2f8f0-177">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="2f8f0-178">Типы дисков виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="2f8f0-178">VM disk types</span></span>

<span data-ttu-id="2f8f0-179">В Azure предоставляются диски двух типов.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-179">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="2f8f0-180">Диск уровня "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="2f8f0-180">Standard disk</span></span>

<span data-ttu-id="2f8f0-181">Хранилище класса Standard использует жесткие диски и обеспечивает экономичное хранилище с достаточной производительностью.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-181">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="2f8f0-182">Эти диски идеально подходят для экономных рабочих нагрузок разработки и тестирования.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-182">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="2f8f0-183">Диск уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="2f8f0-183">Premium disk</span></span>

<span data-ttu-id="2f8f0-184">Диски уровня "Премиум" используют высокопроизводительные твердотельные накопители с низкой задержкой.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-184">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="2f8f0-185">Они идеально подходят для виртуальных машин, выполняющих производственную рабочую нагрузку.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-185">Perfect for VMs running production workload.</span></span> <span data-ttu-id="2f8f0-186">Хранилище уровня "Премиум" поддерживает виртуальные машины серий DS, DSv2, GS и FS.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-186">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="2f8f0-187">Диски Premium бывают трех типов (P10 P20, P30), размер диска hello hello определяет тип диска hello.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-187">Premium disks come in three types (P10, P20, P30), hello size of hello disk determines hello disk type.</span></span> <span data-ttu-id="2f8f0-188">При выборе, следующий тип toohello округляется hello значение размера диска.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-188">When selecting, a disk size hello value is rounded up toohello next type.</span></span> <span data-ttu-id="2f8f0-189">Например если размер hello ниже тип диска hello 128 ГБ будет P10, 129 512 P20 и более 512 P30.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-189">For example, if hello size is below 128 GB hello disk type will be P10, between 129 and 512 P20, and over 512 P30.</span></span> 

### <a name="premium-disk-performance"></a><span data-ttu-id="2f8f0-190">Производительность диска уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="2f8f0-190">Premium disk performance</span></span>

|<span data-ttu-id="2f8f0-191">Тип диска хранилища уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="2f8f0-191">Premium storage disk type</span></span> | <span data-ttu-id="2f8f0-192">P10</span><span class="sxs-lookup"><span data-stu-id="2f8f0-192">P10</span></span> | <span data-ttu-id="2f8f0-193">P20</span><span class="sxs-lookup"><span data-stu-id="2f8f0-193">P20</span></span> | <span data-ttu-id="2f8f0-194">P30</span><span class="sxs-lookup"><span data-stu-id="2f8f0-194">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2f8f0-195">Размер диска (округленный в большую сторону)</span><span class="sxs-lookup"><span data-stu-id="2f8f0-195">Disk size (round up)</span></span> | <span data-ttu-id="2f8f0-196">128 ГБ</span><span class="sxs-lookup"><span data-stu-id="2f8f0-196">128 GB</span></span> | <span data-ttu-id="2f8f0-197">512 ГБ</span><span class="sxs-lookup"><span data-stu-id="2f8f0-197">512 GB</span></span> | <span data-ttu-id="2f8f0-198">1024 ГБ (1 ТБ)</span><span class="sxs-lookup"><span data-stu-id="2f8f0-198">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="2f8f0-199">Количество операций ввода-вывода в секунду на диск</span><span class="sxs-lookup"><span data-stu-id="2f8f0-199">IOPS per disk</span></span> | <span data-ttu-id="2f8f0-200">500</span><span class="sxs-lookup"><span data-stu-id="2f8f0-200">500</span></span> | <span data-ttu-id="2f8f0-201">2300</span><span class="sxs-lookup"><span data-stu-id="2f8f0-201">2,300</span></span> | <span data-ttu-id="2f8f0-202">5 000</span><span class="sxs-lookup"><span data-stu-id="2f8f0-202">5,000</span></span> |
<span data-ttu-id="2f8f0-203">Пропускная способность на диск</span><span class="sxs-lookup"><span data-stu-id="2f8f0-203">Throughput per disk</span></span> | <span data-ttu-id="2f8f0-204">100 МБ/с</span><span class="sxs-lookup"><span data-stu-id="2f8f0-204">100 MB/s</span></span> | <span data-ttu-id="2f8f0-205">150 МБ/с</span><span class="sxs-lookup"><span data-stu-id="2f8f0-205">150 MB/s</span></span> | <span data-ttu-id="2f8f0-206">200 МБ/с</span><span class="sxs-lookup"><span data-stu-id="2f8f0-206">200 MB/s</span></span> |

<span data-ttu-id="2f8f0-207">Хотя hello над таблицей идентифицирует max IOP для дисков, более высокий уровень производительности достигается путем чередования несколько дисков данных.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-207">While hello above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="2f8f0-208">Для экземпляра 64 данных диски могут быть присоединены tooStandard_GS5 виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-208">For instance, 64 data disks can be attached tooStandard_GS5 VM.</span></span> <span data-ttu-id="2f8f0-209">Если каждый из этих дисков относится к размеру P30, можно добиться производительности до 80 000 операций ввода-вывода в секунду.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-209">If each of these disks are sized as a P30, a maximum of 80,000 IOPS can be achieved.</span></span> <span data-ttu-id="2f8f0-210">Дополнительные сведения о максимальных количествах операций ввода-вывода в секунду для виртуальных машин см. в разделе [Размеры виртуальных машин Linux](./sizes.md).</span><span class="sxs-lookup"><span data-stu-id="2f8f0-210">For detailed information on max IOPS per VM, see [Linux VM sizes](./sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="2f8f0-211">Создание и подключение дисков</span><span class="sxs-lookup"><span data-stu-id="2f8f0-211">Create and attach disks</span></span>

<span data-ttu-id="2f8f0-212">Пример hello toocomplete в этом учебнике, необходимо иметь существующую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-212">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="2f8f0-213">Этот [пример сценария](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) позволяет создать ее при необходимости.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-213">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="2f8f0-214">Если заменить прохождение учебника hello группы ресурсов hello и ВМ имен при необходимости.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-214">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

<span data-ttu-id="2f8f0-215">Создание начальной настройки hello с [New AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span><span class="sxs-lookup"><span data-stu-id="2f8f0-215">Create hello initial configuration with [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span></span> <span data-ttu-id="2f8f0-216">Следующий пример Hello настраивает диск, находящийся в размер 128 гигабайт.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-216">hello following example configures a disk that is 128 gigabytes in size.</span></span>

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

<span data-ttu-id="2f8f0-217">Создать диск данных hello hello [New AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) команды.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-217">Create hello data disk with hello [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) command.</span></span>

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

<span data-ttu-id="2f8f0-218">Get hello виртуальной машины, которые должны tooadd hello данных диска toowith hello [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) команды.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-218">Get hello virtual machine that you want tooadd hello data disk toowith hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="2f8f0-219">Добавить hello данных диска toohello конфигурация виртуальной машины с hello [AzureRmVMDataDisk добавить](/powershell/module/azurerm.compute/add-azurermvmdatadisk) команды.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-219">Add hello data disk toohello virtual machine configuration with hello [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

<span data-ttu-id="2f8f0-220">Обновить hello виртуальную машину с hello [AzureRmVM обновление](/powershell/module/azurerm.compute/add-azurermvmdatadisk) команды.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-220">Update hello virtual machine with hello [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a><span data-ttu-id="2f8f0-221">Подготовка дисков данных</span><span class="sxs-lookup"><span data-stu-id="2f8f0-221">Prepare data disks</span></span>

<span data-ttu-id="2f8f0-222">После диск toohello подключенных виртуальных машин, hello операционной системы должен настроить toobe toouse hello диска.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-222">Once a disk has been attached toohello virtual machine, hello operating system needs toobe configured toouse hello disk.</span></span> <span data-ttu-id="2f8f0-223">Hello следующем примере показано, как toomanually Настройка hello первый диск добавлен toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-223">hello following example shows how toomanually configure hello first disk added toohello VM.</span></span> <span data-ttu-id="2f8f0-224">Также можно автоматизировать этот процесс с помощью hello [расширение пользовательского скрипта](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="2f8f0-224">This process can also be automated using hello [custom script extension](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="2f8f0-225">Настройка вручную</span><span class="sxs-lookup"><span data-stu-id="2f8f0-225">Manual configuration</span></span>

<span data-ttu-id="2f8f0-226">Создайте RDP-подключение с hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-226">Create an RDP connection with hello virtual machine.</span></span> <span data-ttu-id="2f8f0-227">Откройте PowerShell и выполните этот сценарий.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-227">Open up PowerShell and run this script.</span></span>

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a><span data-ttu-id="2f8f0-228">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2f8f0-228">Next steps</span></span>

<span data-ttu-id="2f8f0-229">В этом руководстве вы ознакомились с дисками виртуальных машин, а именно с:</span><span class="sxs-lookup"><span data-stu-id="2f8f0-229">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2f8f0-230">дисками ОС и временными дисками;</span><span class="sxs-lookup"><span data-stu-id="2f8f0-230">OS disks and temporary disks</span></span>
> * <span data-ttu-id="2f8f0-231">Диски данных</span><span class="sxs-lookup"><span data-stu-id="2f8f0-231">Data disks</span></span>
> * <span data-ttu-id="2f8f0-232">дисками уровня "Стандартный" и "Премиум";</span><span class="sxs-lookup"><span data-stu-id="2f8f0-232">Standard and Premium disks</span></span>
> * <span data-ttu-id="2f8f0-233">производительностью дисков;</span><span class="sxs-lookup"><span data-stu-id="2f8f0-233">Disk performance</span></span>
> * <span data-ttu-id="2f8f0-234">присоединением и подготовкой дисков данных;</span><span class="sxs-lookup"><span data-stu-id="2f8f0-234">Attaching and preparing data disks</span></span>

<span data-ttu-id="2f8f0-235">Переместить следующий учебник toolearn toohello об автоматической конфигурации виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="2f8f0-235">Advance toohello next tutorial toolearn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2f8f0-236">Автоматизация настройки виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="2f8f0-236">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
