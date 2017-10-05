---
title: "Управление дисками Azure с помощью Azure PowerShell | Документы Майкрософт"
description: "Руководство по управлению дисками Azure с помощью Azure PowerShell."
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
ms.openlocfilehash: 6f1bc9361745adc211f22416a7ba8ac1b8dc614e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-disks-with-powershell"></a><span data-ttu-id="b20f1-103">Управление дисками Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="b20f1-103">Manage Azure disks with PowerShell</span></span>

<span data-ttu-id="b20f1-104">Виртуальные машины Azure хранят операционную систему, приложения и данные на дисках.</span><span class="sxs-lookup"><span data-stu-id="b20f1-104">Azure virtual machines use disks to store the VMs operating system, applications, and data.</span></span> <span data-ttu-id="b20f1-105">При создании виртуальной машины важно выбрать размер диска и конфигурацию в соответствии с ожидаемой рабочей нагрузкой.</span><span class="sxs-lookup"><span data-stu-id="b20f1-105">When creating a VM it is important to choose a disk size and configuration appropriate to the expected workload.</span></span> <span data-ttu-id="b20f1-106">В этом руководстве рассматривается развертывание дисков виртуальных машин и управление ими.</span><span class="sxs-lookup"><span data-stu-id="b20f1-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="b20f1-107">Здесь содержатся сведения о:</span><span class="sxs-lookup"><span data-stu-id="b20f1-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b20f1-108">дисках ОС и временных дисках;</span><span class="sxs-lookup"><span data-stu-id="b20f1-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="b20f1-109">Диски данных</span><span class="sxs-lookup"><span data-stu-id="b20f1-109">Data disks</span></span>
> * <span data-ttu-id="b20f1-110">дисками уровня "Стандартный" и "Премиум";</span><span class="sxs-lookup"><span data-stu-id="b20f1-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="b20f1-111">производительностью дисков;</span><span class="sxs-lookup"><span data-stu-id="b20f1-111">Disk performance</span></span>
> * <span data-ttu-id="b20f1-112">присоединении и подготовке дисков данных.</span><span class="sxs-lookup"><span data-stu-id="b20f1-112">Attaching and preparing data disks</span></span>

