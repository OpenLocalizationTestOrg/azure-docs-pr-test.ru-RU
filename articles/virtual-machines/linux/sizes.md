---
title: "Размеры виртуальных машин Linux в Azure | Документация Майкрософт"
description: "Список различных размеров виртуальных машин Linux в Azure."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: da681171-f045-4c80-a5a9-d8bd47964673
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: fe7a92901ae25aa99ef71f09c416e6c6ad30d39b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="sizes-for-linux-virtual-machines-in-azure"></a><span data-ttu-id="683a3-103">Размеры виртуальных машин Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="683a3-103">Sizes for Linux virtual machines in Azure</span></span>
<span data-ttu-id="683a3-104">В этой статье описаны доступные размеры и разновидности виртуальных машин Azure, которые можно использовать для запуска приложений и рабочих нагрузок Linux.</span><span class="sxs-lookup"><span data-stu-id="683a3-104">This article describes the available sizes and options for the Azure virtual machines you can use to run your Linux apps and workloads.</span></span> <span data-ttu-id="683a3-105">Здесь также предоставлены рекомендации по развертыванию, которые нужно учитывать при планировании использования этих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="683a3-105">It also provides deployment considerations to be aware of when you're planning to use these resources.</span></span> <span data-ttu-id="683a3-106">Также доступна версия этой статьи для [виртуальных машин Windows](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="683a3-106">This article is also available for [Windows virtual machines](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


