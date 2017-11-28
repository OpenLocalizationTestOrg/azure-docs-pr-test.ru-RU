---
title: "Управление дисками Azure с помощью Azure CLI | Документация Майкрософт"
description: "Руководство по управлению дисками Azure с помощью Azure CLI."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: d77dd2b44dca8cee6fa2e93e79cda76c80ccfe1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-disks-with-the-azure-cli"></a><span data-ttu-id="e2c13-103">Управление дисками Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e2c13-103">Manage Azure disks with the Azure CLI</span></span>

<span data-ttu-id="e2c13-104">Виртуальные машины Azure хранят операционную систему, приложения и данные на дисках.</span><span class="sxs-lookup"><span data-stu-id="e2c13-104">Azure virtual machines use disks to store the VMs operating system, applications, and data.</span></span> <span data-ttu-id="e2c13-105">При создании виртуальной машины важно выбрать размер диска и конфигурацию в соответствии с ожидаемой рабочей нагрузкой.</span><span class="sxs-lookup"><span data-stu-id="e2c13-105">When creating a VM it is important to choose a disk size and configuration appropriate to the expected workload.</span></span> <span data-ttu-id="e2c13-106">В этом руководстве рассматривается развертывание дисков виртуальных машин и управление ими.</span><span class="sxs-lookup"><span data-stu-id="e2c13-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="e2c13-107">Здесь содержатся сведения о:</span><span class="sxs-lookup"><span data-stu-id="e2c13-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e2c13-108">дисках ОС и временных дисках;</span><span class="sxs-lookup"><span data-stu-id="e2c13-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="e2c13-109">Диски данных</span><span class="sxs-lookup"><span data-stu-id="e2c13-109">Data disks</span></span>
> * <span data-ttu-id="e2c13-110">дисками уровня "Стандартный" и "Премиум";</span><span class="sxs-lookup"><span data-stu-id="e2c13-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="e2c13-111">производительностью дисков;</span><span class="sxs-lookup"><span data-stu-id="e2c13-111">Disk performance</span></span>
> * <span data-ttu-id="e2c13-112">присоединением и подготовкой дисков данных;</span><span class="sxs-lookup"><span data-stu-id="e2c13-112">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="e2c13-113">изменением размеров дисков;</span><span class="sxs-lookup"><span data-stu-id="e2c13-113">Resizing disks</span></span>
> * <span data-ttu-id="e2c13-114">моментальными снимками дисков.</span><span class="sxs-lookup"><span data-stu-id="e2c13-114">Disk snapshots</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e2c13-115">Если вы решили установить и использовать интерфейс командной строки локально, то для работы с этим руководством вам понадобится Azure CLI 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e2c13-115">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="e2c13-116">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="e2c13-116">Run `az --version` to find the version.</span></span> <span data-ttu-id="e2c13-117">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e2c13-117">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="default-azure-disks"></a><span data-ttu-id="e2c13-118">Диски Azure по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e2c13-118">Default Azure disks</span></span>

<span data-ttu-id="e2c13-119">При создании виртуальной машины Azure к ней автоматически подключаются два диска.</span><span class="sxs-lookup"><span data-stu-id="e2c13-119">When an Azure virtual machine is created, two disks are automatically attached to the virtual machine.</span></span> 

<span data-ttu-id="e2c13-120">**Диск операционной системы**. Размер дисков операционной системы может составлять до 1 ТБ. Это диски, содержащие операционную систему виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e2c13-120">**Operating system disk** - Operating system disks can be sized up to 1 terabyte, and hosts the VMs operating system.</span></span> <span data-ttu-id="e2c13-121">По умолчанию диск ОС помечается как */dev/sda*.</span><span class="sxs-lookup"><span data-stu-id="e2c13-121">The OS disk is labeled */dev/sda* by default.</span></span> <span data-ttu-id="e2c13-122">Конфигурация кэширования диска ОС оптимизирована для производительности операционной системы.</span><span class="sxs-lookup"><span data-stu-id="e2c13-122">The disk caching configuration of the OS disk is optimized for OS performance.</span></span> <span data-ttu-id="e2c13-123">Ввиду этой конфигурации на дисках ОС **не должны** размещаться приложения или данные.</span><span class="sxs-lookup"><span data-stu-id="e2c13-123">Because of this configuration, the OS disk **should not** host applications or data.</span></span> <span data-ttu-id="e2c13-124">Для приложений и данных используйте диски данных, которые описаны далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="e2c13-124">For applications and data, use data disks, which are detailed later in this article.</span></span> 

