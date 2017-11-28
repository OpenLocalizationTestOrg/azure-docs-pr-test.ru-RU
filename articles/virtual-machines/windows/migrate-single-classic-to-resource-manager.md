---
title: "aaaMigrate tooan классических виртуальных Машин ARM управляемого диска ВМ | Документы Microsoft"
description: "Миграция одной виртуальной Машины Azure из классического развертывания hello модели tooManaged дисков в модели развертывания диспетчера ресурсов hello."
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
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a><span data-ttu-id="35d61-103">Вручную перенести tooa классической виртуальной Машины новая ARM управляемого диска ВМ из hello виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="35d61-103">Manually migrate a Classic VM tooa new ARM Managed Disk VM from hello VHD</span></span> 


<span data-ttu-id="35d61-104">Этот раздел поможет вам toomigrate существующих виртуальных машин Azure из hello классической модели развертывания слишком[управляемых дисков](managed-disks-overview.md) в модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="35d61-104">This section helps you toomigrate your existing Azure VMs from hello classic deployment model too[Managed Disks](managed-disks-overview.md) in hello Resource Manager deployment model.</span></span>


## <a name="plan-for-hello-migration-toomanaged-disks"></a><span data-ttu-id="35d61-105">План миграции hello tooManaged дисков</span><span class="sxs-lookup"><span data-stu-id="35d61-105">Plan for hello migration tooManaged Disks</span></span>

<span data-ttu-id="35d61-106">Этот раздел поможет вам toomake hello наилучшее решение в типах виртуальной Машины и диска.</span><span class="sxs-lookup"><span data-stu-id="35d61-106">This section helps you toomake hello best decision on VM and disk types.</span></span>


### <a name="location"></a><span data-ttu-id="35d61-107">Расположение</span><span class="sxs-lookup"><span data-stu-id="35d61-107">Location</span></span>