| <span data-ttu-id="683a3-107">Тип</span><span class="sxs-lookup"><span data-stu-id="683a3-107">Type</span></span>                     | <span data-ttu-id="683a3-108">Размеры</span><span class="sxs-lookup"><span data-stu-id="683a3-108">Sizes</span></span>           |    <span data-ttu-id="683a3-109">Описание</span><span class="sxs-lookup"><span data-stu-id="683a3-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="683a3-110">Универсальные</span><span class="sxs-lookup"><span data-stu-id="683a3-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="683a3-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0–7</span><span class="sxs-lookup"><span data-stu-id="683a3-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7,</span></span>  | <span data-ttu-id="683a3-112">Сбалансированное соотношение ресурсов ЦП и памяти.</span><span class="sxs-lookup"><span data-stu-id="683a3-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="683a3-113">Идеальное решение для тестирования и разработки, небольших и средних баз данных, а также веб-серверов с небольшим или средним объемом трафика.</span><span class="sxs-lookup"><span data-stu-id="683a3-113">Ideal for testing and development, small to medium databases, and low to medium traffic web servers.</span></span> |
| [<span data-ttu-id="683a3-114">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="683a3-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="683a3-115">Fs, F</span><span class="sxs-lookup"><span data-stu-id="683a3-115">Fs, F</span></span>             | <span data-ttu-id="683a3-116">Высокое соотношение ресурсов ЦП и памяти.</span><span class="sxs-lookup"><span data-stu-id="683a3-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="683a3-117">Подходят для веб-серверов со средним объемом трафика, сетевых устройств, пакетных процессов и серверов приложений.</span><span class="sxs-lookup"><span data-stu-id="683a3-117">Good for medium traffic web servers, network appliances, bath processes, and application servers.</span></span>        |
| [<span data-ttu-id="683a3-118">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="683a3-118">Memory optimized</span></span>](sizes-memory.md)         | <span data-ttu-id="683a3-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="683a3-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="683a3-120">Высокое соотношение ресурсов памяти и ядра.</span><span class="sxs-lookup"><span data-stu-id="683a3-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="683a3-121">Отлично подходят для серверов реляционной базы данных, кэша среднего и большого объема, а также выполняющейся в памяти аналитики.</span><span class="sxs-lookup"><span data-stu-id="683a3-121">Great for relational database servers, medium to large caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="683a3-122">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="683a3-122">Storage optimized</span></span>](sizes-storage.md)        | <span data-ttu-id="683a3-123">Ls</span><span class="sxs-lookup"><span data-stu-id="683a3-123">Ls</span></span>                | <span data-ttu-id="683a3-124">Высокая пропускная способность дисков и количество операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="683a3-124">High disk throughput and IO.</span></span> <span data-ttu-id="683a3-125">Идеальный вариант для работы с большими данными, а также с базами данных SQL и NoSQL.</span><span class="sxs-lookup"><span data-stu-id="683a3-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="683a3-126">GPU</span><span class="sxs-lookup"><span data-stu-id="683a3-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="683a3-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="683a3-127">NV, NC</span></span>            | <span data-ttu-id="683a3-128">Специализированные виртуальные машины, предназначенные для ресурсоемкой отрисовки изображений и редактирования видео.</span><span class="sxs-lookup"><span data-stu-id="683a3-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="683a3-129">Доступны виртуальные машины одним или несколькими GPU.</span><span class="sxs-lookup"><span data-stu-id="683a3-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="683a3-130">Для высокопроизводительных вычислений</span><span class="sxs-lookup"><span data-stu-id="683a3-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="683a3-131">H, A8–A11</span><span class="sxs-lookup"><span data-stu-id="683a3-131">H, A8-11</span></span>          | <span data-ttu-id="683a3-132">Виртуальные машины с самыми быстрыми и мощными ЦП, для которых можно настроить сетевые интерфейсы с высокой пропускной способностью (RDMA).</span><span class="sxs-lookup"><span data-stu-id="683a3-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br>

- <span data-ttu-id="683a3-133">Подробнее о ценах на различные размеры см. в разделе [Цены на виртуальные машины](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="683a3-133">For information about pricing of the various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span> 
- <span data-ttu-id="683a3-134">Доступность размеров виртуальных машин см. в статье [Доступность продуктов по регионам](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="683a3-134">For availability of VM sizes in Azure regions, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
- <span data-ttu-id="683a3-135">Сведения об общих ограничениях виртуальных машин Azure см. в статье [Подписка Azure, границы, квоты и ограничения службы](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="683a3-135">To see general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="683a3-136">Узнайте больше о том, как с помощью [единиц вычислений Azure (ACU)](../windows/acu.md) сравнить производительность вычислений для различных номеров SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="683a3-136">Learn more about how [Azure compute units (ACU)](../windows/acu.md) can help you compare compute performance across Azure SKUs.</span></span>


## <a name="rest-api"></a><span data-ttu-id="683a3-137">Rest API</span><span class="sxs-lookup"><span data-stu-id="683a3-137">Rest API</span></span>

<span data-ttu-id="683a3-138">Сведения об использовании Rest API, чтобы получить сведения о размерах виртуальных машин, см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="683a3-138">For information on using the REST API to query for VM sizes, see the following:</span></span>

- <span data-ttu-id="683a3-139">[List available virtual machine sizes for resizing](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing) (Вывод доступных размеров виртуальных машин для изменения размеров)</span><span class="sxs-lookup"><span data-stu-id="683a3-139">[List available virtual machine sizes for resizing](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)</span></span>
- <span data-ttu-id="683a3-140">[List available virtual machine sizes for a subscription](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region) (Вывод доступных размеров виртуальных машин для подписки)</span><span class="sxs-lookup"><span data-stu-id="683a3-140">[List available virtual machine sizes for a subscription](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)</span></span>
- <span data-ttu-id="683a3-141">[List available virtual machine sizes in an availability set](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set) (Вывод доступных размеров виртуальных машин в группе доступности)</span><span class="sxs-lookup"><span data-stu-id="683a3-141">[List available virtual machine sizes in an availability set](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)</span></span>

## <a name="acu"></a><span data-ttu-id="683a3-142">ACU</span><span class="sxs-lookup"><span data-stu-id="683a3-142">ACU</span></span>

<span data-ttu-id="683a3-143">Узнайте больше о том, как с помощью [единиц вычислений Azure (ACU)](acu.md) сравнить производительность вычислений для различных номеров SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="683a3-143">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="683a3-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="683a3-144">Next steps</span></span>

<span data-ttu-id="683a3-145">Узнайте больше о различных доступных размерах виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="683a3-145">Learn more about the different VM sizes that are available:</span></span>
- [<span data-ttu-id="683a3-146">Универсальные</span><span class="sxs-lookup"><span data-stu-id="683a3-146">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="683a3-147">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="683a3-147">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="683a3-148">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="683a3-148">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="683a3-149">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="683a3-149">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="683a3-150">GPU</span><span class="sxs-lookup"><span data-stu-id="683a3-150">GPU</span></span>](sizes-gpu.md)
- [<span data-ttu-id="683a3-151">Для высокопроизводительных вычислений</span><span class="sxs-lookup"><span data-stu-id="683a3-151">High performance compute</span></span>](sizes-hpc.md)