<span data-ttu-id="e2c13-125">**Временный диск**. Временные диски используют твердотельные накопители, расположенные на том же узле Azure, что и виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="e2c13-125">**Temporary disk** - Temporary disks use a solid-state drive that is located on the same Azure host as the VM.</span></span> <span data-ttu-id="e2c13-126">Временные диски обладают высокой производительностью и могут быть использованы для таких операций, как обработка временных данных.</span><span class="sxs-lookup"><span data-stu-id="e2c13-126">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="e2c13-127">Тем не менее, если виртуальная машина перемещается на новый узел, удаляются все данные, хранящиеся на временном диске.</span><span class="sxs-lookup"><span data-stu-id="e2c13-127">However, if the VM is moved to a new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="e2c13-128">Размер временного диска определяется размером виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e2c13-128">The size of the temporary disk is determined by the VM size.</span></span> <span data-ttu-id="e2c13-129">Временные диски помечаются как */dev/sdb* и используют точку подключения */mnt*.</span><span class="sxs-lookup"><span data-stu-id="e2c13-129">Temporary disks are labeled */dev/sdb* and have a mountpoint of */mnt*.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="e2c13-130">Размеры временных дисков</span><span class="sxs-lookup"><span data-stu-id="e2c13-130">Temporary disk sizes</span></span>

