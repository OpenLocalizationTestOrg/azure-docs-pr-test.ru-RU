---
title: "Перенос классической виртуальной машины в виртуальную машину ARM с управляемыми дисками | Документация Майкрософт"
description: "Миграция отдельной виртуальной машины из классической модели развертывания на Управляемые диски Azure в модели развертывания с помощью Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 82389834d85981c0ed71bdcc891fbfdbe1377654
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="manually-migrate-a-classic-vm-to-a-new-arm-managed-disk-vm-from-the-vhd"></a><span data-ttu-id="4b0e3-103">Ручная миграция классической виртуальной машины в новую виртуальную машину ARM с управляемыми дисками с помощью VHD</span><span class="sxs-lookup"><span data-stu-id="4b0e3-103">Manually migrate a Classic VM to a new ARM Managed Disk VM from the VHD</span></span> 


<span data-ttu-id="4b0e3-104">Этот раздел поможет перенести имеющиеся виртуальные машины из классической модели развертывания на [Управляемые диски](managed-disks-overview.md) в модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-104">This section helps you to migrate your existing Azure VMs from the classic deployment model to [Managed Disks](managed-disks-overview.md) in the Resource Manager deployment model.</span></span>


## <a name="plan-for-the-migration-to-managed-disks"></a><span data-ttu-id="4b0e3-105">Планирование миграции на управляемые диски</span><span class="sxs-lookup"><span data-stu-id="4b0e3-105">Plan for the migration to Managed Disks</span></span>

<span data-ttu-id="4b0e3-106">Этот раздел поможет выбрать соответствующие виртуальные машины и типы дисков.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-106">This section helps you to make the best decision on VM and disk types.</span></span>


### <a name="location"></a><span data-ttu-id="4b0e3-107">Расположение</span><span class="sxs-lookup"><span data-stu-id="4b0e3-107">Location</span></span>

<span data-ttu-id="4b0e3-108">Выберите расположение, в котором доступны Управляемые диски Azure.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-108">Pick a location where Azure Managed Disks are available.</span></span> <span data-ttu-id="4b0e3-109">Если миграция выполняется на управляемые диски уровня "Премиум", то в этом регионе должно быть также доступно хранилище уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="4b0e3-109">If you are migrating to Premium Managed Disks, also ensure that Premium storage is available in the region where you are planning to migrate to.</span></span> <span data-ttu-id="4b0e3-110">Актуальные сведения о поддерживаемых расположениях см. на странице [Доступность продуктов по регионам](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="4b0e3-110">See [Azure Services byRegion](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="4b0e3-111">Размеры виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="4b0e3-111">VM sizes</span></span>

<span data-ttu-id="4b0e3-112">Если миграция выполняется на управляемые диски уровня "Премиум", то необходимо выбрать для виртуальной машины размер, поддерживающий хранилище уровня "Премиум", из числа доступных в регионе размещения виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-112">If you are migrating to Premium Managed Disks, you have to update the size of the VM to Premium Storage capable size available in the region where VM is located.</span></span> <span data-ttu-id="4b0e3-113">Изучите размеры виртуальных машин, чтобы выбрать подходящий для хранилища уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="4b0e3-113">Review the VM sizes that are Premium Storage capable.</span></span> <span data-ttu-id="4b0e3-114">Спецификации размеров виртуальных машин Azure перечислены в статье [Размеры виртуальных машин](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="4b0e3-114">The Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span></span>
<span data-ttu-id="4b0e3-115">Просмотрите характеристики виртуальных машин, которые работают с хранилищем класса Premium, и выберите размер виртуальной машины, наиболее подходящий для вашей рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-115">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="4b0e3-116">Убедитесь, что виртуальная машина имеет достаточную пропускную способность для поддержки трафика диска.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-116">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span></span>

### <a name="disk-sizes"></a><span data-ttu-id="4b0e3-117">Размеры диска</span><span class="sxs-lookup"><span data-stu-id="4b0e3-117">Disk sizes</span></span>

<span data-ttu-id="4b0e3-118">**Управляемые диски уровня "Премиум"**</span><span class="sxs-lookup"><span data-stu-id="4b0e3-118">**Premium Managed Disks**</span></span>

