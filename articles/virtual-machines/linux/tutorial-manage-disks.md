---
title: "aaaManage Azure диски с hello Azure CLI | Документы Microsoft"
description: "Учебник - Управление дисками Azure с hello Azure CLI"
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
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a><span data-ttu-id="8b456-103">Управление дисками Azure с hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8b456-103">Manage Azure disks with hello Azure CLI</span></span>

<span data-ttu-id="8b456-104">Виртуальные машины Azure используют диски toostore hello виртуальные машины операционной системы, приложений и данных.</span><span class="sxs-lookup"><span data-stu-id="8b456-104">Azure virtual machines use disks toostore hello VMs operating system, applications, and data.</span></span> <span data-ttu-id="8b456-105">При создании виртуальной Машины это важно toochoose размер диска и рабочей нагрузки соответствующие toohello ожидается конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8b456-105">When creating a VM it is important toochoose a disk size and configuration appropriate toohello expected workload.</span></span> <span data-ttu-id="8b456-106">В этом руководстве рассматривается развертывание дисков виртуальных машин и управление ими.</span><span class="sxs-lookup"><span data-stu-id="8b456-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="8b456-107">Здесь содержатся сведения о:</span><span class="sxs-lookup"><span data-stu-id="8b456-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8b456-108">дисках ОС и временных дисках;</span><span class="sxs-lookup"><span data-stu-id="8b456-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="8b456-109">Диски данных</span><span class="sxs-lookup"><span data-stu-id="8b456-109">Data disks</span></span>
> * <span data-ttu-id="8b456-110">дисками уровня "Стандартный" и "Премиум";</span><span class="sxs-lookup"><span data-stu-id="8b456-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="8b456-111">производительностью дисков;</span><span class="sxs-lookup"><span data-stu-id="8b456-111">Disk performance</span></span>
> * <span data-ttu-id="8b456-112">присоединением и подготовкой дисков данных;</span><span class="sxs-lookup"><span data-stu-id="8b456-112">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="8b456-113">изменением размеров дисков;</span><span class="sxs-lookup"><span data-stu-id="8b456-113">Resizing disks</span></span>
> * <span data-ttu-id="8b456-114">моментальными снимками дисков.</span><span class="sxs-lookup"><span data-stu-id="8b456-114">Disk snapshots</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8b456-115">Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="8b456-115">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="8b456-116">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="8b456-116">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8b456-117">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8b456-117">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="default-azure-disks"></a><span data-ttu-id="8b456-118">Диски Azure по умолчанию</span><span class="sxs-lookup"><span data-stu-id="8b456-118">Default Azure disks</span></span>

<span data-ttu-id="8b456-119">При создании виртуальной машины Azure двух дисков являются toohello автоматически подключенных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="8b456-119">When an Azure virtual machine is created, two disks are automatically attached toohello virtual machine.</span></span> 

<span data-ttu-id="8b456-120">**Диск операционной системы** - дисков операционной системы можно изменять, но копирование too1 терабайт и узлы hello операционной системы виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="8b456-120">**Operating system disk** - Operating system disks can be sized up too1 terabyte, and hosts hello VMs operating system.</span></span> <span data-ttu-id="8b456-121">диск ОС Hello помечается */dev/sda* по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8b456-121">hello OS disk is labeled */dev/sda* by default.</span></span> <span data-ttu-id="8b456-122">кэширование конфигурацию диска ОС hello диска Hello оптимизирован для работы операционной системы.</span><span class="sxs-lookup"><span data-stu-id="8b456-122">hello disk caching configuration of hello OS disk is optimized for OS performance.</span></span> <span data-ttu-id="8b456-123">Из-за этой конфигурации hello диска ОС **не должны** размещения приложений или данных.</span><span class="sxs-lookup"><span data-stu-id="8b456-123">Because of this configuration, hello OS disk **should not** host applications or data.</span></span> <span data-ttu-id="8b456-124">Для приложений и данных используйте диски данных, которые описаны далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="8b456-124">For applications and data, use data disks, which are detailed later in this article.</span></span> 

