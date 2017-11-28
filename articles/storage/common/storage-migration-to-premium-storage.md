---
title: "Перенос виртуальных машин в хранилище Azure класса Premium | Документация Майкрософт"
description: "Перенесите существующие виртуальные машины в хранилище Azure класса Premium. Хранилище Premium обеспечивает поддержку дисков с высокой производительностью и малой задержкой для интенсивных рабочих нагрузок ввода-вывода на виртуальных машинах Azure."
services: storage
documentationcenter: na
author: yuemlu
manager: tadb
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: yuemlu
ms.openlocfilehash: ca893f87b155a92c457e3bf6d9d39aaf86bf5fb3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="migrating-to-azure-premium-storage-unmanaged-disks"></a><span data-ttu-id="979a9-104">Перенос в хранилище Azure класса Premium (использующее неуправляемые диски)</span><span class="sxs-lookup"><span data-stu-id="979a9-104">Migrating to Azure Premium Storage (Unmanaged Disks)</span></span>

> [!NOTE]
> <span data-ttu-id="979a9-105">В этой статье описывается, как перенести виртуальную машину, использующую неуправляемые диски уровня "Стандартный", в виртуальную машину, использующую неуправляемые диски уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="979a9-105">This article discusses how to migrate a VM that uses unmanaged standard disks to a VM that uses unmanaged premium disks.</span></span> <span data-ttu-id="979a9-106">Для новых виртуальных машин мы рекомендуем использовать Управляемые диски Azure и преобразовать неуправляемые диски в управляемые.</span><span class="sxs-lookup"><span data-stu-id="979a9-106">We recommend that you use Azure Managed Disks for new VMs, and that you convert your previous unmanaged disks to managed disks.</span></span> <span data-ttu-id="979a9-107">Вам не нужно обрабатывать базовые учетные записи хранения. Управляемые диски сделают это за вас.</span><span class="sxs-lookup"><span data-stu-id="979a9-107">Managed Disks handle the underlying storage accounts so you don't have to.</span></span> <span data-ttu-id="979a9-108">Дополнительные сведения см. в статье [Managed Disks Overview](../../virtual-machines/windows/managed-disks-overview.md) (Обзор Управляемых дисков).</span><span class="sxs-lookup"><span data-stu-id="979a9-108">For more information, please see our [Managed Disks Overview](../../virtual-machines/windows/managed-disks-overview.md).</span></span>
>

<span data-ttu-id="979a9-109">Хранилище Azure Premium обеспечивает поддержку дисков с высокой производительностью и малой задержкой для виртуальных машин с интенсивной рабочей нагрузкой ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="979a9-109">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="979a9-110">Диски виртуальной машины приложения можно перенести в хранилище Azure класса Premium, чтобы использовать их быстродействие и производительность.</span><span class="sxs-lookup"><span data-stu-id="979a9-110">You can take advantage of the speed and performance of these disks by migrating your application's VM disks to Azure Premium Storage.</span></span>

<span data-ttu-id="979a9-111">Это руководство призвано помочь новым пользователям службы хранилища Azure класса Premium подготовиться к плавному переходу из своей текущей системы к хранилищу класса Premium.</span><span class="sxs-lookup"><span data-stu-id="979a9-111">The purpose of this guide is to help new users of Azure Premium Storage better prepare to make a smooth transition from their current system to Premium Storage.</span></span> <span data-ttu-id="979a9-112">В руководстве рассматриваются три ключевых компонента процесса:</span><span class="sxs-lookup"><span data-stu-id="979a9-112">The guide addresses three of the key components in this process:</span></span>