<span data-ttu-id="4b0e3-119">Существует семь типов управляемых дисков уровня "Премиум", которые можно использовать с виртуальной машиной. Для каждого из них действуют определенные ограничения на пропускную способность и число операций ввода-вывода в секунду.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-119">There are seven types of premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="4b0e3-120">Учитывайте эти ограничения при выборе типа диска уровня "Премиум" для виртуальной машины в зависимости от потребностей приложения с точки зрения емкости, производительности, масштабируемости и пиковых нагрузок.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-120">Consider these limits when choosing the Premium disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="4b0e3-121">Диски уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="4b0e3-121">Premium Disks Type</span></span>  | <span data-ttu-id="4b0e3-122">P4</span><span class="sxs-lookup"><span data-stu-id="4b0e3-122">P4</span></span>    | <span data-ttu-id="4b0e3-123">P6</span><span class="sxs-lookup"><span data-stu-id="4b0e3-123">P6</span></span>    | <span data-ttu-id="4b0e3-124">P10</span><span class="sxs-lookup"><span data-stu-id="4b0e3-124">P10</span></span>   | <span data-ttu-id="4b0e3-125">P20</span><span class="sxs-lookup"><span data-stu-id="4b0e3-125">P20</span></span>   | <span data-ttu-id="4b0e3-126">P30</span><span class="sxs-lookup"><span data-stu-id="4b0e3-126">P30</span></span>   | <span data-ttu-id="4b0e3-127">P40</span><span class="sxs-lookup"><span data-stu-id="4b0e3-127">P40</span></span>   | <span data-ttu-id="4b0e3-128">P50</span><span class="sxs-lookup"><span data-stu-id="4b0e3-128">P50</span></span>   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| <span data-ttu-id="4b0e3-129">Размер диска</span><span class="sxs-lookup"><span data-stu-id="4b0e3-129">Disk size</span></span>           | <span data-ttu-id="4b0e3-130">128 ГБ</span><span class="sxs-lookup"><span data-stu-id="4b0e3-130">128 GB</span></span>| <span data-ttu-id="4b0e3-131">512 ГБ</span><span class="sxs-lookup"><span data-stu-id="4b0e3-131">512 GB</span></span>| <span data-ttu-id="4b0e3-132">128 ГБ</span><span class="sxs-lookup"><span data-stu-id="4b0e3-132">128 GB</span></span>| <span data-ttu-id="4b0e3-133">512 ГБ</span><span class="sxs-lookup"><span data-stu-id="4b0e3-133">512 GB</span></span>            | <span data-ttu-id="4b0e3-134">1024 ГБ (1 ТБ)</span><span class="sxs-lookup"><span data-stu-id="4b0e3-134">1024 GB (1 TB)</span></span>    | <span data-ttu-id="4b0e3-135">2048 ГБ (2 ТБ)</span><span class="sxs-lookup"><span data-stu-id="4b0e3-135">2048 GB (2 TB)</span></span>    | <span data-ttu-id="4b0e3-136">4095 ГБ (4 ТБ)</span><span class="sxs-lookup"><span data-stu-id="4b0e3-136">4095 GB (4 TB)</span></span>    | 
| <span data-ttu-id="4b0e3-137">Количество операций ввода-вывода в секунду на диск</span><span class="sxs-lookup"><span data-stu-id="4b0e3-137">IOPS per disk</span></span>       | <span data-ttu-id="4b0e3-138">120</span><span class="sxs-lookup"><span data-stu-id="4b0e3-138">120</span></span>   | <span data-ttu-id="4b0e3-139">240</span><span class="sxs-lookup"><span data-stu-id="4b0e3-139">240</span></span>   | <span data-ttu-id="4b0e3-140">500</span><span class="sxs-lookup"><span data-stu-id="4b0e3-140">500</span></span>   | <span data-ttu-id="4b0e3-141">2300</span><span class="sxs-lookup"><span data-stu-id="4b0e3-141">2300</span></span>              | <span data-ttu-id="4b0e3-142">5000</span><span class="sxs-lookup"><span data-stu-id="4b0e3-142">5000</span></span>              | <span data-ttu-id="4b0e3-143">7500</span><span class="sxs-lookup"><span data-stu-id="4b0e3-143">7500</span></span>              | <span data-ttu-id="4b0e3-144">7500</span><span class="sxs-lookup"><span data-stu-id="4b0e3-144">7500</span></span>              | 
| <span data-ttu-id="4b0e3-145">Пропускная способность на диск</span><span class="sxs-lookup"><span data-stu-id="4b0e3-145">Throughput per disk</span></span> | <span data-ttu-id="4b0e3-146">25 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="4b0e3-146">25 MB per second</span></span>  | <span data-ttu-id="4b0e3-147">50 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="4b0e3-147">50 MB per second</span></span>  | <span data-ttu-id="4b0e3-148">100 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="4b0e3-148">100 MB per second</span></span> | <span data-ttu-id="4b0e3-149">150 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="4b0e3-149">150 MB per second</span></span> | <span data-ttu-id="4b0e3-150">200 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="4b0e3-150">200 MB per second</span></span> | <span data-ttu-id="4b0e3-151">250 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="4b0e3-151">250 MB per second</span></span> | <span data-ttu-id="4b0e3-152">250 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="4b0e3-152">250 MB per second</span></span> | 