<span data-ttu-id="b20f1-113">Для работы с этим руководством требуется модуль Azure PowerShell версии не ниже 3.6.</span><span class="sxs-lookup"><span data-stu-id="b20f1-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="b20f1-114">Чтобы узнать версию, выполните команду ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="b20f1-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="b20f1-115">Если вам необходимо выполнить обновление, см. статью [об установке и настройке модуля Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="b20f1-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="default-azure-disks"></a><span data-ttu-id="b20f1-116">Диски Azure по умолчанию</span><span class="sxs-lookup"><span data-stu-id="b20f1-116">Default Azure disks</span></span>

<span data-ttu-id="b20f1-117">При создании виртуальной машины Azure к ней автоматически подключаются два диска.</span><span class="sxs-lookup"><span data-stu-id="b20f1-117">When an Azure virtual machine is created, two disks are automatically attached to the virtual machine.</span></span> 

<span data-ttu-id="b20f1-118">**Диск операционной системы**. Размер дисков операционной системы может составлять до 1 ТБ. Это диски, содержащие операционную систему виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b20f1-118">**Operating system disk** - Operating system disks can be sized up to 1 terabyte, and hosts the VMs operating system.</span></span>  <span data-ttu-id="b20f1-119">Для диска ОС по умолчанию назначается буква *c*.</span><span class="sxs-lookup"><span data-stu-id="b20f1-119">The OS disk is assigned a drive letter of *c:* by default.</span></span> <span data-ttu-id="b20f1-120">Конфигурация кэширования диска ОС оптимизирована для производительности операционной системы.</span><span class="sxs-lookup"><span data-stu-id="b20f1-120">The disk caching configuration of the OS disk is optimized for OS performance.</span></span> <span data-ttu-id="b20f1-121">На диске ОС **не должны** размещаться приложения или данные.</span><span class="sxs-lookup"><span data-stu-id="b20f1-121">The OS disk **should not** host applications or data.</span></span> <span data-ttu-id="b20f1-122">Для приложений и данных используйте диск данных, который описан далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="b20f1-122">For applications and data, use a data disk, which is detailed later in this article.</span></span>

<span data-ttu-id="b20f1-123">**Временный диск**. Временные диски используют твердотельные накопители, расположенные на том же узле Azure, что и виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="b20f1-123">**Temporary disk** - Temporary disks use a solid-state drive that is located on the same Azure host as the VM.</span></span> <span data-ttu-id="b20f1-124">Временные диски обладают высокой производительностью и могут быть использованы для таких операций, как обработка временных данных.</span><span class="sxs-lookup"><span data-stu-id="b20f1-124">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="b20f1-125">Тем не менее, если виртуальная машина перемещается на новый узел, удаляются все данные, хранящиеся на временном диске.</span><span class="sxs-lookup"><span data-stu-id="b20f1-125">However, if the VM is moved to a new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="b20f1-126">Размер временного диска определяется размером виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b20f1-126">The size of the temporary disk is determined by the VM size.</span></span> <span data-ttu-id="b20f1-127">Для временных дисков по умолчанию назначается буква *d*.</span><span class="sxs-lookup"><span data-stu-id="b20f1-127">Temporary disks are assigned a drive letter of *d:* by default.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="b20f1-128">Размеры временных дисков</span><span class="sxs-lookup"><span data-stu-id="b20f1-128">Temporary disk sizes</span></span>

| <span data-ttu-id="b20f1-129">Тип</span><span class="sxs-lookup"><span data-stu-id="b20f1-129">Type</span></span> | <span data-ttu-id="b20f1-130">Размер виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b20f1-130">VM Size</span></span> | <span data-ttu-id="b20f1-131">Максимальный размер временного диска (ГБ)</span><span class="sxs-lookup"><span data-stu-id="b20f1-131">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="b20f1-132">Универсальные</span><span class="sxs-lookup"><span data-stu-id="b20f1-132">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="b20f1-133">Серии A и D</span><span class="sxs-lookup"><span data-stu-id="b20f1-133">A and D series</span></span> | <span data-ttu-id="b20f1-134">800</span><span class="sxs-lookup"><span data-stu-id="b20f1-134">800</span></span> |
| [<span data-ttu-id="b20f1-135">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="b20f1-135">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="b20f1-136">Серия F</span><span class="sxs-lookup"><span data-stu-id="b20f1-136">F series</span></span> | <span data-ttu-id="b20f1-137">800</span><span class="sxs-lookup"><span data-stu-id="b20f1-137">800</span></span> |
| [<span data-ttu-id="b20f1-138">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="b20f1-138">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="b20f1-139">Серии D и G</span><span class="sxs-lookup"><span data-stu-id="b20f1-139">D and G series</span></span> | <span data-ttu-id="b20f1-140">6144</span><span class="sxs-lookup"><span data-stu-id="b20f1-140">6144</span></span> |
| [<span data-ttu-id="b20f1-141">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="b20f1-141">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="b20f1-142">Серия L</span><span class="sxs-lookup"><span data-stu-id="b20f1-142">L series</span></span> | <span data-ttu-id="b20f1-143">5630</span><span class="sxs-lookup"><span data-stu-id="b20f1-143">5630</span></span> |
| [<span data-ttu-id="b20f1-144">GPU</span><span class="sxs-lookup"><span data-stu-id="b20f1-144">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="b20f1-145">Серия N</span><span class="sxs-lookup"><span data-stu-id="b20f1-145">N series</span></span> | <span data-ttu-id="b20f1-146">1440</span><span class="sxs-lookup"><span data-stu-id="b20f1-146">1440</span></span> |
| [<span data-ttu-id="b20f1-147">Высокопроизводительные</span><span class="sxs-lookup"><span data-stu-id="b20f1-147">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="b20f1-148">Серии A и H</span><span class="sxs-lookup"><span data-stu-id="b20f1-148">A and H series</span></span> | <span data-ttu-id="b20f1-149">2000</span><span class="sxs-lookup"><span data-stu-id="b20f1-149">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="b20f1-150">Диски данных Azure</span><span class="sxs-lookup"><span data-stu-id="b20f1-150">Azure data disks</span></span>

<span data-ttu-id="b20f1-151">Вы можете добавить дополнительные диски данных, чтобы установить приложения и хранить данные.</span><span class="sxs-lookup"><span data-stu-id="b20f1-151">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="b20f1-152">Диски данных следует использовать в любой ситуации, где требуется надежное хранилище данных, обеспечивающее высокую скорость реагирования.</span><span class="sxs-lookup"><span data-stu-id="b20f1-152">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="b20f1-153">Максимальная емкость каждого диска данных составляет 1 ТБ.</span><span class="sxs-lookup"><span data-stu-id="b20f1-153">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="b20f1-154">Размер виртуальной машины определяет, сколько дисков данных можно к ней подключить.</span><span class="sxs-lookup"><span data-stu-id="b20f1-154">The size of the virtual machine determines how many data disks can be attached to a VM.</span></span> <span data-ttu-id="b20f1-155">Для каждого ядра виртуальной машины можно подключить два диска данных.</span><span class="sxs-lookup"><span data-stu-id="b20f1-155">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="b20f1-156">Максимальное число дисков данных на виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="b20f1-156">Max data disks per VM</span></span>

| <span data-ttu-id="b20f1-157">Тип</span><span class="sxs-lookup"><span data-stu-id="b20f1-157">Type</span></span> | <span data-ttu-id="b20f1-158">Размер виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b20f1-158">VM Size</span></span> | <span data-ttu-id="b20f1-159">Максимальное число дисков данных на виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="b20f1-159">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="b20f1-160">Универсальные</span><span class="sxs-lookup"><span data-stu-id="b20f1-160">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="b20f1-161">Серии A и D</span><span class="sxs-lookup"><span data-stu-id="b20f1-161">A and D series</span></span> | <span data-ttu-id="b20f1-162">32</span><span class="sxs-lookup"><span data-stu-id="b20f1-162">32</span></span> |
| [<span data-ttu-id="b20f1-163">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="b20f1-163">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="b20f1-164">Серия F</span><span class="sxs-lookup"><span data-stu-id="b20f1-164">F series</span></span> | <span data-ttu-id="b20f1-165">32</span><span class="sxs-lookup"><span data-stu-id="b20f1-165">32</span></span> |
| [<span data-ttu-id="b20f1-166">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="b20f1-166">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="b20f1-167">Серии D и G</span><span class="sxs-lookup"><span data-stu-id="b20f1-167">D and G series</span></span> | <span data-ttu-id="b20f1-168">64</span><span class="sxs-lookup"><span data-stu-id="b20f1-168">64</span></span> |
| [<span data-ttu-id="b20f1-169">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="b20f1-169">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="b20f1-170">Серия L</span><span class="sxs-lookup"><span data-stu-id="b20f1-170">L series</span></span> | <span data-ttu-id="b20f1-171">64</span><span class="sxs-lookup"><span data-stu-id="b20f1-171">64</span></span> |
| [<span data-ttu-id="b20f1-172">GPU</span><span class="sxs-lookup"><span data-stu-id="b20f1-172">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="b20f1-173">Серия N</span><span class="sxs-lookup"><span data-stu-id="b20f1-173">N series</span></span> | <span data-ttu-id="b20f1-174">48</span><span class="sxs-lookup"><span data-stu-id="b20f1-174">48</span></span> |
| [<span data-ttu-id="b20f1-175">Высокопроизводительные</span><span class="sxs-lookup"><span data-stu-id="b20f1-175">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="b20f1-176">Серии A и H</span><span class="sxs-lookup"><span data-stu-id="b20f1-176">A and H series</span></span> | <span data-ttu-id="b20f1-177">32</span><span class="sxs-lookup"><span data-stu-id="b20f1-177">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="b20f1-178">Типы дисков виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b20f1-178">VM disk types</span></span>

<span data-ttu-id="b20f1-179">В Azure предоставляются диски двух типов.</span><span class="sxs-lookup"><span data-stu-id="b20f1-179">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="b20f1-180">Диск уровня "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="b20f1-180">Standard disk</span></span>

<span data-ttu-id="b20f1-181">Хранилище класса Standard использует жесткие диски и обеспечивает экономичное хранилище с достаточной производительностью.</span><span class="sxs-lookup"><span data-stu-id="b20f1-181">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="b20f1-182">Эти диски идеально подходят для экономных рабочих нагрузок разработки и тестирования.</span><span class="sxs-lookup"><span data-stu-id="b20f1-182">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="b20f1-183">Диск уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="b20f1-183">Premium disk</span></span>

<span data-ttu-id="b20f1-184">Диски уровня "Премиум" используют высокопроизводительные твердотельные накопители с низкой задержкой.</span><span class="sxs-lookup"><span data-stu-id="b20f1-184">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="b20f1-185">Они идеально подходят для виртуальных машин, выполняющих производственную рабочую нагрузку.</span><span class="sxs-lookup"><span data-stu-id="b20f1-185">Perfect for VMs running production workload.</span></span> <span data-ttu-id="b20f1-186">Хранилище уровня "Премиум" поддерживает виртуальные машины серий DS, DSv2, GS и FS.</span><span class="sxs-lookup"><span data-stu-id="b20f1-186">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="b20f1-187">Диски уровня "Премиум" бывают трех типов: P10, P20, P30. Размер диска определяет его тип.</span><span class="sxs-lookup"><span data-stu-id="b20f1-187">Premium disks come in three types (P10, P20, P30), the size of the disk determines the disk type.</span></span> <span data-ttu-id="b20f1-188">При выборе размер диска округляется в большую сторону до следующего типа.</span><span class="sxs-lookup"><span data-stu-id="b20f1-188">When selecting, a disk size the value is rounded up to the next type.</span></span> <span data-ttu-id="b20f1-189">Например, если размер меньше 128 ГБ, диска будет относиться к типу P10, от 129 до 512 ГБ — P20, более 512 ГБ — P30.</span><span class="sxs-lookup"><span data-stu-id="b20f1-189">For example, if the size is below 128 GB the disk type will be P10, between 129 and 512 P20, and over 512 P30.</span></span> 

### <a name="premium-disk-performance"></a><span data-ttu-id="b20f1-190">Производительность диска уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="b20f1-190">Premium disk performance</span></span>

|<span data-ttu-id="b20f1-191">Тип диска хранилища уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="b20f1-191">Premium storage disk type</span></span> | <span data-ttu-id="b20f1-192">P10</span><span class="sxs-lookup"><span data-stu-id="b20f1-192">P10</span></span> | <span data-ttu-id="b20f1-193">P20</span><span class="sxs-lookup"><span data-stu-id="b20f1-193">P20</span></span> | <span data-ttu-id="b20f1-194">P30</span><span class="sxs-lookup"><span data-stu-id="b20f1-194">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b20f1-195">Размер диска (округленный в большую сторону)</span><span class="sxs-lookup"><span data-stu-id="b20f1-195">Disk size (round up)</span></span> | <span data-ttu-id="b20f1-196">128 ГБ</span><span class="sxs-lookup"><span data-stu-id="b20f1-196">128 GB</span></span> | <span data-ttu-id="b20f1-197">512 ГБ</span><span class="sxs-lookup"><span data-stu-id="b20f1-197">512 GB</span></span> | <span data-ttu-id="b20f1-198">1024 ГБ (1 ТБ)</span><span class="sxs-lookup"><span data-stu-id="b20f1-198">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="b20f1-199">Количество операций ввода-вывода в секунду на диск</span><span class="sxs-lookup"><span data-stu-id="b20f1-199">IOPS per disk</span></span> | <span data-ttu-id="b20f1-200">500</span><span class="sxs-lookup"><span data-stu-id="b20f1-200">500</span></span> | <span data-ttu-id="b20f1-201">2300</span><span class="sxs-lookup"><span data-stu-id="b20f1-201">2,300</span></span> | <span data-ttu-id="b20f1-202">5 000</span><span class="sxs-lookup"><span data-stu-id="b20f1-202">5,000</span></span> |
<span data-ttu-id="b20f1-203">Пропускная способность на диск</span><span class="sxs-lookup"><span data-stu-id="b20f1-203">Throughput per disk</span></span> | <span data-ttu-id="b20f1-204">100 МБ/с</span><span class="sxs-lookup"><span data-stu-id="b20f1-204">100 MB/s</span></span> | <span data-ttu-id="b20f1-205">150 МБ/с</span><span class="sxs-lookup"><span data-stu-id="b20f1-205">150 MB/s</span></span> | <span data-ttu-id="b20f1-206">200 МБ/с</span><span class="sxs-lookup"><span data-stu-id="b20f1-206">200 MB/s</span></span> |

<span data-ttu-id="b20f1-207">Хотя в таблице выше указано максимальное число операций ввода-вывода в секунду на диск, можно обеспечить более высокий уровень производительности, применив чередование нескольких дисков данных.</span><span class="sxs-lookup"><span data-stu-id="b20f1-207">While the above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="b20f1-208">Например, к виртуальной машине Standard_GS5 можно подключить 64 диска данных.</span><span class="sxs-lookup"><span data-stu-id="b20f1-208">For instance, 64 data disks can be attached to Standard_GS5 VM.</span></span> <span data-ttu-id="b20f1-209">Если каждый из этих дисков относится к размеру P30, можно добиться производительности до 80 000 операций ввода-вывода в секунду.</span><span class="sxs-lookup"><span data-stu-id="b20f1-209">If each of these disks are sized as a P30, a maximum of 80,000 IOPS can be achieved.</span></span> <span data-ttu-id="b20f1-210">Дополнительные сведения о максимальных количествах операций ввода-вывода в секунду для виртуальных машин см. в разделе [Размеры виртуальных машин Linux](./sizes.md).</span><span class="sxs-lookup"><span data-stu-id="b20f1-210">For detailed information on max IOPS per VM, see [Linux VM sizes](./sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="b20f1-211">Создание и подключение дисков</span><span class="sxs-lookup"><span data-stu-id="b20f1-211">Create and attach disks</span></span>

<span data-ttu-id="b20f1-212">Для выполнения примера в этом руководстве требуется виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="b20f1-212">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="b20f1-213">Этот [пример сценария](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) позволяет создать ее при необходимости.</span><span class="sxs-lookup"><span data-stu-id="b20f1-213">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="b20f1-214">При работе с примером по мере необходимости заменяйте имена групп ресурсов и виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b20f1-214">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

<span data-ttu-id="b20f1-215">Создайте начальную конфигурацию, выполнив команду [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span><span class="sxs-lookup"><span data-stu-id="b20f1-215">Create the initial configuration with [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span></span> <span data-ttu-id="b20f1-216">В следующем примере настраивается диск размером 128 ГБ.</span><span class="sxs-lookup"><span data-stu-id="b20f1-216">The following example configures a disk that is 128 gigabytes in size.</span></span>

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

<span data-ttu-id="b20f1-217">Создайте диск данных с помощью команды [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="b20f1-217">Create the data disk with the [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) command.</span></span>

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

<span data-ttu-id="b20f1-218">Получите виртуальную машину, в которую вы хотите добавить диск данных, выполнив команду [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="b20f1-218">Get the virtual machine that you want to add the data disk to with the [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="b20f1-219">Добавьте диск данных в конфигурацию виртуальной машины с помощью команды [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="b20f1-219">Add the data disk to the virtual machine configuration with the [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

<span data-ttu-id="b20f1-220">Обновите виртуальную машину с помощью команды [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="b20f1-220">Update the virtual machine with the [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a><span data-ttu-id="b20f1-221">Подготовка дисков данных</span><span class="sxs-lookup"><span data-stu-id="b20f1-221">Prepare data disks</span></span>

<span data-ttu-id="b20f1-222">После подключения диска к виртуальной машине нужно настроить операционную систему для его использования.</span><span class="sxs-lookup"><span data-stu-id="b20f1-222">Once a disk has been attached to the virtual machine, the operating system needs to be configured to use the disk.</span></span> <span data-ttu-id="b20f1-223">В примере ниже показано, как вручную настроить первый диск, добавляемый в виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="b20f1-223">The following example shows how to manually configure the first disk added to the VM.</span></span> <span data-ttu-id="b20f1-224">Этот процесс можно автоматизировать с помощью [расширения настраиваемых сценариев](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="b20f1-224">This process can also be automated using the [custom script extension](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="b20f1-225">Настройка вручную</span><span class="sxs-lookup"><span data-stu-id="b20f1-225">Manual configuration</span></span>

<span data-ttu-id="b20f1-226">Создайте RDP-подключение к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="b20f1-226">Create an RDP connection with the virtual machine.</span></span> <span data-ttu-id="b20f1-227">Откройте PowerShell и выполните этот сценарий.</span><span class="sxs-lookup"><span data-stu-id="b20f1-227">Open up PowerShell and run this script.</span></span>

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a><span data-ttu-id="b20f1-228">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b20f1-228">Next steps</span></span>

<span data-ttu-id="b20f1-229">В этом руководстве вы ознакомились с дисками виртуальных машин, а именно с:</span><span class="sxs-lookup"><span data-stu-id="b20f1-229">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b20f1-230">дисками ОС и временными дисками;</span><span class="sxs-lookup"><span data-stu-id="b20f1-230">OS disks and temporary disks</span></span>
> * <span data-ttu-id="b20f1-231">Диски данных</span><span class="sxs-lookup"><span data-stu-id="b20f1-231">Data disks</span></span>
> * <span data-ttu-id="b20f1-232">дисками уровня "Стандартный" и "Премиум";</span><span class="sxs-lookup"><span data-stu-id="b20f1-232">Standard and Premium disks</span></span>
> * <span data-ttu-id="b20f1-233">производительностью дисков;</span><span class="sxs-lookup"><span data-stu-id="b20f1-233">Disk performance</span></span>
> * <span data-ttu-id="b20f1-234">присоединением и подготовкой дисков данных.</span><span class="sxs-lookup"><span data-stu-id="b20f1-234">Attaching and preparing data disks</span></span>

<span data-ttu-id="b20f1-235">Перейдите к следующему руководству, чтобы узнать об автоматической настройке виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b20f1-235">Advance to the next tutorial to learn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b20f1-236">Автоматизация настройки виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b20f1-236">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