* <span data-ttu-id="979a9-113">[планирование переноса в хранилище класса Premium](#plan-the-migration-to-premium-storage);</span><span class="sxs-lookup"><span data-stu-id="979a9-113">[Plan for the Migration to Premium Storage](#plan-the-migration-to-premium-storage)</span></span>
* <span data-ttu-id="979a9-114">[подготовка и копирование виртуальных жестких дисков (VHD) в хранилище класса Premium](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage);</span><span class="sxs-lookup"><span data-stu-id="979a9-114">[Prepare and Copy Virtual Hard Disks (VHDs) to Premium Storage](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)</span></span>
* <span data-ttu-id="979a9-115">[создание виртуальной машины Azure c использованием хранилища класса Premium](#create-azure-virtual-machine-using-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="979a9-115">[Create Azure Virtual Machine using Premium Storage](#create-azure-virtual-machine-using-premium-storage)</span></span>

<span data-ttu-id="979a9-116">Виртуальные машины можно перенести в хранилище класса Premium с других платформ. Кроме того, имеющиеся виртуальные машины Azure можно перенести из хранилища Azure класса Standard в хранилище класса Premium.</span><span class="sxs-lookup"><span data-stu-id="979a9-116">You can either migrate VMs from other platforms to Azure Premium Storage or migrate existing Azure VMs from Standard Storage to Premium Storage.</span></span> <span data-ttu-id="979a9-117">В этом руководстве рассматриваются оба этих сценария.</span><span class="sxs-lookup"><span data-stu-id="979a9-117">This guide covers steps for both two scenarios.</span></span> <span data-ttu-id="979a9-118">В зависимости от используемого сценария выполняйте инструкции, описанные в соответствующем разделе.</span><span class="sxs-lookup"><span data-stu-id="979a9-118">Follow the steps specified in the relevant section depending on your scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="979a9-119">Общие сведения о возможностях хранилища класса Premium и ценах на него см. в статье [Хранилище класса «Премиум»: высокопроизводительная служба хранилища для рабочих нагрузок виртуальных машин Azure](storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="979a9-119">You can find a feature overview and pricing of Premium Storage in Premium Storage: [High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span> <span data-ttu-id="979a9-120">Для оптимальной работы приложения рекомендуем переносить все диски виртуальных машин, требующие большого числа операций ввода-вывода в секунду, в хранилище Azure класса Premium.</span><span class="sxs-lookup"><span data-stu-id="979a9-120">We recommend migrating any virtual machine disk requiring high IOPS to Azure Premium Storage for the best performance for your application.</span></span> <span data-ttu-id="979a9-121">Если диск не требует большого числа операций ввода-вывода в секунду, выберите более доступное хранилище уровня Standard — в этом случае данные с диска виртуальной машины будут храниться не на твердотельных, а на жестких дисках.</span><span class="sxs-lookup"><span data-stu-id="979a9-121">If your disk does not require high IOPS, you can limit costs by maintaining it in Standard Storage, which stores virtual machine disk data on Hard Disk Drives (HDDs) instead of SSDs.</span></span>
>

<span data-ttu-id="979a9-122">Для полного завершения процесса переноса могут потребоваться дополнительные действия, предваряющие описанные в этом руководстве инструкции и следующие за ними.</span><span class="sxs-lookup"><span data-stu-id="979a9-122">Completing the migration process in its entirety may require additional actions both before and after the steps provided in this guide.</span></span> <span data-ttu-id="979a9-123">Например, может потребоваться настроить виртуальные сети или конечные точки, а также внести изменения в код самого приложения, для чего может потребоваться простой приложения.</span><span class="sxs-lookup"><span data-stu-id="979a9-123">Examples include configuring virtual networks or endpoints or making code changes within the application itself which may require some downtime in your application.</span></span> <span data-ttu-id="979a9-124">Эти действия будут отличаться для каждого приложения. Чтобы максимально плавно полностью перейти к хранилищу класса Premium, их следует выполнять в комплексе с инструкциями этого руководства.</span><span class="sxs-lookup"><span data-stu-id="979a9-124">These actions are unique to each application, and you should complete them along with the steps provided in this guide to make the full transition to Premium Storage as seamless as possible.</span></span>

## <span data-ttu-id="979a9-125"><a name="plan-the-migration-to-premium-storage"></a>Планирование переноса в хранилище класса Premium</span><span class="sxs-lookup"><span data-stu-id="979a9-125"><a name="plan-the-migration-to-premium-storage"></a>Plan for the migration to Premium Storage</span></span>
<span data-ttu-id="979a9-126">Сведения в этом разделе позволят вам подготовить среду к выполнению инструкций по переносу, описанных в этой статье, а также определить оптимальные типы виртуальных машин и дисков.</span><span class="sxs-lookup"><span data-stu-id="979a9-126">This section ensures that you are ready to follow the migration steps in this article, and helps you to make the best decision on VM and Disk types.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="979a9-127">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="979a9-127">Prerequisites</span></span>
* <span data-ttu-id="979a9-128">Вам понадобится подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="979a9-128">You will need an Azure subscription.</span></span> <span data-ttu-id="979a9-129">Если у вас нет подписки, можно оформить [бесплатную пробную](https://azure.microsoft.com/pricing/free-trial/) подписку на один месяц или посетить страницу [Цены Azure](https://azure.microsoft.com/pricing/), чтобы ознакомиться с дополнительными возможностями.</span><span class="sxs-lookup"><span data-stu-id="979a9-129">If you don't have one, you can create a one-month [free trial](https://azure.microsoft.com/pricing/free-trial/) subscription or visit [Azure Pricing](https://azure.microsoft.com/pricing/) for more options.</span></span>
* <span data-ttu-id="979a9-130">Чтобы выполнять командлеты PowerShell, вам потребуется модуль Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="979a9-130">To execute PowerShell cmdlets, you will need the Microsoft Azure PowerShell module.</span></span> <span data-ttu-id="979a9-131">Инструкции по установке см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="979a9-131">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the install point and installation instructions.</span></span>
* <span data-ttu-id="979a9-132">Если вы планируете использовать виртуальные машины Azure в хранилище класса Premium, эти машины должны поддерживать его.</span><span class="sxs-lookup"><span data-stu-id="979a9-132">When you plan to use Azure VMs running on Premium Storage, you need to use the Premium Storage capable VMs.</span></span> <span data-ttu-id="979a9-133">С этими виртуальными машинами можно использовать диски хранилища класса Premium и Standard.</span><span class="sxs-lookup"><span data-stu-id="979a9-133">You can use both Standard and Premium Storage disks with Premium Storage capable VMs.</span></span> <span data-ttu-id="979a9-134">Диски хранилища Premium в будущем будут доступны с большим количеством типов виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="979a9-134">Premium storage disks will be available with more VM types in the future.</span></span> <span data-ttu-id="979a9-135">Дополнительные сведения о всех доступных типах и размерах дисков виртуальной машины Azure см. в разделах [Размеры виртуальных машин](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) и [Размеры для облачных служб](../../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="979a9-135">For more information on all available Azure VM disk types and sizes, see [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sizes for Cloud Services](../../cloud-services/cloud-services-sizes-specs.md).</span></span>

### <a name="considerations"></a><span data-ttu-id="979a9-136">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="979a9-136">Considerations</span></span>
<span data-ttu-id="979a9-137">Виртуальные машины Azure поддерживают подключение нескольких дисков хранилища уровня "Премиум", за счет чего приложения могут использовать до 256 ТБ емкости на каждой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="979a9-137">An Azure VM supports attaching several Premium Storage disks so that your applications can have up to 256 TB of storage per VM.</span></span> <span data-ttu-id="979a9-138">С хранилищем Premium вы получите выполнение до 80 000 операций ввода-вывода в секунду на виртуальную машину и пропускную способность второго диска до 2000 МБ в секунду на виртуальную машину с очень низкой задержкой при операциях чтения.</span><span class="sxs-lookup"><span data-stu-id="979a9-138">With Premium Storage, your applications can achieve 80,000 IOPS (input/output operations per second) per VM and 2000 MB per second disk throughput per VM with extremely low latencies for read operations.</span></span> <span data-ttu-id="979a9-139">Вы можете выбирать виртуальные машины и диски среди множества различных вариантов.</span><span class="sxs-lookup"><span data-stu-id="979a9-139">You have options in a variety of VMs and Disks.</span></span> <span data-ttu-id="979a9-140">Сведения в этом разделе помогут выбрать оптимальный вариант для вашей рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="979a9-140">This section is to help you to find an option that best suits your workload.</span></span>

#### <a name="vm-sizes"></a><span data-ttu-id="979a9-141">Размеры виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="979a9-141">VM sizes</span></span>
<span data-ttu-id="979a9-142">Спецификации размеров виртуальных машин Azure перечислены в статье [Размеры виртуальных машин](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="979a9-142">The Azure VM size specifications are listed in [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="979a9-143">Просмотрите характеристики виртуальных машин, которые работают с хранилищем класса Premium, и выберите размер виртуальной машины, наиболее подходящий для вашей рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="979a9-143">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="979a9-144">Убедитесь, что виртуальная машина имеет достаточную пропускную способность для поддержки трафика диска.</span><span class="sxs-lookup"><span data-stu-id="979a9-144">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span></span>

#### <a name="disk-sizes"></a><span data-ttu-id="979a9-145">Размеры диска</span><span class="sxs-lookup"><span data-stu-id="979a9-145">Disk sizes</span></span>
<span data-ttu-id="979a9-146">Существуют пять типов дисков, которые можно использовать с виртуальной машиной. Для каждого из них действуют определенные ограничения на количество операций ввода-вывода в секунду и пропускную способность.</span><span class="sxs-lookup"><span data-stu-id="979a9-146">There are five types of disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="979a9-147">Учитывайте эти ограничения при выборе типа диска для вашей виртуальной машины в зависимости от потребностей приложения с точки зрения емкости, производительности, масштабируемости и пиковых нагрузок.</span><span class="sxs-lookup"><span data-stu-id="979a9-147">Take into consideration these limits when choosing the disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="979a9-148">Диски уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="979a9-148">Premium Disks Type</span></span>  | <span data-ttu-id="979a9-149">P10</span><span class="sxs-lookup"><span data-stu-id="979a9-149">P10</span></span>   | <span data-ttu-id="979a9-150">P20</span><span class="sxs-lookup"><span data-stu-id="979a9-150">P20</span></span>   | <span data-ttu-id="979a9-151">P30</span><span class="sxs-lookup"><span data-stu-id="979a9-151">P30</span></span>            | <span data-ttu-id="979a9-152">P40</span><span class="sxs-lookup"><span data-stu-id="979a9-152">P40</span></span>            | <span data-ttu-id="979a9-153">P50</span><span class="sxs-lookup"><span data-stu-id="979a9-153">P50</span></span>            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| <span data-ttu-id="979a9-154">Размер диска</span><span class="sxs-lookup"><span data-stu-id="979a9-154">Disk size</span></span>           | <span data-ttu-id="979a9-155">128 ГБ</span><span class="sxs-lookup"><span data-stu-id="979a9-155">128 GB</span></span>| <span data-ttu-id="979a9-156">512 ГБ</span><span class="sxs-lookup"><span data-stu-id="979a9-156">512 GB</span></span>| <span data-ttu-id="979a9-157">1024 ГБ (1 ТБ)</span><span class="sxs-lookup"><span data-stu-id="979a9-157">1024 GB (1 TB)</span></span> | <span data-ttu-id="979a9-158">2048 ГБ (2 ТБ)</span><span class="sxs-lookup"><span data-stu-id="979a9-158">2048 GB (2 TB)</span></span> | <span data-ttu-id="979a9-159">4095 ГБ (4 ТБ)</span><span class="sxs-lookup"><span data-stu-id="979a9-159">4095 GB (4 TB)</span></span> | 
| <span data-ttu-id="979a9-160">Количество операций ввода-вывода в секунду на диск</span><span class="sxs-lookup"><span data-stu-id="979a9-160">IOPS per disk</span></span>       | <span data-ttu-id="979a9-161">500</span><span class="sxs-lookup"><span data-stu-id="979a9-161">500</span></span>   | <span data-ttu-id="979a9-162">2300</span><span class="sxs-lookup"><span data-stu-id="979a9-162">2300</span></span>  | <span data-ttu-id="979a9-163">5000</span><span class="sxs-lookup"><span data-stu-id="979a9-163">5000</span></span>           | <span data-ttu-id="979a9-164">7500</span><span class="sxs-lookup"><span data-stu-id="979a9-164">7500</span></span>           | <span data-ttu-id="979a9-165">7500</span><span class="sxs-lookup"><span data-stu-id="979a9-165">7500</span></span>           | 
| <span data-ttu-id="979a9-166">Пропускная способность на диск</span><span class="sxs-lookup"><span data-stu-id="979a9-166">Throughput per disk</span></span> | <span data-ttu-id="979a9-167">100 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="979a9-167">100 MB per second</span></span> | <span data-ttu-id="979a9-168">150 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="979a9-168">150 MB per second</span></span> | <span data-ttu-id="979a9-169">200 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="979a9-169">200 MB per second</span></span> | <span data-ttu-id="979a9-170">250 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="979a9-170">250 MB per second</span></span> | <span data-ttu-id="979a9-171">250 МБ в секунду</span><span class="sxs-lookup"><span data-stu-id="979a9-171">250 MB per second</span></span> |

<span data-ttu-id="979a9-172">В зависимости от рабочей нагрузки определите, требуются ли дополнительные диски данных для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="979a9-172">Depending on your workload, determine if additional data disks are necessary for your VM.</span></span> <span data-ttu-id="979a9-173">К виртуальной машине можно подключить несколько дисков постоянных данных.</span><span class="sxs-lookup"><span data-stu-id="979a9-173">You can attach several persistent data disks to your VM.</span></span> <span data-ttu-id="979a9-174">Если необходимо увеличить емкость и производительность тома, вы можете создать на дисках чередующийся том.</span><span class="sxs-lookup"><span data-stu-id="979a9-174">If needed, you can stripe across the disks to increase the capacity and performance of the volume.</span></span> <span data-ttu-id="979a9-175">(Дополнительные сведения о чередовании дисков см. [здесь](storage-premium-storage-performance.md#disk-striping).) Если вы создаете чередующийся том на дисках данных хранилища уровня "Премиум" с помощью [дисковых пространств][4], то необходимо настроить по одному столбцу для каждого используемого диска.</span><span class="sxs-lookup"><span data-stu-id="979a9-175">(See what is Disk Striping [here](storage-premium-storage-performance.md#disk-striping).) If you stripe Premium Storage data disks using [Storage Spaces][4], you should configure it with one column for each disk that is used.</span></span> <span data-ttu-id="979a9-176">В противном случае из-за неравномерного распределения трафика между дисками общая производительность чередующегося тома может быть ниже ожидаемой.</span><span class="sxs-lookup"><span data-stu-id="979a9-176">Otherwise, the overall performance of the striped volume may be lower than expected due to uneven distribution of traffic across the disks.</span></span> <span data-ttu-id="979a9-177">Выполнить эту же операцию на виртуальных машинах с Linux можно с помощью служебной программы *mdadm*.</span><span class="sxs-lookup"><span data-stu-id="979a9-177">For Linux VMs you can use the *mdadm* utility to achieve the same.</span></span> <span data-ttu-id="979a9-178">Дополнительные сведения см. в статье [Настройка программного RAID-массива в Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="979a9-178">See article [Configure Software RAID on Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for details.</span></span>

#### <a name="storage-account-scalability-targets"></a><span data-ttu-id="979a9-179">Целевые показатели масштабируемости для учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="979a9-179">Storage account scalability targets</span></span>
<span data-ttu-id="979a9-180">У учетных записей хранения класса Premium есть следующие целевые показатели масштабируемости в дополнение к [целевым показателям масштабируемости и производительности службы хранилища Azure](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="979a9-180">Premium Storage accounts have the following scalability targets in addition to the [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="979a9-181">Если потребности вашего приложения превышают целевые показатели по масштабируемости для отдельной учетной записи хранения, при создании настройте приложение на использование нескольких учетных записей хранения и распределите данные между этими учетными записями.</span><span class="sxs-lookup"><span data-stu-id="979a9-181">If your application requirements exceed the scalability targets of a single storage account, build your application to use multiple storage accounts, and partition your data across those storage accounts.</span></span>

| <span data-ttu-id="979a9-182">Общая емкость учетной записи</span><span class="sxs-lookup"><span data-stu-id="979a9-182">Total Account Capacity</span></span> | <span data-ttu-id="979a9-183">Общая пропускная способность для учетной записи локально избыточного хранилища</span><span class="sxs-lookup"><span data-stu-id="979a9-183">Total Bandwidth for a Locally Redundant Storage Account</span></span> |
|:--- |:--- |
| <span data-ttu-id="979a9-184">Емкость диска: 35 ТБ</span><span class="sxs-lookup"><span data-stu-id="979a9-184">Disk capacity: 35TB</span></span><br /><span data-ttu-id="979a9-185">Емкость для моментальных снимков: 10 ТБ</span><span class="sxs-lookup"><span data-stu-id="979a9-185">Snapshot capacity: 10 TB</span></span> |<span data-ttu-id="979a9-186">До 50 гигабит в секунду для входящих и исходящих подключений</span><span class="sxs-lookup"><span data-stu-id="979a9-186">Up to 50 gigabits per second for Inbound + Outbound</span></span> |

<span data-ttu-id="979a9-187">Дополнительные сведения о характеристиках хранилища класса "Премиум" см. в разделе [Целевые показатели масштабируемости и производительности при использовании хранилища класса "Премиум"](storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="979a9-187">For the more information on Premium Storage specifications, check out [Scalability and Performance Targets when using Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span></span>

#### <a name="disk-caching-policy"></a><span data-ttu-id="979a9-188">Политика кэширования дисков</span><span class="sxs-lookup"><span data-stu-id="979a9-188">Disk caching policy</span></span>
<span data-ttu-id="979a9-189">По умолчанию для политики кэширования дисков задано значение *только чтение* для всех дисков с данными "Премиум" и *чтение и запись* для дисков операционной системы "Премиум", подключенных к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="979a9-189">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span></span> <span data-ttu-id="979a9-190">Этот параметр конфигурации рекомендуется использовать, чтобы достичь оптимальной производительности при операциях ввода-вывода приложения.</span><span class="sxs-lookup"><span data-stu-id="979a9-190">This configuration setting is recommended to achieve the optimal performance for your application's IOs.</span></span> <span data-ttu-id="979a9-191">Отключите кэширование дисков данных, которые отличаются высокой интенсивностью записи или используются только для записи (например, файлов журналов SQL Server), чтобы улучшить производительность приложения.</span><span class="sxs-lookup"><span data-stu-id="979a9-191">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span> <span data-ttu-id="979a9-192">Параметры кэша для существующих дисков данных можно изменить с помощью [портала Azure](https://portal.azure.com) или параметра *-HostCaching* командлета *Set-AzureDataDisk*.</span><span class="sxs-lookup"><span data-stu-id="979a9-192">The cache settings for existing data disks can be updated using [Azure Portal](https://portal.azure.com) or the *-HostCaching* parameter of the *Set-AzureDataDisk* cmdlet.</span></span>

#### <a name="location"></a><span data-ttu-id="979a9-193">Расположение</span><span class="sxs-lookup"><span data-stu-id="979a9-193">Location</span></span>
<span data-ttu-id="979a9-194">Выберите расположение, где доступно хранилище Azure Premium.</span><span class="sxs-lookup"><span data-stu-id="979a9-194">Pick a location where Azure Premium Storage is available.</span></span> <span data-ttu-id="979a9-195">Актуальные сведения о доступных расположениях см. на странице [Доступность продуктов по регионам](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="979a9-195">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span> <span data-ttu-id="979a9-196">Виртуальные машины, расположенные в одном регионе с учетной записью хранения, где хранятся диски для виртуальной машины, обеспечивают более высокую производительность, чем находящиеся в других регионах.</span><span class="sxs-lookup"><span data-stu-id="979a9-196">VMs located in the same region as the Storage account that stores the disks for the VM will give much better performance than if they are in separate regions.</span></span>

#### <a name="other-azure-vm-configuration-settings"></a><span data-ttu-id="979a9-197">Прочие параметры конфигурации виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="979a9-197">Other Azure VM configuration settings</span></span>
<span data-ttu-id="979a9-198">При создании виртуальной машины Azure появится запрос на настройку некоторых ее параметров.</span><span class="sxs-lookup"><span data-stu-id="979a9-198">When creating an Azure VM, you will be asked to configure certain VM settings.</span></span> <span data-ttu-id="979a9-199">Помните, что одни параметры фиксируются на все время существования виртуальной машины, а другие можно изменить или добавить позже.</span><span class="sxs-lookup"><span data-stu-id="979a9-199">Remember, few settings are fixed for the lifetime of the VM, while you can modify or add others later.</span></span> <span data-ttu-id="979a9-200">Просмотрите эти параметры конфигурации виртуальной машины Azure и убедитесь, что они настроены правильно в соответствии с требованиями вашей рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="979a9-200">Review these Azure VM configuration settings and make sure that these are configured appropriately to match your workload requirements.</span></span>

### <a name="optimization"></a><span data-ttu-id="979a9-201">Оптимизация</span><span class="sxs-lookup"><span data-stu-id="979a9-201">Optimization</span></span>
<span data-ttu-id="979a9-202">В статье [Хранилище Azure класса «Премиум»: разработка, обеспечивающая повышенную производительность](storage-premium-storage-performance.md) приведены рекомендации по разработке высокопроизводительных приложений с использованием хранилища Azure класса Premium.</span><span class="sxs-lookup"><span data-stu-id="979a9-202">[Azure Premium Storage: Design for High Performance](storage-premium-storage-performance.md) provides guidelines for building high-performance applications using Azure Premium Storage.</span></span> <span data-ttu-id="979a9-203">Эти рекомендации можно использовать вместе с рекомендациями по производительности, применимыми к технологиям, используемым приложением.</span><span class="sxs-lookup"><span data-stu-id="979a9-203">You can follow the guidelines combined with performance best practices applicable to technologies used by your application.</span></span>

## <span data-ttu-id="979a9-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Подготовка VHD и их копирование в хранилище класса Premium</span><span class="sxs-lookup"><span data-stu-id="979a9-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Prepare and copy virtual hard disks (VHDs) to Premium Storage</span></span>
<span data-ttu-id="979a9-205">В следующем разделе приведены рекомендации по подготовке VHD на виртуальной машине и их копированию в службу хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="979a9-205">The following section provides guidelines for preparing VHDs from your VM and copying VHDs to Azure Storage.</span></span>

* [<span data-ttu-id="979a9-206">Сценарий 1. Перенос имеющихся виртуальных машин Azure в хранилище Azure класса Premium</span><span class="sxs-lookup"><span data-stu-id="979a9-206">Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span></span>](#scenario1)
* [<span data-ttu-id="979a9-207">Сценарий 2. Перенос виртуальных машин в хранилище Azure класса Premium с других платформ</span><span class="sxs-lookup"><span data-stu-id="979a9-207">Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span></span>](#scenario2)

### <a name="prerequisites"></a><span data-ttu-id="979a9-208">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="979a9-208">Prerequisites</span></span>
<span data-ttu-id="979a9-209">Чтобы подготовить VHD к переносу, требуется следующее:</span><span class="sxs-lookup"><span data-stu-id="979a9-209">To prepare the VHDs for migration, you'll need:</span></span>

* <span data-ttu-id="979a9-210">Подписка Azure, учетная запись хранения и контейнер в этой учетной записи хранения, куда будет скопирован VHD.</span><span class="sxs-lookup"><span data-stu-id="979a9-210">An Azure subscription, a storage account, and a container in that storage account to which you can copy your VHD.</span></span> <span data-ttu-id="979a9-211">Обратите внимание, что целевой учетной записью хранения может быть учетная запись хранения Standard или Premium в зависимости от требований.</span><span class="sxs-lookup"><span data-stu-id="979a9-211">Note that the destination storage account can be a Standard or Premium Storage account depending on your requirement.</span></span>
* <span data-ttu-id="979a9-212">Средство для обобщения VHD, если на его основе планируется создать несколько экземпляров виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="979a9-212">A tool to generalize the VHD if you plan to create multiple VM instances from it.</span></span> <span data-ttu-id="979a9-213">Например, sysprep для Windows или virt-sysprep для Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="979a9-213">For example, sysprep for Windows or virt-sysprep for Ubuntu.</span></span>
* <span data-ttu-id="979a9-214">Средство загрузки VHD-файла в учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="979a9-214">A tool to upload the VHD file to the Storage account.</span></span> <span data-ttu-id="979a9-215">См. раздел [Передача данных с помощью служебной программы командной строки AzCopy](storage-use-azcopy.md) или воспользуйтесь [обозревателем хранилищ Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="979a9-215">See [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md) or use an [Azure storage explorer](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span></span> <span data-ttu-id="979a9-216">В этом руководстве описано копирование виртуального жесткого диска с помощью средства AzCopy.</span><span class="sxs-lookup"><span data-stu-id="979a9-216">This guide describes copying your VHD using the AzCopy tool.</span></span>

> [!NOTE]
> <span data-ttu-id="979a9-217">Чтобы добиться оптимальной производительности при синхронном копировании с помощью AzCopy, скопируйте VHD, запустив одно из средств на виртуальной машине Azure, которая принадлежит к тому же региону, что и целевая учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="979a9-217">If you choose synchronous copy option with AzCopy, for optimal performance, copy your VHD by running one of these tools from an Azure VM that is in the same region as the destination storage account.</span></span> <span data-ttu-id="979a9-218">При копировании виртуального жесткого диска из виртуальной машины Azure в другом регионе производительность может быть ниже.</span><span class="sxs-lookup"><span data-stu-id="979a9-218">If you are copying a VHD from an Azure VM in a different region, your performance may be slower.</span></span>
>
> <span data-ttu-id="979a9-219">Для копирования большого объема данных при ограниченной пропускной способности можно [использовать службу импорта и экспорта Azure для передачи данных в хранилище BLOB-объектов](../storage-import-export-service.md). Это позволит перенести данные, доставив жесткие диски в центр обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="979a9-219">For copying a large amount of data over limited bandwidth, consider [using the Azure Import/Export service to transfer data to Blob Storage](../storage-import-export-service.md); this allows you to transfer your data by shipping hard disk drives to an Azure datacenter.</span></span> <span data-ttu-id="979a9-220">С помощью службы импорта и экспорта данных Azure можно скопировать данные только в учетную запись хранения Standard.</span><span class="sxs-lookup"><span data-stu-id="979a9-220">You can use the Azure Import/Export service to copy data to a standard storage account only.</span></span> <span data-ttu-id="979a9-221">После переноса данных в учетную запись хранения категории "Стандартный" их можно передать в учетную запись хранилища класса "Премиум" с помощью [API-копирования BLOB-объектов](https://msdn.microsoft.com/library/azure/dd894037.aspx) или AzCopy.</span><span class="sxs-lookup"><span data-stu-id="979a9-221">Once the data is in your standard storage account, you can use either the [Copy Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) or AzCopy to transfer the data to your premium storage account.</span></span>
>
> <span data-ttu-id="979a9-222">Обратите внимание, что Microsoft Azure поддерживает только файлы виртуальных жестких дисков фиксированного размера.</span><span class="sxs-lookup"><span data-stu-id="979a9-222">Note that Microsoft Azure only supports fixed size VHD files.</span></span> <span data-ttu-id="979a9-223">VHDX-файлы или динамические виртуальные жесткие диски не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="979a9-223">VHDX files or dynamic VHDs are not supported.</span></span> <span data-ttu-id="979a9-224">При наличии динамический виртуальный жесткий диск можно преобразовать в диск фиксированного размера с помощью командлета [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) .</span><span class="sxs-lookup"><span data-stu-id="979a9-224">If you have a dynamic VHD, you can convert it to fixed size using the [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span></span>
>
>

### <span data-ttu-id="979a9-225"><a name="scenario1"></a>Сценарий 1. Перенос имеющихся виртуальных машин Azure в хранилище Azure класса Premium</span><span class="sxs-lookup"><span data-stu-id="979a9-225"><a name="scenario1"></a>Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span></span>
<span data-ttu-id="979a9-226">При переносе имеющихся виртуальных машин Azure остановите работу виртуальной машины, подготовьте VHD в зависимости от выбранного типа, а затем скопируйте диск с помощью AzCopy или PowerShell.</span><span class="sxs-lookup"><span data-stu-id="979a9-226">If you are migrating existing Azure VMs, stop the VM, prepare VHDs per the type of VHD you want, and then copy the VHD with AzCopy or PowerShell.</span></span>

<span data-ttu-id="979a9-227">Чтобы виртуальная машина перешла в исходное состояние, она должна быть полностью выключена.</span><span class="sxs-lookup"><span data-stu-id="979a9-227">The VM needs to be completely down to migrate a clean state.</span></span> <span data-ttu-id="979a9-228">Простой будет длиться до завершения переноса.</span><span class="sxs-lookup"><span data-stu-id="979a9-228">There will be a downtime until the migration completes.</span></span>

#### <a name="step-1-prepare-vhds-for-migration"></a><span data-ttu-id="979a9-229">Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="979a9-229">Step 1.</span></span> <span data-ttu-id="979a9-230">Подготовка VHD к переносу</span><span class="sxs-lookup"><span data-stu-id="979a9-230">Prepare VHDs for migration</span></span>
<span data-ttu-id="979a9-231">При переносе имеющихся виртуальных машин Azure в хранилище класса Premium VHD может представлять собой:</span><span class="sxs-lookup"><span data-stu-id="979a9-231">If you are migrating existing Azure VMs to Premium Storage, your VHD may be:</span></span>

* <span data-ttu-id="979a9-232">обобщенный образ операционной системы;</span><span class="sxs-lookup"><span data-stu-id="979a9-232">A generalized operating system image</span></span>
* <span data-ttu-id="979a9-233">уникальный диск операционной системы;</span><span class="sxs-lookup"><span data-stu-id="979a9-233">A unique operating system disk</span></span>
* <span data-ttu-id="979a9-234">диск данных.</span><span class="sxs-lookup"><span data-stu-id="979a9-234">A data disk</span></span>

<span data-ttu-id="979a9-235">Ниже рассмотрены три соответствующих сценария подготовки VHD.</span><span class="sxs-lookup"><span data-stu-id="979a9-235">Below we walk through these 3 scenarios for preparing your VHD.</span></span>

##### <a name="use-a-generalized-operating-system-vhd-to-create-multiple-vm-instances"></a><span data-ttu-id="979a9-236">Использование обобщенного VHD операционной системы для создания нескольких экземпляров виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="979a9-236">Use a generalized Operating System VHD to create multiple VM instances</span></span>
<span data-ttu-id="979a9-237">При загрузке виртуального жесткого диска, который будет использоваться для создания нескольких экземпляров универсальной ВМ Azure, необходимо сначала произвести обобщение виртуального жесткого диска с помощью программы sysprep.</span><span class="sxs-lookup"><span data-stu-id="979a9-237">If you are uploading a VHD that will be used to create multiple generic Azure VM instances, you must first generalize VHD using a sysprep utility.</span></span> <span data-ttu-id="979a9-238">Это применимо для локального или находящегося в облаке виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="979a9-238">This applies to a VHD that is on-premises or in the cloud.</span></span> <span data-ttu-id="979a9-239">Служебная программа sysprep удаляет все сведения о компьютере с VHD.</span><span class="sxs-lookup"><span data-stu-id="979a9-239">Sysprep removes any machine-specific information from the VHD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="979a9-240">Создайте моментальный снимок или резервную копию виртуальной машины перед ее обобщением.</span><span class="sxs-lookup"><span data-stu-id="979a9-240">Take a snapshot or backup your VM before generalizing it.</span></span> <span data-ttu-id="979a9-241">После запуска sysprep останавливается работа экземпляра виртуальной машины и отменяется его выделение.</span><span class="sxs-lookup"><span data-stu-id="979a9-241">Running sysprep will stop and deallocate the VM instance.</span></span> <span data-ttu-id="979a9-242">Выполните описанные ниже шаги, чтобы запустить sysprep для виртуального жесткого диска операционной системы Windows.</span><span class="sxs-lookup"><span data-stu-id="979a9-242">Follow steps below to sysprep a Windows OS VHD.</span></span> <span data-ttu-id="979a9-243">Обратите внимание, что для запуска команды Sysprep потребуется завершить работу виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="979a9-243">Note that running the Sysprep command will require you to shut down the virtual machine.</span></span> <span data-ttu-id="979a9-244">Дополнительные сведения о команде Sysprep см. в разделах [Обзор Sysprep](http://technet.microsoft.com/library/hh825209.aspx) или [Технический справочник по Sysprep](http://technet.microsoft.com/library/cc766049.aspx).</span><span class="sxs-lookup"><span data-stu-id="979a9-244">For more information about Sysprep, see [Sysprep Overview](http://technet.microsoft.com/library/hh825209.aspx) or [Sysprep Technical Reference](http://technet.microsoft.com/library/cc766049.aspx).</span></span>
>
>

1. <span data-ttu-id="979a9-245">Откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="979a9-245">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="979a9-246">Введите следующую команду, чтобы открыть Sysrep:</span><span class="sxs-lookup"><span data-stu-id="979a9-246">Enter the following command to open Sysprep:</span></span>

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. <span data-ttu-id="979a9-247">В средстве подготовки системы выберите "Ввод системной автоматизации OOBE", установите флажок "Обобщение", выберите **Завершение работы** и затем нажмите **ОК**, как показано на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="979a9-247">In the System Preparation Tool, select Enter System Out-of-Box Experience (OOBE), select the Generalize check box, select **Shutdown**, and then click **OK**, as shown in the image below.</span></span> <span data-ttu-id="979a9-248">Служебная программа sysprep обобщит операционную систему и завершит ее работу.</span><span class="sxs-lookup"><span data-stu-id="979a9-248">Sysprep will generalize the operating system and shut down the system.</span></span>

    ![][1]

<span data-ttu-id="979a9-249">Для виртуальной машины Ubuntu используйте virt-sysrep для достижения этой же цели.</span><span class="sxs-lookup"><span data-stu-id="979a9-249">For an Ubuntu VM, use virt-sysprep to achieve the same.</span></span> <span data-ttu-id="979a9-250">Дополнительные сведения см. в разделе [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html).</span><span class="sxs-lookup"><span data-stu-id="979a9-250">See [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) for more details.</span></span> <span data-ttu-id="979a9-251">См. также прочее [программное обеспечение для подготовки серверов Linux](http://www.cyberciti.biz/tips/server-provisioning-software.html) с открытым кодом при использовании других операционных систем Linux.</span><span class="sxs-lookup"><span data-stu-id="979a9-251">See also some of the open source [Linux Server Provisioning software](http://www.cyberciti.biz/tips/server-provisioning-software.html) for other Linux operating systems.</span></span>

##### <a name="use-a-unique-operating-system-vhd-to-create-a-single-vm-instance"></a><span data-ttu-id="979a9-252">Использование уникального VHD операционной системы для создания одного экземпляра виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="979a9-252">Use a unique Operating System VHD to create a single VM instance</span></span>
<span data-ttu-id="979a9-253">При наличии приложения, которое работает на виртуальной машине и для которого требуются данные конкретного компьютера, не обобщайте виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="979a9-253">If you have an application running on the VM which requires the machine specific data, do not generalize the VHD.</span></span> <span data-ttu-id="979a9-254">Необобщенный виртуальный жесткий диск может использоваться для создания уникального экземпляра виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="979a9-254">A non-generalized VHD can be used to create a unique Azure VM instance.</span></span> <span data-ttu-id="979a9-255">Например, при наличии контроллера домена на вашем виртуальном жестком диске выполнение команды sysprep сделает его неэффективным в качестве контроллера домена.</span><span class="sxs-lookup"><span data-stu-id="979a9-255">For example, if you have Domain Controller on your VHD, executing sysprep will make it ineffective as a Domain Controller.</span></span> <span data-ttu-id="979a9-256">Просмотрите приложения, выполняющиеся на виртуальной машине, а также влияние sysprep на них, прежде чем обобщить VHD.</span><span class="sxs-lookup"><span data-stu-id="979a9-256">Review the applications running on your VM and the impact of running sysprep on them before generalizing the VHD.</span></span>

##### <a name="register-data-disk-vhd"></a><span data-ttu-id="979a9-257">Регистрация VHD в качестве диска данных</span><span class="sxs-lookup"><span data-stu-id="979a9-257">Register data disk VHD</span></span>
<span data-ttu-id="979a9-258">При наличии подлежащих переносу дисков с данными необходимо завершить работу виртуальных машин, использующих эти диски данных.</span><span class="sxs-lookup"><span data-stu-id="979a9-258">If you have data disks in Azure to be migrated, you must make sure the VMs that use these data disks are shut down.</span></span>

<span data-ttu-id="979a9-259">Выполните шаги ниже, чтобы скопировать VHD в хранилище Azure класса Premium и зарегистрировать диск в качестве подготовленного диска данных.</span><span class="sxs-lookup"><span data-stu-id="979a9-259">Follow the steps described below to copy VHD to Azure Premium Storage and register it as a provisioned data disk.</span></span>

#### <a name="step-2-create-the-destination-for-your-vhd"></a><span data-ttu-id="979a9-260">Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="979a9-260">Step 2.</span></span> <span data-ttu-id="979a9-261">Создание целевого объекта для виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="979a9-261">Create the destination for your VHD</span></span>
<span data-ttu-id="979a9-262">Создайте учетную запись хранения для обслуживания виртуальных жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="979a9-262">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="979a9-263">При планировании места хранения VHD учитывайте следующие аспекты.</span><span class="sxs-lookup"><span data-stu-id="979a9-263">Consider the following points when planning where to store your VHDs:</span></span>

* <span data-ttu-id="979a9-264">У целевой учетной записи хранения должен быть класс Premium.</span><span class="sxs-lookup"><span data-stu-id="979a9-264">The target Premium storage account.</span></span>
* <span data-ttu-id="979a9-265">Расположение учетной записи хранения должно совпадать с расположением виртуальных машин Azure хранилища класса Premium, которые будут созданы на последнем этапе.</span><span class="sxs-lookup"><span data-stu-id="979a9-265">The storage account location must be same as Premium Storage capable Azure VMs you will create in the final stage.</span></span> <span data-ttu-id="979a9-266">Можно скопировать в новую учетную запись хранения или запланировать использование прежней учетной записи в зависимости от требований.</span><span class="sxs-lookup"><span data-stu-id="979a9-266">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span></span>
* <span data-ttu-id="979a9-267">Скопируйте и сохраните ключ целевой учетной записи хранения для следующего этапа.</span><span class="sxs-lookup"><span data-stu-id="979a9-267">Copy and save the storage account key of the destination storage account for the next stage.</span></span>

<span data-ttu-id="979a9-268">В учетной записи хранения класса Standard можно хранить некоторые диски данных (например, диски, данные которых используются не так часто), но мы настоятельно рекомендуем перенести все данные рабочей нагрузки в хранилище класса Premium.</span><span class="sxs-lookup"><span data-stu-id="979a9-268">For data disks, you can choose to keep some data disks in a standard storage account (for example, disks that have cooler storage), but we strongly recommend you moving all data for production workload to use premium storage.</span></span>

#### <span data-ttu-id="979a9-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="979a9-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Step 3.</span></span> <span data-ttu-id="979a9-270">Копирование VHD с помощью AzCopy или PowerShell</span><span class="sxs-lookup"><span data-stu-id="979a9-270">Copy VHD with AzCopy or PowerShell</span></span>
<span data-ttu-id="979a9-271">Чтобы скопировать VHD с помощью одного из этих средств, вам понадобится путь контейнера и ключ учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="979a9-271">You will need to find your container path and storage account key to process either of these two options.</span></span> <span data-ttu-id="979a9-272">(выберите **Портал Azure** > **Хранилище**, чтобы узнать их).</span><span class="sxs-lookup"><span data-stu-id="979a9-272">Container path and storage account key can be found in **Azure Portal** > **Storage**.</span></span> <span data-ttu-id="979a9-273">URL-адрес контейнера должен выглядеть так: https://myaccount.blob.core.windows.net/mycontainer/.</span><span class="sxs-lookup"><span data-stu-id="979a9-273">The container URL will be like "https://myaccount.blob.core.windows.net/mycontainer/".</span></span>

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a><span data-ttu-id="979a9-274">Способ 1. Копирование VHD с помощью AzCopy (асинхронное копирование)</span><span class="sxs-lookup"><span data-stu-id="979a9-274">Option 1: Copy a VHD with AzCopy (Asynchronous copy)</span></span>
<span data-ttu-id="979a9-275">Средство AzCopy позволяет легко передать VHD через Интернет.</span><span class="sxs-lookup"><span data-stu-id="979a9-275">Using AzCopy, you can easily upload the VHD over the Internet.</span></span> <span data-ttu-id="979a9-276">В зависимости от размера виртуальных жестких дисков это может занять определенное время.</span><span class="sxs-lookup"><span data-stu-id="979a9-276">Depending on the size of the VHDs, this may take time.</span></span> <span data-ttu-id="979a9-277">Не забывайте проверять ограничения для исходящих и входящих данных учетной записи хранения при использовании этого параметра.</span><span class="sxs-lookup"><span data-stu-id="979a9-277">Remember to check the storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="979a9-278">Дополнительные сведения см. в статье [Целевые показатели производительности и масштабируемости службы хранилища Azure](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="979a9-278">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="979a9-279">Загрузите и установите AzCopy по ссылке: [последняя версия AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="979a9-279">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="979a9-280">Откройте Azure PowerShell и перейдите в папку, где установлена AzCopy.</span><span class="sxs-lookup"><span data-stu-id="979a9-280">Open Azure PowerShell and go to the folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="979a9-281">Используйте следующую команду для копирования файла виртуального жесткого диска из "Источника" в "Место назначения".</span><span class="sxs-lookup"><span data-stu-id="979a9-281">Use the following command to copy the VHD file from "Source" to "Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="979a9-282">Пример:</span><span class="sxs-lookup"><span data-stu-id="979a9-282">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    <span data-ttu-id="979a9-283">Ниже приведено описание параметров, используемых в команде AzCopy.</span><span class="sxs-lookup"><span data-stu-id="979a9-283">Here are descriptions of the parameters used in the AzCopy command:</span></span>

   * <span data-ttu-id="979a9-284">**/Source: *&lt;source&gt;:*** месторасположение папки или URL-адрес контейнера с виртуальным жестким диском.</span><span class="sxs-lookup"><span data-stu-id="979a9-284">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span></span>
   * <span data-ttu-id="979a9-285">**/SourceKey: *&lt;source-account-key&gt;:*** ключ исходной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="979a9-285">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span></span>
   * <span data-ttu-id="979a9-286">**/Dest: *&lt;destination&gt;:*** URL-адрес контейнера хранилища для копирования виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="979a9-286">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span></span>
   * <span data-ttu-id="979a9-287">**/DestKey: *&lt;dest-account-key&gt;:*** ключ целевой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="979a9-287">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span></span>
   * <span data-ttu-id="979a9-288">**/Pattern: *&lt;file-name&gt;:*** указывает имя файла копируемого виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="979a9-288">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span></span>

<span data-ttu-id="979a9-289">Дополнительные сведения об использовании средства AzCopy см. в статье [Передача данных с помощью служебной программы командной строки AzCopy](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="979a9-289">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a><span data-ttu-id="979a9-290">Способ 2. Копирование VHD с помощью PowerShell (синхронное копирование)</span><span class="sxs-lookup"><span data-stu-id="979a9-290">Option 2: Copy a VHD with PowerShell (Synchronized copy)</span></span>
<span data-ttu-id="979a9-291">Вы также можете скопировать файл VHD с помощью командлета PowerShell Start-AzureStorageBlobCopy.</span><span class="sxs-lookup"><span data-stu-id="979a9-291">You can also copy the VHD file using the PowerShell cmdlet Start-AzureStorageBlobCopy.</span></span> <span data-ttu-id="979a9-292">Используйте следующую команду в Azure PowerShell, чтобы скопировать виртуальный жесткий диск: </span><span class="sxs-lookup"><span data-stu-id="979a9-292">Use the following command on Azure PowerShell to copy VHD.</span></span> <span data-ttu-id="979a9-293">Замените значения в угловых скобках <> соответствующими значениями из исходной и целевой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="979a9-293">Replace the values in <> with corresponding values from your source and destination storage account.</span></span> <span data-ttu-id="979a9-294">Чтобы использовать эту команду, в целевой учетной записи хранения должен быть контейнер с именем vhds.</span><span class="sxs-lookup"><span data-stu-id="979a9-294">To use this command, you must have a container called vhds in your destination storage account.</span></span> <span data-ttu-id="979a9-295">Если контейнер не существует, создайте его, прежде чем выполнять команду.</span><span class="sxs-lookup"><span data-stu-id="979a9-295">If the container doesn't exist, create one before running the command.</span></span>

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

<span data-ttu-id="979a9-296">Пример:</span><span class="sxs-lookup"><span data-stu-id="979a9-296">Example:</span></span>

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <span data-ttu-id="979a9-297"><a name="scenario2"></a>Сценарий 2. Перенос виртуальных машин в хранилище Azure класса Premium с других платформ</span><span class="sxs-lookup"><span data-stu-id="979a9-297"><a name="scenario2"></a>Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span></span>
<span data-ttu-id="979a9-298">При переносе виртуального жесткого диска из облачного хранилища, не относящегося к Azure, в хранилище Azure необходимо сначала экспортировать виртуальный жесткий диск в локальный каталог.</span><span class="sxs-lookup"><span data-stu-id="979a9-298">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span></span> <span data-ttu-id="979a9-299">Вручную скопируйте полный исходный путь к локальному каталогу, где хранится VHD, а затем передайте этот диск в службу хранилища Azure с помощью AzCopy.</span><span class="sxs-lookup"><span data-stu-id="979a9-299">Have the complete source path of the local directory where VHD is stored handy, and then using AzCopy to upload it to Azure Storage.</span></span>

#### <a name="step-1-export-vhd-to-a-local-directory"></a><span data-ttu-id="979a9-300">Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="979a9-300">Step 1.</span></span> <span data-ttu-id="979a9-301">Экспорт VHD в локальный каталог</span><span class="sxs-lookup"><span data-stu-id="979a9-301">Export VHD to a local directory</span></span>
##### <a name="copy-a-vhd-from-aws"></a><span data-ttu-id="979a9-302">Копирование VHD из AWS</span><span class="sxs-lookup"><span data-stu-id="979a9-302">Copy a VHD from AWS</span></span>
1. <span data-ttu-id="979a9-303">При использовании AWS экспортируйте экземпляр EC2 на виртуальный жесткий диск в сегмент Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="979a9-303">If you are using AWS, export the EC2 instance to a VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="979a9-304">Выполните действия, описанные в документации по Amazon в разделе об экспорте экземпляров Amazon EC2, чтобы установить интерфейс командной строки Amazon EC2, а также выполнить команду create-instance-export-task и экспортировать экземпляр EC2 в файл VHD.</span><span class="sxs-lookup"><span data-stu-id="979a9-304">Follow the steps described in the Amazon documentation for Exporting Amazon EC2 Instances to install the Amazon EC2 command-line interface (CLI) tool and run the create-instance-export-task command to export the EC2 instance to a VHD file.</span></span> <span data-ttu-id="979a9-305">При выполнении команды **create-instance-export-task** обязательно используйте **VHD** для переменной DISK&#95;IMAGE&#95;FORMAT.</span><span class="sxs-lookup"><span data-stu-id="979a9-305">Be sure to use **VHD** for the DISK&#95;IMAGE&#95;FORMAT variable when running the **create-instance-export-task** command.</span></span> <span data-ttu-id="979a9-306">Экспортированный файл виртуального жесткого диска сохраняется в сегменте Amazon S3, назначенном во время этого процесса.</span><span class="sxs-lookup"><span data-stu-id="979a9-306">The exported VHD file is saved in the Amazon S3 bucket you designate during that process.</span></span>

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. <span data-ttu-id="979a9-307">Загрузите VHD-файл из контейнеров S3.</span><span class="sxs-lookup"><span data-stu-id="979a9-307">Download the VHD file from the S3 bucket.</span></span> <span data-ttu-id="979a9-308">Выберите "Файл виртуального жесткого диска", а затем команду **Действия** > **Загрузка**.</span><span class="sxs-lookup"><span data-stu-id="979a9-308">Select the VHD file, then **Actions** > **Download**.</span></span>

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a><span data-ttu-id="979a9-309">Копирование VHD из облака (вне Azure)</span><span class="sxs-lookup"><span data-stu-id="979a9-309">Copy a VHD from other non-Azure cloud</span></span>
<span data-ttu-id="979a9-310">При переносе виртуального жесткого диска из облачного хранилища, не относящегося к Azure, в хранилище Azure необходимо сначала экспортировать виртуальный жесткий диск в локальный каталог.</span><span class="sxs-lookup"><span data-stu-id="979a9-310">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span></span> <span data-ttu-id="979a9-311">Скопируйте полный исходный путь к локальному каталогу, где хранится VHD.</span><span class="sxs-lookup"><span data-stu-id="979a9-311">Copy the complete source path of the local directory where VHD is stored.</span></span>

##### <a name="copy-a-vhd-from-on-premises"></a><span data-ttu-id="979a9-312">Копирование VHD из локальной среды</span><span class="sxs-lookup"><span data-stu-id="979a9-312">Copy a VHD from on-premises</span></span>
<span data-ttu-id="979a9-313">При переносе VHD из локальной среды необходимо ввести полный исходный путь его хранения.</span><span class="sxs-lookup"><span data-stu-id="979a9-313">If you are migrating VHD from an on-premises environment, you will need the complete source path where VHD is stored.</span></span> <span data-ttu-id="979a9-314">Это может быть адрес сервера или общей папки.</span><span class="sxs-lookup"><span data-stu-id="979a9-314">The source path could be a server location or file share.</span></span>

#### <a name="step-2-create-the-destination-for-your-vhd"></a><span data-ttu-id="979a9-315">Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="979a9-315">Step 2.</span></span> <span data-ttu-id="979a9-316">Создание целевого объекта для виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="979a9-316">Create the destination for your VHD</span></span>
<span data-ttu-id="979a9-317">Создайте учетную запись хранения для обслуживания виртуальных жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="979a9-317">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="979a9-318">При планировании места хранения VHD учитывайте следующие аспекты.</span><span class="sxs-lookup"><span data-stu-id="979a9-318">Consider the following points when planning where to store your VHDs:</span></span>

* <span data-ttu-id="979a9-319">Целевой учетной записью хранения может быть хранилище Standard или Premium в зависимости от требований приложения.</span><span class="sxs-lookup"><span data-stu-id="979a9-319">The target storage account could be standard or premium storage depending on your application requirement.</span></span>
* <span data-ttu-id="979a9-320">Регион учетной записи хранения должен совпадать с регионом виртуальных машин Azure хранилища класса Premium, которые будут созданы на последнем этапе.</span><span class="sxs-lookup"><span data-stu-id="979a9-320">The storage account region must be same as Premium Storage capable Azure VMs you will create in the final stage.</span></span> <span data-ttu-id="979a9-321">Можно скопировать в новую учетную запись хранения или запланировать использование прежней учетной записи в зависимости от требований.</span><span class="sxs-lookup"><span data-stu-id="979a9-321">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span></span>
* <span data-ttu-id="979a9-322">Скопируйте и сохраните ключ целевой учетной записи хранения для следующего этапа.</span><span class="sxs-lookup"><span data-stu-id="979a9-322">Copy and save the storage account key of the destination storage account for the next stage.</span></span>

<span data-ttu-id="979a9-323">Мы настоятельно рекомендуем перенести все данные рабочей нагрузки в хранилище класса Premium.</span><span class="sxs-lookup"><span data-stu-id="979a9-323">We strongly recommend you moving all data for production workload to use premium storage.</span></span>

#### <a name="step-3-upload-the-vhd-to-azure-storage"></a><span data-ttu-id="979a9-324">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="979a9-324">Step 3.</span></span> <span data-ttu-id="979a9-325">Загрузка VHD в службу хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="979a9-325">Upload the VHD to Azure Storage</span></span>
<span data-ttu-id="979a9-326">Теперь, когда VHD расположен в локальном каталоге, с помощью AzCopy или Azure PowerShell VHD-файл можно передать в службу хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="979a9-326">Now that you have your VHD in the local directory, you can use AzCopy or AzurePowerShell to upload the .vhd file to Azure Storage.</span></span> <span data-ttu-id="979a9-327">Это можно сделать двумя способами.</span><span class="sxs-lookup"><span data-stu-id="979a9-327">Both options are provided here:</span></span>

##### <a name="option-1-using-azure-powershell-add-azurevhd-to-upload-the-vhd-file"></a><span data-ttu-id="979a9-328">Способ 1. Передача VHD-файла с помощью командлета Azure PowerShell Add-AzureVhd</span><span class="sxs-lookup"><span data-stu-id="979a9-328">Option 1: Using Azure PowerShell Add-AzureVhd to upload the .vhd file</span></span>

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

<span data-ttu-id="979a9-329">Пример <Uri> может выглядеть следующим образом: ***https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd***.</span><span class="sxs-lookup"><span data-stu-id="979a9-329">An example <Uri> might be ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span></span> <span data-ttu-id="979a9-330">Пример <FileInfo>: ***C:\path\to\upload.vhd***.</span><span class="sxs-lookup"><span data-stu-id="979a9-330">An example <FileInfo> might be ***"C:\path\to\upload.vhd"***.</span></span>

##### <a name="option-2-using-azcopy-to-upload-the-vhd-file"></a><span data-ttu-id="979a9-331">Способ 2. Передача VHD-файла с помощью AzCopy</span><span class="sxs-lookup"><span data-stu-id="979a9-331">Option 2: Using AzCopy to upload the .vhd file</span></span>
<span data-ttu-id="979a9-332">Средство AzCopy позволяет легко передать VHD через Интернет.</span><span class="sxs-lookup"><span data-stu-id="979a9-332">Using AzCopy, you can easily upload the VHD over the Internet.</span></span> <span data-ttu-id="979a9-333">В зависимости от размера виртуальных жестких дисков это может занять определенное время.</span><span class="sxs-lookup"><span data-stu-id="979a9-333">Depending on the size of the VHDs, this may take time.</span></span> <span data-ttu-id="979a9-334">Не забывайте проверять ограничения для исходящих и входящих данных учетной записи хранения при использовании этого параметра.</span><span class="sxs-lookup"><span data-stu-id="979a9-334">Remember to check the storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="979a9-335">Дополнительные сведения см. в статье [Целевые показатели производительности и масштабируемости службы хранилища Azure](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="979a9-335">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="979a9-336">Загрузите и установите AzCopy по ссылке: [последняя версия AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="979a9-336">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="979a9-337">Откройте Azure PowerShell и перейдите в папку, где установлена AzCopy.</span><span class="sxs-lookup"><span data-stu-id="979a9-337">Open Azure PowerShell and go to the folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="979a9-338">Используйте следующую команду для копирования файла виртуального жесткого диска из "Источника" в "Место назначения".</span><span class="sxs-lookup"><span data-stu-id="979a9-338">Use the following command to copy the VHD file from "Source" to "Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="979a9-339">Пример:</span><span class="sxs-lookup"><span data-stu-id="979a9-339">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    <span data-ttu-id="979a9-340">Ниже приведено описание параметров, используемых в команде AzCopy.</span><span class="sxs-lookup"><span data-stu-id="979a9-340">Here are descriptions of the parameters used in the AzCopy command:</span></span>

   * <span data-ttu-id="979a9-341">**/Source: *&lt;source&gt;:*** месторасположение папки или URL-адрес контейнера с виртуальным жестким диском.</span><span class="sxs-lookup"><span data-stu-id="979a9-341">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span></span>
   * <span data-ttu-id="979a9-342">**/SourceKey: *&lt;source-account-key&gt;:*** ключ исходной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="979a9-342">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span></span>
   * <span data-ttu-id="979a9-343">**/Dest: *&lt;destination&gt;:*** URL-адрес контейнера хранилища для копирования виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="979a9-343">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span></span>
   * <span data-ttu-id="979a9-344">**/DestKey: *&lt;dest-account-key&gt;:*** ключ целевой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="979a9-344">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span></span>
   * <span data-ttu-id="979a9-345">**/BlobType: page:** указывает, что местом назначения является страничный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="979a9-345">**/BlobType: page:** Specifies that the destination is a page blob.</span></span>
   * <span data-ttu-id="979a9-346">**/Pattern: *&lt;file-name&gt;:*** указывает имя файла копируемого виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="979a9-346">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span></span>

<span data-ttu-id="979a9-347">Дополнительные сведения об использовании средства AzCopy см. в статье [Передача данных с помощью служебной программы командной строки AzCopy](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="979a9-347">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="979a9-348">Другие возможности загрузки виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="979a9-348">Other options for uploading a VHD</span></span>
<span data-ttu-id="979a9-349">Вы также можете загрузить виртуальный жесткий диск в учетную запись хранения с помощью одного из следующих средств.</span><span class="sxs-lookup"><span data-stu-id="979a9-349">You can also upload a VHD to your storage account using one of the following means:</span></span>

* [<span data-ttu-id="979a9-350">API копирования BLOB-объекта хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="979a9-350">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [<span data-ttu-id="979a9-351">Обозреватель хранилищ Azure для передачи больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="979a9-351">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
* [<span data-ttu-id="979a9-352">Справочник по API REST служб хранилища импорта и экспорта</span><span class="sxs-lookup"><span data-stu-id="979a9-352">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> <span data-ttu-id="979a9-353">Мы рекомендуем использовать службу импорта и экспорта, если предполагаемое время передачи больше 7 дней.</span><span class="sxs-lookup"><span data-stu-id="979a9-353">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="979a9-354">Чтобы оценить предполагаемое время передачи на основе размера данных и средства передачи, используйте компонент [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html).</span><span class="sxs-lookup"><span data-stu-id="979a9-354">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span></span>
>
> <span data-ttu-id="979a9-355">Импорт и экспорт можно использовать для копирования в учетную запись хранения класса Standard.</span><span class="sxs-lookup"><span data-stu-id="979a9-355">Import/Export can be used to copy to a standard storage account.</span></span> <span data-ttu-id="979a9-356">Необходимо осуществить копирование из учетной записи хранения Standard в учетную запись хранения Premium с помощью схожего с AzCopy средства.</span><span class="sxs-lookup"><span data-stu-id="979a9-356">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span></span>
>
>

## <span data-ttu-id="979a9-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Создание виртуальной машины Azure с использованием хранилища Premium</span><span class="sxs-lookup"><span data-stu-id="979a9-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Create Azure VMs using Premium Storage</span></span>
<span data-ttu-id="979a9-358">После загрузки или копирования VHD в необходимую учетную запись хранения следуйте инструкциям в этом разделе, чтобы зарегистрировать VHD в качестве образа ОС или диска ОС в зависимости от сценария, а затем создать на его основе экземпляр виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="979a9-358">After the VHD is uploaded or copied to the desired storage account, follow the instructions in this section to register the VHD as an OS image, or OS disk depending on your scenario and then create a VM instance from it.</span></span> <span data-ttu-id="979a9-359">Диск данных виртуального жесткого диска можно прикрепить к виртуальной машине после ее создания.</span><span class="sxs-lookup"><span data-stu-id="979a9-359">The data disk VHD can be attached to the VM once it is created.</span></span>
<span data-ttu-id="979a9-360">Пример скрипта переноса указан в конце этого раздела.</span><span class="sxs-lookup"><span data-stu-id="979a9-360">A sample migration script is provided at the end of this section.</span></span> <span data-ttu-id="979a9-361">Это простой скрипт, и он подходит не для всех сценариев.</span><span class="sxs-lookup"><span data-stu-id="979a9-361">This simple script does not match all scenarios.</span></span> <span data-ttu-id="979a9-362">Вам может понадобиться обновить скрипт в соответствии с ситуацией.</span><span class="sxs-lookup"><span data-stu-id="979a9-362">You may need to update the script to match with your specific scenario.</span></span> <span data-ttu-id="979a9-363">Сведения о том, применяется ли этот скрипт к вашему сценарию, см.в подразделе [Пример скрипта переноса](#a-sample-migration-script) ниже.</span><span class="sxs-lookup"><span data-stu-id="979a9-363">To see if this script applies to your scenario, see below [A Sample Migration Script](#a-sample-migration-script).</span></span>

### <a name="checklist"></a><span data-ttu-id="979a9-364">Контрольный список</span><span class="sxs-lookup"><span data-stu-id="979a9-364">Checklist</span></span>
1. <span data-ttu-id="979a9-365">Дождитесь завершения копирования VHD.</span><span class="sxs-lookup"><span data-stu-id="979a9-365">Wait until all the VHD disks copying is complete.</span></span>
2. <span data-ttu-id="979a9-366">Убедитесь, что хранилище класса Premium доступно в регионе, в который вы переносите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="979a9-366">Make sure Premium Storage is available in the region you are migrating to.</span></span>
3. <span data-ttu-id="979a9-367">Определите серию виртуальной машины, которую вы будете использовать.</span><span class="sxs-lookup"><span data-stu-id="979a9-367">Decide the new VM series you will be using.</span></span> <span data-ttu-id="979a9-368">Ею должна быть виртуальная машина, поддерживающая хранилище класса Premium, а ее размер зависит от доступности в регионе и потребностей.</span><span class="sxs-lookup"><span data-stu-id="979a9-368">It should be a Premium Storage capable, and the size should be depending on the availability in the region and based on your needs.</span></span>
4. <span data-ttu-id="979a9-369">Определите точный размер виртуальной машины, которую вы будете использовать.</span><span class="sxs-lookup"><span data-stu-id="979a9-369">Decide the exact VM size you will use.</span></span> <span data-ttu-id="979a9-370">Размер виртуальной машины должен быть достаточно большим, чтобы поддерживать количество дисков данных, которые вы используете.</span><span class="sxs-lookup"><span data-stu-id="979a9-370">VM size needs to be large enough to support the number of data disks you have.</span></span> <span data-ttu-id="979a9-371">Например: </span><span class="sxs-lookup"><span data-stu-id="979a9-371">E.g.</span></span> <span data-ttu-id="979a9-372">если вы используете 4 диска данных, виртуальная машина должна иметь минимум 2 ядра.</span><span class="sxs-lookup"><span data-stu-id="979a9-372">if you have 4 data disks, the VM must have 2 or more cores.</span></span> <span data-ttu-id="979a9-373">Кроме того, учитывайте требования к вычислительной мощности, памяти и пропускной способности сети.</span><span class="sxs-lookup"><span data-stu-id="979a9-373">Also, consider processing power, memory and network bandwidth needs.</span></span>
5. <span data-ttu-id="979a9-374">Создайте учетную запись хранения класса Premium в целевом регионе.</span><span class="sxs-lookup"><span data-stu-id="979a9-374">Create a Premium Storage account in the target region.</span></span> <span data-ttu-id="979a9-375">Эту учетную запись вы будете использовать для новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="979a9-375">This is the account you will use for the new VM.</span></span>
6. <span data-ttu-id="979a9-376">Держите сведения о текущей виртуальной машине под рукой, в том числе список дисков и соответствующих BLOB-объектов виртуальных жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="979a9-376">Have the current VM details handy, including the list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="979a9-377">Подготовьте приложение к простою.</span><span class="sxs-lookup"><span data-stu-id="979a9-377">Prepare your application for downtime.</span></span> <span data-ttu-id="979a9-378">Чтобы выполнить чистый перенос, необходимо остановить все процессы, выполняющиеся в текущей системе.</span><span class="sxs-lookup"><span data-stu-id="979a9-378">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="979a9-379">Только так вы получите стабильное состояние, которое можно перенести на новую платформу.</span><span class="sxs-lookup"><span data-stu-id="979a9-379">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="979a9-380">Длительность простоя будет зависеть от объема данных на дисках для переноса.</span><span class="sxs-lookup"><span data-stu-id="979a9-380">Downtime duration will depend on the amount of data in the disks to migrate.</span></span>

> [!NOTE]
> <span data-ttu-id="979a9-381">При создании виртуальной машины Azure Resource Manager на основе специализированного VHD, используйте [этот шаблон](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd), чтобы развернуть виртуальную машину с использованием имеющегося диска.</span><span class="sxs-lookup"><span data-stu-id="979a9-381">If you are creating an Azure Resource Manager VM from a specialized VHD Disk, please refer to [this template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) for deploying Resource Manager VM using existing disk.</span></span>
>
>

### <a name="register-your-vhd"></a><span data-ttu-id="979a9-382">Регистрация виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="979a9-382">Register your VHD</span></span>
<span data-ttu-id="979a9-383">Чтобы создать виртуальную машину на основе VHD операционной системы или присоединить диск данных к новой виртуальной машине, сначала их необходимо зарегистрировать.</span><span class="sxs-lookup"><span data-stu-id="979a9-383">To create a VM from OS VHD or to attach a data disk to a new VM, you must first register them.</span></span> <span data-ttu-id="979a9-384">Выполните приведенные ниже шаги в зависимости от сценария VHD.</span><span class="sxs-lookup"><span data-stu-id="979a9-384">Follow steps below depending on your VHD's scenario.</span></span>

#### <a name="generalized-operating-system-vhd-to-create-multiple-azure-vm-instances"></a><span data-ttu-id="979a9-385">Обобщенный виртуальный жесткий диск операционной системы для создания нескольких экземпляров виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="979a9-385">Generalized Operating System VHD to create multiple Azure VM instances</span></span>
<span data-ttu-id="979a9-386">После загрузки VHD обобщенного образа операционной системы в учетную запись хранения зарегистрируйте его в качестве **образа виртуальной машины Azure**, чтобы на его основе можно было создать один или несколько экземпляров виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="979a9-386">After generalized OS image VHD is uploaded to the storage account, register it as an **Azure VM Image** so that you can create one or more VM instances from it.</span></span> <span data-ttu-id="979a9-387">Используйте следующие командлеты PowerShell для регистрации вашего виртуального жесткого диска в качестве образа ОС виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="979a9-387">Use the following PowerShell cmdlets to register your VHD as an Azure VM OS image.</span></span> <span data-ttu-id="979a9-388">Укажите полный URL-адрес контейнера, в который был скопирован виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="979a9-388">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

<span data-ttu-id="979a9-389">Скопируйте и сохраните имя этого нового образа виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="979a9-389">Copy and save the name of this new Azure VM Image.</span></span> <span data-ttu-id="979a9-390">В приведенном выше примере это *OSImageName*.</span><span class="sxs-lookup"><span data-stu-id="979a9-390">In the example above, it is *OSImageName*.</span></span>

#### <a name="unique-operating-system-vhd-to-create-a-single-azure-vm-instance"></a><span data-ttu-id="979a9-391">Уникальный виртуальный жесткий диск операционной системы для создания одного экземпляра виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="979a9-391">Unique Operating System VHD to create a single Azure VM instance</span></span>
<span data-ttu-id="979a9-392">После загрузки уникального VHD операционной системы в учетную запись хранилища зарегистрируйте его как **диск ОС Azure**, чтобы на его основе можно было создать один или несколько экземпляров виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="979a9-392">After the unique OS VHD is uploaded to the storage account, register it as an **Azure OS Disk** so that you can create a VM instance from it.</span></span> <span data-ttu-id="979a9-393">Используйте эти командлеты PowerShell для регистрации вашего виртуального жесткого диска в качестве диска операционной системы Azure.</span><span class="sxs-lookup"><span data-stu-id="979a9-393">Use these PowerShell cmdlets to register your VHD as an Azure OS Disk.</span></span> <span data-ttu-id="979a9-394">Укажите полный URL-адрес контейнера, в который был скопирован виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="979a9-394">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

<span data-ttu-id="979a9-395">Скопируйте и сохраните имя этого нового образа операционной системы Azure.</span><span class="sxs-lookup"><span data-stu-id="979a9-395">Copy and save the name of this new Azure OS Disk.</span></span> <span data-ttu-id="979a9-396">В приведенном выше примере это *OSDisk*.</span><span class="sxs-lookup"><span data-stu-id="979a9-396">In the example above, it is *OSDisk*.</span></span>

#### <a name="data-disk-vhd-to-be-attached-to-new-azure-vm-instances"></a><span data-ttu-id="979a9-397">Присоединение VHD к новым экземплярам виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="979a9-397">Data disk VHD to be attached to new Azure VM instance(s)</span></span>
<span data-ttu-id="979a9-398">Загрузив виртуальный жесткий диск данных в учетную запись хранения, зарегистрируйте его как диск данных Azure. Это позволит вам присоединить его к новому экземпляру виртуальной машины Azure серии DS, DSv2 или GS.</span><span class="sxs-lookup"><span data-stu-id="979a9-398">After the data disk VHD is uploaded to storage account, register it as an Azure Data Disk so that it can be attached to your new DS Series, DSv2 series or GS Series Azure VM instance.</span></span>

<span data-ttu-id="979a9-399">Используйте эти командлеты PowerShell для регистрации вашего виртуального жесткого диска в качестве диска данных Azure.</span><span class="sxs-lookup"><span data-stu-id="979a9-399">Use these PowerShell cmdlets to register your VHD as an Azure Data Disk.</span></span> <span data-ttu-id="979a9-400">Укажите полный URL-адрес контейнера, в который был скопирован виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="979a9-400">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

<span data-ttu-id="979a9-401">Скопируйте и сохраните имя этого нового диска данных Azure.</span><span class="sxs-lookup"><span data-stu-id="979a9-401">Copy and save the name of this new Azure Data Disk.</span></span> <span data-ttu-id="979a9-402">В приведенном выше примере это *DataDisk*.</span><span class="sxs-lookup"><span data-stu-id="979a9-402">In the example above, it is *DataDisk*.</span></span>

### <a name="create-a-premium-storage-capable-vm"></a><span data-ttu-id="979a9-403">Создание виртуальной машины, поддерживающей хранилище класса Premium</span><span class="sxs-lookup"><span data-stu-id="979a9-403">Create a Premium Storage capable VM</span></span>
<span data-ttu-id="979a9-404">После регистрации образа ОС или диска ОС можно создать виртуальную машину серии DS, DSv2 или GS.</span><span class="sxs-lookup"><span data-stu-id="979a9-404">Once the OS image or OS disk are registered, create a new DS-series, DSv2-series or GS-series VM.</span></span> <span data-ttu-id="979a9-405">Будет использовано зарегистрированное имя образа или диска операционной системы.</span><span class="sxs-lookup"><span data-stu-id="979a9-405">You will be using the operating system image or operating system disk name that you registered.</span></span> <span data-ttu-id="979a9-406">Выберите тип виртуальной машины из уровня хранилища Premium.</span><span class="sxs-lookup"><span data-stu-id="979a9-406">Select the VM type from the Premium Storage tier.</span></span> <span data-ttu-id="979a9-407">В приведенном ниже примере мы используем размер виртуальной машины *Standard_DS2*.</span><span class="sxs-lookup"><span data-stu-id="979a9-407">In example below, we are using the *Standard_DS2* VM size.</span></span>

> [!NOTE]
> <span data-ttu-id="979a9-408">Обновите размер диска, чтобы обеспечить соответствие требованиям к емкости и производительности, а также доступным размерам Azure.</span><span class="sxs-lookup"><span data-stu-id="979a9-408">Update the disk size to make sure it matches your capacity and performance requirements and the available Azure disk sizes.</span></span>
>
>

<span data-ttu-id="979a9-409">Пошагово выполните нижеприведенные командлеты PowerShell для создания новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="979a9-409">Follow the step by step PowerShell cmdlets below to create the new VM.</span></span> <span data-ttu-id="979a9-410">Сначала задайте общие параметры.</span><span class="sxs-lookup"><span data-stu-id="979a9-410">First, set the common parameters:</span></span>

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

<span data-ttu-id="979a9-411">Сначала создайте облачную службу, в которой будут размещаться новые виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="979a9-411">First, create a cloud service in which you will be hosting your new VMs.</span></span>

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

<span data-ttu-id="979a9-412">Затем в зависимости от сценария создайте экземпляр виртуальной машины Azure из зарегистрированного образа или диска ОС.</span><span class="sxs-lookup"><span data-stu-id="979a9-412">Next, depending on your scenario, create the Azure VM instance from either the OS Image or OS Disk that you registered.</span></span>

#### <a name="generalized-operating-system-vhd-to-create-multiple-azure-vm-instances"></a><span data-ttu-id="979a9-413">Обобщенный виртуальный жесткий диск операционной системы для создания нескольких экземпляров виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="979a9-413">Generalized Operating System VHD to create multiple Azure VM instances</span></span>
<span data-ttu-id="979a9-414">Создайте один или несколько экземпляров виртуальной машины Azure серии DS с помощью зарегистрированного **образа ОС Azure** .</span><span class="sxs-lookup"><span data-stu-id="979a9-414">Create the one or more new DS Series Azure VM instances using the **Azure OS Image** that you registered.</span></span> <span data-ttu-id="979a9-415">Укажите имя этого образа ОС в конфигурации виртуальной машины при создании новой виртуальной машины, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="979a9-415">Specify this OS Image name in the VM configuration when creating new VM as shown below.</span></span>

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-to-create-a-single-azure-vm-instance"></a><span data-ttu-id="979a9-416">Уникальный виртуальный жесткий диск операционной системы для создания одного экземпляра виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="979a9-416">Unique Operating System VHD to create a single Azure VM instance</span></span>
<span data-ttu-id="979a9-417">Создайте новый экземпляр виртуальной машины Azure серии DS с помощью зарегистрированного **диска ОС Azure** .</span><span class="sxs-lookup"><span data-stu-id="979a9-417">Create a new DS series Azure VM instance using the **Azure OS Disk** that you registered.</span></span> <span data-ttu-id="979a9-418">Укажите имя этого диска ОС в конфигурации виртуальной машины при создании новой виртуальной машины, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="979a9-418">Specify this OS Disk name in the VM configuration when creating the new VM as shown below.</span></span>

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

<span data-ttu-id="979a9-419">Укажите другие сведения о виртуальной машине Azure, например: облачную службу, регион, учетную запись хранения, группу доступности и политику кэширования.</span><span class="sxs-lookup"><span data-stu-id="979a9-419">Specify other Azure VM information, such as a cloud service, region, storage account, availability set, and caching policy.</span></span> <span data-ttu-id="979a9-420">Обратите внимание, что экземпляр виртуальной машины должен быть связан с операционной системой или дисками данных. Следовательно, выбранная облачная служба, регион и учетная запись хранения должны находиться в том же расположении, что и базовые VHD этих дисков.</span><span class="sxs-lookup"><span data-stu-id="979a9-420">Note that the VM instance must be co-located with associated operating system or data disks, so the selected cloud service, region and storage account must all be in the same location as the underlying VHDs of those disks.</span></span>

### <a name="attach-data-disk"></a><span data-ttu-id="979a9-421">Присоединение диска данных</span><span class="sxs-lookup"><span data-stu-id="979a9-421">Attach data disk</span></span>
<span data-ttu-id="979a9-422">Наконец, зарегистрировав VHD в качестве дисков данных, присоедините их к новой виртуальной машине Azure, поддерживающей хранилище класса Premium.</span><span class="sxs-lookup"><span data-stu-id="979a9-422">Lastly, if you have registered data disk VHDs, attach them to the new Premium Storage capable Azure VM.</span></span>

<span data-ttu-id="979a9-423">Используйте следующий командлет PowerShell, чтобы присоединить диск данных к новой виртуальной машине и указать политику кэширования.</span><span class="sxs-lookup"><span data-stu-id="979a9-423">Use following PowerShell cmdlet to attach data disk to the new VM and specify the caching policy.</span></span> <span data-ttu-id="979a9-424">В примере ниже для политики кэширования установлено значение *ReadOnly*.</span><span class="sxs-lookup"><span data-stu-id="979a9-424">In example below the caching policy is set to *ReadOnly*.</span></span>

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> <span data-ttu-id="979a9-425">Чтобы обеспечить поддержку приложений, может потребоваться выполнить дополнительные шаги, не описанные в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="979a9-425">There may be additional steps necessary to support your application that is not be covered by this guide.</span></span>
>
>

### <a name="checking-and-plan-backup"></a><span data-ttu-id="979a9-426">Проверка и планирование резервного копирования</span><span class="sxs-lookup"><span data-stu-id="979a9-426">Checking and plan backup</span></span>
<span data-ttu-id="979a9-427">После запуска новой виртуальной машины войдите на нее, используя идентификатор входа и пароль исходной виртуальной машины, и убедитесь, что все работает правильно.</span><span class="sxs-lookup"><span data-stu-id="979a9-427">Once the new VM is up and running, access it using the same login id and password is as the original VM, and verify that everything is working as expected.</span></span> <span data-ttu-id="979a9-428">Все настройки, в том числе чередующиеся тома, будут присутствовать в новой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="979a9-428">All the settings, including the striped volumes, would be present in the new VM.</span></span>

<span data-ttu-id="979a9-429">Последний шаг заключается в планировании резервного копирования и расписания обслуживания для новой виртуальной машины в соответствии с требованиями приложения.</span><span class="sxs-lookup"><span data-stu-id="979a9-429">The last step is to plan backup and maintenance schedule for the new VM based on the application's needs.</span></span>

### <span data-ttu-id="979a9-430"><a name="a-sample-migration-script"></a>Пример скрипта переноса</span><span class="sxs-lookup"><span data-stu-id="979a9-430"><a name="a-sample-migration-script"></a>A sample migration script</span></span>
<span data-ttu-id="979a9-431">Автоматизировать перенос нескольких виртуальных машин можно с помощью сценариев PowerShell.</span><span class="sxs-lookup"><span data-stu-id="979a9-431">If you have multiple VMs to migrate, automation through PowerShell scripts will be helpful.</span></span> <span data-ttu-id="979a9-432">Ниже приведен пример сценария, который автоматизирует процесс переноса виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="979a9-432">Following is a sample script that automates the migration of a VM.</span></span> <span data-ttu-id="979a9-433">Обратите внимание, что этот скрипт приведен в качестве примера, что предполагает некоторые допущения в отношении дисков текущей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="979a9-433">Note that below script is only an example, and there are few assumptions made about the current VM disks.</span></span> <span data-ttu-id="979a9-434">Вам может понадобиться обновить скрипт в соответствии с ситуацией.</span><span class="sxs-lookup"><span data-stu-id="979a9-434">You may need to update the script to match with your specific scenario.</span></span>

<span data-ttu-id="979a9-435">Допускается следующее:</span><span class="sxs-lookup"><span data-stu-id="979a9-435">The assumptions are:</span></span>

* <span data-ttu-id="979a9-436">Вы создаете классическую виртуальную машину Azure.</span><span class="sxs-lookup"><span data-stu-id="979a9-436">You are creating classic Azure VMs.</span></span>
* <span data-ttu-id="979a9-437">Исходные диски операционной системы и диски данных находятся в одной учетной записи хранения и одном контейнере.</span><span class="sxs-lookup"><span data-stu-id="979a9-437">Your source OS Disks and source Data Disks are in same storage account and same container.</span></span> <span data-ttu-id="979a9-438">Если они находятся в разных местах, используйте AzCopy или Azure PowerShell, чтобы скопировать VHD.</span><span class="sxs-lookup"><span data-stu-id="979a9-438">If your OS Disks and Data Disks are not in the same place, you can use AzCopy or Azure PowerShell to copy VHDs over storage accounts and containers.</span></span> <span data-ttu-id="979a9-439">Вернитесь к предыдущему шагу: [Копирование VHD с помощью AzCopy или PowerShell](#copy-vhd-with-azcopy-or-powershell).</span><span class="sxs-lookup"><span data-stu-id="979a9-439">Refer to the previous step: [Copy VHD with AzCopy or PowerShell](#copy-vhd-with-azcopy-or-powershell).</span></span> <span data-ttu-id="979a9-440">Скрипт также можно изменить согласно своему сценарию, но мы рекомендуем использовать AzCopy или PowerShell, так как этот способ более удобный и быстрый.</span><span class="sxs-lookup"><span data-stu-id="979a9-440">Editing this script to meet your scenario is another choice, but we recommend using AzCopy or PowerShell since it is easier and faster.</span></span>

<span data-ttu-id="979a9-441">Скрипт автоматизации приводится ниже.</span><span class="sxs-lookup"><span data-stu-id="979a9-441">The automation script is provided below.</span></span> <span data-ttu-id="979a9-442">Замените текст своими сведениями, и обновите скрипт так, чтобы он соответствовал конкретному сценарию.</span><span class="sxs-lookup"><span data-stu-id="979a9-442">Replace text with your information and update the script to match with your specific scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="979a9-443">Имеющийся сценарий не сохраняет конфигурацию сети исходной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="979a9-443">Using the existing script does not preserve the network configuration of your source VM.</span></span> <span data-ttu-id="979a9-444">После переноса виртуальных машин параметры сети необходимо переопределить.</span><span class="sxs-lookup"><span data-stu-id="979a9-444">You will need to re-config the networking settings on your migrated VMs.</span></span>
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE to show how to migrate a VM from a standard storage account to a premium storage account. You can customize it according to your specific requirements.

    .Description
    The script will copy the vhds (page blobs) of the source VM to the new storage account.
    And then it will create a new VM from these copied vhds based on the inputs that you specified for the new VM.
    You can modify the script to satisfy your specific requirement, but please be aware of the items specified
    in the Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. THE ENTIRE RISK OF USE, INABILITY TO USE, OR
    RESULTS FROM THE USE OF THIS CODE REMAINS WITH THE USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    To find more information about how to set up Azure PowerShell, refer to the following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # the cloud service name of the VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # The VM name to copy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # The destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # The destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # the destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # the destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # the location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not to copy the os disk, the default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently to report the copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # the name suffix to add to new created disks to avoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import the Azure PowerShell module
    Write-Host "`n[WORKITEM] - Importing Azure PowerShell module" -ForegroundColor Yellow
    $azureModule = Import-Module Azure -PassThru

    if ($azureModule -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    else
    {
        #show module not found interaction and bail out
        Write-Host "[ERROR] - PowerShell module not found. Exiting." -ForegroundColor Red
        Exit
    }


    #Check the Azure PowerShell module version
    Write-Host "`n[WORKITEM] - Checking Azure PowerShell module verion" -ForegroundColor Yellow
    If ($azureModule.Version -ge (New-Object System.Version -ArgumentList "0.8.14"))
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    Else
    {
        Write-Host "[ERROR] - Azure PowerShell module must be version 0.8.14 or higher. Exiting." -ForegroundColor Red
        Exit
    }

    #Check if there is an azure subscription set up in PowerShell
    Write-Host "`n[WORKITEM] - Checking Azure Subscription" -ForegroundColor Yellow
    $currentSubs = Get-AzureSubscription -Current
    if ($currentSubs -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
        Write-Host "`tYour current azure subscription in PowerShell is $($currentSubs.SubscriptionName)." -ForegroundColor Green
    }
    else
    {
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer to this article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ to connect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if the VM is shut down
    #  Stopping the VM is a required step so that the file system is consistent when you do the copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - The source VM doesn't exist in the current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping the VM is a required step so that the file system is consistent when you do the copy operation. Azure does not support live migration at this time. If you'd like to create a VM from a generalized image, sys-prep the Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish to stop $SourceVMName now? Input 'N' if you want to shut down the VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until the VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName to shut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting the sourve vm to a configuration file, you can restore the original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration to $vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy the vhds of the source vm
    #  You can choose to copy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly to be $false. The default is to copy only data disk vhds
    #  and the new VM will boot from the original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering the data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in the destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need to copy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting the source VM so that dest VM can boot
        # from the same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose to copy data disks only. Moving VM requires removing the original VM (the disks and backing vhd files will NOT be deleted) so that the new VM can boot from the same vhd. This is an irreversible action. Do you wish to proceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing the original VM (the vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill the OS disk is released by source VM. This may take up to several minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy the os disk vhd
        Write-Host "`n[WORKITEM] - Starting copying os disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $allDisksToCopy += @($sourceOSDisk)
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $sourceOSVHD -DestContainer vhds -DestBlob $sourceOSVHD -Context $sourceContext -DestContext $destContext -Force
        $destOSVHD = $targetBlob
    }


    # Copy all data disk vhds
    # Start all async copy requests in parallel.
    foreach($disk in $sourceDataDisks)
    {
        $blobName = $disk.MediaLink.Segments[2]
        # copy all data disks
        Write-Host "`n[WORKITEM] - Starting copying data disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $blobName -DestContainer vhds -DestBlob $blobName -Context $sourceContext -DestContext $destContext -Force
        # update the media link to point to the target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy to complete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
        # check status every 30 seconds
        Sleep -Seconds $CopyStatusReportInterval
        foreach ( $disk in $allDisksToCopy)
        {
            if ($diskComplete -contains $disk)
            {
                Continue
            }
            $blobName = $disk.MediaLink.Segments[2]
            $copyState = Get-AzureStorageBlobCopyState -Blob $blobName -Container vhds -Context $destContext
            if ($copyState.Status -eq "Success")
            {
                Write-Host "`n[Status] - Success for disk copy $($disk.DiskName) at $($copyState.CompletionTime)" -ForegroundColor Green
                $diskComplete += $disk
            }
            else
            {
                if ($copyState.TotalBytes -gt 0)
                {
                    $percent = ($copyState.BytesCopied / $copyState.TotalBytes) * 100
                    Write-Host "`n[Status] - $('{0:N2}' -f $percent)% Complete for disk copy $($disk.DiskName)" -ForegroundColor Green
                }
            }
        }
    }
    while($diskComplete.Count -lt $allDisksToCopy.Count)

    #######################################################################
    #  Create a new vm
    #  the new VM can be created from the copied disks or the original os disk.
    #  You can ddd your own logic here to satisfy your specific requirements of the vm.
    #######################################################################

    # Create a VM from the existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached the copied data disks to the new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of the source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want to add more custimization to the new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <span data-ttu-id="979a9-445"><a name="optimization"></a>Оптимизация</span><span class="sxs-lookup"><span data-stu-id="979a9-445"><a name="optimization"></a>Optimization</span></span>
<span data-ttu-id="979a9-446">Конфигурацию текущей виртуальной машины можно настроить для правильной работы с дисками хранилища класса Standard.</span><span class="sxs-lookup"><span data-stu-id="979a9-446">Your current VM configuration may be customized specifically to work well with Standard disks.</span></span> <span data-ttu-id="979a9-447">Например, можно повысить производительность, используя несколько дисков в чередующемся томе.</span><span class="sxs-lookup"><span data-stu-id="979a9-447">For instance, to increase the performance by using many disks in a striped volume.</span></span> <span data-ttu-id="979a9-448">Например, вместо 4 отдельных дисков в хранилище класса Premium можно использовать один диск, чтобы сократить затраты.</span><span class="sxs-lookup"><span data-stu-id="979a9-448">For example, instead of using 4 disks separately on Premium Storage, you may be able to optimize the cost by having a single disk.</span></span> <span data-ttu-id="979a9-449">Такие способы оптимизации необходимо применять в индивидуальном порядке. Кроме того, после переноса они требуют выполнения дополнительных действий.</span><span class="sxs-lookup"><span data-stu-id="979a9-449">Optimizations like this need to be handled on a case by case basis and require custom steps after the migration.</span></span> <span data-ttu-id="979a9-450">Обратите внимание, что такая оптимизация может быть полезной для баз данных и приложений, которые зависят от разметки диска, определенной во время установки.</span><span class="sxs-lookup"><span data-stu-id="979a9-450">Also, note that this process may not well work for databases and applications that depend on the disk layout defined in the setup.</span></span>

##### <a name="preparation"></a><span data-ttu-id="979a9-451">Подготовка</span><span class="sxs-lookup"><span data-stu-id="979a9-451">Preparation</span></span>
1. <span data-ttu-id="979a9-452">Выполните простой перенос, как описано в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="979a9-452">Complete the Simple Migration as described in the earlier section.</span></span> <span data-ttu-id="979a9-453">Оптимизация будет выполняться на новой виртуальной машине после переноса.</span><span class="sxs-lookup"><span data-stu-id="979a9-453">Optimizations will be performed on the new VM after the migration.</span></span>
2. <span data-ttu-id="979a9-454">Для создания оптимальной конфигурации необходимо определить размеры новых дисков.</span><span class="sxs-lookup"><span data-stu-id="979a9-454">Define the new disk sizes needed for the optimized configuration.</span></span>
3. <span data-ttu-id="979a9-455">Определите сопоставление текущих дисков и томов со спецификациям нового диска.</span><span class="sxs-lookup"><span data-stu-id="979a9-455">Determine mapping of the current disks/volumes to the new disk specifications.</span></span>

##### <a name="execution-steps"></a><span data-ttu-id="979a9-456">Шаги выполнения</span><span class="sxs-lookup"><span data-stu-id="979a9-456">Execution steps</span></span>
1. <span data-ttu-id="979a9-457">Создайте новые диски нужного размера на виртуальной машине хранилища класса Premium.</span><span class="sxs-lookup"><span data-stu-id="979a9-457">Create the new disks with the right sizes on the Premium Storage VM.</span></span>
2. <span data-ttu-id="979a9-458">Войдите на виртуальную машину и скопируйте данные из текущего тома на новый диск, который сопоставлен с этим томом.</span><span class="sxs-lookup"><span data-stu-id="979a9-458">Login to the VM and copy the data from the current volume to the new disk that maps to that volume.</span></span> <span data-ttu-id="979a9-459">Сделайте это для всех текущих томов, которые необходимо сопоставить с новым диском.</span><span class="sxs-lookup"><span data-stu-id="979a9-459">Do this for all the current volumes that need to map to a new disk.</span></span>
3. <span data-ttu-id="979a9-460">Затем измените параметры приложения, чтобы переключиться на новые диски, и отключите старые тома.</span><span class="sxs-lookup"><span data-stu-id="979a9-460">Next, change the application settings to switch to the new disks, and detach the old volumes.</span></span>

<span data-ttu-id="979a9-461">Дополнительные сведения об оптимизации приложений для повышения производительности дисков см. в разделе [Оптимизация производительности приложения](storage-premium-storage-performance.md#optimizing-application-performance).</span><span class="sxs-lookup"><span data-stu-id="979a9-461">For tuning the application for better disk performance, please refer to [Optimizing Application Performance](storage-premium-storage-performance.md#optimizing-application-performance).</span></span>

### <a name="application-migrations"></a><span data-ttu-id="979a9-462">Перенос приложений</span><span class="sxs-lookup"><span data-stu-id="979a9-462">Application migrations</span></span>
<span data-ttu-id="979a9-463">Перенос баз данных и других сложных приложений может потребовать выполнения специальных действий, которые определяет поставщик приложений.</span><span class="sxs-lookup"><span data-stu-id="979a9-463">Databases and other complex applications may require special steps as defined by the application provider for the migration.</span></span> <span data-ttu-id="979a9-464">См. документацию по соответствующему приложению.</span><span class="sxs-lookup"><span data-stu-id="979a9-464">Please refer to respective application documentation.</span></span> <span data-ttu-id="979a9-465">Например: </span><span class="sxs-lookup"><span data-stu-id="979a9-465">E.g.</span></span> <span data-ttu-id="979a9-466">обычно базы данных можно переносить путем резервного копирования и восстановления.</span><span class="sxs-lookup"><span data-stu-id="979a9-466">typically databases can be migrated through backup and restore.</span></span>

## <a name="next-steps"></a><span data-ttu-id="979a9-467">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="979a9-467">Next steps</span></span>
<span data-ttu-id="979a9-468">Ознакомьтесь со следующими ресурсами для конкретных сценариев переноса виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="979a9-468">See the following resources for specific scenarios for migrating virtual machines:</span></span>

* [<span data-ttu-id="979a9-469">Перенос виртуальных машин Azure между учетными записями хранения.</span><span class="sxs-lookup"><span data-stu-id="979a9-469">Migrate Azure Virtual Machines between Storage Accounts</span></span>](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [<span data-ttu-id="979a9-470">Создание и загрузка виртуального жесткого диска Windows Server в Azure.</span><span class="sxs-lookup"><span data-stu-id="979a9-470">Create and upload a Windows Server VHD to Azure.</span></span>](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="979a9-471">Создание и загрузка виртуального жесткого диска, содержащего операционную систему Linux.</span><span class="sxs-lookup"><span data-stu-id="979a9-471">Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System</span></span>](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="979a9-472">Перенос виртуальных машин из Amazon AWS в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="979a9-472">Migrating Virtual Machines from Amazon AWS to Microsoft Azure</span></span>](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

<span data-ttu-id="979a9-473">Дополнительные сведения о службе хранилища Azure и виртуальных машинах Azure см. также в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="979a9-473">Also, see the following resources to learn more about Azure Storage and Azure Virtual Machines:</span></span>

* [<span data-ttu-id="979a9-474">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="979a9-474">Azure Storage</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="979a9-475">Виртуальные машины Azure</span><span class="sxs-lookup"><span data-stu-id="979a9-475">Azure Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="979a9-476">Хранилище Premium: высокопроизводительное хранилище для рабочих нагрузок виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="979a9-476">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