<span data-ttu-id="4b0e3-153">**Управляемые диски уровня "Стандартный"**</span><span class="sxs-lookup"><span data-stu-id="4b0e3-153">**Standard Managed Disks**</span></span>

<span data-ttu-id="4b0e3-154">Существует семь типов управляемых дисков уровня "Стандартный", которые можно использовать с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-154">There are seven types of Standard Managed disks that can be used with your VM.</span></span> <span data-ttu-id="4b0e3-155">У них разная емкость, но одинаковые ограничения пропускной способности и числа операций ввода-вывода в секунду.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-155">Each of them have different capacity but have same IOPS and throughput limits.</span></span> <span data-ttu-id="4b0e3-156">Выберите тип управляемых дисков уровня "Стандартный" в зависимости от потребностей в емкости своего приложения.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-156">Choose the type of Standard Managed disks based on the capacity needs of your application.</span></span>

| <span data-ttu-id="4b0e3-157">Диски уровня "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="4b0e3-157">Standard Disk Type</span></span>  | <span data-ttu-id="4b0e3-158">S4</span><span class="sxs-lookup"><span data-stu-id="4b0e3-158">S4</span></span>               | <span data-ttu-id="4b0e3-159">S6</span><span class="sxs-lookup"><span data-stu-id="4b0e3-159">S6</span></span>               | <span data-ttu-id="4b0e3-160">S10</span><span class="sxs-lookup"><span data-stu-id="4b0e3-160">S10</span></span>              | <span data-ttu-id="4b0e3-161">S20</span><span class="sxs-lookup"><span data-stu-id="4b0e3-161">S20</span></span>              | <span data-ttu-id="4b0e3-162">S30</span><span class="sxs-lookup"><span data-stu-id="4b0e3-162">S30</span></span>              | <span data-ttu-id="4b0e3-163">S40</span><span class="sxs-lookup"><span data-stu-id="4b0e3-163">S40</span></span>              | <span data-ttu-id="4b0e3-164">S50</span><span class="sxs-lookup"><span data-stu-id="4b0e3-164">S50</span></span>              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| <span data-ttu-id="4b0e3-165">Размер диска</span><span class="sxs-lookup"><span data-stu-id="4b0e3-165">Disk size</span></span>           | <span data-ttu-id="4b0e3-166">30 ГБ</span><span class="sxs-lookup"><span data-stu-id="4b0e3-166">30 GB</span></span>            | <span data-ttu-id="4b0e3-167">64 ГБ</span><span class="sxs-lookup"><span data-stu-id="4b0e3-167">64 GB</span></span>            | <span data-ttu-id="4b0e3-168">128 ГБ</span><span class="sxs-lookup"><span data-stu-id="4b0e3-168">128 GB</span></span>           | <span data-ttu-id="4b0e3-169">512 ГБ</span><span class="sxs-lookup"><span data-stu-id="4b0e3-169">512 GB</span></span>           | <span data-ttu-id="4b0e3-170">1024 ГБ (1 ТБ)</span><span class="sxs-lookup"><span data-stu-id="4b0e3-170">1024 GB (1 TB)</span></span>   | <span data-ttu-id="4b0e3-171">2048 ГБ (2 ТБ)</span><span class="sxs-lookup"><span data-stu-id="4b0e3-171">2048 GB (2TB)</span></span>    | <span data-ttu-id="4b0e3-172">4095 ГБ (4 ТБ)</span><span class="sxs-lookup"><span data-stu-id="4b0e3-172">4095 GB (4 TB)</span></span>   | 
| <span data-ttu-id="4b0e3-173">Количество операций ввода-вывода в секунду на диск</span><span class="sxs-lookup"><span data-stu-id="4b0e3-173">IOPS per disk</span></span>       | <span data-ttu-id="4b0e3-174">500</span><span class="sxs-lookup"><span data-stu-id="4b0e3-174">500</span></span>              | <span data-ttu-id="4b0e3-175">500</span><span class="sxs-lookup"><span data-stu-id="4b0e3-175">500</span></span>              | <span data-ttu-id="4b0e3-176">500</span><span class="sxs-lookup"><span data-stu-id="4b0e3-176">500</span></span>              | <span data-ttu-id="4b0e3-177">500</span><span class="sxs-lookup"><span data-stu-id="4b0e3-177">500</span></span>              | <span data-ttu-id="4b0e3-178">500</span><span class="sxs-lookup"><span data-stu-id="4b0e3-178">500</span></span>              | <span data-ttu-id="4b0e3-179">500</span><span class="sxs-lookup"><span data-stu-id="4b0e3-179">500</span></span>             | <span data-ttu-id="4b0e3-180">500</span><span class="sxs-lookup"><span data-stu-id="4b0e3-180">500</span></span>              | 
| <span data-ttu-id="4b0e3-181">Пропускная способность на диск</span><span class="sxs-lookup"><span data-stu-id="4b0e3-181">Throughput per disk</span></span> | <span data-ttu-id="4b0e3-182">60 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="4b0e3-182">60 MB per second</span></span> | <span data-ttu-id="4b0e3-183">60 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="4b0e3-183">60 MB per second</span></span> | <span data-ttu-id="4b0e3-184">60 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="4b0e3-184">60 MB per second</span></span> | <span data-ttu-id="4b0e3-185">60 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="4b0e3-185">60 MB per second</span></span> | <span data-ttu-id="4b0e3-186">60 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="4b0e3-186">60 MB per second</span></span> | <span data-ttu-id="4b0e3-187">60 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="4b0e3-187">60 MB per second</span></span> | <span data-ttu-id="4b0e3-188">60 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="4b0e3-188">60 MB per second</span></span> | 


