---
title: "изменяет размер aaaWindows ВМ в Azure | Документы Microsoft"
description: "Список hello различные размеры, доступные для виртуальных машинах в Azure."
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: aabf0d30-04eb-4d34-b44a-69f8bfb84f22
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 80bd8241b134031c41b56224e841c7557c4845cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a><span data-ttu-id="6bfa1-103">Размеры виртуальных машин Windows в Azure</span><span class="sxs-lookup"><span data-stu-id="6bfa1-103">Sizes for Windows virtual machines in Azure</span></span>

<span data-ttu-id="6bfa1-104">В этой статье описываются доступные размеры hello и параметры для hello виртуальных машинах Azure можно использовать toorun Windows-приложений и рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="6bfa1-104">This article describes hello available sizes and options for hello Azure virtual machines you can use toorun your Windows apps and workloads.</span></span> <span data-ttu-id="6bfa1-105">Он также предоставляет toobe вопросы развертывания учитывать при планировании toouse эти ресурсы.</span><span class="sxs-lookup"><span data-stu-id="6bfa1-105">It also provides deployment considerations toobe aware of when you're planning toouse these resources.</span></span>  <span data-ttu-id="6bfa1-106">Также доступна версия этой статьи для [виртуальных машин Linux](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6bfa1-106">This article is also available for [Linux virtual machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


