---
title: "Размеры виртуальных машин Windows в Azure | Документация Майкрософт"
description: "Список различных размеров виртуальных машин Windows в Azure."
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
ms.openlocfilehash: b3a674137ed3dd47188d4af0bc845104eabc885e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a><span data-ttu-id="43da2-103">Размеры виртуальных машин Windows в Azure</span><span class="sxs-lookup"><span data-stu-id="43da2-103">Sizes for Windows virtual machines in Azure</span></span>

<span data-ttu-id="43da2-104">В этой статье описаны доступные размеры и разновидности виртуальных машин Azure, которые можно использовать для запуска приложений для Windows и рабочих нагрузок Windows.</span><span class="sxs-lookup"><span data-stu-id="43da2-104">This article describes the available sizes and options for the Azure virtual machines you can use to run your Windows apps and workloads.</span></span> <span data-ttu-id="43da2-105">Здесь также предоставлены рекомендации по развертыванию, которые нужно учитывать при планировании использования этих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="43da2-105">It also provides deployment considerations to be aware of when you're planning to use these resources.</span></span>  <span data-ttu-id="43da2-106">Также доступна версия этой статьи для [виртуальных машин Linux](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="43da2-106">This article is also available for [Linux virtual machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


| <span data-ttu-id="43da2-107">Тип</span><span class="sxs-lookup"><span data-stu-id="43da2-107">Type</span></span>                     | <span data-ttu-id="43da2-108">Размеры</span><span class="sxs-lookup"><span data-stu-id="43da2-108">Sizes</span></span>           |    <span data-ttu-id="43da2-109">Описание</span><span class="sxs-lookup"><span data-stu-id="43da2-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="43da2-110">Универсальные</span><span class="sxs-lookup"><span data-stu-id="43da2-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="43da2-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0–7</span><span class="sxs-lookup"><span data-stu-id="43da2-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span> | <span data-ttu-id="43da2-112">Сбалансированное соотношение ресурсов ЦП и памяти.</span><span class="sxs-lookup"><span data-stu-id="43da2-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="43da2-113">Идеальное решение для тестирования и разработки, небольших и средних баз данных, а также веб-серверов с небольшим или средним объемом трафика.</span><span class="sxs-lookup"><span data-stu-id="43da2-113">Ideal for testing and development, small to medium databases, and low to medium traffic web servers.</span></span> |
| [<span data-ttu-id="43da2-114">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="43da2-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="43da2-115">Fs, F</span><span class="sxs-lookup"><span data-stu-id="43da2-115">Fs, F</span></span>             | <span data-ttu-id="43da2-116">Высокое соотношение ресурсов ЦП и памяти.</span><span class="sxs-lookup"><span data-stu-id="43da2-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="43da2-117">Подходят для веб-серверов со средним объемом трафика, сетевых устройств, пакетных процессов и серверов приложений.</span><span class="sxs-lookup"><span data-stu-id="43da2-117">Good for medium traffic web servers, network appliances, batch processes, and application servers.</span></span>        |
| [<span data-ttu-id="43da2-118">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="43da2-118">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)         | <span data-ttu-id="43da2-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="43da2-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="43da2-120">Высокое соотношение ресурсов памяти и ядра.</span><span class="sxs-lookup"><span data-stu-id="43da2-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="43da2-121">Отлично подходят для серверов реляционной базы данных, кэша среднего и большого объема, а также выполняющейся в памяти аналитики.</span><span class="sxs-lookup"><span data-stu-id="43da2-121">Great for relational database servers, medium to large caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="43da2-122">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="43da2-122">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)        | <span data-ttu-id="43da2-123">Ls</span><span class="sxs-lookup"><span data-stu-id="43da2-123">Ls</span></span>                | <span data-ttu-id="43da2-124">Высокая пропускная способность дисков и количество операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="43da2-124">High disk throughput and IO.</span></span> <span data-ttu-id="43da2-125">Идеальный вариант для работы с большими данными, а также с базами данных SQL и NoSQL.</span><span class="sxs-lookup"><span data-stu-id="43da2-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="43da2-126">GPU</span><span class="sxs-lookup"><span data-stu-id="43da2-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="43da2-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="43da2-127">NV, NC</span></span>            | <span data-ttu-id="43da2-128">Специализированные виртуальные машины, предназначенные для ресурсоемкой отрисовки изображений и редактирования видео.</span><span class="sxs-lookup"><span data-stu-id="43da2-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="43da2-129">Доступны виртуальные машины одним или несколькими GPU.</span><span class="sxs-lookup"><span data-stu-id="43da2-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="43da2-130">Для высокопроизводительных вычислений</span><span class="sxs-lookup"><span data-stu-id="43da2-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="43da2-131">H, A8–A11</span><span class="sxs-lookup"><span data-stu-id="43da2-131">H, A8-11</span></span>          | <span data-ttu-id="43da2-132">Виртуальные машины с самыми быстрыми и мощными ЦП, для которых можно настроить сетевые интерфейсы с высокой пропускной способностью (RDMA).</span><span class="sxs-lookup"><span data-stu-id="43da2-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br> 

- <span data-ttu-id="43da2-133">Подробнее о ценах на различные размеры см. в разделе [Цены на виртуальные машины](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span><span class="sxs-lookup"><span data-stu-id="43da2-133">For information about pricing of the various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span></span> 
- <span data-ttu-id="43da2-134">Сведения об общих ограничениях виртуальных машин Azure см. в статье [Подписка Azure, границы, квоты и ограничения службы](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="43da2-134">To see general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="43da2-135">Стоимость хранилища рассчитывается отдельно в зависимости от количества страниц, используемых в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="43da2-135">Storage costs are calculated separately based on used pages in the storage account.</span></span> <span data-ttu-id="43da2-136">Дополнительные сведения см. на странице [Цены на хранилища Azure](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="43da2-136">For details, [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>
- <span data-ttu-id="43da2-137">Узнайте больше о том, как с помощью [единиц вычислений Azure (ACU)](acu.md) сравнить производительность вычислений для различных номеров SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="43da2-137">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>



## <a name="rest-api"></a><span data-ttu-id="43da2-138">Rest API</span><span class="sxs-lookup"><span data-stu-id="43da2-138">Rest API</span></span>

<span data-ttu-id="43da2-139">Сведения об использовании Rest API, чтобы получить сведения о размерах виртуальных машин, см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="43da2-139">For information on using the REST API to query for VM sizes, see the following:</span></span>

- <span data-ttu-id="43da2-140">[List available virtual machine sizes for resizing](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing) (Вывод доступных размеров виртуальных машин для изменения размеров)</span><span class="sxs-lookup"><span data-stu-id="43da2-140">[List available virtual machine sizes for resizing](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)</span></span>
- <span data-ttu-id="43da2-141">[List available virtual machine sizes for a subscription](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region) (Вывод доступных размеров виртуальных машин для подписки)</span><span class="sxs-lookup"><span data-stu-id="43da2-141">[List available virtual machine sizes for a subscription](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)</span></span>
- <span data-ttu-id="43da2-142">[List available virtual machine sizes in an availability set](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set) (Вывод доступных размеров виртуальных машин в группе доступности)</span><span class="sxs-lookup"><span data-stu-id="43da2-142">[List available virtual machine sizes in an availability set](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)</span></span>

## <a name="acu"></a><span data-ttu-id="43da2-143">ACU</span><span class="sxs-lookup"><span data-stu-id="43da2-143">ACU</span></span>

<span data-ttu-id="43da2-144">Узнайте больше о том, как с помощью [единиц вычислений Azure (ACU)](acu.md) сравнить производительность вычислений для различных номеров SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="43da2-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43da2-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="43da2-145">Next steps</span></span>

<span data-ttu-id="43da2-146">Узнайте больше о различных доступных размерах виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="43da2-146">Learn more about the different VM sizes that are available:</span></span>
- [<span data-ttu-id="43da2-147">Универсальные</span><span class="sxs-lookup"><span data-stu-id="43da2-147">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="43da2-148">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="43da2-148">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="43da2-149">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="43da2-149">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="43da2-150">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="43da2-150">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="43da2-151">Оптимизированные для GPU</span><span class="sxs-lookup"><span data-stu-id="43da2-151">GPU optimized</span></span>](sizes-gpu.md)
- [<span data-ttu-id="43da2-152">Для высокопроизводительных вычислений</span><span class="sxs-lookup"><span data-stu-id="43da2-152">High performance compute</span></span>](sizes-hpc.md)