### <a name="disk-caching-policy"></a><span data-ttu-id="4b0e3-189">Политика кэширования дисков</span><span class="sxs-lookup"><span data-stu-id="4b0e3-189">Disk caching policy</span></span> 

<span data-ttu-id="4b0e3-190">**Управляемые диски уровня "Премиум"**</span><span class="sxs-lookup"><span data-stu-id="4b0e3-190">**Premium Managed Disks**</span></span>

<span data-ttu-id="4b0e3-191">По умолчанию для политики кэширования дисков задано значение *только чтение* для всех дисков с данными "Премиум" и *чтение и запись* для дисков операционной системы "Премиум", подключенных к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-191">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span></span> <span data-ttu-id="4b0e3-192">Этот параметр конфигурации рекомендуется использовать, чтобы достичь оптимальной производительности при операциях ввода-вывода приложения.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-192">This configuration setting is recommended to achieve the optimal performance for your application’s IOs.</span></span> <span data-ttu-id="4b0e3-193">Отключите кэширование дисков данных, которые отличаются высокой интенсивностью записи или используются только для записи (например, файлов журналов SQL Server), чтобы улучшить производительность приложения.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-193">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span>

### <a name="pricing"></a><span data-ttu-id="4b0e3-194">Цены</span><span class="sxs-lookup"><span data-stu-id="4b0e3-194">Pricing</span></span>