| <span data-ttu-id="6bfa1-107">Тип</span><span class="sxs-lookup"><span data-stu-id="6bfa1-107">Type</span></span>                     | <span data-ttu-id="6bfa1-108">Размеры</span><span class="sxs-lookup"><span data-stu-id="6bfa1-108">Sizes</span></span>           |    <span data-ttu-id="6bfa1-109">Описание</span><span class="sxs-lookup"><span data-stu-id="6bfa1-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="6bfa1-110">Универсальные</span><span class="sxs-lookup"><span data-stu-id="6bfa1-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="6bfa1-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0–7</span><span class="sxs-lookup"><span data-stu-id="6bfa1-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span> | <span data-ttu-id="6bfa1-112">Сбалансированное соотношение ресурсов ЦП и памяти.</span><span class="sxs-lookup"><span data-stu-id="6bfa1-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="6bfa1-113">Идеально подходит для тестирования и разработки, toomedium небольших баз данных и низким toomedium трафик веб-серверов.</span><span class="sxs-lookup"><span data-stu-id="6bfa1-113">Ideal for testing and development, small toomedium databases, and low toomedium traffic web servers.</span></span> |
| [<span data-ttu-id="6bfa1-114">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="6bfa1-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="6bfa1-115">Fs, F</span><span class="sxs-lookup"><span data-stu-id="6bfa1-115">Fs, F</span></span>             | <span data-ttu-id="6bfa1-116">Высокое соотношение ресурсов ЦП и памяти.</span><span class="sxs-lookup"><span data-stu-id="6bfa1-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="6bfa1-117">Подходят для веб-серверов со средним объемом трафика, сетевых устройств, пакетных процессов и серверов приложений.</span><span class="sxs-lookup"><span data-stu-id="6bfa1-117">Good for medium traffic web servers, network appliances, batch processes, and application servers.</span></span>        |
| [<span data-ttu-id="6bfa1-118">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="6bfa1-118">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)         | <span data-ttu-id="6bfa1-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="6bfa1-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="6bfa1-120">Высокое соотношение ресурсов памяти и ядра.</span><span class="sxs-lookup"><span data-stu-id="6bfa1-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="6bfa1-121">Идеально подходит для серверов реляционной базы данных, кэши средний toolarge и аналитики в памяти.</span><span class="sxs-lookup"><span data-stu-id="6bfa1-121">Great for relational database servers, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="6bfa1-122">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="6bfa1-122">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)        | <span data-ttu-id="6bfa1-123">Ls</span><span class="sxs-lookup"><span data-stu-id="6bfa1-123">Ls</span></span>                | <span data-ttu-id="6bfa1-124">Высокая пропускная способность дисков и количество операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="6bfa1-124">High disk throughput and IO.</span></span> <span data-ttu-id="6bfa1-125">Идеальный вариант для работы с большими данными, а также с базами данных SQL и NoSQL.</span><span class="sxs-lookup"><span data-stu-id="6bfa1-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="6bfa1-126">GPU</span><span class="sxs-lookup"><span data-stu-id="6bfa1-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="6bfa1-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="6bfa1-127">NV, NC</span></span>            | <span data-ttu-id="6bfa1-128">Специализированные виртуальные машины, предназначенные для ресурсоемкой отрисовки изображений и редактирования видео.</span><span class="sxs-lookup"><span data-stu-id="6bfa1-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="6bfa1-129">Доступны виртуальные машины одним или несколькими GPU.</span><span class="sxs-lookup"><span data-stu-id="6bfa1-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="6bfa1-130">Для высокопроизводительных вычислений</span><span class="sxs-lookup"><span data-stu-id="6bfa1-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="6bfa1-131">H, A8–A11</span><span class="sxs-lookup"><span data-stu-id="6bfa1-131">H, A8-11</span></span>          | <span data-ttu-id="6bfa1-132">Виртуальные машины с самыми быстрыми и мощными ЦП, для которых можно настроить сетевые интерфейсы с высокой пропускной способностью (RDMA).</span><span class="sxs-lookup"><span data-stu-id="6bfa1-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br> 

- <span data-ttu-id="6bfa1-133">Сведения о стоимости hello разного размера, в разделе [расценки на виртуальные машины](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span><span class="sxs-lookup"><span data-stu-id="6bfa1-133">For information about pricing of hello various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span></span> 
- <span data-ttu-id="6bfa1-134">Общие ограничения toosee на виртуальных машинах Azure, в разделе [подписка Azure и ограничения служб, квоты и ограничения](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="6bfa1-134">toosee general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="6bfa1-135">Затраты на хранение вычисляются отдельно на основе использованных страниц в учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="6bfa1-135">Storage costs are calculated separately based on used pages in hello storage account.</span></span> <span data-ttu-id="6bfa1-136">Дополнительные сведения см. на странице [Цены на хранилища Azure](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="6bfa1-136">For details, [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>
- <span data-ttu-id="6bfa1-137">Узнайте больше о том, как с помощью [единиц вычислений Azure (ACU)](acu.md) сравнить производительность вычислений для различных номеров SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="6bfa1-137">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>



## <a name="rest-api"></a><span data-ttu-id="6bfa1-138">Rest API</span><span class="sxs-lookup"><span data-stu-id="6bfa1-138">Rest API</span></span>

<span data-ttu-id="6bfa1-139">Сведения об использовании tooquery hello API-интерфейса REST для размеров виртуальных Машин см. в следующем hello:</span><span class="sxs-lookup"><span data-stu-id="6bfa1-139">For information on using hello REST API tooquery for VM sizes, see hello following:</span></span>

- <span data-ttu-id="6bfa1-140">[List available virtual machine sizes for resizing](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing) (Вывод доступных размеров виртуальных машин для изменения размеров)</span><span class="sxs-lookup"><span data-stu-id="6bfa1-140">[List available virtual machine sizes for resizing](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)</span></span>
- <span data-ttu-id="6bfa1-141">[List available virtual machine sizes for a subscription](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region) (Вывод доступных размеров виртуальных машин для подписки)</span><span class="sxs-lookup"><span data-stu-id="6bfa1-141">[List available virtual machine sizes for a subscription](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)</span></span>
- <span data-ttu-id="6bfa1-142">[List available virtual machine sizes in an availability set](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set) (Вывод доступных размеров виртуальных машин в группе доступности)</span><span class="sxs-lookup"><span data-stu-id="6bfa1-142">[List available virtual machine sizes in an availability set](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)</span></span>

## <a name="acu"></a><span data-ttu-id="6bfa1-143">ACU</span><span class="sxs-lookup"><span data-stu-id="6bfa1-143">ACU</span></span>

<span data-ttu-id="6bfa1-144">Узнайте больше о том, как с помощью [единиц вычислений Azure (ACU)](acu.md) сравнить производительность вычислений для различных номеров SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="6bfa1-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6bfa1-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6bfa1-145">Next steps</span></span>

<span data-ttu-id="6bfa1-146">Дополнительные сведения о размерах виртуальных Машин различных hello, которые доступны.</span><span class="sxs-lookup"><span data-stu-id="6bfa1-146">Learn more about hello different VM sizes that are available:</span></span>
- [<span data-ttu-id="6bfa1-147">Универсальные</span><span class="sxs-lookup"><span data-stu-id="6bfa1-147">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="6bfa1-148">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="6bfa1-148">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="6bfa1-149">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="6bfa1-149">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="6bfa1-150">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="6bfa1-150">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="6bfa1-151">Оптимизированные для GPU</span><span class="sxs-lookup"><span data-stu-id="6bfa1-151">GPU optimized</span></span>](sizes-gpu.md)
- [<span data-ttu-id="6bfa1-152">Для высокопроизводительных вычислений</span><span class="sxs-lookup"><span data-stu-id="6bfa1-152">High performance compute</span></span>](sizes-hpc.md)