| <span data-ttu-id="e2c13-131">Тип</span><span class="sxs-lookup"><span data-stu-id="e2c13-131">Type</span></span> | <span data-ttu-id="e2c13-132">Размер виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e2c13-132">VM Size</span></span> | <span data-ttu-id="e2c13-133">Максимальный размер временного диска (ГБ)</span><span class="sxs-lookup"><span data-stu-id="e2c13-133">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="e2c13-134">Универсальные</span><span class="sxs-lookup"><span data-stu-id="e2c13-134">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="e2c13-135">Серии A и D</span><span class="sxs-lookup"><span data-stu-id="e2c13-135">A and D series</span></span> | <span data-ttu-id="e2c13-136">800</span><span class="sxs-lookup"><span data-stu-id="e2c13-136">800</span></span> |
| [<span data-ttu-id="e2c13-137">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="e2c13-137">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="e2c13-138">Серия F</span><span class="sxs-lookup"><span data-stu-id="e2c13-138">F series</span></span> | <span data-ttu-id="e2c13-139">800</span><span class="sxs-lookup"><span data-stu-id="e2c13-139">800</span></span> |
| [<span data-ttu-id="e2c13-140">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="e2c13-140">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="e2c13-141">Серии D и G</span><span class="sxs-lookup"><span data-stu-id="e2c13-141">D and G series</span></span> | <span data-ttu-id="e2c13-142">6144</span><span class="sxs-lookup"><span data-stu-id="e2c13-142">6144</span></span> |
| [<span data-ttu-id="e2c13-143">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="e2c13-143">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="e2c13-144">Серия L</span><span class="sxs-lookup"><span data-stu-id="e2c13-144">L series</span></span> | <span data-ttu-id="e2c13-145">5630</span><span class="sxs-lookup"><span data-stu-id="e2c13-145">5630</span></span> |
| [<span data-ttu-id="e2c13-146">GPU</span><span class="sxs-lookup"><span data-stu-id="e2c13-146">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="e2c13-147">Серия N</span><span class="sxs-lookup"><span data-stu-id="e2c13-147">N series</span></span> | <span data-ttu-id="e2c13-148">1440</span><span class="sxs-lookup"><span data-stu-id="e2c13-148">1440</span></span> |
| [<span data-ttu-id="e2c13-149">Высокопроизводительные</span><span class="sxs-lookup"><span data-stu-id="e2c13-149">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="e2c13-150">Серии A и H</span><span class="sxs-lookup"><span data-stu-id="e2c13-150">A and H series</span></span> | <span data-ttu-id="e2c13-151">2000</span><span class="sxs-lookup"><span data-stu-id="e2c13-151">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="e2c13-152">Диски данных Azure</span><span class="sxs-lookup"><span data-stu-id="e2c13-152">Azure data disks</span></span>

<span data-ttu-id="e2c13-153">Вы можете добавить дополнительные диски данных, чтобы установить приложения и хранить данные.</span><span class="sxs-lookup"><span data-stu-id="e2c13-153">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="e2c13-154">Диски данных следует использовать в любой ситуации, где требуется надежное хранилище данных, обеспечивающее высокую скорость реагирования.</span><span class="sxs-lookup"><span data-stu-id="e2c13-154">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="e2c13-155">Максимальная емкость каждого диска данных составляет 1 ТБ.</span><span class="sxs-lookup"><span data-stu-id="e2c13-155">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="e2c13-156">Размер виртуальной машины определяет, сколько дисков данных можно к ней подключить.</span><span class="sxs-lookup"><span data-stu-id="e2c13-156">The size of the virtual machine determines how many data disks can be attached to a VM.</span></span> <span data-ttu-id="e2c13-157">Для каждого ядра виртуальной машины можно подключить два диска данных.</span><span class="sxs-lookup"><span data-stu-id="e2c13-157">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="e2c13-158">Максимальное число дисков данных на виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="e2c13-158">Max data disks per VM</span></span>

| <span data-ttu-id="e2c13-159">Тип</span><span class="sxs-lookup"><span data-stu-id="e2c13-159">Type</span></span> | <span data-ttu-id="e2c13-160">Размер виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e2c13-160">VM Size</span></span> | <span data-ttu-id="e2c13-161">Максимальное число дисков данных на виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="e2c13-161">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="e2c13-162">Универсальные</span><span class="sxs-lookup"><span data-stu-id="e2c13-162">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="e2c13-163">Серии A и D</span><span class="sxs-lookup"><span data-stu-id="e2c13-163">A and D series</span></span> | <span data-ttu-id="e2c13-164">32</span><span class="sxs-lookup"><span data-stu-id="e2c13-164">32</span></span> |
| [<span data-ttu-id="e2c13-165">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="e2c13-165">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="e2c13-166">Серия F</span><span class="sxs-lookup"><span data-stu-id="e2c13-166">F series</span></span> | <span data-ttu-id="e2c13-167">32</span><span class="sxs-lookup"><span data-stu-id="e2c13-167">32</span></span> |
| [<span data-ttu-id="e2c13-168">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="e2c13-168">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="e2c13-169">Серии D и G</span><span class="sxs-lookup"><span data-stu-id="e2c13-169">D and G series</span></span> | <span data-ttu-id="e2c13-170">64</span><span class="sxs-lookup"><span data-stu-id="e2c13-170">64</span></span> |
| [<span data-ttu-id="e2c13-171">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="e2c13-171">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="e2c13-172">Серия L</span><span class="sxs-lookup"><span data-stu-id="e2c13-172">L series</span></span> | <span data-ttu-id="e2c13-173">64</span><span class="sxs-lookup"><span data-stu-id="e2c13-173">64</span></span> |
| [<span data-ttu-id="e2c13-174">GPU</span><span class="sxs-lookup"><span data-stu-id="e2c13-174">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="e2c13-175">Серия N</span><span class="sxs-lookup"><span data-stu-id="e2c13-175">N series</span></span> | <span data-ttu-id="e2c13-176">48</span><span class="sxs-lookup"><span data-stu-id="e2c13-176">48</span></span> |
| [<span data-ttu-id="e2c13-177">Высокопроизводительные</span><span class="sxs-lookup"><span data-stu-id="e2c13-177">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="e2c13-178">Серии A и H</span><span class="sxs-lookup"><span data-stu-id="e2c13-178">A and H series</span></span> | <span data-ttu-id="e2c13-179">32</span><span class="sxs-lookup"><span data-stu-id="e2c13-179">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="e2c13-180">Типы дисков виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e2c13-180">VM disk types</span></span>

<span data-ttu-id="e2c13-181">В Azure предоставляются диски двух типов.</span><span class="sxs-lookup"><span data-stu-id="e2c13-181">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="e2c13-182">Диск уровня "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="e2c13-182">Standard disk</span></span>

<span data-ttu-id="e2c13-183">Хранилище класса Standard использует жесткие диски и обеспечивает экономичное хранилище с достаточной производительностью.</span><span class="sxs-lookup"><span data-stu-id="e2c13-183">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="e2c13-184">Эти диски идеально подходят для экономных рабочих нагрузок разработки и тестирования.</span><span class="sxs-lookup"><span data-stu-id="e2c13-184">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="e2c13-185">Диск уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="e2c13-185">Premium disk</span></span>

<span data-ttu-id="e2c13-186">Диски уровня "Премиум" используют высокопроизводительные твердотельные накопители с низкой задержкой.</span><span class="sxs-lookup"><span data-stu-id="e2c13-186">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="e2c13-187">Они идеально подходят для виртуальных машин, выполняющих производственную рабочую нагрузку.</span><span class="sxs-lookup"><span data-stu-id="e2c13-187">Perfect for VMs running production workload.</span></span> <span data-ttu-id="e2c13-188">Хранилище уровня "Премиум" поддерживает виртуальные машины серий DS, DSv2, GS и FS.</span><span class="sxs-lookup"><span data-stu-id="e2c13-188">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="e2c13-189">Диски уровня "Премиум" бывают трех типов: P10, P20, P30. Размер диска определяет его тип.</span><span class="sxs-lookup"><span data-stu-id="e2c13-189">Premium disks come in three types (P10, P20, P30), the size of the disk determines the disk type.</span></span> <span data-ttu-id="e2c13-190">При выборе размер диска округляется в большую сторону до следующего типа.</span><span class="sxs-lookup"><span data-stu-id="e2c13-190">When selecting, a disk size the value is rounded up to the next type.</span></span> <span data-ttu-id="e2c13-191">Например, если размер диска составляет менее 128 ГБ, то типом диска является P10.</span><span class="sxs-lookup"><span data-stu-id="e2c13-191">For example, if the disk size is less than 128 GB, the disk type is P10.</span></span> <span data-ttu-id="e2c13-192">Если размер диска составляет от 129 до 512 ГБ, то его размер — P20.</span><span class="sxs-lookup"><span data-stu-id="e2c13-192">If the disk size is between 129 GB and 512 GB, the size is a P20.</span></span> <span data-ttu-id="e2c13-193">Все диски более 512 ГБ относятся к типу P30.</span><span class="sxs-lookup"><span data-stu-id="e2c13-193">Anything over 512 GB, the size is a P30.</span></span>

### <a name="premium-disk-performance"></a><span data-ttu-id="e2c13-194">Производительность диска уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="e2c13-194">Premium disk performance</span></span>

|<span data-ttu-id="e2c13-195">Тип диска хранилища уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="e2c13-195">Premium storage disk type</span></span> | <span data-ttu-id="e2c13-196">P10</span><span class="sxs-lookup"><span data-stu-id="e2c13-196">P10</span></span> | <span data-ttu-id="e2c13-197">P20</span><span class="sxs-lookup"><span data-stu-id="e2c13-197">P20</span></span> | <span data-ttu-id="e2c13-198">P30</span><span class="sxs-lookup"><span data-stu-id="e2c13-198">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e2c13-199">Размер диска (округленный в большую сторону)</span><span class="sxs-lookup"><span data-stu-id="e2c13-199">Disk size (round up)</span></span> | <span data-ttu-id="e2c13-200">128 ГБ</span><span class="sxs-lookup"><span data-stu-id="e2c13-200">128 GB</span></span> | <span data-ttu-id="e2c13-201">512 ГБ</span><span class="sxs-lookup"><span data-stu-id="e2c13-201">512 GB</span></span> | <span data-ttu-id="e2c13-202">1024 ГБ (1 ТБ)</span><span class="sxs-lookup"><span data-stu-id="e2c13-202">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="e2c13-203">Макс. количество операций ввода-вывода в секунду на диск</span><span class="sxs-lookup"><span data-stu-id="e2c13-203">Max IOPS per disk</span></span> | <span data-ttu-id="e2c13-204">500</span><span class="sxs-lookup"><span data-stu-id="e2c13-204">500</span></span> | <span data-ttu-id="e2c13-205">2300</span><span class="sxs-lookup"><span data-stu-id="e2c13-205">2,300</span></span> | <span data-ttu-id="e2c13-206">5 000</span><span class="sxs-lookup"><span data-stu-id="e2c13-206">5,000</span></span> |
<span data-ttu-id="e2c13-207">Пропускная способность на диск</span><span class="sxs-lookup"><span data-stu-id="e2c13-207">Throughput per disk</span></span> | <span data-ttu-id="e2c13-208">100 МБ/с</span><span class="sxs-lookup"><span data-stu-id="e2c13-208">100 MB/s</span></span> | <span data-ttu-id="e2c13-209">150 МБ/с</span><span class="sxs-lookup"><span data-stu-id="e2c13-209">150 MB/s</span></span> | <span data-ttu-id="e2c13-210">200 МБ/с</span><span class="sxs-lookup"><span data-stu-id="e2c13-210">200 MB/s</span></span> |

<span data-ttu-id="e2c13-211">Хотя в таблице выше указано максимальное число операций ввода-вывода в секунду на диск, можно обеспечить более высокий уровень производительности, применив чередование нескольких дисков данных.</span><span class="sxs-lookup"><span data-stu-id="e2c13-211">While the above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="e2c13-212">Например, виртуальная машина Standard_GS5 может достичь 80 000 операций ввода-вывода в секунду.</span><span class="sxs-lookup"><span data-stu-id="e2c13-212">For instance, a Standard_GS5 VM can achieve a maximum of 80,000 IOPS.</span></span> <span data-ttu-id="e2c13-213">Дополнительные сведения о максимальных количествах операций ввода-вывода в секунду для виртуальных машин см. в разделе [Размеры виртуальных машин Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="e2c13-213">For detailed information on max IOPS per VM, see [Linux VM sizes](sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="e2c13-214">Создание и подключение дисков</span><span class="sxs-lookup"><span data-stu-id="e2c13-214">Create and attach disks</span></span>

<span data-ttu-id="e2c13-215">Диски данных можно создать и подключить к существующей виртуальной машины или же сделать это во время создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e2c13-215">Data disks can be created and attached at VM creation time or to an existing VM.</span></span>

### <a name="attach-disk-at-vm-creation"></a><span data-ttu-id="e2c13-216">Подключение диска при создании виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e2c13-216">Attach disk at VM creation</span></span>

<span data-ttu-id="e2c13-217">Создайте группу ресурсов с помощью команды [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e2c13-217">Create a resource group with the [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

<span data-ttu-id="e2c13-218">Создайте виртуальную машину с помощью команды [az vm create]( /cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="e2c13-218">Create a VM using the [az vm create]( /cli/azure/vm#create) command.</span></span> <span data-ttu-id="e2c13-219">Аргумент `--datadisk-sizes-gb` указывает, что должен быть создан дополнительный диск, подключаемый к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="e2c13-219">The `--datadisk-sizes-gb` argument is used to specify that an additional disk should be created and attached to the virtual machine.</span></span> <span data-ttu-id="e2c13-220">Чтобы создать и подключить несколько дисков, используйте список значений размеров дисков, разделенный пробелами.</span><span class="sxs-lookup"><span data-stu-id="e2c13-220">To create and attach more than one disk, use a space-delimited list of disk size values.</span></span> <span data-ttu-id="e2c13-221">В следующем примере создается виртуальная машина с двумя дисками емкостью по 128 ГБ.</span><span class="sxs-lookup"><span data-stu-id="e2c13-221">In the following example, a VM is created with two data disks, both 128 GB.</span></span> <span data-ttu-id="e2c13-222">Так как размеры дисков составляют 128 ГБ, они настроены как диски типа P10, которые обеспечивают до 500 операций ввода-вывода на диск.</span><span class="sxs-lookup"><span data-stu-id="e2c13-222">Because the disk sizes are 128 GB, these disks are both configured as P10s, which provide maximum 500 IOPS per disk.</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-to-existing-vm"></a><span data-ttu-id="e2c13-223">Подключение диска к существующей виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="e2c13-223">Attach disk to existing VM</span></span>

<span data-ttu-id="e2c13-224">Чтобы создать диск и подключить его к существующей виртуальной машине, выполните команду [az vm disk attach](/cli/azure/vm/disk#attach).</span><span class="sxs-lookup"><span data-stu-id="e2c13-224">To create and attach a new disk to an existing virtual machine, use the [az vm disk attach](/cli/azure/vm/disk#attach) command.</span></span> <span data-ttu-id="e2c13-225">Приведенный ниже пример создает диск уровня "Премиум" размера в 128 ГБ и подключает его к виртуальной машине, созданной на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="e2c13-225">The following example creates a premium disk, 128 gigabytes in size, and attaches it to the VM created in the last step.</span></span>

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a><span data-ttu-id="e2c13-226">Подготовка дисков данных</span><span class="sxs-lookup"><span data-stu-id="e2c13-226">Prepare data disks</span></span>

<span data-ttu-id="e2c13-227">После подключения диска к виртуальной машине необходимо настроить операционную систему для его использования.</span><span class="sxs-lookup"><span data-stu-id="e2c13-227">Once a disk has been attached to the virtual machine, the operating system needs to be configured to use the disk.</span></span> <span data-ttu-id="e2c13-228">В примере ниже показано, как настроить диск вручную.</span><span class="sxs-lookup"><span data-stu-id="e2c13-228">The following example shows how to manually configure a disk.</span></span> <span data-ttu-id="e2c13-229">Этот процесс можно автоматизировать с помощью cloud-init, как описывается в [этом руководстве](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="e2c13-229">This process can also be automated using cloud-init, which is covered in a [later tutorial](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="e2c13-230">Настройка вручную</span><span class="sxs-lookup"><span data-stu-id="e2c13-230">Manual configuration</span></span>

<span data-ttu-id="e2c13-231">Создайте SSH-подключение к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="e2c13-231">Create an SSH connection with the virtual machine.</span></span> <span data-ttu-id="e2c13-232">Замените IP-адреса в примере общедоступным IP-адресом виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e2c13-232">Replace the example IP address with the public IP of the virtual machine.</span></span>

```azurecli-interactive 
ssh 52.174.34.95
```

<span data-ttu-id="e2c13-233">Создание разделы на диске с помощью `fdisk`.</span><span class="sxs-lookup"><span data-stu-id="e2c13-233">Partition the disk with `fdisk`.</span></span>

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="e2c13-234">Запишите файловую систему на раздел, выполнив команду `mkfs`.</span><span class="sxs-lookup"><span data-stu-id="e2c13-234">Write a file system to the partition by using the `mkfs` command.</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="e2c13-235">Подключите новый диск, чтобы он был доступен в операционной системе.</span><span class="sxs-lookup"><span data-stu-id="e2c13-235">Mount the new disk so that it is accessible in the operating system.</span></span>

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="e2c13-236">Теперь этот диск доступен через точку подключения *datadrive*, что можно проверить с помощью команды `df -h`.</span><span class="sxs-lookup"><span data-stu-id="e2c13-236">The disk can now be accessed through the *datadrive* mountpoint, which can be verified by running the `df -h` command.</span></span> 

```bash
df -h
```

<span data-ttu-id="e2c13-237">Ее результат показывает, что новый диск подключен к */datadrive*.</span><span class="sxs-lookup"><span data-stu-id="e2c13-237">The output shows the new drive mounted on */datadrive*.</span></span>

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

<span data-ttu-id="e2c13-238">Чтобы обеспечить повторное подключение диска после перезагрузки, его необходимо добавить в файл */etc/fstab*.</span><span class="sxs-lookup"><span data-stu-id="e2c13-238">To ensure that the drive is remounted after a reboot, it must be added to the */etc/fstab* file.</span></span> <span data-ttu-id="e2c13-239">Для этого получите UUID диска с помощью служебной программы `blkid`.</span><span class="sxs-lookup"><span data-stu-id="e2c13-239">To do so, get the UUID of the disk with the `blkid` utility.</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="e2c13-240">На экране отображается UUID диска, в данном случае это `/dev/sdc1`.</span><span class="sxs-lookup"><span data-stu-id="e2c13-240">The output displays the UUID of the drive, `/dev/sdc1` in this case.</span></span>

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

<span data-ttu-id="e2c13-241">Добавьте в файл */etc/fstab* строку следующего вида.</span><span class="sxs-lookup"><span data-stu-id="e2c13-241">Add a line similar to the following to the */etc/fstab* file.</span></span> <span data-ttu-id="e2c13-242">Также обратите внимание на то, что ограничения записи можно отключить с помощью *barrier=0*. Это может повысить производительность диска.</span><span class="sxs-lookup"><span data-stu-id="e2c13-242">Also note that write barriers can be disabled using *barrier=0*, this configuration can improve disk performance.</span></span> 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

<span data-ttu-id="e2c13-243">Теперь, когда диск настроен, закройте сеанс SSH.</span><span class="sxs-lookup"><span data-stu-id="e2c13-243">Now that the disk has been configured, close the SSH session.</span></span>

```bash
exit
```

## <a name="resize-vm-disk"></a><span data-ttu-id="e2c13-244">Изменение размера диска виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e2c13-244">Resize VM disk</span></span>

<span data-ttu-id="e2c13-245">После развертывания виртуальной машины можно увеличить размер ее диска операционной системы или любого подключенного диска данных.</span><span class="sxs-lookup"><span data-stu-id="e2c13-245">Once a VM has been deployed, the operating system disk or any attached data disks can be increased in size.</span></span> <span data-ttu-id="e2c13-246">Это удобно, когда требуется больше места для хранения данных или более высокий уровень производительности (P10, P20 и P30).</span><span class="sxs-lookup"><span data-stu-id="e2c13-246">Increasing the size of a disk is beneficial when needing more storage space or a higher level of performance (P10, P20, P30).</span></span> <span data-ttu-id="e2c13-247">Обратите внимание, что уменьшить размер дисков невозможно.</span><span class="sxs-lookup"><span data-stu-id="e2c13-247">Note, disks cannot be decreased in size.</span></span>

<span data-ttu-id="e2c13-248">Прежде чем увеличить размер диска, требуется получить его идентификатор или имя.</span><span class="sxs-lookup"><span data-stu-id="e2c13-248">Before increasing disk size, the Id or name of the disk is needed.</span></span> <span data-ttu-id="e2c13-249">Введите команду [az disk list](/cli/azure/vm/disk#list), чтобы вывести список всех дисков в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e2c13-249">Use the [az disk list](/cli/azure/vm/disk#list) command to return all disks in a resource group.</span></span> <span data-ttu-id="e2c13-250">Запишите имя диска, размер которого вы хотите изменить.</span><span class="sxs-lookup"><span data-stu-id="e2c13-250">Take note of the disk name that you would like to resize.</span></span>

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

<span data-ttu-id="e2c13-251">Обратите внимание, что виртуальная машина должна быть освобождена.</span><span class="sxs-lookup"><span data-stu-id="e2c13-251">The VM must also be deallocated.</span></span> <span data-ttu-id="e2c13-252">Используйте команду [az vm deallocate]( /cli/azure/vm#deallocate), чтобы остановить и освободить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="e2c13-252">Use the [az vm deallocate]( /cli/azure/vm#deallocate) command to stop and deallocate the VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="e2c13-253">Введите команду [az disk update](/cli/azure/vm/disk#update), чтобы изменить размер диска.</span><span class="sxs-lookup"><span data-stu-id="e2c13-253">Use the [az disk update](/cli/azure/vm/disk#update) command to resize the disk.</span></span> <span data-ttu-id="e2c13-254">Приведенный пример увеличивает размер диска *myDataDisk* до 1 ТБ.</span><span class="sxs-lookup"><span data-stu-id="e2c13-254">This example resizes a disk named *myDataDisk* to 1 terabyte.</span></span>

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

<span data-ttu-id="e2c13-255">После завершения операции изменения размера запустите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="e2c13-255">Once the resize operation has completed, start the VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="e2c13-256">Если вы изменили размер диска операционной системы, ее раздел будет автоматически расширен.</span><span class="sxs-lookup"><span data-stu-id="e2c13-256">If you’ve resized the operating system disk, the partition is automatically be expanded.</span></span> <span data-ttu-id="e2c13-257">Если вы изменили размер диска данных, потребуется расширить все текущие разделы в операционной системе виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e2c13-257">If you have resized a data disk, any current partitions need to be expanded in the VMs operating system.</span></span>

## <a name="snapshot-azure-disks"></a><span data-ttu-id="e2c13-258">Создание моментальных снимков дисков Azure по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e2c13-258">Snapshot Azure disks</span></span>

<span data-ttu-id="e2c13-259">При создании моментального снимка диска создается копия диска на определенный момент времени, предназначенная только для чтения.</span><span class="sxs-lookup"><span data-stu-id="e2c13-259">Taking a disk snapshot creates a read only, point-in-time copy of the disk.</span></span> <span data-ttu-id="e2c13-260">Моментальные снимки виртуальной машины Azure можно использовать для быстрого сохранения ее состояния перед изменением конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e2c13-260">Azure VM snapshots are useful for quickly saving the state of a VM before making configuration changes.</span></span> <span data-ttu-id="e2c13-261">В случае изменения конфигурации, оказавшегося нежелательным, состояние виртуальной машины можно восстановить с помощью моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="e2c13-261">In the event the configuration changes prove to be undesired, VM state can be restored using the snapshot.</span></span> <span data-ttu-id="e2c13-262">Если виртуальная машина содержит более одного диска, создается отдельный моментальный снимок каждого диска.</span><span class="sxs-lookup"><span data-stu-id="e2c13-262">When a VM has more than one disk, a snapshot is taken of each disk independently of the others.</span></span> <span data-ttu-id="e2c13-263">Чтобы создать резервные копии с согласованием приложений, рассмотрите возможность остановки виртуальной машины перед созданием моментальных снимков дисков.</span><span class="sxs-lookup"><span data-stu-id="e2c13-263">For taking application consistent backups, consider stopping the VM before taking disk snapshots.</span></span> <span data-ttu-id="e2c13-264">В качестве альтернативы можно использовать [службу архивации Azure](/azure/backup/), которая обеспечивает автоматическую архивацию при запущенной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="e2c13-264">Alternatively, use the [Azure Backup service](/azure/backup/), which enables you to perform automated backups while the VM is running.</span></span>

### <a name="create-snapshot"></a><span data-ttu-id="e2c13-265">Создание моментального снимка</span><span class="sxs-lookup"><span data-stu-id="e2c13-265">Create snapshot</span></span>

<span data-ttu-id="e2c13-266">Перед созданием моментального снимка диска виртуальной машины нужно получить идентификатор или имя этого диска.</span><span class="sxs-lookup"><span data-stu-id="e2c13-266">Before creating a virtual machine disk snapshot, the Id or name of the disk is needed.</span></span> <span data-ttu-id="e2c13-267">Для этого выполните команду [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="e2c13-267">Use the [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) command to return the disk id.</span></span> <span data-ttu-id="e2c13-268">В этом примере идентификатор диска сохраняется в переменной и может использоваться в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="e2c13-268">In this example, the disk id is stored in a variable so that it can be used in a later step.</span></span>

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

<span data-ttu-id="e2c13-269">Получив идентификатор диска виртуальной машины, выполните следующую команду, создающую его моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="e2c13-269">Now that you have the id of the virtual machine disk, the following command creates a snapshot of the disk.</span></span>

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a><span data-ttu-id="e2c13-270">Создание диска на основе моментального снимка</span><span class="sxs-lookup"><span data-stu-id="e2c13-270">Create disk from snapshot</span></span>

<span data-ttu-id="e2c13-271">Этот моментальный снимок можно преобразовать в диск, с помощью которого можно повторно создать виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="e2c13-271">This snapshot can then be converted into a disk, which can be used to recreate the virtual machine.</span></span>

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a><span data-ttu-id="e2c13-272">Восстановление виртуальной машины на основе моментального снимка</span><span class="sxs-lookup"><span data-stu-id="e2c13-272">Restore virtual machine from snapshot</span></span>

<span data-ttu-id="e2c13-273">Чтобы продемонстрировать восстановление виртуальной машины, удалите существующую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="e2c13-273">To demonstrate virtual machine recovery, delete the existing virtual machine.</span></span> 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="e2c13-274">Создайте виртуальную машину на основе диска моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="e2c13-274">Create a new virtual machine from the snapshot disk.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a><span data-ttu-id="e2c13-275">Повторное подключение диска данных</span><span class="sxs-lookup"><span data-stu-id="e2c13-275">Reattach data disk</span></span>

<span data-ttu-id="e2c13-276">Все диски данных нужно повторно подключить к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="e2c13-276">All data disks need to be reattached to the virtual machine.</span></span>

<span data-ttu-id="e2c13-277">Сначала найдите имя диска данных, выполнив команду [az disk list](https://docs.microsoft.com/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="e2c13-277">First find the data disk name using the [az disk list](https://docs.microsoft.com/cli/azure/disk#list) command.</span></span> <span data-ttu-id="e2c13-278">В этом примере имя диска помещается в переменную *datadisk*, которая будет использоваться на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="e2c13-278">This example places the name of the disk in a variable named *datadisk*, which is used in the next step.</span></span>

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

<span data-ttu-id="e2c13-279">Подключите диск, выполнив команду [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach).</span><span class="sxs-lookup"><span data-stu-id="e2c13-279">Use the [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) command to attach the disk.</span></span>

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a><span data-ttu-id="e2c13-280">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e2c13-280">Next steps</span></span>

<span data-ttu-id="e2c13-281">В этом руководстве вы ознакомились с дисками виртуальных машин, а именно с:</span><span class="sxs-lookup"><span data-stu-id="e2c13-281">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e2c13-282">дисками ОС и временными дисками;</span><span class="sxs-lookup"><span data-stu-id="e2c13-282">OS disks and temporary disks</span></span>
> * <span data-ttu-id="e2c13-283">Диски данных</span><span class="sxs-lookup"><span data-stu-id="e2c13-283">Data disks</span></span>
> * <span data-ttu-id="e2c13-284">дисками уровня "Стандартный" и "Премиум";</span><span class="sxs-lookup"><span data-stu-id="e2c13-284">Standard and Premium disks</span></span>
> * <span data-ttu-id="e2c13-285">производительностью дисков;</span><span class="sxs-lookup"><span data-stu-id="e2c13-285">Disk performance</span></span>
> * <span data-ttu-id="e2c13-286">присоединением и подготовкой дисков данных;</span><span class="sxs-lookup"><span data-stu-id="e2c13-286">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="e2c13-287">изменением размеров дисков;</span><span class="sxs-lookup"><span data-stu-id="e2c13-287">Resizing disks</span></span>
> * <span data-ttu-id="e2c13-288">моментальными снимками дисков.</span><span class="sxs-lookup"><span data-stu-id="e2c13-288">Disk snapshots</span></span>

<span data-ttu-id="e2c13-289">Перейдите к следующему руководству, чтобы узнать об автоматической настройке виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e2c13-289">Advance to the next tutorial to learn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e2c13-290">Автоматизация настройки виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e2c13-290">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