<span data-ttu-id="35d61-108">Выберите расположение, в котором доступны Управляемые диски Azure.</span><span class="sxs-lookup"><span data-stu-id="35d61-108">Pick a location where Azure Managed Disks are available.</span></span> <span data-ttu-id="35d61-109">При переносе дисков управляемых tooPremium Убедитесь также, хранилище Premium доступно в регионе hello, где вы планируете toomigrate для.</span><span class="sxs-lookup"><span data-stu-id="35d61-109">If you are migrating tooPremium Managed Disks, also ensure that Premium storage is available in hello region where you are planning toomigrate to.</span></span> <span data-ttu-id="35d61-110">Актуальные сведения о поддерживаемых расположениях см. на странице [Доступность продуктов по регионам](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="35d61-110">See [Azure Services byRegion](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="35d61-111">Размеры виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="35d61-111">VM sizes</span></span>

<span data-ttu-id="35d61-112">При переносе дисков управляемых tooPremium у вас tooupdate hello размер ВМ hello tooPremium хранилища поддерживает размер доступной в hello регион, где находится виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="35d61-112">If you are migrating tooPremium Managed Disks, you have tooupdate hello size of hello VM tooPremium Storage capable size available in hello region where VM is located.</span></span> <span data-ttu-id="35d61-113">Просмотрите hello размеры виртуальных Машин, поддерживают хранилище класса Premium.</span><span class="sxs-lookup"><span data-stu-id="35d61-113">Review hello VM sizes that are Premium Storage capable.</span></span> <span data-ttu-id="35d61-114">Hello спецификаций размера виртуальной Машины Azure, перечислены в [размеры виртуальных машин](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="35d61-114">hello Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span></span>
<span data-ttu-id="35d61-115">Проверьте характеристики производительности hello виртуальные машины, работающие с хранилищем Premium и выберите размер виртуальной Машины наиболее подходящий hello, который лучше всего подходит для рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="35d61-115">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="35d61-116">Убедитесь, что недоступна достаточную пропускную способность трафика диска виртуальной Машины toodrive hello.</span><span class="sxs-lookup"><span data-stu-id="35d61-116">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

### <a name="disk-sizes"></a><span data-ttu-id="35d61-117">Размеры диска</span><span class="sxs-lookup"><span data-stu-id="35d61-117">Disk sizes</span></span>

<span data-ttu-id="35d61-118">**Управляемые диски уровня "Премиум"**</span><span class="sxs-lookup"><span data-stu-id="35d61-118">**Premium Managed Disks**</span></span>

<span data-ttu-id="35d61-119">Существует семь типов управляемых дисков уровня "Премиум", которые можно использовать с виртуальной машиной. Для каждого из них действуют определенные ограничения на пропускную способность и число операций ввода-вывода в секунду.</span><span class="sxs-lookup"><span data-stu-id="35d61-119">There are seven types of premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="35d61-120">Учитывайте следующие ограничения при выборе hello Premium тип диска для виртуальной Машины на основе hello потребностей вашего приложения с точки зрения производительности, производительность, масштабируемость и пиковых нагрузок.</span><span class="sxs-lookup"><span data-stu-id="35d61-120">Consider these limits when choosing hello Premium disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="35d61-121">Диски уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="35d61-121">Premium Disks Type</span></span>  | <span data-ttu-id="35d61-122">P4</span><span class="sxs-lookup"><span data-stu-id="35d61-122">P4</span></span>    | <span data-ttu-id="35d61-123">P6</span><span class="sxs-lookup"><span data-stu-id="35d61-123">P6</span></span>    | <span data-ttu-id="35d61-124">P10</span><span class="sxs-lookup"><span data-stu-id="35d61-124">P10</span></span>   | <span data-ttu-id="35d61-125">P20</span><span class="sxs-lookup"><span data-stu-id="35d61-125">P20</span></span>   | <span data-ttu-id="35d61-126">P30</span><span class="sxs-lookup"><span data-stu-id="35d61-126">P30</span></span>   | <span data-ttu-id="35d61-127">P40</span><span class="sxs-lookup"><span data-stu-id="35d61-127">P40</span></span>   | <span data-ttu-id="35d61-128">P50</span><span class="sxs-lookup"><span data-stu-id="35d61-128">P50</span></span>   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| <span data-ttu-id="35d61-129">Размер диска</span><span class="sxs-lookup"><span data-stu-id="35d61-129">Disk size</span></span>           | <span data-ttu-id="35d61-130">128 ГБ</span><span class="sxs-lookup"><span data-stu-id="35d61-130">128 GB</span></span>| <span data-ttu-id="35d61-131">512 ГБ</span><span class="sxs-lookup"><span data-stu-id="35d61-131">512 GB</span></span>| <span data-ttu-id="35d61-132">128 ГБ</span><span class="sxs-lookup"><span data-stu-id="35d61-132">128 GB</span></span>| <span data-ttu-id="35d61-133">512 ГБ</span><span class="sxs-lookup"><span data-stu-id="35d61-133">512 GB</span></span>            | <span data-ttu-id="35d61-134">1024 ГБ (1 ТБ)</span><span class="sxs-lookup"><span data-stu-id="35d61-134">1024 GB (1 TB)</span></span>    | <span data-ttu-id="35d61-135">2048 ГБ (2 ТБ)</span><span class="sxs-lookup"><span data-stu-id="35d61-135">2048 GB (2 TB)</span></span>    | <span data-ttu-id="35d61-136">4095 ГБ (4 ТБ)</span><span class="sxs-lookup"><span data-stu-id="35d61-136">4095 GB (4 TB)</span></span>    | 
| <span data-ttu-id="35d61-137">Количество операций ввода-вывода в секунду на диск</span><span class="sxs-lookup"><span data-stu-id="35d61-137">IOPS per disk</span></span>       | <span data-ttu-id="35d61-138">120</span><span class="sxs-lookup"><span data-stu-id="35d61-138">120</span></span>   | <span data-ttu-id="35d61-139">240</span><span class="sxs-lookup"><span data-stu-id="35d61-139">240</span></span>   | <span data-ttu-id="35d61-140">500</span><span class="sxs-lookup"><span data-stu-id="35d61-140">500</span></span>   | <span data-ttu-id="35d61-141">2300</span><span class="sxs-lookup"><span data-stu-id="35d61-141">2300</span></span>              | <span data-ttu-id="35d61-142">5000</span><span class="sxs-lookup"><span data-stu-id="35d61-142">5000</span></span>              | <span data-ttu-id="35d61-143">7500</span><span class="sxs-lookup"><span data-stu-id="35d61-143">7500</span></span>              | <span data-ttu-id="35d61-144">7500</span><span class="sxs-lookup"><span data-stu-id="35d61-144">7500</span></span>              | 
| <span data-ttu-id="35d61-145">Пропускная способность на диск</span><span class="sxs-lookup"><span data-stu-id="35d61-145">Throughput per disk</span></span> | <span data-ttu-id="35d61-146">25 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="35d61-146">25 MB per second</span></span>  | <span data-ttu-id="35d61-147">50 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="35d61-147">50 MB per second</span></span>  | <span data-ttu-id="35d61-148">100 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="35d61-148">100 MB per second</span></span> | <span data-ttu-id="35d61-149">150 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="35d61-149">150 MB per second</span></span> | <span data-ttu-id="35d61-150">200 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="35d61-150">200 MB per second</span></span> | <span data-ttu-id="35d61-151">250 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="35d61-151">250 MB per second</span></span> | <span data-ttu-id="35d61-152">250 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="35d61-152">250 MB per second</span></span> | 

<span data-ttu-id="35d61-153">**Управляемые диски уровня "Стандартный"**</span><span class="sxs-lookup"><span data-stu-id="35d61-153">**Standard Managed Disks**</span></span>

<span data-ttu-id="35d61-154">Существует семь типов управляемых дисков уровня "Стандартный", которые можно использовать с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="35d61-154">There are seven types of Standard Managed disks that can be used with your VM.</span></span> <span data-ttu-id="35d61-155">У них разная емкость, но одинаковые ограничения пропускной способности и числа операций ввода-вывода в секунду.</span><span class="sxs-lookup"><span data-stu-id="35d61-155">Each of them have different capacity but have same IOPS and throughput limits.</span></span> <span data-ttu-id="35d61-156">Выберите тип hello Стандартная управляемых дисков, в зависимости от потребностей в емкости hello приложения.</span><span class="sxs-lookup"><span data-stu-id="35d61-156">Choose hello type of Standard Managed disks based on hello capacity needs of your application.</span></span>

| <span data-ttu-id="35d61-157">Диски уровня "Стандартный"</span><span class="sxs-lookup"><span data-stu-id="35d61-157">Standard Disk Type</span></span>  | <span data-ttu-id="35d61-158">S4</span><span class="sxs-lookup"><span data-stu-id="35d61-158">S4</span></span>               | <span data-ttu-id="35d61-159">S6</span><span class="sxs-lookup"><span data-stu-id="35d61-159">S6</span></span>               | <span data-ttu-id="35d61-160">S10</span><span class="sxs-lookup"><span data-stu-id="35d61-160">S10</span></span>              | <span data-ttu-id="35d61-161">S20</span><span class="sxs-lookup"><span data-stu-id="35d61-161">S20</span></span>              | <span data-ttu-id="35d61-162">S30</span><span class="sxs-lookup"><span data-stu-id="35d61-162">S30</span></span>              | <span data-ttu-id="35d61-163">S40</span><span class="sxs-lookup"><span data-stu-id="35d61-163">S40</span></span>              | <span data-ttu-id="35d61-164">S50</span><span class="sxs-lookup"><span data-stu-id="35d61-164">S50</span></span>              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| <span data-ttu-id="35d61-165">Размер диска</span><span class="sxs-lookup"><span data-stu-id="35d61-165">Disk size</span></span>           | <span data-ttu-id="35d61-166">30 ГБ</span><span class="sxs-lookup"><span data-stu-id="35d61-166">30 GB</span></span>            | <span data-ttu-id="35d61-167">64 ГБ</span><span class="sxs-lookup"><span data-stu-id="35d61-167">64 GB</span></span>            | <span data-ttu-id="35d61-168">128 ГБ</span><span class="sxs-lookup"><span data-stu-id="35d61-168">128 GB</span></span>           | <span data-ttu-id="35d61-169">512 ГБ</span><span class="sxs-lookup"><span data-stu-id="35d61-169">512 GB</span></span>           | <span data-ttu-id="35d61-170">1024 ГБ (1 ТБ)</span><span class="sxs-lookup"><span data-stu-id="35d61-170">1024 GB (1 TB)</span></span>   | <span data-ttu-id="35d61-171">2048 ГБ (2 ТБ)</span><span class="sxs-lookup"><span data-stu-id="35d61-171">2048 GB (2TB)</span></span>    | <span data-ttu-id="35d61-172">4095 ГБ (4 ТБ)</span><span class="sxs-lookup"><span data-stu-id="35d61-172">4095 GB (4 TB)</span></span>   | 
| <span data-ttu-id="35d61-173">Количество операций ввода-вывода в секунду на диск</span><span class="sxs-lookup"><span data-stu-id="35d61-173">IOPS per disk</span></span>       | <span data-ttu-id="35d61-174">500</span><span class="sxs-lookup"><span data-stu-id="35d61-174">500</span></span>              | <span data-ttu-id="35d61-175">500</span><span class="sxs-lookup"><span data-stu-id="35d61-175">500</span></span>              | <span data-ttu-id="35d61-176">500</span><span class="sxs-lookup"><span data-stu-id="35d61-176">500</span></span>              | <span data-ttu-id="35d61-177">500</span><span class="sxs-lookup"><span data-stu-id="35d61-177">500</span></span>              | <span data-ttu-id="35d61-178">500</span><span class="sxs-lookup"><span data-stu-id="35d61-178">500</span></span>              | <span data-ttu-id="35d61-179">500</span><span class="sxs-lookup"><span data-stu-id="35d61-179">500</span></span>             | <span data-ttu-id="35d61-180">500</span><span class="sxs-lookup"><span data-stu-id="35d61-180">500</span></span>              | 
| <span data-ttu-id="35d61-181">Пропускная способность на диск</span><span class="sxs-lookup"><span data-stu-id="35d61-181">Throughput per disk</span></span> | <span data-ttu-id="35d61-182">60 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="35d61-182">60 MB per second</span></span> | <span data-ttu-id="35d61-183">60 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="35d61-183">60 MB per second</span></span> | <span data-ttu-id="35d61-184">60 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="35d61-184">60 MB per second</span></span> | <span data-ttu-id="35d61-185">60 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="35d61-185">60 MB per second</span></span> | <span data-ttu-id="35d61-186">60 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="35d61-186">60 MB per second</span></span> | <span data-ttu-id="35d61-187">60 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="35d61-187">60 MB per second</span></span> | <span data-ttu-id="35d61-188">60 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="35d61-188">60 MB per second</span></span> | 


### <a name="disk-caching-policy"></a><span data-ttu-id="35d61-189">Политика кэширования дисков</span><span class="sxs-lookup"><span data-stu-id="35d61-189">Disk caching policy</span></span> 

<span data-ttu-id="35d61-190">**Управляемые диски уровня "Премиум"**</span><span class="sxs-lookup"><span data-stu-id="35d61-190">**Premium Managed Disks**</span></span>

<span data-ttu-id="35d61-191">По умолчанию политика кэширования диска — *только для чтения* для всех hello Premium дисков с данными и *чтения и записи* для диска операционной системы Premium hello присоединенного toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="35d61-191">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="35d61-192">Этот параметр конфигурации рекомендуется tooachieve hello оптимальную производительность операций ввода-вывода приложения.</span><span class="sxs-lookup"><span data-stu-id="35d61-192">This configuration setting is recommended tooachieve hello optimal performance for your application’s IOs.</span></span> <span data-ttu-id="35d61-193">Отключите кэширование дисков данных, которые отличаются высокой интенсивностью записи или используются только для записи (например, файлов журналов SQL Server), чтобы улучшить производительность приложения.</span><span class="sxs-lookup"><span data-stu-id="35d61-193">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span>

### <a name="pricing"></a><span data-ttu-id="35d61-194">Цены</span><span class="sxs-lookup"><span data-stu-id="35d61-194">Pricing</span></span>

<span data-ttu-id="35d61-195">Просмотрите hello [цены для дисков, управляемых](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="35d61-195">Review hello [pricing for Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span></span> <span data-ttu-id="35d61-196">Цены управляемых дисков "премиум" совпадает с неуправляемой дисков "премиум" hello.</span><span class="sxs-lookup"><span data-stu-id="35d61-196">Pricing of Premium Managed Disks is same as hello Premium Unmanaged Disks.</span></span> <span data-ttu-id="35d61-197">При этом цены на управляемые диски уровня "Стандартный" отличаются от цен на неуправляемые диски уровня "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="35d61-197">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span></span>


## <a name="checklist"></a><span data-ttu-id="35d61-198">Контрольный список</span><span class="sxs-lookup"><span data-stu-id="35d61-198">Checklist</span></span>

1.  <span data-ttu-id="35d61-199">При переносе дисков управляемых tooPremium убедитесь, что он доступен в области hello, которую вы переносите.</span><span class="sxs-lookup"><span data-stu-id="35d61-199">If you are migrating tooPremium Managed Disks, make sure it is available in hello region you are migrating to.</span></span>

2.  <span data-ttu-id="35d61-200">Решите, Серия виртуальных Машин новый hello, который будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="35d61-200">Decide hello new VM series you will be using.</span></span> <span data-ttu-id="35d61-201">При переносе дисков управляемых tooPremium следует возможность хранения уровня Premium.</span><span class="sxs-lookup"><span data-stu-id="35d61-201">It should be a Premium Storage capable if you are migrating tooPremium Managed Disks.</span></span>

3.  <span data-ttu-id="35d61-202">Определите hello точный размер виртуальной Машины используется которой доступны в области hello, которую вы переносите.</span><span class="sxs-lookup"><span data-stu-id="35d61-202">Decide hello exact VM size you will use which are available in hello region you are migrating to.</span></span> <span data-ttu-id="35d61-203">Размер виртуальной Машины должен toobe достаточно большой toosupport hello количество дисков данных вами.</span><span class="sxs-lookup"><span data-stu-id="35d61-203">VM size needs toobe large enough toosupport hello number of data disks you have.</span></span> <span data-ttu-id="35d61-204">Например при наличии четырех дисков данных hello виртуальной Машины должен иметь не менее двух ядер.</span><span class="sxs-lookup"><span data-stu-id="35d61-204">For example, if you have four data disks, hello VM must have two or more cores.</span></span> <span data-ttu-id="35d61-205">Кроме того, учитывайте требования к вычислительной мощности, памяти и пропускной способности сети.</span><span class="sxs-lookup"><span data-stu-id="35d61-205">Also, consider processing power, memory and network bandwidth needs.</span></span>

4.  <span data-ttu-id="35d61-206">Иметь hello текущей виртуальной Машины сведений под рукой, включая hello список дисков и соответствующих больших двоичных объектов VHD.</span><span class="sxs-lookup"><span data-stu-id="35d61-206">Have hello current VM details handy, including hello list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="35d61-207">Подготовьте приложение к простою.</span><span class="sxs-lookup"><span data-stu-id="35d61-207">Prepare your application for downtime.</span></span> <span data-ttu-id="35d61-208">toodo очистить миграции у вас toostop вся обработка hello в текущей системе hello.</span><span class="sxs-lookup"><span data-stu-id="35d61-208">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="35d61-209">Только после этого можно получить его состояние tooconsistent, который можно перенести toohello новой платформы.</span><span class="sxs-lookup"><span data-stu-id="35d61-209">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="35d61-210">Длительность времени простоя зависит от hello объем данных в toomigrate диски hello.</span><span class="sxs-lookup"><span data-stu-id="35d61-210">Downtime duration depends on hello amount of data in hello disks toomigrate.</span></span>


## <a name="migrate-hello-vm"></a><span data-ttu-id="35d61-211">Перенос hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="35d61-211">Migrate hello VM</span></span>

<span data-ttu-id="35d61-212">Подготовьте приложение к простою.</span><span class="sxs-lookup"><span data-stu-id="35d61-212">Prepare your application for downtime.</span></span> <span data-ttu-id="35d61-213">toodo очистить миграции у вас toostop вся обработка hello в текущей системе hello.</span><span class="sxs-lookup"><span data-stu-id="35d61-213">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="35d61-214">Только после этого можно получить его состояние tooconsistent, который можно перенести toohello новой платформы.</span><span class="sxs-lookup"><span data-stu-id="35d61-214">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="35d61-215">Длительность времени простоя зависит от hello объем данных в toomigrate диски hello.</span><span class="sxs-lookup"><span data-stu-id="35d61-215">Downtime duration depends hello amount of data in hello disks toomigrate.</span></span>


1.  <span data-ttu-id="35d61-216">Во-первых можно задать общие параметры hello:</span><span class="sxs-lookup"><span data-stu-id="35d61-216">First, set hello common parameters:</span></span>

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

2.  <span data-ttu-id="35d61-217">Создание управляемого диска операционной системы с помощью hello виртуального жесткого диска из hello классической виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="35d61-217">Create a managed OS disk using hello VHD from hello classic VM.</span></span>

    <span data-ttu-id="35d61-218">Обеспечьте предоставляемых hello завершения URI hello параметр toohello $osVhdUri виртуального жесткого диска операционной системы.</span><span class="sxs-lookup"><span data-stu-id="35d61-218">Ensure that you have provided hello complete URI of hello OS VHD toohello $osVhdUri parameter.</span></span> <span data-ttu-id="35d61-219">Также для параметра **-AccountType** укажите значение **PremiumLRS** или **StandardLRS**, в зависимости от типа дисков ("Премиум" или "Стандартный"), на которые выполняется миграция.</span><span class="sxs-lookup"><span data-stu-id="35d61-219">Also, enter **-AccountType** as **PremiumLRS** or **StandardLRS** based on type of disks (Premium or Standard) you are migrating to.</span></span>

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  <span data-ttu-id="35d61-220">Присоединить диск toohello hello ОС новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="35d61-220">Attach hello OS disk toohello new VM.</span></span>

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  <span data-ttu-id="35d61-221">Создать диск управляемые данные из файла виртуального жесткого диска данных hello и добавьте его toohello новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="35d61-221">Create a managed data disk from hello data VHD file and add it toohello new VM.</span></span>

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  <span data-ttu-id="35d61-222">Создание hello новую виртуальную Машину, установив открытый IP-адрес, виртуальной сети и сетевой адаптер.</span><span class="sxs-lookup"><span data-stu-id="35d61-222">Create hello new VM by setting public IP, Virtual Network and NIC.</span></span>

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
><span data-ttu-id="35d61-223">Может быть toosupport необходимые дополнительные действия приложения, не будут рассмотрены в данном руководстве.</span><span class="sxs-lookup"><span data-stu-id="35d61-223">There may be additional steps necessary toosupport your application that is not be covered by this guide.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="35d61-224">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="35d61-224">Next steps</span></span>

- <span data-ttu-id="35d61-225">Подключение toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="35d61-225">Connect toohello virtual machine.</span></span> <span data-ttu-id="35d61-226">Инструкции см. в разделе [как tooconnect и вход в систему tooan Azure виртуальные машины под управлением Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="35d61-226">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

