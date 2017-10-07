---
title: "изменяет размер aaaLinux ВМ в Azure | Документы Microsoft"
description: "Список hello различные размеры, доступные для виртуальных машин Linux в Azure."
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
ms.openlocfilehash: 56cbe0a0d7d34def07636edba74c4c699e336012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-linux-virtual-machines-in-azure"></a><span data-ttu-id="0e963-103">Размеры виртуальных машин Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="0e963-103">Sizes for Linux virtual machines in Azure</span></span>
<span data-ttu-id="0e963-104">В этой статье описываются доступные размеры hello и параметры для hello виртуальных машинах Azure можно использовать toorun Linux приложений и рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="0e963-104">This article describes hello available sizes and options for hello Azure virtual machines you can use toorun your Linux apps and workloads.</span></span> <span data-ttu-id="0e963-105">Он также предоставляет toobe вопросы развертывания учитывать при планировании toouse эти ресурсы.</span><span class="sxs-lookup"><span data-stu-id="0e963-105">It also provides deployment considerations toobe aware of when you're planning toouse these resources.</span></span> <span data-ttu-id="0e963-106">Также доступна версия этой статьи для [виртуальных машин Windows](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0e963-106">This article is also available for [Windows virtual machines](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


| <span data-ttu-id="0e963-107">Тип</span><span class="sxs-lookup"><span data-stu-id="0e963-107">Type</span></span>                     | <span data-ttu-id="0e963-108">Размеры</span><span class="sxs-lookup"><span data-stu-id="0e963-108">Sizes</span></span>           |    <span data-ttu-id="0e963-109">Описание</span><span class="sxs-lookup"><span data-stu-id="0e963-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="0e963-110">Универсальные</span><span class="sxs-lookup"><span data-stu-id="0e963-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="0e963-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0–7</span><span class="sxs-lookup"><span data-stu-id="0e963-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7,</span></span>  | <span data-ttu-id="0e963-112">Сбалансированное соотношение ресурсов ЦП и памяти.</span><span class="sxs-lookup"><span data-stu-id="0e963-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="0e963-113">Идеально подходит для тестирования и разработки, toomedium небольших баз данных и низким toomedium трафик веб-серверов.</span><span class="sxs-lookup"><span data-stu-id="0e963-113">Ideal for testing and development, small toomedium databases, and low toomedium traffic web servers.</span></span> |
| [<span data-ttu-id="0e963-114">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="0e963-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="0e963-115">Fs, F</span><span class="sxs-lookup"><span data-stu-id="0e963-115">Fs, F</span></span>             | <span data-ttu-id="0e963-116">Высокое соотношение ресурсов ЦП и памяти.</span><span class="sxs-lookup"><span data-stu-id="0e963-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="0e963-117">Подходят для веб-серверов со средним объемом трафика, сетевых устройств, пакетных процессов и серверов приложений.</span><span class="sxs-lookup"><span data-stu-id="0e963-117">Good for medium traffic web servers, network appliances, bath processes, and application servers.</span></span>        |
| [<span data-ttu-id="0e963-118">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="0e963-118">Memory optimized</span></span>](sizes-memory.md)         | <span data-ttu-id="0e963-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="0e963-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="0e963-120">Высокое соотношение ресурсов памяти и ядра.</span><span class="sxs-lookup"><span data-stu-id="0e963-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="0e963-121">Идеально подходит для серверов реляционной базы данных, кэши средний toolarge и аналитики в памяти.</span><span class="sxs-lookup"><span data-stu-id="0e963-121">Great for relational database servers, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="0e963-122">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="0e963-122">Storage optimized</span></span>](sizes-storage.md)        | <span data-ttu-id="0e963-123">Ls</span><span class="sxs-lookup"><span data-stu-id="0e963-123">Ls</span></span>                | <span data-ttu-id="0e963-124">Высокая пропускная способность дисков и количество операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="0e963-124">High disk throughput and IO.</span></span> <span data-ttu-id="0e963-125">Идеальный вариант для работы с большими данными, а также с базами данных SQL и NoSQL.</span><span class="sxs-lookup"><span data-stu-id="0e963-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="0e963-126">GPU</span><span class="sxs-lookup"><span data-stu-id="0e963-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="0e963-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="0e963-127">NV, NC</span></span>            | <span data-ttu-id="0e963-128">Специализированные виртуальные машины, предназначенные для ресурсоемкой отрисовки изображений и редактирования видео.</span><span class="sxs-lookup"><span data-stu-id="0e963-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="0e963-129">Доступны виртуальные машины одним или несколькими GPU.</span><span class="sxs-lookup"><span data-stu-id="0e963-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="0e963-130">Для высокопроизводительных вычислений</span><span class="sxs-lookup"><span data-stu-id="0e963-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="0e963-131">H, A8–A11</span><span class="sxs-lookup"><span data-stu-id="0e963-131">H, A8-11</span></span>          | <span data-ttu-id="0e963-132">Виртуальные машины с самыми быстрыми и мощными ЦП, для которых можно настроить сетевые интерфейсы с высокой пропускной способностью (RDMA).</span><span class="sxs-lookup"><span data-stu-id="0e963-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br>

- <span data-ttu-id="0e963-133">Сведения о стоимости hello разного размера, в разделе [расценки на виртуальные машины](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="0e963-133">For information about pricing of hello various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span> 
- <span data-ttu-id="0e963-134">Доступность размеров виртуальных машин см. в статье [Доступность продуктов по регионам](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="0e963-134">For availability of VM sizes in Azure regions, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
- <span data-ttu-id="0e963-135">Общие ограничения toosee на виртуальных машинах Azure, в разделе [подписка Azure и ограничения служб, квоты и ограничения](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="0e963-135">toosee general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="0e963-136">Узнайте больше о том, как с помощью [единиц вычислений Azure (ACU)](../windows/acu.md) сравнить производительность вычислений для различных номеров SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="0e963-136">Learn more about how [Azure compute units (ACU)](../windows/acu.md) can help you compare compute performance across Azure SKUs.</span></span>


## <a name="rest-api"></a><span data-ttu-id="0e963-137">Rest API</span><span class="sxs-lookup"><span data-stu-id="0e963-137">Rest API</span></span>

<span data-ttu-id="0e963-138">Сведения об использовании tooquery hello API-интерфейса REST для размеров виртуальных Машин см. в следующем hello:</span><span class="sxs-lookup"><span data-stu-id="0e963-138">For information on using hello REST API tooquery for VM sizes, see hello following:</span></span>

- <span data-ttu-id="0e963-139">[List available virtual machine sizes for resizing](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing) (Вывод доступных размеров виртуальных машин для изменения размеров)</span><span class="sxs-lookup"><span data-stu-id="0e963-139">[List available virtual machine sizes for resizing](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)</span></span>
- <span data-ttu-id="0e963-140">[List available virtual machine sizes for a subscription](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region) (Вывод доступных размеров виртуальных машин для подписки)</span><span class="sxs-lookup"><span data-stu-id="0e963-140">[List available virtual machine sizes for a subscription](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)</span></span>
- <span data-ttu-id="0e963-141">[List available virtual machine sizes in an availability set](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set) (Вывод доступных размеров виртуальных машин в группе доступности)</span><span class="sxs-lookup"><span data-stu-id="0e963-141">[List available virtual machine sizes in an availability set](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)</span></span>

## <a name="acu"></a><span data-ttu-id="0e963-142">ACU</span><span class="sxs-lookup"><span data-stu-id="0e963-142">ACU</span></span>

<span data-ttu-id="0e963-143">Узнайте больше о том, как с помощью [единиц вычислений Azure (ACU)](acu.md) сравнить производительность вычислений для различных номеров SKU Azure.</span><span class="sxs-lookup"><span data-stu-id="0e963-143">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e963-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0e963-144">Next steps</span></span>

<span data-ttu-id="0e963-145">Дополнительные сведения о размерах виртуальных Машин различных hello, которые доступны.</span><span class="sxs-lookup"><span data-stu-id="0e963-145">Learn more about hello different VM sizes that are available:</span></span>
- [<span data-ttu-id="0e963-146">Универсальные</span><span class="sxs-lookup"><span data-stu-id="0e963-146">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="0e963-147">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="0e963-147">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="0e963-148">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="0e963-148">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="0e963-149">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="0e963-149">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="0e963-150">GPU</span><span class="sxs-lookup"><span data-stu-id="0e963-150">GPU</span></span>](sizes-gpu.md)
- [<span data-ttu-id="0e963-151">Для высокопроизводительных вычислений</span><span class="sxs-lookup"><span data-stu-id="0e963-151">High performance compute</span></span>](sizes-hpc.md)