<span data-ttu-id="8b456-125">**Временный диск** -временные диски используют твердотельного накопителя, которая находится на hello же Azure узле hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8b456-125">**Temporary disk** - Temporary disks use a solid-state drive that is located on hello same Azure host as hello VM.</span></span> <span data-ttu-id="8b456-126">Временные диски обладают высокой производительностью и могут быть использованы для таких операций, как обработка временных данных.</span><span class="sxs-lookup"><span data-stu-id="8b456-126">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="8b456-127">Данные, хранящиеся на временный диск удаляется, если hello виртуальной Машины, перемещенные tooa новый узел.</span><span class="sxs-lookup"><span data-stu-id="8b456-127">However, if hello VM is moved tooa new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="8b456-128">размер Hello hello временного диска определяется hello размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8b456-128">hello size of hello temporary disk is determined by hello VM size.</span></span> <span data-ttu-id="8b456-129">Временные диски помечаются как */dev/sdb* и используют точку подключения */mnt*.</span><span class="sxs-lookup"><span data-stu-id="8b456-129">Temporary disks are labeled */dev/sdb* and have a mountpoint of */mnt*.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="8b456-130">Размеры временных дисков</span><span class="sxs-lookup"><span data-stu-id="8b456-130">Temporary disk sizes</span></span>