<span data-ttu-id="4b0e3-195">Ознакомьтесь с [ценами на Управляемые диски](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="4b0e3-195">Review the [pricing for Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span></span> <span data-ttu-id="4b0e3-196">Цены на управляемые диски уровня "Премиум" совпадают с ценами на неуправляемые диски уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="4b0e3-196">Pricing of Premium Managed Disks is same as the Premium Unmanaged Disks.</span></span> <span data-ttu-id="4b0e3-197">При этом цены на управляемые диски уровня "Стандартный" отличаются от цен на неуправляемые диски уровня "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="4b0e3-197">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span></span>


## <a name="checklist"></a><span data-ttu-id="4b0e3-198">Контрольный список</span><span class="sxs-lookup"><span data-stu-id="4b0e3-198">Checklist</span></span>

1.  <span data-ttu-id="4b0e3-199">При миграции на управляемые диски уровня "Премиум" убедитесь, что они доступны в выбранном регионе.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-199">If you are migrating to Premium Managed Disks, make sure it is available in the region you are migrating to.</span></span>

2.  <span data-ttu-id="4b0e3-200">Определите серию виртуальной машины, которую вы будете использовать.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-200">Decide the new VM series you will be using.</span></span> <span data-ttu-id="4b0e3-201">Она должна поддерживать хранилище уровня "Премиум", если осуществляется миграция на управляемые диски уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="4b0e3-201">It should be a Premium Storage capable if you are migrating to Premium Managed Disks.</span></span>

3.  <span data-ttu-id="4b0e3-202">Выберите точный размер виртуальной машины, который доступен в регионе, выбранном для миграции.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-202">Decide the exact VM size you will use which are available in the region you are migrating to.</span></span> <span data-ttu-id="4b0e3-203">Размер виртуальной машины должен быть достаточно большим, чтобы поддерживать количество дисков данных, которые вы используете.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-203">VM size needs to be large enough to support the number of data disks you have.</span></span> <span data-ttu-id="4b0e3-204">Например, при наличии четырех дисков данных виртуальная машина должна иметь два или больше ядер.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-204">For example, if you have four data disks, the VM must have two or more cores.</span></span> <span data-ttu-id="4b0e3-205">Кроме того, учитывайте требования к вычислительной мощности, памяти и пропускной способности сети.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-205">Also, consider processing power, memory and network bandwidth needs.</span></span>

4.  <span data-ttu-id="4b0e3-206">Держите сведения о текущей виртуальной машине под рукой, в том числе список дисков и соответствующих BLOB-объектов виртуальных жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-206">Have the current VM details handy, including the list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="4b0e3-207">Подготовьте приложение к простою.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-207">Prepare your application for downtime.</span></span> <span data-ttu-id="4b0e3-208">Чтобы выполнить чистый перенос, необходимо остановить все процессы, выполняющиеся в текущей системе.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-208">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="4b0e3-209">Только так вы получите стабильное состояние, которое можно перенести на новую платформу.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-209">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="4b0e3-210">Длительность простоя зависит от объема данных на переносимых дисках.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-210">Downtime duration depends on the amount of data in the disks to migrate.</span></span>


## <a name="migrate-the-vm"></a><span data-ttu-id="4b0e3-211">Миграция виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="4b0e3-211">Migrate the VM</span></span>

<span data-ttu-id="4b0e3-212">Подготовьте приложение к простою.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-212">Prepare your application for downtime.</span></span> <span data-ttu-id="4b0e3-213">Чтобы выполнить чистый перенос, необходимо остановить все процессы, выполняющиеся в текущей системе.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-213">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="4b0e3-214">Только так вы получите стабильное состояние, которое можно перенести на новую платформу.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-214">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="4b0e3-215">Длительность простоя зависит от объема данных на переносимых дисках.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-215">Downtime duration depends the amount of data in the disks to migrate.</span></span>


1.  <span data-ttu-id="4b0e3-216">Сначала задайте общие параметры.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-216">First, set the common parameters:</span></span>

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  <span data-ttu-id="4b0e3-217">Создайте управляемый диск ОС с помощью виртуального жесткого диска из классической виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-217">Create a managed OS disk using the VHD from the classic VM.</span></span>

    <span data-ttu-id="4b0e3-218">Обязательно укажите полный универсальный код ресурса (URI) виртуального жесткого диска ОС в параметре $osVhdUri.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-218">Ensure that you have provided the complete URI of the OS VHD to the $osVhdUri parameter.</span></span> <span data-ttu-id="4b0e3-219">Также для параметра **-AccountType** укажите значение **PremiumLRS** или **StandardLRS**, в зависимости от типа дисков ("Премиум" или "Стандартный"), на которые выполняется миграция.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-219">Also, enter **-AccountType** as **PremiumLRS** or **StandardLRS** based on type of disks (Premium or Standard) you are migrating to.</span></span>

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  <span data-ttu-id="4b0e3-220">Подключите диск ОС к новой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-220">Attach the OS disk to the new VM.</span></span>

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  <span data-ttu-id="4b0e3-221">Создайте управляемый диск данных из VHD-файла данных и добавьте его в новую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-221">Create a managed data disk from the data VHD file and add it to the new VM.</span></span>

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  <span data-ttu-id="4b0e3-222">Создайте новую виртуальную машину, настроив ее общедоступный IP-адрес, виртуальную сеть и сетевую карту.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-222">Create the new VM by setting public IP, Virtual Network and NIC.</span></span>

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
><span data-ttu-id="4b0e3-223">Чтобы обеспечить поддержку приложений, может потребоваться выполнить дополнительные шаги, не описанные в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-223">There may be additional steps necessary to support your application that is not be covered by this guide.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="4b0e3-224">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4b0e3-224">Next steps</span></span>

- <span data-ttu-id="4b0e3-225">Подключитесь к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="4b0e3-225">Connect to the virtual machine.</span></span> <span data-ttu-id="4b0e3-226">Указания см. в статье [Как подключиться к виртуальной машине Azure под управлением Windows и войти в систему](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4b0e3-226">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