| <span data-ttu-id="8b456-131">Тип</span><span class="sxs-lookup"><span data-stu-id="8b456-131">Type</span></span> | <span data-ttu-id="8b456-132">Размер виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="8b456-132">VM Size</span></span> | <span data-ttu-id="8b456-133">Максимальный размер временного диска (ГБ)</span><span class="sxs-lookup"><span data-stu-id="8b456-133">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="8b456-134">Универсальные</span><span class="sxs-lookup"><span data-stu-id="8b456-134">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="8b456-135">Серии A и D</span><span class="sxs-lookup"><span data-stu-id="8b456-135">A and D series</span></span> | <span data-ttu-id="8b456-136">800</span><span class="sxs-lookup"><span data-stu-id="8b456-136">800</span></span> |
| [<span data-ttu-id="8b456-137">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="8b456-137">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="8b456-138">Серия F</span><span class="sxs-lookup"><span data-stu-id="8b456-138">F series</span></span> | <span data-ttu-id="8b456-139">800</span><span class="sxs-lookup"><span data-stu-id="8b456-139">800</span></span> |
| [<span data-ttu-id="8b456-140">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="8b456-140">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="8b456-141">Серии D и G</span><span class="sxs-lookup"><span data-stu-id="8b456-141">D and G series</span></span> | <span data-ttu-id="8b456-142">6144</span><span class="sxs-lookup"><span data-stu-id="8b456-142">6144</span></span> |
| [<span data-ttu-id="8b456-143">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="8b456-143">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="8b456-144">Серия L</span><span class="sxs-lookup"><span data-stu-id="8b456-144">L series</span></span> | <span data-ttu-id="8b456-145">5630</span><span class="sxs-lookup"><span data-stu-id="8b456-145">5630</span></span> |
| [<span data-ttu-id="8b456-146">GPU</span><span class="sxs-lookup"><span data-stu-id="8b456-146">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="8b456-147">Серия N</span><span class="sxs-lookup"><span data-stu-id="8b456-147">N series</span></span> | <span data-ttu-id="8b456-148">1440</span><span class="sxs-lookup"><span data-stu-id="8b456-148">1440</span></span> |
| [<span data-ttu-id="8b456-149">Высокопроизводительные</span><span class="sxs-lookup"><span data-stu-id="8b456-149">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="8b456-150">Серии A и H</span><span class="sxs-lookup"><span data-stu-id="8b456-150">A and H series</span></span> | <span data-ttu-id="8b456-151">2000</span><span class="sxs-lookup"><span data-stu-id="8b456-151">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="8b456-152">Диски данных Azure</span><span class="sxs-lookup"><span data-stu-id="8b456-152">Azure data disks</span></span>

<span data-ttu-id="8b456-153">Вы можете добавить дополнительные диски данных, чтобы установить приложения и хранить данные.</span><span class="sxs-lookup"><span data-stu-id="8b456-153">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="8b456-154">Диски данных следует использовать в любой ситуации, где требуется надежное хранилище данных, обеспечивающее высокую скорость реагирования.</span><span class="sxs-lookup"><span data-stu-id="8b456-154">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="8b456-155">Максимальная емкость каждого диска данных составляет 1 ТБ.</span><span class="sxs-lookup"><span data-stu-id="8b456-155">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="8b456-156">Hello размера виртуальной машины hello определяет число дисков может быть tooa подключенных виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="8b456-156">hello size of hello virtual machine determines how many data disks can be attached tooa VM.</span></span> <span data-ttu-id="8b456-157">Для каждого ядра виртуальной машины можно подключить два диска данных.</span><span class="sxs-lookup"><span data-stu-id="8b456-157">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="8b456-158">Максимальное число дисков данных на виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="8b456-158">Max data disks per VM</span></span>

| <span data-ttu-id="8b456-159">Тип</span><span class="sxs-lookup"><span data-stu-id="8b456-159">Type</span></span> | <span data-ttu-id="8b456-160">Размер виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="8b456-160">VM Size</span></span> | <span data-ttu-id="8b456-161">Максимальное число дисков данных на виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="8b456-161">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="8b456-162">Универсальные</span><span class="sxs-lookup"><span data-stu-id="8b456-162">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="8b456-163">Серии A и D</span><span class="sxs-lookup"><span data-stu-id="8b456-163">A and D series</span></span> | <span data-ttu-id="8b456-164">32</span><span class="sxs-lookup"><span data-stu-id="8b456-164">32</span></span> |
| [<span data-ttu-id="8b456-165">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="8b456-165">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="8b456-166">Серия F</span><span class="sxs-lookup"><span data-stu-id="8b456-166">F series</span></span> | <span data-ttu-id="8b456-167">32</span><span class="sxs-lookup"><span data-stu-id="8b456-167">32</span></span> |
| [<span data-ttu-id="8b456-168">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="8b456-168">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="8b456-169">Серии D и G</span><span class="sxs-lookup"><span data-stu-id="8b456-169">D and G series</span></span> | <span data-ttu-id="8b456-170">64</span><span class="sxs-lookup"><span data-stu-id="8b456-170">64</span></span> |
| [<span data-ttu-id="8b456-171">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="8b456-171">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="8b456-172">Серия L</span><span class="sxs-lookup"><span data-stu-id="8b456-172">L series</span></span> | <span data-ttu-id="8b456-173">64</span><span class="sxs-lookup"><span data-stu-id="8b456-173">64</span></span> |
| [<span data-ttu-id="8b456-174">GPU</span><span class="sxs-lookup"><span data-stu-id="8b456-174">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="8b456-175">Серия N</span><span class="sxs-lookup"><span data-stu-id="8b456-175">N series</span></span> | <span data-ttu-id="8b456-176">48</span><span class="sxs-lookup"><span data-stu-id="8b456-176">48</span></span> |
| [<span data-ttu-id="8b456-177">Высокопроизводительные</span><span class="sxs-lookup"><span data-stu-id="8b456-177">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="8b456-178">Серии A и H</span><span class="sxs-lookup"><span data-stu-id="8b456-178">A and H series</span></span> | <span data-ttu-id="8b456-179">32</span><span class="sxs-lookup"><span data-stu-id="8b456-179">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="8b456-180">Типы дисков виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="8b456-180">VM disk types</span></span>

<span data-ttu-id="8b456-181">В Azure предоставляются диски двух типов.</span><span class="sxs-lookup"><span data-stu-id="8b456-181">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="8b456-182">Диск уровня "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="8b456-182">Standard disk</span></span>

<span data-ttu-id="8b456-183">Хранилище класса Standard использует жесткие диски и обеспечивает экономичное хранилище с достаточной производительностью.</span><span class="sxs-lookup"><span data-stu-id="8b456-183">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="8b456-184">Эти диски идеально подходят для экономных рабочих нагрузок разработки и тестирования.</span><span class="sxs-lookup"><span data-stu-id="8b456-184">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="8b456-185">Диск уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="8b456-185">Premium disk</span></span>

<span data-ttu-id="8b456-186">Диски уровня "Премиум" используют высокопроизводительные твердотельные накопители с низкой задержкой.</span><span class="sxs-lookup"><span data-stu-id="8b456-186">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="8b456-187">Они идеально подходят для виртуальных машин, выполняющих производственную рабочую нагрузку.</span><span class="sxs-lookup"><span data-stu-id="8b456-187">Perfect for VMs running production workload.</span></span> <span data-ttu-id="8b456-188">Хранилище уровня "Премиум" поддерживает виртуальные машины серий DS, DSv2, GS и FS.</span><span class="sxs-lookup"><span data-stu-id="8b456-188">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="8b456-189">Диски Premium бывают трех типов (P10 P20, P30), размер диска hello hello определяет тип диска hello.</span><span class="sxs-lookup"><span data-stu-id="8b456-189">Premium disks come in three types (P10, P20, P30), hello size of hello disk determines hello disk type.</span></span> <span data-ttu-id="8b456-190">При выборе, следующий тип toohello округляется hello значение размера диска.</span><span class="sxs-lookup"><span data-stu-id="8b456-190">When selecting, a disk size hello value is rounded up toohello next type.</span></span> <span data-ttu-id="8b456-191">Например если размер диска hello не превышает 128 ГБ, hello используется диск P10.</span><span class="sxs-lookup"><span data-stu-id="8b456-191">For example, if hello disk size is less than 128 GB, hello disk type is P10.</span></span> <span data-ttu-id="8b456-192">Если размер диска hello между 129 и 512 ГБ, размер hello — P20.</span><span class="sxs-lookup"><span data-stu-id="8b456-192">If hello disk size is between 129 GB and 512 GB, hello size is a P20.</span></span> <span data-ttu-id="8b456-193">Ничего более 512 ГБ, размер hello — P30.</span><span class="sxs-lookup"><span data-stu-id="8b456-193">Anything over 512 GB, hello size is a P30.</span></span>

### <a name="premium-disk-performance"></a><span data-ttu-id="8b456-194">Производительность диска уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="8b456-194">Premium disk performance</span></span>

|<span data-ttu-id="8b456-195">Тип диска хранилища уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="8b456-195">Premium storage disk type</span></span> | <span data-ttu-id="8b456-196">P10</span><span class="sxs-lookup"><span data-stu-id="8b456-196">P10</span></span> | <span data-ttu-id="8b456-197">P20</span><span class="sxs-lookup"><span data-stu-id="8b456-197">P20</span></span> | <span data-ttu-id="8b456-198">P30</span><span class="sxs-lookup"><span data-stu-id="8b456-198">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8b456-199">Размер диска (округленный в большую сторону)</span><span class="sxs-lookup"><span data-stu-id="8b456-199">Disk size (round up)</span></span> | <span data-ttu-id="8b456-200">128 ГБ</span><span class="sxs-lookup"><span data-stu-id="8b456-200">128 GB</span></span> | <span data-ttu-id="8b456-201">512 ГБ</span><span class="sxs-lookup"><span data-stu-id="8b456-201">512 GB</span></span> | <span data-ttu-id="8b456-202">1024 ГБ (1 ТБ)</span><span class="sxs-lookup"><span data-stu-id="8b456-202">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="8b456-203">Макс. количество операций ввода-вывода в секунду на диск</span><span class="sxs-lookup"><span data-stu-id="8b456-203">Max IOPS per disk</span></span> | <span data-ttu-id="8b456-204">500</span><span class="sxs-lookup"><span data-stu-id="8b456-204">500</span></span> | <span data-ttu-id="8b456-205">2300</span><span class="sxs-lookup"><span data-stu-id="8b456-205">2,300</span></span> | <span data-ttu-id="8b456-206">5 000</span><span class="sxs-lookup"><span data-stu-id="8b456-206">5,000</span></span> |
<span data-ttu-id="8b456-207">Пропускная способность на диск</span><span class="sxs-lookup"><span data-stu-id="8b456-207">Throughput per disk</span></span> | <span data-ttu-id="8b456-208">100 МБ/с</span><span class="sxs-lookup"><span data-stu-id="8b456-208">100 MB/s</span></span> | <span data-ttu-id="8b456-209">150 МБ/с</span><span class="sxs-lookup"><span data-stu-id="8b456-209">150 MB/s</span></span> | <span data-ttu-id="8b456-210">200 МБ/с</span><span class="sxs-lookup"><span data-stu-id="8b456-210">200 MB/s</span></span> |

<span data-ttu-id="8b456-211">Хотя hello над таблицей идентифицирует max IOP для дисков, более высокий уровень производительности достигается путем чередования несколько дисков данных.</span><span class="sxs-lookup"><span data-stu-id="8b456-211">While hello above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="8b456-212">Например, виртуальная машина Standard_GS5 может достичь 80 000 операций ввода-вывода в секунду.</span><span class="sxs-lookup"><span data-stu-id="8b456-212">For instance, a Standard_GS5 VM can achieve a maximum of 80,000 IOPS.</span></span> <span data-ttu-id="8b456-213">Дополнительные сведения о максимальных количествах операций ввода-вывода в секунду для виртуальных машин см. в разделе [Размеры виртуальных машин Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="8b456-213">For detailed information on max IOPS per VM, see [Linux VM sizes](sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="8b456-214">Создание и подключение дисков</span><span class="sxs-lookup"><span data-stu-id="8b456-214">Create and attach disks</span></span>

<span data-ttu-id="8b456-215">Диски данных можно создать и присоединенного во время создания виртуальной Машины или tooan существующей виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8b456-215">Data disks can be created and attached at VM creation time or tooan existing VM.</span></span>

### <a name="attach-disk-at-vm-creation"></a><span data-ttu-id="8b456-216">Подключение диска при создании виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="8b456-216">Attach disk at VM creation</span></span>

<span data-ttu-id="8b456-217">Создание группы ресурсов с hello [Создание группы az](https://docs.microsoft.com/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="8b456-217">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

<span data-ttu-id="8b456-218">Создайте виртуальную Машину с помощью hello [создания виртуальной машины az]( /cli/azure/vm#create) команды.</span><span class="sxs-lookup"><span data-stu-id="8b456-218">Create a VM using hello [az vm create]( /cli/azure/vm#create) command.</span></span> <span data-ttu-id="8b456-219">Hello `--datadisk-sizes-gb` аргумент является используется toospecify, что дополнительный диск должен быть создан и присоединенного toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8b456-219">hello `--datadisk-sizes-gb` argument is used toospecify that an additional disk should be created and attached toohello virtual machine.</span></span> <span data-ttu-id="8b456-220">toocreate и присоединить несколько дисков, используйте несколько значений размера диска.</span><span class="sxs-lookup"><span data-stu-id="8b456-220">toocreate and attach more than one disk, use a space-delimited list of disk size values.</span></span> <span data-ttu-id="8b456-221">В следующем примере hello виртуальная машина создается с дисками данных, оба 128 ГБ.</span><span class="sxs-lookup"><span data-stu-id="8b456-221">In hello following example, a VM is created with two data disks, both 128 GB.</span></span> <span data-ttu-id="8b456-222">Поскольку размеры дисков hello 128 ГБ, эти диски настроены как P10s, содержащие максимальное 500 операций ввода-ВЫВОДА на диске.</span><span class="sxs-lookup"><span data-stu-id="8b456-222">Because hello disk sizes are 128 GB, these disks are both configured as P10s, which provide maximum 500 IOPS per disk.</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a><span data-ttu-id="8b456-223">Присоединить диск tooexisting виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="8b456-223">Attach disk tooexisting VM</span></span>

<span data-ttu-id="8b456-224">toocreate и присоединить новый диск tooan существующей виртуальной машины, используйте hello [присоединить диск виртуальной машины az](/cli/azure/vm/disk#attach) команды.</span><span class="sxs-lookup"><span data-stu-id="8b456-224">toocreate and attach a new disk tooan existing virtual machine, use hello [az vm disk attach](/cli/azure/vm/disk#attach) command.</span></span> <span data-ttu-id="8b456-225">Hello следующий пример создает диск с premium 128 гигабайт и привязывает его toohello создания виртуальной Машины на последнем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="8b456-225">hello following example creates a premium disk, 128 gigabytes in size, and attaches it toohello VM created in hello last step.</span></span>

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a><span data-ttu-id="8b456-226">Подготовка дисков данных</span><span class="sxs-lookup"><span data-stu-id="8b456-226">Prepare data disks</span></span>

<span data-ttu-id="8b456-227">После диск toohello подключенных виртуальных машин, hello операционной системы должен настроить toobe toouse hello диска.</span><span class="sxs-lookup"><span data-stu-id="8b456-227">Once a disk has been attached toohello virtual machine, hello operating system needs toobe configured toouse hello disk.</span></span> <span data-ttu-id="8b456-228">Hello в следующем примере показано, как toomanually Настройка диска.</span><span class="sxs-lookup"><span data-stu-id="8b456-228">hello following example shows how toomanually configure a disk.</span></span> <span data-ttu-id="8b456-229">Этот процесс можно автоматизировать с помощью cloud-init, как описывается в [этом руководстве](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="8b456-229">This process can also be automated using cloud-init, which is covered in a [later tutorial](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="8b456-230">Настройка вручную</span><span class="sxs-lookup"><span data-stu-id="8b456-230">Manual configuration</span></span>

<span data-ttu-id="8b456-231">Создайте SSH-подключения с hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8b456-231">Create an SSH connection with hello virtual machine.</span></span> <span data-ttu-id="8b456-232">Замените hello общедоступный IP-адрес виртуальной машины hello hello примере IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="8b456-232">Replace hello example IP address with hello public IP of hello virtual machine.</span></span>

```azurecli-interactive 
ssh 52.174.34.95
```

<span data-ttu-id="8b456-233">Создать разделы на диске hello с `fdisk`.</span><span class="sxs-lookup"><span data-stu-id="8b456-233">Partition hello disk with `fdisk`.</span></span>

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="8b456-234">Запись toohello системного раздела в файл с помощью hello `mkfs` команды.</span><span class="sxs-lookup"><span data-stu-id="8b456-234">Write a file system toohello partition by using hello `mkfs` command.</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="8b456-235">Подключите новый диск hello, чтобы она доступна в операционной системе hello.</span><span class="sxs-lookup"><span data-stu-id="8b456-235">Mount hello new disk so that it is accessible in hello operating system.</span></span>

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="8b456-236">диск Hello, теперь доступны через hello *datadrive* монтирования по умолчанию, который можно проверить, запустив hello `df -h` команды.</span><span class="sxs-lookup"><span data-stu-id="8b456-236">hello disk can now be accessed through hello *datadrive* mountpoint, which can be verified by running hello `df -h` command.</span></span> 

```bash
df -h
```

<span data-ttu-id="8b456-237">Hello видно hello новый диск подключается к */datadrive*.</span><span class="sxs-lookup"><span data-stu-id="8b456-237">hello output shows hello new drive mounted on */datadrive*.</span></span>

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

<span data-ttu-id="8b456-238">tooensure, hello диск будет подключена снова после перезагрузки, его необходимо добавить toohello */etc/fstab* файла.</span><span class="sxs-lookup"><span data-stu-id="8b456-238">tooensure that hello drive is remounted after a reboot, it must be added toohello */etc/fstab* file.</span></span> <span data-ttu-id="8b456-239">toodo таким образом, получить hello UUID диска hello с hello `blkid` программы.</span><span class="sxs-lookup"><span data-stu-id="8b456-239">toodo so, get hello UUID of hello disk with hello `blkid` utility.</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="8b456-240">Вывод Hello отображает hello UUID диска hello `/dev/sdc1` в этом случае.</span><span class="sxs-lookup"><span data-stu-id="8b456-240">hello output displays hello UUID of hello drive, `/dev/sdc1` in this case.</span></span>

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

<span data-ttu-id="8b456-241">Добавление строки аналогично toohello, следуя toohello */etc/fstab* файла.</span><span class="sxs-lookup"><span data-stu-id="8b456-241">Add a line similar toohello following toohello */etc/fstab* file.</span></span> <span data-ttu-id="8b456-242">Также обратите внимание на то, что ограничения записи можно отключить с помощью *barrier=0*. Это может повысить производительность диска.</span><span class="sxs-lookup"><span data-stu-id="8b456-242">Also note that write barriers can be disabled using *barrier=0*, this configuration can improve disk performance.</span></span> 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

<span data-ttu-id="8b456-243">Теперь, когда hello диск был настроен, закройте сеанс SSH hello.</span><span class="sxs-lookup"><span data-stu-id="8b456-243">Now that hello disk has been configured, close hello SSH session.</span></span>

```bash
exit
```

## <a name="resize-vm-disk"></a><span data-ttu-id="8b456-244">Изменение размера диска виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="8b456-244">Resize VM disk</span></span>

<span data-ttu-id="8b456-245">После развертывания виртуальной Машины диск операционной системы hello или все подключенные диски данных можно увеличить размер.</span><span class="sxs-lookup"><span data-stu-id="8b456-245">Once a VM has been deployed, hello operating system disk or any attached data disks can be increased in size.</span></span> <span data-ttu-id="8b456-246">Увеличение размера hello диска полезно в том случае, при необходимости использовать больший объем памяти или более высокий уровень производительности (P10, P20, P30).</span><span class="sxs-lookup"><span data-stu-id="8b456-246">Increasing hello size of a disk is beneficial when needing more storage space or a higher level of performance (P10, P20, P30).</span></span> <span data-ttu-id="8b456-247">Обратите внимание, что уменьшить размер дисков невозможно.</span><span class="sxs-lookup"><span data-stu-id="8b456-247">Note, disks cannot be decreased in size.</span></span>

<span data-ttu-id="8b456-248">До увеличения места на диске, Здравствуйте, идентификатор или требуется указать имя диска hello.</span><span class="sxs-lookup"><span data-stu-id="8b456-248">Before increasing disk size, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="8b456-249">Используйте hello [список дисков az](/cli/azure/vm/disk#list) команда tooreturn все диски в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8b456-249">Use hello [az disk list](/cli/azure/vm/disk#list) command tooreturn all disks in a resource group.</span></span> <span data-ttu-id="8b456-250">Запишите имя диска hello, желательно tooresize.</span><span class="sxs-lookup"><span data-stu-id="8b456-250">Take note of hello disk name that you would like tooresize.</span></span>

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

<span data-ttu-id="8b456-251">Hello виртуальной Машины также должен быть освобождена.</span><span class="sxs-lookup"><span data-stu-id="8b456-251">hello VM must also be deallocated.</span></span> <span data-ttu-id="8b456-252">Используйте hello [ВМ az deallocate]( /cli/azure/vm#deallocate) команды toostop и освобождать hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8b456-252">Use hello [az vm deallocate]( /cli/azure/vm#deallocate) command toostop and deallocate hello VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="8b456-253">Используйте hello [обновление диска az](/cli/azure/vm/disk#update) команда tooresize hello диска.</span><span class="sxs-lookup"><span data-stu-id="8b456-253">Use hello [az disk update](/cli/azure/vm/disk#update) command tooresize hello disk.</span></span> <span data-ttu-id="8b456-254">Этот пример изменяет размер диска с именем *myDataDisk* too1 терабайт.</span><span class="sxs-lookup"><span data-stu-id="8b456-254">This example resizes a disk named *myDataDisk* too1 terabyte.</span></span>

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

<span data-ttu-id="8b456-255">После завершения операции изменения размера hello, запустите hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8b456-255">Once hello resize operation has completed, start hello VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="8b456-256">Если вы изменили размер hello операционной системы диска, раздел hello автоматически расширяется.</span><span class="sxs-lookup"><span data-stu-id="8b456-256">If you’ve resized hello operating system disk, hello partition is automatically be expanded.</span></span> <span data-ttu-id="8b456-257">Если изменения размера диска данных, все текущие секции должны toobe развернуты в операционной системе hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="8b456-257">If you have resized a data disk, any current partitions need toobe expanded in hello VMs operating system.</span></span>

## <a name="snapshot-azure-disks"></a><span data-ttu-id="8b456-258">Создание моментальных снимков дисков Azure по умолчанию</span><span class="sxs-lookup"><span data-stu-id="8b456-258">Snapshot Azure disks</span></span>

<span data-ttu-id="8b456-259">Создание снимка диск создает чтения только в момент копию hello диска.</span><span class="sxs-lookup"><span data-stu-id="8b456-259">Taking a disk snapshot creates a read only, point-in-time copy of hello disk.</span></span> <span data-ttu-id="8b456-260">Моментальные снимки виртуальной Машины Azure можно использовать для быстрого сохранение состояния hello виртуальной машины перед изменением конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8b456-260">Azure VM snapshots are useful for quickly saving hello state of a VM before making configuration changes.</span></span> <span data-ttu-id="8b456-261">В событии hello hello изменения конфигурации доказать toobe нежелательным, состояние виртуальной Машины можно восстановить с помощью моментального снимка hello.</span><span class="sxs-lookup"><span data-stu-id="8b456-261">In hello event hello configuration changes prove toobe undesired, VM state can be restored using hello snapshot.</span></span> <span data-ttu-id="8b456-262">Если виртуальная машина имеет более одного диска, моментальный снимок каждого диска, независимо от hello другим пользователям.</span><span class="sxs-lookup"><span data-stu-id="8b456-262">When a VM has more than one disk, a snapshot is taken of each disk independently of hello others.</span></span> <span data-ttu-id="8b456-263">Для подсчета согласованных копий приложения, рассмотрите возможность остановки hello виртуальной Машины перед созданием моментальных снимков диска.</span><span class="sxs-lookup"><span data-stu-id="8b456-263">For taking application consistent backups, consider stopping hello VM before taking disk snapshots.</span></span> <span data-ttu-id="8b456-264">Можно также использовать hello [службы архивации Azure](/azure/backup/), который позволит вам tooperform автоматическое резервное копирование, при запущенной виртуальной Машине hello.</span><span class="sxs-lookup"><span data-stu-id="8b456-264">Alternatively, use hello [Azure Backup service](/azure/backup/), which enables you tooperform automated backups while hello VM is running.</span></span>

### <a name="create-snapshot"></a><span data-ttu-id="8b456-265">Создание моментального снимка</span><span class="sxs-lookup"><span data-stu-id="8b456-265">Create snapshot</span></span>

<span data-ttu-id="8b456-266">Перед созданием моментального снимка виртуальной машины диск, hello идентификатор или имя диска hello необходим.</span><span class="sxs-lookup"><span data-stu-id="8b456-266">Before creating a virtual machine disk snapshot, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="8b456-267">Используйте hello [Показать ВМ az](https://docs.microsoft.com/en-us/cli/azure/vm#show) диска с идентификатором hello tooreturn команды. В этом примере диска с идентификатором hello хранится в переменной, чтобы он может использоваться в дальнейшем.</span><span class="sxs-lookup"><span data-stu-id="8b456-267">Use hello [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) command tooreturn hello disk id. In this example, hello disk id is stored in a variable so that it can be used in a later step.</span></span>

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

<span data-ttu-id="8b456-268">Теперь, когда идентификатор hello диска виртуальной машины hello hello следующая команда создает моментальный снимок hello диска.</span><span class="sxs-lookup"><span data-stu-id="8b456-268">Now that you have hello id of hello virtual machine disk, hello following command creates a snapshot of hello disk.</span></span>

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a><span data-ttu-id="8b456-269">Создание диска на основе моментального снимка</span><span class="sxs-lookup"><span data-stu-id="8b456-269">Create disk from snapshot</span></span>

<span data-ttu-id="8b456-270">Затем этот моментальный снимок может быть преобразован в диск, который можно использовать toorecreate hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8b456-270">This snapshot can then be converted into a disk, which can be used toorecreate hello virtual machine.</span></span>

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a><span data-ttu-id="8b456-271">Восстановление виртуальной машины на основе моментального снимка</span><span class="sxs-lookup"><span data-stu-id="8b456-271">Restore virtual machine from snapshot</span></span>

<span data-ttu-id="8b456-272">восстановление виртуальных машин toodemonstrate delete hello существующей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8b456-272">toodemonstrate virtual machine recovery, delete hello existing virtual machine.</span></span> 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="8b456-273">Создайте новую виртуальную машину с диска hello моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="8b456-273">Create a new virtual machine from hello snapshot disk.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a><span data-ttu-id="8b456-274">Повторное подключение диска данных</span><span class="sxs-lookup"><span data-stu-id="8b456-274">Reattach data disk</span></span>

<span data-ttu-id="8b456-275">Все диски с данными необходимо повторно присоединить toobe toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8b456-275">All data disks need toobe reattached toohello virtual machine.</span></span>

<span data-ttu-id="8b456-276">Сначала найти имя диска данных hello, с помощью hello [список дисков az](https://docs.microsoft.com/cli/azure/disk#list) команды.</span><span class="sxs-lookup"><span data-stu-id="8b456-276">First find hello data disk name using hello [az disk list](https://docs.microsoft.com/cli/azure/disk#list) command.</span></span> <span data-ttu-id="8b456-277">В этом примере имя диска hello в переменной с именем hello местах *datadisk*, которое используется в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="8b456-277">This example places hello name of hello disk in a variable named *datadisk*, which is used in hello next step.</span></span>

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

<span data-ttu-id="8b456-278">Используйте hello [присоединить диск виртуальной машины az](https://docs.microsoft.com/cli/azure/vm/disk#attach) команда tooattach hello диска.</span><span class="sxs-lookup"><span data-stu-id="8b456-278">Use hello [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) command tooattach hello disk.</span></span>

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a><span data-ttu-id="8b456-279">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8b456-279">Next steps</span></span>

<span data-ttu-id="8b456-280">В этом руководстве вы ознакомились с дисками виртуальных машин, а именно с:</span><span class="sxs-lookup"><span data-stu-id="8b456-280">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8b456-281">дисками ОС и временными дисками;</span><span class="sxs-lookup"><span data-stu-id="8b456-281">OS disks and temporary disks</span></span>
> * <span data-ttu-id="8b456-282">Диски данных</span><span class="sxs-lookup"><span data-stu-id="8b456-282">Data disks</span></span>
> * <span data-ttu-id="8b456-283">дисками уровня "Стандартный" и "Премиум";</span><span class="sxs-lookup"><span data-stu-id="8b456-283">Standard and Premium disks</span></span>
> * <span data-ttu-id="8b456-284">производительностью дисков;</span><span class="sxs-lookup"><span data-stu-id="8b456-284">Disk performance</span></span>
> * <span data-ttu-id="8b456-285">присоединением и подготовкой дисков данных;</span><span class="sxs-lookup"><span data-stu-id="8b456-285">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="8b456-286">изменением размеров дисков;</span><span class="sxs-lookup"><span data-stu-id="8b456-286">Resizing disks</span></span>
> * <span data-ttu-id="8b456-287">моментальными снимками дисков.</span><span class="sxs-lookup"><span data-stu-id="8b456-287">Disk snapshots</span></span>

<span data-ttu-id="8b456-288">Переместить следующий учебник toolearn toohello об автоматической конфигурации виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8b456-288">Advance toohello next tutorial toolearn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8b456-289">Автоматизация настройки виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="8b456-289">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
